---
title: "IntelliJ용 Azure 도구 키트를 사용하여 Linux 컨테이너에서 Hello World 웹앱 실행"
description: "Linux 컨테이너에서 기본 Hello World 웹앱을 만들고 IntelliJ용 Azure 도구 키트를 사용하여 Azure에 게시하는 방법을 알아봅니다."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm
ms.openlocfilehash: c3c6339bb5a8415854253701d0ac340d42587509
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2017
---
# <a name="run-a-hello-world-web-app-in-a-linux-container-by-using-the-azure-toolkit-for-intellij"></a>IntelliJ용 Azure 도구 키트를 사용하여 Linux 컨테이너에서 Hello World 웹앱 실행

[Docker] 컨테이너는 웹 응용 프로그램을 배포하는 데 널리 사용되는 방법입니다. 개발자는 Docker 컨테이너를 통해 모든 프로젝트 파일과 종속성을 서버에 배포할 단일 패키지로 통합할 수 있습니다. IntelliJ용 Azure 도구 키트는 Microsoft Azure에 컨테이너 배포를 위한 기능을 추가함으로써 Java 개발자들을 위해 이 프로세스를 간소화합니다.

이 문서에서는 기본 Hello World 웹앱을 만들고 IntelliJ용 Azure 도구 키트를 사용하여 Linux 컨테이너의 웹앱을 Azure에 게시하는 데 필요한 단계를 보여 줍니다.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* [Docker] 클라이언트

> [!NOTE]
>
> 이 자습서의 단계를 완료하려면 TLS 없이 포트 2375에서 디먼을 노출하도록 [Docker]를 구성해야 합니다. Docker를 설치할 때 또는 Docker 설정 메뉴를 통해 이 설정을 구성할 수 있습니다.
>
> ![Docker 설정 메뉴][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a>새 웹앱 프로젝트 만들기

1. IntelliJ를 시작하고 [IntelliJ용 Azure 도구 키트에 대한 로그인 지침] 문서의 단계를 사용하여 Azure 계정에 로그인합니다.

1. **파일** 메뉴, **새로 만들기**를 차례로 클릭한 다음 **프로젝트**를 클릭합니다.
   
   ![새 프로젝트 만들기][file-new-project]

1. **새 프로젝트** 대화 상자에서 **Maven**, **maven-archetype-webapp**을 차례로 선택한 후 **다음**을 클릭합니다.
   
   ![Maven archetype webapp 선택][maven-archetype-webapp]
   
1. 웹앱에 대해 **GroupId** 및 **ArtifactId**를 지정한 후 **다음**을 클릭합니다.
   
   ![GroupId 및 ArtifactId 지정][groupid-and-artifactid]

1. Maven 설정을 사용자 지정하거나 기본값을 적용한 후 **다음**을 클릭합니다.
   
   ![Maven 설정 지정][maven-options]

1. 프로젝트 이름 및 위치를 지정한 다음 **마침**을 클릭합니다.
   
   ![프로젝트 이름 지정][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a>Azure Container Registry를 만들어서 개인 Docker 레지스트리로 사용

다음 단계에서는 Azure Portal을 사용하여 Azure Container Registry를 만드는 방법을 설명합니다.

> [!NOTE]
>
> Azure Portal 대신 Azure CLI를 사용하려는 경우 [Azure CLI 2.0을 사용하여 전용 Docker 컨테이너 레지스트리 만들기][Create Docker Registry using Azure CLI]의 단계에 따르세요.
>

1. [Azure Portal]을 찾아 로그인합니다.

   Azure Portal에서 사용자의 계정에 로그인하면 [Azure Portal을 사용하여 개인 Docker 컨테이너 레지스트리 만들기] 문서의 단계를 수행할 수 있습니다. 편의상 다음 단계에서 다시 설명합니다.

1. **+ 새로 만들기**의 메뉴 아이콘을 클릭하고 **컨테이너**를 클릭한 다음 **Azure Container Registry**를 클릭합니다.
   
   ![새로운 Azure Container Registry 만들기][AR01]

1. Azure Container Registry 템플릿에 대한 정보 페이지가 표시되면 **만들기**를 클릭합니다. 

   ![새로운 Azure Container Registry 만들기][AR02]

1. **컨테이너 레지스트리 만들기** 페이지가 표시되면 **레지스트리 이름** 및 **리소스 그룹**을 입력하고 **관리 사용자**에 대해 **사용**을 선택한 다음 **만들기**를 클릭합니다.

   ![Azure Container Registry 설정 구성][AR03]

1. 컨테이너 레지스트리를 만들면 Azure Portal에서 컨테이너 레지스트리를 탐색한 다음 **선택키**를 클릭합니다. 다음 단계에서 사용자 이름과 암호를 적어둡니다.

   ![Azure Container Registry 선택키][AR04]

## <a name="deploy-your-web-app-in-a-docker-container"></a>Docker 컨테이너에서 웹앱 배포

1. 프로젝트 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**를 선택한 다음 **Docker 지원 추가**를 클릭합니다.

   기본 구성을 사용하여 Docker 파일이 자동으로 만들어집니다.

   ![Docker 지원 추가][add-docker-support]

1. Docker 지원을 추가한 후 프로젝트 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**를 선택한 다음 **웹앱 실행(Linux)**을 클릭합니다.

   ![웹앱 실행(Linux)][run-on-web-app-linux]

1. **웹앱 실행(Linux)** 대화 상자가 표시되면 필수 정보를 입력합니다.

   * **이름**: Azure 도구 키트에 표시되는 친숙한 이름을 지정합니다. 

   * **서버 URL**: 이 문서의 이전 섹션에서 컨테이너 레지스트리에 대한 URL을 지정합니다. 일반적으로 다음 구문: "*registry*.azurecr.io"를 사용합니다. 

   * **사용자 이름** 및 **암호**: 이 문서의 이전 섹션에서 컨테이너 레지스트리에 대한 액세스 키를 지정합니다. 

   * **이미지 및 태그**: 컨테이너 이미지 이름을 지정합니다. 일반적으로 다음 구문: "*registry*.azurecr.io/*appname*:latest"를 사용합니다. 여기에서 
      * *registry*는 이 문서의 이전 섹션에서 컨테이너 레지스트리이며 
      * *appname*은 웹앱의 이름입니다. 

   * **기존 웹앱 사용** 또는 **새 웹앱 만들기**: 컨테이너를 기존 웹앱에 배포할지 새 웹앱을 만들지 여부를 지정합니다. 

   * **리소스 그룹**: 기존 리소스 그룹을 사용할지 새 리소스 그룹을 만들지 여부를 지정합니다. 

   * **App Service 계획**: 기존 App Service 계획을 사용할지 새 앱 서비스 계획을 만들지 여부를 지정합니다. 

1. 위에 나열된 설정을 구성했으면 **실행**을 클릭합니다.

   ![웹앱 만들기][create-web-app]

1. 웹앱을 게시한 후 설정은 기본값으로 저장되고 도구 모음에서 녹색 화살표 아이콘을 클릭하여 Azure에서 응용 프로그램을 실행할 수 있습니다. 웹앱에 대한 드롭다운 메뉴를 클릭하여 이러한 설정을 수정하고 **구성 편집**을 클릭할 수 있습니다.

   ![구성 편집 메뉴][edit-configuration-menu]

1. **실행/디버그 구성** 대화 상자가 표시되면 기본 설정을 수정한 다음 **확인**을 클릭할 수 있습니다.

   ![[구성 편집] 대화 상자][edit-configuration-dialog]

## <a name="next-steps"></a>다음 단계

Docker의 추가 리소스는 공식 [Docker 웹 사이트][Docker]를 참조하세요.

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Portal]: https://portal.azure.com/
[Azure Portal을 사용하여 개인 Docker 컨테이너 레지스트리 만들기]: /azure/container-registry/container-registry-get-started-portal
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[AR01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR01.png
[AR02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR02.png
[AR03]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR03.png
[AR04]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR04.png

[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[create-web-app]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-web-app.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
