---
title: Eclipse용 Azure 도구 키트 설치
description: Azure Toolkit for Eclipse 플러그 인을 설치하여 클라우드 애플리케이션을 만들어 Azure에 배포하는 방법에 대해 알아봅니다.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 8e6630f7e019d950249e7e84024ac800a0f2f136
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270841"
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="1b24c-103">Eclipse용 Azure 도구 키트 설치</span><span class="sxs-lookup"><span data-stu-id="1b24c-103">Installing the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="1b24c-104">Azure Toolkit for Eclipse를 두 가지 방법으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-104">There are two ways to install Azure Toolkit for Eclipse:</span></span>

  - [<span data-ttu-id="1b24c-105">Eclipse 마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="1b24c-105">Eclipse marketplace</span></span>](#eclipse-marketplace)
  - [<span data-ttu-id="1b24c-106">새 소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="1b24c-106">Install new software</span></span>](#install-new-software)

> [!NOTE] 
> 
> <span data-ttu-id="1b24c-107">Eclipse용 Azure 도구 키트는 다음 URL에 있는 GitHub의 프로젝트 사이트를 통해 MIT 라이선스에 따라 소스 코드 사용이 허가된 오픈 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-107">The Azure Toolkit for Eclipse is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

[!INCLUDE [azure-toolkit-for-eclipse-basic-prerequisites](../includes/azure-toolkit-for-eclipse-basic-prerequisites.md)]

## <a name="eclipse-marketplace"></a><span data-ttu-id="1b24c-108">Eclipse 마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="1b24c-108">Eclipse marketplace</span></span>

1. <span data-ttu-id="1b24c-109">다음 단추를 실행 중인 Eclipse 작업 영역으로 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-109">Drag the following button to your running Eclipse workspace.</span></span>

    <span data-ttu-id="1b24c-110">[![실행 중인 Eclipse* 작업 영역으로 끌어옵니다. *Eclipse Marketplace 클라이언트가 필요합니다.](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "실행 중인 Eclipse* 작업 영역으로 끌어옵니다. *Eclipse Marketplace 클라이언트가 필요합니다.")</span><span class="sxs-lookup"><span data-stu-id="1b24c-110">[![Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client")</span></span>

2. <span data-ttu-id="1b24c-111">또는 **도움말/Eclipse Marketplace**에서 **Azure Toolkit for Eclipse 플러그인**을 검색하고 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-111">Otherwise, it is also possible to search and install the **Azure Toolkit for Eclipse plugin** at **Help/Eclipse Marketplace**.</span></span>

    ![Marketplace](./media/azure-toolkit-for-eclipse-installation/marketplace.png)

## <a name="install-new-software"></a><span data-ttu-id="1b24c-113">새 소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="1b24c-113">Install new software</span></span>

1. <span data-ttu-id="1b24c-114">Eclipse를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-114">Start Eclipse.</span></span>

1. <span data-ttu-id="1b24c-115">다음 그림에 표시된 대로 **Help** 메뉴를 클릭하고 **Install New Software**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-115">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>

   ![Eclipse용 Azure 도구 키트 설치][01]

1. <span data-ttu-id="1b24c-117">**Available Software** 대화 상자의 **Work with** 텍스트 상자에 `http://dl.microsoft.com/eclipse/`를 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-117">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="1b24c-118">**이름** 창에서 **Java용 Azure 도구 키트**를 선택하고 **Contact all update sites during install to find required software**를 선택하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-118">In the **Name** pane, check **Azure Toolkit for Java**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="1b24c-119">화면은 다음과 유사한 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-119">Your screen should appear similar to the following:</span></span>

   ![Eclipse용 Azure 도구 키트 설치][02]

1. <span data-ttu-id="1b24c-121">**Eclipse용 Azure 도구 키트**를 확장하면 설치되는 구성 요소 목록이 표시되며, 다음은 그 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-121">If you expand **Azure Toolkit for Eclipse**, you will see a list of components that will be installed; for example:</span></span>

   | <span data-ttu-id="1b24c-122">기능</span><span class="sxs-lookup"><span data-stu-id="1b24c-122">Feature</span></span> | <span data-ttu-id="1b24c-123">설명</span><span class="sxs-lookup"><span data-stu-id="1b24c-123">Description</span></span> | 
   |---|---| 
   | <span data-ttu-id="1b24c-124">**Java용 Application Insights 플러그 인**</span><span class="sxs-lookup"><span data-stu-id="1b24c-124">**Application Insights Plugin for Java**</span></span> | <span data-ttu-id="1b24c-125">애플리케이션 및 서버 인스턴스에 Azure 원격 분석 로깅 및 분석 서비스를 사용할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-125">Allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span> | 
   | <span data-ttu-id="1b24c-126">**Azure 공통 플러그 인**</span><span class="sxs-lookup"><span data-stu-id="1b24c-126">**Azure Common Plugin**</span></span> | <span data-ttu-id="1b24c-127">다른 도구 키트 구성 요소에 필요한 공통 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-127">provides the common functionality needed by other toolkit components.</span></span> | 
   | <span data-ttu-id="1b24c-128">**Eclipse용 Azure Container 도구**</span><span class="sxs-lookup"><span data-stu-id="1b24c-128">**Azure Container Tools for Eclipse**</span></span> | <span data-ttu-id="1b24c-129">.WAR을 docker 컴퓨터의 Docker 컨테이너로 빌드 및 배포할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-129">Enables you to build and deploy a .WAR as a Docker container to a docker machine.</span></span> | 
   | <span data-ttu-id="1b24c-130">**Eclipse용 Azure 컨테이너**</span><span class="sxs-lookup"><span data-stu-id="1b24c-130">**Azure Containers for Eclipse**</span></span> | <span data-ttu-id="1b24c-131">.WAR 또는 .JAR 아티팩트를 Azure 가상 머신에 Docker 컨테이너로 배포할 수 있게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-131">Enables you to deploy a .WAR or .JAR artifact as a Docker container to an Azure virtual machine.</span></span> | 
   | <span data-ttu-id="1b24c-132">**Eclipse용 Azure 탐색기**</span><span class="sxs-lookup"><span data-stu-id="1b24c-132">**Azure Explorer for Eclipse**</span></span> | <span data-ttu-id="1b24c-133">Azure 리소스를 관리할 수 있는 탐색기 스타일의 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-133">Provides an explorer-style interface for managing your Azure resources.</span></span> | 
   | <span data-ttu-id="1b24c-134">**SQL Server용 Microsoft JDBC Driver 6.1**</span><span class="sxs-lookup"><span data-stu-id="1b24c-134">**Microsoft JDBC Driver 6.1 for SQL Server**</span></span> | <span data-ttu-id="1b24c-135">SQL Server용 JDBC API와 Java Platform Enterprise Edition 8용 Microsoft Azure SQL Database를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-135">Provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span> | 
   | <span data-ttu-id="1b24c-136">**Java용 Microsoft Azure 라이브러리 패키지**</span><span class="sxs-lookup"><span data-stu-id="1b24c-136">**Package for Microsoft Azure Libraries for Java**</span></span> | <span data-ttu-id="1b24c-137">저장소, service bus, 서비스 런타임 등의 Microsoft Azure 서비스에 액세스하기 위한 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-137">Provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span> | 

1. <span data-ttu-id="1b24c-138">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-138">Click **Next**.</span></span> <span data-ttu-id="1b24c-139">(도구 키트를 설치하는 동안 비정상적인 지연이 발생하는 경우에는 **Contact all update sites during install to find required software** 가 선택되어 있지 않은지 확인합니다.)</span><span class="sxs-lookup"><span data-stu-id="1b24c-139">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="1b24c-140">**설치 세부 정보** 대화 상자에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-140">In the **Install Details** dialog, click **Next**.</span></span>

   ![설치 세부 정보 검토][03]

1. <span data-ttu-id="1b24c-142">**Review Licenses** 대화 상자에서 사용권 계약 조건을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-142">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="1b24c-143">사용권 계약 조건에 동의하면 **동의함**을 클릭한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-143">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="1b24c-144">(나머지 단계에서는 사용권 계약 조건에 동의한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-144">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="1b24c-145">사용권 계약 조건에 동의하지 않으면 설치 프로세스를 종료합니다.)</span><span class="sxs-lookup"><span data-stu-id="1b24c-145">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>

   ![Review Licenses][04]

   <span data-ttu-id="1b24c-147">Eclipse는 필수 패키지를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-147">Eclipse will download and install the requisite packages.</span></span>

   ![설치 진행률][05]

1. <span data-ttu-id="1b24c-149">설치를 완료하기 위해 Eclipse를 다시 시작한다는 메시지가 표시되면 **Yes**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1b24c-149">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>

   ![다시 시작 프롬프트][06]

## <a name="next-steps"></a><span data-ttu-id="1b24c-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b24c-151">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->
[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
