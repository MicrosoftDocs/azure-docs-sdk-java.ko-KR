---
title: Java용 Azure CDN 라이브러리
description: Java용 CDN 관리 라이브러리에 대한 참조 설명서
keywords: Azure, Java, SDK, API, 콘텐츠, 배포, 네트워크, CDN
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cdn
ms.openlocfilehash: 199e9b4b2b2431e23954d24e4adeb4326eb4741c
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893074"
---
# <a name="azure-cdn-libraries-for-java"></a>Java용 Azure CDN 라이브러리

## <a name="overview"></a>개요

전략적으로 배치된 위치에 정적 웹 콘텐츠를 캐싱하여 [Azure CDN(Content Delivery Network)](/azure/cdn/cdn-overview) 사용자에게 최대 처리량을 제공합니다.

Azure CDN을 시작하려면 [Azure CDN 시작](/azure/cdn/cdn-create-new-endpoint)을 참조하세요.

## <a name="management-api"></a>관리 API

관리 API를 사용하여 CDN 프로필을 만들고, 엔드포인트를 정의하며, CDN에 콘텐츠를 추가합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-cdn</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a>예

CDN 프로필을 만들고, 엔드포인트를 할당하고, CDN에 콘텐츠를 로드합니다.

```java
CdnProfile profile = azure.cdnProfiles().define("testCDN")
        .withRegion(Region.US_EAST)
        .withNewResourceGroup()
        .withStandardVerizonSku()
        .withNewEndpoint("webAppHostname1")
        .withNewEndpoint("webAppHostname2")
        .create();

List<String> contentList = new ArrayList<String>();
contentList.add("/client.js");
contentList.add("/media/fabrikam_logo.png");

for (CdnEndpoint endpoint : profile.endpoints().values()) {
    endpoint.loadContent(contentList);
}
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/java/api/overview/azure/cdn/management)

## <a name="samples"></a>샘플

[Java를 사용하여 CDN 관리](https://github.com/Azure-Samples/cdn-java-manage-cdn)

앱에서 사용할 수 있는 [Azure CDN용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn)를 추가로 탐색합니다.