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
ms.openlocfilehash: c9dc6bedfd8f7a79494a8a547983b2771e51a494
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593248"
---
# <a name="azure-traffic-manager-libraries-for-java"></a><span data-ttu-id="93d1a-104">Java용 Azure Traffic Manager 라이브러리</span><span class="sxs-lookup"><span data-stu-id="93d1a-104">Azure Traffic Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="93d1a-105">개요</span><span class="sxs-lookup"><span data-stu-id="93d1a-105">Overview</span></span>

<span data-ttu-id="93d1a-106">[Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview)를 사용하여 여러 데이터 센터에 있는 서비스 엔드포인트에 대한 사용자 트래픽 분산을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="93d1a-106">Control the distribution of user traffic for service endpoints in different datacenters with [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>

<span data-ttu-id="93d1a-107">Azure Traffic Manager를 시작하려면 [Traffic Manager 프로필 만들기](/azure/traffic-manager/traffic-manager-create-profile)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="93d1a-107">To get started with Azure Traffic Manager, see [Create a Traffic Manager profile](/azure/traffic-manager/traffic-manager-create-profile).</span></span>

## <a name="management-api"></a><span data-ttu-id="93d1a-108">관리 API</span><span class="sxs-lookup"><span data-stu-id="93d1a-108">Management API</span></span>

<span data-ttu-id="93d1a-109">관리 API를 사용하여 Traffic Manager 프로필을 만들고, 엔드포인트를 정의하고, 라우팅 메서드를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="93d1a-109">Create Traffic Manager profiles, define endpoints, and change the routing method with the management API.</span></span> 

<span data-ttu-id="93d1a-110">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="93d1a-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-trafficmanager</artifactId>
    <version>1.3.0</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="93d1a-111">예</span><span class="sxs-lookup"><span data-stu-id="93d1a-111">Example</span></span>

<span data-ttu-id="93d1a-112">Traffic Manager 프로필을 만들고, 단일 엔드포인트를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="93d1a-112">Create a Traffic Manager profile and assign a single endpoint.</span></span>

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
> [<span data-ttu-id="93d1a-113">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="93d1a-113">Explore the Management APIs</span></span>](/java/api/overview/azure/trafficmanager/management)

## <a name="samples"></a><span data-ttu-id="93d1a-114">샘플</span><span class="sxs-lookup"><span data-stu-id="93d1a-114">Samples</span></span>

[<span data-ttu-id="93d1a-115">여러 지역에서 웹앱 트래픽 분산</span><span class="sxs-lookup"><span data-stu-id="93d1a-115">Balance web app traffic across multiple regions</span></span>](https://github.com/Azure-Samples/traffic-manager-java-manage-profiles)

<span data-ttu-id="93d1a-116">앱에서 사용할 수 있는 [Azure Traffic Manager용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="93d1a-116">Explore more [sample Java code for Azure Traffic Manager](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) you can use in your apps.</span></span>
