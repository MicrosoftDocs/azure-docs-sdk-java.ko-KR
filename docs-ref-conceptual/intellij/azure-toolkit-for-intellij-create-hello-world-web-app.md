---
title: "IntelliJ에서 기본 Azure Web App 만들기"
description: "이 자습서에서는 IntelliJ용 Azure 도구 키트를 사용하여 Azure용 Hello World 웹앱을 만드는 방법을 보여 줍니다."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: 323ce74f2d4dad10460a0c2bc0fb59f2bbdbbf3c
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="86a09-103">IntelliJ에서 기본 Azure Web App 만들기</span><span class="sxs-lookup"><span data-stu-id="86a09-103">Create a basic Azure web app in IntelliJ</span></span>

<span data-ttu-id="86a09-104">이 자습서에서는 [IntelliJ용 Azure 도구 키트]를 사용하여 기본 Hello World 응용 프로그램을 만들고 Azure에 웹앱으로 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
> 
> <span data-ttu-id="86a09-105">IntelliJ용 Azure 도구 키트는 2017년 8월에 다른 워크플로로 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-105">The Azure Toolkit for IntelliJ was updated in August 2017, with a different workflow.</span></span> <span data-ttu-id="86a09-106">이 점을 염두에 두고 이 문서는 두 가지 섹션으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-106">With that in mind, this article contains two different sections:</span></span>
>
> * <span data-ttu-id="86a09-107">첫 번째 섹션에서는 IntelliJ용 Azure 도구 키트의 2017년 8월(또는 이후) 버전을 사용하여 Hello World 웹앱을 만드는 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-107">The first section illustrates creating a Hello World web app by using the August 2017 (or later) version of the Azure Toolkit for IntelliJ.</span></span>
>
> * <span data-ttu-id="86a09-108">이 문서의 두 번째 섹션에서는 도구 키트의 2017년 8월(또는 이전) 버전을 사용하여 Hello World 웹앱을 만드는 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-108">The second section of this article demonstrates creating a Hello World web app by using the April 2017 (or earlier) version of the toolkit.</span></span>
> 

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-hello-world-web-app-by-using-the-version-307-or-later-toolkit"></a><span data-ttu-id="86a09-109">도구 키트 버전 3.0.7 이상을 사용하여 Hello World 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="86a09-109">Create a Hello World web app by using the version 3.0.7 or later toolkit</span></span>

### <a name="create-a-new-web-app-project"></a><span data-ttu-id="86a09-110">새 웹앱 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="86a09-110">Create a new web app project</span></span>

1. <span data-ttu-id="86a09-111">IntelliJ를 시작하고 [IntelliJ용 Azure 도구 키트에 대한 로그인 지침] 문서의 단계를 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-111">Start IntelliJ and sign-in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="86a09-112">**파일** 메뉴, **새로 만들기**를 차례로 클릭한 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-112">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![새 프로젝트 만들기][file-new-project]

1. <span data-ttu-id="86a09-114">**새 프로젝트** 대화 상자에서 **Maven**, **maven-archetype-webapp**을 차례로 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-114">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Maven archetype webapp 선택][maven-archetype-webapp]
   
1. <span data-ttu-id="86a09-116">웹앱에 대해 **GroupId** 및 **ArtifactId**를 지정한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-116">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![GroupId 및 ArtifactId 지정][groupid-and-artifactid]

1. <span data-ttu-id="86a09-118">Maven 설정을 사용자 지정하거나 기본값을 적용한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-118">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Maven 설정 지정][maven-options]

1. <span data-ttu-id="86a09-120">프로젝트 이름 및 위치를 지정한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-120">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![프로젝트 이름 지정][project-name]

1. <span data-ttu-id="86a09-122">IntelliJ의 Project Explorer 보기 내에서 **src**, **main**, **webapp**을 차례로 확장한 다음 **index.jsp**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-122">Within IntelliJ's Project Explorer view, expand **src**, then **main**, then **webapp**, and then double-click **index.jsp**.</span></span>
   
   ![인덱스 페이지 열기][open-index-page]

1. <span data-ttu-id="86a09-124">IntelliJ에서 index.jsp 파일이 열리면 **Hello World!**를 동적으로 표시하도록 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-124">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="86a09-125">기존 `<body>` 요소 내.</span><span class="sxs-lookup"><span data-stu-id="86a09-125">within the existing `<body>` element.</span></span> <span data-ttu-id="86a09-126">업데이트된 `<body>` 콘텐츠는 다음 예제와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-126">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![인덱스 페이지 편집][edit-index-page]

1. <span data-ttu-id="86a09-128">index.jsp를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-128">Save index.jsp.</span></span>

### <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="86a09-129">Azure에 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="86a09-129">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="86a09-130">IntelliJ의 Project Explorer 보기 내에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**, **웹앱 실행**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-130">Within IntelliJ's Project Explorer view, right-click your project, choose **Azure**, and then choose **Run on Web App**.</span></span>
   
   ![[웹앱 실행] 메뉴][run-on-web-app-menu]

1. <span data-ttu-id="86a09-132">[웹앱 실행] 대화 상자에서 다음 옵션 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-132">In the Run on Web App dialog box, you can choose one of the following options:</span></span>

   * <span data-ttu-id="86a09-133">기존 웹앱을 선택한 후(있는 경우) **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-133">Choose an existing web app (if one exists), and then click **Run**.</span></span>

      ![[웹앱 실행] 대화 상자][run-on-web-app-dialog]

   * <span data-ttu-id="86a09-135">**새 웹앱 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-135">Click **Create New Web App**.</span></span> <span data-ttu-id="86a09-136">새 웹앱 만들기를 선택한 경우 웹앱에 대한 필수 정보를 지정한 후 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-136">If you choose to create a new web app, specify the requisite information for your web app, and then click **Run**.</span></span>

      ![새 웹앱 만들기][create-new-web-app-dialog]

1. <span data-ttu-id="86a09-138">도구 키트에는 웹앱이 성공적으로 배포될 때 상태 메시지가 표시되며 배포된 웹앱의 URL도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-138">The toolkit will display a status message when it has successfully deployed your web app, which will also display the URL of your deployed web app.</span></span>

   ![배포 정상 완료][successfully-deployed]

1. <span data-ttu-id="86a09-140">상태 메시지에 제공된 링크를 사용하여 웹앱으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-140">You can browse to your web app using the link provided in the status message.</span></span>

   ![웹앱 찾아보기][browse-web-app]

1. <span data-ttu-id="86a09-142">웹앱을 게시한 후 설정은 기본값으로 저장되고 도구 모음에서 녹색 화살표 아이콘을 클릭하여 Azure에서 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-142">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="86a09-143">웹앱에 대한 드롭다운 메뉴를 클릭하여 설정을 수정하고 **구성 편집**을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-143">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![[구성 편집] 메뉴][edit-configuration-menu]

1. <span data-ttu-id="86a09-145">**실행/디버그 구성** 대화 상자가 표시되면 기본 설정을 수정한 다음 **확인**을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-145">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![[구성 편집] 대화 상자][edit-configuration-dialog]

<hr />

## <a name="create-a-hello-world-web-app-by-using-the-version-306-or-earlier-toolkit"></a><span data-ttu-id="86a09-147">도구 키트 버전 3.0.6 이하를 사용하여 Hello World 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="86a09-147">Create a Hello World web app by using the version 3.0.6 or earlier toolkit</span></span>

### <a name="create-a-new-web-app-project"></a><span data-ttu-id="86a09-148">새 웹앱 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="86a09-148">Create a new web app project</span></span>

1. <span data-ttu-id="86a09-149">IntelliJ를 시작하고 **File** 메뉴를 클릭한 후 **New**를 클릭하고 **Project**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-149">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![파일 새로 만들기 프로젝트][02]

2. <span data-ttu-id="86a09-151">**New Project** 대화 상자에서 **Java**를 선택하고 **Web Application**을 선택한 후 **New**를 클릭하여 프로젝트 SDK를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-151">In the **New Project** dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
   ![새 프로젝트 대화 상자][03a]
   
3. <span data-ttu-id="86a09-153">Select Home Directory for JDK 대화 상자에서 JDK가 설치되어 있는 폴더를 선택한 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-153">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="86a09-154">New Project 대화 상자에서 **Next**를 클릭하여 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-154">Click **Next** in the New Project dialog box to continue.</span></span>
   
   ![JDK 홈 디렉터리 지정][03b]

4. <span data-ttu-id="86a09-156">이 자습서의 목적에 따라 프로젝트의 이름을 **Java-Web-App-On-Azure**로 지정하고 **Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-156">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
   ![새 프로젝트 대화 상자][04]

5. <span data-ttu-id="86a09-158">IntelliJ의 Project Explorer 보기 내에서 **Java-Web-App-On-Azure**를 확장한 다음 **web**을 확장하고 **index.jsp**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-158">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
   ![인덱스 페이지 열기][05c]

6. <span data-ttu-id="86a09-160">IntelliJ에서 index.jsp 파일이 열리면 **Hello World!**를 동적으로 표시하도록 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-160">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="86a09-161">기존 `<body>` 요소 내.</span><span class="sxs-lookup"><span data-stu-id="86a09-161">within the existing `<body>` element.</span></span> <span data-ttu-id="86a09-162">업데이트된 `<body>` 콘텐츠는 다음 예제와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-162">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

7. <span data-ttu-id="86a09-163">index.jsp를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-163">Save index.jsp.</span></span>

### <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="86a09-164">Azure에 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="86a09-164">Deploy your web app to Azure</span></span>
<span data-ttu-id="86a09-165">몇 가지 방법으로 Azure에 Java 웹앱을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-165">There are several ways by which you can deploy a Java web app to Azure.</span></span> <span data-ttu-id="86a09-166">이 자습서에서는 가장 간단한 방법 중 하나를 설명합니다. 즉, 특별한 프로젝트 형식이나 추가 도구 없이 Azure 웹앱 컨테이너에 응용 프로그램을 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-166">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="86a09-167">JDK 및 웹 컨테이너 소프트웨어는 Azure에서 제공되므로 별도로 업로드할 필요가 없습니다. Java 웹앱만 있으면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-167">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="86a09-168">따라서 응용 프로그램 게시 프로세스에 걸리는 시간이 몇 분이 아니라 몇 초입니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-168">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="86a09-169">응용 프로그램을 게시하기 전에 먼저 모듈 설정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-169">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="86a09-170">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-170">To do so, use the following steps:</span></span>

1. <span data-ttu-id="86a09-171">IntelliJ의 Project Explorer에서 **Java-Web-App-On-Azure** 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-171">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="86a09-172">상황에 맞는 메뉴가 나타나면 **모듈 설정 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-172">When the context menu appears, click **Open Module Settings**.</span></span>

   ![모듈 설정 열기][05a]

2. <span data-ttu-id="86a09-174">프로젝트 구조 대화 상자가 나타나면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-174">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="86a09-175">a.</span><span class="sxs-lookup"><span data-stu-id="86a09-175">a.</span></span> <span data-ttu-id="86a09-176">**프로젝트 설정** 목록에서 **아티팩트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-176">Click **Artifacts** in the list of **Project Settings**.</span></span>

   <span data-ttu-id="86a09-177">b.</span><span class="sxs-lookup"><span data-stu-id="86a09-177">b.</span></span> <span data-ttu-id="86a09-178">**이름** 상자에서 아티팩트 이름에 공백 또는 특수 문자가 포함되지 않도록 이름을 변경합니다. 이 작업은 해당 이름이 URI(Uniform Resource Identifier)에 사용되기 때문에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-178">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>

   <span data-ttu-id="86a09-179">c.</span><span class="sxs-lookup"><span data-stu-id="86a09-179">c.</span></span> <span data-ttu-id="86a09-180">**형식**을 **웹 응용 프로그램: 보관**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-180">Change the **Type** to **Web Application: Archive**.</span></span>

   <span data-ttu-id="86a09-181">d.</span><span class="sxs-lookup"><span data-stu-id="86a09-181">d.</span></span> <span data-ttu-id="86a09-182">**확인**을 클릭하여 프로젝트 구조 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-182">Click **OK** to close the Project Structure dialog box.</span></span>

   ![모듈 설정 열기][05b]

<span data-ttu-id="86a09-184">모듈 설정을 구성한 경우 다음 단계를 사용하여 Azure에 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-184">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="86a09-185">IntelliJ의 Project Explorer에서 **Java-Web-App-On-Azure** 프로젝트를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-185">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="86a09-186">상황에 맞는 메뉴가 나타나면 **Azure**를 선택한 다음 **Azure 웹앱으로 게시...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-186">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
   ![Azure 게시 상황에 맞는 메뉴][06]

2. <span data-ttu-id="86a09-188">IntelliJ에서 Azure에 로그인하지 않은 경우 Azure 계정으로 로그인하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-188">If you have not already signed in to Azure from IntelliJ, you will be prompted to sign in to your Azure account.</span></span> <span data-ttu-id="86a09-189">Azure 계정이 여러 개 있으면 로그인 프로세스 중에 일부 메시지가 동일한 것이더라도 두 번 이상 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-189">(If you have multiple Azure accounts, some of the prompts during the sign-in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="86a09-190">이 경우 로그인 지침에 따라 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-190">When this happens, continue to follow the sign-in instructions.)</span></span>
   
   ![Azure 로그인 대화 상자][07]

3. <span data-ttu-id="86a09-192">Azure 계정에 성공적으로 로그인하면 **구독 관리** 대화 상자에는 자격 증명과 연결된 구독 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-192">After you have successfully signed in to your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="86a09-193">여러 구독이 나열된 경우 특정 하위 집합만 사용하려면 사용하지 않을 구독의 선택을 취소하면 됩니다. 구독을 선택했으면 **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-193">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
   ![구독 관리][08]

4. <span data-ttu-id="86a09-195">**Azure 웹앱 컨테이너에 배포** 대화 상자가 나타나는 경우 이전에 만든 웹앱 컨테이너가 표시됩니다. 컨테이너를 만들지 않은 경우에는 목록이 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-195">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![앱 컨테이너][09]

5. <span data-ttu-id="86a09-197">이전에 Azure 웹앱 컨테이너를 만들지 않은 경우 또는 응용 프로그램을 새 컨테이너에 게시하려는 경우 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-197">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="86a09-198">그렇지 않으면 기존 웹앱 컨테이너를 선택하고 아래의 6단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-198">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   <span data-ttu-id="86a09-199">a.</span><span class="sxs-lookup"><span data-stu-id="86a09-199">a.</span></span> <span data-ttu-id="86a09-200">**+** 기호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-200">Click the **+** sign.</span></span>
      
      ![앱 컨테이너 추가][10]

   <span data-ttu-id="86a09-202">b.</span><span class="sxs-lookup"><span data-stu-id="86a09-202">b.</span></span> <span data-ttu-id="86a09-203">다음 몇 개 단계에서 사용되는 **새 웹앱 컨테이너** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-203">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
      ![새 앱 컨테이너][11a]
   
   <span data-ttu-id="86a09-205">c.</span><span class="sxs-lookup"><span data-stu-id="86a09-205">c.</span></span> <span data-ttu-id="86a09-206">웹앱 컨테이너에 **DNS 레이블**을 입력합니다. 이렇게 하면 Azure에서 웹 응용 프로그램에 대한 호스트 URL의 리프 DNS 레이블을 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-206">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="86a09-207">이름은 사용 가능해야 하며, Azure 웹앱 명명 요구 사항을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-207">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>

   <span data-ttu-id="86a09-208">d.</span><span class="sxs-lookup"><span data-stu-id="86a09-208">d.</span></span> <span data-ttu-id="86a09-209">**웹 컨테이너** 드롭다운 메뉴에서 응용 프로그램에 적절한 소프트웨어를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-209">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="86a09-210">현재, Tomcat 8, Tomcat 7, Jetty 9 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-210">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="86a09-211">선택한 소프트웨어의 최근 배포는 Azure에서 제공되며, Oracle에서 만들고 Azure에서 제공되는 JDK 8의 최근 배포에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-211">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="86a09-212">e.</span><span class="sxs-lookup"><span data-stu-id="86a09-212">e.</span></span> <span data-ttu-id="86a09-213">**구독** 드롭다운 메뉴에서 이 배포에 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-213">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="86a09-214">f.</span><span class="sxs-lookup"><span data-stu-id="86a09-214">f.</span></span> <span data-ttu-id="86a09-215">**리소스 그룹** 드롭다운 메뉴에서 웹앱을 연결할 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-215">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="86a09-216">(Azure 리소스 그룹을 사용하여 함께 삭제할 수 있도록 관련된 리소스를 그룹화할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="86a09-216">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="86a09-217">기존 리소스 그룹(있는 경우)을 선택하고 아래 g 단계로 건너뛰거나 다음 단계를 통해 새 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-217">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="86a09-218">**리소스 그룹** 드롭다운 메뉴에서 **&lt;&lt;새 리소스 그룹 만들기&gt;&gt;**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-218">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="86a09-219">**새 리소스 그룹** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-219">The **New Resource Group** dialog box will be displayed:</span></span>
        
         ![새 리소스 그룹][12]

      * <span data-ttu-id="86a09-221">**이름** 텍스트 상자에서 새 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-221">In the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="86a09-222">**지역** 드롭다운 메뉴에서 리소스 그룹에 적합한 Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-222">In the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="86a09-223">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-223">Click **OK**.</span></span>

   <span data-ttu-id="86a09-224">g.</span><span class="sxs-lookup"><span data-stu-id="86a09-224">g.</span></span> <span data-ttu-id="86a09-225">**앱 서비스 계획** 드롭다운 메뉴에 선택한 리소스 그룹과 연결된 앱 서비스 계획이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-225">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="86a09-226">앱 서비스 계획은 웹 앱, 가격 책정 계층 및 계산 인스턴스 크기의 위치와 같은 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-226">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="86a09-227">App Service 계획 하나를 여러 Web Apps에 사용할 수 있기 때문에 App Service 계획은 특정 웹앱 배포와는 별도로 관리됩니다.)</span><span class="sxs-lookup"><span data-stu-id="86a09-227">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
      <span data-ttu-id="86a09-228">기존 App Service 계획(있는 경우)을 선택하고 아래 h 단계로 건너뛰거나 다음 단계를 통해 새 App Service 계획을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-228">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="86a09-229">**App Service 계획** 드롭다운 메뉴에서 **&lt;&lt;새 App Service 계획 만들기&gt;&gt;**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-229">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="86a09-230">**새 앱 서비스 계획** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-230">The **New App Service Plan** dialog box will be displayed:</span></span>
        
         ![새 앱 서비스 계획][13]

      * <span data-ttu-id="86a09-232">**이름** 텍스트 상자에서 새 App Service 계획의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-232">In the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="86a09-233">**위치** 드롭다운 메뉴에서 계획에 적합한 Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-233">In the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="86a09-234">**가격 책정 계층** 드롭다운 메뉴에서 계획에 적합한 가격 책정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-234">In the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="86a09-235">테스트 목적으로 **무료**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-235">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="86a09-236">**인스턴스 크기** 드롭다운 메뉴에서 계획에 적절한 인스턴스 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-236">In the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="86a09-237">테스트 목적으로 **Small**을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-237">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="86a09-238">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-238">Click **OK**.</span></span>

   <span data-ttu-id="86a09-239">h.</span><span class="sxs-lookup"><span data-stu-id="86a09-239">h.</span></span> <span data-ttu-id="86a09-240">(선택 사항) 기본적으로 Java 8 최신 배포판은 자동으로 Azure에 의해 웹앱 컨테이너에 JVM으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-240">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="86a09-241">그러나 JVM의 다른 버전 및 배포판을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-241">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="86a09-242">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-242">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="86a09-243">**새 웹앱 컨테이너** 대화 상자에서 **JDK** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-243">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="86a09-244">다음 두 가지 옵션 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-244">You can choose from one of the following options:</span></span>
        
         * <span data-ttu-id="86a09-245">Azure에서 제공하는 기본 JDK 배포</span><span class="sxs-lookup"><span data-stu-id="86a09-245">Deploy the default JDK which is offered by Azure</span></span>
         * <span data-ttu-id="86a09-246">Azure에서 사용할 수 있는 추가 JDK 드롭다운 목록에서 타사 JDK 배포</span><span class="sxs-lookup"><span data-stu-id="86a09-246">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
         * <span data-ttu-id="86a09-247">사용자 지정 JDK 배포(이 JDK는 ZIP 파일로 패키지된 후 공개적으로 제공되거나 Azure Storage 계정에 제공되어야 함)</span><span class="sxs-lookup"><span data-stu-id="86a09-247">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
      ![새 앱 컨테이너 JDK 탭][11b]

   <span data-ttu-id="86a09-249">i.</span><span class="sxs-lookup"><span data-stu-id="86a09-249">i.</span></span> <span data-ttu-id="86a09-250">위 단계를 모두 완료한 경우 New Web App Container 대화 상자가 다음 그림과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-250">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![새 앱 컨테이너][14]
   
   <span data-ttu-id="86a09-252">j.</span><span class="sxs-lookup"><span data-stu-id="86a09-252">j.</span></span> <span data-ttu-id="86a09-253">**확인** 을 클릭하여 새 웹앱 컨테이너 만들기를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-253">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="86a09-254">웹 앱 컨테이너의 목록이 새로 고쳐지도록 몇 초 간 기다리고 나면 새로 만든 웹 앱 컨테이너를 목록에서 선택할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-254">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

6. <span data-ttu-id="86a09-255">이제 Azure에 대한 웹앱의 초기 배포를 완료할 준비가 되었습니다. **확인**을 클릭하여 Java 응용 프로그램을 선택한 웹앱 컨테이너에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-255">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="86a09-256">기본적으로 응용 프로그램은 응용 프로그램 서버의 하위 디렉터리로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-256">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="86a09-257">루트 응용 프로그램으로 배포하려면 **확인**을 클릭하기 전에 **루트에 배포** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-257">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
   ![Azure에 배포][15]

7. <span data-ttu-id="86a09-259">이제 웹앱의 배포 상태를 나타내는 **Azure 동작 로그** 보기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-259">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![진행률 표시기][16]
   
   <span data-ttu-id="86a09-261">Azure에 웹앱을 배포하는 프로세스는 몇 초 내에 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-261">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="86a09-262">응용 프로그램이 준비되면 **상태** 열에 **게시됨**이라는 링크가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-262">When your application is ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="86a09-263">이 링크를 클릭하여 배포된 웹앱의 홈페이지로 이동하거나, 다음 섹션의 단계를 사용하여 해당 웹앱으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-263">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

### <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="86a09-264">Azure에서 웹앱 검색</span><span class="sxs-lookup"><span data-stu-id="86a09-264">Browsing to your Web App on Azure</span></span>
<span data-ttu-id="86a09-265">Azure에서 웹앱을 검색하려면 **Azure 탐색기** 보기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-265">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="86a09-266">**Azure 탐색기** 보기가 열려 있지 않은 경우 IntelliJ에서 **View** 메뉴를 클릭한 다음 **Tool Windows**, **Service Explorer**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-266">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="86a09-267">이전에 로그인하지 않은 경우 로그인하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-267">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="86a09-268">**Azure 탐색기** 보기가 표시되면 다음 단계에 따라 웹앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-268">When the **Azure Explorer** view is displayed, follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="86a09-269">**Azure** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-269">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="86a09-270">**웹앱** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-270">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="86a09-271">원하는 웹앱을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-271">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="86a09-272">상황에 맞는 메뉴가 나타나면 **브라우저에서 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-272">When the context menu appears, click **Open in Browser**.</span></span>
   
   ![웹앱 찾아보기][17]

### <a name="updating-your-web-app"></a><span data-ttu-id="86a09-274">웹앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="86a09-274">Updating your web app</span></span>
<span data-ttu-id="86a09-275">실행 중인 기존 Azure 웹앱을 빠르고 쉽게 업데이트할 수 있으며, 두 가지 업데이트 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-275">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="86a09-276">기존 Java 웹앱의 배포를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-276">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="86a09-277">동일한 웹앱 컨테이너에 추가 Java 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-277">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="86a09-278">두 경우 모두 프로세스는 동일하며 몇 초만 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-278">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="86a09-279">IntelliJ Project Explorer에서 업데이트하거나 기존 웹앱 컨테이너에 추가할 Java 응용 프로그램을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-279">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="86a09-280">상황에 맞는 메뉴가 나타나면 **Azure**를 선택한 다음 **Azure 웹앱으로 게시...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-280">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="86a09-281">이전에 이미 로그인했으므로 기존 웹앱 컨테이너 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-281">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="86a09-282">Java 응용 프로그램을 게시하거나 다시 게시할 컨테이너를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-282">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="86a09-283">몇 초 후 **Azure 동작 로그** 보기에 업데이트된 배포가 **게시됨**으로 표시되고, 웹 브라우저에서 업데이트된 응용 프로그램을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-283">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

### <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="86a09-284">기존 웹앱 시작, 중지 또는 다시 시작</span><span class="sxs-lookup"><span data-stu-id="86a09-284">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="86a09-285">기존 Azure 웹앱 컨테이너(여기에 배포된 모든 Java 응용 프로그램 포함)를 시작 또는 중지하려면 **Azure 탐색기** 보기를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-285">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="86a09-286">**Azure 탐색기** 보기가 열려 있지 않은 경우 IntelliJ에서 **View** 메뉴를 클릭한 다음 **Tool Windows**, **Service Explorer**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-286">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="86a09-287">이전에 로그인하지 않은 경우 로그인하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-287">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="86a09-288">**Azure 탐색기** 보기가 표시되면 다음 단계에 따라 웹앱을 시작하거나 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-288">When the **Azure Explorer** view is displayed, follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="86a09-289">**Azure** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-289">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="86a09-290">**웹앱** 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-290">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="86a09-291">원하는 웹앱을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-291">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="86a09-292">상황에 맞는 메뉴가 나타나면 **시작**, **중지** 또는 **다시 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-292">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="86a09-293">메뉴 선택 항목은 상황별로 변경되므로 실행 중인 웹앱만 중지하고, 현재 실행되고 있지 않은 웹앱만 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86a09-293">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![웹 앱 중지][18]

## <a name="next-steps"></a><span data-ttu-id="86a09-295">다음 단계</span><span class="sxs-lookup"><span data-stu-id="86a09-295">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="86a09-296">Azure 웹앱 만들기에 대한 자세한 내용은 [웹앱 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="86a09-296">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[IntelliJ용 Azure 도구 키트]: azure-toolkit-for-intellij.md
[웹앱 개요]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/18-Stop-Web-App.png

[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[run-on-web-app-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[run-on-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
