---
title: Java용 Azure DNS 라이브러리
description: Java용 Azure DNS 관리 라이브러리에 대한 참조 설명서
keywords: Azure, Java, SDK, API, 도메인, DNS, 이름, 서비스, 도메인 이름 서비스
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: dns
ms.openlocfilehash: 2cd8fe7ee4d6a87da32a349fe8f1d2815d3fd36d
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823636"
---
# <a name="azure-traffic-manager-libraries-for-java"></a>Java용 Azure Traffic Manager 라이브러리

## <a name="overview"></a>개요

[Azure DNS](/azure/dns/dns-overview)를 통해 다른 Azure 서비스와 동일한 자격 증명, API, 도구 및 대금 청구를 사용하여 도메인 이름 확인을 제공하고 DNS 레코드를 관리합니다.

Azure DNS를 시작하려면 [Azure CLI 2.0을 사용하여 Azure DNS 시작](/azure/dns/dns-getstarted-cli)을 참조하세요.

## <a name="management-api"></a>관리 API

관리 API를 사용하여 DNS 영역을 만들고 영역에 레코드를 추가합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-dns</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a>예

루트 DNS 영역을 만들고 기존 리소스 그룹에 `www` CNAME 레코드를 추가합니다.

```java
DnsZone rootDnsZone = azure.dnsZones().define("contoso.com")
        .withExistingResourceGroup("myResourceGroup")
        .create();
rootDnsZone = rootDnsZone.update()
        .withCNameRecordSet("www", "172.30.241.20")
        .apply();
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/java/api/overview/azure/dns/management)

## <a name="samples"></a>샘플

[Azure DNS를 사용하여 도메인 호스팅 및 관리](https://github.com/Azure-Samples/dns-java-host-and-manage-your-domains)

앱에서 사용할 수 있는 [Azure DNS용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=dns)를 추가로 탐색합니다.

<!---Loc Comment: Please, refer to conversation section to check the issue. Thanks.--->
