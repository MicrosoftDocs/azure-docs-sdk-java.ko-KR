---
title: Eclipse를 사용하여 Azure용 Hello World 웹앱 만들기
description: 이 자습서에서는Eclipse용 Azure 도구 키트를 사용하여 Azure용 Hello World 웹앱을 만드는 방법을 보여 줍니다.
services: app-service
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
ms.openlocfilehash: 5e025c90c2619ec72ffddf5815fd49c3ac59c00f
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893094"
---
# <a name="create-a-hello-world-web-app-for-azure-using-eclipse"></a><span data-ttu-id="22b00-103">Eclipse를 사용하여 Azure용 Hello World 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="22b00-103">Create a Hello World web app for Azure using Eclipse</span></span>

<span data-ttu-id="22b00-104">이 자습서에서는 [Eclipse용 Azure 도구 키트 설치]를 사용하여 기본 Hello World 응용 프로그램을 만들고 Azure에 웹앱으로 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for Eclipse].</span></span>

> [!NOTE]
>
> <span data-ttu-id="22b00-105">[IntelliJ용 Azure 도구 키트]를 사용하는 이 문서의 버전에 대한 내용은 [IntelliJ를 사용하여 Azure용 Hello World 웹앱 만들기][intellij-hello-world]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22b00-105">For a version of this article that uses the [Azure Toolkit for IntelliJ], see [Create a Hello World web app for Azure using IntelliJ][intellij-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="22b00-106">Eclipse용 Azure 도구 키트는 2017년 8월에 다른 워크플로로 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-106">The Azure Toolkit for Eclipse was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="22b00-107">이 문서에서는 Eclipse용 Azure 도구 키트 버전 3.0.7 이상을 사용하여 Hello World 웹앱을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-107">This article illustrates creating a Hello World web app by using version 3.0.7 (or later) of the Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="22b00-108">도구 키트 버전 3.0.6 이하를 사용하는 경우 [레거시 도구 키트를 사용하여 Eclipse에서 Azure용 Hello World 웹앱 만들기][Legacy Version]의 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-108">If you are using the version 3.0.6 (or earlier) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in Eclipse using the legacy toolkit][Legacy Version].</span></span>
> 

<span data-ttu-id="22b00-109">이 자습서를 완료한 경우 웹 브라우저에서 응용 프로그램을 보면 다음 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Hello World 앱의 미리 보기][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="22b00-111">새 웹앱 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="22b00-111">Create a new web app project</span></span>

1. <span data-ttu-id="22b00-112">Eclipse를 시작하고, [Eclipse용 Azure 도구 키트에 대한 Azure 로그인 지침][eclipse-sign-in-instructions] 문서의 지침을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-112">Start Eclipse, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse][eclipse-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="22b00-113">**파일**, **새로 만들기**, **동적 웹 프로젝트**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-113">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="22b00-114">(**File**, **New**를 차례로 클릭한 후 **Dynamic Web Project**가 사용 가능한 프로젝트로 표시되지 않는 경우 **File**, **New**, **Project...** 를 차례로 클릭한 후 **Web**을 확장하고 **Dynamic Web Project**를 클릭한 후 **Next**를 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="22b00-114">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

   ![새로운 동적 웹 프로젝트 만들기][file-new-dynamic-web-project]

2. <span data-ttu-id="22b00-116">이 자습서에서는 프로젝트의 이름을 **MyWebApp**으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-116">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="22b00-117">화면이 다음과 유사하게 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-117">Your screen will appear similar to the following:</span></span>
   
   ![새 동적 웹 프로젝트 속성][dynamic-web-project-properties]

3. <span data-ttu-id="22b00-119">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-119">Click **Finish**.</span></span>

4. <span data-ttu-id="22b00-120">Eclipse의 Project Explorer 뷰 내에서 **MyWebApp**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-120">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="22b00-121">**WebContent**를 마우스 오른쪽 단추로 클릭하고 **New**를 클릭한 후 **JSP File**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-121">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

   ![새 JSP 파일 만들기][create-new-jsp-file]

5. <span data-ttu-id="22b00-123">**새 JSP 파일** 대화 상자에서 **index.jsp** 파일의 이름을 지정하고 부모 폴더를 **MyWebApp/WebContent**로 유지한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-123">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

   ![새 JSP 파일 대화 상자][new-jsp-file-dialog]

6. <span data-ttu-id="22b00-125">**JSP 템플릿 선택** 대화 상자에서 이 자습서의 목적에 따라, **새 JSP 파일(html)** 을 선택한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-125">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

   ![JSP 템플릿 선택][select-jsp-template]

7. <span data-ttu-id="22b00-127">Eclipse에서 index.jsp 파일이 열리면 **Hello World!** 를 동적으로 표시하도록 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-127">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="22b00-128">기존 `<body>` 요소 내.</span><span class="sxs-lookup"><span data-stu-id="22b00-128">within the existing `<body>` element.</span></span> <span data-ttu-id="22b00-129">업데이트된 `<body>` 콘텐츠는 다음 예제와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-129">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="22b00-130">index.jsp를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-130">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="22b00-131">Azure에 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="22b00-131">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="22b00-132">Eclipse의 Project Explorer 보기 내에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**, **Azure Web App으로 게시**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-132">Within Eclipse's Project Explorer view, right-click your project, choose **Azure**, and then choose **Publish as Azure Web App**.</span></span>
   
   ![Azure 웹앱으로 게시][publish-as-azure-web-app]

1. <span data-ttu-id="22b00-134">**웹앱 배포** 대화 상자가 나타나면 다음 옵션 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-134">When the **Deploy Web App** dialog box appears, you can choose one of the following options:</span></span>

   * <span data-ttu-id="22b00-135">기존 웹앱이 있으면 기존 웹앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-135">Select an existing web app if one exists.</span></span>

      ![앱 서비스 선택][select-app-service]

   * <span data-ttu-id="22b00-137">**새 웹앱 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-137">Click **Create New Web App**.</span></span>

      ![App Service 만들기][create-app-service]

      <span data-ttu-id="22b00-139">**App Service 만들기** 대화 상자에서 웹앱에 대한 필수 정보를 지정한 후 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-139">Specify the requisite information for your web app in the **Create App Service** dialog box, and then click **Create**.</span></span>

      ![App Service 만들기 대화 상자][create-app-service-dialog]

1. <span data-ttu-id="22b00-141">웹앱을 선택한 다음 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-141">Select your web app and then click **Deploy**.</span></span>

   ![앱 서비스 배포][deploy-app-service]

1. <span data-ttu-id="22b00-143">웹앱이 성공적으로 배포되면 도구 키트가 **Azure 활동 로그** 탭 아래에 **게시됨** 상태를 표시하며, 이것은 배포된 웹앱의 URL에 대한 하이퍼링크입니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-143">The toolkit will display a **Published** status under the **Azure Activity Log** tab when it has successfully deployed your web app, which is a hyperlink for the URL of your deployed web app.</span></span>

   ![게시 상태][publish-status]

1. <span data-ttu-id="22b00-145">상태 메시지에 제공된 링크를 사용하여 웹앱으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-145">You can browse to your web app using the link provided in the status message.</span></span>

   ![웹앱 찾아보기][browse-web-app]

1. <span data-ttu-id="22b00-147">Azure에 웹앱을 게시한 후에는 마우스 오른쪽 단추로 앱을 클릭하고 상황에 맞는 메뉴에서 옵션 중 하나를 선택하여 앱을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-147">After you have published your web to Azure, you can manage your app by right-clicking on it and selecting one of the options on the context menu.</span></span> <span data-ttu-id="22b00-148">예를 들어 웹앱을 **시작**, **중지** 또는 **삭제**할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22b00-148">For example, you can **Start**, **Stop**, or **Delete** your web app.</span></span>

   ![앱 서비스 관리][manage-app-service]

## <a name="next-steps"></a><span data-ttu-id="22b00-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22b00-150">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="22b00-151">Azure Web Apps 만들기에 대한 자세한 내용은 [Web Apps 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22b00-151">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

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
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->

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
