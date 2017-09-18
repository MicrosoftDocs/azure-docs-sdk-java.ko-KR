---
title: "Eclipse에서 Java용 Azure 라이브러리 패키지의 Javadoc 콘텐츠 표시"
description: "Eclipse에서 Azure 라이브러리의 Javadoc 콘텐츠를 표시하는 방법입니다."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 2d1f03f993f0c88401efaa9985f773b9a4b92cc4
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-the-azure-libraries-package-for-java"></a><span data-ttu-id="dee7e-103">Eclipse에서 Java용 Azure 라이브러리 패키지의 Javadoc 콘텐츠 표시</span><span class="sxs-lookup"><span data-stu-id="dee7e-103">Displaying Javadoc Content in Eclipse for the Azure Libraries Package for Java</span></span>

<span data-ttu-id="dee7e-104">Javadoc 콘텐츠를 Java용 Azure 라이브러리 패키지에 연결하면 Java용 Azure 라이브러리 패키지의 Javadoc 콘텐츠를 Eclipse 환경 내에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-104">The Javadoc content for the Azure Libraries for Java can be viewed within your Eclipse environment by associating the Javadoc content to the Azure Libraries for Java.</span></span> <span data-ttu-id="dee7e-105">다음 단계는 Eclipse 내에서 이 기능을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-105">The following steps show you how to use this functionality within Eclipse.</span></span>

<span data-ttu-id="dee7e-106">이 절차는 빌드 경로에 Java용 Azure 라이브러리를 이미 추가했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-106">This procedure assumes you have already added the Azure Library for Java to your build path.</span></span>

## <a name="to-display-javadoc-content-in-eclipse-for-the-azure-libraries-for-java"></a><span data-ttu-id="dee7e-107">Eclipse에서 Java용 Azure 라이브러리의 Javadoc 콘텐츠를 표시하려면</span><span class="sxs-lookup"><span data-stu-id="dee7e-107">To display Javadoc content in Eclipse for the Azure Libraries for Java</span></span>

1. <span data-ttu-id="dee7e-108">Eclipse의 프로젝트 탐색기에 있는 프로젝트 **참조 라이브러리** 섹션에서 Java JAR용 Azure 라이브러리의 상황에 맞는 메뉴를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-108">Within Eclipse's Project Explorer, in the **Referenced Libraries** section of your project, open the context menu for the Azure Library for Java JAR.</span></span> <span data-ttu-id="dee7e-109">예를 들어 **microsoft windowsazure-api 0.1.0.jar** (버전 번호는 설치한 버전에 따라 다를 수 있음)입니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (the version number may be different, dependent upon which version you have installed).</span></span>

1. <span data-ttu-id="dee7e-110">**속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-110">Click **Properties**.</span></span>

1. <span data-ttu-id="dee7e-111">**속성** 대화 상자의 왼쪽 창에서 **Javadoc 위치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-111">Within the **Properties** dialog, in the left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="dee7e-112">**Javadoc Location** (Javadoc 위치) 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-112">The **Javadoc Location** dialog is displayed.</span></span>

1. <span data-ttu-id="dee7e-113">**Javadoc URL** 또는 **보관 중인 Javadoc**을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="dee7e-114">**Javadoc URL**을 지정하도록 선택하는 경우 **http://dl.windowsazure.com/javadoc** 또는 **http://dl.windowsazure.com/storage/javadoc**와 같은 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-114">If you choose to specify a **Javadoc URL**, use the URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="dee7e-115">**Javadoc in archive**(보관 중인 Javadoc)를 사용하도록 선택하는 경우 외부 파일 또는 작업 영역 파일을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-115">If you choose to use **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="dee7e-116">필요에 따라 선택하여 찾거나 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="dee7e-117">다음 예제에서는 Java용 Azure 라이브러리를 **c:\MyAzureJARs**라는 폴더에 로컬로 다운로드된 해당 Javadoc JAR와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-117">The following example associates the Azure Libraries for Java with the corresponding Javadoc JAR that has been downloaded locally to a folder named **c:\MyAzureJARs**.</span></span>

   ![Javadoc 콘텐츠를 표시합니다.][ic553487]

1. <span data-ttu-id="dee7e-119">*옵션 단계*: **유효성 검사**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-119">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="dee7e-120">Javadoc JAR의 잠재적 문제가 여기에 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-120">Potential issues with the Javadoc JAR could be displayed here.</span></span>

1. <span data-ttu-id="dee7e-121">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-121">Click **OK**.</span></span>

<span data-ttu-id="dee7e-122">라이브러리에 연결되면 Javadoc 콘텐츠가 Eclipse IDE 내에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-122">Once associated with the library, the Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="dee7e-123">예를 들어 `blob`이 코드에서 `CloudBlockBlob` 형식으로 정의되는 경우 다음은 코드에서 `blob.acquireLease`를 입력했을 때 표시되는 Javadoc 콘텐츠의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="dee7e-123">For example, if `blob` is defined of type `CloudBlockBlob` within your code, the following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![Javadoc 콘텐츠를 표시합니다.][ic553488]

## <a name="next-steps"></a><span data-ttu-id="dee7e-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dee7e-125">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->

<!-- IMG List -->

[ic553487]: media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png