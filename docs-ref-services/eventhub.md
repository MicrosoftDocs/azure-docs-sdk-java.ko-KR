---
title: "Java용 Azure Event Hub 라이브러리"
description: "Java용 Event Hub 라이브러리에 대한 참조 설명서"
keywords: "Azure, Java, SDK, API, 이벤트 허브, IoT, 스트림 처리"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: event-hub
ms.openlocfilehash: 8e5b032624862ffbef18c718abf4fa29359b3e67
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-event-hub-libraries-for-java"></a>Java용 Azure Event Hub 라이브러리

## <a name="overview"></a>개요

[Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs)를 사용하여 연결된 IoT 장치 및 응용 프로그램에서 초당 수백만 개의 이벤트를 수집하고 관리합니다.

Azure Event Hubs를 시작하려면 [Java를 사용하여 Azure Event Hubs에서 이벤트 수신](/azure/event-hubs/event-hubs-java-get-started-receive-eph)을 참조하세요.


## <a name="client-library"></a>클라이언트 라이브러리

Event Hubs 클라이언트 라이브러리를 사용하여 Azure Event Hub에 이벤트를 보내고 Event Hub에서 이벤트를 소비하고 처리합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>0.14.3</version>
</dependency>
```   

## <a name="example"></a>예제

이벤트 허브에 이벤트를 보냅니다.

```java
ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName,sasKeyName, sasKey);

byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
EventData sendEvent = new EventData(payloadBytes);
EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
ehClient.sendSync(sendEvent);
```

> [!div class="nextstepaction"]
> [클라이언트 API 탐색](/java/api/overview/azure/eventhub/clientlibrary)


## <a name="samples"></a>샘플

[JMS를 통해 Event Hub에 쓰기 및 Apache Storm에서 읽기][1]
[하이브리드 .NET/Java 토폴로지를 사용하여 Event Hubs에서 읽기 및 쓰기][2] 

[1]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[2]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

앱에서 사용할 수 있는 [Azure Event Hubs용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=event)를 추가로 탐색합니다.

