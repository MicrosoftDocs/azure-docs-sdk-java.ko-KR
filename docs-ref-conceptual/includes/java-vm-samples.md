---
ms.openlocfilehash: ab31ee32ea940db2d7bcfa2fe36475d8a648bfc9
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592614"
---
| **가상 머신 만들기** || 
|---|---|
| [가상 머신 관리][1] | 가상 머신을 생성, 수정, 시작, 중지 및 삭제합니다. |
| [사용자 지정 이미지에서 가상 컴퓨터 만들기][2] | 사용자 지정 가상 머신 이미지를 만들고, 이를 사용하여 새 가상 머신을 만듭니다. | 
| [스냅숏에서 특수 VHD를 사용하여 가상 머신 만들기][3] | 가상 머신의 OS 및 데이터 디스크에서 스냅숏을 만들고, 스냅숏에서 관리 디스크를 만든 다음, 관리 디스크를 연결하여 가상 머신을 만듭니다. |  
| [동일한 네트워크에서 동시에 가상 머신 만들기][4] | 두 개의 서브넷을 병렬로 사용하여 동일한 가상 네트워크의 동일한 지역에 가상 머신을 만듭니다. |
| [지역 간에 동시에 가상 머신 만들기][5] | 여러 Azure 지역에서 가상 머신 집합을 만들고, 부하를 분산합니다. |
| **네트워크 가상 머신** || 
| [가상 네트워크 관리][6] | 두 개의 서브넷이 있는 가상 네트워크를 설정하고 인터넷 액세스를 제한합니다. |
| **확장 집합 만들기** ||
| [부하 분산 장치를 사용하여 가상 머신 확장 집합 만들기][7] | VM 확장 집합을 만들고, 부하 분산 장치를 설정하고, 확장 집합 VM에 SSH 연결 문자열을 가져옵니다. |

[1]: ../java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[3]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-specialized-disk-from-vhd/
[4]: https://azure.microsoft.com/resources/samples/compute-java-manage-virtual-machines-in-parallel/
[5]: ../java-sdk-virtual-machines-in-parallel.md
[6]: ../java-sdk-manage-virtual-networks.md
[7]: ../java-sdk-manage-vm-scalesets.md