---
title: Docker 및 Azure를 사용하여 클라우드로 MicroProfile 앱 배포
description: Docker 및 Azure Container 인스턴스를 사용하여 클라우드로 MicroProfile 앱을 배포하는 방법에 대해 알아봅니다.
services: container-instances;container-retistry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 22870b7ba32f115e7270c63d1bf42cbfc6531d7e
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338787"
---
# <a name="deploy-a-microprofile-application-to-the-cloud-with-docker-and-azure"></a><span data-ttu-id="1e1b7-103">Docker 및 Azure를 사용하여 클라우드로 MicroProfile 애플리케이션 배포</span><span class="sxs-lookup"><span data-stu-id="1e1b7-103">Deploy a MicroProfile application to the cloud with Docker and Azure</span></span>

<span data-ttu-id="1e1b7-104">이 문서에서는 [MicroProfile.io] 애플리케이션을 Docker 컨테이너에 압축하고 Azure 컨테이너 인스턴스에서 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-104">This article demonstrates how to pack a [MicroProfile.io] application in a Docker container and run it on Azure Container Instances.</span></span>

> [!NOTE]
>
> <span data-ttu-id="1e1b7-105">Docker 컨테이너 이미지가 자체 실행 가능(즉, 런타임을 포함)한 경우, 이 절차는MicroProfile.io의 모든 구현을 사용하여 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-105">This procedure works with any implementation of MicroProfile.io as long the Docker container image is self-executable (i.e. includes the runtime).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e1b7-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1e1b7-106">Prerequisites</span></span>

<span data-ttu-id="1e1b7-107">이 자습서의 단계를 완료하려면 다음 필수 조건이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-107">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="1e1b7-108">Azure 구독; Azure 구독이 아직 없는 경우 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-108">An Azure subscription; if you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="1e1b7-109">[Azure CLI(명령줄 인터페이스)]</span><span class="sxs-lookup"><span data-stu-id="1e1b7-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="1e1b7-110">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="1e1b7-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="1e1b7-111">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="1e1b7-112">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="1e1b7-112">Apache's [Maven] build tool (version 3+).</span></span>
* <span data-ttu-id="1e1b7-113">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="1e1b7-113">A [Git] client.</span></span>

## <a name="microprofile-hello-azure-sample"></a><span data-ttu-id="1e1b7-114">MicroProfile Hello Azure 예제</span><span class="sxs-lookup"><span data-stu-id="1e1b7-114">MicroProfile Hello Azure sample</span></span>

<span data-ttu-id="1e1b7-115">이 문서에서는 [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-115">For this article, we will use the [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) sample:</span></span>

### <a name="clone-build-and-run-locally"></a><span data-ttu-id="1e1b7-116">복제, 빌드 및 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="1e1b7-116">Clone, build, and run locally</span></span>

```bash
$ git clone https://github.com/Azure-Samples/microprofile-hello-azure.git
$ mvn clean package
...
[INFO] BUILD SUCCESS
...
$ mvn payara-micro:start
...
[2018-07-30T13:34:51.553-0700] [] [INFO] [] [PayaraMicro] [tid: _ThreadID=1 _ThreadName=main] [timeMillis: 1532982891553] [levelValue: 800] Payara Micro  5.182 #badassmicrofish (build 303) ready in 10,304 (ms)
...
```

<span data-ttu-id="1e1b7-117">`curl`을 호출하거나 [브라우저](http://localhost:8080/api/hello)를 통해 방문하여 응용 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-117">You can test the application by calling `curl` or visiting through a [browser](http://localhost:8080/api/hello):</span></span>

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-to-azure"></a><span data-ttu-id="1e1b7-118">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="1e1b7-118">Deploy to Azure</span></span>

<span data-ttu-id="1e1b7-119">이제 [Azure Container Instances] 및 [Azure Container Registry] 서비스를 사용하여 클라우드에 이 애플리케이션을 배포해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-119">Now let's bring this application to the cloud using [Azure Container Instances] and [Azure Container Registry] services.</span></span>

### <a name="build-a-docker-image"></a><span data-ttu-id="1e1b7-120">Docker 이미지 빌드</span><span class="sxs-lookup"><span data-stu-id="1e1b7-120">Build a Docker image</span></span>

<span data-ttu-id="1e1b7-121">예제 프로젝트는 사용할 수 있는 Dockerfile을 이미 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-121">The sample project already provides a Dockerfile you can use.</span></span> <span data-ttu-id="1e1b7-122">Azure Container Registry 빌드 기능을 사용하여 클라우드에서 이미지를 빌드하므로 Docker가 설치되어 있지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-122">You don't need Docker installed though, as we will use Azure Container Registry Build feature to build the image in the cloud.</span></span>

<span data-ttu-id="1e1b7-123">이미지를 빌드하고 Azure에서 실행하도록 준비 하려면 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-123">To build the image and be ready to run on Azure, you will have to follow these steps:</span></span>

1. <span data-ttu-id="1e1b7-124">Azure CLI 설치 및 로그인</span><span class="sxs-lookup"><span data-stu-id="1e1b7-124">Install and log in with Azure CLI</span></span>
1. <span data-ttu-id="1e1b7-125">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="1e1b7-125">Create an Azure Resource Group</span></span>
1. <span data-ttu-id="1e1b7-126">ACR(Azure Container Registry) 만들기</span><span class="sxs-lookup"><span data-stu-id="1e1b7-126">Create an Azure Container Registry (ACR)</span></span>
1. <span data-ttu-id="1e1b7-127">Docker 이미지 빌드</span><span class="sxs-lookup"><span data-stu-id="1e1b7-127">Build the Docker image</span></span>
1. <span data-ttu-id="1e1b7-128">이전에 만든 ACR에 Docker 이미지 게시</span><span class="sxs-lookup"><span data-stu-id="1e1b7-128">Publish the Docker image to the ACR created before</span></span>
1. <span data-ttu-id="1e1b7-129">(선택 사항) 하나의 명령으로 빌드 및 ACR에 게시</span><span class="sxs-lookup"><span data-stu-id="1e1b7-129">(Optionally) Build and publish to ACR in one command</span></span>


#### <a name="set-up-azure-cli"></a><span data-ttu-id="1e1b7-130">Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="1e1b7-130">Set up Azure CLI</span></span>

<span data-ttu-id="1e1b7-131">Azure 구독, [Azure CLI 설치](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), 계정 인증을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-131">Make sure you have an Azure subscription, [Azure CLI installed](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), and that you are authenticated to your account:</span></span>

```bash
az login
```

#### <a name="create-a-resource-group"></a><span data-ttu-id="1e1b7-132">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="1e1b7-132">Create a Resource Group</span></span>

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-an-azure-container-registry-instance"></a><span data-ttu-id="1e1b7-133">Azure Container Registry 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="1e1b7-133">Create an Azure Container Registry instance</span></span>

<span data-ttu-id="1e1b7-134">이 명령은 기본 이름에 임의의 숫자를 사용하여 전역적으로 유일한 컨테이너 레지스트리를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-134">This command will create a globally unique (hopefully) container registry using a basic name with a random number.</span></span>

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a><span data-ttu-id="1e1b7-135">Docker 이미지 빌드</span><span class="sxs-lookup"><span data-stu-id="1e1b7-135">Build the Docker image</span></span>

<span data-ttu-id="1e1b7-136">Docker 자체를 사용하여 Docker 이미지를 로컬에서 쉽게 만들 수 있지만 몇 가지 이유로 인해 Docker를 클라우드에서 빌드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-136">While you can easily build the Docker image locally using Docker itself, you may want to consider building it in the Cloud for few reasons:</span></span>

1. <span data-ttu-id="1e1b7-137">Docker를 로컬로 설치할 필요 없음</span><span class="sxs-lookup"><span data-stu-id="1e1b7-137">No need to install Docker locally</span></span>
1. <span data-ttu-id="1e1b7-138">빌드가 다른 곳에서 발생하기 때문에 훨씬 빠릅니다(컨텍스트 업로드 시간 제외).</span><span class="sxs-lookup"><span data-stu-id="1e1b7-138">Much faster since build will happen elsewhere (except for context upload time)</span></span>
1. <span data-ttu-id="1e1b7-139">클라우드의 프로세스는 보다 빠른 인터넷에 액세스하므로 빠른 다운로드가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-139">Process in the Cloud has access to faster Internet, therefore faster downloads</span></span>
1. <span data-ttu-id="1e1b7-140">이미지가 컨테이너 레지스트리로 직접 이동</span><span class="sxs-lookup"><span data-stu-id="1e1b7-140">Image goes directly into the Container Registry</span></span>

<span data-ttu-id="1e1b7-141">이러한 이유 때문에 [Azure Container Registry 빌드] 기능을 사용하여 이미지를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-141">Because of these reasons, we will build the image using the [Azure Container Registry Build] feature:</span></span>

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-docker-image-from-azure-container-registry-acr-into-container-instances-aci"></a><span data-ttu-id="1e1b7-142">Azure Container Registry(ACR)의 Docker 이미지를 컨테이너 인스턴스(ACI)로 배포</span><span class="sxs-lookup"><span data-stu-id="1e1b7-142">Deploy Docker Image from Azure Container Registry (ACR) into Container Instances (ACI)</span></span>

<span data-ttu-id="1e1b7-143">ACR에서 이미지를 사용할 수 있게 되었으므로 ACI에서 컨테이너 인스턴스를 푸시하고 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-143">Now that the image is available on your ACR, let's push and instanciate a container instance on ACI.</span></span> <span data-ttu-id="1e1b7-144">하지만 먼저 ACR에 인증할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-144">But first, we need to make sure we can authenticate into the ACR:</span></span>

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a><span data-ttu-id="1e1b7-145">배포된 MicroProfile 애플리케이션 테스트</span><span class="sxs-lookup"><span data-stu-id="1e1b7-145">Test Your Deployed MicroProfile Application</span></span>

<span data-ttu-id="1e1b7-146">이제 애플리케이션이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-146">Your application should now be up and running.</span></span> <span data-ttu-id="1e1b7-147">명령줄 테스트하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-147">To test it from the command-line, try the following command:</span></span>

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

<span data-ttu-id="1e1b7-148">축하합니다!</span><span class="sxs-lookup"><span data-stu-id="1e1b7-148">Congratulations!</span></span> <span data-ttu-id="1e1b7-149">Microsoft Azure에 Docker 컨테이너로 MicroProfile 애플리케이션을 성공적으로 구축하고 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-149">You have successfuly built and deployed a MicroProfile application as a Docker container onto Microsoft Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e1b7-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e1b7-150">Next steps</span></span>

<span data-ttu-id="1e1b7-151">이 문서에서 설명하는 다양한 기술에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1e1b7-151">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* [<span data-ttu-id="1e1b7-152">Azure CLI에서 Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="1e1b7-152">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

<!-- URL List -->

[Azure Container Registry 빌드]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry