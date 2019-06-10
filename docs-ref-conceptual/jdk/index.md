---
title: Azure 개발에 대한 Java JDK 및 장기 지원
description: Java 애플리케이션을 개발하고 실행하는 Azure 지원의 다운로드 및 설명입니다.
author: bmitchell287
manager: douge
ms.devlang: java
ms.topic: conceptual
ms.date: 04/09/2019
ms.author: brendm
ms.openlocfilehash: 340f6149ffe39ccbb2d7de534ed63b8784d1f63a
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270879"
---
# <a name="java-long-term-support-for-azure-and-azure-stack"></a><span data-ttu-id="2e74c-103">Azure 및 Azure Stack에 대한 Java 장기 지원</span><span class="sxs-lookup"><span data-stu-id="2e74c-103">Java Long-Term Support for Azure and Azure Stack</span></span>

<span data-ttu-id="2e74c-104">Azure 및 Azure Stack의 Java 개발자는 추가 지원 비용 없이 [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/)를 사용하여 프로덕션 Java 애플리케이션을 빌드하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-104">Java developers on Azure and Azure Stack can build and run production Java applications using [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="2e74c-105">Azure에서 원하는 모든 Java 런타임을 사용할 수 있지만 Zulu를 사용하는 경우 무료 유지 관리 업데이트를 가져오면 Microsoft와의 지원 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-105">You can use any Java runtime you want on Azure, but when you use Zulu you get free maintenance updates and can create support issues with Microsoft.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2e74c-106">Java 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="2e74c-106">Download and install Java</span></span>](java-jdk-install.md)

## <a name="long-term-support-lts"></a><span data-ttu-id="2e74c-107">LTS(장기 지원)</span><span class="sxs-lookup"><span data-stu-id="2e74c-107">Long-term support (LTS)</span></span>

* [<span data-ttu-id="2e74c-108">Java 11</span><span class="sxs-lookup"><span data-stu-id="2e74c-108">Java 11</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java11)
* [<span data-ttu-id="2e74c-109">Java 8</span><span class="sxs-lookup"><span data-stu-id="2e74c-109">Java 8</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java8)
* [<span data-ttu-id="2e74c-110">Java 7</span><span class="sxs-lookup"><span data-stu-id="2e74c-110">Java 7</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a><span data-ttu-id="2e74c-111">기술 미리 보기</span><span class="sxs-lookup"><span data-stu-id="2e74c-111">Technical preview</span></span>

* [<span data-ttu-id="2e74c-112">Java 12</span><span class="sxs-lookup"><span data-stu-id="2e74c-112">Java 12</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a><span data-ttu-id="2e74c-113">Azure용 Zulu OpenJDK란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="2e74c-113">What is the Zulu OpenJDK for Azure?</span></span>

<span data-ttu-id="2e74c-114">OpenJDK의 Azul Zulu Enterprise 빌드는 Microsoft와 Azul Systems가 후원하는 Azure 및 Azure Stack에 대한 OpenJDK의 무료 다중 플랫폼 프로덕션 준비 배포입니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-114">Azul Zulu Enterprise builds of OpenJDK are a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure and Azure Stack backed by Microsoft and Azul Systems.</span></span> <span data-ttu-id="2e74c-115">해당 배포는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-115">These distributions are:</span></span>

* <span data-ttu-id="2e74c-116">JDK(Java Development Kit), JRE(Java Runtime Environment) 및 Headless JRE로 패키지된 OpenJDK의 100% 오픈 소스 빌드.</span><span class="sxs-lookup"><span data-stu-id="2e74c-116">100% open source builds of OpenJDK packaged as Java Development Kits (JDKs), Java Runtime Environments (JREs), and Headless JREs.</span></span> <span data-ttu-id="2e74c-117">이 이진 파일은 Java 애플리케이션 또는 Azure 및 Azure Stack의 구성 요소와 함께 사용할 수 있는 Java SE(Standard Edition)의 완전히 호환되고 상용으로 적합한 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-117">These binaries are fully compatible and compliant commercial builds of Java Standard Edition (SE) that can be used with Java applications or components on Azure and Azure Stack.</span></span>
* <span data-ttu-id="2e74c-118">버그 수정, 성능 향상 및 보안 패치를 포함한 장기 지원과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-118">Provided with long-term support including bug fixes, performance enhancements, and security patches.</span></span>
* <span data-ttu-id="2e74c-119">Windows, Linux 및 MacOS에서 Java 애플리케이션을 개발하고 실행하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-119">Available for developing and running Java applications on Windows, Linux, and MacOS.</span></span>
* <span data-ttu-id="2e74c-120">Docker Hub의 컨테이너 이미지 및 Azure Marketplace의 가상 머신(Windows 및 Linux)으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-120">Available as container images on Docker Hub and as virtual machines (Windows and Linux) on Azure Marketplace.</span></span>
* <span data-ttu-id="2e74c-121">Microsoft Azure에서 다음과 같은 많은 Azure 서비스를 지원하기 위해 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-121">Used by Microsoft Azure to power many Azure services, such as:</span></span>
  * <span data-ttu-id="2e74c-122">App Service Windows</span><span class="sxs-lookup"><span data-stu-id="2e74c-122">App Service Windows</span></span>
  * <span data-ttu-id="2e74c-123">App Service Linux</span><span class="sxs-lookup"><span data-stu-id="2e74c-123">App Service Linux</span></span>
  * <span data-ttu-id="2e74c-124">Functions</span><span class="sxs-lookup"><span data-stu-id="2e74c-124">Functions</span></span>
  * <span data-ttu-id="2e74c-125">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2e74c-125">Service Fabric</span></span>
  * <span data-ttu-id="2e74c-126">HDInsight</span><span class="sxs-lookup"><span data-stu-id="2e74c-126">HDInsight</span></span>
  * <span data-ttu-id="2e74c-127">검색</span><span class="sxs-lookup"><span data-stu-id="2e74c-127">Search</span></span>
  * <span data-ttu-id="2e74c-128">Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="2e74c-128">Azure DevOps</span></span>
  * <span data-ttu-id="2e74c-129">Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="2e74c-129">Cloud Shell</span></span>  

## <a name="supported-java-versions-and-update-schedule"></a><span data-ttu-id="2e74c-130">지원되는 Java 버전 및 업데이트 일정</span><span class="sxs-lookup"><span data-stu-id="2e74c-130">Supported Java versions and update schedule</span></span>

<span data-ttu-id="2e74c-131">Azul Systems는 Java SE 7, 8 및 11부터 Java의 모든 LTS(장기 지원) 버전에 대해 완벽하게 지원되는 [Microsoft Azure용 OpenJDK의 Zulu Enterprise 빌드](https://www.azul.com/downloads/azure-only/zulu/)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-131">Azul Systems provides fully-supported [Zulu Enterprise builds of OpenJDK for Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) for all long-term support (LTS) versions of Java, starting with Java SE 7, 8, and 11.</span></span> <span data-ttu-id="2e74c-132">자세한 내용은 [Azul 보도 자료](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-132">More information can be found in the [Azul press release](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span></span>

|<span data-ttu-id="2e74c-133">Java SE LTS</span><span class="sxs-lookup"><span data-stu-id="2e74c-133">Java SE LTS</span></span>  |<span data-ttu-id="2e74c-134">지원 기한</span><span class="sxs-lookup"><span data-stu-id="2e74c-134">Support until</span></span>  |
|---------|----------|
|<span data-ttu-id="2e74c-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span><span class="sxs-lookup"><span data-stu-id="2e74c-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span></span> |<span data-ttu-id="2e74c-136">2023년 7월</span><span class="sxs-lookup"><span data-stu-id="2e74c-136">July 2023</span></span> |
|<span data-ttu-id="2e74c-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span><span class="sxs-lookup"><span data-stu-id="2e74c-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span></span> |<span data-ttu-id="2e74c-138">2025년 3월</span><span class="sxs-lookup"><span data-stu-id="2e74c-138">March 2025</span></span>|
|<span data-ttu-id="2e74c-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span><span class="sxs-lookup"><span data-stu-id="2e74c-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span></span> |<span data-ttu-id="2e74c-140">2026년 9월</span><span class="sxs-lookup"><span data-stu-id="2e74c-140">Sept. 2026</span></span>|
|<span data-ttu-id="2e74c-141">[![Java 12](../media/jdk/java-12.png)]()</span><span class="sxs-lookup"><span data-stu-id="2e74c-141">[![Java 12](../media/jdk/java-12.png)]()</span></span> |<span data-ttu-id="2e74c-142">**미리 보기**</span><span class="sxs-lookup"><span data-stu-id="2e74c-142">**PREVIEW**</span></span>|

<span data-ttu-id="2e74c-143">위의 JDK 버전에는 분기별 보안 업데이트, 버그 수정, 그리고 필요한 경우 중요 대역 외 업데이트 및 패치가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-143">These JDK releases have quarterly security updates, bug fixes, and critical out-of-band updates and patches as needed.</span></span>  <span data-ttu-id="2e74c-144">이 지원에는 Java 11과 같은 Java의 최신 버전에서 보고된 Java 7 및 8에 대한 보안 업데이트 및 버그 수정 이식이 포함되며, 이전 버전의 Java에 대한 지속적인 안정성 및 보안을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-144">This support includes back ports of security updates and bug fixes to Java 7 and 8 reported in newer versions of Java such as Java 11, which ensures the continued stability and security of older versions of Java.</span></span>  <span data-ttu-id="2e74c-145">Azure 고객은 계획되지 않은 모든 Java SE 구독 요금이 발생하지 않고 이러한 보안 업데이트 및 플랫폼 버그 수정을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-145">Azure customers can get these security updates and platform bug fixes without incurring any unplanned Java SE subscription fees.</span></span>

<span data-ttu-id="2e74c-146">Azul Systems는 이러한 릴리스에 대한 [Java SE 로드맵](https://www.azul.com/products/azul_support_roadmap/)을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-146">Azul Systems maintains a [Java SE roadmap](https://www.azul.com/products/azul_support_roadmap/) for these releases.</span></span>

## <a name="benefits-for-developers"></a><span data-ttu-id="2e74c-147">개발자에 대한 혜택</span><span class="sxs-lookup"><span data-stu-id="2e74c-147">Benefits for developers</span></span>

<span data-ttu-id="2e74c-148">Azul Zulu JDK 릴리스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-148">The Azul Zulu JDK releases are:</span></span>

1. <span data-ttu-id="2e74c-149">Microsoft와 Azul Systems에서 모두 후원 및 지원</span><span class="sxs-lookup"><span data-stu-id="2e74c-149">Backed and supported by both Microsoft and Azul Systems</span></span>

   * <span data-ttu-id="2e74c-150">Zulu 이진 파일은 프로덕션 준비 상태이며 Microsoft 및 Azul Systems에서 후원</span><span class="sxs-lookup"><span data-stu-id="2e74c-150">Zulu binaries are production-ready and backed by Microsoft and Azul Systems</span></span>
   * <span data-ttu-id="2e74c-151">Zulu에는 Java 7, 8 및 11에 대한 무료 LTS(장기 지원)가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-151">Zulu comes with zero-cost long-term support (LTS) for Java 7, 8, and 11.</span></span> <span data-ttu-id="2e74c-152">(LTS는 Java 17에 대해서도 제공됩니다.)</span><span class="sxs-lookup"><span data-stu-id="2e74c-152">(LTS will be provided for Java 17, as well).</span></span> <span data-ttu-id="2e74c-153">Java 버전은 필요한 경우에만 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-153">You can upgrade Java versions only when you need to.</span></span>
   * <span data-ttu-id="2e74c-154">Java 7은 2023년 7월까지 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-154">Java 7 supported until July 2023.</span></span> <span data-ttu-id="2e74c-155">Java 8 및 11은 2024년 이후에도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-155">Java 8 and 11 are supported beyond 2024.</span></span>
   * <span data-ttu-id="2e74c-156">Microsoft는 많은 Azure 서비스 기반 머신에서 내부적으로 Zulu 실행을 약속했습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-156">Microsoft is committed to running Zulu internally on machines that power many Azure services.</span></span>

2. <span data-ttu-id="2e74c-157">프로덕션 준비</span><span class="sxs-lookup"><span data-stu-id="2e74c-157">Production-ready</span></span>

   * <span data-ttu-id="2e74c-158">OpenJDK의 해당 빌드에 대한 100% 오픈 소스.</span><span class="sxs-lookup"><span data-stu-id="2e74c-158">100% open-source for its builds of OpenJDK.</span></span>
   * <span data-ttu-id="2e74c-159">많은 Java SE 배포에 대한 드롭인 교체.</span><span class="sxs-lookup"><span data-stu-id="2e74c-159">Drop-in replacements for many Java SE distributions.</span></span>
   * <span data-ttu-id="2e74c-160">JDK, JRE 및 JRE 헤드리스</span><span class="sxs-lookup"><span data-stu-id="2e74c-160">JDK, JRE, and JRE-headless</span></span>
   * <span data-ttu-id="2e74c-161">Java 7, 8 및 11</span><span class="sxs-lookup"><span data-stu-id="2e74c-161">Java 7, 8, and 11</span></span>
   * <span data-ttu-id="2e74c-162">OpenJDK Community TCK(Technology Compatibility Kit)를 사용하여 Java SE 사양에 적합한 것으로 확인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-162">Verified compliant with the Java SE  specifications using the OpenJDK Community Technology Compatibility Kit (TCK).</span></span>
   * <span data-ttu-id="2e74c-163">개발자는 Java SE 7, 8 및 11에 대한 버그 수정, 성능 향상 및 보안 패치를 포함하여 Java SE에 대한 프로덕션 업데이트를 계속 받습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-163">Developers will continue to receive production updates for Java SE, including bug fixes, performance enhancements, and security patches for Java SE 7, 8, and 11.</span></span>

3. <span data-ttu-id="2e74c-164">다중 플랫폼 지원.</span><span class="sxs-lookup"><span data-stu-id="2e74c-164">Supported for multi-platform.</span></span> <span data-ttu-id="2e74c-165">Zulu는 다음을 포함한 여러 플랫폼 및 버전에 대한 이진 파일을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-165">Zulu supports binaries for multiple platforms and versions, including:</span></span>

   * <span data-ttu-id="2e74c-166">Windows 클라이언트</span><span class="sxs-lookup"><span data-stu-id="2e74c-166">Windows Client</span></span>
     * <span data-ttu-id="2e74c-167">10</span><span class="sxs-lookup"><span data-stu-id="2e74c-167">10</span></span>
     * <span data-ttu-id="2e74c-168">8.1</span><span class="sxs-lookup"><span data-stu-id="2e74c-168">8.1</span></span>
     * <span data-ttu-id="2e74c-169">8, 7</span><span class="sxs-lookup"><span data-stu-id="2e74c-169">8, 7</span></span>
   * <span data-ttu-id="2e74c-170">Windows Server</span><span class="sxs-lookup"><span data-stu-id="2e74c-170">Windows Server</span></span>
     * <span data-ttu-id="2e74c-171">2016R2</span><span class="sxs-lookup"><span data-stu-id="2e74c-171">2016R2</span></span>
     * <span data-ttu-id="2e74c-172">2016</span><span class="sxs-lookup"><span data-stu-id="2e74c-172">2016</span></span>
     * <span data-ttu-id="2e74c-173">2012 R2</span><span class="sxs-lookup"><span data-stu-id="2e74c-173">2012 R2</span></span>
     * <span data-ttu-id="2e74c-174">2012</span><span class="sxs-lookup"><span data-stu-id="2e74c-174">2012</span></span>
     * <span data-ttu-id="2e74c-175">2008 R2</span><span class="sxs-lookup"><span data-stu-id="2e74c-175">2008 R2</span></span>
   * <span data-ttu-id="2e74c-176">다음을 포함한 Linux</span><span class="sxs-lookup"><span data-stu-id="2e74c-176">Linux, including</span></span>
     * <span data-ttu-id="2e74c-177">RHEL</span><span class="sxs-lookup"><span data-stu-id="2e74c-177">RHEL</span></span>
     * <span data-ttu-id="2e74c-178">CentOS</span><span class="sxs-lookup"><span data-stu-id="2e74c-178">CentOS</span></span>
     * <span data-ttu-id="2e74c-179">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="2e74c-179">Ubuntu</span></span>
     * <span data-ttu-id="2e74c-180">SLES</span><span class="sxs-lookup"><span data-stu-id="2e74c-180">SLES</span></span>
     * <span data-ttu-id="2e74c-181">Debian</span><span class="sxs-lookup"><span data-stu-id="2e74c-181">Debian</span></span>
     * <span data-ttu-id="2e74c-182">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="2e74c-182">Oracle Linux</span></span>
   * <span data-ttu-id="2e74c-183">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="2e74c-183">Mac OS X</span></span>
   * <span data-ttu-id="2e74c-184">여러 패키지 형식으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-184">delivered in multiple package types:</span></span>
     * <span data-ttu-id="2e74c-185">MSI, ZIP, TAR, DEB, RPM 및 DMG</span><span class="sxs-lookup"><span data-stu-id="2e74c-185">MSI, ZIP, TAR, DEB, RPM, and DMG</span></span>

    <span data-ttu-id="2e74c-186">여러 기본 OS 이미지의 Zulu JDK, JRE 및 JRE 헤드리스에 대해 인증된 Docker 컨테이너 이미지를 Docker에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-186">Certified Docker container images for Zulu JDK, JRE, and JRE-headless on multiple base OS images are available at Docker.</span></span>

    <span data-ttu-id="2e74c-187">허브:</span><span class="sxs-lookup"><span data-stu-id="2e74c-187">Hub:</span></span>

    * [<span data-ttu-id="2e74c-188">JDK</span><span class="sxs-lookup"><span data-stu-id="2e74c-188">JDK</span></span>](https://hub.docker.com/_/microsoft-java-jdk)
    * [<span data-ttu-id="2e74c-189">JRE</span><span class="sxs-lookup"><span data-stu-id="2e74c-189">JRE</span></span>](https://hub.docker.com/_/microsoft-java-jre)
    * [<span data-ttu-id="2e74c-190">JRE 헤드리스</span><span class="sxs-lookup"><span data-stu-id="2e74c-190">JRE-headless</span></span>](https://hub.docker.com/_/microsoft-java-jre-headless)

4. <span data-ttu-id="2e74c-191">무료</span><span class="sxs-lookup"><span data-stu-id="2e74c-191">No cost</span></span>

   * <span data-ttu-id="2e74c-192">Microsoft는 Azure에서 Java 앱을 빌드하고 확장하는 데 필요한 모든 것을 무료로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-192">Microsoft provides everything you need to build and scale Java apps on Azure at no cost to you.</span></span> <span data-ttu-id="2e74c-193">즉, Zulu를 통해 Java 앱에 대한 무료 보안 업데이트 및 플랫폼 버그 수정을 수수료 없이 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-193">Through Zulu you'll receive free security updates and platform bug fixes for Java apps without any fees.</span></span>
   * <span data-ttu-id="2e74c-194">[Java Flight Recorder 및 Mission Control](java-jdk-flight-recorder-and-mission-control.md)은 Zulu Java 8, 11 및 12(미리 보기)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-194">[Java Flight Recorder and Mission Control](java-jdk-flight-recorder-and-mission-control.md) are available in Zulu Java 8, 11, and 12 (Preview).</span></span>

5. <span data-ttu-id="2e74c-195">LTS 이외 버전의 기술 미리 보기</span><span class="sxs-lookup"><span data-stu-id="2e74c-195">Tech Preview of Non-LTS versions</span></span>

   * <span data-ttu-id="2e74c-196">기술 미리 보기는 결국 Java 17 LTS로 종료될 단기 버전에 제공될 때 새 기능을 점진적으로 테스트할 기회를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-196">Tech previews provide you with opportunities to progressively test new features as they are delivered in short-term versions that will eventually graduate to Java 17 LTS.</span></span>

6. <span data-ttu-id="2e74c-197">OpenJDK 변경이 업스트림됨</span><span class="sxs-lookup"><span data-stu-id="2e74c-197">Changes to OpenJDK are up-streamed</span></span>

   * <span data-ttu-id="2e74c-198">Azul Systems 커미터는 Zulu 변경 내용을 OpenJDK에 푸시하여 업스트림 리포지토리를 포괄적이고 모든 것이 포함되도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-198">Azul Systems committers push Zulu changes to OpenJDK which makes the upstream repo comprehensive and inclusive.</span></span>

<span data-ttu-id="2e74c-199">늘 그렇듯이 Java 개발자는 Oracle JDK 및 Red Hat JDK를 포함한 자신의 고유한 Java 런타임을 Azure로 가져오고 보안 인프라 및 기능이 풍부한 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-199">As always, Java developers can bring their own Java run-times, including Oracle JDK and Red Hat JDK, to Azure and use  the secure infrastructure and feature-rich services.</span></span> <span data-ttu-id="2e74c-200">또한 Java 개발자는 Oracle Java SE의 프로덕션 버전을 사용하여 Azure의 Windows 또는 Linux 가상 머신에서 Java 워크로드를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-200">The production edition of Oracle Java SE is also available to Java developers for running Java workloads in Windows or Linux virtual machines on Azure.</span></span>

## <a name="use-for-local-development"></a><span data-ttu-id="2e74c-201">로컬 개발을 위해 사용</span><span class="sxs-lookup"><span data-stu-id="2e74c-201">Use for local development</span></span> 

<span data-ttu-id="2e74c-202">개발자는 로컬 개발 환경에서 사용하기 위해 Azure 및 Azure Stack용 Java JDK를 [다운로드](https://www.azul.com/downloads/azure-only/zulu/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-202">Developers can [download](https://www.azul.com/downloads/azure-only/zulu/) Java JDKs for Azure and Azure Stack for use in local development environments.</span></span> <span data-ttu-id="2e74c-203">Windows, Linux 및 macOS에서 다운로드가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-203">Downloads are available for Windows, Linux, and macOS.</span></span> <span data-ttu-id="2e74c-204">Linux에서 작업하는 개발자는 [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) 및 [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) 패키지 관리자를 통해 패키지를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e74c-204">Developers working on Linux can also get packages through the [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) and [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) package managers.</span></span>

<span data-ttu-id="2e74c-205">추가 지침은 [Azure용 Docker 이미지](java-jdk-docker-images.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e74c-205">For additional guidance see [Docker images for Azure](java-jdk-docker-images.md).</span></span>