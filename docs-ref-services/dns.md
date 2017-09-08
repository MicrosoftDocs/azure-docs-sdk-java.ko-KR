---
title: "Java용 Azure DNS 라이브러리"
description: "Java용 Azure DNS 관리 라이브러리에 대한 참조 설명서"
keywords: "Azure, Java, SDK, API, 도메인, DNS, 이름, 서비스, 도메인 이름 서비스"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: dns
ms.openlocfilehash: 7b4f26fe6d99620207e3a53c8262180cccc66fd6
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-traffic-manager-libraries-for-java"></a><span data-ttu-id="0ca20-104">Java용 Azure Traffic Manager 라이브러리</span><span class="sxs-lookup"><span data-stu-id="0ca20-104">Azure Traffic Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="0ca20-105">개요</span><span class="sxs-lookup"><span data-stu-id="0ca20-105">Overview</span></span>

<span data-ttu-id="0ca20-106">[Azure DNS](/azure/dns/dns-overview)를 통해 다른 Azure 서비스와 동일한 자격 증명, API, 도구 및 대금 청구를 사용하여 도메인 이름 확인을 제공하고 DNS 레코드를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca20-106">Provide domain name resolution and manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services with [Azure DNS](/azure/dns/dns-overview).</span></span>

<span data-ttu-id="0ca20-107">Azure DNS를 시작하려면 [Azure CLI 2.0을 사용하여 Azure DNS 시작](/azure/dns/dns-getstarted-cli)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0ca20-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure CLI 2.0](/azure/dns/dns-getstarted-cli).</span></span>

## <a name="management-api"></a><span data-ttu-id="0ca20-108">관리 API</span><span class="sxs-lookup"><span data-stu-id="0ca20-108">Management API</span></span>

<span data-ttu-id="0ca20-109">관리 API를 사용하여 DNS 영역을 만들고 영역에 레코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca20-109">Create DNS zones and add records to zones with the management API.</span></span>

<span data-ttu-id="0ca20-110">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca20-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-dns</artifactId>
    <version>1.1.2</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="0ca20-111">예제</span><span class="sxs-lookup"><span data-stu-id="0ca20-111">Example</span></span>

<span data-ttu-id="0ca20-112">루트 DNS 영역을 만들고 기존 리소스 그룹에 `www` CNAME 레코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca20-112">Create a root DNS zone and add a `www` CNAME record in an existing resource group.</span></span>

```java
DnsZone rootDnsZone = azure.dnsZones().define("contoso.com")
        .withExistingResourceGroup("myResourceGroup")
        .create();
rootDnsZone = rootDnsZone.update()
        .withCNameRecordSet("www", "172.30.241.20")
        .apply();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="0ca20-113">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="0ca20-113">Explore the Management APIs</span></span>](/java/api/overview/azure/dns/managementapi)

## <a name="samples"></a><span data-ttu-id="0ca20-114">샘플</span><span class="sxs-lookup"><span data-stu-id="0ca20-114">Samples</span></span>

[<span data-ttu-id="0ca20-115">Azure DNS를 사용하여 도메인 호스팅 및 관리</span><span class="sxs-lookup"><span data-stu-id="0ca20-115">Host and manage your domains with Azure DNS</span></span>](https://github.com/Azure-Samples/dns-java-host-and-manage-your-domains)

<span data-ttu-id="0ca20-116">앱에서 사용할 수 있는 [Azure DNS용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=dns)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="0ca20-116">Explore more [sample Java code for Azure DNS](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) you can use in your apps.</span></span>