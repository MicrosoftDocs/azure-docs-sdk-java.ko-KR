---
title: Java용 Azure IoT Hub 라이브러리
description: Java용 Azure IoT Hub 라이브러리에 대한 참조 설명서
keywords: Azure, Java, SDK, API, 이벤트, IoT, 스트림, 디바이스, IoT Hub
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.technology: azure
ms.devlang: java
ms.service: iot-hub
ms.openlocfilehash: 497b2a72d851b8e43a48384c6f1a160e8a38cbe6
ms.sourcegitcommit: bb7286fad75a2bb43e6ce1a8f1b09e701147c9f9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047150"
---
# <a name="azure-iot-libraries-for-java"></a>Java용 Azure IoT 라이브러리

[Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-what-is-iot-hub)를 사용하여 IoT(사물 인터넷) 자산을 연결, 모니터링 및 제어합니다.

Azure IoT Hub를 시작하려면 [Java를 사용하여 IoT Hub에 디바이스 연결](/azure/iot-hub/iot-hub-java-java-getstarted)을 참조하세요.

## <a name="iot-service-library"></a>IoT 서비스 라이브러리

IoT 서비스 라이브러리를 사용하여 디바이스를 등록하고, 클라우드에서 등록된 디바이스로 메시지를 보냅니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.6.23</version>
</dependency>
```   

## <a name="iot-device-library"></a>Iot 디바이스 라이브러리

IoT 디바이스 라이브러리를 사용하여 클라우드로 메시지를 보내고 디바이스에서 메시지를 받습니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.31</version>
</dependency>
```

> [!div class="nextstepaction"]
> [클라이언트 API 탐색](/java/api/overview/azure/iot/client)   

## <a name="example"></a>예

Azure IoT Hub에서 디바이스로 메시지를 보냅니다.

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


## <a name="samples"></a>샘플

[IoT 장치 샘플](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)     
[IoT 서비스 샘플](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples)

앱에서 사용할 수 있는 [Azure IoT용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=iot)를 추가로 탐색합니다.
