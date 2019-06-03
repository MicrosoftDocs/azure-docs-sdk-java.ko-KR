---
title: IntelliJ용 Azure 도구 키트를 사용하는 클라우드 내의 Linux 컨테이너에서 실행되는 Hello World 웹앱 배포
description: Linux 컨테이너에서 기본 Hello World 웹앱을 실행하여 IntelliJ용 Azure 도구 키트를 사용하는 클라우드에 배포합니다.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/20/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: fdff8dc2bd7a29473314d5c0bc99b7bcda369156
ms.sourcegitcommit: 54e7f077d694a5b1dd7fa6c8870b7d476af9829c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55648727"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="fdee9-103">IntelliJ용 Azure 도구 키트를 사용하는 클라우드 내의 Linux 컨테이너에 Hello World 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="fdee9-103">Deploy a Hello World web app to a Linux container in the cloud using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="fdee9-104">[Docker] 컨테이너는 웹 애플리케이션을 배포하는 데 널리 사용되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-104">[Docker] containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="fdee9-105">개발자는 Docker 컨테이너를 통해 모든 프로젝트 파일과 종속성을 서버에 배포할 단일 패키지로 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="fdee9-106">IntelliJ용 Azure 도구 키트는 Microsoft Azure에 컨테이너 배포를 위한 기능을 추가함으로써 Java 개발자들을 위해 이 프로세스를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding features for to deploy containers to Microsoft Azure.</span></span>

<span data-ttu-id="fdee9-107">이 문서에서는 기본 Hello World 웹앱을 만들고 IntelliJ용 Azure 도구 키트를 사용하여 Linux 컨테이너의 웹앱을 Azure에 게시하는 데 필요한 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-107">This article demonstrates the steps that are required to create a basic Hello World web app and publish your web app in a Linux container to Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* <span data-ttu-id="fdee9-108">[Docker] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="fdee9-108">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="fdee9-109">이 자습서의 단계를 완료하려면 TLS 없이 포트 2375에서 디먼을 노출하도록 [Docker]를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-109">To complete the steps in this tutorial, you need to configure [Docker] to expose the daemon on port 2375 without TLS.</span></span> <span data-ttu-id="fdee9-110">Docker를 설치할 때 또는 Docker 설정 메뉴를 통해 이 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-110">You can configure this setting when installing Docker, or through the Docker settings menu.</span></span>
>
> ![Docker 설정 메뉴][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="fdee9-112">새 웹앱 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="fdee9-112">Create a new web app project</span></span>

1. <span data-ttu-id="fdee9-113">IntelliJ를 시작하고 [IntelliJ용 Azure 도구 키트에 대한 로그인 지침](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions) 문서의 단계를 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-113">Start IntelliJ and sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions) article.</span></span>

1. <span data-ttu-id="fdee9-114">**파일** 메뉴, **새로 만들기**를 차례로 클릭한 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-114">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![새 프로젝트 만들기][file-new-project]

1. <span data-ttu-id="fdee9-116">**새 프로젝트** 대화 상자에서 **Maven**, **maven-archetype-webapp**을 차례로 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-116">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Maven archetype webapp 선택][maven-archetype-webapp]
   
1. <span data-ttu-id="fdee9-118">웹앱에 대해 **GroupId** 및 **ArtifactId**를 지정한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-118">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![GroupId 및 ArtifactId 지정][groupid-and-artifactid]

1. <span data-ttu-id="fdee9-120">Maven 설정을 사용자 지정하거나 기본값을 적용한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-120">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Maven 설정 지정][maven-options]

1. <span data-ttu-id="fdee9-122">프로젝트 이름 및 위치를 지정한 다음 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-122">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![프로젝트 이름 지정][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="fdee9-124">Azure Container Registry를 만들어서 프라이빗 Docker 레지스트리로 사용</span><span class="sxs-lookup"><span data-stu-id="fdee9-124">Create an Azure Container Registry to use as a private Docker registry</span></span>

<span data-ttu-id="fdee9-125">다음 단계에서는 Azure Portal을 사용하여 Azure Container Registry를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-125">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="fdee9-126">Azure Portal 대신 Azure CLI를 사용하려는 경우 [Azure CLI 2.0을 사용하여 프라이빗 Docker 컨테이너 레지스트리 만들기][Create Docker Registry using Azure CLI]의 단계에 따르세요.</span><span class="sxs-lookup"><span data-stu-id="fdee9-126">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0][Create Docker Registry using Azure CLI].</span></span>
>

1. <span data-ttu-id="fdee9-127">[Azure Portal]을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-127">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="fdee9-128">Azure Portal에서 사용자의 계정에 로그인하면 [Azure Portal을 사용하여 개인 Docker 컨테이너 레지스트리 만들기] 문서의 단계를 수행할 수 있습니다. 편의상 다음 단계에서 다시 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-128">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="fdee9-129">**+리소스 만들기**의 메뉴 아이콘을 클릭하고 **컨테이너**를 클릭한 다음, **Container Registry**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-129">Click the menu icon for **+ Create a resource**, then click **Containers**, and then click **Container Registry**.</span></span>
   
   ![새로운 Azure Container Registry 만들기][create-container-registry-01]

1. <span data-ttu-id="fdee9-131">**컨테이너 레지스트리 만들기** 페이지가 표시되면 **레지스트리 이름** 및 **리소스 그룹**을 입력하고 **관리 사용자**에 대해 **사용**을 선택한 다음, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-131">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Azure Container Registry 설정 구성][create-container-registry-02]

## <a name="deploy-your-web-app-in-a-docker-container"></a><span data-ttu-id="fdee9-133">Docker 컨테이너에서 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="fdee9-133">Deploy your web app in a Docker container</span></span>

1. <span data-ttu-id="fdee9-134">프로젝트 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**를 선택한 다음 **Docker 지원 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-134">Right-click your project in the project explorer, choose **Azure**, and then click **Add Docker Support**.</span></span>

   <span data-ttu-id="fdee9-135">기본 구성을 사용하여 Docker 파일이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-135">This will automatically create a Docker file with a default configuration.</span></span>

   ![Docker 지원 추가][add-docker-support]

1. <span data-ttu-id="fdee9-137">Docker 지원을 추가한 후 프로젝트 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**를 선택한 다음 **Web App for Containers에서 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-137">After you have added Docker support, right-click your project in the project explorer, choose **Azure**, and then click **Run on Web App for Containers**.</span></span>

   ![Web App for Containers에서 실행][run-on-web-app-for-containers]

1. <span data-ttu-id="fdee9-139">**Web App for Containers에서 실행** 대화 상자가 표시되면 필수 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-139">When the **Run on Web App for Containers** dialog box is displayed, fill in the requisite information:</span></span>

   * <span data-ttu-id="fdee9-140">**이름**: Azure 도구 키트에 표시되는 친숙한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-140">**Name**: This specifies the friendly name which is displayed in the Azure Toolkit.</span></span> 

   * <span data-ttu-id="fdee9-141">**Container Registry**: 이 문서의 이전 섹션에서 만든 드롭다운 메뉴에서 컨테이너 레지스트리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-141">**Container Registry**: Choose the container registry from the drop-down menu that you created in the previous section of this article.</span></span> <span data-ttu-id="fdee9-142">**서버 URL**, **사용자 이름**, **암호** 필드는 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-142">The fields for **Server URL**, **Username**, and **Password** will be automatically populated.</span></span>

   * <span data-ttu-id="fdee9-143">**이미지 및 태그**: 컨테이너 이미지 이름을 지정합니다. 일반적으로 다음 구문: "*registry*.azurecr.io/*appname*:latest"를 사용합니다. 여기에서</span><span class="sxs-lookup"><span data-stu-id="fdee9-143">**Image and tag**: Specifies the container image name; typically this will use the following syntax: "*registry*.azurecr.io/*appname*:latest", where:</span></span> 
      * <span data-ttu-id="fdee9-144">*registry*는 이 문서의 이전 섹션에서 컨테이너 레지스트리이며</span><span class="sxs-lookup"><span data-stu-id="fdee9-144">*registry* is your container registry from the previous section of this article</span></span> 
      * <span data-ttu-id="fdee9-145">*appname*은 웹앱의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-145">*appname* is the name of your web app</span></span> 

   * <span data-ttu-id="fdee9-146">**기존 웹앱 사용** 또는 **새 웹앱 만들기**: 컨테이너를 기존 웹앱에 배포할지 새 웹앱을 만들지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-146">**Use Existing Web App** or **Create New Web App**: Specifies whether you will deploy your container to an existing web app or create a new web app.</span></span> <span data-ttu-id="fdee9-147">**앱 이름**을 지정하면 웹앱에 대한 URL이 만들어집니다. 예: *wingtiptoys.azurewebsites.net*</span><span class="sxs-lookup"><span data-stu-id="fdee9-147">The **App name** that you specify will create the URL for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   * <span data-ttu-id="fdee9-148">**리소스 그룹**: 기존 리소스 그룹을 사용할지 새 리소스 그룹을 만들지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-148">**Resource Group**: Specifies whether you will use an existing or create a new resource group.</span></span> 

   * <span data-ttu-id="fdee9-149">**App Service 계획**: 기존 앱 서비스 플랜을 사용할지 새로 만들지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-149">**App Service Plan**: Specifies whether you will use an existing or create a new app service plan.</span></span> 

   ![Web App for Containers에서 실행][run-on-web-app-linux]

1. <span data-ttu-id="fdee9-151">위에 나열된 설정을 구성했으면 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-151">When you have finished configuring the settings listed above, click **Run**.</span></span> <span data-ttu-id="fdee9-152">웹앱이 성공적으로 배포된 경우 상태가 **실행** 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-152">When your web app has been successfully deployed, the status will be displayed in the **Run** window.</span></span>

   ![성공적으로 웹앱을 배포했습니다.][successfully-deployed]

1. <span data-ttu-id="fdee9-154">웹앱이 게시된 후에는 웹앱에 대해 이전에 지정한 URL로 이동할 수 있습니다. 예: *wingtiptoys.azurewebsites.net*</span><span class="sxs-lookup"><span data-stu-id="fdee9-154">After your web app has been published, you can browse to the URL that specifed earlier for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   ![웹앱 검색][browsing-to-web-app]

## <a name="optional-modify-your-web-app-publish-settings"></a><span data-ttu-id="fdee9-156">선택 사항: 웹 앱 게시 설정 수정</span><span class="sxs-lookup"><span data-stu-id="fdee9-156">Optional: Modify your web app publish settings</span></span>

1. <span data-ttu-id="fdee9-157">웹앱을 게시한 후 설정은 기본값으로 저장되고 도구 모음에서 녹색 화살표 아이콘을 클릭하여 Azure에서 애플리케이션을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-157">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="fdee9-158">웹앱에 대한 드롭다운 메뉴를 클릭하여 이러한 설정을 수정하고 **구성 편집**을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-158">You can modify these settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![구성 편집 메뉴][edit-configuration-menu]

1. <span data-ttu-id="fdee9-160">**실행/디버그 구성** 대화 상자가 표시되면 기본 설정을 수정한 다음 **확인**을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdee9-160">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![[구성 편집] 대화 상자][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="fdee9-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fdee9-162">Next steps</span></span>

<span data-ttu-id="fdee9-163">Docker의 추가 리소스는 공식 [Docker 웹 사이트][Docker]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fdee9-163">For additional resources for Docker, see the official [Docker website][Docker].</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Azure Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Azure Portal을 사용하여 개인 Docker 컨테이너 레지스트리 만들기]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[browsing-to-web-app]:  media/azure-toolkit-for-intellij-hello-world-web-app-linux/browsing-to-web-app.png
[create-container-registry-01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-container-registry-01.png
[create-container-registry-02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-container-registry-02.png
[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[run-on-web-app-for-containers]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-for-containers.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
