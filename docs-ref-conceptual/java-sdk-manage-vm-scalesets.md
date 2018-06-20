---
title: Java를 사용하여 가상 컴퓨터 확장 집합 관리 | Microsoft Docs
description: Java용 Azure SDK를 사용하여 Azure 가상 컴퓨터 확장 집합을 관리하는 샘플 코드
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 4653726b387369c18942b6c11392f15b9f0351f3
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931159"
---
# <a name="manage-azure-virtual-machine-scale-sets-from-your-java-applications"></a><span data-ttu-id="42571-103">Java 응용 프로그램에서 Azure 가상 컴퓨터 확장 집합 관리</span><span class="sxs-lookup"><span data-stu-id="42571-103">Manage Azure virtual machine scale sets from your Java applications</span></span>

<span data-ttu-id="42571-104">[이 샘플](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets)에서는 [Java 관리 라이브러리](https://github.com/Azure/azure-sdk-for-java)를 사용하여 [가상 컴퓨터 확장 집합](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42571-104">[This sample](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets) creates a  [virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview) using the [Java management libraries](https://github.com/Azure/azure-sdk-for-java).</span></span> 

## <a name="run-the-sample"></a><span data-ttu-id="42571-105">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="42571-105">Run the sample</span></span>

<span data-ttu-id="42571-106">[인증 파일](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md)을 만들고 컴퓨터에서 파일의 전체 경로가 포함된 `AZURE_AUTH_LOCATION` 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="42571-107">그런 후 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets.git
cd compute-java-manage-virtual-machine-scale-sets
mvn clean compile exec:java
```

<span data-ttu-id="42571-108">[GitHub에서 전체 샘플 코드(영문)](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java)를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="42571-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="42571-109">Azure를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="42571-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-virtual-network-for-the-scale-set"></a><span data-ttu-id="42571-110">확장 집합에 대한 가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="42571-110">Create a virtual network for the scale set</span></span>

```java
Network network = azure.networks().define(vnetName)
                    .withRegion(region)
                    .withNewResourceGroup(rgName)
                    .withAddressSpace("172.16.0.0/16")
                    .defineSubnet("Front-end")
                    .withAddressPrefix("172.16.1.0/24")
                    .attach()
                    .create();
```

<span data-ttu-id="42571-111">확장 집합 정의를 만들기 전에 가상 네트워크 및 부하 분산 장치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-111">Set up a virtual network and load balancer before creating the scale set definition.</span></span> <span data-ttu-id="42571-112">이러한 리소스는 확장 집합에서 초기 구성에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-112">The scale set uses these resources for its initial configuration.</span></span>

## <a name="create-a-load-balancer-to-distribute-load-across-the-scale-set"></a><span data-ttu-id="42571-113">부하 분산 장치를 만들어 확장 집합 간 부하 분산</span><span class="sxs-lookup"><span data-stu-id="42571-113">Create a load balancer to distribute load across the scale set</span></span>

```java
LoadBalancer loadBalancer1 = azure.loadBalancers().define(loadBalancerName1)
                    .withRegion(region)
                    .withExistingResourceGroup(rgName)
                    // assign a public IP address to the load balancer
                    .definePublicFrontend(frontendName)
                        .withExistingPublicIPAddress(publicIPAddress)
                        .attach()
                    // Add two backend address pools
                    .defineBackend(backendPoolName1)
                        .attach()
                    .defineBackend(backendPoolName2)
                        .attach()
                    // Add two health probes on 80 and 443
                    .defineHttpProbe(httpProbe)
                        .withRequestPath("/")
                        .withPort(80)
                        .attach()
                    .defineHttpProbe(httpsProbe)
                        .withRequestPath("/")
                        .withPort(443)
                        .attach()

                    // balance HTTP and HTTPs traffic
                    .defineLoadBalancingRule(httpLoadBalancingRule)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPort(80)
                        .withProbe(httpProbe)
                        .withBackend(backendPoolName1)
                        .attach()
                    .defineLoadBalancingRule(httpsLoadBalancingRule)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPort(443)
                        .withProbe(httpsProbe)
                        .withBackend(backendPoolName2)
                        .attach()

                    // Add NAT definitions to enable SSH and telnet to the VMs 
                    .defineInboundNatPool(natPool50XXto22)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPortRange(5000, 5099)
                        .withBackendPort(22)
                        .attach()
                    .defineInboundNatPool(natPool60XXto23)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPortRange(6000, 6099)
                        .withBackendPort(23)
                        .attach()
                    .create();
```

 <span data-ttu-id="42571-114">부하 분산 장치는 두 개의 백 엔드 네트워크 주소 풀을 정의합니다. 하나는 HTTP(`backendPoolName1`)에서 부하를 분산하고, 다른 하나는 HTTPS(`backendPoolName2`)에서 부하를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-114">The load balancer defines two backend network address pools-one to balance load across HTTP (`backendPoolName1`) and the other to balance load across HTTPS (`backendPoolName2`).</span></span>  <span data-ttu-id="42571-115">`defineHttpProbe()` 메서드는 부하 분산 장치에 대한 [상태 프로브 끝점](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-115">The `defineHttpProbe()` methods set up [health probe endpoints](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview) on the load balancers.</span></span> <span data-ttu-id="42571-116">NAT 규칙은 텔넷 및 SSH 액세스를 위해 확장 집합 가상 컴퓨터에서 22와 23 포트를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-116">NAT rules expose ports 22 and 23 on the scale set virtual machines for telnet and SSH access.</span></span>

## <a name="create-a-scale-set"></a><span data-ttu-id="42571-117">확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="42571-117">Create a scale set</span></span>
 
```java
 // Create a virtual machine scale set with three virtual machines
 // And, install Apache Web servers on them
VirtualMachineScaleSet virtualMachineScaleSet = azure.virtualMachineScaleSets()
       .define(vmssName)
                .withRegion(region)
                .withExistingResourceGroup(rgName)
                .withSku(VirtualMachineScaleSetSkuTypes.STANDARD_D3_V2)
                .withExistingPrimaryNetworkSubnet(network, "Front-end")
                .withExistingPrimaryInternetFacingLoadBalancer(loadBalancer1)
                .withPrimaryInternetFacingLoadBalancerBackends(backendPoolName1, backendPoolName2)
                .withPrimaryInternetFacingLoadBalancerInboundNatPools(natPool50XXto22, natPool60XXto23)
                .withoutPrimaryInternalLoadBalancer()
                .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                .withRootUsername(userName)
                .withSsh(sshKey)
                .withNewDataDisk(100)
                .withNewDataDisk(100, 1, CachingTypes.READ_WRITE)
                .withNewDataDisk(100, 2, 
                     CachingTypes.READ_WRITE, StorageAccountTypes.STANDARD_LRS)
                .withCapacity(3)
                // Use a VM extension to install Apache Web servers
                .defineNewExtension("CustomScriptForLinux")
                    .withPublisher("Microsoft.OSTCExtensions")
                    .withType("CustomScriptForLinux")
                    .withVersion("1.4")
                    .withMinorVersionAutoUpgrade()
                    .withPublicSetting("fileUris", fileUris)
                    .withPublicSetting("commandToExecute", installCommand)
                    .attach()
                .create();
```

<span data-ttu-id="42571-118">이전 단계에서 만든 가상 네트워크 정의와 부하 분산 장치 정의를 사용하여 세 개의 Linux 인스턴스(`withCapacity(3)`) 및 각각 세 개의 100GB 데이터 디스크가 있는 확장 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42571-118">Use the virtual network definition and load balancer definitions created in the previous step to create a scale set with three Linux instances (`withCapacity(3)`) and three 100GB data disks each.</span></span> <span data-ttu-id="42571-119">`defineNewExtension()` 메서드 체인은 각 VM에 Apache 웹 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-119">The `defineNewExtension()` method chain installs the Apache web server on each VM.</span></span>

## <a name="list-virtual-machine-scale-set-network-interfaces"></a><span data-ttu-id="42571-120">가상 컴퓨터 확장 집합 네트워크 인터페이스 나열</span><span class="sxs-lookup"><span data-stu-id="42571-120">List virtual machine scale set network interfaces</span></span>

```java
// List network interfaces on the scale set and iterate through them
PagedList<VirtualMachineScaleSetNetworkInterface> vmssNics = 
     virtualMachineScaleSet.listNetworkInterfaces();
for (VirtualMachineScaleSetNetworkInterface vmssNic : vmssNics) {
    System.out.println(vmssNic.id());
}
```

## <a name="get-ssh-connection-strings-for-each-scale-set-virtual-machine"></a><span data-ttu-id="42571-121">각 확장 집합 가상 컴퓨터에 대한 SSH 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="42571-121">Get SSH connection strings for each scale set virtual machine</span></span>

```java
for (VirtualMachineScaleSetVM instance : virtualMachineScaleSet.virtualMachines().list()) {
    System.out.println("Scale set virtual machine instance #" + instance.instanceId());
    System.out.println(instance.id());
    PagedList<VirtualMachineScaleSetNetworkInterface> networkInterfaces = 
         instance.listNetworkInterfaces();
    // Pick the first NIC on the instance and use its primary IP address
    VirtualMachineScaleSetNetworkInterface networkInterface = networkInterfaces.get(0);
    for (VirtualMachineScaleSetNicIPConfiguration ipConfig : networkInterface.ipConfigurations().values()) {
        if (ipConfig.isPrimary()) {
            List<LoadBalancerInboundNatRule> natRules = ipConfig.listAssociatedLoadBalancerInboundNatRules();
            for (LoadBalancerInboundNatRule natRule : natRules) {
                // find rule matching the inbound SSH port on the backend for the IP address
                // and return the SSH connection string to that port on the load balancer
                if (natRule.backendPort() == 22) {
                    System.out.println("SSH connection string: " + userName + 
                        "@" + publicIPAddress.fqdn() + ":" + natRule.frontendPort());
                break;
                }
            }
            break;
        }
    }
}
```

<span data-ttu-id="42571-122">이전에 만든 NAT 풀에서 가상 컴퓨터의 SSH 및 텔넷 포트(각각 22 및 23)를 부하 분산 장치의 포트에 매핑했습니다.</span><span class="sxs-lookup"><span data-stu-id="42571-122">The NAT pool created earlier mapped the SSH and telnet ports (22 and 23, respectively) on the virtual machines to ports on the load balancer.</span></span> <span data-ttu-id="42571-123">이 코드는 각 가상 컴퓨터에 대한 SSH 연결 문자열을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-123">This code builds the SSH connection string for each virtual machine.</span></span>

## <a name="stop-the-virtual-machine-scale-set"></a><span data-ttu-id="42571-124">가상 컴퓨터 확장 집합 중지</span><span class="sxs-lookup"><span data-stu-id="42571-124">Stop the virtual machine scale set</span></span>

```java
// stop (not deallocate) all scale set instances
virtualMachineScaleSet.powerOff();
```

<span data-ttu-id="42571-125">중지된 가상 컴퓨터는 예약된 리소스를 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-125">Stopped virtual machines continue to consume reserved resources.</span></span> <span data-ttu-id="42571-126">`deallocate()`를 사용하여 가상 컴퓨터에서 운영 체제를 중지하고 해당 계산 리소스를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-126">Use `deallocate()` to stop the operating system on the virtual machines and release their compute resources.</span></span>

## <a name="deallocate-the-virtual-machine-scale-set"></a><span data-ttu-id="42571-127">가상 컴퓨터 크기 집합 할당 해제</span><span class="sxs-lookup"><span data-stu-id="42571-127">Deallocate the virtual machine scale set</span></span>

```java
// deallocate the virtual machine scale set
virtualMachineScaleSet.deallocate();
```

<span data-ttu-id="42571-128">Deallocate()는 가상 컴퓨터에서 운영 체제를 종료하고 확장 집합 인스턴스에서 사용하는 계산 및 네트워크 리소스(예: IP 주소)를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-128">Deallocate() shuts down the operating system on the virtual machines and frees up the compute and network resources (such as IP addresses) used by the scale set instances.</span></span> <span data-ttu-id="42571-129">가상 컴퓨터에 연결된 모든 디스크(OS 포함)에 대해 저장소 요금이 계속 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-129">You continue to accrue storage charges for any disks (including the OS) attached to the virtual machines.</span></span>

## <a name="start-a-virtual-machine-scale-set"></a><span data-ttu-id="42571-130">가상 컴퓨터 확장 집합 시작</span><span class="sxs-lookup"><span data-stu-id="42571-130">Start a virtual machine scale set</span></span>

```java
// start a deallocated or stopped virtual machine scale set
virtualMachineScaleSet.start();
```

## <a name="update-the-number-of-virtual-machines-instances-in-the-scale-set"></a><span data-ttu-id="42571-131">확장 집합의 가상 컴퓨터 인스턴스 수 업데이트</span><span class="sxs-lookup"><span data-stu-id="42571-131">Update the number of virtual machines instances in the scale set</span></span>
```java
// increase the number of virtual machine scale set instances from three to six
virtualMachineScaleSet.update()
                    .withCapacity(6)
                    .apply();
```

<span data-ttu-id="42571-132">`withCapacity()`를 사용하여 확장 집합의 가상 컴퓨터 수를 조정하고, `withSku()`를 사용하여 각 가상 컴퓨터의 용량을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-132">Scale the number of virtual machines in the scale set using `withCapacity()` and scale the capacity of each virtual machine using `withSku()`.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="42571-133">샘플 설명</span><span class="sxs-lookup"><span data-stu-id="42571-133">Sample explanation</span></span>

<span data-ttu-id="42571-134">[샘플 코드](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java)에서는 먼저 통신하도록 설정된 확장 집합에 대한 가상 네트워크와 부하 분산 장치를 만들어 가상 컴퓨터 간에 트래픽을 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-134">[The sample code](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java) first creates a virtual network for the scale set to communicate across and a load balancer to distribute traffic across the virtual machines.</span></span> <span data-ttu-id="42571-135">`azure.virtualMachineScaleSets().define()...create()` 메서드 체인은 Apache 웹 서버를 실행하는 세 개의 Linux 인스턴스가 있는 확장 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="42571-135">The `azure.virtualMachineScaleSets().define()...create()` method chain creates the scale set with three Linux instances running the Apache web server.</span></span>    
   
| <span data-ttu-id="42571-136">샘플에 사용되는 클래스</span><span class="sxs-lookup"><span data-stu-id="42571-136">Class used in sample</span></span> | <span data-ttu-id="42571-137">참고 사항</span><span class="sxs-lookup"><span data-stu-id="42571-137">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="42571-138">VirtualMachineScaleSet</span><span class="sxs-lookup"><span data-stu-id="42571-138">VirtualMachineScaleSet</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set) | <span data-ttu-id="42571-139">확장 집합의 모든 가상 컴퓨터를 쿼리, 시작, 중지, 업데이트 및 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="42571-139">Query, start, stop, update and delete all virtual machines in the scale set.</span></span>
| [<span data-ttu-id="42571-140">VirtualMachineScaleSetVM</span><span class="sxs-lookup"><span data-stu-id="42571-140">VirtualMachineScaleSetVM</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_v_m) | <span data-ttu-id="42571-141">`virtualMachineScaleSet.virtualMachines().get()` 또는 `list()`에서 검색되고, 이를 사용하여 확장 집합의 가상 컴퓨터를 쿼리, 시작, 중지, 구성 및 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42571-141">Retrieved from `virtualMachineScaleSet.virtualMachines().get()` or `list()`, allows you to query, start, stop, configure and delete virtual machines in the scale set.</span></span>
| [<span data-ttu-id="42571-142">VirtualMachineScaleSetNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="42571-142">VirtualMachineScaleSetNetworkInterface</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_network_interface) | <span data-ttu-id="42571-143">`virtualMachineScaleSet.listNetworkInterfaces()`에서 반환되고, 확장 집합의 가상 컴퓨터에 있는 네트워크 인터페이스에 대한 읽기 전용 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="42571-143">Returned from `virtualMachineScaleSet.listNetworkInterfaces()`, read-only representation of a network interface on a virtual machine in a scale set.</span></span>
| [<span data-ttu-id="42571-144">VirtualMachineScaleSetSkuTypes</span><span class="sxs-lookup"><span data-stu-id="42571-144">VirtualMachineScaleSetSkuTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_sku_types) | <span data-ttu-id="42571-145">확장 집합 멤버에서 소비할 수 있는 리소스의 크기를 정의하는 데 사용되는 [가상 컴퓨터 확장 집합 계층](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/)을 설정하는 데 사용되는 정적 필드 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="42571-145">Class of static fields used to set the [virtual machine scale set tier](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) used to define how much resources scale set members can consume.</span></span>
| [<span data-ttu-id="42571-146">VirtualMachineScaleSetNicIpConfiguration</span><span class="sxs-lookup"><span data-stu-id="42571-146">VirtualMachineScaleSetNicIpConfiguration</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_nic_i_p_configuration) | <span data-ttu-id="42571-147">확장 집합 가상 컴퓨터에서 네트워크 인터페이스와 연결된 IP 구성을 쿼리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="42571-147">Used to query the IP configuration associated with a network interface on a scale set virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42571-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="42571-148">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]