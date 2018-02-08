---
title: "Eclipse용 Azure 도구 키트를 사용하여 Spring Boot 앱을 Docker 컨테이너로 게시"
description: "Eclipse용 Azure 도구 키트를 사용하여 Docker 컨테이너로 Microsoft Azure에 웹앱을 게시하는 방법을 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: b54c10dc33324d902a0e778770df8ec4d71dc9a1
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Eclipse용 Azure 도구 키트를 사용하여 Spring Boot 앱을 Docker 컨테이너로 게시

[Spring Framework]는 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만드는 데 도움이 되는 오픈 소스 솔루션입니다. 해당 플랫폼을 기반으로 하여 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 응용 프로그램을 만드는 간단한 방법을 제공합니다.

[Docker]는 개발자가 컨테이너에서 실행되는 응용 프로그램의 배포, 크기 조정 및 관리를 자동화하는 데 도움이 되는 오픈 소스 솔루션입니다.

이 자습서에서는 Eclipse용 Azure 도구 키트를 사용하여 Microsoft Azure에 Docker 컨테이너로 Spring Boot 응용 프로그램을 배포하는 단계를 안내합니다.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a>기본 Spring Boot Docker 리포지토리 복제

### <a name="import-the-public-repository"></a>공용 리포지토리 가져오기

다음 단계는 IntelliJ를 사용하여 Spring Boot Docker 리포지토리를 로컬 컴퓨터로 복제하는 방법을 안내합니다. 명령줄을 사용하려면 [Azure Container Service에서 Linux에 Spring Boot 응용 프로그램 배포][Deploy Spring Boot on Linux in AKS]를 참조하세요.

1. Eclipse를 엽니다.

1. **File** > **Import**를 차례로 클릭합니다.

   ![File Import 메뉴][CL01]

1. **Import** 대화 상자가 열리면:

   a. **Git**를 확장합니다.

   나. **Projects from Git**를 선택합니다.
   
   다. **다음**을 클릭합니다.

   ![Import 대화 상자][CL02]

1. **Select Repository Source** 페이지에서:

   a. **Clone URI**를 선택합니다.
   
   나. **다음**을 클릭합니다.

   ![Select Repository Source 페이지][CL03]

1. **Source Git Repository** 페이지에서:

   a. **URI**에 대해 `https://github.com/spring-guides/gs-spring-boot-docker.git`를 입력합니다. 이 단계에서는 **Host** 및 **Repository path** 필드에 올바른 값을 자동으로 채웁니다.
   
   나. Spring Boot 리포지토리는 공개되어 있으므로 Git 사용자 이름과 암호를 입력하지 않아도 됩니다.
   
   다. **다음**을 클릭합니다.

   ![Source Git Repository 페이지][CL04]

1. **Branch Selection** 페이지에서 **Next**를 클릭합니다.

   ![Branch Selection 페이지][CL05]

1. **Local Destination** 페이지에서:

   a. 로컬 리포지토리를 저장할 로컬 폴더를 지정합니다.
   
   나. **다음**을 클릭합니다.

   ![Local Destination 페이지][CL06]

1. **Select a wizard to use for importing projects** 페이지에서:

   a. **Import as a general project**를 선택합니다.
   
   나. **다음**을 클릭합니다.

   !["Select a wizard to use for importing projects" 페이지][CL07]

1. **Import Projects** 페이지에서:

   a. 프로젝트 이름을 지정합니다.
   
   나. **Finish**를 클릭합니다.

   ![Import Projects 페이지][CL08]

1. 리포지토리가 성공적으로 복제되면 Eclipse에 나열된 모든 파일을 볼 수 있습니다.

   ![로컬 리포지토리][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>로컬 리포지토리에서 Maven 프로젝트 만들기

Spring Boot Docker 리포지토리는 이 자습서에서 사용할 완성된 Maven 프로젝트를 포함하고 있습니다. 

1. **File** > **Import**를 차례로 클릭합니다.

   ![File 메뉴의 Import 명령][CL01]

1. **Import** 대화 상자가 열리면:

   a. **Maven**을 확장합니다.
   
   나. **Existing Maven Projects**를 선택합니다.
   
   다. **다음**을 클릭합니다.

   ![Import 대화 상자][MV01]

1. **Maven Projects** 페이지에서:

   a. **Root Directory**에 대해 로컬 리포지토리의 **전체** 폴더를 지정합니다.
   
   나. **Advanced** 섹션을 펼치고 **Name template**에 사용자 지정 이름을 입력합니다.
   
   다. 프로젝트에서 **pom.xml** 파일에 대한 상자를 선택합니다.
   
   d. **Finish**를 클릭합니다.

   ![Maven Projects 페이지][MV02]

1. Maven 프로젝트가 성공적으로 열리면 Eclipse에 나열된 두 번째 프로젝트가 표시됩니다.

   ![로컬 Maven 프로젝트][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Maven을 사용하여 Spring Boot 앱 빌드

1. Eclipse Project Explorer에서 Maven 프로젝트를 선택합니다.

1. **Run** > **Run As** > **Maven build**를 차례로 클릭합니다.

   ![Maven build로 실행하는 명령][BU01]

1. 응용 프로그램이 성공적으로 빌드되면 콘솔 창에 상태가 표시됩니다.

   ![성공적인 Maven 빌드][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Docker 컨테이너를 사용하여 Azure에 웹앱 게시

1. Eclipse Project Explorer에서 Maven 프로젝트를 선택합니다.

1. Azure **Publish** 메뉴를 클릭한 다음 **Publish as Docker Container**를 클릭합니다.

   ![Publish as Docker Container 명령][PU01]

1. **Deploying Docker Container on Azure** 대화 상자가 표시되면 다음을 수행합니다.

   a. 사용자 지정 Docker 이미지 이름을 입력합니다.
   
   나. **Artifact to deploy**에 대해 방금 빌드한 **gs-spring-boot-docker-0.1.0.jar** 파일의 경로를 지정합니다.

   ![Docker 옵션 지정][PU02]

   기존의 모든 Docker 호스트가 표시됩니다. 

1. 기존 호스트에 배포하려는 경우 5단계로 건너뛸 수 있습니다. 그렇지 않으면 다음 단계에 따라 호스트를 만듭니다.

   a. **추가**를 클릭합니다.

      ![새 Docker 호스트 추가][PU03]

   나. **Create Docker Host** 대화 상자가 표시되면 기본값을 그대로 허용하도록 선택하거나 새 Docker 호스트에 대한 사용자 지정 설정을 지정할 수 있습니다. 다양한 설정에 대한 자세한 설명은 [IntelliJ용 Azure 도구 키트를 사용하여 웹앱을 Docker 컨테이너로 게시][Publish Container with Azure Toolkit]를 참조하세요. 사용할 설정을 지정하면 **다음**을 클릭합니다.

      ![Docker 호스트 옵션 지정][PU04]

   다. Azure Key Vault에서 기존 로그인 자격 증명을 사용하도록 선택하거나 새 Docker 로그인 자격 증명을 입력하도록 선택할 수 있습니다. 옵션을 지정하면 **마침**을 클릭합니다.

      ![Docker 호스트 자격 증명 지정][PU05]

1. Docker 호스트를 선택하고 **Next**를 클릭합니다.

   ![사용할 Docker 호스트 선택][PU06]

1. **Deploying Docker Container on Azure** 대화 상자의 마지막 페이지에서 다음 옵션을 지정합니다.

   a. Docker 컨테이너를 호스팅할 컨테이너에 대한 사용자 지정 이름을 지정하도록 선택하거나 기본값을 적용할 수 있습니다.

   나. *[외부 포트]*:*[내부 포트]* 구문을 사용하여 Docker 호스트에 대한 TCP 포트를 입력합니다. 예를 들어 **80:8080**은 80 외부 포트 및 8080 기본 내부 Spring Boot 포트를 지정합니다.
   
      내부 포트를 사용자 지정한 경우(예: application.yml 파일 편집) Azure에서 올바른 라우팅을 수행할 포트 번호를 지정해야 합니다.

   다. 이러한 옵션을 구성했으면 **Finish**를 클릭합니다.

   ![Azure에 Docker 컨테이너 배포][PU07]

1. Azure 도구 키트에서 게시를 완료하면 Azure 활동 로그에 **게시됨** 상태가 표시됩니다.

   ![Docker 호스트를 성공적으로 배포][PU08]

## <a name="next-steps"></a>다음 단계

Docker의 추가 리소스는 공식 [Docker 웹 사이트]를 참조하세요.

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: azure-toolkit-for-eclipse-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
