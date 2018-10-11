---
title: Java 웹앱 샘플용 Azure 관리 라이브러리
description: Java용 Azure 관리 라이브러리를 사용하여 App Service에서 호스팅되는 Azure 웹앱을 만들고 업데이트하기 위한 샘플 코드를 얻습니다.
keywords: Azure, Java, SDK, API, Maven, Gradle, 웹앱, App Service
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 43633e5c-9fb1-4807-ba63-e24c126754e2
ms.openlocfilehash: 2f1e43f3835ffcdb138bf7e29a1656b7ee381281
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893034"
---
# <a name="azure-management-libraries-for-java-samples-for-web-apps"></a><span data-ttu-id="be50f-104">Java 웹앱 샘플용 Azure 관리 라이브러리</span><span class="sxs-lookup"><span data-stu-id="be50f-104">Azure management libraries for Java samples for web apps</span></span>

| <span data-ttu-id="be50f-105">**앱 만들기**</span><span class="sxs-lookup"><span data-stu-id="be50f-105">**Create an app**</span></span> ||
|---|---|
| <span data-ttu-id="be50f-106">[웹앱 만들기 및 FTP 또는 GitHub에서 코드 배포][1]</span><span class="sxs-lookup"><span data-stu-id="be50f-106">[Create a web app and deploy from FTP or GitHub][1]</span></span> | <span data-ttu-id="be50f-107">로컬 Git, FTP 및 GitHub의 연속 통합에서 웹앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="be50f-107">Deploy web apps from local Git, FTP, and continuous integration from GitHub.</span></span> |
| <span data-ttu-id="be50f-108">[웹앱 만들기 및 배포 슬롯 관리][2]</span><span class="sxs-lookup"><span data-stu-id="be50f-108">[Create a web app and manage deployment slots][2]</span></span> | <span data-ttu-id="be50f-109">웹앱을 만들고, 스테이징 슬롯에 배포한 다음, 슬롯 간에 배포를 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="be50f-109">Create a web app and deploy to staging slots, and then swap deployments between slots.</span></span> |
| <span data-ttu-id="be50f-110">**앱 구성**</span><span class="sxs-lookup"><span data-stu-id="be50f-110">**Configure app**</span></span> ||
| <span data-ttu-id="be50f-111">[웹앱 만들기 및 사용자 지정 도메인 구성][3]</span><span class="sxs-lookup"><span data-stu-id="be50f-111">[Create a web app and configure a custom domain][3]</span></span> | <span data-ttu-id="be50f-112">사용자 지정 도메인 및 자체 서명된 SSL 인증서가 있는 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be50f-112">Create a web app with a custom domain and self-signed SSL certificate.</span></span> |
| <span data-ttu-id="be50f-113">**앱 크기 조정**</span><span class="sxs-lookup"><span data-stu-id="be50f-113">**Scale apps**</span></span> ||
| <span data-ttu-id="be50f-114">[여러 지역에서 항상 사용 가능한 웹앱 크기 조정][4]</span><span class="sxs-lookup"><span data-stu-id="be50f-114">[Scale a web app with high availability across multiple regions][4]</span></span> | <span data-ttu-id="be50f-115">Azure Traffic Manager를 사용하여 서로 다른 세 지역의 웹앱 크기를 조정하고 단일 엔드포인트를 통해 사용할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="be50f-115">Scale a web app in three different geographical regions and make them available through a single endpoint using Azure Traffic Manager.</span></span> | 
| <span data-ttu-id="be50f-116">**리소스에 앱 연결**</span><span class="sxs-lookup"><span data-stu-id="be50f-116">**Connect app to resources**</span></span> ||
| <span data-ttu-id="be50f-117">[저장소 계정에 웹앱 연결][5]</span><span class="sxs-lookup"><span data-stu-id="be50f-117">[Connect a web app to a storage account][5]</span></span> | <span data-ttu-id="be50f-118">Azure 저장소 계정을 만들고, 앱 설정에 저장소 계정 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="be50f-118">Create an Azure storage account and add the storage account connection string to the app settings.</span></span> |
| <span data-ttu-id="be50f-119">[SQL 데이터베이스에 웹앱 연결][6]</span><span class="sxs-lookup"><span data-stu-id="be50f-119">[Connect a web app to a SQL database][6]</span></span> | <span data-ttu-id="be50f-120">웹앱 및 SQL 데이터베이스를 만들고, 앱 설정에 SQL 데이터베이스 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="be50f-120">Create a web app and SQL database, and then add the SQL database connection string to the app settings.</span></span> |

[1]: java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
[5]: https://azure.microsoft.com/resources/samples/app-service-java-manage-storage-connections-for-web-apps/
[6]: https://azure.microsoft.com/resources/samples/app-service-java-manage-data-connections-for-web-apps/