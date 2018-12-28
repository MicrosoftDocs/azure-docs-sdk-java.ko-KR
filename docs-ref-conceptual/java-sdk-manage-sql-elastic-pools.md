---
title: Java를 사용하여 SQL 데이터베이스 탄력적 풀 관리 | Microsoft Docs
description: Java용 Azure SDK를 사용하여 Azure SQL 데이터베이스를 만들고 구성하는 샘플 코드
author: rloutlaw
manager: douge
ms.assetid: 9b461de8-46bc-4650-8e9e-59531f4e2a53
ms.topic: article
ms.service: Azure
ms.devlang: java
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 9ec0cf3083b8659fa850b798ca0ecf18b2757234
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893574"
---
# <a name="manage-azure-sql-databases-in-elastic-pools-from-your-java-applications"></a><span data-ttu-id="9c050-103">Java 애플리케이션에서 탄력적 풀의 Azure SQL 데이터베이스 관리</span><span class="sxs-lookup"><span data-stu-id="9c050-103">Manage Azure SQL databases in elastic pools from your Java applications</span></span>

<span data-ttu-id="9c050-104">[이 샘플](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool)에서는 단일 계획에서 여러 데이터베이스의 리소스를 관리하고 크기 조정할 수 있는 [탄력적 풀](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)이 있는 SQL 데이터베이스 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-104">[This sample](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool) creates a SQL database server with an [elastic pool](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) to manage and scale resources for mulitple databases in a single plan.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="9c050-105">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="9c050-105">Run the sample</span></span>

<span data-ttu-id="9c050-106">[인증 파일](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md)을 만들고 컴퓨터에서 파일의 전체 경로가 포함된 `AZURE_AUTH_LOCATION` 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="9c050-107">그런 후 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool
cd sql-database-java-manage-sql-dbs-in-elastic-pool
mvn clean compile exec:java
```

<span data-ttu-id="9c050-108">[GitHub에서 전체 샘플 코드(영문)](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool)를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-108">[View the complete code sample on GitHub](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool)</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="9c050-109">Azure를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="9c050-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-sql-database-server-with-an-elastic-pool"></a><span data-ttu-id="9c050-110">탄력적 풀이 있는 SQL 데이터베이스 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="9c050-110">Create a SQL database server with an elastic pool</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    // Use ElasticPoolEditions.STANDARD as the edition
                    // and create two databases
                    .withNewElasticPool(elasticPoolName, ElasticPoolEditions.STANDARD, 
                        database1Name, database2Name)
                    .create();
```

<span data-ttu-id="9c050-111">현재 버전 값은 [ElasticPoolEditions 클래스 참조](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c050-111">See the [ElasticPoolEditions class reference](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) for current edition values.</span></span> <span data-ttu-id="9c050-112">버전 리소스 특성을 비교하려면 [SQL 데이터베이스 탄력적 풀 설명서](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-112">Review the [SQL database elastic pool documentation](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) to compare edition resource characteristics.</span></span> 

## <a name="change-database-transaction-unit-dtu-settings-in-an-elastic-pool"></a><span data-ttu-id="9c050-113">탄력적 풀의 DTU(데이터베이스 트랜잭션 단위) 설정 변경</span><span class="sxs-lookup"><span data-stu-id="9c050-113">Change Database Transaction Unit (DTU) settings in an elastic pool</span></span>

```java
// Set an pool of 200 eDTUs to share between the databases
// and ensure that a database always has 10 DTUs available but never uses more than 50
elasticPool = elasticPool.update()
                    .withDtu(200)
                    .withDatabaseDtuMin(10)
                    .withDatabaseDtuMax(50)
                    .apply();
```

<span data-ttu-id="9c050-114">SQL 데이터베이스에 리소스를 할당하는 방법에 대해 자세한 내용은 [DTU 및 eDTU 설명서](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-114">Review the [DTUs and eDTUs documentation](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu) to learn more about allocating resources to SQL databases.</span></span>

## <a name="create-a-new-database-and-add-it-to-an-elastic-pool"></a><span data-ttu-id="9c050-115">새 데이터베이스 만들기 및 탄력적 풀에 추가</span><span class="sxs-lookup"><span data-stu-id="9c050-115">Create a new database and add it to an elastic pool</span></span>

```java
// Add a newly created database to the elastic pool
SqlDatabase anotherDatabase = sqlServer.databases().define(anotherDatabaseName).create();
elasticPool.update().withExistingDatabase(anotherDatabase).apply();            
```

<span data-ttu-id="9c050-116">API에서 첫 번째 문의 [S0 계층](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers)에 `anotherDatabase`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-116">The API creates `anotherDatabase` at [S0 tier](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers) in the first statement.</span></span> <span data-ttu-id="9c050-117">`anotherDatabase`를 탄력적 풀로 이동하면 풀 설정에 따라 데이터베이스 리소스가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-117">Moving `anotherDatabase` to the elastic pool assigns the database resources based on the pool settings.</span></span>

## <a name="remove-a-database-from-an-elastic-pool"></a><span data-ttu-id="9c050-118">탄력적 풀에서 데이터베이스 제거</span><span class="sxs-lookup"><span data-stu-id="9c050-118">Remove a database from an elastic pool</span></span>
```java
// Assign an edition since the database resources are no longer managed in the pool 
anotherDatabase = anotherDatabase.update()
                     .withoutElasticPool()
                     .withEdition(DatabaseEditions.STANDARD)
                     .apply();
```

<span data-ttu-id="9c050-119">값을 `withEdition()`으로 전달하려면 [DatabaseEditions 클래스 참조](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c050-119">See the [DatabaseEditions class reference](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) for values to pass to `withEdition()`.</span></span>

## <a name="list-current-database-activities-in-an-elastic-pool"></a><span data-ttu-id="9c050-120">탄력적 풀의 현재 데이터베이스 작업 나열</span><span class="sxs-lookup"><span data-stu-id="9c050-120">List current database activities in an elastic pool</span></span>
```java
// get a list of in-flight elastic operations on databases in the pool and log them 
for (ElasticPoolDatabaseActivity databaseActivity : elasticPool.listDatabaseActivities()) {
    System.out.println("Database " + databaseActivity.databaseName() 
        + " performing operation " + databaseActivity.operation() + 
        " with objective " + databaseActivity.requestedServiceObjective());
}
```

<span data-ttu-id="9c050-121">데이터베이스 작업에는 탄력적 풀 내외로 데이터베이스를 이동하고 탄력적 풀에서 데이터베이스를 업데이트하는 작업이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-121">Database activities include moving a database in or out of an elastic pool and updating databases in an elastic pool.</span></span>


## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="9c050-122">탄력적 풀에 데이터베이스 나열</span><span class="sxs-lookup"><span data-stu-id="9c050-122">List databases in an elastic pool</span></span>
```java
// Log a list of databases in the elastic pool 
for (SqlDatabase databaseInServer : elasticPool.listDatabases()) {
    System.out.println(databaseInServer.name());
}
```

<span data-ttu-id="9c050-123">데이터베이스를 더 자세히 쿼리하려면 [com.microsoft.Azure.management.sql.SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database)에 있는 메서드를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-123">Review the methods in [com.microsoft.azure.management.sql.SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) to query the databases in more detail.</span></span>

## <a name="delete-an-elastic-pool"></a><span data-ttu-id="9c050-124">탄력적 풀 삭제</span><span class="sxs-lookup"><span data-stu-id="9c050-124">Delete an elastic pool</span></span>
```java
sqlServer.elasticPools().delete(elasticPoolName);
```

<span data-ttu-id="9c050-125">탄력적 풀은 삭제하기 전에 비어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-125">The elastic pool must be empty before deleting it.</span></span>

## <a name="sample-code-summary"></a><span data-ttu-id="9c050-126">샘플 코드 요약</span><span class="sxs-lookup"><span data-stu-id="9c050-126">Sample code summary.</span></span>

<span data-ttu-id="9c050-127">이 샘플에서는 단일 탄력적 풀에서 관리되는 두 개의 데이터베이스가 있는 SQL 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-127">The sample creates a SQL server with two databases managed in a single elasic pool.</span></span> <span data-ttu-id="9c050-128">탄력적 풀 리소스 제한을 업데이트한 다음 풀에 추가 데이터베이스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-128">The elastic pool resource limits are updated, then additional databases are added to the pool.</span></span> <span data-ttu-id="9c050-129">그런 다음 코드에서 탄력적 풀의 구성과 상태를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-129">The code then reads the elastic pool's configuration and state.</span></span> 

<span data-ttu-id="9c050-130">만든 리소스를 모두 삭제한 후에 샘플이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-130">The sample deletes all resources it created before exiting.</span></span>

| <span data-ttu-id="9c050-131">샘플에 사용되는 클래스</span><span class="sxs-lookup"><span data-stu-id="9c050-131">Class used in sample</span></span> | <span data-ttu-id="9c050-132">메모</span><span class="sxs-lookup"><span data-stu-id="9c050-132">Notes</span></span> |
|-------|-------|
| [<span data-ttu-id="9c050-133">SqlServer</span><span class="sxs-lookup"><span data-stu-id="9c050-133">SqlServer</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_server) | <span data-ttu-id="9c050-134">`azure.sqlServers().define()...create()` 흐름 체인으로 만든 Azure의 SQL DB 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-134">SQL DB server in Azure created by `azure.sqlServers().define()...create()` fluent chain.</span></span> <span data-ttu-id="9c050-135">탄력적 풀과 데이터베이스를 만들고 사용하는 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-135">Provides methods to create and work with elastic pools and databases.</span></span> 
| [<span data-ttu-id="9c050-136">SqlDatabase</span><span class="sxs-lookup"><span data-stu-id="9c050-136">SqlDatabase</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) | <span data-ttu-id="9c050-137">SQL 데이터베이스를 나타내는 클라이언트 쪽 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-137">Client side object representing a SQL database.</span></span> <span data-ttu-id="9c050-138">`sqlServer().define()...create()`를 통해 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-138">Created through `sqlServer().define()...create()`.</span></span> 
| [<span data-ttu-id="9c050-139">DatabaseEditions</span><span class="sxs-lookup"><span data-stu-id="9c050-139">DatabaseEditions</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) | <span data-ttu-id="9c050-140">탄력적 풀 외부에서 데이터베이스를 만들거나 이동할 때 데이터베이스 리소스를 설정하는 데 사용되는 정적 상수 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-140">Constant static fields used to set database resources when creating a database outside of an elastic pool or when moving a database out of an elastic pool</span></span>  
| [<span data-ttu-id="9c050-141">SqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="9c050-141">SqlElasticPool</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_elastic_pool) | <span data-ttu-id="9c050-142">Azure에서 SqlServer를 만든 흐름 체인의 `withNewElasticPool()` 섹션에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-142">Created from the `withNewElasticPool()` section of the fluent chain that created the SqlServer in Azure.</span></span> <span data-ttu-id="9c050-143">탄력적 풀 및 탄력적 풀 자체에서 실행 중인 데이터베이스에 대한 리소스 제한을 설정하는 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-143">Provides methods to set resource limits for databases running in the elastic pool and for the elastic pool itself.</span></span> 
| [<span data-ttu-id="9c050-144">ElasticPoolEditions</span><span class="sxs-lookup"><span data-stu-id="9c050-144">ElasticPoolEditions</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) | <span data-ttu-id="9c050-145">탄력적 풀에 사용할 수 있는 리소스를 정의하는 상수 필드의 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-145">Class of constant fields defining the resources available to an elastic pool.</span></span> <span data-ttu-id="9c050-146">계층에 대한 자세한 내용은 [SQL 데이터베이스 탄력적 풀 설명서](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c050-146">See [SQL database elastic pool documentation](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) for tier details.</span></span> 
| [<span data-ttu-id="9c050-147">ElasticPoolDatabaseActivity</span><span class="sxs-lookup"><span data-stu-id="9c050-147">ElasticPoolDatabaseActivity</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_database_activity) | <span data-ttu-id="9c050-148">`SqlElasticPool.listDatabaseActivities()`에서 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-148">Retreived from `SqlElasticPool.listDatabaseActivities()`.</span></span> <span data-ttu-id="9c050-149">이 형식의 각 개체는 탄력적 풀의 데이터베이스에서 수행된 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-149">Each object of this type represents an activity performed on a database in the elastic pool.</span></span>
| [<span data-ttu-id="9c050-150">ElasticPoolActivity</span><span class="sxs-lookup"><span data-stu-id="9c050-150">ElasticPoolActivity</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_activity) | <span data-ttu-id="9c050-151">`SqlElasticPool.listActivities()`의 목록에서 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-151">Retrieved in a List from `SqlElasticPool.listActivities()`.</span></span> <span data-ttu-id="9c050-152">목록의 각 개체는 탄력적 풀(탄력적 풀의 데이터베이스가 아님)에서 수행된 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9c050-152">Each of object in the list represents an activity performed on the elastic pool (not the databases in the elastic pool).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c050-153">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9c050-153">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]