---
title: Azure SQL Database에서 Spring Data JPA를 사용하는 방법
description: Azure SQL 데이터베이스에서 Spring Data JPA를 사용하는 방법을 알아보세요.
services: sql-database
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: sql-database
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 02b6eff059c8b7dff1c7473d0460ca44e76f6f2e
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64673962"
---
# <a name="how-to-use-spring-data-jpa-with-azure-sql-database"></a><span data-ttu-id="ef5c8-103">Azure SQL Database에서 Spring Data JPA를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="ef5c8-103">How to use Spring Data JPA with Azure SQL Database</span></span>

## <a name="overview"></a><span data-ttu-id="ef5c8-104">개요</span><span class="sxs-lookup"><span data-stu-id="ef5c8-104">Overview</span></span>

<span data-ttu-id="ef5c8-105">이 문서는 [Spring Data]를 사용하는 샘플 애플리케이션을 만들어 [JPA(Java Persistence API)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm)를 사용하여 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)에서 정보를 저장 및 검색하는 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) using [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef5c8-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ef5c8-106">Prerequisites</span></span>

<span data-ttu-id="ef5c8-107">이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="ef5c8-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="ef5c8-109">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="ef5c8-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="ef5c8-110">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="ef5c8-111">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="ef5c8-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="ef5c8-112">[Curl](https://curl.haxx.se/) 또는 기능을 테스트하는 유사한 HTTP 유틸리티.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="ef5c8-113">[Git](https://git-scm.com/downloads) 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ef5c8-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="ef5c8-114">Azure SQL Database 만들기</span><span class="sxs-lookup"><span data-stu-id="ef5c8-114">Create an Azure SQL Database</span></span>

### <a name="create-a-sql-database-server-using-the-azure-portal"></a><span data-ttu-id="ef5c8-115">Azure Portal을 사용하여 SQL 데이터베이스 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="ef5c8-115">Create a SQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="ef5c8-116">Azure SQL 데이터베이스 만들기에 관한 자세한 정보는 [Azure portal에서 Azure SQL 데이터베이스 만들기](/azure/sql-database/sql-database-get-started-portal)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-116">You can read more detailed information about creating Azure SQL databases in [Create an Azure SQL database in the Azure portal](/azure/sql-database/sql-database-get-started-portal).</span></span>

1. <span data-ttu-id="ef5c8-117"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-117">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="ef5c8-118">**+리소스 만들기**를 클릭한 다음 **데이터베이스**를 클릭하고 **SQL Database**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-118">Click **+Create a resource**, then **Databases**, and then click **SQL Database**.</span></span>

   ![SQL 데이터베이스 만들기][SQL01]

1. <span data-ttu-id="ef5c8-120">다음 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-120">Specify the following information:</span></span>

   - <span data-ttu-id="ef5c8-121">**데이터베이스 이름**: SQL 데이터베이스의 고유명을 선택합니다. 이 고유명은 나중에 지정할 SQL 서버에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-121">**Database name**: Choose a unique name for your SQL database; this will be created in the SQL server that you will specify later.</span></span>
   - <span data-ttu-id="ef5c8-122">**구독**: 사용할 Azure 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-122">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="ef5c8-123">**리소스 그룹**: 새 리소스 그룹을 만들지 기존 리소스 그룹을 선택할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-123">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="ef5c8-124">**원본 선택**: 이 자습서에서는 `Blank database`를 선택하여 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-124">**Select source**: For this tutorial, select `Blank database` to create a new database.</span></span>

   ![SQL 데이터베이스 속성 지정하기][SQL02]
   
1. <span data-ttu-id="ef5c8-126">**서버**를 클릭한 다음 **새 서버 만들기**를 클릭하여 다음 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-126">Click **Server**, then **Create a new server**, and then specify the following information:</span></span>

   - <span data-ttu-id="ef5c8-127">**서버 이름**: SQL 서버의 고유명을 선택합니다. 이 고유명은 *wingtiptoyssql.database.windows.net* 같은 정규화된 도메인 이름을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-127">**Server name**: Choose a unique name for your SQL server; this will be used to create a fully-qualified domain name like *wingtiptoyssql.database.windows.net*.</span></span>
   - <span data-ttu-id="ef5c8-128">**서버 관리자 로그인**: 데이터베이스 관리자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-128">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="ef5c8-129">**암호** 및 **암호 확인**: 데이터베이스 관리자용 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-129">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="ef5c8-130">**위치**: 데이터베이스에 가장 가까운 Azure 지역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-130">**Location**: Specify the closest geographic region for your database.</span></span>

   ![SQL 서버 지정하기][SQL03]

1. <span data-ttu-id="ef5c8-132">위 정보를 모두 입력하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-132">When you have entered all of the above information, click **Select**.</span></span>

1. <span data-ttu-id="ef5c8-133">이 자습서에서는 가장 저렴한 **가격 책정 계층**을 지정한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-133">For this tutorial, specify the least-expensive **Pricing tier**, and then click **Create**.</span></span>

   ![SQL 데이터베이스 만들기][SQL04]

### <a name="configure-a-firewall-rule-for-your-sql-server-using-the-azure-portal"></a><span data-ttu-id="ef5c8-135">Azure Portal을 사용하여 SQL 서버용 방화벽 규칙 구성하기</span><span class="sxs-lookup"><span data-stu-id="ef5c8-135">Configure a firewall rule for your SQL server using the Azure Portal</span></span>

1. <span data-ttu-id="ef5c8-136"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-136">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="ef5c8-137">**모든 리소스**를 클릭한 다음, 방금 만든 SQL 서버를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-137">Click **All Resources**, then click the SQL server you just created.</span></span>

   ![SQL 서버 선택하기][SQL05]

1. <span data-ttu-id="ef5c8-139">**개요** 섹션에서 **방화벽 설정 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-139">In the **Overview** section, click **Show firewall settings**</span></span>

   ![방화벽 설정 표시하기][SQL06]

1. <span data-ttu-id="ef5c8-141">**방화벽 및 가상 네트워크** 섹션에서 규칙의 고유명을 지정하여 새 규칙을 만든 다음, 데이터베이스 액세스 권한이 필요한 IP 주소 범위를 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-141">In the **Firewalls and virtual networks** section, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![방화벽 설정 구성하기][SQL07]

### <a name="retrieve-the-connection-string-for-your-sql-server-using-the-azure-portal"></a><span data-ttu-id="ef5c8-143">Azure Portal을 사용하여 SQL 서버의 연결 문자열 검색하기</span><span class="sxs-lookup"><span data-stu-id="ef5c8-143">Retrieve the connection string for your SQL server using the Azure Portal</span></span>

1. <span data-ttu-id="ef5c8-144"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-144">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="ef5c8-145">**모든 리소스**를 클릭한 다음, 방금 만든 SQL 데이터베이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-145">Click **All Resources**, then click the SQL database you just created.</span></span>

   ![SQL 데이터베이스 선택하기][SQL08]

1. <span data-ttu-id="ef5c8-147">**연결 문자열**을 클릭한 다음 **JDBC**를 클릭하여 JDBC 텍스트 필드 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-147">Click **Connection strings**, then click **JDBC**, and copy the value in the JDBC text field.</span></span>

   ![JDBC 연결 문자열 검색하기][SQL09]

## <a name="configure-the-sample-application"></a><span data-ttu-id="ef5c8-149">샘플 애플리케이션 구성</span><span class="sxs-lookup"><span data-stu-id="ef5c8-149">Configure the sample application</span></span>

1. <span data-ttu-id="ef5c8-150">명령 셸을 열고 다음 예와 같이 git 명령을 사용하여 샘플 프로젝트를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-150">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="ef5c8-151">샘플 프로젝트의 *리소스* 디렉터리에서 *application.properties* 파일을 찾거나, 파일이 아직 없는 경우 해당 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-151">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="ef5c8-152">텍스트 편집기에서 *application.properties* 파일을 열어 파일에 다음 줄을 추가하거나 구성하고 샘플 값을 앞서 다룬 적절한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-152">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:sqlserver://wingtiptoyssql.database.windows.net:1433;database=wingtiptoys;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
   spring.datasource.username=wingtiptoysuser@wingtiptoyssql
   spring.datasource.password=********
    ```
   <span data-ttu-id="ef5c8-153">위치:</span><span class="sxs-lookup"><span data-stu-id="ef5c8-153">Where:</span></span>

   | <span data-ttu-id="ef5c8-154">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ef5c8-154">Parameter</span></span> | <span data-ttu-id="ef5c8-155">설명</span><span class="sxs-lookup"><span data-stu-id="ef5c8-155">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="ef5c8-156">이 문서에서 앞서 다룬 SQL JDBC 문자열의 편집 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-156">Specifies an edited version of your SQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="ef5c8-157">이 문서에서 앞서 다룬 SQL 관리자 이름을 축약된 서버 이름을 추가하여 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-157">Specifies your SQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="ef5c8-158">이 문서에서 앞서 다룬 SQL 관리자 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-158">Specifies your SQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="ef5c8-159">*application.properties* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-159">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="ef5c8-160">샘플 애플리케이션 패키지 및 테스트하기</span><span class="sxs-lookup"><span data-stu-id="ef5c8-160">Package and test the sample application</span></span> 

1. <span data-ttu-id="ef5c8-161">다음 예와 같이 Maven을 사용하여 샘플 애플리케이션을 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-161">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P sql
   ```

1. <span data-ttu-id="ef5c8-162">다음 예와 같이 샘플 애플리케이션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-162">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jpa-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="ef5c8-163">다음 예와 같이 명령 프롬프트에서 `curl`을 사용하여 새 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-163">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="ef5c8-164">애플리케이션이 다음과 같이 값을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-164">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="ef5c8-165">다음 예와 같이 명령 프롬프트에서 `curl`을 사용하여 모든 기존 레코드 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-165">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="ef5c8-166">애플리케이션이 다음과 같이 값을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-166">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="ef5c8-167">요약</span><span class="sxs-lookup"><span data-stu-id="ef5c8-167">Summary</span></span>

<span data-ttu-id="ef5c8-168">이 자습서에서는, Spring Data를 사용하는 Java 샘플 애플리케이션을 만들어 JPA를 사용하여 Azure SQL 데이터베이스에서 정보를 저장 및 검색했습니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-168">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure SQL database using JPA.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef5c8-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef5c8-169">Next steps</span></span>

<span data-ttu-id="ef5c8-170">Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-170">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ef5c8-171">Azure의 Spring</span><span class="sxs-lookup"><span data-stu-id="ef5c8-171">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="ef5c8-172">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ef5c8-172">Additional Resources</span></span>

<span data-ttu-id="ef5c8-173">Java와 함께 Azure를 사용하는 방법에 관한 자세한 정보는 [Java 개발자를 위한 Azure]와 [Azure DevOps 및 Java 사용하기]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef5c8-173">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<!-- URL List -->

[Java 개발자를 위한 Azure]: /java/azure/
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

[SQL01]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-01.png
[SQL02]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-02.png
[SQL03]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-03.png
[SQL04]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-04.png
[SQL05]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-05.png
[SQL06]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-06.png
[SQL07]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-07.png
[SQL08]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-08.png
[SQL09]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-09.png
