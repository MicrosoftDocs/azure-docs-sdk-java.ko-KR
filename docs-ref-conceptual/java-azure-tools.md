---
title: Azure Java 개발자용 도구 | Microsoft Docs
description: Azure에서 작업하는 Java 개발자를 위한 IDE 통합, 에뮬레이터, 리소스 탐색기 및 명령줄 인터페이스입니다.
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 11/13/2018
ms.author: routlaw
ms.openlocfilehash: 9e9828540ddc678f69eab11f5a61eef8bf8e916c
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339017"
---
# <a name="azure-tools-for-java-developers"></a><span data-ttu-id="88dd3-103">Java 개발자용 Azure 도구</span><span class="sxs-lookup"><span data-stu-id="88dd3-103">Azure tools for Java developers</span></span>

## <a name="supported-jdk-runtimes"></a><span data-ttu-id="88dd3-104">지원되는 JDK 런타임</span><span class="sxs-lookup"><span data-stu-id="88dd3-104">Supported JDK runtimes</span></span>

<span data-ttu-id="88dd3-105">Azure 및 Azure Stack에서 Java 개발자는 추가 지원 비용 없이 [OpenJDK의 Azul Systems Zulu Enterprise 빌드](https://www.azul.com/downloads/azure-only/zulu/)를 사용하여 프로덕션 Java 7, 8 및 11 애플리케이션을 빌드하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88dd3-105">Java developers on Azure and Azure Stack can build and run production Java 7,8, and 11 applications using [Azul Systems Zulu Enterprise builds of OpenJDK](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="88dd3-106">현재 다른 JDK를 사용하여 Java 앱을 실행하는 경우 무료 지원 및 유지 관리를 위해 Azure에서 Zulu로 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="88dd3-106">If you’re currently running Java apps with other JDKs, consider migrating to Zulu on Azure for free support and maintenance.</span></span> 

<span data-ttu-id="88dd3-107">Azure에서 개발하는 경우 사용 가능한 지원되는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="88dd3-107">For more information about the supported JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>

## <a name="eclipse-and-intellij-plugins"></a><span data-ttu-id="88dd3-108">Eclipse 및 IntelliJ 플러그 인</span><span class="sxs-lookup"><span data-stu-id="88dd3-108">Eclipse and IntelliJ plugins</span></span>

<span data-ttu-id="88dd3-109">[Eclipse](eclipse/azure-toolkit-for-eclipse.md) 및 [IntelliJ](intellij/azure-toolkit-for-intellij.md)용 Azure 도구 키트를 사용하여 Azure 리소스를 관리하고 IDE에서 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="88dd3-109">Manage Azure resources and deploy apps from your IDE with The Azure toolkits for [Eclipse](eclipse/azure-toolkit-for-eclipse.md) and [IntelliJ](intellij/azure-toolkit-for-intellij.md).</span></span>   

![Azure 탐색기를 보여 주는 IntelliJ 도구 키트](media/intelliJ-azure-explorer.png)

<span data-ttu-id="88dd3-111">[Eclipse용 Azure 도구 키트 시작](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [IntelliJ용 Azure 도구 키트 시작](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span><span class="sxs-lookup"><span data-stu-id="88dd3-111">[Get started with Azure Toolkit for Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Get started with Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span></span> 

## <a name="visual-studio-code"></a><span data-ttu-id="88dd3-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="88dd3-112">Visual Studio Code</span></span>

<span data-ttu-id="88dd3-113">[VS Code](https://code.visualstudio.com/)는 가벼우면서 강력한 코드 편집기로, MacOS, Windows, Linux에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88dd3-113">[VS Code](https://code.visualstudio.com/) is a lightweight but powerful code editor available for MacOS, Windows, and Linux.</span></span> <span data-ttu-id="88dd3-114">VS Code는 프로젝트 지원, 코드 완성, 디버깅, 린팅, 탐색을 제공하는 여러 확장을 통해 간단한 최신 Java 개발 워크플로를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="88dd3-114">VS Code supports a simple, modern Java development workflow through a set of extensions that provide project support, code completion, debugging, linting, and navigation.</span></span>

<span data-ttu-id="88dd3-115">[VS Code 및 Java 시작](https://code.visualstudio.com/docs/java)
[VS Code용 Java 확장 팩](https://code.visualstudio.com/docs/java/extensions)</span><span class="sxs-lookup"><span data-stu-id="88dd3-115">[Get Started with VS Code and Java](https://code.visualstudio.com/docs/java)
[Java extension pack for VS Code](https://code.visualstudio.com/docs/java/extensions)</span></span>  

## <a name="azure-cli-20"></a><span data-ttu-id="88dd3-116">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="88dd3-116">Azure CLI 2.0</span></span>

<span data-ttu-id="88dd3-117">Azure 2.0 CLI는 Azure 리소스를 관리하는 명령줄 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="88dd3-117">The Azure 2.0 CLI provides a command-line experience to manage Azure resources.</span></span> <span data-ttu-id="88dd3-118">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview)을 실행하는 브라우저에서 사용하거나 macOS, Linux 및 Windows에서 [설치](https://docs.microsoft.com/cli/azure/install-azure-cli)하고 명령줄에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="88dd3-118">You can use it in your browser with [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), or you can [install](https://docs.microsoft.com/cli/azure/install-azure-cli) it on macOS, Linux, and Windows and run it from the command line.</span></span>

<span data-ttu-id="88dd3-119">[Azure CLI 2.0 시작](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="88dd3-119">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>

## <a name="azure-storage-explorer"></a><span data-ttu-id="88dd3-120">Azure Storage 탐색기</span><span class="sxs-lookup"><span data-stu-id="88dd3-120">Azure Storage Explorer</span></span> 

<span data-ttu-id="88dd3-121">바탕 화면에서 Azure 저장소 계정, 컨테이너 및 Blob/파일을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="88dd3-121">Manage Azure storage accounts, containers, and blobs/files from your desktop.</span></span> <span data-ttu-id="88dd3-122">Azure Storage 탐색기는 현재 미리 보기로 있으며 Windows, macOS 및 Linux에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="88dd3-122">Azure Storage Explorer is currently in Preview and works on Windows, macOS, and Linux.</span></span>

[<span data-ttu-id="88dd3-123">Azure Storage 탐색기 시작</span><span class="sxs-lookup"><span data-stu-id="88dd3-123">Get started with Azure Storage Explorer</span></span>](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)
