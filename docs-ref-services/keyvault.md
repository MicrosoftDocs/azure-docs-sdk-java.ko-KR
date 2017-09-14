---
title: "Java용 Azure Key Vault 라이브러리"
description: "Java용 Azure Key Vault 라이브러리 개요"
keywords: "Azure, Java, SDK, API, 키 자격 증명 모음, 보안, 키, 비밀, 자격 증명 모음"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: keyvault
ms.openlocfilehash: d87ad458eeefb090a23529662695c4faa4a75b38
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/09/2017
---
# <a name="azure-key-vault-libraries-for-java"></a>Java용 Azure Key Vault 라이브러리

## <a name="overview"></a>개요

[Azure Key Vault](/azure/key-vault/)를 사용하여 클라우드 응용 프로그램 및 서비스에서 사용하는 암호화 키와 비밀을 보호하고 관리합니다.

Azure Key Vault를 시작하려면 [Azure Key Vault 시작](/azure/key-vault/key-vault-get-started)을 참조하세요.

## <a name="client-library"></a>클라이언트 라이브러리

클라이언트 라이브러리를 사용하여 Azure Key Vault에서 키와 비밀을 생성, 업데이트 및 삭제합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```   

## <a name="example"></a>예제

Key Vault에서 [JSON 웹 키](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18)를 검색합니다.

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [클라이언트 API 탐색](/java/api/overview/azure/keyvault/clientlibrary)


## <a name="management-api"></a>관리 API

Azure Key Vault 관리 라이브러리를 사용하여 키 자격 증명 모음을 만들고, 응용 프로그램에 권한을 부여하고, 권한을 관리합니다. 

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.2.1</version>
</dependency>
```

## <a name="example"></a>예제

키 자격 증명 모음에서 비밀을 나열하고 검색하기 위해 `clientId` [서비스 사용자](/azure/azure-resource-manager/resource-group-create-service-principal-portal)를 사용하여 실행되는 응용 프로그램에 권한을 부여합니다. 

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
> [관리 API 탐색](/java/api/overview/azure/keyvault/managementapi)


## <a name="samples"></a>샘플

[Key Vault 관리][1]   

[1]: https://github.com/Azure-Samples/key-vault-java-manage-key-vaults

앱에서 사용할 수 있는 [Azure Key Vault용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault)를 추가로 탐색합니다.
