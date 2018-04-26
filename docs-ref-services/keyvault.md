---
title: Java용 Azure Key Vault 라이브러리
description: Java용 Azure Key Vault 라이브러리 개요
keywords: Azure, Java, SDK, API, 키 자격 증명 모음, 보안, 키, 비밀, 자격 증명 모음
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: keyvault
ms.openlocfilehash: 396d02b8bba5878ffb24f5f8994ae29aef36cfdc
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="azure-key-vault-libraries-for-java"></a><span data-ttu-id="afe39-104">Java용 Azure Key Vault 라이브러리</span><span class="sxs-lookup"><span data-stu-id="afe39-104">Azure Key Vault libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="afe39-105">개요</span><span class="sxs-lookup"><span data-stu-id="afe39-105">Overview</span></span>

<span data-ttu-id="afe39-106">[Azure Key Vault](/azure/key-vault/)를 사용하여 클라우드 응용 프로그램 및 서비스에서 사용하는 암호화 키와 비밀을 보호하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="afe39-106">Safeguard and manage cryptographic keys and secrets used by cloud applications and services with [Azure Key Vault](/azure/key-vault/).</span></span>

<span data-ttu-id="afe39-107">Azure Key Vault를 시작하려면 [Azure Key Vault 시작](/azure/key-vault/key-vault-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afe39-107">To get started with Azure Key Vault, see [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="afe39-108">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="afe39-108">Client library</span></span>

<span data-ttu-id="afe39-109">클라이언트 라이브러리를 사용하여 Azure Key Vault에서 키와 비밀을 생성, 업데이트 및 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="afe39-109">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="afe39-110">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="afe39-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="afe39-111">예</span><span class="sxs-lookup"><span data-stu-id="afe39-111">Example</span></span>

<span data-ttu-id="afe39-112">Key Vault에서 [JSON 웹 키](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18)를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="afe39-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = kvc.getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="afe39-113">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="afe39-113">Explore the Client APIs</span></span>](/java/api/overview/azure/keyvault/client)


## <a name="management-api"></a><span data-ttu-id="afe39-114">관리 API</span><span class="sxs-lookup"><span data-stu-id="afe39-114">Management API</span></span>

<span data-ttu-id="afe39-115">Azure Key Vault 관리 라이브러리를 사용하여 키 자격 증명 모음을 만들고, 응용 프로그램에 권한을 부여하고, 권한을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="afe39-115">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="afe39-116">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="afe39-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="afe39-117">예</span><span class="sxs-lookup"><span data-stu-id="afe39-117">Example</span></span>

<span data-ttu-id="afe39-118">키 자격 증명 모음에서 비밀을 나열하고 검색하기 위해 `clientId` [서비스 사용자](/azure/azure-resource-manager/resource-group-create-service-principal-portal)를 사용하여 실행되는 응용 프로그램에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="afe39-118">Authorize and application running with [service principal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` to list and retrieve secrets from a key vault.</span></span> 

```java
vault1 = vault1.update()
            .defineAccessPolicy()
                .forServicePrincipal(clientId)
                .allowKeyAllPermissions()
                .allowSecretPermissions(SecretPermissions.GET)
                .allowSecretPermissions(SecretPermissions.LIST)
                .attach()
            .apply();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="afe39-119">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="afe39-119">Explore the Management APIs</span></span>](/java/api/overview/azure/keyvault/management)


## <a name="samples"></a><span data-ttu-id="afe39-120">샘플</span><span class="sxs-lookup"><span data-stu-id="afe39-120">Samples</span></span>

<span data-ttu-id="afe39-121">[Key Vault 관리][1]</span><span class="sxs-lookup"><span data-stu-id="afe39-121">[Manage Key Vaults][1]</span></span>   

[1]: https://github.com/Azure-Samples/key-vault-java-manage-key-vaults

<span data-ttu-id="afe39-122">앱에서 사용할 수 있는 [Azure Key Vault용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="afe39-122">Explore more [sample Java code for Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) you can use in your apps.</span></span>
