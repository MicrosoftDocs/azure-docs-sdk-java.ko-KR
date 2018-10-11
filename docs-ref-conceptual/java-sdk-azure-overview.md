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
# <a name="azure-libraries-for-java"></a><span data-ttu-id="33fd2-104">Java용 Azure 라이브러리</span><span class="sxs-lookup"><span data-stu-id="33fd2-104">Azure libraries for Java</span></span>

<span data-ttu-id="33fd2-105">Java용 Azure 라이브러리를 사용하면 Azure 리소스를 관리하고 응용 프로그램 코드에서 서비스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33fd2-105">The Azure libraries for Java help you manage Azure resources and connect to services from your application code.</span></span> <span data-ttu-id="33fd2-106">라이브러리는 Java 프로젝트에서 사용할 [Maven 가져오기](java-sdk-azure-install.md)로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33fd2-106">The libraries are available as [Maven imports](java-sdk-azure-install.md) for use in your Java projects.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="33fd2-107">Azure 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="33fd2-107">Manage Azure resources</span></span>

<span data-ttu-id="33fd2-108">[Java용 Azure 관리 라이브러리](java-sdk-azure-get-started.md)를 사용하여 Java 응용 프로그램에서 Azure 리소스를 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="33fd2-108">Create and manage Azure resources from your Java applications using the [Azure management libraries for Java](java-sdk-azure-get-started.md).</span></span> <span data-ttu-id="33fd2-109">이러한 라이브러리를 사용하여 사용자 고유의 Azure 자동화 도구 및 서비스를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="33fd2-109">Use these libraries to build your own Azure automation tools and services.</span></span> 

<span data-ttu-id="33fd2-110">예를 들어 Linux VM을 만들려면 다음 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="33fd2-110">For example, to create a Linux VM you would write the following code:</span></span>

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

<span data-ttu-id="33fd2-111">라이브러리의 전체 목록 및 프로젝트로 가져오는 방법에 대한 [설치 지침](java-sdk-azure-install.md)을 검토한 다음 [시작 문서](java-sdk-azure-get-started.md)를 참조하여 인증을 설정하고 자신의 Azure 구독에 대한 샘플 코드를 실행합니다 .</span><span class="sxs-lookup"><span data-stu-id="33fd2-111">Review the [install instructions](java-sdk-azure-install.md) for a full list of the libraries and how to import them into your projects and then read the [get started article](java-sdk-azure-get-started.md) to set up your authentication and run sample code against your own Azure subscription.</span></span> 

## <a name="connect-to-azure-services"></a><span data-ttu-id="33fd2-112">Azure 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="33fd2-112">Connect to Azure services</span></span>

<span data-ttu-id="33fd2-113">Java 라이브러리를 사용하여 Azure 내에서 리소스를 만들고 관리하는 것 외에도, Java 라이브러리를 사용하여 앱에서 해당 리소스를 연결하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33fd2-113">In addition to using Java libraries to create and manage resources within Azure, you can also use Java libraries to connect  and use those resources in your apps.</span></span> <span data-ttu-id="33fd2-114">예를 들어 SQL Database 테이블을 업데이트하거나 Azure Storage에 파일을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33fd2-114">For example, you might update a table SQL Database or store files in Azure Storage.</span></span> <span data-ttu-id="33fd2-115">[라이브러리 전체 목록](java-sdk-azure-install.md)에서 특정 서비스에 필요한 라이브러리를 선택하고, [Java 개발자 센터](https://azure.microsoft.com/develop/java/)를 방문하여 앱에서 사용하는 데 도움이 되는 자습서와 샘플 코드를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="33fd2-115">Select the library you need for a particular service from the [complete list of libraries](java-sdk-azure-install.md) and visit the [Java developer center](https://azure.microsoft.com/develop/java/) for tutorials and sample code for help using them in your apps.</span></span>

<span data-ttu-id="33fd2-116">예를 들어 Azure 저장소 컨테이너에 있는 모든 Blob의 내용을 출력하려면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="33fd2-116">For example, to print out the contents of every blob in an Azure storage container:</span></span>

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

## <a name="sample-code-and-reference"></a><span data-ttu-id="33fd2-117">샘플 코드 및 참조</span><span class="sxs-lookup"><span data-stu-id="33fd2-117">Sample code and reference</span></span>

<span data-ttu-id="33fd2-118">다음 샘플에는 Java용 Azure 관리 라이브러리를 사용하여 일반적인 자동화 작업을 수행하고 자신의 앱에서 사용할 준비가 된 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33fd2-118">The following samples cover common automation tasks with the Azure management libraries for Java and have code ready to use in your own apps:</span></span>

- [<span data-ttu-id="33fd2-119">가상 머신</span><span class="sxs-lookup"><span data-stu-id="33fd2-119">Virtual machines</span></span>](java-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="33fd2-120">웹앱</span><span class="sxs-lookup"><span data-stu-id="33fd2-120">Web apps</span></span>](java-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="33fd2-121">SQL Database</span><span class="sxs-lookup"><span data-stu-id="33fd2-121">SQL Database</span></span>](java-sdk-azure-sql-database-samples.md)
   
<span data-ttu-id="33fd2-122">[참조](https://docs.microsoft.com/java/api)는 서비스 라이브러리와 관리 라이브러리의 모든 패키지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33fd2-122">A [reference](https://docs.microsoft.com/java/api) is available for all packages in both the service and management libraries.</span></span> <span data-ttu-id="33fd2-123">새 기능, 주요 변경 내용 및 이전 버전에서의 마이그레이션 지침은 [릴리스 정보](java-sdk-azure-release-notes.md)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33fd2-123">New features, breaking changes, and migration instructions from previous versions are available in the [release notes](java-sdk-azure-release-notes.md).</span></span>