---
title: Java용 Azure Data Lake Analytics 라이브러리
description: Java용 Data Lake Analytics 라이브러리에 대한 참조 설명서
keywords: Azure, Java, SDK, API, 빅 데이터, Data Lake
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: c14c89f961951d114362adee4fec6239e78cffb3
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892744"
---
# <a name="azure-data-lake-analytics-libraries-for-java"></a>Java용 Azure Data Lake Analytics 라이브러리

## <a name="overview"></a>개요

[Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview)를 사용하여 대규모 데이터 집합으로 조정되는 빅 데이터 분석 작업을 실행합니다.

Azure Data Lake Analytics를 시작하려면 [Java SDK를 사용하여 Azure Data Lake Analytics 시작](/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk)을 참조하세요.

## <a name="management-api"></a>관리 API

관리 API를 사용하여 Data Lake Analytics 계정, 작업, 정책 및 카탈로그를 관리합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-analytics</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

## <a name="example"></a>예

Data Lake Analytics에 새 U-SQL 작업을 제출합니다.

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
> [관리 API 탐색](/java/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a>샘플

[Java SDK를 사용하는 Azure Data Lake Analytics][1] 

[1]: https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk

Azure Data Lake Analytics 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=java&term=analytics)을 봅니다.
