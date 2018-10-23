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
# <a name="partner-center-libraries-for-java"></a>Java 용 파트너 센터 라이브러리

## <a name="overview"></a>개요

Java 용 파트너센터 라이브러리는 Microsoft의 파트너 센터 서비스와 상호작용하는 기능을 제공하는 SDK입니다. 파트너는 이를 통해 프로그래매틱 방식으로 파트너 센터 작업을 수행할 수 있습니다. 이는 REST API 및.NET SDK의 기존 포트폴리오에 대한 최신 추가입니다.

## <a name="client-library"></a>클라이언트 라이브러리

클라이언트 라이브러리를 사용하여 파트너 센터에서 리소스를 관리합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.

```xml
<dependency>
    <groupId>com.microsoft.store</groupId>
    <artifactId>partnercenter</artifactId>
    <version>1.8.0</version>
</dependency>
```   

### <a name="example"></a>예

인증된 해당 재판매인과 연관된 고객의 전체 목록을 검색합니다.

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

## <a name="samples"></a>샘플

[지원되는 시나리오](https://docs.microsoft.com/partner-center/develop/scenarios)
[샘플 콘솔 응용 프로그램](https://github.com/Microsoft/Partner-Center-Java-Samples)  