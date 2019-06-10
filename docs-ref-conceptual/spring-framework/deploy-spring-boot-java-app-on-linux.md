---
title: Azure App Service for Container에서 Spring Boot 웹앱 배포
description: 이 자습서에서는 Microsoft Azure에서 Linux Web App으로 Spring Boot 애플리케이션을 배포하는 단계를 설명합니다.
services: azure app service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: azure app service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 407b852e24ef88d2fb075bd064f1acf2b107ddc1
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270859"
---
# <a name="deploy-a-spring-boot-application-on-azure-app-service-for-container"></a><span data-ttu-id="0cef4-103">Azure App Service for Container에서 Spring Boot 애플리케이션 배포</span><span class="sxs-lookup"><span data-stu-id="0cef4-103">Deploy a Spring Boot application on Azure App Service for Container</span></span>

<span data-ttu-id="0cef4-104">이 자습서에서는 [Docker]를 사용하여 [Azure App Service](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro)에서 [Spring Boot] 애플리케이션을 컨테이너화하고 Linux 호스트로 Docker 이미지를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-104">This tutorial walks you through using [Docker] to containerize your [Spring Boot] application and deploy your own docker image to a Linux host in the [Azure App Service](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cef4-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0cef4-105">Prerequisites</span></span>

<span data-ttu-id="0cef4-106">이 자습서의 단계를 완료하려면 다음 필수 조건이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-106">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="0cef4-107">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="0cef4-108">[Azure CLI(명령줄 인터페이스)]</span><span class="sxs-lookup"><span data-stu-id="0cef4-108">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="0cef4-109">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="0cef4-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="0cef4-110">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cef4-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="0cef4-111">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="0cef4-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="0cef4-112">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="0cef4-112">A [Git] client.</span></span>
* <span data-ttu-id="0cef4-113">[Docker] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="0cef4-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="0cef4-114">이 자습서의 가상화 요구 사항으로 인해 가상 머신에는 이 문서의 단계를 따를 수 없습니다. 따라서 가상화 기능이 사용하도록 설정된 물리적 컴퓨터를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="0cef4-115">Spring Boot on Docker 시작 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0cef4-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="0cef4-116">다음 단계에서는 간단한 Spring Boot 웹 애플리케이션을 만들어 로컬로 테스트하는 데 필요한 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-116">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="0cef4-117">명령 프롬프트를 열고 애플리케이션을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="0cef4-118">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="0cef4-118">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="0cef4-119">[Spring Boot on Docker 시작] 샘플 프로젝트를 방금 만든 디렉터리에 복제합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="0cef4-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="0cef4-120">디렉터리를 완료된 프로젝트로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="0cef4-120">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="0cef4-121">Maven을 사용하여 JAR 파일을 빌드합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="0cef4-121">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="0cef4-122">웹앱이 만들어지면 디렉터리를 JAR 파일이 위치한 `target` 디렉터리로 변경하고 웹앱을 시작합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="0cef4-122">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="0cef4-123">웹 브라우저를 사용하여 로컬로 이동하여 웹앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-123">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="0cef4-124">예를 들어 curl을 사용할 수 있고 포트 80에서 실행하도록 Tomcat 서버를 구성한 경우:</span><span class="sxs-lookup"><span data-stu-id="0cef4-124">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="0cef4-125">다음 메시지가 표시되어야 합니다. **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="0cef4-125">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![로컬로 샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="0cef4-127">Azure Container Registry를 만들어서 프라이빗 Docker 레지스트리로 사용</span><span class="sxs-lookup"><span data-stu-id="0cef4-127">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="0cef4-128">다음 단계에서는 Azure Portal을 사용하여 Azure Container Registry를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-128">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="0cef4-129">Azure Portal 대신 Azure CLI를 사용하려는 경우 [Azure CLI 2.0을 사용하여 프라이빗 Docker 컨테이너 레지스트리 만들기](/azure/container-registry/container-registry-get-started-azure-cli)의 단계에 따르세요.</span><span class="sxs-lookup"><span data-stu-id="0cef4-129">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
>

1. <span data-ttu-id="0cef4-130">[Azure Portal]을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-130">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="0cef4-131">Azure Portal에서 사용자의 계정에 로그인하면 [Azure Portal을 사용하여 프라이빗 Docker 컨테이너 레지스트리 만들기] 문서의 단계를 수행할 수 있습니다. 편의상 다음 단계에서 다시 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-131">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="0cef4-132">**+ 새로 만들기**의 메뉴 아이콘을 클릭하고 **컨테이너**를 클릭한 다음, **Azure Container Registry**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-132">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![새로운 Azure Container Registry 만들기][AR01]

1. <span data-ttu-id="0cef4-134">Azure Container Registry 템플릿에 대한 정보 페이지가 표시되면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-134">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![새로운 Azure Container Registry 만들기][AR02]

1. <span data-ttu-id="0cef4-136">**컨테이너 레지스트리 만들기** 페이지가 표시되면 **레지스트리 이름** 및 **리소스 그룹**을 입력하고 **관리 사용자**에 대해 **사용**을 선택한 다음, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-136">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Azure Container Registry 설정 구성][AR03]

1. <span data-ttu-id="0cef4-138">컨테이너 레지스트리를 만들면 Azure Portal에서 컨테이너 레지스트리를 탐색한 다음, **선택키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-138">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="0cef4-139">다음 단계에서 사용하기 위해 사용자 이름과 암호를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-139">Take note of the username and password for the next steps.</span></span>

   ![Azure Container Registry 선택키][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="0cef4-141">Azure Container Registry 선택키를 사용하도록 Maven 구성</span><span class="sxs-lookup"><span data-stu-id="0cef4-141">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="0cef4-142">Spring Boot 애플리케이션의 완성된 프로젝트 디렉터리(예: "*C:\SpringBoot\gs-spring-boot-docker\complete*" 또는 " */users/robert/SpringBoot/gs-spring-boot-docker/complete*") 텍스트 편집기를 사용하여 *pom.xml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-142">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="0cef4-143">최신 버전의 [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) 및 로그인 서버 값을 사용하여 *pom.xml* 파일의 `<properties>` 컬렉션을 업데이트하고 이 자습서의 이전 섹션에서 Azure Container Registry에 대한 설정에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-143">Update the `<properties>` collection in the *pom.xml* file with the latest version of [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) and login server value and access settings for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="0cef4-144">예:</span><span class="sxs-lookup"><span data-stu-id="0cef4-144">For example:</span></span>

   ```xml
   <properties>
      <jib-maven-plugin.version>1.2.0</jib-maven-plugin.version>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <username>wingtiptoysregistry</username>
      <password>{put your Azure Container Registry access key here}</password>
   </properties>
   ```

1. <span data-ttu-id="0cef4-145">*pom.xml* 파일의 `<plugins>` 컬렉션에 [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin)을 추가하고 `<from>/<image>`에서 기본 이미지 및 최종 이미지 이름 `<to>/<image>`를 지정하고 `<to>/<auth>`의 이전 섹션에서 사용자 이름 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-145">Add [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) to the `<plugins>` collection in the *pom.xml* file, specify the base image at `<from>/<image>` and  final image name `<to>/<image>`, specify the username and password from previous section at `<to>/<auth>`.</span></span> <span data-ttu-id="0cef4-146">예:</span><span class="sxs-lookup"><span data-stu-id="0cef4-146">For example:</span></span>

   ```xml
   <plugin>
     <artifactId>jib-maven-plugin</artifactId>
     <groupId>com.google.cloud.tools</groupId>
     <version>${jib-maven-plugin.version}</version>
     <configuration>
        <from>
            <image>openjdk:8-jre-alpine</image>
        </from>
        <to>
            <image>${docker.image.prefix}/${project.artifactId}</image>
            <auth>
               <username>${username}</username>
               <password>${password}</password>
            </auth>
        </to>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="0cef4-147">Spring Boot 애플리케이션의 완성된 프로젝트 디렉터리로 이동하고 다음 명령을 실행하여 애플리케이션을 다시 빌드하고 Azure Container Registry에 컨테이너를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-147">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```cmd
   mvn compile jib:build
   ```

> [!NOTE]
>
> <span data-ttu-id="0cef4-148">지브를 사용하여 이미지를 Azure Container Registry에 푸시하는 경우 이미지는 *Dockerfile*을 유지하지 않습니다. 자세한 내용은 [이](https://cloudplatform.googleblog.com/2018/07/introducing-jib-build-java-docker-images-better.html) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cef4-148">When you are using Jib to push your image to the Azure Container Registry, the image will not honor *Dockerfile*, see [this](https://cloudplatform.googleblog.com/2018/07/introducing-jib-build-java-docker-images-better.html) document for details.</span></span>
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="0cef4-149">컨테이너 이미지를 사용하여 Azure App Service에서 Linux에 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0cef4-149">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="0cef4-150">[Azure Portal]을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-150">Browse to the [Azure portal] and sign in.</span></span>

2. <span data-ttu-id="0cef4-151">**+ 리소스 만들기**에 대한 아이콘, **웹**, **Web App for Containers**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-151">Click the menu icon for **+ Create a resource**, then click **Web**, and then click **Web App for Containers**.</span></span>
   
   ![Azure Portal에서 새로운 웹앱 만들기][LX01]

3. <span data-ttu-id="0cef4-153">**Web App on Linux** 페이지가 표시되면 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-153">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="0cef4-154">a.</span><span class="sxs-lookup"><span data-stu-id="0cef4-154">a.</span></span> <span data-ttu-id="0cef4-155">**앱 이름**에 고유한 이름을 입력합니다. 예: "*wingtiptoyslinux*"</span><span class="sxs-lookup"><span data-stu-id="0cef4-155">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*"</span></span>

   <span data-ttu-id="0cef4-156">b.</span><span class="sxs-lookup"><span data-stu-id="0cef4-156">b.</span></span> <span data-ttu-id="0cef4-157">드롭다운 목록에서 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-157">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="0cef4-158">다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-158">c.</span></span> <span data-ttu-id="0cef4-159">기존 **리소스 그룹**을 선택하거나 새 리소스 그룹을 만들기 위해 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-159">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="0cef4-160">d.</span><span class="sxs-lookup"><span data-stu-id="0cef4-160">d.</span></span> <span data-ttu-id="0cef4-161">**OS**로 *Linux*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-161">Choose *Linux* as the **OS**.</span></span>

   <span data-ttu-id="0cef4-162">e.</span><span class="sxs-lookup"><span data-stu-id="0cef4-162">e.</span></span> <span data-ttu-id="0cef4-163">**App Service 플랜/위치**를 클릭하고 기존 앱 서비스 플랜을 선택하거나 **새로 만들기**를 클릭하여 새 앱 서비스 플랜을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-163">Click **App Service plan/Location** and choose an existing app service plan, or click **Create new** to create a new app service plan.</span></span>

   <span data-ttu-id="0cef4-164">f.</span><span class="sxs-lookup"><span data-stu-id="0cef4-164">f.</span></span> <span data-ttu-id="0cef4-165">**컨테이너 구성**을 클릭하고 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-165">Click **Configure container** and enter the following information:</span></span>

   * <span data-ttu-id="0cef4-166">**단일 컨테이너** 및 **Azure Container Registry**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-166">Choose **Single Container** and  **Azure Container Registry**.</span></span>

   * <span data-ttu-id="0cef4-167">**레지스트리**: 이전에 만든 컨테이너 이름을 선택합니다. 예: "*wingtiptoysregistry*"</span><span class="sxs-lookup"><span data-stu-id="0cef4-167">**Registry**: Choose your container name created earlier; for example: "*wingtiptoysregistry*"</span></span>

   * <span data-ttu-id="0cef4-168">**이미지**: 이미지 이름을 선택합니다. 예: "*gs-spring-boot-docker*"</span><span class="sxs-lookup"><span data-stu-id="0cef4-168">**Image**: Choose the image name; for example: "*gs-spring-boot-docker*"</span></span>
   
   * <span data-ttu-id="0cef4-169">**태그**: 이미지에 대한 태그를 선택합니다. 예: "*latest*"</span><span class="sxs-lookup"><span data-stu-id="0cef4-169">**Tag**: Choose the tag for the image; for example: "*latest*"</span></span>
   
   * <span data-ttu-id="0cef4-170">**시작 파일**: 이미지에 시작 명령이 이미 있으므로 공백으로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-170">**Startup File**: Keep it blank since the image already has the start up command</span></span>
   
   <span data-ttu-id="0cef4-171">e.</span><span class="sxs-lookup"><span data-stu-id="0cef4-171">e.</span></span> <span data-ttu-id="0cef4-172">위의 정보를 모두 입력한 후 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-172">Once you have entered all of the above information, click **Apply**.</span></span>

   ![웹앱 설정 구성][LX02]

4. <span data-ttu-id="0cef4-174">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="0cef4-175">Azure에서는 표준 포트 80 또는 8080에서 실행되는 임베디드 Tomcat 서버에 인터넷 요청을 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-175">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="0cef4-176">그러나 사용자 지정 포트에서 임베디드 Tomcat 서버를 실행하도록 구성한 경우, 임베디드 Tomcat 서버에 포트를 정의하는 웹앱에 환경 변수를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-176">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="0cef4-177">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-177">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="0cef4-178">[Azure Portal]을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-178">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="0cef4-179">**App Services**에 대한 아이콘을 클릭하고 목록에서 웹앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-179">Click the icon for **App Services**, and select your web app from the list.</span></span>
>
> 4. <span data-ttu-id="0cef4-180">**구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-180">Click **Configuration**.</span></span> <span data-ttu-id="0cef4-181">(아래 이미지에서 항목 #1)</span><span class="sxs-lookup"><span data-stu-id="0cef4-181">(Item #1 in the image below.)</span></span>
>
> 5. <span data-ttu-id="0cef4-182">**애플리케이션 설정** 섹션에서 **PORT**라는 새 설정을 추가하고 값에 대한 사용자 지정 포트 번호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-182">In the **Application settings** section, add a new setting named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="0cef4-183">(아래 이미지에서 항목 #2, #3, #4)</span><span class="sxs-lookup"><span data-stu-id="0cef4-183">(Item #2, #3, #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="0cef4-184">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-184">Click **Save**.</span></span> <span data-ttu-id="0cef4-185">(아래 이미지에서 항목 #5)</span><span class="sxs-lookup"><span data-stu-id="0cef4-185">(Item #5 in the image below.)</span></span>
>
> ![Azure Portal에서 사용자 지정 포트 번호 저장][LX03]
>

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="0cef4-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0cef4-187">Next steps</span></span>

<span data-ttu-id="0cef4-188">Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="0cef4-188">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0cef4-189">Azure의 Spring</span><span class="sxs-lookup"><span data-stu-id="0cef4-189">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="0cef4-190">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0cef4-190">Additional Resources</span></span>

<span data-ttu-id="0cef4-191">Azure에서 Spring Boot 애플리케이션을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cef4-191">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="0cef4-192">Azure App Service에 Spring Boot 애플리케이션 배포</span><span class="sxs-lookup"><span data-stu-id="0cef4-192">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="0cef4-193">Azure Container Service의 Kubernetes 클러스터에 Spring Boot 애플리케이션 배포</span><span class="sxs-lookup"><span data-stu-id="0cef4-193">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="0cef4-194">Java와 함께 Azure를 사용하는 방법에 관한 자세한 정보는 [Java 개발자를 위한 Azure]와 [Azure DevOps 및 Java 사용하기]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cef4-194">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="0cef4-195">Spring Boot on Docker 샘플 프로젝트에 대한 자세한 정보는 [Spring Boot on Docker 시작]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cef4-195">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="0cef4-196">자체 Spring Boot 애플리케이션을 시작하는 데 도움이 필요하면 https://start.spring.io/에서 **Spring Initializr**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cef4-196">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="0cef4-197">간단한 Spring Boot 애플리케이션을 만들기 시작하는 방법에 대한 자세한 내용은 https://start.spring.io/에서 Spring Initializr를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cef4-197">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="0cef4-198">Azure와 함께 사용자 지정 Docker 이미지를 사용하는 방법에 대한 추가 예제를 보려면 [Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cef4-198">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Java 개발자를 위한 Azure]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Azure Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Azure Portal을 사용하여 프라이빗 Docker 컨테이너 레지스트리 만들기]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Azure DevOps 및 Java 사용하기]: /azure/devops/java/
[Working with Azure DevOps and Java]: /azure/devops/java/
[Maven]: http://maven.apache.org/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker 시작]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-linux/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-linux/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-linux/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-linux/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-linux/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-linux/AR04.png

[LX01]: ./media/deploy-spring-boot-java-app-on-linux/LX01.png
[LX02]: ./media/deploy-spring-boot-java-app-on-linux/LX02.png
[LX03]: ./media/deploy-spring-boot-java-app-on-linux/LX03.png
