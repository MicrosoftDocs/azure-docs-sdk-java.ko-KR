---
title: Java용 Azure Storage 라이브러리
description: ''
keywords: Azure, Java, SDK, API, Storage
author: douge
ms.author: douge
manager: douge
ms.date: 10/19/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: fba48dfa04f223dce72a0ee54da967565ebd3687
ms.sourcegitcommit: 66f3dd4bdb09712b73c9194e23028567c0c4ee3f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50235264"
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="3937f-103">Java용 Azure Storage 라이브러리</span><span class="sxs-lookup"><span data-stu-id="3937f-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="3937f-104">개요</span><span class="sxs-lookup"><span data-stu-id="3937f-104">Overview</span></span>

<span data-ttu-id="3937f-105">[Azure Storage](/azure/storage/storage-introduction)를 사용하여 Java 응용 프로그램의 Blob(개체) 데이터, 파일 및 메시지를 읽고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="3937f-105">Read and write blob (object) data, files, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="3937f-106">Azure Storage를 시작하려면 [Java에서 Blob 저장소를 사용하는 방법](/azure/storage/blobs/storage-quickstart-blobs-java-v10)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3937f-106">To get started with Azure Storage, see [How to use Blob storage from Java](/azure/storage/blobs/storage-quickstart-blobs-java-v10).</span></span>

## <a name="client-library"></a><span data-ttu-id="3937f-107">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="3937f-107">Client library</span></span>

<span data-ttu-id="3937f-108">Azure Active Directory의 공유 키, SAS 토큰 또는 OAuth 토큰을 사용하여 Azure Storage 서비스에서 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="3937f-108">Use a Shared Key, SAS token or an OAuth token from the Azure Active Directory to authorize with Azure Storage services.</span></span> <span data-ttu-id="3937f-109">그런 다음, 클라이언트 라이브러리의 클래스 및 메서드를 사용하여 Blob, 파일 또는 큐 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3937f-109">Then use the client libraries' classes and methods to work with blob, file, or queue storage.</span></span> 

<span data-ttu-id="3937f-110">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3937f-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

<span data-ttu-id="3937f-111">**Blob 서비스에 대한 종속성**</span><span class="sxs-lookup"><span data-stu-id="3937f-111">**Dependency for Blob service**:</span></span>
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-blob</artifactId>
    <version>10.1.0</version>
</dependency>
```

<span data-ttu-id="3937f-112">**큐 서비스에 대한 종속성**</span><span class="sxs-lookup"><span data-stu-id="3937f-112">**Dependency for Queue service**:</span></span>
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-queue</artifactId>
    <version>10.0.0-Preview</version>
</dependency>
```


### <a name="example"></a><span data-ttu-id="3937f-113">예</span><span class="sxs-lookup"><span data-stu-id="3937f-113">Example</span></span>

<span data-ttu-id="3937f-114">로컬 파일 시스템의 이미지 파일을 기존 Azure Storage Blob 컨테이너의 새 Blob에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="3937f-114">Write an image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


```java
// Retrieve the credentials and initialize SharedKeyCredentials
String accountName = System.getenv("AZURE_STORAGE_ACCOUNT");
String accountKey = System.getenv("AZURE_STORAGE_ACCESS_KEY");

// Create a BlockBlobURL to run operations on Block Blobs. Alternatively create a ServiceURL, or ContainerURL for operations on Blob service, and Blob containers
SharedKeyCredentials creds = new SharedKeyCredentials(accountName, accountKey);

// We are using a default pipeline here, you can learn more about it at https://github.com/Azure/azure-storage-java/wiki/Azure-Storage-Java-V10-Overview
final BlockBlobURL blobURL = new BlockBlobURL(
    new URL("https://" + accountName + ".blob.core.windows.net/mycontainer/myimage.jpg"), 
        StorageURL.createPipeline(creds, new PipelineOptions())
);

AsynchronousFileChannel fileChannel = AsynchronousFileChannel.open(Paths.get("myimage.jpg"));
TransferManager.uploadFileToBlockBlob(fileChannel, blobURL,0, null).blockingGet();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3937f-115">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="3937f-115">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/client)

## <a name="management-api"></a><span data-ttu-id="3937f-116">관리 API</span><span class="sxs-lookup"><span data-stu-id="3937f-116">Management API</span></span>

<span data-ttu-id="3937f-117">관리 API를 사용하여 Azure Storage 계정 및 연결 키를 만들고 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="3937f-117">Crete and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="3937f-118">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3937f-118">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="3937f-119">예</span><span class="sxs-lookup"><span data-stu-id="3937f-119">Example</span></span>

<span data-ttu-id="3937f-120">구독에 새 Azure Storage 계정을 만들고 액세스 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="3937f-120">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

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
> [<span data-ttu-id="3937f-121">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="3937f-121">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/management)


## <a name="samples"></a><span data-ttu-id="3937f-122">샘플</span><span class="sxs-lookup"><span data-stu-id="3937f-122">Samples</span></span>

<span data-ttu-id="3937f-123">[Java용 Azure Storage SDK](https://github.com/azure/azure-storage-java)
[개체 읽기 및 Blob 저장소에 쓰기](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span><span class="sxs-lookup"><span data-stu-id="3937f-123">[Azure Storage SDK for Java](https://github.com/azure/azure-storage-java)
[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span></span>  
[<span data-ttu-id="3937f-124">큐를 사용하여 메시지 읽기 및 쓰기</span><span class="sxs-lookup"><span data-stu-id="3937f-124">Read and write messages with queues</span></span>](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
