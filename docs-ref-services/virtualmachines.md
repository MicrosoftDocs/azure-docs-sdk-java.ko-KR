---
title: "Java용 Azure Virtual Machine 라이브러리"
description: 
keywords: Azure, Java, SDK, API, Compute , Virtual Machines
author: douge
ms.author: douge
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: compute
ms.openlocfilehash: f9a816d5787e41a4ee4643b1bc66bf21192ea298
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2017
---
# <a name="azure-virtual-machine-libraries"></a>Azure 가상 컴퓨터 라이브러리

## <a name="overview"></a>개요

Linux 또는 Windows를 실행하는 요청 시 확장 가능한 컴퓨팅 리소스입니다.

Azure 가상 컴퓨터를 시작하려면 [Azure Portal을 사용하여 Linux 가상 컴퓨터 만들기](/azure/virtual-machines/linux/quick-create-portal)를 참조하세요.

## <a name="management-api"></a>관리 API

관리 API를 사용하여 코드에서 Azure의 Windows 및 Linux 가상 컴퓨터를 생성, 구성 및 확장할 수 있습니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-compute</artifactId>
    <version>1.3.0</version>
</dependency>
```   


## <a name="example"></a>예제

새 Azure 리소스 그룹에 새 Linux 가상 컴퓨터를 만듭니다.

```java
VirtualMachine newLinuxVm = azure.virtualMachines().define(linuxVmName)
            .withRegion(Region.US_EAST)
            .withNewResourceGroup("myResourceGroup")
            .withNewPrimaryNetwork("10.0.0.0/28")
            .withPrimaryPrivateIpAddressDynamic()
            .withoutPrimaryPublicIpAddress()
            .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
            .withRootUsername(userName)
            .withSshKey(key)
            .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
            .create();
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/java/api/overview/azure/virtualmachines/managementapi)


## <a name="samples"></a>샘플

[가상 컴퓨터 관리][1]   
[가상 네트워크 관리][6]   
[사용자 지정 이미지에서 가상 컴퓨터 만들기][2]   
[지역 간에 동시에 가상 컴퓨터 만들기][5]    
[부하 분산 장치를 사용하여 가상 컴퓨터 확장 집합 만들기][7]    

[1]: ../docs-ref-conceptual/java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[5]: ../docs-ref-conceptual/java-sdk-virtual-machines-in-parallel.md
[6]: ../docs-ref-conceptual/java-sdk-manage-virtual-networks.md
[7]: ../docs-ref-conceptual/java-sdk-manage-vm-scalesets.md

앱에서 사용할 수 있는 [Azure 가상 컴퓨터용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=VM)를 추가로 탐색합니다.