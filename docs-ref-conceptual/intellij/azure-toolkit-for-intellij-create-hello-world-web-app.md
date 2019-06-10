---
title: IntelliJ를 사용하여 Azure App Service용 Hello World 웹앱 만들기
description: 이 자습서에서는 IntelliJ용 Azure 도구 키트를 사용하여 Azure용 Hello World 웹앱을 만드는 방법을 보여 줍니다.
services: app-service
keywords: Java, Intellij, 웹앱, Azure App Service, Hello World, 빠른 시작
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
ms.openlocfilehash: ae0749ce1ddab971f1a83e2e5e58492fd8ccb287
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65626116"
---
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-intellij"></a><span data-ttu-id="9c409-104">IntelliJ를 사용하여 Azure App Service용 Hello World 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="9c409-104">Create a Hello World web app for Azure App Service using IntelliJ</span></span>

<span data-ttu-id="9c409-105">오픈 소스형 [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) 플러그인을 사용하여 몇 분 만에 기본 Hello World 애플리케이션을 만들고 Azure App Service에 웹앱으로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-105">Using open sourced [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) plugin, creating and deploying a basic Hello World application to Azure App Service as a web app can be done in a few minutes.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9c409-106">Eclipse 사용을 선호하는 경우 [유사한 Eclipse 자습서][eclipse-hello-world]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c409-106">If you prefer using Eclipse, check out our [similar tutorial for Eclipse][eclipse-hello-world].</span></span>
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> <span data-ttu-id="9c409-107">이 자습서를 완료한 후 반드시 리소스를 정리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-107">Don't forget to clean up the resources after you complete this tutorial.</span></span> <span data-ttu-id="9c409-108">이 경우 이 가이드 실행은 체험 계정 할당량을 초과하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-108">In that case, running this guide will not exceed your free account quota.</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-intellij-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a><span data-ttu-id="9c409-109">설치 및 로그인</span><span class="sxs-lookup"><span data-stu-id="9c409-109">Installation and Sign-in</span></span>

1. <span data-ttu-id="9c409-110">IntelliJ IDEA의 설정/기본 설정 대화 상자(Ctrl+Alt+S)에서 **플러그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-110">In IntelliJ IDEA's Settings/Preferences dialog (Ctrl+Alt+S), select **Plugins**.</span></span> <span data-ttu-id="9c409-111">그런 다음, **Marketplace**에서 **Azure Toolkit for IntelliJ**를 찾고 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-111">Then, find the **Azure Toolkit for IntelliJ** in the **Marketplace** and click **Install**.</span></span> <span data-ttu-id="9c409-112">설치가 완료된 후 **다시 시작**을 클릭하여 플러그인을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-112">After installed, click **Restart** to activate the plugin.</span></span> 

   ![Marketplace의 Azure Toolkit for IntelliJ][marketplace]

2. <span data-ttu-id="9c409-114">Azure 계정에 로그인하려면 사이드바 **Azure Explorer**를 연 다음, 위쪽 막대에서(또는 IDEA 메뉴 **도구/Azure/Azure 로그인**에서) **Azure 로그인** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-114">To sign in to your Azure account, open sidebar **Azure Explorer**, and then click the **Azure Sign In** icon in the bar on top (or from IDEA menu **Tools/Azure/Azure Sign in**).</span></span>

   ![IntelliJ Azure 로그인 명령][I01]

3. <span data-ttu-id="9c409-116">**Azure 로그인** 창에서 **디바이스 로그인**을 선택하고 **로그인**([다른 로그인 옵션](azure-toolkit-for-intellij-sign-in-instructions.md))을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-116">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in** ([other sign in options](azure-toolkit-for-intellij-sign-in-instructions.md)).</span></span>

   ![디바이스 로그인을 선택한 Azure 로그인 창][I02]

4. <span data-ttu-id="9c409-118">**Azure 디바이스 로그인** 대화 상자에서 **복사 및 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-118">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![Azure 로그인 대화 상자 창][I03]

5. <span data-ttu-id="9c409-120">브라우저에서, 마지막 단계에서 **복사 및 열기**를 클릭할 때 복사한 디바이스 코드를 붙여넣은 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-120">In the browser, paste your device code (which has been copied when you click **Copy&Open** in last step) and then click **Next**.</span></span>

   ![디바이스 로그인 브라우저][I04]

6. <span data-ttu-id="9c409-122">**구독 선택** 대화 상자에서 사용하려는 구독을 선택한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-122">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![구독 선택 대화 상자][I05]

## <a name="creating-web-app-project"></a><span data-ttu-id="9c409-124">웹앱 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="9c409-124">Creating web app project</span></span>

1. <span data-ttu-id="9c409-125">IntelliJ에서 **파일** 메뉴, **새로 만들기**, **프로젝트**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-125">In IntelliJ, click the **File** menu, then click **New**, and then click **Project**.</span></span>

   ![새 프로젝트 만들기][file-new-project]

2. <span data-ttu-id="9c409-127">**새 프로젝트** 대화 상자에서 **Maven**, **maven-archetype-webapp**을 차례로 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-127">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>

   ![Maven 원어 웹앱 선택][maven-archetype-webapp]

3. <span data-ttu-id="9c409-129">웹앱에 대해 **GroupId** 및 **ArtifactId**를 지정한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-129">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>

   ![GroupId 및 ArtifactId 지정][groupid-and-artifactid]

4. <span data-ttu-id="9c409-131">Maven 설정을 사용자 지정하거나 기본값을 적용한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-131">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>

   ![Maven 설정 지정][maven-options]

5. <span data-ttu-id="9c409-133">프로젝트 이름 및 위치를 지정한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-133">Specify your project name and location, and then click **Finish**.</span></span>

   ![프로젝트 이름 지정][project-name]

6. <span data-ttu-id="9c409-135">프로젝트 탐색기 보기 아래에서 **src/main/webapp/index.jsp** 파일을 열고 다음과 같이 편집한 후 **변경 내용을 저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-135">Under Project Explorer view, open and edit the file **src/main/webapp/index.jsp** as following and **save the changes**:</span></span>

   ```html
   <html>
    <body>
      <b><% out.println("Hello World!"); %></b>
    </body>
   </html>
   ```

   ![인덱스 페이지 편집][edit-index-page]

## <a name="deploying-web-app-to-azure"></a><span data-ttu-id="9c409-137">Azure에 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="9c409-137">Deploying web app to Azure</span></span>

1. <span data-ttu-id="9c409-138">프로젝트 탐색기 보기 아래에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**를 확장한 다음, **Azure에 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-138">Under Project Explorer view, right-click your project, expand **Azure**, then click **Deploy to Azure**.</span></span>

   ![Azure에 배포 메뉴][deploy-to-azure-menu]

1. <span data-ttu-id="9c409-140">Azure에 배포 대화 상자에서 애플리케이션을 기존 Tomcat 웹앱(이미 있는 경우)에 직접 배포할 수 있습니다. 아직 없는 경우 먼저 새 웹앱을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-140">In the Deploy to Azure dialog box, you can directly deploy the application to an existing Tomcat webapp if you already have one, otherwise you should create a new one first.</span></span>
   1. <span data-ttu-id="9c409-141">**사용 가능한 웹앱 없음. 새 웹앱을 만들려면 클릭하세요** 링크를 클릭하여 새 웹앱을 만들 수 있습니다. 또는 구독에 기존 웹앱이 있는 경우 웹앱 드롭다운 목록에서 **새 웹앱 만들기**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-141">Click the link **No Available webapp, click to create a new one** to crete a new web app, you could choose **Create New WebApp** from WebApp dropdown if there are existing webapps in your subscription.</span></span>

      ![Azure 대화 상자에 배포][deploy-to-azure-dialog]

   1. <span data-ttu-id="9c409-143">팝업 대화 상자에서 웹 컨테이너로 **TOMCAT 8.5-jre8**을 선택하고 다른 필수 정보를 지정한 다음, **확인**을 클릭하여 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-143">In the pop-up dialog box, chose **TOMCAT 8.5-jre8** as Web Container and specify other required information, then click **OK** to create the webapp.</span></span>

      ![새 웹앱 만들기][create-new-web-app-dialog]

   1. <span data-ttu-id="9c409-145">웹앱 드롭다운 목록에서 웹앱을 선택한 다음, **실행**을 클릭합니다. 기존 웹앱에 배포하려는 경우 여기서 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-145">Choose the web app from WebApp drop down, and then click **Run**.(You could start from here if you want deploy to an existing webapp)</span></span>

      ![기존 웹앱에 배포][deploy-to-existing-webapp]

1. <span data-ttu-id="9c409-147">도구 키트에는 웹앱이 성공적으로 배포되면 상태 메시지가 표시되며, 배포에 성공한 경우 배포된 웹앱의 URL도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-147">The toolkit will display a status message when it has successfully deployed your web app, along with the URL of your deployed web app if succeed.</span></span>

   ![배포 정상 완료][successfully-deployed]

1. <span data-ttu-id="9c409-149">상태 메시지에 제공된 링크를 사용하여 웹앱으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-149">You can browse to your web app using the link provided in the status message.</span></span>

   ![웹앱 찾아보기][browse-web-app]

## <a name="managing-deploy-configurations"></a><span data-ttu-id="9c409-151">배포 구성 관리</span><span class="sxs-lookup"><span data-stu-id="9c409-151">Managing deploy configurations</span></span>

1. <span data-ttu-id="9c409-152">웹앱을 게시한 후 설정이 기본값으로 저장되며, 도구 모음에서 녹색 화살표 아이콘을 클릭하여 배포를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-152">After you have published your web app, your settings will be saved as the default, and you can run the deployment by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="9c409-153">웹앱에 대한 드롭다운 메뉴를 클릭하여 설정을 수정하고 **구성 편집**을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-153">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![[구성 편집] 메뉴][edit-configuration-menu]

1. <span data-ttu-id="9c409-155">**실행/디버그 구성** 대화 상자가 표시되면 기본 설정을 수정한 다음 **확인**을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c409-155">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![[구성 편집] 대화 상자][edit-configuration-dialog]

## <a name="cleaning-up-resources"></a><span data-ttu-id="9c409-157">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="9c409-157">Cleaning up resources</span></span>

1. <span data-ttu-id="9c409-158">Azure Explorer에서 웹앱 삭제</span><span class="sxs-lookup"><span data-stu-id="9c409-158">Deleting Web Apps in Azure Explorer</span></span>

     ![리소스 정리][clean-resources]

## <a name="next-steps"></a><span data-ttu-id="9c409-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c409-160">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="9c409-161">Azure Web Apps 만들기에 대한 자세한 내용은 [Web Apps 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c409-161">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Web Apps 개요]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->
[marketplace]:./media/azure-toolkit-for-intellij-create-hello-world-web-app/marketplace.png
[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[deploy-to-azure-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[deploy-to-azure-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[deploy-to-existing-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/deploy-to-existing-webapp.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
[clean-resources]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/clean-resource.png
[I01]: media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-intellij-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-intellij-sign-in-instructions/I05.png
