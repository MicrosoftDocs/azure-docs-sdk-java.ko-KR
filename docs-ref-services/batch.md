---
title: Java용 Azure Batch 라이브러리
description: Java용 Batch 라이브러리에 대한 참조 설명서
keywords: Azure, Java, SDK, API, Batch, 처리, 일정 계획, 장기 실행
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: batch
ms.openlocfilehash: d8e7a6969bf35d98f03c5d3e335fbaf2f6b3a51d
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324360"
---
# <a name="azure-batch-libraries-for-java"></a><span data-ttu-id="bfbcb-104">Java용 Azure Batch 라이브러리</span><span class="sxs-lookup"><span data-stu-id="bfbcb-104">Azure Batch libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="bfbcb-105">개요</span><span class="sxs-lookup"><span data-stu-id="bfbcb-105">Overview</span></span>

<span data-ttu-id="bfbcb-106">[Azure Batch](/azure/batch/batch-technical-overview)를 사용하여 클라우드에서 대규모 병렬 및 고성능 컴퓨팅 응용 프로그램을 효율적으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbcb-106">Run large-scale parallel and high-performance computing applications efficiently in the cloud with [Azure Batch](/azure/batch/batch-technical-overview).</span></span>   

<span data-ttu-id="bfbcb-107">Azure Batch를 시작하려면 [Azure Portal에서 Batch 계정 만들기](/azure/batch/batch-account-create-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bfbcb-107">To get started with Azure Batch, see [Create a Batch account with the Azure portal](/azure/batch/batch-account-create-portal).</span></span>

## <a name="client-library"></a><span data-ttu-id="bfbcb-108">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="bfbcb-108">Client library</span></span>

<span data-ttu-id="bfbcb-109">Azure Batch 클라이언트 라이브러리를 사용하여 계산 노드와 풀을 구성하고, 태스크를 정의하고 작업에서 실행되도록 구성하고, 작업 실행을 제어하고 모니터링하도록 작업 관리자를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbcb-109">The Azure Batch client libraries let you configure compute nodes and pools, define tasks and configure them to run in jobs, and set up a job manager to control and monitor job execution.</span></span> <span data-ttu-id="bfbcb-110">이러한 개체를 사용하여 대규모 병렬 계산 솔루션을 실행하는 방법에 대해 [자세히 알아보세요](/azure/batch/batch-api-basics).</span><span class="sxs-lookup"><span data-stu-id="bfbcb-110">[Learn more](/azure/batch/batch-api-basics) about using these objects to run large-scale parallel compute solutions.</span></span>

<span data-ttu-id="bfbcb-111">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbcb-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span> <span data-ttu-id="bfbcb-112">클라이언트 라이브러리 소스 코드는 [Github](https://github.com/Azure/azure-batch-sdk-for-java)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbcb-112">The client library source code can be found in [Github](https://github.com/Azure/azure-batch-sdk-for-java).</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>4.0.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="bfbcb-113">예</span><span class="sxs-lookup"><span data-stu-id="bfbcb-113">Example</span></span>

<span data-ttu-id="bfbcb-114">배치 계정에 Linux 계산 노드 풀을 설정하려면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbcb-114">Set up a pool of Linux compute nodes in a batch account:</span></span>

```java
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://fabrikambatch.eastus.batch.azure.com", "fabrikambatch", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="bfbcb-115">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="bfbcb-115">Explore the Client APIs</span></span>](/java/api/overview/azure/batch/client)


## <a name="management-api"></a><span data-ttu-id="bfbcb-116">관리 API</span><span class="sxs-lookup"><span data-stu-id="bfbcb-116">Management API</span></span>

<span data-ttu-id="bfbcb-117">Azure Batch 관리 라이브러리를 사용하여 Batch 계정을 만들고 삭제하고, Batch 계정 키를 읽고 다시 생성하며, Batch 계정 저장소를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbcb-117">Use the Azure Batch management libraries to create and delete batch accounts, read and regenerate batch account keys, and manage batch account storage.</span></span>

<span data-ttu-id="bfbcb-118">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbcb-118">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-batch</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="bfbcb-119">예</span><span class="sxs-lookup"><span data-stu-id="bfbcb-119">Example</span></span>

<span data-ttu-id="bfbcb-120">Azure Batch 계정을 만들고, 새 애플리케이션 및 Azure Storage 계정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbcb-120">Create an Azure Batch account and configure a new application and Azure storage account for it.</span></span>

```java
BatchAccount batchAccount = azure.batchAccounts().define("newBatchAcct")
    .withRegion(Region.US_EAST)
    .withNewResourceGroup("myResourceGroup")
    .defineNewApplication("batchAppName")
        .defineNewApplicationPackage(applicationPackageName)
        .withAllowUpdates(true)
        .withDisplayName(applicationDisplayName)
        .attach()
    .withNewStorageAccount("batchStorageAcct")
    .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="bfbcb-121">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="bfbcb-121">Explore the Management APIs</span></span>](/java/api/overview/azure/batch/management)


## <a name="samples"></a><span data-ttu-id="bfbcb-122">샘플</span><span class="sxs-lookup"><span data-stu-id="bfbcb-122">Samples</span></span>

<span data-ttu-id="bfbcb-123">[Batch 계정 관리][1]</span><span class="sxs-lookup"><span data-stu-id="bfbcb-123">[Manage Batch accounts][1]</span></span>   

<span data-ttu-id="bfbcb-124">앱에서 사용할 수 있는 [Azure Batch용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=batch)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbcb-124">Explore more [sample Java code for Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) you can use in your apps.</span></span>

[1]: https://github.com/Azure-Samples/batch-java-manage-batch-accounts
