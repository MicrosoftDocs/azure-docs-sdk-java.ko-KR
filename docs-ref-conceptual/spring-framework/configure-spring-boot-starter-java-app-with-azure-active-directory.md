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
ms.date: 11/21/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 89e294fa739b59f87667f901e914fd5f050b5b8c
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338777"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="224bd-103">자습서: Azure Active Directory용 Spring Boot Starter를 사용하여 Java 웹앱 보호</span><span class="sxs-lookup"><span data-stu-id="224bd-103">Tutorial: Secure a Java web app using the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="224bd-104">개요</span><span class="sxs-lookup"><span data-stu-id="224bd-104">Overview</span></span>

<span data-ttu-id="224bd-105">이 문서에서는 Azure Active Directory(Azure AD)용 Spring Boot Starter를 사용하는 **[Spring Initializr]** 를 통한 Java 앱 만들기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-105">This article demonstrates creating a Java app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="224bd-106">이 자습서에서는 다음 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="224bd-107">Spring Initializr를 사용하여 Java 애플리케이션 만들기</span><span class="sxs-lookup"><span data-stu-id="224bd-107">Create a Java application using the Spring Initializr</span></span>
> * <span data-ttu-id="224bd-108">Azure Active Directory 구성</span><span class="sxs-lookup"><span data-stu-id="224bd-108">Configure Azure Active Directory</span></span>
> * <span data-ttu-id="224bd-109">Spring Boot 클래스 및 주석을 사용하여 애플리케이션 보호</span><span class="sxs-lookup"><span data-stu-id="224bd-109">Secure the application with Spring Boot classes and annotations</span></span>
> * <span data-ttu-id="224bd-110">Java 애플리케이션 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="224bd-110">Build and test your Java application</span></span>

<span data-ttu-id="224bd-111">Azure 구독이 아직 없는 경우 시작하기 전에 [체험 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="224bd-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="224bd-112">Prerequisites</span></span>

<span data-ttu-id="224bd-113">이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-113">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="224bd-114">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="224bd-114">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="224bd-115">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="224bd-115">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="224bd-116">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="224bd-116">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="224bd-117">Spring Initialzr를 사용하여 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="224bd-117">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="224bd-118"><https://start.spring.io/>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-118">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="224bd-119">**Java**에서 **Maven** 프로젝트를 생성한다고 지정하고, 응용 프로그램에 대한 **그룹** 및 **아티팩트** 이름을 입력한 다음 Spring Initializr의 **정식 버전으로 전환**하는 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-119">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![그룹 및 아티팩트 이름 지정][create-spring-app-01]

1. <span data-ttu-id="224bd-121">**핵심** 섹션으로 스크롤하여 **보안**에 대한 확인란을 선택하고, **웹** 섹션에서 **웹**에 대한 확인란을 선택한 다음 **Azure** 섹션으로 스크롤해서 **Azure Active Directory**의 확인란을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="224bd-121">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**, then scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![보안, 웹 및 Azure Active Directory 스타터를 선택합니다][create-spring-app-02]

1. <span data-ttu-id="224bd-123">페이지 상단이나 하단까지 스크롤하고 버튼을 클릭하여 **프로젝트를 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-123">Scroll to the top or bottom of the page and click the button to **Generate Project**.</span></span>

   ![Spring Boot 프로젝트 생성][create-spring-app-03]

1. <span data-ttu-id="224bd-125">메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-125">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-azure-active-directory-instance"></a><span data-ttu-id="224bd-126">Azure Active Directory 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="224bd-126">Create Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="224bd-127">Active Directory 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="224bd-127">Create the Active Directory instance</span></span>

1. <span data-ttu-id="224bd-128"><https://portal.azure.com>에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-128">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="224bd-129">**+리소스 만들기**, **ID**, **Azure Active Directory**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-129">Click **+Create a resource**, then **Identity**, and then **Azure Active Directory**.</span></span>

   ![새 Azure Active Directory 인스턴스 만들기][create-directory-01]

1. <span data-ttu-id="224bd-131">**조직 이름**과 **초기 도메인 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-131">Enter your **Organization name** and your **Initial domain name**.</span></span> <span data-ttu-id="224bd-132">사용자 디렉터리의 전체 URL을 복사합니다. 이는 자습서의 뒷부분에서 사용자 계정을 추가 하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-132">Copy the full URL of your directory; you will use that to add user accounts later in this tutorial.</span></span> <span data-ttu-id="224bd-133">(예: `wingtiptoysdirectory.onmicrosoft.com`) 완료되면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-133">(For example: `wingtiptoysdirectory.onmicrosoft.com`.) When you have finished, click **Create**.</span></span>

   ![Azure Active Directory 이름 지정][create-directory-02]

1. <span data-ttu-id="224bd-135">Azure portal 도구 모음의 오른쪽 상단에서 계정 이름을 선택한 다음 **디렉터리 전환**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-135">Select your account name on the top-right of the Azure portal toolbar, then click **Switch directory**.</span></span>

   ![Azure 계정 이름을 선택합니다.][create-directory-03]

1. <span data-ttu-id="224bd-137">드롭다운 메뉴에서 새 Azure Active Directory를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-137">Select your new Azure Active Directory from the drop-down menu.</span></span>

   ![Azure Active Directory 선택][create-directory-04]

1. <span data-ttu-id="224bd-139">포털 메뉴에서 **Azure Active Directory**를 선택하고, **속성**을 클릭하여 **디렉터리 ID**를 복사합니다. 이 값은 이 자습서의 뒷부분에서 *application.properties* 파일을 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-139">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID**; you will use that value to configure your *application.properties* file later in this tutorial.</span></span>

   ![Azure Active Directory ID 복사][create-directory-05]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="224bd-141">Spring Boot 앱에 대한 애플리케이션 등록 추가</span><span class="sxs-lookup"><span data-stu-id="224bd-141">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="224bd-142">포털 메뉴에서 **Azure Active Directory**를 선택하고 **앱 등록**, **새 응용 프로그램 등록**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-142">Select **Azure Active Directory** from the portal menu, click **App registrations**, and then click **New application registration**, .</span></span>

   ![새 앱 등록 추가][create-app-registration-01]

2. <span data-ttu-id="224bd-144">애플리케이션 **이름**을 지정한 다음 http://localhost:8080을 **로그온 URL**에 사용하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-144">Specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![새 앱 등록 만들기][create-app-registration-02]

4. <span data-ttu-id="224bd-146">앱 등록 페이지가 표시되면 **애플리케이션 ID**를 복사합니다. 이 값은 이 자습서의 뒷부분에서 *application.properties* 파일을 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-146">When the page for your app registration appears, copy your **Application ID**; you will use this value to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="224bd-147">**설정**을 클릭한 다음 **키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-147">Click **Settings**, and then click **Keys**.</span></span>

   ![앱 등록 키 만들기][create-app-registration-03]

5. <span data-ttu-id="224bd-149">**설명**을 추가하고 새 키에 대해 **기간**을 지정한 다음 **저장**을 클릭합니다. **저장** 아이콘을 클릭하면 키 값이 자동으로 입력되며, 나중에 이 자습서의 뒷부분에서 *application.properties* 파일을 구성하기 위해 키 값을 복사해 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-149">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="224bd-150">이 값은 나중에 검색할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-150">(You will not be able to retrieve this value later.)</span></span>

   ![앱 등록 키 매개 변수 지정][create-app-registration-04]

6. <span data-ttu-id="224bd-152">앱 등록을 위한 기본 페이지에서 **설정**을 클릭하고 **필요한 권한**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-152">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![앱 등록 필요 권한][create-app-registration-05]

7. <span data-ttu-id="224bd-154">**Windows Azure Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-154">Click **Windows Azure Active Directory**.</span></span>

   ![Windows Azure Active Directory 선택][create-app-registration-06]

8. <span data-ttu-id="224bd-156">**로그인한 사용자로 디렉터리 액세스**와 **로그인 및 사용자 프로필 읽기**에 대한 상자를 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-156">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![액세스 권한 사용][create-app-registration-07]

9. <span data-ttu-id="224bd-158">**필요한 권한** 페이지에서 **사용 권한 부여**를 클릭하고 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-158">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![액세스 권한 부여][create-app-registration-08]

10. <span data-ttu-id="224bd-160">앱 등록을 위한 기본 페이지에서 **설정**을 클릭하고 **회신 URL**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-160">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

    ![회신 URL 편집][create-app-registration-09]

11. <span data-ttu-id="224bd-162">"<http://localhost:8080/login/oauth2/code/azure>"을 새 회신 URL로 입력하고, **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-162">Enter "<http://localhost:8080/login/oauth2/code/azure>" as a new reply URL, and then click **Save**.</span></span>

    ![새 회신 URL 추가][create-app-registration-10]

12. <span data-ttu-id="224bd-164">앱 등록에 대한 기본 페이지에서 **매니페스트**를 클릭하고 `oauth2AllowImplicitFlow` 매개 변수의 값을 `true`로 설정하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-164">From the main page for your app registration, click **Manifest**, then set the value of the `oauth2AllowImplicitFlow` parameter to `true`, and then click **Save**.</span></span>

    ![앱 매니페스트 구성][create-app-registration-11]

    > [!NOTE]
    > 
    > <span data-ttu-id="224bd-166">`oauth2AllowImplicitFlow` 매개 변수 및 다른 응용 프로그램 설정에 대한 자세한 내용은 [Azure Active Directory 응용 프로그램 매니페스트][AAD app manifest]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="224bd-166">For more information about the `oauth2AllowImplicitFlow` parameter and other application settings, see [Azure Active Directory application manifest][AAD app manifest].</span></span> 
    >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a><span data-ttu-id="224bd-167">디렉터리에 사용자 계정을 추가하고 해당 계정을 그룹에 추가합니다</span><span class="sxs-lookup"><span data-stu-id="224bd-167">Add a user account to your directory, and add that account to a group</span></span>

1. <span data-ttu-id="224bd-168">Active Directory의 **개요** 페이지에서 **모든 사용자**를, 그리고 **새 사용자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-168">From the **Overview** page of your Active Directory, click **All Users**, and then click **New user**.</span></span>

   ![새 사용자 계정 추가하기][create-user-01]

1. <span data-ttu-id="224bd-170">**사용자** 패널이 표시되면, **이름** 및 **사용자 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-170">When the **User** panel is displayed, enter the **Name** and **User name**.</span></span>

   ![사용자 계정 정보 입력][create-user-02]

   > [!NOTE]
   > 
   > <span data-ttu-id="224bd-172">사용자 이름을 입력하려면 자습서의 앞부분에 나온 디렉터리 URL을 지정해야 합니다. 예를 들어,</span><span class="sxs-lookup"><span data-stu-id="224bd-172">You need to specify your directory URL from earlier in this tutorial when you enter the user name; for example:</span></span>
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. <span data-ttu-id="224bd-173">**그룹**을 클릭하고, 응용 프로그램에서 권한 부여를 위해 사용할 그룹을 선택한 다음 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-173">Click **Groups**, then select the groups that you will use for authorization in your application, and then click **Select**.</span></span> <span data-ttu-id="224bd-174">(이 자습서의 목적에 따라 _사용자_ 그룹에 계정을 추가합니다.)</span><span class="sxs-lookup"><span data-stu-id="224bd-174">(For the purposes of this tutorial, add the account to the _Users_ group.)</span></span>

   ![사용자의 그룹을 선택합니다.][create-user-03]

1. <span data-ttu-id="224bd-176">**암호 표시**를 클릭하여 암호를 복사합니다. 이는 이 자습서의 뒷부분에서 응용 프로그램에 로그인할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-176">Click **Show password**, and copy the password; you will use this when you log into your application later in this tutorial.</span></span> <span data-ttu-id="224bd-177">암호를 복사한 다음, **만들기**를 클릭하여 디렉터리에 새 사용자 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-177">When you have copied the password, click **Create** to add the new user account to your directory.</span></span>

   ![암호 표시][create-user-04]

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="224bd-179">앱 구성 및 컴파일</span><span class="sxs-lookup"><span data-stu-id="224bd-179">Configure and compile your app</span></span>

1. <span data-ttu-id="224bd-180">이 자습서의 앞부분에서 작성하고 다운로드한 프로젝트 아카이브의 파일을 디렉터리로 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-180">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

1. <span data-ttu-id="224bd-181">프로젝트에서 상위 폴더로 이동하고 텍스트 편집기에서 `pom.xml`Maven 프로젝트 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-181">Navigate to the parent folder for your project, and open the `pom.xml` Maven project file in a text editor.</span></span>

1. <span data-ttu-id="224bd-182">Spring OAuth2 보안의 종속성을 `pom.xml`에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-182">Add the dependencies for Spring OAuth2 security to the `pom.xml`:</span></span>

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

1. <span data-ttu-id="224bd-183">*pom.xml* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-183">Save and close the *pom.xml* file.</span></span>

1. <span data-ttu-id="224bd-184">프로젝트에서 *src/main/resources* 폴더로 이동하고 텍스트 편집기에서 *application.properties* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-184">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="224bd-185">이전에 생성한 값을 사용하여 앱 등록을 위한 설정을 지정합니다. 예를 들어,</span><span class="sxs-lookup"><span data-stu-id="224bd-185">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

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
   <span data-ttu-id="224bd-186">위치:</span><span class="sxs-lookup"><span data-stu-id="224bd-186">Where:</span></span>

   | <span data-ttu-id="224bd-187">매개 변수</span><span class="sxs-lookup"><span data-stu-id="224bd-187">Parameter</span></span> | <span data-ttu-id="224bd-188">설명</span><span class="sxs-lookup"><span data-stu-id="224bd-188">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="224bd-189">앞에 나온 Active Directory의 **디렉터리 ID** 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-189">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="224bd-190">앞에서 완료한 앱 등록의 **애플리케이션 ID**를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-190">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="224bd-191">앞에서 완료한 앱 등록 키의 **값**을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-191">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="224bd-192">권한 부여에 사용할 Active Directory 그룹 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-192">Contains a list of Active Directory groups to use for authorization.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="224bd-193">*application.properties* 파일에서 사용할 수 있는 값의 전체 목록은 GitHub에서 [Azure Active Directory Spring Boot 샘플][AAD Spring Boot Sample]을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-193">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

1. <span data-ttu-id="224bd-194">*application.properties* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-194">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="224bd-195">애플리케이션에 대해 Java 소스 폴더에 이름이 *controller*인 폴더를 만듭니다. 예를 들어 *src/main/java/com/wingtiptoys/security/controller*입니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-195">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="224bd-196">*controller* 폴더에 이름이 *HelloController.java*인 새 Java 파일을 만들고 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-196">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="224bd-197">다음 코드를 입력한 다음 저장하고 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-197">Enter the following code, then save and close the file:</span></span>

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
   > <span data-ttu-id="224bd-198">`@PreAuthorize("hasRole('')")` 메서드에 지정한 그룹 이름은 *application.properties* 파일의 `azure.activedirectory.active-directory-groups` 필드에 지정한 그룹 중 하나를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-198">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   > 
   > <span data-ttu-id="224bd-199">다른 요청 매핑에 대한 다른 권한 부여 설정을 지정할 수도 있습니다. 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="224bd-199">You can also specify different authorization settings for different request mappings; for example:</span></span>
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

1. <span data-ttu-id="224bd-200">애플리케이션에 대해 Java 소스 폴더에 이름이 *security*인 폴더를 만듭니다. 예를 들어 *src/main/java/com/wingtiptoys/security/security*입니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-200">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="224bd-201">*security* 폴더에 이름이 *WebSecurityConfig.java*인 새 Java 파일을 만들고 텍스트 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-201">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="224bd-202">다음 코드를 입력한 다음 저장하고 파일을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-202">Enter the following code, then save and close the file:</span></span>

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

## <a name="build-and-test-your-app"></a><span data-ttu-id="224bd-203">앱 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="224bd-203">Build and test your app</span></span>

1. <span data-ttu-id="224bd-204">명령 프롬프트를 열고 디렉터리를 앱의 *pom.xml* 파일이 위치한 폴더로 변경합니다. </span><span class="sxs-lookup"><span data-stu-id="224bd-204">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="224bd-205">Maven을 사용하여 Spring Boot 애플리케이션을 빌드하고 실행합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="224bd-205">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![사용 중인 애플리케이션 빌드][build-application]

1. <span data-ttu-id="224bd-207">애플리케이션이 Maven에서 빌드 및 시작되고 나면, <http://localhost:8080>을 웹 브라우저에서 엽니다. 사용자 이름 및 암호 입력 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-207">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![애플리케이션에 로그인][application-login]

   > [!NOTE]
   > 
   > <span data-ttu-id="224bd-209">새 사용자 계정에서 처음 로그인한 경우라면, 암호를 변경하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-209">You may be prompted to change your password if this is the first login for a new user account.</span></span>
   > 
   > ![암호 변경][update-password]
   > 

1. <span data-ttu-id="224bd-211">사용자가 성공적으로 로그인한 후 컨트롤러에서 샘플 "Hello World" 텍스트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-211">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![로그인 성공][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="224bd-213">승인되지 않은 사용자 계정인 경우 **HTTP 403 Unauthorized** 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-213">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="summary"></a><span data-ttu-id="224bd-214">요약</span><span class="sxs-lookup"><span data-stu-id="224bd-214">Summary</span></span>

<span data-ttu-id="224bd-215">이 자습서에서는 Azure Active Directory 스타터를 사용하여 새 Java 웹 애플리케이션을 만들고, 새로 구성한 Azure AD 테넌트에 새 애플리케이션을 등록하고, 애플리케이션이 웹을 보호하기 위한 Spring 주석 및 클래스를 사용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-215">In this tutorial, you created a new Java web application using the Azure Active Directory starter, configured a new Azure AD tenant and registered a new application in it, and then configured your application to use the Spring annotations and classes to protect the web app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="224bd-216">다음 단계</span><span class="sxs-lookup"><span data-stu-id="224bd-216">Next steps</span></span>

<span data-ttu-id="224bd-217">Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="224bd-217">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="224bd-218">Azure의 Spring</span><span class="sxs-lookup"><span data-stu-id="224bd-218">Spring on Azure</span></span>](/java/azure/spring-framework)

<!-- URL List -->

[Azure Active Directory Documentation]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure for Java Developers]: /java/azure/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[AAD Spring Boot Sample]: https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-backend-sample

<!-- IMG List -->

[create-spring-app-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-01.png
[create-spring-app-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-02.png
[create-spring-app-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-03.png

[create-directory-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-01.png
[create-directory-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-02.png
[create-directory-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-03.png
[create-directory-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-04.png
[create-directory-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-05.png

[create-app-registration-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-01.png
[create-app-registration-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-02.png
[create-app-registration-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-03.png
[create-app-registration-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-04.png
[create-app-registration-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-05.png
[create-app-registration-06]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-06.png
[create-app-registration-07]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-07.png
[create-app-registration-08]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-08.png
[create-app-registration-09]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-09.png
[create-app-registration-10]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-10.png
[create-app-registration-11]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-11.png

[create-user-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-01.png
[create-user-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-02.png
[create-user-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-03.png
[create-user-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-04.png

[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
[update-password]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/update-password.png
