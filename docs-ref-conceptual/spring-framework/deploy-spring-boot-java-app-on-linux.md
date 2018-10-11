---
title: Azure Container Service에서 Linux에 Spring Boot Web App 배포
description: 이 자습서에서는 Microsoft Azure에서 Linux Web App으로 Spring Boot 응용 프로그램을 배포하는 단계를 설명합니다.
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: asirveda;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: container-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 49d94d11ad6a4e103ded849e477d99f01955c693
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48899206"
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a>Azure Container Service에서 Linux에 Spring Boot 응용 프로그램 배포

이 자습서에서는 [Docker]를 사용하여 [AKS(Azure Container Service)]에서 [Spring Boot] 응용 프로그램을 개발하고 Linux 호스트에 배포하는 방법을 설명합니다.

## <a name="prerequisites"></a>필수 조건

이 자습서의 단계를 완료하려면 다음 필수 조건이 필요합니다.

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.
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

다음 단계에서는 간단한 Spring Boot 웹 응용 프로그램을 만들어 로컬로 테스트하는 데 필요한 단계를 안내합니다.

1. 명령 프롬프트를 열고 응용 프로그램을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- 또는 --
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. [Spring Boot on Docker 시작] 샘플 프로젝트를 방금 만든 디렉터리에 복제합니다. 예:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. 디렉터리를 완료된 프로젝트로 변경합니다. 예:
   ```
   cd gs-spring-boot-docker/complete
   ```

1. Maven을 사용하여 JAR 파일을 빌드합니다. 예:
   ```
   mvn package
   ```

1. 웹앱이 만들어지면 디렉터리를 JAR 파일이 위치한 `target` 디렉터리로 변경하고 웹앱을 시작합니다. 예:
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. 웹 브라우저를 사용하여 로컬로 이동하여 웹앱을 테스트합니다. 예를 들어 curl을 사용할 수 있고 포트 80에서 실행하도록 Tomcat 서버를 구성한 경우:
   ```
   curl http://localhost
   ```

1. **Hello Docker World!** 라는 메시지가 표시되어야 합니다.

   ![로컬로 샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a>Azure Container Registry를 만들어서 개인 Docker 레지스트리로 사용

다음 단계에서는 Azure Portal을 사용하여 Azure Container Registry를 만드는 방법을 설명합니다.

> [!NOTE]
>
> Azure Portal 대신 Azure CLI를 사용하려는 경우 [Azure CLI 2.0을 사용하여 개인 Docker 컨테이너 레지스트리 만들기](/azure/container-registry/container-registry-get-started-azure-cli)의 단계에 따르세요.
>

1. [Azure Portal]을 찾아 로그인합니다.

   Azure Portal에서 사용자의 계정에 로그인한 다음, [Azure Portal을 사용하여 개인 Docker 컨테이너 레지스트리 만들기] 문서의 단계를 수행할 수 있습니다. 편의상 다음 단계에서 다시 설명합니다.

1. **+ 새로 만들기**의 메뉴 아이콘을 클릭하고 **컨테이너**를 클릭한 다음, **Azure Container Registry**를 클릭합니다.
   
   ![새로운 Azure Container Registry 만들기][AR01]

1. Azure Container Registry 템플릿에 대한 정보 페이지가 표시되면 **만들기**를 클릭합니다. 

   ![새로운 Azure Container Registry 만들기][AR02]

1. **컨테이너 레지스트리 만들기** 페이지가 표시되면 **레지스트리 이름** 및 **리소스 그룹**을 입력하고 **관리 사용자**에 대해 **사용**을 선택한 다음, **만들기**를 클릭합니다.

   ![Azure Container Registry 설정 구성][AR03]

1. 컨테이너 레지스트리를 만들면 Azure Portal에서 컨테이너 레지스트리를 탐색한 다음, **선택키**를 클릭합니다. 다음 단계에서 사용하기 위해 사용자 이름과 암호를 적어둡니다.

   ![Azure Container Registry 선택키][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a>Azure Container Registry 선택키를 사용하도록 Maven 구성

1. Maven 설치를 위해 구성 디렉터리로 이동한 후 텍스트 편집기를 사용하여 *settings.xml* 파일을 엽니다.

1. 이 자습서의 이전 섹션에서 *settings.xml* 파일의 `<servers>` 컬렉션에 Azure Container Registry 액세스 설정을 추가합니다. 예:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Spring Boot 응용 프로그램의 완성된 프로젝트 디렉터리로 이동하고(예: “*C:\SpringBoot\gs-spring-boot-docker\complete*” 또는 “*/users/robert/SpringBoot/gs-spring-boot-docker/complete*”) 텍스트 편집기를 사용하여 *pom.xml* 파일을 엽니다.

1. *pom.xml* 파일의 `<properties>` 컬렉션을 이 자습서의 이전 섹션에서 사용한 Azure Container Registry의 로그인 서버 값으로 업데이트합니다. 예:

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. *pom.xml* 파일의 `<plugins>` 컬렉션을 업데이트하여 `<plugin>`에 이 자습서의 이전 섹션에서 사용한 Azure Container Registry의 로그인 서버 주소 및 레지스트리 이름이 포함되도록 합니다. 예: 

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

1. Spring Boot 응용 프로그램의 완성된 프로젝트 디렉터리로 이동하고 다음 명령을 실행하여 응용 프로그램을 다시 빌드하고 Azure Container Registry에 컨테이너를 푸시합니다.

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> Azure에 Docker 컨테이너를 푸시할 때 Docker 컨테이너를 성공적으로 만들었더라도 다음 중 하나와 비슷한 오류 메시지가 표시될 수 있습니다.
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> 이런 경우 Docker 명령줄에서 Azure 계정에 로그인해야 합니다. 예:
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> 그런 다음, 명령줄에서 컨테이너를 푸시할 수 있습니다. 예:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>컨테이너 이미지를 사용하여 Azure App Service에서 Linux에 웹앱 만들기

1. [Azure Portal]을 찾아 로그인합니다.

2. **+ 새로 만들기**의 메뉴 아이콘을 클릭하고 **웹 + 모바일**을 클릭한 다음 **}Web App on Linux**를 클릭합니다.
   
   ![Azure Portal에서 새로운 웹앱 만들기][LX01]

3. **Web App on Linux** 페이지가 표시되면 다음 정보를 입력합니다.

   a. **앱 이름**에 고유한 이름을 입력합니다. 예: "*wingtiptoyslinux*."

   b. 드롭다운 목록에서 **구독**을 선택합니다.

   다. 기존 **리소스 그룹**을 선택하거나 새 리소스 그룹을 만들기 위해 이름을 지정합니다.

   d. **컨테이너 구성**을 클릭하고 다음 정보를 입력합니다.

   * **개인 레지스트리**를 선택합니다.

   * **이미지 및 선택적 태그**: 이전에 사용한 컨테이너 이름을 지정합니다. 예: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"

   * **서버 URL**: 이전의 레지스트리 URL을 지정합니다. 예: "*<https://wingtiptoysregistry.azurecr.io>*"

   * **로그인 사용자 이름** 및 **암호**: 이전 단계에서 사용한 **액세스 키**의 로그인 자격 증명을 지정합니다.
   
   e. 위의 정보를 모두 입력하면 **확인**을 클릭합니다.

   ![웹앱 설정 구성][LX02]

4. **만들기**를 클릭합니다.

> [!NOTE]
>
> Azure에서는 표준 포트 80 또는 8080에서 실행되는 임베디드 Tomcat 서버에 인터넷 요청을 자동으로 매핑합니다. 그러나 사용자 지정 포트에서 임베디드 Tomcat 서버를 실행하도록 구성한 경우, 임베디드 Tomcat 서버에 포트를 정의하는 웹앱에 환경 변수를 추가해야 합니다. 이렇게 하려면 다음 단계를 수행합니다.
>
> 1. [Azure Portal]을 찾아 로그인합니다.
> 
> 2. **App Services** 아이콘을 클릭합니다. (아래 이미지에서 항목 #1 참조)
>
> 3. 목록에서 웹앱을 선택합니다. (아래 이미지에서 항목 #2)
>
> 4. **응용 프로그램 설정**을 클릭합니다. (아래 이미지에서 항목 #3)
>
> 5. **앱 설정** 섹션에서 **PORT**라는 새 환경 변수를 추가하고 값에 사용자 지정 포트 번호를 입력합니다. (아래 이미지에서 항목 #4)
>
> 6. **저장**을 클릭합니다. (아래 이미지에서 항목 #5)
>
> ![Azure Portal에서 사용자 지정 포트 번호 저장][LX03]
>

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a>다음 단계

Azure에서 Spring Boot 응용 프로그램을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Azure App Service에 Spring Boot 응용 프로그램 배포](deploy-spring-boot-java-web-app-on-azure.md)
* [Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 배포](deploy-spring-boot-java-app-on-kubernetes.md)

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.

Spring Boot on Docker 샘플 프로젝트에 대한 자세한 정보는 [Spring Boot on Docker 시작]을 참조하세요.

자체 Spring Boot 응용 프로그램을 시작하는 데 도움이 필요하면 https://start.spring.io/에서 **Spring Initializr**를 참조하세요.

간단한 Spring Boot 응용 프로그램을 만들기 시작하는 방법에 대한 자세한 내용은 https://start.spring.io/에서 Spring Initializr를 참조하세요.

Azure와 함께 사용자 지정 Docker 이미지를 사용하는 방법에 대한 추가 예제를 보려면 [Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]을 참조하세요.

<!-- URL List -->

[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview
[AKS(Azure Container Service)]: https://azure.microsoft.com/services/container-service/
[Java 개발자용 Azure]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[Azure Portal을 사용하여 개인 Docker 컨테이너 레지스트리 만들기]: /azure/container-registry/container-registry-get-started-portal
[Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK(Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker 시작]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-linux/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-linux/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-linux/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-linux/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-linux/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-linux/AR04.png

[LX01]: ./media/deploy-spring-boot-java-app-on-linux/LX01.png
[LX02]: ./media/deploy-spring-boot-java-app-on-linux/LX02.png
[LX03]: ./media/deploy-spring-boot-java-app-on-linux/LX03.png
