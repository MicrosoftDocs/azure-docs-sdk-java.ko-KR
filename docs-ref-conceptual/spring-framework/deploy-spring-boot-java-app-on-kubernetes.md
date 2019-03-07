---
title: Azure Kubernetes Service에서 Kubernetes에 Spring Boot 앱 배포
description: 이 자습서에서는 Microsoft Azure에서 Kubernetes 클러스터에 Spring Boot 애플리케이션을 배포하는 단계를 안내합니다.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: 87bbf46fe5b22c4a147d6010d3813334caa774fb
ms.sourcegitcommit: 1c1412ad5d8960975c3fc7fd3d1948152ef651ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57335416"
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-kubernetes-service"></a><span data-ttu-id="f7970-103">Azure Kubernetes Service의 Kubernetes 클러스터에 Spring Boot 애플리케이션 배포</span><span class="sxs-lookup"><span data-stu-id="f7970-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Kubernetes Service</span></span>

<span data-ttu-id="f7970-104">**[Kubernetes]** 및 **[Docker]** 는 개발자가 컨테이너에서 실행 중인 애플리케이션의 배포, 확장 및 관리를 자동화하는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-104">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications running in containers.</span></span>

<span data-ttu-id="f7970-105">이 자습서에서는 이러한 두 가지 인기 있는 오픈 소스 기술을 결합하여 Spring Boot 애플리케이션을 개발하고 Microsoft Azure에 배포하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-105">This tutorial walks you through combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="f7970-106">좀 더 구체적으로 말하면 애플리케이션 개발을 위해 *[Spring Boot]*, 컨테이너 배포를 위해 *[Kubernetes]* 및 애플리케이션을 호스트하기 위해 [AKS(Azure Kubernetes Service)]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-106">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Kubernetes Service (AKS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f7970-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f7970-107">Prerequisites</span></span>

* <span data-ttu-id="f7970-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="f7970-109">[Azure CLI(명령줄 인터페이스)]</span><span class="sxs-lookup"><span data-stu-id="f7970-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="f7970-110">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="f7970-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="f7970-111">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7970-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="f7970-112">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="f7970-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="f7970-113">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="f7970-113">A [Git] client.</span></span>
* <span data-ttu-id="f7970-114">[Docker] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="f7970-114">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="f7970-115">이 자습서의 가상화 요구 사항으로 인해 가상 머신에는 이 문서의 단계를 따를 수 없습니다. 따라서 가상화 기능이 사용하도록 설정된 물리적 컴퓨터를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-115">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="f7970-116">Spring Boot on Docker 시작 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="f7970-116">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="f7970-117">다음 단계에서는 Spring Boot 웹 애플리케이션을 빌드하고 로컬로 테스트하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-117">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="f7970-118">명령 프롬프트를 열고 애플리케이션을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-118">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="f7970-119">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="f7970-119">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="f7970-120">[Spring Boot on Docker 시작] 샘플 프로젝트를 디렉터리에 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-120">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="f7970-121">디렉터리를 완료된 프로젝트로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-121">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="f7970-122">Maven을 사용하여 샘플 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-122">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="f7970-123">`http://localhost:8080`으로 이동하거나 `curl` 명령을 사용하여 웹앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-123">Test the web app by browsing to `http://localhost:8080`, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="f7970-124">다음 메시지가 표시되어야 합니다. **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="f7970-124">You should see the following message displayed: **Hello Docker World**</span></span>

   ![로컬로 샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="f7970-126">Azure CLI를 사용하여 Azure Container Registry 만들기</span><span class="sxs-lookup"><span data-stu-id="f7970-126">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="f7970-127">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-127">Open a command prompt.</span></span>

1. <span data-ttu-id="f7970-128">Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-128">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="f7970-129">Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-129">Choose your Azure Subscription:</span></span>
   ```azurecli
   az account set -s <YourSubscriptionID>
   ```

1. <span data-ttu-id="f7970-130">이 자습서에서 사용되는 Azure 리소스에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-130">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="f7970-131">리소스 그룹에서 개인 Azure Container Registry를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-131">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="f7970-132">이 자습서는 이후 단계에서 샘플 앱을 이 레지스트리에 Docker 이미지로 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-132">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="f7970-133">`wingtiptoysregistry`를 레지스트리의 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a><span data-ttu-id="f7970-134">컨테이너 레지스트리에 앱 푸시</span><span class="sxs-lookup"><span data-stu-id="f7970-134">Push your app to the container registry</span></span>

1. <span data-ttu-id="f7970-135">Maven 설치에 대한 구성 디렉터리(default ~/.m2/ 또는 C:\Users\username\.m2)로 이동한 후 텍스트 편집기를 사용하여 *settings.xml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-135">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="f7970-136">Azure CLI에서 컨테이너 레지스트리에 대한 암호를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-136">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="f7970-137">Azure Container Registry ID 및 암호를 *settings.xml* 파일의 새 `<server>` 컬렉션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-137">Add your Azure Container Registry id and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="f7970-138">`id` 및 `username`은 레지스트리의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-138">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="f7970-139">이전 명령의 `password` 값을 사용합니다(따옴표 제외).</span><span class="sxs-lookup"><span data-stu-id="f7970-139">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="f7970-140">Spring Boot 애플리케이션에 대해 완료된 프로젝트 디렉터리로 이동하고(예: "*C:\SpringBoot\gs-spring-boot-docker\complete*"또는"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") 텍스트 편집기를 사용하여 *pom.xml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-140">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="f7970-141">*pom.xml* 파일의 `<properties>` 컬렉션을 Azure Container Registry의 로그인 서버 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-141">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="f7970-142">*pom.xml* 파일의 `<plugins>` 컬렉션을 업데이트하여 `<plugin>`에 Azure Container Registry의 로그인 서버 주소 및 레지스트리 이름이 포함되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-142">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <buildArgs>
            <JAR_FILE>target/${project.build.finalName}.jar</JAR_FILE>
         </buildArgs>
         <baseImage>java</baseImage>
         <entryPoint>["java", "-jar", "/${project.build.finalName}.jar"]</entryPoint>
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

1. <span data-ttu-id="f7970-143">Spring Boot 애플리케이션에 대한 완성된 프로젝트 디렉터리로 이동한 후 다음 명령을 실행하여 Docker 컨테이너를 빌드하고 레지스트리에 이미지를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-143">Navigate to the completed project directory for your Spring Boot application and run the following command to build the Docker container and push the image to the registry:</span></span>

   ```
   mvn package dockerfile:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="f7970-144">Maven이 Azure에 이미지를 푸시하는 경우 다음 중 하나와 비슷한 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-144">You may receive an error message that is similar to one of the following when Maven pushes the image to Azure:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="f7970-145">이 오류가 발생하는 경우 Docker 명령줄에서 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-145">If you get this error, log in to Azure from the Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="f7970-146">그런 다음 컨테이너를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a><span data-ttu-id="f7970-147">Azure CLI를 사용하여 AKS에서 Kubernetes 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="f7970-147">Create a Kubernetes Cluster on AKS using the Azure CLI</span></span>

1. <span data-ttu-id="f7970-148">Azure Kubernetes Service에서 Kubernetes 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="f7970-148">Create a Kubernetes cluster in Azure Kubernetes Service.</span></span> <span data-ttu-id="f7970-149">다음 명령은 *wingtiptoys-akscluster*를 클러스터 이름으로 사용하고 *wingtiptoys-kubernetes*를 DNS 접두어로 사용하여 *wingtiptoys-kubernetes* 리소스 그룹에 *kubernetes* 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-149">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-akscluster* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az aks create --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster \ 
    --dns-name-prefix=wingtiptoys-kubernetes --generate-ssh-keys
   ```
   <span data-ttu-id="f7970-150">이 명령을 완료하는 데 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-150">This command may take a while to complete.</span></span>

1. <span data-ttu-id="f7970-151">AKS(Azure Kubernetes Service)에서 ACR(Azure Container Registry)을 사용할 때는 인증 메커니즘을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-151">When you're using Azure Container Registry (ACR) with Azure Kubernetes Service (AKS), an authentication mechanism needs to be established.</span></span> <span data-ttu-id="f7970-152">[Azure Kubernetes Service의 Azure Container Registry를 사용하여 인증]의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-152">Follow the steps in [Authenticate with Azure Container Registry from Azure Kubernetes Service] to grant AKS access to ACR.</span></span>


1. <span data-ttu-id="f7970-153">Azure CLI를 사용하여 `kubectl`을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-153">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="f7970-154">Linux 사용자는 이 명령 앞에 `sudo`를 붙여야 할 수 있습니다. 그러면 Kubernetes CLI가 `/usr/local/bin`에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-154">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az aks install-cli
   ```

1. <span data-ttu-id="f7970-155">Kubernetes 웹 인터페이스 및 `kubectl`에서 클러스터를 관리할 수 있도록 클러스터 구성 정보를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-155">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az aks get-credentials --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="f7970-156">Kubernetes 클러스터에 이미지 배포</span><span class="sxs-lookup"><span data-stu-id="f7970-156">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="f7970-157">이 자습서는 `kubectl`을 사용하여 앱을 배포한 다음 Kubernetes 웹 인터페이스를 통해 배포를 탐색할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-157">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="f7970-158">Kubernetes 웹 인터페이스를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="f7970-158">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="f7970-159">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-159">Open a command prompt.</span></span>

1. <span data-ttu-id="f7970-160">기본 브라우저에서 Kubernetes 클러스터에 대한 구성 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-160">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az aks browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

1. <span data-ttu-id="f7970-161">브라우저에서 Kubernetes 구성 웹 사이트가 열리면 해당 링크를 클릭하여 **컨테이너화된 앱을 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-161">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Kubernetes 구성 웹 사이트][KB01]

1. <span data-ttu-id="f7970-163">**Resource Creation** 페이지가 표시되면 다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-163">When the **Resource Creation** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="f7970-164">a.</span><span class="sxs-lookup"><span data-stu-id="f7970-164">a.</span></span> <span data-ttu-id="f7970-165">**앱 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-165">Select **CREATE AN APP**.</span></span>

   <span data-ttu-id="f7970-166">b.</span><span class="sxs-lookup"><span data-stu-id="f7970-166">b.</span></span> <span data-ttu-id="f7970-167">**App name**에 Spring Boot 애플리케이션 이름을 입력합니다(예: "*gs-spring-boot-docker*").</span><span class="sxs-lookup"><span data-stu-id="f7970-167">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="f7970-168">다.</span><span class="sxs-lookup"><span data-stu-id="f7970-168">c.</span></span> <span data-ttu-id="f7970-169">**Container image**에 대해 이전의 로그인 서버 및 컨테이너 이미지를 입력합니다(예: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*").</span><span class="sxs-lookup"><span data-stu-id="f7970-169">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="f7970-170">d.</span><span class="sxs-lookup"><span data-stu-id="f7970-170">d.</span></span> <span data-ttu-id="f7970-171">**Service**에 대해 **External**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-171">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="f7970-172">e.</span><span class="sxs-lookup"><span data-stu-id="f7970-172">e.</span></span> <span data-ttu-id="f7970-173">**Port** 및 **Target Port** 텍스트 상자에 외부 및 내부 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-173">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Kubernetes 구성 웹 사이트][KB02]


1. <span data-ttu-id="f7970-175">**Deploy**를 클릭하여 컨테이너를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-175">Click **Deploy** to deploy the container.</span></span>

   ![Kubernetes 배포][KB05]

1. <span data-ttu-id="f7970-177">애플리케이션이 배포되면 **Services** 아래에 Spring Boot 애플리케이션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-177">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Kubernetes 서비스][KB06]

1. <span data-ttu-id="f7970-179">**External endpoints**에 대한 링크를 클릭하면 Azure에서 Spring Boot 애플리케이션이 실행되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-179">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Kubernetes 서비스][KB07]

   ![Azure에서 샘플 앱 찾아보기][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="f7970-182">kubectl을 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="f7970-182">Deploy with kubectl</span></span>

1. <span data-ttu-id="f7970-183">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-183">Open a command prompt.</span></span>

1. <span data-ttu-id="f7970-184">`kubectl run` 명령을 사용하여 Kubernetes 클러스터에서 컨테이너를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-184">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="f7970-185">Kubernetes의 앱에 대한 서비스 이름 및 전체 이미지 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-185">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="f7970-186">예: </span><span class="sxs-lookup"><span data-stu-id="f7970-186">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="f7970-187">이 명령에서 다음이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-187">In this command:</span></span>

   * <span data-ttu-id="f7970-188">컨테이너 이름 `gs-spring-boot-docker`는 `run` 명령 바로 다음에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-188">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="f7970-189">`--image` 매개 변수는 결합된 로그인 서버 및 이미지 이름을 `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-189">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="f7970-190">`kubectl expose` 명령을 사용하여 Kubernetes 클러스터를 외부에 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-190">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="f7970-191">서비스 이름, 앱에 액세스하는 데 사용되는 공용 TCP 포트 및 앱이 수신 대기하는 내부 대상 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-191">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="f7970-192">예: </span><span class="sxs-lookup"><span data-stu-id="f7970-192">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="f7970-193">이 명령에서 다음이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-193">In this command:</span></span>

   * <span data-ttu-id="f7970-194">컨테이너 이름 `gs-spring-boot-docker`는 `expose deployment` 명령 바로 다음에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-194">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="f7970-195">`--type` 매개 변수는 클러스터가 부하 분산 장치를 사용함을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-195">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="f7970-196">`--port` 매개 변수는 공용 TCP 포트 80을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-196">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="f7970-197">이 포트에서 앱에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-197">You access the app on this port.</span></span>

   * <span data-ttu-id="f7970-198">`--target-port` 매개 변수는 내부 TCP 포트 8080을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-198">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="f7970-199">부하 분산 장치는 이 포트에서 앱으로 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-199">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="f7970-200">앱이 클러스터에 배포되면 외부 IP 주소를 쿼리하고 웹 브라우저에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-200">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Azure에서 샘플 앱 찾아보기][SB02]


## <a name="next-steps"></a><span data-ttu-id="f7970-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7970-202">Next steps</span></span>

<span data-ttu-id="f7970-203">Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-203">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f7970-204">Azure의 Spring</span><span class="sxs-lookup"><span data-stu-id="f7970-204">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="f7970-205">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f7970-205">Additional Resources</span></span>

<span data-ttu-id="f7970-206">Azure에서 Spring Boot를 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7970-206">For more information about using Spring Boot on Azure, see the following articles:</span></span>

* [<span data-ttu-id="f7970-207">Azure App Service에 Spring Boot 애플리케이션 배포</span><span class="sxs-lookup"><span data-stu-id="f7970-207">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="f7970-208">Azure Container Service에서 Linux에 Spring Boot 애플리케이션 배포</span><span class="sxs-lookup"><span data-stu-id="f7970-208">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)

<span data-ttu-id="f7970-209">Java와 함께 Azure를 사용하는 방법에 관한 자세한 정보는 [Java 개발자를 위한 Azure]와 [Azure DevOps 및 Java 사용하기]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7970-209">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="f7970-210">Visual Studio Code를 사용하여 Kubernetes에 Java 애플리케이션을 배포하는 방법에 관한 자세한 정보는 [Visual Studio Code Java 자습서]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7970-210">For more information about deploying a Java application to Kubernetes with Visual Studio Code, see [Visual Studio Code Java Tutorials].</span></span>

<span data-ttu-id="f7970-211">Spring Boot on Docker 샘플 프로젝트에 대한 자세한 내용은 [Spring Boot on Docker 시작] 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7970-211">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="f7970-212">다음 링크는 Spring Boot 애플리케이션을 만드는 방법에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-212">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="f7970-213">간단한 Spring Boot 애플리케이션 만들기에 대한 자세한 내용은 https://start.spring.io/에서 Spring Initializr를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7970-213">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="f7970-214">다음 링크는 Azure에서 Kubernetes를 사용하는 방법에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-214">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="f7970-215">Azure Kubernetes Service에서 Kubernetes 클러스터 시작하기</span><span class="sxs-lookup"><span data-stu-id="f7970-215">Get started with a Kubernetes cluster in Azure Kubernetes Service</span></span>](/azure/aks/intro-kubernetes)

<span data-ttu-id="f7970-216">Kubernetes 명령줄 인터페이스를 사용하는 방법에 대한 자세한 내용은 <https://kubernetes.io/docs/user-guide/kubectl/>의 **kubectl** 사용자 가이드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-216">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="f7970-217">Kubernetes 웹 사이트에는 개인 레지스트리에서 이미지를 사용하는 방법을 설명하는 일부 문서가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7970-217">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="f7970-218">[Pod에 대한 서비스 계정 구성]</span><span class="sxs-lookup"><span data-stu-id="f7970-218">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="f7970-219">[네임스페이스]</span><span class="sxs-lookup"><span data-stu-id="f7970-219">[Namespaces]</span></span>
* <span data-ttu-id="f7970-220">[개인 레지스트리에서 이미지 끌어오기]</span><span class="sxs-lookup"><span data-stu-id="f7970-220">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="f7970-221">Azure와 함께 사용자 지정 Docker 이미지를 사용하는 방법에 대한 추가 예제를 보려면 [Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7970-221">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[AKS(Azure Kubernetes Service)]: https://azure.microsoft.com/services/kubernetes-service/
[Azure Kubernetes Service (AKS)]: https://azure.microsoft.com/services/kubernetes-service/
[Java 개발자를 위한 Azure]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Azure DevOps 및 Java 사용하기]: /azure/devops/java/
[Working with Azure DevOps and Java]: /azure/devops/java/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker 시작]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Pod에 대한 서비스 계정 구성]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[네임스페이스]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[개인 레지스트리에서 이미지 끌어오기]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/
[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- Newly added -->
[Azure Kubernetes Service의 Azure Container Registry를 사용하여 인증]: /azure/container-registry/container-registry-auth-aks/
[Authenticate with Azure Container Registry from Azure Kubernetes Service]: /azure/container-registry/container-registry-auth-aks/
[Visual Studio Code Java 자습서]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Visual Studio Code Java Tutorials]: https://code.visualstudio.com/docs/java/java-kubernetes/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR04.png

[KB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB01.png
[KB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB02.png
[KB03]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB03.png
[KB04]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB04.png
[KB05]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB05.png
[KB06]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB06.png
[KB07]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB07.png
