---
title: "Java용 Azure 배치 라이브러리"
description: "Java용 배치 라이브러리에 대한 참조 설명서"
keywords: "Azure, Java, SDK, API, 배치, 처리, 일정 계획, 장기 실행"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: batch
ms.openlocfilehash: ebf86e358ff541632e2d1f9503ebae593bdbdb3c
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/09/2017
---
# <a name="azure-batch-libraries-for-java"></a><span data-ttu-id="a6174-104">Java용 Azure 배치 라이브러리</span><span class="sxs-lookup"><span data-stu-id="a6174-104">Azure Batch libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="a6174-105">개요</span><span class="sxs-lookup"><span data-stu-id="a6174-105">Overview</span></span>

<span data-ttu-id="a6174-106">[Azure 배치](/azure/batch/batch-technical-overview)를 사용하여 클라우드에서 대규모 병렬 및 고성능 컴퓨팅 응용 프로그램을 효율적으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6174-106">Run large-scale parallel and high-performance computing applications efficiently in the cloud with [Azure Batch](/azure/batch/batch-technical-overview).</span></span>   

<span data-ttu-id="a6174-107">Azure 배치를 시작하려면 [Azure Portal에서 배치 계정 만들기](/azure/batch/batch-account-create-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6174-107">To get started with Azure Batch, see [Create a Batch account with the Azure portal](/azure/batch/batch-account-create-portal).</span></span>

## <a name="client-library"></a><span data-ttu-id="a6174-108">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="a6174-108">Client library</span></span>

<span data-ttu-id="a6174-109">Azure 배치 클라이언트 라이브러리를 사용하여 계산 노드와 풀을 구성하고, 태스크를 정의하고 작업에서 실행되도록 구성하고, 작업 실행을 제어하고 모니터링하도록 작업 관리자를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6174-109">The Azure Batch client libraries let you configure compute nodes and pools, define tasks and configure them to run in jobs, and set up a job manager to control and monitor job execution.</span></span> <span data-ttu-id="a6174-110">이러한 개체를 사용하여 대규모 병렬 계산 솔루션을 실행하는 방법에 대해 [자세히 알아보세요](/azure/batch/batch-api-basics).</span><span class="sxs-lookup"><span data-stu-id="a6174-110">[Learn more](/azure/batch/batch-api-basics) about using these objects to run large-scale parallel compute solutions.</span></span>

<span data-ttu-id="a6174-111">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6174-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="a6174-112">예제</span><span class="sxs-lookup"><span data-stu-id="a6174-112">Example</span></span>

<span data-ttu-id="a6174-113">배치 계정에 Linux 계산 노드 풀을 설정하려면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a6174-113">Set up a pool of Linux compute nodes in a batch account:</span></span>

```java
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://fabrikambatch.eastus.batch.azure.com", "fabrikambatch", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a6174-114">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="a6174-114">Explore the Client APIs</span></span>](/java/api/overview/azure/batch/clientlibrary)


## <a name="management-api"></a><span data-ttu-id="a6174-115">관리 API</span><span class="sxs-lookup"><span data-stu-id="a6174-115">Management API</span></span>

<span data-ttu-id="a6174-116">Azure 배치 관리 라이브러리를 사용하여 배치 계정을 만들고 삭제하고, 배치 계정 키를 읽고 다시 생성하며, 배치 계정 저장소를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="a6174-116">Use the Azure Batch management libraries to create and delete batch accounts, read and regenerate batch account keys, and manage batch account storage.</span></span>

<span data-ttu-id="a6174-117">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6174-117">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-batch</artifactId>
    <version>1.2.1</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="a6174-118">예제</span><span class="sxs-lookup"><span data-stu-id="a6174-118">Example</span></span>

<span data-ttu-id="a6174-119">Azure 배치 계정을 만들고, 새 응용 프로그램 및 Azure 저장소 계정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a6174-119">Create an Azure Batch account and configure a new application and Azure storage account for it.</span></span>

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
> [<span data-ttu-id="a6174-120">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="a6174-120">Explore the Management APIs</span></span>](/java/api/overview/azure/batch/managementapi)


## <a name="samples"></a><span data-ttu-id="a6174-121">샘플</span><span class="sxs-lookup"><span data-stu-id="a6174-121">Samples</span></span>

<span data-ttu-id="a6174-122">[배치 계정 관리][1]</span><span class="sxs-lookup"><span data-stu-id="a6174-122">[Manage Batch accounts][1]</span></span>   

<span data-ttu-id="a6174-123">앱에서 사용할 수 있는 [Azure 배치용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=batch)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="a6174-123">Explore more [sample Java code for Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) you can use in your apps.</span></span>

[1]: https://github.com/Azure-Samples/batch-java-manage-batch-accounts