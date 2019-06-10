---
title: IntelliJ용 Azure 도구 키트 설치
description: Azure Toolkit for IntelliJ 플러그 인을 설치하여 클라우드 애플리케이션을 만들어 Azure에 배포하는 방법에 대해 알아봅니다.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 86cef07873ae7a2ba75aab1044fe4d241cd5b13e
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270877"
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="13a1f-103">IntelliJ용 Azure 도구 키트 설치</span><span class="sxs-lookup"><span data-stu-id="13a1f-103">Installing the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="13a1f-104">Azure Toolkit for IntelliJ는 IntelliJ IDEA 개발 환경을 사용하여 클라우드 애플리케이션을 쉽게 작성, 개발, 테스트 및 Azure에 배포할 수 있는 템플릿과 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy cloud application to Azure using the IntelliJ IDEA development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="13a1f-105">IntelliJ용 Azure 도구 키트는 다음 URL에 있는 GitHub의 프로젝트 사이트를 통해 MIT 라이선스에 따라 소스 코드 사용이 허가된 오픈 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

<span data-ttu-id="13a1f-106">IntelliJ용 Azure 도구 키트를 설치하는 두 가지 방법이 있는데, 하나는 **설정** 대화 상자를 사용하는 것이고 다른 하나는 시작 화면의 **구성** 메뉴를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-106">There are two methods of installing the Azure Toolkit for IntelliJ: by using the **Settings** dialog box, and by using the **Configure** menu on the start screen.</span></span> <span data-ttu-id="13a1f-107">두 설치 방법 모두 다음 단계에서 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-107">Both installation methods will be demonstrated in the following steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13a1f-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="13a1f-108">Prerequisites</span></span>

<span data-ttu-id="13a1f-109">Azure Toolkit for IntelliJ에는 다음 소프트웨어 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-109">The Azure Toolkit for IntelliJ requires to the following software components:</span></span>

* <span data-ttu-id="13a1f-110">JDK(Java Development Kit) 8 이상 설치, 예: [OpenJDK](https://openjdk.java.net/) 또는 [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)</span><span class="sxs-lookup"><span data-stu-id="13a1f-110">An Java Development Kit (JDK) 8+ installed, for example: [OpenJDK](https://openjdk.java.net/) or [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)</span></span>
* <span data-ttu-id="13a1f-111">[IntelliJ IDEA](https://www.jetbrains.com/idea/download/) Ultimate Edition 또는 Community Edition 설치</span><span class="sxs-lookup"><span data-stu-id="13a1f-111">An [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) Ultimate Edition or Community Edition installed</span></span>

> [!NOTE]
> 
> <span data-ttu-id="13a1f-112">JetBrains 플러그인 리포지토리에 있는 [IntelliJ용 Azure Toolkit](https://plugins.jetbrains.com/plugin/8053) 페이지는 툴킷과 호환되는 빌드를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-112">The [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) page at the JetBrains Plugin Repository lists the builds that are compatible with the toolkit.</span></span>
> 

<!--
> [!IMPORTANT]
> 
> If you are using the Azure Toolkit for IntelliJ on Windows, the toolkit requires installing the Azure SDK 2.9.6 or later in order to use the Azure emulator. You have two options for installing the Azure SDK:
> 
> * You can download and install the Azure SDK by using the [Web Platform Installer (WebPI)](http://go.microsoft.com/fwlink/?LinkID=252838).
> * If you do not have the Azure SDK installed when you create your first Azure deployment project, you will be prompted to automatically download install the requisite version of the Azure SDK.
> 
> Note that the Azure SDK is only required on Windows.
> 
-->


## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="13a1f-113">설정 대화 상자에서 IntelliJ용 Azure 도구 키트를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="13a1f-113">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>

1. <span data-ttu-id="13a1f-114">IntelliJ IDEA를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-114">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="13a1f-115">IntelliJ IDEA가 열리면 **File**을 클릭한 다음 **Settings**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-115">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
   ![IntelliJ IDEA Settings 대화 상자 열기][01a]

1. <span data-ttu-id="13a1f-117">설정 대화 상자에서 **Plugins**를 클릭하고 **Browse repositories**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-117">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
   ![IntelliJ IDEA Settings 대화 상자][02a]

1. <span data-ttu-id="13a1f-119">**Browse repositories** 대화 상자에서 검색 상자에 "Azure"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-119">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="13a1f-120">**IntelliJ용 Azure 도구 키트**를 강조 표시하고 **Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-120">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![IntelliJ용 Azure 도구 키트 검색][03]
   
   <span data-ttu-id="13a1f-122">IntelliJ IDEA 대화 상자에서 설치 진행 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-122">IntelliJ IDEA displays the installation progress in a dialog box.</span></span>
   
   ![설치 진행률][04]

1. <span data-ttu-id="13a1f-124">설치가 완료되면 **Restart IntelliJ IDEA**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-124">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="13a1f-126">**OK** 를 클릭하여 Settings 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-126">Click **OK** to close the Settings dialog box.</span></span>
   
   ![IntelliJ IDEA Settings 대화 상자 닫기][06]

1. <span data-ttu-id="13a1f-128">IntelliJ IDEA를 다시 시작할지 또는 연기할지 묻는 메시지가 나타나면 **Restart**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-128">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
<span data-ttu-id="13a1f-129">1</span><span class="sxs-lookup"><span data-stu-id="13a1f-129">1</span></span>   ![Restart IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="13a1f-131">시작 화면에서 IntelliJ용 Azure 도구 키트를 설치하려면</span><span class="sxs-lookup"><span data-stu-id="13a1f-131">To install the Azure Toolkit for IntelliJ from the start screen</span></span>

1. <span data-ttu-id="13a1f-132">IntelliJ IDEA를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-132">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="13a1f-133">IntelliJ IDEA 시작 화면이 나타나면 **Configure**를 클릭하고 **Plugins**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-133">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
   ![IntelliJ IDEA 플러그 인 설치][01b]

1. <span data-ttu-id="13a1f-135">**Plugins** 대화 상자에서 **Browse repositories**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-135">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
   ![IntelliJ 아이디어 플러그 인 저장소 찾아보기][02b]

1. <span data-ttu-id="13a1f-137">**Browse repositories** 대화 상자에서 검색 상자에 "Azure"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-137">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="13a1f-138">**IntelliJ용 Azure 도구 키트**를 강조 표시하고 **Install**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-138">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![IntelliJ용 Azure 도구 키트 검색][03]
   
   <span data-ttu-id="13a1f-140">IntelliJ IDEA 대화 상자에서 설치 진행 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-140">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
   ![설치 진행률][04]

1. <span data-ttu-id="13a1f-142">설치가 완료되면 **Restart IntelliJ IDEA**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-142">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="13a1f-144">IntelliJ IDEA를 다시 시작할지 또는 연기할지 묻는 메시지가 나타나면 **Restart**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="13a1f-144">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
   ![Restart IntelliJ IDEA][07]

## <a name="next-steps"></a><span data-ttu-id="13a1f-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="13a1f-146">Next steps</span></span>

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
