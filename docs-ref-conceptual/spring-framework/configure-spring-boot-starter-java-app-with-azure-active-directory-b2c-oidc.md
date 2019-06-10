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
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory-b2c"></a><span data-ttu-id="a0dc6-103">자습서: Azure Active Directory B2C용 Spring Boot Starter를 사용하여 Java 웹앱을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-103">Tutorial: Secure a Java web app using the Spring Boot Starter for Azure Active Directory B2C.</span></span>

## <a name="overview"></a><span data-ttu-id="a0dc6-104">개요</span><span class="sxs-lookup"><span data-stu-id="a0dc6-104">Overview</span></span>

<span data-ttu-id="a0dc6-105">이 문서에서는 Azure AD(Azure Active Directory)용 Spring Boot Starter를 사용하는 [Spring Initializr](https://start.spring.io/)를 통한 Java 앱 만들기를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-105">This article demonstrates creating a Java app with the [Spring Initializr](https://start.spring.io/) that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0dc6-106">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a0dc6-107">Spring Initializr를 사용하여 Java 애플리케이션 만들기</span><span class="sxs-lookup"><span data-stu-id="a0dc6-107">Create a Java application using the Spring Initializr</span></span>
> * <span data-ttu-id="a0dc6-108">Azure Active Directory B2C 구성</span><span class="sxs-lookup"><span data-stu-id="a0dc6-108">Configure Azure Active Directory B2C</span></span>
> * <span data-ttu-id="a0dc6-109">Spring Boot 클래스 및 주석을 사용하여 애플리케이션 보호</span><span class="sxs-lookup"><span data-stu-id="a0dc6-109">Secure the application with Spring Boot classes and annotations</span></span>
> * <span data-ttu-id="a0dc6-110">Java 애플리케이션 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a0dc6-110">Build and test your Java application</span></span>

<span data-ttu-id="a0dc6-111">Azure 구독이 아직 없는 경우 시작하기 전에 [체험 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0dc6-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a0dc6-112">Prerequisites</span></span>

<span data-ttu-id="a0dc6-113">이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-113">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="a0dc6-114">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="a0dc6-114">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="a0dc6-115">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-115">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="a0dc6-116">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="a0dc6-116">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="a0dc6-117">Spring Initialzr를 사용하여 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="a0dc6-117">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="a0dc6-118"><https://start.spring.io/>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-118">Browse to <https://start.spring.io/>.</span></span>

2. <span data-ttu-id="a0dc6-119">**Java**를 사용하여 **Maven** 프로젝트를 생성하도록 지정하고 애플리케이션의 **그룹** 및 **아티팩트** 이름을 입력한 다음, Spring Initializr의 **웹** 및 **보안**  모듈을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-119">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then select the **Web** and **Security** module of the Spring Initializr.</span></span>

   ![그룹 및 아티팩트 이름 지정](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/SI.png)


3. <span data-ttu-id="a0dc6-121">`Generate Project`를 클릭하고 메시지가 표시되면 프로젝트를 로컬 컴퓨터의 경로에 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-121">Click `Generate Project`, download the project to a path on your local computer when prompted.</span></span>

## <a name="create-azure-active-directory-instance"></a><span data-ttu-id="a0dc6-122">Azure Active Directory 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="a0dc6-122">Create Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="a0dc6-123">Active Directory 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="a0dc6-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="a0dc6-124"><https://portal.azure.com>에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-124">Log into <https://portal.azure.com>.</span></span>

2. <span data-ttu-id="a0dc6-125">**+리소스 만들기**, **ID**, **Azure Active Directory B2C**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-125">Click **+Create a resource**, then **Identity**, and then **Azure Active Directory B2C**.</span></span>

   ![새 Azure Active Directory B2C 인스턴스 만들기](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ1.png)

3. <span data-ttu-id="a0dc6-127">**조직 이름** 및 **초기 도메인 이름**을 입력하고 **도메인 이름**을 `${your-tenant-name}`으로 기록하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-127">Enter your **Organization name** and your **Initial domain name**, record the **domain name** as your `${your-tenant-name}` and click **Create**.</span></span>

   ![B2C 테넌트 이름 가져오기](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ5.png)

4. <span data-ttu-id="a0dc6-129">Azure portal 도구 모음의 오른쪽 상단에서 계정 이름을 선택한 다음 **디렉터리 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-129">Select your account name on the top-right of the Azure portal toolbar, then click **Switch directory**.</span></span>

   ![Azure Active Directory 선택](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ2.png)

5. <span data-ttu-id="a0dc6-131">드롭다운 메뉴에서 새 Azure Active Directory를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-131">Select your new Azure Active Directory from the drop-down menu.</span></span>

   ![Azure Active Directory 선택](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ3.png)

6. <span data-ttu-id="a0dc6-133">`b2c`를 검색하고 `Azure AD B2C` 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-133">Search `b2c` and click `Azure AD B2C` service.</span></span>

   ![Azure Active Directory B2C 인스턴스 찾기](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ4.png)

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="a0dc6-135">Spring Boot 앱에 대한 애플리케이션 등록 추가</span><span class="sxs-lookup"><span data-stu-id="a0dc6-135">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="a0dc6-136">포털 메뉴에서 **Azure AD B2C**를 선택하고 **애플리케이션**, **추가**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-136">Select **Azure AD B2C** from the portal menu, click **Applications**, and then click **Add**.</span></span>

   ![새 앱 등록 추가](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C1.png)

2. <span data-ttu-id="a0dc6-138">애플리케이션 **이름**을 지정하고 **회신 URL**에 대해 `http://localhost:8080/home`을 추가하고 **애플리케이션 ID**를 `${your-client-id}`로 기록한 다음, **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-138">Specify your application **Name**, add `http://localhost:8080/home` for the **Reply URL**, record the **Application ID** as your `${your-client-id}` and then click **Save**.</span></span>

   ![애플리케이션 회신 URL 추가](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C2.png)

3. <span data-ttu-id="a0dc6-140">애플리케이션에서 **키**를 선택하고 **키 생성**을 클릭하여 `${your-client-secret}`을 생성한 다음, **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-140">Select **Keys** from your application, click **Generate key** to generate `${your-client-secret}` and then **Save**.</span></span>

4. <span data-ttu-id="a0dc6-141">왼쪽에서 **사용자 흐름**을 선택한 다음, **새 사용자 흐름**을 **클릭**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-141">Select **User flows** on your left, and then **Click** \*\*New user flow \*\*.</span></span>

   ![사용자 흐름 만들기](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C3.png)

5. <span data-ttu-id="a0dc6-143">**가입 또는 로그인**, **프로필 편집** 및 **암호 재설정**을 선택하여 각각 사용자 흐름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-143">Choose **Sign up or in**, **Profile editing** and **Password reset** to create user flows respectively.</span></span> <span data-ttu-id="a0dc6-144">사용자 흐름 **이름** 및 **사용자 특성 및 클레임**을 지정하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-144">Specify your user flow **Name** and **User attributes and claims**, click **Create**.</span></span>

   ![사용자 흐름 구성](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C4.png)

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="a0dc6-146">앱 구성 및 컴파일</span><span class="sxs-lookup"><span data-stu-id="a0dc6-146">Configure and compile your app</span></span>

1. <span data-ttu-id="a0dc6-147">이 자습서의 앞부분에서 작성하고 다운로드한 프로젝트 아카이브의 파일을 디렉터리로 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-147">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

2. <span data-ttu-id="a0dc6-148">프로젝트에서 상위 폴더로 이동하고 텍스트 편집기에서 `pom.xml`Maven 프로젝트 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-148">Navigate to the parent folder for your project, and open the `pom.xml` Maven project file in a text editor.</span></span>

3. <span data-ttu-id="a0dc6-149">Spring OAuth2 보안의 종속성을 `pom.xml`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-149">Add the dependencies for Spring OAuth2 security to the `pom.xml`:</span></span>

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

4. <span data-ttu-id="a0dc6-150">*pom.xml* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-150">Save and close the *pom.xml* file.</span></span>

5. <span data-ttu-id="a0dc6-151">프로젝트에서 *src/main/resources* 폴더로 이동하고 텍스트 편집기에서 *application.yml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-151">Navigate to the *src/main/resources* folder in your project and open the *application.yml* file in a text editor.</span></span>

6. <span data-ttu-id="a0dc6-152">이전에 생성한 값을 사용하여 앱 등록을 위한 설정을 지정합니다. 예를 들어,</span><span class="sxs-lookup"><span data-stu-id="a0dc6-152">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

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
   <span data-ttu-id="a0dc6-153">위치:</span><span class="sxs-lookup"><span data-stu-id="a0dc6-153">Where:</span></span>

   | <span data-ttu-id="a0dc6-154">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a0dc6-154">Parameter</span></span> | <span data-ttu-id="a0dc6-155">설명</span><span class="sxs-lookup"><span data-stu-id="a0dc6-155">Description</span></span> |
   |---|---|
   | `azure.activedirectory.b2c.tenant` | <span data-ttu-id="a0dc6-156">앞에서 지정한 AD B2C의 `${your-tenant-name`을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-156">Contains your AD B2C's `${your-tenant-name` from earlier.</span></span> |
   | `azure.activedirectory.b2c.client-id` | <span data-ttu-id="a0dc6-157">앞에서 완료한 애플리케이션의 `${your-client-id}`를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-157">Contains the `${your-client-id}` from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.client-secret` | <span data-ttu-id="a0dc6-158">앞에서 완료한 애플리케이션의 `${your-client-secret}`을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-158">Contains the `${your-client-secret}` from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.reply-url` | <span data-ttu-id="a0dc6-159">앞에서 완료한 애플리케이션의 **회신 URL** 중 하나를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-159">Contains one of the **Reply URL** from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.logout-success-url` | <span data-ttu-id="a0dc6-160">애플리케이션이 성공적으로 로그아웃하면 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-160">Specify the URL when your application logout successfully.</span></span> |
   | `azure.activedirectory.b2c.user-flows` | <span data-ttu-id="a0dc6-161">앞에서 완료한 사용자 흐름의 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-161">Contains the name of the user flows that you completed earlier.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="a0dc6-162">*application.yml* 파일에서 사용할 수 있는 값의 전체 목록은 GitHub의 [Azure Active Directory B2C Spring Boot 샘플][AAD B2C Spring Boot 샘플]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-162">For a full list of values that are available in your *application.yml* file, see the [Azure Active Directory B2C Spring Boot Sample][AAD B2C Spring Boot Sample] on GitHub.</span></span>
   >

7. <span data-ttu-id="a0dc6-163">*application.yml* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-163">Save and close the *application.yml* file.</span></span>

8. <span data-ttu-id="a0dc6-164">애플리케이션용 Java 소스 폴더에 *컨트롤러*라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-164">Create a folder named *controller* in the Java source folder for your application.</span></span>

9. <span data-ttu-id="a0dc6-165">*controller* 폴더에 이름이 *HelloController.java*인 새 Java 파일을 만들고 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-165">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

10. <span data-ttu-id="a0dc6-166">다음 코드를 입력한 다음 저장하고 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-166">Enter the following code, then save and close the file:</span></span>

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

11. <span data-ttu-id="a0dc6-167">애플리케이션용 Java 소스 폴더에 *보안*이라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-167">Create a folder named *security* in the Java source folder for your application.</span></span>

12. <span data-ttu-id="a0dc6-168">*security* 폴더에 이름이 *WebSecurityConfig.java*인 새 Java 파일을 만들고 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-168">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

13. <span data-ttu-id="a0dc6-169">다음 코드를 입력한 다음 저장하고 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-169">Enter the following code, then save and close the file:</span></span>

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
14. <span data-ttu-id="a0dc6-170">[Azure AD B2C Spring Boot 샘플](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates)에서 `greeting.html` 및 `home.html`을 복사하고 `${your-profile-edit-user-flow}` 및 `${your-password-reset-user-flow}`를 앞에서 완료한 사용자 흐름 이름으로 각각 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-170">Copy the `greeting.html` and `home.html` from [Azure AD B2C Spring Boot Sample](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates), and replace the `${your-profile-edit-user-flow}` and `${your-password-reset-user-flow}` with your user flow name respectively that completed earlier.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="a0dc6-171">앱 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="a0dc6-171">Build and test your app</span></span>

1. <span data-ttu-id="a0dc6-172">명령 프롬프트를 열고 디렉터리를 앱의 *pom.xml* 파일이 위치한 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-172">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

2. <span data-ttu-id="a0dc6-173">Maven을 사용하여 Spring Boot 애플리케이션을 빌드하고 실행합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="a0dc6-173">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

3. <span data-ttu-id="a0dc6-174">애플리케이션이 Maven에 의해 빌드되고 시작된 후 웹 브라우저에서 <http://localhost:8080/>을 엽니다. 로그인 페이지로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-174">After your application is built and started by Maven, open <http://localhost:8080/> in a web browser; you should be redirected to login page.</span></span>

   ![로그인 페이지](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO1.png)

4. <span data-ttu-id="a0dc6-176">`${your-sign-up-or-in}` 사용자 흐름의 이름이 포함된 링크를 클릭합니다. 인증 프로세스를 시작하기 위해 Azure AD B2C로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-176">Click linke with name of `${your-sign-up-or-in}` user flow, you should be rediected Azure AD B2C to start the authentication process.</span></span>

   ![Azure AD B2C 로그인](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO2.png)

4. <span data-ttu-id="a0dc6-178">성공적으로 로그인한 후 브라우저에서 샘플 `home page`가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-178">After you have logged in successfully, you should see the sample `home page` from the browser,</span></span>

   ![로그인 성공](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO3.png)

## <a name="summary"></a><span data-ttu-id="a0dc6-180">요약</span><span class="sxs-lookup"><span data-stu-id="a0dc6-180">Summary</span></span>

<span data-ttu-id="a0dc6-181">이 자습서에서는 Azure Active Directory B2C 스타터를 사용하여 새 Java 웹 애플리케이션을 만들고, 새로 구성한 Azure AD B2C 테넌트에 새 애플리케이션을 등록하고, 애플리케이션이 웹을 보호하기 위한 Spring 주석 및 클래스를 사용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-181">In this tutorial, you created a new Java web application using the Azure Active Directory B2C starter, configured a new Azure AD B2C tenant and registered a new application in it, and then configured your application to use the Spring annotations and classes to protect the web app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0dc6-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0dc6-182">Next steps</span></span>

<span data-ttu-id="a0dc6-183">Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="a0dc6-183">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a0dc6-184">Azure의 Spring</span><span class="sxs-lookup"><span data-stu-id="a0dc6-184">Spring on Azure</span></span>](/java/azure/spring-framework)
