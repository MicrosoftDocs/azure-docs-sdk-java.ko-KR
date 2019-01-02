---
title: Azure DevOps를 사용하는 MicroProfile 애플리케이션의 CI/CD
description: Azure DevOps를 사용하여 MicroProfile 애플리케이션을 컨테이너 인스턴스용 Azure 웹 앱에 배포하기 위해 CI/CD 릴리스 주기를 설정하는 방법에 대해 알아봅니다.
services: Azure DevOps
documentationcenter: MicroProfile
author: ruyakubu
manager: brunoborges
editor: ruyakubu
ms.assetid: ''
ms.author: ruyakubu
ms.date: 09/14/2018
ms.devlang: Java
ms.service: Azure DevOps
ms.tgt_pltfrm: multiple
ms.topic: tutorial
ms.workload: web
ms.openlocfilehash: 818e37291fa47f99cb161c63a86062bddbf6248c
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799939"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a>Azure DevOps를 사용하는 MicroProfile 애플리케이션의 CI/CD

이 자습서에서는 Java EE 개발자가 Azure DevOps(공식적으로는 VSTS라고 함)를 사용하는 컨테이너 용 Azure 웹 앱에 [MicroProfile](http://microprofile.io) 애플리케이션을 배포하기 위해 CI/CD 릴리스 주기를 쉽게 설정하는 방법을 보여줍니다.  이 예제에서는 [Payara Micro](https://www.payara.fish/payara_micro)를 기본 이미지로 사용하는 MicroProfile 애플리케이션을 사용합니다.   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
Docker 이미지를 만들고 컨테이너 이미지를 Azure 컨테이너 레지스터에 푸시하여 Azure DevOps 컨테이너화 프로세스를 시작합니다.  그런 다음 Azure DevOps 릴리스 파이프라인을 사용하여 컨테이너 이미지를 웹 앱에 배포합니다.

## <a name="prerequisites"></a>필수 조건
- [Github](https://github.com/Azure-Samples/microprofile-hello-azure)에서 Git url을 복사하고 저장합니다.
- [Azure DevOps](https://dev.azure.com) 계정을 등록 또는 계정에 로그인합니다.
- 새 [Azure DevOps 프로젝트](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav)를 만들고 위의 Git url을 사용하여 **리포지토리 가져오기**를 합니다.
- [ACR(Azure Container Registry)](https://azure.microsoft.com/en-us/services/container-registry) 만들기
- 컨테이너용 Azure 웹 앱 만들기
  > [!NOTE]
  >
  > 웹 앱 인스턴스를 프로비저닝할 때 컨테이너 설정에서 "빠른 시작" 선택


## <a name="create-a-build-definition"></a>빌드 정의 만들기

Azure DevOps의 빌드 정의는 Java EE 애플리케이션 소스 애플리케이션에서 커밋이 있을 때마다 빌드의 모든 작업을 자동으로 실행합니다.  이 예제에서는 Azure DevOps는 MicroProfile Java 프로젝트를 빌드하기 위해 Maven을 사용합니다.

1. Azure DevOps 프로젝트 페이지 위쪽에서 "빌드 및 릴리스" 탭을 클릭합니다.  그런 다음, **빌드** 링크를 선택합니다. 

<img src="media/VSTS/Buid-and-Release1.png">

2. 빌드 작업을 정의하려면**새 파이프라인** 단추를 클릭하고 나서 **계속**을 클릭합니다.
3. Java 프로젝트를 빌드하려면 템플릿 목록에서 "Maven"을 선택한 다음 **적용** 단추를 클릭합니다.
4. 에이전트 풀 필드에 대한 드롭다운 메뉴를 사용하여 **호스팅된 Linux 미리 보기** 옵션을 선택합니다.
   > [!NOTE]
   >
   > 이는 Azure DevOps에 어느 빌드 서버를 사용할지를 알립니다.  개인 사용자 지정된 빌드 서버를 사용할 수 있습니다.

5. 지속적인 통합을 위해 빌드를 구성하려면 **트리거** 탭을 선택하고 **연속 통합 사용** 확인란을 선택하십시오.  

<img src="media/VSTS/Build-Triggers2.png"> 

6. 기본 빌드 파이프라인 페이지로 다시 돌아가려면 <strong>작업</strong> 탭을 선택합니다.
7. <strong>저장 &amp; 큐</strong> 드롭다운 메뉴를 사용하여 <strong>저장</strong> 옵션을 선택합니다.


## <a name="create-a-docker-build-image"></a>Docker 빌드 이미지 만들기

이 작업에서는 Azure DevOps가 Payara Micro의 기본 이미지와 함께 Docker 파일을 사용하여 Docker 이미지를 만듭니다.  

1. 기본 빌드 파이프라인 페이지로 다시 돌아가려면 **작업** 탭을 선택합니다.
2. 빌드 정의에 새 작업을 추가하려면 **+** 아이콘을 클릭합니다.

<img src="media/VSTS/Tasks-add4.png">

3. 템플릿 목록에서 &quot;Docker&quot;를 선택한 다음, <strong>추가</strong> 단추를 클릭합니다.
4. <strong>표시 이름</strong> 필드에 대한 설명 이름을 입력합니다.
5. <strong>컨테이너 레지스트리 유형</strong>의 드롭다운 메뉴에서 <strong>Azure Container Registry</strong>가 선택되었는지 확인합니다.
&gt; [!NOTE]
&gt; &gt; Docker 허브 또는 다른 레지스트리를 사용하는 경우 대신 &quot;Container Registry&quot;를 선택합니다.  그리고 자격 증명 및 이에 대한 연결 정보를 제공하려면 &quot;+새로 만들기&quot; 단추를 클릭합니다. 계속 하려면 명령 섹션을 건너뜁니다.

6. **Azure 구독** 드롭다운 메뉴를 사용하여 Azure 구독 ID를 선택합니다.  그런 다음 **권한 부여** 단추를 클릭합니다.
7. **Azure 컨테이너 레지스트리** 드롭다운 메뉴에서 Azure에서 만든 레지스트리 이름을 선택합니다.
8. **명령** 드롭다운 메뉴에서 **빌드** 옵션이 선택되었는지 확인합니다.
9. **Dockerfile**의 경우 텍스트 상자 옆에 있는 경로 탐색 아이콘을 클릭하여 github 프로젝트에서 Dockerfile을 선택하십시오.  그리고 **확인** 단추를 클릭합니다.

<img src="media/VSTS/Dockerfile5.png">

10. **이미지 이름** 아래 **최신 태그 포함** 확인란을 선택합니다. 
11. **저장 및 큐** 드롭다운 메뉴를 사용하여 **저장** 옵션을 선택합니다.

## <a name="push-docker-image-to-acr"></a>ACR에 Docker 이미지 푸시

이 작업에서 Azure DevOps는 Azure Container Registry로 Docker 이미지를 푸시합니다.  이는 MicroProfile API 애플리케이션을 컨테이너화된 Java 웹 앱으로 실행하는 데 사용됩니다.

1. Azure DevOps에서 Docker를 사용하고 있으므로 **Docker Build Image 만들기** 섹션에서 위의 1 - 7 단계를 반복하여 새 Docker 템플릿을 만듭니다.
2. **명령** 드롭다운 메뉴에서 **푸시**를 선택합니다.
3. **저장 및 큐** 탭을 클릭한 다음, **저장 및 큐** 옵션을 선택합니다.
4. **호스팅된 Linux 미리 보기**가 팝업 창에서 에이전트 풀에 대해 선택되었는지 확인합니다.  그리고 **저장 및 큐** 단추를 클릭합니다.
5. 빌드 번호를 클릭하여 Java 프로젝트의 빌드 파이프라인이 성공적으로 완료되었는지 확인합니다.

<img src="media/VSTS/Build-Number6.png">


## <a name="create-a-release-definition-for-a-java-app"></a>Java 앱에 대한 릴리스 정의 만들기

Azure DevOps의 릴리스 파이프라인은 빌드 프로세스가 성공적으로 완료되는 즉시 Azure와 같은 대상 환경에 빌드 아티팩트의 배포를 자동으로 트리거합니다.   개발, 테스트, 스테이징 또는 프로덕션 환경에 대 한 릴리스 파이프라인을 만들 수 있습니다.

1. Azure DevOps 프로젝트 페이지 위쪽에서 "빌드 및 릴리스" 탭을 클릭합니다.  그리고 **릴리스** 링크를 선택합니다.

<img src="media/VSTS/Release-new-pipeline7.png">

2. &quot;새 파이프라인** 단추를 클릭합니다.
3. 템플릿 목록에서 <strong>Azure App Service에 Java 앱 배포</strong>를 선택하고, <strong>적용</strong> 단추를 클릭합니다.

<img src="media/VSTS/deploy-java-template8.png">

4. <strong>단계 이름</strong>(예: 개발, 테스트, 스테이징 또는 프로덕션)을 설정합니다.  그리고 팝업 창을 닫으려면 <strong>X</strong> 단추를 클릭합니다.
5. 아티팩트 섹션에서 <strong>+추가</strong> 단추를 클릭합니다.  이는 빌드 정의에서 이 릴리스 정의로 아티팩트를 연결합니다.<br/>6. 빌드 정의를 선택하려면 <strong>소스(빌드 파이프라인)</strong>에 대한 드롭다운 메뉴를 사용합니다. 그리고 계속하려면 <strong>추가</strong> 단추를 클릭합니다.

<img src="media/VSTS/add-artifact9.png">

7. 파이프라인에서 <strong>작업</strong> 탭을 클릭합니다.  그런 다음 단계 이름을 선택합니다.

<img src="media/VSTS/release-stage10.png">

8. **Azure 구독** 드롭다운 메뉴를 사용하여 Azure 구독 ID를 선택합니다.
9. **앱 유형** 드롭다운 메뉴에서 **Linux 앱**을 선택합니다.
10. **앱 서비스 이름** 드롭다운 메뉴에서 위에서 작성한 컨테이너 인스턴스의 웹 앱 이름을 선택합니다.
11. **레지스트리 또는 네임스페이스** 필드에 Azure 컨테이너 레지스트리의 이름을 입력합니다.  E.g **myregistry.azure.io**
12. **리포지토리** 필드에 레지스트리 이름을 입력합니다.
13. **Azure App Service 배포**를 클릭합니다.  **태그** 텍스트상자에 컨테이너 이미지의 태그를 입력합니다. 
14. **에이전트에서 실행**을 클릭합니다.  에이전트 풀 드롭다운 메뉴에서 **호스팅된 Linux 미리보기**를 선택합니다. 

## <a name="setup-environment-variables"></a>환경 변수를 설정합니다.

1. **변수** 탭을 클릭합니다.  환경 변수를 정의하려면 **+추가** 단추를 클릭합니다.
2. 컨테이너 레지스트리 url, 사용자 이름 및 암호 변수 이름과 값을 추가합니다.   보안을 위해, 암호 값 숨김을 유지하려면 자물쇠 아이콘을 클릭합니다.

예: 
- registry.password
- registry.url
- registry.username

<img src="media/VSTS/environment-variables12.png">

3. 주 릴리스 파이프라인 정의 페이지로 돌아가려면 **작업** 탭을 클릭합니다.
4. **Azure App Service 배포**를 클릭합니다. 
5. **응용 프로그램 및 구성 설정** 섹션을 확장한 다음 **응용 프로그램 설정** 필드의 탐색 경로를 클릭하여 배포 중에 컨테이너 레지스트리에 연결할 환경 변수를 추가합니다.
6. **+ 추가** 버튼을 클릭하여 다음 앱 설정을 정의하고 환경 변수를 할당합니다.
7. DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)
8. DOCKER_REGISTRY_SERVER_URL = $(registry.url)
9. DOCKER_REGISTRY_SERVER_URL = $(registry.url)

<img src="media/VSTS/environment-variables14.png">

7. 계속하려면 <strong>확인</strong> 단추를 클릭합니다.

## <a name="setup-continious-deployment--deploy-java-application"></a>지속적인 배포 설정 및 Java 응용 프로그램 배포

1. 지속적인 배포를 활성화하려면 **파이프라인** 탭을 클릭합니다.
2. 아티팩트 섹션에서 번갯불 아이콘을 클릭합니다.  그런 다음 **지속적인 배포 트리거**를 활성화로 설정합니다.

<img src="media/VSTS/release-enable-CD.png">

3. <strong>저장</strong> 단추를 클릭하고 <strong>확인</strong> 단추를 클릭합니다. 
4. <strong>릴리스</strong> 드롭다운 메뉴를 클릭하고 <strong>릴리스 만들기</strong> 링크를 선택합니다.
5. <strong>자동에서 수동으로 변경을 트리거하는 단계</strong> 드롭다운 메뉴를 사용하여 단계 이름의 확인란을 선택합니다.
6. 계속하려면 <strong>만들기</strong> 단추를 클릭합니다.
7. 릴리스 번호를 클릭합니다.  그런 다음 스테이지 이름 위로 마우스 커서를 이동하고 <strong>배포</strong> 단추를 클릭합니다.
8. Azure에 배포 프로세스를 시작하려면 팝업 창에서 <strong>배포</strong> 단추를 클릭합니다.


## <a name="test-the-java-web-application"></a>Java 웹 애플리케이션 테스트하기
1. 웹 브라우저에서 웹 앱 url을 실행합니다.  
   https://{your-app-service-name}.azurewebsites.net/api/hello


<img src="media/VSTS/web-app16.png">

2. 웹 페이지에 **Hello Azure!** 가 나타납니다.

<img src="media/VSTS/web-api17.png">
