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
ms.openlocfilehash: 326357e5b4667cc06a6058cb29e9685428174dee
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823686"
---
# <a name="azure-resource-manager-libraries-for-java"></a>Java용 Azure Resource Manager 라이브러리

## <a name="overview"></a>개요

[Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)를 사용하여 그룹에서 리소스를 배포, 모니터링 및 관리합니다.

## <a name="management-api"></a>관리 API

관리 API를 사용하여 리소스 그룹을 만들고, 템플릿에서 리소스를 배포합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-resources</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a>예

Azure Eastern US 지역에 새 리소스 그룹을 만듭니다.

```java
ResourceGroup resourceGroup = azure.resourceGroups().define("myResourceGroup")
            .withRegion(Region.US_EAST)
            .create();
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/java/api/overview/azure/resources/management)

## <a name="samples"></a>샘플

[Java를 사용하여 Azure 리소스 그룹 관리][1] 
[ARM 템플릿을 사용하여 리소스 배포][2]

[1]: https://github.com/Azure-Samples/resources-java-manage-resource-group
[2]: https://github.com/Azure-Samples/resources-java-deploy-using-arm-template

Azure Resource Manager 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=java&term=resource)을 봅니다.
