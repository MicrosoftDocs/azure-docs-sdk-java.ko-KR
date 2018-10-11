---
title: Java용 Azure Traffic Manager 라이브러리
description: Java용 Traffic Manager 관리 라이브러리에 대한 참조 설명서
keywords: Azure, Java, SDK, API, 부하 분산, 네트워크, Traffic Manager
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: traffic-manager
ms.openlocfilehash: fd78402f50df16ad7d57c0ca67815bfad5b18d51
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892874"
---
# <a name="azure-traffic-manager-libraries-for-java"></a>Java용 Azure Traffic Manager 라이브러리

## <a name="overview"></a>개요

[Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview)를 사용하여 여러 데이터 센터에 있는 서비스 엔드포인트에 대한 사용자 트래픽 분산을 제어합니다.

Azure Traffic Manager를 시작하려면 [Traffic Manager 프로필 만들기](/azure/traffic-manager/traffic-manager-create-profile)를 참조하세요.

## <a name="management-api"></a>관리 API

관리 API를 사용하여 Traffic Manager 프로필을 만들고, 엔드포인트를 정의하고, 라우팅 메서드를 변경합니다. 

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-trafficmanager</artifactId>
    <version>1.3.0</version>
</dependency>
```   

## <a name="example"></a>예

Traffic Manager 프로필을 만들고, 단일 엔드포인트를 할당합니다.

```java
TrafficManagerProfile tmProfile = azure.trafficManagerProfiles().define("testTMProfile")
        .withNewResourceGroup(Region.US_EAST)
        .withLeafDomainLabel("testTMProfile")
        .withPriorityBasedRouting()
        .defineAzureTargetEndpoint("endpoint")
        .toResourceId(webAppId)
        .withRoutingPriority(1)
        .attach()
        .create();
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/java/api/overview/azure/trafficmanager/management)

## <a name="samples"></a>샘플

[여러 지역에서 웹앱 트래픽 분산](https://github.com/Azure-Samples/traffic-manager-java-manage-profiles)

앱에서 사용할 수 있는 [Azure Traffic Manager용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic)를 추가로 탐색합니다.
