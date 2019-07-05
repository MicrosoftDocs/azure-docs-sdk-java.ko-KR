---
title: Docker 및 Azure를 사용하여 클라우드로 MicroProfile 앱 배포
description: Docker 및 Azure Container 인스턴스를 사용하여 클라우드로 MicroProfile 앱을 배포하는 방법에 대해 알아봅니다.
services: container-instances;container-registry
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
ms.openlocfilehash: 6ba12bb183969103676fa988199603df6cf36bba
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533608"
---
# <a name="deploy-a-microprofile-app-to-the-cloud-by-using-docker-and-azure"></a><span data-ttu-id="1afe2-103">Docker 및 Azure를 사용하여 클라우드로 MicroProfile 앱 배포</span><span class="sxs-lookup"><span data-stu-id="1afe2-103">Deploy a MicroProfile app to the cloud by using Docker and Azure</span></span>

<span data-ttu-id="1afe2-104">이 문서에서는 [MicroProfile.io] 애플리케이션을 Docker 컨테이너에 압축하고 Azure 컨테이너 인스턴스에서 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-104">This article demonstrates how to pack a [MicroProfile.io] application in a Docker container and run it on Azure Container Instances.</span></span>

> [!NOTE]
> <span data-ttu-id="1afe2-105">Docker 컨테이너 이미지가 자체 실행 가능(즉, 이미지가 런타임을 포함)한 경우, 이 절차는 MicroProfile.io의 모든 구현을 사용하여 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-105">This procedure works with any implementation of MicroProfile.io, as long as the Docker container image is self-executable (that is, the image includes the runtime).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1afe2-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1afe2-106">Prerequisites</span></span>

<span data-ttu-id="1afe2-107">이 자습서를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-107">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="1afe2-108">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="1afe2-108">An Azure subscription.</span></span> <span data-ttu-id="1afe2-109">Azure 구독이 아직 없는 경우 [체험판 Azure 계정]에서 무료 평가판에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-109">If you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="1afe2-110">[Azure CLI]가 설치되어 있음</span><span class="sxs-lookup"><span data-stu-id="1afe2-110">The [Azure CLI], installed.</span></span>
* <span data-ttu-id="1afe2-111">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="1afe2-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="1afe2-112">Azure에서 개발하는 데 사용할 수 있는 JDK에 대한 자세한 내용은 [Azure 및 Azure Stack에 대한 Java 장기 지원](https://aka.ms/azure-jdks)을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-112">For more information about the JDKs that are available to use when you develop on Azure, see [Java long-term support for Azure and Azure Stack](https://aka.ms/azure-jdks).</span></span>
* <span data-ttu-id="1afe2-113">[Apache Maven] 빌드 도구(버전 3 이상).</span><span class="sxs-lookup"><span data-stu-id="1afe2-113">The [Apache Maven] build tool (version 3 or later).</span></span>
* <span data-ttu-id="1afe2-114">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="1afe2-114">A [Git] client.</span></span>

## <a name="microprofile-hello-azure-sample"></a><span data-ttu-id="1afe2-115">MicroProfile Hello Azure 예제</span><span class="sxs-lookup"><span data-stu-id="1afe2-115">MicroProfile Hello Azure sample</span></span>

<span data-ttu-id="1afe2-116">이 문서에서는 [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-116">In this article, you use the [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) sample.</span></span> <span data-ttu-id="1afe2-117">다음 명령을 사용하여 복제, 빌드 및 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-117">Clone, build, and run it locally by using the following commands:</span></span>

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

<span data-ttu-id="1afe2-118">`curl`을 호출하거나 [브라우저](http://localhost:8080/api/hello)를 사용하여 애플리케이션을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-118">You can test the application by calling `curl` or by using a [browser](http://localhost:8080/api/hello):</span></span>

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="1afe2-119">Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="1afe2-119">Deploy the app to Azure</span></span>

<span data-ttu-id="1afe2-120">이제 [Azure Container Instances] 및 [Azure Container Registry] 서비스를 사용하여 Azure에 이 애플리케이션을 배포해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-120">Now bring this application to Azure by using the [Azure Container Instances] and [Azure Container Registry] services.</span></span>

### <a name="build-a-docker-image"></a><span data-ttu-id="1afe2-121">Docker 이미지 빌드</span><span class="sxs-lookup"><span data-stu-id="1afe2-121">Build a Docker image</span></span>

<span data-ttu-id="1afe2-122">예제 프로젝트는 사용할 수 있는 Dockerfile을 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-122">The sample project provides a Dockerfile that you can use.</span></span> <span data-ttu-id="1afe2-123">Azure Container Registry 빌드 기능을 사용하여 클라우드에서 이미지를 빌드하므로 Docker가 설치되어 있지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-123">You don't need to have Docker installed, though, because you'll use the Azure Container Registry Build feature to build the image in the cloud.</span></span>

<span data-ttu-id="1afe2-124">이미지를 빌드하고 Azure에서 실행하도록 준비하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-124">To build the image and prepare to run it on Azure, do the following:</span></span>

1. <span data-ttu-id="1afe2-125">Azure CLI를 설치하고 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-125">Install and sign in to the Azure CLI.</span></span>
1. <span data-ttu-id="1afe2-126">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="1afe2-126">Create an Azure resource group.</span></span>
1. <span data-ttu-id="1afe2-127">Azure 컨테이너 레지스트리 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-127">Create an Azure container registry instance.</span></span>
1. <span data-ttu-id="1afe2-128">Docker 이미지를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-128">Build a Docker image.</span></span>
1. <span data-ttu-id="1afe2-129">이전에 만든 컨테이너 레지스트리 인스턴스에 Docker 이미지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-129">Publish the Docker image to the previously created container registry instance.</span></span>
1. <span data-ttu-id="1afe2-130">(선택 사항) 하나의 명령으로 컨테이너 레지스트리 인스턴스에 이미지를 빌드 및 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-130">(Optional) Build and publish the image to the container registry instance in one command.</span></span>


#### <a name="set-up-the-azure-cli"></a><span data-ttu-id="1afe2-131">Azure CLI 설치</span><span class="sxs-lookup"><span data-stu-id="1afe2-131">Set up the Azure CLI</span></span>

<span data-ttu-id="1afe2-132">Azure 구독, [Azure CLI ](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) 설치 완료, 계정 인증을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-132">Make sure that you have an Azure subscription, that you've installed [the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), and that you're authenticated to your account:</span></span>

```bash
az login
```

#### <a name="create-a-resource-group"></a><span data-ttu-id="1afe2-133">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="1afe2-133">Create a resource group</span></span>

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-a-container-registry-instance"></a><span data-ttu-id="1afe2-134">컨테이너 레지스트리 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="1afe2-134">Create a container registry instance</span></span>

<span data-ttu-id="1afe2-135">이 명령은 기본 이름에 임의의 숫자를 사용하여 전역적으로 유일한 컨테이너 레지스트리 인스턴스를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-135">This command should create a globally unique container registry instance with a basic name and a random number.</span></span>

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a><span data-ttu-id="1afe2-136">Docker 이미지 빌드</span><span class="sxs-lookup"><span data-stu-id="1afe2-136">Build the Docker image</span></span>

<span data-ttu-id="1afe2-137">Docker 자체를 사용하여 Docker 이미지를 로컬에서 쉽게 만들 수 있지만 몇 가지 이유로 인해 Docker를 클라우드에서 빌드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-137">Although you can easily build the Docker image locally by using Docker itself, you might consider building it in the cloud for few reasons:</span></span>

* <span data-ttu-id="1afe2-138">Docker를 로컬로 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-138">You don't have to install Docker locally.</span></span>
* <span data-ttu-id="1afe2-139">빌드가 다른 곳에서 발생하기 때문에 훨씬 빠릅니다(컨텍스트 업로드 시간 제외).</span><span class="sxs-lookup"><span data-stu-id="1afe2-139">It's much faster, because the build happens elsewhere (except for context upload time).</span></span>
* <span data-ttu-id="1afe2-140">클라우드의 프로세스는 인터넷에 보다 빠르게 액세스하므로 빠른 다운로드가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-140">The process in the cloud has faster access to the internet and, therefore, faster downloads.</span></span>
* <span data-ttu-id="1afe2-141">이미지가 컨테이너 레지스트리 인스턴스로 직접 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-141">The image goes directly into the container registry instance.</span></span>

<span data-ttu-id="1afe2-142">이러한 이유 때문에 [Azure Container Registry 빌드] 기능을 사용하여 이미지를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-142">For these reasons, you build the image by using the [Azure Container Registry Build] feature:</span></span>

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-the-docker-image-from-the-azure-container-registry-instance-to-container-instances"></a><span data-ttu-id="1afe2-143">Azure 컨테이너 레지스트리 인스턴스에서 Container Instances로 Docker 이미지를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-143">Deploy the Docker image from the Azure container registry instance to Container Instances</span></span>

<span data-ttu-id="1afe2-144">이제 이미지를 컨테이너 레지스트리 인스턴스에 사용할 수 있으므로 Container Instances에서 컨테이너 인스턴스를 인스턴스화합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-144">Now that the image is available on your container registry instance, push and instantiate a container instance on Container Instances.</span></span> <span data-ttu-id="1afe2-145">하지만 먼저 컨테이너 레지스트리 인스턴스에 인증할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-145">But first, make sure that you can authenticate into the container registry instance:</span></span>

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a><span data-ttu-id="1afe2-146">배포된 MicroProfile 애플리케이션 테스트</span><span class="sxs-lookup"><span data-stu-id="1afe2-146">Test your deployed MicroProfile application</span></span>

<span data-ttu-id="1afe2-147">이제 애플리케이션이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-147">Your application should now be up and running.</span></span> <span data-ttu-id="1afe2-148">명령줄 인터페이스에서 테스트하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-148">To test it from the command-line interface, use the following command:</span></span>

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

<span data-ttu-id="1afe2-149">축하합니다!</span><span class="sxs-lookup"><span data-stu-id="1afe2-149">Congratulations!</span></span> <span data-ttu-id="1afe2-150">Microsoft Azure에 Docker 컨테이너로 MicroProfile 애플리케이션을 성공적으로 구축하고 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="1afe2-150">You've successfully built a MicroProfile application as a Docker container and deployed it to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1afe2-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1afe2-151">Next steps</span></span>

<span data-ttu-id="1afe2-152">이 문서에서 설명하는 다양한 기술에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1afe2-152">For more information about the various technologies discussed in this article, see:</span></span>

* [<span data-ttu-id="1afe2-153">Azure CLI에서 Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="1afe2-153">Sign in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

<!-- URL List -->

[Azure Container Registry 빌드]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Azure CLI]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Apache Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry
