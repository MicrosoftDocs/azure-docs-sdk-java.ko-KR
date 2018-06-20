---
title: IntelliJ용 Azure 탐색기를 사용하여 Redis Cache 관리
description: IntelliJ용 Azure 탐색기를 사용하여 Azure Redis Cache를 관리하는 방법을 알아봅니다.
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
ms.openlocfilehash: 046ae0428d50a7f173f5ad15be53ffd8e66c11c5
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954184"
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="e26c8-103">IntelliJ용 Azure 탐색기를 사용하여 Redis Cache 관리</span><span class="sxs-lookup"><span data-stu-id="e26c8-103">Managing Redis Caches using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="e26c8-104">IntelliJ용 Azure 도구 키트의 일부인 Azure 탐색기는 IntelliJ IDE 내에서 Azure 계정의 Redis Cache를 관리하기 위한 사용하기 쉬운 솔루션을 Java 개발자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside the IntelliJ IDE.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a><span data-ttu-id="e26c8-105">IntelliJ를 사용하여 Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="e26c8-105">Create a Redis Cache by using IntelliJ</span></span>

<span data-ttu-id="e26c8-106">다음 단계에서는 Azure 탐색기를 사용하여 Redis Cache를 만드는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-106">The following steps walk you through the steps to create a redis cache using the Azure Explorer.</span></span>

1. <span data-ttu-id="e26c8-107">[IntelliJ용 Azure 도구 키트에 대한 로그인 지침] 문서의 단계를 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-107">Sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="e26c8-108">**Azure 탐색기** 도구 창에서 **Azure** 노드를 펼치고 **Redis Caches**를 마우스 오른쪽 단추로 클릭한 다음 **Redis Cache 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-108">In the **Azure Explorer** tool window, expand the **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Redis Cache 만들기 메뉴][CR01]

1. <span data-ttu-id="e26c8-110">**새 Redis Cache** 대화 상자가 표시되면 다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-110">When the **New Redis Cache** dialog box appears, specify the following options:</span></span>

   ![새 Redis Cache 만들기 대화 상자][CR02]

   <span data-ttu-id="e26c8-112">a.</span><span class="sxs-lookup"><span data-stu-id="e26c8-112">a.</span></span> <span data-ttu-id="e26c8-113">**DNS 이름**: 새 Redis Cache에 대한 DNS 하위 도메인을 지정합니다. 이 주소는 ".redis.cache.windows.net" 앞에 추가됩니다(예: *wingtiptoys.redis.cache.windows.net*).</span><span class="sxs-lookup"><span data-stu-id="e26c8-113">**DNS Name**: Specifies the DNS subdomain for the new redis cache, which are prepended to ".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="e26c8-114">나.</span><span class="sxs-lookup"><span data-stu-id="e26c8-114">b.</span></span> <span data-ttu-id="e26c8-115">**구독**: 새 Redis Cache에 사용할 Azure 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-115">**Subscription**: Specifies the Azure subscription you want to use for the new redis cache.</span></span>

   <span data-ttu-id="e26c8-116">다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-116">c.</span></span> <span data-ttu-id="e26c8-117">**리소스 그룹**: Redis Cache에 대한 리소스 그룹을 지정합니다. 다음 옵션 중 하나를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-117">**Resource Group**: Specifies the resource group for your redis cache; you need to choose one of the following options:</span></span> 
      * <span data-ttu-id="e26c8-118">**새로 만들기**: 새 리소스 그룹을 만들도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-118">**Create New**: Specifies that you want to create a new resource group.</span></span> 
      * <span data-ttu-id="e26c8-119">**기존 그룹 사용**: Azure 계정과 연결된 리소스 그룹 목록에서 선택하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span> 

   <span data-ttu-id="e26c8-120">d.</span><span class="sxs-lookup"><span data-stu-id="e26c8-120">d.</span></span> <span data-ttu-id="e26c8-121">**위치**: Redis Cache를 만들 위치를 지정합니다(예: *미국 서부*).</span><span class="sxs-lookup"><span data-stu-id="e26c8-121">**Location**: Specifies the location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="e26c8-122">e.</span><span class="sxs-lookup"><span data-stu-id="e26c8-122">e.</span></span> <span data-ttu-id="e26c8-123">**가격 책정 계층**: Redis Cache에서 사용하는 가격 책정 계층을 지정합니다. 이 설정은 클라이언트 연결 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines the number of client connections.</span></span> <span data-ttu-id="e26c8-124">자세한 내용은 [Redis Cache 가격]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e26c8-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="e26c8-125">f.</span><span class="sxs-lookup"><span data-stu-id="e26c8-125">f.</span></span> <span data-ttu-id="e26c8-126">**비SSL 포트**: Redis Cache에서 비SSL 연결을 허용하는지 여부를 지정합니다. 기본적으로 SSL 연결만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="e26c8-127">모든 Redis Cache 설정을 지정한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="e26c8-128">Redis Cache를 만들면 Azure 탐색기에서 해당 Redis Cache가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-128">After your redis cache has been created, it will be displayed in the Azure Explorer.</span></span>

   ![Azure 탐색기의 Redis Cache][CR03]

> [!NOTE]
>
> <span data-ttu-id="e26c8-130">Azure Redis Cache 설정을 구성하는 방법에 대한 자세한 내용은 [Azure Redis Cache 구성 방법]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e26c8-130">For more information about configuring your Azure redis cache settings, see [How to configure Azure Redis Cache].</span></span>
>

## <a name="display-the-properties-for-your-redis-cache-in-intellij"></a><span data-ttu-id="e26c8-131">IntelliJ에서 Redis Cache에 대한 속성 표시</span><span class="sxs-lookup"><span data-stu-id="e26c8-131">Display the properties for your Redis Cache in IntelliJ</span></span>

1. <span data-ttu-id="e26c8-132">[Azure 탐색기]에서 Redis Cache를 마우스 오른쪽 단추로 클릭하고 **속성 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-132">In the Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Redis Cache에 대한 속성을 표시하는 Azure 탐색기 컨텍스트 메뉴][SP01]

1. <span data-ttu-id="e26c8-134">Azure 탐색기에서 Redis Cache에 대한 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-134">The Azure Explorer displays the properties for your redis cache.</span></span>

   ![Redis Cache 속성][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a><span data-ttu-id="e26c8-136">IntelliJ를 사용하여 Redis Cache 삭제</span><span class="sxs-lookup"><span data-stu-id="e26c8-136">Delete your Redis Cache by using IntelliJ</span></span>

1. <span data-ttu-id="e26c8-137">[Azure 탐색기]에서 Redis Cache를 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-137">In the Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Redis Cache를 삭제하는 Azure 탐색기 컨텍스트 메뉴][DE01]

1. <span data-ttu-id="e26c8-139">Redis Cache를 삭제할지 묻는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e26c8-139">Click **Yes** when prompted to delete your redis cache.</span></span>

   ![Redis Cache 삭제 프롬프트][DE02]

## <a name="next-steps"></a><span data-ttu-id="e26c8-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e26c8-141">Next steps</span></span>

<span data-ttu-id="e26c8-142">Azure Redis Cache, 구성 설정 및 가격 책정에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e26c8-142">For more information about Azure redis caches, configuration settings and pricing, see the following links:</span></span>

* <span data-ttu-id="e26c8-143">[Azure Redis 캐시(영문)]</span><span class="sxs-lookup"><span data-stu-id="e26c8-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="e26c8-144">[Redis Cache 설명서]</span><span class="sxs-lookup"><span data-stu-id="e26c8-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="e26c8-145">[Redis Cache 가격]</span><span class="sxs-lookup"><span data-stu-id="e26c8-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="e26c8-146">[Azure Redis Cache 구성 방법]</span><span class="sxs-lookup"><span data-stu-id="e26c8-146">[How to configure Azure Redis Cache]</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Redis Cache 가격]: https://azure.microsoft.com/pricing/details/cache/
[Redis Cache Pricing]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis 캐시(영문)]: https://azure.microsoft.com/services/cache/
[Azure Redis Cache]: https://azure.microsoft.com/services/cache/
[Redis Cache 설명서]: /azure/redis-cache
[Redis Cache Documentation]: /azure/redis-cache
[Azure Redis Cache 구성 방법]: /azure/redis-cache/cache-configure
[How to configure Azure Redis Cache]: /azure/redis-cache/cache-configure
[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
