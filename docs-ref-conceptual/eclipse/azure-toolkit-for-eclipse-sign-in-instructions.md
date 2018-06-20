---
title: Eclipse용 Azure 도구 키트에 대한 로그인 지침
description: Eclipse용 Azure 도구 키트를 사용하여 Microsoft Azure에 로그인하는 방법을 알아봅니다.
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
ms.openlocfilehash: eb6099ab0c19bf3588cb7fd668f070771e58fe74
ms.sourcegitcommit: 8230cf6b15ac51a9f8a209e9b76411a0385029aa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2018
ms.locfileid: "34216027"
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="9b8c0-103">Eclipse용 Azure 도구 키트에 대한 Azure 로그인 지침</span><span class="sxs-lookup"><span data-stu-id="9b8c0-103">Azure Sign In Instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="9b8c0-104">Eclipse용 Azure 도구 키트는 Azure 계정에 로그인하는 두 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="9b8c0-105">**자동** - 이 방법을 사용하는 경우 서비스 주체 데이터를 포함하는 자격 증명 파일을 만든 다음 해당 자격 증명 파일을 사용하여 Azure 계정에 자동으로 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-105">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use the credentials file to automatically sign into your Azure account.</span></span>
  * <span data-ttu-id="9b8c0-106">**대화형** - 이 방법을 사용하는 경우 Azure 계정에 로그인할 때마다 Azure 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-106">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>

<span data-ttu-id="9b8c0-107">다음 섹션의 단계에서는 각 방법을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-107">The steps in the following sections will describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a><span data-ttu-id="9b8c0-108">Azure 계정에 자동으로 로그인 및 나중에 사용할 자격 증명 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="9b8c0-108">Signing into your Azure account automatically and creating a credentials file to use in the future</span></span>

<span data-ttu-id="9b8c0-109">다음 단계에서는 서비스 주체 데이터를 포함하는 자격 증명 파일을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-109">The following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="9b8c0-110">이러한 단계를 완료한 후 Eclipse에서는 사용자가 프로젝트를 열 때마다 해당 자격 증명 파일을 자동으로 사용해서 Azure에 자동으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-110">Once you have completed these steps, Eclipse will automatically use the credentials file to automatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="9b8c0-111">Eclipse로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-111">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="9b8c0-112">**도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-112">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure 로그인을 위한 Eclipse 메뉴][A01]

1. <span data-ttu-id="9b8c0-114">**Azure 로그인** 대화 상자가 나타나면 **자동**을 선택한 다음 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-114">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![로그인 대화 상자][A02]

1. <span data-ttu-id="9b8c0-116">**Azure 로그인** 대화 상자가 나타나면 Azure 자격 증명을 입력하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-116">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Azure 로그인 대화 상자][A03]

1. <span data-ttu-id="9b8c0-118">**인증 파일 만들기** 대화 상자가 나타나면 사용할 구독을 선택하고 대상 디렉터리를 선택한 후 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-118">When the **Create authentication files** dialog box appears, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Azure 로그인 대화 상자][A04]

1. <span data-ttu-id="9b8c0-120">**서비스 주체 만들기 상태** 대화 상자가 표시됩니다. 파일이 성공적으로 만들어진 후에 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-120">The **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![서비스 주체 만들기 상태 대화 상자][A05]

1. <span data-ttu-id="9b8c0-122">**Azure 로그인** 대화 상자가 나타나면 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-122">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Azure 로그인 대화 상자][A06]

1. <span data-ttu-id="9b8c0-124">**구독 선택** 대화 상자가 나타나면 사용하려는 구독을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-124">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![구독 선택 대화 상자 관리][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="9b8c0-126">자동으로 로그인되었을 때 Azure 계정에서 로그아웃</span><span class="sxs-lookup"><span data-stu-id="9b8c0-126">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="9b8c0-127">이전 섹션의 단계를 구성한 후에는 Eclipse를 다시 시작할 때마다 Azure 도구 키트를 통해 Azure 계정에서 자동으로 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-127">After you have configured the steps in the previous section, the Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="9b8c0-128">그러나 Azure 계정에서 로그아웃하고 Azure 도구 키트를 통해 자동으로 로그인되지 않게 하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-128">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, use the following steps.</span></span>

1. <span data-ttu-id="9b8c0-129">Eclipse에서 **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그아웃**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-129">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Azure 로그아웃을 위한 Eclipse 메뉴][L01]

1. <span data-ttu-id="9b8c0-131">**Azure 로그아웃** 대화 상자가 나타나면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-131">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![로그아웃 대화 상자][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="9b8c0-133">이미 만든 자격 증명 파일을 사용하여 Azure 계정에 자동으로 로그인</span><span class="sxs-lookup"><span data-stu-id="9b8c0-133">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="9b8c0-134">Eclipse를 사용할 때 Azure에서 로그아웃된 경우 Azure 계정으로 자동으로 로그인하려면 만든 자격 증명을 사용하도록 Eclipse용 Azure 도구 키트를 다시 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-134">If you sign out of Azure when you are using Eclipse, you will need to reconfigure the Azure Toolkit for Eclipse to use a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="9b8c0-135">다음 단계에서는 기존 자격 증명 파일을 사용하도록 Azure 도구 키트를 구성하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-135">The following steps will walk you through configuring the Azure Toolkit to use an existing credentials file.</span></span>

1. <span data-ttu-id="9b8c0-136">Eclipse로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-136">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="9b8c0-137">**도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-137">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure 로그인을 위한 Eclipse 메뉴][A01]

1. <span data-ttu-id="9b8c0-139">**Azure 로그인** 대화 상자가 나타나면 **자동**을 선택한 다음 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-139">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![로그인 대화 상자][A02]

1. <span data-ttu-id="9b8c0-141">**인증된 파일 선택** 대화 상자가 나타나면 이전에 만든 자격 증명 파일을 선택한 다음 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-141">When the **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Open**.</span></span>

   ![로그인 대화 상자][A08]

1. <span data-ttu-id="9b8c0-143">**Azure 로그인** 대화 상자가 나타나면 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-143">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Azure 로그인 대화 상자][A06]

1. <span data-ttu-id="9b8c0-145">**구독 선택** 대화 상자가 나타나면 사용하려는 구독을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-145">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![구독 선택 대화 상자 관리][A07]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="9b8c0-147">대화형으로 Azure 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="9b8c0-147">Signing into your Azure account interactively</span></span>

<span data-ttu-id="9b8c0-148">다음 단계에서는 Azure 자격 증명을 수동으로 입력하여 Azure에 로그인하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-148">The following steps will illustrate how to sign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="9b8c0-149">Eclipse로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-149">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="9b8c0-150">**도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-150">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Azure 로그인을 위한 Eclipse 메뉴][I01]

1. <span data-ttu-id="9b8c0-152">**Azure 로그인** 대화 상자가 나타나면 **대화형**을 선택한 다음 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-152">When the **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![로그인 대화 상자][I02]

1. <span data-ttu-id="9b8c0-154">**Azure 로그인** 대화 상자가 나타나면 Azure 자격 증명을 입력하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-154">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Azure 로그인 대화 상자][I03]

1. <span data-ttu-id="9b8c0-156">**구독 선택** 대화 상자가 나타나면 사용하려는 구독을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-156">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![구독 선택 대화 상자 관리][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="9b8c0-158">대화형으로 로그인되었을 때 Azure 계정에서 로그아웃</span><span class="sxs-lookup"><span data-stu-id="9b8c0-158">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="9b8c0-159">이전 섹션의 단계를 구성한 후에는 Eclipse를 다시 시작할 때마다 Azure 계정에서 자동으로 로그아웃됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-159">After you have configured the steps in the previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="9b8c0-160">그러나 Eclipse를 다시 시작하지 않고 Azure 계정에서 로그아웃하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-160">However, if you want to sign out of your Azure account without restarting Eclipse, use the following steps.</span></span>

1. <span data-ttu-id="9b8c0-161">Eclipse에서 **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그아웃**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-161">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Azure 로그아웃을 위한 Eclipse 메뉴][L01]

1. <span data-ttu-id="9b8c0-163">**Azure 로그아웃** 대화 상자가 나타나면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b8c0-163">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![로그아웃 대화 상자][L02]

## <a name="next-steps"></a><span data-ttu-id="9b8c0-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9b8c0-165">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
