---
title: "Eclipse용 Azure 도구 키트 설치"
description: "Eclipse용 Azure 도구 키트를 설치하는 방법을 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 59a8bfb6ab4db8ea8c6c9025ca3ced8a13192628
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="d207b-103">Eclipse용 Azure 도구 키트 설치</span><span class="sxs-lookup"><span data-stu-id="d207b-103">Installing the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="d207b-104">Eclipse용 Azure 도구 키트는 Eclipse 개발 환경에서 Azure 응용 프로그램을 쉽게 작성, 개발, 테스트 및 배포할 수 있는 템플릿과 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the Eclipse development environment.</span></span> <span data-ttu-id="d207b-105">Eclipse용 Azure 도구 키트는 오픈 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-105">The Azure Toolkit for Eclipse is an Open Source project.</span></span> <span data-ttu-id="d207b-106">소스 코드는 <https://github.com/microsoft/azure-tools-for-java>의 MIT 라이선스 아래에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-106">The source code is available under the MIT License from <https://github.com/microsoft/azure-tools-for-java>.</span></span>

<span data-ttu-id="d207b-107">다음 단계는 Eclipse용 Azure 도구 키트를 설치하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="d207b-108">Eclipse용 Azure 도구 키트 설치</span><span class="sxs-lookup"><span data-stu-id="d207b-108">To install the Azure Toolkit for Eclipse</span></span>

1. <span data-ttu-id="d207b-109">Eclipse를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-109">Start Eclipse.</span></span>

1. <span data-ttu-id="d207b-110">다음 그림에 표시된 대로 **Help** 메뉴를 클릭하고 **Install New Software**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
   ![Eclipse용 Azure 도구 키트 설치][01]

1. <span data-ttu-id="d207b-112">**Available Software** 대화 상자의 **Work with** 텍스트 상자에 `http://dl.microsoft.com/eclipse/`를 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="d207b-113">**Name** 창에서 **Azure Toolkit for Eclipse**를 선택하고 **Contact all update sites during install to find required software**를 선택하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="d207b-114">화면은 다음과 유사한 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-114">Your screen should appear similar to the following:</span></span>
   
   ![Eclipse용 Azure 도구 키트 설치][02]

1. <span data-ttu-id="d207b-116">**Azure Toolkit for Eclipse**를 확장하면 다음 예제처럼 항목의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-116">If you expand the **Azure Toolkit for Eclipse**, you will see a list of items like following example:</span></span>
   
   * <span data-ttu-id="d207b-117">**Application Insights Plugin for Java**: 이 구성 요소는 응용 프로그램 및 서버 인스턴스에 대해 Azure의 원격 분석 로깅 및 분석 서비스를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-117">**Application Insights Plugin for Java**: This component allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span>
   * <span data-ttu-id="d207b-118">**Azure Access Control Services Filter**:이 구성 요소는 Azure ACS에서 응용 프로그램 사용자를 인증하도록 하고 Single Sign-On 시나리오를 사용하도록 하고 응용 프로그램에서 ID 논리를 외부화합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-118">**Azure Access Control Services Filter**: This component provides support for authenticating application users with Azure ACS, enabling single sign-on scenarios and externalizing identity logic from the application.</span></span>
   * <span data-ttu-id="d207b-119">**Azure Common Plugin**: 이 구성 요소는 다른 도구 키트 구성 요소에 필요한 공통 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-119">**Azure Common Plugin**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="d207b-120">**Azure Explorer for Eclipse**: 이 구성 요소는 다른 도구 키트 구성 요소에 필요한 공통 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-120">**Azure Explorer for Eclipse**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="d207b-121">**Azure Plugin for Eclipse with Java**: 이 구성 요소는 Eclipse에서 및 명령줄을 통해 Microsoft Azure 클라우드용 Java 응용 프로그램을 빌드, 테스트 및 배포하도록 지원하는 프로젝트를 개발할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-121">**Azure Plugin for Eclipse with Java**: This component provides support for developing projects that help build, test and deploy Java applications for the Microsoft Azure cloud in Eclipse and via command line.</span></span>
   * <span data-ttu-id="d207b-122">**Azure Web Apps Plugin with Java**: 이 구성 요소는 Microsoft Azure 웹앱 컨테이너에 Java 웹 응용 프로그램을 배포할 수 있도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-122">**Azure Web Apps Plugin with Java**: This component provides support for deploying Java web applications to Microsoft Azure Web App containers.</span></span>
   * <span data-ttu-id="d207b-123">**Microsoft JDBC Driver 4.2 for SQL Server**: 이 구성 요소는 SQL Server용 JDBC API와 Java Platform Enterprise Edition 8용 Microsoft Azure SQL 데이터베이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-123">**Microsoft JDBC Driver 4.2 for SQL Server**: This component provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span>
   * <span data-ttu-id="d207b-124">**Package for Apache Qpid Client Libraries for JMS**: 이 구성 요소는 응용 프로그램이 Microsoft Azure 내에서 AMQP 메시징을 사용할 수 있도록 Apache Qpid 프로젝트의 JMS 클라이언트 구성 요소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-124">**Package for Apache Qpid Client Libraries for JMS**: This component provides the JMS client component from the Apache Qpid project to enable your application to use AMQP messaging in Microsoft Azure.</span></span>
   * <span data-ttu-id="d207b-125">**Package for Microsoft Azure Libraries for Java**: 이 구성 요소는 저장소, 서비스 버스, 서비스 런타임 등의 Microsoft Azure 서비스에 액세스하기 위한 API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-125">**Package for Microsoft Azure Libraries for Java**: This component provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span>

1. <span data-ttu-id="d207b-126">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-126">Click **Next**.</span></span> <span data-ttu-id="d207b-127">(도구 키트를 설치하는 동안 비정상적인 지연이 발생하는 경우에는 **Contact all update sites during install to find required software** 가 선택되어 있지 않은지 확인합니다.)</span><span class="sxs-lookup"><span data-stu-id="d207b-127">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="d207b-128">**설치 세부 정보** 대화 상자에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-128">In the **Install Details** dialog, click **Next**.</span></span>
   
   ![설치 세부 정보 검토][03]

1. <span data-ttu-id="d207b-130">**Review Licenses** 대화 상자에서 사용권 계약 조건을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-130">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="d207b-131">사용권 계약 조건에 동의하면 **동의함**을 클릭한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-131">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="d207b-132">(나머지 단계에서는 사용권 계약 조건에 동의한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-132">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="d207b-133">사용권 계약 조건에 동의하지 않으면 설치 프로세스를 종료합니다.)</span><span class="sxs-lookup"><span data-stu-id="d207b-133">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
   ![Review Licenses][04]
   
   <span data-ttu-id="d207b-135">Eclipse는 필수 패키지를 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-135">Eclipse will download and install the requisite packages.</span></span>
   
   ![설치 진행률][05]

1. <span data-ttu-id="d207b-137">설치를 완료하기 위해 Eclipse를 다시 시작한다는 메시지가 표시되면 **Yes**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d207b-137">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
   ![다시 시작 프롬프트][06]

## <a name="next-steps"></a><span data-ttu-id="d207b-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d207b-139">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->

[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
