---
title: Azure Cosmos DB SQL API에서 Spring Data Gremlin Starter를 사용하는 방법
description: Azure Cosmos DB SQL API에서 Spring Boot Initializer를 사용하여 만든 응용 프로그램을 구성하는 방법에 대해 알아봅니다.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 08/20/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 0976f4b0c13ce5c577458f2974f5dce123bf7e59
ms.sourcegitcommit: 77dc6c03a2e6264df688d91a04fc6b40950779ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43241139"
---
# <a name="how-to-use-the-spring-data-gremlin-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="69284-103">Azure Cosmos DB SQL API에서 Spring Data Gremlin Starter를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="69284-103">How to use the Spring Data Gremlin Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="69284-104">개요</span><span class="sxs-lookup"><span data-stu-id="69284-104">Overview</span></span>

<span data-ttu-id="69284-105">Spring 데이터 Gremlin Starter는 개발자가 Gremlin 호환 데이터 저장소에서 사용할 수 있는 Apache의 Gremlin 쿼리 언어에 대한 Spring 데이터 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-105">The Spring Data Gremlin Starter provides Spring Data support for the Gremlin query language from Apache, which developers can use with any Gremlin-compatible data store.</span></span>

<span data-ttu-id="69284-106">이 문서에서는 Gremlin API와 함께 사용할 Azure Portal을 사용하여 Azure Cosmos DB를 만들고, **[Spring Initializr]** 를 사용하여 사용자 지정 java 응용 프로그램을 만들고, Spring Data Gremlin Starter 기능을 사용자 지정 응용 프로그램에 추가하여 데이터를 저장하고 Gremlin을 사용하여 Azure Cosmos DB에서 데이터를 검색하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="69284-106">This article demonstrates creating an Azure Cosmos DB by using the Azure portal for use with Gremlin API, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Data Gremlin Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using Gremlin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69284-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="69284-107">Prerequisites</span></span>

<span data-ttu-id="69284-108">이 문서의 단계를 수행하기 위해 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-108">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="69284-109">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-109">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="69284-110">[JDK(Java Development Kit)](http://www.oracle.com/technetwork/java/javase/downloads/), 버전 1.7 이상</span><span class="sxs-lookup"><span data-stu-id="69284-110">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="69284-111">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="69284-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="69284-112">이 문서의 단계를 완료하려면 Spring Boot 버전 2.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-cosmos-db-using-the-azure-portal"></a><span data-ttu-id="69284-113">Azure Portal을 사용하여 Azure Cosmos DB 만들기</span><span class="sxs-lookup"><span data-stu-id="69284-113">Create an Azure Cosmos DB using the Azure portal</span></span>

### <a name="create-your-azure-cosmos-database-for-use-with-gremlin-api"></a><span data-ttu-id="69284-114">Gremlin API에 사용할 Azure Cosmos 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="69284-114">Create your Azure Cosmos Database for use with Gremlin API</span></span>

1. <span data-ttu-id="69284-115">Azure Portal(<https://portal.azure.com/>)로 이동하고 **+리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-115">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![리소스 만들기][AZ01]

1. <span data-ttu-id="69284-117">**데이터베이스**를 클릭한 후 **Azure Cosmos DB**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-117">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure Cosmos DB 만들기][AZ02]

1. <span data-ttu-id="69284-119">**Azure Cosmos DB** 페이지에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-119">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="69284-120">고유한 **ID**를 입력합니다. 이 항목은 데이터베이스의 Gremlin URI의 일부로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-120">Enter a unique **ID**, which you will use as part of the Gremlin URI for your database.</span></span> <span data-ttu-id="69284-121">예를 들어 **ID**로 **wingtiptoysdata**를 입력한 경우, Gremlin URI는 *wingtiptoysdata.gremlin.cosmosdb.azure.com*입니다.</span><span class="sxs-lookup"><span data-stu-id="69284-121">For example: if you entered **wingtiptoysdata** for the **ID**, the Gremlin URI would be *wingtiptoysdata.gremlin.cosmosdb.azure.com*.</span></span>
   * <span data-ttu-id="69284-122">API로 **Gremlin(그래프)** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-122">Choose **Gremlin (Graph)** for the API.</span></span>
   * <span data-ttu-id="69284-123">데이터베이스에 사용하려는 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-123">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="69284-124">데이터베이스에 새 **리소스 그룹**을 만들지 아니면 기존 리소스 그룹을 선택할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-124">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="69284-125">데이터베이스의 **위치**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-125">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="69284-126">이러한 옵션을 지정한 경우 **만들기**를 클릭하여 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69284-126">When you have specified these options, click **Create** to create your database.</span></span>

   ![Azure Cosmos DB 옵션 지정][AZ03]

1. <span data-ttu-id="69284-128">데이터베이스를 만든 경우 Azure **대시보드** 뿐 아니라 **모든 리소스** 및 **Azure Cosmos DB** 페이지에도 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="69284-128">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="69284-129">해당 위치 중 하나에서 데이터베이스를 클릭하여 캐시에 대한 속성 페이지를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-129">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![모든 리소스][AZ04]

1. <span data-ttu-id="69284-131">데이터베이스에 대한 속성 페이지가 표시되면 **액세스 키**를 클릭하고 데이터베이스에 대한 URI 및 액세스 키를 복사합니다. 이러한 값은 Spring Boot 응용 프로그램에서 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69284-131">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![액세스 키][AZ05]

### <a name="add-a-graph-to-your-azure-cosmos-database"></a><span data-ttu-id="69284-133">Azure Cosmos 데이터베이스에 그래프를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-133">Add a graph to your Azure Cosmos Database</span></span>

1. <span data-ttu-id="69284-134">**데이터 탐색기**를 클릭한 다음 **새 그래프**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-134">Click **Data Explorer**, and then click **New Graph**.</span></span>

   ![새 그래프][AZ06]

1. <span data-ttu-id="69284-136">**그래프 추가**가 표시되면 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-136">When the **Add Graph** is displayed, enter the following information:</span></span>

   * <span data-ttu-id="69284-137">데이터베이스에 대해 고유한 **데이터베이스 id**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-137">Specify a unique **Database id** for your database.</span></span>
   * <span data-ttu-id="69284-138">그래프 대해 고유한 **그래프 id**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-138">Specify a unique **Graph id** for your graph.</span></span>
   * <span data-ttu-id="69284-139">**저장소 용량**을 지정하도록 선택할 수 있으며 기본값을 적용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-139">You can choose to specify your **Storage capacity**, or you can accept the default.</span></span>
   * <span data-ttu-id="69284-140">**전체**를 지정합니다. 본 예제의 경우 400 요청 단위(RU)를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-140">Specify your **Throughout**, and for this example you can choose 400 Request Units (RUs).</span></span>
   
   <span data-ttu-id="69284-141">이러한 옵션을 지정한 경우 **OK**를 클릭하여 그래프를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69284-141">When you have specified these options, click **OK** to create your graph.</span></span>

   ![그래프 추가][AZ07]

1. <span data-ttu-id="69284-143">그래프를 만든 후 **데이터 탐색기**를 사용하여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-143">After your graph has been created, you can use the **Data Explorer** to view it.</span></span>

   ![Graph 속성 표시][AZ08]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="69284-145">Spring Initializr를 사용하여 간단한 Spring Boot 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="69284-145">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="69284-146"><https://start.spring.io/>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-146">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="69284-147">**Java**에서 **Maven** 프로젝트를 생성한다고 지정하고, 응용 프로그램 **그룹** 및 **아티팩트** 이름을 입력한 다음, 2.0 이상의 **Spring Boot** 버전을 지정하고 **프로젝트를 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-147">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, specify your **Spring Boot** version with a version that is equal to or greater than 2.0, and then click **Generate Project**.</span></span>

   ![기본 Spring Initializr 옵션][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="69284-149">Spring Initializr는 **그룹** 및 **아티팩트** 이름을 사용하여 패키지 이름을 만듭니다(예: \*com.example.wintiptoysdata).</span><span class="sxs-lookup"><span data-stu-id="69284-149">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: \*com.example.wintiptoysdata.</span></span>
   >

1. <span data-ttu-id="69284-150">메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-150">When prompted, download the project to a path on your local computer.</span></span>

   ![사용자 지정 Spring Boot 프로젝트 다운로드][SI02]

1. <span data-ttu-id="69284-152">로컬 시스템에서 파일의 압축을 푼 후에 단순한 Spring Boot 응용 프로그램을 편집할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-152">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![사용자 지정 Spring Boot 프로젝트 파일][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-spring-data-gremlin-starter"></a><span data-ttu-id="69284-154">Spring Data Gremlin Starter를 사용하도록 Spring Boot 앱 구성</span><span class="sxs-lookup"><span data-stu-id="69284-154">Configure your Spring Boot app to use the Spring Data Gremlin Starter</span></span>

1. <span data-ttu-id="69284-155">앱의 디렉터리에서 *pom.xml* 파일을 찾습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="69284-155">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="69284-156">또는</span><span class="sxs-lookup"><span data-stu-id="69284-156">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![pom.xml 파일 찾기][PM01]

1. <span data-ttu-id="69284-158">텍스트 편집기에서 *pom.xml* 파일을 열고 Spring Data Gremlin Starter를 `<dependencies>` 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-158">Open the *pom.xml* file in a text editor, and add the Spring Data Gremlin Starter to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.spring.data.gremlin</groupId>
      <artifactId>spring-data-gremlin</artifactId>
      <version>2.0.0</version>
   </dependency>
   ```

   ![pom.xml 파일 편집][PM02]

1. <span data-ttu-id="69284-160">*pom.xml* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-160">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="69284-161">Azure Cosmos DB를 사용하도록 Spring Boot 앱 구성</span><span class="sxs-lookup"><span data-stu-id="69284-161">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="69284-162">앱의 *리소스* 디렉터리를 찾아*application.yml*라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69284-162">Locate the *resources* directory of your app, and create a new file named *application.yml*.</span></span> <span data-ttu-id="69284-163">예: </span><span class="sxs-lookup"><span data-stu-id="69284-163">For example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.yml`

   <span data-ttu-id="69284-164">또는</span><span class="sxs-lookup"><span data-stu-id="69284-164">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.yml`

   ![application.yml 파일을 만듭니다.][RE01]

1.  <span data-ttu-id="69284-166">텍스트 편집기에서 *application.yml* 파일을 찾고 파일에 다음 줄을 추가하고 샘플 값을 데이터베이스의 적절한 속성으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="69284-166">Open the *application.yml* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   gremlin:
      endpoint: wingtiptoys.gremlin.cosmosdb.azure.com
      port: 443
      username: /dbs/wingtiptoysdb/colls/wingtiptoysgraph
      password: 57686f6120447564652c20426f6220526f636b73==
      telemetryAllowed: false
   ```
   <span data-ttu-id="69284-167">위치:</span><span class="sxs-lookup"><span data-stu-id="69284-167">Where:</span></span>
   | <span data-ttu-id="69284-168">필드</span><span class="sxs-lookup"><span data-stu-id="69284-168">Field</span></span> | <span data-ttu-id="69284-169">설명</span><span class="sxs-lookup"><span data-stu-id="69284-169">Description</span></span> |
   | ---|---|
   | `endpoint` | <span data-ttu-id="69284-170">이 자습서의 앞부분에서 Azure Cosmos DB를 만들 때 지정한 고유한 **ID**에서 파생된 데이터베이스의 Gremlin URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-170">Specifies the Gremlin URI for your database, which is derived from the unique **ID** that you specified when you created your Azure Cosmos DB earlier in this tutorial.</span></span> |
   | `port` | <span data-ttu-id="69284-171">TCP/IP 포트를 지정합니다. HTTPS의 경우 **443**입니다.</span><span class="sxs-lookup"><span data-stu-id="69284-171">Specifies the TCP/IP port, which should be **443** for HTTPS.</span></span> |
   | `username` | <span data-ttu-id="69284-172">이 자습서의 앞부분에 그래프를 추가할 때 사용한 고유한 **데이터베이스 id**와 **그래프 id**를 지정합니다. "/dbs/**{Database id}**/colls/ **{Graph id}**"구문을 사용하여 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-172">Specifies the unique **Database id** and **Graph id** that you used when you added your graph earlier in this tutorial; this must be entered using the following syntax: "/dbs/**{Database id}**/colls/**{Graph id}**".</span></span> |
   | `password` | <span data-ttu-id="69284-173">이 자습서의 앞부분에서 복사한 기본 또는 보조 **액세스 키**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-173">Specifies either the primary or secondary **Access key** that you copied earlier in this tutorial.</span></span> |
   | `telemetryAllowed` | <span data-ttu-id="69284-174">원격 분석을 사용하려는 경우 **true**를, 그렇지 않으면 **false**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-174">Specify **true** if you want to enable telemetry; otherwise, **false**.</span></span>

1. <span data-ttu-id="69284-175">*application.yml* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-175">Save and close the *application.yml* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="69284-176">기본 데이터베이스 기능을 구현하는 샘플 코드 추가</span><span class="sxs-lookup"><span data-stu-id="69284-176">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="69284-177">이 섹션에서는 데이터베이스에서 데이터를 저장 하는 데 필요한 Java 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69284-177">In this section, you create the necessary Java classes for storing data in your database.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="69284-178">기본 응용 프로그램 클래스 수정</span><span class="sxs-lookup"><span data-stu-id="69284-178">Modify the main application class</span></span>

1. <span data-ttu-id="69284-179">앱의 패키지 디렉터리에서 기본 응용 프로그램 Java 파일을 찾습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="69284-179">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="69284-180">또는</span><span class="sxs-lookup"><span data-stu-id="69284-180">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![응용 프로그램 Java 파일 찾기][JV01]

1. <span data-ttu-id="69284-182">텍스트 편집기에서 응용 프로그램 Java 파일을 열고 다음 줄을 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-182">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.example.wingtiptoysdata;
   
   // These imports are required for the application.
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.example.wingtiptoysdata.domain.Network;
   import com.example.wingtiptoysdata.domain.Person;
   import com.example.wingtiptoysdata.domain.Relation;
   import com.example.wingtiptoysdata.repository.NetworkRepository;
   import com.example.wingtiptoysdata.repository.PersonRepository;
   import com.example.wingtiptoysdata.repository.RelationRepository;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import javax.annotation.PostConstruct;
   import javax.annotation.PreDestroy;
   
   @SpringBootApplication
   public class WingtiptoysdataApplication {
   
       // Define several person classes to store personal data.
       private final Person person1 = new Person("01", "Nellie Hughes", "23");
       private final Person person2 = new Person("02", "Delmar Alfred", "34");
       private final Person person3 = new Person("03", "Kelley Hunter", "45");
       private final Person person4 = new Person("04", "Roscoe Guerin", "56");
       private final Person person5 = new Person("05", "Gracie Chavez", "67");
   
       // Define relationship classes to define the relationships between some of the persons.
       private final Relation relation1 = new Relation("0102", "siblings", person1, person2);
       private final Relation relation2 = new Relation("0203", "coworkers", person2, person3);
       private final Relation relation3 = new Relation("0301", "parent", person3, person1);
       private final Relation relation4 = new Relation("0302", "parent", person3, person2);
       private final Relation relation5 = new Relation("0501", "grandparent", person5, person1);
       private final Relation relation6 = new Relation("0502", "grandparent", person5, person2);
   
       // Define the network.
       private final Network network = new Network();
   
       // Autowire the repositories and factory.
       @Autowired
       private PersonRepository personRepo;
       @Autowired
       private RelationRepository relationRepo;
       @Autowired
       private NetworkRepository networkRepo;
       @Autowired
       private GremlinFactory factory;
   
       // Run the Spring application and exit.
    public static void main(String[] args) {
           SpringApplication.run(WingtiptoysdataApplication.class, args);
           System.exit(0);
    }
   
       // Perform post-construct operations.    
       @PostConstruct
       public void setup() {
           // Delete any existing data from the database.
           this.networkRepo.deleteAll();
   
           // Add the relationship classes as edges.
           this.network.getEdges().add(this.relation1);
           this.network.getEdges().add(this.relation2);
           this.network.getEdges().add(this.relation3);
           this.network.getEdges().add(this.relation4);
           this.network.getEdges().add(this.relation5);
           this.network.getEdges().add(this.relation6);
   
           // Add the person classes as vertices.
           this.network.getVertexes().add(this.person1);
           this.network.getVertexes().add(this.person2);
           this.network.getVertexes().add(this.person3);
           this.network.getVertexes().add(this.person4);
           this.network.getVertexes().add(this.person5);
   
           // Save the network.
           this.networkRepo.save(this.network);
       }
   }
   ```

1. <span data-ttu-id="69284-183">기본 응용 프로그램 Java 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-183">Save and close the main application Java file.</span></span>

### <a name="define-a-basic-class-for-storing-configuration-information"></a><span data-ttu-id="69284-184">구성 정보를 저장하기 위한 기본 클래스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-184">Define a basic class for storing configuration information</span></span>

1. <span data-ttu-id="69284-185">앱의 패키지 디렉터리 아래 *config*라는 이름의 폴더를 만듭니다. 예를 들어,</span><span class="sxs-lookup"><span data-stu-id="69284-185">Create a folder named *config* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\config`

   <span data-ttu-id="69284-186">또는</span><span class="sxs-lookup"><span data-stu-id="69284-186">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/config`

1. <span data-ttu-id="69284-187">*config* 디렉터리 에 *UserRepositoryConfiguration.java*라는 새 Java 파일을 만듭니다. 그리고 파일 텍스트 편집기에서 해당 파일을 열고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-187">Create a new Java file named *UserRepositoryConfiguration.java* in the *config* directory, then open the file in a text editor, and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.config;

   import com.microsoft.spring.data.gremlin.common.GremlinConfiguration;
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.microsoft.spring.data.gremlin.config.AbstractGremlinConfiguration;
   import com.microsoft.spring.data.gremlin.repository.config.EnableGremlinRepositories;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.context.properties.EnableConfigurationProperties;
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;
   import org.springframework.context.annotation.PropertySource;
   
   @Configuration
   @EnableGremlinRepositories(basePackages = "com.example.wingtiptoysdata.repository")
   @EnableConfigurationProperties(GremlinConfiguration.class)
   @PropertySource("classpath:application.yml")
   public class UserRepositoryConfiguration extends AbstractGremlinConfiguration {
   
       @Autowired
       private GremlinConfiguration config;
   
       @Override
       public GremlinConfiguration getGremlinConfiguration() {
           return this.config;
       }
   }
   ```

1. <span data-ttu-id="69284-188">*UserRepositoryConfiguration.java* 파일을 저장 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-188">Save and close the *UserRepositoryConfiguration.java* file.</span></span>

### <a name="define-a-set-of-classes-that-define-the-elements-of-your-graph-database"></a><span data-ttu-id="69284-189">그래프 데이터베이스의 요소를 정의하는 클래스 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-189">Define a set of classes that define the elements of your graph database</span></span>

1. <span data-ttu-id="69284-190">앱의 패키지 디렉터리 아래 *domain*이라는 이름의 폴더를 만듭니다. 예를 들어,</span><span class="sxs-lookup"><span data-stu-id="69284-190">Create a folder named *domain* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\domain`

   <span data-ttu-id="69284-191">또는</span><span class="sxs-lookup"><span data-stu-id="69284-191">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/domain`

1. <span data-ttu-id="69284-192">*domain* 디렉터리 에 *Person.java*라는 새 Java 파일을 만듭니다. 그리고 파일 텍스트 편집기에서 해당 파일을 열고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-192">Create a new Java file named *Person.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Vertex;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Vertex
   @AllArgsConstructor
   @NoArgsConstructor
   public class Person {
   
       @Id
       private String id;
   
       private String name;
   
       private String age;
   }
   ```

1. <span data-ttu-id="69284-193">*Person.java* 파일을 저장 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-193">Save and close the *Person.java* file.</span></span>

1. <span data-ttu-id="69284-194">*domain* 디렉터리 에 *Relation.java*라는 새 Java 파일을 만듭니다. 그리고 파일 텍스트 편집기에서 해당 파일을 열고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-194">Create a new Java file named *Relation.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Edge;
   import com.microsoft.spring.data.gremlin.annotation.EdgeFrom;
   import com.microsoft.spring.data.gremlin.annotation.EdgeTo;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Edge
   @AllArgsConstructor
   @NoArgsConstructor
   public class Relation {
   
       @Id
       private String id;
   
       private String name;
   
       @EdgeFrom
       private Person personFrom;
   
       @EdgeTo
       private Person personTo;
   }
   ```

1. <span data-ttu-id="69284-195">*Relation.java* 파일을 저장 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-195">Save and close the *Relation.java* file.</span></span>

1. <span data-ttu-id="69284-196">*domain* 디렉터리 에 *Network.java*라는 새 Java 파일을 만듭니다. 그리고 파일 텍스트 편집기에서 해당 파일을 열고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-196">Create a new Java file named *Network.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.EdgeSet;
   import com.microsoft.spring.data.gremlin.annotation.Graph;
   import com.microsoft.spring.data.gremlin.annotation.VertexSet;
   import lombok.Getter;
   import org.springframework.data.annotation.Id;
   
   import java.util.ArrayList;
   import java.util.List;
   
   @Graph
   public class Network {
   
       @Id
       private String id;
   
       public Network() {
           this.edges = new ArrayList<Object>();
           this.vertexes = new ArrayList<Object>();
       }
   
       @EdgeSet
       @Getter
       private List<Object> edges;
   
       @VertexSet
       @Getter
       private List<Object> vertexes;
   }
   ```

1. <span data-ttu-id="69284-197">*Network.java* 파일을 저장 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-197">Save and close the *Network.java* file.</span></span>

### <a name="define-a-set-of-classes-that-define-the-repositories-for-your-graph-database"></a><span data-ttu-id="69284-198">그래프 데이터베이스의 리포지토리를 정의하는 클래스 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-198">Define a set of classes that define the repositories for your graph database</span></span>

1. <span data-ttu-id="69284-199">앱의 패키지 디렉터리 아래 *repository*라는 이름의 폴더를 만듭니다. 예를 들어,</span><span class="sxs-lookup"><span data-stu-id="69284-199">Create a folder named *repository* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\repository`

   <span data-ttu-id="69284-200">또는</span><span class="sxs-lookup"><span data-stu-id="69284-200">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/repository`

1. <span data-ttu-id="69284-201">*repository* 디렉터리에 *NetworkRepository.java*라는 새 Java 파일을 만듭니다. 그리고 파일 텍스트 편집기에서 해당 파일을 열고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-201">Create a new Java file named *NetworkRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Network;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface NetworkRepository extends GremlinRepository<Network, String> {
   }
   ```

1. <span data-ttu-id="69284-202">*NetworkRepository.java* 파일을 저장 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-202">Save and close the *NetworkRepository.java* file.</span></span>

1. <span data-ttu-id="69284-203">*repository* 디렉터리에 *PersonRepository.java*라는 새 Java 파일을 만듭니다. 그리고 파일 텍스트 편집기에서 해당 파일을 열고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-203">Create a new Java file named *PersonRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Person;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface PersonRepository extends GremlinRepository<Person, String> {
   }
   ```

1. <span data-ttu-id="69284-204">*PersonRepository.java* 파일을 저장 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-204">Save and close the *PersonRepository.java* file.</span></span>

1. <span data-ttu-id="69284-205">*repository* 디렉터리에 *RelationRepository.java*라는 새 Java 파일을 만듭니다. 그리고 파일 텍스트 편집기에서 해당 파일을 열고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-205">Create a new Java file named *RelationRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Relation;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface RelationRepository extends GremlinRepository<Relation, String> {
   }
   ```

1. <span data-ttu-id="69284-206">*RelationRepository.java* 파일을 저장 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-206">Save and close the *RelationRepository.java* file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="69284-207">앱 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="69284-207">Build and test your app</span></span>

1. <span data-ttu-id="69284-208">명령 프롬프트를 열고 디렉터리를 *pom.xml* 파일이 위치한 폴더로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="69284-208">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="69284-209">또는</span><span class="sxs-lookup"><span data-stu-id="69284-209">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="69284-210">Maven을 사용하여 Spring Boot 응용 프로그램을 빌드하고 실행합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="69284-210">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="69284-211">응용 프로그램에 여러 런타임 메시지가 표시되고 오류가 없는 경우 Azure 포털을 사용하여 Azure Cosmos DB의 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-211">Your application will display several runtime messages, and if there were no errors, you can use the Azure portal to view the contents of your Azure Cosmos DB.</span></span> <span data-ttu-id="69284-212">이렇게 하려면 데이터베이스의 속성 페이지에서 **데이터 탐색기**를 클릭하고 **Gremlin 쿼리 실행**을 클릭한 다음, 결과 목록에서 항목을 선택하여 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="69284-212">To do so, click **Data Explorer** on the properties page for your database, then click **Execute Gremlin Query**, and then select an item from the list of results to view the data.</span></span>

   ![문서 탐색기를 사용하여 데이터 보기][JV03]

## <a name="next-steps"></a><span data-ttu-id="69284-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69284-214">Next steps</span></span>

<span data-ttu-id="69284-215">Azure Gremlin 및 Graph API에 대한 지원에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69284-215">For more information about Azure support for Gremlin and Graph API, see the following articles:</span></span>

* [<span data-ttu-id="69284-216">Azure Cosmos DB: Graph API 소개</span><span class="sxs-lookup"><span data-stu-id="69284-216">Introduction to Azure Cosmos DB: Graph API</span></span>](https://docs.microsoft.com/azure/cosmos-db/graph-introduction)

* [<span data-ttu-id="69284-217">Azure Cosmos DB Gremlin 그래프 지원</span><span class="sxs-lookup"><span data-stu-id="69284-217">Azure Cosmos DB Gremlin graph support</span></span>](https://docs.microsoft.com/azure/cosmos-db/gremlin-support)

* [<span data-ttu-id="69284-218">Azure Cosmos DB: Java 및 Azure Portal을 사용하여 그래프 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="69284-218">Azure Cosmos DB: Create a graph database using Java and the Azure portal</span></span>](https://docs.microsoft.com/azure/cosmos-db/create-graph-java)

* [<span data-ttu-id="69284-219">자습서: Gremlin을 사용하여 Azure Cosmos DB Graph API 쿼리</span><span class="sxs-lookup"><span data-stu-id="69284-219">Tutorial: Query Azure Cosmos DB Graph API by using Gremlin</span></span>](https://docs.microsoft.com/azure/cosmos-db/tutorial-query-graph)

* <span data-ttu-id="69284-220">[Spring 데이터 Gremlin Starter]</span><span class="sxs-lookup"><span data-stu-id="69284-220">[Spring Data Gremlin Starter]</span></span>

<span data-ttu-id="69284-221">Azure Cosmos DB 및 Java를 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69284-221">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="69284-222">[Azure Cosmos DB 설명서]</span><span class="sxs-lookup"><span data-stu-id="69284-222">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="69284-223">[Azure Cosmos DB: Java 및 Azure Portal을 사용하여 문서 데이터베이스 만들기][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="69284-223">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="69284-224">[Azure Cosmos DB SQL API용 Spring 데이터]</span><span class="sxs-lookup"><span data-stu-id="69284-224">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="69284-225">Azure에서 Spring Boot 응용 프로그램을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69284-225">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="69284-226">Azure App Service에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="69284-226">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="69284-227">Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="69284-227">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="69284-228">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69284-228">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="69284-229">**[Spring Framework]** 는 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만드는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="69284-229">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="69284-230">해당 플랫폼을 기반으로 하여 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 응용 프로그램을 만드는 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="69284-230">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="69284-231">Spring Boot을 시작하는 개발자를 도우려면 <https://github.com/spring-guides/>에서 몇 가지 샘플 Spring Boot 패키지를 사용할 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69284-231">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="69284-232">기본 Spring Boot 프로젝트 목록에서 선택하는 것 외에도 **[Spring Initializr]** 를 통해 사용자 지정 Spring Boot 응용 프로그램을 만들기 시작하는 개발자에게 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="69284-232">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>


<!-- URL List -->

[Azure Cosmos DB 설명서]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Java 개발자용 Azure]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Azure Cosmos DB SQL API용 Spring 데이터]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring 데이터 Gremlin Starter]: https://github.com/Microsoft/spring-data-gremlin
[Spring Data Gremlin Starter]: https://github.com/Microsoft/spring-data-gremlin
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ05.png
[AZ06]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ06.png
[AZ07]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ07.png
[AZ08]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ08.png

[SI01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV03.png
