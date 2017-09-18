---
title: "Java용 Azure App Service 라이브러리"
description: "Azure 관리 API를 사용하여 Azure App Service에서 웹앱을 자동으로 배포합니다."
keywords: "Azure, Java, SDK, API, 웹앱, 모바일, App Service"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/09/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: appservice
ms.openlocfilehash: e5d2a66dc984d34fb9a6668d2ea3bf1ee6164e70
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/09/2017
---
# <a name="azure-app-service-libraries-for-java"></a><span data-ttu-id="39c07-104">Java용 Azure App Service 라이브러리</span><span class="sxs-lookup"><span data-stu-id="39c07-104">Azure App Service libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="39c07-105">개요</span><span class="sxs-lookup"><span data-stu-id="39c07-105">Overview</span></span>

<span data-ttu-id="39c07-106">[Azure App Service](/azure/app-service)를 사용하여 웹 사이트, 웹 응용 프로그램 및 REST API를 배포하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="39c07-106">Deploy and manage websites, web applications, and REST APIs with [Azure App Service](/azure/app-service).</span></span>

<span data-ttu-id="39c07-107">Azure App Service를 시작하려면 [Azure에서 첫 번째 Java 웹앱 만들기](/azure/app-service-web/app-service-web-get-started-java)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39c07-107">To get started with Azure App Service, see [Create your first Java web app in Azure](/azure/app-service-web/app-service-web-get-started-java).</span></span>

## <a name="management-api"></a><span data-ttu-id="39c07-108">관리 API</span><span class="sxs-lookup"><span data-stu-id="39c07-108">Management API</span></span>

<span data-ttu-id="39c07-109">관리 API를 사용하여 Azure App Service에서 응용 프로그램을 배포, 크기 조정 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="39c07-109">Deploy, scale, and configure applications in Azure App Service with the management API.</span></span>

<span data-ttu-id="39c07-110">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="39c07-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-appservice</artifactId>
    <version>1.2.1</version>
</dependency>
```   

> [!div class="nextstepaction"]
> [<span data-ttu-id="39c07-111">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="39c07-111">Explore the Management APIs</span></span>](/java/api/overview/azure)

### <a name="example"></a><span data-ttu-id="39c07-112">예제</span><span class="sxs-lookup"><span data-stu-id="39c07-112">Example</span></span>

<span data-ttu-id="39c07-113">Docker 이미지에서 Linux에서 실행되는 Azure Web App으로 웹앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="39c07-113">Deploy a webapp from a Docker image into an Azure Web App running on Linux.</span></span>

```java
WebApp app = azure.webApps().define("newLinuxWebApp")
    .withExistingLinuxPlan(myLinuxAppServicePlan)
    .withExistingResourceGroup("myResourceGroup")
    .withPrivateDockerHubImage("username/my-java-app")
    .withCredentials("dockerHubUser","dockerHubPassword")
    .withAppSetting("PORT","8080").
    .create();
```

## <a name="samples"></a><span data-ttu-id="39c07-114">샘플</span><span class="sxs-lookup"><span data-stu-id="39c07-114">Samples</span></span>

<span data-ttu-id="39c07-115">[FTP 또는 GitHub에서 웹앱 배포][1]</span><span class="sxs-lookup"><span data-stu-id="39c07-115">[Deploy a web app from FTP or GitHub][1]</span></span>  
<span data-ttu-id="39c07-116">[배포 슬롯을 사용하여 앱 버전 간 전환][2]</span><span class="sxs-lookup"><span data-stu-id="39c07-116">[Swap between app versions with deployment slots][2]</span></span>  
<span data-ttu-id="39c07-117">[사용자 지정 도메인 구성][3] </span><span class="sxs-lookup"><span data-stu-id="39c07-117">[Configure a custom domain][3] </span></span>  
<span data-ttu-id="39c07-118">[여러 지역에서 웹앱 크기 조정][4]</span><span class="sxs-lookup"><span data-stu-id="39c07-118">[Scale a web app across multiple regions][4]</span></span>   

<span data-ttu-id="39c07-119">앱에서 사용할 수 있는 [Azure App Service용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="39c07-119">Explore more [sample Java code for Azure App Service](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice) you can use in your apps.</span></span>

[1]: ../docs-ref-conceptual/java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/