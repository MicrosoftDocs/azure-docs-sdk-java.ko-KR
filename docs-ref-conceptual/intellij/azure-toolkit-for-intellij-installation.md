---
title: "IntelliJ용 Azure 도구 키트 설치"
description: "IntelliJ IDEA용 Azure 도구 키트를 설치하는 방법을 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 03767edf0b879e469dc6d47444fb862e6654d2f1
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2017
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="51b40-103">IntelliJ용 Azure 도구 키트 설치</span><span class="sxs-lookup"><span data-stu-id="51b40-103">Installing the Azure Toolkit for IntelliJ</span></span>
<span data-ttu-id="51b40-104">IntelliJ용 Azure 도구 키트는 IntelliJ IDEA 개발 환경에서 Azure 응용 프로그램을 쉽게 작성, 개발, 테스트 및 배포할 수 있는 템플릿과 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the IntelliJ IDEA development environment.</span></span> <span data-ttu-id="51b40-105">IntelliJ용 Azure 도구 키트는 다음 URL에 있는 GitHub의 프로젝트 사이트를 통해 MIT 라이선스에 따라 소스 코드 사용이 허가된 오픈 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span>

<span data-ttu-id="51b40-106"><https://github.com/microsoft/azure-tools-for-java></span><span class="sxs-lookup"><span data-stu-id="51b40-106"><https://github.com/microsoft/azure-tools-for-java></span></span>

<span data-ttu-id="51b40-107">IntelliJ용 Azure 도구 키트는 설정 대화 상자와 시작 화면의 구성 메뉴에서 설치할 수 있습니다. 다음 단계에서는 두 설치 방법을 모두 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-107">There are two methods of installing the Azure Toolkit for IntelliJ, from the Settings dialog box and from the Configure menu on the start screen; both installation methods will be demonstrated in the following steps.</span></span>

[!INCLUDE [azure-toolkit-for-IntelliJ-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="51b40-108">설정 대화 상자에서 IntelliJ용 Azure 도구 키트를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="51b40-108">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>

1. <span data-ttu-id="51b40-109">IntelliJ IDEA를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-109">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="51b40-110">IntelliJ IDEA가 열리면 **File**을 클릭한 다음 **Settings**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-110">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
   ![IntelliJ IDEA Settings 대화 상자 열기][01a]

1. <span data-ttu-id="51b40-112">설정 대화 상자에서 **Plugins**를 클릭하고 **Browse repositories**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-112">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
   ![IntelliJ IDEA Settings 대화 상자][02a]

1. <span data-ttu-id="51b40-114">**Browse repositories** 대화 상자에서 검색 상자에 "Azure"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-114">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="51b40-115">**IntelliJ용 Azure 도구 키트**를 강조 표시하고 **Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-115">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![IntelliJ용 Azure 도구 키트 검색][03]
   
   <span data-ttu-id="51b40-117">IntelliJ IDEA 대화 상자에서 설치 진행 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-117">IntelliJ IDEA displays the installation progress in a dialog box.</span></span>
   
   ![설치 진행률][04]

1. <span data-ttu-id="51b40-119">설치가 완료되면 **Restart IntelliJ IDEA**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-119">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="51b40-121">**OK** 를 클릭하여 Settings 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-121">Click **OK** to close the Settings dialog box.</span></span>
   
   ![IntelliJ IDEA Settings 대화 상자 닫기][06]

1. <span data-ttu-id="51b40-123">IntelliJ IDEA를 다시 시작할지 또는 연기할지 묻는 메시지가 나타나면 **Restart**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-123">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
<span data-ttu-id="51b40-124">1</span><span class="sxs-lookup"><span data-stu-id="51b40-124">1</span></span>   ![Restart IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="51b40-126">시작 화면에서 IntelliJ용 Azure 도구 키트를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="51b40-126">To install the Azure Toolkit for IntelliJ from the start screen</span></span>

1. <span data-ttu-id="51b40-127">IntelliJ IDEA를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-127">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="51b40-128">IntelliJ IDEA 시작 화면이 나타나면 **Configure**를 클릭하고 **Plugins**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-128">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
   ![IntelliJ IDEA 플러그 인 설치][01b]

1. <span data-ttu-id="51b40-130">**Plugins** 대화 상자에서 **Browse repositories**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-130">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
   ![IntelliJ 아이디어 플러그 인 저장소 찾아보기][02b]

1. <span data-ttu-id="51b40-132">**Browse repositories** 대화 상자에서 검색 상자에 "Azure"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-132">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="51b40-133">**IntelliJ용 Azure 도구 키트**를 강조 표시하고 **Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-133">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![IntelliJ용 Azure 도구 키트 검색][03]
   
   <span data-ttu-id="51b40-135">IntelliJ IDEA 대화 상자에서 설치 진행 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-135">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
   ![설치 진행률][04]

1. <span data-ttu-id="51b40-137">설치가 완료되면 **Restart IntelliJ IDEA**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-137">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="51b40-139">IntelliJ IDEA를 다시 시작할지 또는 연기할지 묻는 메시지가 나타나면 **Restart**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51b40-139">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
   ![Restart IntelliJ IDEA][07]

## <a name="next-steps"></a><span data-ttu-id="51b40-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="51b40-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

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
