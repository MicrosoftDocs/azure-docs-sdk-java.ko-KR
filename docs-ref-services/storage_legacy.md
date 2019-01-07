---
title: Java용 Azure Storage 라이브러리
description: ''
keywords: Azure, Java, SDK, API, Storage
author: douge
ms.author: seguler
manager: dineshm
ms.date: 10/29/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: 68a5fdbf8e2fbfe83f9ea09112d64488e0c11d08
ms.sourcegitcommit: 66f3dd4bdb09712b73c9194e23028567c0c4ee3f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50235254"
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="3b3d4-103">Java용 Azure Storage 라이브러리</span><span class="sxs-lookup"><span data-stu-id="3b3d4-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="3b3d4-104">개요</span><span class="sxs-lookup"><span data-stu-id="3b3d4-104">Overview</span></span>

<span data-ttu-id="3b3d4-105">[Azure Storage](/azure/storage/storage-introduction)를 사용하여 Java 응용 프로그램의 Blob(개체) 데이터, 파일 및 메시지를 읽고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="3b3d4-105">Read and write blob (object) data, files, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="3b3d4-106">Azure Storage를 시작하려면 [Java SDK v7에서 Blob 스토리지를 사용하는 방법](/azure/storage/blobs/storage-quickstart-blobs-java)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b3d4-106">To get started with Azure Storage, see [How to use Blob storage from Java SDK v7](/azure/storage/blobs/storage-quickstart-blobs-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="3b3d4-107">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="3b3d4-107">Client library</span></span>

<span data-ttu-id="3b3d4-108">Azure Active Directory의 공유 키, SAS 토큰 또는 OAuth 토큰을 사용하여 Azure Storage 서비스에서 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3d4-108">Use a Shared Key, SAS token or an OAuth token from the Azure Active Directory to authorize with Azure Storage services.</span></span> <span data-ttu-id="3b3d4-109">그런 다음, 클라이언트 라이브러리의 클래스 및 메서드를 사용하여 Blob, 파일 또는 큐 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3d4-109">Then use the client libraries' classes and methods to work with blob, file, or queue storage.</span></span> 

<span data-ttu-id="3b3d4-110">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3d4-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

<span data-ttu-id="3b3d4-111">**기존 Azure Storage SDK v7의 종속성**:</span><span class="sxs-lookup"><span data-stu-id="3b3d4-111">**Dependency for the legacy Azure Storage SDK v7**:</span></span>
```XML
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/azure-storage -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>8.0.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="3b3d4-112">예</span><span class="sxs-lookup"><span data-stu-id="3b3d4-112">Example</span></span>

<span data-ttu-id="3b3d4-113">로컬 파일 시스템의 이미지 파일을 기존 Azure Storage Blob 컨테이너의 새 Blob에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="3b3d4-113">Write an image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


```java
// Parse the connection string and create a blob client to interact with Blob storage
CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient blobClient = storageAccount.createCloudBlobClient();
CloudBlobContainer container = blobClient.getContainerReference("quickstartcontainer");

// Create the container if it does not exist with public access.
container.createIfNotExists(BlobContainerPublicAccessType.CONTAINER, new BlobRequestOptions(), new OperationContext());         
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b3d4-114">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="3b3d4-114">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/client)

## <a name="management-api"></a><span data-ttu-id="3b3d4-115">관리 API</span><span class="sxs-lookup"><span data-stu-id="3b3d4-115">Management API</span></span>

<span data-ttu-id="3b3d4-116">관리 API를 사용하여 Azure Storage 계정 및 연결 키를 만들고 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3d4-116">Crete and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="3b3d4-117">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3d4-117">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="3b3d4-118">예</span><span class="sxs-lookup"><span data-stu-id="3b3d4-118">Example</span></span>

<span data-ttu-id="3b3d4-119">구독에 새 Azure Storage 계정을 만들고 액세스 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3b3d4-119">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

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
> [<span data-ttu-id="3b3d4-120">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="3b3d4-120">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/management)


## <a name="samples"></a><span data-ttu-id="3b3d4-121">샘플</span><span class="sxs-lookup"><span data-stu-id="3b3d4-121">Samples</span></span>

<span data-ttu-id="3b3d4-122">[Java용 Azure Storage SDK](https://github.com/azure/azure-storage-java)
[개체 읽기 및 Blob 저장소에 쓰기](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span><span class="sxs-lookup"><span data-stu-id="3b3d4-122">[Azure Storage SDK for Java](https://github.com/azure/azure-storage-java)
[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span></span>  
[<span data-ttu-id="3b3d4-123">큐를 사용하여 메시지 읽기 및 쓰기</span><span class="sxs-lookup"><span data-stu-id="3b3d4-123">Read and write messages with queues</span></span>](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
