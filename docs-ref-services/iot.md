---
title: "Java용 Azure IoT Hub 라이브러리"
description: "Java용 Azure IoT Hub 라이브러리에 대한 참조 설명서"
keywords: "Azure, Java, SDK, API, 이벤트, IoT, 스트림, 장치, IoT Hub"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: iot-hub
ms.openlocfilehash: b386612741e222fcaeb7b6c38753d0cb7d616239
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-iot-libraries-for-java"></a><span data-ttu-id="e9f4e-104">Java용 Azure IoT 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e9f4e-104">Azure IoT libraries for Java</span></span>

<span data-ttu-id="e9f4e-105">[Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-what-is-iot-hub)를 사용하여 IoT(사물 인터넷) 자산을 연결, 모니터링 및 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f4e-105">Connect, monitor, and control Internet of Things assets with [Azure IoT Hub](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-what-is-iot-hub).</span></span>

<span data-ttu-id="e9f4e-106">Azure IoT Hub를 시작하려면 [Java를 사용하여 IoT Hub에 장치 연결](/azure/iot-hub/iot-hub-java-java-getstarted)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e9f4e-106">To get started with Azure IoT Hub, see [Connect your device to your IoT hub using Java](/azure/iot-hub/iot-hub-java-java-getstarted).</span></span>

## <a name="iot-service-library"></a><span data-ttu-id="e9f4e-107">IoT 서비스 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e9f4e-107">IoT Service library</span></span>

<span data-ttu-id="e9f4e-108">IoT 서비스 라이브러리를 사용하여 장치를 등록하고, 클라우드에서 등록된 장치로 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9f4e-108">Register devices and send messages from the cloud to registered devices using the IoT Service library.</span></span>

<span data-ttu-id="e9f4e-109">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f4e-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.6.23</version>
</dependency>
```   

## <a name="iot-device-library"></a><span data-ttu-id="e9f4e-110">Iot 장치 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e9f4e-110">Iot Device library</span></span>

<span data-ttu-id="e9f4e-111">IoT 장치 라이브러리를 사용하여 클라우드로 메시지를 보내고 장치에서 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e9f4e-111">Send messages to the cloud and receive messages on devices using the IoT Device library.</span></span>

<span data-ttu-id="e9f4e-112">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f4e-112">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.31</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e9f4e-113">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="e9f4e-113">Explore the Client APIs</span></span>](/java/api/overview/azure/iot/clientlibrary)   

## <a name="example"></a><span data-ttu-id="e9f4e-114">예제</span><span class="sxs-lookup"><span data-stu-id="e9f4e-114">Example</span></span>

<span data-ttu-id="e9f4e-115">Azure IoT Hub에서 장치로 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9f4e-115">Send a message from Azure IoT Hub to a device.</span></span>

```java
Message messageToSend = new Message(messageText);
messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
messageToSend.setMessageId(java.util.UUID.randomUUID().toString());

// set message properties
Map<String, String> propertiesToSend = new HashMap<String, String>();
propertiesToSend.put(messagePropertyKey,messagePropertyKey);
messageToSend.setProperties(propertiesToSend);

CompletableFuture<Void> future = serviceClient.sendAsync(deviceId, messageToSend);
try {
    future.get();
}
catch (ExecutionException e) {
    System.out.println("Exception : " + e.getMessage());
}
```


## <a name="samples"></a><span data-ttu-id="e9f4e-116">샘플</span><span class="sxs-lookup"><span data-stu-id="e9f4e-116">Samples</span></span>

<span data-ttu-id="e9f4e-117">[IoT 장치 샘플](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)   </span><span class="sxs-lookup"><span data-stu-id="e9f4e-117">[IoT Device samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)   </span></span>  
[<span data-ttu-id="e9f4e-118">IoT 서비스 샘플</span><span class="sxs-lookup"><span data-stu-id="e9f4e-118">IoT Service samples</span></span>](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples)

<span data-ttu-id="e9f4e-119">앱에서 사용할 수 있는 [Azure IoT용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=iot)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="e9f4e-119">Explore more [sample Java code for Azure IoT](https://azure.microsoft.com/resources/samples/?platform=java&term=iot) you can use in your apps.</span></span>
