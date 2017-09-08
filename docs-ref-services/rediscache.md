---
title: "Java용 Redis Cache 라이브러리"
description: "Java용 Redis Cache 클라이언트 및 관리 라이브러리에 대한 참조 설명서"
keywords: "Azure, Java, SDK, API, 캐시, Redis, 웹 캐시, 키-값, 메모리 내"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: redis-cache
ms.openlocfilehash: 25c91e02d1ce52afab68286c89c859ab61da56fe
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2017
---
# <a name="redis-cache-libraries-for-java"></a><span data-ttu-id="1bb82-104">Java용 Redis Cache 라이브러리</span><span class="sxs-lookup"><span data-stu-id="1bb82-104">Redis Cache libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="1bb82-105">개요</span><span class="sxs-lookup"><span data-stu-id="1bb82-105">Overview</span></span>

<span data-ttu-id="1bb82-106">Azure Redis Cache는 인기 있는 [Redis](https://redis.io/) 오픈 소스 캐시를 기반으로 하는 안전한 분산 키-값 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="1bb82-106">Azure Redis Cache is a secure, distributed key-value store based on the popular open source [Redis](https://redis.io/) cache.</span></span> 

<span data-ttu-id="1bb82-107">Azure Redis Cache를 시작하려면 [Azure Redis Cache를 Java와 함께 사용하는 방법](/azure/redis-cache/cache-java-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1bb82-107">To get started with Azure Redis Cache, see [How to use Azure Redis Cache with Java](/azure/redis-cache/cache-java-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="1bb82-108">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="1bb82-108">Client library</span></span>

<span data-ttu-id="1bb82-109">Azure Redis Cache에 연결하고, [Jedis](https://github.com/xetorthio/jedis) 오픈 소스 클라이언트를 사용하여 캐시에서 값을 저장 및 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb82-109">Connect to Azure Redis Cache and store and retrieve values from the cache using the open-source [Jedis](https://github.com/xetorthio/jedis) client.</span></span>  

<span data-ttu-id="1bb82-110">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb82-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
</dependency>
```

## <a name="example"></a><span data-ttu-id="1bb82-111">예제</span><span class="sxs-lookup"><span data-stu-id="1bb82-111">Example</span></span>

<span data-ttu-id="1bb82-112">Azure Redis에 연결하고, 캐시에 문자열을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb82-112">Connect to Azure Redis and insert a string into the cache.</span></span>

```java
JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */
    Jedis jedis = new Jedis(shardInfo);
    jedis.set("foo", "bar");
```

## <a name="management-api"></a><span data-ttu-id="1bb82-113">관리 API</span><span class="sxs-lookup"><span data-stu-id="1bb82-113">Management API</span></span>

<span data-ttu-id="1bb82-114">관리 API를 사용하여 Azure Redis 리소스를 만들어 크기를 조정하고, 액세스 키를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb82-114">Create and scale Azure Redis resources and manage access keys to with the management API.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-redis</artifactId>
    <version>1.1.2</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="1bb82-115">예제</span><span class="sxs-lookup"><span data-stu-id="1bb82-115">Example</span></span>

<span data-ttu-id="1bb82-116">[2노드 표준 계층](https://azure.microsoft.com/services/cache/)에 새 Azure Redis Cache를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1bb82-116">Create a new Azure Redis Cache in the [two-node standard tier](https://azure.microsoft.com/services/cache/).</span></span> 

```java
RedisCache cache = azure.redisCaches().define(redisCacheName1)
    .withRegion(Region.US_CENTRAL)
    .withNewResourceGroup(rgName)
    .withStandardSku();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="1bb82-117">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="1bb82-117">Explore the Management APIs</span></span>](/java/api/overview/azure/rediscache/managementapi)

## <a name="samples"></a><span data-ttu-id="1bb82-118">샘플</span><span class="sxs-lookup"><span data-stu-id="1bb82-118">Samples</span></span>

[<span data-ttu-id="1bb82-119">Azure Redis Cache 관리</span><span class="sxs-lookup"><span data-stu-id="1bb82-119">Manage Azure Redis Cache</span></span>](https://github.com/Azure-Samples/redis-java-manage-cache)   

<span data-ttu-id="1bb82-120">앱에서 사용할 수 있는 [Azure Redis Cache용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=redis)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb82-120">Explore more [sample Java code for Azure Redis Cache](https://azure.microsoft.com/resources/samples/?platform=java&term=redis) you can use in your apps.</span></span>
