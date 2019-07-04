---
title: Maven 및 Azure를 사용하여 Spring Boot JAR 파일 앱을 클라우드에 배포
description: Linux용 Azure Web Apps의 Maven 플러그 인을 사용하여 Spring Boot 앱을 클라우드에 배포하는 방법에 대해 알아봅니다.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: brborges
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: b133290d1f14429cbf36d6ed5a67d27e1a637593
ms.sourcegitcommit: 599405a9ce892d75073ef0776befa2fa22407b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67237602"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a>Linux에 Azure App Service에 Spring Boot JAR 파일 웹앱 배포

이 문서에서는 [Azure App Service Web Apps용 Maven Plugin](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme)을 사용하여 Java SE JAR로 패키지된 Spring Boot 애플리케이션을 [Linux의 Azure App Service](/azure/app-service/containers/)에 배포하는 방법을 보여줍니다. 앱의 의존성, 런타임 및 구성을 배포 가능한 단일 아티팩트에 통합하려면 [Tomcat 및 WAR 파일](/azure/app-service/containers/quickstart-java)에 대해 Java SE 배포를 선택합니다.


Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.

## <a name="prerequisites"></a>필수 조건

이 자습서의 단계를 완료하려면 다음이 설치 및 구성되어야 합니다.

* [Azure CLI](/cli/azure/), 로컬로 또는 [Azure Cloud Shell](https://shell.azure.com)을 통해.
* 지원되는 JDK(Java Development Kit) Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.
* Apache [Maven](https://maven.apache.org/), 버전 3).
* [Git](https://git-scm.com/downloads) 클라이언트

## <a name="install-and-sign-in-to-azure-cli"></a>Azure CLI 설치 및 로그인

Maven Plugin이 Spring Boot 애플리케이션을 배포하도록 하는 가장 간단하고 쉬운 방법은 [ Azure CLI](/cli/azure/)를 사용하는 것입니다.

Azure CLI를 사용하여 Azure 계정에 로그인합니다.
   
   ```shell
   az login
   ```
   
지시에 따라 로그인 프로세스를 완료합니다.

## <a name="clone-the-sample-app"></a>샘플 앱 복제

이 섹션에서는 완료된 Spring Boot 애플리케이션을 복제하고 로컬로 테스트합니다.

1. 명령 프롬프트 또는 터미널 창을 열고 Spring Boot 애플리케이션을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예:
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

1. 다음 메시지가 표시되어야 합니다. **Greetings from Spring Boot!**

## <a name="configure-maven-plugin-for-azure-app-service"></a>Azure App Service용 Maven 플러그인 구성

이 섹션에서는 Maven이 Linux의 Azure App Service에 앱을 배포할 수 있도록 Spring Boot 프로젝트 `pom.xml`을 구성합니다.

1. 코드 편집기에서 `pom.xml`를 엽니다.

2. pom.xml의 `<build>` 섹션에서 `<plugins>` 태그 안에 다음 `<plugin>` 항목을 추가하세요.

   ```xml
   <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.6.0</version>
   </plugin>
   ```

3. 그런 다음 배포를 구성하고 명령 프롬프트에서 maven 명령 `mvn azure-webapp:config`를 실행하고 **번호**를 사용하여 프롬프트에서 다음 옵션을 선택할 수 있습니다.
    * **OS**: linux  
    * **javaVersion**: jre8
    * **runtimeStack**: jre8

**확인(Y/N)** 프롬프트가 표시되면 **'y'** 키를 누르면 구성이 완료됩니다.

```cmd
~@Azure:~/gs-spring-boot/complete$ mvn azure-webapp:config
[INFO] Scanning for projects...
[INFO]
[INFO] -----------------< org.springframework:gs-spring-boot >-----------------
[INFO] Building gs-spring-boot 0.1.0
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- azure-webapp-maven-plugin:1.6.0:config (default-cli) @ gs-spring-boot ---
[WARNING] The plugin may not work if you change the os of an existing webapp.
Define value for OS(Default: Linux):
1. linux [*]
2. windows
3. docker
Enter index to use:
Define value for javaVersion(Default: jre8):
1. jre8 [*]
2. java11
Enter index to use:
Define value for runtimeStack(Default: TOMCAT 8.5):
1. TOMCAT 9.0
2. jre8
3. TOMCAT 8.5 [*]
4. WILDFLY 14
Enter index to use: 2
Please confirm webapp properties
AppName : gs-spring-boot-1559091271202
ResourceGroup : gs-spring-boot-1559091271202-rg
Region : westeurope
PricingTier : Premium_P1V2
OS : Linux
RuntimeStack : JAVA 8-jre8
Deploy to slot : false
Confirm (Y/N)? : Y
```

4. `<azure-webapp-maven-plugin>`의 `<configuration>` 섹션에 `<appSettings>` 섹션을 추가하여 *80* 포트에서 수신 대기합니다.

    ```xml
   <plugin>
       <groupId>com.microsoft.azure</groupId>
       <artifactId>azure-webapp-maven-plugin</artifactId>
       <version>1.6.0</version>
       <configuration>
          <schemaVersion>V2</schemaVersion>
          <resourceGroup>gs-spring-boot-1559091271202-rg</resourceGroup>
          <appName>gs-spring-boot-1559091271202</appName>
          <region>westeurope</region>
          <pricingTier>P1V2</pricingTier>

          <!-- Begin of App Settings  -->
          <appSettings>
             <property>
                   <name>JAVA_OPTS</name>
                   <value>-Dserver.port=80</value>
             </property>
          </appSettings>
          <!-- End of App Settings  -->
          ...
         </configuration>
   </plugin>
   ```

## <a name="deploy-the-app-to-azure"></a>Azure에 앱 배포

이 문서의 이전 섹션에서 설정을 모두 구성했으면 웹앱을 Azure에 배포할 준비가 되었습니다. 이렇게 하려면 다음 단계를 수행합니다.

1. *pom.xml* 파일을 변경한 경우 이전에 사용하던 명령 프롬프트 또는 터미널 창에서 Maven를 사용하여 JAR 파일을 다시 작성합니다. 예:
   ```shell
   mvn clean package
   ```

1. Maven을 사용하여 Azure에 웹앱을 배포합니다. 예:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven은 Azure에 웹앱을 배포합니다. 웹앱이나 웹앱 플랜이 아직 없는 경우 생성됩니다.

웹을 배포하면 [Azure Portal]을 사용하여 작업을 관리할 수 있습니다.

* 웹앱은 **App Services**에 나열됩니다.

   ![Azure Portal App Services에 나열된 웹앱][AP01]

* 웹앱의 URL은 웹앱의 **개요**에 나열됩니다.

   ![웹앱의 URL 확인][AP02]

`localhost` 대신 포털의 웹앱 URL을 사용하여 이전과 동일한 cURL 명령을 사용하여 배포가 성공적으로 완료되었는지 확인합니다. 다음 메시지가 표시되어야 합니다. **Greetings from Spring Boot!** 

## <a name="next-steps"></a>다음 단계

Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.

> [!div class="nextstepaction"]
> [Azure의 Spring](/java/azure/spring-framework)

### <a name="additional-resources"></a>추가 리소스

이 문서에서 설명하는 다양한 기술에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Azure Web Apps의 Maven 플러그 인]

* [Azure Web Apps의 Maven 플러그 인을 사용하여 컨테이너화된 Spring Boot 앱을 Azure에 배포하는 방법](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Maven 설정 참조](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: /java/azure/
[Azure Portal]: https://portal.azure.com/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot 시작하기]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Azure Web Apps의 Maven 플러그 인]: /java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
