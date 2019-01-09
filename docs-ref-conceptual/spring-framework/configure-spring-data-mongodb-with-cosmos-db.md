---
title: Azure Cosmos DB에서 Spring Data MongoDB API를 사용하는 방법
description: Azure Cosmos DB에서 Spring Data MongoDB API를 사용하는 방법을 알아보세요.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 55fb356820e2cc5eb8d1fe4030053d9e580583af
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992401"
---
# <a name="how-to-use-spring-data-mongodb-api-with-azure-cosmos-db"></a><span data-ttu-id="4d866-103">Azure Cosmos DB에서 Spring Data MongoDB API를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="4d866-103">How to use Spring Data MongoDB API with Azure Cosmos DB</span></span>

## <a name="overview"></a><span data-ttu-id="4d866-104">개요</span><span class="sxs-lookup"><span data-stu-id="4d866-104">Overview</span></span>

<span data-ttu-id="4d866-105">이 문서는 [Spring Data]를 사용하여 샘플 애플리케이션을 만들어 [Azure Cosmos DB MongoDB API](/azure/cosmos-db/mongodb-introduction)를 사용하여 정보를 저장 및 검색하는 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information using the [Azure Cosmos DB MongoDB API](/azure/cosmos-db/mongodb-introduction).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d866-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4d866-106">Prerequisites</span></span>

<span data-ttu-id="4d866-107">이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="4d866-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="4d866-109">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="4d866-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="4d866-110">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d866-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="4d866-111">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="4d866-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="4d866-112">[Git](https://git-scm.com/downloads) 클라이언트</span><span class="sxs-lookup"><span data-stu-id="4d866-112">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="4d866-113">Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="4d866-113">Create an Azure Cosmos DB account</span></span>

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a><span data-ttu-id="4d866-114">Azure Portal을 사용하여 Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="4d866-114">Create a Cosmos DB account using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="4d866-115">Azure Cosmos DB 계정 만들기에 관한 자세한 정보는 [Azure Cosmos DB 설명서](/azure/cosmos-db/)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-115">You can read more detailed information about creating Azure Cosmos DB accounts in [Azure Cosmos DB Documentation](/azure/cosmos-db/).</span></span>

1. <span data-ttu-id="4d866-116"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-116">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="4d866-117">**+리소스 만들기**를 클릭한 다음 **데이터베이스**를 클릭하고 **Azure Cosmos DB**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-117">Click **+Create a resource**, then **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure Cosmos DB 계정 만들기][COSMOSDB01]

1. <span data-ttu-id="4d866-119">다음 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-119">Specify the following information:</span></span>

   - <span data-ttu-id="4d866-120">**구독**: 사용할 Azure 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-120">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="4d866-121">**리소스 그룹**: 새 리소스 그룹을 만들지 기존 리소스 그룹을 선택할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-121">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="4d866-122">**계정 이름**: Cosmos DB 계정의 고유명을 선택합니다. 이 고유명은 *wingtiptoysmongodb.documents.azure.com* 같은 정규화된 도메인 이름을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-122">**Account name**: Choose a unique name for your Cosmos DB account; this will be used to create a fully-qualified domain name like *wingtiptoysmongodb.documents.azure.com*.</span></span>
   - <span data-ttu-id="4d866-123">**API**: 이 자습서의 경우 `Azure Cosmos DB for MongoDB API`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-123">**API**: Specify `Azure Cosmos DB for MongoDB API` for this tutorial.</span></span>
   - <span data-ttu-id="4d866-124">**위치**: 데이터베이스에 가장 가까운 Azure 지역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-124">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Cosmos DB 계정 설정 지정하기][COSMOSDB02]
   
1. <span data-ttu-id="4d866-126">위 정보를 모두 입력하고 **검토 + 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-126">When you have entered all of the above information, click **Review + create**.</span></span>

1. <span data-ttu-id="4d866-127">검토 페이지의 모든 항목이 올바르면, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-127">If everything looks correct on the review page, click **Create**.</span></span>

   ![Cosmos DB 계정 설정 검토하기][COSMOSDB03]

### <a name="retrieve-the-connection-string-for-your-azure-cosmos-db-account"></a><span data-ttu-id="4d866-129">Azure Cosmos DB 계정의 연결 문자열 검토하기</span><span class="sxs-lookup"><span data-stu-id="4d866-129">Retrieve the connection string for your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="4d866-130"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-130">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="4d866-131">**모든 리소스**를 클릭한 다음, 방금 만든Azure Cosmos DB 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-131">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Azure Cosmos DB 계정 선택하기][COSMOSDB04]

1. <span data-ttu-id="4d866-133">**연결 문자열**을 클릭하고 **기본 연결 문자열** 필드 값을 복사합니다. 나중에 응용 프로그램을 구성할 때 이 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-133">Click **Connection strings**, and copy the value for the **Primary Connection String** field; you will use that value to configure your application later.</span></span>

   ![Cosmos DB 연결 문자열 검색하기][COSMOSDB06]

## <a name="configure-the-sample-application"></a><span data-ttu-id="4d866-135">샘플 애플리케이션 구성</span><span class="sxs-lookup"><span data-stu-id="4d866-135">Configure the sample application</span></span>

1. <span data-ttu-id="4d866-136">명령 셸을 열고 다음 예와 같이 git 명령을 사용하여 샘플 프로젝트를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-136">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/spring-guides/gs-accessing-data-mongodb.git
   ```

1. <span data-ttu-id="4d866-137">동일 프로젝트의 *&lt;project root&gt;/complete/src/main* 디렉터리에 *리소스* 디렉터리를 만들고, *리소스* 디렉터리에 *application.properties* 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-137">Create a *resources* directory in the *&lt;project root&gt;/complete/src/main* directory of the sample project, and create an *application.properties* file in the *resources* directory.</span></span>

1. <span data-ttu-id="4d866-138">텍스트 편집기에서 *application.properties* 파일을 열어 파일에 다음 줄을 추가하고 샘플 값을 앞서 다룬 적절한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-138">Open the *application.properties* file in a text editor, and add the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.data.mongodb.database=wingtiptoysmongodb
   spring.data.mongodb.uri=mongodb://wingtiptoysmongodb:AbCdEfGhIjKlMnOpQrStUvWxYz==@wingtiptoysmongodb.documents.azure.com:10255/?ssl=true&replicaSet=globaldb
   ```
   <span data-ttu-id="4d866-139">위치:</span><span class="sxs-lookup"><span data-stu-id="4d866-139">Where:</span></span>

   | <span data-ttu-id="4d866-140">매개 변수</span><span class="sxs-lookup"><span data-stu-id="4d866-140">Parameter</span></span> | <span data-ttu-id="4d866-141">설명</span><span class="sxs-lookup"><span data-stu-id="4d866-141">Description</span></span> |
   |---|---|
   | `spring.data.mongodb.database` | <span data-ttu-id="4d866-142">이 문서에서 앞서 다룬 Cosmos DB 계정의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-142">Specifies the name of your Cosmos DB account from earlier in this article.</span></span> |
   | `spring.data.mongodb.uri` | <span data-ttu-id="4d866-143">이 문서에서 앞서 다룬 **기본 연결 문자열**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-143">Specifies the **Primary Connection String** from earlier in this article.</span></span> |

1. <span data-ttu-id="4d866-144">*application.properties* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-144">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="4d866-145">샘플 애플리케이션 패키지 및 테스트하기</span><span class="sxs-lookup"><span data-stu-id="4d866-145">Package and test the sample application</span></span> 

1. <span data-ttu-id="4d866-146">다음 예와 같이 Maven을 사용하여 샘플 애플리케이션을 컴파일하고 테스트를 건너뛰도록 Maven을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-146">Build the sample application with Maven, and configure Maven to skip tests; for example:</span></span>

   ```shell
   mvn clean package -DskipTests
   ```

1. <span data-ttu-id="4d866-147">다음 예와 같이 샘플 애플리케이션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-147">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/gs-accessing-data-mongodb-0.1.0.jar
   ```
    
   <span data-ttu-id="4d866-148">애플리케이션이 다음과 같이 값을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-148">Your application should return values like the following:</span></span>

   ```json
   Customers found with findAll():
   -------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customer[id=5c1b4ae4d0b5080ac105cc14, firstName='Bob', lastName='Smith']
   
   Customer found with findByFirstName('Alice'):
   --------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customers found with findByLastName('Smith'):
   --------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customer[id=5c1b4ae4d0b5080ac105cc14, firstName='Bob', lastName='Smith']
   ```

## <a name="summary"></a><span data-ttu-id="4d866-149">요약</span><span class="sxs-lookup"><span data-stu-id="4d866-149">Summary</span></span>

<span data-ttu-id="4d866-150">이 자습서에서는, Spring Data를 사용하는 Java 샘플 애플리케이션을 만들어 Azure Cosmos DB MongoDB API를 사용하여 정보를 저장 및 검색했습니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-150">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information using the Azure Cosmos DB MongoDB API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d866-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d866-151">Next steps</span></span>

<span data-ttu-id="4d866-152">Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4d866-152">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4d866-153">Azure의 Spring</span><span class="sxs-lookup"><span data-stu-id="4d866-153">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="4d866-154">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="4d866-154">Additional Resources</span></span>

<span data-ttu-id="4d866-155">Java와 함께 Azure를 사용하는 방법에 관한 자세한 정보는 [Java 개발자용 Azure]와 [Azure DevOps 및 Java 사용하기]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d866-155">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<!-- URL List -->

[Java 개발자용 Azure]: /java/azure/
[Azure for Java Developers]: /java/azure/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Azure DevOps 및 Java 사용하기]: /azure/devops/
[Working with Azure DevOps and Java]: /azure/devops/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Data]: https://spring.io/projects/spring-data
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[COSMOSDB01]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB06]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-06.png
