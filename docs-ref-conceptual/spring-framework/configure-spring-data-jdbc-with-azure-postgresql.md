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
ms.openlocfilehash: 371a8c686f7ad045443328d02a32a4e65af55981
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992337"
---
# <a name="how-to-use-spring-data-jdbc-with-azure-postgresql"></a><span data-ttu-id="de444-103">Azure PostgreSQL에서 Spring Data JDBC를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="de444-103">How to use Spring Data JDBC with Azure PostgreSQL</span></span>

## <a name="overview"></a><span data-ttu-id="de444-104">개요</span><span class="sxs-lookup"><span data-stu-id="de444-104">Overview</span></span>

<span data-ttu-id="de444-105">이 문서는 [Spring Data]를 사용하는 샘플 애플리케이션을 만들어 [JDBC(Java Database Connectivity)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/)를 사용하여 Azure [PostgreSQL]https://www.postgresql.org/ 데이터베이스에서 정보를 저장 및 검색하는 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="de444-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [PostgreSQL]https://www.postgresql.org/ database using [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de444-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="de444-106">Prerequisites</span></span>

<span data-ttu-id="de444-107">이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="de444-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de444-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="de444-109">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="de444-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="de444-110">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de444-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="de444-111">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="de444-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="de444-112">[Curl](https://curl.haxx.se/) 또는 기능을 테스트하는 유사한 HTTP 유틸리티.</span><span class="sxs-lookup"><span data-stu-id="de444-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="de444-113">[psql](https://www.postgresql.org/docs/current/app-psql.html) 명령줄 유틸리티.</span><span class="sxs-lookup"><span data-stu-id="de444-113">The [psql](https://www.postgresql.org/docs/current/app-psql.html) command-line utility.</span></span>
* <span data-ttu-id="de444-114">[Git](https://git-scm.com/downloads) 클라이언트</span><span class="sxs-lookup"><span data-stu-id="de444-114">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-postgresql-database-for-azure"></a><span data-ttu-id="de444-115">Azure용 PostgreSQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="de444-115">Create a PostgreSQL database for Azure</span></span>

### <a name="create-a-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="de444-116">Azure Portal을 사용하여 PostgreSQL 데이터베이스 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="de444-116">Create a PostgreSQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="de444-117">PostgreSQL 데이터베이스 만들기에 관한 자세한 정보는 [Azure portal을 사용하여 Azure Database for PostgreSQL 서버 만들기](/azure/postgresql/quickstart-create-server-database-portal)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de444-117">You can read more detailed information about creating PostgreSQL databases in [Create an Azure Database for PostgreSQL server by using the Azure portal](/azure/postgresql/quickstart-create-server-database-portal).</span></span>

1. <span data-ttu-id="de444-118"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-118">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="de444-119">**+리소스 만들기**를 클릭한 다음 **데이터베이스**를 클릭하고 **Azure Database for PostgreSQL**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-119">Click **+Create a resource**, then **Databases**, and then click **Azure Database for PostgreSQL**.</span></span>

   ![PostgreSQL 데이터베이스 만들기][POSTGRESQL01]

1. <span data-ttu-id="de444-121">다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-121">Enter the following information:</span></span>

   - <span data-ttu-id="de444-122">**서버 이름**: PostgreSQL 서버의 고유명을 선택합니다. 이 고유명은 *wingtiptoyspostgresql.postgres.database.azure.com* 같은 정규화된 도메인 이름을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="de444-122">**Server name**: Choose a unique name for your PostgreSQL server; this will be used to create a fully-qualified domain name like *wingtiptoyspostgresql.postgres.database.azure.com*.</span></span>
   - <span data-ttu-id="de444-123">**구독**: 사용할 Azure 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-123">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="de444-124">**리소스 그룹**: 새 리소스 그룹을 만들지 기존 리소스 그룹을 선택할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-124">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="de444-125">**원본 선택**: 이 자습서에서는 `Blank`를 선택하여 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="de444-125">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="de444-126">**서버 관리자 로그인**: 데이터베이스 관리자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-126">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="de444-127">**암호** 및 **암호 확인**: 데이터베이스 관리자용 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-127">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="de444-128">**위치**: 데이터베이스에 가장 가까운 Azure 지역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-128">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="de444-129">**버전**: 최신 데이터베이스 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-129">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="de444-130">**가격 책정 계층**: 이 자습서에서는 가장 저렴한 가격 책정 계층을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-130">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![PostgreSQL 데이터베이스 속성 만들기][POSTGRESQL02]

1. <span data-ttu-id="de444-132">위 정보를 모두 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-132">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="de444-133">Azure Portal을 사용하여 PostgreSQL 데이터베이스 서버용 방화벽 규칙 구성하기</span><span class="sxs-lookup"><span data-stu-id="de444-133">Configure a firewall rule for your PostgreSQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="de444-134"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-134">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="de444-135">**모든 리소스**를 클릭한 다음, 방금 만든 PostgreSQL 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-135">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![PostgreSQL 데이터베이스 선택하기][POSTGRESQL03]

1. <span data-ttu-id="de444-137">**연결 보안**을 클릭하고 **방화벽 규칙**에서 규칙의 고유명을 지정하여 새 규칙을 만든 다음, 데이터베이스 액세스 권한이 필요한 IP 주소 범위를 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-137">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![연결 보안 구성하기][POSTGRESQL04]

### <a name="retrieve-the-connection-string-for-your-postgresql-server-using-the-azure-portal"></a><span data-ttu-id="de444-139">Azure Portal을 사용하여 PostgreSQL 서버의 연결 문자열 검색하기</span><span class="sxs-lookup"><span data-stu-id="de444-139">Retrieve the connection string for your PostgreSQL server using the Azure Portal</span></span>

1. <span data-ttu-id="de444-140"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-140">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="de444-141">**모든 리소스**를 클릭한 다음, 방금 만든 PostgreSQL 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-141">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![PostgreSQL 데이터베이스 선택하기][POSTGRESQL03]

1. <span data-ttu-id="de444-143">**연결 문자열**을 클릭하고 **JDBC** 텍스트 필드 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-143">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![JDBC 연결 문자열 검색하기][POSTGRESQL05]

### <a name="create-postgresql-database-using-the-psql-command-line-utility"></a><span data-ttu-id="de444-145">`psql` 명령줄 유틸리티를 사용하여 PostgreSQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="de444-145">Create PostgreSQL database using the `psql` command-line utility</span></span>

1. <span data-ttu-id="de444-146">다음 예와 같이 `psql` 명령을 입력하여 명령 셸을 열고 PostgreSQL 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-146">Open a command shell and connect to your PostgreSQL server by entering a `psql` command like the following example:</span></span>

   ```shell
   psql --host=wingtiptoyspostgresql.postgres.database.azure.com --port=5432 --username=wingtiptoysuser@wingtiptoyspostgresql --dbname=postgres
   ```
   <span data-ttu-id="de444-147">위치:</span><span class="sxs-lookup"><span data-stu-id="de444-147">Where:</span></span>

   | <span data-ttu-id="de444-148">매개 변수</span><span class="sxs-lookup"><span data-stu-id="de444-148">Parameter</span></span> | <span data-ttu-id="de444-149">설명</span><span class="sxs-lookup"><span data-stu-id="de444-149">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="de444-150">이 문서에서 앞서 다룬 정규화된 PostgreSQL 서버 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-150">Specifies your fully qualified PostgreSQL server name from earlier in this article.</span></span> |
   | `host` | <span data-ttu-id="de444-151">PostgreSQL 서버 포트를 지정합니다(기본값 `5432`).</span><span class="sxs-lookup"><span data-stu-id="de444-151">Specifies the PostgreSQL server port, which is `5432` by default.</span></span> |
   | `username` | <span data-ttu-id="de444-152">이 문서에서 앞서 다룬 PostgreSQL 관리자와 축약된 서버 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-152">Specifies your PostgreSQL administrator and shortened server name from earlier in this article.</span></span> |
   | `dbname` | <span data-ttu-id="de444-153">이제 기본 `postgres` 데이터베이스를 사용하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-153">Specifies that you want to use the default `postgres` database for now.</span></span> |

   <span data-ttu-id="de444-154">PostgreSQL 서버가 다음 예와 같은 응답을 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-154">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   psql (9.3.24, server 10.5)
   SSL connection (cipher: ECDHE-RSA-AES256-SHA384, bits: 256)
   Type "help" for help.
   
   postgres=>
   ```

1. <span data-ttu-id="de444-155">다음 예와 같이 `psql` 명령을 입력하여 *mypgsqldb*라는 이름의 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="de444-155">Create a database named *mypgsqldb* by entering a `psql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mypgsqldb;
   ```

   <span data-ttu-id="de444-156">PostgreSQL 서버가 다음 예와 같은 응답을 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-156">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   CREATE DATABASE
   ```

1. <span data-ttu-id="de444-157">선택 사항: `psql`에 `\l`을 입력하여 데이터베이스가 만들어졌음을 확인할 수 있습니다. PostgreSQL 서버가 다음 예와 같이 응답해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-157">OPTIONAL: You can verify that your database was created by entering a `\l` at the `psql`; your PostgreSQL server should respond with something like the following example:</span></span>

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

1. <span data-ttu-id="de444-158">`\q`를 입력하여 `psql` 유틸리티를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-158">Enter `\q` to exit the `psql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="de444-159">샘플 애플리케이션 구성</span><span class="sxs-lookup"><span data-stu-id="de444-159">Configure the sample application</span></span>

1. <span data-ttu-id="de444-160">명령 셸을 열고 다음 예와 같이 git 명령을 사용하여 샘플 프로젝트를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-160">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="de444-161">샘플 프로젝트의 *리소스* 디렉터리에서 *application.properties* 파일을 찾거나, 파일이 아직 없는 경우 해당 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="de444-161">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="de444-162">텍스트 편집기에서 *application.properties* 파일을 열어 파일에 다음 줄을 추가하거나 구성하고 샘플 값을 앞서 다룬 적절한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="de444-162">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:postgresql://wingtiptoyspostgresql.postgres.database.azure.com:5432/mypgsqldb?ssl=true&sslmode=prefer
   spring.datasource.username=wingtiptoysuser@wingtiptoyspostgresql
   spring.datasource.password=********
    ```
   <span data-ttu-id="de444-163">위치:</span><span class="sxs-lookup"><span data-stu-id="de444-163">Where:</span></span>

   | <span data-ttu-id="de444-164">매개 변수</span><span class="sxs-lookup"><span data-stu-id="de444-164">Parameter</span></span> | <span data-ttu-id="de444-165">설명</span><span class="sxs-lookup"><span data-stu-id="de444-165">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="de444-166">이 문서에서 앞서 다룬 PostgreSQL JDBC 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-166">Specifies your PostgreSQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="de444-167">이 문서에서 앞서 다룬 PostgreSQL 관리자 이름을 축약된 서버 이름을 추가하여 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-167">Specifies your PostgreSQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="de444-168">이 문서에서 앞서 다룬 PostgreSQL 관리자 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-168">Specifies your PostgreSQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="de444-169">*application.properties* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="de444-169">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="de444-170">샘플 애플리케이션 패키지 및 테스트하기</span><span class="sxs-lookup"><span data-stu-id="de444-170">Package and test the sample application</span></span> 

1. <span data-ttu-id="de444-171">다음 예와 같이 Maven을 사용하여 샘플 애플리케이션을 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-171">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P postgresql
   ```

1. <span data-ttu-id="de444-172">다음 예와 같이 샘플 애플리케이션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-172">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="de444-173">다음 예와 같이 명령 프롬프트에서 `curl`을 사용하여 새 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="de444-173">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="de444-174">애플리케이션이 다음과 같이 값을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-174">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="de444-175">다음 예와 같이 명령 프롬프트에서 `curl`을 사용하여 모든 기존 레코드 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-175">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="de444-176">애플리케이션이 다음과 같이 값을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-176">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="de444-177">요약</span><span class="sxs-lookup"><span data-stu-id="de444-177">Summary</span></span>

<span data-ttu-id="de444-178">이 자습서에서는, Spring Data를 사용하는 Java 샘플 애플리케이션을 만들어 JDBC를 사용하여 Azure PostgreSQL 데이터베이스에서 정보를 저장 및 검색했습니다.</span><span class="sxs-lookup"><span data-stu-id="de444-178">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure PostgreSQL database using JDBC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de444-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="de444-179">Next steps</span></span>

<span data-ttu-id="de444-180">Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="de444-180">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="de444-181">Azure의 Spring</span><span class="sxs-lookup"><span data-stu-id="de444-181">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="de444-182">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="de444-182">Additional Resources</span></span>

<span data-ttu-id="de444-183">Java와 함께 Azure를 사용하는 방법에 관한 자세한 정보는 [Java 개발자용 Azure]와 [Azure DevOps 및 Java 사용하기]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de444-183">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<!-- URL List -->

[Java 개발자용 Azure]: /java/azure/
[Azure for Java Developers]: /java/azure/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Azure DevOps 및 Java 사용하기]: /azure/devops/
[Working with Azure DevOps and Java]: /azure/devops/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
