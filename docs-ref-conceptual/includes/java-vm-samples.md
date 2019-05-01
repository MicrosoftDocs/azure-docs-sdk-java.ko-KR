---
ms.openlocfilehash: ab31ee32ea940db2d7bcfa2fe36475d8a648bfc9
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592614"
---
| <span data-ttu-id="4071b-101">**가상 머신 만들기**</span><span class="sxs-lookup"><span data-stu-id="4071b-101">**Create virtual machines**</span></span> || 
|---|---|
| <span data-ttu-id="4071b-102">[가상 머신 관리][1]</span><span class="sxs-lookup"><span data-stu-id="4071b-102">[Manage virtual machines][1]</span></span> | <span data-ttu-id="4071b-103">가상 머신을 생성, 수정, 시작, 중지 및 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4071b-103">Create, modify, start, stop, and delete virtual machines.</span></span> |
| <span data-ttu-id="4071b-104">[사용자 지정 이미지에서 가상 컴퓨터 만들기][2]</span><span class="sxs-lookup"><span data-stu-id="4071b-104">[Create a virtual machine from a custom image][2]</span></span> | <span data-ttu-id="4071b-105">사용자 지정 가상 머신 이미지를 만들고, 이를 사용하여 새 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4071b-105">Create a custom virtual machine image and use it to create new virtual machines.</span></span> | 
| <span data-ttu-id="4071b-106">[스냅숏에서 특수 VHD를 사용하여 가상 머신 만들기][3]</span><span class="sxs-lookup"><span data-stu-id="4071b-106">[Create a virtual machine using specialized VHD from a snapshot][3]</span></span> | <span data-ttu-id="4071b-107">가상 머신의 OS 및 데이터 디스크에서 스냅숏을 만들고, 스냅숏에서 관리 디스크를 만든 다음, 관리 디스크를 연결하여 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4071b-107">Create snapshot from the virtual machine's OS and data disks, create managed disks from the snapshots, and then create a virtual machine by attaching the managed disks.</span></span> |  
| <span data-ttu-id="4071b-108">[동일한 네트워크에서 동시에 가상 머신 만들기][4]</span><span class="sxs-lookup"><span data-stu-id="4071b-108">[Create virtual machines in parallel in the same network][4]</span></span> | <span data-ttu-id="4071b-109">두 개의 서브넷을 병렬로 사용하여 동일한 가상 네트워크의 동일한 지역에 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4071b-109">Create virtual machines in the same region on the same virtual network with two subnets in parallel.</span></span> |
| <span data-ttu-id="4071b-110">[지역 간에 동시에 가상 머신 만들기][5]</span><span class="sxs-lookup"><span data-stu-id="4071b-110">[Create virtual machines across regions in parallel][5]</span></span> | <span data-ttu-id="4071b-111">여러 Azure 지역에서 가상 머신 집합을 만들고, 부하를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="4071b-111">Create and load-balance a set of virtual machines across multiple Azure regions.</span></span> |
| <span data-ttu-id="4071b-112">**네트워크 가상 머신**</span><span class="sxs-lookup"><span data-stu-id="4071b-112">**Network virtual machines**</span></span> || 
| <span data-ttu-id="4071b-113">[가상 네트워크 관리][6]</span><span class="sxs-lookup"><span data-stu-id="4071b-113">[Manage virtual networks][6]</span></span> | <span data-ttu-id="4071b-114">두 개의 서브넷이 있는 가상 네트워크를 설정하고 인터넷 액세스를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="4071b-114">Set up a virtual network with two subnets and restrict Internet access to them.</span></span> |
| <span data-ttu-id="4071b-115">**확장 집합 만들기**</span><span class="sxs-lookup"><span data-stu-id="4071b-115">**Create scale sets**</span></span> ||
| <span data-ttu-id="4071b-116">[부하 분산 장치를 사용하여 가상 머신 확장 집합 만들기][7]</span><span class="sxs-lookup"><span data-stu-id="4071b-116">[Create a virtual machine scale set with a load balancer][7]</span></span> | <span data-ttu-id="4071b-117">VM 확장 집합을 만들고, 부하 분산 장치를 설정하고, 확장 집합 VM에 SSH 연결 문자열을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4071b-117">Create a VM scale set, set up a load balancer, and get SSH connection strings to the scale set VMs.</span></span> |

[1]: ../java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[3]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-specialized-disk-from-vhd/
[4]: https://azure.microsoft.com/resources/samples/compute-java-manage-virtual-machines-in-parallel/
[5]: ../java-sdk-virtual-machines-in-parallel.md
[6]: ../java-sdk-manage-virtual-networks.md
[7]: ../java-sdk-manage-vm-scalesets.md