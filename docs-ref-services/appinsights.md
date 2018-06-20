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
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823766"
---
# <a name="azure-application-insights-libraries-for-java"></a>Java용 Azure Application Insights 라이브러리

## <a name="overview"></a>개요

[Application Insights](/azure/application-insights/app-insights-overview)를 사용하여 웹앱 및 서비스의 문제를 검색, 심사 및 진단합니다.

Application Insights를 시작하려면 [Java 웹 프로젝트에서 Application Insights 시작](/azure/application-insights/app-insights-java-get-started)을 참조하세요.

## <a name="client-library"></a>클라이언트 라이브러리

Application Insights 클라이언트 라이브러리를 사용하여 앱의 이벤트, 예외 및 사용자 메트릭을 추적하는 원격 분석을 추가합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>   
    <version>1.0.8</version>
</dependency>
```   

### <a name="example"></a>예

새 메트릭 항목을 만들고 해당 값을 기록합니다.

```java
    MetricTelemetry sample = new MetricTelemetry();
    sample.setName("metric name");
    sample.setValue(42.3);
    telemetryClient.TrackMetric(sample);
```

> [!div class="nextstepaction"]
> [클라이언트 API 탐색](/java/api/overview/azure/appinsights/client)

## <a name="samples"></a>샘플

앱에서 사용할 수 있는 [Application Insights용 Java 샘플 코드](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java)를 추가로 탐색합니다.
