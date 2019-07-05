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
# <a name="java-long-term-support-for-azure-and-azure-stack"></a>Azure 및 Azure Stack에 대한 Java 장기 지원

Microsoft Azure 및 Azure Stack의 Java 개발자는 추가 지원 비용 없이 [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/)를 사용하여 프로덕션 Java 애플리케이션을 빌드하고 실행할 수 있습니다. Azure에서 원하는 모든 Java 런타임을 사용할 수 있지만 Zulu를 사용하는 경우 무료 유지 관리 업데이트를 얻고 Microsoft와 지원 문제를 해결할 수 있습니다.

> [!div class="nextstepaction"]
> [Java 다운로드 및 설치](java-jdk-install.md)

## <a name="long-term-support"></a>장기 지원

* [Java 11](https://www.azul.com/downloads/azure-only/zulu/#java11)
* [Java 8](https://www.azul.com/downloads/azure-only/zulu/#java8)
* [Java 7](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a>기술 미리 보기

* [Java 12](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a>Azure용 Zulu OpenJDK란 무엇인가요?

OpenJDK의 Azul Zulu Enterprise 빌드는 Microsoft와 Azul Systems가 후원하는 Azure 및 Azure Stack에 대한 OpenJDK의 무료 다중 플랫폼 프로덕션 준비 배포입니다. 해당 배포는 다음과 같습니다.

* JDK(Java Development Kit), JRE(Java Runtime Environment) 및 Headless JRE로 패키지된 OpenJDK의 100% 오픈 소스 빌드. 이 이진 파일은 Java 애플리케이션 또는 Azure 및 Azure Stack의 구성 요소와 함께 사용할 수 있는 Java SE(Standard Edition)의 완전히 호환되고 상용으로 적합한 빌드입니다.
* 버그 수정, 성능 향상 및 보안 패치를 포함한 장기 지원(LTS)과 함께 제공됩니다.
* Windows, Linux 및 MacOS에서 Java 애플리케이션을 개발하고 실행하는 데 사용할 수 있습니다.
* Docker Hub의 컨테이너 이미지 및 Azure Marketplace의 가상 머신(Windows 및 Linux)으로 사용할 수 있습니다.
* Azure에서 다음과 같은 많은 Azure 서비스를 지원하기 위해 사용합니다.
  * Azure App Service(Windows)
  * Azure App Service(Linux)
  * Azure 기능
  * Azure Service Fabric
  * Azure HDInsight
  * Azure Search
  * Azure DevOps
  * Azure Cloud Shell  

## <a name="supported-java-versions-and-update-schedule"></a>지원되는 Java 버전 및 업데이트 일정

Azul Systems는 Java SE 7, 8 및 11부터 Java의 모든 LTS 버전에 대해 완벽하게 지원되는 [Azure용 OpenJDK의 Zulu Enterprise 빌드](https://www.azul.com/downloads/azure-only/zulu/)를 제공합니다. 자세한 내용은 [Azul 보도 자료](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack)를 참조하세요.

|Java SE LTS  |지원 기한  |
|---------|----------|
|[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7) |2023년 7월 |
|[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8) |2025년 3월|
|[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11) |2026년 9월|
|[![Java 12](../media/jdk/java-12.png)]() |**미리 보기**|

위의 JDK 버전에는 분기별 보안 업데이트, 버그 수정, 그리고 필요한 경우 중요 대역 외 업데이트 및 패치가 포함됩니다. 이 지원에는 Java 11과 같은 최신 버전의 Java에서 보고되는 보안 업데이트의 백 포트 및 Java 7 및 8에 대한 버그 수정이 포함됩니다. 이 지원은 Java 이전 버전의 지속적인 안정성과 보안을 보장하기 위한 것입니다. Azure 고객은 계획되지 않은 모든 Java SE 구독 요금이 발생하지 않고 이러한 보안 업데이트 및 플랫폼 버그 수정을 가져올 수 있습니다.

Azul Systems는 이러한 릴리스에 대한 [Java SE 로드맵](https://www.azul.com/products/azul_support_roadmap/)을 유지 관리합니다.

## <a name="benefits-for-developers"></a>개발자에 대한 혜택

Azul Zulu JDK 릴리스는 다음과 같습니다.

* Microsoft와 Azul Systems에서 모두 후원 및 지원.

   * Zulu 이진 파일은 프로덕션 준비 상태이며 Microsoft 및 Azul Systems에서 후원.
   * Zulu는 Java 7, 8 및 11에 대한 비용이 없는 LTS와 함께 제공됩니다(LTS는 Java 17에도 제공됩니다). Java 버전은 필요한 경우에만 업그레이드할 수 있습니다.
   * Java 7은 2023년 7월까지 지원됩니다. Java 8 및 11은 2024년 이후에도 지원됩니다.
   * Microsoft는 많은 Azure 서비스 기반 머신에서 내부적으로 Zulu 실행을 약속했습니다.

* 프로덕션 준비.

   * OpenJDK의 해당 빌드에 대한 100% 오픈 소스.
   * 많은 Java SE 배포에 대한 드롭인 교체.
   * JDK, JRE 및 JRE 헤드리스.
   * Java 7, 8 및 11.
   * OpenJDK Community TCK(Technology Compatibility Kit)를 사용하여 Java SE 사양에 적합한 것으로 확인되었습니다.
   * 개발자는 Java SE 7, 8 및 11에 대한 버그 수정, 성능 향상 및 보안 패치를 포함하여 Java SE에 대한 프로덕션 업데이트를 계속 받습니다.

* 다중 플랫폼 지원. Zulu는 다음을 포함한 여러 플랫폼 및 버전에 대한 이진 파일을 지원합니다.

   * Windows 클라이언트
     * 10
     * 8.1
     * 8, 7
   * Windows Server
     * 2016 R2
     * 2016
     * 2012 R2
     * 2012
     * 2008 R2
   * 다음을 포함한 Linux
     * RHEL
     * CentOS
     * Ubuntu
     * SLES
     * Debian
     * Oracle Linux
   * macOS X
   * 여러 패키지 형식으로 제공됩니다.
     * MSI, ZIP, TAR, DEB, RPM 및 DMG

    여러 기본 OS 이미지의 Zulu JDK, JRE 및 JRE 헤드리스에 대해 인증된 Docker 컨테이너 이미지를 Docker에서 사용할 수 있습니다.

    허브:

    * [JDK](https://hub.docker.com/_/microsoft-java-jdk)
    * [JRE](https://hub.docker.com/_/microsoft-java-jre)
    * [JRE 헤드리스](https://hub.docker.com/_/microsoft-java-jre-headless)

* 무료입니다.

   * Microsoft는 Azure에서 Java 앱을 빌드하고 확장하는 데 필요한 모든 것을 무료로 제공합니다. 즉, Zulu를 통해 Java 앱에 대한 무료 보안 업데이트 및 플랫폼 버그 수정을 수수료 없이 받게 됩니다.
   * [Java Flight Recorder 및 Mission Control](java-jdk-flight-recorder-and-mission-control.md)은 Zulu Java 8, 11 및 12(미리 보기)에서 사용할 수 있습니다.

* LTS 이외 버전의 기술 미리 보기로 사용 가능합니다.

   * 기술 미리 보기를 통해, 결국 Java 17 LTS로 종료될 단기 버전에 제공될 때 새 기능을 점진적으로 테스트할 수 있습니다.

* OpenJDK 변경이 업스트림 전송됩니다.

   * Azul Systems 커미터는 Zulu 변경 내용을 OpenJDK에 푸시하여 업스트림 리포지토리를 포괄적이고 모든 것이 포함되도록 만듭니다.

항상 Java 개발자는 Azure로 Oracle JDK 및 Red Hat JDK를 포함하여 사용자 고유의 Java 런타임을 가져올 수 있습니다. 또한 보안 인프라와 풍부한 기능을 갖춘 서비스를 사용할 수 있습니다. 또한 Oracle Java SE의 프로덕션 버전을 사용하여 Azure의 Windows 또는 Linux 가상 머신에서 Java 워크로드를 실행할 수도 있습니다.

## <a name="use-java-jdks-for-local-development"></a>로컬 개발을 위해 Java JDK 사용 

로컬 개발 환경에서 사용하기 위해 [Azure 및 Azure Stack용 Java JDK를 다운로드](https://www.azul.com/downloads/azure-only/zulu/)할 수 있습니다. Windows, Linux 및 macOS에서 다운로드가 지원됩니다. Linux에서 작업하는 경우, [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) 및 [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) 패키지 관리자를 통해 패키지를 가져올 수도 있습니다.

추가 지침은 [Azure용 Docker 이미지](java-jdk-docker-images.md)를 참조하세요.
