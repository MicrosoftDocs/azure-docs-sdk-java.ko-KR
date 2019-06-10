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
ms.openlocfilehash: b4b13de38913ae6e7ae2bb09210ac742efc9d0ad
ms.sourcegitcommit: d18d9dce22b7f7af178f756bd341433d24e3c3b5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66575310"
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="87baa-103">Eclipse용 Azure 도구 키트에 대한 로그인 지침</span><span class="sxs-lookup"><span data-stu-id="87baa-103">Sign-in instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="87baa-104">Eclipse용 Azure 도구 키트는 Azure 계정에 로그인하는 두 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  - [<span data-ttu-id="87baa-105">디바이스 로그인에 의해 Azure 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="87baa-105">Sign in to your Azure account by Device Login</span></span>](#sign-in-to-your-azure-account-by-device-login)
  - [<span data-ttu-id="87baa-106">서비스 주체에 의해 Azure 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="87baa-106">Sign in to your Azure account by Service Principal</span></span>](#sign-in-to-your-azure-account-by-service-principal)

<span data-ttu-id="87baa-107">[**로그아웃**](#sign-out-of-your-azure-account) 방법도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-107">[**Sign out**](#sign-out-of-your-azure-account) methods are also provided.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-by-device-login"></a><span data-ttu-id="87baa-108">디바이스 로그인에 의해 Azure 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="87baa-108">Sign in to your Azure account by Device Login</span></span>

<span data-ttu-id="87baa-109">디바이스 로그인에 의해 Azure에 로그인하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-109">To sign in Azure by device login, do the following:</span></span>

1. <span data-ttu-id="87baa-110">Eclipse로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-110">Open your project with Eclipse.</span></span>

2. <span data-ttu-id="87baa-111">**도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="87baa-112">![Azure 로그인을 위한 Eclipse 메뉴][I01]</span><span class="sxs-lookup"><span data-stu-id="87baa-112">![Eclipse Menu for Azure Sign In][I01]</span></span>

3. <span data-ttu-id="87baa-113">**Azure 로그인** 창에서 **디바이스 로그인**을 선택한 다음, **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-113">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in**.</span></span>

   ![디바이스 로그인을 선택한 Azure 로그인 창][I02]

4. <span data-ttu-id="87baa-115">**Azure 디바이스 로그인** 대화 상자에서 **복사 및 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-115">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![Azure 로그인 대화 상자 창][I03]

> [!NOTE]
>
> <span data-ttu-id="87baa-117">브라우저가 열리지 않는 경우 Eclipse를 Internet Explorer, Firefox 또는 Chrome과 같은 외부 브라우저를 사용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-117">If the browser doesn't open, configure Eclipse to use an external browser like Internet Explorer, Firefox, or Chrome:</span></span>
>
> 1. <span data-ttu-id="87baa-118">기본 설정 -> 일반 -> 웹 브라우저 -> Eclipse에서 외부 웹 브라우저 사용을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-118">Open Preferences -> General -> Web Browser -> Use external web browser in Eclipse</span></span>
>
> 2. <span data-ttu-id="87baa-119">즐겨 사용하는 브라우저를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-119">Select the browser you prefer to use</span></span>
>

5. <span data-ttu-id="87baa-120">브라우저에서, 마지막 단계에서 **복사 및 열기**를 클릭할 때 복사한 디바이스 코드를 붙여넣은 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-120">In the browser, paste your device code (which has been copied when you clicked **Copy&Open** in last step) and then click **Next**.</span></span>

   ![디바이스 로그인 브라우저][I04]

6. <span data-ttu-id="87baa-122">끝으로 **구독 선택** 대화 상자에서 사용하려는 구독을 선택한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-122">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![구독 선택 대화 상자][I05]

## <a name="sign-in-to-your-azure-account-by-service-principal"></a><span data-ttu-id="87baa-124">서비스 주체에 의해 Azure 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="87baa-124">Sign in to your Azure account by Service Principal</span></span>

<span data-ttu-id="87baa-125">이 섹션에서는 서비스 주체 데이터를 포함하는 자격 증명 파일을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-125">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="87baa-126">이 프로세스를 완료하면 Eclipse에서는 사용자가 프로젝트를 열 때 해당 자격 증명 파일을 사용해서 Azure에 자동으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-126">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure when open your project.</span></span>

1. <span data-ttu-id="87baa-127">Eclipse로 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-127">Open your project with Eclipse.</span></span>

2. <span data-ttu-id="87baa-128">**도구**를 클릭한 다음 **Azure**를 클릭하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-128">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="87baa-129">![Eclipse Azure 로그인 명령][A01]</span><span class="sxs-lookup"><span data-stu-id="87baa-129">![The Eclipse Azure Sign In command][A01]</span></span>

3. <span data-ttu-id="87baa-130">**Azure 로그인** 창에서 **서비스 주체**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-130">In the **Azure Sign In** window, select **Service Principal**.</span></span> <span data-ttu-id="87baa-131">서비스 주체 인증 파일이 아직 없는 경우 **새로 만들기**를 클릭하여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-131">If you do not have the service principal authentication file yet, click **New** to create one.</span></span> <span data-ttu-id="87baa-132">또는 **찾아보기**를 클릭하여 열고 8단계로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-132">Otherwise you can click **Browse** to open it and jump to step 8.</span></span>

   ![서비스 주체를 선택한 Azure 로그인 창][A02]

4. <span data-ttu-id="87baa-134">**Azure 디바이스 로그인** 대화 상자에서 **복사 및 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-134">Click **Copy&Open** in **Azure Device Login** dialog.</span></span>

   ![Azure 로그인 대화 상자 창][A08]

> [!NOTE]
>
> <span data-ttu-id="87baa-136">브라우저가 열리지 않은 경우 Eclipse를 IE 또는 Chrome과 같은 외부 브라우저를 사용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-136">If the browser doesn't open, configure eclipse to use an external browser like IE or Chrome:</span></span>
>
> 1. <span data-ttu-id="87baa-137">기본 설정 -> 일반 -> 웹 브라우저 -> Eclipse에서 외부 웹 브라우저 사용을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-137">Open Preferences -> General -> Web Browser -> Use external web browser in Eclipse</span></span>
>
> 2. <span data-ttu-id="87baa-138">즐겨 사용하는 브라우저를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-138">Select the browser you prefer to use</span></span>
>

5. <span data-ttu-id="87baa-139">브라우저에서, 마지막 단계에서 **복사 및 열기**를 클릭할 때 복사한 디바이스 코드를 붙여넣은 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-139">In the browser, paste your device code (which has been copied when you click **Copy&Open** in last step) and then click **Next**.</span></span>

   ![디바이스 로그인 브라우저][A03]

6. <span data-ttu-id="87baa-141">**인증 파일 만들기** 창에서 사용할 구독을 선택하고 대상 디렉터리를 선택한 다음, **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-141">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![인증 파일 만들기 창][A04]

7. <span data-ttu-id="87baa-143">**서비스 주체 만들기 상태** 대화 상자에서 파일을 성공적으로 만든 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-143">In the **Service Principal Creation Status** dialog box, click **OK** after your files have been created successfully.</span></span>

   ![서비스 주체 만들기 상태 대화 상자][A05]

8. <span data-ttu-id="87baa-145">생성된 파일의 주소가 **Azure 로그인** 창에 자동으로 채워진 후 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-145">Address of the created file will be automatically filled in the **Azure Sign In** window, now click **Sign in**.</span></span>

   ![Azure 로그인 대화 상자][A06]

9. <span data-ttu-id="87baa-147">끝으로 **구독 선택** 대화 상자에서 사용하려는 구독을 선택한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-147">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![구독 선택 대화 상자][A07]

## <a name="sign-out-of-your-azure-account"></a><span data-ttu-id="87baa-149">Azure 계정에서 로그아웃</span><span class="sxs-lookup"><span data-stu-id="87baa-149">Sign out of your Azure account</span></span>

<span data-ttu-id="87baa-150">이전 단계에서 계정을 구성한 후에는 Eclipse를 시작할 때마다 자동으로 로그인됩니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-150">After you have configured your account by preceding steps, you will be automatically signed in each time you start Eclipse.</span></span> <span data-ttu-id="87baa-151">그러나 Azure 계정에서 로그아웃하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-151">However, if you want to sign out of your Azure account, use the following steps.</span></span>

1. <span data-ttu-id="87baa-152">Eclipse에서 **도구**를 클릭한 다음 **Azure**를 클릭하고 **로그아웃**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-152">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Azure 로그아웃을 위한 Eclipse 메뉴][L01]

2. <span data-ttu-id="87baa-154">**Azure 로그아웃** 대화 상자가 나타나면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="87baa-154">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![로그아웃 대화 상자][L02]

## <a name="next-steps"></a><span data-ttu-id="87baa-156">다음 단계</span><span class="sxs-lookup"><span data-stu-id="87baa-156">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-eclipse-sign-in-instructions/I05.png

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
