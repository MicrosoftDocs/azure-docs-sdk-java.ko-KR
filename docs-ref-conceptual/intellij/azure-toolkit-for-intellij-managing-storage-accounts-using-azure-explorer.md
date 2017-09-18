---
title: "IntelliJ용 Azure Explorer를 사용하여 저장소 계정 관리"
description: "IntelliJ용 Azure 탐색기를 사용하여 Azure Storage 계정을 관리하는 방법을 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 44d2ade8a0900b60222f06dfb9f93c1df17228c8
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="f3f6e-103">IntelliJ용 Azure Explorer를 사용하여 저장소 계정 관리</span><span class="sxs-lookup"><span data-stu-id="f3f6e-103">Manage storage accounts by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="f3f6e-104">IntelliJ용 Azure 도구 키트의 일부인 Azure Explorer는 IntelliJ IDE(통합 개발 환경) 내에서 Azure 계정의 저장소 계정을 관리하기 위한 사용하기 쉬운 솔루션을 Java 개발자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a><span data-ttu-id="f3f6e-105">IntelliJ에서 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f3f6e-105">Create a storage account in IntelliJ</span></span>

<span data-ttu-id="f3f6e-106">Azure Explorer를 사용하여 저장소 계정을 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="f3f6e-107">[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]을 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for IntelliJ].</span></span> 

2. <span data-ttu-id="f3f6e-108">**Azure Explorer** 보기에서 **Azure** 노드를 확장하고 **저장소 계정**을 마우스 오른쪽 단추로 클릭한 후 **저장소 계정 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![저장소 계정 만들기 명령][CS01]

3. <span data-ttu-id="f3f6e-110">**저장소 계정 만들기** 대화 상자에서 다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![새 저장소 계정 만들기 대화 상자][CS02]

   * <span data-ttu-id="f3f6e-112">**이름**: 새 저장소 계정의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="f3f6e-113">**계정 종류**: 만들려는 저장소 계정의 형식을 지정합니다(예: “Blob Storage”).</span><span class="sxs-lookup"><span data-stu-id="f3f6e-113">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="f3f6e-114">자세한 내용은 [Azure 저장소 계정 정보]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-114">For more information, see [About Azure storage accounts].</span></span> 

   * <span data-ttu-id="f3f6e-115">**성능**: 선택한 게시자에서 사용할 저장소 계정 제품을 지정합니다(예: “프리미엄”).</span><span class="sxs-lookup"><span data-stu-id="f3f6e-115">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="f3f6e-116">자세한 내용은 [Azure Storage 확장성 및 성능 목표]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-116">For more information, see [Azure storage scalability and performance targets].</span></span> 

   * <span data-ttu-id="f3f6e-117">**복제**: 저장소 계정에 대한 복제를 지정합니다(예: “영역 중복”).</span><span class="sxs-lookup"><span data-stu-id="f3f6e-117">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="f3f6e-118">자세한 내용은 [Azure Storage 복제]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-118">For more information, see [Azure storage replication].</span></span> 

   * <span data-ttu-id="f3f6e-119">**구독**: 새 저장소 계정에 사용할 Azure 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-119">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="f3f6e-120">**위치**: 저장소 계정을 만들 위치를 지정합니다(예: “미국 서부”).</span><span class="sxs-lookup"><span data-stu-id="f3f6e-120">**Location**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="f3f6e-121">**리소스 그룹**: 가상 컴퓨터에 사용할 리소스 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-121">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="f3f6e-122">다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-122">Select one of the following options:</span></span>
      * <span data-ttu-id="f3f6e-123">**새로 만들기**: 새 리소스 그룹을 만들도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-123">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="f3f6e-124">**기존 그룹 사용**: Azure 계정에 연결된 리소스 그룹 목록에서 선택하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-124">**Use existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

4. <span data-ttu-id="f3f6e-125">위의 옵션을 모두 지정했으면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-125">When you have specified all of the preceding options, click **OK**.</span></span>

## <a name="create-a-storage-container-in-intellij"></a><span data-ttu-id="f3f6e-126">IntelliJ에서 저장소 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="f3f6e-126">Create a storage container in IntelliJ</span></span>

<span data-ttu-id="f3f6e-127">Azure Explorer를 사용하여 저장소 컨테이너를 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="f3f6e-128">Azure Explorer에서 컨테이너를 만들 저장소 계정을 마우스 오른쪽 단추로 클릭하고 **Blob 컨테이너 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-128">In the Azure Explorer view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Blob 컨테이너 만들기 명령][CC01]

2. <span data-ttu-id="f3f6e-130">**Blob 컨테이너 만들기** 대화 상자에서 컨테이너의 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="f3f6e-131">저장소 컨테이너 이름 지정에 대한 자세한 내용은 [컨테이너, BLOB 및 메타데이터 이름 지정 및 참조]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![저장소 컨테이너 만들기 대화 상자][CC02]

## <a name="delete-a-storage-container-in-intellij"></a><span data-ttu-id="f3f6e-133">IntelliJ에서 저장소 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="f3f6e-133">Delete a storage container in IntelliJ</span></span>

<span data-ttu-id="f3f6e-134">Azure Explorer를 사용하여 저장소 컨테이너를 삭제하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="f3f6e-135">Azure Explorer 보기에서 저장소 컨테이너를 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-135">In the Azure Explorer view, right-click the storage container, and then click **Delete**.</span></span>

   ![저장소 컨테이너 삭제 명령][DC01]

2. <span data-ttu-id="f3f6e-137">확인 창에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-137">In the confirmation window, click **Yes**.</span></span>

   ![저장소 컨테이너 삭제 확인 창][DC02]

## <a name="delete-a-storage-account-in-intellij"></a><span data-ttu-id="f3f6e-139">IntelliJ에서 저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="f3f6e-139">Delete a storage account in IntelliJ</span></span>

<span data-ttu-id="f3f6e-140">Azure Explorer를 사용하여 저장소 계정을 삭제하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="f3f6e-141">**Azure Explorer** 보기에서 저장소 계정을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-141">In the **Azure Explorer** view, right-click the storage account, and then select **Delete**.</span></span>

   ![저장소 계정 삭제 메뉴][DS01]

2. <span data-ttu-id="f3f6e-143">확인 창에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-143">In the confirmation window, click **Yes**.</span></span>

   ![저장소 계정 삭제 확인 창][DS02]

## <a name="next-steps"></a><span data-ttu-id="f3f6e-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f3f6e-145">Next steps</span></span>

<span data-ttu-id="f3f6e-146">Azure Storage 계정, 크기 및 가격 책정에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f3f6e-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="f3f6e-147">[Microsoft Azure 저장소 소개]</span><span class="sxs-lookup"><span data-stu-id="f3f6e-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="f3f6e-148">[Azure 저장소 계정 정보]</span><span class="sxs-lookup"><span data-stu-id="f3f6e-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="f3f6e-149">Azure Storage 계정 크기</span><span class="sxs-lookup"><span data-stu-id="f3f6e-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="f3f6e-150">[Azure의 Windows 저장소 계정 크기]</span><span class="sxs-lookup"><span data-stu-id="f3f6e-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="f3f6e-151">[Azure의 Linux 저장소 계정 크기]</span><span class="sxs-lookup"><span data-stu-id="f3f6e-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="f3f6e-152">Azure Storage 계정 가격 책정</span><span class="sxs-lookup"><span data-stu-id="f3f6e-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="f3f6e-153">[Windows 저장소 계정 가격 책정]</span><span class="sxs-lookup"><span data-stu-id="f3f6e-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="f3f6e-154">[Linux 저장소 계정 가격 책정]</span><span class="sxs-lookup"><span data-stu-id="f3f6e-154">[Linux storage-account pricing]</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Microsoft Azure 저장소 소개]: /azure/storage/storage-introduction
[Azure 저장소 계정 정보]: /azure/storage/storage-create-storage-account
[Azure Storage 복제]: /azure/storage/storage-redundancy
[Azure Storage 확장성 및 성능 목표]: /azure/storage/storage-scalability-targets
[컨테이너, BLOB, 메타데이터 이름 지정 및 참조]: http://go.microsoft.com/fwlink/?LinkId=255555

[Azure의 Windows 저장소 계정 크기]: /azure/virtual-machines/virtual-machines-windows-sizes
[Azure의 Linux 저장소 계정 크기]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows 저장소 계정 가격 책정]: /pricing/details/virtual-machines/windows/
[Linux 저장소 계정 가격 책정]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
