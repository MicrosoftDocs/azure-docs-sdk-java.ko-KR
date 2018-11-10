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
# <a name="azure-storage-libraries-for-java"></a>Java용 Azure Storage 라이브러리

## <a name="overview"></a>개요

[Azure Storage](/azure/storage/storage-introduction)를 사용하여 Java 응용 프로그램의 Blob(개체) 데이터, 파일 및 메시지를 읽고 씁니다.

Azure Storage를 시작하려면 [Java SDK v7에서 Blob 저장소를 사용하는 방법](/azure/storage/blobs/storage-quickstart-blobs-java)을 참조하세요.

## <a name="client-library"></a>클라이언트 라이브러리

Azure Active Directory의 공유 키, SAS 토큰 또는 OAuth 토큰을 사용하여 Azure Storage 서비스에서 권한을 부여합니다. 그런 다음, 클라이언트 라이브러리의 클래스 및 메서드를 사용하여 Blob, 파일 또는 큐 저장소를 사용합니다. 

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.   

**기존 Azure Storage SDK v7의 종속성**:
```XML
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/azure-storage -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>8.0.0</version>
</dependency>
```

### <a name="example"></a>예

로컬 파일 시스템의 이미지 파일을 기존 Azure Storage Blob 컨테이너의 새 Blob에 씁니다.


```java
// Parse the connection string and create a blob client to interact with Blob storage
CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient blobClient = storageAccount.createCloudBlobClient();
CloudBlobContainer container = blobClient.getContainerReference("quickstartcontainer");

// Create the container if it does not exist with public access.
container.createIfNotExists(BlobContainerPublicAccessType.CONTAINER, new BlobRequestOptions(), new OperationContext());         
```

> [!div class="nextstepaction"]
> [클라이언트 API 탐색](/java/api/overview/azure/storage/client)

## <a name="management-api"></a>관리 API

관리 API를 사용하여 Azure Storage 계정 및 연결 키를 만들고 및 관리합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a>예

구독에 새 Azure Storage 계정을 만들고 액세스 키를 검색합니다.

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
> [관리 API 탐색](/java/api/overview/azure/storage/management)


## <a name="samples"></a>샘플

[Java용 Azure Storage SDK](https://github.com/azure/azure-storage-java)
[개체 읽기 및 Blob 저장소에 쓰기](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart)   
[큐를 사용하여 메시지 읽기 및 쓰기](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
