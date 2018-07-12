---
title: Eclipse용 Azure Explorer를 사용하여 가상 머신 관리
description: Eclipse용 Azure 탐색기를 사용하여 Azure Virtual Machines를 관리하는 방법을 알아봅니다.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: c04f5225f0bb99898f69b26a4782aa57d75c4f22
ms.sourcegitcommit: 0ed7c5af0152125322ff1d265c179f35028f3c15
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38074568"
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="77f2d-103">Eclipse용 Azure Explorer를 사용하여 가상 머신 관리</span><span class="sxs-lookup"><span data-stu-id="77f2d-103">Manage virtual machines by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="77f2d-104">Eclipse용 Azure 도구 키트의 일부인 Azure Explorer는 Eclipse IDE(통합 개발 환경) 내에서 Azure 계정의 가상 머신을 관리하기 위한 사용하기 쉬운 솔루션을 Java 개발자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="77f2d-105">Eclipse에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="77f2d-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="77f2d-106">Azure Explorer를 사용하여 가상 머신을 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="77f2d-107">[Eclipse용 Azure 도구 키트에 대한 로그인 지침](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions)을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span></span>

2. <span data-ttu-id="77f2d-108">**Azure Explorer** 보기에서 **Azure** 노드를 확장하고 **Virtual Machines**를 마우스 오른쪽 단추로 클릭한 후 **VM 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   ![VM 만들기 명령][CR01]  

   <span data-ttu-id="77f2d-110">**새 Virtual Machine 만들기** 마법사가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="77f2d-111">**구독 선택** 창에서 구독을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![구독 선택 창][CR02]

4. <span data-ttu-id="77f2d-113">**Virtual Machine 이미지 선택** 창에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="77f2d-114">**위치**: 가상 머신을 만들 위치(예: *미국 서부*)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="77f2d-115">**게시자**: 가상 머신을 만드는 데 사용할 이미지를 만든 게시자를 지정합니다(예: *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="77f2d-115">**Publisher**: Specifies the publisher that created the image you'll use to create your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="77f2d-116">
  **제품**: 선택한 게시자에서 사용할 가상 머신 제품을 지정합니다(예: *JDK*).</span><span class="sxs-lookup"><span data-stu-id="77f2d-116">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="77f2d-117">
  **SKU**: 선택한 제품에서 사용할 SKU(Stockkeeping Unit)를 지정합니다(예: *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="77f2d-117">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="77f2d-118">**버전 번호**: 선택한 SKU에서 사용할 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-118">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![Virtual Machine 이미지 선택 창][CR03]

5. <span data-ttu-id="77f2d-120">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-120">Click **Next**.</span></span>

6. <span data-ttu-id="77f2d-121">**Virtual Machine 기본 설정** 창에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-121">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="77f2d-122">**Virtual Machine Name**: 새 가상 머신의 이름을 지정합니다. 이름은 문자로 시작하고 문자, 숫자 및 하이픈만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-122">**Virtual Machine Name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="77f2d-123">**크기**: 가상 컴퓨터용으로 할당할 코어 수 및 메모리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-123">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="77f2d-124">**사용자 이름**: 가상 머신을 관리하기 위해 만들 관리자 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-124">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="77f2d-125">**암호** 및 **확인**: 관리자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-125">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![Virtual Machine 기본 설정 창][CR04]

7. <span data-ttu-id="77f2d-127">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-127">Click **Next**.</span></span>

8. <span data-ttu-id="77f2d-128">**새 Storage 계정 만들기** 창에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-128">In the **Create New Storage Account** window, enter the following information:</span></span>

   * <span data-ttu-id="77f2d-129">**리소스 그룹**: 가상 머신에 사용할 리소스 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-129">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="77f2d-130">다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-130">Select one of the following options:</span></span>
     * <span data-ttu-id="77f2d-131">**새로 만들기**: 새 리소스 그룹을 만들도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-131">**Create new**: Specifies that you want to create a new resource group.</span></span>
     * <span data-ttu-id="77f2d-132">**기존 그룹 사용**: Azure 계정에 이미 연결된 리소스 그룹을 선택할 것임을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-132">**Use existing**: Specifies that you want to select a resource group that is already associated with your Azure account.</span></span>

       ![새 Storage 계정 만들기 대화 상자][CR05]

   * <span data-ttu-id="77f2d-134">**Storage 계정**: 가상 머신을 저장하는 데 사용할 Storage 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-134">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="77f2d-135">기존 저장소 계정을 사용하거나 새 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="77f2d-136">**Virtual Network** 및 **서브넷**: 가상 머신이 연결될 가상 네트워크 및 서브넷을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-136">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="77f2d-137">기존 네트워크 및 서브넷을 사용하거나 새 네트워크 및 서브넷을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="77f2d-138">**새로 만들기**를 선택하는 경우 다음과 같은 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-138">If you select **Create new**, the following dialog box is displayed:</span></span>

      ![새 Virtual Network 만들기 대화 상자][CR06]

9. <span data-ttu-id="77f2d-140">**연결된 리소스** 창에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-140">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="77f2d-141">**공용 IP 주소**: 가상 머신에 대한 외부 연결 IP 주소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="77f2d-142">새 IP 주소를 만들도록 선택하거나, 가상 머신에 공용 IP 주소가 없는 경우 **(없음)** 을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-142">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="77f2d-143">**네트워크 보안 그룹**: 가상 머신에 대한 선택적 네트워킹 방화벽을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="77f2d-144">기존 방화벽을 선택하거나, 가상 머신에서 네트워크 방화벽을 사용하지 않을 경우 **(없음)** 을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="77f2d-145">**가용성 집합**: 가상 머신이 속할 선택적 가용성 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="77f2d-146">기존 가용성 집합을 선택하거나, 새 가용성 집합을 만들거나, 가상 머신이 가용성 집합에 속하지 않을 경우 **(없음)** 을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong to an availability set, you can select **(None)**.</span></span>

   ![연결된 리소스 창][CR07]

10. <span data-ttu-id="77f2d-148">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-148">Click **Finish**.</span></span>  

    <span data-ttu-id="77f2d-149">새 가상 머신이 Azure Explorer 도구 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-149">Your new virtual machine is displayed in the Azure Explorer tool window.</span></span>

    ![새 Virtual Machine][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="77f2d-151">Eclipse에서 가상 컴퓨터 다시 시작</span><span class="sxs-lookup"><span data-stu-id="77f2d-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="77f2d-152">Eclipse에서 Azure Explorer를 사용하여 가상 머신을 다시 시작하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-152">To restart a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="77f2d-153">**Azure Explorer** 보기에서 가상 머신을 마우스 오른쪽 단추로 클릭하고 **다시 시작**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-153">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![가상 컴퓨터 다시 시작 명령][RE01]

1. <span data-ttu-id="77f2d-155">확인 창에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-155">In the confirmation window, click **Yes**.</span></span>

   ![다시 시작 확인 창][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="77f2d-157">Eclipse에서 가상 머신 종료</span><span class="sxs-lookup"><span data-stu-id="77f2d-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="77f2d-158">Eclipse에서 Azure Explorer를 사용하여 가상 머신을 종료하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-158">To shut down a running virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="77f2d-159">**Azure Explorer** 보기에서 가상 머신을 마우스 오른쪽 단추로 클릭하고 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-159">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![가상 컴퓨터 종료 명령][SH01]

1. <span data-ttu-id="77f2d-161">확인 창에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-161">In the confirmation window, click **Yes**.</span></span>

   ![가상 컴퓨터 종료 확인 창][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="77f2d-163">Eclipse에서 가상 머신 삭제</span><span class="sxs-lookup"><span data-stu-id="77f2d-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="77f2d-164">Eclipse에서 Azure Explorer를 사용하여 가상 머신을 삭제하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-164">To delete a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="77f2d-165">**Azure Explorer** 보기에서 가상 머신을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-165">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![가상 컴퓨터 삭제 명령][DE01]

1. <span data-ttu-id="77f2d-167">확인 창에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="77f2d-167">In the confirmation window, click **Yes**.</span></span>

   ![가상 컴퓨터 삭제 확인 창][DE02]

## <a name="next-steps"></a><span data-ttu-id="77f2d-169">다음 단계</span><span class="sxs-lookup"><span data-stu-id="77f2d-169">Next steps</span></span>

<span data-ttu-id="77f2d-170">Azure 가상 컴퓨터 크기 및 가격 책정에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="77f2d-170">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="77f2d-171">Azure Virtual Machines 크기</span><span class="sxs-lookup"><span data-stu-id="77f2d-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="77f2d-172">[Azure에서 Windows 가상 머신에 대한 크기]</span><span class="sxs-lookup"><span data-stu-id="77f2d-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="77f2d-173">[Azure에서 Linux 가상 머신에 대한 크기]</span><span class="sxs-lookup"><span data-stu-id="77f2d-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="77f2d-174">Azure Virtual Machines 가격 책정</span><span class="sxs-lookup"><span data-stu-id="77f2d-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="77f2d-175">[Windows 가상 컴퓨터 가격 책정]</span><span class="sxs-lookup"><span data-stu-id="77f2d-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="77f2d-176">[Linux 가상 컴퓨터 가격 책정]</span><span class="sxs-lookup"><span data-stu-id="77f2d-176">[Linux virtual-machine pricing]</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Azure에서 Windows 가상 머신에 대한 크기]: /azure/virtual-machines/virtual-machines-windows-sizes
[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Azure에서 Linux 가상 머신에 대한 크기]: /azure/virtual-machines/virtual-machines-linux-sizes
[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows 가상 컴퓨터 가격 책정]: /pricing/details/virtual-machines/windows/
[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/
[Linux 가상 컴퓨터 가격 책정]: /pricing/details/virtual-machines/linux/
[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
