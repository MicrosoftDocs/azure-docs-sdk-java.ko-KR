---
title: "Java 개발자용 Azure | Microsoft Docs"
description: "Azure용 Java SDK 및 API 참조"
keywords: "Azure Java Azure Java API 참조, Azure Java 클래스 라이브러리, Azure SDK"
author: routlaw
manager: douge
ms.assetid: 7b92e776-959b-4632-8b1d-047ce1417616
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 570f820e1349e1dfd01a6c7f323b5312c14c40c6
ms.sourcegitcommit: 4b63ecd2c92a9115dfae018618e4e4046b061b3e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2017
---
# <a name="azure-libraries-for-java"></a><span data-ttu-id="d36e4-104">Java용 Azure 라이브러리</span><span class="sxs-lookup"><span data-stu-id="d36e4-104">Azure libraries for Java</span></span>

<span data-ttu-id="d36e4-105">Azure 라이브러리는 Java 앱에서 네이티브 인터페이스를 통해 Azure 서비스를 사용하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-105">Azure libraries help you consume Azure services in your Java apps using native interfaces.</span></span> <span data-ttu-id="d36e4-106">각 라이브러리는 독립적이며 다른 라이브러리와 별도로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-106">Each library is independent and can be used separately from the others another.</span></span>

| | | | |
|:-------------:|:----------:|:----:|:---:|
| [<span data-ttu-id="d36e4-107">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="d36e4-107">Azure Storage</span></span>](#azure-storage) | [<span data-ttu-id="d36e4-108">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d36e4-108">SQL Database</span></span>](#sql-database)  | [<span data-ttu-id="d36e4-109">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="d36e4-109">Redis Cache</span></span>](#redis-cache)   | [<span data-ttu-id="d36e4-110">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d36e4-110">DocumentDB</span></span>](#documentdb) |
| [<span data-ttu-id="d36e4-111">서비스 버스</span><span class="sxs-lookup"><span data-stu-id="d36e4-111">Service Bus</span></span>](#servicebus)  | [<span data-ttu-id="d36e4-112">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d36e4-112">Azure Active Directory</span></span>](#azuread) | [<span data-ttu-id="d36e4-113">키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="d36e4-113">Key Vault</span></span>](#keyvault)  | [<span data-ttu-id="d36e4-114">이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="d36e4-114">Event Hub</span></span>](#eventhub)
| [<span data-ttu-id="d36e4-115">IoT 서비스</span><span class="sxs-lookup"><span data-stu-id="d36e4-115">IoT Service</span></span>](#iotservice) | [<span data-ttu-id="d36e4-116">IoT 장치</span><span class="sxs-lookup"><span data-stu-id="d36e4-116">IoT Device</span></span>](#iotdevice) | [<span data-ttu-id="d36e4-117">Data Lake</span><span class="sxs-lookup"><span data-stu-id="d36e4-117">Data Lake</span></span>](#datalake)  | [<span data-ttu-id="d36e4-118">AppInsights</span><span class="sxs-lookup"><span data-stu-id="d36e4-118">AppInsights</span></span>](#appinsights) | 
| [<span data-ttu-id="d36e4-119">배치</span><span class="sxs-lookup"><span data-stu-id="d36e4-119">Batch</span></span>](#batch) | [<span data-ttu-id="d36e4-120">Azure 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="d36e4-120">Manage Azure resources</span></span>](#management) |

## <a name="install-with-maven"></a><span data-ttu-id="d36e4-121">Maven을 사용하여 설치</span><span class="sxs-lookup"><span data-stu-id="d36e4-121">Install with Maven</span></span>

<span data-ttu-id="d36e4-122">`pom.xml`에 종속성 항목을 추가하여 라이브러리를 [Maven](https://maven.apache.org) 프로젝트로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-122">Add a dependency entry in your `pom.xml` to import a library into your [Maven](https://maven.apache.org) project.</span></span>

<span data-ttu-id="d36e4-123">예를 들어 최신 버전의 [Java용 Azure 관리 라이브러리](#management)를 포함하는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-123">For example, to include the latest version of the [Azure management libraries for Java](#management):</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

<span data-ttu-id="d36e4-124">Gradle과 같은 다른 Java 빌드 도구가 지원되지만, 설치 단계는 이 문서에서 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-124">Other Java build tools like Gradle are supported but the install steps are not provided in this article.</span></span> <span data-ttu-id="d36e4-125">Maven 가져오기를 사용하는 방법은 빌드 도구에 대한 설명서를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="d36e4-125">Review the documentation for your build tool on how to consume Maven imports.</span></span>

## <a name="azure-service-libraries"></a><span data-ttu-id="d36e4-126">Azure 서비스 라이브러리</span><span class="sxs-lookup"><span data-stu-id="d36e4-126">Azure service libraries</span></span>

<span data-ttu-id="d36e4-127">Azure 서비스를 통합하여 이러한 라이브러리를 사용하여 앱에 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-127">Integrate Azure services to add functionality to your apps using these libraries.</span></span> <span data-ttu-id="d36e4-128">[Java 개발자 센터](https://azure.microsoft.com/develop/java)에서 Azure 서비스를 사용하여 앱을 만드는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="d36e4-128">Learn more about building apps with Azure services at the [Java developer center](https://azure.microsoft.com/develop/java).</span></span>

<a name="azure-storage"></a>

### <a name="azure-storageazurestoragestorage-introduction"></a>[<span data-ttu-id="d36e4-129">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="d36e4-129">Azure Storage</span></span>](/azure/storage/storage-introduction)  

<span data-ttu-id="d36e4-130">응용 프로그램에 대한 데이터 저장소 및 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-130">Data storage and messaging for your applications.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.4.0</version>
</dependency>
```   

<span data-ttu-id="d36e4-131">[샘플](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [참조](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [릴리스 정보](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)</span><span class="sxs-lookup"><span data-stu-id="d36e4-131">[Samples](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Reference](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Release Notes](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)</span></span>

<a name="sql-database"></a>

### <a name="sql-databaseazuresql-databasesql-database-technical-overview"></a>[<span data-ttu-id="d36e4-132">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="d36e4-132">SQL Database</span></span>](/azure/sql-database/sql-database-technical-overview)

<span data-ttu-id="d36e4-133">Azure SQL Database용 JDBC 드라이버입니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-133">JDBC driver for Azure SQL Database.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

<span data-ttu-id="d36e4-134">[샘플](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [참조](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [릴리스 정보](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)</span><span class="sxs-lookup"><span data-stu-id="d36e4-134">[Samples](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Reference](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Release Notes](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)</span></span>

<a name="redis-cache"></a>

### <a name="redis-cachehttpsazuremicrosoftcomservicescache"></a>[<span data-ttu-id="d36e4-135">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="d36e4-135">Redis Cache</span></span>](https://azure.microsoft.com/services/cache/)

<span data-ttu-id="d36e4-136">낮은 대기 시간, 고성능 키-값 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-136">Low-latency, high-performance key-value store.</span></span>

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
```   

<span data-ttu-id="d36e4-137">[샘플](/azure/redis-cache/cache-java-get-started) | [참조](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [릴리스 정보](https://github.com/xetorthio/jedis/releases)</span><span class="sxs-lookup"><span data-stu-id="d36e4-137">[Samples](/azure/redis-cache/cache-java-get-started) | [Reference](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Release Notes](https://github.com/xetorthio/jedis/releases)</span></span>  

<a name="documentdb"></a>

### <a name="cosmos-dbazuredocumentdbdocumentdb-introduction"></a>[<span data-ttu-id="d36e4-138">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d36e4-138">Cosmos DB</span></span>](/azure/documentdb/documentdb-introduction)

<span data-ttu-id="d36e4-139">JSON 문서 및 SQL 또는 JavaScript 쿼리 구문을 사용하여 확장 가능한 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-139">Scalable NoSQL database with JSON documents and a SQL or JavaScript query syntax.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

<span data-ttu-id="d36e4-140">[샘플](/azure/documentdb/documentdb-java-application) | [참조](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [릴리스 정보](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)</span><span class="sxs-lookup"><span data-stu-id="d36e4-140">[Samples](/azure/documentdb/documentdb-java-application) | [Reference](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Release Notes](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)</span></span>

<a name="servicebus"></a>
 
 ### <a name="servicebusazureservice-bus-messagingservice-bus-messaging-overview"></a>[<span data-ttu-id="d36e4-141">Service Bus</span><span class="sxs-lookup"><span data-stu-id="d36e4-141">ServiceBus</span></span>](/azure/service-bus-messaging/service-bus-messaging-overview) 
    
 <span data-ttu-id="d36e4-142">Service Bus는 엔터프라이즈급 트랜잭션 메시지 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-142">Service Bus is an enterprise-class, transactional messaging platform service.</span></span>
 
 ```XML
 <dependency> 
     <groupId>com.microsoft.azure</groupId> 
     <artifactId>azure-servicebus</artifactId> 
     <version>1.0.0</version> 
 </dependency>   
 ```
 
 <span data-ttu-id="d36e4-143">[샘플](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [참조](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [릴리스 정보](https://github.com/Azure/azure-service-bus-java)</span><span class="sxs-lookup"><span data-stu-id="d36e4-143">[Samples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Reference](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Release Notes](https://github.com/Azure/azure-service-bus-java)</span></span>   
  
<a name="azuread"></a>

### <a name="azure-active-directoryazureactive-directoryactive-directory-whatis"></a>[<span data-ttu-id="d36e4-144">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d36e4-144">Azure Active Directory</span></span>](/azure/active-directory/active-directory-whatis)   

<span data-ttu-id="d36e4-145">응용 프로그램에 대한 ID 관리 및 보안 로그인입니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-145">Identity management and secure sign-in for your applications.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```
   
<span data-ttu-id="d36e4-146">[샘플](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [참조](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [릴리스 정보](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)</span><span class="sxs-lookup"><span data-stu-id="d36e4-146">[Samples](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Reference](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Release Notes](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)</span></span>
 
<a name="keyvault"></a>

### <a name="key-vaultazurekey-vault"></a>[<span data-ttu-id="d36e4-147">키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="d36e4-147">Key Vault</span></span>](/azure/key-vault) 

<span data-ttu-id="d36e4-148">응용 프로그램의 키와 비밀에 안전하게 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-148">Safely access keys and secrets from your applications.</span></span> 

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

<span data-ttu-id="d36e4-149">[샘플](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [참조](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [릴리스 정보](https://github.com/Azure/azure-keyvault-java)</span><span class="sxs-lookup"><span data-stu-id="d36e4-149">[Samples](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Reference](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Release Notes](https://github.com/Azure/azure-keyvault-java)</span></span> 

<a name="eventhub"></a>

### <a name="event-hubazureevent-hubsevent-hubs-what-is-event-hubs"></a>[<span data-ttu-id="d36e4-150">이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="d36e4-150">Event Hub</span></span>](/azure/event-hubs/event-hubs-what-is-event-hubs) 
   
<span data-ttu-id="d36e4-151">계측 또는 IoT 시나리오에 대해 처리량이 많은 이벤트 및 원격 분석을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-151">High-throughput event and telemetry handling for your instrumentation or IoT scenarios.</span></span>

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-eventhubs</artifactId> 
    <version>0.14.4</version> 
</dependency>   
```

<span data-ttu-id="d36e4-152">[샘플](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [참조](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [릴리스 정보](https://github.com/Azure/azure-event-hubs-java)</span><span class="sxs-lookup"><span data-stu-id="d36e4-152">[Samples](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Reference](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Release Notes](https://github.com/Azure/azure-event-hubs-java)</span></span>

<a name="iotservice"></a> 

### <a name="iot-serviceazureiot-hub"></a>[<span data-ttu-id="d36e4-153">IoT 서비스</span><span class="sxs-lookup"><span data-stu-id="d36e4-153">IoT Service</span></span>](/azure/iot-hub/)

<span data-ttu-id="d36e4-154">IoT Hub에 등록된 장치에서 ID를 관리하고, 메시지를 보내고, 피드백을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-154">Manage identities, send messages, and get feedback from devices registered with your IoT hub.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.7.23</version>
</dependency>
```   
   
<span data-ttu-id="d36e4-155">[샘플](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [참조](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [릴리스 정보](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span><span class="sxs-lookup"><span data-stu-id="d36e4-155">[Samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Reference](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Release Notes](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span></span>

<a name="iotdevice"></a> 

### <a name="iot-deviceazureiot-hubiot-hub-devguide"></a>[<span data-ttu-id="d36e4-156">IoT 장치</span><span class="sxs-lookup"><span data-stu-id="d36e4-156">IoT Device</span></span>](/azure/iot-hub/iot-hub-devguide)

<span data-ttu-id="d36e4-157">장치에서 IoT Hub로 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-157">Send a message to an IoT hub from your device.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.32</version>
</dependency>
```  

<span data-ttu-id="d36e4-158">[샘플](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [참조](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [릴리스 정보](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span><span class="sxs-lookup"><span data-stu-id="d36e4-158">[Samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Reference](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Release Notes](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span></span>

<a name="datalake"></a> 

### <a name="data-lake-storeazuredata-lake-storedata-lake-store-overview"></a>[<span data-ttu-id="d36e4-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d36e4-159">Data Lake Store</span></span>](/azure/data-lake-store/data-lake-store-overview)   
   
<span data-ttu-id="d36e4-160">분석을 수행하기 위해 모든 크기와 셰이프의 데이터를 단일 위치로 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-160">Capture data of any size and shape into a single location for performing analytics.</span></span>    

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

<span data-ttu-id="d36e4-161">[샘플](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [참조](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [릴리스 정보](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)</span><span class="sxs-lookup"><span data-stu-id="d36e4-161">[Samples](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Reference](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Release Notes](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)</span></span>

<a name="appinsights"></a> 

### <a name="appinsightsazureapplication-insightsapp-insights-overview"></a>[<span data-ttu-id="d36e4-162">AppInsights</span><span class="sxs-lookup"><span data-stu-id="d36e4-162">AppInsights</span></span>](/azure/application-insights/app-insights-overview)

<span data-ttu-id="d36e4-163">사용을 추적하고, 원격 분석을 추가하고, 웹앱을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-163">Track usage, add telemetry, and monitor your web apps.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>
    <version>1.0.8</version>
</dependency>
```

<span data-ttu-id="d36e4-164">[샘플](/azure/application-insights/app-insights-java-get-started) | [참조](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [릴리스 정보](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)</span><span class="sxs-lookup"><span data-stu-id="d36e4-164">[Samples](/azure/application-insights/app-insights-java-get-started) | [Reference](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Release Notes](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)</span></span>

<a name="batch"></a>

### <a name="batchazurebatch"></a>[<span data-ttu-id="d36e4-165">배치</span><span class="sxs-lookup"><span data-stu-id="d36e4-165">Batch</span></span>](/azure/batch)

<span data-ttu-id="d36e4-166">클라우드에서 대규모 병렬 및 고성능 컴퓨팅 응용 프로그램을 효율적으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-166">Run large-scale parallel and high-performance computing applications efficiently in the cloud.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```

<span data-ttu-id="d36e4-167">[샘플](https://github.com/azure/azure-batch-samples) | [참조](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [릴리스 정보](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="d36e4-167">[Samples](https://github.com/azure/azure-batch-samples) | [Reference](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Release Notes](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)</span></span>

<a name="management"></a> 

## <a name="manage-azure-resources"></a><span data-ttu-id="d36e4-168">Azure 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="d36e4-168">Manage Azure resources</span></span>

<span data-ttu-id="d36e4-169">응용 프로그램 코드에서 Azure 리소스를 생성, 업데이트 및 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-169">Create, update, and delete Azure resources from your application code.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

<span data-ttu-id="d36e4-170">[샘플](https://github.com/Azure/azure-sdk-for-java#sample-code) | [참조](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [릴리스 정보](java-sdk-azure-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="d36e4-170">[Samples](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Reference](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Release Notes](java-sdk-azure-release-notes.md)</span></span>

<a name="servicebus"></a>

### <a name="servicebushttpsdocsmicrosoftcomazureservice-bus-messagingservice-bus-messaging-overview"></a>[<span data-ttu-id="d36e4-171">Service Bus</span><span class="sxs-lookup"><span data-stu-id="d36e4-171">ServiceBus</span></span>](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) 
   
<span data-ttu-id="d36e4-172">Service Bus는 엔터프라이즈급 트랜잭션 메시지 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d36e4-172">Service Bus is an enterprise-class, transactional messaging platform service.</span></span>

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-servicebus</artifactId> 
    <version>1.0.0</version> 
</dependency>   
```

<span data-ttu-id="d36e4-173">[샘플](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [참조](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [릴리스 정보](https://github.com/Azure/azure-service-bus-java)</span><span class="sxs-lookup"><span data-stu-id="d36e4-173">[Samples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Reference](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Release Notes](https://github.com/Azure/azure-service-bus-java)</span></span>

