---
title: Azure Container Service에서 Linux에 Spring Boot Web App 배포
description: 이 자습서에서는 Microsoft Azure에서 Linux Web App으로 Spring Boot 애플리케이션을 배포하는 단계를 설명합니다.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 30be16aebb18e3c9e18f9a023ea9b82e5d614e94
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339147"
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a><span data-ttu-id="8051a-103">Azure Container Service에서 Linux에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="8051a-103">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>

<span data-ttu-id="8051a-104">이 자습서에서는 [Docker]를 사용하여 [AKS(Azure Container Service)]에서 [Spring Boot] 응용 프로그램을 개발하고 Linux 호스트에 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-104">This tutorial walks you through using [Docker] to develop and deploy a [Spring Boot] application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8051a-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8051a-105">Prerequisites</span></span>

<span data-ttu-id="8051a-106">이 자습서의 단계를 완료하려면 다음 필수 조건이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-106">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="8051a-107">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="8051a-108">[Azure CLI(명령줄 인터페이스)]</span><span class="sxs-lookup"><span data-stu-id="8051a-108">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="8051a-109">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="8051a-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="8051a-110">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8051a-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="8051a-111">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="8051a-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="8051a-112">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="8051a-112">A [Git] client.</span></span>
* <span data-ttu-id="8051a-113">[Docker] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="8051a-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="8051a-114">이 자습서의 가상화 요구 사항으로 인해 가상 머신에는 이 문서의 단계를 따를 수 없습니다. 따라서 가상화 기능이 사용하도록 설정된 물리적 컴퓨터를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="8051a-115">Spring Boot on Docker 시작 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="8051a-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="8051a-116">다음 단계에서는 간단한 Spring Boot 웹 응용 프로그램을 만들어 로컬로 테스트하는 데 필요한 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-116">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="8051a-117">명령 프롬프트를 열고 애플리케이션을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="8051a-118">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="8051a-118">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="8051a-119">[Spring Boot on Docker 시작] 샘플 프로젝트를 방금 만든 디렉터리에 복제합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8051a-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="8051a-120">디렉터리를 완료된 프로젝트로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8051a-120">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="8051a-121">Maven을 사용하여 JAR 파일을 빌드합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8051a-121">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="8051a-122">웹앱이 만들어지면 디렉터리를 JAR 파일이 위치한 `target` 디렉터리로 변경하고 웹앱을 시작합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8051a-122">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="8051a-123">웹 브라우저를 사용하여 로컬로 이동하여 웹앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-123">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="8051a-124">예를 들어 curl을 사용할 수 있고 포트 80에서 실행하도록 Tomcat 서버를 구성한 경우:</span><span class="sxs-lookup"><span data-stu-id="8051a-124">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="8051a-125">**Hello Docker World!** 라는 메시지가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-125">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![로컬로 샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="8051a-127">Azure Container Registry를 만들어서 개인 Docker 레지스트리로 사용</span><span class="sxs-lookup"><span data-stu-id="8051a-127">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="8051a-128">다음 단계에서는 Azure Portal을 사용하여 Azure Container Registry를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-128">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="8051a-129">Azure Portal 대신 Azure CLI를 사용하려는 경우 [Azure CLI 2.0을 사용하여 개인 Docker 컨테이너 레지스트리 만들기](/azure/container-registry/container-registry-get-started-azure-cli)의 단계에 따르세요.</span><span class="sxs-lookup"><span data-stu-id="8051a-129">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
>

1. <span data-ttu-id="8051a-130">[Azure Portal]을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-130">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="8051a-131">Azure Portal에서 사용자의 계정에 로그인한 다음, [Azure Portal을 사용하여 개인 Docker 컨테이너 레지스트리 만들기] 문서의 단계를 수행할 수 있습니다. 편의상 다음 단계에서 다시 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-131">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="8051a-132">**+ 새로 만들기**의 메뉴 아이콘을 클릭하고 **컨테이너**를 클릭한 다음, **Azure Container Registry**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-132">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![새로운 Azure Container Registry 만들기][AR01]

1. <span data-ttu-id="8051a-134">Azure Container Registry 템플릿에 대한 정보 페이지가 표시되면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-134">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![새로운 Azure Container Registry 만들기][AR02]

1. <span data-ttu-id="8051a-136">**컨테이너 레지스트리 만들기** 페이지가 표시되면 **레지스트리 이름** 및 **리소스 그룹**을 입력하고 **관리 사용자**에 대해 **사용**을 선택한 다음, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-136">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Azure Container Registry 설정 구성][AR03]

1. <span data-ttu-id="8051a-138">컨테이너 레지스트리를 만들면 Azure Portal에서 컨테이너 레지스트리를 탐색한 다음, **선택키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-138">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="8051a-139">다음 단계에서 사용하기 위해 사용자 이름과 암호를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-139">Take note of the username and password for the next steps.</span></span>

   ![Azure Container Registry 선택키][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="8051a-141">Azure Container Registry 선택키를 사용하도록 Maven 구성</span><span class="sxs-lookup"><span data-stu-id="8051a-141">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="8051a-142">Maven 설치를 위해 구성 디렉터리로 이동한 후 텍스트 편집기를 사용하여 *settings.xml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-142">Navigate to the configuration directory for your Maven installation and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="8051a-143">이 자습서의 이전 섹션에서 *settings.xml* 파일의 `<servers>` 컬렉션에 Azure Container Registry 액세스 설정을 추가합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8051a-143">Add your Azure Container Registry access settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="8051a-144">Spring Boot 응용 프로그램의 완성된 프로젝트 디렉터리로 이동하고(예: “*C:\SpringBoot\gs-spring-boot-docker\complete*” 또는 “*/users/robert/SpringBoot/gs-spring-boot-docker/complete*”) 텍스트 편집기를 사용하여 *pom.xml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-144">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="8051a-145">*pom.xml* 파일의 `<properties>` 컬렉션을 이 자습서의 이전 섹션에서 사용한 Azure Container Registry의 로그인 서버 값으로 업데이트합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8051a-145">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="8051a-146">*pom.xml* 파일의 `<plugins>` 컬렉션을 업데이트하여 `<plugin>`에 이 자습서의 이전 섹션에서 사용한 Azure Container Registry의 로그인 서버 주소 및 레지스트리 이름이 포함되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-146">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="8051a-147">예: </span><span class="sxs-lookup"><span data-stu-id="8051a-147">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="8051a-148">Spring Boot 응용 프로그램의 완성된 프로젝트 디렉터리로 이동하고 다음 명령을 실행하여 응용 프로그램을 다시 빌드하고 Azure Container Registry에 컨테이너를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-148">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="8051a-149">Azure에 Docker 컨테이너를 푸시할 때 Docker 컨테이너를 성공적으로 만들었더라도 다음 중 하나와 비슷한 오류 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-149">When you are pushing your Docker container to Azure, you may receive an error message that is similar to one of the following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="8051a-150">이런 경우 Docker 명령줄에서 Azure 계정에 로그인해야 합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8051a-150">If this happens, you may need to sign in to your Azure account from the Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="8051a-151">그런 다음, 명령줄에서 컨테이너를 푸시할 수 있습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8051a-151">You can then push your container from the command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="8051a-152">컨테이너 이미지를 사용하여 Azure App Service에서 Linux에 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="8051a-152">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="8051a-153">[Azure Portal]을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-153">Browse to the [Azure portal] and sign in.</span></span>

2. <span data-ttu-id="8051a-154">**+ 새로 만들기**의 메뉴 아이콘을 클릭하고 **웹 + 모바일**을 클릭한 다음 **}Web App on Linux**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-154">Click the menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Azure Portal에서 새로운 웹앱 만들기][LX01]

3. <span data-ttu-id="8051a-156">**Web App on Linux** 페이지가 표시되면 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-156">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="8051a-157">a.</span><span class="sxs-lookup"><span data-stu-id="8051a-157">a.</span></span> <span data-ttu-id="8051a-158">**앱 이름**에 고유한 이름을 입력합니다. 예: "*wingtiptoyslinux*."</span><span class="sxs-lookup"><span data-stu-id="8051a-158">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="8051a-159">b.</span><span class="sxs-lookup"><span data-stu-id="8051a-159">b.</span></span> <span data-ttu-id="8051a-160">드롭다운 목록에서 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-160">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="8051a-161">다.</span><span class="sxs-lookup"><span data-stu-id="8051a-161">c.</span></span> <span data-ttu-id="8051a-162">기존 **리소스 그룹**을 선택하거나 새 리소스 그룹을 만들기 위해 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-162">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="8051a-163">d.</span><span class="sxs-lookup"><span data-stu-id="8051a-163">d.</span></span> <span data-ttu-id="8051a-164">**컨테이너 구성**을 클릭하고 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-164">Click **Configure container** and enter the following information:</span></span>

   * <span data-ttu-id="8051a-165">**개인 레지스트리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-165">Choose **Private registry**.</span></span>

   * <span data-ttu-id="8051a-166">**이미지 및 선택적 태그**: 이전에 사용한 컨테이너 이름을 지정합니다. 예: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span><span class="sxs-lookup"><span data-stu-id="8051a-166">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

   * <span data-ttu-id="8051a-167">**서버 URL**: 이전의 레지스트리 URL을 지정합니다. 예: "*<https://wingtiptoysregistry.azurecr.io>*"</span><span class="sxs-lookup"><span data-stu-id="8051a-167">**Server URL**: Specify your registry URL from earlier; for example: "*<https://wingtiptoysregistry.azurecr.io>*"</span></span>

   * <span data-ttu-id="8051a-168">**로그인 사용자 이름** 및 **암호**: 이전 단계에서 사용한 **액세스 키**의 로그인 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-168">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="8051a-169">e.</span><span class="sxs-lookup"><span data-stu-id="8051a-169">e.</span></span> <span data-ttu-id="8051a-170">위의 정보를 모두 입력하면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-170">Once you have entered all of the above information, click **OK**.</span></span>

   ![웹앱 설정 구성][LX02]

4. <span data-ttu-id="8051a-172">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-172">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="8051a-173">Azure에서는 표준 포트 80 또는 8080에서 실행되는 임베디드 Tomcat 서버에 인터넷 요청을 자동으로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-173">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="8051a-174">그러나 사용자 지정 포트에서 임베디드 Tomcat 서버를 실행하도록 구성한 경우, 임베디드 Tomcat 서버에 포트를 정의하는 웹앱에 환경 변수를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-174">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="8051a-175">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-175">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="8051a-176">[Azure Portal]을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-176">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="8051a-177">**App Services** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-177">Click the icon for **App Services**.</span></span> <span data-ttu-id="8051a-178">(아래 이미지에서 항목 #1 참조)</span><span class="sxs-lookup"><span data-stu-id="8051a-178">(See item #1 in the image below.)</span></span>
>
> 3. <span data-ttu-id="8051a-179">목록에서 웹앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-179">Select your web app from the list.</span></span> <span data-ttu-id="8051a-180">(아래 이미지에서 항목 #2)</span><span class="sxs-lookup"><span data-stu-id="8051a-180">(Item #2 in the image below.)</span></span>
>
> 4. <span data-ttu-id="8051a-181">**응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-181">Click **Application Settings**.</span></span> <span data-ttu-id="8051a-182">(아래 이미지에서 항목 #3)</span><span class="sxs-lookup"><span data-stu-id="8051a-182">(Item #3 in the image below.)</span></span>
>
> 5. <span data-ttu-id="8051a-183">**앱 설정** 섹션에서 **PORT**라는 새 환경 변수를 추가하고 값에 사용자 지정 포트 번호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-183">In the **App settings** section, add a new environment variable named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="8051a-184">(아래 이미지에서 항목 #4)</span><span class="sxs-lookup"><span data-stu-id="8051a-184">(Item #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="8051a-185">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8051a-185">Click **Save**.</span></span> <span data-ttu-id="8051a-186">(아래 이미지에서 항목 #5)</span><span class="sxs-lookup"><span data-stu-id="8051a-186">(Item #5 in the image below.)</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="8051a-188">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8051a-188">Next steps</span></span>

<span data-ttu-id="8051a-189">Azure에서 Spring Boot 애플리케이션을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8051a-189">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="8051a-190">Azure App Service에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="8051a-190">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="8051a-191">Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="8051a-191">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="8051a-192">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8051a-192">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="8051a-193">Spring Boot on Docker 샘플 프로젝트에 대한 자세한 정보는 [Spring Boot on Docker 시작]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8051a-193">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="8051a-194">자체 Spring Boot 애플리케이션을 시작하는 데 도움이 필요하면 https://start.spring.io/에서 **Spring Initializr**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8051a-194">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="8051a-195">간단한 Spring Boot 애플리케이션을 만들기 시작하는 방법에 대한 자세한 내용은 https://start.spring.io/에서 Spring Initializr를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8051a-195">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="8051a-196">Azure와 함께 사용자 지정 Docker 이미지를 사용하는 방법에 대한 추가 예제를 보려면 [Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8051a-196">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[AKS(Azure Container Service)]: https://azure.microsoft.com/services/container-service/
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Java 개발자용 Azure]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Azure Portal을 사용하여 개인 Docker 컨테이너 레지스트리 만들기]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
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
