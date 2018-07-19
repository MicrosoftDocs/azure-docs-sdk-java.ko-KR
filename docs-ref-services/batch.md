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
ms.openlocfilehash: 67381d68d23f98579a472aefbebaa929af622b8d
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823596"
---
# <a name="azure-batch-libraries-for-java"></a>Java용 Azure Batch 라이브러리

## <a name="overview"></a>개요

[Azure Batch](/azure/batch/batch-technical-overview)를 사용하여 클라우드에서 대규모 병렬 및 고성능 컴퓨팅 응용 프로그램을 효율적으로 실행합니다.   

Azure Batch를 시작하려면 [Azure Portal에서 Batch 계정 만들기](/azure/batch/batch-account-create-portal)를 참조하세요.

## <a name="client-library"></a>클라이언트 라이브러리

Azure Batch 클라이언트 라이브러리를 사용하여 계산 노드와 풀을 구성하고, 태스크를 정의하고 작업에서 실행되도록 구성하고, 작업 실행을 제어하고 모니터링하도록 작업 관리자를 설정할 수 있습니다. 이러한 개체를 사용하여 대규모 병렬 계산 솔루션을 실행하는 방법에 대해 [자세히 알아보세요](/azure/batch/batch-api-basics).

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```   

### <a name="example"></a>예

배치 계정에 Linux 계산 노드 풀을 설정하려면 다음과 같습니다.

```java
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://fabrikambatch.eastus.batch.azure.com", "fabrikambatch", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

> [!div class="nextstepaction"]
> [클라이언트 API 탐색](/java/api/overview/azure/batch/client)


## <a name="management-api"></a>관리 API

Azure Batch 관리 라이브러리를 사용하여 Batch 계정을 만들고 삭제하고, Batch 계정 키를 읽고 다시 생성하며, Batch 계정 저장소를 관리합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-batch</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a>예

Azure Batch 계정을 만들고, 새 응용 프로그램 및 Azure 저장소 계정을 구성합니다.

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
> [관리 API 탐색](/java/api/overview/azure/batch/management)


## <a name="samples"></a>샘플

[Batch 계정 관리][1]   

앱에서 사용할 수 있는 [Azure Batch용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=batch)를 추가로 탐색합니다.

[1]: https://github.com/Azure-Samples/batch-java-manage-batch-accounts