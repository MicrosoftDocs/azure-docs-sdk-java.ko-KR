---
title: "Java용 Azure Database for MySQL 라이브러리"
description: "Java용 Azure Database for MySQL 클라이언트 라이브러리에 대한 참조 설명서"
keywords: "Azure, Java, SDK, API, SQL, 데이터베이스, PostGres, MySQL"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: mysql
ms.openlocfilehash: 72c94ef4bdad7adeae63da2efda93b52a9afef53
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-database-for-mysql-libraries-for-java"></a>Java용 Azure Database for MySQL 라이브러리

## <a name="overview"></a>개요

[Azure Database for MySQL](/azure/sql-database/sql-database-technical-overview)은 [MySQL](https://www.mysql.com/) 오픈 소스 서버 엔진을 기반으로 하는 관계형 데이터베이스 서비스입니다. 

Azure Database for MySQL을 시작하려면 [Java를 사용하여 데이터 연결 및 쿼리](/azure/mysql/connect-java)를 참조하세요.

## <a name="client-jbdc-driver"></a>클라이언트 JBDC 드라이버

[MySQL JDBC 드라이버](https://dev.mysql.com/downloads/connector/j/) 오픈 소스를 사용하여 응용 프로그램에서 Azure Database for MySQL에 연결합니다. [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/)를 사용하여 데이터베이스에 직접 연결하거나 [최대 절전 모드](http://hibernate.org/)와 같이 JDBC를 통해 데이터베이스와 상호 작용하는 데이터 액세스 프레임워크를 사용할 수 있습니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 JDBC 드라이버를 사용합니다.  

```XML
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.42</version>
</dependency>
```   

## <a name="example"></a>예제

JDBC를 사용하여 Azure Database for MySQL에 연결하고 sales 테이블의 모든 레코드를 선택합니다. Azure Portal에서 데이터베이스에 대한 JDBC 연결 문자열을 가져올 수 있습니다.

```java
String url = String.format("jdbc:mysql://fabrikamysql.mysql.database.azure.com:3306/fabrikamdb?verifyServerCertificate=true&useSSL=true&requireSSL=false");
try {
    Connection conn = DriverManager.getConnection(url, "frank@fabrikamysql", "aBcDeFgHiJkL");
    String selectSql = "SELECT * FROM SALES";
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a>샘플

[Java 및 MySQL 웹앱 빌드](/azure/app-service-web/app-service-web-tutorial-java-mysql)   
[Azure CLI를 사용하여 MySQL 데이터베이스 디자인](/azure/mysql/tutorial-design-database-using-cli)   

앱에서 사용할 수 있는 [Azure Database for MySQL용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql)를 추가로 탐색합니다.
