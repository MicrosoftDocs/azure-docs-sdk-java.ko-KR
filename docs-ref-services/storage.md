---
title: Java용 Azure Storage 라이브러리
description: ''
keywords: Azure, Java, SDK, API, Storage
author: douge
ms.author: douge
manager: douge
ms.date: 02/07/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: ec06e79374176b5a4795d27c5fbbb2260e65cd8c
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893594"
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="205ca-103">Java용 Azure Storage 라이브러리</span><span class="sxs-lookup"><span data-stu-id="205ca-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="205ca-104">개요</span><span class="sxs-lookup"><span data-stu-id="205ca-104">Overview</span></span>

<span data-ttu-id="205ca-105">[Azure Storage](/azure/storage/storage-introduction)를 사용하여 Java 응용 프로그램의 파일, Blob(개체) 데이터, 키-값 쌍 및 메시지를 읽고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="205ca-105">Read and write files, blob (object) data, key-value pairs, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="205ca-106">Azure Storage를 시작하려면 [Java에서 Blob 저장소를 사용하는 방법](/azure/storage/storage-java-how-to-use-blob-storage)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="205ca-106">To get started with Azure Storage, see [How to use Blob storage from Java](/azure/storage/storage-java-how-to-use-blob-storage).</span></span>

## <a name="client-library"></a><span data-ttu-id="205ca-107">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="205ca-107">Client library</span></span>

<span data-ttu-id="205ca-108">[연결 문자열](/azure/storage/storage-create-storage-account#manage-your-storage-account)을 사용하여 Azure Storage 계정에 연결한 다음, 클라이언트 라이브러리의 클래스와 메서드를 사용하여 Blob, 테이블, 파일 또는 큐 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="205ca-108">Use [connection strings](/azure/storage/storage-create-storage-account#manage-your-storage-account) to connect to an Azure Storage account, then use the client libraries' classes and methods to work with blob, table, file, or queue storage.</span></span> 

<span data-ttu-id="205ca-109">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="205ca-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>7.0.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="205ca-110">예</span><span class="sxs-lookup"><span data-stu-id="205ca-110">Example</span></span>

<span data-ttu-id="205ca-111">로컬 파일 시스템의 이미지 파일을 기존 Azure Storage Blob 컨테이너의 새 Blob에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="205ca-111">Write a image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


```java
String storageConnectionString = "DefaultEndpointsProtocol=https;" + 
"AccountName=fabrikamblobstorage;" + 
"AccountKey=keyvalue;EndpointSuffix=core.windows.net";

CloudStorageAccount account = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient serviceClient = account.createCloudBlobClient();
CloudBlobContainer container = serviceClient.getContainerReference(blobContainer);

// write a blob from a local filesystem path to the container as logo.png
CloudBlockBlob blob = container.getBlockBlobReference("logo.png");
blob.uploadFromFile("/Users/raisa/fabrikam.png");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="205ca-112">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="205ca-112">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/client)

## <a name="management-api"></a><span data-ttu-id="205ca-113">관리 API</span><span class="sxs-lookup"><span data-stu-id="205ca-113">Management API</span></span>

<span data-ttu-id="205ca-114">관리 API를 사용하여 Azure Storage 계정 및 연결 키를 만들고 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="205ca-114">Crete and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="205ca-115">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="205ca-115">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="205ca-116">예</span><span class="sxs-lookup"><span data-stu-id="205ca-116">Example</span></span>

<span data-ttu-id="205ca-117">구독에 새 Azure Storage 계정을 만들고 액세스 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="205ca-117">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

```java
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
        .withRegion(Region.US_EAST)
        .withNewResourceGroup(rgName)
        .create();

// get a list of storage account keys related to the account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="205ca-118">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="205ca-118">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/management)


## <a name="samples"></a><span data-ttu-id="205ca-119">샘플</span><span class="sxs-lookup"><span data-stu-id="205ca-119">Samples</span></span>

<span data-ttu-id="205ca-120">[Azure Storage 계정 관리](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)  </span><span class="sxs-lookup"><span data-stu-id="205ca-120">[Manage Azure Storage accounts](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)  </span></span>  
<span data-ttu-id="205ca-121">[Blob 저장소에 개체 읽기 및 쓰기(영문)](https://github.com/Azure-Samples/storage-blob-java-getting-started) </span><span class="sxs-lookup"><span data-stu-id="205ca-121">[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blob-java-getting-started) </span></span>  
<span data-ttu-id="205ca-122">[큐를 사용하여 메시지 읽기 및 쓰기(영문)](https://github.com/Azure-Samples/storage-queue-java-getting-started) </span><span class="sxs-lookup"><span data-stu-id="205ca-122">[Read and write messages with queues](https://github.com/Azure-Samples/storage-queue-java-getting-started) </span></span>  
[<span data-ttu-id="205ca-123">웹앱의 Blob 저장소에서 파일 읽기(영문)</span><span class="sxs-lookup"><span data-stu-id="205ca-123">Read files from blob storage in a web app</span></span>](https://github.com/Azure-Samples/app-service-java-manage-storage-connections-for-web-apps-on-linux)

<span data-ttu-id="205ca-124">앱에서 사용할 수 있는 [Azure Storage용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=storage)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="205ca-124">Explore more [sample Java code for Azure Storage](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) you can use in your apps.</span></span>
