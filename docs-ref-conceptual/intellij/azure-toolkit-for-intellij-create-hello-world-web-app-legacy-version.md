---
title: 레거시 IntelliJ용 도구 키트를 사용하여 Azure용 Hello World 웹앱 만들기
description: 이 자습서에서는 IntelliJ용 Azure 도구 키트 버전 3.0.6 이하를 사용하여 Azure용 Hello World 웹앱을 만드는 방법을 보여 줍니다.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/13/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 4a1d9ee79fdc4284dff65f6b026ec103b3d623ce
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338977"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-intellij"></a><span data-ttu-id="cdf62-103">레거시 IntelliJ용 도구 키트를 사용하여 Azure용 Hello World 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="cdf62-103">Create a Hello World web app for Azure using the legacy toolkit for IntelliJ</span></span>

<span data-ttu-id="cdf62-104">이 자습서에서는 [IntelliJ용 Azure 도구 키트] 버전 3.0.6 이하를 사용하여 기본 Hello World 응용 프로그램을 만들고 Azure에 웹앱으로 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using version 3.0.6 (or earlier) of the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
>
> <span data-ttu-id="cdf62-105">[Eclipse용 Azure 도구 키트 설치]를 사용하는 이 문서의 버전에 대한 내용은 [Eclipse를 사용하여 Azure용 Hello World 웹앱 만들기][eclipse-hello-world]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdf62-105">For a version of this article that uses the [Azure Toolkit for Eclipse], see [Create a Hello World web app for Azure using Eclipse][eclipse-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="cdf62-106">IntelliJ용 Azure 도구 키트는 2017년 8월에 다른 워크플로로 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-106">The Azure Toolkit for IntelliJ was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="cdf62-107">이 문서에서는 IntelliJ용 Azure 도구 키트 버전 3.0.6 이하를 사용하여 Hello World 웹앱을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-107">This article illustrates creating a Hello World web app by using version 3.0.6 (or earlier) of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="cdf62-108">도구 키트 버전 3.0.7 이상을 사용하는 경우 [IntelliJ에서 Azure용 Hello World 웹앱 만들기][Updated Version]의 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-108">If you are using the version 3.0.7 (or later) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in IntelliJ][Updated Version].</span></span>
>

<span data-ttu-id="cdf62-109">이 자습서를 완료한 경우 웹 브라우저에서 응용 프로그램을 보면 다음 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Hello World 앱의 미리 보기][01]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="cdf62-111">새 웹앱 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="cdf62-111">Create a new web app project</span></span>

1. <span data-ttu-id="cdf62-112">IntelliJ를 시작하고 [IntelliJ용 Azure 도구 키트에 대한 Azure 로그인 지침][intelliJ-sign-in-instructions] 문서의 지침을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-112">Start IntelliJ, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for IntelliJ][intelliJ-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="cdf62-113">**파일** 메뉴, **새로 만들기**를 차례로 클릭한 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-113">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![파일 새로 만들기 프로젝트][02]

2. <span data-ttu-id="cdf62-115">**New Project** 대화 상자에서 **Java**를 선택하고 **Web Application**을 선택한 후 **New**를 클릭하여 프로젝트 SDK를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-115">In the **New Project** dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
   ![새 프로젝트 대화 상자][03a]
   
3. <span data-ttu-id="cdf62-117">Select Home Directory for JDK 대화 상자에서 JDK가 설치되어 있는 폴더를 선택한 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-117">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="cdf62-118">New Project 대화 상자에서 **Next**를 클릭하여 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-118">Click **Next** in the New Project dialog box to continue.</span></span>
   
   ![JDK 홈 디렉터리 지정][03b]

4. <span data-ttu-id="cdf62-120">이 자습서의 목적에 따라 프로젝트의 이름을 **Java-Web-App-On-Azure**로 지정하고 **Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-120">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
   ![새 프로젝트 대화 상자][04]

5. <span data-ttu-id="cdf62-122">IntelliJ의 Project Explorer 보기 내에서 **Java-Web-App-On-Azure**를 확장한 다음 **web**을 확장하고 **index.jsp**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-122">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
   ![인덱스 페이지 열기][05c]

6. <span data-ttu-id="cdf62-124">IntelliJ에서 index.jsp 파일이 열리면 **Hello World!** 를 동적으로 표시하도록 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-124">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="cdf62-125">기존 `<body>` 요소 내.</span><span class="sxs-lookup"><span data-stu-id="cdf62-125">within the existing `<body>` element.</span></span> <span data-ttu-id="cdf62-126">업데이트된 `<body>` 콘텐츠는 다음 예제와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-126">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

7. <span data-ttu-id="cdf62-127">index.jsp를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-127">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="cdf62-128">Azure에 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="cdf62-128">Deploy your web app to Azure</span></span>

<span data-ttu-id="cdf62-129">몇 가지 방법으로 Azure에 Java 웹앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-129">There are several ways by which you can deploy a Java web app to Azure.</span></span> <span data-ttu-id="cdf62-130">이 자습서에서는 가장 간단한 방법 중 하나를 설명합니다. 즉, 특별한 프로젝트 형식이나 추가 도구 없이 Azure 웹앱 컨테이너에 응용 프로그램을 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-130">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="cdf62-131">JDK 및 웹 컨테이너 소프트웨어는 Azure에서 제공되므로 별도로 업로드할 필요가 없습니다. Java 웹앱만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-131">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="cdf62-132">따라서 애플리케이션 게시 프로세스에 걸리는 시간이 몇 분이 아니라 몇 초입니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-132">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="cdf62-133">응용 프로그램을 게시하기 전에 먼저 모듈 설정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-133">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="cdf62-134">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-134">To do so, use the following steps:</span></span>

1. <span data-ttu-id="cdf62-135">IntelliJ의 Project Explorer에서 **Java-Web-App-On-Azure** 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-135">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="cdf62-136">상황에 맞는 메뉴가 나타나면 **모듈 설정 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-136">When the context menu appears, click **Open Module Settings**.</span></span>

   ![모듈 설정 열기][05a]

2. <span data-ttu-id="cdf62-138">프로젝트 구조 대화 상자가 나타나면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-138">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="cdf62-139">a.</span><span class="sxs-lookup"><span data-stu-id="cdf62-139">a.</span></span> <span data-ttu-id="cdf62-140">**프로젝트 설정** 목록에서 **아티팩트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-140">Click **Artifacts** in the list of **Project Settings**.</span></span>

   <span data-ttu-id="cdf62-141">b.</span><span class="sxs-lookup"><span data-stu-id="cdf62-141">b.</span></span> <span data-ttu-id="cdf62-142">**이름** 상자에서 아티팩트 이름에 공백 또는 특수 문자가 포함되지 않도록 이름을 변경합니다. 이 작업은 해당 이름이 URI(Uniform Resource Identifier)에 사용되기 때문에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-142">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>

   <span data-ttu-id="cdf62-143">다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-143">c.</span></span> <span data-ttu-id="cdf62-144">**형식**을 **웹 응용 프로그램: 보관**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-144">Change the **Type** to **Web Application: Archive**.</span></span>

   <span data-ttu-id="cdf62-145">d.</span><span class="sxs-lookup"><span data-stu-id="cdf62-145">d.</span></span> <span data-ttu-id="cdf62-146">**확인**을 클릭하여 프로젝트 구조 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-146">Click **OK** to close the Project Structure dialog box.</span></span>

   ![모듈 설정 열기][05b]

<span data-ttu-id="cdf62-148">모듈 설정을 구성한 경우 다음 단계를 사용하여 Azure에 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-148">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="cdf62-149">IntelliJ의 Project Explorer에서 **Java-Web-App-On-Azure** 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-149">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="cdf62-150">상황에 맞는 메뉴가 나타나면 **Azure**를 선택한 다음 **Azure 웹앱으로 게시...** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-150">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
   ![Azure 게시 상황에 맞는 메뉴][06]

2. <span data-ttu-id="cdf62-152">IntelliJ에서 Azure에 로그인하지 않은 경우 Azure 계정으로 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-152">If you have not already signed in to Azure from IntelliJ, you will be prompted to sign in to your Azure account.</span></span> <span data-ttu-id="cdf62-153">Azure 계정이 여러 개 있으면 로그인 프로세스 중에 일부 메시지가 동일한 것이더라도 두 번 이상 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-153">(If you have multiple Azure accounts, some of the prompts during the sign-in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="cdf62-154">이 경우 로그인 지침에 따라 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-154">When this happens, continue to follow the sign-in instructions.)</span></span>
   
   ![Azure 로그인 대화 상자][07]

3. <span data-ttu-id="cdf62-156">Azure 계정에 성공적으로 로그인하면 **구독 관리** 대화 상자에는 자격 증명과 연결된 구독 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-156">After you have successfully signed in to your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="cdf62-157">여러 구독이 나열된 경우 특정 하위 집합만 사용하려면 사용하지 않을 구독의 선택을 취소하면 됩니다. 구독을 선택했으면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-157">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
   ![구독 관리][08]

4. <span data-ttu-id="cdf62-159">**Azure 웹앱 컨테이너에 배포** 대화 상자가 나타나는 경우 이전에 만든 웹앱 컨테이너가 표시됩니다. 컨테이너를 만들지 않은 경우에는 목록이 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-159">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![앱 컨테이너][09]

5. <span data-ttu-id="cdf62-161">이전에 Azure 웹앱 컨테이너를 만들지 않은 경우 또는 응용 프로그램을 새 컨테이너에 게시하려는 경우 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-161">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="cdf62-162">그렇지 않으면 기존 웹앱 컨테이너를 선택하고 아래의 6단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-162">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   <span data-ttu-id="cdf62-163">a.</span><span class="sxs-lookup"><span data-stu-id="cdf62-163">a.</span></span> <span data-ttu-id="cdf62-164">**+** 기호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-164">Click the **+** sign.</span></span>
      
      ![앱 컨테이너 추가][10]

   <span data-ttu-id="cdf62-166">b.</span><span class="sxs-lookup"><span data-stu-id="cdf62-166">b.</span></span> <span data-ttu-id="cdf62-167">다음 몇 개 단계에서 사용되는 **새 웹앱 컨테이너** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-167">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
      ![새 앱 컨테이너][11a]
   
   <span data-ttu-id="cdf62-169">다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-169">c.</span></span> <span data-ttu-id="cdf62-170">웹앱 컨테이너에 **DNS 레이블**을 입력합니다. 이렇게 하면 Azure에서 웹 애플리케이션에 대한 호스트 URL의 리프 DNS 레이블을 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-170">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="cdf62-171">이름은 사용 가능해야 하며, Azure 웹앱 명명 요구 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-171">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>

   <span data-ttu-id="cdf62-172">d.</span><span class="sxs-lookup"><span data-stu-id="cdf62-172">d.</span></span> <span data-ttu-id="cdf62-173">**웹 컨테이너** 드롭다운 메뉴에서 응용 프로그램에 적절한 소프트웨어를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-173">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="cdf62-174">현재, Tomcat 8, Tomcat 7, Jetty 9 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-174">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="cdf62-175">선택한 소프트웨어의 최근 배포는 Azure에서 제공되며, Azure에서 제공되는 JDK의 최근 배포에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-175">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of the JDK provided by Azure.</span></span>

   <span data-ttu-id="cdf62-176">e.</span><span class="sxs-lookup"><span data-stu-id="cdf62-176">e.</span></span> <span data-ttu-id="cdf62-177">**구독** 드롭다운 메뉴에서 이 배포에 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="cdf62-178">f.</span><span class="sxs-lookup"><span data-stu-id="cdf62-178">f.</span></span> <span data-ttu-id="cdf62-179">**리소스 그룹** 드롭다운 메뉴에서 웹앱을 연결할 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-179">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="cdf62-180">(Azure 리소스 그룹을 사용하여 함께 삭제할 수 있도록 관련된 리소스를 그룹화할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="cdf62-180">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="cdf62-181">기존 리소스 그룹(있는 경우)을 선택하고 아래 g 단계로 건너뛰거나 다음 단계를 통해 새 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-181">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="cdf62-182">**리소스 그룹** 드롭다운 메뉴에서 **&lt;&lt;새 리소스 그룹 만들기&gt;&gt;** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-182">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="cdf62-183">**새 리소스 그룹** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-183">The **New Resource Group** dialog box will be displayed:</span></span>
        
         ![새 리소스 그룹][12]

      * <span data-ttu-id="cdf62-185">**이름** 텍스트 상자에서 새 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-185">In the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="cdf62-186">**지역** 드롭다운 메뉴에서 리소스 그룹에 적합한 Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-186">In the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="cdf62-187">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-187">Click **OK**.</span></span>

   <span data-ttu-id="cdf62-188">g.</span><span class="sxs-lookup"><span data-stu-id="cdf62-188">g.</span></span> <span data-ttu-id="cdf62-189">**App Service 계획** 드롭다운 메뉴에 선택한 리소스 그룹과 연결된 App Service 계획이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-189">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="cdf62-190">App Service 계획은 웹앱, 가격 책정 계층 및 계산 인스턴스 크기의 위치와 같은 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-190">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="cdf62-191">App Service 계획 하나를 여러 Web Apps에 사용할 수 있기 때문에 App Service 계획은 특정 웹앱 배포와는 별도로 관리됩니다.)</span><span class="sxs-lookup"><span data-stu-id="cdf62-191">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
      <span data-ttu-id="cdf62-192">기존 App Service 계획(있는 경우)을 선택하고 아래 h 단계로 건너뛰거나 다음 단계를 통해 새 App Service 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-192">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="cdf62-193">**App Service 계획** 드롭다운 메뉴에서 **&lt;&lt;새 App Service 계획 만들기&gt;&gt;** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-193">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="cdf62-194">**새 App Service 계획** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-194">The **New App Service Plan** dialog box will be displayed:</span></span>
        
         ![새 App Service 계획][13]

      * <span data-ttu-id="cdf62-196">**이름** 텍스트 상자에서 새 App Service 계획의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-196">In the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="cdf62-197">**위치** 드롭다운 메뉴에서 계획에 적합한 Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-197">In the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="cdf62-198">**가격 책정 계층** 드롭다운 메뉴에서 계획에 적합한 가격 책정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-198">In the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="cdf62-199">테스트 목적으로 **무료**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-199">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="cdf62-200">**인스턴스 크기** 드롭다운 메뉴에서 계획에 적절한 인스턴스 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-200">In the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="cdf62-201">테스트 목적으로 **Small**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-201">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="cdf62-202">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-202">Click **OK**.</span></span>

   <span data-ttu-id="cdf62-203">h.</span><span class="sxs-lookup"><span data-stu-id="cdf62-203">h.</span></span> <span data-ttu-id="cdf62-204">(선택 사항) 기본적으로 Java 8 최신 배포판은 자동으로 Azure에 의해 웹앱 컨테이너에 JVM으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-204">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="cdf62-205">그러나 JVM의 다른 버전 및 배포판을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-205">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="cdf62-206">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-206">To do so, use the following steps:</span></span>
      
   * <span data-ttu-id="cdf62-207">**새 웹앱 컨테이너** 대화 상자에서 **JDK** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-207">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
   * <span data-ttu-id="cdf62-208">다음 두 가지 옵션 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-208">You can choose from one of the following options:</span></span>
        
      * <span data-ttu-id="cdf62-209">Azure에서 제공하는 기본 JDK 배포</span><span class="sxs-lookup"><span data-stu-id="cdf62-209">Deploy the default JDK which is offered by Azure</span></span>
      * <span data-ttu-id="cdf62-210">Azure에서 사용할 수 있는 추가 JDK 드롭다운 목록에서 타사 JDK 배포</span><span class="sxs-lookup"><span data-stu-id="cdf62-210">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
      * <span data-ttu-id="cdf62-211">사용자 지정 JDK 배포(이 JDK는 ZIP 파일로 패키지된 후 공개적으로 제공되거나 Azure Storage 계정에 제공되어야 함)</span><span class="sxs-lookup"><span data-stu-id="cdf62-211">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
     ![새 앱 컨테이너 JDK 탭][11b]

   <span data-ttu-id="cdf62-213">i.</span><span class="sxs-lookup"><span data-stu-id="cdf62-213">i.</span></span> <span data-ttu-id="cdf62-214">위 단계를 모두 완료한 경우 New Web App Container 대화 상자가 다음 그림과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-214">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![새 앱 컨테이너][14]
   
   <span data-ttu-id="cdf62-216">j.</span><span class="sxs-lookup"><span data-stu-id="cdf62-216">j.</span></span> <span data-ttu-id="cdf62-217">**확인** 을 클릭하여 새 웹앱 컨테이너 만들기를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-217">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="cdf62-218">웹 앱 컨테이너의 목록이 새로 고쳐지도록 몇 초 간 기다리고 나면 새로 만든 웹 앱 컨테이너를 목록에서 선택할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-218">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

6. <span data-ttu-id="cdf62-219">이제 Azure에 대한 웹앱의 초기 배포를 완료할 준비가 되었습니다. **확인**을 클릭하여 Java 애플리케이션을 선택한 웹앱 컨테이너에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-219">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="cdf62-220">기본적으로 응용 프로그램은 응용 프로그램 서버의 하위 디렉터리로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-220">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="cdf62-221">루트 애플리케이션으로 배포하려면 **확인**을 클릭하기 전에 **루트에 배포** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-221">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
   ![Azure에 배포][15]

7. <span data-ttu-id="cdf62-223">이제 웹앱의 배포 상태를 나타내는 **Azure 동작 로그** 보기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-223">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![진행률 표시기][16]
   
   <span data-ttu-id="cdf62-225">Azure에 웹앱을 배포하는 프로세스는 몇 초 내에 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-225">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="cdf62-226">응용 프로그램이 준비되면 **상태** 열에 **게시됨**이라는 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-226">When your application is ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="cdf62-227">이 링크를 클릭하여 배포된 웹앱의 홈페이지로 이동하거나, 다음 섹션의 단계를 사용하여 해당 웹앱으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-227">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="cdf62-228">Azure에서 웹앱 검색</span><span class="sxs-lookup"><span data-stu-id="cdf62-228">Browsing to your Web App on Azure</span></span>

<span data-ttu-id="cdf62-229">Azure에서 웹앱을 검색하려면 **Azure 탐색기** 보기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-229">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="cdf62-230">**Azure 탐색기** 보기가 열려 있지 않은 경우 IntelliJ에서 **View** 메뉴를 클릭한 다음 **Tool Windows**, **Service Explorer**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-230">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="cdf62-231">이전에 로그인하지 않은 경우 로그인하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-231">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="cdf62-232">**Azure 탐색기** 보기가 표시되면 다음 단계에 따라 웹앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-232">When the **Azure Explorer** view is displayed, follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="cdf62-233">**Azure** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-233">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="cdf62-234">**Web Apps** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-234">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="cdf62-235">원하는 웹앱을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-235">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="cdf62-236">상황에 맞는 메뉴가 나타나면 **브라우저에서 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-236">When the context menu appears, click **Open in Browser**.</span></span>
   
   ![웹앱 찾아보기][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="cdf62-238">웹앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="cdf62-238">Updating your web app</span></span>

<span data-ttu-id="cdf62-239">실행 중인 기존 Azure 웹앱을 빠르고 쉽게 업데이트할 수 있으며, 두 가지 업데이트 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-239">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="cdf62-240">기존 Java 웹앱의 배포를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-240">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="cdf62-241">동일한 웹앱 컨테이너에 추가 Java 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-241">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="cdf62-242">두 경우 모두 프로세스는 동일하며 몇 초만 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-242">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="cdf62-243">IntelliJ Project Explorer에서 업데이트하거나 기존 웹앱 컨테이너에 추가할 Java 응용 프로그램을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-243">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="cdf62-244">상황에 맞는 메뉴가 나타나면 **Azure**를 선택한 다음 **Azure 웹앱으로 게시...** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-244">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="cdf62-245">이전에 이미 로그인했으므로 기존 웹앱 컨테이너 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-245">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="cdf62-246">Java 응용 프로그램을 게시하거나 다시 게시할 컨테이너를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-246">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="cdf62-247">몇 초 후 **Azure 동작 로그** 보기에 업데이트된 배포가 **게시됨**으로 표시되고, 웹 브라우저에서 업데이트된 애플리케이션을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-247">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="cdf62-248">기존 웹앱 시작, 중지 또는 다시 시작</span><span class="sxs-lookup"><span data-stu-id="cdf62-248">Starting, stopping, or restarting an existing web app</span></span>

<span data-ttu-id="cdf62-249">기존 Azure 웹앱 컨테이너(여기에 배포된 모든 Java 애플리케이션 포함)를 시작 또는 중지하려면 **Azure 탐색기** 보기를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-249">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="cdf62-250">**Azure 탐색기** 보기가 열려 있지 않은 경우 IntelliJ에서 **View** 메뉴를 클릭한 다음 **Tool Windows**, **Service Explorer**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-250">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="cdf62-251">이전에 로그인하지 않은 경우 로그인하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-251">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="cdf62-252">**Azure 탐색기** 보기가 표시되면 다음 단계에 따라 웹앱을 시작하거나 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-252">When the **Azure Explorer** view is displayed, follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="cdf62-253">**Azure** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-253">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="cdf62-254">**Web Apps** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-254">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="cdf62-255">원하는 웹앱을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-255">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="cdf62-256">상황에 맞는 메뉴가 나타나면 **시작**, **중지** 또는 **다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-256">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="cdf62-257">메뉴 선택 항목은 상황별로 변경되므로 실행 중인 웹앱만 중지하고, 현재 실행되고 있지 않은 웹앱만 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cdf62-257">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![웹 앱 중지][18]

## <a name="next-steps"></a><span data-ttu-id="cdf62-259">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cdf62-259">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="cdf62-260">Azure Web Apps 만들기에 대한 자세한 내용은 [Web Apps 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cdf62-260">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[IntelliJ용 Azure 도구 키트]: azure-toolkit-for-intellij.md
[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Eclipse용 Azure 도구 키트 설치]: ../eclipse/azure-toolkit-for-eclipse.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Web Apps 개요]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Updated Version]: azure-toolkit-for-intellij-create-hello-world-web-app.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/02-File-New-Project.png
[03a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-Dialog.png
[03b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-SDK-Dialog.png
[04]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/04-New-Project-Dialog.png
[05a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Module-Settings.png
[05b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Project-Structure-Dialog.png
[05c]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Index-Page.png
[06]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/06-Azure-Publish-Context-Menu.png
[07]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/07-Azure-Log-In-Dialog.png
[08]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/08-Manage-Subscriptions.png
[09]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/09-App-Containers.png
[10]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/10-Add-App-Container.png
[11a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container.png
[11b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container-JDK-Tab.png
[12]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/12-New-Resource-Group.png
[13]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/13-New-App-Service-Plan.png
[14]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/14-New-App-Container.png
[15]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/15-Deploy-To-Azure.png
[16]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/16-Progress-Indicator.png
[17]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/17-Browse-Web-App.png
[18]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/18-Stop-Web-App.png
