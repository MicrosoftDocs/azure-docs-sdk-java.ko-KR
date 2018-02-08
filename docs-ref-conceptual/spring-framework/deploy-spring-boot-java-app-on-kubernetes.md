---
title: "Azure Container Service에서 Kubernetes에 Spring Boot 앱 배포"
description: "이 자습서에서는 Microsoft Azure에서 Kubernetes 클러스터에 Spring Boot 응용 프로그램을 배포하는 단계를 안내합니다."
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: asirveda;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: 9eb37f302835ea40e92b5212d5bbc305d1311bc4
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a><span data-ttu-id="bb7be-103">Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="bb7be-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>

<span data-ttu-id="bb7be-104">**[Kubernetes]** 및  **[Docker]**는 개발자가 컨테이너에서 실행 중인 응용 프로그램의 배포, 확장 및 관리를 자동화하는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-104">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="bb7be-105">이 자습서에서는 이러한 두 가지 인기 있는 오픈 소스 기술을 결합하여 Spring Boot 응용 프로그램을 개발하고 Microsoft Azure에 배포하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-105">This tutorial walks you though combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="bb7be-106">좀 더 구체적으로 말하면 응용 프로그램 개발을 위해 *[Spring Boot]*, 컨테이너 배포를 위해 *[Kubernetes]* 및 응용 프로그램을 호스트하기 위해 [AKS(Azure Container Service)]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-106">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Container Service (AKS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="bb7be-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="bb7be-107">Prerequisites</span></span>

* <span data-ttu-id="bb7be-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [무료 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="bb7be-109">[Azure CLI(명령줄 인터페이스)]</span><span class="sxs-lookup"><span data-stu-id="bb7be-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="bb7be-110">최신 [JDK(Java Developer Kit)]</span><span class="sxs-lookup"><span data-stu-id="bb7be-110">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="bb7be-111">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="bb7be-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="bb7be-112">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="bb7be-112">A [Git] client.</span></span>
* <span data-ttu-id="bb7be-113">[Docker] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="bb7be-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="bb7be-114">이 자습서의 가상화 요구 사항으로 인해 가상 머신에는 이 문서의 단계를 따를 수 없습니다. 따라서 가상화 기능이 사용하도록 설정된 물리적 컴퓨터를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="bb7be-115">Spring Boot on Docker 시작 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="bb7be-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="bb7be-116">다음 단계에서는 Spring Boot 웹 응용 프로그램을 빌드하고 로컬로 테스트하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-116">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="bb7be-117">명령 프롬프트를 열고 응용 프로그램을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="bb7be-118">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="bb7be-118">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="bb7be-119">[ 시작] 샘플 프로젝트를 디렉터리에 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="bb7be-120">디렉터리를 완료된 프로젝트로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-120">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="bb7be-121">Maven을 사용하여 샘플 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-121">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="bb7be-122">http://localhost:8080 으로 이동하거나 다음`curl` 명령을 사용하여 웹앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-122">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="bb7be-123">**Hello Docker World** 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-123">You should see the following message displayed: **Hello Docker World**</span></span>

   ![로컬로 샘플 앱 찾아보기][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="bb7be-125">Azure CLI를 사용하여 Azure Container Registry 만들기</span><span class="sxs-lookup"><span data-stu-id="bb7be-125">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="bb7be-126">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-126">Open a command prompt.</span></span>

1. <span data-ttu-id="bb7be-127">Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-127">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="bb7be-128">이 자습서에서 사용되는 Azure 리소스에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-128">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="bb7be-129">리소스 그룹에서 개인 Azure Container Registry를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-129">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="bb7be-130">이 자습서는 이후 단계에서 샘플 앱을 이 레지스트리에 Docker 이미지로 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-130">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="bb7be-131">`wingtiptoysregistry`를 레지스트리의 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-131">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a><span data-ttu-id="bb7be-132">컨테이너 레지스트리에 앱 푸시</span><span class="sxs-lookup"><span data-stu-id="bb7be-132">Push your app to the container registry</span></span>

1. <span data-ttu-id="bb7be-133">Maven 설치에 대한 구성 디렉터리(default ~/.m2/ 또는 C:\Users\username\.m2)로 이동한 후 텍스트 편집기를 사용하여 *settings.xml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-133">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="bb7be-134">Azure CLI에서 컨테이너 레지스트리에 대한 암호를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-134">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="bb7be-135">Azure Container Registry ID 및 암호를 *settings.xml* 파일의 새 `<server>` 컬렉션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-135">Add your Azure Container Registry id and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="bb7be-136">`id` 및 `username`은 레지스트리의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-136">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="bb7be-137">이전 명령의 `password` 값을 사용합니다(따옴표 제외).</span><span class="sxs-lookup"><span data-stu-id="bb7be-137">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="bb7be-138">Spring Boot 응용 프로그램에 대해 완료된 프로젝트 디렉터리로 이동하고(예: "*C:\SpringBoot\gs-spring-boot-docker\complete*"또는"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") 텍스트 편집기를 사용하여 *pom.xml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-138">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="bb7be-139">*pom.xml* 파일의 `<properties>` 컬렉션을 Azure Container Registry의 로그인 서버 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-139">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="bb7be-140">*pom.xml* 파일의 `<plugins>` 컬렉션을 업데이트하여 `<plugin>`에 Azure Container Registry의 로그인 서버 주소 및 레지스트리 이름이 포함되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-140">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="bb7be-141">Spring Boot 응용 프로그램에 대한 완성된 프로젝트 디렉터리로 이동한 후 다음 명령을 실행하여 Docker 컨테이너를 빌드하고 레지스트리에 이미지를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-141">Navigate to the completed project directory for your Spring Boot application and run the following command to build the Docker container and push the image to the registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="bb7be-142">Maven이 Azure에 이미지를 푸시하는 경우 다음 중 하나와 비슷한 오류 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-142">You may receive an error message that is similar to one of the following when Maven pushes the image to Azure:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="bb7be-143">이 오류가 발생하는 경우 Docker 명령줄에서 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-143">If you get this error, log in to Azure from the Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="bb7be-144">그런 다음 컨테이너를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-144">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a><span data-ttu-id="bb7be-145">Azure CLI를 사용하여 AKS에서 Kubernetes 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="bb7be-145">Create a Kubernetes Cluster on AKS using the Azure CLI</span></span>

1. <span data-ttu-id="bb7be-146">Azure Container Service에서 Kubernetes 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-146">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="bb7be-147">다음 명령은 *wingtiptoys-containerservice*를 클러스터 이름으로 사용하고 *wingtiptoys-kubernetes*를 DNS 접두어로 사용하여 *wingtiptoys-kubernetes* 리소스 그룹에 *kubernetes* 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-147">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="bb7be-148">이 명령을 완료하는 데 다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-148">This command may take a while to complete.</span></span>

1. <span data-ttu-id="bb7be-149">Azure CLI를 사용하여 `kubectl`을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-149">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="bb7be-150">Linux 사용자는 이 명령 앞에 `sudo`를 붙여야 할 수 있습니다. 그러면 Kubernetes CLI가 `/usr/local/bin`에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-150">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="bb7be-151">Kubernetes 웹 인터페이스 및 `kubectl`에서 클러스터를 관리할 수 있도록 클러스터 구성 정보를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-151">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="bb7be-152">Kubernetes 클러스터에 이미지 배포</span><span class="sxs-lookup"><span data-stu-id="bb7be-152">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="bb7be-153">이 자습서는 `kubectl`을 사용하여 앱을 배포한 다음 Kubernetes 웹 인터페이스를 통해 배포를 탐색할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-153">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="bb7be-154">Kubernetes 웹 인터페이스를 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="bb7be-154">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="bb7be-155">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-155">Open a command prompt.</span></span>

1. <span data-ttu-id="bb7be-156">기본 브라우저에서 Kubernetes 클러스터에 대한 구성 웹 사이트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-156">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="bb7be-157">브라우저에서 Kubernetes 구성 웹 사이트가 열리면 해당 링크를 클릭하여 **컨테이너화된 앱을 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-157">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Kubernetes 구성 웹 사이트][KB01]

1. <span data-ttu-id="bb7be-159">**Deploy a containerized app** 페이지가 표시되면 다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-159">When the **Deploy a containerized app** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="bb7be-160">a.</span><span class="sxs-lookup"><span data-stu-id="bb7be-160">a.</span></span> <span data-ttu-id="bb7be-161">**Specify app details below**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-161">Select **Specify app details below**.</span></span>

   <span data-ttu-id="bb7be-162">나.</span><span class="sxs-lookup"><span data-stu-id="bb7be-162">b.</span></span> <span data-ttu-id="bb7be-163">**App name**에 Spring Boot 응용 프로그램 이름을 입력합니다(예: "*gs-spring-boot-docker*").</span><span class="sxs-lookup"><span data-stu-id="bb7be-163">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="bb7be-164">다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-164">c.</span></span> <span data-ttu-id="bb7be-165">**Container image**에 대해 이전의 로그인 서버 및 컨테이너 이미지를 입력합니다(예: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*").</span><span class="sxs-lookup"><span data-stu-id="bb7be-165">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="bb7be-166">d.</span><span class="sxs-lookup"><span data-stu-id="bb7be-166">d.</span></span> <span data-ttu-id="bb7be-167">**Service**에 대해 **External**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-167">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="bb7be-168">e.</span><span class="sxs-lookup"><span data-stu-id="bb7be-168">e.</span></span> <span data-ttu-id="bb7be-169">**Port** 및 **Target Port** 텍스트 상자에 외부 및 내부 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-169">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Kubernetes 구성 웹 사이트][KB02]


1. <span data-ttu-id="bb7be-171">**Deploy**를 클릭하여 컨테이너를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-171">Click **Deploy** to deploy the container.</span></span>

   ![컨테이너 배포][KB05]

1. <span data-ttu-id="bb7be-173">응용 프로그램이 배포되면 **Services** 아래에 Spring Boot 응용 프로그램이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-173">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Kubernetes 서비스][KB06]

1. <span data-ttu-id="bb7be-175">**External endpoints**에 대한 링크를 클릭하면 Azure에서 Spring Boot 응용 프로그램이 실행되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-175">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Kubernetes 서비스][KB07]

   ![Azure에서 샘플 앱 찾아보기][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="bb7be-178">kubectl을 사용하여 배포</span><span class="sxs-lookup"><span data-stu-id="bb7be-178">Deploy with kubectl</span></span>

1. <span data-ttu-id="bb7be-179">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-179">Open a command prompt.</span></span>

1. <span data-ttu-id="bb7be-180">`kubectl run` 명령을 사용하여 Kubernetes 클러스터에서 컨테이너를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-180">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="bb7be-181">Kubernetes의 앱에 대한 서비스 이름 및 전체 이미지 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-181">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="bb7be-182">예: </span><span class="sxs-lookup"><span data-stu-id="bb7be-182">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="bb7be-183">이 명령에서 다음이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-183">In this command:</span></span>

   * <span data-ttu-id="bb7be-184">컨테이너 이름 `gs-spring-boot-docker`는 `run` 명령 바로 다음에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-184">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="bb7be-185">`--image` 매개 변수는 결합된 로그인 서버 및 이미지 이름을 `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-185">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="bb7be-186">`kubectl expose` 명령을 사용하여 Kubernetes 클러스터를 외부에 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-186">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="bb7be-187">서비스 이름, 앱에 액세스하는 데 사용되는 공용 TCP 포트 및 앱이 수신 대기하는 내부 대상 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-187">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="bb7be-188">예: </span><span class="sxs-lookup"><span data-stu-id="bb7be-188">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="bb7be-189">이 명령에서 다음이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-189">In this command:</span></span>

   * <span data-ttu-id="bb7be-190">컨테이너 이름 `gs-spring-boot-docker`는 `expose deployment` 명령 바로 다음에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-190">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="bb7be-191">`--type` 매개 변수는 클러스터가 부하 분산 장치를 사용함을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-191">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="bb7be-192">`--port` 매개 변수는 공용 TCP 포트 80을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-192">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="bb7be-193">이 포트에서 앱에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-193">You access the app on this port.</span></span>

   * <span data-ttu-id="bb7be-194">`--target-port` 매개 변수는 내부 TCP 포트 8080을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-194">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="bb7be-195">부하 분산 장치는 이 포트에서 앱으로 요청을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-195">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="bb7be-196">앱이 클러스터에 배포되면 외부 IP 주소를 쿼리하고 웹 브라우저에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-196">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Azure에서 샘플 앱 찾아보기][SB02]


## <a name="next-steps"></a><span data-ttu-id="bb7be-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bb7be-198">Next steps</span></span>

<span data-ttu-id="bb7be-199">Azure에서 Spring Boot를 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb7be-199">For more information about using Spring Boot on Azure, see the following articles:</span></span>

* [<span data-ttu-id="bb7be-200">Azure App Service에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="bb7be-200">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="bb7be-201">Azure Container Service에서 Linux에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="bb7be-201">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)

<span data-ttu-id="bb7be-202">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb7be-202">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="bb7be-203">Spring Boot on Docker 샘플 프로젝트에 대한 자세한 내용은 [ 시작]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb7be-203">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="bb7be-204">다음 링크는 Spring Boot 응용 프로그램을 만드는 방법에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-204">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="bb7be-205">간단한 Spring Boot 응용 프로그램 만들기에 대한 자세한 내용은 https://start.spring.io/에서 Spring Initializr를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb7be-205">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="bb7be-206">다음 링크는 Azure에서 Kubernetes를 사용하는 방법에 대한 추가 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-206">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="bb7be-207">Container Service에서 Kubernetes 클러스터 시작</span><span class="sxs-lookup"><span data-stu-id="bb7be-207">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="bb7be-208">Azure Container Service에서 Kubernetes 웹 UI 사용</span><span class="sxs-lookup"><span data-stu-id="bb7be-208">Using the Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="bb7be-209">Kubernetes 명령줄 인터페이스를 사용하는 방법에 대한 자세한 내용은 <https://kubernetes.io/docs/user-guide/kubectl/>의 **kubectl** 사용자 가이드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-209">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="bb7be-210">Kubernetes 웹 사이트에는 개인 레지스트리에서 이미지를 사용하는 방법을 설명하는 일부 문서가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bb7be-210">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="bb7be-211">[Pod에 대한 서비스 계정 구성]</span><span class="sxs-lookup"><span data-stu-id="bb7be-211">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="bb7be-212">[네임스페이스]</span><span class="sxs-lookup"><span data-stu-id="bb7be-212">[Namespaces]</span></span>
* <span data-ttu-id="bb7be-213">[개인 레지스트리에서 이미지 끌어오기]</span><span class="sxs-lookup"><span data-stu-id="bb7be-213">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="bb7be-214">Azure와 함께 사용자 지정 Docker 이미지를 사용하는 방법에 대한 추가 예제를 보려면 [Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bb7be-214">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview
[AKS(Azure Container Service)]: https://azure.microsoft.com/services/container-service/
[Java 개발자용 Azure]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[무료 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK(Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[ 시작]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Pod에 대한 서비스 계정 구성]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[네임스페이스]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[개인 레지스트리에서 이미지 끌어오기]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

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
