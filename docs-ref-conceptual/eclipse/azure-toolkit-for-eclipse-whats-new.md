---
title: "Eclipse용 Azure 도구 키트의 새로운 기능"
description: "Eclipse용 Azure 도구 키트의 최신 기능에 대해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 16b066ea-aae7-4c30-9a12-fa0c3711b93e
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: 31af7e6494f978f341e1f99a30117c57ef30a05b
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-eclipse"></a>Eclipse용 Azure 도구 키트의 새로운 기능

## <a name="azure-toolkit-for-eclipse-releases"></a>Eclipse 릴리스용 Azure 도구 키트
이 문서는 다양한 릴리스 정보 및 Eclipse용 Azure 도구 키트에 대한 최신 업데이트를 포함합니다.

> [!NOTE]
> IntelliJ IDE용 Azure 도구 키트도 있습니다. 자세한 내용은 [IntelliJ용 Azure 도구 키트]를 참조하세요.
> 
> 

### <a name="april-14-2017"></a>2017년 4월 14일
Eclipse용 Azure 도구 키트 - 2017년 4월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **향상된 Azure 로그인 환경**: Eclipse용 Azure 도구 키트에서는 이제 Azure 계정에 로그인하는 두 가지 방법인 *대화형* 및 *자동*을 지원합니다. 자세한 내용은 [Eclipse용 Azure 도구 키트에 대한 Azure 로그인 지침]을 참조하세요.
* **Docker 컨테이너를 사용한 게시**: 이제 Eclipse용 Azure 도구 키트를 사용하여 웹 응용 프로그램을 Docker 컨테이너로 게시할 수 있습니다. 자세한 내용은 [Eclipse용 Azure 도구 키트를 사용하여 웹앱을 Docker 컨테이너로 게시하는 방법]을 참조하세요.
* **저장소 계정 관리**: Eclipse용 Azure 도구 키트에서는 이제 Azure 탐색기 보기에서 저장소 계정을 관리하도록 지원합니다. 자세한 내용은 [Eclipse용 Azure 탐색기를 사용하여 저장소 계정 관리]를 참조하세요.
* **가상 컴퓨터 관리**: Eclipse용 Azure 도구 키트에서는 이제 Azure 탐색기 보기에서 가상 컴퓨터를 관리하도록 지원합니다. 자세한 내용은 [Eclipse용 Azure 탐색기를 사용하여 Virtual Machines 관리]를 참조하세요.
* **원격 디버깅 지원 제거**. Azure App Service의 Java 웹앱에 대한 원격 디버깅 기능이 Eclipse용 Azure 도구 키트에서 제거되었습니다. 도구 키트 사용 시 발생하는 몇 가지 문제를 해결하기 위해 제거가 필요했습니다 .

### <a name="august-26-2016"></a>2016년 8월 26일
Eclipse용 Azure 도구 키트 - 2016년 8월 릴리스에는 다음과 같은 향상된 기능이 포함되어 있습니다.

* **사용자 지정 JDK 배포**. 이제 Eclipse용 Azure 도구 키트에서 Azure WebApp 컨테이너에 임의의 JDK 버전을 지정하고 배포하도록 지원합니다.
  * Azure에서 제공하는 JDK 외에도, Azul Systems가 Azure에서 사용할 수 있도록 다양하게 엄선해 놓은 Zulu OpenJDK 버전 중에 선택할 수도 있습니다.
  * 저장소 계정에 ZIP 파일로 업로드하면 자신만의 JDK 배포를 지정할 수도 있습니다.
* **Azure Explorer 보기 향상**:
  * Azure의 새로운 Resource Manager 모델을 사용한 가상 컴퓨터 관리 지원: IDE를 벗어나지 않고 리소스 관리자 기반 가상 컴퓨터를 나열하고, 만들고, 삭제할 수 있습니다.
  * Azure의 Resource Manager를 사용한 저장소 계정 BLOB 관리 지원은 “기본” 저장소 계정을 관리하는 기존 기능을 보완합니다.
* **SQL Server용 Microsoft JDBC Driver 6.0**. 이 업데이트는 Microsoft SQL Server(v6.0)용 최신 JDBC 드라이버를 포함하며, 이제 Java 프로젝트에 손쉽게 추가할 수 있는 라이브러리로 포함되기 때문에 이전 버전을 대체합니다.

### <a name="june-29-2016"></a>2016년 6월 29일
Eclipse용 Azure 도구 키트 - 2016년 6월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **Java 8 요구 사항**. 이제 Eclipse용 Azure 도구 키트에는 Java 8이 필요하지만 이 요구 사항은 도구 키트에만 해당합니다. 응용 프로그램은 Azure에서 지원되는 모든 버전의 Java를 계속 사용할 수 있습니다.
* **최신 Java JDK에 대한 지원**. 이제 최신 버전의 Java JDK가 Eclipse용 Azure 도구 키트에서 지원됩니다.
* **Azure SDK v2.9.1에 대한 지원**. 이제 Azure SDK 최신 버전은 Eclipse용 Azure 도구 키트에 필요한 최소 구성 요소입니다.
* **통합된 샘플**. 이제 Eclipse용 Azure 도구 키트가 몇 가지 샘플 응용 프로그램을 갖추어 개발자가 사용할 수 있습니다.
* **HDInsight 도구 통합**. 이제 Azure의 HDInsight 도구는 Eclipse용 Azure 도구 키트와 함께 제공됩니다. 자세한 내용은 [Eclipse용 HDInsight 도구 플러그 인]을 참조하세요.
* **Java 웹앱의 원격 디버깅**. 이제 Eclipse용 Azure 도구 키트는 Azure 앱 서비스에서 Java 웹앱의 원격 디버깅을 지원합니다.
* **Eclipse Luna 릴리스에 대한 지원.** 최소한의 새로운 Eclipse IDE 버전은 Luna입니다.

### <a name="april-12-2016"></a>2016년 4월 12일
Eclipse용 Azure 도구 키트 - 2016년 4월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **Azure SDK v2.9.0에 대한 지원**. 이제 Azure SDK 최신 버전은 Eclipse용 Azure 도구 키트에 필요한 최소 구성 요소입니다.
* **Azure 웹앱 지원과 관련된 여러 유용성, 응답성 및 성능 개선**. 도구 키트가 Azure 결과와 통신하는 방법에 있어서 보다 응답성이 뛰어난 UI를 통해 다양한 성능 최적화가 이루어졌습니다.
* **Eclipse 내에서 Azure의 기존 웹 응용 프로그램 컨테이너를 삭제하는 기능**. 이제 Eclipse용 Azure 도구 키트를 사용하면 Eclipse를 종료하지 않고 기존 Azure 웹 컨테이너를 삭제할 수 있습니다.

### <a name="march-7-2016"></a>2016년 3월 7일
Eclipse용 Azure 도구 키트 - 2016년 3월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **간단한 Java 응용 프로그램의 빠른 배포 지원**. Eclipse용 Azure 도구 키트는 Azure 웹앱 컨테이너에 간단한 Java 응용 프로그램의 빠른 배포를 지원하므로 이제는 Java 응용 프로그램 배포를 몇 분이 아닌 몇 초만에 할 수 있습니다.
* **Azure 탐색기 보기를 사용한 웹앱 관리 지원**. 이제 도구 키트의 Azure 탐색기 보기를 통해 Azure 웹앱을 나열하고 시작하고 중지할 수 있습니다.
* **업데이트된 Tomcat, Jetty 및 Zulu OpenJDK 배포판**. Eclipse용 Azure 도구 키트는 Azure 클라우드 서비스로의 Java 배포를 위해 업데이트된 버전의 Tomcat, Jetty 및 Zulu OpenJDK를 지원합니다.

### <a name="january-4-2016"></a>2016년 1월 4일
Eclipse용 Azure 도구 키트 - 2016년 1월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **Zulu OpenJDK 업데이트에 대한 지원**. 자세한 내용은 [Zulu OpenJDK용 Azul Systems 웹 페이지]를 참조하세요.
* **업데이트된 Tomcat 및 Jetty 배포판**. Eclipse용 Azure 도구 키트와 함께 사용할 Microsoft Azure에서 사용할 수 있는 Jetty 및 Tomcat 배포판이 업데이트되었습니다.
* **Azure용 Eclipse 및 IntelliJ 도구 키트 간 기능 패리티**. 이제 Eclipse용 Azure 도구 키트 및 [IntelliJ용 Azure 도구 키트] 는 동일한 기능 집합을 지원합니다.

### <a name="september-1-2015"></a>2015년 9월 1일
Eclipse용 Azure 도구 키트 - 2015년 9월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **Zulu OpenJDK 업데이트에 대한 지원**. 자세한 내용은 [Zulu OpenJDK용 Azul Systems 웹 페이지]를 참조하세요.
* **업데이트된 Tomcat 및 Jetty 배포판**. Eclipse용 Azure 도구 키트와 함께 사용할 Microsoft Azure에서 사용할 수 있는 Jetty 및 Tomcat 배포판이 업데이트되었습니다. (이러한 배포판을 통해 개발자는 빠른 개발을 만들고 Eclipse용 Azure 도구 키트를 사용하여 프로젝트를 테스트할 수 있습니다.
* **자동으로 업데이트되는 Tomcat 및 Jetty 참조에 대한 지원**. Azure에서 사용할 수 있는 특정 버전의 Tomcat 및 Jetty 외에도 개발자는 이제 다음 번에 역할 인스턴스가 재활용되는 각 주요 버전의 Jetty 또는 Tomcat의 최신 배포판으로 자동으로 업데이트되는 "최신(자동 업데이트)"이라는 배포판을 참조할 수 있습니다. (재활용은 자동으로 발생하지만 개발자는 Azure 포털을 통해 재활용을 수동으로 트리거할 수 있습니다.) 이 새로운 기능은 개발자가 서버 소프트웨어 업데이트를 할 수 있도록 응용 프로그램을 다시 배포할 필요가 없음을 의미합니다. (
* 이 기능은 현재 개발 및 테스트 목적 또는 중요하지 않은 업무용 응용 프로그램에만 쓰이며 프로덕션에 권장되지 않습니다.)
* **Azure 저장소의 Blob, 큐 및 테이블에 대한 Azure 탐색기 보기**. 이 기능을 통해 개발자가 Eclipse IDE에서 직접 해당 저장소 아티팩트를 사용하여 일반적인 작업의 집합을 수행할 수 있습니다. 예: Blob 삭제, 업로드 또는 다운로드

### <a name="august-1-2015"></a>2015년 8월 1일
Eclipse용 Azure 도구 키트 - 2015년 8월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **Application Insights 계측 키 관리**. 이 업데이트를 통해 Eclipse IDE에서 직접 Application Insights 계측 키를 획득, 만들기 및 관리할 수 있습니다.
* **SQL Server용 Microsoft JDBC Driver 4.1**. 이 업데이트는 Microsoft SQL Server용 최신 JDBC 드라이버에 대한 지원을 포함합니다.
* **Azure SDK의 버전 2.7**. Azure SDK에 대한 이 최신 업데이트는 Windows에 설치하는 경우 도구 키트에 대한 새로운 필수 구성 요소입니다. (Windows 이외의 운영 체제에는 필요하지 않습니다.)
* **Zulu OpenJDK v7 업데이트에 대한 지원**. 자세한 내용은 [Zulu OpenJDK용 Azul Systems 웹 페이지]를 참조하세요.

### <a name="may-1-2015"></a>2015년 5월 1일
Eclipse용 Azure 도구 키트 - 2015년 5월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **향상된 서버 선택 UI**. 이 릴리스에서 Windows 이외의 운영 체제에서 도구 키트의 사용을 간소화합니다.
* **Maven 프로젝트에 대한 지원**. 이 릴리스에서 도구 키트가 Azure에 배포하고 Application Insights를 구성할 수 있는 응용 프로그램으로 Maven 프로젝트를 지원합니다.
* **Azure SDK의 버전 2.6**. Azure SDK에 대한 이 최신 업데이트는 Windows에 설치하는 경우 도구 키트에 대한 새로운 필수 구성 요소입니다. (Windows 이외의 운영 체제에는 필요하지 않습니다.)
* **다시 게시하는 대신 배포 업그레이드**. 이전 버전이 이미 활성 상태일 때 배포 프로젝트를 다시 게시하는 경우 도구 키트 이제 과거에 했던 것처럼 이전 배포를 종료하고 처음부터 다시 게시하는 대신 Azure의 배포 업그레이드 기능을 사용합니다. 그러면 가능할 때마다 중단 없이 클라우드 서비스를 실행하고 업데이트 중에도 고가용성을 얻을 수 있도록 하며 다시 게시하는 프로세스의 속도를 높입니다.
* **최신 Zulu OpenJDK v8에 대한 지원 - 업데이트 40**. 자세한 내용은 [Zulu OpenJDK용 Azul Systems 웹 페이지]를 참조하세요.

### <a name="march-9-2015"></a>2015년 3월 9일
Eclipse용 Azure 도구 키트 - 2015년 3월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **Mac, Ubuntu 및 추가 Linux 버전에 대한 지원**. Eclipse용 Azure 도구 키트의 이 릴리스는 Mac OS 및 여러 Unix 플랫폼이 대한 지원을 추가하므로 개발자는 Windows 이외의 운영 체제에서 실행되는 Eclipse에서 Azure 클라우드 서비스(PaaS)에 Java 프로젝트를 만들고 구성하고 게시하는 도구 키트를 설치할 수 있습니다.

> [!NOTE]
> 이 기능은 미리 보기이며 프로덕션 환경에서 사용하지 않는 것이 좋습니다. 고객 지원 서비스 수준 규약(SLA)은 없지만 모든 피드백은 환영합니다.
> 
> 

* **새로운 Application Insights 플러그 인**. 이제 개발자는 Azure에서 Application Insights를 사용하여 자동 서버 원격 분석을 구성할 수 있습니다.
* **Ant 기반 명령줄 배포 자동화**. 이 기능을 통해 개발자는 Eclipse 외부에서 Ant를 사용하여 배포의 최신 버전에 대한 게시를 자동화할 수 있습니다. Eclipse에서 처음으로 배포된 후 프로젝트에 대한 미리 생성된 스트립트가 자동으로 구성되고 후속 배포는 명령줄만을 통해 배포를 완전히 자동화하는 스크립트를 사용할 수 있습니다.
* **간단하고 신속한 배포를 위한 Azure에서의 Tomcat 및 Jetty 가용성**. 이제 개발자는 Java 서버를 계정에 업로드(또는 도구 키트를 통해)해야 하는 대신 Azure에서 직접 사용 가능한 다양한 Tomcat 및 Jetty 버전을 참조할 수 있으므로 빠른 시작 시나리오를 위해 Java 서버를 업로드할 필요가 없습니다.
* **Azure 클라우드 서비스에 Java 웹앱을 게시하기 위한 바로 가기 메서드**. 간단한 개발 및 테스트 시나리오를 위한 학습 곡선을 줄이기 위해 개발자는 이제 Azure에 보다 직접적으로 Java 응용 프로그램을 게시할 수 있습니다. Azure 배포 프로젝트를 만들기 및 구성하는 과정을 통해야 하는 대신 Tomcat v8 및 Zulu JVM(OpenJDK)의 기본 인스턴스를 사용하여 응용 프로그램이 배포됩니다.

### <a name="january-30-2015"></a>2015년 1월 30일
Eclipse용 Azure 도구 키트 - 2015년 1월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **IBM® WebSphere® Application Server Liberty Core에 대한 지원**. 이 릴리스는 도구 키트를 Azure에 배포할 수 있는 지원되는 응용 프로그램 서버 목록에 IBM WebSphere Application Server Liberty Core를 추가합니다. 이 최신 추가는 다양한 버전의 Tomcat, Jetty, JBoss 및 GlassFish가 이미 포함되어 있는 도구 키트로 &quot;기본적으로&quot; 지원되는 현재 응용 프로그램 서버 목록을 확장합니다.
* **Application Insights SDK의 포함**. 이 새롭게 출시된 클라이언트 API 라이브러리(v0.9.0)는 Java 용 Azure 라이브러리 패키지에 포함되었습니다.
* **업데이트된 Java용 Azure 라이브러리 패키지**. 이 업데이트는 새로 출시된 Application Insights SDK v 0.9.0 뿐만 아니라 Java v0.7.0 및 저장소 클라이언트 API v2.0.0용 Azure 라이브러리를 포함합니다.

### <a name="november-12-2014"></a>2014년 11월 12일
Eclipse용 Azure 도구 키트 - 2014년 11월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **Azure SDK 2.5에 대한 지원**. Azure SDK에 대한 이 최신 업데이트는 도구 키트에 대한 새로운 필수 구성 요소입니다.
* **Zulu OpenJDK v1.8, v1.7, v1.6 패키지의 업데이트 버전에 대한 지원**. 자세한 내용은 [Zulu OpenJDK용 Azul Systems 웹 페이지]를 참조하세요.
* 향상된 성능과 추가 메모리 리소스를 제공하는 **클라우드 서비스에 대한 새로운 표준 D 크기에 대한 지원**. 자세한 내용은 [Azure를 위한 가상 컴퓨터 및 클라우드 서비스 크기]를 참조하세요.

### <a name="october-17-2014"></a>2014년 10월 17일
Eclipse용 Azure 도구 키트 - 2014년 10월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **클라우드 시나리오에 게시에 대한 성능 향상**. 사용자가 여러 구독 및 저장소 계정을 가진 경우 구독 정보 로드 속도가 훨씬 빠릅니다.
* **Zulu OpenJDK v1.8 패키지의 업데이트 버전에 대한 지원**. 자세한 내용은 [Zulu OpenJDK용 Azul Systems 웹 페이지]를 참조하세요.
* **타사 JDK의 이전 버전 지양에 대한 지원**. 사용되지 않는 JDK 패키지는 더 이상 새 배포 프로젝트에 대한 드롭다운 메뉴에서 표시되지 않습니다. 사용되지 않는 JDK 패키지를 참조하는 기존 프로젝트는 당분간 계속해서 실행 가능하지만 해당 프로젝트가 최신 버전을 사용하도록 업그레이드하는 것이 좋습니다.
* **Java 클라이언트 API 라이브러리용 Azure 라이브러리 패키지의 업데이트 된 버전**. 자세한 내용은 [Microsoft Azure 클라이언트 API]를 참조하세요.
* **버그 수정.** 이 릴리스는 사용자의 보고 및 테스트에 기반한 다양한 버그 수정을 포함합니다.

### <a name="august-5-2014"></a>2014년 8월 5일
Eclipse용 Azure 도구 키트 - 2014년 8월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **Azure SDK 2.4에 대한 지원.** 이전 버전의 Eclipse 도구 키트는 새로 출시된 SDK와 함께 작동하지 않습니다.
* **Zulu OpenJDK v1.6, 1.7 및 v1.8 패키지의 업데이트 버전.** 자세한 내용은 [Zulu OpenJDK용 Azul Systems 웹 페이지]를 참조하세요.
* **Java 클라이언트 API 라이브러리용 Azure 라이브러리 패키지의 업데이트 된 버전.** 자세한 내용은 [Microsoft Azure 클라이언트 API]를 참조하세요.
* **최신 버전의 게시 설정 파일 형식에 대한 지원.** 게시 설정 파일 형식 버전 2.0에 대한 지원이 추가되었습니다.
* **클라우드에 게시 기능의 아키텍처 변경.** 도구 키트는 이제 클라우드에 게시 지원을 위해 새로 출시된 Java용 Microsoft Azure 클라이언트 API를 사용합니다.
* **버그 수정.** 이 릴리스는 다양한 사용자 요청 버그 수정을 포함합니다.

### <a name="june-12-2014"></a>2014년 6월 12일
Eclipse용 Azure 도구 키트 - 2014년 6월 릴리스는 다음과 같은 향상된 기능을 제공하는 몇 가지 서비스 업데이트입니다.

* **Zulu OpenJDK 패키지 v1.8에 대한 지원.** 자세한 내용은 [Zulu OpenJDK용 Azul Systems 웹 페이지]를 참조하세요.
* **Zulu OpenJDK v1.6 및 1.7 패키지의 업데이트 버전.** 자세한 내용은 [Zulu OpenJDK용 Azul Systems 웹 페이지]를 참조하세요.
* **Java 클라이언트 API 라이브러리용 Azure 라이브러리 패키지의 업데이트 된 버전.** 자세한 내용은 [Microsoft Azure 클라이언트 API]를 참조하세요.
* **버그 수정.** 이 릴리스는 다양한 사용자 요청 버그 수정을 포함합니다.

### <a name="april-4-2014"></a>2014년 4월 4일
2014년 4월 - Eclipse용 Azure 플러그 인 릴리스가 출시되었습니다. 필수 구성 요소이며 플러그 인을 설치할 때 자동으로 다운로드되는 Azure SDK 2.3의 출시와 함께 제공되는 업데이트입니다. 이 업데이트는 2014년 2월 미리 보기 이후의 새 기능, 버그 수정 및 일부 피드백 기반 유용성 향상 기능을 포함합니다.

* **Azure SDK 2.3 릴리스에 대한 지원.** 2014년 4월 - Eclipse용 Azure 플러그 인 릴리스는 Azure SDK 2.3이 필요합니다. Azure SDK 2.3이 아직 없는 경우 새 플러그 인을 사용할 때 설치를 허용하라는 메시지가 표시됩니다. 이전 버전의 플러그 인에는 Azure SDK 2.3을 사용하지 마십시오.
* **전체 패키지 배포 없이 응용 프로그램 업그레이드.** 프로젝트의 일부인 Java 응용 프로그램을 배포할 때는 선택한 저장소 계정으로 플러그 인이 자동으로 업로드되므로 전체 패키지를 다시 작성하고 다시 배포할 필요 없이 최신 응용 프로그램 비트를 배포하도록 업데이트하고 역할 인스턴스를 재활용할 수 있습니다.
* **Tomcat 8은 이제 인식된 응용 프로그램 서버입니다.** **Azure 배포 프로젝트** 대화 상자의 **서버** 탭에서 컴퓨터에서 Tomcat 8 설치 디렉터리를 선택하는 경우 플러그 인은 이제 이를 자동으로 감지하고 이미 목록에 있는 이전 버전의 Tomcat과 유사하게 자동으로 Tomcat 8을 배포할 수 있습니다.
* **Azul Zulu OpenJDK 패키지 업데이트: v 1.7 업데이트 51 및 v1.6 업데이트 47.** 이 릴리스와 함께 효과적으로 Azul Systems의 Zulu Openjdk v7 패키지 업데이트 51을 사용할 수 있습니다. 또한 업데이트 47로 시작하는 Zulu Open JDK v6 패키지는 사용할 수 있습니다. 이전에 제공되었던 Zulu Openjdk v7 패키지 업데이트 45, 업데이트 40 및 업데이트 25 이외의 업데이트입니다.
* **A8 및 A9 Microsoft Azure 가상 컴퓨터 크기에 대한 지원.** 이제 높은 메모리 A8 및 A9 가상 컴퓨터 크기에 클라우드 서비스를 배포할 수 있습니다. 이러한 VM 크기에 대한 자세한 내용은 [Azure를 위한 가상 컴퓨터 및 클라우드 서비스 크기]를 참조하세요.
* **SSL 사용 역할에 대한 HTTP에서 HTTPS로 자동 리디렉션.** 클라우드 서비스가 HTTPS 역할만을 포함할 때 사용자 요청이 HTTP를 지정하는 경우 HTTPS로 자동 리디렉션됩니다. HTTP 요청을 처리할 별도의 역할을 만들지 않아도 됩니다.
* **로컬 에뮬레이션에 사용되는 Express 에뮬레이터.** 응용 프로그램을 로컬로 디버깅하는 경우 Azure Express 에뮬레이터는 이제 에뮬레이터로 사용됩니다.
* **Azure는 Microsoft Azure로 변경되었습니다.** 이제 UI 화면은 Azure가 변경되었으며 더 이상 Azure라고 부르지 않는 것을 반영합니다.

### <a name="february-6-2014"></a>2014년 2월 6일
2014년 2월 - Eclipse용 Azure 플러그 인 미리 보기가 출시되었습니다. 이 업데이트는 2013년 10월 미리 보기 이후의 새 기능, 버그 수정 및 일부 피드백 기반 유용성 향상 기능을 포함합니다.

* **SSL 오프로딩에 대한 지원.** SSL(Secure Sockets Layer) 오프로딩은 기능으로 추가되었으며 Java 응용 프로그램 서버에서 SSL을 구성하지 않고 Azure의 Java 배포에서 HTTPS(Hypertext Transfer Protocol Secure) 지원을 손쉽게 사용할 수 있습니다. 이는 특히 세션 선호도 및/또는 인증된 통신 시나리오에 관련됩니다. 예를 들어 도구 키트에서 이미 지원되는 액세스 제어 서비스(ACS) 필터를 사용하는 경우입니다. 자세한 내용은 [SSL 오프로딩] 및 [SSL 오프로딩을 사용하는 방법]을 참조하세요.
* **GlassFish 4는 이제 인식된 응용 프로그램 서버입니다.** **Azure 배포 프로젝트** 대화 상자의 **서버** 탭에서 컴퓨터에서 GlassFish 4 설치 디렉터리를 선택하는 경우 플러그 인은 이제 이를 자동으로 감지하고 이미 목록에 있는 GlassFish OSE 3 버전과 유사하게 자동으로 GlassFish OSE 4를 배포할 수 있습니다.
* **Azul Zulu OpenJDK 패키지 업데이트 45.** 이 릴리스와 함께 효과적으로 Azul Systems의 Zulu(Openjdk v7 패키지) 업데이트 45를 사용할 수 있습니다. 이전에 제공되었던 업데이트 40 및 업데이트 25 이외의 것입니다.
* **개인 끝점 포트를 위한 '자동'에 대한 지원.** Azure가 해당 끝점에 자동으로 포트를 할당하도록 입력 끝점 및 내부 끝점에 대해 자동으로 개인 포트를 설정할 수 있습니다. 이전에는 특정 포트 번호만 할당할 수 있었습니다.
* **자체 서명된 인증서 생성 UI에서 인증서 이름(CN) 사용자 지정에 대한 지원.** 이전에는 모든 새 인증서에 대해 동일한 하드 코드된 이름이 사용되었습니다. 이제 Azure 포털에서 다양한 용도에 사용되는 여러 인증서를 구별할 수 있도록 고유 인증서 이름을 지정할 수 있습니다.
* **Azure 도구 모음:** Azure 도구 모음은 다음 변경 내용으로 업데이트되었습니다. 
  * ![][ic710876]**새 Azure 배포 프로젝트**에 대해 이 아이콘이 추가되었습니다.
  * ![][ic710877] 이 아이콘은 자체 서명된 인증서 만들기 대화 상자에 바로 가기로 추가되었습니다.
* **A5 Azure 가상 컴퓨터 크기에 대한 지원.** 이제 높은 메모리 A5 가상 컴퓨터 크기에 클라우드 서비스를 배포할 수 있습니다. 이 VM 크기에 대한 자세한 내용은 [Azure를 위한 가상 컴퓨터 및 클라우드 서비스 크기]를 참조하세요.
* **Microsoft Windows Server 2012 R2에 대한 지원.** 이제 클라우드 운영 체제로 Windows Server 2012 R2를 선택할 수 있습니다.

### <a name="october-22-2013"></a>2013년 10월 22일
2013년 10월 - Eclipse용 Azure 플러그 인 미리 보기가 출시되었습니다. 이 업데이트는 2013년 9월 미리 보기 이후의 새 기능, 버그 수정 및 일부 피드백 기반 유용성 향상 기능을 포함합니다.

* **Azure SDK 2.2 릴리스에 대한 지원.** 2013년 10월 - Eclipse용 Azure 플러그 인 미리 보기는 Azure SDK 2.2를 지원합니다. 플러그 인은 Azure SDK 2.1에서도 계속 작동하고 Azure SDK 2.1이 아직 설치되지 않은 경우 Azure SDK 2.2를 자동으로 설치합니다.
* **Azul Zulu OpenJDK 패키지 업데이트 40.** 2013년 9월 미리 보기에 발표된 것처럼 이제 플러그 인을 통해 JDK를 직접 업로드하지 않아도 Azure에서 직접 타사 제공 JDK를 사용할 수 있습니다. 2013년 10월 릴리스에서 Azul Systems의 Zulu(Openjdk v7 패키지) 업데이트 40을 사용할 수 있습니다. 원래 게시된 업데이트 25 이외의 것입니다.
* **활동 로그에 있는 클라우드 배포 링크.** Azure 활동 로그 내에서 배포가 **게시됨**의 상태에 있을 때 이제 배포에 대한 링크이므로 **게시됨**을 클릭할 수 있습니다. 그러면 배포가 브라우저에서 열립니다. (**게시됨**의 상태는 이전에 레이블이 지정된 **실행 중**입니다.)
* **게시 시간에 사용 가능한 대상 OS 선택.** **Azure에 게시** 대화 상자는 대상 운영 체제를 설정하도록 보다 쉽게 검색할 수 있는 방법을 제공하는 새 필드, **대상 OS**를 포함합니다.
* **이전 배포 자동 덮어쓰기.** **Azure에 게시** 대화 상자는 새 확인란, **이전 배포 덮어쓰기**를 포함합니다. 이 옵션을 선택하는 경우 새 배포가 게시될 때 이전 배포를 자동으로 덮어씁니다. 이전 배포를 먼저 배포 취소하지 않고 동일한 위치에 게시할 때 &quot;409 충돌&quot; 문제가 발생하지 않습니다.
* **Jetty 9는 이제 인식된 응용 프로그램 서버입니다.** **Azure 배포 프로젝트** 대화 상자의 **서버** 탭에서 컴퓨터에서 Jetty 9 설치 디렉터리를 선택하는 경우 플러그 인은 이제 이를 자동으로 감지하고 이미 목록에 있는 이전 버전의 Jetty와 유사하게 자동으로 Jetty 9를 배포할 수 있습니다.
* **프로젝트 컨텍스트 메뉴에서 역할을 추가합니다.** **Azure** 프로젝트 컨텍스트 메뉴에는 이제 Azure 프로젝트에 새 역할을 추가하기 위해 더 빠르고 더 쉽게 검색 가능한 방법을 제공하는 새 메뉴 항목, **역할 추가**가 포함됩니다.
* **Java 라이브러리용 Azure 라이브러리 패키지에 대한 업데이트.** 이는 [Microsoft Azure 클라이언트 API]를 참조하세요.

### <a name="september-25-2013"></a>2013년 9월 25일
2013년 9월 - Eclipse용 Azure 플러그 인 미리 보기가 출시되었습니다. 이 업데이트는 2013년 8월 미리 보기 이후의 새 기능, 버그 수정 및 일부 피드백 기반 유용성 향상 기능을 포함합니다.

* **Azure에서 사용할 수 있는 Azul Zulu OpenJDK 패키지를 배포하는 기능.** Azure 배포에 사용할 JDK를 지정할 때 새로운 옵션이 추가되었습니다. 이 옵션을 사용하여 직접 업로드할 필요 없이 Azure 클라우드에서 직접 타사 JDK 패키지를 배포할 수 있습니다. Azul Systems는 이제 이 옵션을 사용하여 배포할 수 있는 OpenJDK를 기반으로 한 Zulu라는 첫 번째 패키지를 제공합니다.
* **Java 라이브러리용 Azure 라이브러리 패키지에 대한 업데이트.** 이는 [Microsoft Azure 클라이언트 API]를 참조하세요.

### <a name="august-1-2013"></a>2013년 8월 1일
2013년 8월 - Eclipse용 Azure 플러그 인 미리 보기가 출시되었습니다. 필수 구성 요소이며 플러그 인을 설치할 때 자동으로 다운로드되는 Azure SDK 2.1의 출시와 함께 제공되는 업데이트입니다. 이 업데이트는 2013년 7월 미리 보기 이후의 새 기능, 버그 수정 및 일부 피드백 기반 유용성 향상 기능을 포함합니다.

* **배포 패키지의 일부로 로컬 JDK 및 로컬 응용 프로그램 서버를 포함하는 옵션 제거.** 더 작은 배포 패키지 크기, 더 빠른 배포 시간 및 손쉬운 유지 관리 결과로 항목을 다운로드하므로 패키지에서 이러한 구성 요소를 포함하도록 배포하는 동안 클라우드 저장소에서 JDK 및 응용 프로그램 서버를 다운로드하는 것이 좋습니다. 결과적으로 배포 패키지에서 JDK 및 응용 프로그램 서버를 포함하는 옵션이 제거되었습니다. 배포 패키지의 일부로 로컬 JDK 및 로컬 응용 프로그램 서버를 포함하도록 구성된 기존 프로젝트는 클라우드 저장소에 JDK 및 응용 프로그램 서버를 자동 업로드하도록 자동으로 변환됩니다.
* **Azure SDK 2.1 릴리스에 대한 지원.** 2013년 8월 - Eclipse용 Azure 플러그 인 미리 보기에는 Azure SDK 2.1이 필요합니다. 이전 버전의 Azure SDK와 함께 2013년 8월 미리 보기를 사용하지 마십시오. 이전 버전의 Eclipse용 Azure 플러그 인과 함께 Azure SDK 2.1을 사용하지 마십시오.
* **Eclipse Kepler 릴리스에 대한 지원.** 이와 관련하여 새로운 최소한의 Eclipse IDE 버전은 Indigo입니다. Eclipse용 Azure 플러그 인은 공식적으로 더 이상 Helios에서 테스트되지 않습니다.

### <a name="july-3-2013"></a>2013년 7월 3일
2013년 7월 - Eclipse용 Azure 플러그 인 미리 보기가 출시되었습니다. 이 업데이트는 2013년 5월 미리 보기 이후의 새 기능, 버그 수정 및 일부 피드백 기반 유용성 향상 기능을 포함합니다.

* **새 저장소 계정을 만드는 기능.** **새로 만들기** 단추가 **저장소 계정 추가** 대화 상자에 추가되었습니다. 이 옵션을 사용하면 Azure 관리 포털에 로그인할 필요 없이 Eclipse 플러그 인 내에서 저장소 계정을 만들 수 있습니다. (이 기능을 사용하려면 Azure 구독이 있어야 합니다.) 새 저장소 계정 만들기에 대한 자세한 내용은 [새 저장소 계정 만들기]를 참조하세요.
* **JDK 및 서버의 자동 배포 및 캐싱에 사용되는 저장소 계정에 대한 새로운 &quot;(자동)&quot; 옵션.** JDK 및 응용 프로그램 서버에 대해 **자동으로 업로드**를 사용하는 경우 JDK 및 응용 프로그램 서버를 업로드하거나 Azure 캐싱을 사용할 때 사용하도록 URL 및 저장소 계정에 대해 **(자동)**을 지정할 수 있습니다. 그런 다음 이러한 기능은 **Azure 게시** 대화 상자에서 선택한 것과 동일한 저장소 계정을 자동으로 사용합니다. 새로운 [Eclipse에서 Azure용 Hello World 응용 프로그램 만들기] 옵션을 사용하도록 **(자동)** 자습서가 업데이트되었습니다.
* **Azure 서비스 끝점을 설정하는 기능.** 응용 프로그램이 글로벌 Azure 플랫폼에서 배포되고 관리되는지, 중국의 21Vianet에서 운영하는 Azure인지, 개인 Azure 플랫폼인지 결정하는 서비스 끝점을 지정합니다. 자세한 내용은 [Azure 서비스 끝점]을 참조하세요.
* **대규모 배포는 로컬 저장소 리소스를 지정할 수 있습니다.** 배포가 너무 커서 기본 approot 폴더에 들어가지 않는 경우 이제 로컬 저장소 리소스를 JDK 및 응용 프로그램 서버의 배포 대상으로 지정할 수 있습니다. 자세한 내용은 [대규모 배포]를 참조하세요.
* **A6 및 A7 Azure 가상 컴퓨터 크기에 대한 지원.** 이제 높은 메모리 A6 및 A7 가상 컴퓨터 크기에 클라우드 서비스를 배포할 수 있습니다. 이러한 크기에 대한 자세한 내용은 [Azure를 위한 가상 컴퓨터 및 클라우드 서비스 크기]를 참조하세요.
* **Java 라이브러리용 Azure 라이브러리 패키지에 대한 업데이트.** 이는 [Microsoft Azure 클라이언트 API]를 참조하세요.

### <a name="may-1-2013"></a>2013년 5월 1일
2013년 5월 - Eclipse용 Azure 플러그 인 미리 보기가 출시되었습니다. 필수 구성 요소이며 플러그 인을 설치할 때 자동으로 다운로드되는 Azure SDK 2.0의 출시와 함께 제공되는 주요 업데이트입니다. 이 릴리스는 2013년 2월 미리 보기 이후의 새 기능, 버그 수정 및 일부 피드백 기반 유용성 향상 기능을 포함합니다.

* **Azure 저장소로 JDK 및 응용 프로그램 서버 자동 업로드 및 Azure 저장소에서 배포.** 배포 패키지에 포함하거나 사용자가 수동으로 업로드하는 대신 필요할 때 지정된 Azure 저장소 계정에 선택한 JDK 및 응용 프로그램 서버를 자동으로 업로드하고 해당 위치에서 이러한 구성 요소를 배포하는 새로운 옵션입니다. 이 일반적 요청 기능은 특히 초보자를 위해 JDK 및 서버 구성 요소 배포의 용이성을 크게 향상시킬 수 있습니다. 이러한 옵션을 사용하는 연습의 경우 [Eclipse에서 Azure용 Hello World 응용 프로그램 만들기]를 참조하세요.
* **중앙 집중식 저장소 계정 추적 및 더 쉽게 저장소 계정을 참조하는 기능(드롭다운 컨트롤을 통해).** 이는 JDK 및 서버 구성 요소 배포, 캐싱과 같은 저장소를 사용하는 여러 기능에 적용됩니다. 자세한 내용은 [Azure 저장소 계정 목록]을 참조하세요.
* **클라우드에 게시 마법사에서 간소화된 원격 액세스 설정.** 원격 액세스를 활성화하도록 사용자 이름 및 암호를 입력하거나 원격 액세스를 비활성화 상태로 유지하도록 비워 둡니다.
* **Java 라이브러리용 Azure 라이브러리 패키지에 대한 업데이트.** 이는 [Microsoft Azure 클라이언트 API]를 참조하세요.
* **Windows Server 2012에서 고정 세션에 대한 지원.** 이전에 고정 세션은 Windows Server 2008 R2 에서만 작동했지만 이제는 두 클라우드 운영 체제 대상은 세션 선호도를 지원합니다.
* **패키지 업로드 성능 개선.** JDK 및 응용 프로그램 서버가 배포 패키지에 포함된 경우에도 배포 프로세스의 업로드 부분은 이전 버전에 비해 약 2배 정도 빨라질 수 있습니다.

### <a name="february-8-2013"></a>2013년 2월 8일
2013년 2월 - Eclipse용 Azure 플러그 인 미리 보기가 출시되었습니다. 이 업데이트는 2012년 11월 미리 보기 이후의 버그 수정, 일부 피드백 기반 유용성 향상 및 일부 새 기능을 포함하는 몇 가지 업데이트입니다.

* 클라우드로 배포할 때 배포 패키지에 포함하는 대신 JDK, 응용 프로그램 서버 배포 및 공용 또는 개인 Azure Blob 저장소 다운로드에서 임의의 기타 구성 요소에 대한 지원.
* **Azure 역할 속성**의 **구성 요소** 섹션에서 **위로 이동** 및 **아래로 이동** 단추를 추가하여 역할의 사용자 정의 구성 요소가 처리되는 순서를 변경하는 기능.
* **Java용 Azure 라이브러리 패키지** 라이브러리에 대한 업데이트는 [Microsoft Azure 클라이언트 API]의 버전 0.4.0을 기반으로 합니다.

### <a name="november-5-2012"></a>2012년 11월 5일
2012년 11월 - Eclipse용 Azure 플러그 인 미리 보기가 출시되었습니다. 2012년 9월 미리 보기 이후의 추가 버그 수정 및 피드백 기반 유용성 향상 뿐만 아니라 다양한 새로운 기능이 포함된 주요 업데이트입니다.

* 클라우드 운영 체제로 Microsoft Windows Server 2012에 대한 지원.
* memcached 클라이언트를 위한 Azure 공동 배치된 캐싱 지원에 대한 지원.
* Azure AMQP 기반 메시징 활용을 위한 Apache Qpid JMS 클라이언트 라이브러리 포함.
* 사용자가 프로젝트에 여러 주요 기능: 고정 세션, 캐싱 및 원격 디버깅을 신속하게 사용할 수 있는 기능을 제공하는 끝에 새 페이지로 향상된 **새 프로젝트** 마법사.
* 서버 인스턴스 간의 포트 바인딩 충돌을 방지하도록 계산 에뮬레이터에서 실행하는 경우 역할 인스턴스를 1로 자동 감소.

### <a name="september-28-2012"></a>2012년 9월 28일
2012년 9월 - Eclipse용 Azure 플러그 인 미리 보기가 출시되었습니다. 이 서비스 업데이트는 기존 기능에 일부 피드백 기반 유용성 향상 뿐 아니라 2012년 8월 미리 보기 이후의 다양한 추가 버그 수정을 포함합니다.

* 이전에 해당 운영 체제에서 플러그 인이 제대로 작동하는 것을 방해하는 문제를 해결하는 개발 운영 체제로 Microsoft Windows 8 및 Microsoft Windows Server 2012에 대한 지원.
* 끝점 포트 범위 지정에 대한 향상된 지원.
* 공백이 포함된 파일 경로 관련 버그 수정.
* 역할 관련 구성 설정에 대한 빠른 액세스를 위한 역할 컨텍스트 메뉴 개선.
* **클라우드에 게시** 마법사의 몇 가지 개선 및 다양한 추가 버그 수정.

### <a name="august-28-2012"></a>2012년 8월 28일
2012년 8월 - Eclipse용 Azure 플러그 인 미리 보기가 출시되었습니다. 이 서비스 업데이트는 기존 기능에 여러 피드백 기반 유용성 향상 뿐 아니라 2012년 7월 미리 보기 이후의 추가 버그 수정을 포함합니다.

* Azure Access Control Services Filter 대화 상자 내에서:
  * **서명 인증서를 포함하는 옵션** .
  * **자체 서명된 인증서를 만드는 옵션** . Azure Access Control Services Filter에 대한 자세한 내용은 [Eclipse를 사용하여 Azure 액세스 제어 서비스로 웹 사용자를 인증하는 방법]을 참조하세요.
* Azure 배포 프로젝트 마법사 내에서(역할의 서버 구성 속성 페이지에도 적용됨):
  * **JDK 위치의 자동 검색** (필요한 경우 재정의할 수 있음).
  * **서버 유형의 자동 검색** .

### <a name="july-15-2012"></a>2012년 7월 15일
2012년 7월 - 2012년 6월 릴리스 후 사용자에 의해 발견되거나 보고된 다양한 가장 높은 우선 순위 버그를 해결하는 Eclipse용 Azure 플러그 인 미리 보기가 출시되었습니다. 서비스 업데이트이며 새 기능이 포함되지 않았습니다.

### <a name="june-7-2012"></a>2012년 6월 7일
2012년 6월 - Eclipse용 Azure 플러그 인 CTP가 출시되었습니다. 새로운 기능은 다음과 같습니다.

* **새 Azure 배포 프로젝트 마법사:** 개선된 마법사 UI에서 직접 JDK, Java 응용 프로그램 서버 및 Java 응용 프로그램을 선택할 수 있습니다. 목록에서 선택할 수 있도록 Tomcat 6, Tomcat 7, GlassFish OSE 3, Jetty 7, Jetty 8, JBoss 6, JBoss 7(독립 실행형)이 기본 서버 구성 목록에 포함되었습니다. 또한 서버 구성 목록을 사용자 지정할 수 있습니다. 이 UI 개선은 이전의 기본 방식이었던 압축 파일을 끌어서 놓기 및 시작 스크립트 복사에 대한 대안입니다. 해당 방식은 여전히 제대로 작동하지만 고급 시나리오에 대해서만 사용될 가능성이 있습니다.
* **서버 구성 역할 속성 페이지:** 프로젝트를 만든 후 배포와 연결된 JDK, Java 응용 프로그램 서버 및 응용 프로그램을 쉽게 전환할 수 있습니다. 자세한 내용은 [서버 구성 속성]을 참조하세요.
* **&quot;클라우드에 게시&quot; 마법사:** 이전의 수동 자격 증명 가져오기의 자동화, Azure 관리 포털에 로그인,패키지 등 업로드로 Eclipse에서 직접 Azure에 프로젝트를 배포하는 쉬운 방법을 제공합니다. Azure에 프로젝트를 직접 배포하는 방법의 예제는 [Eclipse에서 Azure용 Hello World 응용 프로그램 만들기]를 참조하세요.
* **Azure 도구 모음:** 다음과 같은 기능을 호출하는 단추가 포함된 Azure 도구 모음을 이제 Eclipse에서 사용할 수 있습니다.
  * ![][ic710879] **Azure 에뮬레이터에서 실행**: 에뮬레이터에서 프로젝트를 실행합니다.
  * ![][ic710880] **Azure 에뮬레이터 재설정**: 에뮬레이터를 재설정합니다.
  * ![][ic710881] **Azure용 클라우드 패키지 빌드**: 배포에 대한 패키지를 컴파일합니다.
  * ![][ic710876] **새 Azure 배포 프로젝트**: 새 Azure 배포 프로젝트를 만듭니다.
  * ![][ic710882] **Azure 클라우드에 게시**: Azure에 프로젝트를 게시합니다.
  * ![][ic710883] **게시 취소**: 배포를 삭제합니다.
  * 이러한 Azure 도구 모음 단추의 대부분은 [Eclipse에서 Azure용 Hello World 응용 프로그램 만들기]에서 사용됩니다.
* **Java용 Azure 라이브러리:** 이제 Eclipse에서 Java 라이브러리용 Azure 라이브러리에 대한 단일 패키지의 일부로 사용할 수 있습니다. 플러그 인 설치를 제공하고 필수 종속성을 포함합니다. Java 프로젝트에 라이브러리에 대한 참조를 추가하고 별도로 어떤 항목도 다운로드할 필요가 없습니다. 자세한 내용은 [Eclipse용 Azure 도구 키트 설치]를 참조하세요.
* **플러그 인 설치 중 SQL Server용 Microsoft JDBC 드라이버 4.0 사용 가능:** 새 플러그 인을 설치하는 동안 최신 버전의 SQL Server용 Microsoft JDBC 드라이버를 설치할 수 있습니다.
* **플러그 인 설치 중 Azure 액세스 제어 서비스 필터 사용 가능:** 도구 키트에 Eclipse 라이브러리로 포함된 이 새 구성 요소를 통해 Java 웹 응용 프로그램에서 Google, Live.com, yahoo!와 같은 다양한 ID 공급자를 사용하여 Azure ACS(액세스 제어 서비스) 인증을 원활하게 활용할 수 있습니다. 사용자가 직접 인증 논리를 작성할 필요가 없고 몇 가지 옵션을 구성하고 필터가 ACS를 사용하여 사용자가 로그인을 하도록 두면 됩니다. 요청 개체 내의 필터로 응용 프로그램에 반환되므로 사용자에게 ID를 기반으로 한 리소스에 대한 액세스를 주는 코드 작성에 주력할 수 있습니다. ACS 필터 사용에 대한 자습서는 [Eclipse를 사용하여 Azure 액세스 제어 서비스로 웹 사용자를 인증하는 방법]을 참조하세요.
* **Azure SDK 1.7 필수 구성 요소의 자동 검색:** 새 Azure 배포 프로젝트를 만들 때 아직 설치되지 않은 경우 Azure SDK 1.7이 자동으로 다운로드됩니다.
* **인스턴스 끝점:** 부하 분산된 역할 인스턴스와의 통신을 위한 직접 포트 끝점 액세스를 허용합니다. [끝점 속성] 페이지를 통해 사용 가능한 끝점 UI를 통해 인스턴스 끝점을 추가할 수 있습니다. 이렇게 하면 다중 인스턴스 배포로 시나리오의 클라우드에서 실행 중인 특정 계산 인스턴스에 대한 원격 디버깅 및 JMX 진단을 사용할 수 있습니다. 
* **구성 요소 UI:** 고급 사용자가 프로젝트의 개별 Azure 역할과 Java 응용 프로그램 프로젝트와 같은 기타 외부 리소스 간 프로젝트 종속성을 쉽게 설정하고 배포 논리를 쉽게 설명할 수 있도록 합니다. 자세한 내용은 [구성 요소 속성]을 참조하세요.
* **프로젝트의 이전 버전의 자동 업그레이드:** 이전 버전의 플러그 인을 사용하여 만든 Azure 프로젝트를 포함하는 작업 영역을 열 때 이전 버전의 프로젝트는 새 릴리스와 호환되지 않으므로 이전 프로젝트가 Eclipse에서 닫힌 것으로 표시됩니다. 이러한 이전 프로젝트 중 하나를 열려고 시도하면 업그레이드 마법사가 시작됩니다. 업그레이드에 동의하는 경우 이름에 추가된 **_Upgraded**로 새 프로젝트가 생성되며 새 릴리스를 사용하도록 자동으로 업데이트됩니다. 필요에 따라 새 프로젝트의 이름을 변경할 수 있습니다. 업그레이드의 일환으로 원래 프로젝트는 수정되지 않습니다(닫힌 상태로 유지됨).

### <a name="december-10-2011"></a>2011년 12월 10일
2011년 12월 - Eclipse용 Azure 플러그 인 CTP가 출시되었습니다. 새로운 기능은 다음과 같습니다.

* **세션 선호도(&quot;고정 세션&quot;) 지원:** 확인한 하나만으로 상태 저장, 클러스터형 Java 응용 프로그램을 사용할 수 있습니다. 자세한 내용은 [세션 선호도]를 참조하세요.
* **미리 작성된 시작 스크립트 샘플:** 프로젝트의 샘플 디렉터리에서 시작 스크립트로 간단히 복사/붙여 넣기할 수 있는 가장 인기 있는 Java 서버(Tomcat, Jetty, JBoss, GlassFish)용
* **실시간 에뮬레이터 시작 출력:** 이제 전용 콘솔 창에서 시작 스크립트에서 모든 단계의 실행을 볼 수 있습니다. Azure에서 실행되므로 스크립트에서 진행률 및 실패를 보여 줍니다.
* **자동, 간단한 java.exe 모니터링:** java.exe가 실행을 중지할 때 배포에 자동으로 포함된 간단하고 미리 만들어진 스크립트를 사용하여 역할 재활용 시킵니다.
* **원격 Java 앱 디버깅 구성 UI:** 실시간으로 단계를 실행하고 Java 코드를 디버깅할 수 있도록 에뮬레이터 또는 Azure 클라우드에서 실행 중인 Java 앱에 액세스하는 Eclipse의 원격 디버거를 손쉽게 사용하도록 허용합니다. 자세한 내용은 [Eclipse에서 Azure 응용 프로그램 디버깅]을 참조하세요.
* **로컬 저장소 리소스 구성 UI:** XML을 직접 조작하여 로컬 리소스를 구성할 필요가 없습니다. 또한 이 기능을 사용하면 시작 스크립트에서 직접 참조할 수 있는 환경 변수를 통해 배포된 후에 로컬 리소스의 실제 파일 경로에 액세스할 수 있습니다. 자세한 내용은 [로컬 저장소 속성]을 참조하세요.
* **환경 변수 구성 UI:** 구성 XML 수동 편집을 통해 환경 변수를 설정할 필요가 없습니다. 자세한 내용은 [환경 변수 속성]을 참조하세요.
* **SQL Azure용 JDBC 드라이버:** SQL Azure에 대한 손쉬운 프로그래밍을 사용하여 매끄럽게 통합된 Eclipse 라이브러리로 플러그 인을 통해 설치됩니다. 
* **역할 구성 UI에 대한 빠른 컨텍스트 메뉴 액세스**: 역할 폴더를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.
* **사용자 지정 Azure 프로젝트 및 역할 폴더 아이콘:** 작업 영역 및 프로젝트 내에서 명확하고 쉬운 탐색을 위한 것입니다.

## <a name="next-steps"></a>다음 단계

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[IntelliJ용 Azure 도구 키트]: ../intellij/azure-toolkit-for-intellij.md
[Eclipse용 Azure 도구 키트 설치]: azure-toolkit-for-eclipse-installation.md

[Eclipse용 Azure 도구 키트에 대한 Azure 로그인 지침]: azure-toolkit-for-eclipse-sign-in-instructions.md
[Eclipse용 Azure 도구 키트를 사용하여 웹앱을 Docker 컨테이너로 게시하는 방법]: ./azure-toolkit-for-eclipse-publish-as-docker-container.md
[Eclipse용 Azure 탐색기를 사용하여 저장소 계정 관리]: ./azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer.md
[Eclipse용 Azure 탐색기를 사용하여 Virtual Machines 관리]: ./azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer.md

[Azure Java Developer Center]: https://docs.microsoft.com/java/azure

[Zulu OpenJDK용 Azul Systems 웹 페이지]: http://go.microsoft.com/fwlink/?LinkId=402457
[Azure 서비스 끝점]: http://go.microsoft.com/fwlink/?LinkID=699526
[Azure 저장소 계정 목록]: http://go.microsoft.com/fwlink/?LinkID=699528
[구성 요소 속성]: http://go.microsoft.com/fwlink/?LinkID=699525#components_properties
[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기]: http://go.microsoft.com/fwlink/?LinkID=699533
[Eclipse에서 Azure 응용 프로그램 디버깅]: http://go.microsoft.com/fwlink/?LinkID=699535
[대규모 배포]: http://go.microsoft.com/fwlink/?LinkID=699536
[끝점 속성]: http://go.microsoft.com/fwlink/?LinkID=699525#endpoints_properties
[환경 변수 속성]: http://go.microsoft.com/fwlink/?LinkID=699525#environment_variables_properties
[Eclipse용 HDInsight 도구 플러그 인]: /azure/hdinsight/hdinsight-apache-spark-eclipse-tool-plugin
[Eclipse를 사용하여 Azure 액세스 제어 서비스로 웹 사용자를 인증하는 방법]: http://go.microsoft.com/fwlink/?LinkID=264703
[SSL 오프로딩을 사용하는 방법]: http://go.microsoft.com/fwlink/?LinkID=699545
[로컬 저장소 속성]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties
[Microsoft Azure 클라이언트 API]: http://go.microsoft.com/fwlink/?LinkId=280397
[서버 구성 속성]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[세션 선호도]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL 오프로딩]: http://go.microsoft.com/fwlink/?LinkID=699549
[새 저장소 계정 만들기]: http://go.microsoft.com/fwlink/?LinkID=699528#create_new
[Azure를 위한 가상 컴퓨터 및 클라우드 서비스 크기]: http://go.microsoft.com/fwlink/?LinkId=466520

<!-- IMG List -->

[ic710876]: media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710877]: media/azure-toolkit-for-eclipse-whats-new/ic710877.png
[ic710879]: media/azure-toolkit-for-eclipse-whats-new/ic710879.png
[ic710880]: media/azure-toolkit-for-eclipse-whats-new/ic710880.png
[ic710881]: media/azure-toolkit-for-eclipse-whats-new/ic710881.png
[ic710876]: media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710882]: media/azure-toolkit-for-eclipse-whats-new/ic710882.png
[ic710883]: media/azure-toolkit-for-eclipse-whats-new/ic710883.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh694270.aspx -->
