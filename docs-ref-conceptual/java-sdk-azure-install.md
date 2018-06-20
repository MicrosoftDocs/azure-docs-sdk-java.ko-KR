---
title: Java 개발자용 Azure | Microsoft Docs
description: Azure용 Java SDK 및 API 참조
keywords: Azure Java Azure Java API 참조, Azure Java 클래스 라이브러리, Azure SDK
author: routlaw
manager: douge
ms.assetid: 7b92e776-959b-4632-8b1d-047ce1417616
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 5c8bb4b81080461285551573eefc0d76b47b2d3d
ms.sourcegitcommit: 61030d025614b084e897809e603b2ec79900ec8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2018
ms.locfileid: "30302551"
---
# <a name="azure-libraries-for-java"></a>Java용 Azure 라이브러리

Azure 라이브러리는 Java 앱에서 네이티브 인터페이스를 통해 Azure 서비스를 사용하는 데 도움이 됩니다. 각 라이브러리는 독립적이며 다른 라이브러리와 별도로 사용할 수 있습니다.

| | | | |
|:-------------:|:----------:|:----:|:---:|
| [Azure Storage](#azure-storage) | [SQL Database](#sql-database)  | [Redis Cache](#redis-cache)   | [Azure Cosmos DB](#cosmos-db) |
| [Service Bus](#servicebus)  | [Azure Active Directory](#azuread) | [Key Vault](#keyvault)  | [이벤트 허브](#eventhub)
| [IoT 서비스](#iotservice) | [IoT 장치](#iotdevice) | [Data Lake](#datalake)  | [AppInsights](#appinsights) | 
| [Batch](#batch) | [Azure 리소스 관리](#management) |

## <a name="install-with-maven"></a>Maven을 사용하여 설치

`pom.xml`에 종속성 항목을 추가하여 라이브러리를 [Maven](https://maven.apache.org) 프로젝트로 가져옵니다.

예를 들어 최신 버전의 [Java용 Azure 관리 라이브러리](#management)를 포함하는 예제는 다음과 같습니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

Gradle과 같은 다른 Java 빌드 도구가 지원되지만, 설치 단계는 이 문서에서 제공되지 않습니다. Maven 가져오기를 사용하는 방법은 빌드 도구에 대한 설명서를 검토하세요.

## <a name="azure-service-libraries"></a>Azure 서비스 라이브러리

Azure 서비스를 통합하여 이러한 라이브러리를 사용하여 앱에 기능을 추가합니다. [Java 개발자 센터](https://azure.microsoft.com/develop/java)에서 Azure 서비스를 사용하여 앱을 만드는 방법에 대해 자세히 알아보세요.

<a name="azure-storage"></a>

### <a name="azure-storageazurestoragestorage-introduction"></a>[Azure Storage](/azure/storage/storage-introduction)  

응용 프로그램에 대한 데이터 저장소 및 메시지입니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.4.0</version>
</dependency>
```   

[샘플](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [참조](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [릴리스 정보](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)

<a name="sql-database"></a>

### <a name="sql-databaseazuresql-databasesql-database-technical-overview"></a>[SQL Database](/azure/sql-database/sql-database-technical-overview)

Azure SQL Database용 JDBC 드라이버입니다.

```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

[샘플](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [참조](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [릴리스 정보](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)

<a name="redis-cache"></a>

### <a name="redis-cachehttpsazuremicrosoftcomservicescache"></a>[Redis Cache](https://azure.microsoft.com/services/cache/)

낮은 대기 시간, 고성능 키-값 저장소입니다.

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
```   

[샘플](/azure/redis-cache/cache-java-get-started) | [참조](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [릴리스 정보](https://github.com/xetorthio/jedis/releases)  

<a name="cosmos-db"></a>

### <a name="azure-cosmos-dbazurecosmos-dbintroduction"></a>[Azure Cosmos DB](/azure/cosmos-db/introduction)

JSON 문서 및 SQL 또는 JavaScript 쿼리 구문을 사용하여 확장 가능한 NoSQL 데이터베이스입니다.   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

[샘플](/azure/cosmos-db/sql-api-java-application) | [참조](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [릴리스 정보](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)

<a name="servicebus"></a>
 
 ### <a name="servicebusazureservice-bus-messagingservice-bus-messaging-overview"></a>[Service Bus](/azure/service-bus-messaging/service-bus-messaging-overview) 
    
 Service Bus는 엔터프라이즈급 트랜잭션 메시지 플랫폼 서비스입니다.
 
 ```XML
 <dependency> 
     <groupId>com.microsoft.azure</groupId> 
     <artifactId>azure-servicebus</artifactId> 
     <version>1.0.0</version> 
 </dependency>   
 ```
 
 [샘플](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [참조](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [릴리스 정보](https://github.com/Azure/azure-service-bus-java)   
  
<a name="azuread"></a>

### <a name="azure-active-directoryazureactive-directoryactive-directory-whatis"></a>[Azure Active Directory](/azure/active-directory/active-directory-whatis)   

응용 프로그램에 대한 ID 관리 및 보안 로그인입니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```
   
[샘플](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [참조](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [릴리스 정보](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)
 
<a name="keyvault"></a>

### <a name="key-vaultazurekey-vault"></a>[Key Vault](/azure/key-vault) 

응용 프로그램의 키와 비밀에 안전하게 액세스합니다. 

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

[샘플](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [참조](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [릴리스 정보](https://github.com/Azure/azure-keyvault-java) 

<a name="eventhub"></a>

### <a name="event-hubazureevent-hubsevent-hubs-what-is-event-hubs"></a>[이벤트 허브](/azure/event-hubs/event-hubs-what-is-event-hubs) 
   
계측 또는 IoT 시나리오에 대해 처리량이 많은 이벤트 및 원격 분석을 처리합니다.

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-eventhubs</artifactId> 
    <version>0.14.4</version> 
</dependency>   
```

[샘플](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [참조](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [릴리스 정보](https://github.com/Azure/azure-event-hubs-java)

<a name="iotservice"></a> 

### <a name="iot-serviceazureiot-hub"></a>[IoT 서비스](/azure/iot-hub/)

IoT Hub에 등록된 장치에서 ID를 관리하고, 메시지를 보내고, 피드백을 받습니다.

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.7.23</version>
</dependency>
```   
   
[샘플](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [참조](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [릴리스 정보](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="iotdevice"></a> 

### <a name="iot-deviceazureiot-hubiot-hub-devguide"></a>[IoT 장치](/azure/iot-hub/iot-hub-devguide)

장치에서 IoT Hub로 메시지를 보냅니다.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.32</version>
</dependency>
```  

[샘플](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [참조](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [릴리스 정보](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="datalake"></a> 

### <a name="data-lake-storeazuredata-lake-storedata-lake-store-overview"></a>[Data Lake Store](/azure/data-lake-store/data-lake-store-overview)   
   
분석을 수행하기 위해 모든 크기와 셰이프의 데이터를 단일 위치로 캡처합니다.    

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

[샘플](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [참조](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [릴리스 정보](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)

<a name="appinsights"></a> 

### <a name="appinsightsazureapplication-insightsapp-insights-overview"></a>[AppInsights](/azure/application-insights/app-insights-overview)

사용을 추적하고, 원격 분석을 추가하고, 웹앱을 모니터링합니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>
    <version>1.0.8</version>
</dependency>
```

[샘플](/azure/application-insights/app-insights-java-get-started) | [참조](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [릴리스 정보](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)

<a name="batch"></a>

### <a name="batchazurebatch"></a>[Batch](/azure/batch)

클라우드에서 대규모 병렬 및 고성능 컴퓨팅 응용 프로그램을 효율적으로 실행합니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```

[샘플](https://github.com/azure/azure-batch-samples) | [참조](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [릴리스 정보](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)

<a name="management"></a> 

## <a name="manage-azure-resources"></a>Azure 리소스 관리

응용 프로그램 코드에서 Azure 리소스를 생성, 업데이트 및 삭제합니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

[샘플](https://github.com/Azure/azure-sdk-for-java#sample-code) | [참조](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [릴리스 정보](java-sdk-azure-release-notes.md)

<a name="servicebus"></a>

### <a name="servicebushttpsdocsmicrosoftcomazureservice-bus-messagingservice-bus-messaging-overview"></a>[Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) 
   
Service Bus는 엔터프라이즈급 트랜잭션 메시지 플랫폼 서비스입니다.

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-servicebus</artifactId> 
    <version>1.0.0</version> 
</dependency>   
```

[샘플](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [참조](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [릴리스 정보](https://github.com/Azure/azure-service-bus-java)

