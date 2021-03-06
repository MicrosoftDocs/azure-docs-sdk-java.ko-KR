---
title: Java용 Service Bus 라이브러리
description: Java 클라이언트에 대한 참조 설명서 및 Service Bus에 대한 관리 라이브러리
keywords: Azure, Java, SDK, API, 메시지, amqp, qpid JMS, pubsub, pub-sub, 메시지 브로커
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: service-bus
ms.openlocfilehash: 2099695784a59bf539aeae745df1fe38ec84f511
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593278"
---
# <a name="service-bus-libraries-for-java"></a>Java용 Service Bus 라이브러리

## <a name="overview"></a>개요

Service Bus는 매우 신뢰할 수 있는 큐와 게시/구독 토픽에 순차적 전달, 세션, 분할, 일정 계획, 복잡한 구독 및 워크플로 및 트랜잭션 처리와 같은 심층적인 기능을 제공하는 엔터프라이즈급 트랜잭션 메시지 플랫폼 서비스입니다.

Service Bus 기능은 비교 가능하며, 종종 고급 온-프레미스 레거시 메시지 브로커의 기능을 능가합니다. Service Bus 기능은 AMQP 1.0 및 HTTPS와 같은 표준 기반 프로토콜을 통해 사용할 수 있으며, 모든 프로토콜 제스처가 완전하게 문서화되어 광범위한 상호 운용성을 허용하고 있습니다. 

항상 사용 가능하고 신뢰할 수 있는 지속형 메시지에 집중하고 있는 Service Bus Premium은 하드웨어 선택 및 취득 프로세스, 배포 계획 및 실행, 무한의 성능 최적화 세션 없이 상당한 로컬 데이터 센터 배포로도 경쟁력 있는 처리량 성능을 제공합니다. 

Service Bus Premium은 간단하고 용량 지향적인 가격 책정 모델 및 상용 온-프레미스 브로커보다 훨씬 낮은 전체 비용으로 예측 가능한 성능을 제공하는 각 테넌트에 예약된 전용 용량을 갖추고서 완전하게 관리되는 제품입니다. 많은 고객을 위해 Service Bus Premium은 현재 연결된 워크로드가 클라우드에서 실행되지 않는 경우에도 전용 온-프레미스 메시지 클러스터를 대체할 수 있습니다. 

[메시지 설명서 섹션](https://docs.microsoft.com/azure/service-bus-messaging/)에서 Service Bus 개념에 대해 자세히 알아보세요. 

Java 개발자를 위해 Service Bus는 Microsoft에서 지원하는 기본 API를 제공하며, Apache Qpid Proton의 JMS 공급자와 같은 AMQP 1.0 규격 라이브러리와 함께 사용할 수도 있습니다.

## <a name="client-library"></a>클라이언트 라이브러리

공식 Service Bus 클라이언트는 [GitHub에서 소스 코드 형식](https://github.com/azure/azure-service-bus-java)으로 사용할 수 있으며, 이진 파일 및 패키지에 포함된 소스는 [Maven Central에서 사용할 수 있습니다](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).

**[샘플 코드 리포지토리](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/)에는 다음에 대한 샘플이 포함되어 있습니다.**
* [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java)를 사용하는 방법
* [TopicClient 및 SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java)를 사용하는 방법
* Service Bus에서 [MessageSender 및 MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) 메시지를 사용하는 방법입니다.

Maven 프로젝트의 `pom.xml` 파일에 종속성을 추가하여 자신의 프로젝트에서 라이브러리를 사용합니다. 필요에 따라 버전을 지정합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-servicebus</artifactId>
    <version>1.0.0</version>
</dependency>
```

```java
public class BasicSendReceiveWithQueueClient {
    // Connection String for the namespace can be obtained from the Azure portal under the
    // 'Shared Access policies' section.
    private static final String connectionString = "{connection string}";
    private static final String queueName = "{queue name}";
    private static IQueueClient queueClient;
    private static int totalSend = 100;
    private static int totalReceived = 0;

    public static void main(String[] args) throws Exception {

        Log.log("Starting BasicSendReceiveWithQueueClient sample");

        // create client
        Log.log("Create queue client.");
        queueClient = new QueueClient(new ConnectionStringBuilder(connectionString, queueName), ReceiveMode.PeekLock);

        // send and receive
        queueClient.registerMessageHandler(new MessageHandler(queueClient), new MessageHandlerOptions(1, false, Duration.ofMinutes(1)));
        for (int i = 0; i < totalSend; i++) {
            int j = i;
            Log.log("Sending message #%d.", j);
            queueClient.sendAsync(new Message("" + i)).thenRunAsync(() -> { Log.log("Sent message #%d.", j);});
        }

        while(totalReceived != totalSend) {
            Thread.sleep(1000);
        }

        Log.log("Received all messages, exiting the sample.");
        Log.log("Closing queue client.");
        queueClient.close();
    }

    static class MessageHandler implements IMessageHandler {
        private IQueueClient client;

        public MessageHandler(IQueueClient client) {
            this.client = client;
        }

        @Override
        public CompletableFuture<Void> onMessageAsync(IMessage iMessage) {
            Log.log("Received message with sq#: %d and lock token: %s.", iMessage.getSequenceNumber(), iMessage.getLockToken());
            return this.client.completeAsync(iMessage.getLockToken()).thenRunAsync(() -> {
                Log.log("Completed message sq#: %d and locktoken: %s", iMessage.getSequenceNumber(), iMessage.getLockToken());
                totalReceived++;
            });
        }

        @Override
        public void notifyException(Throwable throwable, ExceptionPhase exceptionPhase) {
            Log.log(exceptionPhase + "-" + throwable.getMessage());
        }
    }
}
```

> [!div class="nextstepaction"]
> [클라이언트 API 탐색](/java/api/overview/azure/servicebus/client)
> [여기에서 더 많은 예제 찾기(자세한 내용은 위를 참조)](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/)

## <a name="management-api"></a>관리 API

관리 API를 사용하여 네임스페이스, 토픽, 큐 및 구독을 만들고 관리합니다.

**여기에서 몇 가지 예를 찾으세요.**
* [Service Bus 큐 관리](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
* [Service Bus 토픽 만들기 및 구독](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)

**프로젝트에서 관리 API를 사용합니다.**
\
`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-servicebus</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/java/api/overview/azure/servicebus/management)

앱에서 사용할 수 있는 [Azure Service Bus용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=bus)를 추가로 탐색합니다.
