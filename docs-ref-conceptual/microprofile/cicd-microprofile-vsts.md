---
title: Azure DevOps를 사용하는 MicroProfile 응용 프로그램의 CI/CD
description: Azure DevOps를 사용하여 MicroProfile 응용 프로그램을 컨테이너 인스턴스용 Azure 웹 앱에 배포하기 위해 CI/CD 릴리스 주기를 설정하는 방법에 대해 알아봅니다.
services: Azure DevOps
documentationcenter: MicroProfile
author: ruyakubu
manager: brunoborges
editor: ruyakubu
ms.assetid: ''
ms.author: ruyakubu
ms.date: 09/14/2018
ms.devlang: Java
ms.service: Azure DevOps
ms.tgt_pltfrm: multiple
ms.topic: tutorial
ms.workload: web
ms.openlocfilehash: 818e37291fa47f99cb161c63a86062bddbf6248c
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799939"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a><span data-ttu-id="d9346-103">Azure DevOps를 사용하는 MicroProfile 응용 프로그램의 CI/CD</span><span class="sxs-lookup"><span data-stu-id="d9346-103">CI/CD for MicroProfile applications using Azure DevOps</span></span>

<span data-ttu-id="d9346-104">이 자습서에서는 Java EE 개발자가 Azure DevOps(공식적으로는 VSTS라고 함)를 사용하는 컨테이너 용 Azure 웹 앱에 [MicroProfile](http://microprofile.io) 응용 프로그램을 배포하기 위해 CI/CD 릴리스 주기를 쉽게 설정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-104">This tutorial will show how Java EE developers can easily setup a CI/CD release cycle to deploy their [MicroProfile](http://microprofile.io) applications to an Azure Web App for Containers using Azure DevOps (formally known as VSTS).</span></span>  <span data-ttu-id="d9346-105">이 예제에서는 [Payara Micro](https://www.payara.fish/payara_micro)를 기본 이미지로 사용하는 MicroProfile 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-105">In this example, we’ll be using a MicroProfile application that uses a [Payara Micro](https://www.payara.fish/payara_micro) as a base image.</span></span>   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
<span data-ttu-id="d9346-106">Docker 이미지를 만들고 컨테이너 이미지를 Azure 컨테이너 레지스터에 푸시하여 Azure DevOps 컨테이너화 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-106">We will start the Azure DevOps containerize process by building a Docker image and pushing the container image to an Azure Container Register.</span></span>  <span data-ttu-id="d9346-107">그런 다음 Azure DevOps 릴리스 파이프라인을 사용하여 컨테이너 이미지를 웹 앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-107">Then complete with a Azure DevOps release pipeline to deploy the container image to a Web App.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9346-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d9346-108">Prerequisites</span></span>
- <span data-ttu-id="d9346-109">[Github](https://github.com/Azure-Samples/microprofile-hello-azure)에서 Git url을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-109">Copy and save the Git url from [Github](https://github.com/Azure-Samples/microprofile-hello-azure)</span></span>
- <span data-ttu-id="d9346-110">[Azure DevOps](https://dev.azure.com) 계정을 등록 또는 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-110">Register or Log into your [Azure DevOps](https://dev.azure.com) account</span></span>
- <span data-ttu-id="d9346-111">새 [Azure DevOps 프로젝트](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav)를 만들고 위의 Git url을 사용하여 **리포지토리 가져오기**를 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-111">Create a new [Azure DevOps project](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) and use the above Git url to **import a repository**</span></span>
- <span data-ttu-id="d9346-112">[ACR(Azure Container Registry)](https://azure.microsoft.com/en-us/services/container-registry) 만들기</span><span class="sxs-lookup"><span data-stu-id="d9346-112">Create an [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry) (ACR)</span></span>
- <span data-ttu-id="d9346-113">컨테이너용 Azure 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d9346-113">Create an Azure Web App for Container</span></span>
  > [!NOTE]
  >
  > <span data-ttu-id="d9346-114">웹 앱 인스턴스를 프로비저닝할 때 컨테이너 설정에서 "빠른 시작" 선택</span><span class="sxs-lookup"><span data-stu-id="d9346-114">Select "Quickstart" in the Container Settings when provisioning the Web App instance</span></span>


## <a name="create-a-build-definition"></a><span data-ttu-id="d9346-115">빌드 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="d9346-115">Create a Build definition</span></span>

<span data-ttu-id="d9346-116">Azure DevOps의 빌드 정의는 Java EE 응용 프로그램 소스 응용 프로그램에서 커밋이 있을 때마다 빌드의 모든 작업을 자동으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-116">The build definition in Azure DevOps automatically executes all the tasks in the build each time there’s a commit in Java EE application source application.</span></span>  <span data-ttu-id="d9346-117">이 예제에서는 Azure DevOps는 MicroProfile Java 프로젝트를 빌드하기 위해 Maven을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-117">In this example, Azure DevOps will use Maven to build the Java MicroProfile project.</span></span>

1. <span data-ttu-id="d9346-118">Azure DevOps 프로젝트 페이지 위쪽에서 "빌드 및 릴리스" 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-118">Click on the "Build and Release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="d9346-119">그런 다음, **빌드** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-119">Then, select the **Builds** link</span></span> 

<img src="media/VSTS/Buid-and-Release1.png">

2. <span data-ttu-id="d9346-120">빌드 작업을 정의하려면**새 파이프라인** 단추를 클릭하고 나서 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-120">Click on the **New Pipeline** button, and then **Continue** to start defining your build tasks</span></span>
3. <span data-ttu-id="d9346-121">Java 프로젝트를 빌드하려면 템플릿 목록에서 "Maven"을 선택한 다음 **적용** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-121">Select "Maven" from the list of templates, then click on the **Apply** button to build your Java project</span></span>
4. <span data-ttu-id="d9346-122">에이전트 풀 필드에 대한 드롭다운 메뉴를 사용하여 **호스팅된 Linux 미리 보기** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-122">Use the drop-down menu for the Agent pool field to select **Hosted Linux Preview** option.</span></span>
   > [!NOTE]
   >
   > <span data-ttu-id="d9346-123">이는 Azure DevOps에 어느 빌드 서버를 사용할지를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-123">This informs Azure DevOps which build server to use.</span></span>  <span data-ttu-id="d9346-124">개인 사용자 지정된 빌드 서버를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-124">You can use your private customized build server</span></span>

5. <span data-ttu-id="d9346-125">지속적인 통합을 위해 빌드를 구성하려면 **트리거** 탭을 선택하고 **연속 통합 사용** 확인란을 선택하십시오.</span><span class="sxs-lookup"><span data-stu-id="d9346-125">To configure your build for continuous integration, select the **Triggers** tab and check the **Enable continuous integration** checkbox.</span></span>  

<img src="media/VSTS/Build-Triggers2.png"> 

6. <span data-ttu-id="d9346-126">기본 빌드 파이프라인 페이지로 다시 돌아가려면 <strong>작업</strong> 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-126">Select the <strong>Tasks</strong> tab to return back to the main build pipeline page</span></span>
7. <span data-ttu-id="d9346-127"><strong>저장 &amp; 큐</strong> 드롭다운 메뉴를 사용하여 <strong>저장</strong> 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-127">Use the <strong>Save &amp; queue</strong> drop-down menu to select the <strong>Save</strong> option</span></span>


## <a name="create-a-docker-build-image"></a><span data-ttu-id="d9346-128">Docker 빌드 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="d9346-128">Create a Docker Build Image</span></span>

<span data-ttu-id="d9346-129">이 작업에서는 Azure DevOps가 Payara Micro의 기본 이미지와 함께 Docker 파일을 사용하여 Docker 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-129">In this task, Azure DevOps uses a Dockerfile with a base image from Payara Micro to create a Docker image.</span></span>  

1. <span data-ttu-id="d9346-130">기본 빌드 파이프라인 페이지로 다시 돌아가려면 **작업** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-130">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
2. <span data-ttu-id="d9346-131">빌드 정의에 새 작업을 추가하려면 **+** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-131">Click on the **+** icon to add new task to the build definition</span></span>

<img src="media/VSTS/Tasks-add4.png">

3. <span data-ttu-id="d9346-132">템플릿 목록에서 &quot;Docker&quot;를 선택한 다음, <strong>추가</strong> 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-132">Select &quot;Docker&quot; from the list of templates, then click on the <strong>Add</strong> button</span></span>
4. <span data-ttu-id="d9346-133"><strong>표시 이름</strong> 필드에 대한 설명 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-133">Enter a description name for the <strong>Display name</strong> field</span></span>
5. <span data-ttu-id="d9346-134"><strong>컨테이너 레지스트리 유형</strong>의 드롭다운 메뉴에서 <strong>Azure Container Registry</strong>가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-134">Verify that <strong>Azure Container Registry</strong> is selected in the drop-down menu for <strong>Container registry type</strong>.</span></span>
<span data-ttu-id="d9346-135">&gt;</span><span class="sxs-lookup"><span data-stu-id="d9346-135">&gt;</span></span> [!NOTE]
<span data-ttu-id="d9346-136">&gt; &gt; Docker 허브 또는 다른 레지스트리를 사용하는 경우 대신 &quot;Container Registry&quot;를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-136">&gt; &gt;  If you are using Docker Hub or another registry, select &quot;Container Registry&quot; instead.</span></span>  <span data-ttu-id="d9346-137">그리고 자격 증명 및 이에 대한 연결 정보를 제공하려면 &quot;+새로 만들기&quot; 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-137">Then click on the &quot;+ New&quot; button to provide the credentials and connection information for it.</span></span> <span data-ttu-id="d9346-138">계속 하려면 명령 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-138">Then skip to the Commands section to continue.</span></span>

6. <span data-ttu-id="d9346-139">**Azure 구독** 드롭다운 메뉴를 사용하여 Azure 구독 ID를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-139">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>  <span data-ttu-id="d9346-140">그런 다음 **권한 부여** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-140">Then click on the **Authorize** button</span></span>
7. <span data-ttu-id="d9346-141">**Azure 컨테이너 레지스트리** 드롭다운 메뉴에서 Azure에서 만든 레지스트리 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-141">In the **Azure container registry** drop-down menu, select registry name you created in Azure.</span></span>
8. <span data-ttu-id="d9346-142">**명령** 드롭다운 메뉴에서 **빌드** 옵션이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-142">Verify that **build** option is selected in the **Command** drop-down menu.</span></span>
9. <span data-ttu-id="d9346-143">**Dockerfile**의 경우 텍스트 상자 옆에 있는 경로 탐색 아이콘을 클릭하여 github 프로젝트에서 Dockerfile을 선택하십시오.</span><span class="sxs-lookup"><span data-stu-id="d9346-143">For the **Dockerfile**, click on the path navigation icon next to the textbox to select the Dockerfile from the github project.</span></span>  <span data-ttu-id="d9346-144">그리고 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-144">Then click the **OK** button.</span></span>

<img src="media/VSTS/Dockerfile5.png">

10. <span data-ttu-id="d9346-145">**이미지 이름** 아래 **최신 태그 포함** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-145">Under the **Image name**, check the **Include latest tag** checkbox.</span></span> 
11. <span data-ttu-id="d9346-146">**저장 및 큐** 드롭다운 메뉴를 사용하여 **저장** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-146">Use the **Save & queue** drop-down menu to select the **Save** option.</span></span>

## <a name="push-docker-image-to-acr"></a><span data-ttu-id="d9346-147">ACR에 Docker 이미지 푸시</span><span class="sxs-lookup"><span data-stu-id="d9346-147">Push Docker Image to ACR</span></span>

<span data-ttu-id="d9346-148">이 작업에서 Azure DevOps는 Azure Container Registry로 Docker 이미지를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-148">In this task, Azure DevOps will push the docker image to your Azure Container Registry.</span></span>  <span data-ttu-id="d9346-149">이는 MicroProfile API 응용 프로그램을 컨테이너화된 Java 웹 앱으로 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-149">This will be used to run the MicroProfile API application as a containerized Java web app.</span></span>

1. <span data-ttu-id="d9346-150">Azure DevOps에서 Docker를 사용하고 있으므로 **Docker Build Image 만들기** 섹션에서 위의 1 - 7 단계를 반복하여 새 Docker 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-150">Since we are using Docker in Azure DevOps, create a new Docker template by repeating steps 1 - 7 above in the **Create a Docker Build Image** section.</span></span>
2. <span data-ttu-id="d9346-151">**명령** 드롭다운 메뉴에서 **푸시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-151">Select **push** in the **Command** drop-down menu.</span></span>
3. <span data-ttu-id="d9346-152">**저장 및 큐** 탭을 클릭한 다음, **저장 및 큐** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-152">Click on the **Save & queue** tab, then select **Save & queue** option.</span></span>
4. <span data-ttu-id="d9346-153">**호스팅된 Linux 미리 보기**가 팝업 창에서 에이전트 풀에 대해 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-153">Verify that the **Hosted Linux Preview** is select for the Agent pool on the pop-up window.</span></span>  <span data-ttu-id="d9346-154">그리고 **저장 및 큐** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-154">Then click on the **Save & queue** button.</span></span>
5. <span data-ttu-id="d9346-155">빌드 번호를 클릭하여 Java 프로젝트의 빌드 파이프라인이 성공적으로 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-155">Click on the build number to verify that the build pipeline for the Java project completed successfully.</span></span>

<img src="media/VSTS/Build-Number6.png">


## <a name="create-a-release-definition-for-a-java-app"></a><span data-ttu-id="d9346-156">Java 앱에 대한 릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="d9346-156">Create a release definition for a Java app</span></span>

<span data-ttu-id="d9346-157">Azure DevOps의 릴리스 파이프라인은 빌드 프로세스가 성공적으로 완료되는 즉시 Azure와 같은 대상 환경에 빌드 아티팩트의 배포를 자동으로 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-157">The release pipeline in Azure DevOps automatically triggers the deployment of build artifacts to a target environment like Azure as soon as the Build process completes successfully.</span></span>   <span data-ttu-id="d9346-158">개발, 테스트, 스테이징 또는 프로덕션 환경에 대 한 릴리스 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-158">The release pipeline can be created for dev, test, staging or production environments.</span></span>

1. <span data-ttu-id="d9346-159">Azure DevOps 프로젝트 페이지 위쪽에서 "빌드 및 릴리스" 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-159">Click on the "Build and release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="d9346-160">그리고 **릴리스** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-160">Then, select the **Releases** link.</span></span>

<img src="media/VSTS/Release-new-pipeline7.png">

2. <span data-ttu-id="d9346-161">&quot;새 파이프라인\*\* 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-161">Click on the &quot;New pipeline\*\* button</span></span>
3. <span data-ttu-id="d9346-162">템플릿 목록에서 <strong>Azure App Service에 Java 앱 배포</strong>를 선택하고, <strong>적용</strong> 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-162">Select the <strong>Deploy a Java app to Azure App Service</strong> in the list of templates, then click on the <strong>Apply</strong> button.</span></span>

<img src="media/VSTS/deploy-java-template8.png">

4. <span data-ttu-id="d9346-163"><strong>단계 이름</strong>(예: 개발, 테스트, 스테이징 또는 프로덕션)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-163">Set a <strong>Stage name</strong> (e.g Dev, Test, Staging or Production).</span></span>  <span data-ttu-id="d9346-164">그리고 팝업 창을 닫으려면 <strong>X</strong> 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-164">Then click on the <strong>X</strong> button to close the pop-up window</span></span>
5. <span data-ttu-id="d9346-165">아티팩트 섹션에서 <strong>+추가</strong> 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-165">Click on the <strong>+ Add</strong> button in the Artifacts section.</span></span>  <span data-ttu-id="d9346-166">이는 빌드 정의에서 이 릴리스 정의로 아티팩트를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-166">This will link artifacts from the build definition to this release definition.</span></span><br/><span data-ttu-id="d9346-167">6. 빌드 정의를 선택하려면 <strong>소스(빌드 파이프라인)</strong>에 대한 드롭다운 메뉴를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-167">6. Use the drop-down menu for the <strong>Source (build pipeline)</strong> to select your build definition.</span></span> <span data-ttu-id="d9346-168">그리고 계속하려면 <strong>추가</strong> 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-168">Then click the <strong>Add</strong> button to continue.</span></span>

<img src="media/VSTS/add-artifact9.png">

7. <span data-ttu-id="d9346-169">파이프라인에서 <strong>작업</strong> 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-169">Click on the <strong>Tasks</strong> tab on the pipeline.</span></span>  <span data-ttu-id="d9346-170">그런 다음 단계 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-170">Then, select your stage name.</span></span>

<img src="media/VSTS/release-stage10.png">

8. <span data-ttu-id="d9346-171">**Azure 구독** 드롭다운 메뉴를 사용하여 Azure 구독 ID를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-171">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>
9. <span data-ttu-id="d9346-172">**앱 유형** 드롭다운 메뉴에서 **Linux 앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-172">Select **Linux App** from the **App type** drop-down menu</span></span>
10. <span data-ttu-id="d9346-173">**앱 서비스 이름** 드롭다운 메뉴에서 위에서 작성한 컨테이너 인스턴스의 웹 앱 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-173">Select the name of the Web App for Container instance you created above in the **App service name** drop-down menu</span></span>
11. <span data-ttu-id="d9346-174">**레지스트리 또는 네임스페이스** 필드에 Azure 컨테이너 레지스트리의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-174">Enter the name of your azure container registry in the **Registry or Namespaces** field.</span></span>  <span data-ttu-id="d9346-175">E.g **myregistry.azure.io**</span><span class="sxs-lookup"><span data-stu-id="d9346-175">E.g **myregistry.azure.io**</span></span>
12. <span data-ttu-id="d9346-176">**리포지토리** 필드에 레지스트리 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-176">Enter the registry name in the **Repository** field</span></span>
13. <span data-ttu-id="d9346-177">**Azure App Service 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-177">Click on **Deploy Azure App Service**.</span></span>  <span data-ttu-id="d9346-178">**태그** 텍스트상자에 컨테이너 이미지의 태그를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-178">Enter the tag for the container image in the **Tag** textbox</span></span> 
14. <span data-ttu-id="d9346-179">**에이전트에서 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-179">Click on **Run on agent**.</span></span>  <span data-ttu-id="d9346-180">에이전트 풀 드롭다운 메뉴에서 **호스팅된 Linux 미리보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-180">Select **Hosted Linux Preview** in the Agent pool drop-down menu</span></span> 

## <a name="setup-environment-variables"></a><span data-ttu-id="d9346-181">환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-181">Setup Environment Variables</span></span>

1. <span data-ttu-id="d9346-182">**변수** 탭을 클릭합니다.  환경 변수를 정의하려면 **+추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-182">Click on the **Variables** tab.  Then click on the **+ Add** button to define your environment variables</span></span>
2. <span data-ttu-id="d9346-183">컨테이너 레지스트리 url, 사용자 이름 및 암호 변수 이름과 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-183">Add the variable name and values for your container registry url, username and password.</span></span>   <span data-ttu-id="d9346-184">보안을 위해, 암호 값 숨김을 유지하려면 자물쇠 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-184">For security, click on the lock icon to keep the password value hidden.</span></span>

<span data-ttu-id="d9346-185">예: </span><span class="sxs-lookup"><span data-stu-id="d9346-185">For example:</span></span>
- <span data-ttu-id="d9346-186">registry.password</span><span class="sxs-lookup"><span data-stu-id="d9346-186">registry.password</span></span>
- <span data-ttu-id="d9346-187">registry.url</span><span class="sxs-lookup"><span data-stu-id="d9346-187">registry.url</span></span>
- <span data-ttu-id="d9346-188">registry.username</span><span class="sxs-lookup"><span data-stu-id="d9346-188">registry.username</span></span>

<img src="media/VSTS/environment-variables12.png">

3. <span data-ttu-id="d9346-189">주 릴리스 파이프라인 정의 페이지로 돌아가려면 **작업** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-189">Click on the **Tasks** tab to return to the main release pipeline definition page</span></span>
4. <span data-ttu-id="d9346-190">**Azure App Service 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-190">Click on **Deploy Azure App Service**.</span></span> 
5. <span data-ttu-id="d9346-191">**응용 프로그램 및 구성 설정** 섹션을 확장한 다음 **응용 프로그램 설정** 필드의 탐색 경로를 클릭하여 배포 중에 컨테이너 레지스트리에 연결할 환경 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-191">Expand the **Application and Configuration Settings** section, then click on the navigation path for the **App Settings** field to add environments variable to connect to the container registry during deployment.</span></span>
6. <span data-ttu-id="d9346-192">**+ 추가** 버튼을 클릭하여 다음 앱 설정을 정의하고 환경 변수를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-192">Click on the \*\* + Add\*\* button to define the following app settings and assign the environment variables</span></span>
7. <span data-ttu-id="d9346-193">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span><span class="sxs-lookup"><span data-stu-id="d9346-193">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span></span>
8. <span data-ttu-id="d9346-194">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span><span class="sxs-lookup"><span data-stu-id="d9346-194">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span></span>
9. <span data-ttu-id="d9346-195">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span><span class="sxs-lookup"><span data-stu-id="d9346-195">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span></span>

<img src="media/VSTS/environment-variables14.png">

7. <span data-ttu-id="d9346-196">계속하려면 <strong>확인</strong> 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-196">Click on the <strong>OK</strong> button to continue</span></span>

## <a name="setup-continious-deployment--deploy-java-application"></a><span data-ttu-id="d9346-197">지속적인 배포 설정 및 Java 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="d9346-197">Setup Continious Deployment & Deploy Java Application</span></span>

1. <span data-ttu-id="d9346-198">지속적인 배포를 활성화하려면 **파이프라인** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-198">To enable continuous deployment, click the **Pipelines** tab</span></span>
2. <span data-ttu-id="d9346-199">아티팩트 섹션에서 번갯불 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-199">In the Artifacts section, click on the lightening icon.</span></span>  <span data-ttu-id="d9346-200">그런 다음 **지속적인 배포 트리거**를 활성화로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-200">Then set the **Continuous deployment trigger** to Enabled.</span></span>

<img src="media/VSTS/release-enable-CD.png">

3. <span data-ttu-id="d9346-201"><strong>저장</strong> 단추를 클릭하고 <strong>확인</strong> 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-201">Click on the <strong>Save</strong> button, then the <strong>OK</strong> button</span></span> 
4. <span data-ttu-id="d9346-202"><strong>릴리스</strong> 드롭다운 메뉴를 클릭하고 <strong>릴리스 만들기</strong> 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-202">Click on the <strong>+ Release</strong> drop-down menu, then select <strong>Create a release</strong> link</span></span>
5. <span data-ttu-id="d9346-203"><strong>자동에서 수동으로 변경을 트리거하는 단계</strong> 드롭다운 메뉴를 사용하여 단계 이름의 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-203">Use the <strong>Stages for a trigger change from automated to manual</strong> drop-down menu to select the checkbox for your stage name</span></span>
6. <span data-ttu-id="d9346-204">계속하려면 <strong>만들기</strong> 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-204">Click the <strong>Create</strong> button to continue</span></span>
7. <span data-ttu-id="d9346-205">릴리스 번호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-205">Click on the release number.</span></span>  <span data-ttu-id="d9346-206">그런 다음 스테이지 이름 위로 마우스 커서를 이동하고 <strong>배포</strong> 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-206">Then hover your mouse cursor over the stage name and click on the <strong>Deploy</strong> button</span></span>
8. <span data-ttu-id="d9346-207">Azure에 배포 프로세스를 시작하려면 팝업 창에서 <strong>배포</strong> 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-207">The click on the <strong>Deploy</strong> button on the pop-up window to start the deployment process to Azure</span></span>


## <a name="test-the-java-web-application"></a><span data-ttu-id="d9346-208">Java 웹 응용 프로그램 테스트하기</span><span class="sxs-lookup"><span data-stu-id="d9346-208">Test the Java Web Application</span></span>
1. <span data-ttu-id="d9346-209">웹 브라우저에서 웹 앱 url을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-209">Run the web app url in web browser:</span></span>  
   <span data-ttu-id="d9346-210">https://{your-app-service-name}.azurewebsites.net/api/hello</span><span class="sxs-lookup"><span data-stu-id="d9346-210">https://{your-app-service-name}.azurewebsites.net/api/hello</span></span>


<img src="media/VSTS/web-app16.png">

2. <span data-ttu-id="d9346-211">웹 페이지에 **Hello Azure!** 가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="d9346-211">The web page should say **Hello Azure!**</span></span>

<img src="media/VSTS/web-api17.png">
