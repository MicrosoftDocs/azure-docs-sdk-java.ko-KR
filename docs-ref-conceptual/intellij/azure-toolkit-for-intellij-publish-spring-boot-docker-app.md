---
title: IntelliJ용 Azure 도구 키트를 사용하여 Spring Boot 앱을 Docker 컨테이너로 게시
description: IntelliJ용 Azure 도구 키트를 사용하여 Docker 컨테이너로 Microsoft Azure에 웹앱을 게시하는 방법을 알아봅니다.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 4228352efa4354bfe4969c1a5ecd3f3b40483f85
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893584"
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>IntelliJ용 Azure 도구 키트를 사용하여 Spring Boot 앱을 Docker 컨테이너로 게시

[Spring Framework]는 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만드는 데 도움이 되는 오픈 소스 솔루션입니다. 해당 플랫폼을 기반으로 하여 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 응용 프로그램을 만드는 간단한 방법을 제공합니다.

[Docker]는 개발자가 컨테이너에서 실행되는 응용 프로그램의 배포, 크기 조정 및 관리를 자동화하는 데 도움이 되는 오픈 소스 솔루션입니다.

이 자습서에서는 IntelliJ용 Azure 도구 키트를 사용하여 Microsoft Azure에 Docker 컨테이너로 Spring Boot 응용 프로그램을 배포하는 단계를 안내합니다.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a>기본 Spring Boot Docker 리포지토리 복제

다음 단계는 IntelliJ를 사용하여 Spring Boot Docker 리포지토리를 복제하는 방법을 설명합니다. 명령줄을 사용하려면 [Azure Container Service에서 Linux에 Spring Boot 응용 프로그램 배포][Deploy Spring Boot on Linux in AKS]를 참조하세요.

1. IntelliJ를 엽니다.

1. 시작 화면의 **버전 제어에서 체크 아웃** 목록에서 **GitHub** 옵션을 선택합니다.

   ![버전 제어에 대한 GitHub 옵션][CL01]

1. 로그인하라는 메시지가 표시되면 자격 증명을 입력합니다.

   * GitHub에 로그인하는 데 사용자 이름/암호를 사용하는 경우: 

      ![GitHub 사용자 이름 및 암호를 입력하는 대화 상자][CL02a]

   * GitHub에 로그인하는 데 토큰을 사용하는 경우: 

      ![GitHub 토큰을 입력하는 대화 상자][CL02b]

1. 리포지토리 URL에 대해 **https://github.com/spring-guides/gs-spring-boot-docker.git**를 입력하고 로컬 경로 및 폴더 정보를 지정한 다음 **복제**를 클릭합니다.

   ![리포지토리 복제 대화 상자][CL03]

1. IntelliJ 프로젝트를 만들 것인지 묻는 메시지가 표시되면 **아니요**를 선택합니다.

   ![IntelliJ 프로젝트 만들지 않기][CL04]

1. 홈페이지에서 **프로젝트 가져오기**를 클릭합니다.

   ![프로젝트 가져오기 선택 영역][CL05]

1. Spring Boot 리포지토리를 복제한 경로를 찾고 루트 아래의 **완료** 폴더를 선택한 다음 **확인**을 클릭합니다.

   ![가져올 폴더 선택][CL06]

1. 메시지가 표시되면 **기존 원본에서 프로젝트 만들기**를 선택합니다.

   ![기존 원본에서 프로젝트를 만드는 옵션][CL07]

1. 프로젝트 이름을 지정하거나 기본값을 적용하고 **완료** 폴더에 올바른 경로를 확인한 후 **다음**을 클릭합니다.

   ![프로젝트 이름 지정][CL08]

1. 가져오기에 대한 모든 디렉터리를 사용자 지정한 후 **다음**을 클릭합니다.

   ![디렉터리 선택][CL09]

1. 가져올 라이브러리를 검토한 후 **다음**을 클릭합니다.

   ![프로젝트 라이브러리 검토][CL10]

1. 모듈 구조를 검토한 후 **다음**을 클릭합니다.

   ![모듈 구조 검토][CL11]

1. JDK를 지정한 후 **다음**을 클릭합니다.

   ![JDK 지정][CL12]

1. **Finish**를 클릭합니다.

   ![마침 단추][CL13]

IntelliJ는 프로젝트로 Spring Boot 앱을 가져오고 가져오기가 완료되면 구조를 표시합니다.

![IntelliJ에서 Spring Boot 앱][CL14]

## <a name="build-your-spring-boot-app"></a>Spring Boot 앱 빌드

### <a name="build-the-app-by-using-the-maven-pom"></a>Maven POM을 사용하여 앱 빌드

1. 아직 열려 있지 않은 경우 Maven 도구 창을 엽니다. **보기** > **도구 창** > **Maven 프로젝트**를 클릭합니다.

   ![도구 창과 Maven 프로젝트 명령][BU01]

1. Maven 도구 창에서 마우스 오른쪽 단추로 **패키지**를 클릭하고 **Maven 빌드 실행**을 선택합니다. (Maven 프로젝트가 자동으로 표시되지 않는 경우 Maven 툴바의 **다시 가져오기** 아이콘을 클릭합니다.)

   ![Maven 빌드 실행 명령][BU02]

1. IntelliJ는 Spring Boot 앱이 성공적으로 생성되면 **빌드 성공** 메시지를 표시해야 합니다.

   ![빌드 성공 메시지][BU03]

### <a name="create-a-deployment-ready-artifact"></a>배포 준비된 아티팩트 만들기

Spring Boot 앱을 게시하려면 배포 준비된 아티팩트를 만들어야 합니다. 다음 단계를 사용하세요.

1. IntelliJ의 웹앱 프로젝트를 엽니다.

1. **파일**을 클릭한 다음 **프로젝트 구조**를 클릭합니다.

   ![프로젝트 구조 명령][ART01]

1. 녹색 더하기(**+**) 기호를 클릭하여 아티팩트를 추가하고 **JAR**을 클릭한 다음 **비어 있음**을 클릭합니다.

   ![아티팩트 추가][ART02]

1. ".jar" 확장명을 추가하지 않도록 하는 동안 아티팩트의 이름을 지정한 다음 Maven 출력에 대한 대상 폴더를 지정합니다.

   ![아티팩트 속성 지정][ART03]

1. 아티팩트에 대한 매니페스트를 만듭니다(선택 사항).

   a. **매니페스트 만들기**를 클릭합니다.

      ![매니페스트 만들기 단추 클릭][ART04a]

   b. 아티팩트에 대한 기본 경로를 선택한 다음 **확인**을 클릭합니다.

      ![아티팩트 경로 지정][ART04b]

   다. 줄임표 **...** 를 클릭하여 기본 클래스를 찾습니다.

      ![기본 클래스 찾기][ART04c]

   d. 기본 클래스를 선택한 다음 **확인**을 클릭합니다.

      ![기본 클래스 지정][ART04d]

1. **확인**을 클릭합니다.

   ![프로젝트 구조 대화 상자 닫기][ART05]

> [!NOTE]
> IntelliJ에서 아티팩트를 만드는 데 관한 자세한 내용은 JetBrains 웹 사이트의 [아티팩트 구성]을 참조하세요.
>

### <a name="build-the-artifact-for-deployment"></a>배포에 대한 아티팩트 빌드

1. **빌드**를 클릭한 다음 **아티팩트**를 클릭합니다.

   ![아티팩트 빌드 명령][BU04]

1. **아티팩트 빌드** 바로 가기 메뉴가 나타나면 **빌드**를 클릭합니다.

   ![아티팩트 빌드 컨텍스트 메뉴][BU05]

IntelliJ는 프로젝트 도구 창에서 Spring Boot 앱에 대한 완료된 아티팩트를 표시해야 합니다.

   ![만든 아티팩트][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Docker 컨테이너를 사용하여 Azure에 웹앱 게시

1. Azure 계정에 로그인하지 않은 경우 [IntelliJ용 Azure 도구 키트에 대한 로그인 지침][Azure Sign In for IntelliJ]의 단계를 따릅니다.

1. 프로젝트 탐색기 도구 창에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **Azure** > **Docker 컨테이너로 게시**를 선택합니다.

   ![Docker 컨테이너로 게시 명령][PU01]

1. **Azure에서 Docker 컨테이너 배포** 대화 상자가 표시되는 경우 기존 Docker 호스트가 표시됩니다. 기존 호스트에 배포하려는 경우 4단계로 건너뛸 수 있습니다. 그렇지 않으면 다음 단계에 따라 호스트를 만듭니다.

   a. 녹색 더하기(**+**) 기호를 클릭합니다.

      ![새 Docker 호스트 추가][PU02]

   b. **Create Docker Host** 대화 상자가 표시되면 기본값을 그대로 허용하도록 선택하거나 새 Docker 호스트에 대한 사용자 지정 설정을 지정할 수 있습니다. 다양한 설정에 대한 자세한 설명은 [IntelliJ용 Azure 도구 키트를 사용하여 웹앱을 Docker 컨테이너로 게시][Publish Container with Azure Toolkit]를 참조하세요. 사용할 설정을 지정하면 **다음**을 클릭합니다.

      ![Docker 호스트 옵션 지정][PU03a]

   다. Azure Key Vault에서 기존 로그인 자격 증명을 사용하도록 선택하거나 새 Docker 로그인 자격 증명을 입력하도록 선택할 수 있습니다. 옵션을 지정하면 **마침**을 클릭합니다.

      ![Docker 호스트 자격 증명 지정][PU03b]

1. Docker 호스트를 선택하고 **다음**을 클릭합니다.

   ![사용할 Docker 호스트 선택][PU04]

1. **Azure에 Docker 컨테이너 배포** 대화 상자의 마지막 페이지에서 다음 옵션을 지정합니다.

   a. Docker 컨테이너를 호스팅할 컨테이너에 대한 사용자 지정 이름을 지정하도록 선택하거나 기본값을 적용할 수 있습니다.

   b. *[외부 포트]*:*[내부 포트]* 구문을 사용하여 Docker 호스트에 대한 TCP 포트를 입력합니다. 예를 들어 **80:8080**은 80 외부 포트 및 8080 기본 내부 Spring Boot 포트를 지정합니다.
   
      내부 포트를 사용자 지정한 경우(예: application.yml 파일 편집) Azure에서 올바른 라우팅을 수행할 포트 번호를 지정해야 합니다.

   다. 이러한 옵션을 구성했으면 **마침**을 클릭합니다.

   ![Azure에 Docker 컨테이너 배포][PU05]

1. Azure 도구 키트에서 게시를 완료하면 Azure 활동 로그에 **게시됨** 상태가 표시됩니다.

   ![Docker 호스트를 성공적으로 배포][PU06]

## <a name="next-steps"></a>다음 단계

IntelliJ를 사용하여 Spring Boot 앱을 만들기 위한 추가 방법에 대해 알아보려면 JetBrains 웹 사이트에서 [Spring Boot 프로젝트 만들기](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html)를 참조하세요.

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[아티팩트 구성]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
