---
title: "Java용 Azure 관리 라이브러리 릴리스 정보 | Microsoft Docs"
description: "Java용 Azure 관리 라이브러리에 대한 새 기능과 주요 변경 내용을 확인합니다."
keywords: "Azure, Java, API, 참조, 정보, 업데이트, 사용 중단"
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: c0d5c4b3702d3bee4e93de51cec36e72aeaf598f
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/09/2017
---
# <a name="release-notes"></a>릴리스 정보 

## <a name="june-30-2017---110"></a>2017년 6월 30일 - 1.1.0 

V1.1은 공용으로 사용하도록 설계되어 V1.0의 일반 가용성(안정) 단계에 도달한 API에서 V1.0 이전 버전과 호환됩니다.

V.0에서 @Beta 주석으로 표시된 API에서 도입된 몇 가지 혁신적인 변경 내용이 있습니다.

코드를 1.1.0으로 마이그레이션하는 경우 [이 정보](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)를 사용하면 1.0.0에서 1.1.0용 코드를 준비할 수 있습니다.

### <a name="generally-availabile-in-v11"></a>V1.1에서 일반적으로 사용 가능한 기능

특히 다음과 같은 V1.0 베타 버전에 있던 일부 API도 이제는 V1.1의 GA가 되었습니다.

- 비동기 메서드
- 이전에 베타 버전이었던 모든 CDN 메서드
- 이전에 베타 버전이었던 모든 응용 프로그램 게이트웨이 메서드 및 인터페이스

 라이브러리의 일부는 여전히 미리 보기로 있습니다. 라이브러리의 현재 상태에 대해 아래 표를 참조하세요.

서비스 또는 기능 | GA로 사용 가능 | 미리 보기로 사용 가능  | 서비스 예정 |
---------|---------|---------|---------|
Compute  | 가상 컴퓨터 및 VM 확장, 가상 컴퓨터 확장 집합, 관리 디스크   | Azure 컨테이너 서비스, Azure 컨테이너 레지스트리 |    |
저장소   |  저장소 계정       |         |   암호화      |
SQL 데이터베이스  | 데이터베이스, 방화벽, 탄력적 풀        |         |   더 많은 기능      |
네트워킹    |  가상 네트워크, 네트워크 인터페이스, IP 주소, 라우팅 테이블, 네트워크 보안 그룹, DNS, Traffic Manager, 응용 프로그램 게이트웨이  |    부하 분산 장치     |   VPN, 네트워크 감시자   |
더 많은 서비스    |  리소스 관리자, Key Vault, Redis, CDN, Batch       |  웹앱, 함수 앱, Service Bus, Graph RBAC, DocumentDB   | 모니터, Scheduler, 함수 관리, 검색, 더 많은 Graph RBAC 기능        |
기본 사항     |   인증 - 코어, 비동기 메서드       |      |         |

### <a name="import-with-maven"></a>Maven을 사용하여 가져오기

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a>도움말 가져오기 및 피드백 제공

자신의 코드에 있는 라이브러리를 사용하여 도움말을 얻으려면 [Stack Overflow(영문)](http://stackoverflow.com/questions/tagged/azure-java-sdk) 커뮤니티를 확인해 주세요. 버그가 발생하거나 이러한 라이브러리를 향상시키기 위한 제안 사항이 있으면 [GitHub](https://github.com/Azure/azure-sdk-for-java/issues)를 통해 문제를 제출해 주세요.

### <a name="migrate-from-previous-releases"></a>이전 릴리스에서 마이그레이션

[1.0.0-beta5에서 마이그레이션(영문)](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md) [1.1.0에서 마이그레이션(영문)](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)


