---
title: Eclipse를 사용하여 Azure App Service용 Hello World 웹앱 만들기
description: 이 자습서에서는Eclipse용 Azure 도구 키트를 사용하여 Azure용 Hello World 웹앱을 만드는 방법을 보여 줍니다.
services: app-service
keywords: Java, Eclipse, 웹앱, Azure App Service, Hello World, 빠른 시작
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 7e88298afaf0b4601d85d6063b7096c79e677421
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65625828"
---
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-eclipse"></a><span data-ttu-id="896ae-104">Eclipse를 사용하여 Azure App Service용 Hello World 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="896ae-104">Create a Hello World web app for Azure App Service using Eclipse</span></span>

<span data-ttu-id="896ae-105">오픈 소스형 [Azure Toolkit for Eclipse](https://marketplace.eclipse.org/content/azure-toolkit-eclipse) 플러그인을 사용하여 몇 분 만에 기본 Hello World 애플리케이션을 만들고 Azure App Service에 웹앱으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-105">Using open sourced [Azure Toolkit for Eclipse](https://marketplace.eclipse.org/content/azure-toolkit-eclipse) plugin, creating and deploying a basic Hello World application to Azure App Service as a web app can be done in a few minutes.</span></span>

> [!NOTE]
>
> <span data-ttu-id="896ae-106">IntelliJ IDEA 사용을 선호하는 경우 [유사한 IntelliJ 자습서][intellij-hello-world]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="896ae-106">If you prefer using IntelliJ IDEA, check out our [similar tutorial for IntelliJ][intellij-hello-world].</span></span>
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> <span data-ttu-id="896ae-107">이 자습서를 완료한 후 반드시 리소스를 정리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-107">Don't forget to clean up the resources after you complete this tutorial.</span></span> <span data-ttu-id="896ae-108">이 경우 이 가이드 실행은 체험 계정 할당량을 초과하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-108">In that case, running this guide will not exceed your free account quota.</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-eclipse-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a><span data-ttu-id="896ae-109">설치 및 로그인</span><span class="sxs-lookup"><span data-stu-id="896ae-109">Installation and sign-in</span></span>

1. <span data-ttu-id="896ae-110">다음 단추를 실행 중인 Eclipse 작업 영역으로 끌어와서 Azure Toolkit for Eclipse 플러그인([다른 설치 옵션](azure-toolkit-for-eclipse-installation.md))을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-110">Drag the following button to your running Eclipse workspace to install the Azure Toolkit for Eclipse plugin ([other installation options](azure-toolkit-for-eclipse-installation.md)).</span></span>

    <span data-ttu-id="896ae-111">[![실행 중인 Eclipse* 작업 영역으로 끌어옵니다. *Eclipse Marketplace 클라이언트가 필요합니다.](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "실행 중인 Eclipse* 작업 영역으로 끌어옵니다. *Eclipse Marketplace 클라이언트가 필요합니다.")</span><span class="sxs-lookup"><span data-stu-id="896ae-111">[![Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client")</span></span>

1. <span data-ttu-id="896ae-112">Azure 계정에 로그인하려면 **도구**, **Azure**, **로그인**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-112">To sign in to your Azure account, click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="896ae-113">![Azure 로그인을 위한 Eclipse 메뉴][I01]</span><span class="sxs-lookup"><span data-stu-id="896ae-113">![Eclipse Menu for Azure Sign In][I01]</span></span>

1. <span data-ttu-id="896ae-114">**Azure 로그인** 창에서 **디바이스 로그인**을 선택하고 **로그인**([다른 로그인 옵션](azure-toolkit-for-eclipse-sign-in-instructions.md))을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-114">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in** ([other sign-in options](azure-toolkit-for-eclipse-sign-in-instructions.md)).</span></span>

   ![디바이스 로그인을 선택한 Azure 로그인 창][I02]

1. <span data-ttu-id="896ae-116">**Azure 디바이스 로그인** 대화 상자에서 **복사 및 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-116">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![Azure 로그인 대화 상자 창][I03]

1. <span data-ttu-id="896ae-118">브라우저에서, 마지막 단계에서 **복사 및 열기**를 클릭할 때 복사한 디바이스 코드를 붙여넣은 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-118">In the browser, paste your device code (which has been copied when you clicked **Copy&Open** in last step) and then click **Next**.</span></span>

   ![디바이스 로그인 브라우저][I04]

1. <span data-ttu-id="896ae-120">끝으로 **구독 선택** 대화 상자에서 사용하려는 구독을 선택한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-120">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![구독 선택 대화 상자][I05]

## <a name="creating-web-app-project"></a><span data-ttu-id="896ae-122">웹앱 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="896ae-122">Creating web app project</span></span>

1. <span data-ttu-id="896ae-123">**파일**, **새로 만들기**, **동적 웹 프로젝트**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-123">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="896ae-124">(**File**, **New**를 차례로 클릭한 후 **Dynamic Web Project**가 사용 가능한 프로젝트로 표시되지 않는 경우 **File**, **New**, **Project...** 를 차례로 클릭한 후 **Web**을 확장하고 **Dynamic Web Project**를 클릭한 후 **Next**를 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="896ae-124">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

   ![새로운 동적 웹 프로젝트 만들기][file-new-dynamic-web-project]

2. <span data-ttu-id="896ae-126">이 자습서에서는 프로젝트의 이름을 **MyWebApp**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-126">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="896ae-127">화면이 다음과 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-127">Your screen will appear similar to the following:</span></span>
   
   ![새 동적 웹 프로젝트 속성][dynamic-web-project-properties]

3. <span data-ttu-id="896ae-129">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-129">Click **Finish**.</span></span>

4. <span data-ttu-id="896ae-130">Eclipse의 Project Explorer 뷰 내에서 **MyWebApp**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-130">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="896ae-131">**WebContent**를 마우스 오른쪽 단추로 클릭하고 **New**를 클릭한 후 **JSP File**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-131">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

   ![새 JSP 파일 만들기][create-new-jsp-file]

5. <span data-ttu-id="896ae-133">**새 JSP 파일** 대화 상자에서 **index.jsp** 파일의 이름을 지정하고 부모 폴더를 **MyWebApp/WebContent**로 유지한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-133">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

   ![새 JSP 파일 대화 상자][new-jsp-file-dialog]

6. <span data-ttu-id="896ae-135">**JSP 템플릿 선택** 대화 상자에서 이 자습서의 목적에 따라, **새 JSP 파일(html)** 을 선택한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-135">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

   ![JSP 템플릿 선택][select-jsp-template]

7. <span data-ttu-id="896ae-137">Eclipse에서 index.jsp 파일이 열리면 **Hello World!** 를 동적으로 표시하도록 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-137">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="896ae-138">기존 `<body>` 요소 내.</span><span class="sxs-lookup"><span data-stu-id="896ae-138">within the existing `<body>` element.</span></span> <span data-ttu-id="896ae-139">업데이트된 `<body>` 콘텐츠는 다음 예제와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-139">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="896ae-140">index.jsp를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-140">Save index.jsp.</span></span>

## <a name="deploying-web-app-to-azure"></a><span data-ttu-id="896ae-141">Azure에 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="896ae-141">Deploying web app to Azure</span></span>

1. <span data-ttu-id="896ae-142">Eclipse의 Project Explorer 보기 내에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**, **Azure Web App으로 게시**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-142">Within Eclipse's Project Explorer view, right-click your project, choose **Azure**, and then choose **Publish as Azure Web App**.</span></span>
   
   ![Azure 웹앱으로 게시][publish-as-azure-web-app]

1. <span data-ttu-id="896ae-144">**웹앱 배포** 대화 상자가 나타나면 다음 옵션 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-144">When the **Deploy Web App** dialog box appears, you can choose one of the following options:</span></span>

   * <span data-ttu-id="896ae-145">기존 웹앱이 있으면 기존 웹앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-145">Select an existing web app if one exists.</span></span>

      ![앱 서비스 선택][select-app-service]

   * <span data-ttu-id="896ae-147">**새 웹앱 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-147">Click **Create New Web App**.</span></span>

      ![App Service 만들기][create-app-service]

      <span data-ttu-id="896ae-149">**App Service 만들기** 대화 상자에서 웹앱에 대한 필수 정보를 지정한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-149">Specify the requisite information for your web app in the **Create App Service** dialog box, and then click **Create**.</span></span>

      <span data-ttu-id="896ae-150">여기서 런타임 환경, 앱 설정, 서비스 계획 및 리소스 그룹을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-150">Here you can configure the runtime environment, app settings, service plan and resource group.</span></span>

      ![App Service 만들기 대화 상자][create-app-service-dialog]

1. <span data-ttu-id="896ae-152">웹앱을 선택한 다음 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-152">Select your web app and then click **Deploy**.</span></span>

   ![앱 서비스 배포][deploy-app-service]

1. <span data-ttu-id="896ae-154">웹앱이 성공적으로 배포되면 도구 키트가 **Azure 활동 로그** 탭 아래에 **게시됨** 상태를 표시하며, 이것은 배포된 웹앱의 URL에 대한 하이퍼링크입니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-154">The toolkit will display a **Published** status under the **Azure Activity Log** tab when it has successfully deployed your web app, which is a hyperlink for the URL of your deployed web app.</span></span>

   ![게시 상태][publish-status]

1. <span data-ttu-id="896ae-156">상태 메시지에 제공된 링크를 사용하여 웹앱으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-156">You can browse to your web app using the link provided in the status message.</span></span>

   ![웹앱 찾아보기][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="cleaning-up-resources"></a><span data-ttu-id="896ae-158">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="896ae-158">Cleaning up resources</span></span>

1. <span data-ttu-id="896ae-159">Azure에 웹앱을 게시한 후에는 Azure Explorer에서 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 옵션 중 하나를 선택하여 웹앱을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-159">After you have published your web app to Azure, you can manage it by right-clicking in Azure Explorer and selecting one of the options in the context menu.</span></span> <span data-ttu-id="896ae-160">예를 들어 여기서 웹앱을 **삭제**하여 이 자습서의 리소스를 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="896ae-160">For example, you can **Delete** your web app here to clean up the resource for this tutorial.</span></span>

   ![앱 서비스 관리][manage-app-service]

## <a name="next-steps"></a><span data-ttu-id="896ae-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="896ae-162">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="896ae-163">Azure Web Apps 만들기에 대한 자세한 내용은 [Web Apps 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="896ae-163">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Web Apps 개요]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->
[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-eclipse-sign-in-instructions/I05.png

[browse-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/browse-web-app.png
[file-new-dynamic-web-project]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/file-new-dynamic-web-project.png
[dynamic-web-project-properties]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/dynamic-web-project-properties.png
[create-new-jsp-file]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-new-jsp-file.png
[new-jsp-file-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/new-jsp-file-dialog.png
[select-jsp-template]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-jsp-template.png
[publish-as-azure-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-as-azure-web-app.png
[deploy-web-app-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-web-app-dialog.png
[select-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-app-service.png
[create-app-service-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service-dialog.png
[publish-status]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-status.png
[create-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service.png
[deploy-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-app-service.png
[manage-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/manage-app-service.png
