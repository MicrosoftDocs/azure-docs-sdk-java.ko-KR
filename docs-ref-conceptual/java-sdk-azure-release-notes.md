---
title: Java용 Azure 관리 라이브러리 릴리스 정보 | Microsoft Docs
description: Java용 Azure 관리 라이브러리에 대한 새 기능과 주요 변경 내용을 확인합니다.
keywords: Azure, Java, API, 참조, 정보, 업데이트, 사용 중단
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 0aaa83ceb42192441decb5972baae56fed337fb2
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48899458"
---
# <a name="release-notes"></a><span data-ttu-id="ef963-104">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="ef963-104">Release Notes</span></span> 

## <a name="october-5-2017---130"></a><span data-ttu-id="ef963-105">2017년 10월 5일 - 1.3.0</span><span class="sxs-lookup"><span data-stu-id="ef963-105">October 5, 2017 - 1.3.0</span></span> 

<span data-ttu-id="ef963-106">버전 1.3.0은 이전 릴리스에서 일반 가용성(안정적인) 단계에 도달하도록 서비스 및 기능을 사용하기 위해 이전 버전과 호환 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="ef963-106">Version 1.3.0 is backwards compatible with previous versions for services and features use that reached the general availability (stable) stage in previous releases.</span></span>

<span data-ttu-id="ef963-107">해당 서비스에 대한 미리 보기 버전의 모든 주요 변경 내용은 @Beta 주석으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef963-107">Any breaking changes from Preview versions for those services are marked with the @Beta annotation.</span></span>

<span data-ttu-id="ef963-108">코드를 1.3.0으로 마이그레이션하는 경우 [이 정보](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md)를 사용하여 1.3 버전용 기존 코드를 준비할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef963-108">If you are migrating your code to 1.3.0, you can use [these notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) to prepare your existing code for the 1.3 version.</span></span>

### <a name="generally-availabile-in-v13"></a><span data-ttu-id="ef963-109">V1.3에서 일반적으로 사용 가능</span><span class="sxs-lookup"><span data-stu-id="ef963-109">Generally availabile in V1.3</span></span>

<span data-ttu-id="ef963-110">특히 다음과 같은 이전 릴리스에 있던 일부 API도 이제는 GA가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ef963-110">Some of the APIs that were still in Beta in previous releases are now GA, in particular:</span></span>

- <span data-ttu-id="ef963-111">비동기 메서드</span><span class="sxs-lookup"><span data-stu-id="ef963-111">async methods</span></span>
- <span data-ttu-id="ef963-112">이전에 베타 버전이었던 모든 CDN 메서드</span><span class="sxs-lookup"><span data-stu-id="ef963-112">all methods in CDN that were previously in Beta</span></span>
- <span data-ttu-id="ef963-113">이전에 베타 버전이었던 모든 Application Gateway 메서드 및 인터페이스</span><span class="sxs-lookup"><span data-stu-id="ef963-113">all methods and interfaces in Application Gateways that were previously in Beta</span></span>

  <span data-ttu-id="ef963-114">라이브러리의 일부는 여전히 미리 보기로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef963-114">Some parts of the library are still in Preview.</span></span> <span data-ttu-id="ef963-115">라이브러리의 현재 상태에 대해 아래 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef963-115">Refer to the table below for the current state of the libraries:</span></span>

<span data-ttu-id="ef963-116">서비스 또는 기능</span><span class="sxs-lookup"><span data-stu-id="ef963-116">Service or feature</span></span> | <span data-ttu-id="ef963-117">GA로 사용 가능</span><span class="sxs-lookup"><span data-stu-id="ef963-117">Available as GA</span></span> | <span data-ttu-id="ef963-118">미리 보기로 사용 가능</span><span class="sxs-lookup"><span data-stu-id="ef963-118">Available as Preview</span></span> 
---------|---------|---------|-
<span data-ttu-id="ef963-119">컴퓨팅</span><span class="sxs-lookup"><span data-stu-id="ef963-119">Compute</span></span>  | <span data-ttu-id="ef963-120">가상 머신 및 VM 확장, 가상 머신 확장 집합, 관리 디스크</span><span class="sxs-lookup"><span data-stu-id="ef963-120">Virtual machines and VM extensions, Virtual machine scale sets, managed disks</span></span>   | <span data-ttu-id="ef963-121">Azure 컨테이너 서비스, Azure 컨테이너 레지스트리</span><span class="sxs-lookup"><span data-stu-id="ef963-121">Azure container service, Azure container registry</span></span> 
<span data-ttu-id="ef963-122">Storage</span><span class="sxs-lookup"><span data-stu-id="ef963-122">Storage</span></span>   |  <span data-ttu-id="ef963-123">Storage 계정</span><span class="sxs-lookup"><span data-stu-id="ef963-123">Storage accounts</span></span>       |    <span data-ttu-id="ef963-124">암호화</span><span class="sxs-lookup"><span data-stu-id="ef963-124">Encryption</span></span>     
<span data-ttu-id="ef963-125">SQL Database</span><span class="sxs-lookup"><span data-stu-id="ef963-125">SQL Database</span></span>  | <span data-ttu-id="ef963-126">데이터베이스, 방화벽, 탄력적 풀</span><span class="sxs-lookup"><span data-stu-id="ef963-126">Databases, firewalls, elastic pools</span></span>              
<span data-ttu-id="ef963-127">네트워킹</span><span class="sxs-lookup"><span data-stu-id="ef963-127">Networking</span></span>    |  <span data-ttu-id="ef963-128">가상 네트워크, 네트워크 인터페이스, IP 주소, 라우팅 테이블, 네트워크 보안 그룹, DNS, Traffic Manager, 응용 프로그램 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="ef963-128">Virtual networks , network interfaces , IP addresses ,routing tables, network security groups , DNS, Traffic managers, Application gateways</span></span>  |    <span data-ttu-id="ef963-129">부하 분산 장치, 네트워크 피어링, Virtual Network 게이트웨이, 네트워크 감시자</span><span class="sxs-lookup"><span data-stu-id="ef963-129">Load balancers, Network peering, Virtual Network Gateway, Network watchers</span></span> 
<span data-ttu-id="ef963-130">더 많은 서비스</span><span class="sxs-lookup"><span data-stu-id="ef963-130">More services</span></span>    |  <span data-ttu-id="ef963-131">리소스 관리자, Key Vault, Redis, CDN, Batch</span><span class="sxs-lookup"><span data-stu-id="ef963-131">Resource Manager, Key Vault, Redis,  CDN, Batch</span></span>       |  <span data-ttu-id="ef963-132">웹앱, 함수 앱, Service Bus, Graph RBAC, Cosmos DB, 검색</span><span class="sxs-lookup"><span data-stu-id="ef963-132">Web apps, Function apps, Service Bus, Graph RBAC, Cosmos DB, Search</span></span>  
<span data-ttu-id="ef963-133">기본 사항</span><span class="sxs-lookup"><span data-stu-id="ef963-133">Fundamentals</span></span>     |   <span data-ttu-id="ef963-134">인증 - 코어, 비동기 메서드, 관리되는 서비스 ID</span><span class="sxs-lookup"><span data-stu-id="ef963-134">Authentication - core , Async methods , Managed Service Identity</span></span>      |      |

> <span data-ttu-id="ef963-135">미리 보기 기능은 클래스에서 `@Beta` 주석 또는 라이브러리에서 인터페이스 또는 메서드 수준으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef963-135">Preview features are marked with a `@Beta` annotation at the class or interface or method level in libraries.</span></span> <span data-ttu-id="ef963-136">이러한 기능은 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef963-136">These features are subject to change.</span></span> <span data-ttu-id="ef963-137">나중에 어떤 방식으로든 수정 또는 제거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef963-137">They can be modified in any way, or even removed, in the future.</span></span>

### <a name="import-with-maven"></a><span data-ttu-id="ef963-138">Maven을 사용하여 가져오기</span><span class="sxs-lookup"><span data-stu-id="ef963-138">Import with Maven</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a><span data-ttu-id="ef963-139">도움말 가져오기 및 피드백 제공</span><span class="sxs-lookup"><span data-stu-id="ef963-139">Get help and give feedback</span></span>

<span data-ttu-id="ef963-140">자신의 코드에 있는 라이브러리를 사용하여 도움말을 얻으려면 [Stack Overflow(영문)](http://stackoverflow.com/questions/tagged/azure-java-sdk) 커뮤니티를 확인해 주세요.</span><span class="sxs-lookup"><span data-stu-id="ef963-140">Check out the [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) community for help using the libraries in your own code.</span></span> <span data-ttu-id="ef963-141">버그가 발생하거나 이러한 라이브러리를 향상시키기 위한 제안 사항이 있으면 [GitHub](https://github.com/Azure/azure-sdk-for-java/issues)를 통해 문제를 제출해 주세요.</span><span class="sxs-lookup"><span data-stu-id="ef963-141">If you encounter any bugs or have suggestions to improve these libraries, please file issues via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span></span>


