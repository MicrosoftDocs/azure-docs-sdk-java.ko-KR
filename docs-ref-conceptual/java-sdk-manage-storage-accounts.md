---
title: Java를 사용하여 Azure 저장소 계정 관리 | Microsoft Docs
description: Java용 Azure SDK를 사용하여 Azure 저장소 계정을 관리하는 샘플 코드
author: rloutlaw
manager: douge
ms.assetid: 49be8b66-3b56-4c10-8f14-9d326d815cb4
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 5945164b2b04e1fa9169590a71f6c5f9f45842d6
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893065"
---
# <a name="manage-azure-storage-accounts-from-your-java-applications"></a>Java 응용 프로그램에서 Azure 저장소 계정 관리

[이 샘플](https://github.com/Azure-Samples/storage-java-manage-storage-accounts)에서는 [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction) 계정을 만들고 [Java 관리 라이브러리](https://github.com/Azure/azure-sdk-for-java)를 사용하여 계정 액세스 키를 통해 작동합니다. 

## <a name="run-the-sample"></a>샘플 실행

[인증 파일](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md)을 만들고 컴퓨터에서 파일의 전체 경로가 포함된 `AZURE_AUTH_LOCATION` 환경 변수를 설정합니다. 그런 후 다음을 실행합니다.

```
git clone https://github.com/Azure-Samples/storage-java-manage-storage-accounts.git
cd storage-java-manage-storage-accounts
mvn clean compile exec:java
```

[GitHub에서 전체 샘플 코드(영문)](https://github.com/Azure-Samples/storage-java-manage-storage-accounts)를 봅니다.

## <a name="authenticate-with-azure"></a>Azure를 사용하여 인증

[!INCLUDE [auth-include](includes/java-auth-include.md)] 

## <a name="create-a-storage-account"></a>저장소 계정 만들기

```java
// create a new storage account
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .create();
```

제공된 저장소 이름은 Azure의 모든 이름에서 고유해야 하며 소문자와 숫자만 포함해야 합니다. 이 계정에 사용되는 기본 성능 및 복제 프로필은 [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage)입니다.

## <a name="list-keys-in-a-storage-account"></a>저장소 계정의 키 나열
```java
// list the name and value for each access key in the storage account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

한 키를 다시 생성하는 한편 다른 키를 사용하여 저장소에 대한 액세스를 허용할 수 있도록 각 Azure저장소 계정에 두 개의 키가 제공됩니다.

## <a name="regenerate-a-key-in-a-storage-account"></a>저장소 계정에서 키 다시 생성

```java
// regenerate the first key in a storage account and return an updated list of keys 
List<StorageAccountKey> updatedStorageAccountKeys =
    storageAccount.regenerateKey(storageAccountKeys.get(0).keyName());
```

새 키를 생성한 후에는 모든 Azure 리소스 및 응용 프로그램을 새 키로 업데이트해야 합니다.

## <a name="list-all-storage-accounts-in-a-resource-group"></a>리소스 그룹의 모든 저장소 계정 나열
```java
// get a list of accounts in a resource group , log info about each one
List<StorageAccount> accounts = azure.storageAccounts().listByResourceGroup(rgName);
for (StorageAccount sa : accounts) {
    System.out.println("Storage Account " + sa.name() + " created @ " + sa.creationTime());
}
```

[com.microsoft.Azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account)에서 저장소 계정 구성을 검사하는 유용한 메서드 집합을 제공합니다.

## <a name="delete-a-storage-account"></a>저장소 계정 삭제
```java
// delete by ID when you already have a storage account object
azure.storageAccounts().deleteById(storageAccount.id());

// delete by resource group and account name if you don't have an account object
azure.storageAccounts().deleteByResourceGroup(rgName,accountName);
```

> [!NOTE]
> 다른 아티팩트에서 사용 중인 가상 머신 또는 디스크에 연결된 사용 중인 디스크 이미지가 있는 Storage 계정은 이러한 메서드로 제거할 수 없습니다. 계정을 제거하려면 먼저 이러한 리소스에서 저장소를 분리하세요.

## <a name="sample-explanation"></a>샘플 설명

[GitHub의 샘플 코드](https://github.com/Azure-Samples/storage-java-manage-storage-accounts):

- 저장소 계정을 만듭니다.
- 액세스 키를 읽고 다시 생성합니다.
- 리소스 그룹의 모든 저장소 계정을 나열합니다.
- 저장소 계정을 삭제합니다. 

| 샘플에 사용되는 클래스 | 메모
|-------|-------|
| [StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account)  | Azure 저장소 계정에 대한 표현입니다. 클래스의 메서드를 사용하여 저장소 계정에 대한 정보를 얻습니다.
| [StorageAccountKey](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account_key) | `StorageAccount.getKeys()`는 저장소 계정 키를 반환합니다. `StorageAccount`의 `regenerateKey` 메서드를 사용하여 키를 업데이트합니다.

## <a name="next-steps"></a>다음 단계

[!INCLUDE [next-steps](includes/java-next-steps.md)]