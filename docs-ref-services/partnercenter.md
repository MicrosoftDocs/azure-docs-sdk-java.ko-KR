---
title: 파트너 센터 Java SDK
description: 파트너 센터 Java SDK 참조 문서
keywords: API, CSP, 클라우드 솔루션 공급자, Java, 파트너 센터, SDK
author: iswillia
ms.author: iswillia
manager: lesliep
ms.date: 10/09/2018
ms.topic: reference
ms.prod: partnercenter
ms.technology: partnercenter
ms.devlang: java
ms.openlocfilehash: 2adfbdbd37d6eb91e48ee37091f951b3f7d59eb9
ms.sourcegitcommit: 4da7d2f470331feb7d76a1658f5825f365cdba9a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49121650"
---
# <a name="partner-center-libraries-for-java"></a><span data-ttu-id="f6d83-104">Java 용 파트너 센터 라이브러리</span><span class="sxs-lookup"><span data-stu-id="f6d83-104">Partner Center libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="f6d83-105">개요</span><span class="sxs-lookup"><span data-stu-id="f6d83-105">Overview</span></span>

<span data-ttu-id="f6d83-106">Java 용 파트너센터 라이브러리는 Microsoft의 파트너 센터 서비스와 상호작용하는 기능을 제공하는 SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="f6d83-106">The Partner Center libraries for Java is a SDK that provides the ability to interact with Microsoft's Partner Center service.</span></span> <span data-ttu-id="f6d83-107">파트너는 이를 통해 프로그래매틱 방식으로 파트너 센터 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6d83-107">This enables partners to perform the Partner Center operations programmatically.</span></span> <span data-ttu-id="f6d83-108">이는 REST API 및.NET SDK의 기존 포트폴리오에 대한 최신 추가입니다.</span><span class="sxs-lookup"><span data-stu-id="f6d83-108">This is the latest addition to existing portfolio of REST APIs and the .NET SDK.</span></span>

## <a name="client-library"></a><span data-ttu-id="f6d83-109">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="f6d83-109">Client library</span></span>

<span data-ttu-id="f6d83-110">클라이언트 라이브러리를 사용하여 파트너 센터에서 리소스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f6d83-110">Manage resources in Partner Center using the client library.</span></span>

<span data-ttu-id="f6d83-111">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f6d83-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```xml
<dependency>
    <groupId>com.microsoft.store</groupId>
    <artifactId>partnercenter</artifactId>
    <version>1.8.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="f6d83-112">예</span><span class="sxs-lookup"><span data-stu-id="f6d83-112">Example</span></span>

<span data-ttu-id="f6d83-113">인증된 해당 재판매인과 연관된 고객의 전체 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f6d83-113">Retrieves a complete list of customer associated with the authenticated reseller.</span></span>

```java
IPartnerCredentials appCredentials = PartnerCredentials.getInstance().generateByApplicationCredentials('YOUR_APP_ID', 'YOUR_APP_SECRET', 'YOUR_TENANT_ID');
IAggregatePartner partnerOperations = PartnerService.getInstance().createPartnerOperations(appCredentials);

// Query the customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(100));
this.getContext().getConsoleHelper().stopProgress();

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while ( customersEnumerator.hasValue() )
{
    /*
     * Perform some operation with the current page of customers using 
     * customersEnumerator.getCurrent()  
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="samples"></a><span data-ttu-id="f6d83-114">샘플</span><span class="sxs-lookup"><span data-stu-id="f6d83-114">Samples</span></span>

<span data-ttu-id="f6d83-115">[지원되는 시나리오](https://docs.microsoft.com/partner-center/develop/scenarios)
[샘플 콘솔 응용 프로그램](https://github.com/Microsoft/Partner-Center-Java-Samples)</span><span class="sxs-lookup"><span data-stu-id="f6d83-115">[Supported scenarios](https://docs.microsoft.com/partner-center/develop/scenarios)
[Sample console application](https://github.com/Microsoft/Partner-Center-Java-Samples)</span></span>  