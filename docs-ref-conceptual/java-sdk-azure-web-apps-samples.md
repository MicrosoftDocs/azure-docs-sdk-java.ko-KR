---
title: "Java 웹앱 샘플용 Azure 관리 라이브러리"
description: "Java용 Azure 관리 라이브러리를 사용하여 App Service에서 호스팅되는 Azure 웹앱을 만들고 업데이트하기 위한 샘플 코드를 얻습니다."
keywords: "Azure, Java, SDK, API, Maven, Gradle, 웹앱, App Service"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 43633e5c-9fb1-4807-ba63-e24c126754e2
ms.openlocfilehash: 2f1e43f3835ffcdb138bf7e29a1656b7ee381281
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-management-libraries-for-java-samples-for-web-apps"></a>Java 웹앱 샘플용 Azure 관리 라이브러리

| **앱 만들기** ||
|---|---|
| [웹앱 만들기 및 FTP 또는 GitHub에서 코드 배포][1] | 로컬 Git, FTP 및 GitHub의 연속 통합에서 웹앱을 배포합니다. |
| [웹앱 만들기 및 배포 슬롯 관리][2] | 웹앱을 만들고, 스테이징 슬롯에 배포한 다음, 슬롯 간에 배포를 교환합니다. |
| **앱 구성** ||
| [웹앱 만들기 및 사용자 지정 도메인 구성][3] | 사용자 지정 도메인 및 자체 서명된 SSL 인증서가 있는 웹앱을 만듭니다. |
| **앱 크기 조정** ||
| [여러 지역에서 항상 사용 가능한 웹앱 크기 조정][4] | Azure Traffic Manager를 사용하여 서로 다른 세 지역의 웹앱 크기를 조정하고 단일 끝점을 통해 사용할 수 있게 합니다. | 
| **리소스에 앱 연결** ||
| [저장소 계정에 웹앱 연결][5] | Azure 저장소 계정을 만들고, 앱 설정에 저장소 계정 연결 문자열을 추가합니다. |
| [SQL 데이터베이스에 웹앱 연결][6] | 웹앱 및 SQL 데이터베이스를 만들고, 앱 설정에 SQL 데이터베이스 연결 문자열을 추가합니다. |

[1]: java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
[5]: https://azure.microsoft.com/resources/samples/app-service-java-manage-storage-connections-for-web-apps/
[6]: https://azure.microsoft.com/resources/samples/app-service-java-manage-data-connections-for-web-apps/