---
title: Java용 Azure SQL Database 라이브러리
description: 관리 API를 사용하여 JDBC 드라이버 또는 Azure SQL Database 관리 인스턴스를 사용하는 Azure SQL Database에 연결합니다.
keywords: Azure, Java, SDK, API, SQL, 데이터베이스, JDBC
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/05/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: sql-database
ms.openlocfilehash: 37f7d3caf10e6b709cee2452c63a543d49e0ead8
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893314"
---
# <a name="azure-sql-database-libraries-for-java"></a><span data-ttu-id="c0989-104">Java용 Azure SQL Database 라이브러리</span><span class="sxs-lookup"><span data-stu-id="c0989-104">Azure SQL Database libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="c0989-105">개요</span><span class="sxs-lookup"><span data-stu-id="c0989-105">Overview</span></span>

<span data-ttu-id="c0989-106">[Azure SQL Database](/azure/sql-database/sql-database-technical-overview)는 테이블, JSON, 공간 및 XML 데이터를 지원하는 Microsoft SQL Server 엔진을 사용하는 관계형 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c0989-106">[Azure SQL Database](/azure/sql-database/sql-database-technical-overview) is a relational database service using the Microsoft SQL Server engine that supports table, JSON, spatial, and XML data.</span></span> 

<span data-ttu-id="c0989-107">Azure SQL Database를 시작하려면 [Azure SQL Database: Java를 사용하여 데이터 연결 및 쿼리](/azure/sql-database/sql-database-connect-query-java)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c0989-107">To get started with Azure SQL Database, see [Azure SQL Database: Use Java to connect and query data](/azure/sql-database/sql-database-connect-query-java).</span></span>

## <a name="client-jdbc-driver"></a><span data-ttu-id="c0989-108">클라이언트 JDBC 드라이버</span><span class="sxs-lookup"><span data-stu-id="c0989-108">Client JDBC driver</span></span>

<span data-ttu-id="c0989-109">[SQL Database JDBC 드라이버](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server)를 사용하여 응용 프로그램에서 Azure SQL Database에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c0989-109">Connect to Azure SQL Database from your applications using the [SQL Database JDBC driver](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server).</span></span> <span data-ttu-id="c0989-110">[Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/)를 사용하여 데이터베이스에 직접 연결하거나 [최대 절전 모드](http://hibernate.org/)와 같이 JDBC를 통해 데이터베이스와 상호 작용하는 데이터 액세스 프레임워크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c0989-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect with the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="c0989-111">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 JDBC 드라이버를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c0989-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="c0989-112">예</span><span class="sxs-lookup"><span data-stu-id="c0989-112">Example</span></span>

<span data-ttu-id="c0989-113">SQL 데이터베이스에 연결하고 JDBC를 사용하여 테이블의 모든 레코드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c0989-113">Connect to SQL database and select all records in a table using JDBC.</span></span>

```java
String connectionString = "jdbc:sqlserver://fabrikam.database.windows.net:1433;database=fiber;user=raisa;password=testpass;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
try {
    Connection conn = DriverManager.getConnection(connectionString);
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery("SELECT * FROM SALES");
}  
```

## <a name="management-api"></a><span data-ttu-id="c0989-114">관리 API</span><span class="sxs-lookup"><span data-stu-id="c0989-114">Management API</span></span>

<span data-ttu-id="c0989-115">관리 API를 사용하여 구독의 Azure SQL Database 리소스를 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="c0989-115">Create and manage Azure SQL Database resources in your subscription with the management API.</span></span>   

<span data-ttu-id="c0989-116">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c0989-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-sql</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c0989-117">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="c0989-117">Explore the Management APIs</span></span>](/java/api/overview/azure/sql/management)

### <a name="example"></a><span data-ttu-id="c0989-118">예</span><span class="sxs-lookup"><span data-stu-id="c0989-118">Example</span></span>

<span data-ttu-id="c0989-119">SQL Database 리소스를 만들고 방화벽 규칙을 사용하여 IP 주소 범위에 대한 액세스를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="c0989-119">Create a SQL Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlDbName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(resourceGroupName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    .withNewFirewallRule("172.16.0.0", "172.31.255.255")
                    .create();
```

## <a name="samples"></a><span data-ttu-id="c0989-120">샘플</span><span class="sxs-lookup"><span data-stu-id="c0989-120">Samples</span></span>

[!INCLUDE [java-sql-samples](../docs-ref-conceptual/includes/sql.md)]

<span data-ttu-id="c0989-121">앱에서 사용할 수 있는 [Azure SQL Database용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="c0989-121">Explore more [sample Java code for Azure SQL Database](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL) you can use in your apps.</span></span>