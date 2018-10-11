---
title: Java를 사용하여 Azure 가상 머신 관리 | Microsoft Docs
description: Java용 Azure SDK를 사용하여 Azure 가상 머신을 관리하는 샘플 코드
author: rloutlaw
manager: douge
ms.assetid: 88629aee-6279-433e-a08b-4f8e290446d0
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: e3048b3317477f4b1fb8edf93e4bebad6b7fafce
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893614"
---
# <a name="manage-azure-virtual-machines-from-your-java-applications"></a><span data-ttu-id="3799c-103">Java 응용 프로그램에서 Azure 가상 머신 관리</span><span class="sxs-lookup"><span data-stu-id="3799c-103">Manage Azure virtual machines from your Java applications</span></span>

<span data-ttu-id="3799c-104">[이 샘플](https://github.com/Azure-Samples/compute-java-manage-vm/)에서는 [Java용 Azure 관리 라이브러리](https://github.com/Azure/azure-sdk-for-java)를 사용하여 Azure 가상 머신을 만들고 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-104">[This sample](https://github.com/Azure-Samples/compute-java-manage-vm/) uses the [Azure management libraries for Java](https://github.com/Azure/azure-sdk-for-java) to create and work with Azure virtual machines.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="3799c-105">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="3799c-105">Run the sample</span></span>

<span data-ttu-id="3799c-106">[인증 파일](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md)을 만들고 컴퓨터에서 파일의 전체 경로가 포함된 `AZURE_AUTH_LOCATION` 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="3799c-107">그런 후 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-manage-vm.git
cd compute-java-manage-vm
mvn clean compile exec:java
```

<span data-ttu-id="3799c-108">[GitHub에서 전체 샘플 코드(영문)](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java)를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="3799c-109">Azure를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="3799c-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-windows-virtual-machine"></a><span data-ttu-id="3799c-110">Windows 가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="3799c-110">Create a Windows virtual machine</span></span>

```java
// Prepare a data disk for VM
Disk dataDisk = azure.disks().define(SdkContext.randomResourceName("dsk", 30))
            .withRegion(region)
            .withNewResourceGroup(rgName)
            .withData()
            .withSizeInGB(50)
            .create();

// create the windows virtual machine with the data disk            
VirtualMachine windowsVM = azure.virtualMachines().define(windowsVmName)
            .withRegion(region)
            .withNewResourceGroup(rgName)
            .withNewPrimaryNetwork("10.0.0.0/28")
            .withPrimaryPrivateIpAddressDynamic()
            .withoutPrimaryPublicIpAddress()
            .withPopularWindowsImage(KnownWindowsVirtualMachineImage.WINDOWS_SERVER_2012_R2_DATACENTER)
            .withAdminUsername(userName)
            .withAdminPassword(password)
            .withNewDataDisk(10)
            .withNewDataDisk(dataDiskCreatable)
            .withExistingDataDisk(dataDisk)
            .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
            .create();
```

<span data-ttu-id="3799c-111">이 코드에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-111">This code:</span></span>   

0. <span data-ttu-id="3799c-112">가상 컴퓨터에서 사용할 `Disk` Creatable을 50GB 크기와 임의의 이름으로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-112">Defines a `Disk` Creatable with a 50GB size and random name for use with a virtual machine.</span></span>
0. <span data-ttu-id="3799c-113">`azure.virtualMachines().define()..create()` 체인을 사용하여 Windows Server 2012 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-113">Uses the `azure.virtualMachines().define()..create()` chain to create the Windows Server 2012 virtual machine.</span></span> <span data-ttu-id="3799c-114">API에서 가상 머신과 동일한 시간에 이전 단계에서 정의된 `Disk`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-114">The API creates the `Disk` defined in the previous step the same time as the virtual machine.</span></span> <span data-ttu-id="3799c-115">10GB 데이터 디스크도 `withNewDataDisk(10)`를 통해 가상 머신에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-115">A 10GB data disk is also attached to the virtual machine through `withNewDataDisk(10)`.</span></span>

<span data-ttu-id="3799c-116">[Creatable<T> 개체](java-sdk-azure-concepts.md#Creatables)를 사용하여 리소스의 로컬 표현을 정의하고 다른 Azure 리소스에 필요한 만큼 리소스를 만드는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="3799c-116">Learn more about using [Creatable<T> objects](java-sdk-azure-concepts.md#Creatables) to define local representations of resources and create them just as other Azure resources need them.</span></span>

## <a name="stop-start-and-restart-a-virtual-machine"></a><span data-ttu-id="3799c-117">가상 머신 중지, 시작 및 다시 시작</span><span class="sxs-lookup"><span data-stu-id="3799c-117">Stop, start, and restart a virtual machine</span></span>

```java
// look up a virtual machine by its ID and then restart, stop, and start it
azureVM = azure.getVirtualMachine.getById(windowsVM.id());

azureVM.restart();
azureVM.powerOff();
azureVM.start();
```

<span data-ttu-id="3799c-118">`powerOff()`는 가상 컴퓨터 운영 체제를 중지하지만 해당 리소스의 할당을 취소하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-118">`powerOff()` stops the virtual machine operating system but does not deallocate its resources.</span></span>

## <a name="add-a-virtual-machine-to-an-existing-network"></a><span data-ttu-id="3799c-119">기존 네트워크에 가상 컴퓨터 추가</span><span class="sxs-lookup"><span data-stu-id="3799c-119">Add a virtual machine to an existing network</span></span>

```java
// Get the virtual network the current virtual machine is using
Network network = windowsVM.getPrimaryNetworkInterface().primaryIPConfiguration().getNetwork();

// Create a Linux VM in the same subnet
VirtualMachine linuxVM = azure.virtualMachines().define(linuxVmName)
           .withRegion(region)
           .withExistingResourceGroup(rgName)
           .withExistingPrimaryNetwork(network)
           .withSubnet("subnet1") // default subnet name when no name specified at creation
           .withPrimaryPrivateIPAddressDynamic()
           .withoutPrimaryPublicIPAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withRootPassword(password)
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
```

<span data-ttu-id="3799c-120">`withPopularLinuxImage`를 사용하여 Windows VM 대신 Linux VM을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-120">Use `withPopularLinuxImage` to define a Linux VM instead of a Windows one.</span></span>


## <a name="list-virtual-machines"></a><span data-ttu-id="3799c-121">가상 머신 나열</span><span class="sxs-lookup"><span data-stu-id="3799c-121">List virtual machines</span></span>

```java
// get a list of VMs in the same resource group as an existing VM
String resourceGroupName = windowsVM.resourceGroupName();
PagedList<VirtualMachine> resourceGroupVMs = azure.virtualMachines()
        .listByResourceGroup(resourceGroupName); 

// for each vitual machine in the resource group, log their name and plan
for (VirtualMachine virtualMachine : azure.virtualMachines().listByResourceGroup(resourceGroupName)) {
    System.out.println("VM " + virtualMachine.computerName() + 
        " has plan " + virtualMachine.plan());
}
```

<span data-ttu-id="3799c-122">`azure.virtualMachines().list()`를 사용하여 구독에 대한 가상 머신을 모두 나열하고, `tags()`에서 반환한 Map을 반복하여 리소스 그룹에서 태그가 지정된 가상 머신 컬렉션을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-122">List all virtual machines for a subscription using `azure.virtualMachines().list()` and iterate through the Map returned by `tags()` to manage tagged collections of virtual machines across resource groups.</span></span>

## <a name="update-a-virtual-machine"></a><span data-ttu-id="3799c-123">가상 머신 업데이트</span><span class="sxs-lookup"><span data-stu-id="3799c-123">Update a virtual machine</span></span>

```java
// add a 10GB data disk to the virtual machine
windowsVM.update()
     .withNewDataDisk(10)
     .apply();
```

<span data-ttu-id="3799c-124">`update()...apply()` 및 `define()...create()`를 통해 가상 컴퓨터를 만들 때 해당 가상 컴퓨터를 구성하는 데 사용한 것과 동일한 메서드를 사용하여 가상 컴퓨터 구성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-124">Update the virtual machine configuration using `update()...apply()` and the same methods used to configure the virtual machine when created through `define()...create()`.</span></span>

## <a name="delete-a-virtual-machine"></a><span data-ttu-id="3799c-125">가상 머신 삭제</span><span class="sxs-lookup"><span data-stu-id="3799c-125">Delete a virtual machine</span></span>

```java
// delete by ID if you already are working with the VM object
azure.virtualMachines().deleteById(windowsVM.id());

// delete by resource group and name
azure.virtualMachines().deleteByResourceGroup(rgName,windowsVmName);
```

## <a name="sample-explanation"></a><span data-ttu-id="3799c-126">샘플 설명</span><span class="sxs-lookup"><span data-stu-id="3799c-126">Sample explanation</span></span>

<span data-ttu-id="3799c-127">[샘플 코드](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java)에서는 50GB 데이터 디스크가 있는 Windows 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-127">[The sample code](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) creates a Windows virtual machine with a 50GB data disk.</span></span> <span data-ttu-id="3799c-128">그런 다음 샘플에서 두 번째 10GB 데이터 디스크를 만들어 이 Windows 가상 머신에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-128">The sample then creates a second 10GB data disk and attaches it to this Windows virtual machine.</span></span>
<span data-ttu-id="3799c-129">그런 다음 샘플에서 Windows 가상 머신과 동일한 가상 네트워크에 Linux 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-129">Then the sample creates a Linux virtual machine in the same virtual network as the Windows virtual machine.</span></span>

<span data-ttu-id="3799c-130">샘플에서는 두 가상 머신에 대한 정보를 모두 기록하고 완료하기 전에 모두 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-130">The sample logs information about both virtual machines and deletes them both before completing.</span></span>

| <span data-ttu-id="3799c-131">샘플에 사용되는 클래스</span><span class="sxs-lookup"><span data-stu-id="3799c-131">Class used in sample</span></span> | <span data-ttu-id="3799c-132">메모</span><span class="sxs-lookup"><span data-stu-id="3799c-132">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="3799c-133">VirtualMachine</span><span class="sxs-lookup"><span data-stu-id="3799c-133">VirtualMachine</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | <span data-ttu-id="3799c-134">속성을 쿼리하고 가상 머신의 상태를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-134">Query properties and manage state of virtual machines.</span></span> <span data-ttu-id="3799c-135">`azure.virtualMachines().list()` 또는 이름별 또는 ID `azure.virtualMachines().getByResourceGroup()` 목록 형식으로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-135">Retrieved in list form  with`azure.virtualMachines().list()` or by name or ID `azure.virtualMachines().getByResourceGroup()`</span></span>
| [<span data-ttu-id="3799c-136">VirtualMachineSizeTypes</span><span class="sxs-lookup"><span data-stu-id="3799c-136">VirtualMachineSizeTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | <span data-ttu-id="3799c-137">[가상 머신 크기 옵션](https://azure.microsoft.com/pricing/details/virtual-machines/linux/)에 매핑되는 정적 값이 있는 클래스입니다. `withSize()` 메서드에서 VM에 할당된 리소스를 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-137">Class with static values that map to [virtual machine size options](https://azure.microsoft.com/pricing/details/virtual-machines/linux/), used by the `withSize()` method to define the resources allocated to the VM.</span></span>
| [<span data-ttu-id="3799c-138">디스크</span><span class="sxs-lookup"><span data-stu-id="3799c-138">Disk</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk) | <span data-ttu-id="3799c-139">`withData()`를 사용하여 데이터를 저장하거나 디스크를 정의할 때 적절한 `withLinux` 또는 `withWindows` 메서드 사용하여 운영 체제 이미지를 저장할 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-139">Create a disk to store data using `withData()` or operating system image using the appropriate `withLinux` or `withWindows` method when defining the disk.</span></span> <span data-ttu-id="3799c-140">만들 때(`using withNewDataDisk` 또는 `withExistingDataDisk`) 또는 VirtualMachine 개체의 `update()..apply()`로 만든 후에 가상 머신에 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-140">Attach disks to virtual machines either at the time of creation (`using withNewDataDisk` or `withExistingDataDisk`) or after creation by `update()..apply()` on the VirtualMachine object.</span></span>
| [<span data-ttu-id="3799c-141">DiskSkuTypes</span><span class="sxs-lookup"><span data-stu-id="3799c-141">DiskSkuTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk_sku_types) | <span data-ttu-id="3799c-142">표준 또는 [프리미엄](https://docs.microsoft.com/azure/storage/storage-premium-storage) 저장소 계획이 있는 디스크를 정의하는 정적 값이 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-142">Class with static values to define a disk with a standard or [premium](https://docs.microsoft.com/azure/storage/storage-premium-storage) storage plan.</span></span>
| [<span data-ttu-id="3799c-143">KnownLinuxVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="3799c-143">KnownLinuxVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | <span data-ttu-id="3799c-144">가상 머신을 정의할 때 `withPopularLinuxImage()` 메서드와 함께 사용할 Linux 가상 머신 옵션 집합이 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-144">Class with a set of Linux virtual machine options for use with the `withPopularLinuxImage()` method when defining a virtual machine.</span></span>
| [<span data-ttu-id="3799c-145">KnownWindowsVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="3799c-145">KnownWindowsVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_windows_virtual_machine_image) | <span data-ttu-id="3799c-146">가상 컴퓨터를 정의할 때 `withPopularWindowsImage()` 메서드와 함께 사용할 Windows 가상 컴퓨터 이미지 옵션 집합이 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3799c-146">Class with a set of Windows virtual machine image options for use with the `withPopularWindowsImage()` method when defining a virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3799c-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3799c-147">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]