---
title: Maven 및 Azure를 사용하여 Spring Boot 앱을 클라우드에 배포
description: Azure Web Apps의 Maven 플러그 인을 사용하여 Spring Boot 앱을 클라우드에 배포하는 방법에 대해 알아봅니다.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.assetid: ''
ms.author: robmcm;kevinzha;brborges
ms.date: 06/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 3610312ed17301131967bd2c047c86656de070e7
ms.sourcegitcommit: f313c14e92f38c54a3a583270ee85cc928cd39d7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34689426"
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-app-service"></a>Azure Apps Service의 Maven 플러그 인을 사용하여 Spring Boot 앱을 클라우드에 배포

이 문서에서는 Azure App Service Web Apps의 Maven 플러그 인을 사용하여 샘플 Spring Boot 응용 프로그램을 배포하는 방법을 보여줍니다.

> [!NOTE]
> 
> [Apache Maven](http://maven.apache.org/)에서 Azure Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme)용 [Maven 플러그인은 Maven 프로젝트에 Azure App Service의 원활한 통합을 제공하고, 개발자가 Azure App Service에 웹앱을 배포하는 프로세스를 간소화합니다.

Maven 플러그인을 사용하기 전에 Maven Central에서 사용 가능한 플러그인 최신 버전을 확인합니다: [ ![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22) 

## <a name="prerequisites"></a>필수 조건

이 자습서의 단계를 완료하려면 다음 필수 조건이 필요합니다.

* Azure 구독; Azure 구독이 아직 없는 경우 [체험판 Azure 계정]에 등록할 수 있습니다.
* [Azure CLI(명령줄 인터페이스)]
* 최신 [JDK(Java Development Kit)], 버전 1.7 이상
* Apache의 [Maven] 빌드 도구(버전 3)
* [Git] 클라이언트

## <a name="clone-the-sample-spring-boot-web-app"></a>샘플 Spring Boot 웹앱 복제

이 섹션에서는 완료된 Spring Boot 응용 프로그램을 복제하고 로컬로 테스트합니다.

1. 명령 프롬프트 또는 터미널 창을 열고 Spring Boot 응용 프로그램을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- 또는 --
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. [Spring Boot 시작하기] 샘플 프로젝트를 만든 디렉터리에 복제합니다. 예:
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. 디렉터리를 완료된 프로젝트로 변경합니다. 예:
   ```shell
   cd gs-spring-boot/complete
   ```

1. Maven을 사용하여 JAR 파일을 빌드합니다. 예:
   ```shell
   mvn clean package
   ```

1. 웹앱을 만들면 Maven을 사용하여 웹앱을 시작합니다. 예:
   ```shell
   mvn spring-boot:run
   ```

1. 웹 브라우저를 사용하여 로컬로 이동하여 웹앱을 테스트합니다. 예를 들어, curl을 사용할 수 있는 경우 다음 명령을 사용할 수 있습니다.
   ```shell
   curl http://localhost:8080
   ```

1. 다음과 같이 **Greetings from Spring Boot!** 라는 메시지가 표시됩니다.

## <a name="adjust-project-for-war-based-deployment-on-azure-app-service"></a>Azure App Service에 WAR 기반 배포에 대한 프로젝트를 조정합니다.

이 섹션에서는 기본적으로 Tomcat을 런타임으로 제공하는 Azure App Service에 WAR 파일로 배포할 Spring Boot 프로젝트를 신속하게 조정하게 됩니다. 이 작업을 위해서는 두 가지 파일이 수정되어야 합니다.

- Maven `pom.xml` 파일
- `Application` Java 클래스

Maven 설정부터 시작해 보겠습니다.

1. `pom.xml` 열기

1. 맨 위에 있는 `<artifactId>` 정의 바로 뒤에 `<packaging>war</packaging>` 추가합니다.
   ```xml
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.springframework</groupId>
    <artifactId>gs-spring-boot</artifactId>

    <packaging>war</packaging>
   ```

1. 다음 종속성을 추가합니다.
   ```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
   ```

이제 `Application` 클래스를 열고, IDE가 새 종속성을 이미 선택했으면, 다음과 같이 수정을 진행합니다.

1. 클래스 응용프로그램을 `SpringBootServletInitializer`의 서브 클래스로 만듭니다.
   ```java
   @SpringBootApplication
   public class Application extends SpringBootServletInitializer {
     // ...
   }
   ```

1. 응용프로그램 클래스에 다음 메서드를 추가합니다.
   ```java
       @Override
       protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
           return application.sources(Application.class);
       }
   ```

이제 응용프로그램은 Tomcat 및 다른 Servlet 런타임(예: Jetty)에 배포될 수 있습니다.

## <a name="add-the-maven-plugin-for-azure-app-service-web-apps"></a>Azure App Service Web Apps용 Maven 플러그인 추가

이 섹션에서는 Azure App Service Web Apps에 이 응용프로그램의 전체 배포를 자동화하는 Maven 플러그인을 추가합니다.

1. `pom.xml`을 다시 한 번 엽니다.

1. `<properties>` 내에서, `maven.build.timestamp.format` 속성으로 사용자 지정 타임스탬프 형식을 설정합니다. Azure App Service는 응용프로그램의 공개 URL을 생성하기 때문에, 이 설정은 배포 이름을 생성하고 다른 사용자의 실시간 배포와의 충돌을 피하기 위해 사용됩니다.
   ```xml
    <properties>
        <java.version>1.8</java.version>
        <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
    </properties>
   ```

1. `<plugins>` 요소에 다음을 추가합니다.
   ```xml
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
    </plugin>
   ```

이러한 설정을 통해, 귀하의 Maven 프로젝트는 이제 실시간으로 Azure App Service Web App에 배포될 수 있습니다.

## <a name="install-and-log-in-to-azure-cli"></a>Azure CLI 설치 및 로그인

Maven Plugin이 Spring Boot 응용프로그램을 배포하도록 하는 가장 간단하고 쉬운 방법은 [ Azure CLI](https://docs.microsoft.com/cli/azure/)를 사용하는 것입니다. 설치되어 있는지 확인해 보세요.

1. Azure CLI를 사용하여 Azure 계정에 로그인합니다.
   ```shell
   az login
   ```
   지시에 따라 로그인 프로세스를 완료합니다.

## <a name="optionally-customize-pomxml-before-deploying"></a>또는 배포 전에 pom.xml을 사용자 지정합니다.

텍스트 편집기에서 Spring Boot 응용 프로그램에 대한 `pom.xml` 파일을 열고 `azure-webapp-maven-plugin`에 대한 `<plugin>` 요소를 찾습니다. 이 요소는 다음 예제와 유사합니다.

   ```xml
  <plugins>
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
      <configuration>
         <resourceGroup>maven-projects</resourceGroup>
         <appName>${project.artifactId}-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>war</deploymentType>
      </configuration>
    </plugin>
  </plugins>
   ```

Maven 플러그 인에 대해 수정할 수 있는 여러 값이 있으며 이러한 각 요소에 대한 자세한 설명을 [Azure Web Apps의 Maven 플러그 인] 설명서에서 사용할 수 있습니다. 즉, 이 문서에서 강조 표시된 값은 여러 개입니다.

| 요소 | 설명 |
|---|---|
| `<version>` | [Azure Web Apps의 Maven 플러그 인] 버전을 지정합니다. [Maven 중앙 리포지토리](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22)에 나열된 버전을 검사하여 최신 버전을 사용하고 있는지 확인합니다. |
| `<resourceGroup>` | 대상 리소스 그룹, 즉, 이 예에서 `maven-plugin`을 지정합니다. 리소스 그룹이 아직 존재하지 않는 경우 배포 중에 만들어집니다. |
| `<appName>` | 웹앱에 대한 대상 이름을 지정합니다. 이 예제에서는 대상 이름은 `maven-web-app-${maven.build.timestamp}`이며 이 예제에서 충돌을 피하기 위해 여기에 `${maven.build.timestamp}` 접미사가 추가됩니다. (타임스탬프는 선택 사항입니다. 앱 이름에 대한 고유한 문자열을 지정할 수 있습니다.) |
| `<region>` | 대상 지역을 지정합니다. 이 예제에서는 `westus`입니다. (전체 목록은 [Azure Web Apps의 Maven 플러그 인] 설명서에서 제공됩니다.) |
| `<javaVersion>` | 웹앱에 Java 런타임 버전을 지정합니다. (전체 목록은 [Azure Web Apps의 Maven 플러그 인] 설명서에서 제공됩니다.) |
| `<deploymentType>` | 웹앱의 배포 형식을 지정합니다. 기본값은 `war`입니다. |

## <a name="build-and-deploy-your-web-app-to-azure"></a>Azure에 웹앱 빌드 및 배포

이 문서의 이전 섹션에서 설정을 모두 구성했으면 웹앱을 Azure에 배포할 준비가 되었습니다. 이렇게 하려면 다음 단계를 수행합니다.

1. *pom.xml* 파일을 변경한 경우 이전에 사용하던 명령 프롬프트 또는 터미널 창에서 Maven를 사용하여 JAR 파일을 다시 작성합니다. 예:
   ```shell
   mvn clean package
   ```

1. Maven을 사용하여 Azure에 웹앱을 배포합니다. 예:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven은 Azure에 웹앱을 배포합니다. 웹앱이 아직 없는 경우 생성됩니다.

웹을 배포하면 [Azure Portal]을 사용하여 작업을 관리할 수 있습니다.

* 웹앱은 **App Services**에 나열됩니다.

   ![Azure Portal App Services에 나열된 웹앱][AP01]

* 웹앱의 URL은 웹앱의 **개요**에 나열됩니다.

   ![웹앱의 URL 확인][AP02]

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

이 문서에서 설명하는 다양한 기술에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Azure Web Apps의 Maven 플러그 인]

* [Azure CLI에서 Azure에 로그인](/azure/xplat-cli-connect)

* [Azure Web Apps의 Maven 플러그 인을 사용하여 컨테이너화된 Spring Boot 앱을 Azure에 배포하는 방법](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Maven 설정 참조](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot 시작하기]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Azure Web Apps의 Maven 플러그 인]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
