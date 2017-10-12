---
title: "Java용 Azure CDN 라이브러리"
description: "Java용 CDN 관리 라이브러리에 대한 참조 설명서"
keywords: "Azure, Java, SDK, API, 콘텐츠, 배포, 네트워크, CDN"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cdn
ms.openlocfilehash: 91df958d2d78fb4fd959c228b28c6ae003716be6
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2017
---
# <a name="azure-cdn-libraries-for-java"></a><span data-ttu-id="458d2-104">Java용 Azure CDN 라이브러리</span><span class="sxs-lookup"><span data-stu-id="458d2-104">Azure CDN libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="458d2-105">개요</span><span class="sxs-lookup"><span data-stu-id="458d2-105">Overview</span></span>

<span data-ttu-id="458d2-106">전략적으로 배치된 위치에 정적 웹 콘텐츠를 캐싱하여 [Azure CDN(Content Delivery Network)](/azure/cdn/cdn-overview) 사용자에게 최대 처리량을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="458d2-106">Cache static web content at strategically placed locations to provide maximum throughput for users with [Azure Content Delivery Network](/azure/cdn/cdn-overview) (CDN).</span></span>

<span data-ttu-id="458d2-107">Azure CDN을 시작하려면 [Azure CDN 시작](/azure/cdn/cdn-create-new-endpoint)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="458d2-107">To get started with Azure CDN, see [Getting started with Azure CDN](/azure/cdn/cdn-create-new-endpoint).</span></span>

## <a name="management-api"></a><span data-ttu-id="458d2-108">관리 API</span><span class="sxs-lookup"><span data-stu-id="458d2-108">Management API</span></span>

<span data-ttu-id="458d2-109">관리 API를 사용하여 CDN 프로필을 만들고, 끝점을 정의하며, CDN에 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="458d2-109">Create CDN profiles, define endpoints, and add content to the CDN using the management API.</span></span>

<span data-ttu-id="458d2-110">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="458d2-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-cdn</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="458d2-111">예제</span><span class="sxs-lookup"><span data-stu-id="458d2-111">Example</span></span>

<span data-ttu-id="458d2-112">CDN 프로필을 만들고, 끝점을 할당하고, CDN에 콘텐츠를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="458d2-112">Create a CDN profile, assign endpoints, and load content into the CDN.</span></span>

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
> [<span data-ttu-id="458d2-113">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="458d2-113">Explore the Management APIs</span></span>](/java/api/overview/azure/cdn/managementapi)

## <a name="samples"></a><span data-ttu-id="458d2-114">샘플</span><span class="sxs-lookup"><span data-stu-id="458d2-114">Samples</span></span>

[<span data-ttu-id="458d2-115">Java를 사용하여 CDN 관리</span><span class="sxs-lookup"><span data-stu-id="458d2-115">Manage CDNs with Java</span></span>](https://github.com/Azure-Samples/cdn-java-manage-cdn)

<span data-ttu-id="458d2-116">앱에서 사용할 수 있는 [Azure CDN용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="458d2-116">Explore more [sample Java code for Azure CDN](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn) you can use in your apps.</span></span>