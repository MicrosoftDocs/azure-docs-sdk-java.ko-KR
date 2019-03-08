---
title: Azure PostgreSQL에서 Spring Data JDBC를 사용하는 방법
description: Azure PostgreSQL 데이터베이스에서 Spring Data JDBC를 사용하는 방법을 알아보세요.
services: postgresql
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: postgresql
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 29f3c957dd0ccd754eedef12e3fc01c3484dddf3
ms.sourcegitcommit: 1c1412ad5d8960975c3fc7fd3d1948152ef651ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57335396"
---
# <a name="how-to-use-spring-data-jdbc-with-azure-postgresql"></a>Azure PostgreSQL에서 Spring Data JDBC를 사용하는 방법

## <a name="overview"></a>개요

이 문서는 [Spring Data]를 사용하는 샘플 애플리케이션을 만들어 [JDBC(Java Database Connectivity)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/)를 사용하여 Azure [PostgreSQL](https://www.postgresql.org/) 데이터베이스에서 정보를 저장 및 검색하는 것을 보여줍니다.

## <a name="prerequisites"></a>필수 조건

이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.
* 지원되는 JDK(Java Development Kit) Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.
* [Apache Maven](http://maven.apache.org/), 버전 3.0 이상
* [Curl](https://curl.haxx.se/) 또는 기능을 테스트하는 유사한 HTTP 유틸리티.
* [psql](https://www.postgresql.org/docs/current/app-psql.html) 명령줄 유틸리티.
* [Git](https://git-scm.com/downloads) 클라이언트

## <a name="create-a-postgresql-database-for-azure"></a>Azure용 PostgreSQL 데이터베이스 만들기

### <a name="create-a-postgresql-database-server-using-the-azure-portal"></a>Azure Portal을 사용하여 PostgreSQL 데이터베이스 서버 만들기

> [!NOTE]
> 
> PostgreSQL 데이터베이스 만들기에 관한 자세한 정보는 [Azure portal을 사용하여 Azure Database for PostgreSQL 서버 만들기](/azure/postgresql/quickstart-create-server-database-portal)에서 확인할 수 있습니다.

1. <https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.

1. **+리소스 만들기**를 클릭한 다음 **데이터베이스**를 클릭하고 **Azure Database for PostgreSQL**을 클릭합니다.

   ![PostgreSQL 데이터베이스 만들기][POSTGRESQL01]

1. 다음 정보를 입력합니다.

   - **서버 이름**: PostgreSQL 서버의 고유명을 선택합니다. 이 고유명은 *wingtiptoyspostgresql.postgres.database.azure.com* 같은 정규화된 도메인 이름을 만드는 데 사용됩니다.
   - **구독**: 사용할 Azure 구독을 지정합니다.
   - **리소스 그룹**: 새 리소스 그룹을 만들지 기존 리소스 그룹을 선택할지를 지정합니다.
   - **원본 선택**: 이 자습서에서는 `Blank`를 선택하여 새 데이터베이스를 만듭니다.
   - **서버 관리자 로그인**: 데이터베이스 관리자 이름을 지정합니다.
   - **암호** 및 **암호 확인**: 데이터베이스 관리자용 암호를 지정합니다.
   - **위치**: 데이터베이스에 가장 가까운 Azure 지역을 지정합니다.
   - **버전**: 최신 데이터베이스 버전을 지정합니다.
   - **가격 책정 계층**: 이 자습서에서는 가장 저렴한 가격 책정 계층을 지정합니다.

   ![PostgreSQL 데이터베이스 속성 만들기][POSTGRESQL02]

1. 위 정보를 모두 입력하고 **만들기**를 클릭합니다.

### <a name="configure-a-firewall-rule-for-your-postgresql-database-server-using-the-azure-portal"></a>Azure Portal을 사용하여 PostgreSQL 데이터베이스 서버용 방화벽 규칙 구성하기

1. <https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.

1. **모든 리소스**를 클릭한 다음, 방금 만든 PostgreSQL 데이터베이스를 클릭합니다.

   ![PostgreSQL 데이터베이스 선택하기][POSTGRESQL03]

1. **연결 보안**을 클릭하고 **방화벽 규칙**에서 규칙의 고유명을 지정하여 새 규칙을 만든 다음, 데이터베이스 액세스 권한이 필요한 IP 주소 범위를 입력하고 **저장**을 클릭합니다.

   ![연결 보안 구성하기][POSTGRESQL04]

### <a name="retrieve-the-connection-string-for-your-postgresql-server-using-the-azure-portal"></a>Azure Portal을 사용하여 PostgreSQL 서버의 연결 문자열 검색하기

1. <https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.

1. **모든 리소스**를 클릭한 다음, 방금 만든 PostgreSQL 데이터베이스를 클릭합니다.

   ![PostgreSQL 데이터베이스 선택하기][POSTGRESQL03]

1. **연결 문자열**을 클릭하고 **JDBC** 텍스트 필드 값을 복사합니다.

   ![JDBC 연결 문자열 검색하기][POSTGRESQL05]

### <a name="create-postgresql-database-using-the-psql-command-line-utility"></a>`psql` 명령줄 유틸리티를 사용하여 PostgreSQL 데이터베이스 만들기

1. 다음 예와 같이 `psql` 명령을 입력하여 명령 셸을 열고 PostgreSQL 서버에 연결합니다.

   ```shell
   psql --host=wingtiptoyspostgresql.postgres.database.azure.com --port=5432 --username=wingtiptoysuser@wingtiptoyspostgresql --dbname=postgres
   ```
   위치:

   | 매개 변수 | 설명 |
   |---|---|
   | `host` | 이 문서에서 앞서 다룬 정규화된 PostgreSQL 서버 이름을 지정합니다. |
   | `host` | PostgreSQL 서버 포트를 지정합니다(기본값 `5432`). |
   | `username` | 이 문서에서 앞서 다룬 PostgreSQL 관리자와 축약된 서버 이름을 지정합니다. |
   | `dbname` | 이제 기본 `postgres` 데이터베이스를 사용하도록 지정합니다. |

   PostgreSQL 서버가 다음 예와 같은 응답을 보여야 합니다.

   ```shell
   psql (9.3.24, server 10.5)
   SSL connection (cipher: ECDHE-RSA-AES256-SHA384, bits: 256)
   Type "help" for help.
   
   postgres=>
   ```

1. 다음 예와 같이 `psql` 명령을 입력하여 *mypgsqldb*라는 이름의 데이터베이스를 만듭니다.

   ```SQL
   CREATE DATABASE mypgsqldb;
   ```

   PostgreSQL 서버가 다음 예와 같은 응답을 보여야 합니다.

   ```shell
   CREATE DATABASE
   ```

1. 선택 사항: `psql`에 `\l`을 입력하여 데이터베이스가 만들어졌음을 확인할 수 있습니다. PostgreSQL 서버가 다음 예와 같이 응답해야 합니다.

   ```shell
                   List of databases
          Name        |      Owner      | Encoding
   -------------------+-----------------+----------
    azure_maintenance | azure_superuser | UTF8
    azure_sys         | azure_superuser | UTF8
    mypgsqldb         | wingtiptoysuser | UTF8
    postgres          | azure_superuser | UTF8
    template0         | azure_superuser | UTF8
    template1         | azure_superuser | UTF8
   (6 rows)
   ```

1. `\q`를 입력하여 `psql` 유틸리티를 종료합니다.

## <a name="configure-the-sample-application"></a>샘플 애플리케이션 구성

1. 명령 셸을 열고 다음 예와 같이 git 명령을 사용하여 샘플 프로젝트를 복제합니다.

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. 샘플 프로젝트의 *리소스* 디렉터리에서 *application.properties* 파일을 찾거나, 파일이 아직 없는 경우 해당 파일을 만듭니다.

1. 텍스트 편집기에서 *application.properties* 파일을 열어 파일에 다음 줄을 추가하거나 구성하고 샘플 값을 앞서 다룬 적절한 값으로 바꿉니다.

   ```yaml
   spring.datasource.url=jdbc:postgresql://wingtiptoyspostgresql.postgres.database.azure.com:5432/mypgsqldb?ssl=true&sslmode=prefer
   spring.datasource.username=wingtiptoysuser@wingtiptoyspostgresql
   spring.datasource.password=********
    ```
   위치:

   | 매개 변수 | 설명 |
   |---|---|
   | `spring.datasource.url` | 이 문서에서 앞서 다룬 PostgreSQL JDBC 문자열을 지정합니다. |
   | `spring.datasource.username` | 이 문서에서 앞서 다룬 PostgreSQL 관리자 이름을 축약된 서버 이름을 추가하여 지정합니다. |
   | `spring.datasource.password` | 이 문서에서 앞서 다룬 PostgreSQL 관리자 암호를 지정합니다. |

1. *application.properties* 파일을 저장하고 닫습니다.

## <a name="package-and-test-the-sample-application"></a>샘플 애플리케이션 패키지 및 테스트하기 

1. 다음 예와 같이 Maven을 사용하여 샘플 애플리케이션을 컴파일합니다.

   ```shell
   mvn clean package -P postgresql
   ```

1. 다음 예와 같이 샘플 애플리케이션을 시작합니다.

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. 다음 예와 같이 명령 프롬프트에서 `curl`을 사용하여 새 레코드를 만듭니다.

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   애플리케이션이 다음과 같이 값을 반환해야 합니다.

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. 다음 예와 같이 명령 프롬프트에서 `curl`을 사용하여 모든 기존 레코드 검색합니다.

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   애플리케이션이 다음과 같이 값을 반환해야 합니다.

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a>요약

이 자습서에서는, Spring Data를 사용하는 Java 샘플 애플리케이션을 만들어 JDBC를 사용하여 Azure PostgreSQL 데이터베이스에서 정보를 저장 및 검색했습니다.

## <a name="next-steps"></a>다음 단계

Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.

> [!div class="nextstepaction"]
> [Azure의 Spring](/java/azure/spring-framework)

### <a name="additional-resources"></a>추가 리소스

Java와 함께 Azure를 사용하는 방법에 관한 자세한 정보는 [Java 개발자를 위한 Azure]와 [Azure DevOps 및 Java 사용하기]를 참조하세요.

<!-- URL List -->

[Java 개발자를 위한 Azure]: /java/azure/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Azure DevOps 및 Java 사용하기]: /azure/devops/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Data]: https://spring.io/projects/spring-data
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[POSTGRESQL01]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-01.png
[POSTGRESQL02]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-02.png
[POSTGRESQL03]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-03.png
[POSTGRESQL04]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-04.png
[POSTGRESQL05]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-05.png
