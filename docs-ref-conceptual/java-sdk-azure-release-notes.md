---
title: "Java용 Azure 관리 라이브러리 릴리스 정보 | Microsoft Docs"
description: "Java용 Azure 관리 라이브러리에 대한 새 기능과 주요 변경 내용을 확인합니다."
keywords: "Azure, Java, API, 참조, 정보, 업데이트, 사용 중단"
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: c0d5c4b3702d3bee4e93de51cec36e72aeaf598f
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/09/2017
---
# <a name="release-notes"></a><span data-ttu-id="dbb1b-104">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="dbb1b-104">Release Notes</span></span> 

## <a name="june-30-2017---110"></a><span data-ttu-id="dbb1b-105">2017년 6월 30일 - 1.1.0</span><span class="sxs-lookup"><span data-stu-id="dbb1b-105">June 30, 2017 - 1.1.0</span></span> 

<span data-ttu-id="dbb1b-106">V1.1은 공용으로 사용하도록 설계되어 V1.0의 일반 가용성(안정) 단계에 도달한 API에서 V1.0 이전 버전과 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1b-106">V1.1 is backwards compatible with V1.0 in the APIs intended for public use that reached the general availability (stable) stage in V1.0.</span></span>

<span data-ttu-id="dbb1b-107">V.0에서 @Beta 주석으로 표시된 API에서 도입된 몇 가지 혁신적인 변경 내용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1b-107">Some breaking changes were introduced in APIs marked with the @Beta annotation in V.0</span></span>

<span data-ttu-id="dbb1b-108">코드를 1.1.0으로 마이그레이션하는 경우 [이 정보](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)를 사용하면 1.0.0에서 1.1.0용 코드를 준비할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1b-108">If you are migrating your code to 1.1.0, you can use [these notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) for preparing your code for 1.1.0 from 1.0.0.</span></span>

### <a name="generally-availabile-in-v11"></a><span data-ttu-id="dbb1b-109">V1.1에서 일반적으로 사용 가능한 기능</span><span class="sxs-lookup"><span data-stu-id="dbb1b-109">Generally availabile in V1.1</span></span>

<span data-ttu-id="dbb1b-110">특히 다음과 같은 V1.0 베타 버전에 있던 일부 API도 이제는 V1.1의 GA가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1b-110">Some of the APIs that were still in Beta in V1.0 are now GA in V1.1, in particular:</span></span>

- <span data-ttu-id="dbb1b-111">비동기 메서드</span><span class="sxs-lookup"><span data-stu-id="dbb1b-111">async methods</span></span>
- <span data-ttu-id="dbb1b-112">이전에 베타 버전이었던 모든 CDN 메서드</span><span class="sxs-lookup"><span data-stu-id="dbb1b-112">all methods in CDN that were previously in Beta</span></span>
- <span data-ttu-id="dbb1b-113">이전에 베타 버전이었던 모든 응용 프로그램 게이트웨이 메서드 및 인터페이스</span><span class="sxs-lookup"><span data-stu-id="dbb1b-113">all methods and interfaces in Application Gateways that were previously in Beta</span></span>

 <span data-ttu-id="dbb1b-114">라이브러리의 일부는 여전히 미리 보기로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbb1b-114">Some parts of the library are still in Preview.</span></span> <span data-ttu-id="dbb1b-115">라이브러리의 현재 상태에 대해 아래 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbb1b-115">Refer to the table below for the current state of the libraries:</span></span>

<span data-ttu-id="dbb1b-116">서비스 또는 기능</span><span class="sxs-lookup"><span data-stu-id="dbb1b-116">Service or feature</span></span> | <span data-ttu-id="dbb1b-117">GA로 사용 가능</span><span class="sxs-lookup"><span data-stu-id="dbb1b-117">Available as GA</span></span> | <span data-ttu-id="dbb1b-118">미리 보기로 사용 가능</span><span class="sxs-lookup"><span data-stu-id="dbb1b-118">Available as Preview</span></span>  | <span data-ttu-id="dbb1b-119">서비스 예정</span><span class="sxs-lookup"><span data-stu-id="dbb1b-119">Coming soon</span></span> |
---------|---------|---------|---------|
<span data-ttu-id="dbb1b-120">Compute</span><span class="sxs-lookup"><span data-stu-id="dbb1b-120">Compute</span></span>  | <span data-ttu-id="dbb1b-121">가상 컴퓨터 및 VM 확장, 가상 컴퓨터 확장 집합, 관리 디스크</span><span class="sxs-lookup"><span data-stu-id="dbb1b-121">Virtual machines and VM extensions, Virtual machine scale sets, managed disks</span></span>   | <span data-ttu-id="dbb1b-122">Azure 컨테이너 서비스, Azure 컨테이너 레지스트리</span><span class="sxs-lookup"><span data-stu-id="dbb1b-122">Azure container service, Azure container registry</span></span> |    |
<span data-ttu-id="dbb1b-123">저장소</span><span class="sxs-lookup"><span data-stu-id="dbb1b-123">Storage</span></span>   |  <span data-ttu-id="dbb1b-124">저장소 계정</span><span class="sxs-lookup"><span data-stu-id="dbb1b-124">Storage accounts</span></span>       |         |   <span data-ttu-id="dbb1b-125">암호화</span><span class="sxs-lookup"><span data-stu-id="dbb1b-125">Encryption</span></span>      |
<span data-ttu-id="dbb1b-126">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="dbb1b-126">SQL Database</span></span>  | <span data-ttu-id="dbb1b-127">데이터베이스, 방화벽, 탄력적 풀</span><span class="sxs-lookup"><span data-stu-id="dbb1b-127">Databases, firewalls, elastic pools</span></span>        |         |   <span data-ttu-id="dbb1b-128">더 많은 기능</span><span class="sxs-lookup"><span data-stu-id="dbb1b-128">More features</span></span>      |
<span data-ttu-id="dbb1b-129">네트워킹</span><span class="sxs-lookup"><span data-stu-id="dbb1b-129">Networking</span></span>    |  <span data-ttu-id="dbb1b-130">가상 네트워크, 네트워크 인터페이스, IP 주소, 라우팅 테이블, 네트워크 보안 그룹, DNS, Traffic Manager, 응용 프로그램 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="dbb1b-130">Virtual networks , network interfaces , IP addresses ,routing tables, network security groups , DNS, Traffic managers, Application gateways</span></span>  |    <span data-ttu-id="dbb1b-131">부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="dbb1b-131">Load balancers</span></span>     |   <span data-ttu-id="dbb1b-132">VPN, 네트워크 감시자</span><span class="sxs-lookup"><span data-stu-id="dbb1b-132">VPN, Network watchers</span></span>   |
<span data-ttu-id="dbb1b-133">더 많은 서비스</span><span class="sxs-lookup"><span data-stu-id="dbb1b-133">More services</span></span>    |  <span data-ttu-id="dbb1b-134">리소스 관리자, Key Vault, Redis, CDN, Batch</span><span class="sxs-lookup"><span data-stu-id="dbb1b-134">Resource Manager, Key Vault, Redis,  CDN, Batch</span></span>       |  <span data-ttu-id="dbb1b-135">웹앱, 함수 앱, Service Bus, Graph RBAC, DocumentDB</span><span class="sxs-lookup"><span data-stu-id="dbb1b-135">Web apps, Function apps, Service Bus, Graph RBAC, DocumentDB</span></span>   | <span data-ttu-id="dbb1b-136">모니터, Scheduler, 함수 관리, 검색, 더 많은 Graph RBAC 기능</span><span class="sxs-lookup"><span data-stu-id="dbb1b-136">Monitor ,Scheduler, Functions management, Search, more Graph RBAC features</span></span>        |
<span data-ttu-id="dbb1b-137">기본 사항</span><span class="sxs-lookup"><span data-stu-id="dbb1b-137">Fundamentals</span></span>     |   <span data-ttu-id="dbb1b-138">인증 - 코어, 비동기 메서드</span><span class="sxs-lookup"><span data-stu-id="dbb1b-138">Authentication - core , Async methods</span></span>       |      |         |

### <a name="import-with-maven"></a><span data-ttu-id="dbb1b-139">Maven을 사용하여 가져오기</span><span class="sxs-lookup"><span data-stu-id="dbb1b-139">Import with Maven</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a><span data-ttu-id="dbb1b-140">도움말 가져오기 및 피드백 제공</span><span class="sxs-lookup"><span data-stu-id="dbb1b-140">Get help and give feedback</span></span>

<span data-ttu-id="dbb1b-141">자신의 코드에 있는 라이브러리를 사용하여 도움말을 얻으려면 [Stack Overflow(영문)](http://stackoverflow.com/questions/tagged/azure-java-sdk) 커뮤니티를 확인해 주세요.</span><span class="sxs-lookup"><span data-stu-id="dbb1b-141">Check out the [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) community for help using the libraries in your own code.</span></span> <span data-ttu-id="dbb1b-142">버그가 발생하거나 이러한 라이브러리를 향상시키기 위한 제안 사항이 있으면 [GitHub](https://github.com/Azure/azure-sdk-for-java/issues)를 통해 문제를 제출해 주세요.</span><span class="sxs-lookup"><span data-stu-id="dbb1b-142">If you encounter any bugs or have suggestions to improve these libraries, please file issues via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span></span>

### <a name="migrate-from-previous-releases"></a><span data-ttu-id="dbb1b-143">이전 릴리스에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="dbb1b-143">Migrate from previous releases</span></span>

<span data-ttu-id="dbb1b-144">[1.0.0-beta5에서 마이그레이션(영문)](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md) [1.1.0에서 마이그레이션(영문)](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)</span><span class="sxs-lookup"><span data-stu-id="dbb1b-144">[Migrate from 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md)  [Migrate from 1.1.0](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)</span></span>


