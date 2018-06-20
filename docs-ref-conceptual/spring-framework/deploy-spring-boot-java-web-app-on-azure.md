---
title: Azure App Service로 클라우드에 Spring Boot 응용 프로그램 배포
description: 이 자습서는 개발자에게 Azure App Service를 사용하는 클라우드에 Spring Boot 시작하기 웹앱을 배포하는 단계를 안내합니다.
services: app-service
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
ms.openlocfilehash: adf779e2ba6ca73ea3a2406613f9622cc9ecbf99
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954526"
---
# <a name="deploy-a-spring-boot-application-to-the-cloud-with-azure-app-service"></a>Azure App Service로 클라우드에 Spring Boot 응용 프로그램 배포

이 자습서에서는 샘플 [Spring Boot] 시작하기 웹앱을 만들어 [Azure App Service]에 배포하는 방법을 안내합니다.

### <a name="prerequisites"></a>필수 조건

이 자습서의 단계를 완료하려면 다음이 필요합니다.

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정{]에 등록할 수 있습니다.
* 최신 [JDK(Java Developer Kit)]
* Apache의 [Maven] 빌드 도구(버전 3)
* [Git] 클라이언트

## <a name="create-the-spring-boot-getting-started-web-app"></a>Spring Boot 시작하기 웹앱 만들기

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

1. [Spring Boot 시작하기] 샘플 프로젝트를 방금 만든 디렉터리에 복제합니다. 예:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. 디렉터리를 완료된 프로젝트로 변경합니다. 예:
   ```
   cd gs-spring-boot
   cd complete
   ```

1. Maven을 사용하여 JAR 파일을 빌드합니다. 예:
   ```
   mvn package
   ```

1. 웹앱이 만들어지면 디렉터리를 JAR 파일로 변경하고 웹앱을 시작합니다. 예:
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. 웹 브라우저를 통해 http://localhost:8080 으로 이동하여 웹앱을 테스트하거나 사용 가능한 curl이 있는 경우 다음 예제와 같이 구문을 사용합니다.
   ```
   curl http://localhost:8080
   ```

1. 다음과 같이 **Greetings from Spring Boot!** 라는 메시지가 표시됩니다.

   ![샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a>Java에서 사용할 Azure 웹앱 만들기

다음 단계에서는 Azure 웹앱을 만들고 Java에 필요한 설정을 구성하고 FTP 자격 증명을 구성하는 단계를 안내합니다.

1. [Azure Portal]로 이동하고 로그인합니다.

1. Azure Portal의 계정에 로그인한 후 **App Services** 메뉴 아이콘을 클릭합니다.
   
   ![Azure portal][AZ01]

1. **App Services** 페이지가 표시되면 **+ 추가**를 클릭하여 새 App Service를 만듭니다.

   ![App Service 만들기][AZ02]

1. 웹앱 템플릿 목록이 표시되면 기본 Microsoft 웹앱에 대한 링크를 클릭합니다.

   ![웹앱 템플릿][AZ03]

1. 웹앱 템플릿에 대한 정보 페이지가 표시되면 **만들기**를 클릭합니다.

   ![웹앱 만들기][AZ04]

1. 웹앱에 고유한 이름을 제공하고 모든 추가 설정을 지정한 다음 **만들기**를 클릭합니다.

   ![웹앱 만들기 설정][AZ05]

1. 웹앱을 만든 후 **App Services** 메뉴 아이콘을 클릭한 다음 새로 만든 웹앱을 클릭합니다.

   ![Web Apps 나열][AZ06]

1. 웹앱이 표시되면 다음 단계를 사용하여 Java 버전을 지정합니다.

   a. **응용 프로그램 설정** 메뉴 항목을 클릭합니다.

   나. Java 버전으로 **Java 8**을 선택합니다.

   다. 부 Java 버전으로 **가장 최근 항목**을 선택합니다.

   d. 웹 컨테이너로 **최신 Tomcat 8.5**를 선택합니다. (이 컨테이너는 실제로 사용되지 않습니다. Azure는 Spring Boot 응용 프로그램의 컨테이너를 사용합니다.)

   e. **저장**을 클릭합니다.

   ![응용 프로그램 설정][AZ07]

1. 다음 단계를 사용하여 FTP 배포 자격 증명을 지정 합니다.

   a. **배포 자격 증명** 메뉴 항목을 클릭합니다.

   나. 사용자 이름 및 암호를 지정합니다.

   다. **저장**을 클릭합니다.

   ![배포 자격 증명 지정][AZ08]

1. 다음 단계를 사용하여 FTP 연결 정보를 검색합니다.

   a. **배포 자격 증명** 메뉴 항목을 클릭합니다.

   나. 전체 FTP 사용자 이름 및 URL을 복사하고 이 자습서의 다음 섹션을 위해 저장합니다.

   ![FTP URL 및 자격 증명][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a>Azure에 Spring Boot 웹앱 배포

다음 단계에서는 Azure에 Spring Boot 웹앱을 배포하는 단계를 안내합니다.

1. Windows 메모장과 같은 텍스트 편집기를 열고 새 문서에 다음 텍스트를 붙여넣은 후 파일을 *web.config*로 저장합니다
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. *web.config* 파일을 시스템에 저장한 후 이 자습서의 이전 섹션에 나온 URL, 사용자 이름 및 암호를 사용하여 FTP를 통해 웹앱에 연결합니다. 예: 
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. 원격 디렉터리를 웹앱의 루트 폴더(*/site/wwwroot*)로 변경한 다음 Spring Boot 응용 프로그램의 JAR 파일과 앞에서의 *web.config*를 복사합니다. 예: 
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. JAR 파일과 *web.config* 파일을 웹앱에 배포한 후 Azure Portal을 사용하여 웹앱을 다시 시작해야 합니다.

   ![웹앱을 다시 시작합니다.][AZ10]

1. 웹 브라우저를 사용해 웹앱의 URL로 이동하여 웹앱을 테스트하거나 사용 가능한 curl이 있는 경우 다음 예제와 같이 구문을 사용합니다.
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. 다음과 같이 **Greetings from Spring Boot!** 라는 메시지가 표시됩니다.

   ![샘플 앱 찾아보기][SB02]

## <a name="next-steps"></a>다음 단계

Azure에서 Spring Boot 응용 프로그램을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Azure Container Service에서 Linux에 Spring Boot 응용 프로그램 배포](deploy-spring-boot-java-app-on-linux.md)

* [Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 배포](deploy-spring-boot-java-app-on-kubernetes.md)

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.

FTP를 사용하여 Azure에 웹앱을 배포하는 방법에 대한 자세한 내용은 [FTP/S를 사용하여 Azure App Service에 앱 배포]를 참조하세요.

Spring Boot 샘플 프로젝트에 대한 자세한 내용은 [Spring Boot 시작하기]를 참조하세요.

자체 Spring Boot 응용 프로그램을 시작하는 데 도움이 필요하면 https://start.spring.io/에서 **Spring Initializr**를 참조하세요.

웹앱의 추가 설정 구성에 대한 자세한 내용은 [Azure App Service에서 웹앱 구성]을 참조하세요.

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Java 개발자용 Azure]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[Azure App Service에서 웹앱 구성]: /azure/app-service/web-sites-configure
[FTP/S를 사용하여 Azure App Service에 앱 배포]: https://docs.microsoft.com/azure/app-service/app-service-deploy-ftp
[체험판 Azure 계정{]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK(Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot 시작하기]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-web-app-on-azure/SB01.png
[SB02]: ./media/deploy-spring-boot-java-web-app-on-azure/SB02.png

[AZ01]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ01.png
[AZ02]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ02.png
[AZ03]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ03.png
[AZ04]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ04.png
[AZ05]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ05.png
[AZ06]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ06.png
[AZ07]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ07.png
[AZ08]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ08.png
[AZ09]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ09.png
[AZ10]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ10.png
