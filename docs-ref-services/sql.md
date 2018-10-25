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
ms.openlocfilehash: 75b31aa0ffd32707deb4b28f9912aa4c9d1e4d7c
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799789"
---
# <a name="azure-sql-database-libraries-for-java"></a>Java용 Azure SQL Database 라이브러리

## <a name="overview"></a>개요

[Azure SQL Database](/azure/sql-database/sql-database-technical-overview)는 테이블, JSON, 공간 및 XML 데이터를 지원하는 Microsoft SQL Server 엔진을 사용하는 관계형 데이터베이스 서비스입니다. 

Azure SQL Database를 시작하려면 [Azure SQL Database: Java를 사용하여 데이터 연결 및 쿼리](/azure/sql-database/sql-database-connect-query-java)를 참조하세요.

## <a name="client-jdbc-driver"></a>클라이언트 JDBC 드라이버

[SQL Database JDBC 드라이버](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server)를 사용하여 응용 프로그램에서 Azure SQL Database에 연결합니다. [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/)를 사용하여 데이터베이스에 직접 연결하거나 [최대 절전 모드](http://hibernate.org/)와 같이 JDBC를 통해 데이터베이스와 상호 작용하는 데이터 액세스 프레임워크를 사용할 수 있습니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 JDBC 드라이버를 사용합니다.


```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```   

### <a name="example"></a>예

SQL 데이터베이스에 연결하고 JDBC를 사용하여 테이블의 모든 레코드를 선택합니다.

```java
String connectionString = "jdbc:sqlserver://fabrikam.database.windows.net:1433;database=fiber;user=raisa;password=testpass;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
try {
    Connection conn = DriverManager.getConnection(connectionString);
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery("SELECT * FROM SALES");
}  
```

## <a name="management-api"></a>관리 API

관리 API를 사용하여 구독의 Azure SQL Database 리소스를 만들고 관리합니다.   

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-sql</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/java/api/overview/azure/sql/management)

### <a name="example"></a>예

SQL Database 리소스를 만들고 방화벽 규칙을 사용하여 IP 주소 범위에 대한 액세스를 제한합니다.

```java
SqlServer sqlServer = azure.sqlServers().define(sqlDbName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(resourceGroupName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    .withNewFirewallRule("172.16.0.0", "172.31.255.255")
                    .create();
```

## <a name="samples"></a>샘플

[!INCLUDE [java-sql-samples](../docs-ref-conceptual/includes/sql.md)]

앱에서 사용할 수 있는 [Azure SQL Database용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL)를 추가로 탐색합니다.