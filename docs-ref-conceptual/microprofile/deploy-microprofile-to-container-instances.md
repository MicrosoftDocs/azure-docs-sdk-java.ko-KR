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
ms.date: 07/30/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 336af51bbdf5d2f843c3868ebc2358e128daaeaa
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324329"
---
# <a name="deploy-a-microprofile-application-to-the-cloud-with-docker-and-azure"></a><span data-ttu-id="9321c-103">Docker 및 Azure를 사용하여 클라우드로 MicroProfile 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="9321c-103">Deploy a MicroProfile application to the cloud with Docker and Azure</span></span>

<span data-ttu-id="9321c-104">이 문서에서는 [MicroProfile.io] 응용 프로그램을 Docker 컨테이너에 압축하고 Azure 컨테이너 인스턴스에서 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-104">This article demonstrates how to pack a [MicroProfile.io] application in a Docker container and run it on Azure Container Instances.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9321c-105">Docker 컨테이너 이미지가 자체 실행 가능(즉, 런타임을 포함)한 경우, 이 절차는MicroProfile.io의 모든 구현을 사용하여 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-105">This procedure works with any implementation of MicroProfile.io as long the Docker container image is self-executable (i.e. includes the runtime).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9321c-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9321c-106">Prerequisites</span></span>

<span data-ttu-id="9321c-107">이 자습서의 단계를 완료하려면 다음 필수 조건이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-107">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="9321c-108">Azure 구독; Azure 구독이 아직 없는 경우 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-108">An Azure subscription; if you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="9321c-109">[Azure CLI(명령줄 인터페이스)]</span><span class="sxs-lookup"><span data-stu-id="9321c-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="9321c-110">최신 [JDK(Java Development Kit)], 버전 1.8 이상</span><span class="sxs-lookup"><span data-stu-id="9321c-110">An up-to-date [Java Development Kit (JDK)], version 1.8 or later.</span></span>
* <span data-ttu-id="9321c-111">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="9321c-111">Apache's [Maven] build tool (version 3+).</span></span>
* <span data-ttu-id="9321c-112">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="9321c-112">A [Git] client.</span></span>

## <a name="microprofile-hello-azure-sample"></a><span data-ttu-id="9321c-113">MicroProfile Hello Azure 예제</span><span class="sxs-lookup"><span data-stu-id="9321c-113">MicroProfile Hello Azure sample</span></span>

<span data-ttu-id="9321c-114">이 문서에서는 [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-114">For this article, we will use the [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) sample:</span></span>

### <a name="clone-build-and-run-locally"></a><span data-ttu-id="9321c-115">복제, 빌드 및 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="9321c-115">Clone, build, and run locally</span></span>

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

<span data-ttu-id="9321c-116">`curl`을 호출하거나 [브라우저](http://localhost:8080/api/hello)를 통해 방문하여 응용 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-116">You can test the application by calling `curl` or visiting through a [browser](http://localhost:8080/api/hello):</span></span>

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-to-azure"></a><span data-ttu-id="9321c-117">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="9321c-117">Deploy to Azure</span></span>

<span data-ttu-id="9321c-118">이제 [Azure Container Instances] 및 [Azure Container Registry] 서비스를 사용하여 클라우드에 이 응용 프로그램을 배포해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-118">Now let's bring this application to the cloud using [Azure Container Instances] and [Azure Container Registry] services.</span></span>

### <a name="build-a-docker-image"></a><span data-ttu-id="9321c-119">Docker 이미지 빌드</span><span class="sxs-lookup"><span data-stu-id="9321c-119">Build a Docker image</span></span>

<span data-ttu-id="9321c-120">예제 프로젝트는 사용할 수 있는 Dockerfile을 이미 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-120">The sample project already provides a Dockerfile you can use.</span></span> <span data-ttu-id="9321c-121">Azure Container Registry 빌드 기능을 사용하여 클라우드에서 이미지를 빌드하므로 Docker가 설치되어 있지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-121">You don't need Docker installed though, as we will use Azure Container Registry Build feature to build the image in the cloud.</span></span>

<span data-ttu-id="9321c-122">이미지를 빌드하고 Azure에서 실행하도록 준비 하려면 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-122">To build the image and be ready to run on Azure, you will have to follow these steps:</span></span>

1. <span data-ttu-id="9321c-123">Azure CLI 설치 및 로그인</span><span class="sxs-lookup"><span data-stu-id="9321c-123">Install and log in with Azure CLI</span></span>
1. <span data-ttu-id="9321c-124">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="9321c-124">Create an Azure Resource Group</span></span>
1. <span data-ttu-id="9321c-125">ACR(Azure Container Registry) 만들기</span><span class="sxs-lookup"><span data-stu-id="9321c-125">Create an Azure Container Registry (ACR)</span></span>
1. <span data-ttu-id="9321c-126">Docker 이미지 빌드</span><span class="sxs-lookup"><span data-stu-id="9321c-126">Build the Docker image</span></span>
1. <span data-ttu-id="9321c-127">이전에 만든 ACR에 Docker 이미지 게시</span><span class="sxs-lookup"><span data-stu-id="9321c-127">Publish the Docker image to the ACR created before</span></span>
1. <span data-ttu-id="9321c-128">(선택 사항) 하나의 명령으로 빌드 및 ACR에 게시</span><span class="sxs-lookup"><span data-stu-id="9321c-128">(Optionally) Build and publish to ACR in one command</span></span>


#### <a name="set-up-azure-cli"></a><span data-ttu-id="9321c-129">Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="9321c-129">Set up Azure CLI</span></span>

<span data-ttu-id="9321c-130">Azure 구독, [Azure CLI 설치](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), 계정 인증을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-130">Make sure you have an Azure subscription, [Azure CLI installed](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), and that you are authenticated to your account:</span></span>

```bash
az login
```

#### <a name="create-a-resource-group"></a><span data-ttu-id="9321c-131">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="9321c-131">Create a Resource Group</span></span>

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-an-azure-container-registry-instance"></a><span data-ttu-id="9321c-132">Azure Container Registry 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="9321c-132">Create an Azure Container Registry instance</span></span>

<span data-ttu-id="9321c-133">이 명령은 기본 이름에 임의의 숫자를 사용하여 전역적으로 유일한 컨테이너 레지스트리를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-133">This command will create a globally unique (hopefully) container registry using a basic name with a random number.</span></span>

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a><span data-ttu-id="9321c-134">Docker 이미지 빌드</span><span class="sxs-lookup"><span data-stu-id="9321c-134">Build the Docker image</span></span>

<span data-ttu-id="9321c-135">Docker 자체를 사용하여 Docker 이미지를 로컬에서 쉽게 만들 수 있지만 몇 가지 이유로 인해 Docker를 클라우드에서 빌드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-135">While you can easily build the Docker image locally using Docker itself, you may want to consider building it in the Cloud for few reasons:</span></span>

1. <span data-ttu-id="9321c-136">Docker를 로컬로 설치할 필요 없음</span><span class="sxs-lookup"><span data-stu-id="9321c-136">No need to install Docker locally</span></span>
1. <span data-ttu-id="9321c-137">빌드가 다른 곳에서 발생하기 때문에 훨씬 빠릅니다(컨텍스트 업로드 시간 제외).</span><span class="sxs-lookup"><span data-stu-id="9321c-137">Much faster since build will happen elsewhere (except for context upload time)</span></span>
1. <span data-ttu-id="9321c-138">클라우드의 프로세스는 보다 빠른 인터넷에 액세스하므로 빠른 다운로드가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-138">Process in the Cloud has access to faster Internet, therefore faster downloads</span></span>
1. <span data-ttu-id="9321c-139">이미지가 컨테이너 레지스트리로 직접 이동</span><span class="sxs-lookup"><span data-stu-id="9321c-139">Image goes directly into the Container Registry</span></span>

<span data-ttu-id="9321c-140">이러한 이유 때문에 [Azure Container Registry 빌드] 기능을 사용하여 이미지를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-140">Because of these reasons, we will build the image using the [Azure Container Registry Build] feature:</span></span>

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-docker-image-from-azure-container-registry-acr-into-container-instances-aci"></a><span data-ttu-id="9321c-141">Azure Container Registry(ACR)의 Docker 이미지를 컨테이너 인스턴스(ACI)로 배포</span><span class="sxs-lookup"><span data-stu-id="9321c-141">Deploy Docker Image from Azure Container Registry (ACR) into Container Instances (ACI)</span></span>

<span data-ttu-id="9321c-142">ACR에서 이미지를 사용할 수 있게 되었으므로 ACI에서 컨테이너 인스턴스를 푸시하고 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-142">Now that the image is available on your ACR, let's push and instanciate a container instance on ACI.</span></span> <span data-ttu-id="9321c-143">하지만 먼저 ACR에 인증할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-143">But first, we need to make sure we can authenticate into the ACR:</span></span>

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a><span data-ttu-id="9321c-144">배포된 MicroProfile 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="9321c-144">Test Your Deployed MicroProfile Application</span></span>

<span data-ttu-id="9321c-145">이제 응용 프로그램이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-145">Your application should now be up and running.</span></span> <span data-ttu-id="9321c-146">명령줄 테스트하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-146">To test it from the command-line, try the following command:</span></span>

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

<span data-ttu-id="9321c-147">축하합니다!</span><span class="sxs-lookup"><span data-stu-id="9321c-147">Congratulations!</span></span> <span data-ttu-id="9321c-148">Microsoft Azure에 Docker 컨테이너로 MicroProfile 응용 프로그램을 성공적으로 구축하고 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="9321c-148">You have successfuly built and deployed a MicroProfile application as a Docker container onto Microsoft Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9321c-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9321c-149">Next steps</span></span>

<span data-ttu-id="9321c-150">이 문서에서 설명하는 다양한 기술에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9321c-150">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* [<span data-ttu-id="9321c-151">Azure CLI에서 Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="9321c-151">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

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
[JDK(Java Development Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[Java Development Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry