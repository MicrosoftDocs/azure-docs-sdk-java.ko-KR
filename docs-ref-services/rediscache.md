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
ms.openlocfilehash: 2bba290e16cac638685aa91b435876433fc1ea91
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/09/2017
---
# <a name="redis-cache-libraries-for-java"></a>Java용 Redis Cache 라이브러리

## <a name="overview"></a>개요

Azure Redis Cache는 인기 있는 [Redis](https://redis.io/) 오픈 소스 캐시를 기반으로 하는 안전한 분산 키-값 저장소입니다. 

Azure Redis Cache를 시작하려면 [Azure Redis Cache를 Java와 함께 사용하는 방법](/azure/redis-cache/cache-java-get-started)을 참조하세요.

## <a name="client-library"></a>클라이언트 라이브러리

Azure Redis Cache에 연결하고, [Jedis](https://github.com/xetorthio/jedis) 오픈 소스 클라이언트를 사용하여 캐시에서 값을 저장 및 검색합니다.  

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.   

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
</dependency>
```

## <a name="example"></a>예제

Azure Redis에 연결하고, 캐시에 문자열을 삽입합니다.

```java
JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */
    Jedis jedis = new Jedis(shardInfo);
    jedis.set("foo", "bar");
```

## <a name="management-api"></a>관리 API

관리 API를 사용하여 Azure Redis 리소스를 만들어 크기를 조정하고, 액세스 키를 관리합니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-redis</artifactId>
    <version>1.2.1</version>
</dependency>
```

## <a name="example"></a>예제

[2노드 표준 계층](https://azure.microsoft.com/services/cache/)에 새 Azure Redis Cache를 만듭니다. 

```java
RedisCache cache = azure.redisCaches().define(redisCacheName1)
    .withRegion(Region.US_CENTRAL)
    .withNewResourceGroup(rgName)
    .withStandardSku();
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/java/api/overview/azure/rediscache/managementapi)

## <a name="samples"></a>샘플

[Azure Redis Cache 관리](https://github.com/Azure-Samples/redis-java-manage-cache)   

앱에서 사용할 수 있는 [Azure Redis Cache용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=redis)를 추가로 탐색합니다.
