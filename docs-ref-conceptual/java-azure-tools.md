---
title: "Azure Java 개발자용 도구 | Microsoft Docs"
description: "Azure에서 작업하는 Java 개발자를 위한 IDE 통합, 에뮬레이터, 리소스 탐색기 및 명령줄 인터페이스입니다."
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 4/10/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: ce0b003cc7c48c8690f4236547ddec36e6ea9d53
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/09/2017
---
# <a name="azure-tools-for-java-developers"></a><span data-ttu-id="1bdf5-103">Java 개발자용 Azure 도구</span><span class="sxs-lookup"><span data-stu-id="1bdf5-103">Azure tools for Java developers</span></span>

## <a name="client-and-management-libraries"></a><span data-ttu-id="1bdf5-104">클라이언트 및 관리 라이브러리</span><span class="sxs-lookup"><span data-stu-id="1bdf5-104">Client and management libraries</span></span>

<span data-ttu-id="1bdf5-105">Java용 Azure 라이브러리를 사용하여 서비스에 연결하고 응용 프로그램에서 Azure 리소스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1bdf5-105">Connect to services and manage Azure resources from your applications with the Azure libraries for Java.</span></span> <span data-ttu-id="1bdf5-106">이 종속성을 *pom.xml* 프로젝트에 추가하여 관리 라이브러리를 Maven 프로젝트로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1bdf5-106">Import the management libraries into your Maven projects by adding this dependency to your project *pom.xml*.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
```

<span data-ttu-id="1bdf5-107">Java용 Azure 라이브러리와 함께 [라이브러리의 전체 목록](java-sdk-azure-install.md) 및 [시작](java-sdk-azure-get-started.md)을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1bdf5-107">View the [complete list of libraries](java-sdk-azure-install.md) and [get started](java-sdk-azure-get-started.md) with the Azure libraries for Java.</span></span>

## <a name="eclipse-and-intellij-plugins"></a><span data-ttu-id="1bdf5-108">Eclipse 및 IntelliJ 플러그 인</span><span class="sxs-lookup"><span data-stu-id="1bdf5-108">Eclipse and IntelliJ plugins</span></span>

<span data-ttu-id="1bdf5-109">[Eclipse](eclipse/azure-toolkit-for-eclipse.md) 및 [IntelliJ](intellij/azure-toolkit-for-intellij.md)용 Azure 도구 키트를 사용하여 Azure 리소스를 관리하고 IDE에서 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1bdf5-109">Manage Azure resources and deploy apps from your IDE with The Azure toolkits for [Eclipse](eclipse/azure-toolkit-for-eclipse.md) and [IntelliJ](intellij/azure-toolkit-for-intellij.md).</span></span>   

![Azure 탐색기를 보여 주는 IntelliJ 도구 키트](media/intelliJ-azure-explorer.png)

<span data-ttu-id="1bdf5-111">[Eclipse용 Azure 도구 키트 시작](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [IntelliJ용 Azure 도구 키트 시작](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span><span class="sxs-lookup"><span data-stu-id="1bdf5-111">[Get started with Azure Toolkit for Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Get started with Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span></span> 

## <a name="azure-cli-20"></a><span data-ttu-id="1bdf5-112">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1bdf5-112">Azure CLI 2.0</span></span>

<span data-ttu-id="1bdf5-113">Azure 2.0 CLI는 Azure 리소스를 관리하는 명령줄 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1bdf5-113">The Azure 2.0 CLI provides a command-line experience to manage Azure resources.</span></span> <span data-ttu-id="1bdf5-114">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview)을 실행하는 브라우저에서 사용하거나 macOS, Linux 및 Windows에서 [설치](https://docs.microsoft.com/cli/azure/install-azure-cli)하고 명령줄에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bdf5-114">You can use it in your browser with [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), or you can [install](https://docs.microsoft.com/cli/azure/install-azure-cli) it on macOS, Linux, and Windows and run it from the command line.</span></span>

<span data-ttu-id="1bdf5-115">[Azure CLI 2.0 시작](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="1bdf5-115">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>

## <a name="azure-storage-explorer"></a><span data-ttu-id="1bdf5-116">Azure Storage 탐색기</span><span class="sxs-lookup"><span data-stu-id="1bdf5-116">Azure Storage Explorer</span></span> 

<span data-ttu-id="1bdf5-117">바탕 화면에서 Azure 저장소 계정, 컨테이너 및 Blob/파일을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1bdf5-117">Manage Azure storage accounts, containers, and blobs/files from your desktop.</span></span> <span data-ttu-id="1bdf5-118">Azure Storage 탐색기는 현재 미리 보기로 있으며 Windows, macOS 및 Linux에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1bdf5-118">Azure Storage Explorer is currently in Preview and works on Windows, macOS, and Linux.</span></span>

[<span data-ttu-id="1bdf5-119">Azure 저장소 탐색기 시작</span><span class="sxs-lookup"><span data-stu-id="1bdf5-119">Get started with Azure Storage Explorer</span></span>](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)