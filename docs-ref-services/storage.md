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
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823656"
---
# <a name="azure-storage-libraries-for-java"></a>Java용 Azure Storage 라이브러리

## <a name="overview"></a>개요

[Azure Storage](/azure/storage/storage-introduction)를 사용하여 Java 응용 프로그램의 파일, Blob(개체) 데이터, 키-값 쌍 및 메시지를 읽고 씁니다.

Azure Storage를 시작하려면 [Java에서 Blob 저장소를 사용하는 방법](/azure/storage/storage-java-how-to-use-blob-storage)을 참조하세요.

## <a name="client-library"></a>클라이언트 라이브러리

[연결 문자열](/azure/storage/storage-create-storage-account#manage-your-storage-account)을 사용하여 Azure Storage 계정에 연결한 다음, 클라이언트 라이브러리의 클래스와 메서드를 사용하여 Blob, 테이블, 파일 또는 큐 저장소를 사용합니다. 

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>7.0.0</version>
</dependency>
```   

### <a name="example"></a>예

로컬 파일 시스템의 이미지 파일을 기존 Azure Storage Blob 컨테이너의 새 Blob에 씁니다.


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

[Azure Storage 계정 관리](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)    
[Blob 저장소에 개체 읽기 및 쓰기(영문)](https://github.com/Azure-Samples/storage-blob-java-getting-started)   
[큐를 사용하여 메시지 읽기 및 쓰기(영문)](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
[웹앱의 Blob 저장소에서 파일 읽기(영문)](https://github.com/Azure-Samples/app-service-java-manage-storage-connections-for-web-apps-on-linux)

앱에서 사용할 수 있는 [Azure Storage용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=storage)를 추가로 탐색합니다.
