---
title: Java용 Azure 라이브러리
description: Java용 Azure 관리 및 서비스 라이브러리 개요
keywords: Azure, Java, SDK, API
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 9aaf22a2-382a-4b13-a8e3-0e467d607207
ms.openlocfilehash: 22a337e928085475e905a271f991147729d97671
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892734"
---
# <a name="azure-libraries-for-java"></a>Java용 Azure 라이브러리

Java용 Azure 라이브러리를 사용하면 Azure 리소스를 관리하고 응용 프로그램 코드에서 서비스에 연결할 수 있습니다. 라이브러리는 Java 프로젝트에서 사용할 [Maven 가져오기](java-sdk-azure-install.md)로 사용할 수 있습니다. 

## <a name="manage-azure-resources"></a>Azure 리소스 관리

[Java용 Azure 관리 라이브러리](java-sdk-azure-get-started.md)를 사용하여 Java 응용 프로그램에서 Azure 리소스를 만들고 관리합니다. 이러한 라이브러리를 사용하여 사용자 고유의 Azure 자동화 도구 및 서비스를 빌드합니다. 

예를 들어 Linux VM을 만들려면 다음 코드를 작성합니다.

```java
VirtualMachine linuxVM = azure.virtualMachines().define("myAzureVM")
           .withRegion(region)
           .withExistingResourceGroup("sampleResourceGroup")
           .withNewPrimaryNetwork("10.0.0.0/28")
           .withPrimaryPrivateIpAddressDynamic()
           .withoutPrimaryPublicIpAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withSsh(key)
           .withUnmanagedStorage()
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
 ```

라이브러리의 전체 목록 및 프로젝트로 가져오는 방법에 대한 [설치 지침](java-sdk-azure-install.md)을 검토한 다음 [시작 문서](java-sdk-azure-get-started.md)를 참조하여 인증을 설정하고 자신의 Azure 구독에 대한 샘플 코드를 실행합니다 . 

## <a name="connect-to-azure-services"></a>Azure 서비스에 연결

Java 라이브러리를 사용하여 Azure 내에서 리소스를 만들고 관리하는 것 외에도, Java 라이브러리를 사용하여 앱에서 해당 리소스를 연결하여 사용할 수 있습니다. 예를 들어 SQL Database 테이블을 업데이트하거나 Azure Storage에 파일을 저장할 수 있습니다. [라이브러리 전체 목록](java-sdk-azure-install.md)에서 특정 서비스에 필요한 라이브러리를 선택하고, [Java 개발자 센터](https://azure.microsoft.com/develop/java/)를 방문하여 앱에서 사용하는 데 도움이 되는 자습서와 샘플 코드를 참조합니다.

예를 들어 Azure 저장소 컨테이너에 있는 모든 Blob의 내용을 출력하려면 다음과 같습니다.

```java
// get the container from the blob client
CloudBlobContainer container = blobClient.getContainerReference("blobcontainer");

// For each item in the container
for (ListBlobItem blobItem : container.listBlobs()) {
    // If the item is a blob, not a virtual directory
    if (blobItem instanceof CloudBlockBlob) {
        // Download the text
        CloudBlockBlob retrievedBlob = (CloudBlockBlob) blobItem;
        System.out.println(retrievedBlob.downloadText());
    }
}
```

## <a name="sample-code-and-reference"></a>샘플 코드 및 참조

다음 샘플에는 Java용 Azure 관리 라이브러리를 사용하여 일반적인 자동화 작업을 수행하고 자신의 앱에서 사용할 준비가 된 코드가 있습니다.

- [가상 머신](java-sdk-azure-virtual-machine-samples.md)
- [웹앱](java-sdk-azure-web-apps-samples.md)
- [SQL Database](java-sdk-azure-sql-database-samples.md)
   
[참조](https://docs.microsoft.com/java/api)는 서비스 라이브러리와 관리 라이브러리의 모든 패키지에서 사용할 수 있습니다. 새 기능, 주요 변경 내용 및 이전 버전에서의 마이그레이션 지침은 [릴리스 정보](java-sdk-azure-release-notes.md)에서 사용할 수 있습니다.