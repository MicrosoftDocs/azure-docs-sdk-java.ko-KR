---
title: Java용 Azure App Service 라이브러리
description: Azure 관리 API를 사용하여 Azure App Service에서 웹앱을 자동으로 배포합니다.
keywords: Azure, Java, SDK, API, 웹앱, 모바일, App Service
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/09/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: appservice
ms.openlocfilehash: 49063e48ec739b912c418774f531f11b16a3ff1e
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799829"
---
# <a name="azure-app-service-libraries-for-java"></a>Java용 Azure App Service 라이브러리

## <a name="overview"></a>개요

[Azure App Service](/azure/app-service)를 사용하여 웹 사이트, 웹 응용 프로그램 및 REST API를 배포하고 관리합니다.

Azure App Service를 시작하려면 [Azure에서 첫 번째 Java 웹앱 만들기](/azure/app-service-web/app-service-web-get-started-java)를 참조하세요.

## <a name="management-api"></a>관리 API

관리 API를 사용하여 Azure App Service에서 응용 프로그램을 배포, 크기 조정 및 구성합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-appservice</artifactId>
    <version>1.3.0</version>
</dependency>
```   

> [!div class="nextstepaction"]
> [관리 API 탐색](/java/api/overview/azure/appservice/management)

### <a name="example"></a>예

Docker 이미지에서 Linux에서 실행되는 Azure Web App으로 웹앱을 배포합니다.

```java
WebApp app = azure.webApps().define("newLinuxWebApp")
    .withExistingLinuxPlan(myLinuxAppServicePlan)
    .withExistingResourceGroup("myResourceGroup")
    .withPrivateDockerHubImage("username/my-java-app")
    .withCredentials("dockerHubUser","dockerHubPassword")
    .withAppSetting("PORT","8080").
    .create();
```

## <a name="samples"></a>샘플

[FTP 또는 GitHub에서 웹앱 배포][1]  
[배포 슬롯을 사용하여 앱 버전 간 전환][2]  
[사용자 지정 도메인 구성][3]   
[여러 지역에서 웹앱 크기 조정][4]   

앱에서 사용할 수 있는 [Azure App Service용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice)를 추가로 탐색합니다.

[1]: ../docs-ref-conceptual/java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
