---
title: "IntelliJ용 Azure 도구 키트의 새로운 기능"
description: "IntelliJ용 Azure 도구 키트의 최신 기능에 대해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 46ed791f-df59-416a-809e-f52345ad973c
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: 40d93306b840736bd7eb860933cdbfe03c82691c
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-intellij"></a>IntelliJ용 Azure 도구 키트의 새로운 기능

## <a name="azure-toolkit-for-intellij-releases"></a>IntelliJ용 Azure 도구 키트 릴리스
이 문서는 다양한 릴리스 정보 및 IntelliJ용 Azure 도구 키트에 대한 최신 업데이트를 포함합니다.

> [!NOTE]
> 최신 정보는 다음 웹 페이지를 참조하세요.
> 
> <https://github.com/Microsoft/azure-tools-for-java/releases>

> [!NOTE]
> Azure Toolkit for Eclipse IDE이기도합니다. 자세한 내용은 [Eclipse용 Azure 도구 키트 설치]를 참조하세요.
> 
> 

### <a name="april-14-2017"></a>2017년 4월 14일
IntelliJ용 Azure 도구 키트 - 2017년 4월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **향상된 Azure 로그인 환경**: IntelliJ용 Azure 도구 키트에서는 이제 Azure 계정에 로그인하는 두 가지 방법인 *대화형* 및 *자동*을 지원합니다. 자세한 내용은 [IntelliJ용 Azure 도구 키트에 대한 Azure 로그인 지침]을 참조하세요.
* **Docker 컨테이너를 사용한 게시**: 이제 IntelliJ용 Azure 도구 키트를 사용하여 웹 응용 프로그램을 Docker 컨테이너로 게시할 수 있습니다. 자세한 내용은 [IntelliJ용 Azure 도구 키트를 사용하여 웹앱을 Docker 컨테이너로 게시하는 방법]을 참조하세요.
* **Storage 계정 관리**: IntelliJ용 Azure 도구 키트에서는 이제 Azure 탐색기 보기에서 Storage 계정을 관리하도록 지원합니다. 자세한 내용은 [IntelliJ용 Azure 탐색기를 사용하여 Storage 계정 관리]를 참조하세요.
* **관리**: IntelliJ용 Azure 도구 키트에서는 이제 Azure 탐색기 보기에서 가상 컴퓨터를 관리하도록 지원합니다. 자세한 내용은 [IntelliJ용 Azure 탐색기를 사용하여 Virtual Machines 관리]를 참조하세요.
* **원격 디버깅 지원 제거**. Azure App Service의 Java 웹앱에 대한 원격 디버깅 기능이 IntelliJ용 Azure 도구 키트에서 제거되었습니다. 도구 키트 사용 시 발생하는 몇 가지 문제를 해결하기 위해 제거가 필요했습니다.

### <a name="august-26-2016"></a>2016년 8월 26일
IntelliJ용 Azure 도구 키트 - 2016년 8월 릴리스에는 다음과 같은 향상된 기능이 포함되어 있습니다.

* **사용자 지정 JDK 배포**. 이제 IntelliJ용 Azure 도구 키트에서 Azure WebApp 컨테이너에 임의의 JDK 버전을 지정하고 배포하도록 지원합니다.
  * Azure에서 제공하는 JDK 외에도, Azul Systems가 Azure에서 사용할 수 있도록 다양하게 엄선해 놓은 Zulu OpenJDK 버전 중에 선택할 수도 있습니다.
  * 저장소 계정에 ZIP 파일로 업로드하면 자신만의 JDK 배포를 지정할 수도 있습니다.
* **Azure Explorer 보기 향상**:
  * Azure의 새로운 Resource Manager 모델을 사용한 가상 컴퓨터 관리 지원: IDE를 벗어나지 않고 리소스 관리자 기반 가상 컴퓨터를 나열하고, 만들고, 삭제할 수 있습니다.
  * Azure의 Resource Manager를 사용한 Storage 계정 BLOB 관리 지원은 “기본” Storage 계정을 관리하는 기존 기능을 보완합니다.
* **SQL Server용 Microsoft JDBC Driver 6.0**. 이 업데이트는 Microsoft SQL Server(v6.0)용 최신 JDBC 드라이버를 포함하며, 이제 Java 프로젝트에 손쉽게 추가할 수 있는 라이브러리로 포함되기 때문에 이전 버전을 대체합니다.

### <a name="june-29-2016"></a>2016년 6월 29일
IntelliJ용 Azure 도구 키트 - 2016년 6월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **Java 8 요구 사항**. 이제 IntelliJ용 Azure 도구 키트에는 Java 8이 필요하지만 이 요구 사항은 도구 키트에만 해당합니다. 응용 프로그램은 Azure에서 지원되는 모든 버전의 Java를 계속 사용할 수 있습니다.
* **최신 Java JDK에 대한 지원**. 이제 최신 버전의 Java JDK가 IntelliJ용 Azure 도구 키트에서 지원됩니다.
* **Azure SDK v2.9.1에 대한 지원**. 이제 Azure SDK 최신 버전은 IntelliJ용 Azure 도구 키트에 필요한 최소 구성 요소입니다.
* **통합된 샘플**. 이제 IntelliJ용 Azure 도구 키트가 몇 가지 샘플 응용 프로그램을 갖추어 개발자가 사용할 수 있습니다.
* **HDInsight 도구 통합**. 이제 Azure의 HDInsight 도구는 IntelliJ용 Azure 도구 키트와 함께 제공됩니다. 자세한 내용은 [IntelliJ용 HDInsight 도구 플러그 인]을 참조하세요.
* **Java Web Apps의 원격 디버깅**. 이제 IntelliJ용 Azure 도구 키트는 Azure App Service에서 Java 웹앱의 원격 디버깅을 지원합니다.

### <a name="april-12-2016"></a>2016년 4월 12일
IntelliJ용 Azure 도구 키트 - 2016년 4월 릴리스에는 다음과 같은 향상 기능이 포함되어 있습니다.

* **Azure SDK v2.9.0에 대한 지원**. 이제 Azure SDK 최신 버전은 IntelliJ용 Azure 도구 키트에 필요한 최소 구성 요소입니다.
* **Azure 웹앱 지원과 관련된 여러 유용성, 응답성 및 성능 개선**. 도구 키트가 Azure 결과와 통신하는 방법에 있어서 보다 응답성이 뛰어난 UI를 통해 다양한 성능 최적화가 이루어졌습니다.
* **IntelliJ 내에서 Azure의 기존 웹 응용 프로그램 컨테이너를 삭제하는 기능**. 이제 IntelliJ용 Azure 도구 키트를 사용하면 IntelliJ를 종료하지 않고 기존 Azure 웹 컨테이너를 삭제할 수 있습니다.

## <a name="next-steps"></a>다음 단계

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Eclipse용 Azure 도구 키트 설치]: ../eclipse/azure-toolkit-for-eclipse.md

[IntelliJ용 Azure 도구 키트에 대한 Azure 로그인 지침]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[IntelliJ용 Azure 도구 키트를 사용하여 웹앱을 Docker 컨테이너로 게시하는 방법]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[IntelliJ용 Azure 탐색기를 사용하여 Storage 계정 관리]: ./azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer.md
[IntelliJ용 Azure 탐색기를 사용하여 Virtual Machines 관리]: ./azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer.md

[Azure Java Developer Center]: https://docs.microsoft.com/java/azure

[IntelliJ용 HDInsight 도구 플러그 인]: /azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin
