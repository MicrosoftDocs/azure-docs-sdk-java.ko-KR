---
title: IntelliJ용 Azure 도구 키트를 사용하여 Spring Boot 앱을 Docker 컨테이너로 게시
description: IntelliJ용 Azure 도구 키트를 사용하여 Docker 컨테이너로 Microsoft Azure에 웹앱을 게시하는 방법을 알아봅니다.
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/13/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 4b8527ced4aa8010a26b6d1f99f76943a875e66e
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338707"
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="a89ba-103">IntelliJ용 Azure 도구 키트를 사용하여 Spring Boot 앱을 Docker 컨테이너로 게시</span><span class="sxs-lookup"><span data-stu-id="a89ba-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="a89ba-104">[Spring Framework]는 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만드는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="a89ba-105">해당 플랫폼을 기반으로 하여 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 응용 프로그램을 만드는 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="a89ba-106">[Docker]는 개발자가 컨테이너에서 실행되는 응용 프로그램의 배포, 크기 조정 및 관리를 자동화하는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="a89ba-107">이 자습서에서는 IntelliJ용 Azure 도구 키트를 사용하여 Microsoft Azure에 Docker 컨테이너로 Spring Boot 응용 프로그램을 배포하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a><span data-ttu-id="a89ba-108">기본 Spring Boot Docker 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="a89ba-108">Clone the default Spring Boot Docker repo</span></span>

<span data-ttu-id="a89ba-109">다음 단계는 IntelliJ를 사용하여 Spring Boot Docker 리포지토리를 복제하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-109">The following steps walk you through cloning the Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="a89ba-110">명령줄을 사용하려면 [Azure Container Service에서 Linux에 Spring Boot 응용 프로그램 배포][Deploy Spring Boot on Linux in AKS]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a89ba-110">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in AKS].</span></span>

1. <span data-ttu-id="a89ba-111">IntelliJ를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="a89ba-112">시작 화면의 **버전 제어에서 체크 아웃** 목록에서 **GitHub** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-112">On the welcome screen, select the **GitHub** option in the **Check out from Version Control** list.</span></span>

   ![버전 제어에 대한 GitHub 옵션][CL01]

1. <span data-ttu-id="a89ba-114">로그인하라는 메시지가 표시되면 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-114">Enter your credentials if you are prompted to log in.</span></span>

   * <span data-ttu-id="a89ba-115">GitHub에 로그인하는 데 사용자 이름/암호를 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="a89ba-115">If you are using a username/password to log in to GitHub:</span></span> 

      ![GitHub 사용자 이름 및 암호를 입력하는 대화 상자][CL02a]

   * <span data-ttu-id="a89ba-117">GitHub에 로그인하는 데 토큰을 사용하는 경우:</span><span class="sxs-lookup"><span data-stu-id="a89ba-117">If you are using a token to log in to GitHub:</span></span> 

      ![GitHub 토큰을 입력하는 대화 상자][CL02b]

1. <span data-ttu-id="a89ba-119">리포지토리 URL에 대해 **https://github.com/spring-guides/gs-spring-boot-docker.git**를 입력하고 로컬 경로 및 폴더 정보를 지정한 다음 **복제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for the repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![리포지토리 복제 대화 상자][CL03]

1. <span data-ttu-id="a89ba-121">IntelliJ 프로젝트를 만들 것인지 묻는 메시지가 표시되면 **아니요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-121">When you're prompted to create an IntelliJ project, select **No**.</span></span>

   ![IntelliJ 프로젝트 만들지 않기][CL04]

1. <span data-ttu-id="a89ba-123">홈페이지에서 **프로젝트 가져오기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-123">On the welcome page, click **Import Project**.</span></span>

   ![프로젝트 가져오기 선택 영역][CL05]

1. <span data-ttu-id="a89ba-125">Spring Boot 리포지토리를 복제한 경로를 찾고 루트 아래의 **완료** 폴더를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-125">Locate the path where you cloned the Spring Boot repo, select the **complete** folder under the root, and then click **OK**.</span></span>

   ![가져올 폴더 선택][CL06]

1. <span data-ttu-id="a89ba-127">메시지가 표시되면 **기존 원본에서 프로젝트 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![기존 원본에서 프로젝트를 만드는 옵션][CL07]

1. <span data-ttu-id="a89ba-129">프로젝트 이름을 지정하거나 기본값을 적용하고 **완료** 폴더에 올바른 경로를 확인한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-129">Specify your project name or accept the default, verify the correct path to the **complete** folder, and then click **Next**.</span></span>

   ![프로젝트 이름 지정][CL08]

1. <span data-ttu-id="a89ba-131">가져오기에 대한 모든 디렉터리를 사용자 지정한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![디렉터리 선택][CL09]

1. <span data-ttu-id="a89ba-133">가져올 라이브러리를 검토한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-133">Review the libraries to import, and then click **Next**.</span></span>

   ![프로젝트 라이브러리 검토][CL10]

1. <span data-ttu-id="a89ba-135">모듈 구조를 검토한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-135">Review the module structure, and then click **Next**.</span></span>

   ![모듈 구조 검토][CL11]

1. <span data-ttu-id="a89ba-137">JDK를 지정한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-137">Specify your JDK, and then click **Next**.</span></span>

   ![JDK 지정][CL12]

1. <span data-ttu-id="a89ba-139">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-139">Click **Finish**.</span></span>

   ![마침 단추][CL13]

<span data-ttu-id="a89ba-141">IntelliJ는 프로젝트로 Spring Boot 앱을 가져오고 가져오기가 완료되면 구조를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-141">IntelliJ imports the Spring Boot app as a project and displays the structure when the import has finished.</span></span>

![IntelliJ에서 Spring Boot 앱][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="a89ba-143">Spring Boot 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="a89ba-143">Build your Spring Boot app</span></span>

### <a name="build-the-app-by-using-the-maven-pom"></a><span data-ttu-id="a89ba-144">Maven POM을 사용하여 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="a89ba-144">Build the app by using the Maven POM</span></span>

1. <span data-ttu-id="a89ba-145">아직 열려 있지 않은 경우 Maven 도구 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-145">Open the Maven tool window if it is not already opened.</span></span> <span data-ttu-id="a89ba-146">**보기** > **도구 창** > **Maven 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![도구 창과 Maven 프로젝트 명령][BU01]

1. <span data-ttu-id="a89ba-148">Maven 도구 창에서 마우스 오른쪽 단추로 **패키지**를 클릭하고 **Maven 빌드 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-148">In the Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="a89ba-149">(Maven 프로젝트가 자동으로 표시되지 않는 경우 Maven 툴바의 **다시 가져오기** 아이콘을 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="a89ba-149">(If your Maven project does not show up automatically, click the **Reimport** icon on the Maven toolbar.)</span></span>

   ![Maven 빌드 실행 명령][BU02]

1. <span data-ttu-id="a89ba-151">IntelliJ는 Spring Boot 앱이 성공적으로 생성되면 **빌드 성공** 메시지를 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![빌드 성공 메시지][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="a89ba-153">배포 준비된 아티팩트 만들기</span><span class="sxs-lookup"><span data-stu-id="a89ba-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="a89ba-154">Spring Boot 앱을 게시하려면 배포 준비된 아티팩트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-154">To publish your Spring Boot app, you need to create a deployment-ready artifact.</span></span> <span data-ttu-id="a89ba-155">다음 단계를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="a89ba-155">Use the following steps:</span></span>

1. <span data-ttu-id="a89ba-156">IntelliJ의 웹앱 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="a89ba-157">**파일**을 클릭한 다음 **프로젝트 구조**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-157">Click **File**, and then click **Project Structure**.</span></span>

   ![프로젝트 구조 명령][ART01]

1. <span data-ttu-id="a89ba-159">녹색 더하기(**+**) 기호를 클릭하여 아티팩트를 추가하고 **JAR**을 클릭한 다음 **비어 있음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-159">Click the green plus (**+**) symbol to add an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![아티팩트 추가][ART02]

1. <span data-ttu-id="a89ba-161">".jar" 확장명을 추가하지 않도록 하는 동안 아티팩트의 이름을 지정한 다음 Maven 출력에 대한 대상 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-161">Name your artifact while making sure not to add the ".jar" extension, and then specify the target folder for the Maven output.</span></span>

   ![아티팩트 속성 지정][ART03]

1. <span data-ttu-id="a89ba-163">아티팩트에 대한 매니페스트를 만듭니다(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="a89ba-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="a89ba-164">a.</span><span class="sxs-lookup"><span data-stu-id="a89ba-164">a.</span></span> <span data-ttu-id="a89ba-165">**매니페스트 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-165">Click **Create Manifest**.</span></span>

      ![매니페스트 만들기 단추 클릭][ART04a]

   <span data-ttu-id="a89ba-167">b.</span><span class="sxs-lookup"><span data-stu-id="a89ba-167">b.</span></span> <span data-ttu-id="a89ba-168">아티팩트에 대한 기본 경로를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-168">Choose the default path for the artifact, and then click **OK**.</span></span>

      ![아티팩트 경로 지정][ART04b]

   <span data-ttu-id="a89ba-170">다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-170">c.</span></span> <span data-ttu-id="a89ba-171">줄임표 **...** 를 클릭하여 기본 클래스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-171">Click the ellipsis (**...**) to locate the main class.</span></span>

      ![기본 클래스 찾기][ART04c]

   <span data-ttu-id="a89ba-173">d.</span><span class="sxs-lookup"><span data-stu-id="a89ba-173">d.</span></span> <span data-ttu-id="a89ba-174">기본 클래스를 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-174">Choose your main class, and then click **OK**.</span></span>

      ![기본 클래스 지정][ART04d]

1. <span data-ttu-id="a89ba-176">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-176">Click **OK**.</span></span>

   ![프로젝트 구조 대화 상자 닫기][ART05]

> [!NOTE]
> <span data-ttu-id="a89ba-178">IntelliJ에서 아티팩트를 만드는 데 관한 자세한 내용은 JetBrains 웹 사이트의 [아티팩트 구성]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a89ba-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on the JetBrains website.</span></span>
>

### <a name="build-the-artifact-for-deployment"></a><span data-ttu-id="a89ba-179">배포에 대한 아티팩트 빌드</span><span class="sxs-lookup"><span data-stu-id="a89ba-179">Build the artifact for deployment</span></span>

1. <span data-ttu-id="a89ba-180">**빌드**를 클릭한 다음 **아티팩트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![아티팩트 빌드 명령][BU04]

1. <span data-ttu-id="a89ba-182">**아티팩트 빌드** 바로 가기 메뉴가 나타나면 **빌드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-182">When the **Build Artifact** context menu appears, click **Build**.</span></span>

   ![아티팩트 빌드 컨텍스트 메뉴][BU05]

<span data-ttu-id="a89ba-184">IntelliJ는 프로젝트 도구 창에서 Spring Boot 앱에 대한 완료된 아티팩트를 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-184">IntelliJ should display the completed artifact for your Spring Boot app in the project tool window.</span></span>

   ![만든 아티팩트][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="a89ba-186">Docker 컨테이너를 사용하여 Azure에 웹앱 게시</span><span class="sxs-lookup"><span data-stu-id="a89ba-186">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="a89ba-187">Azure 계정에 로그인하지 않은 경우 [IntelliJ용 Azure 도구 키트에 대한 로그인 지침][Azure Sign In for IntelliJ]의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-187">If you have not signed in to your Azure account, follow the steps in [Sign-in instructions for the Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="a89ba-188">프로젝트 탐색기 도구 창에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **Azure** > **Docker 컨테이너로 게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-188">In the Project Explorer tool window, right-click the project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Docker 컨테이너로 게시 명령][PU01]

1. <span data-ttu-id="a89ba-190">**Azure에서 Docker 컨테이너 배포** 대화 상자가 표시되는 경우 기존 Docker 호스트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-190">When the **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="a89ba-191">기존 호스트에 배포하려는 경우 4단계로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-191">If you choose to deploy to an existing host, you can skip to step 4.</span></span> <span data-ttu-id="a89ba-192">그렇지 않으면 다음 단계에 따라 호스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-192">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="a89ba-193">a.</span><span class="sxs-lookup"><span data-stu-id="a89ba-193">a.</span></span> <span data-ttu-id="a89ba-194">녹색 더하기(**+**) 기호를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-194">Click the green plus (**+**) symbol.</span></span>

      ![새 Docker 호스트 추가][PU02]

   <span data-ttu-id="a89ba-196">b.</span><span class="sxs-lookup"><span data-stu-id="a89ba-196">b.</span></span> <span data-ttu-id="a89ba-197">**Create Docker Host** 대화 상자가 표시되면 기본값을 그대로 허용하도록 선택하거나 새 Docker 호스트에 대한 사용자 지정 설정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-197">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="a89ba-198">다양한 설정에 대한 자세한 설명은 [IntelliJ용 Azure 도구 키트를 사용하여 웹앱을 Docker 컨테이너로 게시][Publish Container with Azure Toolkit]를 참조하세요. 사용할 설정을 지정하면 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-198">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Docker 호스트 옵션 지정][PU03a]

   <span data-ttu-id="a89ba-200">다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-200">c.</span></span> <span data-ttu-id="a89ba-201">Azure Key Vault에서 기존 로그인 자격 증명을 사용하도록 선택하거나 새 Docker 로그인 자격 증명을 입력하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-201">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="a89ba-202">옵션을 지정하면 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-202">Click **Finish** when you have specified your options.</span></span>

      ![Docker 호스트 자격 증명 지정][PU03b]

1. <span data-ttu-id="a89ba-204">Docker 호스트를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-204">Select your Docker host, and then click **Next**.</span></span>

   ![사용할 Docker 호스트 선택][PU04]

1. <span data-ttu-id="a89ba-206">**Azure에 Docker 컨테이너 배포** 대화 상자의 마지막 페이지에서 다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-206">On the last page of the **Deploy Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="a89ba-207">a.</span><span class="sxs-lookup"><span data-stu-id="a89ba-207">a.</span></span> <span data-ttu-id="a89ba-208">Docker 컨테이너를 호스팅할 컨테이너에 대한 사용자 지정 이름을 지정하도록 선택하거나 기본값을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-208">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="a89ba-209">b.</span><span class="sxs-lookup"><span data-stu-id="a89ba-209">b.</span></span> <span data-ttu-id="a89ba-210">*[외부 포트]*:*[내부 포트]* 구문을 사용하여 Docker 호스트에 대한 TCP 포트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-210">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="a89ba-211">예를 들어 **80:8080**은 80 외부 포트 및 8080 기본 내부 Spring Boot 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-211">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="a89ba-212">내부 포트를 사용자 지정한 경우(예: application.yml 파일 편집) Azure에서 올바른 라우팅을 수행할 포트 번호를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-212">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="a89ba-213">다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-213">c.</span></span> <span data-ttu-id="a89ba-214">이러한 옵션을 구성했으면 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-214">After you have configured these options, click **Finish**.</span></span>

   ![Azure에 Docker 컨테이너 배포][PU05]

1. <span data-ttu-id="a89ba-216">Azure 도구 키트에서 게시를 완료하면 Azure 활동 로그에 **게시됨** 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a89ba-216">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Docker 호스트를 성공적으로 배포][PU06]

## <a name="next-steps"></a><span data-ttu-id="a89ba-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a89ba-218">Next steps</span></span>

<span data-ttu-id="a89ba-219">IntelliJ를 사용하여 Spring Boot 앱을 만들기 위한 추가 방법에 대해 알아보려면 JetBrains 웹 사이트에서 [Spring Boot 프로젝트 만들기](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a89ba-219">To learn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on the JetBrains website.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[아티팩트 구성]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Configuring Artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
