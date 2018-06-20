---
title: Java를 사용하여 Azure 가상 네트워크 관리 | Microsoft Docs
description: Java 코드에서 Azure 가상 네트워크를 관리하는 샘플 코드
author: rloutlaw
manager: douge
ms.assetid: 92736911-3df6-46e7-b751-25bb36bf89b9
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 3d21cdd890912c1fc58fc65a79ba972b8327edeb
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931089"
---
# <a name="create-and-manage-azure-virtual-networks-from-your-java-apps"></a><span data-ttu-id="d483f-103">Java 앱에서 Azure 가상 네트워크 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="d483f-103">Create and manage Azure virtual networks from your Java apps</span></span>

<span data-ttu-id="d483f-104">[이 샘플](https://github.com/Azure-Samples/network-java-manage-virtual-network)에서는 제어하는 네트워크 세그먼트에서 Azure 리소스를 격리하는 [가상 네트워크](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-104">[This sample](https://github.com/Azure-Samples/network-java-manage-virtual-network) creates a [virtual network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) to isolate your Azure resources on network segment you control.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="d483f-105">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="d483f-105">Run the sample</span></span>

<span data-ttu-id="d483f-106">[인증 파일](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md)을 만들고 컴퓨터에서 파일의 전체 경로가 포함된 `AZURE_AUTH_LOCATION` 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="d483f-107">그런 후 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/network-java-manage-virtual-network.git
cd network-java-manage-virtual-network
mvn clean compile exec:java
```

<span data-ttu-id="d483f-108">[GitHub에서 전체 샘플 코드(영문)](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java)를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="d483f-109">Azure를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="d483f-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-network-security-group-to-block-internet-traffic"></a><span data-ttu-id="d483f-110">인터넷 트래픽을 차단하는 네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d483f-110">Create a network security group to block Internet traffic</span></span>

```java
// this NSG definition block traffic to and from the public Internet
NetworkSecurityGroup backEndSubnetNsg = azure.networkSecurityGroups()
              .define(vnet1BackEndSubnetNsgName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .defineRule("DenyInternetInComing")
                        .denyInbound()
                        .fromAddress("INTERNET")
                        .fromAnyPort()
                        .toAnyAddress()
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .defineRule("DenyInternetOutGoing")
                        .denyOutbound()
                        .fromAnyAddress()
                        .fromAnyPort()
                        .toAddress("INTERNET")
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .create();
```

<span data-ttu-id="d483f-111">이 [네트워크 보안 규칙](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)은 인바운드 및 아웃바운드 공용 인터넷 트래픽을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-111">This [network security rule](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) blocks both inbound and outbound public Internet traffic.</span></span> <span data-ttu-id="d483f-112">이 네트워크 보안 그룹은 가상 네트워크의 서브넷에 적용될 때까지 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-112">This network security group will not have an effect until applied to a subnet in your virtual network.</span></span>

## <a name="create-a-virtual-network-with-two-subnets"></a><span data-ttu-id="d483f-113">두 서브넷이 있는 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="d483f-113">Create a virtual network with two subnets</span></span>

```java
// create the a virtual network with two subnets
// assign the backend subnet a rule blocking public internet traffic
Network virtualNetwork1 = azure.networks().define(vnetName1)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .withAddressSpace("192.168.0.0/16")
                    .withSubnet(vnet1FrontEndSubnetName, "192.168.1.0/24")
                    .defineSubnet(vnet1BackEndSubnetName)
                        .withAddressPrefix("192.168.2.0/24")
                        .withExistingNetworkSecurityGroup(backEndSubnetNsg)
                        .attach()
                    .create();
```

<span data-ttu-id="d483f-114">백 엔드 서브넷에서 네트워크 보안 그룹에 설정된 규칙에 따라 인터넷 액세스를 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-114">The backend subnet denies Internet access usingfollowing the rules set in the network security group.</span></span> <span data-ttu-id="d483f-115">프런트 엔드 서브넷에서는 인터넷으로의 아웃바운드 트래픽을 허용하는 [기본 규칙](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-115">The front end subnet uses the [default rules](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) which allow outbound traffic to the Internet.</span></span>

## <a name="create-a-network-security-group-to-allow-inbound-http-traffic"></a><span data-ttu-id="d483f-116">인바운드 HTTP 트래픽을 허용하는 네트워크 보안 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d483f-116">Create a network security group to allow inbound HTTP traffic</span></span>
```java
// create a rule that allows inbound HTTP and blocks outbound Internet traffic
NetworkSecurityGroup frontEndSubnetNsg = azure.networkSecurityGroups()
               .define(vnet1FrontEndSubnetNsgName)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .defineRule("AllowHttpInComing")
                        .allowInbound()
                        .fromAddress("INTERNET")
                        .fromAnyPort()
                        .toAnyAddress()
                        .toPort(80)
                        .withProtocol(SecurityRuleProtocol.TCP)
                        .attach()
                    .defineRule("DenyInternetOutGoing")
                        .denyOutbound()
                        .fromAnyAddress()
                        .fromAnyPort()
                        .toAddress("INTERNET")
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .create();
```

<span data-ttu-id="d483f-117">이 네트워크 보안 규칙은 공용 인터넷에서 80 포트의 인바운드 트래픽을 열고 네트워크 내부에서 공용 인터넷으로 보내는 모든 아웃바운드 트래픽을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-117">This network security rule opens up inbound traffic on port 80 from the public Internet, and blocks all outbound traffic from inside the network to the public Internet.</span></span> 

## <a name="update-a-virtual-network"></a><span data-ttu-id="d483f-118">가상 네트워크 업데이트</span><span class="sxs-lookup"><span data-stu-id="d483f-118">Update a virtual network</span></span>
```java
// update the front end subnet to use the rules in the new network security group
virtualNetwork1.update()
          .updateSubnet(vnet1FrontEndSubnetName)
          .withExistingNetworkSecurityGroup(frontEndSubnetNsg)
          .parent()
          .apply();
```

<span data-ttu-id="d483f-119">이전 단계에서 만든 네트워크 보안 규칙을 사용하여 인바운드 HTTP 트래픽을 허용하도록 프런트 엔드 서브넷을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-119">Update the front end subnet to allow inbound HTTP traffic using the network security rule created in the previous step.</span></span>

## <a name="create-a-virtual-machine-on-a-subnet"></a><span data-ttu-id="d483f-120">서브넷에 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="d483f-120">Create a virtual machine on a subnet</span></span>
```java
// attach the new VM to the front end subnet on the virtual network
VirtualMachine frontEndVM = azure.virtualMachines().define(frontEndVmName)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .withExistingPrimaryNetwork(virtualNetwork1) 
                    .withSubnet(vnet1FrontEndSubnetName)
                    .withPrimaryPrivateIpAddressDynamic()
                    .withNewPrimaryPublicIpAddress(publicIpAddressLeafDnsForFrontEndVm)
                    .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                    .withRootUsername(userName)
                    .withSsh(sshKey)
                    .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
                    .create();
```

<span data-ttu-id="d483f-121">`withExistingPrimaryNetwork()` 및 `withSubnet()`은 이전 단계에서 만든 가상 네트워크에서 프런트 엔드 서브넷을 사용하도록 가상 컴퓨터를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-121">`withExistingPrimaryNetwork()` and `withSubnet()` configure the virtual machine to use the front-end subnet on the virtual network created in the previous steps.</span></span>

## <a name="list-virtual-networks-in-a-resource-group"></a><span data-ttu-id="d483f-122">리소스 그룹의 가상 네트워크 나열</span><span class="sxs-lookup"><span data-stu-id="d483f-122">List virtual networks in a resource group</span></span>
```java
// iterate over every virtual network in the resource group 
for (Network virtualNetwork : azure.networks().listByResourceGroup(rgName)) {
    // for each subnet on the virtual network, log the network address prefix 
    for (Map.Entry<String, Subnet> entry : virtualNetwork.subnets().entrySet()) {
        String subnetName = entry.getKey();
        Subnet subnet = entry.getValue();
        System.out.println("Address prefix for subnet " + subnetName + 
             " is " + subnet.addressPrefix());
    }
}
```       

<span data-ttu-id="d483f-123">외부 컬렉션을 사용하여 `Network` 개체를 나열하고 검사하거나 이 예제와 같이 중첩된 for-each 루프를 사용하여 각 네트워크의 각 자식 리소스를 반복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-123">You can list and inspect `Network` object using the outer collection or iterate through each child resource for each network using the nested for-each loop as seen in this example.</span></span>

## <a name="delete-a-virtual-network"></a><span data-ttu-id="d483f-124">가상 네트워크 삭제</span><span class="sxs-lookup"><span data-stu-id="d483f-124">Delete a virtual network</span></span>
```java
// if you already have the virtual network object it is easiest to delete by ID
azure.networks().deleteById(virtualNetwork1.id());

// Delete by resource group and name if you don't have the VirtualMachine object
azure.networks().deleteByResourceGroup(rgName,vnetName1);
```

<span data-ttu-id="d483f-125">가상 네트워크를 제거하면 네트워크의 서브넷이 삭제되지만 서브넷에 적용된 네트워크 보안 그룹 규칙은 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-125">Removing a virtual network deletes the subnets on the network but does not delete the network security group rules applied to the subnets.</span></span> <span data-ttu-id="d483f-126">이러한 정의는 다른 서브넷에 다시 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-126">Those definitions can be reapplied to other subnets.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="d483f-127">샘플 설명</span><span class="sxs-lookup"><span data-stu-id="d483f-127">Sample explanation</span></span>

<span data-ttu-id="d483f-128">이 샘플에서는 두 서브넷과 각 서브넷에 하나의 가상 컴퓨터가 있는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-128">This sample creates a virtual network with two subnets and with one virtual machine on each subnet.</span></span> <span data-ttu-id="d483f-129">백 서브넷은 공용 인터넷에서 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-129">The back subnet is cut off from the public Internet.</span></span> <span data-ttu-id="d483f-130">프런트 엔드 연결 서브넷에서 인터넷의 인바운드 HTTP 트래픽을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-130">The front-facing subnet accepts inbound HTTP traffic from the Internet.</span></span> <span data-ttu-id="d483f-131">가상 네트워크의 두 가상 컴퓨터는 모두 기본 네트워크 보안 그룹 규칙을 통해 서로 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-131">Both virtual machines in the virtual network communicate with each other through the default network security group rules.</span></span>

| <span data-ttu-id="d483f-132">샘플에 사용되는 클래스</span><span class="sxs-lookup"><span data-stu-id="d483f-132">Class used in sample</span></span> | <span data-ttu-id="d483f-133">참고 사항</span><span class="sxs-lookup"><span data-stu-id="d483f-133">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="d483f-134">네트워크</span><span class="sxs-lookup"><span data-stu-id="d483f-134">Network</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | <span data-ttu-id="d483f-135">`azure.networks().define()...create()`에서 만든 가상 네트워크의 로컬 개체 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-135">Local object representation of the virtual network created from `azure.networks().define()...create()` .</span></span> <span data-ttu-id="d483f-136">기존 가상 네트워크를 업데이트하려면 `update()...apply()` 흐름 체인을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-136">Use the `update()...apply()` fluent chain to update an existing virtual network.</span></span>
| [<span data-ttu-id="d483f-137">서브넷</span><span class="sxs-lookup"><span data-stu-id="d483f-137">Subnet</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._subnet) | <span data-ttu-id="d483f-138">`withSubnet()`을 사용하여 네트워크를 정의하거나 업데이트할 때 가상 네트워크에 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-138">Create subnets on the virtual network when defining or updating the network using `withSubnet()`.</span></span> <span data-ttu-id="d483f-139">`Network.subnets().get()` 또는 `Network.subnets().entrySet()`에서 서브넷의 개체 표현을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-139">Get object representations of a subnet from `Network.subnets().get()` or `Network.subnets().entrySet()`.</span></span> <span data-ttu-id="d483f-140">이러한 개체에는 서브넷 속성을 쿼리하는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-140">These objects have methods to query subnet properties.</span></span>
| [<span data-ttu-id="d483f-141">NetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="d483f-141">NetworkSecurityGroup</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network_security_group) | <span data-ttu-id="d483f-142">`azure.networkSecurityGroups().define()...create()` 흐름 체인을 사용하여 만든 다음 가상 네트워크에서 서브넷을 업데이트하거나 만들 때 서브넷에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d483f-142">Created using the `azure.networkSecurityGroups().define()...create()` fluent chain and then applied to subnets through the updating or creating subnets in a virtual network.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d483f-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d483f-143">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]