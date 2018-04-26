---
title: Java용 Azure Cosmos DB 라이브러리
description: Java용 Azure Cosmos DB 클라이언트 라이브러리에 대한 참조 설명서
keywords: Azure, Java, SDK, API, SQL, database, MongoDB, Cosmos DB, NoSQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/10/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cosmosdb
ms.openlocfilehash: 6fc9f90cb3c8130aa82b20554a94a8b5ab78c083
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="azure-cosmos-db-libraries-for-java"></a>Java용 Azure Cosmos DB 라이브러리

## <a name="overview"></a>개요

[Azure Cosmos DB](/azure/cosmos-db/introduction)를 사용하여 키-값, JSON 문서, 그래프 및 열 형식 데이터를 전 세계에 분산된 데이터베이스에 저장하고 쿼리합니다.

Azure Cosmos DB를 시작하려면 [Azure Cosmos DB: Java 및 Azure Portal을 사용하여 API 앱 빌드](/azure/cosmos-db/create-sql-api-java)를 참조하세요.

## <a name="client-library"></a>클라이언트 라이브러리

[SQL API](/azure/cosmos-db/sql-api-introduction) 클라이언트 라이브러리로 Azure Cosmos DB에 연결하여 [SQL 쿼리 구문](/azure/cosmos-db/sql-api-sql-query)으로 JSON 데이터 작업을 수행합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 Cosmos DB 클라이언트 라이브러리를 사용합니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

### <a name="example"></a>예

SQL 쿼리 구문을 사용하여 Cosmos DB에서 일치하는 JSON 문서를 선택합니다.

```java
DocumentClient client = new DocumentClient("https://contoso.documents.azure.com:443",
                "contosoCosmosDBKey", 
                new ConnectionPolicy(),
                ConsistencyLevel.Session);

List<Document> results = client.queryDocuments("dbs/" + DATABASE_ID + "/colls/" + COLLECTION_ID,
        "SELECT * FROM myCollection WHERE myCollection.email = 'allen [at] contoso.com'",
        null)
    .getQueryIterable()
    .toList();

```

> [!div class="nextstepaction"]
> [클라이언트 API 탐색](/java/api/overview/azure/cosmosdb/client)


## <a name="samples"></a>샘플

[Azure Cosmos DB MongoDB API를 사용하여 Java 앱 개발(영문)][2]   
[Azure Cosmos DB Graph API를 사용하여 Java 앱 개발(영문)][3]   
[Azure Cosmos DB SQL API를 사용하여 Java 앱 개발][4]        

앱에서 사용할 수 있는 [Azure Cosmos DB용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos)를 추가로 탐색합니다.

[2]: https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started
[3]: https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started
[4]: https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started
