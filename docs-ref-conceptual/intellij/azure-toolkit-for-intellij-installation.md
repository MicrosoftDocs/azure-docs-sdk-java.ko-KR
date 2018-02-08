---
title: "IntelliJ용 Azure 도구 키트 설치"
description: "IntelliJ용 Azure 도구 키트 플러그 인을 설치하여 클라우드 응용 프로그램을 만들어 Azure에 배포하는 방법에 대해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 0f3df5c8cf3c83c1ce9a4ca32c753b5fc39ab1df
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="8b9e1-103">IntelliJ용 Azure 도구 키트 설치</span><span class="sxs-lookup"><span data-stu-id="8b9e1-103">Installing the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="8b9e1-104">IntelliJ용 Azure 도구 키트는 IntelliJ IDEA 개발 환경을 사용하여 클라우드 응용 프로그램을 쉽게 작성, 개발, 테스트 및 Azure에 배포할 수 있는 템플릿과 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy cloud application to Azure using the IntelliJ IDEA development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8b9e1-105">IntelliJ용 Azure 도구 키트는 다음 URL에 있는 GitHub의 프로젝트 사이트를 통해 MIT 라이선스에 따라 소스 코드 사용이 허가된 오픈 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <span data-ttu-id="8b9e1-106"><https://github.com/microsoft/azure-tools-for-java></span><span class="sxs-lookup"><span data-stu-id="8b9e1-106"><https://github.com/microsoft/azure-tools-for-java></span></span> 
> 

<span data-ttu-id="8b9e1-107">IntelliJ용 Azure 도구 키트를 설치하는 두 가지 방법이 있는데, 하나는 **설정** 대화 상자를 사용하는 것이고 다른 하나는 시작 화면의 **구성** 메뉴를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-107">There are two methods of installing the Azure Toolkit for IntelliJ: by using the **Settings** dialog box, and by using the **Configure** menu on the start screen.</span></span> <span data-ttu-id="8b9e1-108">두 설치 방법 모두 다음 단계에서 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-108">Both installation methods will be demonstrated in the following steps.</span></span>

[!INCLUDE [azure-toolkit-for-IntelliJ-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="8b9e1-109">설정 대화 상자에서 IntelliJ용 Azure 도구 키트를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="8b9e1-109">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>

1. <span data-ttu-id="8b9e1-110">IntelliJ IDEA를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-110">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="8b9e1-111">IntelliJ IDEA가 열리면 **File**을 클릭한 다음 **Settings**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-111">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
   ![IntelliJ IDEA Settings 대화 상자 열기][01a]

1. <span data-ttu-id="8b9e1-113">설정 대화 상자에서 **Plugins**를 클릭하고 **Browse repositories**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-113">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
   ![IntelliJ IDEA Settings 대화 상자][02a]

1. <span data-ttu-id="8b9e1-115">**Browse repositories** 대화 상자에서 검색 상자에 "Azure"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-115">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="8b9e1-116">**IntelliJ용 Azure 도구 키트**를 강조 표시하고 **Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-116">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![IntelliJ용 Azure 도구 키트 검색][03]
   
   <span data-ttu-id="8b9e1-118">IntelliJ IDEA 대화 상자에서 설치 진행 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-118">IntelliJ IDEA displays the installation progress in a dialog box.</span></span>
   
   ![설치 진행률][04]

1. <span data-ttu-id="8b9e1-120">설치가 완료되면 **Restart IntelliJ IDEA**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-120">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="8b9e1-122">**OK** 를 클릭하여 Settings 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-122">Click **OK** to close the Settings dialog box.</span></span>
   
   ![IntelliJ IDEA Settings 대화 상자 닫기][06]

1. <span data-ttu-id="8b9e1-124">IntelliJ IDEA를 다시 시작할지 또는 연기할지 묻는 메시지가 나타나면 **Restart**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-124">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
<span data-ttu-id="8b9e1-125">1</span><span class="sxs-lookup"><span data-stu-id="8b9e1-125">1</span></span>   ![Restart IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="8b9e1-127">시작 화면에서 IntelliJ용 Azure 도구 키트를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="8b9e1-127">To install the Azure Toolkit for IntelliJ from the start screen</span></span>

1. <span data-ttu-id="8b9e1-128">IntelliJ IDEA를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-128">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="8b9e1-129">IntelliJ IDEA 시작 화면이 나타나면 **Configure**를 클릭하고 **Plugins**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-129">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
   ![IntelliJ IDEA 플러그 인 설치][01b]

1. <span data-ttu-id="8b9e1-131">**Plugins** 대화 상자에서 **Browse repositories**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-131">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
   ![IntelliJ 아이디어 플러그 인 저장소 찾아보기][02b]

1. <span data-ttu-id="8b9e1-133">**Browse repositories** 대화 상자에서 검색 상자에 "Azure"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-133">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="8b9e1-134">**IntelliJ용 Azure 도구 키트**를 강조 표시하고 **Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-134">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![IntelliJ용 Azure 도구 키트 검색][03]
   
   <span data-ttu-id="8b9e1-136">IntelliJ IDEA 대화 상자에서 설치 진행 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-136">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
   ![설치 진행률][04]

1. <span data-ttu-id="8b9e1-138">설치가 완료되면 **Restart IntelliJ IDEA**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-138">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="8b9e1-140">IntelliJ IDEA를 다시 시작할지 또는 연기할지 묻는 메시지가 나타나면 **Restart**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8b9e1-140">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
   ![Restart IntelliJ IDEA][07]

## <a name="next-steps"></a><span data-ttu-id="8b9e1-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b9e1-142">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

<!-- IMG List -->

[01a]: media/azure-toolkit-for-intellij-installation/01-intellij-file-settings.png
[01b]: media/azure-toolkit-for-intellij-installation/01-intellij-configure-dropdown.png
[02a]: media/azure-toolkit-for-intellij-installation/02-intellij-settings-dialog.png
[02b]: media/azure-toolkit-for-intellij-installation/02-intellij-plugins-dialog.png
[03]: media/azure-toolkit-for-intellij-installation/03-intellij-browse-repositories.png
[04]: media/azure-toolkit-for-intellij-installation/04-install-progress.png
[05]: media/azure-toolkit-for-intellij-installation/05-restart-intellij.png
[06]: media/azure-toolkit-for-intellij-installation/06-intellij-settings-dialog.png
[07]: media/azure-toolkit-for-intellij-installation/07-restart-intellij.png
