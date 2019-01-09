---
title: Azure MySQL에서 Spring Data JPA를 사용하는 방법
description: Azure MySQL 데이터베이스에서 Spring Data JPA를 사용하는 방법을 알아보세요.
services: mysql
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: mysql
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 95dfc292d8f6d7e03d396afd7da4cfff0bd05b1b
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992409"
---
# <a name="how-to-use-spring-data-jpa-with-azure-mysql"></a><span data-ttu-id="f8940-103">Azure MySQL에서 Spring Data JPA를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="f8940-103">How to use Spring Data JPA with Azure MySQL</span></span>

## <a name="overview"></a><span data-ttu-id="f8940-104">개요</span><span class="sxs-lookup"><span data-stu-id="f8940-104">Overview</span></span>

<span data-ttu-id="f8940-105">이 문서는 [Spring Data]를 사용하는 샘플 애플리케이션을 만들어 [JPA(Java Persistence API)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm)를 사용하여 Azure [MySQL](https://www.mysql.com/) 데이터베이스에서 정보를 저장 및 검색하는 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [MySQL](https://www.mysql.com/) database using [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8940-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f8940-106">Prerequisites</span></span>

<span data-ttu-id="f8940-107">이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="f8940-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="f8940-109">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="f8940-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="f8940-110">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8940-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="f8940-111">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="f8940-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="f8940-112">[Curl](https://curl.haxx.se/) 또는 기능을 테스트하는 유사한 HTTP 유틸리티.</span><span class="sxs-lookup"><span data-stu-id="f8940-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="f8940-113">[mysql](https://dev.mysql.com/downloads/) 명령줄 유틸리티.</span><span class="sxs-lookup"><span data-stu-id="f8940-113">The [mysql](https://dev.mysql.com/downloads/) command-line utility.</span></span>
* <span data-ttu-id="f8940-114">[Git](https://git-scm.com/downloads) 클라이언트</span><span class="sxs-lookup"><span data-stu-id="f8940-114">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-mysql-database-for-azure"></a><span data-ttu-id="f8940-115">Azure용 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="f8940-115">Create a MySQL database for Azure</span></span>

### <a name="create-a-mysql-database-server-using-the-azure-portal"></a><span data-ttu-id="f8940-116">Azure Portal을 사용하여 MySQL 데이터베이스 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="f8940-116">Create a MySQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="f8940-117">MySQL 데이터베이스 만들기에 관한 자세한 정보는 [Azure portal을 사용하여 Azure Database for MySQL 서버 만들기](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-117">You can read more detailed information about creating MySQL databases in [Create an Azure Database for MySQL server by using the Azure portal](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span></span>

1. <span data-ttu-id="f8940-118"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-118">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="f8940-119">**+리소스 만들기**를 클릭한 다음 **데이터베이스**를 클릭하고 **Azure Database for MySQL**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-119">Click **+Create a resource**, then **Databases**, and then click **Azure Database for MySQL**.</span></span>

   ![MySQL 데이터베이스 만들기][MYSQL01]

1. <span data-ttu-id="f8940-121">다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-121">Enter the following information:</span></span>

   - <span data-ttu-id="f8940-122">**서버 이름**: MySQL 서버의 고유명을 선택합니다. 이 고유명은 *wingtiptoysmysql.mysql.database.azure.com* 같은 정규화된 도메인 이름을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-122">**Server name**: Choose a unique name for your MySQL server; this will be used to create a fully-qualified domain name like *wingtiptoysmysql.mysql.database.azure.com*.</span></span>
   - <span data-ttu-id="f8940-123">**구독**: 사용할 Azure 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-123">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="f8940-124">**리소스 그룹**: 새 리소스 그룹을 만들지 기존 리소스 그룹을 선택할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-124">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="f8940-125">**원본 선택**: 이 자습서에서는 `Blank`를 선택하여 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-125">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="f8940-126">**서버 관리자 로그인**: 데이터베이스 관리자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-126">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="f8940-127">**암호** 및 **암호 확인**: 데이터베이스 관리자용 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-127">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="f8940-128">**위치**: 데이터베이스에 가장 가까운 Azure 지역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-128">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="f8940-129">**버전**: 최신 데이터베이스 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-129">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="f8940-130">**가격 책정 계층**: 이 자습서에서는 가장 저렴한 가격 책정 계층을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-130">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![MySQL 데이터베이스 속성 만들기][MYSQL02]

1. <span data-ttu-id="f8940-132">위 정보를 모두 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-132">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-mysql-database-server-using-the-azure-portal"></a><span data-ttu-id="f8940-133">Azure Portal을 사용하여 MySQL 데이터베이스 서버용 방화벽 규칙 구성하기</span><span class="sxs-lookup"><span data-stu-id="f8940-133">Configure a firewall rule for your MySQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="f8940-134"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-134">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="f8940-135">**모든 리소스**를 클릭한 다음, 방금 만든 MySQL 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-135">Click **All Resources**, then click the MySQL database you just created.</span></span>

   ![MySQL 데이터베이스 선택하기][MYSQL03]

1. <span data-ttu-id="f8940-137">**연결 보안**을 클릭하고 **방화벽 규칙**에서 규칙의 고유명을 지정하여 새 규칙을 만든 다음, 데이터베이스 액세스 권한이 필요한 IP 주소 범위를 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-137">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![연결 보안 구성하기][MYSQL04]

### <a name="retrieve-the-connection-string-for-your-mysql-server-using-the-azure-portal"></a><span data-ttu-id="f8940-139">Azure Portal을 사용하여 MySQL 서버의 연결 문자열 검색하기</span><span class="sxs-lookup"><span data-stu-id="f8940-139">Retrieve the connection string for your MySQL server using the Azure Portal</span></span>

1. <span data-ttu-id="f8940-140"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-140">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="f8940-141">**모든 리소스**를 클릭한 다음, 방금 만든 MySQL 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-141">Click **All Resources**, then click the MySQL database you just created.</span></span>

   ![MySQL 데이터베이스 선택하기][MYSQL03]

1. <span data-ttu-id="f8940-143">**연결 문자열**을 클릭하고 **JDBC** 텍스트 필드 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-143">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![JDBC 연결 문자열 검색하기][MYSQL05]

### <a name="create-mysql-database-using-the-mysql-command-line-utility"></a><span data-ttu-id="f8940-145">`mysql` 명령줄 유틸리티를 사용하여 MySQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="f8940-145">Create MySQL database using the `mysql` command-line utility</span></span>

1. <span data-ttu-id="f8940-146">다음 예와 같이 `mysql` 명령을 입력하여 명령 셸을 열고 MySQL 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-146">Open a command shell and connect to your MySQL server by entering a `mysql` command like the following example:</span></span>

   ```shell
   mysql --host wingtiptoysmysql.mysql.database.azure.com --user wingtiptoysuser@wingtiptoysmysql -p
   ```
   <span data-ttu-id="f8940-147">위치:</span><span class="sxs-lookup"><span data-stu-id="f8940-147">Where:</span></span>

   | <span data-ttu-id="f8940-148">매개 변수</span><span class="sxs-lookup"><span data-stu-id="f8940-148">Parameter</span></span> | <span data-ttu-id="f8940-149">설명</span><span class="sxs-lookup"><span data-stu-id="f8940-149">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="f8940-150">이 문서에서 앞서 다룬 정규화된 MySQL 서버 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-150">Specifies your fully qualified MySQL server name from earlier in this article.</span></span> |
   | `user` | <span data-ttu-id="f8940-151">이 문서에서 앞서 다룬 MySQL 관리자와 축약된 서버 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-151">Specifies your MySQL administrator and shortened server name from earlier in this article.</span></span> |
   | `p` | <span data-ttu-id="f8940-152">암호 관련 메시지가 나타날 때까지 대기하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-152">Specifies to wait until prompted for a password.</span></span> |


   <span data-ttu-id="f8940-153">MySQL 서버가 다음 예와 같은 응답을 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-153">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   Welcome to the MySQL monitor.  Commands end with ; or \g.
   Your MySQL connection id is 64552
   Server version: 5.6.39.0 MySQL Community Server (GPL)
   
   Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.
   
   Oracle is a registered trademark of Oracle Corporation and/or its
   affiliates. Other names may be trademarks of their respective
   owners.
   
   Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
   
   mysql>
   ```

1. <span data-ttu-id="f8940-154">다음 예와 같이 `mysql` 명령을 입력하여 *mysqldb*라는 이름의 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-154">Create a database named *mysqldb* by entering a `mysql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mysqldb;
   ```

   <span data-ttu-id="f8940-155">MySQL 서버가 다음 예와 같은 응답을 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-155">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   Query OK, 1 row affected (0.30 sec)
   ```

1. <span data-ttu-id="f8940-156">선택 사항: 다음 예와 같이 `mysql` 명령을 입력하여 데이터베이스가 만들어졌음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-156">OPTIONAL: You can verify that your database was created by entering a `mysql` command like the following example:</span></span>

   ```SQL
   SHOW DATABASES;
   ```

   <span data-ttu-id="f8940-157">MySQL 서버가 다음 예와 같은 응답을 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-157">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   +--------------------+
   | Database           |
   +--------------------+
   | information_schema |
   | mysql              |
   | mysqldb            |
   | performance_schema |
   | sys                |
   +--------------------+
   ```

1. <span data-ttu-id="f8940-158">`\q`를 입력하여 `mysql` 유틸리티를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-158">Enter `\q` to exit the `mysql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="f8940-159">샘플 애플리케이션 구성</span><span class="sxs-lookup"><span data-stu-id="f8940-159">Configure the sample application</span></span>

1. <span data-ttu-id="f8940-160">명령 셸을 열고 다음 예와 같이 git 명령을 사용하여 샘플 프로젝트를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-160">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jpa-on-azure.git
   ```

1. <span data-ttu-id="f8940-161">샘플 프로젝트의 *리소스* 디렉터리에서 *application.properties* 파일을 찾거나, 파일이 아직 없는 경우 해당 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-161">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="f8940-162">텍스트 편집기에서 *application.properties* 파일을 열어 파일에 다음 줄을 추가하거나 구성하고 샘플 값을 앞서 다룬 적절한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-162">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.jpa.database-platform=org.hibernate.dialect.MySQL5InnoDBDialect
   spring.datasource.url=jdbc:mysql://wingtiptoysmysql.mysql.database.azure.com:3306/mysqldb?useSSL=true&requireSSL=false
   spring.datasource.username=wingtiptoysuser@wingtiptoysmysql
   spring.datasource.password=********
    ```
   <span data-ttu-id="f8940-163">위치:</span><span class="sxs-lookup"><span data-stu-id="f8940-163">Where:</span></span>

   | <span data-ttu-id="f8940-164">매개 변수</span><span class="sxs-lookup"><span data-stu-id="f8940-164">Parameter</span></span> | <span data-ttu-id="f8940-165">설명</span><span class="sxs-lookup"><span data-stu-id="f8940-165">Description</span></span> |
   |---|---|
   | `spring.jpa.database-platform` | <span data-ttu-id="f8940-166">JPA 데이터베이스 플랫폼을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-166">Specifies the JPA database platform.</span></span> |
   | `spring.datasource.url` | <span data-ttu-id="f8940-167">이 문서에서 앞서 다룬 MySQL JDBC 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-167">Specifies your MySQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="f8940-168">이 문서에서 앞서 다룬 MySQL 관리자 이름을 축약된 서버 이름을 추가하여 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-168">Specifies your MySQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="f8940-169">이 문서에서 앞서 다룬 MySQL 관리자 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-169">Specifies your MySQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="f8940-170">*application.properties* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-170">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="f8940-171">샘플 애플리케이션 패키지 및 테스트하기</span><span class="sxs-lookup"><span data-stu-id="f8940-171">Package and test the sample application</span></span> 

1. <span data-ttu-id="f8940-172">다음 예와 같이 Maven을 사용하여 샘플 애플리케이션을 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-172">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P mysql
   ```

1. <span data-ttu-id="f8940-173">다음 예와 같이 샘플 애플리케이션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-173">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jpa-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="f8940-174">다음 예와 같이 명령 프롬프트에서 `curl`을 사용하여 새 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-174">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="f8940-175">애플리케이션이 다음과 같이 값을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-175">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="f8940-176">다음 예와 같이 명령 프롬프트에서 `curl`을 사용하여 모든 기존 레코드 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-176">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="f8940-177">애플리케이션이 다음과 같이 값을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-177">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="f8940-178">요약</span><span class="sxs-lookup"><span data-stu-id="f8940-178">Summary</span></span>

<span data-ttu-id="f8940-179">이 자습서에서는, Spring Data를 사용하는 Java 샘플 애플리케이션을 만들어 JPA를 사용하여 Azure MySQL 데이터베이스에서 정보를 저장 및 검색했습니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-179">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure MySQL database using JPA.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8940-180">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f8940-180">Next steps</span></span>

<span data-ttu-id="f8940-181">Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="f8940-181">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f8940-182">Azure의 Spring</span><span class="sxs-lookup"><span data-stu-id="f8940-182">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="f8940-183">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f8940-183">Additional Resources</span></span>

<span data-ttu-id="f8940-184">Java와 함께 Azure를 사용하는 방법에 관한 자세한 정보는 [Java 개발자용 Azure]와 [Azure DevOps 및 Java 사용하기]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8940-184">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[MYSQL01]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-01.png
[MYSQL02]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-02.png
[MYSQL03]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-03.png
[MYSQL04]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-04.png
[MYSQL05]: media/configure-spring-data-jpa-with-azure-mysql/create-mysql-05.png
