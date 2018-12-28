---
title: 지역 간에 동시에 VM 만들기 | Microsoft Docs
description: Java용 Azure SDK를 사용하여 여러 Azure 지역 간에 동시에 가상 머신을 만드는 샘플 코드
author: rloutlaw
manager: douge
ms.assetid: e5a36699-2d96-4571-84f9-a6af13f3c067
ms.service: Azure
ms.devlang: java
ms.topic: article
ms.date: 03/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: e20feb555c3a360eceae60c1569af9a00a5cd027
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893214"
---
# <a name="create-virtual-machines-across-multiple-regions-from-your-java-applications"></a><span data-ttu-id="7e551-103">Java 애플리케이션에서 여러 지역에 가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="7e551-103">Create virtual machines across multiple regions from your Java applications</span></span>

<span data-ttu-id="7e551-104">[이 샘플](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel)에서는 [Java용 Azure 관리 라이브러리](https://github.com/Azure/azure-sdk-for-java)를 사용하여 서로 다른 Azure 지역에서 동시에 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-104">[This sample](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) creates virtual machines in parallel across different Azure regions using the [Azure management libraries for Java](https://github.com/Azure/azure-sdk-for-java).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e551-105">샘플에서는 네 개 지역에서 [STANDARD_DS3_V2 크기](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes)의 Ubuntu 16.04 LTS를 실행하는 총 48개의 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-105">The sample creates a total of 48 VMs running Ubuntu 16.04 LTS of [size STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) across four regions.</span></span> <span data-ttu-id="7e551-106">샘플 코드는 종료하기 전에 이러한 가상 머신을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-106">The sample code deletes these virtual machines before exiting.</span></span> <span data-ttu-id="7e551-107">이 샘플을 VM의 기본 개수로 실행하기 전에 반드시 [서비스 제한 및 할당량을 확인](http://docs.microsoft.com/azure/azure-subscription-service-limits)하세요.</span><span class="sxs-lookup"><span data-stu-id="7e551-107">Make sure to [check your service limits and quota](http://docs.microsoft.com/azure/azure-subscription-service-limits) before running this sample with the default number of VMs.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="7e551-108">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="7e551-108">Run the sample</span></span>

<span data-ttu-id="7e551-109">[인증 파일](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md)을 만들고 컴퓨터에서 파일의 전체 경로가 포함된 `AZURE_AUTH_LOCATION` 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-109">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="7e551-110">그런 후 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-110">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel.git
cd compute-java-create-virtual-machines-across-regions-in-parallel
mvn clean compile exec:java
```

<span data-ttu-id="7e551-111">[GitHub에서 전체 샘플 코드(영문)](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java)를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-111">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="7e551-112">Azure를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="7e551-112">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="set-locations-and-counts-for-the-virtual-machines"></a><span data-ttu-id="7e551-113">가상 머신에 대한 위치 및 개수 설정</span><span class="sxs-lookup"><span data-stu-id="7e551-113">Set locations and counts for the virtual machines</span></span>

```java
// use a Map to define how where and how many VMs to create 
Map<Region, Integer> virtualMachinesByLocation = new HashMap<Region, Integer>();

// create 12 virtual machines in four regions
virtualMachinesByLocation.put(Region.US_EAST, 12);
virtualMachinesByLocation.put(Region.US_SOUTH_CENTRAL, 12);
virtualMachinesByLocation.put(Region.US_WEST, 12);
virtualMachinesByLocation.put(Region.US_NORTH_CENTRAL, 12);
```

<span data-ttu-id="7e551-114">이 `Map`은 샘플의 뒷부분에서 전 세계 VM 배포를 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-114">This `Map` is used later in the sample to set the distrubtion of the VMs worldwide.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="7e551-115">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="7e551-115">Create a resource group</span></span> 

```java
// logically associate the resources in the sample into a randomly named resource group
final String rgName = SdkContext.randomResourceName("rgCOPD", 24);
ResourceGroup resourceGroup = azure.resourceGroups().define(rgName)
                .withRegion(Region.US_EAST)
                .create();
```

<span data-ttu-id="7e551-116">샘플의 각 리소스는 이 리소스 그룹에서 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-116">Each resource in the sample is managed by this resource group.</span></span> <span data-ttu-id="7e551-117">이렇게 하면 나중에 리소스 그룹을 삭제하여 리소스를 쉽게 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-117">This makes the resources easy to clean up later by deleting the resource group.</span></span>

## <a name="define-the-virtual-machines"></a><span data-ttu-id="7e551-118">가상 머신 정의</span><span class="sxs-lookup"><span data-stu-id="7e551-118">Define the virtual machines</span></span>
```java
// list to store the VirtualMachine definitions
List<Creatable<VirtualMachine>> creatableVirtualMachines = new ArrayList<>();
    
// outer loop: iterate through each region included in the map
for (Map.Entry<Region, Integer> entry : virtualMachinesByLocation.entrySet()) {
    Region region = entry.getKey();
    Integer vmCount = entry.getValue();

    // Define one virtual network Creatable per region for the VMs to share
    String networkName = SdkContext.randomResourceName("vnetCOPD-", 20);
    Creatable<Network> networkCreatable = azure.networks().define(networkName)
           .withRegion(region)
           .withExistingResourceGroup(resourceGroup)
           .withAddressSpace("172.16.0.0/16");

    // Define one storage account Creatable per region for storing VM disks
    String storageAccountName = SdkContext.randomResourceName("stgcopd", 20);
    Creatable<StorageAccount> storageAccountCreatable = azure.storageAccounts()
        .define(storageAccountName)
              .withRegion(region)
              .withExistingResourceGroup(resourceGroup);

    // generate a common prefix for every VM name
    String linuxVMNamePrefix = SdkContext.randomResourceName("vm-", 15);

    // inner loop: iterate once for every VM instance in the region
    for (int i = 1; i <= vmCount; i++) {

        // Create one public IP address Creatable for each VM
        Creatable<PublicIpAddress> publicIpAddressCreatable = azure.publicIpAddresses()
             .define(String.format("%s-%d", linuxVMNamePrefix, i))
             .withRegion(region)
             .withExistingResourceGroup(resourceGroup)
             .withLeafDomainLabel(SdkContext.randomResourceName("pip", 10));

        publicIpCreatableKeys.add(publicIpAddressCreatable.key());

        // Create one virtual machine Creatable 
        Creatable<VirtualMachine> virtualMachineCreatable = azure.virtualMachines()
             .define(String.format("%s-%d", linuxVMNamePrefix, i))
             .withRegion(region)
             .withExistingResourceGroup(resourceGroup)
             .withNewPrimaryNetwork(networkCreatable)
             .withPrimaryPrivateIpAddressDynamic()
             .withNewPrimaryPublicIpAddress(publicIpAddressCreatable)
             .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
             .withRootUsername(userName)
             .withSsh(sshKey)
             .withSize(VirtualMachineSizeTypes.STANDARD_DS3_V2)
             .withNewStorageAccount(storageAccountCreatable);
        // add the virtual machine Creatable to the list     
        creatableVirtualMachines.add(virtualMachineCreatable); 
     }
}
```

<span data-ttu-id="7e551-119">위의 `for` 외부 루프는 각 지역을 반복하여 해당 지역의 모든 가상 머신에서 사용할 가상 네트워크 Creatable 개체와 저장소 계정 Creatable 개체를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-119">The outer `for` loop above iterates through each region, defining a virtual network Creatable and storage account Creatable for use by all virtual machines in that region.</span></span> <span data-ttu-id="7e551-120">관리 라이브러리를 사용할 때 필요한 경우에만 [Creatable 개체](java-sdk-azure-concepts.md#Creatables)를 사용하여 리소스를 만드는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7e551-120">Learn more about using [Creatables](java-sdk-azure-concepts.md#Creatables) to create resources only as needed when using the management libraries.</span></span>

<span data-ttu-id="7e551-121">`for` 내부 루프는 가상 컴퓨터에 대한 공용 IP 주소 Creatable 개체를 가져온 다음 이전에 정의한 가상 네트워크, 저장소 계정 및 공용 IP 주소에 대한 Creatable 개체를 사용하여 가상 컴퓨터 Creatable 개체를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-121">The inner `for` loop gets a public IP address Creatable for the virtual machine and then defines a virtual machine Creatable using the Creatables for the virtual network, storage account, and public IP address defined previously.</span></span>  <span data-ttu-id="7e551-122">그런 다음 `creatableVirtualMachines` 목록에 이 VirtualMachine Creatable 개체를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-122">This VirtualMachine Creatable is then added to the `creatableVirtualMachines` list.</span></span>

## <a name="create-the-virtual-machines"></a><span data-ttu-id="7e551-123">가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="7e551-123">Create the virtual machines</span></span>

```java
// create all virtual machines defined in the list, return all Creatable objects used
// including networks, public IP addresses, and storage accounts
CreatedResources<VirtualMachine> virtualMachines = azure.virtualMachines().create(creatableVirtualMachines);

// list the IDs of each virtual machine created 
for (VirtualMachine virtualMachine : virtualMachines.values()) {
    System.out.println(virtualMachine.id());
}

// call createdRelatedResource(key) to get the resources used to define the virtual machines. 
// Save the key at the time you define the Creatable to use CreatedResources like this
for (String publicIpCreatableKey : publicIpCreatableKeys) {
    PublicIPAddress pip = 
         (PublicIPAddress) virtualMachines.createdRelatedResource(publicIpCreatableKey);
}
```

<span data-ttu-id="7e551-124">`azure.virtualMachines().create(creatableVirtualMachines)` 호출은 `creatableVirtualMachines` 목록에 정의된 모든 가상 머신을 지역 전체에서 동시에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-124">The `azure.virtualMachines().create(creatableVirtualMachines)` call creates all of the virtual machines defined in the `creatableVirtualMachines` List in parallel across the regions.</span></span>

<span data-ttu-id="7e551-125">반환된 `CreatedResources<VirtualMachine>` 개체를 사용하여 반환된 `VirtualMachine` 형식 외에도 `create()` 메서드 중에 Azure 구독에 만들어진 모든 리소스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-125">Use the returned `CreatedResources<VirtualMachine>` object to access any resources created in the Azure subscription during the the `create()` method, not just the returned `VirtualMachine` type.</span></span> <span data-ttu-id="7e551-126">`createdRelatedResources()`에서 반환된 값을 올바른 형식으로 캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-126">Cast the returned value from `createdRelatedResources()` to the correct type.</span></span> 

<span data-ttu-id="7e551-127">[라이브러리 개념 문서](java-sdk-azure-concepts.md)에서 `Creatable<T>` 및 `CreatedResources` 사용에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7e551-127">Learn more about working with `Creatable<T>` and `CreatedResources` in our [library concepts article](java-sdk-azure-concepts.md).</span></span>

## <a name="delete-the-resource-group"></a><span data-ttu-id="7e551-128">리소스 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="7e551-128">Delete the resource group</span></span> 

```java
// finally block deletes the resource group before the code exits
// deleting a resource group deletes all resources created in it
finally {
    try {
        System.out.println("Deleting Resource Group: " + rgName);
        azure.resourceGroups().deleteByName(rgName);
        System.out.println("Deleted Resource Group: " + rgName);
    } catch (NullPointerException npe) {
        System.out.println("Did not create any resources in Azure. No clean up is necessary");
    } catch (Exception g) {
        g.printStackTrace();
    }
}
```

<span data-ttu-id="7e551-129">이 블록에서는 먼저 샘플에서 만든 리소스를 삭제한 후에 샘플이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-129">This block deletes resources created in the sample before the sample exits.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="7e551-130">샘플 설명</span><span class="sxs-lookup"><span data-stu-id="7e551-130">Sample explanation</span></span>

<span data-ttu-id="7e551-131">[GitHub에서 전체 샘플 코드(영문)](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel)를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-131">View the complete sample code on [Github](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel).</span></span>

<span data-ttu-id="7e551-132">이 샘플에서는 `Creatable` 개체를 사용하여 가상 머신을 호스팅하는 각 지역에 대한 가상 네트워크 및 저장소 계정을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-132">The sample uses `Creatable` objects to define a virtual network and storage account for each region hosting the virtual machines.</span></span> <span data-ttu-id="7e551-133">그런 다음 각 가상 머신의 공용 IP 주소에 대해 `Creatable` 개체가 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-133">`Creatable` objects are then defined for the public IP address for each virtual machine.</span></span> <span data-ttu-id="7e551-134">샘플은 이러한 `Creatable` 개체를 사용하여 가상 머신을 정의하고 `virtualMachineCreatable` 목록에 이 VM 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-134">The sample defines the virtual machines using these `Creatable` objects, and sample adds the VM definition to the `virtualMachineCreatable` list.</span></span>

<span data-ttu-id="7e551-135">코드에서 목록에 모든 가상 컴퓨터 정의를 추가하면 `azure.virtualMachines().create(creatableVirtualMachines)`는 Azure에서 각 가상 컴퓨터를 동시에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-135">After the code adds every virtual machine definition to the list, `azure.virtualMachines().create(creatableVirtualMachines)` creates each virtual machine in parallel in Azure.</span></span>

<span data-ttu-id="7e551-136">그런 다음 샘플 코드는 반환된 CreatedResources 개체에서 만들어진 모든 가상 머신에 대한 IP 주소를 가져와서 가상 머신 간에 부하를 분산할 수 있는 [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-136">The sample code then gets the IP addresses for all of the created virtual machines from the returned CreatedResources object to create a [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) to distribute load across the virtual machines.</span></span> 

<span data-ttu-id="7e551-137">`finally` 블록에서는 오류가 발생하더라도 Azure 구독에서 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-137">The `finally` block deletes the resources from your Azure subscription even in the case of an error.</span></span>

| <span data-ttu-id="7e551-138">샘플에 사용되는 클래스</span><span class="sxs-lookup"><span data-stu-id="7e551-138">Class used in sample</span></span> | <span data-ttu-id="7e551-139">메모</span><span class="sxs-lookup"><span data-stu-id="7e551-139">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="7e551-140">VirtualMachine</span><span class="sxs-lookup"><span data-stu-id="7e551-140">VirtualMachine</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | <span data-ttu-id="7e551-141">속성을 쿼리하고 가상 머신의 상태를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-141">Query properties and manage state of virtual machines.</span></span> <span data-ttu-id="7e551-142">`azure.virtualMachines().list()` 또는 이름별 또는 ID `azure.virtualMachines().getByResourceGroup()` 목록 형식으로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-142">Retrieved in list form from `azure.virtualMachines().list()` or by name or ID `azure.virtualMachines().getByResourceGroup()`</span></span>
| [<span data-ttu-id="7e551-143">VirtualMachineSizeTypes</span><span class="sxs-lookup"><span data-stu-id="7e551-143">VirtualMachineSizeTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | <span data-ttu-id="7e551-144">가상 머신을 정의할 때 `withSize()`에 대한 매개 변수로 사용할 [가상 머신 크기 옵션](https://azure.microsoft.com/pricing/details/virtual-machines/linux/)에 매핑되는 정적 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-144">Static values that map to [virtual machine size options](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) for use as a parameter to `withSize()` when defining a virtual machine.</span></span>
| [<span data-ttu-id="7e551-145">PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="7e551-145">PublicIpAddress</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._public_i_p_address) | <span data-ttu-id="7e551-146">`azure.publicIpAddresses().define()`을 통해 각 가상 컴퓨터에 대해 정의되지만 즉시 만들어지지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-146">Defined, but not immediately created, for each virtual machine through `azure.publicIpAddresses().define()`.</span></span> <span data-ttu-id="7e551-147">각 `Creatable`에 대한 키를 저장하고 나중에 `createdRelatedResource()`를 통해 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-147">Store the key for each `Creatable` and retrieve later through `createdRelatedResource()`</span></span>
| [<span data-ttu-id="7e551-148">KnownLinuxVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="7e551-148">KnownLinuxVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | <span data-ttu-id="7e551-149">가상 컴퓨터를 정의할 때 `withPopularLinuxImage()` 메서드에 대한 매개 변수로 사용되는 Linux 가상 컴퓨터 옵션 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-149">Set of Linux virtual machine options used as a parameter to `withPopularLinuxImage()` method when defining a virtual machine.</span></span>
| [<span data-ttu-id="7e551-150">네트워크</span><span class="sxs-lookup"><span data-stu-id="7e551-150">Network</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | <span data-ttu-id="7e551-151">샘플에서는 `azure.networks().define()`을 통해 각 지역에 대해 하나의 가상 네트워크를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7e551-151">The sample defines one virtual network for each region through  `azure.networks().define()` .</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7e551-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7e551-152">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]