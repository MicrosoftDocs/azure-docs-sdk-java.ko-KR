---
title: "IntelliJ에서 기본 Azure Web App 만들기"
description: "이 자습서에서는 IntelliJ용 Azure 도구 키트를 사용하여 Azure용 Hello World 웹앱을 만드는 방법을 보여 줍니다."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: 323ce74f2d4dad10460a0c2bc0fb59f2bbdbbf3c
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a>IntelliJ에서 기본 Azure Web App 만들기

이 자습서에서는 [IntelliJ용 Azure 도구 키트]를 사용하여 기본 Hello World 응용 프로그램을 만들고 Azure에 웹앱으로 배포하는 방법을 보여 줍니다.

> [!NOTE]
> 
> IntelliJ용 Azure 도구 키트는 2017년 8월에 다른 워크플로로 업데이트되었습니다. 이 점을 염두에 두고 이 문서는 두 가지 섹션으로 구성됩니다.
>
> * 첫 번째 섹션에서는 IntelliJ용 Azure 도구 키트의 2017년 8월(또는 이후) 버전을 사용하여 Hello World 웹앱을 만드는 과정을 설명합니다.
>
> * 이 문서의 두 번째 섹션에서는 도구 키트의 2017년 8월(또는 이전) 버전을 사용하여 Hello World 웹앱을 만드는 과정을 설명합니다.
> 

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-hello-world-web-app-by-using-the-version-307-or-later-toolkit"></a>도구 키트 버전 3.0.7 이상을 사용하여 Hello World 웹앱 만들기

### <a name="create-a-new-web-app-project"></a>새 웹앱 프로젝트 만들기

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

1. IntelliJ의 Project Explorer 보기 내에서 **src**, **main**, **webapp**을 차례로 확장한 다음 **index.jsp**를 두 번 클릭합니다.
   
   ![인덱스 페이지 열기][open-index-page]

1. IntelliJ에서 index.jsp 파일이 열리면 **Hello World!**를 동적으로 표시하도록 텍스트를 추가합니다. 기존 `<body>` 요소 내. 업데이트된 `<body>` 콘텐츠는 다음 예제와 유사하게 표시됩니다.
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![인덱스 페이지 편집][edit-index-page]

1. index.jsp를 저장합니다.

### <a name="deploy-your-web-app-to-azure"></a>Azure에 웹앱 배포

1. IntelliJ의 Project Explorer 보기 내에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**, **웹앱 실행**을 차례로 선택합니다.
   
   ![[웹앱 실행] 메뉴][run-on-web-app-menu]

1. [웹앱 실행] 대화 상자에서 다음 옵션 중 하나를 선택할 수 있습니다.

   * 기존 웹앱을 선택한 후(있는 경우) **실행**을 클릭합니다.

      ![[웹앱 실행] 대화 상자][run-on-web-app-dialog]

   * **새 웹앱 만들기**를 클릭합니다. 새 웹앱 만들기를 선택한 경우 웹앱에 대한 필수 정보를 지정한 후 **실행**을 클릭합니다.

      ![새 웹앱 만들기][create-new-web-app-dialog]

1. 도구 키트에는 웹앱이 성공적으로 배포될 때 상태 메시지가 표시되며 배포된 웹앱의 URL도 표시됩니다.

   ![배포 정상 완료][successfully-deployed]

1. 상태 메시지에 제공된 링크를 사용하여 웹앱으로 이동할 수 있습니다.

   ![웹앱 찾아보기][browse-web-app]

1. 웹앱을 게시한 후 설정은 기본값으로 저장되고 도구 모음에서 녹색 화살표 아이콘을 클릭하여 Azure에서 응용 프로그램을 실행할 수 있습니다. 웹앱에 대한 드롭다운 메뉴를 클릭하여 설정을 수정하고 **구성 편집**을 클릭할 수 있습니다.

   ![[구성 편집] 메뉴][edit-configuration-menu]

1. **실행/디버그 구성** 대화 상자가 표시되면 기본 설정을 수정한 다음 **확인**을 클릭할 수 있습니다.

   ![[구성 편집] 대화 상자][edit-configuration-dialog]

<hr />

## <a name="create-a-hello-world-web-app-by-using-the-version-306-or-earlier-toolkit"></a>도구 키트 버전 3.0.6 이하를 사용하여 Hello World 웹앱 만들기

### <a name="create-a-new-web-app-project"></a>새 웹앱 프로젝트 만들기

1. IntelliJ를 시작하고 **File** 메뉴를 클릭한 후 **New**를 클릭하고 **Project**를 클릭합니다.
   
   ![파일 새로 만들기 프로젝트][02]

2. **New Project** 대화 상자에서 **Java**를 선택하고 **Web Application**을 선택한 후 **New**를 클릭하여 프로젝트 SDK를 추가합니다.
   
   ![새 프로젝트 대화 상자][03a]
   
3. Select Home Directory for JDK 대화 상자에서 JDK가 설치되어 있는 폴더를 선택한 후 **OK**를 클릭합니다. New Project 대화 상자에서 **Next**를 클릭하여 계속 진행합니다.
   
   ![JDK 홈 디렉터리 지정][03b]

4. 이 자습서의 목적에 따라 프로젝트의 이름을 **Java-Web-App-On-Azure**로 지정하고 **Finish**를 클릭합니다.
   
   ![새 프로젝트 대화 상자][04]

5. IntelliJ의 Project Explorer 보기 내에서 **Java-Web-App-On-Azure**를 확장한 다음 **web**을 확장하고 **index.jsp**를 두 번 클릭합니다.
   
   ![인덱스 페이지 열기][05c]

6. IntelliJ에서 index.jsp 파일이 열리면 **Hello World!**를 동적으로 표시하도록 텍스트를 추가합니다. 기존 `<body>` 요소 내. 업데이트된 `<body>` 콘텐츠는 다음 예제와 유사하게 표시됩니다.
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

7. index.jsp를 저장합니다.

### <a name="deploy-your-web-app-to-azure"></a>Azure에 웹앱 배포
몇 가지 방법으로 Azure에 Java 웹앱을 배포할 수 있습니다. 이 자습서에서는 가장 간단한 방법 중 하나를 설명합니다. 즉, 특별한 프로젝트 형식이나 추가 도구 없이 Azure 웹앱 컨테이너에 응용 프로그램을 배포하는 방법을 설명합니다. JDK 및 웹 컨테이너 소프트웨어는 Azure에서 제공되므로 별도로 업로드할 필요가 없습니다. Java 웹앱만 있으면 됩니다. 따라서 응용 프로그램 게시 프로세스에 걸리는 시간이 몇 분이 아니라 몇 초입니다.

응용 프로그램을 게시하기 전에 먼저 모듈 설정을 구성해야 합니다. 이렇게 하려면 다음 단계를 수행합니다.

1. IntelliJ의 Project Explorer에서 **Java-Web-App-On-Azure** 프로젝트를 마우스 오른쪽 단추로 클릭합니다. 상황에 맞는 메뉴가 나타나면 **모듈 설정 열기**를 클릭합니다.

   ![모듈 설정 열기][05a]

2. 프로젝트 구조 대화 상자가 나타나면 다음을 수행합니다.

   a. **프로젝트 설정** 목록에서 **아티팩트**를 클릭합니다.

   b. **이름** 상자에서 아티팩트 이름에 공백 또는 특수 문자가 포함되지 않도록 이름을 변경합니다. 이 작업은 해당 이름이 URI(Uniform Resource Identifier)에 사용되기 때문에 필요합니다.

   c. **형식**을 **웹 응용 프로그램: 보관**으로 변경합니다.

   d. **확인**을 클릭하여 프로젝트 구조 대화 상자를 닫습니다.

   ![모듈 설정 열기][05b]

모듈 설정을 구성한 경우 다음 단계를 사용하여 Azure에 응용 프로그램을 게시할 수 있습니다.

1. IntelliJ의 Project Explorer에서 **Java-Web-App-On-Azure** 프로젝트를 마우스 오른쪽 단추로 클릭합니다. 상황에 맞는 메뉴가 나타나면 **Azure**를 선택한 다음 **Azure 웹앱으로 게시...**를 선택합니다.
   
   ![Azure 게시 상황에 맞는 메뉴][06]

2. IntelliJ에서 Azure에 로그인하지 않은 경우 Azure 계정으로 로그인하라는 메시지가 표시됩니다. Azure 계정이 여러 개 있으면 로그인 프로세스 중에 일부 메시지가 동일한 것이더라도 두 번 이상 표시될 수 있습니다. 이 경우 로그인 지침에 따라 계속 진행합니다.
   
   ![Azure 로그인 대화 상자][07]

3. Azure 계정에 성공적으로 로그인하면 **구독 관리** 대화 상자에는 자격 증명과 연결된 구독 목록이 표시됩니다. 여러 구독이 나열된 경우 특정 하위 집합만 사용하려면 사용하지 않을 구독의 선택을 취소하면 됩니다. 구독을 선택했으면 **닫기**를 클릭합니다.
   
   ![구독 관리][08]

4. **Azure 웹앱 컨테이너에 배포** 대화 상자가 나타나는 경우 이전에 만든 웹앱 컨테이너가 표시됩니다. 컨테이너를 만들지 않은 경우에는 목록이 비어 있습니다.
   
   ![앱 컨테이너][09]

5. 이전에 Azure 웹앱 컨테이너를 만들지 않은 경우 또는 응용 프로그램을 새 컨테이너에 게시하려는 경우 다음 단계를 사용합니다. 그렇지 않으면 기존 웹앱 컨테이너를 선택하고 아래의 6단계로 건너뜁니다.
   
   a. **+** 기호를 클릭합니다.
      
      ![앱 컨테이너 추가][10]

   b. 다음 몇 개 단계에서 사용되는 **새 웹앱 컨테이너** 대화 상자가 표시됩니다.
      
      ![새 앱 컨테이너][11a]
   
   c. 웹앱 컨테이너에 **DNS 레이블**을 입력합니다. 이렇게 하면 Azure에서 웹 응용 프로그램에 대한 호스트 URL의 리프 DNS 레이블을 형성합니다. 이름은 사용 가능해야 하며, Azure 웹앱 명명 요구 사항을 준수해야 합니다.

   d. **웹 컨테이너** 드롭다운 메뉴에서 응용 프로그램에 적절한 소프트웨어를 선택합니다.
      
      현재, Tomcat 8, Tomcat 7, Jetty 9 중에서 선택할 수 있습니다. 선택한 소프트웨어의 최근 배포는 Azure에서 제공되며, Oracle에서 만들고 Azure에서 제공되는 JDK 8의 최근 배포에서 실행됩니다.

   e. **구독** 드롭다운 메뉴에서 이 배포에 사용할 구독을 선택합니다.

   f. **리소스 그룹** 드롭다운 메뉴에서 웹앱을 연결할 리소스 그룹을 선택합니다. (Azure 리소스 그룹을 사용하여 함께 삭제할 수 있도록 관련된 리소스를 그룹화할 수 있습니다.)
      
      기존 리소스 그룹(있는 경우)을 선택하고 아래 g 단계로 건너뛰거나 다음 단계를 통해 새 리소스 그룹을 만들 수 있습니다.
      
      * **리소스 그룹** 드롭다운 메뉴에서 **&lt;&lt;새 리소스 그룹 만들기&gt;&gt;**를 선택합니다.
      * **새 리소스 그룹** 대화 상자가 표시됩니다.
        
         ![새 리소스 그룹][12]

      * **이름** 텍스트 상자에서 새 리소스 그룹의 이름을 지정합니다.
      * **지역** 드롭다운 메뉴에서 리소스 그룹에 적합한 Azure 데이터 센터 위치를 선택합니다.
      * **확인**을 클릭합니다.

   g. **앱 서비스 계획** 드롭다운 메뉴에 선택한 리소스 그룹과 연결된 앱 서비스 계획이 나열됩니다. 앱 서비스 계획은 웹 앱, 가격 책정 계층 및 계산 인스턴스 크기의 위치와 같은 정보를 지정합니다. App Service 계획 하나를 여러 Web Apps에 사용할 수 있기 때문에 App Service 계획은 특정 웹앱 배포와는 별도로 관리됩니다.)
      
      기존 App Service 계획(있는 경우)을 선택하고 아래 h 단계로 건너뛰거나 다음 단계를 통해 새 App Service 계획을 만들 수 있습니다.
      
      * **App Service 계획** 드롭다운 메뉴에서 **&lt;&lt;새 App Service 계획 만들기&gt;&gt;**를 선택합니다.
      * **새 앱 서비스 계획** 대화 상자가 표시됩니다.
        
         ![새 앱 서비스 계획][13]

      * **이름** 텍스트 상자에서 새 App Service 계획의 이름을 지정합니다.
      * **위치** 드롭다운 메뉴에서 계획에 적합한 Azure 데이터 센터 위치를 선택합니다.
      * **가격 책정 계층** 드롭다운 메뉴에서 계획에 적합한 가격 책정을 선택합니다. 테스트 목적으로 **무료**를 선택할 수 있습니다.
      * **인스턴스 크기** 드롭다운 메뉴에서 계획에 적절한 인스턴스 크기를 선택합니다. 테스트 목적으로 **Small**을 선택할 수 있습니다.
      * **확인**을 클릭합니다.

   h. (선택 사항) 기본적으로 Java 8 최신 배포판은 자동으로 Azure에 의해 웹앱 컨테이너에 JVM으로 배포됩니다. 그러나 JVM의 다른 버전 및 배포판을 선택할 수 있습니다. 이렇게 하려면 다음 단계를 수행합니다.
      
      * **새 웹앱 컨테이너** 대화 상자에서 **JDK** 탭을 클릭합니다.
      * 다음 두 가지 옵션 중에서 선택할 수 있습니다.
        
         * Azure에서 제공하는 기본 JDK 배포
         * Azure에서 사용할 수 있는 추가 JDK 드롭다운 목록에서 타사 JDK 배포
         * 사용자 지정 JDK 배포(이 JDK는 ZIP 파일로 패키지된 후 공개적으로 제공되거나 Azure Storage 계정에 제공되어야 함)
        
      ![새 앱 컨테이너 JDK 탭][11b]

   i. 위 단계를 모두 완료한 경우 New Web App Container 대화 상자가 다음 그림과 유사하게 표시됩니다.
      
      ![새 앱 컨테이너][14]
   
   j. **확인** 을 클릭하여 새 웹앱 컨테이너 만들기를 완료합니다.
       
      웹 앱 컨테이너의 목록이 새로 고쳐지도록 몇 초 간 기다리고 나면 새로 만든 웹 앱 컨테이너를 목록에서 선택할 수 있게 됩니다.

6. 이제 Azure에 대한 웹앱의 초기 배포를 완료할 준비가 되었습니다. **확인**을 클릭하여 Java 응용 프로그램을 선택한 웹앱 컨테이너에 배포합니다. 기본적으로 응용 프로그램은 응용 프로그램 서버의 하위 디렉터리로 배포됩니다. 루트 응용 프로그램으로 배포하려면 **확인**을 클릭하기 전에 **루트에 배포** 확인란을 선택합니다.
   
   ![Azure에 배포][15]

7. 이제 웹앱의 배포 상태를 나타내는 **Azure 동작 로그** 보기를 확인합니다.
   
   ![진행률 표시기][16]
   
   Azure에 웹앱을 배포하는 프로세스는 몇 초 내에 완료됩니다. 응용 프로그램이 준비되면 **상태** 열에 **게시됨**이라는 링크가 표시됩니다. 이 링크를 클릭하여 배포된 웹앱의 홈페이지로 이동하거나, 다음 섹션의 단계를 사용하여 해당 웹앱으로 이동할 수 있습니다.

### <a name="browsing-to-your-web-app-on-azure"></a>Azure에서 웹앱 검색
Azure에서 웹앱을 검색하려면 **Azure 탐색기** 보기를 사용할 수 있습니다.

**Azure 탐색기** 보기가 열려 있지 않은 경우 IntelliJ에서 **View** 메뉴를 클릭한 다음 **Tool Windows**, **Service Explorer**를 차례로 클릭합니다. 이전에 로그인하지 않은 경우 로그인하라는 메시지가 나타납니다.

**Azure 탐색기** 보기가 표시되면 다음 단계에 따라 웹앱으로 이동합니다. 

1. **Azure** 노드를 확장합니다.
2. **웹앱** 노드를 확장합니다. 
3. 원하는 웹앱을 마우스 오른쪽 단추로 클릭합니다.
4. 상황에 맞는 메뉴가 나타나면 **브라우저에서 열기**를 클릭합니다.
   
   ![웹앱 찾아보기][17]

### <a name="updating-your-web-app"></a>웹앱 업데이트
실행 중인 기존 Azure 웹앱을 빠르고 쉽게 업데이트할 수 있으며, 두 가지 업데이트 옵션이 있습니다.

* 기존 Java 웹앱의 배포를 업데이트할 수 있습니다.
* 동일한 웹앱 컨테이너에 추가 Java 응용 프로그램을 게시할 수 있습니다.

두 경우 모두 프로세스는 동일하며 몇 초만 소요됩니다.

1. IntelliJ Project Explorer에서 업데이트하거나 기존 웹앱 컨테이너에 추가할 Java 응용 프로그램을 마우스 오른쪽 단추로 클릭합니다.
2. 상황에 맞는 메뉴가 나타나면 **Azure**를 선택한 다음 **Azure 웹앱으로 게시...**를 선택합니다.
3. 이전에 이미 로그인했으므로 기존 웹앱 컨테이너 목록이 표시됩니다. Java 응용 프로그램을 게시하거나 다시 게시할 컨테이너를 선택하고 **확인**을 클릭합니다.

몇 초 후 **Azure 동작 로그** 보기에 업데이트된 배포가 **게시됨**으로 표시되고, 웹 브라우저에서 업데이트된 응용 프로그램을 확인할 수 있습니다.

### <a name="starting-stopping-or-restarting-an-existing-web-app"></a>기존 웹앱 시작, 중지 또는 다시 시작
기존 Azure 웹앱 컨테이너(여기에 배포된 모든 Java 응용 프로그램 포함)를 시작 또는 중지하려면 **Azure 탐색기** 보기를 사용하면 됩니다.

**Azure 탐색기** 보기가 열려 있지 않은 경우 IntelliJ에서 **View** 메뉴를 클릭한 다음 **Tool Windows**, **Service Explorer**를 차례로 클릭합니다. 이전에 로그인하지 않은 경우 로그인하라는 메시지가 나타납니다.

**Azure 탐색기** 보기가 표시되면 다음 단계에 따라 웹앱을 시작하거나 중지합니다. 

1. **Azure** 노드를 확장합니다.
2. **웹앱** 노드를 확장합니다. 
3. 원하는 웹앱을 마우스 오른쪽 단추로 클릭합니다.
4. 상황에 맞는 메뉴가 나타나면 **시작**, **중지** 또는 **다시 시작**을 클릭합니다. 메뉴 선택 항목은 상황별로 변경되므로 실행 중인 웹앱만 중지하고, 현재 실행되고 있지 않은 웹앱만 시작할 수 있습니다.
   
   ![웹 앱 중지][18]

## <a name="next-steps"></a>다음 단계

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Azure 웹앱 만들기에 대한 자세한 내용은 [웹앱 개요]를 참조하세요.

<!-- URL List -->

[IntelliJ용 Azure 도구 키트]: azure-toolkit-for-intellij.md
[웹앱 개요]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/18-Stop-Web-App.png

[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[run-on-web-app-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[run-on-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
