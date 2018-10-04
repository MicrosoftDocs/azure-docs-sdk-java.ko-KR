---
title: Azure Active Directory에 Spring Boot Starter를 사용하는 방법
description: Azure Active Directory 스타터에 Spring Boot Initializer 앱을 구성하는 방법을 알아봅니다.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 07/02/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: d3b6bdc4aaae79864d370c581585167cf3732160
ms.sourcegitcommit: bb7286fad75a2bb43e6ce1a8f1b09e701147c9f9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047187"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a>Azure Active Directory에 Spring Boot Starter를 사용하는 방법

## <a name="overview"></a>개요

이 문서에서는 Azure Active Directory(Azure AD)용 Spring Boot Starter를 사용하는 **[Spring Initializr]** 를 통한 앱 만들기를 보여 줍니다.

## <a name="prerequisites"></a>필수 조건

이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.
* [JDK(Java Development Kit)](http://www.oracle.com/technetwork/java/javase/downloads/), 버전 1.7 이상
* [Apache Maven](http://maven.apache.org/), 버전 3.0 이상

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Spring Initializr를 사용하여 사용자 지정 응용 프로그램 만들기

1. <https://start.spring.io/>로 이동합니다.

1. **Java**에서 **Maven** 프로젝트를 생성한다고 지정하고, 응용 프로그램에 대한 **그룹** 및 **아티팩트** 이름을 입력한 다음 Spring Initializr의 **정식 버전으로 전환**하는 링크를 클릭합니다.

   ![그룹 및 아티팩트 이름 지정][security-01]

1. **코어** 섹션으로 스크롤하여 **보안**에 대한 상자를 선택하고 **웹** 섹션에서 **웹** 확인란을 선택합니다.

   ![보안 및 웹 스타터를 선택합니다.][security-02]

1. **Azure** 섹션까지 아래로 스크롤하여 **Azure Active Directory**의 상자를 선택합니다.

   ![Azure Active Directory 스타터 선택][security-03]

1. 페이지 하단까지 스크롤하고 버튼을 클릭하여 **프로젝트를 생성**합니다.

   ![Spring Boot 프로젝트 생성][security-04]

1. 메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a>새 Azure Active Directory 인스턴스 만들기 및 구성

### <a name="create-the-active-directory-instance"></a>Active Directory 인스턴스 만들기

1. <https://portal.azure.com>에 로그인합니다.

1. **+ 새로 만들기**, **보안 + ID**, **Azure Active Directory**를 차례로 클릭합니다.

   ![새 Azure Active Directory 인스턴스 만들기][directory-01]

1. **조직 이름**과 **초기 도메인 이름**을 입력합니다. 사용자 디렉터리의 전체 URL을 복사합니다. 이는 자습서의 뒷부분에서 사용자 계정을 추가 하는 데 사용됩니다. (예: `wingtiptoysdirectory.onmicrosoft.com`) 완료되면 **만들기**를 클릭합니다.

   ![Azure Active Directory 이름 지정][directory-02]

1. Azure Portal의 상단 도구 모음에 있는 드롭다운 메뉴에서 새 Azure Active Directory를 선택합니다.

   ![Azure Active Directory 선택][directory-03]

1. 포털 메뉴에서 **Azure Active Directory**를 선택하고, **속성**을 클릭하여 **디렉터리 ID**를 복사합니다. 이 값은 이 자습서의 뒷부분에서 *application.properties* 파일을 구성하는 데 사용됩니다.

   ![Azure Active Directory ID 복사][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Spring Boot 앱에 대한 응용 프로그램 등록 추가

1. 포털 메뉴에서 **Azure Active Directory**를 선택하고 **개요**, **앱 등록**을 차례로 클릭합니다.

   ![새 앱 등록 추가][directory-04]

1. **새 응용 프로그램 등록** 을 클릭하고 응용 프로그램 **이름**을 지정한 다음 http://localhost:8080 **로그온 URL**에 사용하고 **만들기**를 클릭합니다.

   ![새 앱 등록 만들기][directory-05]

1. 응용 프로그램 등록을 만든 후 클릭합니다.

   ![앱 등록 선택][directory-06]

1. 앱 등록 페이지가 표시되면 **응용 프로그램 ID**를 복사합니다. 이 값은 이 자습서의 뒷부분에서 *application.properties* 파일을 구성하는 데 사용됩니다. **설정**을 클릭한 다음 **키**를 클릭합니다.

   ![앱 등록 키 만들기][directory-07]

1. **설명**을 추가하고 새 키에 대해 **기간**을 지정한 다음 **저장**을 클릭합니다. **저장** 아이콘을 클릭하면 키 값이 자동으로 입력되며, 나중에 이 자습서의 뒷부분에서 *application.properties* 파일을 구성하기 위해 키 값을 복사해 두어야 합니다. 이 값은 나중에 검색할 수 없습니다.

   ![앱 등록 키 매개 변수 지정][directory-08]

1. 앱 등록을 위한 기본 페이지에서 **설정**을 클릭하고 **필요한 권한**을 클릭합니다.

   ![앱 등록 필요 권한][directory-09]

1. **Windows Azure Active Directory**를 클릭합니다.

   ![Windows Azure Active Directory 선택][directory-10]

1. **로그인한 사용자로 디렉터리 액세스**와 **로그인 및 사용자 프로필 읽기**에 대한 상자를 선택하고 **저장**을 클릭합니다.

   ![액세스 권한 사용][directory-11]

1. **필요한 권한** 페이지에서 **사용 권한 부여**를 클릭하고 메시지가 표시되면 **예**를 클릭합니다.

   ![액세스 권한 부여][directory-12]

1. 앱 등록을 위한 기본 페이지에서 **설정**을 클릭하고 **회신 URL**을 클릭합니다.

   ![회신 URL 편집][directory-14]

1. "http://localhost:8080/login/oauth2/code/azure"을 새 회신 URL로 입력하고, **저장**을 클릭합니다.

   ![새 회신 URL 추가][directory-15]

1. 앱 등록에 대한 기본 페이지에서 **매니페스트**를 클릭하고 `oauth2AllowImplicitFlow` 매개 변수의 값을 `true`로 설정하고 **저장**을 클릭합니다.

   ![앱 매니페스트 구성][directory-16]

   > [!NOTE]
   > 
   > `oauth2AllowImplicitFlow` 매개 변수 및 다른 응용 프로그램 설정에 대한 자세한 내용은 [Azure Active Directory 응용 프로그램 매니페스트][AAD app manifest]를 참조하세요. 
   >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a>디렉터리에 사용자 계정을 추가하고 해당 계정을 그룹에 추가합니다

1. Active Directory의 **개요** 페이지에서 **사용자**를 클릭합니다.

   ![사용자 패널을 엽니다.][directory-17]

1. **사용자** 패널이 표시되면, **새 사용자**를 클릭합니다.

   ![새 사용자 계정 추가하기][directory-18]

1. **사용자** 패널이 표시되면, **이름** 및 **사용자 이름**을 입력합니다.

   ![사용자 계정 정보 입력][directory-19]

   > [!NOTE]
   > 
   > 사용자 이름을 입력하려면 자습서의 앞부분에 나온 디렉터리 URL을 지정해야 합니다. 예를 들어,
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. **그룹**을 클릭하고, 응용 프로그램에서 권한 부여를 위해 사용할 그룹을 선택한 다음 **선택**을 클릭합니다. (이 자습서의 목적에 따라 _사용자_ 그룹에 계정을 추가합니다.)

   ![사용자의 그룹을 선택합니다.][directory-20]

1. **암호 표시**를 클릭하여 암호를 복사합니다. 이는 이 자습서의 뒷부분에서 응용 프로그램에 로그인할 때 사용됩니다.

   ![암호 표시][directory-21]

1. **만들기**를 클릭하여 디렉터리에 새 사용자 계정을 추가합니다.

   ![새 사용자 계정 만들기][directory-22]

## <a name="configure-and-compile-your-spring-boot-application"></a>Spring Boot 응용 프로그램 구성 및 컴파일

1. 이 자습서의 앞부분에서 작성하고 다운로드한 프로젝트 아카이브의 파일을 디렉터리로 추출합니다.

1. 프로젝트에서 상위 폴더로 이동하고 텍스트 편집기에서 *pom.xml* 파일을 엽니다.

1. Spring OAuth2 보안의 종속성을 추가합니다. 예를 들면 다음과 같습니다.

   ```xml
   <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-oauth2-client</artifactId>
   </dependency>
   <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-oauth2-jose</artifactId>
   </dependency>
   ```

1. *pom.xml* 파일을 저장하고 닫습니다.

1. 프로젝트에서 *src/main/resources* 폴더로 이동하고 텍스트 편집기에서 *application.properties* 파일을 엽니다.

1. 이전에 생성한 값을 사용하여 앱 등록을 위한 설정을 지정합니다. 예를 들어,

   ```yaml
   # Specifies your Active Directory ID:
   azure.activedirectory.tenant-id=22222222-2222-2222-2222-222222222222

   # Specifies your App Registration's Application ID:
   spring.security.oauth2.client.registration.azure.client-id=11111111-1111-1111-1111-1111111111111111

   # Specifies your App Registration's secret key:
   spring.security.oauth2.client.registration.azure.client-secret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authorization:
   azure.activedirectory.active-directory-groups=Users
   ```
   위치:

   | 매개 변수 | 설명 |
   |---|---|
   | `azure.activedirectory.tenant-id` | 앞에 나온 Active Directory의 **디렉터리 ID** 포함합니다. |
   | `spring.security.oauth2.client.registration.azure.client-id` | 앞에서 완료한 앱 등록의 **응용프로그램 ID**를 포함합니다. |
   | `spring.security.oauth2.client.registration.azure.client-secret` | 앞에서 완료한 앱 등록 키의 **값**을 포함합니다. |
   | `azure.activedirectory.active-directory-groups` | 권한 부여에 사용할 Active Directory 그룹 목록을 포함합니다. |

   > [!NOTE]
   > 
   > *application.properties* 파일에서 사용할 수 있는 값의 전체 목록은 GitHub에서 [Azure Active Directory Spring Boot 샘플][AAD Spring Boot Sample]을 참조합니다.
   >

1. *application.properties* 파일을 저장하고 닫습니다.

1. 응용 프로그램에 대해 Java 소스 폴더에 이름이 *controller*인 폴더를 만듭니다. 예를 들어 *src/main/java/com/wingtiptoys/security/controller*입니다.

1. *controller* 폴더에 이름이 *HelloController.java*인 새 Java 파일을 만들고 텍스트 편집기에서 엽니다.

1. 다음 코드를 입력한 다음 저장하고 파일을 닫습니다.

   ```java
   package com.wingtiptoys.security;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.security.access.prepost.PreAuthorize;
   import org.springframework.security.oauth2.client.OAuth2AuthorizedClient;
   import org.springframework.security.oauth2.client.authentication.OAuth2AuthenticationToken;
   import org.springframework.ui.Model;

   @RestController
   public class HelloController {
      @Autowired
      @PreAuthorize("hasRole('Users')")
      @RequestMapping("/")
      public String helloWorld() {
         return "Hello World!";
      }
   }
   ```
   > [!NOTE]
   > 
   > `@PreAuthorize("hasRole('')")` 메서드에 지정한 그룹 이름은 *application.properties* 파일의 `azure.activedirectory.active-directory-groups` 필드에 지정한 그룹 중 하나를 포함해야 합니다.
   >

   > [!NOTE]
   > 
   > 다른 요청 매핑에 대한 다른 권한 부여 설정을 지정할 수 있습니다. 예를 들어:
   >
   > ``` java
   > public class HelloController {
   >    @Autowired
   >    @PreAuthorize("hasRole('Users')")
   >    @RequestMapping("/")
   >    public String helloWorld() {
   >       return "Hello Users!";
   >    }
   >    @PreAuthorize("hasRole('Group1')")
   >    @RequestMapping("/Group1")
   >    public String groupOne() {
   >       return "Hello Group 1 Users!";
   >    }
   >    @PreAuthorize("hasRole('Group2')")
   >    @RequestMapping("/Group2")
   >    public String groupTwo() {
   >       return "Hello Group 2 Users!";
   >    }
   > }
   > ```
   >    

1. 응용 프로그램에 대해 Java 소스 폴더에 이름이 *security*인 폴더를 만듭니다. 예를 들어 *src/main/java/com/wingtiptoys/security/security*입니다.

1. *security* 폴더에 이름이 *WebSecurityConfig.java*인 새 Java 파일을 만들고 텍스트 편집기에서 엽니다.

1. 다음 코드를 입력한 다음 저장하고 파일을 닫습니다.

    ```java
    package com.wingtiptoys.security;

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
    import org.springframework.security.config.annotation.web.builders.HttpSecurity;
    import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
    import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
    import org.springframework.security.oauth2.client.oidc.userinfo.OidcUserRequest;
    import org.springframework.security.oauth2.client.userinfo.OAuth2UserService;
    import org.springframework.security.oauth2.core.oidc.user.OidcUser;

    @EnableWebSecurity
    @EnableGlobalMethodSecurity(prePostEnabled = true)
    public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
        @Autowired
        private OAuth2UserService<OidcUserRequest, OidcUser> oidcUserService;

        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http
                .authorizeRequests()
                .anyRequest().authenticated()
                .and()
                .oauth2Login()
                .userInfoEndpoint()
                .oidcUserService(oidcUserService);
        }
    }
    ```

## <a name="build-and-test-your-app"></a>앱 빌드 및 테스트

1. 명령 프롬프트를 열고 디렉터리를 앱의 *pom.xml* 파일이 위치한 폴더로 변경합니다. 

1. Maven을 사용하여 Spring Boot 응용 프로그램을 빌드하고 실행합니다. 예:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![사용 중인 응용 프로그램 빌드][build-application]

1. 응용프로그램이 Maven에서 빌드 및 시작되고 나면, <http://localhost:8080>을 웹 브라우저에서 엽니다. 사용자 이름 및 암호 입력 메시지가 나타납니다.

   ![응용프로그램에 로그인][application-login]

   > [!NOTE]
   > 
   > 새 사용자 계정에서 처음 로그인한 경우라면, 암호를 변경하라는 메시지가 표시될 수 있습니다.
   > 
   > ![암호 변경][update-password]
   > 

1. 사용자가 성공적으로 로그인한 후 컨트롤러에서 샘플 "Hello World" 텍스트가 표시됩니다.

   ![로그인 성공][hello-world]

   > [!NOTE]
   > 
   > 승인되지 않은 사용자 계정인 경우 **HTTP 403 Unauthorized** 메시지가 나타납니다.
   >

## <a name="next-steps"></a>다음 단계

Azure Active Directory 사용에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Azure Active Directory 설명서].

Azure에서 Spring Boot 응용 프로그램을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Azure App Service에 Spring Boot 응용 프로그램 배포](deploy-spring-boot-java-web-app-on-azure.md)

* [Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 실행](deploy-spring-boot-java-app-on-kubernetes.md)

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.

**[Spring Framework]** 는 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만드는 데 도움이 되는 오픈 소스 솔루션입니다. 해당 플랫폼을 기반으로 하여 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 응용 프로그램을 만드는 간단한 방법을 제공합니다. Spring Boot을 시작하는 개발자를 도우려면 <https://github.com/spring-guides/>에서 몇 가지 샘플 Spring Boot 패키지를 사용할 있습니다. 기본 Spring Boot 프로젝트 목록에서 선택하는 것 외에도 **[Spring Initializr]** 를 통해 사용자 지정 Spring Boot 응용 프로그램을 만들기 시작하는 개발자에게 도움을 줍니다.

더 자세한 예제는 Github [Azure Active Directory Spring Boot 샘플][AAD Spring Boot Sample]을 참조합니다.

<!-- URL List -->

[Azure Active Directory 설명서]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Java 개발자용 Azure]: /java/azure/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[AAD Spring Boot Sample]: https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-backend-sample

<!-- IMG List -->

[security-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-01.png
[security-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-02.png
[security-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-03.png
[security-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-04.png

[directory-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-01.png
[directory-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-02.png
[directory-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-03.png
[directory-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-04.png
[directory-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-05.png
[directory-06]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-06.png
[directory-07]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-07.png
[directory-08]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-08.png
[directory-09]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-09.png
[directory-10]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-10.png
[directory-11]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-11.png
[directory-12]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-12.png
[directory-13]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-13.png
[directory-14]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-14.png
[directory-15]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-15.png
[directory-16]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-16.png
[directory-17]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-17.png
[directory-18]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-18.png
[directory-19]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-19.png
[directory-20]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-20.png
[directory-21]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-21.png
[directory-22]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-22.png

[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
[update-password]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/update-password.png
