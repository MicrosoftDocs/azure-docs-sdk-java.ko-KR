---
title: Java용 Azure 관리 라이브러리 릴리스 정보 | Microsoft Docs
description: Java용 Azure 관리 라이브러리에 대한 새 기능과 주요 변경 내용을 확인합니다.
keywords: Azure, Java, API, 참조, 정보, 업데이트, 사용 중단
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 0aaa83ceb42192441decb5972baae56fed337fb2
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48899458"
---
# <a name="release-notes"></a>릴리스 정보 

## <a name="october-5-2017---130"></a>2017년 10월 5일 - 1.3.0 

버전 1.3.0은 이전 릴리스에서 일반 가용성(안정적인) 단계에 도달하도록 서비스 및 기능을 사용하기 위해 이전 버전과 호환 가능합니다.

해당 서비스에 대한 미리 보기 버전의 모든 주요 변경 내용은 @Beta 주석으로 표시됩니다.

코드를 1.3.0으로 마이그레이션하는 경우 [이 정보](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md)를 사용하여 1.3 버전용 기존 코드를 준비할 수 있습니다.

### <a name="generally-availabile-in-v13"></a>V1.3에서 일반적으로 사용 가능

특히 다음과 같은 이전 릴리스에 있던 일부 API도 이제는 GA가 되었습니다.

- 비동기 메서드
- 이전에 베타 버전이었던 모든 CDN 메서드
- 이전에 베타 버전이었던 모든 Application Gateway 메서드 및 인터페이스

  라이브러리의 일부는 여전히 미리 보기로 있습니다. 라이브러리의 현재 상태에 대해 아래 표를 참조하세요.

서비스 또는 기능 | GA로 사용 가능 | 미리 보기로 사용 가능 
---------|---------|---------|-
컴퓨팅  | 가상 머신 및 VM 확장, 가상 머신 확장 집합, 관리 디스크   | Azure 컨테이너 서비스, Azure 컨테이너 레지스트리 
Storage   |  Storage 계정       |    암호화     
SQL Database  | 데이터베이스, 방화벽, 탄력적 풀              
네트워킹    |  가상 네트워크, 네트워크 인터페이스, IP 주소, 라우팅 테이블, 네트워크 보안 그룹, DNS, Traffic Manager, 애플리케이션 게이트웨이  |    부하 분산 장치, 네트워크 피어링, Virtual Network 게이트웨이, 네트워크 감시자 
더 많은 서비스    |  리소스 관리자, Key Vault, Redis, CDN, Batch       |  웹앱, 함수 앱, Service Bus, Graph RBAC, Cosmos DB, 검색  
기본 사항     |   인증 - 코어, 비동기 메서드, 관리되는 서비스 ID      |      |

> 미리 보기 기능은 클래스에서 `@Beta` 주석 또는 라이브러리에서 인터페이스 또는 메서드 수준으로 표시됩니다. 이러한 기능은 변경될 수 있습니다. 나중에 어떤 방식으로든 수정 또는 제거될 수 있습니다.

### <a name="import-with-maven"></a>Maven을 사용하여 가져오기

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a>도움말 가져오기 및 피드백 제공

자신의 코드에 있는 라이브러리를 사용하여 도움말을 얻으려면 [Stack Overflow(영문)](http://stackoverflow.com/questions/tagged/azure-java-sdk) 커뮤니티를 확인해 주세요. 버그가 발생하거나 이러한 라이브러리를 향상시키기 위한 제안 사항이 있으면 [GitHub](https://github.com/Azure/azure-sdk-for-java/issues)를 통해 문제를 제출해 주세요.


