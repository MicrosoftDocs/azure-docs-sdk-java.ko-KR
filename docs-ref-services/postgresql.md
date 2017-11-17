---
title: "Java용 Azure Database for PostgreSQL 라이브러리"
description: "Java용 Azure Database for PostgreSQL 클라이언트 라이브러리에 대한 참조 설명서"
keywords: "Azure, Java, SDK, API, SQL, 데이터베이스, PostGres, PostgreSQL"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: postgresql
ms.openlocfilehash: d6fa2acb9a2f44b157ae52ba6e41f6777a43b574
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-database-for-postgresql-libraries-for-java"></a><span data-ttu-id="b6322-104">Java용 Azure Database for PostgreSQL 라이브러리</span><span class="sxs-lookup"><span data-stu-id="b6322-104">Azure Database for PostgreSQL libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="b6322-105">개요</span><span class="sxs-lookup"><span data-stu-id="b6322-105">Overview</span></span>

<span data-ttu-id="b6322-106">[Azure Database for PostgreSQL](/azure/sql-database/sql-database-technical-overview)은 커뮤니티 버전의 [PostgreSQL](https://www.postgresql.org/) 오픈 소스 데이터베이스 엔진을 기반으로 하여 개발자용으로 빌드된 Azure의 관계형 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b6322-106">[Azure Database for PostgreSQL](/azure/sql-database/sql-database-technical-overview) is a relational database service in Azure built for developers based on the community version of open source [PostgreSQL](https://www.postgresql.org/) database engine.</span></span>

<span data-ttu-id="b6322-107">Azure Database for PostgreSQL을 시작하려면 [Java를 사용하여 데이터 연결 및 쿼리](/azure/postgresql/connect-java)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6322-107">To get started with Azure Database for PostgreSQL, see [Use Java to connect and query data](/azure/postgresql/connect-java).</span></span>

## <a name="client-jdbc-driver"></a><span data-ttu-id="b6322-108">클라이언트 JDBC 드라이버</span><span class="sxs-lookup"><span data-stu-id="b6322-108">Client JDBC driver</span></span>

<span data-ttu-id="b6322-109">[PostgreSQL JDBC 드라이버](https://jdbc.postgresql.org/) 오픈 소스를 사용하여 응용 프로그램에서 Azure Database for PostgreSQL에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b6322-109">Connect to Azure Database for PostgreSQL from your applications using the open-source [PostgreSQL JDBC driver](https://jdbc.postgresql.org/).</span></span> <span data-ttu-id="b6322-110">[Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/)를 사용하여 데이터베이스에 직접 연결하거나 [최대 절전 모드](http://hibernate.org/)와 같이 JDBC를 통해 데이터베이스와 상호 작용하는 데이터 액세스 프레임워크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6322-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect to the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="b6322-111">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 JDBC 드라이버를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6322-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>  

```XML
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.1.1</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="b6322-112">예제</span><span class="sxs-lookup"><span data-stu-id="b6322-112">Example</span></span>

<span data-ttu-id="b6322-113">JDBC를 사용하여 Azure Database for PostgreSQL에 연결하고 sales 테이블의 모든 레코드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6322-113">Connect to Azure Database for PostgreSQL using JDBC and select all records in the sales table.</span></span> <span data-ttu-id="b6322-114">Azure Portal에서 데이터베이스에 대한 JDBC 연결 문자열을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6322-114">You can get the JDBC connection string for the database from the Azure Portal.</span></span>

```java
String url = String.format("jdbc:postgresql://mypostgresdb.postgres.database.azure.com:5432/mydb?user=frank@mypostgresdb&password=AbCdEfGhIjK&ssl=true");
Connection connection = null;
try {
    connection = DriverManager.getConnection(url);
    String selectSql = "SELECT * FROM SALES";
    Statement statement = connection.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a><span data-ttu-id="b6322-115">샘플</span><span class="sxs-lookup"><span data-stu-id="b6322-115">Samples</span></span>

[<span data-ttu-id="b6322-116">Azure CLI를 사용하여 PostgreSQL 데이터베이스 디자인</span><span class="sxs-lookup"><span data-stu-id="b6322-116">Design a PostgreSQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) 

<span data-ttu-id="b6322-117">앱에서 사용할 수 있는 [Azure Database for PostgreSQL용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="b6322-117">Explore more [sample Java code for Azure Database for PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres) you can use in your apps.</span></span>
