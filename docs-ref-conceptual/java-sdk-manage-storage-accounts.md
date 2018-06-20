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
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931059"
---
# <a name="manage-azure-storage-accounts-from-your-java-applications"></a><span data-ttu-id="a31c7-103">Java 응용 프로그램에서 Azure 저장소 계정 관리</span><span class="sxs-lookup"><span data-stu-id="a31c7-103">Manage Azure storage accounts from your Java applications</span></span>

<span data-ttu-id="a31c7-104">[이 샘플](https://github.com/Azure-Samples/storage-java-manage-storage-accounts)에서는 [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction) 계정을 만들고 [Java 관리 라이브러리](https://github.com/Azure/azure-sdk-for-java)를 사용하여 계정 액세스 키를 통해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-104">[This sample](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) creates an [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction) account and works with the account access keys using the [Java management libraries](https://github.com/Azure/azure-sdk-for-java).</span></span> 

## <a name="run-the-sample"></a><span data-ttu-id="a31c7-105">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="a31c7-105">Run the sample</span></span>

<span data-ttu-id="a31c7-106">[인증 파일](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md)을 만들고 컴퓨터에서 파일의 전체 경로가 포함된 `AZURE_AUTH_LOCATION` 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="a31c7-107">그런 후 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/storage-java-manage-storage-accounts.git
cd storage-java-manage-storage-accounts
mvn clean compile exec:java
```

<span data-ttu-id="a31c7-108">[GitHub에서 전체 샘플 코드(영문)](https://github.com/Azure-Samples/storage-java-manage-storage-accounts)를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="a31c7-109">Azure를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="a31c7-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)] 

## <a name="create-a-storage-account"></a><span data-ttu-id="a31c7-110">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="a31c7-110">Create a storage account</span></span>

```java
// create a new storage account
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .create();
```

<span data-ttu-id="a31c7-111">제공된 저장소 이름은 Azure의 모든 이름에서 고유해야 하며 소문자와 숫자만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-111">The storage name provided must be unique across all names in Azure and contain only lowercase letters and numbers.</span></span> <span data-ttu-id="a31c7-112">이 계정에 사용되는 기본 성능 및 복제 프로필은 [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage)입니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-112">The default performance and replication profile used for this account is [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage).</span></span>

## <a name="list-keys-in-a-storage-account"></a><span data-ttu-id="a31c7-113">저장소 계정의 키 나열</span><span class="sxs-lookup"><span data-stu-id="a31c7-113">List keys in a storage account</span></span>
```java
// list the name and value for each access key in the storage account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

<span data-ttu-id="a31c7-114">한 키를 다시 생성하는 한편 다른 키를 사용하여 저장소에 대한 액세스를 허용할 수 있도록 각 Azure저장소 계정에 두 개의 키가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-114">Two keys are provided in each Azure storage account so that you can regenerate one key while still allowing access to storage using the other key.</span></span>

## <a name="regenerate-a-key-in-a-storage-account"></a><span data-ttu-id="a31c7-115">저장소 계정에서 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="a31c7-115">Regenerate a key in a storage account</span></span>

```java
// regenerate the first key in a storage account and return an updated list of keys 
List<StorageAccountKey> updatedStorageAccountKeys =
    storageAccount.regenerateKey(storageAccountKeys.get(0).keyName());
```

<span data-ttu-id="a31c7-116">새 키를 생성한 후에는 모든 Azure 리소스 및 응용 프로그램을 새 키로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-116">You must update all Azure resources and applications with the new key after generating a new one.</span></span>

## <a name="list-all-storage-accounts-in-a-resource-group"></a><span data-ttu-id="a31c7-117">리소스 그룹의 모든 저장소 계정 나열</span><span class="sxs-lookup"><span data-stu-id="a31c7-117">List all storage accounts in a resource group</span></span>
```java
// get a list of accounts in a resource group , log info about each one
List<StorageAccount> accounts = azure.storageAccounts().listByResourceGroup(rgName);
for (StorageAccount sa : accounts) {
    System.out.println("Storage Account " + sa.name() + " created @ " + sa.creationTime());
}
```

<span data-ttu-id="a31c7-118">[com.microsoft.Azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account)에서 저장소 계정 구성을 검사하는 유용한 메서드 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-118">[com.microsoft.azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account) provides a set of useful methods to inspect the configuration of a storage account.</span></span>

## <a name="delete-a-storage-account"></a><span data-ttu-id="a31c7-119">저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="a31c7-119">Delete a storage account</span></span>
```java
// delete by ID when you already have a storage account object
azure.storageAccounts().deleteById(storageAccount.id());

// delete by resource group and account name if you don't have an account object
azure.storageAccounts().deleteByResourceGroup(rgName,accountName);
```

> [!NOTE]
> <span data-ttu-id="a31c7-120">다른 아티팩트에서 사용 중인 가상 컴퓨터 또는 디스크에 연결된 사용 중인 디스크 이미지가 있는 저장소 계정은 이러한 메서드로 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-120">Storage accounts with in-use disk images connected to virtual machines or disks in use by other artifacts may not remove with these methods.</span></span> <span data-ttu-id="a31c7-121">계정을 제거하려면 먼저 이러한 리소스에서 저장소를 분리하세요.</span><span class="sxs-lookup"><span data-stu-id="a31c7-121">Detach the storage from these resources before removing the account.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="a31c7-122">샘플 설명</span><span class="sxs-lookup"><span data-stu-id="a31c7-122">Sample explanation</span></span>

<span data-ttu-id="a31c7-123">[GitHub의 샘플 코드](https://github.com/Azure-Samples/storage-java-manage-storage-accounts):</span><span class="sxs-lookup"><span data-stu-id="a31c7-123">[The sample code on GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts):</span></span>

- <span data-ttu-id="a31c7-124">저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-124">creates a storage account</span></span>
- <span data-ttu-id="a31c7-125">액세스 키를 읽고 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-125">reads and regenerates access keys</span></span>
- <span data-ttu-id="a31c7-126">리소스 그룹의 모든 저장소 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-126">lists all storage accounts in a resource group</span></span>
- <span data-ttu-id="a31c7-127">저장소 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-127">deletes the storage account</span></span> 

| <span data-ttu-id="a31c7-128">샘플에 사용되는 클래스</span><span class="sxs-lookup"><span data-stu-id="a31c7-128">Class used in sample</span></span> | <span data-ttu-id="a31c7-129">참고 사항</span><span class="sxs-lookup"><span data-stu-id="a31c7-129">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="a31c7-130">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="a31c7-130">StorageAccount</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account)  | <span data-ttu-id="a31c7-131">Azure 저장소 계정에 대한 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-131">Representation of an Azure storage account.</span></span> <span data-ttu-id="a31c7-132">클래스의 메서드를 사용하여 저장소 계정에 대한 정보를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-132">Use the methods in the class to get information about the storage account.</span></span>
| [<span data-ttu-id="a31c7-133">StorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="a31c7-133">StorageAccountKey</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account_key) | <span data-ttu-id="a31c7-134">`StorageAccount.getKeys()`는 저장소 계정 키를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-134">`StorageAccount.getKeys()` returns the storage account keys.</span></span> <span data-ttu-id="a31c7-135">`StorageAccount`의 `regenerateKey` 메서드를 사용하여 키를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a31c7-135">Use the `regenerateKey` methods in `StorageAccount` to update the keys.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a31c7-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a31c7-136">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]