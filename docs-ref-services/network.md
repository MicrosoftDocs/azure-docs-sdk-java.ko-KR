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
ms.openlocfilehash: bb74ccd8826df7b627e0b5f4e4ffd2da44b2642d
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823606"
---
# <a name="azure-network-libraries-for-java"></a><span data-ttu-id="09336-104">Java용 Azure Network 라이브러리</span><span class="sxs-lookup"><span data-stu-id="09336-104">Azure Network libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="09336-105">개요</span><span class="sxs-lookup"><span data-stu-id="09336-105">Overview</span></span>

<span data-ttu-id="09336-106">[Azure Networking](/azure/networking/networking-overview)을 사용하여 Azure 리소스를 연결하고, 트래픽을 필터링 및 분산하고, 라우팅을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="09336-106">Connect Azure resources, filter and balance traffic, and manage routing with [Azure Networking](/azure/networking/networking-overview).</span></span>

<span data-ttu-id="09336-107">Azure Networking을 시작하려면 [첫 번째 가상 네트워크 만들기](/azure/virtual-network/virtual-network-get-started-vnet-subnet)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09336-107">To get started with Azure Networking, see [Create your first virtual network](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span></span>

## <a name="management-api"></a><span data-ttu-id="09336-108">관리 API</span><span class="sxs-lookup"><span data-stu-id="09336-108">Management API</span></span>

<span data-ttu-id="09336-109">관리 API를 사용하여 Azure [가상 네트워크](/azure/virtual-network/virtual-networks-overview), [ExpressRoute](/azure/expressroute/) 및 [Application Gateway](/azure/application-gateway/)를 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="09336-109">Create and manage Azure [virtual networks](/azure/virtual-network/virtual-networks-overview) , [ExpressRoutes](/azure/expressroute/) , and [Application Gateways](/azure/application-gateway/) with the management API.</span></span>

<span data-ttu-id="09336-110">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="09336-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-network</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="09336-111">예</span><span class="sxs-lookup"><span data-stu-id="09336-111">Example</span></span>

<span data-ttu-id="09336-112">단일 서브넷이 있는 새 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09336-112">Create a new virtual network with a single subnet.</span></span>

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
> [<span data-ttu-id="09336-113">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="09336-113">Explore the Management APIs</span></span>](/java/api/overview/azure/networking/management)

## <a name="samples"></a><span data-ttu-id="09336-114">샘플</span><span class="sxs-lookup"><span data-stu-id="09336-114">Samples</span></span>

<span data-ttu-id="09336-115">[가상 네트워크 관리(영문)](https://github.com/Azure-Samples/network-java-manage-virtual-network) </span><span class="sxs-lookup"><span data-stu-id="09336-115">[Manage virtual networks](https://github.com/Azure-Samples/network-java-manage-virtual-network) </span></span>  
<span data-ttu-id="09336-116">[네트워크 인터페이스 관리(영문)](https://github.com/Azure-Samples/network-java-manage-network-interface) </span><span class="sxs-lookup"><span data-stu-id="09336-116">[Manage network interfaces](https://github.com/Azure-Samples/network-java-manage-network-interface) </span></span>  
<span data-ttu-id="09336-117">[Application Gateway 관리(영문)](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways) </span><span class="sxs-lookup"><span data-stu-id="09336-117">[Manage Application Gateways](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways) </span></span>  
[<span data-ttu-id="09336-118">인터넷 연결 부하 분산 장치 관리(영문)</span><span class="sxs-lookup"><span data-stu-id="09336-118">Manage internet facing load balancers</span></span>](https://github.com/Azure-Samples/network-java-manage-internet-facing-load-balancers)   

<span data-ttu-id="09336-119">앱에서 사용할 수 있는 [Azure Networking용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=network)을 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="09336-119">Explore more [sample Java code for Azure Networking](https://azure.microsoft.com/resources/samples/?platform=java&term=network) you can use in your apps.</span></span>
