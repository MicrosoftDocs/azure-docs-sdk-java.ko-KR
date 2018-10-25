---
title: Java용 Azure Resource Manager 라이브러리
description: Java용 리소스 관리자 라이브러리에 대한 참조 설명서
keywords: Azure, Java, SDK, API, 리소스 그룹, ARM, 리소스 관리자
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: 7316c05e39bc88c50670dcb0f6331ce8440fd711
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799809"
---
# <a name="azure-resource-manager-libraries-for-java"></a><span data-ttu-id="6eb0e-104">Java용 Azure Resource Manager 라이브러리</span><span class="sxs-lookup"><span data-stu-id="6eb0e-104">Azure Resource Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="6eb0e-105">개요</span><span class="sxs-lookup"><span data-stu-id="6eb0e-105">Overview</span></span>

<span data-ttu-id="6eb0e-106">[Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)를 사용하여 그룹에서 리소스를 배포, 모니터링 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb0e-106">Deploy, monitor, and manage resources in groups with [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-api"></a><span data-ttu-id="6eb0e-107">관리 API</span><span class="sxs-lookup"><span data-stu-id="6eb0e-107">Management API</span></span>

<span data-ttu-id="6eb0e-108">관리 API를 사용하여 리소스 그룹을 만들고, 템플릿에서 리소스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb0e-108">Use the management API to create resource groups and deploy resources from templates.</span></span>

<span data-ttu-id="6eb0e-109">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6eb0e-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-resources</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="6eb0e-110">예</span><span class="sxs-lookup"><span data-stu-id="6eb0e-110">Example</span></span>

<span data-ttu-id="6eb0e-111">Azure Eastern US 지역에 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6eb0e-111">Create a new resource group in the Azure Eastern US region.</span></span>

```java
ResourceGroup resourceGroup = azure.resourceGroups().define("myResourceGroup")
            .withRegion(Region.US_EAST)
            .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6eb0e-112">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="6eb0e-112">Explore the Management APIs</span></span>](/java/api/overview/azure/resources/management)

## <a name="samples"></a><span data-ttu-id="6eb0e-113">샘플</span><span class="sxs-lookup"><span data-stu-id="6eb0e-113">Samples</span></span>

<span data-ttu-id="6eb0e-114">[Java를 사용하여 Azure 리소스 그룹 관리][1] 
[ARM 템플릿을 사용하여 리소스 배포][2]</span><span class="sxs-lookup"><span data-stu-id="6eb0e-114">[Manage Azure Resource Groups with Java][1] 
[Deploy resources using an ARM template][2]</span></span>

[1]: https://github.com/Azure-Samples/resources-java-manage-resource-group
[2]: https://github.com/Azure-Samples/resources-java-deploy-using-arm-template

<span data-ttu-id="6eb0e-115">Azure Resource Manager 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=java&term=resource)을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6eb0e-115">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) of Azure Resource Manager samples.</span></span>
