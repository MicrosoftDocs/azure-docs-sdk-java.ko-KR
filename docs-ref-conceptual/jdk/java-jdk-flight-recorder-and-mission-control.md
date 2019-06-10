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
# <a name="using-java-flight-recorder-jfr-and-mission-control"></a>JFR(Java Flight Recorder) 및 Mission Control 사용

Zulu Mission Control은 2018년 Oracle이 오픈 소스로 공개하고 OpenJDK 보호 대상 프로젝트로 관리되는 JDK Mission Control의 완전히 테스트된 빌드입니다. Flight Recorder와 결합할 경우 Mission Control은 오버헤드가 낮고 대화형으로 모니터링하는 Java 워크로드 관리 기능을 제공합니다.

Zulu Mission Control은 다음과 같은 JDK/JRE와 호환됩니다.

* Zulu 12.1 이상
* Zulu 11.0 이상
* Zulu 8u202(8.36) 이상
* Oracle OpenJDK 11+15 이상
* Oracle Java 11.0 이상
* Oracle Java 8.0 이상

아래 단계에 따라 Zulu Mission Control을 설치하고 JVM(Java Virtual Machine)에 연결하고 실행 중인 애플리케이션의 모든 특성을 실시간으로 파악합니다.

1.  [Zulu Mission Control 호환 JDK/JRE를 설치합니다](java-jdk-install.md).

2.  [Azul 다운로드 사이트](https://www.azul.com/products/zulu-mission-control/)에서 Zulu Mission Control을 다운로드하고 시스템에 맞는 버전을 선택하고 로컬로 저장한 후, 해당 디렉터리로 변경합니다.

3.  다운로드한 파일을 확장합니다.

    **Linux:**

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    **Windows:**

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    **MacOS:**

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

4.  호환되는 JDK 중 하나를 사용하여 Java 애플리케이션을 시작합니다. 예:

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

5.  Zulu Mission Control 시작

    **Linux:**

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    **Windows:**

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    **MacOS:**

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

6.  Mission Control에 대한 JVM 설치 전환(선택 사항)

    Windows에서 *zmc.exe*는 레지스트리에 구성된 기본 JVM 설치를 사용합니다. Zulu Mission Control은 전체 JDK에서 시작해야 로컬 JVM 인스턴스를 자동으로 검색할 수 있습니다. JRE의 경우 아래 경고가 표시됩니다.

    > [!div class="mx-imgBorder"]
    ![JDK 설치가 JRE 전용인 경우 경고](../media/jdk/azul-jfr-1.png)

    Mission Control에서 사용하는 JVM을 변경하려면 아래 단계를 따릅니다. 
    1.  *zmc.exe*와 같은 디렉터리에 있는 *zmc.ini* 구성 파일을 엽니다.
    2.  `-vmargs` 줄 앞에 다음 두 줄을 추가합니다.
        * 첫 번째 줄에서 `–vm`를 씁니다.
        * 두 번째 줄에서 JDK 설치 경로를 씁니다. (예, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).

7.  애플리케이션을 실행 중인 JVM을 찾습니다.
    1.  Zulu Mission Control 창의 왼쪽 위 창에서 **JVM Browser**라는 탭을 클릭합니다.
    2.  애플리케이션을 실행 중인 JVM 인스턴스에 대해 왼쪽 위의 목록 항목을 선택하고 확장합니다.

    > [!div class="mx-imgBorder"]
    ![JVM 인스턴스에 대한 왼쪽 위의 목록 항목을 확장합니다.](../media/jdk/azul-jfr-2.png)


8.  필요한 경우 비행 기록을 시작합니다.
    1.  Flight Recorder에 "기록 없음"이 표시된 경우 JVM Browser 탭의 Flight Recorder 줄을 마우스 오른쪽 단추로 클릭하고 **비행 기록 시작...** 을 선택하여 기록을 시작합니다.
    2.  고정 기간 기록 또는 연속 기록 및 구성 프로파일링(세분화된) 또는 연속 구성(낮은 오버헤드)을 선택한 다음, **마침**을 클릭합니다.

    > [!div class="mx-imgBorder"]
    ![비행 기록 시작](../media/jdk/azul-jfr-3.png)

9.  비행 기록 덤프
    1.  JVM Browser의 Flight Recorder 줄 아래에 비행 기록이 나타나야 합니다. 비행 기록을 나타내는 줄을 마우스 오른쪽 단추로 클릭하고 **전체 기록 덤프**를 선택합니다.
    2.  Zulu Mission Control 창 오른쪽의 큰 창에 새 탭이 나타납니다. 이 창은 애플리케이션을 실행 중인 JVM에서 방금 덤프한 비행 기록을 표시합니다.

10. Zulu Mission Control을 사용하여 비행 기록 검토
    1.  아직 활성화되지 않은 경우 Zulu Mission Control 창의 왼쪽 창에서 **개요**라는 탭을 선택합니다. 이 탭은 비행 기록에 수집된 데이터의 다양한 보기를 포함합니다.
 
    > [!div class="mx-imgBorder"]
    ![비행 기록 검토](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a>리소스

Azul Systems 기술 부책임자(Deputy CTO) Simon Ritter가 낭송한 [데모 동영상](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/)도 준비했습니다. 이 동영상은 Flight Recorder 및 Zulu Mission Control의 구성 및 설정을 단계별로 보여줍니다. Flight Recorder 토론은 31분 30초 부분에서 시작합니다.

