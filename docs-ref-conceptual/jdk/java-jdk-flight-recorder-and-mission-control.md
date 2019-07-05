---
title: Java Flight Recorder 및 Mission Control
description: Java Flight Recorder 및 Mission Control을 사용하여 앱 데이터를 수집하고 검토하기 위한 지침입니다.
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: 64f64f2e5891fccf9d62510f39bd99d73457d590
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533628"
---
# <a name="use-java-flight-recorder-and-mission-control"></a><span data-ttu-id="e8595-103">Java Flight Recorder 및 Mission Control 사용</span><span class="sxs-lookup"><span data-stu-id="e8595-103">Use Java Flight Recorder and Mission Control</span></span>

<span data-ttu-id="e8595-104">Zulu Mission Control은 2018년 Oracle이 오픈 소스로 공개하고 OpenJDK 보호 대상 프로젝트로 관리되는 JDK Mission Control의 완전히 테스트된 빌드입니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-104">Zulu Mission Control is a fully-tested build of JDK Mission Control, which was open-sourced by Oracle in 2018 and is managed as a project under the OpenJDK umbrella.</span></span> <span data-ttu-id="e8595-105">Java Flight Recorder(JFR)와 결합할 경우 Mission Control은 오버헤드가 낮고 대화형으로 모니터링하는 Java 워크로드 관리 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-105">Coupled with Java Flight Recorder (JFR), Mission Control delivers low-overhead, interactive monitoring and management capabilities for Java workloads.</span></span>

<span data-ttu-id="e8595-106">Zulu 미션 컨트롤은 다음 Java Development Kit(JDK) 및 Java 런타임 환경(JRE)과 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-106">Zulu Mission Control is compatible with the following Java Development Kits (JDKs) and Java Runtime Environments (JREs):</span></span>

* <span data-ttu-id="e8595-107">Zulu 12.1 이상</span><span class="sxs-lookup"><span data-stu-id="e8595-107">Zulu 12.1 and later</span></span>
* <span data-ttu-id="e8595-108">Zulu 11.0 이상</span><span class="sxs-lookup"><span data-stu-id="e8595-108">Zulu 11.0 and later</span></span>
* <span data-ttu-id="e8595-109">Zulu 8u202(8.36) 이상</span><span class="sxs-lookup"><span data-stu-id="e8595-109">Zulu 8u202 (8.36) and later</span></span>
* <span data-ttu-id="e8595-110">Oracle OpenJDK 11 및 15 이상</span><span class="sxs-lookup"><span data-stu-id="e8595-110">Oracle OpenJDK 11 and 15 and later</span></span>
* <span data-ttu-id="e8595-111">Oracle Java 11.0 이상</span><span class="sxs-lookup"><span data-stu-id="e8595-111">Oracle Java 11.0 and later</span></span>
* <span data-ttu-id="e8595-112">Oracle Java 8.0 이상</span><span class="sxs-lookup"><span data-stu-id="e8595-112">Oracle Java 8.0 and later</span></span>

## <a name="install-zulu-mission-control-and-connect-to-a-jvm"></a><span data-ttu-id="e8595-113">Zulu 미션 컨트롤을 설치하고 JVM에 연결</span><span class="sxs-lookup"><span data-stu-id="e8595-113">Install Zulu Mission Control and connect to a JVM</span></span>

<span data-ttu-id="e8595-114">Zulu Mission Control을 설치하고 JVM(Java Virtual Machine)에 연결하고 실행 중인 애플리케이션의 모든 특성을 실시간으로 파악하려면 아래를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-114">To install Zulu Mission Control, connect to a Java Virtual Machine (JVM), and gain real-time visibility into all aspects of a running application, do the following:</span></span>

1.  <span data-ttu-id="e8595-115">[Zulu Mission Control 호환 JDK 및 JRE를 설치합니다](java-jdk-install.md).</span><span class="sxs-lookup"><span data-stu-id="e8595-115">[Install a Zulu Mission Control-compatible JDK and JRE](java-jdk-install.md).</span></span>

1.  <span data-ttu-id="e8595-116">[Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/)을 다운로드하고 시스템에 맞는 버전을 선택하고 로컬로 저장한 후, 해당 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-116">[Download Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/), choose the appropriate version for your system, save it locally, and change to that directory.</span></span>

1.  <span data-ttu-id="e8595-117">다운로드한 파일을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-117">Expand the downloaded file.</span></span>

    <span data-ttu-id="e8595-118">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="e8595-118">**Linux:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    <span data-ttu-id="e8595-119">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="e8595-119">**Windows:**</span></span>

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    <span data-ttu-id="e8595-120">**macOS:**</span><span class="sxs-lookup"><span data-stu-id="e8595-120">**macOS:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

1.  <span data-ttu-id="e8595-121">호환되는 JDK 중 하나를 사용하여 Java 애플리케이션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-121">Start your Java application by using one of the compatible JDKs.</span></span> <span data-ttu-id="e8595-122">예:</span><span class="sxs-lookup"><span data-stu-id="e8595-122">For example:</span></span>

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

1.  <span data-ttu-id="e8595-123">Zulu Mission Control을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-123">Start Zulu Mission Control.</span></span>

    <span data-ttu-id="e8595-124">**Linux:**</span><span class="sxs-lookup"><span data-stu-id="e8595-124">**Linux:**</span></span>

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    <span data-ttu-id="e8595-125">**Windows:**</span><span class="sxs-lookup"><span data-stu-id="e8595-125">**Windows:**</span></span>

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    <span data-ttu-id="e8595-126">**macOS:**</span><span class="sxs-lookup"><span data-stu-id="e8595-126">**macOS:**</span></span>

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

1.  <span data-ttu-id="e8595-127">(선택 사항) Mission Control에 대한 JVM 설치를 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-127">(Optional) Switch the JVM installation for Mission Control.</span></span>

    <span data-ttu-id="e8595-128">Windows 디바이스에서 *zmc.exe*는 레지스트리에 구성된 기본 JVM 설치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-128">On Windows devices, *zmc.exe* uses the default JVM installation that's configured in the registry.</span></span> <span data-ttu-id="e8595-129">Zulu Mission Control은 전체 JDK에서 시작해야 로컬 JVM 인스턴스를 자동으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-129">Zulu Mission Control must be launched from a full JDK to be able to detect local JVM instances automatically.</span></span> <span data-ttu-id="e8595-130">JRE가 설치된 경우 JVM은 검색되지 않으며 다음 경고를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-130">If the installation is a JRE, no JVM will be detected, and you will receive the following warning:</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="e8595-131">![JDK 설치가 JRE 전용인 경우 경고](../media/jdk/azul-jfr-1.png)</span><span class="sxs-lookup"><span data-stu-id="e8595-131">![Warning if JDK installation is JRE-only](../media/jdk/azul-jfr-1.png)</span></span>

    <span data-ttu-id="e8595-132">Mission Control에서 사용하는 JVM을 변경하려면 아래 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-132">To change the JVM that's used by Mission Control, do the following:</span></span> 

    <span data-ttu-id="e8595-133">a.</span><span class="sxs-lookup"><span data-stu-id="e8595-133">a.</span></span> <span data-ttu-id="e8595-134">*zmc.exe* 파일과 같은 디렉터리에 있는 *zmc.ini* 구성 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-134">Open the *zmc.ini* configuration file, which is in the same directory as the *zmc.exe* file.</span></span>

    <span data-ttu-id="e8595-135">b.</span><span class="sxs-lookup"><span data-stu-id="e8595-135">b.</span></span> <span data-ttu-id="e8595-136">`-vmargs` 줄 앞에 다음 두 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-136">Before the line `-vmargs`, add two lines:</span></span>  

       * <span data-ttu-id="e8595-137">첫 번째 줄에서 `–vm`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-137">On the first line, enter `–vm`.</span></span>  
       * <span data-ttu-id="e8595-138">두 번째 줄에서 JDK 설치 경로(예: `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`)를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-138">On the second line, enter the path to your JDK installation (for example, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span></span>

1.  <span data-ttu-id="e8595-139">다음을 수행하여 애플리케이션을 실행 중인 JVM을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-139">Locate the JVM that's running your application by doing the following:</span></span>

    <span data-ttu-id="e8595-140">a.</span><span class="sxs-lookup"><span data-stu-id="e8595-140">a.</span></span> <span data-ttu-id="e8595-141">Zulu Mission Control 창의 왼쪽 창에서 **JVM 브라우저** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-141">In the left pane of the Zulu Mission Control window, select the **JVM Browser** tab.</span></span>

    <span data-ttu-id="e8595-142">b.</span><span class="sxs-lookup"><span data-stu-id="e8595-142">b.</span></span> <span data-ttu-id="e8595-143">목록에서 애플리케이션을 실행 중인 JVM 인스턴스를 선택하고 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-143">In the list, select and expand the JVM instance that's running your application.</span></span>

    ![확장된 목록의 JVM 인스턴스](../media/jdk/azul-jfr-2.png)


1.  <span data-ttu-id="e8595-145">필요한 경우 플라이트 레코딩을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-145">Start a flight recording, if necessary.</span></span>

    <span data-ttu-id="e8595-146">a.</span><span class="sxs-lookup"><span data-stu-id="e8595-146">a.</span></span> <span data-ttu-id="e8595-147">왼쪽 창에서 **플라이트 레코드** 아래 *기록 없음* 메시지가 표시되면 **플라이트 레코더**를 마우스 오른쪽 단추로 클릭한 다음 **플라이트 레코딩 시작**을 선택하여 레코딩을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-147">In the left pane, under **Flight Recorder**, if a *No Recordings* message is displayed, start a recording by right-clicking **Flight Recorder** and then selecting **Start Flight Recording**.</span></span>

    <span data-ttu-id="e8595-148">b.</span><span class="sxs-lookup"><span data-stu-id="e8595-148">b.</span></span> <span data-ttu-id="e8595-149">**고정 시간 기록** 또는 **연속 기록** 중 하나를 선택하고  **프로파일링** 구성(세분화된) 또는 **연속** 구성(낮은 오버헤드)를 선택한 다음 **마침**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-149">Select either **Time fixed recording** or **Continuous recording**, and either a **Profiling** configuration (fine-grained) or a **Continuous** configuration (lower overhead), and then select **Finish**.</span></span>

    ![플라이트 기록 시작](../media/jdk/azul-jfr-3.png)

    <span data-ttu-id="e8595-151">JVM Browser의 **Flight Recorder** 줄 아래에 비행 기록이 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-151">A flight recording should appear below the **Flight Recorder** line in the JVM browser.</span></span>

1. <span data-ttu-id="e8595-152">플라이트 기록을 덤프합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-152">Dump the flight recording.</span></span> <span data-ttu-id="e8595-153">플라이트 기록을 나타내는 줄을 마우스 오른쪽 단추로 클릭하고 **전체 기록 덤프**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-153">To do so, right-click the line that represents the flight recording, and then select **Dump whole recording**.</span></span>

    <span data-ttu-id="e8595-154">Zulu Mission Control 창 오른쪽의 큰 창에 새 탭이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-154">A new tab appears in the large pane on the right side of the Zulu Mission Control window.</span></span> <span data-ttu-id="e8595-155">이 창은 애플리케이션을 실행 중인 JVM에서 방금 덤프한 플라이트 기록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-155">This pane represents the flight recording that was just dumped from the JVM that's running your application.</span></span>

1. <span data-ttu-id="e8595-156">Zulu Mission Control을 사용하여 플라이트 기록을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-156">Examine the flight recording by using Zulu Mission Control.</span></span> <span data-ttu-id="e8595-157">Zulu Mission Control 창의 왼쪽 창에서 **개요** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-157">To do so, select the **Outline** tab in the left pane of the Zulu Mission Control window.</span></span> <span data-ttu-id="e8595-158">이 탭은 플라이트 기록에 수집된 데이터의 다양한 보기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-158">This tab displays various views of the data that's collected in the flight recording.</span></span>
 
    ![플라이트 기록 검토](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a><span data-ttu-id="e8595-160">리소스</span><span class="sxs-lookup"><span data-stu-id="e8595-160">Resources</span></span>

<span data-ttu-id="e8595-161">자세한 내용은 Azul Systems 사이트로 이동하여[Azul 웨비나를 봅니다. 원본 플라이트 레코더 및 Mission Control - OpenJDK 8 성능 관리 및 측정](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-161">To learn more, go to the Azul Systems site and view [Azul Webinar: Open Source Flight Recorder and Mission Control - Managing and Measuring OpenJDK 8 Performance](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/).</span></span> <span data-ttu-id="e8595-162">비디오는 Simon Ritter(Azul Systems Deputy CTO)의 음성 프레젠테이션으로 소개됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-162">The video is narrated by Azul Systems Deputy CTO Simon Ritter.</span></span> <span data-ttu-id="e8595-163">Flight Recorder 토론은 31분 30초 부분에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e8595-163">The Flight Recorder discussion starts at 31:30.</span></span>

