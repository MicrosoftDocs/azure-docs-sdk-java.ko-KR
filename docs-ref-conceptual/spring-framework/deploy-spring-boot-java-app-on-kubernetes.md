---
title: Azure Container Service에서 Kubernetes에 Spring Boot 앱 배포
description: 이 자습서에서는 Microsoft Azure에서 Kubernetes 클러스터에 Spring Boot 응용 프로그램을 배포하는 단계를 안내합니다.
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: asirveda;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: 9eb37f302835ea40e92b5212d5bbc305d1311bc4
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954644"
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a>Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 배포

**[Kubernetes]** 및  **[Docker]** 는 개발자가 컨테이너에서 실행 중인 응용 프로그램의 배포, 확장 및 관리를 자동화하는 데 도움이 되는 오픈 소스 솔루션입니다.

이 자습서에서는 이러한 두 가지 인기 있는 오픈 소스 기술을 결합하여 Spring Boot 응용 프로그램을 개발하고 Microsoft Azure에 배포하는 과정을 안내합니다. 좀 더 구체적으로 말하면 응용 프로그램 개발을 위해 *[Spring Boot]*, 컨테이너 배포를 위해 *[Kubernetes]* 및 응용 프로그램을 호스트하기 위해 [AKS(Azure Container Service)]를 사용합니다.

### <a name="prerequisites"></a>필수 조건

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.
* [Azure CLI(명령줄 인터페이스)]
* 최신 [JDK(Java Developer Kit)]
* Apache의 [Maven] 빌드 도구(버전 3)
* [Git] 클라이언트
* [Docker] 클라이언트

> [!NOTE]
>
> 이 자습서의 가상화 요구 사항으로 인해 가상 머신에는 이 문서의 단계를 따를 수 없습니다. 따라서 가상화 기능이 사용하도록 설정된 물리적 컴퓨터를 사용해야 합니다.
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a>Spring Boot on Docker 시작 웹앱 만들기

다음 단계에서는 Spring Boot 웹 응용 프로그램을 빌드하고 로컬로 테스트하는 과정을 안내합니다.

1. 명령 프롬프트를 열고 응용 프로그램을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예를 들면 다음과 같습니다.
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

1. http://localhost:8080 으로 이동하거나 다음`curl` 명령을 사용하여 웹앱을 테스트합니다.
   ```
   curl http://localhost:8080
   ```

1. **Hello Docker World** 메시지가 표시됩니다.

   ![로컬로 샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a>Azure CLI를 사용하여 Azure Container Registry 만들기

1. 명령 프롬프트를 엽니다.

1. Azure 계정에 로그인합니다.
   ```azurecli
   az login
   ```

1. 이 자습서에서 사용되는 Azure 리소스에 대한 리소스 그룹을 만듭니다.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. 리소스 그룹에서 개인 Azure Container Registry를 만듭니다. 이 자습서는 이후 단계에서 샘플 앱을 이 레지스트리에 Docker 이미지로 푸시합니다. `wingtiptoysregistry`를 레지스트리의 고유한 이름으로 바꿉니다.
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a>컨테이너 레지스트리에 앱 푸시

1. Maven 설치에 대한 구성 디렉터리(default ~/.m2/ 또는 C:\Users\username\.m2)로 이동한 후 텍스트 편집기를 사용하여 *settings.xml* 파일을 엽니다.

1. Azure CLI에서 컨테이너 레지스트리에 대한 암호를 검색합니다.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. Azure Container Registry ID 및 암호를 *settings.xml* 파일의 새 `<server>` 컬렉션에 추가합니다.
`id` 및 `username`은 레지스트리의 이름입니다. 이전 명령의 `password` 값을 사용합니다(따옴표 제외).

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Spring Boot 응용 프로그램에 대해 완료된 프로젝트 디렉터리로 이동하고(예: "*C:\SpringBoot\gs-spring-boot-docker\complete*"또는"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") 텍스트 편집기를 사용하여 *pom.xml* 파일을 엽니다.

1. *pom.xml* 파일의 `<properties>` 컬렉션을 Azure Container Registry의 로그인 서버 값으로 업데이트합니다.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. *pom.xml* 파일의 `<plugins>` 컬렉션을 업데이트하여 `<plugin>`에 Azure Container Registry의 로그인 서버 주소 및 레지스트리 이름이 포함되도록 합니다.

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. Spring Boot 응용 프로그램에 대한 완성된 프로젝트 디렉터리로 이동한 후 다음 명령을 실행하여 Docker 컨테이너를 빌드하고 레지스트리에 이미지를 푸시합니다.

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  Maven이 Azure에 이미지를 푸시하는 경우 다음 중 하나와 비슷한 오류 메시지가 나타날 수 있습니다.
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> 이 오류가 발생하는 경우 Docker 명령줄에서 Azure에 로그인합니다.
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> 그런 다음 컨테이너를 푸시합니다.
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a>Azure CLI를 사용하여 AKS에서 Kubernetes 클러스터 만들기

1. Azure Container Service에서 Kubernetes 클러스터를 만듭니다. 다음 명령은 *wingtiptoys-containerservice*를 클러스터 이름으로 사용하고 *wingtiptoys-kubernetes*를 DNS 접두어로 사용하여 *wingtiptoys-kubernetes* 리소스 그룹에 *kubernetes* 클러스터를 만듭니다.
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   이 명령을 완료하는 데 다소 시간이 걸릴 수 있습니다.

1. Azure CLI를 사용하여 `kubectl`을 설치합니다. Linux 사용자는 이 명령 앞에 `sudo`를 붙여야 할 수 있습니다. 그러면 Kubernetes CLI가 `/usr/local/bin`에 배포됩니다.
   ```azurecli
   az acs kubernetes install-cli
   ```

1. Kubernetes 웹 인터페이스 및 `kubectl`에서 클러스터를 관리할 수 있도록 클러스터 구성 정보를 다운로드합니다. 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a>Kubernetes 클러스터에 이미지 배포

이 자습서는 `kubectl`을 사용하여 앱을 배포한 다음 Kubernetes 웹 인터페이스를 통해 배포를 탐색할 수 있도록 합니다.

### <a name="deploy-with-the-kubernetes-web-interface"></a>Kubernetes 웹 인터페이스를 사용하여 배포

1. 명령 프롬프트를 엽니다.

1. 기본 브라우저에서 Kubernetes 클러스터에 대한 구성 웹 사이트를 엽니다.
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. 브라우저에서 Kubernetes 구성 웹 사이트가 열리면 해당 링크를 클릭하여 **컨테이너화된 앱을 배포**합니다.

   ![Kubernetes 구성 웹 사이트][KB01]

1. **Deploy a containerized app** 페이지가 표시되면 다음 옵션을 지정합니다.

   a. **Specify app details below**를 선택합니다.

   나. **App name**에 Spring Boot 응용 프로그램 이름을 입력합니다(예: "*gs-spring-boot-docker*").

   다. **Container image**에 대해 이전의 로그인 서버 및 컨테이너 이미지를 입력합니다(예: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*").

   d. **Service**에 대해 **External**을 선택합니다.

   e. **Port** 및 **Target Port** 텍스트 상자에 외부 및 내부 포트를 지정합니다.

   ![Kubernetes 구성 웹 사이트][KB02]


1. **Deploy**를 클릭하여 컨테이너를 배포합니다.

   ![컨테이너 배포][KB05]

1. 응용 프로그램이 배포되면 **Services** 아래에 Spring Boot 응용 프로그램이 표시됩니다.

   ![Kubernetes 서비스][KB06]

1. **External endpoints**에 대한 링크를 클릭하면 Azure에서 Spring Boot 응용 프로그램이 실행되는 것을 볼 수 있습니다.

   ![Kubernetes 서비스][KB07]

   ![Azure에서 샘플 앱 찾아보기][SB02]


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
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Azure에서 샘플 앱 찾아보기][SB02]


## <a name="next-steps"></a>다음 단계

Azure에서 Spring Boot를 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Azure App Service에 Spring Boot 응용 프로그램 배포](deploy-spring-boot-java-web-app-on-azure.md)
* [Azure Container Service에서 Linux에 Spring Boot 응용 프로그램 배포](deploy-spring-boot-java-app-on-linux.md)

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.

Spring Boot on Docker 샘플 프로젝트에 대한 자세한 내용은 [Spring Boot on Docker 시작] 을 참조하세요.

다음 링크는 Spring Boot 응용 프로그램을 만드는 방법에 대한 추가 정보를 제공합니다.

* 간단한 Spring Boot 응용 프로그램 만들기에 대한 자세한 내용은 https://start.spring.io/에서 Spring Initializr를 참조하세요.

다음 링크는 Azure에서 Kubernetes를 사용하는 방법에 대한 추가 정보를 제공합니다.

* [Container Service에서 Kubernetes 클러스터 시작](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [Azure Container Service에서 Kubernetes 웹 UI 사용](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

Kubernetes 명령줄 인터페이스를 사용하는 방법에 대한 자세한 내용은 <https://kubernetes.io/docs/user-guide/kubectl/>의 **kubectl** 사용자 가이드에서 사용할 수 있습니다.

Kubernetes 웹 사이트에는 개인 레지스트리에서 이미지를 사용하는 방법을 설명하는 일부 문서가 포함되어 있습니다.

* [Pod에 대한 서비스 계정 구성]
* [네임스페이스]
* [개인 레지스트리에서 이미지 끌어오기]

Azure와 함께 사용자 지정 Docker 이미지를 사용하는 방법에 대한 추가 예제를 보려면 [Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]을 참조하세요.

<!-- URL List -->

[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview
[AKS(Azure Container Service)]: https://azure.microsoft.com/services/container-service/
[Java 개발자용 Azure]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[무료 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK(Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/
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
