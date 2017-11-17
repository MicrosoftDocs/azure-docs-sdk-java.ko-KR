---
title: "Java용 Azure Virtual Machine 라이브러리"
description: 
keywords: Azure, Java, SDK, API, Compute , Virtual Machines
author: douge
ms.author: douge
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: compute
ms.openlocfilehash: f9a816d5787e41a4ee4643b1bc66bf21192ea298
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2017
---
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="c1ec7-103">Azure 가상 컴퓨터 라이브러리</span><span class="sxs-lookup"><span data-stu-id="c1ec7-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="c1ec7-104">개요</span><span class="sxs-lookup"><span data-stu-id="c1ec7-104">Overview</span></span>

<span data-ttu-id="c1ec7-105">Linux 또는 Windows를 실행하는 요청 시 확장 가능한 컴퓨팅 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="c1ec7-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="c1ec7-106">Azure 가상 컴퓨터를 시작하려면 [Azure Portal을 사용하여 Linux 가상 컴퓨터 만들기](/azure/virtual-machines/linux/quick-create-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1ec7-106">To get started with Azure virtual machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="c1ec7-107">관리 API</span><span class="sxs-lookup"><span data-stu-id="c1ec7-107">Management API</span></span>

<span data-ttu-id="c1ec7-108">관리 API를 사용하여 코드에서 Azure의 Windows 및 Linux 가상 컴퓨터를 생성, 구성 및 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1ec7-108">Create, configure, and scale out Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="c1ec7-109">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ec7-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-compute</artifactId>
    <version>1.3.0</version>
</dependency>
```   


## <a name="example"></a><span data-ttu-id="c1ec7-110">예제</span><span class="sxs-lookup"><span data-stu-id="c1ec7-110">Example</span></span>

<span data-ttu-id="c1ec7-111">새 Azure 리소스 그룹에 새 Linux 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1ec7-111">Create a new Linux virtual machine in a new Azure resource group.</span></span>

```java
VirtualMachine newLinuxVm = azure.virtualMachines().define(linuxVmName)
            .withRegion(Region.US_EAST)
            .withNewResourceGroup("myResourceGroup")
            .withNewPrimaryNetwork("10.0.0.0/28")
            .withPrimaryPrivateIpAddressDynamic()
            .withoutPrimaryPublicIpAddress()
            .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
            .withRootUsername(userName)
            .withSshKey(key)
            .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
            .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c1ec7-112">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="c1ec7-112">Explore the Management APIs</span></span>](/java/api/overview/azure/virtualmachines/managementapi)


## <a name="samples"></a><span data-ttu-id="c1ec7-113">샘플</span><span class="sxs-lookup"><span data-stu-id="c1ec7-113">Samples</span></span>

<span data-ttu-id="c1ec7-114">[가상 컴퓨터 관리][1] </span><span class="sxs-lookup"><span data-stu-id="c1ec7-114">[Manage virtual machines][1] </span></span>  
<span data-ttu-id="c1ec7-115">[가상 네트워크 관리][6] </span><span class="sxs-lookup"><span data-stu-id="c1ec7-115">[Manage virtual networks][6] </span></span>  
<span data-ttu-id="c1ec7-116">[사용자 지정 이미지에서 가상 컴퓨터 만들기][2] </span><span class="sxs-lookup"><span data-stu-id="c1ec7-116">[Create a virtual machine from a custom image][2] </span></span>  
<span data-ttu-id="c1ec7-117">[지역 간에 동시에 가상 컴퓨터 만들기][5]  </span><span class="sxs-lookup"><span data-stu-id="c1ec7-117">[Create virtual machines across regions in parallel][5]  </span></span>  
<span data-ttu-id="c1ec7-118">[부하 분산 장치를 사용하여 가상 컴퓨터 확장 집합 만들기][7]</span><span class="sxs-lookup"><span data-stu-id="c1ec7-118">[Create a virtual machine scale set with a load balancer][7]</span></span>    

[1]: ../docs-ref-conceptual/java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[5]: ../docs-ref-conceptual/java-sdk-virtual-machines-in-parallel.md
[6]: ../docs-ref-conceptual/java-sdk-manage-virtual-networks.md
[7]: ../docs-ref-conceptual/java-sdk-manage-vm-scalesets.md

<span data-ttu-id="c1ec7-119">앱에서 사용할 수 있는 [Azure 가상 컴퓨터용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=VM)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ec7-119">Explore more [sample Java code for Azure virtual machines](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) you can use in your apps.</span></span>