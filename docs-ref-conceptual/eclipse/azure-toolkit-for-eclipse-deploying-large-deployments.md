---
title: "대규모 배포"
description: "Eclipse용 Azure 도구 키트를 사용하여 대규모 배포를 배포하는 방법에 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 0e367e74d038043f1626dbf19aab87db6451bc02
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2017
---
# <a name="deploying-large-deployments"></a>대규모 배포

배포가 너무 커서 기본 approot 폴더에 들어가지 않는 경우 로컬 저장소 리소스를 JDK 및 응용 프로그램 서버의 배포 루트 폴더로 사용할 수 있습니다.

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a>로컬 저장소 리소스를 대규모 배포에 대한 배포 루트 폴더로 사용하려면

1. 새 로컬 저장소 리소스를 만듭니다. 리소스의 이름은 중요하지 않습니다. 저장소 리소스는 역할 수준에서 정의됩니다. 다음 단계를 사용하면 가장 빠르게 로컬 저장소 구성 대화 상자에 액세스하여 새 로컬 저장소 리소스를 만들 수 있습니다. **프로젝트 탐색기** 보기에서 역할을 마우스 오른쪽 단추로 클릭하고(역할이 보이지 않는 경우 Azure 프로젝트 노드 확장) **Azure**를 클릭한 다음 **로컬 저장소**를 클릭합니다. **로컬 저장소** 대화 상자에서 **추가**를 클릭하여 새 로컬 저장소 리소스를 만듭니다.

1. 원하는 크기를 2048MB 이상으로 설정합니다. 이보다 크기가 작으면 approot에서 발생했던 것과 같은 파일 크기 문제가 생길 수 있습니다.

1. **역할 인스턴스를 재활용할 때 콘텐츠 정리**가 선택되어 있는지 확인합니다. 선택하면 역할 인스턴스가 재활용되는 경우 배포의 시작 논리 실행 시 리소스에 있는 기존 파일과 충돌하지 않습니다.

1. **배포 후 리소스의 디렉터리 경로를 저장하는 환경 변수** 값이 **DEPLOYROOT** 문자열로 설정되어 있는지 확인합니다. 로컬 저장소 리소스 대화 상자는 다음과 유사합니다.

   ![][ic667943]

또는 **DEPLOYROOT**를 로컬 리소스의 *이름*으로 사용하고 자동으로 생성된 환경 변수 이름을 변경하지 않는 경우(그런 경우 **DEPLOYROOT_PATH**로 설정됨) 응용 프로그램에 대해서도 이처럼 작업합니다.

로컬 저장소 리소스를 만드는 방법에 대한 추가 정보는 [로컬 저장소 속성][Local storage properties]에서 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
