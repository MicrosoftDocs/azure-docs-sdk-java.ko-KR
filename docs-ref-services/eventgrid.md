---
title: Java용 Azure Event Grid 라이브러리
description: Azure Event Grid Java 라이브러리를 위한 참조 설명서
keywords: Azure, Java, SDK, API, Event Grid, 메시징, 이벤트 기반
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 07/11/2017
ms.topic: managed-reference
ms.devlang: java
ms.service: event-grid
ms.openlocfilehash: 35acbdeede2fbc541128029ad43f149209a057c4
ms.sourcegitcommit: db36eeb667a0bfe6d113953bb0583240db61b0f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50134635"
---
# <a name="azure-event-grid-libraries-for-java"></a><span data-ttu-id="3fbb6-104">Java용 Azure Event Grid 라이브러리</span><span class="sxs-lookup"><span data-stu-id="3fbb6-104">Azure Event Grid libraries for Java</span></span>

<span data-ttu-id="3fbb6-105">Azure Event Grid에서 간단한 HTTP 기반 이벤트 처리를 사용하여 Azure 서비스 및 사용자 지정 원본의 이벤트에 대해 수신 대기하고 대응하는 이벤트 기반 응용 프로그램을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="3fbb6-105">Build event-driven applications that listen and react to events from Azure services and custom sources using simple HTTP-based event handling with Azure Event Grid.</span></span>

<span data-ttu-id="3fbb6-106">Azure Event Grid에 대해 [자세히 알아보고](/azure/event-grid/overview), [Azure Blob 저장소 이벤트 자습서](/azure/storage/blobs/storage-blob-event-quickstart)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3fbb6-106">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart).</span></span> 

## <a name="client-sdk"></a><span data-ttu-id="3fbb6-107">Client SDK</span><span class="sxs-lookup"><span data-stu-id="3fbb6-107">Client SDK</span></span>

<span data-ttu-id="3fbb6-108">Azure Event Grid Client SDK를 사용하여 이벤트를 만들고, 인증하고, 토픽에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="3fbb6-108">Create events, authenticate, and post to topics using the Azure Event Grid Client SDK.</span></span>

<span data-ttu-id="3fbb6-109">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3fbb6-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventgrid</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="publish-events"></a><span data-ttu-id="3fbb6-110">이벤트 게시</span><span class="sxs-lookup"><span data-stu-id="3fbb6-110">Publish events</span></span>

<span data-ttu-id="3fbb6-111">다음 코드는 Azure로 인증하고 사용자 지정 형식(이 예제에서는 `Contoso.Items.ItemsReceived`)의 `EventGridEvent` 이벤트 `List`를 토픽에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="3fbb6-111">The following code authenticates with Azure and publishes a `List` of  `EventGridEvent` events of a custom type (in this example, `Contoso.Items.ItemsReceived` ) to a topic.</span></span> <span data-ttu-id="3fbb6-112">샘플에 사용된 항목 키 및 엔드포인트 주소는 Azure 명령줄 인터페이스에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fbb6-112">The topic key and endpoint address used in the sample can be retrieved from the Azure CLI:</span></span>

```azurecli-interactive
az eventgrid topic show -g gridResourceGroup -n topicName
az eventgrid topic key list -g gridResourceGroup -n topicName
```

```java
// Create an event grid client.
TopicCredentials topicCredentials = new TopicCredentials(System.getenv("EVENTGRID_TOPIC_KEY"));
EventGridClient client = new EventGridClientImpl(topicCredentials);

// Publish custom events to the EventGrid.
System.out.println("Publish custom events to the EventGrid");
List<EventGridEvent> eventsList = new ArrayList<>();
for (int i = 0; i < 5; i++) {
    eventsList.add(new EventGridEvent(
        UUID.randomUUID().toString(),
        String.format("Door%d", i),
        new ContosoItemReceivedEventData("Contoso Item SKU #1"),
        "Contoso.Items.ItemReceived",
        DateTime.now(),
        "2.0"
    ));
}

String eventGridEndpoint = String.format("https://%s/", new URI(System.getenv("EVENTGRID_TOPIC_ENDPOINT")).getHost());

client.publishEvents(eventGridEndpoint, eventsList);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3fbb6-113">Event Grid 클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="3fbb6-113">Explore the Event Grid Client APIs</span></span>](/java/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="3fbb6-114">관리 SDK</span><span class="sxs-lookup"><span data-stu-id="3fbb6-114">Management SDK</span></span>

<span data-ttu-id="3fbb6-115">Event Grid management SDK를 사용하여 Event Grid 인스턴스, 항목 및 구독을 만들거나, 업데이트하거나, 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3fbb6-115">Create, update, or delete Event Grid instances, topics, and subscriptions with the Event Grid management SDK.</span></span>

<span data-ttu-id="3fbb6-116">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3fbb6-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.16.0</version>
</dependency>
```   

<span data-ttu-id="3fbb6-117">다음 예에서는 [EventGrid Java 샘플](https://github.com/Azure-Samples/event-grid-java-publish-consume-events)에서 가져온 Event Grid 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3fbb6-117">The following example creates an Event Grid subscription, taken from the [EventGrid Java samples](https://github.com/Azure-Samples/event-grid-java-publish-consume-events)</span></span>

```java
// Create an event grid subscription.
//
System.out.println("Creating an Azure EventGrid Subscription");

EventSubscription eventSubscription = eventGridManager.eventSubscriptions().define(eventSubscriptionName)
    .withScope(eventGridTopic.id())
    .withDestination(new EventHubEventSubscriptionDestination()
        .withResourceId(eventHub.id()))
    .withFilter(new EventSubscriptionFilter()
        .withIsSubjectCaseSensitive(false)
        .withSubjectBeginsWith("")
        .withSubjectEndsWith(""))
    .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3fbb6-118">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="3fbb6-118">Explore the management APIs</span></span>](/java/api/overview/azure/eventgrid/management)