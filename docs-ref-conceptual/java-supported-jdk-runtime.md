---
title: Azure 개발에 대한 Java JDK 및 장기 지원
description: Java 응용 프로그램을 개발하고 실행하는 Azure 지원의 다운로드 및 설명입니다.
author: rloutlaw
manager: angerobe
ms.devlang: java
ms.topic: article
ms.date: 10/15/2017
ms.author: routlaw
ms.openlocfilehash: 2865219f350990e8b07f7d2cd99f536168a6b8d4
ms.sourcegitcommit: 7df2d442ad7cbdb235e5dd35302a9b73379c23d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50026999"
---
# <a name="get-java-jdk-downloads-and-support-when-developing-for-azure"></a>Azure에 대해 개발하는 경우 Java JDK 다운로드 및 지원 가져오기

Azure 및 Azure Stack에서 Java 개발자는 추가 지원 비용 없이 [OpenJDK의 Azul Systems Zulu Enterprise 빌드](https://www.azul.com/downloads/azure-only/zulu/)를 사용하여 프로덕션 Java 응용 프로그램을 빌드하고 실행할 수 있습니다. Azure에서 원하는 모든 Java 런타임을 사용할 수 있지만 Zulu를 사용하는 경우 [정규화된 Azure 지원 계획](https://azure.microsoft.com/support/plans/)을 사용하여 무료 유지 관리 업데이트를 가져오고 Microsoft와 관련된 지원 문제를 만들 수 있습니다.

## <a name="supported-java-versions-and-update-schedule"></a>지원되는 Java 버전 및 업데이트 일정

Azul Systems는 Java SE 7, 8 및 11부터 Java의 모든 LTS(장기 지원) 버전에 대해 완벽하게 지원되는 [Microsoft Azure용 OpenJDK의 Zulu Enterprise 빌드](https://www.azul.com/downloads/azure-only/zulu/)를 제공합니다. 자세한 내용은 [Azul 보도 자료](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack)에서 찾을 수 있습니다.


이러한 JDK 버전에는 분기별 보안 업데이트 및 버그 수정뿐만 아니라 필요에 따라 대역 외 중요 업데이트 및 패치가 포함됩니다.  이 지원에는 Java 11과 같은 Java의 최신 버전에서 보고된 Java 7 및 8에 대한 보안 업데이트 및 버그 수정 이식이 포함되고, 이전 버전의 Java에 대한 지속적인 안정성 및 보안을 보장합니다.  Azure 고객은 계획되지 않은 모든 Java SE 구독 요금이 발생하지 않고 이러한 보안 업데이트 및 플랫폼 버그 수정의 대상이 됩니다. 아래 이미지에서 Java SE의 각 버전에 대한 지원 날짜가 강조 표시됩니다.

![Azure용 JDK 지원 타임라인](media/azure-jdk-support.png)

Azul Systems는 이러한 릴리스에 대한 [Java SE 로드맵](https://www.azul.com/products/azul_support_roadmap/)을 유지 관리합니다.

## <a name="use-for-local-development"></a>로컬 개발을 위해 사용 

개발자는 [Azul Systems 웹 사이트](https://www.azul.com/downloads/azure-only/zulu/)에서 Azure 및 Azure Stack용 Java JDK를 다운로드할 수 있습니다. Windows, Linux 및 macOS에서 다운로드가 지원됩니다. Linux에서 작업하는 개발자는 [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) 및 [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) 패키지 관리자를 통해 패키지를 가져올 수도 있습니다.

[정규화된 Azure 지원 계획](https://azure.microsoft.com/support/plans/)을 사용하여 Azure 또는 Azure Stack용 제품을 개발하는 경우 Azure에서 지원하는 Azul Zulu JDK에 대한 제품 지원이 지원됩니다.

## <a name="use-in-docker-containers"></a>Docker 컨테이너에서 사용

선택한 배포판에서 OpenJDK의 Zulu Enterprise 빌드를 사용하여 무제한 Docker 이미지를 빌드할 수 있습니다. Azure JDK용 Azul Zulu Enterprise를 기반으로 하는 Zulu Docker 이미지는 [Microsoft의 공용 Docker 리포지토리](https://hub.docker.com/r/microsoft/java-jdk/)에서 지원됩니다. 이러한 이미지를 빌드하는 데 사용되는 Dockerfile은 [Microsoft의 Java GitHub 리포지토리](https://github.com/Microsoft/java/tree/master/docker)에서 지원됩니다.

이러한 이미지를 사용하여 앱을 컨테이너화하려면 Dockerfile에서 `FROM` 문을 설정한 다음, 응용 프로그램의 종속성을 사용하여 컨테이너를 구성해야 합니다. 예를 들어, 포트 8080에 바인딩되는 JAR 파일 패키지 Java SE 응용 프로그램을 실행하려면:

```Dockerfile
FROM  microsoft/java-jdk:<tag>
EXPOSE 8080
ADD target/hello.jar hello.jar
ENTRYPOINT ["java", "-jar","/hello.jar"]
```

## <a name="azure-service-runtime-support"></a>Azure 서비스 런타임 지원

[App Service](/azure/app-service/containers/), [Functions](/azure/azure-functions/functions-create-first-java-maven), [Service Fabric](/azure/service-fabric/) 및 [HDInsight](/azure/hdinsight/)와 같은 Azure 플랫폼 서비스는 보안 패치 및 버그 수정이 포함된 부 릴리스의 기본 제공 자동 패치에서 OpenJDK의 Zulu Enterprise 빌드를 사용합니다.