---
title: Java용 Azure Application Insights 라이브러리
description: Java용 Azure Appplication Insights 관리 API에 대한 참조 설명서
keywords: Azure, Java, SDK, API, AppInsights, 원격 분석, 진단, 추적, 로그, 성능
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: appinsights
ms.openlocfilehash: d881ff66ad806e13f7d2cbafff6ce85c23240304
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893414"
---
# <a name="azure-application-insights-libraries-for-java"></a><span data-ttu-id="f9d7d-104">Java용 Azure Application Insights 라이브러리</span><span class="sxs-lookup"><span data-stu-id="f9d7d-104">Azure Application Insights libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="f9d7d-105">개요</span><span class="sxs-lookup"><span data-stu-id="f9d7d-105">Overview</span></span>

<span data-ttu-id="f9d7d-106">[Application Insights](/azure/application-insights/app-insights-overview)를 사용하여 웹앱 및 서비스의 문제를 검색, 심사 및 진단합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d7d-106">Detect, triage, and diagnose issues in your web apps and services with [Application Insights](/azure/application-insights/app-insights-overview).</span></span>

<span data-ttu-id="f9d7d-107">Application Insights를 시작하려면 [Java 웹 프로젝트에서 Application Insights 시작](/azure/application-insights/app-insights-java-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9d7d-107">To get started with Application Insights, see [Get started with Application Insights in a Java web project](/azure/application-insights/app-insights-java-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="f9d7d-108">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="f9d7d-108">Client library</span></span>

<span data-ttu-id="f9d7d-109">Application Insights 클라이언트 라이브러리를 사용하여 앱의 이벤트, 예외 및 사용자 메트릭을 추적하는 원격 분석을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d7d-109">Add telemetry to track events, exceptions, and user metrics in your apps with the Application Insights client library.</span></span>

<span data-ttu-id="f9d7d-110">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d7d-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>   
    <version>1.0.8</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="f9d7d-111">예</span><span class="sxs-lookup"><span data-stu-id="f9d7d-111">Example</span></span>

<span data-ttu-id="f9d7d-112">새 메트릭 항목을 만들고 해당 값을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d7d-112">Create a new metric entry and record a value for it.</span></span>

```java
    MetricTelemetry sample = new MetricTelemetry();
    sample.setName("metric name");
    sample.setValue(42.3);
    telemetryClient.TrackMetric(sample);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f9d7d-113">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="f9d7d-113">Explore the Client APIs</span></span>](/java/api/overview/azure/appinsights/client)

## <a name="samples"></a><span data-ttu-id="f9d7d-114">샘플</span><span class="sxs-lookup"><span data-stu-id="f9d7d-114">Samples</span></span>

<span data-ttu-id="f9d7d-115">앱에서 사용할 수 있는 [Application Insights용 Java 샘플 코드](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="f9d7d-115">Explore more [sample Java code for Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java) you can use in your apps.</span></span>
