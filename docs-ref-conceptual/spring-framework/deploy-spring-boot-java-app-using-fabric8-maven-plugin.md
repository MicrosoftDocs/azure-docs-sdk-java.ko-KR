---
title: Fabric8 Maven 플러그인을 사용하여 Spring Boot 앱 배포
description: 이 자습서에서는 Apache Maven용 Fabric8 플러그인을 사용하여 Microsoft Azure에 Spring Boot 응용 프로그램을 배포하는 단계를 설명합니다.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: ab3babf358cf4899709a9a9d2d7917cb2c6d220e
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338837"
---
# <a name="deploy-a-spring-boot-app-using-the-fabric8-maven-plugin"></a><span data-ttu-id="6d284-103">Fabric8 Maven 플러그인을 사용하여 Spring Boot 앱 배포</span><span class="sxs-lookup"><span data-stu-id="6d284-103">Deploy a Spring Boot app using the Fabric8 Maven Plugin</span></span>

<span data-ttu-id="6d284-104">**[Fabric8]** 은 개발자들이 Linux 컨테이너에서 응용 프로그램을 만들 수 있게 지원하는 **[Kubernetes]** 기반 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-104">**[Fabric8]** is an open-source solution that is built on **[Kubernetes]**, which helps developers create applications in Linux containers.</span></span>

<span data-ttu-id="6d284-105">이 자습서에서는 Maven용 Fabric8 플러그인을 사용하여 [AKS(Azure Container Service)]에서 애플리케이션을 개발하고 Linux 호스트에 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-105">This tutorial walks you through using the Fabric8 plugin for Maven to develop to deploy an application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d284-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6d284-106">Prerequisites</span></span>

<span data-ttu-id="6d284-107">이 자습서의 단계를 완료하려면 다음 필수 조건이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-107">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="6d284-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="6d284-109">[Azure CLI(명령줄 인터페이스)]</span><span class="sxs-lookup"><span data-stu-id="6d284-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="6d284-110">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="6d284-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="6d284-111">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d284-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="6d284-112">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="6d284-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="6d284-113">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="6d284-113">A [Git] client.</span></span>
* <span data-ttu-id="6d284-114">[Docker] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="6d284-114">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="6d284-115">이 자습서의 가상화 요구 사항으로 인해 가상 머신에는 이 문서의 단계를 따를 수 없습니다. 따라서 가상화 기능이 사용하도록 설정된 물리적 컴퓨터를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-115">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="6d284-116">Spring Boot on Docker 시작 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="6d284-116">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="6d284-117">다음 단계에서는 Spring Boot 웹 애플리케이션을 빌드하고 로컬로 테스트하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-117">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="6d284-118">명령 프롬프트를 열고 애플리케이션을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-118">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```shell
   md /home/GenaSoto/SpringBoot
   cd /home/GenaSoto/SpringBoot
   ```
   <span data-ttu-id="6d284-119">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="6d284-119">-- or --</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```

1. <span data-ttu-id="6d284-120">[Spring Boot on Docker 시작] 샘플 프로젝트를 디렉터리에 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-120">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="6d284-121">디렉터리를 완료된 프로젝트로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="6d284-121">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```
   <span data-ttu-id="6d284-122">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="6d284-122">-- or --</span></span>
   ```shell
   cd gs-spring-boot-docker\complete
   ```

1. <span data-ttu-id="6d284-123">Maven을 사용하여 샘플 앱을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-123">Use Maven to build and run the sample app.</span></span>
   ```shell
   mvn clean package spring-boot:run
   ```

1. <span data-ttu-id="6d284-124">http://localhost:8080으로 이동하거나 `curl` 명령을 사용하여 웹앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-124">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="6d284-125">**Hello Docker World**라는 메시지가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-125">You should see a **Hello Docker World** message displayed.</span></span>

   ![샘플 응용 프로그램을 로컬로 찾아보기][SB01]


## <a name="install-the-kubernetes-command-line-interface-and-create-an-azure-resource-group-using-the-azure-cli"></a><span data-ttu-id="6d284-127">Kubernetes 명령줄 인터페이스를 설치하고 Azure CLI를 사용하여 Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6d284-127">Install the Kubernetes command-line interface and create an Azure resource group using the Azure CLI</span></span>

1. <span data-ttu-id="6d284-128">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-128">Open a command prompt.</span></span>

1. <span data-ttu-id="6d284-129">다음 명령을 입력하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-129">Type the following command to log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="6d284-130">지시에 따라 로그인 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-130">Follow the instructions to complete the login process</span></span>

   <span data-ttu-id="6d284-131">Azure CLI가 다음 예제처럼 계정 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-131">The Azure CLI will display a list of your accounts; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "00000000-0000-0000-0000-000000000000",
       "isDefault": false,
       "name": "Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "00000000-0000-0000-0000-000000000000",
       "user": {
         "name": "Gena.Soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```

1. <span data-ttu-id="6d284-132">아직 Kubernetes 명령줄 인터페이스(`kubectl`)를 설치하지 않은 경우 다음 예제처럼 Azure CLI를 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-132">If you do not already have the Kubernetes command-line interface (`kubectl`) installed, you can install using the Azure CLI; for example:</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="6d284-133">Linux 사용자는 이 명령 앞에 `sudo`를 붙여야 할 수 있습니다. 그러면 Kubernetes CLI가 `/usr/local/bin`에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-133">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   >
   > <span data-ttu-id="6d284-134">이미 `kubectl`을 설치하였고 `kubectl` 버전이 너무 오래되었으면 이 문서의 뒷부분에 등장하는 절차를 완료하려 할 때 다음 예제와 유사한 오류 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-134">If you already have `kubectl`) installed and your version of `kubectl` is too old, you may see an error message similar to the following example when you attempt to complete the steps listed later in this article:</span></span>
   >
   > ```
   > error: group map[autoscaling:0x0000000000 batch:0x0000000000 certificates.k8s.io
   > :0x0000000000 extensions:0x0000000000 storage.k8s.io:0x0000000000 apps:0x0000000
   > 000 authentication.k8s.io:0x0000000000 policy:0x0000000000 rbac.authorization.k8
   > s.io:0x0000000000 federation:0x0000000000 authorization.k8s.io:0x0000000000 comp
   > onentconfig:0x0000000000] is already registered
   > ```
   >
   > <span data-ttu-id="6d284-135">이 경우 `kubectl`을 다시 설치하여 버전을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-135">If this happens, you will need to reinstall `kubectl` to update your version.</span></span>
   >

1. <span data-ttu-id="6d284-136">다음 예제처럼 이 문서에서 사용할 Azure 리소스에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-136">Create a resource group for the Azure resources that you will use in this tutorial; for example:</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=westeurope
   ```
   <span data-ttu-id="6d284-137">위치:</span><span class="sxs-lookup"><span data-stu-id="6d284-137">Where:</span></span>  
      * <span data-ttu-id="6d284-138">*wingtiptoys-kubernetes*는 리소스 그룹의 고유한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-138">*wingtiptoys-kubernetes* is a unique name for your resource group</span></span>  
      * <span data-ttu-id="6d284-139">*westeurope*은 응용 프로그램의 적합한 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-139">*westeurope* is an appropriate geographic location for your application</span></span>  

   <span data-ttu-id="6d284-140">Azure CLI가 다음 에제처럼 리소스 그룹 만들기 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-140">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes",
     "location": "westeurope",
     "managedBy": null,
     "name": "wingtiptoys-kubernetes",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```


## <a name="create-a-kubernetes-cluster-using-the-azure-cli"></a><span data-ttu-id="6d284-141">Azure CLI를 사용하여 Kubernetes 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="6d284-141">Create a Kubernetes cluster using the Azure CLI</span></span>

1. <span data-ttu-id="6d284-142">다음 예제처럼 새 리소스 그룹에서 Kubernetes 클러스터를 만듭니다. </span><span class="sxs-lookup"><span data-stu-id="6d284-142">Create a Kubernetes cluster in your new resource group; for example:</span></span>  
   ```azurecli 
   az acs create --orchestrator-type kubernetes --resource-group wingtiptoys-kubernetes --name wingtiptoys-cluster --generate-ssh-keys --dns-prefix=wingtiptoys
   ```
   <span data-ttu-id="6d284-143">위치:</span><span class="sxs-lookup"><span data-stu-id="6d284-143">Where:</span></span>  
      * <span data-ttu-id="6d284-144">*wingtiptoys kubernetes*는 이 문서의 앞부분에 나온 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-144">*wingtiptoys-kubernetes* is the name of your resource group from earlier in this article</span></span>  
      * <span data-ttu-id="6d284-145">*wingtiptoys-cluster*는 Kubernetes클러스터의 고유한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-145">*wingtiptoys-cluster* is a unique name for your Kubernetes cluster</span></span>
      * <span data-ttu-id="6d284-146">*wingtiptoys*는 응용 프로그램의 고유한 DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-146">*wingtiptoys* is a unique name DNS name for your application</span></span>

   <span data-ttu-id="6d284-147">Azure CLI가 다음 예제처럼 클러스터 만들기 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-147">The Azure CLI will display the results of your cluster creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.Resources/deployments/azurecli0000000000.00000000000",
     "name": "azurecli0000000000.00000000000",
     "properties": {
       "correlationId": "00000000-0000-0000-0000-000000000000",
       "debugSetting": null,
       "dependencies": [],
       "mode": "Incremental",
       "outputs": {
         "masterFQDN": {
           "type": "String",
           "value": "wingtiptoysmgmt.westeurope.cloudapp.azure.com"
         },
         "sshMaster0": {
           "type": "String",
           "value": "ssh azureuser@wingtiptoysmgmt.westeurope.cloudapp.azure.com -A -p 22"
         }
       },
       "parameters": {
         "clientSecret": {
           "type": "SecureString"
         }
       },
       "parametersLink": null,
       "providers": [
         {
           "id": null,
           "namespace": "Microsoft.ContainerService",
           "registrationState": null,
           "resourceTypes": [
             {
               "aliases": null,
               "apiVersions": null,
               "locations": [
                 "westeurope"
               ],
               "properties": null,
               "resourceType": "containerServices"
             }
           ]
         }
       ],
       "provisioningState": "Succeeded",
       "template": null,
       "templateLink": null,
       "timestamp": "2017-09-15T01:00:00.000000+00:00"
     },
     "resourceGroup": "wingtiptoys-kubernetes"
   }
   ```

1. <span data-ttu-id="6d284-148">다음 예제처럼 새 Kubernetes 클러스터에 대한 자격 증명을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-148">Download your credentials for your new Kubernetes cluster; for example:</span></span>  
   ```azurecli 
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes --name wingtiptoys-cluster
   ```

1. <span data-ttu-id="6d284-149">다음 명령을 사용하여 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-149">Verify your connection with the following command:</span></span>
   ```shell 
   kubectl get nodes
   ```

   <span data-ttu-id="6d284-150">다음 예제와 유사한 노드 및 상태 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-150">You should see a list of nodes and statuses like the following example:</span></span>

   ```shell
   NAME                    STATUS                     AGE       VERSION
   k8s-agent-00000000-0    Ready                      5h        v1.6.6
   k8s-agent-00000000-1    Ready                      5h        v1.6.6
   k8s-agent-00000000-2    Ready                      5h        v1.6.6
   k8s-master-00000000-0   Ready,SchedulingDisabled   5h        v1.6.6
   ```


## <a name="create-a-private-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="6d284-151">Azure CLI를 사용하여 개인 Azure Container Registry 만들기</span><span class="sxs-lookup"><span data-stu-id="6d284-151">Create a private Azure container registry using the Azure CLI</span></span>

1. <span data-ttu-id="6d284-152">다음 예제처럼 리소스 그룹에서 Docker 이미지를 호스팅할 개인 Azure Container Registry를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-152">Create a private Azure container registry in your resource group to host your Docker image; for example:</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes --location westeurope --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="6d284-153">위치:</span><span class="sxs-lookup"><span data-stu-id="6d284-153">Where:</span></span>

   | <span data-ttu-id="6d284-154">매개 변수</span><span class="sxs-lookup"><span data-stu-id="6d284-154">Parameter</span></span> | <span data-ttu-id="6d284-155">설명</span><span class="sxs-lookup"><span data-stu-id="6d284-155">Description</span></span> |
   |---|---|
   | `wingtiptoys-kubernetes` | <span data-ttu-id="6d284-156">이 문서의 앞부분에 나온 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-156">Specifies the name of your resource group from earlier in this article.</span></span> |
   | `wingtiptoysregistry` | <span data-ttu-id="6d284-157">개인 레지스트리에 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-157">Specifies a unique name for your private registry.</span></span> |
   | `westeurope` | <span data-ttu-id="6d284-158">애플리케이션의 적합한 지리적 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-158">Specifies an appropriate geographic location for your application.</span></span> |

   <span data-ttu-id="6d284-159">Azure CLI가 다음 예제처럼 레지스트리 만들기 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-159">The Azure CLI will display the results of your registry creation; for example:</span></span>  

   ```json
   {
     "adminUserEnabled": true,
     "creationDate": "2017-09-15T01:00:00.000000+00:00",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.ContainerRegistry/registries/wingtiptoysregistry",
     "location": "westeurope",
     "loginServer": "wingtiptoysregistry.azurecr.io",
     "name": "wingtiptoysregistry",
     "provisioningState": "Succeeded",
     "resourceGroup": "wingtiptoys-kubernetes",
     "sku": {
       "name": "Basic",
       "tier": "Basic"
     },
     "storageAccount": {
       "name": "wingtiptoysregistr000000"
     },
     "tags": {},
     "type": "Microsoft.ContainerRegistry/registries"
   }
   ```

2. <span data-ttu-id="6d284-160">Azure CLI에서 컨테이너 레지스트리에 대한 암호를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-160">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   <span data-ttu-id="6d284-161">Azure CLI가 다음 예제처럼 레지스트리의 암호를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-161">The Azure CLI will display the password for your registry; for example:</span></span>  

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

3. <span data-ttu-id="6d284-162">Maven 설치에 대한 구성 디렉터리(default ~/.m2/ 또는 C:\Users\username\.m2)로 이동한 후 텍스트 편집기를 사용하여 *settings.xml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-162">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

4. <span data-ttu-id="6d284-163">Azure Container Registry URL, 사용자 이름 및 암호를 *settings.xml* 파일의 새 `<server>` 컬렉션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-163">Add your Azure Container Registry URL, username and password to a new `<server>` collection in the *settings.xml* file.</span></span>
   <span data-ttu-id="6d284-164">`id` 및 `username`은 레지스트리의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-164">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="6d284-165">이전 명령의 `password` 값을 사용합니다(따옴표 제외).</span><span class="sxs-lookup"><span data-stu-id="6d284-165">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry.azurecr.io</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

5. <span data-ttu-id="6d284-166">Spring Boot 응용 프로그램에 대해 완료된 프로젝트 디렉터리로 이동하고(예: "*C:\SpringBoot\gs-spring-boot-docker\complete*" 또는 "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*") 텍스트 편집기를 사용하여 *pom.xml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-166">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

6. <span data-ttu-id="6d284-167">*pom.xml* 파일의 `<properties>` 컬렉션을 Azure Container Registry의 로그인 서버 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-167">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

7. <span data-ttu-id="6d284-168">*pom.xml* 파일의 `<plugins>` 컬렉션을 업데이트하여 `<plugin>`에 Azure Container Registry의 로그인 서버 주소 및 레지스트리 이름이 포함되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-168">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
     <groupId>com.spotify</groupId>
     <artifactId>dockerfile-maven-plugin</artifactId>
     <version>1.3.4</version>
     <configuration>
       <repository>${docker.image.prefix}/${project.artifactId}</repository>
       <serverId>${docker.image.prefix}</serverId>
       <registryUrl>https://${docker.image.prefix}</registryUrl>
     </configuration>
   </plugin>
   ```

8. <span data-ttu-id="6d284-169">Spring Boot 응용 프로그램에 대한 완성된 프로젝트 디렉터리로 이동한 후 다음 Maven 명령을 실행하여 Docker 컨테이너를 빌드하고 레지스트리에 이미지를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-169">Navigate to the completed project directory for your Spring Boot application, and run the following Maven command to build the Docker container and push the image to your registry:</span></span>

   ```shell
   mvn package dockerfile:build -DpushImage
   ```

   <span data-ttu-id="6d284-170">Maven이 빌드의 결과를 다음 예제처럼 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-170">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 38.113 s
   [INFO] Finished at: 2017-09-15T02:00:00-07:00
   [INFO] Final Memory: 47M/338M
   [INFO] ----------------------------------------------------
   ```


## <a name="configure-your-spring-boot-app-to-use-the-fabric8-maven-plugin"></a><span data-ttu-id="6d284-171">Fabric8 Maven 플러그인을 사용하도록 Spring Boot 앱 구성</span><span class="sxs-lookup"><span data-stu-id="6d284-171">Configure your Spring Boot app to use the Fabric8 Maven plugin</span></span>

1. <span data-ttu-id="6d284-172">Spring Boot 응용 프로그램에 대해 완료된 프로젝트 디렉터리로 이동하고(예: "*C:\SpringBoot\gs-spring-boot-docker\complete*" 또는 "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*") 텍스트 편집기를 사용하여 *pom.xml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-172">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="6d284-173">*pom.xml* 파일의 `<plugins>` 컬렉션을 업데이트하여 Fabric8 Maven 플러그인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-173">Update the `<plugins>` collection in the *pom.xml* file to add the Fabric8 Maven plugin:</span></span>

   ```xml
   <plugin>
     <groupId>io.fabric8</groupId>
     <artifactId>fabric8-maven-plugin</artifactId>
     <version>3.5.30</version>
     <configuration>
       <ignoreServices>false</ignoreServices>
       <registry>${docker.image.prefix}</registry>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="6d284-174">Spring Boot 응용 프로그램의 기본 원본 디렉터리로 이동하고(예: "*C:\SpringBoot\gs-spring-boot-docker\complete\src\main*" 또는 "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*") 이름이 "*fabric8*"인 새 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-174">Navigate to the main source directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete\src\main*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*"), and create a new folder named "*fabric8*".</span></span>

1. <span data-ttu-id="6d284-175">새 *fabric8* 폴더에 3개의 YAML 조각 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-175">Create three YAML fragment files in the new *fabric8* folder:</span></span>

   <span data-ttu-id="6d284-176">a.</span><span class="sxs-lookup"><span data-stu-id="6d284-176">a.</span></span> <span data-ttu-id="6d284-177">다음과 같은 콘텐츠가 포함된 **deployment.yml** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-177">Create a file named **deployment.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: extensions/v1beta1
      kind: Deployment
      metadata:
        name: ${project.artifactId}
        labels:
          run: gs-spring-boot-docker
      spec:
        replicas: 1
        selector:
          matchLabels:
            run: gs-spring-boot-docker
        strategy:
          rollingUpdate:
            maxSurge: 1
            maxUnavailable: 1
          type: RollingUpdate
        template:
          metadata:
            labels:
              run: gs-spring-boot-docker
          spec:
            containers:
            - image: ${docker.image.prefix}/${project.artifactId}:latest
              name: gs-spring-boot-docker
              imagePullPolicy: Always
              ports:
              - containerPort: 8080
            imagePullSecrets:
              - name: mysecrets
      ```

   <span data-ttu-id="6d284-178">b.</span><span class="sxs-lookup"><span data-stu-id="6d284-178">b.</span></span> <span data-ttu-id="6d284-179">다음과 같은 콘텐츠가 포함된 **secrets.yml** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-179">Create a file named **secrets.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: v1
      kind: Secret
      metadata:
        name: mysecrets
        namespace: default
        annotations:
          maven.fabric8.io/dockerServerId:  ${docker.image.prefix}
      type: kubernetes.io/dockercfg
      ```

   <span data-ttu-id="6d284-180">다.</span><span class="sxs-lookup"><span data-stu-id="6d284-180">c.</span></span> <span data-ttu-id="6d284-181">다음과 같은 콘텐츠가 포함된 **service.yml** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-181">Create a file named **service.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: v1
      kind: Service
      metadata:
        name: ${project.artifactId}
        labels:
          expose: "true"
      spec:
        ports:
        - port: 80
          targetPort: 8080
        type: LoadBalancer
      ```

1. <span data-ttu-id="6d284-182">Kubernetes 리소스 목록 파일을 빌드하는 다음 Maven 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-182">Run the following Maven command to build the Kubernetes resource list file:</span></span>

   ```shell
   mvn fabric8:resource
   ```

   <span data-ttu-id="6d284-183">이 명령은 *src/main/fabric8* 폴더 아래의 모든 Kubernetes 리소스 yaml 파일을 Kubernetes 리소스 목록이 포함된 한 YAML 파일로 병합합니다. 이를 Kubernetes 클러스터에 직접 적용하거나 Helm 차트로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-183">This command merges all Kubernetes resource yaml files under the *src/main/fabric8* folder to a YAML file that contains a Kubernetes resource list, which can be applied to Kubernetes cluster directly or export to a helm chart.</span></span>

   <span data-ttu-id="6d284-184">Maven이 빌드의 결과를 다음 예제처럼 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-184">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 16.744 s
   [INFO] Finished at: 2017-09-15T02:35:00-07:00
   [INFO] Final Memory: 30M/290M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="6d284-185">다음 Maven 명령을 실행하여 리소스 목록 파일을 Kubernetes 클러스터에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-185">Run the following Maven command to apply the resource list file to your Kubernetes cluster:</span></span>

   ```shell
   mvn fabric8:apply
   ```

   <span data-ttu-id="6d284-186">Maven이 빌드의 결과를 다음 예제처럼 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-186">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 14.814 s
   [INFO] Finished at: 2017-09-15T02:41:00-07:00
   [INFO] Final Memory: 35M/288M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="6d284-187">앱이 클러스터에 배포되면 다음 예제처럼 `kubectl` 응용 프로그램을 사용하여 외부 IP 주소를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-187">Once the app is deployed to the cluster, query the external IP address using the `kubectl` application; for example:</span></span>
   ```shell
   kubectl get svc -w
   ```

   <span data-ttu-id="6d284-188">`kubectl`에 다음 예제처럼 내부 및 외부 IP 주소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-188">`kubectl` will display your internal and external IP addresses; for example:</span></span>

   ```shell
   NAME                    CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
   kubernetes              10.0.0.1     <none>        443/TCP        19h
   gs-spring-boot-docker   10.0.242.8   13.65.196.3   80:31215/TCP   3m
   ```

   <span data-ttu-id="6d284-189">외부 IP 주소를 사용하여 웹 브라우저에 응용 프로그램을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-189">You can use the external IP address to open your application in a web browser.</span></span>

   ![샘플 응용 프로그램을 외부로 찾아보기][SB02]

## <a name="delete-your-kubernetes-cluster"></a><span data-ttu-id="6d284-191">Kubernetes 클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="6d284-191">Delete your Kubernetes cluster</span></span>

<span data-ttu-id="6d284-192">Kubernetes 클러스터가 더 이상 필요하지 않게 되면 `az group delete` 명령을 사용하여 리소스 그룹을 제거할 수 있습니다. 그러면 모든 관련 리소스가 제거되며 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d284-192">When your Kubernetes cluster is no longer needed, you can use the `az group delete` command to remove the resource group, which will remove all of its related resources; for example:</span></span>

   ```azurecli
   az group delete --name wingtiptoys-kubernetes --yes --no-wait
   ```

## <a name="next-steps"></a><span data-ttu-id="6d284-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6d284-193">Next steps</span></span>

<span data-ttu-id="6d284-194">Azure에서 Spring Boot 애플리케이션을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d284-194">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="6d284-195">Azure App Service에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="6d284-195">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="6d284-196">Azure Container Service에서 Linux에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="6d284-196">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)
* [<span data-ttu-id="6d284-197">Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="6d284-197">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="6d284-198">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d284-198">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="6d284-199">Spring Boot on Docker 샘플 프로젝트에 대한 자세한 정보는 [Spring Boot on Docker 시작]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d284-199">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="6d284-200">자체 Spring Boot 애플리케이션을 시작하는 데 도움이 필요하면 <https://start.spring.io/>에서 **Spring Initializr**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d284-200">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at <https://start.spring.io/>.</span></span>

<span data-ttu-id="6d284-201">간단한 Spring Boot 애플리케이션을 만들기 시작하는 방법에 대한 자세한 내용은 <https://start.spring.io/>에서 Spring Initializr를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d284-201">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at <https://start.spring.io/>.</span></span>

<span data-ttu-id="6d284-202">Azure와 함께 사용자 지정 Docker 이미지를 사용하는 방법에 대한 추가 예제를 보려면 [Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d284-202">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[AKS(Azure Container Service)]: https://azure.microsoft.com/services/container-service/
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Java 개발자용 Azure]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Azure Web App on Linux에 대한 사용자 지정 Docker 이미지 사용]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Fabric8]: https://fabric8.io/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
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

[SB01]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB02.png
