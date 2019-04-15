---
title: Azure Kubernetes Service에서 Kubernetes에 Spring Boot 앱 배포
description: 이 자습서에서는 Microsoft Azure에서 Kubernetes 클러스터에 Spring Boot 애플리케이션을 배포하는 단계를 안내합니다.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: 42bb030a916cc5aaf1e20242518a0a400b8baa88
ms.sourcegitcommit: 3b10fe30dcc83e4c2e4c94d5b55e37ddbaa23c7a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59071012"
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-kubernetes-service"></a>Azure Kubernetes Service의 Kubernetes 클러스터에 Spring Boot 애플리케이션 배포

**[Kubernetes]** 및 **[Docker]** 는 개발자가 컨테이너에서 실행 중인 애플리케이션의 배포, 확장 및 관리를 자동화하는 데 도움이 되는 오픈 소스 솔루션입니다.

이 자습서에서는 이러한 두 가지 인기 있는 오픈 소스 기술을 결합하여 Spring Boot 애플리케이션을 개발하고 Microsoft Azure에 배포하는 과정을 안내합니다. 좀 더 구체적으로 말하면 애플리케이션 개발을 위해 *[Spring Boot]*, 컨테이너 배포를 위해 *[Kubernetes]* 및 애플리케이션을 호스트하기 위해 [AKS(Azure Kubernetes Service)]를 사용합니다.

### <a name="prerequisites"></a>필수 조건

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.
* [Azure CLI(명령줄 인터페이스)]
* 지원되는 JDK(Java Development Kit) Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.
* Apache의 [Maven] 빌드 도구(버전 3)
* [Git] 클라이언트
* [Docker] 클라이언트

> [!NOTE]
>
> 이 자습서의 가상화 요구 사항으로 인해 가상 머신에는 이 문서의 단계를 따를 수 없습니다. 따라서 가상화 기능이 사용하도록 설정된 물리적 컴퓨터를 사용해야 합니다.
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a>Spring Boot on Docker 시작 웹앱 만들기

다음 단계에서는 Spring Boot 웹 애플리케이션을 빌드하고 로컬로 테스트하는 과정을 안내합니다.

1. 명령 프롬프트를 열고 애플리케이션을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예를 들면 다음과 같습니다.
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- 또는 --
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. [Spring Boot on Docker 시작] 샘플 프로젝트를 디렉터리에 복제합니다.
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. 디렉터리를 완료된 프로젝트로 변경합니다.
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. Maven을 사용하여 샘플 앱을 빌드하고 실행합니다.
   ```
   mvn package spring-boot:run
   ```

1. `http://localhost:8080`으로 이동하거나 `curl` 명령을 사용하여 웹앱을 테스트합니다.
   ```
   curl http://localhost:8080
   ```

1. 다음 메시지가 표시되어야 합니다. **Hello Docker World**

   ![로컬로 샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a>Azure CLI를 사용하여 Azure Container Registry 만들기

1. 명령 프롬프트를 엽니다.

1. Azure 계정에 로그인합니다.
   ```azurecli
   az login
   ```

1. Azure 구독을 선택합니다.
   ```azurecli
   az account set -s <YourSubscriptionID>
   ```

1. 이 자습서에서 사용되는 Azure 리소스에 대한 리소스 그룹을 만듭니다.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. 리소스 그룹에서 개인 Azure Container Registry를 만듭니다. 이 자습서는 이후 단계에서 샘플 앱을 이 레지스트리에 Docker 이미지로 푸시합니다. `wingtiptoysregistry`를 레지스트리의 고유한 이름으로 바꿉니다.
   ```azurecli
   az acr create --resource-group wingtiptoys-kubernetes --location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry-via-jib"></a>Jib을 통해 컨테이너 레지스트리에 앱 푸시

1. Azure CLI에서 Azure Container Registry에 로그인합니다.
   ```azurecli
   # set the default name for Azure Container Registry, otherwise you will need to specify the name in "az acr login"
   az configure --defaults acr=wingtiptoysregistry
   az acr login
   ```

1. Spring Boot 애플리케이션에 대해 완료된 프로젝트 디렉터리로 이동하고(예: "*C:\SpringBoot\gs-spring-boot-docker\complete*"또는"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") 텍스트 편집기를 사용하여 *pom.xml* 파일을 엽니다.

1. *pom.xml* 파일의 `<properties>` 컬렉션을 Azure Container Registry의 레지스트리 이름과 최신 버전의 [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin)으로 업데이트합니다.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <jib-maven-plugin.version>1.0.2</jib-maven-plugin.version>
      <java.version>1.8</java.version>
   </properties>
   ```

1. `<plugin>`에 `jib-maven-plugin`이 포함되도록 *pom.xml* 파일에서 `<plugins>` 컬렉션을 업데이트합니다.

   ```xml
   <plugin>
     <artifactId>jib-maven-plugin</artifactId>
     <groupId>com.google.cloud.tools</groupId>
     <version>${jib-maven-plugin.version}</version>
     <configuration>
        <from>              
            <image>openjdk:8-jre-alpine</image>
        </from>
        <to>                
            <image>${docker.image.prefix}/${project.artifactId}</image>
        </to>
     </configuration>
   </plugin>
   ```

1. Spring Boot 애플리케이션에 대한 완성된 프로젝트 디렉터리로 이동하고, 다음 명령을 실행하여 이미지를 빌드하고 레지스트리로 푸시합니다.

   ```
   mvn compile jib:build
   ```

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a>Azure CLI를 사용하여 AKS에서 Kubernetes 클러스터 만들기

1. Azure Kubernetes Service에서 Kubernetes 클러스터 만들기 다음 명령은 *wingtiptoys-akscluster*를 클러스터 이름으로 사용하고 *wingtiptoys-kubernetes*를 DNS 접두어로 사용하여 *wingtiptoys-kubernetes* 리소스 그룹에 *kubernetes* 클러스터를 만듭니다.
   ```azurecli
   az aks create --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster \ 
    --dns-name-prefix=wingtiptoys-kubernetes --generate-ssh-keys
   ```
   이 명령을 완료하는 데 다소 시간이 걸릴 수 있습니다.

1. AKS(Azure Kubernetes Service)에서 ACR(Azure Container Registry)을 사용하는 경우 Azure Kubernetes Service 끌어오기 액세스 권한을 Azure Container Registry에 부여해야 합니다. Azure는 Azure Kubernetes Service를 만들 때 기본 서비스 주체를 만듭니다. 다음 스크립트를 bash 또는 Powershell에서 실행하여 AKS 액세스 권한을 ACR에 부여합니다. 자세한 내용은 [Azure Kubernetes Service의 Azure Container Registry를 사용하여 인증]을 참조하세요.

```bash
   # Get the id of the service principal configured for AKS
   CLIENT_ID=$(az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv)
   
   # Get the ACR registry resource id
   ACR_ID=$(az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv)
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

  -- 또는 --

```PowerShell
   # Get the id of the service principal configured for AKS
   $CLIENT_ID = az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv
   
   # Get the ACR registry resource id
   $ACR_ID = az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

1. Azure CLI를 사용하여 `kubectl`을 설치합니다. Linux 사용자는 이 명령 앞에 `sudo`를 붙여야 할 수 있습니다. 그러면 Kubernetes CLI가 `/usr/local/bin`에 배포됩니다.
   ```azurecli
   az aks install-cli
   ```

1. Kubernetes 웹 인터페이스 및 `kubectl`에서 클러스터를 관리할 수 있도록 클러스터 구성 정보를 다운로드합니다. 
   ```azurecli
   az aks get-credentials --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a>Kubernetes 클러스터에 이미지 배포

이 자습서는 `kubectl`을 사용하여 앱을 배포한 다음 Kubernetes 웹 인터페이스를 통해 배포를 탐색할 수 있도록 합니다.

### <a name="deploy-with-kubectl"></a>kubectl을 사용하여 배포

1. 명령 프롬프트를 엽니다.

1. `kubectl run` 명령을 사용하여 Kubernetes 클러스터에서 컨테이너를 실행합니다. Kubernetes의 앱에 대한 서비스 이름 및 전체 이미지 이름을 지정합니다. 예: 
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   이 명령에서 다음이 적용됩니다.

   * 컨테이너 이름 `gs-spring-boot-docker`는 `run` 명령 바로 다음에 지정됩니다.

   * `--image` 매개 변수는 결합된 로그인 서버 및 이미지 이름을 `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`로 지정합니다.

1. `kubectl expose` 명령을 사용하여 Kubernetes 클러스터를 외부에 노출합니다. 서비스 이름, 앱에 액세스하는 데 사용되는 공용 TCP 포트 및 앱이 수신 대기하는 내부 대상 포트를 지정합니다. 예: 
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   이 명령에서 다음이 적용됩니다.

   * 컨테이너 이름 `gs-spring-boot-docker`는 `expose deployment` 명령 바로 다음에 지정됩니다.

   * `--type` 매개 변수는 클러스터가 부하 분산 장치를 사용함을 지정합니다.

   * `--port` 매개 변수는 공용 TCP 포트 80을 지정합니다. 이 포트에서 앱에 액세스합니다.

   * `--target-port` 매개 변수는 내부 TCP 포트 8080을 지정합니다. 부하 분산 장치는 이 포트에서 앱으로 요청을 전달합니다.

1. 앱이 클러스터에 배포되면 외부 IP 주소를 쿼리하고 웹 브라우저에서 엽니다.

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=default
   ```

   ![Azure에서 샘플 앱 찾아보기][SB02]



### <a name="deploy-with-the-kubernetes-web-interface"></a>Kubernetes 웹 인터페이스를 사용하여 배포

1. 명령 프롬프트를 엽니다.

1. 기본 브라우저에서 Kubernetes 클러스터에 대한 구성 웹 사이트를 엽니다.
   ```
   az aks browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

1. 브라우저에서 Kubernetes 구성 웹 사이트가 열리면 해당 링크를 클릭하여 **컨테이너화된 앱을 배포**합니다.

   ![Kubernetes 구성 웹 사이트][KB01]

1. **Resource Creation** 페이지가 표시되면 다음 옵션을 지정합니다.

   a. **앱 만들기**를 선택합니다.

   b. **App name**에 Spring Boot 애플리케이션 이름을 입력합니다(예: "*gs-spring-boot-docker*").

   다. **Container image**에 대해 이전의 로그인 서버 및 컨테이너 이미지를 입력합니다(예: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*").

   d. **Service**에 대해 **External**을 선택합니다.

   e. **Port** 및 **Target Port** 텍스트 상자에 외부 및 내부 포트를 지정합니다.

   ![Kubernetes 구성 웹 사이트][KB02]


1. **Deploy**를 클릭하여 컨테이너를 배포합니다.

   ![Kubernetes 배포][KB05]

1. 애플리케이션이 배포되면 **Services** 아래에 Spring Boot 애플리케이션이 표시됩니다.

   ![Kubernetes 서비스][KB06]

1. **External endpoints**에 대한 링크를 클릭하면 Azure에서 Spring Boot 애플리케이션이 실행되는 것을 볼 수 있습니다.

   ![Kubernetes 서비스][KB07]

   ![Azure에서 샘플 앱 찾아보기][SB02]

## <a name="next-steps"></a>다음 단계

Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.

> [!div class="nextstepaction"]
> [Azure의 Spring](/java/azure/spring-framework)

### <a name="additional-resources"></a>추가 리소스

Azure에서 Spring Boot를 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Azure App Service에 Spring Boot 애플리케이션 배포](deploy-spring-boot-java-web-app-on-azure.md)

Java와 함께 Azure를 사용하는 방법에 관한 자세한 정보는 [Java 개발자를 위한 Azure]와 [Azure DevOps 및 Java 사용하기]를 참조하세요.

Visual Studio Code를 사용하여 Kubernetes에 Java 애플리케이션을 배포하는 방법에 관한 자세한 정보는 [Visual Studio Code Java 자습서]를 참조하세요.

Spring Boot on Docker 샘플 프로젝트에 대한 자세한 내용은 [Spring Boot on Docker 시작] 을 참조하세요.

다음 링크는 Spring Boot 애플리케이션을 만드는 방법에 대한 추가 정보를 제공합니다.

* 간단한 Spring Boot 애플리케이션 만들기에 대한 자세한 내용은 https://start.spring.io/에서 Spring Initializr를 참조하세요.

다음 링크는 Azure에서 Kubernetes를 사용하는 방법에 대한 추가 정보를 제공합니다.

* [Azure Kubernetes Service에서 Kubernetes 클러스터 시작하기](/azure/aks/intro-kubernetes)

Kubernetes 명령줄 인터페이스를 사용하는 방법에 대한 자세한 내용은 <https://kubernetes.io/docs/user-guide/kubectl/>의 **kubectl** 사용자 가이드에서 사용할 수 있습니다.

Kubernetes 웹 사이트에는 개인 레지스트리에서 이미지를 사용하는 방법을 설명하는 일부 문서가 포함되어 있습니다.

* [Pod에 대한 서비스 계정 구성]
* [네임스페이스]
* [개인 레지스트리에서 이미지 끌어오기]

Azure와 함께 사용자 지정 Docker 이미지를 사용하는 방법에 대한 추가 예제를 보려면 [Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]을 참조하세요.

Azure Dev Spaces가 있는 AKS(Azure Kubernetes Service)에서 직접 컨테이너를 반복적으로 실행하고 디버그하는 방법에 대한 자세한 내용은 [Azure Dev Spaces에서 Java를 사용하여 시작]을 참조하세요.

<!-- URL List -->

[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview
[AKS(Azure Kubernetes Service)]: https://azure.microsoft.com/services/kubernetes-service/
[Java 개발자를 위한 Azure]: /java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Azure DevOps 및 Java 사용하기]: /azure/devops/java/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker 시작]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Pod에 대한 서비스 계정 구성]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[네임스페이스]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[개인 레지스트리에서 이미지 끌어오기]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- Newly added -->
[Azure Kubernetes Service의 Azure Container Registry를 사용하여 인증]: /azure/container-registry/container-registry-auth-aks/
[Visual Studio Code Java 자습서]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Azure Dev Spaces에서 Java를 사용하여 시작]: https://docs.microsoft.com/en-us/azure/dev-spaces/get-started-java
<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR04.png

[KB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB01.png
[KB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB02.png
[KB03]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB03.png
[KB04]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB04.png
[KB05]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB05.png
[KB06]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB06.png
[KB07]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB07.png
