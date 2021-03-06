---
title: IntelliJ용 Azure Explorer를 사용하여 Virtual Machines 관리
description: IntelliJ용 Azure 탐색기를 사용하여 Azure 가상 머신을 관리하는 방법을 알아봅니다.
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/13/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: a3aff77bc2fd2dac0396187d9e6b27910bc60e58
ms.sourcegitcommit: 24f037d133875f86761ec893dfa74e723de040b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53636418"
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a>IntelliJ용 Azure Explorer를 사용하여 Virtual Machines 관리

IntelliJ용 Azure 도구 키트의 일부인 Azure Explorer는 IntelliJ IDE(통합 개발 환경) 내에서 Azure 계정의 Virtual Machines를 관리하기 위한 사용하기 쉬운 솔루션을 Java 개발자에게 제공합니다.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a>IntelliJ에서 가상 머신 만들기

Azure Explorer를 사용하여 가상 머신을 만들려면 다음을 수행합니다. 

1. [IntelliJ용 Azure 도구 키트에 대한 로그인 지침] 문서의 단계를 사용하여 Azure 계정에 로그인합니다.

2. **Azure Explorer** 보기에서 **Azure** 노드를 확장하고 **Virtual Machines**를 마우스 오른쪽 단추로 클릭한 후 **VM 만들기**를 클릭합니다. 

   ![VM 만들기 명령][CR01]  
    **새 Virtual Machine 만들기** 마법사가 열립니다.

3. **구독 선택** 창에서 구독을 선택하고 **다음**을 클릭합니다. 

   ![구독 선택 창][CR02]

4. **Virtual Machine 이미지 선택** 창에서 다음 정보를 입력합니다.

   * **위치**: 가상 머신을 만들 위치(예: *미국 서부*)를 지정합니다. 

   * **권장되는 이미지 크기**: 일반적으로 사용되는 이미지의 요약 목록에서 이미지를 선택하도록 지정합니다.

   * **사용자 지정 이미지**: 다음 정보를 제공하여 사용자 지정 이미지를 선택하도록 지정합니다.

      * **게시자**: 가상 머신에 사용할 이미지를 만든 게시자를 지정합니다(예: *Microsoft*).

      * **제품**: 선택한 게시자에서 사용할 가상 머신 제품을 지정합니다(예: *JDK*).

      * **SKU**: 선택한 제품에서 사용할 SKU(Stockkeeping Unit)를 지정합니다(예: *JDK_8*).

      * **버전 번호**: 선택한 SKU의 사용 버전을 지정합니다.

   ![Virtual Machine 이미지 선택 창][CR03]

5. **다음**을 클릭합니다. 

6. **Virtual Machine 기본 설정** 창에서 다음 정보를 입력합니다.

   * **가상 머신 이름**: 새 가상 머신의 이름을 지정합니다. 이름은 문자로 시작하고 문자, 숫자 및 하이픈만 포함해야 합니다.

   * **크기**: 가상 머신용으로 할당할 코어 수 및 메모리를 지정합니다.

   * **사용자 이름**: 가상 머신 관리용으로 만들 관리자 계정을 지정합니다.

   * **암호** 및 **확인**: 관리자 계정의 암호를 지정합니다.

   ![Virtual Machine 기본 설정 창][CR04]

7. **다음**을 클릭합니다. 

8. **연결된 리소스** 창에서 다음 정보를 입력합니다.

   * **리소스 그룹**: 가상 머신용 리소스 그룹을 지정합니다. 다음 옵션 중 하나를 선택합니다.
      * **새로 만들기**: 새 리소스 그룹을 만들도록 지정합니다.
      * **기존 리소스 사용**: Azure 계정에 연결된 리소스 그룹 목록에서 선택하도록 지정합니다.

       ![연결된 리소스 창][CR07]

   * **스토리지 계정**: 가상 머신 저장용으로 사용할 스토리지 계정을 지정합니다. 기존 저장소 계정을 사용하거나 새 저장소 계정을 만들 수 있습니다. **새로 만들기**를 선택하면 다음 대화 상자가 표시됩니다.

      ![Storage 계정 만들기 대화 상자][CR05]

   * **가상 네트워크** 및 **서브넷**: 가상 머신이 연결될 가상 네트워크 및 서브넷을 지정합니다. 기존 네트워크 및 서브넷을 사용하거나 새 네트워크 및 서브넷을 만들 수 있습니다. **새로 만들기**를 선택하는 경우 다음과 같은 대화 상자가 나타납니다.

      ![Virtual Network 만들기 대화 상자][CR06]

   * **공용 IP 주소**: 가상 머신용 외부 연결 IP 주소를 지정합니다. 새 IP 주소를 만들도록 선택하거나, 가상 머신에 공용 IP 주소가 없는 경우 **(없음)** 을 선택할 수 있습니다. 

   * **네트워크 보안 그룹**: 가상 머신을 위한 선택적 네트워킹 방화벽을 지정합니다. 기존 방화벽을 선택하거나, 가상 머신에서 네트워크 방화벽을 사용하지 않을 경우 **(없음)** 을 선택할 수 있습니다. 

   * **가용성 집합**: 가상 머신이 속할 선택적 가용성 집합을 지정합니다. 기존 가용성 집합을 선택하거나, 새 가용성 집합을 만들거나, 가상 머신이 가용성 집합에 속하지 않을 경우 **(없음)** 을 선택할 수 있습니다.

9. **Finish**를 클릭합니다.  
    새 가상 머신이 Azure Explorer 도구 창에 나타납니다. 

   ![Azure Explorer 보기의 새 가상 머신][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a>IntelliJ에서 가상 머신 다시 시작

IntelliJ에서 Azure Explorer를 사용하여 가상 머신을 다시 시작하려면 다음을 수행합니다.

1. **Azure Explorer** 보기에서 가상 머신을 마우스 오른쪽 단추로 클릭하고 **다시 시작**을 선택합니다.

   ![가상 컴퓨터 다시 시작 명령][RE01]

2. 확인 창에서 **예**를 클릭합니다. 

   ![가상 머신 다시 시작 확인 창][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a>IntelliJ에서 가상 머신 종료

IntelliJ에서 Azure Explorer를 사용하여 가상 머신을 종료하려면 다음을 수행합니다.

1. **Azure Explorer** 보기에서 가상 머신을 마우스 오른쪽 단추로 클릭하고 **종료**를 선택합니다.

   ![가상 컴퓨터 종료 명령][SH01]

2. 확인 창에서 **예**를 클릭합니다. 

   ![가상 머신 종료 확인 창][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a>IntelliJ에서 가상 머신 삭제

IntelliJ에서 Azure Explorer를 사용하여 가상 머신을 삭제하려면 다음을 수행합니다.

1. **Azure Explorer** 보기에서 가상 머신을 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.

   ![가상 컴퓨터 삭제 명령][DE01]

2. 확인 창에서 **예**를 클릭합니다. 

   ![가상 머신 삭제 확인 창][DE02]

## <a name="next-steps"></a>다음 단계

Azure 가상 컴퓨터 크기 및 가격 책정에 대한 자세한 내용은 다음 리소스를 참조하세요.

* Azure Virtual Machines 크기
  * [Azure에서 Windows 가상 머신에 대한 크기]
  * [Azure에서 Linux 가상 머신에 대한 크기]
* Azure Virtual Machines 가격 책정
  * [Windows 가상 컴퓨터 가격 책정]
  * [Linux 가상 컴퓨터 가격 책정]

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[IntelliJ용 Azure 도구 키트에 대한 로그인 지침]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Azure에서 Windows 가상 머신에 대한 크기]: /azure/virtual-machines/virtual-machines-windows-sizes
[Azure에서 Linux 가상 머신에 대한 크기]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows 가상 컴퓨터 가격 책정]: https://azure.microsoft.com/pricing/details/virtual-machines/windows/
[Linux 가상 컴퓨터 가격 책정]: https://azure.microsoft.com/pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
