---
title: "Eclipse를 사용하여 기본 Azure Web App 만들기"
description: "이 자습서에서는Eclipse용 Azure 도구 키트를 사용하여 Azure용 Hello World 웹앱을 만드는 방법을 보여 줍니다."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: dcab31ad99fb79a91374d95c2b8b0d9d10346f5f
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="3c8f7-103">Eclipse를 사용하여 기본 Azure Web App 만들기</span><span class="sxs-lookup"><span data-stu-id="3c8f7-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="3c8f7-104">이 자습서에서는 [Eclipse용 Azure 도구 키트]를 사용하여 기본 Hello World 응용 프로그램을 만들고 Azure에 웹앱으로 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="3c8f7-105">기본 JSP 예제는 편의를 위해 표시되지만 Azure 배포가 관련되는 한, 유사한 단계는 Java 서블릿에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="3c8f7-106">이 자습서를 완료한 경우 웹 브라우저에서 응용 프로그램을 보면 다음 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Hello World 앱의 미리 보기][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="3c8f7-108">Hello World 응용 프로그램을 만들려면</span><span class="sxs-lookup"><span data-stu-id="3c8f7-108">To create a Hello World application</span></span>
<span data-ttu-id="3c8f7-109">먼저 java 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-109">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="3c8f7-110">Eclipse를 시작하고 메뉴에서 **File**, **New**, **Dynamic Web Project**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-110">Start Eclipse, and at the menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="3c8f7-111">(**File**, **New**를 차례로 클릭한 후 **Dynamic Web Project**가 사용 가능한 프로젝트로 표시되지 않는 경우 **File**, **New**, **Project...**를 차례로 클릭한 후 **Web**을 확장하고 **Dynamic Web Project**를 클릭한 후 **Next**를 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="3c8f7-111">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

2. <span data-ttu-id="3c8f7-112">이 자습서에서는 프로젝트의 이름을 **MyWebApp**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-112">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="3c8f7-113">화면이 다음과 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-113">Your screen will appear similar to the following:</span></span>
   
   ![새로운 동적 웹 프로젝트 만들기][02]

3. <span data-ttu-id="3c8f7-115">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-115">Click **Finish**.</span></span>

4. <span data-ttu-id="3c8f7-116">Eclipse의 Project Explorer 뷰 내에서 **MyWebApp**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-116">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="3c8f7-117">**WebContent**를 마우스 오른쪽 단추로 클릭하고 **New**를 클릭한 후 **JSP File**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-117">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

5. <span data-ttu-id="3c8f7-118">**새 JSP 파일** 대화 상자에서 **index.jsp** 파일의 이름을 지정하고 부모 폴더를 **MyWebApp/WebContent**로 유지한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-118">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

6. <span data-ttu-id="3c8f7-119">**JSP 템플릿 선택** 대화 상자에서 이 자습서의 목적에 따라, **새 JSP 파일(html)**을 선택한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-119">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

7. <span data-ttu-id="3c8f7-120">Eclipse에서 index.jsp 파일이 열리면 **Hello World!**를 동적으로 표시하도록 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-120">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="3c8f7-121">기존 `<body>` 요소 내.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-121">within the existing `<body>` element.</span></span> <span data-ttu-id="3c8f7-122">업데이트된 `<body>` 콘텐츠는 다음 예제와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-122">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="3c8f7-123">index.jsp를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-123">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="3c8f7-124">Azure Web App 컨테이너에 응용 프로그램을 배포하려면</span><span class="sxs-lookup"><span data-stu-id="3c8f7-124">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="3c8f7-125">몇 가지 방법으로 Azure에 Java 웹 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-125">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="3c8f7-126">이 자습서에서는 가장 간단한 방법 중 하나를 설명합니다. 즉, 특별한 프로젝트 형식이나 추가 도구 없이 Azure 웹앱 컨테이너에 응용 프로그램을 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-126">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="3c8f7-127">JDK 및 웹 컨테이너 소프트웨어는 Azure에서 제공되므로 별도로 업로드할 필요가 없습니다. Java 웹앱만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-127">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="3c8f7-128">따라서 응용 프로그램 게시 프로세스에 걸리는 시간이 몇 분이 아니라 몇 초입니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-128">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="3c8f7-129">Eclipse의 프로젝트 탐색기에서 **MyWebApp**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-129">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>

2. <span data-ttu-id="3c8f7-130">상황에 맞는 메뉴에서 **Azure**를 선택하고 **Azure 웹앱으로 게시...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-130">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
   ![Azure 웹앱으로 게시][03]
   
   <span data-ttu-id="3c8f7-132">또는 프로젝트 탐색기에서 웹 응용 프로그램 프로젝트를 선택한 상태로 도구 모음에서 **게시** 드롭다운 단추를 클릭하고 다음에서 **Azure 웹앱으로 게시**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-132">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span></span>
   
   ![Azure 웹앱으로 게시][14]

3. <span data-ttu-id="3c8f7-134">Eclipse에서 Azure에 로그인하지 않은 경우 Azure 계정으로 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-134">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span></span>
   
   ![Azure 로그인 대화 상자][04]
   
   <span data-ttu-id="3c8f7-136">Azure 계정이 여러 개 있으면 로그인 프로세스 중에 일부 메시지가 동일한 것이더라도 두 번 이상 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-136">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="3c8f7-137">이 경우 로그인 지침에 따라 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-137">When this happens, continue following the sign in instructions.</span></span>

4. <span data-ttu-id="3c8f7-138">Azure 계정에 성공적으로 로그인하면 **구독 관리** 대화 상자에는 자격 증명과 연결된 구독 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-138">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="3c8f7-139">여러 구독이 나열된 경우 특정 하위 집합만 사용하려면 선택적으로 사용할 구독을 선택 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-139">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span></span> <span data-ttu-id="3c8f7-140">구독을 선택했으면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-140">When you have selected your subscriptions, click **Close**.</span></span>
   
   ![구독 대화 상자 관리][05]

5. <span data-ttu-id="3c8f7-142">**Azure 웹앱 컨테이너에 배포** 대화 상자가 나타나는 경우 이전에 만든 웹앱 컨테이너가 표시됩니다. 컨테이너를 만들지 않은 경우에는 목록이 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-142">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Azure 웹앱 컨테이너에 배포 대화 상자][06]

6. <span data-ttu-id="3c8f7-144">이전에 Azure 웹앱 컨테이너를 만들지 않은 경우 또는 응용 프로그램을 새 컨테이너에 게시하려는 경우 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-144">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="3c8f7-145">그렇지 않으면 기존 웹앱 컨테이너를 선택하고 아래의 7단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-145">Otherwise, select an existing Web App Container and skip to step 7 below.</span></span>
   
   <span data-ttu-id="3c8f7-146">a.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-146">a.</span></span> <span data-ttu-id="3c8f7-147">**새로 만들기...**</span><span class="sxs-lookup"><span data-stu-id="3c8f7-147">Click **New...**</span></span>
      
      ![Azure 웹앱 컨테이너에 배포 대화 상자][15]

   <span data-ttu-id="3c8f7-149">b.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-149">b.</span></span> <span data-ttu-id="3c8f7-150">**새 웹앱 컨테이너** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-150">The **New Web App Container** dialog box will be displayed:</span></span>
      
      ![새 웹앱 컨테이너 대화 상자][07a]

   <span data-ttu-id="3c8f7-152">c.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-152">c.</span></span> <span data-ttu-id="3c8f7-153">웹앱 컨테이너에 **DNS 레이블**을 입력합니다. 이렇게 하면 Azure에서 웹 응용 프로그램에 대한 호스트 URL의 리프 DNS 레이블을 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-153">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="3c8f7-154">(이름은 사용 가능해야 하며, Azure 웹앱 명명 요구 사항을 준수해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="3c8f7-154">(Note that the name must be available and conform to Azure Web App naming requirements.)</span></span>

   <span data-ttu-id="3c8f7-155">d.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-155">d.</span></span> <span data-ttu-id="3c8f7-156">**웹 컨테이너** 드롭다운 메뉴에서 응용 프로그램에 적절한 소프트웨어를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-156">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="3c8f7-157">현재, Tomcat 8, Tomcat 7, Jetty 9 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-157">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="3c8f7-158">선택한 소프트웨어의 최근 배포는 Azure에서 제공되며, Oracle에서 만들고 Azure에서 제공되는 JDK 8의 최근 배포에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-158">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="3c8f7-159">e.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-159">e.</span></span> <span data-ttu-id="3c8f7-160">**구독** 드롭다운 메뉴에서 이 배포에 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-160">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="3c8f7-161">f.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-161">f.</span></span> <span data-ttu-id="3c8f7-162">**리소스 그룹** 드롭다운 메뉴에서 웹앱을 연결할 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-162">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="3c8f7-163">(Azure 리소스 그룹을 사용하여 함께 삭제할 수 있도록 관련된 리소스를 그룹화할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="3c8f7-163">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="3c8f7-164">기존 리소스 그룹(있는 경우)을 선택하고 아래 g 단계로 건너뛰거나 이들 단계를 통해 새 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-164">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="3c8f7-165">**새로 만들기...**</span><span class="sxs-lookup"><span data-stu-id="3c8f7-165">Click **New...**</span></span>
      * <span data-ttu-id="3c8f7-166">**새 리소스 그룹** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-166">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![새 리소스 그룹 대화 상자][08]
      * <span data-ttu-id="3c8f7-168">**이름** 텍스트 상자에서 새 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-168">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="3c8f7-169">**지역** 드롭다운 메뉴에서 리소스 그룹에 적합한 Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-169">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="3c8f7-170">선택 사항: 기본적으로 Java 8 최신 배포판은 Azure가 자동으로 웹앱 컨테이너에 JVM으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-170">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span></span> <span data-ttu-id="3c8f7-171">그러나 웹앱에서 요구하는 경우 JVM의 다른 버전 및 배포판을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-171">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span></span> <span data-ttu-id="3c8f7-172">웹앱에 대한 JDK를 지정하려면 **JDK** 탭을 클릭하고 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-172">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span></span>
         * <span data-ttu-id="3c8f7-173">**Azure Web Apps에서 제공하는 기본 JDK 배포**: 이 옵션을 선택하면 Java 8 최신 배포판이 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-173">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
         * <span data-ttu-id="3c8f7-174">**Azure에 제공되는 타사 JDK 배포**: 이 옵션을 선택하면 Microsoft Azure에서 제공하는 JDK 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-174">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span></span>
         * <span data-ttu-id="3c8f7-175">**이 다운로드 위치에서 나의 고유한 JDK 배포**: 이 옵션을 선택하면 사용자 고유의 JDK 배포판을 지정할 수 있으며, 사용자 고유의 배포판을 ZIP 파일로 패키지하여 공개적으로 이용 가능한 다운로드 위치 또는 사용자가 액세스 권한을 갖고 있는 Azure Storage 계정에 업로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-175">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span></span>
          
         ![새 웹앱 컨테이너 대화 상자][07b]

   <span data-ttu-id="3c8f7-177">g.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-177">g.</span></span> <span data-ttu-id="3c8f7-178">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-178">Click **OK**.</span></span>

   <span data-ttu-id="3c8f7-179">h.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-179">h.</span></span> <span data-ttu-id="3c8f7-180">**앱 서비스 계획** 드롭다운 메뉴에 선택한 리소스 그룹과 연결된 앱 서비스 계획이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-180">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="3c8f7-181">(App Service 계획은 웹앱의 위치, 가격 책정 계층, 계산 인스턴스 크기 등의 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-181">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="3c8f7-182">App Service 계획 하나를 여러 Web Apps에 사용할 수 있기 때문에 App Service 계획은 특정 웹앱 배포와는 별도로 관리됩니다.)</span><span class="sxs-lookup"><span data-stu-id="3c8f7-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * <span data-ttu-id="3c8f7-183">**새로 만들기...**</span><span class="sxs-lookup"><span data-stu-id="3c8f7-183">Click **New...**</span></span>
      * <span data-ttu-id="3c8f7-184">**새 앱 서비스 계획** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-184">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![새 App Service 계획 대화 상자][09]
      * <span data-ttu-id="3c8f7-186">**이름** 텍스트 상자에서 새 앱 서비스 계획의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-186">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="3c8f7-187">**위치** 드롭다운 메뉴에서 계획에 적합한 Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-187">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="3c8f7-188">**가격 책정 계층** 드롭다운 메뉴에서 계획에 적합한 가격 책정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-188">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="3c8f7-189">테스트 목적으로 **무료**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-189">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="3c8f7-190">**인스턴스 크기** 드롭다운 메뉴에서 계획에 적절한 인스턴스 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-190">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="3c8f7-191">테스트 목적으로 **Small**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-191">For testing purposes you can choose **Small**.</span></span>

   <span data-ttu-id="3c8f7-192">i.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-192">i.</span></span> <span data-ttu-id="3c8f7-193">위 단계를 모두 완료한 경우 New Web App Container 대화 상자가 다음 그림과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-193">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![새 웹앱 컨테이너 대화 상자][10]

   <span data-ttu-id="3c8f7-195">j.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-195">j.</span></span> <span data-ttu-id="3c8f7-196">**확인** 을 클릭하여 새 웹앱 컨테이너 만들기를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-196">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="3c8f7-197">웹 앱 컨테이너의 목록이 새로 고쳐지도록 몇 초 간 기다리고 나면 새로 만든 웹 앱 컨테이너를 목록에서 선택할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-197">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

7. <span data-ttu-id="3c8f7-198">이제 Azure에 웹앱의 초기 배포를 완료할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-198">You are now ready to complete the initial deployment of your Web App to Azure:</span></span>
   
   ![Azure 웹앱 컨테이너에 배포 대화 상자][11]
   
   <span data-ttu-id="3c8f7-200">**확인** 을 클릭하여 선택한 웹앱 컨테이너에 Java 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-200">Click **OK** to deploy your Java application to the selected Web App container.</span></span>
   
   <span data-ttu-id="3c8f7-201">기본적으로 응용 프로그램은 응용 프로그램 서버의 하위 디렉터리로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-201">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="3c8f7-202">루트 응용 프로그램으로 배포하려면 **확인**을 클릭하기 전에 **루트에 배포** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-202">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>

8. <span data-ttu-id="3c8f7-203">이제 웹앱의 배포 상태를 나타내는 **Azure 동작 로그** 보기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-203">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Azure 동작 로그][12]
   
   <span data-ttu-id="3c8f7-205">Azure에 웹앱을 배포하는 프로세스는 몇 초 내에 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-205">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="3c8f7-206">응용 프로그램이 준비되면 **게시됨** in the **게시됨** 이라는 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-206">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="3c8f7-207">이 링크를 클릭하면 배포된 웹앱의 홈 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-207">When you click the link, it will take you to your deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="3c8f7-208">웹앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="3c8f7-208">Updating your web app</span></span>
<span data-ttu-id="3c8f7-209">실행 중인 기존 Azure 웹앱을 빠르고 쉽게 업데이트할 수 있으며, 두 가지 업데이트 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-209">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="3c8f7-210">기존 Java 웹앱의 배포를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-210">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="3c8f7-211">동일한 웹앱 컨테이너에 추가 Java 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-211">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="3c8f7-212">두 경우 모두 프로세스는 동일하며 몇 초만 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-212">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="3c8f7-213">Eclipse Project Explorer에서 업데이트하거나 기존 웹앱 컨테이너에 추가할 Java 응용 프로그램을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-213">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>

2. <span data-ttu-id="3c8f7-214">상황에 맞는 메뉴가 나타나면 **Azure**를 선택한 다음 **Azure 웹앱으로 게시...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-214">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>

3. <span data-ttu-id="3c8f7-215">이전에 이미 로그인했으므로 기존 웹앱 컨테이너 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-215">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="3c8f7-216">Java 응용 프로그램을 게시하거나 다시 게시할 컨테이너를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-216">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="3c8f7-217">몇 초 후 **Azure 동작 로그** 보기에 업데이트된 배포가 **게시됨**으로 표시되고, 웹 브라우저에서 업데이트된 응용 프로그램을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-217">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="3c8f7-218">기존 웹앱 시작, 중지 또는 다시 시작</span><span class="sxs-lookup"><span data-stu-id="3c8f7-218">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="3c8f7-219">기존 Azure 웹앱 컨테이너(여기에 배포된 모든 Java 응용 프로그램 포함)를 시작 또는 중지하려면 **Azure 탐색기** 보기를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-219">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="3c8f7-220">**Azure 탐색기** 보기가 열려 있지 않은 경우 Eclipse에서 **Window** 메뉴를 클릭한 다음 **보기 표시**, **기타...**, **Azure**, **Azure 탐색기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-220">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="3c8f7-221">이전에 로그인하지 않은 경우 로그인하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-221">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="3c8f7-222">**Azure 탐색기** 보기가 표시되면 다음 단계에 따라 웹앱을 시작하거나 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-222">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="3c8f7-223">**Azure** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-223">Expand the **Azure** node.</span></span>

2. <span data-ttu-id="3c8f7-224">**웹앱** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-224">Expand the **Web Apps** node.</span></span> 

3. <span data-ttu-id="3c8f7-225">원하는 웹앱을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-225">Right-click the desired Web App.</span></span>

4. <span data-ttu-id="3c8f7-226">상황에 맞는 메뉴가 나타나면 **시작**, **중지** 또는 **다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-226">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="3c8f7-227">메뉴 선택 항목은 상황별로 변경되므로 실행 중인 웹앱만 중지하고, 현재 실행되고 있지 않은 웹앱만 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-227">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![기존 웹앱 중지][13]

## <a name="next-steps"></a><span data-ttu-id="3c8f7-229">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3c8f7-229">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="3c8f7-230">Azure 웹앱 만들기에 대한 자세한 내용은 [웹앱 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c8f7-230">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Eclipse용 Azure 도구 키트]: azure-toolkit-for-eclipse.md
[웹앱 개요]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
