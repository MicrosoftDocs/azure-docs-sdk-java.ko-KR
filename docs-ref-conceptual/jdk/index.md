---
title: Azure 개발에 대한 Java JDK 및 장기 지원
description: 이 문서는 Java 애플리케이션을 개발하고 실행하는 Azure 지원의 다운로드 링크 및 설명을 제공합니다.
author: bmitchell287
manager: douge
ms.devlang: java
ms.topic: conceptual
ms.date: 04/09/2019
ms.author: brendm
ms.openlocfilehash: 1bb93f775686b5b0f127c586dda802f4eb5f775d
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533635"
---
# <a name="java-long-term-support-for-azure-and-azure-stack"></a><span data-ttu-id="53f14-103">Azure 및 Azure Stack에 대한 Java 장기 지원</span><span class="sxs-lookup"><span data-stu-id="53f14-103">Java long-term support for Azure and Azure Stack</span></span>

<span data-ttu-id="53f14-104">Microsoft Azure 및 Azure Stack의 Java 개발자는 추가 지원 비용 없이 [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/)를 사용하여 프로덕션 Java 애플리케이션을 빌드하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-104">As a Java developer on Microsoft Azure and Azure Stack, you can build and run production Java applications by using [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="53f14-105">Azure에서 원하는 모든 Java 런타임을 사용할 수 있지만 Zulu를 사용하는 경우 무료 유지 관리 업데이트를 얻고 Microsoft와 지원 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-105">You can use any Java runtime you want on Azure, but when you use Zulu, you get free maintenance updates and you can resolve support issues with Microsoft.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="53f14-106">Java 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="53f14-106">Download and install Java</span></span>](java-jdk-install.md)

## <a name="long-term-support"></a><span data-ttu-id="53f14-107">장기 지원</span><span class="sxs-lookup"><span data-stu-id="53f14-107">Long-term support</span></span>

* [<span data-ttu-id="53f14-108">Java 11</span><span class="sxs-lookup"><span data-stu-id="53f14-108">Java 11</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java11)
* [<span data-ttu-id="53f14-109">Java 8</span><span class="sxs-lookup"><span data-stu-id="53f14-109">Java 8</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java8)
* [<span data-ttu-id="53f14-110">Java 7</span><span class="sxs-lookup"><span data-stu-id="53f14-110">Java 7</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a><span data-ttu-id="53f14-111">기술 미리 보기</span><span class="sxs-lookup"><span data-stu-id="53f14-111">Technical preview</span></span>

* [<span data-ttu-id="53f14-112">Java 12</span><span class="sxs-lookup"><span data-stu-id="53f14-112">Java 12</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a><span data-ttu-id="53f14-113">Azure용 Zulu OpenJDK란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="53f14-113">What is the Zulu OpenJDK for Azure?</span></span>

<span data-ttu-id="53f14-114">OpenJDK의 Azul Zulu Enterprise 빌드는 Microsoft와 Azul Systems가 후원하는 Azure 및 Azure Stack에 대한 OpenJDK의 무료 다중 플랫폼 프로덕션 준비 배포입니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-114">Azul Zulu Enterprise builds of OpenJDK are a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure and Azure Stack that's backed by Microsoft and Azul Systems.</span></span> <span data-ttu-id="53f14-115">해당 배포는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-115">These distributions are:</span></span>

* <span data-ttu-id="53f14-116">JDK(Java Development Kit), JRE(Java Runtime Environment) 및 Headless JRE로 패키지된 OpenJDK의 100% 오픈 소스 빌드.</span><span class="sxs-lookup"><span data-stu-id="53f14-116">100 percent open-source builds of OpenJDK that are packaged as Java Development Kits (JDKs), Java Runtime Environments (JREs), and Headless JREs.</span></span> <span data-ttu-id="53f14-117">이 이진 파일은 Java 애플리케이션 또는 Azure 및 Azure Stack의 구성 요소와 함께 사용할 수 있는 Java SE(Standard Edition)의 완전히 호환되고 상용으로 적합한 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-117">These binaries are fully compatible and compliant commercial builds of Java Standard Edition (SE) that can be used with Java applications or components on Azure and Azure Stack.</span></span>
* <span data-ttu-id="53f14-118">버그 수정, 성능 향상 및 보안 패치를 포함한 장기 지원(LTS)과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-118">Provided with long-term support (LTS), which includes bug fixes, performance enhancements, and security patches.</span></span>
* <span data-ttu-id="53f14-119">Windows, Linux 및 MacOS에서 Java 애플리케이션을 개발하고 실행하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-119">Available for developing and running Java applications on Windows, Linux, and macOS.</span></span>
* <span data-ttu-id="53f14-120">Docker Hub의 컨테이너 이미지 및 Azure Marketplace의 가상 머신(Windows 및 Linux)으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-120">Available as container images on Docker Hub and as virtual machines (Windows and Linux) in the Azure Marketplace.</span></span>
* <span data-ttu-id="53f14-121">Azure에서 다음과 같은 많은 Azure 서비스를 지원하기 위해 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-121">Used by Azure to power many Azure services, such as:</span></span>
  * <span data-ttu-id="53f14-122">Azure App Service(Windows)</span><span class="sxs-lookup"><span data-stu-id="53f14-122">Azure App Service (Windows)</span></span>
  * <span data-ttu-id="53f14-123">Azure App Service(Linux)</span><span class="sxs-lookup"><span data-stu-id="53f14-123">Azure App Service (Linux)</span></span>
  * <span data-ttu-id="53f14-124">Azure 기능</span><span class="sxs-lookup"><span data-stu-id="53f14-124">Azure Functions</span></span>
  * <span data-ttu-id="53f14-125">Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="53f14-125">Azure Service Fabric</span></span>
  * <span data-ttu-id="53f14-126">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="53f14-126">Azure HDInsight</span></span>
  * <span data-ttu-id="53f14-127">Azure Search</span><span class="sxs-lookup"><span data-stu-id="53f14-127">Azure Search</span></span>
  * <span data-ttu-id="53f14-128">Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="53f14-128">Azure DevOps</span></span>
  * <span data-ttu-id="53f14-129">Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="53f14-129">Azure Cloud Shell</span></span>  

## <a name="supported-java-versions-and-update-schedule"></a><span data-ttu-id="53f14-130">지원되는 Java 버전 및 업데이트 일정</span><span class="sxs-lookup"><span data-stu-id="53f14-130">Supported Java versions and update schedule</span></span>

<span data-ttu-id="53f14-131">Azul Systems는 Java SE 7, 8 및 11부터 Java의 모든 LTS 버전에 대해 완벽하게 지원되는 [Azure용 OpenJDK의 Zulu Enterprise 빌드](https://www.azul.com/downloads/azure-only/zulu/)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-131">Azul Systems provides fully supported [Zulu Enterprise builds of OpenJDK for Azure](https://www.azul.com/downloads/azure-only/zulu/) for all LTS versions of Java, starting with Java SE 7, 8, and 11.</span></span> <span data-ttu-id="53f14-132">자세한 내용은 [Azul 보도 자료](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53f14-132">For more information, see the [Azul press release](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span></span>

|<span data-ttu-id="53f14-133">Java SE LTS</span><span class="sxs-lookup"><span data-stu-id="53f14-133">Java SE LTS</span></span>  |<span data-ttu-id="53f14-134">지원 기한</span><span class="sxs-lookup"><span data-stu-id="53f14-134">Support until</span></span>  |
|---------|----------|
|<span data-ttu-id="53f14-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span><span class="sxs-lookup"><span data-stu-id="53f14-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span></span> |<span data-ttu-id="53f14-136">2023년 7월</span><span class="sxs-lookup"><span data-stu-id="53f14-136">July 2023</span></span> |
|<span data-ttu-id="53f14-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span><span class="sxs-lookup"><span data-stu-id="53f14-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span></span> |<span data-ttu-id="53f14-138">2025년 3월</span><span class="sxs-lookup"><span data-stu-id="53f14-138">March 2025</span></span>|
|<span data-ttu-id="53f14-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span><span class="sxs-lookup"><span data-stu-id="53f14-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span></span> |<span data-ttu-id="53f14-140">2026년 9월</span><span class="sxs-lookup"><span data-stu-id="53f14-140">September 2026</span></span>|
|<span data-ttu-id="53f14-141">[![Java 12](../media/jdk/java-12.png)]()</span><span class="sxs-lookup"><span data-stu-id="53f14-141">[![Java 12](../media/jdk/java-12.png)]()</span></span> |<span data-ttu-id="53f14-142">**미리 보기**</span><span class="sxs-lookup"><span data-stu-id="53f14-142">**Preview**</span></span>|

<span data-ttu-id="53f14-143">위의 JDK 버전에는 분기별 보안 업데이트, 버그 수정, 그리고 필요한 경우 중요 대역 외 업데이트 및 패치가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-143">These JDK releases have quarterly security updates, bug fixes, and critical out-of-band updates and patches as needed.</span></span> <span data-ttu-id="53f14-144">이 지원에는 Java 11과 같은 최신 버전의 Java에서 보고되는 보안 업데이트의 백 포트 및 Java 7 및 8에 대한 버그 수정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-144">This support includes back ports of security updates and bug fixes to Java 7 and 8 that are reported in newer versions of Java, such as Java 11.</span></span> <span data-ttu-id="53f14-145">이 지원은 Java 이전 버전의 지속적인 안정성과 보안을 보장하기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-145">The support ensures the continued stability and security of older versions of Java.</span></span> <span data-ttu-id="53f14-146">Azure 고객은 계획되지 않은 모든 Java SE 구독 요금이 발생하지 않고 이러한 보안 업데이트 및 플랫폼 버그 수정을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-146">Azure customers can get these security updates and platform bug fixes without incurring any unplanned Java SE subscription fees.</span></span>

<span data-ttu-id="53f14-147">Azul Systems는 이러한 릴리스에 대한 [Java SE 로드맵](https://www.azul.com/products/azul_support_roadmap/)을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-147">Azul Systems maintains a [Java SE roadmap](https://www.azul.com/products/azul_support_roadmap/) for these releases.</span></span>

## <a name="benefits-for-developers"></a><span data-ttu-id="53f14-148">개발자에 대한 혜택</span><span class="sxs-lookup"><span data-stu-id="53f14-148">Benefits for developers</span></span>

<span data-ttu-id="53f14-149">Azul Zulu JDK 릴리스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-149">The Azul Zulu JDK releases are:</span></span>

* <span data-ttu-id="53f14-150">Microsoft와 Azul Systems에서 모두 후원 및 지원.</span><span class="sxs-lookup"><span data-stu-id="53f14-150">Backed and supported by both Microsoft and Azul Systems.</span></span>

   * <span data-ttu-id="53f14-151">Zulu 이진 파일은 프로덕션 준비 상태이며 Microsoft 및 Azul Systems에서 후원.</span><span class="sxs-lookup"><span data-stu-id="53f14-151">Zulu binaries are production ready and backed by Microsoft and Azul Systems.</span></span>
   * <span data-ttu-id="53f14-152">Zulu는 Java 7, 8 및 11에 대한 비용이 없는 LTS와 함께 제공됩니다(LTS는 Java 17에도 제공됩니다).</span><span class="sxs-lookup"><span data-stu-id="53f14-152">Zulu comes with zero-cost LTS for Java 7, 8, and 11 (LTS will be provided for Java 17, as well).</span></span> <span data-ttu-id="53f14-153">Java 버전은 필요한 경우에만 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-153">You can upgrade Java versions only when you need to.</span></span>
   * <span data-ttu-id="53f14-154">Java 7은 2023년 7월까지 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-154">Java 7 is supported until July 2023.</span></span> <span data-ttu-id="53f14-155">Java 8 및 11은 2024년 이후에도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-155">Java 8 and 11 are supported beyond 2024.</span></span>
   * <span data-ttu-id="53f14-156">Microsoft는 많은 Azure 서비스 기반 머신에서 내부적으로 Zulu 실행을 약속했습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-156">Microsoft is committed to running Zulu internally on machines that power many Azure services.</span></span>

* <span data-ttu-id="53f14-157">프로덕션 준비.</span><span class="sxs-lookup"><span data-stu-id="53f14-157">Production-ready.</span></span>

   * <span data-ttu-id="53f14-158">OpenJDK의 해당 빌드에 대한 100% 오픈 소스.</span><span class="sxs-lookup"><span data-stu-id="53f14-158">100 percent open-source for its builds of OpenJDK.</span></span>
   * <span data-ttu-id="53f14-159">많은 Java SE 배포에 대한 드롭인 교체.</span><span class="sxs-lookup"><span data-stu-id="53f14-159">Drop-in replacements for many Java SE distributions.</span></span>
   * <span data-ttu-id="53f14-160">JDK, JRE 및 JRE 헤드리스.</span><span class="sxs-lookup"><span data-stu-id="53f14-160">JDK, JRE, and JRE-headless.</span></span>
   * <span data-ttu-id="53f14-161">Java 7, 8 및 11.</span><span class="sxs-lookup"><span data-stu-id="53f14-161">Java 7, 8, and 11.</span></span>
   * <span data-ttu-id="53f14-162">OpenJDK Community TCK(Technology Compatibility Kit)를 사용하여 Java SE 사양에 적합한 것으로 확인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-162">Verified compliant with the Java SE specifications that use the OpenJDK Community Technology Compatibility Kit (TCK).</span></span>
   * <span data-ttu-id="53f14-163">개발자는 Java SE 7, 8 및 11에 대한 버그 수정, 성능 향상 및 보안 패치를 포함하여 Java SE에 대한 프로덕션 업데이트를 계속 받습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-163">As a developer, you continue to receive production updates for Java SE, including bug fixes, performance enhancements, and security patches for Java SE 7, 8, and 11.</span></span>

* <span data-ttu-id="53f14-164">다중 플랫폼 지원.</span><span class="sxs-lookup"><span data-stu-id="53f14-164">Supported for multi-platform.</span></span> <span data-ttu-id="53f14-165">Zulu는 다음을 포함한 여러 플랫폼 및 버전에 대한 이진 파일을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-165">Zulu supports binaries for multiple platforms and versions, including:</span></span>

   * <span data-ttu-id="53f14-166">Windows 클라이언트</span><span class="sxs-lookup"><span data-stu-id="53f14-166">Windows client</span></span>
     * <span data-ttu-id="53f14-167">10</span><span class="sxs-lookup"><span data-stu-id="53f14-167">10</span></span>
     * <span data-ttu-id="53f14-168">8.1</span><span class="sxs-lookup"><span data-stu-id="53f14-168">8.1</span></span>
     * <span data-ttu-id="53f14-169">8, 7</span><span class="sxs-lookup"><span data-stu-id="53f14-169">8, 7</span></span>
   * <span data-ttu-id="53f14-170">Windows Server</span><span class="sxs-lookup"><span data-stu-id="53f14-170">Windows Server</span></span>
     * <span data-ttu-id="53f14-171">2016 R2</span><span class="sxs-lookup"><span data-stu-id="53f14-171">2016 R2</span></span>
     * <span data-ttu-id="53f14-172">2016</span><span class="sxs-lookup"><span data-stu-id="53f14-172">2016</span></span>
     * <span data-ttu-id="53f14-173">2012 R2</span><span class="sxs-lookup"><span data-stu-id="53f14-173">2012 R2</span></span>
     * <span data-ttu-id="53f14-174">2012</span><span class="sxs-lookup"><span data-stu-id="53f14-174">2012</span></span>
     * <span data-ttu-id="53f14-175">2008 R2</span><span class="sxs-lookup"><span data-stu-id="53f14-175">2008 R2</span></span>
   * <span data-ttu-id="53f14-176">다음을 포함한 Linux</span><span class="sxs-lookup"><span data-stu-id="53f14-176">Linux, including</span></span>
     * <span data-ttu-id="53f14-177">RHEL</span><span class="sxs-lookup"><span data-stu-id="53f14-177">RHEL</span></span>
     * <span data-ttu-id="53f14-178">CentOS</span><span class="sxs-lookup"><span data-stu-id="53f14-178">CentOS</span></span>
     * <span data-ttu-id="53f14-179">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="53f14-179">Ubuntu</span></span>
     * <span data-ttu-id="53f14-180">SLES</span><span class="sxs-lookup"><span data-stu-id="53f14-180">SLES</span></span>
     * <span data-ttu-id="53f14-181">Debian</span><span class="sxs-lookup"><span data-stu-id="53f14-181">Debian</span></span>
     * <span data-ttu-id="53f14-182">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="53f14-182">Oracle Linux</span></span>
   * <span data-ttu-id="53f14-183">macOS X</span><span class="sxs-lookup"><span data-stu-id="53f14-183">macOS X</span></span>
   * <span data-ttu-id="53f14-184">여러 패키지 형식으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-184">Delivery in multiple package types:</span></span>
     * <span data-ttu-id="53f14-185">MSI, ZIP, TAR, DEB, RPM 및 DMG</span><span class="sxs-lookup"><span data-stu-id="53f14-185">MSI, ZIP, TAR, DEB, RPM, and DMG</span></span>

    <span data-ttu-id="53f14-186">여러 기본 OS 이미지의 Zulu JDK, JRE 및 JRE 헤드리스에 대해 인증된 Docker 컨테이너 이미지를 Docker에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-186">Certified Docker container images for Zulu JDK, JRE, and JRE-headless on multiple base OS images are available at Docker.</span></span>

    <span data-ttu-id="53f14-187">허브:</span><span class="sxs-lookup"><span data-stu-id="53f14-187">Hub:</span></span>

    * [<span data-ttu-id="53f14-188">JDK</span><span class="sxs-lookup"><span data-stu-id="53f14-188">JDK</span></span>](https://hub.docker.com/_/microsoft-java-jdk)
    * [<span data-ttu-id="53f14-189">JRE</span><span class="sxs-lookup"><span data-stu-id="53f14-189">JRE</span></span>](https://hub.docker.com/_/microsoft-java-jre)
    * [<span data-ttu-id="53f14-190">JRE 헤드리스</span><span class="sxs-lookup"><span data-stu-id="53f14-190">JRE-headless</span></span>](https://hub.docker.com/_/microsoft-java-jre-headless)

* <span data-ttu-id="53f14-191">무료입니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-191">No cost.</span></span>

   * <span data-ttu-id="53f14-192">Microsoft는 Azure에서 Java 앱을 빌드하고 확장하는 데 필요한 모든 것을 무료로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-192">Microsoft provides everything you need to build and scale Java apps on Azure, at no cost to you.</span></span> <span data-ttu-id="53f14-193">즉, Zulu를 통해 Java 앱에 대한 무료 보안 업데이트 및 플랫폼 버그 수정을 수수료 없이 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-193">Through Zulu you'll receive free security updates and platform bug fixes for Java apps without any fees.</span></span>
   * <span data-ttu-id="53f14-194">[Java Flight Recorder 및 Mission Control](java-jdk-flight-recorder-and-mission-control.md)은 Zulu Java 8, 11 및 12(미리 보기)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-194">[Java Flight Recorder and Mission Control](java-jdk-flight-recorder-and-mission-control.md) are available in Zulu Java 8, 11, and 12 (Preview).</span></span>

* <span data-ttu-id="53f14-195">LTS 이외 버전의 기술 미리 보기로 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-195">Available as tech preview of non-LTS versions.</span></span>

   * <span data-ttu-id="53f14-196">기술 미리 보기를 통해, 결국 Java 17 LTS로 종료될 단기 버전에 제공될 때 새 기능을 점진적으로 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-196">With tech previews, you can progressively test new features as they're delivered, in short-term versions that will eventually graduate to Java 17 LTS.</span></span>

* <span data-ttu-id="53f14-197">OpenJDK 변경이 업스트림 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-197">Changes to OpenJDK are sent upstream.</span></span>

   * <span data-ttu-id="53f14-198">Azul Systems 커미터는 Zulu 변경 내용을 OpenJDK에 푸시하여 업스트림 리포지토리를 포괄적이고 모든 것이 포함되도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-198">Azul Systems committers push Zulu changes to OpenJDK, which makes the upstream repo comprehensive and inclusive.</span></span>

<span data-ttu-id="53f14-199">항상 Java 개발자는 Azure로 Oracle JDK 및 Red Hat JDK를 포함하여 사용자 고유의 Java 런타임을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-199">As always, as a Java developer, you can bring to Azure your own Java runtimes, including the Oracle JDK and the Red Hat JDK.</span></span> <span data-ttu-id="53f14-200">또한 보안 인프라와 풍부한 기능을 갖춘 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-200">You can also use the secure infrastructure and feature-rich services.</span></span> <span data-ttu-id="53f14-201">또한 Oracle Java SE의 프로덕션 버전을 사용하여 Azure의 Windows 또는 Linux 가상 머신에서 Java 워크로드를 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-201">The production edition of Oracle Java SE is available to you for running Java workloads in Windows or Linux virtual machines on Azure.</span></span>

## <a name="use-java-jdks-for-local-development"></a><span data-ttu-id="53f14-202">로컬 개발을 위해 Java JDK 사용</span><span class="sxs-lookup"><span data-stu-id="53f14-202">Use Java JDKs for local development</span></span> 

<span data-ttu-id="53f14-203">로컬 개발 환경에서 사용하기 위해 [Azure 및 Azure Stack용 Java JDK를 다운로드](https://www.azul.com/downloads/azure-only/zulu/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-203">You can [download Java JDKs for Azure and Azure Stack](https://www.azul.com/downloads/azure-only/zulu/) for use in your local development environments.</span></span> <span data-ttu-id="53f14-204">Windows, Linux 및 macOS에서 다운로드가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-204">Downloads are available for Windows, Linux, and macOS.</span></span> <span data-ttu-id="53f14-205">Linux에서 작업하는 경우, [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) 및 [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) 패키지 관리자를 통해 패키지를 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53f14-205">If you're working on Linux, you can also get packages through the [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) and [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) package managers.</span></span>

<span data-ttu-id="53f14-206">추가 지침은 [Azure용 Docker 이미지](java-jdk-docker-images.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53f14-206">For additional guidance, see [Docker images for Azure](java-jdk-docker-images.md).</span></span>
