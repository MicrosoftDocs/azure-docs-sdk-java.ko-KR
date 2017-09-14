---
title: "IntelliJ용 Azure 도구 키트에 대한 로그인 지침"
description: "IntelliJ용 Azure 도구 키트를 사용하여 Microsoft Azure에 로그인하는 방법을 알아봅니다."
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
ms.openlocfilehash: 85fa5eb979e4d28d49db215ee1653b4c064a87c5
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a><span data-ttu-id="b1628-103">IntelliJ용 Azure 도구 키트에 대한 로그인 지침</span><span class="sxs-lookup"><span data-stu-id="b1628-103">Sign-in instructions for the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="b1628-104">IntelliJ용 Azure 도구 키트는 Azure 계정에 로그인하는 두 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-104">The Azure Toolkit for IntelliJ provides two methods for signing in to your Azure account:</span></span>

  * <span data-ttu-id="b1628-105">**자동**: 자동으로 Azure 계정에 로그인하는 데 사용할 수 있는 자격 증명 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-105">**Automated**: You create a credentials file that you can use to automatically sign in to your Azure account.</span></span>
  * <span data-ttu-id="b1628-106">**대화형**: Azure 계정에 로그인할 때마다 Azure 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-106">**Interactive**: You enter your Azure credentials each time you sign in to your Azure account.</span></span>

<span data-ttu-id="b1628-107">다음 섹션에서는 각 방법을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-107">The following sections describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-automatically"></a><span data-ttu-id="b1628-108">Azure 계정에 자동으로 로그인</span><span class="sxs-lookup"><span data-stu-id="b1628-108">Sign in to your Azure account automatically</span></span>

<span data-ttu-id="b1628-109">이 섹션에서는 서비스 주체 데이터를 포함하는 자격 증명 파일을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-109">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="b1628-110">이 프로세스를 완료하면 Eclipse에서는 사용자가 프로젝트를 열 때마다 해당 자격 증명 파일을 사용해서 자동으로 Azure에 자동으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-110">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure each time you open your project.</span></span>

1. <span data-ttu-id="b1628-111">IntelliJ IDEA로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-111">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="b1628-112">**도구** 메뉴에서 **Azure**를 가리킨 다음, **Azure 로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-112">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![IntelliJ Azure 로그인 명령][A01]

1. <span data-ttu-id="b1628-114">**Azure 로그인** 창에서 **자동**을 선택한 다음 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-114">In the **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![선택한 자동을 통한 Azure 로그인 창][A02]

1. <span data-ttu-id="b1628-116">**Azure 로그인 대화 상자** 창에서 Azure 자격 증명을 입력한 다음, **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-116">In the **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Azure 로그인 대화 상자 창][A03]

1. <span data-ttu-id="b1628-118">**인증 파일 만들기** 창에서 사용할 구독을 선택하고 대상 디렉터리를 선택한 다음, **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-118">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![인증 파일 만들기 창][A04]

1. <span data-ttu-id="b1628-120">**서비스 주체 만들기 상태** 대화 상자에서 파일을 성공적으로 만든 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-120">In the **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![서비스 주체 만들기 상태 대화 상자][A05]

1. <span data-ttu-id="b1628-122">**Azure 로그인** 창에서 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-122">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Azure 로그인 대화 상자][A06]

1. <span data-ttu-id="b1628-124">**구독 선택** 대화 상자에서 사용하려는 구독을 선택한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-124">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![구독 선택 대화 상자][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="b1628-126">자동으로 로그인한 후 Azure 계정에서 로그아웃</span><span class="sxs-lookup"><span data-stu-id="b1628-126">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="b1628-127">이전 단계를 사용하여 계정을 구성한 후에는 Azure 도구 키트는 IntelliJ IDEA를 다시 시작할 때마다 Azure 계정에 자동으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-127">After you have configured your account by using the preceding steps, the Azure Toolkit automatically signs you in to your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="b1628-128">그러나 Azure 계정에서 로그아웃하고 Azure 도구 키트가 자동으로 로그인하지 않도록 하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-128">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, do the following:</span></span>

1. <span data-ttu-id="b1628-129">IntelliJ IDEA에서 **도구** 메뉴에서 **Azure**를 가리킨 다음, **Azure 로그아웃**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-129">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![IntelliJ Azure 로그아웃 명령][L01]

1. <span data-ttu-id="b1628-131">**Azure 로그아웃** 확인 창에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-131">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Azure 로그아웃 확인 창][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="b1628-133">기존 자격 증명 파일을 사용하여 자동으로 Azure 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="b1628-133">Sign in to your Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="b1628-134">IntelliJ IDEA를 사용할 때 Azure 계정에서 로그아웃하는 경우 기존 자격 증명 파일을 사용하여 계정에 자동으로 다시 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-134">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file to automatically sign back in to the account.</span></span> <span data-ttu-id="b1628-135">기존 자격 증명을 사용하도록 Eclipse용 Azure 도구 키트를 구성하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-135">To configure the Azure Toolkit for Eclipse to use an existing credentials file, do the following:</span></span>

1. <span data-ttu-id="b1628-136">IntelliJ IDEA로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-136">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="b1628-137">**도구** 메뉴에서 **Azure**를 가리킨 다음, **Azure 로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-137">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![IntelliJ Azure 로그인 명령][A01]

1. <span data-ttu-id="b1628-139">**Azure 로그인** 창에서 **자동**을 선택한 다음 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-139">In the **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![선택한 자동을 통한 Azure 로그인 창][A02]

1. <span data-ttu-id="b1628-141">**인증 파일 선택** 대화 상자에서 이전에 만든 자격 증명 파일을 선택한 다음, **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-141">In the **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![인증 파일 선택 대화 상자][A08]

1. <span data-ttu-id="b1628-143">**Azure 로그인** 창에서 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-143">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![선택한 자동을 통한 Azure 로그인 창][A06]

1. <span data-ttu-id="b1628-145">**구독 선택** 대화 상자에서 사용하려는 구독을 선택한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-145">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![구독 선택 대화 상자][A07]

## <a name="sign-in-to-your-azure-account-interactively"></a><span data-ttu-id="b1628-147">대화형으로 Azure 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="b1628-147">Sign in to your Azure account interactively</span></span>

<span data-ttu-id="b1628-148">Azure 자격 증명을 수동으로 입력하여 Azure에 로그인하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-148">To sign in to Azure by manually entering your Azure credentials, do the following:</span></span>

1. <span data-ttu-id="b1628-149">IntelliJ IDEA로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-149">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="b1628-150">**도구**를 클릭하고 **Azure**를 가리킨 다음, **Azure 로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-150">Click **Tools**, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![IntelliJ Azure 로그인 명령][I01]

1. <span data-ttu-id="b1628-152">**Azure 로그인** 창에서 **대화형**을 선택한 다음 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-152">In the **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![선택한 대화형을 사용한 Azure 로그인 창][I02]

1. <span data-ttu-id="b1628-154">**Azure 로그인** 대화 상자가 나타나면 Azure 자격 증명을 입력한 다음, **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-154">In the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Azure 로그인 대화 상자 창][I03]

1. <span data-ttu-id="b1628-156">**구독 선택** 대화 상자에서 사용하려는 구독을 선택한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-156">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![구독 선택 대화 상자][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="b1628-158">대화형으로 로그인한 후 Azure 계정에서 로그아웃</span><span class="sxs-lookup"><span data-stu-id="b1628-158">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="b1628-159">이전 단계를 사용하여 계정을 구성한 후에는 IntelliJ IDEA를 다시 시작할 때마다 Azure 계정에서 자동으로 로그아웃됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-159">After you have configured your account by using the preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="b1628-160">그러나 IntelliJ IDEA를 다시 시작하지 *않고* Azure 계정에서 로그아웃하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-160">However, if you want to sign out of your Azure account *without* restarting IntelliJ IDEA, do the following.</span></span>

1. <span data-ttu-id="b1628-161">IntelliJ IDEA에서 **도구** 메뉴에서 **Azure**를 가리킨 다음, **Azure 로그아웃**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-161">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![IntelliJ Azure 로그아웃 명령][L01]

1. <span data-ttu-id="b1628-163">**Azure 로그아웃** 확인 창에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b1628-163">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Azure 로그아웃 확인 창][L02]

## <a name="next-steps"></a><span data-ttu-id="b1628-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b1628-165">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

<!-- IMG List -->

[I01]: media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
