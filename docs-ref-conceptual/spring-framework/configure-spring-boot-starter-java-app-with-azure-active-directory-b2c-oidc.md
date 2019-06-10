---
title: Azure Active Directory B2C용 Spring Boot Starter 사용 방법
description: Azure Active Directory B2C 스타터를 사용하여 Spring Boot Initializer 앱을 구성하는 방법을 알아봅니다.
services: active-directory-b2c
documentationcenter: java
author: panli
manager: kevinzha
editor: panli
ms.assetid: ''
ms.author: panli
ms.date: 02/28/2019
ms.devlang: java
ms.service: active-directory-b2c
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 21aa6c812a519d686356851a57f00688d9a24fa4
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65625716"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory-b2c"></a>자습서: Azure Active Directory B2C용 Spring Boot Starter를 사용하여 Java 웹앱을 보호합니다.

## <a name="overview"></a>개요

이 문서에서는 Azure AD(Azure Active Directory)용 Spring Boot Starter를 사용하는 [Spring Initializr](https://start.spring.io/)를 통한 Java 앱 만들기를 보여줍니다.

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Spring Initializr를 사용하여 Java 애플리케이션 만들기
> * Azure Active Directory B2C 구성
> * Spring Boot 클래스 및 주석을 사용하여 애플리케이션 보호
> * Java 애플리케이션 빌드 및 테스트

Azure 구독이 아직 없는 경우 시작하기 전에 [체험 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.

## <a name="prerequisites"></a>필수 조건

이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.

* 지원되는 JDK(Java Development Kit) Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.
* [Apache Maven](http://maven.apache.org/), 버전 3.0 이상

## <a name="create-an-app-using-spring-initializr"></a>Spring Initialzr를 사용하여 앱 만들기

1. <https://start.spring.io/>로 이동합니다.

2. **Java**를 사용하여 **Maven** 프로젝트를 생성하도록 지정하고 애플리케이션의 **그룹** 및 **아티팩트** 이름을 입력한 다음, Spring Initializr의 **웹** 및 **보안**  모듈을 선택합니다.

   ![그룹 및 아티팩트 이름 지정](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/SI.png)


3. `Generate Project`를 클릭하고 메시지가 표시되면 프로젝트를 로컬 컴퓨터의 경로에 다운로드합니다.

## <a name="create-azure-active-directory-instance"></a>Azure Active Directory 인스턴스 만들기

### <a name="create-the-active-directory-instance"></a>Active Directory 인스턴스 만들기

1. <https://portal.azure.com>에 로그인합니다.

2. **+리소스 만들기**, **ID**, **Azure Active Directory B2C**를 차례로 클릭합니다.

   ![새 Azure Active Directory B2C 인스턴스 만들기](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ1.png)

3. **조직 이름** 및 **초기 도메인 이름**을 입력하고 **도메인 이름**을 `${your-tenant-name}`으로 기록하고 **만들기**를 클릭합니다.

   ![B2C 테넌트 이름 가져오기](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ5.png)

4. Azure portal 도구 모음의 오른쪽 상단에서 계정 이름을 선택한 다음 **디렉터리 전환**을 클릭합니다.

   ![Azure Active Directory 선택](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ2.png)

5. 드롭다운 메뉴에서 새 Azure Active Directory를 선택합니다.

   ![Azure Active Directory 선택](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ3.png)

6. `b2c`를 검색하고 `Azure AD B2C` 서비스를 클릭합니다.

   ![Azure Active Directory B2C 인스턴스 찾기](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ4.png)

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Spring Boot 앱에 대한 애플리케이션 등록 추가

1. 포털 메뉴에서 **Azure AD B2C**를 선택하고 **애플리케이션**, **추가**를 차례로 클릭합니다.

   ![새 앱 등록 추가](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C1.png)

2. 애플리케이션 **이름**을 지정하고 **회신 URL**에 대해 `http://localhost:8080/home`을 추가하고 **애플리케이션 ID**를 `${your-client-id}`로 기록한 다음, **저장**을 클릭합니다.

   ![애플리케이션 회신 URL 추가](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C2.png)

3. 애플리케이션에서 **키**를 선택하고 **키 생성**을 클릭하여 `${your-client-secret}`을 생성한 다음, **저장**을 클릭합니다.

4. 왼쪽에서 **사용자 흐름**을 선택한 다음, **새 사용자 흐름**을 **클릭**합니다.

   ![사용자 흐름 만들기](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C3.png)

5. **가입 또는 로그인**, **프로필 편집** 및 **암호 재설정**을 선택하여 각각 사용자 흐름을 만듭니다. 사용자 흐름 **이름** 및 **사용자 특성 및 클레임**을 지정하고 **만들기**를 클릭합니다.

   ![사용자 흐름 구성](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C4.png)

## <a name="configure-and-compile-your-app"></a>앱 구성 및 컴파일

1. 이 자습서의 앞부분에서 작성하고 다운로드한 프로젝트 아카이브의 파일을 디렉터리로 추출합니다.

2. 프로젝트에서 상위 폴더로 이동하고 텍스트 편집기에서 `pom.xml`Maven 프로젝트 파일을 엽니다.

3. Spring OAuth2 보안의 종속성을 `pom.xml`에 추가합니다.

   ```xml
   <dependency>
       <groupId>com.microsoft.azure</groupId>
       <artifactId>azure-active-directory-b2c-spring-boot-starter</artifactId>
       <version>2.1.6.M2</version>
   </dependency>
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-thymeleaf</artifactId>
   </dependency>
   <dependency>
       <groupId>org.thymeleaf.extras</groupId>
       <artifactId>thymeleaf-extras-springsecurity5</artifactId>
   </dependency>
   ```

4. *pom.xml* 파일을 저장하고 닫습니다.

5. 프로젝트에서 *src/main/resources* 폴더로 이동하고 텍스트 편집기에서 *application.yml* 파일을 엽니다.

6. 이전에 생성한 값을 사용하여 앱 등록을 위한 설정을 지정합니다. 예를 들어,

   ```yaml
   azure:
     activedirectory:
       b2c:
         tenant: ${your-tenant-name}
         client-id: ${your-client-id}
         client-secret: ${your-client-secret}
         reply-url: ${your-reply-url-from-aad} # should be absolute url.
         logout-success-url: ${you-logout-success-url}
         user-flows:
           sign-up-or-sign-in: ${your-sign-up-or-in-user-flow}
           profile-edit: ${your-profile-edit-user-flow}     # optional
           password-reset: ${your-password-reset-user-flow} # optional
   ```
   위치:

   | 매개 변수 | 설명 |
   |---|---|
   | `azure.activedirectory.b2c.tenant` | 앞에서 지정한 AD B2C의 `${your-tenant-name`을 포함합니다. |
   | `azure.activedirectory.b2c.client-id` | 앞에서 완료한 애플리케이션의 `${your-client-id}`를 포함합니다. |
   | `azure.activedirectory.b2c.client-secret` | 앞에서 완료한 애플리케이션의 `${your-client-secret}`을 포함합니다. |
   | `azure.activedirectory.b2c.reply-url` | 앞에서 완료한 애플리케이션의 **회신 URL** 중 하나를 포함합니다. |
   | `azure.activedirectory.b2c.logout-success-url` | 애플리케이션이 성공적으로 로그아웃하면 URL을 지정합니다. |
   | `azure.activedirectory.b2c.user-flows` | 앞에서 완료한 사용자 흐름의 이름을 포함합니다.

   > [!NOTE]
   > 
   > *application.yml* 파일에서 사용할 수 있는 값의 전체 목록은 GitHub의 [Azure Active Directory B2C Spring Boot 샘플][AAD B2C Spring Boot 샘플]을 참조하세요.
   >

7. *application.yml* 파일을 저장하고 닫습니다.

8. 애플리케이션용 Java 소스 폴더에 *컨트롤러*라는 폴더를 만듭니다.

9. *controller* 폴더에 이름이 *HelloController.java*인 새 Java 파일을 만들고 텍스트 편집기에서 엽니다.

10. 다음 코드를 입력한 다음 저장하고 파일을 닫습니다.

    ```java
    package sample.aad.controller;
    
    import org.springframework.security.oauth2.client.authentication.OAuth2AuthenticationToken;
    import org.springframework.security.oauth2.core.user.OAuth2User;
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.Model;
    import org.springframework.web.bind.annotation.GetMapping;
    
    @Controller
    public class WebController {
    
        private void initializeModel(Model model, OAuth2AuthenticationToken token) {
            if (token != null) {
                final OAuth2User user = token.getPrincipal();
    
                model.addAttribute("grant_type", user.getAuthorities());
                model.addAllAttributes(user.getAttributes());
            }
        }
    
        @GetMapping(value = "/")
        public String index(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "home";
        }
    
        @GetMapping(value = "/greeting")
        public String greeting(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "greeting";
        }
    
        @GetMapping(value = "/home")
        public String home(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "home";
        }
    }
    ```

11. 애플리케이션용 Java 소스 폴더에 *보안*이라는 폴더를 만듭니다.

12. *security* 폴더에 이름이 *WebSecurityConfig.java*인 새 Java 파일을 만들고 텍스트 편집기에서 엽니다.

13. 다음 코드를 입력한 다음 저장하고 파일을 닫습니다.

    ```java
    package sample.aad.security;
    
    import com.microsoft.azure.spring.autoconfigure.b2c.AADB2COidcLoginConfigurer;
    import org.springframework.security.config.annotation.web.builders.HttpSecurity;
    import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
    import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
    
    @EnableWebSecurity
    public class WebSecurityConfiguration extends WebSecurityConfigurerAdapter {
    
        private final AADB2COidcLoginConfigurer configurer;
    
        public WebSecurityConfiguration(AADB2COidcLoginConfigurer configurer) {
            this.configurer = configurer;
        }
    
        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http
                    .authorizeRequests()
                    .anyRequest()
                    .authenticated()
                    .and()
                    .apply(configurer)
            ;
        }
    }
    ```
14. [Azure AD B2C Spring Boot 샘플](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates)에서 `greeting.html` 및 `home.html`을 복사하고 `${your-profile-edit-user-flow}` 및 `${your-password-reset-user-flow}`를 앞에서 완료한 사용자 흐름 이름으로 각각 바꿉니다.

## <a name="build-and-test-your-app"></a>앱 빌드 및 테스트

1. 명령 프롬프트를 열고 디렉터리를 앱의 *pom.xml* 파일이 위치한 폴더로 변경합니다.

2. Maven을 사용하여 Spring Boot 애플리케이션을 빌드하고 실행합니다. 예:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

3. 애플리케이션이 Maven에 의해 빌드되고 시작된 후 웹 브라우저에서 <http://localhost:8080/>을 엽니다. 로그인 페이지로 이동됩니다.

   ![로그인 페이지](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO1.png)

4. `${your-sign-up-or-in}` 사용자 흐름의 이름이 포함된 링크를 클릭합니다. 인증 프로세스를 시작하기 위해 Azure AD B2C로 이동됩니다.

   ![Azure AD B2C 로그인](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO2.png)

4. 성공적으로 로그인한 후 브라우저에서 샘플 `home page`가 표시됩니다.

   ![로그인 성공](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO3.png)

## <a name="summary"></a>요약

이 자습서에서는 Azure Active Directory B2C 스타터를 사용하여 새 Java 웹 애플리케이션을 만들고, 새로 구성한 Azure AD B2C 테넌트에 새 애플리케이션을 등록하고, 애플리케이션이 웹을 보호하기 위한 Spring 주석 및 클래스를 사용하도록 구성합니다.

## <a name="next-steps"></a>다음 단계

Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.

> [!div class="nextstepaction"]
> [Azure의 Spring](/java/azure/spring-framework)
