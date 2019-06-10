---
title: Java Flight Recorder 및 Mission Control
description: Java Flight Recorder 및 Mission Control을 사용하여 앱 데이터를 수집하고 검토하기 위한 지침입니다.
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: b27e0f741f1322b7e8e1df363dbb2f40a3d34d53
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2019
ms.locfileid: "64568566"
---
# <a name="using-java-flight-recorder-jfr-and-mission-control"></a><span data-ttu-id="f34d2-103">JFR(Java Flight Recorder) 및 Mission Control 사용</span><span class="sxs-lookup"><span data-stu-id="f34d2-103">Using Java Flight Recorder (JFR) and Mission Control</span></span>

<span data-ttu-id="f34d2-104">Zulu Mission Control은 2018년 Oracle이 오픈 소스로 공개하고 OpenJDK 보호 대상 프로젝트로 관리되는 JDK Mission Control의 완전히 테스트된 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-104">Zulu Mission Control is a fully-tested build of JDK Mission Control, which was open sourced by Oracle in 2018 and is managed as a project under the OpenJDK umbrella.</span></span> <span data-ttu-id="f34d2-105">Flight Recorder와 결합할 경우 Mission Control은 오버헤드가 낮고 대화형으로 모니터링하는 Java 워크로드 관리 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-105">Coupled with Flight Recorder, Mission Control delivers low-overhead, interactive monitoring and management capabilities for Java workloads.</span></span>

<span data-ttu-id="f34d2-106">Zulu Mission Control은 다음과 같은 JDK/JRE와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-106">Zulu Mission Control is compatible with the following JDKs/JREs:</span></span>

* <span data-ttu-id="f34d2-107">Zulu 12.1 이상</span><span class="sxs-lookup"><span data-stu-id="f34d2-107">Zulu 12.1 and later</span></span>
* <span data-ttu-id="f34d2-108">Zulu 11.0 이상</span><span class="sxs-lookup"><span data-stu-id="f34d2-108">Zulu 11.0 and later</span></span>
* <span data-ttu-id="f34d2-109">Zulu 8u202(8.36) 이상</span><span class="sxs-lookup"><span data-stu-id="f34d2-109">Zulu 8u202 (8.36) and later</span></span>
* <span data-ttu-id="f34d2-110">Oracle OpenJDK 11+15 이상</span><span class="sxs-lookup"><span data-stu-id="f34d2-110">Oracle OpenJDK 11+15 and later</span></span>
* <span data-ttu-id="f34d2-111">Oracle Java 11.0 이상</span><span class="sxs-lookup"><span data-stu-id="f34d2-111">Oracle Java 11.0 and later</span></span>
* <span data-ttu-id="f34d2-112">Oracle Java 8.0 이상</span><span class="sxs-lookup"><span data-stu-id="f34d2-112">Oracle Java 8.0 and later</span></span>

<span data-ttu-id="f34d2-113">아래 단계에 따라 Zulu Mission Control을 설치하고 JVM(Java Virtual Machine)에 연결하고 실행 중인 애플리케이션의 모든 특성을 실시간으로 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-113">Follow the steps below to install Zulu Mission Control, connect to a Java Virtual Machine (JVM), and gain real-time visibility into all aspects of a running application.</span></span>

1.  <span data-ttu-id="f34d2-114">[Zulu Mission Control 호환 JDK/JRE를 설치합니다](java-jdk-install.md).</span><span class="sxs-lookup"><span data-stu-id="f34d2-114">[Install a Zulu Mission Control compatible JDK/JRE](java-jdk-install.md).</span></span>

2.  <span data-ttu-id="f34d2-115">[Azul 다운로드 사이트](https://www.azul.com/products/zulu-mission-control/)에서 Zulu Mission Control을 다운로드하고 시스템에 맞는 버전을 선택하고 로컬로 저장한 후, 해당 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-115">Download Zulu Mission Control from [the Azul download site](https://www.azul.com/products/zulu-mission-control/), choose the appropriate version for your system, save it locally, and change to that directory.</span></span>

3.  <span data-ttu-id="f34d2-116">다운로드한 파일을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-116">Expand the downloaded file.</span></span>

    <span data-ttu-id="f34d2-117">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="f34d2-117">**Linux:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    <span data-ttu-id="f34d2-118">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="f34d2-118">**Windows:**</span></span>

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    <span data-ttu-id="f34d2-119">**MacOS:**</span><span class="sxs-lookup"><span data-stu-id="f34d2-119">**MacOS:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

4.  <span data-ttu-id="f34d2-120">호환되는 JDK 중 하나를 사용하여 Java 애플리케이션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-120">Start your Java application using one of the compatible JDKs.</span></span> <span data-ttu-id="f34d2-121">예:</span><span class="sxs-lookup"><span data-stu-id="f34d2-121">E.g.:</span></span>

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

5.  <span data-ttu-id="f34d2-122">Zulu Mission Control 시작</span><span class="sxs-lookup"><span data-stu-id="f34d2-122">Start Zulu Mission Control</span></span>

    <span data-ttu-id="f34d2-123">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="f34d2-123">**Linux:**</span></span>

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    <span data-ttu-id="f34d2-124">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="f34d2-124">**Windows:**</span></span>

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    <span data-ttu-id="f34d2-125">**MacOS:**</span><span class="sxs-lookup"><span data-stu-id="f34d2-125">**MacOS:**</span></span>

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

6.  <span data-ttu-id="f34d2-126">Mission Control에 대한 JVM 설치 전환(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="f34d2-126">Switch the JVM installation for Mission Control (Optional)</span></span>

    <span data-ttu-id="f34d2-127">Windows에서 *zmc.exe*는 레지스트리에 구성된 기본 JVM 설치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-127">On Windows, *zmc.exe* will use the default JVM installation configured in the registry.</span></span> <span data-ttu-id="f34d2-128">Zulu Mission Control은 전체 JDK에서 시작해야 로컬 JVM 인스턴스를 자동으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-128">Zulu Mission Control must be launched from a full JDK to be able to detect local JVM instances automatically.</span></span> <span data-ttu-id="f34d2-129">JRE의 경우 아래 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-129">If this is a JRE, you will see the warning below:</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="f34d2-130">![JDK 설치가 JRE 전용인 경우 경고](../media/jdk/azul-jfr-1.png)</span><span class="sxs-lookup"><span data-stu-id="f34d2-130">![Warning if JDK install is JRE-only](../media/jdk/azul-jfr-1.png)</span></span>

    <span data-ttu-id="f34d2-131">Mission Control에서 사용하는 JVM을 변경하려면 아래 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-131">To change the JVM used by Mission Control, follow these steps:</span></span> 
    1.  <span data-ttu-id="f34d2-132">*zmc.exe*와 같은 디렉터리에 있는 *zmc.ini* 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-132">Open *zmc.ini* configuration file, located in the same directory as the *zmc.exe*</span></span>
    2.  <span data-ttu-id="f34d2-133">`-vmargs` 줄 앞에 다음 두 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-133">Before the line `-vmargs`, add two lines:</span></span>
        * <span data-ttu-id="f34d2-134">첫 번째 줄에서 `–vm`를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-134">On the first line, write `–vm`</span></span>
        * <span data-ttu-id="f34d2-135">두 번째 줄에서 JDK 설치 경로를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-135">On the second line, write the path to your JDK installation.</span></span> <span data-ttu-id="f34d2-136">(예, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span><span class="sxs-lookup"><span data-stu-id="f34d2-136">(For example, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span></span>

7.  <span data-ttu-id="f34d2-137">애플리케이션을 실행 중인 JVM을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-137">Locate the JVM running your application</span></span>
    1.  <span data-ttu-id="f34d2-138">Zulu Mission Control 창의 왼쪽 위 창에서 **JVM Browser**라는 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-138">In the upper left pane of the Zulu Mission Control window click on the tab labelled **JVM Browser**.</span></span>
    2.  <span data-ttu-id="f34d2-139">애플리케이션을 실행 중인 JVM 인스턴스에 대해 왼쪽 위의 목록 항목을 선택하고 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-139">Select and expand the list item in the upper left for your the JVM instance running your application.</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="f34d2-140">![JVM 인스턴스에 대한 왼쪽 위의 목록 항목을 확장합니다.](../media/jdk/azul-jfr-2.png)</span><span class="sxs-lookup"><span data-stu-id="f34d2-140">![Expand the list item in the upper-left for your JVM instance](../media/jdk/azul-jfr-2.png)</span></span>


8.  <span data-ttu-id="f34d2-141">필요한 경우 비행 기록을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-141">Start a Flight Recording, if necessary</span></span>
    1.  <span data-ttu-id="f34d2-142">Flight Recorder에 "기록 없음"이 표시된 경우 JVM Browser 탭의 Flight Recorder 줄을 마우스 오른쪽 단추로 클릭하고 **비행 기록 시작...** 을 선택하여 기록을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-142">If the Flight Recorder displays "No Recordings", start one by right-clicking on the Flight Recorder line in the JVM Browser tab and selecting **Start Flight Recording...**</span></span>
    2.  <span data-ttu-id="f34d2-143">고정 기간 기록 또는 연속 기록 및 구성 프로파일링(세분화된) 또는 연속 구성(낮은 오버헤드)을 선택한 다음, **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-143">Select either a fixed duration recording or a continuous recording, and either a Profiling configuration (fine-grained) or a Continuous configuration (lower overhead), then click **Finish**.</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="f34d2-144">![비행 기록 시작](../media/jdk/azul-jfr-3.png)</span><span class="sxs-lookup"><span data-stu-id="f34d2-144">![Start a Flight Recording](../media/jdk/azul-jfr-3.png)</span></span>

9.  <span data-ttu-id="f34d2-145">비행 기록 덤프</span><span class="sxs-lookup"><span data-stu-id="f34d2-145">Dump the Flight Recording</span></span>
    1.  <span data-ttu-id="f34d2-146">JVM Browser의 Flight Recorder 줄 아래에 비행 기록이 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-146">A Flight Recording should appear below the Flight Recorder line in the JVM Browser.</span></span> <span data-ttu-id="f34d2-147">비행 기록을 나타내는 줄을 마우스 오른쪽 단추로 클릭하고 **전체 기록 덤프**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-147">Right-click on the line representing the Flight Recording and select **Dump whole recording**.</span></span>
    2.  <span data-ttu-id="f34d2-148">Zulu Mission Control 창 오른쪽의 큰 창에 새 탭이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-148">A new tab will appear in the large pane on the right side of the Zulu Mission Control window.</span></span> <span data-ttu-id="f34d2-149">이 창은 애플리케이션을 실행 중인 JVM에서 방금 덤프한 비행 기록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-149">This pane represents the Flight Recording just dumped from the JVM running your application.</span></span>

10. <span data-ttu-id="f34d2-150">Zulu Mission Control을 사용하여 비행 기록 검토</span><span class="sxs-lookup"><span data-stu-id="f34d2-150">Examine the Flight Recording using Zulu Mission Control</span></span>
    1.  <span data-ttu-id="f34d2-151">아직 활성화되지 않은 경우 Zulu Mission Control 창의 왼쪽 창에서 **개요**라는 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-151">If not already activated, select the tab labelled **Outline** in the left pane of the Zulu Mission Control Window.</span></span> <span data-ttu-id="f34d2-152">이 탭은 비행 기록에 수집된 데이터의 다양한 보기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-152">This tab contains different views of the data collected in the Flight Recording.</span></span>
 
    > [!div class="mx-imgBorder"]
    <span data-ttu-id="f34d2-153">![비행 기록 검토](../media/jdk/azul-jfr-4.png)</span><span class="sxs-lookup"><span data-stu-id="f34d2-153">![Review the Fliight Recording](../media/jdk/azul-jfr-4.png)</span></span>

## <a name="resources"></a><span data-ttu-id="f34d2-154">리소스</span><span class="sxs-lookup"><span data-stu-id="f34d2-154">Resources</span></span>

<span data-ttu-id="f34d2-155">Azul Systems 기술 부책임자(Deputy CTO) Simon Ritter가 낭송한 [데모 동영상](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/)도 준비했습니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-155">We have also prepared a [demonstration video](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) narrated by Azul Systems Deputy CTO Simon Ritter.</span></span> <span data-ttu-id="f34d2-156">이 동영상은 Flight Recorder 및 Zulu Mission Control의 구성 및 설정을 단계별로 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-156">The video walks you through the configuration and setup of both Flight Recorder and Zulu Mission Control.</span></span> <span data-ttu-id="f34d2-157">Flight Recorder 토론은 31분 30초 부분에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f34d2-157">The Flight Recorder discussion starts at 31:30.</span></span>

