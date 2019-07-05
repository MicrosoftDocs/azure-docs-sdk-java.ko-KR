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
# <a name="use-java-flight-recorder-and-mission-control"></a>Java Flight Recorder 및 Mission Control 사용

Zulu Mission Control은 2018년 Oracle이 오픈 소스로 공개하고 OpenJDK 보호 대상 프로젝트로 관리되는 JDK Mission Control의 완전히 테스트된 빌드입니다. Java Flight Recorder(JFR)와 결합할 경우 Mission Control은 오버헤드가 낮고 대화형으로 모니터링하는 Java 워크로드 관리 기능을 제공합니다.

Zulu 미션 컨트롤은 다음 Java Development Kit(JDK) 및 Java 런타임 환경(JRE)과 호환됩니다.

* Zulu 12.1 이상
* Zulu 11.0 이상
* Zulu 8u202(8.36) 이상
* Oracle OpenJDK 11 및 15 이상
* Oracle Java 11.0 이상
* Oracle Java 8.0 이상

## <a name="install-zulu-mission-control-and-connect-to-a-jvm"></a>Zulu 미션 컨트롤을 설치하고 JVM에 연결

Zulu Mission Control을 설치하고 JVM(Java Virtual Machine)에 연결하고 실행 중인 애플리케이션의 모든 특성을 실시간으로 파악하려면 아래를 수행합니다.

1.  [Zulu Mission Control 호환 JDK 및 JRE를 설치합니다](java-jdk-install.md).

1.  [Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/)을 다운로드하고 시스템에 맞는 버전을 선택하고 로컬로 저장한 후, 해당 디렉터리로 변경합니다.

1.  다운로드한 파일을 확장합니다.

    **Linux:**

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    **Windows:**

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    **macOS:**

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

1.  호환되는 JDK 중 하나를 사용하여 Java 애플리케이션을 시작합니다. 예:

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

1.  Zulu Mission Control을 시작합니다.

    **Linux:**

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    **Windows:**

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    **macOS:**

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

1.  (선택 사항) Mission Control에 대한 JVM 설치를 전환합니다.

    Windows 디바이스에서 *zmc.exe*는 레지스트리에 구성된 기본 JVM 설치를 사용합니다. Zulu Mission Control은 전체 JDK에서 시작해야 로컬 JVM 인스턴스를 자동으로 검색할 수 있습니다. JRE가 설치된 경우 JVM은 검색되지 않으며 다음 경고를 받게 됩니다.

    > [!div class="mx-imgBorder"]
    ![JDK 설치가 JRE 전용인 경우 경고](../media/jdk/azul-jfr-1.png)

    Mission Control에서 사용하는 JVM을 변경하려면 아래 단계를 수행합니다. 

    a. *zmc.exe* 파일과 같은 디렉터리에 있는 *zmc.ini* 구성 파일을 엽니다.

    b. `-vmargs` 줄 앞에 다음 두 줄을 추가합니다.  

       * 첫 번째 줄에서 `–vm`을 입력합니다.  
       * 두 번째 줄에서 JDK 설치 경로(예: `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`)를 씁니다.

1.  다음을 수행하여 애플리케이션을 실행 중인 JVM을 찾습니다.

    a. Zulu Mission Control 창의 왼쪽 창에서 **JVM 브라우저** 탭을 선택합니다.

    b. 목록에서 애플리케이션을 실행 중인 JVM 인스턴스를 선택하고 확장합니다.

    ![확장된 목록의 JVM 인스턴스](../media/jdk/azul-jfr-2.png)


1.  필요한 경우 플라이트 레코딩을 시작합니다.

    a. 왼쪽 창에서 **플라이트 레코드** 아래 *기록 없음* 메시지가 표시되면 **플라이트 레코더**를 마우스 오른쪽 단추로 클릭한 다음 **플라이트 레코딩 시작**을 선택하여 레코딩을 시작합니다.

    b. **고정 시간 기록** 또는 **연속 기록** 중 하나를 선택하고  **프로파일링** 구성(세분화된) 또는 **연속** 구성(낮은 오버헤드)를 선택한 다음 **마침**을 선택합니다.

    ![플라이트 기록 시작](../media/jdk/azul-jfr-3.png)

    JVM Browser의 **Flight Recorder** 줄 아래에 비행 기록이 나타나야 합니다.

1. 플라이트 기록을 덤프합니다. 플라이트 기록을 나타내는 줄을 마우스 오른쪽 단추로 클릭하고 **전체 기록 덤프**를 선택합니다.

    Zulu Mission Control 창 오른쪽의 큰 창에 새 탭이 나타납니다. 이 창은 애플리케이션을 실행 중인 JVM에서 방금 덤프한 플라이트 기록을 표시합니다.

1. Zulu Mission Control을 사용하여 플라이트 기록을 검토합니다. Zulu Mission Control 창의 왼쪽 창에서 **개요** 탭을 선택합니다. 이 탭은 플라이트 기록에 수집된 데이터의 다양한 보기를 표시합니다.
 
    ![플라이트 기록 검토](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a>리소스

자세한 내용은 Azul Systems 사이트로 이동하여[Azul 웨비나를 봅니다. 원본 플라이트 레코더 및 Mission Control - OpenJDK 8 성능 관리 및 측정](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/)을 엽니다. 비디오는 Simon Ritter(Azul Systems Deputy CTO)의 음성 프레젠테이션으로 소개됩니다. Flight Recorder 토론은 31분 30초 부분에서 시작합니다.

