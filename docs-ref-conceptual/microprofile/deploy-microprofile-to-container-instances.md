---
title: Docker 및 Azure를 사용하여 클라우드로 MicroProfile 앱 배포
description: Docker 및 Azure Container 인스턴스를 사용하여 클라우드로 MicroProfile 앱을 배포하는 방법에 대해 알아봅니다.
services: container-instances;container-registry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 6ba12bb183969103676fa988199603df6cf36bba
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533608"
---
# <a name="deploy-a-microprofile-app-to-the-cloud-by-using-docker-and-azure"></a>Docker 및 Azure를 사용하여 클라우드로 MicroProfile 앱 배포

이 문서에서는 [MicroProfile.io] 애플리케이션을 Docker 컨테이너에 압축하고 Azure 컨테이너 인스턴스에서 실행하는 방법을 설명합니다.

> [!NOTE]
> Docker 컨테이너 이미지가 자체 실행 가능(즉, 이미지가 런타임을 포함)한 경우, 이 절차는 MicroProfile.io의 모든 구현을 사용하여 실행됩니다.

## <a name="prerequisites"></a>필수 조건

이 자습서를 완료하려면 다음 필수 구성 요소가 필요합니다.

* Azure 구독. Azure 구독이 아직 없는 경우 [체험판 Azure 계정]에서 무료 평가판에 등록할 수 있습니다.
* [Azure CLI]가 설치되어 있음
* 지원되는 JDK(Java Development Kit) Azure에서 개발하는 데 사용할 수 있는 JDK에 대한 자세한 내용은 [Azure 및 Azure Stack에 대한 Java 장기 지원](https://aka.ms/azure-jdks)을 참조합니다.
* [Apache Maven] 빌드 도구(버전 3 이상).
* [Git] 클라이언트

## <a name="microprofile-hello-azure-sample"></a>MicroProfile Hello Azure 예제

이 문서에서는 [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) 예제를 사용합니다. 다음 명령을 사용하여 복제, 빌드 및 로컬로 실행합니다.

```bash
$ git clone https://github.com/Azure-Samples/microprofile-hello-azure.git
$ mvn clean package
...
[INFO] BUILD SUCCESS
...
$ mvn payara-micro:start
...
[2018-07-30T13:34:51.553-0700] [] [INFO] [] [PayaraMicro] [tid: _ThreadID=1 _ThreadName=main] [timeMillis: 1532982891553] [levelValue: 800] Payara Micro  5.182 #badassmicrofish (build 303) ready in 10,304 (ms)
...
```

`curl`을 호출하거나 [브라우저](http://localhost:8080/api/hello)를 사용하여 애플리케이션을 테스트할 수 있습니다.

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-the-app-to-azure"></a>Azure에 앱 배포

이제 [Azure Container Instances] 및 [Azure Container Registry] 서비스를 사용하여 Azure에 이 애플리케이션을 배포해 보겠습니다.

### <a name="build-a-docker-image"></a>Docker 이미지 빌드

예제 프로젝트는 사용할 수 있는 Dockerfile을 제공하고 있습니다. Azure Container Registry 빌드 기능을 사용하여 클라우드에서 이미지를 빌드하므로 Docker가 설치되어 있지 않아도 됩니다.

이미지를 빌드하고 Azure에서 실행하도록 준비하려면 다음을 수행합니다.

1. Azure CLI를 설치하고 로그인합니다.
1. Azure 리소스 그룹 만들기
1. Azure 컨테이너 레지스트리 인스턴스를 만듭니다.
1. Docker 이미지를 빌드합니다.
1. 이전에 만든 컨테이너 레지스트리 인스턴스에 Docker 이미지를 게시합니다.
1. (선택 사항) 하나의 명령으로 컨테이너 레지스트리 인스턴스에 이미지를 빌드 및 게시합니다.


#### <a name="set-up-the-azure-cli"></a>Azure CLI 설치

Azure 구독, [Azure CLI ](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) 설치 완료, 계정 인증을 확인합니다.

```bash
az login
```

#### <a name="create-a-resource-group"></a>리소스 그룹 만들기

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-a-container-registry-instance"></a>컨테이너 레지스트리 인스턴스 만들기

이 명령은 기본 이름에 임의의 숫자를 사용하여 전역적으로 유일한 컨테이너 레지스트리 인스턴스를 작성합니다.

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a>Docker 이미지 빌드

Docker 자체를 사용하여 Docker 이미지를 로컬에서 쉽게 만들 수 있지만 몇 가지 이유로 인해 Docker를 클라우드에서 빌드하는 것이 좋습니다.

* Docker를 로컬로 설치할 필요가 없습니다.
* 빌드가 다른 곳에서 발생하기 때문에 훨씬 빠릅니다(컨텍스트 업로드 시간 제외).
* 클라우드의 프로세스는 인터넷에 보다 빠르게 액세스하므로 빠른 다운로드가 가능합니다.
* 이미지가 컨테이너 레지스트리 인스턴스로 직접 이동합니다.

이러한 이유 때문에 [Azure Container Registry 빌드] 기능을 사용하여 이미지를 빌드합니다.

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-the-docker-image-from-the-azure-container-registry-instance-to-container-instances"></a>Azure 컨테이너 레지스트리 인스턴스에서 Container Instances로 Docker 이미지를 배포합니다.

이제 이미지를 컨테이너 레지스트리 인스턴스에 사용할 수 있으므로 Container Instances에서 컨테이너 인스턴스를 인스턴스화합니다. 하지만 먼저 컨테이너 레지스트리 인스턴스에 인증할 수 있는지 확인합니다.

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a>배포된 MicroProfile 애플리케이션 테스트

이제 애플리케이션이 실행됩니다. 명령줄 인터페이스에서 테스트하려면 다음 명령을 실행합니다.

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

축하합니다! Microsoft Azure에 Docker 컨테이너로 MicroProfile 애플리케이션을 성공적으로 구축하고 배포했습니다.

## <a name="next-steps"></a>다음 단계

이 문서에서 설명하는 다양한 기술에 대한 자세한 내용은 다음을 참조하세요.

* [Azure CLI에서 Azure에 로그인](/azure/xplat-cli-connect)

<!-- URL List -->

[Azure Container Registry 빌드]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Azure CLI]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Apache Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry
