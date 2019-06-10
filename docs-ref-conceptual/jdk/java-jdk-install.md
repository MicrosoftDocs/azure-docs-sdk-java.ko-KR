---
title: Azure 및 Azure Stack용 Azul Zulu JDK 설치
description: Windows, Linux 및 Mac을 사용하여 Azure 개발용 Azul Zulu JDK(Java Development Kit)를 설치하는 방법
author: erickson-doug
manager: douge
ms.author: douge
ms.date: 4/19/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: 33d2206f9a0a1cc9fadc60b17c1a93f66c592fe3
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2019
ms.locfileid: "64568596"
---
# <a name="install-the-jdk-for-azure-and-azure-stack"></a>Azure 및 Azure Stack용 JDK 설치

OpenJDK의 Azul Zulu Enterprise 빌드는 Microsoft와 Azul Systems가 후원하는 Azure 및 Azure Stack에 대한 OpenJDK의 무료 다중 플랫폼 프로덕션 준비 배포입니다. 여기에는 Java SE 애플리케이션을 빌드하고 실행하기 위한 모든 구성 요소가 포함됩니다.

[각 클라이언트 OS에 대해 지원되는 여러 다운로드 패키지 형식](https://www.azul.com/downloads/azure-only/zulu/)이 있습니다. Azure Marketplace 갤러리에서 다음 플랫폼에 대한 가상 머신 이미지를 가져올 수도 있습니다.

  * [Azul Zulu: Ubuntu 18.04의 Java 8](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-ubuntu-1804)
  * [Azul Zulu: Windows Server 2019의 Java 8](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-windows-2019)
  
  * [Azul Zulu: Ubuntu 18.04의 Java 11](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-ubuntu-1804)
  * [Azul Zulu: Windows Server 2019의 Java 11](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-windows-2019)


> [!NOTE]
> 이 지침은 JDK의 64비트 Java 8 버전을 대상으로 합니다. 또한 Azul은 JRE(Java Run-time Environment)를 독립 실행형 설치로 제공합니다. JRE에는 JDK 설치가 포함되어 있습니다.
>
>  Java 11 패키지는 [Azul의 Azure 다운로드 페이지](https://www.azul.com/downloads/azure-only/zulu/)에서도 제공됩니다.

## <a name="download-and-install-the-azul-zulu-jdks-for-windows"></a>Windows용 Azul Zulu JDK 다운로드 및 설치 

1. [64비트 Azul Zulu JDK 8을 MSI로](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi) 클라이언트의 위치에 설치합니다. 예: `C:\Users\<your_login>\Downloads`. (.ZIP 패키지는 [Azul의 Azure 다운로드 페이지](https://www.azul.com/downloads/azure-only/zulu/)에서도 제공됩니다.)

2. 설치를 시작하려면 해당 디렉터리로 이동한 후 다운로드한 MSI 파일을 두 번 클릭합니다.

## <a name="download-and-install-the-azul-zulu-jdks-for-mac"></a>Mac용 Azul Zulu JDK 다운로드 및 설치 

다음 단계에서는 ZIP 파일을 Mac에 다운로드합니다. DMG 버전을 사용할 수도 있습니다.

1. [64비트 Azul Zulu JDK 8을 ZIP 파일로](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip) 클라이언트의 위치에 다운로드합니다. 예: `/Library/Java/JavaVirtualMachines/`. (.DMG 패키지는 [Azul의 Azure 다운로드 페이지](https://www.azul.com/downloads/azure-only/zulu/)에서도 제공됩니다.)

2. 파인더를 시작하고 다운로드 디렉터리로 이동한 다음, ZIP 파일을 두 번 클릭합니다. 또는 터미널 명령 창을 시작하고 디렉터리로 이동한 후 다음을 실행할 수 있습니다.

```cli
unzip <name_of_zulu_package>.zip
```

## <a name="download-and-install-the-azul-zulu-jdks-for-alpine-linux"></a>Alpine Linux용 Azul Zulu JDK 다운로드 및 설치

1. [64비트 Azul Zulu JDK 8을 TAR 파일로](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz) 클라이언트의 위치에 다운로드합니다. 예: `/usr/lib/jvm`. (.RPM 및 .DEB 패키지는 [Azul의 Azure 다운로드 페이지](https://www.azul.com/downloads/azure-only/zulu/)에서도 제공됩니다.)

2. 디렉터리로 이동하고 다음 명령을 실행하여 파일의 압축을 풀고 확장합니다.

    ```cli
    tar -xvf <name_of_zulu_package>.tar
    ```

## <a name="confirm-your-installation"></a>설치 확인

설치를 확인하려면 명령줄로 이동하고 `java -version`를 실행합니다.

명령의 출력은 다음과 같아야 합니다.

```cli
$ java -version

openjdk version "1.8.0_212"
OpenJDK Runtime Environment (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 1.8.0_212-b04)
OpenJDK 64-Bit Server VM (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 25.212-b04, mixed mode)

```

## <a name="download-and-install-the-azul-zulu-jdks-from-a-yum-repository"></a>Yum 리포지토리에서 Azul Zulu JDK 다운로드 및 설치

Azul Zulu JDK는 Azul에 의해 [Yum 리포지토리](http://repos.azul.com/azure-only/zulu-azure.repo)에서 제공됩니다.

**Java 8용 Azul Zulu JDK를 설치하려면 CLI에서 다음 명령을 실행합니다.**

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-8-azure-jdk
```

Java 11의 경우 다음을 실행합니다.

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-11-azure-jdk
```

Java 12(미리 보기)의 경우 다음을 실행합니다.

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-12-azure-jdk
```

**Yum 리포지토리에서 Zulu JDK 8 패키지를 업데이트하려면 다음을 수행합니다.**

```cli
sudo yum -q -y install zulu-8-azure-jdk
```

(버전 11 또는 12를 사용하는 경우 위의 명령에서 버전 번호를 변경하세요.)

**Yum 리포지토리에서 Zulu JDK 8 패키지를 제거하려면 다음을 수행합니다.**

```cli
sudo yum -y erase zulu-8-azure-jdk
```
(버전 11 또는 12를 사용하는 경우 위의 명령에서 버전 번호를 변경하세요.)

## <a name="download-and-install-the-azul-zulu-jdks-from-an-apt-get-repository"></a>apt-get 리포지토리에서 Azul Zulu JDK 다운로드 및 설치

Azul Zulu JDK는 Azul에 의해 [apt-get 리포지토리](http://repos.azul.com/azure-only/zulu/apt)에서도 제공됩니다.

**apt-get를 사용하여 Java 8용 Azul Zulu JDK를 설치하려면 CLI에서 다음 명령을 실행합니다.**

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

Java 11의 경우 다음을 실행합니다.

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-11-azure-jdk
```

Java 12(미리 보기)의 경우 다음을 실행합니다.

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-12-azure-jdk
```

**apt-get 리포지토리에서 Zulu JDK 8 패키지를 업데이트하려면 다음을 수행합니다.**

```cli
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

이전 릴리스는 자동으로 제거됩니다.
(버전 11 또는 12를 사용하는 경우 위의 명령에서 버전 번호를 변경하세요.)

**apt-get 리포지토리에서 Zulu JDK 8 패키지를 제거하려면 다음을 수행합니다.**

```cli
sudo apt-get -y purge zulu-8-azure-jdk
```

(버전 11 또는 12를 사용하는 경우 위의 명령에서 버전 번호를 변경하세요.)

Azure 개발용 Azul Zulu JDK 준비, 설치 및 관리에 대한 자세한 내용은 [공식 Zulu 문서](https://docs.azul.com/zulu/zuludocs/index.htm)를 읽으세요.

