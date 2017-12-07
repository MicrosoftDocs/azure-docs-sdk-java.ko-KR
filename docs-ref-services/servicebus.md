---
title: "Java용 Service Bus 라이브러리"
description: "Java 클라이언트에 대한 참조 설명서 및 Service Bus에 대한 관리 라이브러리"
keywords: "Azure, Java, SDK, API, 메시지, amqp, qpid JMS, pubsub, pub-sub, 메시지 브로커"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: service-bus
ms.openlocfilehash: 6fccbc76a3600e2bbe43e4332c6146d2be81b6c9
ms.sourcegitcommit: fcf1189ede712ae30f8c7626bde50c9b8bb561bc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="service-bus-libraries-for-java"></a><span data-ttu-id="cf56c-104">Java용 Service Bus 라이브러리</span><span class="sxs-lookup"><span data-stu-id="cf56c-104">Service Bus libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="cf56c-105">개요</span><span class="sxs-lookup"><span data-stu-id="cf56c-105">Overview</span></span>

<span data-ttu-id="cf56c-106">Service Bus는 매우 신뢰할 수 있는 큐와 게시/구독 토픽에 순차적 전달, 세션, 분할, 일정 계획, 복잡한 구독 및 워크플로 및 트랜잭션 처리와 같은 심층적인 기능을 제공하는 엔터프라이즈급 트랜잭션 메시지 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="cf56c-106">Service Bus is an enterprise-class, transactional messaging platform service that provides highly reliable queues and publish/subscribe topics with deep feature capabilities such as ordered delivery, sessions, partitioning, scheduling, complex subscriptions, as well as workflow and transaction handling.</span></span>

<span data-ttu-id="cf56c-107">Service Bus 기능은 비교 가능하며, 종종 고급 온-프레미스 레거시 메시지 브로커의 기능을 능가합니다.</span><span class="sxs-lookup"><span data-stu-id="cf56c-107">The Service Bus feature capabilities are comparable and often exceed those of high-end, on-premises legacy message brokers.</span></span> <span data-ttu-id="cf56c-108">Service Bus 기능은 AMQP 1.0 및 HTTPS와 같은 표준 기반 프로토콜을 통해 사용할 수 있으며, 모든 프로토콜 제스처가 완전하게 문서화되어 광범위한 상호 운용성을 허용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf56c-108">The Service Bus features are available via standards-based protocols like AMQP 1.0 and HTTPS and all protocol gestures are fully documented, allowing for broad interoperability.</span></span> 

<span data-ttu-id="cf56c-109">항상 사용 가능하고 신뢰할 수 있는 지속형 메시지에 집중하고 있는 Service Bus Premium은 하드웨어 선택 및 취득 프로세스, 배포 계획 및 실행, 무한의 성능 최적화 세션 없이 상당한 로컬 데이터 센터 배포로도 경쟁력 있는 처리량 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cf56c-109">Focusing on highly available and reliable durable messaging, the Service Bus Premium provides competitive throughput performance even with substantial local datacenter deployments, but without hardware selection and acquisition processes, deployment planning and execution, and endless performance optimization sessions.</span></span> 

<span data-ttu-id="cf56c-110">Service Bus Premium은 간단하고 용량 지향적인 가격 책정 모델 및 상용 온-프레미스 브로커보다 훨씬 낮은 전체 비용으로 예측 가능한 성능을 제공하는 각 테넌트에 예약된 전용 용량을 갖추고서 완전하게 관리되는 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="cf56c-110">Service Bus Premium is a fully managed offering with dedicated capacity reserved for each tenant that yields predictable performance with a simple, capacity-oriented pricing model and at extremely lower overall cost than commercial on-premises brokers.</span></span> <span data-ttu-id="cf56c-111">많은 고객을 위해 Service Bus Premium은 현재 연결된 워크로드가 클라우드에서 실행되지 않는 경우에도 전용 온-프레미스 메시지 클러스터를 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf56c-111">For many customers, Service Bus Premium can replace dedicated on-premises messaging clusters today, even if the attached workloads do not run in the cloud.</span></span> 

<span data-ttu-id="cf56c-112">[메시지 설명서 섹션](https://docs.microsoft.com/azure/service-bus-messaging/)에서 Service Bus 개념에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="cf56c-112">Learn more about Service Bus concepts [in the messaging documentation section](https://docs.microsoft.com/azure/service-bus-messaging/)</span></span> 

<span data-ttu-id="cf56c-113">Java 개발자를 위해 Service Bus는 Microsoft에서 지원하는 기본 API를 제공하며, Apache Qpid Proton의 JMS 공급자와 같은 AMQP 1.0 규격 라이브러리와 함께 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf56c-113">For Java developers, Service Bus provides a Microsoft supported native API and Service Bus can also be used with AMQP 1.0 compliant libraries such as Apache Qpid Proton's JMS provider.</span></span>

<span data-ttu-id="cf56c-114">공식 Service Bus 클라이언트는 [GitHub에서 소스 코드 형식](https://github.com/azure/azure-service-bus-java)으로 사용할 수 있으며, 이진 파일 및 패키지에 포함된 소스는 [Maven Central에서 사용할 수 있습니다](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).</span><span class="sxs-lookup"><span data-stu-id="cf56c-114">The official Service Bus client is available in [source code form on GitHub](https://github.com/azure/azure-service-bus-java) and binaries and packaged sources [are available on Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).</span></span> 


## <a name="client-library"></a><span data-ttu-id="cf56c-115">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="cf56c-115">Client library</span></span>


<span data-ttu-id="cf56c-116">Maven 프로젝트의 `pom.xml` 파일에 종속성을 추가하여 자신의 프로젝트에서 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cf56c-116">Add a dependency to your Maven project's `pom.xml` file to use the library in your own project.</span></span> <span data-ttu-id="cf56c-117">필요에 따라 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf56c-117">Specify the version as desired.</span></span>

<span data-ttu-id="cf56c-118">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cf56c-118">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-servicebus</artifactId>
    <version>1.0.0</version>
</dependency>
```

## <a name="examples"></a><span data-ttu-id="cf56c-119">예</span><span class="sxs-lookup"><span data-stu-id="cf56c-119">Examples</span></span>

<span data-ttu-id="cf56c-120">[샘플 코드 리포지토리](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/)에는 Service Bus의 [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java), [TopicClient 및 SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java), [MessageSender 및 MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) 메시지에 대한 샘플이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf56c-120">The [sample code repository](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) contains samples for how to [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java) and [TopicClient and SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java) and [MessageSender and MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) messages from Service Bus.</span></span>


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
> [<span data-ttu-id="cf56c-121">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="cf56c-121">Explore the Client APIs</span></span>](/java/api/overview/azure/servicebus/clientlibrary)

## <a name="management-api"></a><span data-ttu-id="cf56c-122">관리 API</span><span class="sxs-lookup"><span data-stu-id="cf56c-122">Management API</span></span>

<span data-ttu-id="cf56c-123">관리 API를 사용하여 네임스페이스, 토픽, 큐 및 구독을 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="cf56c-123">Create and manage namespaces, topics, queues, and subscriptions with the management API.</span></span>

<span data-ttu-id="cf56c-124">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cf56c-124">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-servicebus</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="cf56c-125">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="cf56c-125">Explore the Management APIs</span></span>](/java/api/overview/azure/servicebus/managementapi)


## <a name="examples"></a><span data-ttu-id="cf56c-126">예</span><span class="sxs-lookup"><span data-stu-id="cf56c-126">Examples</span></span>

<span data-ttu-id="cf56c-127">[Service Bus 큐 관리(영문)](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
[Service Bus 토픽 만들기 및 구독(영문)](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)</span><span class="sxs-lookup"><span data-stu-id="cf56c-127">[Manage Service Bus queues](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
[Create and subscribe to Service Bus topics](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)</span></span>

<span data-ttu-id="cf56c-128">앱에서 사용할 수 있는 [Azure Service Bus용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=bus)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="cf56c-128">Explore more [sample Java code for Azure Service Bus](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) you can use in your apps.</span></span>
