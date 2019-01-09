---
title: Azure Cosmos DB에서 Spring Data Apache Cassandra API를 사용하는 방법
description: Azure Cosmos DB에서 Spring Data Apache Cassandra API를 사용하는 방법을 알아보세요.
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
ms.openlocfilehash: 1f3f7a55b49d64077df9e7d4d6acc3af4495b424
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992328"
---
# <a name="how-to-use-spring-data-apache-cassandra-api-with-azure-cosmos-db"></a><span data-ttu-id="330ce-103">Azure Cosmos DB에서 Spring Data Apache Cassandra API를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="330ce-103">How to use Spring Data Apache Cassandra API with Azure Cosmos DB</span></span>

## <a name="overview"></a><span data-ttu-id="330ce-104">개요</span><span class="sxs-lookup"><span data-stu-id="330ce-104">Overview</span></span>

<span data-ttu-id="330ce-105">이 문서는 [Spring Data]를 사용하는 샘플 애플리케이션을 만들어 [Azure Cosmos DB Cassandra API](/azure/cosmos-db/cassandra-introduction)를 사용하여 정보를 저장 및 검색하는 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information using the [Azure Cosmos DB Cassandra API](/azure/cosmos-db/cassandra-introduction).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="330ce-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="330ce-106">Prerequisites</span></span>

<span data-ttu-id="330ce-107">이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="330ce-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="330ce-109">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="330ce-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="330ce-110">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="330ce-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="330ce-111">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="330ce-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="330ce-112">[Curl](https://curl.haxx.se/) 또는 기능을 테스트하는 유사한 HTTP 유틸리티.</span><span class="sxs-lookup"><span data-stu-id="330ce-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="330ce-113">[Git](https://git-scm.com/downloads) 클라이언트</span><span class="sxs-lookup"><span data-stu-id="330ce-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="330ce-114">Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="330ce-114">Create an Azure Cosmos DB account</span></span>

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a><span data-ttu-id="330ce-115">Azure Portal을 사용하여 Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="330ce-115">Create a Cosmos DB account using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="330ce-116">Azure Cosmos DB 계정 만들기에 관한 자세한 정보는 [Azure Cosmos DB 설명서](/azure/cosmos-db/)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-116">You can read more detailed information about creating Azure Cosmos DB accounts in [Azure Cosmos DB Documentation](/azure/cosmos-db/).</span></span>

1. <span data-ttu-id="330ce-117"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-117">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="330ce-118">**+리소스 만들기**를 클릭한 다음 **데이터베이스**를 클릭하고 **Azure Cosmos DB**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-118">Click **+Create a resource**, then **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure Cosmos DB 계정 만들기][COSMOSDB01]

1. <span data-ttu-id="330ce-120">다음 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-120">Specify the following information:</span></span>

   - <span data-ttu-id="330ce-121">**구독**: 사용할 Azure 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-121">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="330ce-122">**리소스 그룹**: 새 리소스 그룹을 만들지 기존 리소스 그룹을 선택할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-122">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="330ce-123">**계정 이름**: Cosmos DB 계정의 고유명을 선택합니다. 이 고유명은 *wingtiptoyscassandra.documents.azure.com* 같은 정규화된 도메인 이름을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-123">**Account name**: Choose a unique name for your Cosmos DB account; this will be used to create a fully-qualified domain name like *wingtiptoyscassandra.documents.azure.com*.</span></span>
   - <span data-ttu-id="330ce-124">**API**: 이 자습서의 경우 `Cassandra`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-124">**API**: Specify `Cassandra` for this tutorial.</span></span>
   - <span data-ttu-id="330ce-125">**위치**: 데이터베이스에 가장 가까운 Azure 지역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-125">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Cosmos DB 계정 설정 지정하기][COSMOSDB02]
   
1. <span data-ttu-id="330ce-127">위 정보를 모두 입력하고 **검토 + 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-127">When you have entered all of the above information, click **Review + create**.</span></span>

1. <span data-ttu-id="330ce-128">검토 페이지의 모든 항목이 올바르면, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-128">If everything looks correct on the review page, click **Create**.</span></span>

   ![Cosmos DB 계정 설정 검토하기][COSMOSDB03]

### <a name="add-a-keyspace-to-your-azure-cosmos-db-account"></a><span data-ttu-id="330ce-130">Azure Cosmos DB 계정에 키스페이스 추가하기</span><span class="sxs-lookup"><span data-stu-id="330ce-130">Add a keyspace to your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="330ce-131"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-131">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="330ce-132">**모든 리소스**를 클릭한 다음, 방금 만든Azure Cosmos DB 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-132">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Azure Cosmos DB 계정 선택하기][COSMOSDB04]

1. <span data-ttu-id="330ce-134">**데이터 탐색기**를 클릭한 다음 **새 키스페이스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-134">Click **Data Explorer**, then click **New Keyspace**.</span></span> <span data-ttu-id="330ce-135">**키스페이스 id**의 고유 식별자를 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-135">Enter a unique identifier for your **Keyspace id**, then click **OK**.</span></span>

   ![Cosmos DB 키스페이스 만들기][COSMOSDB05]

### <a name="retrieve-the-connection-settings-for-your-azure-cosmos-db-account"></a><span data-ttu-id="330ce-137">Azure Cosmos DB 계정의 연결 문자열 검색하기</span><span class="sxs-lookup"><span data-stu-id="330ce-137">Retrieve the connection settings for your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="330ce-138"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-138">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="330ce-139">**모든 리소스**를 클릭한 다음, 방금 만든Azure Cosmos DB 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-139">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Azure Cosmos DB 계정 선택하기][COSMOSDB04]

1. <span data-ttu-id="330ce-141">**연결 문자열**을 클릭하고 **접점**, **포트**, **사용자 이름**, 및 **기본 암호** 필드 값을 복사합니다. 이 값은 나중에 애플리케이션을 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-141">Click **Connection strings**, and copy the values for the **Contact Point**, **Port**, **Username**, and **Primary Password** fields; you will use those values to configure your application later.</span></span>

   ![Cosmos DB 연결 문자열 검색하기][COSMOSDB05]

## <a name="configure-the-sample-application"></a><span data-ttu-id="330ce-143">샘플 애플리케이션 구성</span><span class="sxs-lookup"><span data-stu-id="330ce-143">Configure the sample application</span></span>

1. <span data-ttu-id="330ce-144">명령 셸을 열고 다음 예와 같이 git 명령을 사용하여 샘플 프로젝트를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-144">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-cassandra-on-azure.git
   ```

1. <span data-ttu-id="330ce-145">샘플 프로젝트의 *리소스* 디렉터리에서 *application.properties* 파일을 찾거나, 파일이 아직 없는 경우 해당 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-145">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="330ce-146">텍스트 편집기에서 *application.properties* 파일을 열어 파일에 다음 줄을 추가하거나 구성하고 샘플 값을 앞서 다룬 적절한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-146">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.data.cassandra.contact-points=wingtiptoyscassandra.cassandra.cosmosdb.azure.com
   spring.data.cassandra.port=10350
   spring.data.cassandra.username=wingtiptoyscassandra
   spring.data.cassandra.password=********
   ```
   <span data-ttu-id="330ce-147">위치:</span><span class="sxs-lookup"><span data-stu-id="330ce-147">Where:</span></span>

   | <span data-ttu-id="330ce-148">매개 변수</span><span class="sxs-lookup"><span data-stu-id="330ce-148">Parameter</span></span> | <span data-ttu-id="330ce-149">설명</span><span class="sxs-lookup"><span data-stu-id="330ce-149">Description</span></span> |
   |---|---|
   | `spring.data.cassandra.contact-points` | <span data-ttu-id="330ce-150">이 문서에서 앞서 다룬 **접점**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-150">Specifies the **Contact Point** from earlier in this article.</span></span> |
   | `spring.data.cassandra.port` | <span data-ttu-id="330ce-151">이 문서에서 앞서 다룬 **포트**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-151">Specifies the **Port** from earlier in this article.</span></span> |
   | `spring.data.cassandra.username` | <span data-ttu-id="330ce-152">이 문서에서 앞서 다룬 **사용자 이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-152">Specifies your **Username** from earlier in this article.</span></span> |
   | `spring.data.cassandra.password` | <span data-ttu-id="330ce-153">이 문서에서 앞서 다룬 **기본 암호**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-153">Specifies your **Primary Password** from earlier in this article.</span></span> |

1. <span data-ttu-id="330ce-154">*application.properties* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-154">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="330ce-155">샘플 애플리케이션 패키지 및 테스트하기</span><span class="sxs-lookup"><span data-stu-id="330ce-155">Package and test the sample application</span></span> 

1. <span data-ttu-id="330ce-156">다음 예와 같이 Maven을 사용하여 샘플 애플리케이션을 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-156">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="330ce-157">다음 예와 같이 샘플 애플리케이션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-157">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-cassandra-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="330ce-158">다음 예와 같이 명령 프롬프트에서 `curl`을 사용하여 새 레코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-158">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="330ce-159">애플리케이션이 다음과 같이 값을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-159">Your application should return values like the following:</span></span>

   ```shell
   Added Pet{id=60fa8cb0-0423-11e9-9a70-39311962166b, name='dog', species='canine'}.

   Added Pet{id=72c1c9e0-0423-11e9-9a70-39311962166b, name='cat', species='feline'}.
   ```

1. <span data-ttu-id="330ce-160">다음 예와 같이 명령 프롬프트에서 `curl`을 사용하여 모든 기존 레코드 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-160">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="330ce-161">애플리케이션이 다음과 같이 값을 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-161">Your application should return values like the following:</span></span>

   ```json
   [{"id":"60fa8cb0-0423-11e9-9a70-39311962166b","name":"dog","species":"canine"},{"id":"72c1c9e0-0423-11e9-9a70-39311962166b","name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="330ce-162">요약</span><span class="sxs-lookup"><span data-stu-id="330ce-162">Summary</span></span>

<span data-ttu-id="330ce-163">이 자습서에서는, Spring Data를 사용하는 Java 샘플 애플리케이션을 만들어 Azure Cosmos DB Cassandra API를 사용하여 정보를 저장 및 검색했습니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-163">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information using the Azure Cosmos DB Cassandra API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="330ce-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="330ce-164">Next steps</span></span>

<span data-ttu-id="330ce-165">Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="330ce-165">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="330ce-166">Azure의 Spring</span><span class="sxs-lookup"><span data-stu-id="330ce-166">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="330ce-167">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="330ce-167">Additional Resources</span></span>

<span data-ttu-id="330ce-168">Java와 함께 Azure를 사용하는 방법에 관한 자세한 정보는 [Java 개발자용 Azure]와 [Azure DevOps 및 Java 사용하기]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="330ce-168">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[COSMOSDB01]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB05]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-05.png
