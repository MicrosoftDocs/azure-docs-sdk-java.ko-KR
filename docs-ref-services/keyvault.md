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
ms.openlocfilehash: f025479301fd923b7620e8560e8586c8ab63c80b
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338987"
---
# <a name="azure-key-vault-libraries-for-java"></a><span data-ttu-id="2eafc-104">Java용 Azure Key Vault 라이브러리</span><span class="sxs-lookup"><span data-stu-id="2eafc-104">Azure Key Vault libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="2eafc-105">개요</span><span class="sxs-lookup"><span data-stu-id="2eafc-105">Overview</span></span>

<span data-ttu-id="2eafc-106">[Azure Key Vault](/azure/key-vault/)를 사용하여 클라우드 응용 프로그램 및 서비스에서 사용하는 암호화 키와 비밀을 보호하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="2eafc-106">Safeguard and manage cryptographic keys and secrets used by cloud applications and services with [Azure Key Vault](/azure/key-vault/).</span></span>

<span data-ttu-id="2eafc-107">Azure Key Vault를 시작하려면 [Azure Key Vault 시작](/azure/key-vault/key-vault-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2eafc-107">To get started with Azure Key Vault, see [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="2eafc-108">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="2eafc-108">Client library</span></span>

<span data-ttu-id="2eafc-109">클라이언트 라이브러리를 사용하여 Azure Key Vault에서 키와 비밀을 생성, 업데이트 및 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2eafc-109">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="2eafc-110">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2eafc-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.1.2</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="2eafc-111">예</span><span class="sxs-lookup"><span data-stu-id="2eafc-111">Example</span></span>

<span data-ttu-id="2eafc-112">Key Vault에서 [JSON 웹 키](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18)를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2eafc-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = kvc.getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="2eafc-113">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="2eafc-113">Explore the Client APIs</span></span>](/java/api/overview/azure/keyvault/client)


## <a name="management-api"></a><span data-ttu-id="2eafc-114">관리 API</span><span class="sxs-lookup"><span data-stu-id="2eafc-114">Management API</span></span>

<span data-ttu-id="2eafc-115">Azure Key Vault 관리 라이브러리를 사용하여 키 자격 증명 모음을 만들고, 애플리케이션에 권한을 부여하고, 권한을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="2eafc-115">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="2eafc-116">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2eafc-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.15.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="2eafc-117">예</span><span class="sxs-lookup"><span data-stu-id="2eafc-117">Example</span></span>

<span data-ttu-id="2eafc-118">키 자격 증명 모음에서 비밀을 나열하고 검색하기 위해 `clientId` [서비스 사용자](/azure/azure-resource-manager/resource-group-create-service-principal-portal)를 사용하여 실행되는 응용 프로그램에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="2eafc-118">Authorize and application running with [service principal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` to list and retrieve secrets from a key vault.</span></span> 

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
> [<span data-ttu-id="2eafc-119">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="2eafc-119">Explore the Management APIs</span></span>](/java/api/overview/azure/keyvault/management)


## <a name="samples"></a><span data-ttu-id="2eafc-120">샘플</span><span class="sxs-lookup"><span data-stu-id="2eafc-120">Samples</span></span>

<span data-ttu-id="2eafc-121">앱에서 사용할 수 있는 [Azure Key Vault용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="2eafc-121">Explore more [sample Java code for Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) you can use in your apps.</span></span>
