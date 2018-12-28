---
title: IntelliJ를 사용하여 Azure용 Hello World 웹앱 만들기
description: 이 자습서에서는 IntelliJ용 Azure 도구 키트를 사용하여 Azure용 Hello World 웹앱을 만드는 방법을 보여 줍니다.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: cc68e16a6940a1f0f2b08f0b63c90c58ec6dbc4e
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892864"
---
# <a name="create-a-hello-world-web-app-for-azure-using-intellij"></a><span data-ttu-id="fe396-103">IntelliJ를 사용하여 Azure용 Hello World 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="fe396-103">Create a Hello World web app for Azure using IntelliJ</span></span>

<span data-ttu-id="fe396-104">이 자습서에서는 [IntelliJ용 Azure 도구 키트]를 사용하여 기본 Hello World 애플리케이션을 만들고 Azure에 웹앱으로 배포하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
>
> <span data-ttu-id="fe396-105">[Eclipse용 Azure 도구 키트 설치]를 사용하는 이 문서의 버전에 대한 내용은 [Eclipse를 사용하여 Azure용 Hello World 웹앱 만들기][eclipse-hello-world]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe396-105">For a version of this article that uses the [Azure Toolkit for Eclipse], see [Create a Hello World web app for Azure using Eclipse][eclipse-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="fe396-106">IntelliJ용 Azure 도구 키트는 2017년 8월에 다른 워크플로로 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-106">The Azure Toolkit for IntelliJ was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="fe396-107">이 문서에서는 IntelliJ용 Azure 도구 키트 버전 3.0.7 이상을 사용하여 Hello World 웹앱을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-107">This article illustrates creating a Hello World web app by using version 3.0.7 (or later) of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="fe396-108">도구 키트 버전 3.0.6 이하를 사용하는 경우 [레거시 도구 키트를 사용하여 IntelliJ에서 Azure용 Hello World 웹앱 만들기][Legacy Version]의 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-108">If you are using the version 3.0.6 (or earlier) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in IntelliJ using the legacy toolkit][Legacy Version].</span></span>
> 

<span data-ttu-id="fe396-109">이 자습서를 완료한 경우 웹 브라우저에서 응용 프로그램을 보면 다음 그림과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Hello World 앱의 미리 보기][browse-web-app]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="fe396-111">새 웹앱 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="fe396-111">Create a new web app project</span></span>

1. <span data-ttu-id="fe396-112">IntelliJ를 시작하고 [IntelliJ용 Azure 도구 키트에 대한 Azure 로그인 지침][intelliJ-sign-in-instructions] 문서의 지침을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-112">Start IntelliJ, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for IntelliJ][intelliJ-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="fe396-113">**파일** 메뉴, **새로 만들기**를 차례로 클릭한 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-113">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![새 프로젝트 만들기][file-new-project]

1. <span data-ttu-id="fe396-115">**새 프로젝트** 대화 상자에서 **Maven**, **maven-archetype-webapp**을 차례로 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-115">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Maven archetype webapp 선택][maven-archetype-webapp]
   
1. <span data-ttu-id="fe396-117">웹앱에 대해 **GroupId** 및 **ArtifactId**를 지정한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-117">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![GroupId 및 ArtifactId 지정][groupid-and-artifactid]

1. <span data-ttu-id="fe396-119">Maven 설정을 사용자 지정하거나 기본값을 적용한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-119">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Maven 설정 지정][maven-options]

1. <span data-ttu-id="fe396-121">프로젝트 이름 및 위치를 지정한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-121">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![프로젝트 이름 지정][project-name]

1. <span data-ttu-id="fe396-123">IntelliJ의 Project Explorer 보기 내에서 **src**, **main**, **webapp**을 차례로 확장한 다음 **index.jsp**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-123">Within IntelliJ's Project Explorer view, expand **src**, then **main**, then **webapp**, and then double-click **index.jsp**.</span></span>
   
   ![인덱스 페이지 열기][open-index-page]

1. <span data-ttu-id="fe396-125">IntelliJ에서 index.jsp 파일이 열리면 **Hello World!** 를 동적으로 표시하도록 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-125">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="fe396-126">기존 `<body>` 요소 내.</span><span class="sxs-lookup"><span data-stu-id="fe396-126">within the existing `<body>` element.</span></span> <span data-ttu-id="fe396-127">업데이트된 `<body>` 콘텐츠는 다음 예제와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-127">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![인덱스 페이지 편집][edit-index-page]

1. <span data-ttu-id="fe396-129">index.jsp를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-129">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="fe396-130">Azure에 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="fe396-130">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="fe396-131">IntelliJ의 Project Explorer 보기 내에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**, **웹앱 실행**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-131">Within IntelliJ's Project Explorer view, right-click your project, choose **Azure**, and then choose **Run on Web App**.</span></span>
   
   ![[웹앱 실행] 메뉴][run-on-web-app-menu]

1. <span data-ttu-id="fe396-133">[웹앱 실행] 대화 상자에서 다음 옵션 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-133">In the Run on Web App dialog box, you can choose one of the following options:</span></span>

   * <span data-ttu-id="fe396-134">기존 웹앱을 선택한 후(있는 경우) **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-134">Choose an existing web app (if one exists), and then click **Run**.</span></span>

      ![[웹앱 실행] 대화 상자][run-on-web-app-dialog]

   * <span data-ttu-id="fe396-136">**새 웹앱 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-136">Click **Create New Web App**.</span></span> <span data-ttu-id="fe396-137">새 웹앱 만들기를 선택한 경우 웹앱에 대한 필수 정보를 지정한 후 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-137">If you choose to create a new web app, specify the requisite information for your web app, and then click **Run**.</span></span>

      ![새 웹앱 만들기][create-new-web-app-dialog]

1. <span data-ttu-id="fe396-139">도구 키트에는 웹앱이 성공적으로 배포될 때 상태 메시지가 표시되며 배포된 웹앱의 URL도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-139">The toolkit will display a status message when it has successfully deployed your web app, which will also display the URL of your deployed web app.</span></span>

   ![배포 정상 완료][successfully-deployed]

1. <span data-ttu-id="fe396-141">상태 메시지에 제공된 링크를 사용하여 웹앱으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-141">You can browse to your web app using the link provided in the status message.</span></span>

   ![웹앱 찾아보기][browse-web-app]

1. <span data-ttu-id="fe396-143">웹앱을 게시한 후 설정은 기본값으로 저장되고 도구 모음에서 녹색 화살표 아이콘을 클릭하여 Azure에서 애플리케이션을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-143">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="fe396-144">웹앱에 대한 드롭다운 메뉴를 클릭하여 설정을 수정하고 **구성 편집**을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-144">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![[구성 편집] 메뉴][edit-configuration-menu]

1. <span data-ttu-id="fe396-146">**실행/디버그 구성** 대화 상자가 표시되면 기본 설정을 수정한 다음 **확인**을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe396-146">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![[구성 편집] 대화 상자][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="fe396-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fe396-148">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="fe396-149">Azure Web Apps 만들기에 대한 자세한 내용은 [Web Apps 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe396-149">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

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
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

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
