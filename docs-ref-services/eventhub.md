---
title: Java용 Azure Event Hub 라이브러리
description: Java용 Event Hub 라이브러리에 대한 참조 설명서
keywords: Azure, Java, SDK, API, 이벤트 허브, IoT, 스트림 처리
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: event-hub
ms.openlocfilehash: b6646ef27edace4247090e749c9a52cd6a33a82c
ms.sourcegitcommit: 3d3460289ab6b9165c2cf6a3dd56eafd0692501e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34283027"
---
# <a name="azure-event-hub-libraries-for-java"></a>Java용 Azure Event Hub 라이브러리

## <a name="overview"></a>개요

[Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs)를 사용하여 연결된 IoT 장치 및 응용 프로그램에서 초당 수백만 개의 이벤트를 수집하고 관리합니다.

Azure Event Hubs를 시작하려면 [Java를 사용하여 Azure Event Hubs에서 이벤트 수신](/azure/event-hubs/event-hubs-java-get-started-receive-eph)을 참조하세요.


## <a name="client-library"></a>클라이언트 라이브러리

Event Hubs 클라이언트 라이브러리를 사용하여 Azure Event Hub에 이벤트를 보내고 Event Hub에서 이벤트를 소비하고 처리합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 [클라이언트 라이브러리](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventhubs)를 사용합니다.
 

## <a name="example"></a>예

이벤트 허브에 이벤트를 보냅니다.

```java
final ConnectionStringBuilder connStr = new ConnectionStringBuilder()
                                            .setNamespaceName(namespaceName)
                                            .setEventHubName(eventHubName)
                                            .setSasKeyName(sasKeyName)
                                            .setSasKey(sasKey);
final EventHubClient ehClient = EventHubClient.createSync(connStr.toString());

final byte[] payloadBytes = "Test AMQP message".getBytes("UTF-8");
final EventData sendEvent = new EventData(payloadBytes);

ehClient.sendSync(sendEvent);
```


> [!div class="nextstepaction"]
> [클라이언트 API 탐색](/java/api/overview/azure/eventhubs/client)



## <a name="samples"></a>샘플

[샘플을 사용하여 Event Hub 데이터 평면 API 살펴보기][1]

[JMS를 통해 Event Hub에 쓰기 및 Apache Storm에서 읽기][2]

[하이브리드 .NET/Java 토폴로지를 사용하여 Event Hubs에서 읽기 및 쓰기][3] 

[1]: https://github.com/Azure/azure-event-hubs/tree/master/samples/Java
[2]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[3]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

앱에서 사용할 수 있는 [Azure Event Hubs용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=event)를 추가로 탐색합니다.

