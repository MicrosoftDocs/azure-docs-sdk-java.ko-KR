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
ms.openlocfilehash: c2b6bf3370982d26d8d23fede370e0105a70b734
ms.sourcegitcommit: fd67d4088be2cad01c642b9ecf3f9475d9cb4f3c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46506590"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a><span data-ttu-id="74ee6-103">Azure DevOps를 사용하는 MicroProfile 응용 프로그램의 CI/CD</span><span class="sxs-lookup"><span data-stu-id="74ee6-103">CI/CD for MicroProfile applications using Azure DevOps</span></span>

<span data-ttu-id="74ee6-104">이 자습서에서는 Java EE 개발자가 Azure DevOps(공식적으로는 VSTS라고 함)를 사용하는 컨테이너 용 Azure 웹 앱에 [MicroProfile](http://microprofile.io) 응용 프로그램을 배포하기 위해 CI/CD 릴리스 주기를 쉽게 설정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-104">This tutorial will show how Java EE developers can easily setup a CI/CD release cycle to deploy their [MicroProfile](http://microprofile.io) applications to an Azure Web App for Containers using Azure DevOps (formally known as VSTS).</span></span>  <span data-ttu-id="74ee6-105">이 예제에서는 [Payara Micro](https://www.payara.fish/payara_micro)를 기본 이미지로 사용하는 MicroProfile 응용 프로그램을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-105">In this example, we’ll be using a MicroProfile application that uses a [Payara Micro](https://www.payara.fish/payara_micro) as a base image.</span></span>   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
<span data-ttu-id="74ee6-106">Docker 이미지를 만들고 컨테이너 이미지를 Azure 컨테이너 레지스터에 푸시하여 Azure DevOps 컨테이너화 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-106">We will start the Azure DevOps containerize process by building a Docker image and pushing the container image to an Azure Container Register.</span></span>  <span data-ttu-id="74ee6-107">그런 다음 Azure DevOps 릴리스 파이프라인을 사용하여 컨테이너 이미지를 웹 앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-107">Then complete with a Azure DevOps release pipeline to deploy the container image to a Web App.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74ee6-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="74ee6-108">Prerequisites</span></span>
- <span data-ttu-id="74ee6-109">[Github](https://github.com/Azure-Samples/microprofile-hello-azure)에서 Git url을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-109">Copy and save the Git url from [Github](https://github.com/Azure-Samples/microprofile-hello-azure)</span></span>
- <span data-ttu-id="74ee6-110">[Azure DevOps](https://dev.azure.com) 계정을 등록 또는 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-110">Register or Log into your [Azure DevOps](https://dev.azure.com) account</span></span>
- <span data-ttu-id="74ee6-111">새 [Azure DevOps 프로젝트](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav)를 만들고 위의 Git url을 사용하여 **리포지토리 가져오기**를 합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-111">Create a new [Azure DevOps project](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) and use the above Git url to **import a repository**</span></span>
- <span data-ttu-id="74ee6-112">[ACR(Azure Container Registry)](https://azure.microsoft.com/en-us/services/container-registry) 만들기</span><span class="sxs-lookup"><span data-stu-id="74ee6-112">Create an [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry) (ACR)</span></span>
- <span data-ttu-id="74ee6-113">컨테이너용 Azure 웹 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="74ee6-113">Create an Azure Web App for Container</span></span>
> [!NOTE]
>
> <span data-ttu-id="74ee6-114">웹 앱 인스턴스를 프로비저닝할 때 컨테이너 설정에서 "빠른 시작" 선택</span><span class="sxs-lookup"><span data-stu-id="74ee6-114">Select "Quickstart" in the Container Settings when provisioning the Web App instance</span></span>


## <a name="create-a-build-definition"></a><span data-ttu-id="74ee6-115">빌드 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="74ee6-115">Create a Build definition</span></span>

<span data-ttu-id="74ee6-116">Azure DevOps의 빌드 정의는 Java EE 응용 프로그램 소스 응용 프로그램에서 커밋이 있을 때마다 빌드의 모든 작업을 자동으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-116">The build definition in Azure DevOps automatically executes all the tasks in the build each time there’s a commit in Java EE application source application.</span></span>  <span data-ttu-id="74ee6-117">이 예제에서는 Azure DevOps는 MicroProfile Java 프로젝트를 빌드하기 위해 Maven을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-117">In this example, Azure DevOps will use Maven to build the Java MicroProfile project.</span></span>

1. <span data-ttu-id="74ee6-118">Azure DevOps 프로젝트 페이지 위쪽에서 "빌드 및 릴리스" 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-118">Click on the "Build and Release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="74ee6-119">그런 다음, **빌드** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-119">Then, select the **Builds** link</span></span> 

<img src="media/VSTS/Buid-and-Release1.png">

2. <span data-ttu-id="74ee6-120">빌드 작업을 정의하려면**새 파이프라인** 단추를 클릭하고 나서 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-120">Click on the **New Pipeline** button, and then **Continue** to start defining your build tasks</span></span>
3. <span data-ttu-id="74ee6-121">Java 프로젝트를 빌드하려면 템플릿 목록에서 "Maven"을 선택한 다음 **적용** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-121">Select "Maven" from the list of templates, then click on the **Apply** button to build your Java project</span></span>
4. <span data-ttu-id="74ee6-122">에이전트 풀 필드에 대한 드롭다운 메뉴를 사용하여 **호스팅된 Linux 미리 보기** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-122">Use the drop-down menu for the Agent pool field to select **Hosted Linux Preview** option.</span></span>
> [!NOTE]
>
> <span data-ttu-id="74ee6-123">이는 Azure DevOps에 어느 빌드 서버를 사용할지를 알립니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-123">This informs Azure DevOps which build server to use.</span></span>  <span data-ttu-id="74ee6-124">개인 사용자 지정된 빌드 서버를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-124">You can use your private customized build server</span></span>

5. <span data-ttu-id="74ee6-125">지속적인 통합을 위해 빌드를 구성하려면 **트리거** 탭을 선택하고 **연속 통합 사용** 확인란을 선택하십시오.</span><span class="sxs-lookup"><span data-stu-id="74ee6-125">To configure your build for continuous integration, select the **Triggers** tab and check the **Enable continuous integration** checkbox.</span></span>  

<img src="media/VSTS/Build-Triggers2.png"> 
 
6. <span data-ttu-id="74ee6-126">기본 빌드 파이프라인 페이지로 다시 돌아가려면 **작업** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-126">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
7. <span data-ttu-id="74ee6-127">**저장 및 큐** 드롭다운 메뉴를 사용하여 **저장** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-127">Use the **Save & queue** drop-down menu to select the **Save** option</span></span>
 

## <a name="create-a-docker-build-image"></a><span data-ttu-id="74ee6-128">Docker 빌드 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="74ee6-128">Create a Docker Build Image</span></span>

<span data-ttu-id="74ee6-129">이 작업에서는 Azure DevOps가 Payara Micro의 기본 이미지와 함께 Docker 파일을 사용하여 Docker 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-129">In this task, Azure DevOps uses a Dockerfile with a base image from Payara Micro to create a Docker image.</span></span>  

1. <span data-ttu-id="74ee6-130">기본 빌드 파이프라인 페이지로 다시 돌아가려면 **작업** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-130">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
2. <span data-ttu-id="74ee6-131">빌드 정의에 새 작업을 추가하려면 **+** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-131">Click on the **+** icon to add new task to the build definition</span></span>
 
<img src="media/VSTS/Tasks-add4.png">
 
3. <span data-ttu-id="74ee6-132">템플릿 목록에서 "Docker"를 선택한 다음 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-132">Select "Docker" from the list of templates, then click on the **Add** button</span></span>
4. <span data-ttu-id="74ee6-133">**표시 이름** 필드에 대한 설명 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-133">Enter a description name for the **Display name** field</span></span>
5. <span data-ttu-id="74ee6-134">**컨테이너 레지스트리 유형**의 드롭다운 메뉴에서 **Azure Container Registry**가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-134">Verify that **Azure Container Registry** is selected in the drop-down menu for **Container registry type**.</span></span>
> [!NOTE]
>
>  <span data-ttu-id="74ee6-135">Docker 허브 또는 다른 레지스트리를 사용하는 경우, "Container Registry"를 대신 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-135">If you are using Docker Hub or another registry, select "Container Registry" instead.</span></span>  <span data-ttu-id="74ee6-136">그리고 자격 증명 및 이에 대한 연결 정보를 제공하려면 "+새로 만들기" 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-136">Then click on the "+ New" button to provide the credentials and connection information for it.</span></span> <span data-ttu-id="74ee6-137">계속 하려면 명령 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-137">Then skip to the Commands section to continue.</span></span>

6. <span data-ttu-id="74ee6-138">**Azure 구독** 드롭다운 메뉴를 사용하여 Azure 구독 ID를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-138">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>  <span data-ttu-id="74ee6-139">그런 다음 **권한 부여** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-139">Then click on the **Authorize** button</span></span>
7. <span data-ttu-id="74ee6-140">**Azure 컨테이너 레지스트리** 드롭다운 메뉴에서 Azure에서 만든 레지스트리 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-140">In the **Azure container registry** drop-down menu, select registry name you created in Azure.</span></span>
8. <span data-ttu-id="74ee6-141">**명령** 드롭다운 메뉴에서 **빌드** 옵션이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-141">Verify that **build** option is selected in the **Command** drop-down menu.</span></span>
9. <span data-ttu-id="74ee6-142">**Dockerfile**의 경우 텍스트 상자 옆에 있는 경로 탐색 아이콘을 클릭하여 github 프로젝트에서 Dockerfile을 선택하십시오.</span><span class="sxs-lookup"><span data-stu-id="74ee6-142">For the **Dockerfile**, click on the path navigation icon next to the textbox to select the Dockerfile from the github project.</span></span>  <span data-ttu-id="74ee6-143">그리고 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-143">Then click the **OK** button.</span></span>

<img src="media/VSTS/Dockerfile5.png">

10. <span data-ttu-id="74ee6-144">**이미지 이름** 아래 **최신 태그 포함** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-144">Under the **Image name**, check the **Include latest tag** checkbox.</span></span> 
11. <span data-ttu-id="74ee6-145">**저장 및 큐** 드롭다운 메뉴를 사용하여 **저장** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-145">Use the **Save & queue** drop-down menu to select the **Save** option.</span></span>

## <a name="push-docker-image-to-acr"></a><span data-ttu-id="74ee6-146">ACR에 Docker 이미지 푸시</span><span class="sxs-lookup"><span data-stu-id="74ee6-146">Push Docker Image to ACR</span></span>

<span data-ttu-id="74ee6-147">이 작업에서 Azure DevOps는 Azure Container Registry로 Docker 이미지를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-147">In this task, Azure DevOps will push the docker image to your Azure Container Registry.</span></span>  <span data-ttu-id="74ee6-148">이는 MicroProfile API 응용 프로그램을 컨테이너화된 Java 웹 앱으로 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-148">This will be used to run the MicroProfile API application as a containerized Java web app.</span></span>

1. <span data-ttu-id="74ee6-149">Azure DevOps에서 Docker를 사용하고 있으므로 **Docker Build Image 만들기** 섹션에서 위의 1 - 7 단계를 반복하여 새 Docker 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-149">Since we are using Docker in Azure DevOps, create a new Docker template by repeating steps 1 - 7 above in the **Create a Docker Build Image** section.</span></span>
2. <span data-ttu-id="74ee6-150">**명령** 드롭다운 메뉴에서 **푸시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-150">Select **push** in the **Command** drop-down menu.</span></span>
3. <span data-ttu-id="74ee6-151">**저장 및 큐** 탭을 클릭한 다음, **저장 및 큐** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-151">Click on the **Save & queue** tab, then select **Save & queue** option.</span></span>
4. <span data-ttu-id="74ee6-152">**호스팅된 Linux 미리 보기**가 팝업 창에서 에이전트 풀에 대해 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-152">Verify that the **Hosted Linux Preview** is select for the Agent pool on the pop-up window.</span></span>  <span data-ttu-id="74ee6-153">그리고 **저장 및 큐** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-153">Then click on the **Save & queue** button.</span></span>
5. <span data-ttu-id="74ee6-154">빌드 번호를 클릭하여 Java 프로젝트의 빌드 파이프라인이 성공적으로 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-154">Click on the build number to verify that the build pipeline for the Java project completed successfully.</span></span>

<img src="media/VSTS/Build-Number6.png">
 

## <a name="create-a-release-definition-for-a-java-app"></a><span data-ttu-id="74ee6-155">Java 앱에 대한 릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="74ee6-155">Create a release definition for a Java app</span></span>

<span data-ttu-id="74ee6-156">Azure DevOps의 릴리스 파이프라인은 빌드 프로세스가 성공적으로 완료되는 즉시 Azure와 같은 대상 환경에 빌드 아티팩트의 배포를 자동으로 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-156">The release pipeline in Azure DevOps automatically triggers the deployment of build artifacts to a target environment like Azure as soon as the Build process completes successfully.</span></span>   <span data-ttu-id="74ee6-157">개발, 테스트, 스테이징 또는 프로덕션 환경에 대 한 릴리스 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-157">The release pipeline can be created for dev, test, staging or production environments.</span></span>

1. <span data-ttu-id="74ee6-158">Azure DevOps 프로젝트 페이지 위쪽에서 "빌드 및 릴리스" 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-158">Click on the "Build and release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="74ee6-159">그리고 **릴리스** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-159">Then, select the **Releases** link.</span></span>

<img src="media/VSTS/Release-new-pipeline7.png">
 
2. <span data-ttu-id="74ee6-160">“새 파이프라인” 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-160">Click on the "New pipeline\*\* button</span></span>
3. <span data-ttu-id="74ee6-161">템플릿 목록에서 **Azure App Service에 Java 앱 배포**를 선택하고, **적용** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-161">Select the **Deploy a Java app to Azure App Service** in the list of templates, then click on the **Apply** button.</span></span>

<img src="media/VSTS/deploy-java-template8.png">
 
4. <span data-ttu-id="74ee6-162">**단계 이름**(예: 개발, 테스트, 스테이징 또는 프로덕션)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-162">Set a **Stage name** (e.g Dev, Test, Staging or Production).</span></span>  <span data-ttu-id="74ee6-163">그리고 팝업 창을 닫으려면 **X** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-163">Then click on the **X** button to close the pop-up window</span></span>
5. <span data-ttu-id="74ee6-164">아티팩트 섹션에서 **+추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-164">Click on the **+ Add** button in the Artifacts section.</span></span>  <span data-ttu-id="74ee6-165">이는 빌드 정의에서 이 릴리스 정의로 아티팩트를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-165">This will link artifacts from the build definition to this release definition.</span></span>  
6. <span data-ttu-id="74ee6-166">빌드 정의를 선택하려면 **소스(빌드 파이프라인)** 에 대한 드롭다운 메뉴를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-166">Use the drop-down menu for the **Source (build pipeline)** to select your build definition.</span></span> <span data-ttu-id="74ee6-167">그리고 계속하려면 **추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-167">Then click the **Add** button to continue.</span></span>

<img src="media/VSTS/add-artifact9.png">
 
7. <span data-ttu-id="74ee6-168">파이프라인에서 **작업** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-168">Click on the **Tasks** tab on the pipeline.</span></span>  <span data-ttu-id="74ee6-169">그런 다음 단계 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-169">Then, select your stage name.</span></span>
 
<img src="media/VSTS/release-stage10.png">

8. <span data-ttu-id="74ee6-170">**Azure 구독** 드롭다운 메뉴를 사용하여 Azure 구독 ID를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-170">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>
9. <span data-ttu-id="74ee6-171">**앱 유형** 드롭다운 메뉴에서 **Linux 앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-171">Select **Linux App** from the **App type** drop-down menu</span></span>
10. <span data-ttu-id="74ee6-172">**앱 서비스 이름** 드롭다운 메뉴에서 위에서 작성한 컨테이너 인스턴스의 웹 앱 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-172">Select the name of the Web App for Container instance you created above in the **App service name** drop-down menu</span></span>
11. <span data-ttu-id="74ee6-173">**레지스트리 또는 네임스페이스** 필드에 Azure 컨테이너 레지스트리의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-173">Enter the name of your azure container registry in the **Registry or Namespaces** field.</span></span>  <span data-ttu-id="74ee6-174">E.g **myregistry.azure.io**</span><span class="sxs-lookup"><span data-stu-id="74ee6-174">E.g **myregistry.azure.io**</span></span>
12. <span data-ttu-id="74ee6-175">**리포지토리** 필드에 레지스트리 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-175">Enter the registry name in the **Repository** field</span></span>
13. <span data-ttu-id="74ee6-176">**Azure App Service 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-176">Click on **Deploy Azure App Service**.</span></span>  <span data-ttu-id="74ee6-177">**태그** 텍스트상자에 컨테이너 이미지의 태그를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-177">Enter the tag for the container image in the **Tag** textbox</span></span> 
14. <span data-ttu-id="74ee6-178">**에이전트에서 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-178">Click on **Run on agent**.</span></span>  <span data-ttu-id="74ee6-179">에이전트 풀 드롭다운 메뉴에서 **호스팅된 Linux 미리보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-179">Select **Hosted Linux Preview** in the Agent pool drop-down menu</span></span> 

## <a name="setup-environment-variables"></a><span data-ttu-id="74ee6-180">환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-180">Setup Environment Variables</span></span>

1. <span data-ttu-id="74ee6-181">**변수** 탭을 클릭합니다.  환경 변수를 정의하려면 **+추가** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-181">Click on the **Variables** tab.  Then click on the **+ Add** button to define your environment variables</span></span>
2. <span data-ttu-id="74ee6-182">컨테이너 레지스트리 url, 사용자 이름 및 암호 변수 이름과 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-182">Add the variable name and values for your container registry url, username and password.</span></span>   <span data-ttu-id="74ee6-183">보안을 위해, 암호 값 숨김을 유지하려면 자물쇠 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-183">For security, click on the lock icon to keep the password value hidden.</span></span>

<span data-ttu-id="74ee6-184">예: </span><span class="sxs-lookup"><span data-stu-id="74ee6-184">For example:</span></span>
- <span data-ttu-id="74ee6-185">registry.password</span><span class="sxs-lookup"><span data-stu-id="74ee6-185">registry.password</span></span>
- <span data-ttu-id="74ee6-186">registry.url</span><span class="sxs-lookup"><span data-stu-id="74ee6-186">registry.url</span></span>
- <span data-ttu-id="74ee6-187">registry.username</span><span class="sxs-lookup"><span data-stu-id="74ee6-187">registry.username</span></span>

<img src="media/VSTS/environment-variables12.png">

3. <span data-ttu-id="74ee6-188">주 릴리스 파이프라인 정의 페이지로 돌아가려면 **작업** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-188">Click on the **Tasks** tab to return to the main release pipeline definition page</span></span>
4. <span data-ttu-id="74ee6-189">**Azure App Service 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-189">Click on **Deploy Azure App Service**.</span></span> 
5. <span data-ttu-id="74ee6-190">**응용 프로그램 및 구성 설정** 섹션을 확장한 다음 **응용 프로그램 설정** 필드의 탐색 경로를 클릭하여 배포 중에 컨테이너 레지스트리에 연결할 환경 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-190">Expand the **Application and Configuration Settings** section, then click on the navigation path for the **App Settings** field to add environments variable to connect to the container registry during deployment.</span></span>
6. <span data-ttu-id="74ee6-191">**+ 추가** 버튼을 클릭하여 다음 앱 설정을 정의하고 환경 변수를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-191">Click on the \*\* + Add\*\* button to define the following app settings and assign the environment variables</span></span>
- <span data-ttu-id="74ee6-192">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span><span class="sxs-lookup"><span data-stu-id="74ee6-192">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span></span>
- <span data-ttu-id="74ee6-193">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span><span class="sxs-lookup"><span data-stu-id="74ee6-193">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span></span>
- <span data-ttu-id="74ee6-194">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span><span class="sxs-lookup"><span data-stu-id="74ee6-194">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span></span>

<img src="media/VSTS/environment-variables14.png">
 
7. <span data-ttu-id="74ee6-195">계속하려면 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-195">Click on the **OK** button to continue</span></span>

## <a name="setup-continious-deployment--deploy-java-application"></a><span data-ttu-id="74ee6-196">지속적인 배포 설정 및 Java 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="74ee6-196">Setup Continious Deployment & Deploy Java Application</span></span>

1. <span data-ttu-id="74ee6-197">지속적인 배포를 활성화하려면 **파이프라인** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-197">To enable continuous deployment, click the **Pipelines** tab</span></span>
2. <span data-ttu-id="74ee6-198">아티팩트 섹션에서 번갯불 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-198">In the Artifacts section, click on the lightening icon.</span></span>  <span data-ttu-id="74ee6-199">그런 다음 **지속적인 배포 트리거**를 활성화로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-199">Then set the **Continuous deployment trigger** to Enabled.</span></span>

<img src="media/VSTS/release-enable-CD.png">
 
3. <span data-ttu-id="74ee6-200">**저장** 단추를 클릭하고 **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-200">Click on the **Save** button, then the **OK** button</span></span> 
4. <span data-ttu-id="74ee6-201">**릴리스** 드롭다운 메뉴를 클릭하고 **릴리스 만들기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-201">Click on the **+ Release** drop-down menu, then select **Create a release** link</span></span>
5. <span data-ttu-id="74ee6-202">**자동에서 수동으로 변경을 트리거하는 단계** 드롭다운 메뉴를 사용하여 단계 이름의 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-202">Use the **Stages for a trigger change from automated to manual** drop-down menu to select the checkbox for your stage name</span></span>
6. <span data-ttu-id="74ee6-203">계속하려면 **만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-203">Click the **Create** button to continue</span></span>
7. <span data-ttu-id="74ee6-204">릴리스 번호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-204">Click on the release number.</span></span>  <span data-ttu-id="74ee6-205">그런 다음 스테이지 이름 위로 마우스 커서를 이동하고 **배포** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-205">Then hover your mouse cursor over the stage name and click on the **Deploy** button</span></span>
8. <span data-ttu-id="74ee6-206">Azure에 배포 프로세스를 시작하려면 팝업 창에서 **배포** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-206">The click on the **Deploy** button on the pop-up window to start the deployment process to Azure</span></span>


## <a name="test-the-java-web-application"></a><span data-ttu-id="74ee6-207">Java 웹 응용 프로그램 테스트하기</span><span class="sxs-lookup"><span data-stu-id="74ee6-207">Test the Java Web Application</span></span>
1. <span data-ttu-id="74ee6-208">웹 브라우저에서 웹 앱 url을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-208">Run the web app url in web browser:</span></span>  
<span data-ttu-id="74ee6-209">https://{your-app-service-name}.azurewebsites.net/api/hello</span><span class="sxs-lookup"><span data-stu-id="74ee6-209">https://{your-app-service-name}.azurewebsites.net/api/hello</span></span>

 
<img src="media/VSTS/web-app16.png">

2. <span data-ttu-id="74ee6-210">웹 페이지에 **Hello Azure!** 가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="74ee6-210">The web page should say **Hello Azure!**</span></span>
 
<img src="media/VSTS/web-api17.png">
