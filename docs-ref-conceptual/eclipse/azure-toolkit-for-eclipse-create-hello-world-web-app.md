---
title: Eclipse를 사용하여 Azure용 Hello World 웹앱 만들기
description: 이 자습서에서는Eclipse용 Azure 도구 키트를 사용하여 Azure용 Hello World 웹앱을 만드는 방법을 보여 줍니다.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 5e025c90c2619ec72ffddf5815fd49c3ac59c00f
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893094"
---
# <a name="create-a-hello-world-web-app-for-azure-using-eclipse"></a>Eclipse를 사용하여 Azure용 Hello World 웹앱 만들기

이 자습서에서는 [Eclipse용 Azure 도구 키트 설치]를 사용하여 기본 Hello World 애플리케이션을 만들고 Azure에 웹앱으로 배포하는 방법을 보여 줍니다.

> [!NOTE]
>
> [IntelliJ용 Azure 도구 키트]를 사용하는 이 문서의 버전에 대한 내용은 [IntelliJ를 사용하여 Azure용 Hello World 웹앱 만들기][intellij-hello-world]를 참조하세요.
>

> [!IMPORTANT]
> 
> Eclipse용 Azure 도구 키트는 2017년 8월에 다른 워크플로로 업데이트되었습니다. 이 문서에서는 Eclipse용 Azure 도구 키트 버전 3.0.7 이상을 사용하여 Hello World 웹앱을 만드는 방법을 설명합니다. 도구 키트 버전 3.0.6 이하를 사용하는 경우 [레거시 도구 키트를 사용하여 Eclipse에서 Azure용 Hello World 웹앱 만들기][Legacy Version]의 단계를 수행해야 합니다.
> 

이 자습서를 완료한 경우 웹 브라우저에서 애플리케이션을 보면 다음 그림과 같이 표시됩니다.

![Hello World 앱의 미리 보기][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>새 웹앱 프로젝트 만들기

1. Eclipse를 시작하고, [Eclipse용 Azure 도구 키트에 대한 Azure 로그인 지침][eclipse-sign-in-instructions] 문서의 지침을 사용하여 Azure 계정에 로그인합니다.

1. **파일**, **새로 만들기**, **동적 웹 프로젝트**를 차례로 클릭합니다. (**File**, **New**를 차례로 클릭한 후 **Dynamic Web Project**가 사용 가능한 프로젝트로 표시되지 않는 경우 **File**, **New**, **Project...** 를 차례로 클릭한 후 **Web**을 확장하고 **Dynamic Web Project**를 클릭한 후 **Next**를 클릭합니다.)

   ![새로운 동적 웹 프로젝트 만들기][file-new-dynamic-web-project]

2. 이 자습서에서는 프로젝트의 이름을 **MyWebApp**으로 지정합니다. 화면이 다음과 유사하게 나타납니다.
   
   ![새 동적 웹 프로젝트 속성][dynamic-web-project-properties]

3. **Finish**를 클릭합니다.

4. Eclipse의 Project Explorer 뷰 내에서 **MyWebApp**을 확장합니다. **WebContent**를 마우스 오른쪽 단추로 클릭하고 **New**를 클릭한 후 **JSP File**을 클릭합니다.

   ![새 JSP 파일 만들기][create-new-jsp-file]

5. **새 JSP 파일** 대화 상자에서 **index.jsp** 파일의 이름을 지정하고 부모 폴더를 **MyWebApp/WebContent**로 유지한 후 **다음**을 클릭합니다.

   ![새 JSP 파일 대화 상자][new-jsp-file-dialog]

6. **JSP 템플릿 선택** 대화 상자에서 이 자습서의 목적에 따라, **새 JSP 파일(html)** 을 선택한 후 **마침**을 클릭합니다.

   ![JSP 템플릿 선택][select-jsp-template]

7. Eclipse에서 index.jsp 파일이 열리면 **Hello World!** 를 동적으로 표시하도록 텍스트를 추가합니다. 기존 `<body>` 요소 내. 업데이트된 `<body>` 콘텐츠는 다음 예제와 유사하게 표시됩니다.
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. index.jsp를 저장합니다.

## <a name="deploy-your-web-app-to-azure"></a>Azure에 웹앱 배포

1. Eclipse의 Project Explorer 보기 내에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**, **Azure Web App으로 게시**를 차례로 선택합니다.
   
   ![Azure 웹앱으로 게시][publish-as-azure-web-app]

1. **웹앱 배포** 대화 상자가 나타나면 다음 옵션 중 하나를 선택할 수 있습니다.

   * 기존 웹앱이 있으면 기존 웹앱을 선택합니다.

      ![앱 서비스 선택][select-app-service]

   * **새 웹앱 만들기**를 클릭합니다.

      ![App Service 만들기][create-app-service]

      **App Service 만들기** 대화 상자에서 웹앱에 대한 필수 정보를 지정한 후 **만들기**를 클릭합니다.

      ![App Service 만들기 대화 상자][create-app-service-dialog]

1. 웹앱을 선택한 다음 **배포**를 클릭합니다.

   ![앱 서비스 배포][deploy-app-service]

1. 웹앱이 성공적으로 배포되면 도구 키트가 **Azure 활동 로그** 탭 아래에 **게시됨** 상태를 표시하며, 이것은 배포된 웹앱의 URL에 대한 하이퍼링크입니다.

   ![게시 상태][publish-status]

1. 상태 메시지에 제공된 링크를 사용하여 웹앱으로 이동할 수 있습니다.

   ![웹앱 찾아보기][browse-web-app]

1. Azure에 웹앱을 게시한 후에는 마우스 오른쪽 단추로 앱을 클릭하고 상황에 맞는 메뉴에서 옵션 중 하나를 선택하여 앱을 관리할 수 있습니다. 예를 들어 웹앱을 **시작**, **중지** 또는 **삭제**할 수 있습니다.

   ![앱 서비스 관리][manage-app-service]

## <a name="next-steps"></a>다음 단계

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

Azure Web Apps 만들기에 대한 자세한 내용은 [Web Apps 개요]를 참조하세요.

<!-- URL List -->

[Eclipse용 Azure 도구 키트 설치]: azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Web Apps 개요]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->

[browse-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/browse-web-app.png
[file-new-dynamic-web-project]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/file-new-dynamic-web-project.png
[dynamic-web-project-properties]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/dynamic-web-project-properties.png
[create-new-jsp-file]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-new-jsp-file.png
[new-jsp-file-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/new-jsp-file-dialog.png
[select-jsp-template]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-jsp-template.png
[publish-as-azure-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-as-azure-web-app.png
[deploy-web-app-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-web-app-dialog.png
[select-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-app-service.png
[create-app-service-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service-dialog.png
[publish-status]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-status.png
[create-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service.png
[deploy-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-app-service.png
[manage-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/manage-app-service.png
