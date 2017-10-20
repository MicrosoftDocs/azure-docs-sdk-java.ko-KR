---
title: "Java용 Azure Data Lake Analytics 라이브러리"
description: "Java용 Data Lake Analytics 라이브러리에 대한 참조 설명서"
keywords: "Azure, Java, SDK, API, 빅 데이터, Data Lake"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: 70cfe1417d460172df0cb753d2b719a635978ca8
ms.sourcegitcommit: 4b63ecd2c92a9115dfae018618e4e4046b061b3e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2017
---
# <a name="azure-data-lake-analytics-libraries-for-java"></a><span data-ttu-id="d8f0a-104">Java용 Azure Data Lake Analytics 라이브러리</span><span class="sxs-lookup"><span data-stu-id="d8f0a-104">Azure Data Lake Analytics libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="d8f0a-105">개요</span><span class="sxs-lookup"><span data-stu-id="d8f0a-105">Overview</span></span>

<span data-ttu-id="d8f0a-106">[Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview)를 사용하여 대규모 데이터 집합으로 조정되는 빅 데이터 분석 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f0a-106">Run big data analysis jobs that scale to massive data sets with [Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).</span></span>

<span data-ttu-id="d8f0a-107">Azure Data Lake Analytics를 시작하려면 [Java SDK를 사용하여 Azure Data Lake Analytics 시작](/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d8f0a-107">To get started with Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics using Java SDK](/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk).</span></span>

## <a name="management-api"></a><span data-ttu-id="d8f0a-108">관리 API</span><span class="sxs-lookup"><span data-stu-id="d8f0a-108">Management API</span></span>

<span data-ttu-id="d8f0a-109">관리 API를 사용하여 Data Lake Analytics 계정, 작업, 정책 및 카탈로그를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f0a-109">Use the management API to manage Data Lake Analytics accounts, jobs, policies, and catalogs.</span></span>

<span data-ttu-id="d8f0a-110">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f0a-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-analytics</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="d8f0a-111">예제</span><span class="sxs-lookup"><span data-stu-id="d8f0a-111">Example</span></span>

<span data-ttu-id="d8f0a-112">Data Lake Analytics에 새 U-SQL 작업을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="d8f0a-112">Submit a new U-SQL job to Data Lake Analytics.</span></span>

```java
// authenticate with service principal credentials
ApplicationTokenCredentials creds = new ApplicationTokenCredentials(_clientId, _tenantId, _clientSecret, null);
DataLakeAnalyticsJobManagementClient adlaJobClient = new DataLakeAnalyticsJobManagementClientImpl(creds);

// set up job parameters
UUID jobId = java.util.UUID.randomUUID();
USqlJobProperties properties = new USqlJobProperties();
properties.setScript("@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input TO @\"/output1.csv\" USING Outputters.Csv();");
JobInformation parameters = new JobInformation();
parameters.setName("testJob");
parameters.setJobId(jobId);
parameters.setType(JobType.USQL);
parameters.setProperties(properties);

// create the job
JobInformation jobInfo = adlaJobClient.getJobOperations().create(accountName, jobId, parameters).getBody();

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d8f0a-113">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="d8f0a-113">Explore the Client APIs</span></span>](/java/api/overview/azure/datalakeanalytics/managementapi)

## <a name="samples"></a><span data-ttu-id="d8f0a-114">샘플</span><span class="sxs-lookup"><span data-stu-id="d8f0a-114">Samples</span></span>

<span data-ttu-id="d8f0a-115">[Java SDK를 사용하는 Azure Data Lake Analytics][1]</span><span class="sxs-lookup"><span data-stu-id="d8f0a-115">[Azure Data Lake Analytics using Java SDK][1]</span></span> 

[1]: https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk

<span data-ttu-id="d8f0a-116">Azure Data Lake Analytics 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=java&term=analytics)을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d8f0a-116">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=java&term=analytics) of Azure Data Lake Analytics samples.</span></span>
