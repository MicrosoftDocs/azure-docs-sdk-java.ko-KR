---
title: Java용 Azure Network 라이브러리
description: Java용 Azure Network 관리 라이브러리에 대한 참조 설명서
keywords: Azure, Java, SDK, API, 네트워킹, 부하 분산, VNet, 서브넷
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: networking
ms.openlocfilehash: 4eb4f583da686508db9fb0c4346f2525502f669d
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593328"
---
# <a name="azure-network-libraries-for-java"></a>Java용 Azure Network 라이브러리

## <a name="overview"></a>개요

[Azure Networking](/azure/networking/networking-overview)을 사용하여 Azure 리소스를 연결하고, 트래픽을 필터링 및 분산하고, 라우팅을 관리합니다.

Azure Networking을 시작하려면 [첫 번째 가상 네트워크 만들기](/azure/virtual-network/virtual-network-get-started-vnet-subnet)를 참조하세요.

## <a name="management-api"></a>관리 API

관리 API를 사용하여 Azure [가상 네트워크](/azure/virtual-network/virtual-networks-overview), [ExpressRoute](/azure/expressroute/) 및 [Application Gateway](/azure/application-gateway/)를 만들고 관리합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-network</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a>예

단일 서브넷이 있는 새 가상 네트워크를 만듭니다.

```java
Network virtualNetwork1 = azure.networks().define(vnetName1)
        .withRegion(Region.US_EAST)
        .withExistingResourceGroup("myResourceGroup")
        .withAddressSpace("192.168.0.0/16")
        .defineSubnet("myVirtualNetwork")
            .withAddressPrefix("192.168.2.0/24")
            .attach()
        .create();
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/java/api/overview/azure/networking/management)

## <a name="samples"></a>샘플

[가상 네트워크 관리(영문)](https://github.com/Azure-Samples/network-java-manage-virtual-network)   
[네트워크 인터페이스 관리(영문)](https://github.com/Azure-Samples/network-java-manage-network-interface)   
[Application Gateway 관리](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways)   
[인터넷 연결 부하 분산 장치 관리(영문)](https://github.com/Azure-Samples/network-java-manage-internet-facing-load-balancers)   

앱에서 사용할 수 있는 [Azure Networking용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=network)을 추가로 탐색합니다.
