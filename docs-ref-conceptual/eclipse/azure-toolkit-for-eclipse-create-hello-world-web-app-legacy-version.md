---
title: ''
description: 이 자습서에서는 Eclipse용 Azure 도구 키트 버전 3.0.6 이하를 사용하여 Azure용 Hello World 웹앱을 만드는 방법을 보여 줍니다.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 896e7eff389bc7d3ac119d315c50aae505a381da
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892564"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-eclipse"></a><span data-ttu-id="473a0-102">레거시 Eclipse용 도구 키트를 사용하여 Azure용 Hello World 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="473a0-102">Create a Hello World web app for Azure using the legacy toolkit for Eclipse</span></span>

<span data-ttu-id="473a0-103">이 자습서에서는 [Eclipse용 Azure 도구 키트 설치] 버전 3.0.6 이하를 사용하여 기본 Hello World 응용 프로그램을 만들고 Azure에 웹앱으로 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-103">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using version 3.0.6 (or earlier) of the [Azure Toolkit for Eclipse].</span></span>

> [!NOTE]
>
> <span data-ttu-id="473a0-104">[IntelliJ용 Azure 도구 키트]를 사용하는 이 문서의 버전에 대한 내용은 [IntelliJ를 사용하여 Azure용 Hello World 웹앱 만들기][intellij-hello-world]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="473a0-104">For a version of this article that uses the [Azure Toolkit for IntelliJ], see [Create a Hello World web app for Azure using IntelliJ][intellij-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="473a0-105">Eclipse용 Azure 도구 키트는 2017년 8월에 다른 워크플로로 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-105">The Azure Toolkit for Eclipse was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="473a0-106">이 문서에서는 Eclipse용 Azure 도구 키트 버전 3.0.6 이하를 사용하여 Hello World 웹앱을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-106">This article illustrates creating a Hello World web app by using version 3.0.6 (or earlier) of the Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="473a0-107">도구 키트 버전 3.0.7 이상을 사용하는 경우 [Eclipse에서 Azure용 Hello World 웹앱 만들기][Updated Version]의 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-107">If you are using the version 3.0.7 (or later) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in Eclipse][Updated Version].</span></span>
>

<span data-ttu-id="473a0-108">이 자습서를 완료한 경우 웹 브라우저에서 응용 프로그램을 보면 다음 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-108">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Hello World 앱의 미리 보기][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="473a0-110">새 웹앱 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="473a0-110">Create a new web app project</span></span>

1. <span data-ttu-id="473a0-111">Eclipse를 시작하고 [Eclipse용 Azure 도구 키트에 대한 Azure 로그인 지침][eclipse-sign-in-instructions] 문서의 지침을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-111">Start Eclipse, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse][eclipse-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="473a0-112">**파일**, **새로 만들기**, **동적 웹 프로젝트**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-112">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="473a0-113">(**File**, **New**를 차례로 클릭한 후 **Dynamic Web Project**가 사용 가능한 프로젝트로 표시되지 않는 경우 **File**, **New**, **Project...** 를 차례로 클릭한 후 **Web**을 확장하고 **Dynamic Web Project**를 클릭한 후 **Next**를 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="473a0-113">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

2. <span data-ttu-id="473a0-114">이 자습서에서는 프로젝트의 이름을 **MyWebApp**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-114">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="473a0-115">화면이 다음과 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-115">Your screen will appear similar to the following:</span></span>
   
   ![새로운 동적 웹 프로젝트 만들기][02]

3. <span data-ttu-id="473a0-117">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-117">Click **Finish**.</span></span>

4. <span data-ttu-id="473a0-118">Eclipse의 **Project Explorer** 뷰 내에서 **MyWebApp**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-118">Within Eclipse's **Project Explorer** view, expand **MyWebApp**.</span></span> <span data-ttu-id="473a0-119">**WebContent**를 마우스 오른쪽 단추로 클릭하고 **New**를 클릭한 후 **JSP File**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-119">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

5. <span data-ttu-id="473a0-120">**새 JSP 파일** 대화 상자에서 **index.jsp** 파일의 이름을 지정하고 부모 폴더를 **MyWebApp/WebContent**로 유지한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-120">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

6. <span data-ttu-id="473a0-121">**JSP 템플릿 선택** 대화 상자에서 이 자습서의 목적에 따라, **새 JSP 파일(html)** 을 선택한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-121">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

7. <span data-ttu-id="473a0-122">Eclipse에서 index.jsp 파일이 열리면 **Hello World!** 를 동적으로 표시하도록 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-122">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="473a0-123">기존 `<body>` 요소 내.</span><span class="sxs-lookup"><span data-stu-id="473a0-123">within the existing `<body>` element.</span></span> <span data-ttu-id="473a0-124">업데이트된 `<body>` 콘텐츠는 다음 예제와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-124">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="473a0-125">index.jsp를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-125">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="473a0-126">Azure에 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="473a0-126">Deploy your web app to Azure</span></span>

<span data-ttu-id="473a0-127">몇 가지 방법으로 Azure에 Java 웹 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-127">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="473a0-128">이 자습서에서는 가장 간단한 방법 중 하나를 설명합니다. 즉, 특별한 프로젝트 형식이나 추가 도구 없이 Azure 웹앱 컨테이너에 응용 프로그램을 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-128">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="473a0-129">JDK 및 웹 컨테이너 소프트웨어는 Azure에서 제공되므로 별도로 업로드할 필요가 없습니다. Java 웹앱만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-129">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="473a0-130">따라서 응용 프로그램 게시 프로세스에 걸리는 시간이 몇 분이 아니라 몇 초입니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-130">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="473a0-131">Eclipse의 프로젝트 탐색기에서 **MyWebApp**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-131">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>

2. <span data-ttu-id="473a0-132">상황에 맞는 메뉴에서 **Azure**를 선택하고 **Azure 웹앱으로 게시...** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-132">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
   ![Azure 웹앱으로 게시][03]
   
   <span data-ttu-id="473a0-134">또는 프로젝트 탐색기에서 웹 응용 프로그램 프로젝트를 선택한 상태로 도구 모음에서 **게시** 드롭다운 단추를 클릭하고 다음에서 **Azure 웹앱으로 게시**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-134">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span></span>
   
   ![Azure 웹앱으로 게시][14]

3. <span data-ttu-id="473a0-136">Eclipse에서 Azure에 로그인하지 않은 경우 Azure 계정으로 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-136">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span></span>
   
   ![Azure 로그인 대화 상자][04]
   
   <span data-ttu-id="473a0-138">Azure 계정이 여러 개 있으면 로그인 프로세스 중에 일부 메시지가 동일한 것이더라도 두 번 이상 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-138">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="473a0-139">이 경우 로그인 지침에 따라 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-139">When this happens, continue following the sign in instructions.</span></span>

4. <span data-ttu-id="473a0-140">Azure 계정에 성공적으로 로그인하면 **구독 관리** 대화 상자에는 자격 증명과 연결된 구독 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-140">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="473a0-141">여러 구독이 나열된 경우 특정 하위 집합만 사용하려면 선택적으로 사용할 구독을 선택 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-141">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span></span> <span data-ttu-id="473a0-142">구독을 선택했으면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-142">When you have selected your subscriptions, click **Close**.</span></span>
   
   ![구독 대화 상자 관리][05]

5. <span data-ttu-id="473a0-144">**Azure 웹앱 컨테이너에 배포** 대화 상자가 나타나는 경우 이전에 만든 웹앱 컨테이너가 표시됩니다. 컨테이너를 만들지 않은 경우에는 목록이 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-144">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Azure 웹앱 컨테이너에 배포 대화 상자][06]

6. <span data-ttu-id="473a0-146">이전에 Azure 웹앱 컨테이너를 만들지 않은 경우 또는 응용 프로그램을 새 컨테이너에 게시하려는 경우 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-146">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="473a0-147">그렇지 않으면 기존 웹앱 컨테이너를 선택하고 아래의 7단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-147">Otherwise, select an existing Web App Container and skip to step 7 below.</span></span>
   
   <span data-ttu-id="473a0-148">a.</span><span class="sxs-lookup"><span data-stu-id="473a0-148">a.</span></span> <span data-ttu-id="473a0-149">**새로 만들기...**</span><span class="sxs-lookup"><span data-stu-id="473a0-149">Click **New...**</span></span>
      
      ![Azure 웹앱 컨테이너에 배포 대화 상자][15]

   <span data-ttu-id="473a0-151">b.</span><span class="sxs-lookup"><span data-stu-id="473a0-151">b.</span></span> <span data-ttu-id="473a0-152">**새 웹앱 컨테이너** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-152">The **New Web App Container** dialog box will be displayed:</span></span>
      
      ![새 웹앱 컨테이너 대화 상자][07a]

   <span data-ttu-id="473a0-154">다.</span><span class="sxs-lookup"><span data-stu-id="473a0-154">c.</span></span> <span data-ttu-id="473a0-155">웹앱 컨테이너에 **DNS 레이블**을 입력합니다. 이렇게 하면 Azure에서 웹 응용 프로그램에 대한 호스트 URL의 리프 DNS 레이블을 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-155">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="473a0-156">(이름은 사용 가능해야 하며, Azure 웹앱 명명 요구 사항을 준수해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="473a0-156">(Note that the name must be available and conform to Azure Web App naming requirements.)</span></span>

   <span data-ttu-id="473a0-157">d.</span><span class="sxs-lookup"><span data-stu-id="473a0-157">d.</span></span> <span data-ttu-id="473a0-158">**웹 컨테이너** 드롭다운 메뉴에서 응용 프로그램에 적절한 소프트웨어를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-158">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="473a0-159">현재, Tomcat 8, Tomcat 7, Jetty 9 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-159">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="473a0-160">선택한 소프트웨어의 최근 배포는 Azure에서 제공되며, Oracle에서 만들고 Azure에서 제공되는 JDK 8의 최근 배포에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-160">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="473a0-161">e.</span><span class="sxs-lookup"><span data-stu-id="473a0-161">e.</span></span> <span data-ttu-id="473a0-162">**구독** 드롭다운 메뉴에서 이 배포에 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-162">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="473a0-163">f.</span><span class="sxs-lookup"><span data-stu-id="473a0-163">f.</span></span> <span data-ttu-id="473a0-164">**리소스 그룹** 드롭다운 메뉴에서 웹앱을 연결할 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-164">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="473a0-165">(Azure 리소스 그룹을 사용하여 함께 삭제할 수 있도록 관련된 리소스를 그룹화할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="473a0-165">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="473a0-166">기존 리소스 그룹(있는 경우)을 선택하고 아래 g 단계로 건너뛰거나 이들 단계를 통해 새 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-166">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span></span>
      
   * <span data-ttu-id="473a0-167">**새로 만들기...**</span><span class="sxs-lookup"><span data-stu-id="473a0-167">Click **New...**</span></span>
   * <span data-ttu-id="473a0-168">**새 리소스 그룹** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-168">The **New Resource Group** dialog box will be displayed:</span></span>
        
       ![새 리소스 그룹 대화 상자][08]
   * <span data-ttu-id="473a0-170">**이름** 텍스트 상자에서 새 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-170">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
   * <span data-ttu-id="473a0-171">**지역** 드롭다운 메뉴에서 리소스 그룹에 적합한 Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-171">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
   * <span data-ttu-id="473a0-172">선택 사항: 기본적으로 Java 8 최신 배포판은 Azure가 자동으로 웹앱 컨테이너에 JVM으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span></span> <span data-ttu-id="473a0-173">그러나 웹앱에서 요구하는 경우 JVM의 다른 버전 및 배포판을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-173">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span></span> <span data-ttu-id="473a0-174">웹앱에 대한 JDK를 지정하려면 **JDK** 탭을 클릭하고 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-174">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span></span>
     * <span data-ttu-id="473a0-175">**Azure Web Apps에서 제공하는 기본 JDK 배포**: 이 옵션을 선택하면 Java 8 최신 배포판이 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-175">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
     * <span data-ttu-id="473a0-176">**Azure에 제공되는 타사 JDK 배포**: 이 옵션을 선택하면 Microsoft Azure에서 제공하는 JDK 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-176">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span></span>
     * <span data-ttu-id="473a0-177">**이 다운로드 위치에서 나의 고유한 JDK 배포**: 이 옵션을 선택하면 사용자 고유의 JDK 배포판을 지정할 수 있으며, 사용자 고유의 배포판을 ZIP 파일로 패키지하여 공개적으로 이용 가능한 다운로드 위치 또는 사용자가 액세스 권한을 갖고 있는 Azure Storage 계정에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-177">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span></span>
          
       ![새 웹앱 컨테이너 대화 상자][07b]

   <span data-ttu-id="473a0-179">g.</span><span class="sxs-lookup"><span data-stu-id="473a0-179">g.</span></span> <span data-ttu-id="473a0-180">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-180">Click **OK**.</span></span>

   <span data-ttu-id="473a0-181">h.</span><span class="sxs-lookup"><span data-stu-id="473a0-181">h.</span></span> <span data-ttu-id="473a0-182">**App Service 계획** 드롭다운 메뉴에 선택한 리소스 그룹과 연결된 App Service 계획이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-182">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="473a0-183">(App Service 계획은 웹앱의 위치, 가격 책정 계층, 계산 인스턴스 크기 등의 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-183">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="473a0-184">App Service 계획 하나를 여러 Web Apps에 사용할 수 있기 때문에 App Service 계획은 특정 웹앱 배포와는 별도로 관리됩니다.)</span><span class="sxs-lookup"><span data-stu-id="473a0-184">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * <span data-ttu-id="473a0-185">**새로 만들기...**</span><span class="sxs-lookup"><span data-stu-id="473a0-185">Click **New...**</span></span>
      * <span data-ttu-id="473a0-186">**새 App Service 계획** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-186">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![새 App Service 계획 대화 상자][09]
      * <span data-ttu-id="473a0-188">**이름** 텍스트 상자에서 새 App Service 계획의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-188">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="473a0-189">**위치** 드롭다운 메뉴에서 계획에 적합한 Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-189">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="473a0-190">**가격 책정 계층** 드롭다운 메뉴에서 계획에 적합한 가격 책정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-190">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="473a0-191">테스트 목적으로 **무료**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-191">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="473a0-192">**인스턴스 크기** 드롭다운 메뉴에서 계획에 적절한 인스턴스 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-192">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="473a0-193">테스트 목적으로 **Small**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-193">For testing purposes you can choose **Small**.</span></span>

   <span data-ttu-id="473a0-194">i.</span><span class="sxs-lookup"><span data-stu-id="473a0-194">i.</span></span> <span data-ttu-id="473a0-195">위 단계를 모두 완료한 경우 New Web App Container 대화 상자가 다음 그림과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-195">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![새 웹앱 컨테이너 대화 상자][10]

   <span data-ttu-id="473a0-197">j.</span><span class="sxs-lookup"><span data-stu-id="473a0-197">j.</span></span> <span data-ttu-id="473a0-198">**확인** 을 클릭하여 새 웹앱 컨테이너 만들기를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-198">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="473a0-199">웹 앱 컨테이너의 목록이 새로 고쳐지도록 몇 초 간 기다리고 나면 새로 만든 웹 앱 컨테이너를 목록에서 선택할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-199">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

7. <span data-ttu-id="473a0-200">이제 Azure에 웹앱의 초기 배포를 완료할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-200">You are now ready to complete the initial deployment of your Web App to Azure:</span></span>
   
   ![Azure 웹앱 컨테이너에 배포 대화 상자][11]
   
   <span data-ttu-id="473a0-202">**확인** 을 클릭하여 선택한 웹앱 컨테이너에 Java 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-202">Click **OK** to deploy your Java application to the selected Web App container.</span></span>
   
   <span data-ttu-id="473a0-203">기본적으로 응용 프로그램은 응용 프로그램 서버의 하위 디렉터리로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-203">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="473a0-204">루트 응용 프로그램으로 배포하려면 **확인**을 클릭하기 전에 **루트에 배포** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-204">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>

8. <span data-ttu-id="473a0-205">이제 웹앱의 배포 상태를 나타내는 **Azure 동작 로그** 보기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-205">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Azure 동작 로그][12]
   
   <span data-ttu-id="473a0-207">Azure에 웹앱을 배포하는 프로세스는 몇 초 내에 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-207">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="473a0-208">응용 프로그램이 준비되면 **게시됨** in the **게시됨** 이라는 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-208">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="473a0-209">이 링크를 클릭하면 배포된 웹앱의 홈 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-209">When you click the link, it will take you to your deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="473a0-210">웹앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="473a0-210">Updating your web app</span></span>

<span data-ttu-id="473a0-211">실행 중인 기존 Azure 웹앱을 빠르고 쉽게 업데이트할 수 있으며, 두 가지 업데이트 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-211">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="473a0-212">기존 Java 웹앱의 배포를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-212">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="473a0-213">동일한 웹앱 컨테이너에 추가 Java 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-213">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="473a0-214">두 경우 모두 프로세스는 동일하며 몇 초만 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-214">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="473a0-215">Eclipse Project Explorer에서 업데이트하거나 기존 웹앱 컨테이너에 추가할 Java 응용 프로그램을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-215">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>

2. <span data-ttu-id="473a0-216">상황에 맞는 메뉴가 나타나면 **Azure**를 선택한 다음 **Azure 웹앱으로 게시...** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-216">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>

3. <span data-ttu-id="473a0-217">이전에 이미 로그인했으므로 기존 웹앱 컨테이너 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-217">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="473a0-218">Java 응용 프로그램을 게시하거나 다시 게시할 컨테이너를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-218">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="473a0-219">몇 초 후 **Azure 동작 로그** 보기에 업데이트된 배포가 **게시됨**으로 표시되고, 웹 브라우저에서 업데이트된 응용 프로그램을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-219">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="473a0-220">기존 웹앱 시작, 중지 또는 다시 시작</span><span class="sxs-lookup"><span data-stu-id="473a0-220">Starting, stopping, or restarting an existing web app</span></span>

<span data-ttu-id="473a0-221">기존 Azure 웹앱 컨테이너(여기에 배포된 모든 Java 응용 프로그램 포함)를 시작 또는 중지하려면 **Azure 탐색기** 보기를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-221">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="473a0-222">**Azure 탐색기** 보기가 열려 있지 않은 경우 Eclipse에서 **Window** 메뉴를 클릭한 다음 **보기 표시**, **기타...**, **Azure**, **Azure 탐색기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-222">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="473a0-223">이전에 로그인하지 않은 경우 로그인하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-223">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="473a0-224">**Azure 탐색기** 보기가 표시되면 다음 단계에 따라 웹앱을 시작하거나 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-224">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="473a0-225">**Azure** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-225">Expand the **Azure** node.</span></span>

2. <span data-ttu-id="473a0-226">**Web Apps** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-226">Expand the **Web Apps** node.</span></span> 

3. <span data-ttu-id="473a0-227">원하는 웹앱을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-227">Right-click the desired Web App.</span></span>

4. <span data-ttu-id="473a0-228">상황에 맞는 메뉴가 나타나면 **시작**, **중지** 또는 **다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-228">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="473a0-229">메뉴 선택 항목은 상황별로 변경되므로 실행 중인 웹앱만 중지하고, 현재 실행되고 있지 않은 웹앱만 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="473a0-229">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![기존 웹앱 중지][13]

## <a name="next-steps"></a><span data-ttu-id="473a0-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="473a0-231">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="473a0-232">Azure Web Apps 만들기에 대한 자세한 내용은 [Web Apps 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="473a0-232">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Eclipse용 Azure 도구 키트 설치]: azure-toolkit-for-eclipse.md
[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ../intellij/azure-toolkit-for-intellij.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Web Apps 개요]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Updated Version]: azure-toolkit-for-eclipse-create-hello-world-web-app.md
[eclipse-sign-in-instructions]: azure-toolkit-for-eclipse-sign-in-instructions.md


<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/02-Dynamic-Web-Project.png
[03]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/03-Context-Menu.png
[04]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/04-Log-In-Dialog.png
[05]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/05-Manage-Subscriptions-Dialog.png
[06]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/07b-New-Web-App-Container-Dialog.png
[08]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/08-New-Resource-Group-Dialog.png
[09]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/09-New-Service-Plan-Dialog.png
[10]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/11-Completed-Deploy-Dialog.png
[12]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/12-Activity-Log-View.png
[13]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/13-Azure-Explorer-Web-App.png
[14]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/14-publishDropdownButton.png
[15]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/15-New-Azure-Web-Container.png
