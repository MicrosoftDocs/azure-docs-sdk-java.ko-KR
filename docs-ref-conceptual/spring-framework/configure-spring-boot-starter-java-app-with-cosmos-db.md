---
title: Azure Cosmos DB SQL API에서 Spring Boot Starter를 사용하는 방법
description: Azure Cosmos DB SQL API에서 Spring Boot Initializer를 사용하여 만든 응용 프로그램을 구성하는 방법에 대해 알아봅니다.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 08/10/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: dcb5ef5f12cc1682175da147268eb4a6a89f820b
ms.sourcegitcommit: 0f38ef9ad64cffdb7b2e9e966224dfd0af251b0f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703526"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="9d48d-103">Azure Cosmos DB SQL API에서 Spring Boot Starter를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9d48d-103">How to use the Spring Boot Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="9d48d-104">개요</span><span class="sxs-lookup"><span data-stu-id="9d48d-104">Overview</span></span>

<span data-ttu-id="9d48d-105">Azure Cosmos DB는 개발자가 SQL, MongoDB, Graph 및 Table API와 같은 표준 API를 사용하여 데이터를 사용할 수 있도록 하는 전역 분산 데이터베이스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-105">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as SQL, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="9d48d-106">Microsoft의 Spring Boot Starter를 사용하면 개발자가 SQL API를 사용하여 Azure Cosmos DB와 쉽게 통합하는 Spring Boot 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-106">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using the SQL API.</span></span>

<span data-ttu-id="9d48d-107">이 문서에서는 Azure Portal을 사용하여 Azure Cosmos DB를 만들고, **[Spring Initializr]** 를 사용하여 사용자 지정 java 응용 프로그램을 만들고, Spring Boot Starter 기능을 사용자 지정 응용 프로그램에 추가하여 데이터를 저장하고 SQL API를 사용하여 Azure Cosmos DB에서 데이터를 검색하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-107">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Boot Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using the SQL API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d48d-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9d48d-108">Prerequisites</span></span>

<span data-ttu-id="9d48d-109">이 문서의 단계를 수행하기 위해 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-109">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="9d48d-110">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="9d48d-111">[JDK(Java Development Kit)](http://www.oracle.com/technetwork/java/javase/downloads/), 버전 1.7 이상</span><span class="sxs-lookup"><span data-stu-id="9d48d-111">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="9d48d-112">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="9d48d-112">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="9d48d-113">Azure Portal을 사용하여 Azure Cosmos DB 만들기</span><span class="sxs-lookup"><span data-stu-id="9d48d-113">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="9d48d-114">Azure Portal(<https://portal.azure.com/>)로 이동하고 **+리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-114">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![Azure portal][AZ01]

1. <span data-ttu-id="9d48d-116">**데이터베이스**를 클릭한 후 **Azure Cosmos DB**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-116">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure portal][AZ02]

1. <span data-ttu-id="9d48d-118">**Azure Cosmos DB** 페이지에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-118">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="9d48d-119">고유한 **ID**를 입력합니다. 이 항목은 데이터베이스의 URI로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-119">Enter a unique **ID**, which you will use as the URI for your database.</span></span> <span data-ttu-id="9d48d-120">예: *wingtiptoysdata.documents.azure.com*</span><span class="sxs-lookup"><span data-stu-id="9d48d-120">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="9d48d-121">API에 대한 **SQL**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-121">Choose **SQL** for the API.</span></span>
   * <span data-ttu-id="9d48d-122">데이터베이스에 사용하려는 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-122">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="9d48d-123">데이터베이스에 새 **리소스 그룹**을 만들지 아니면 기존 리소스 그룹을 선택할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-123">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="9d48d-124">데이터베이스의 **위치**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-124">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="9d48d-125">이러한 옵션을 지정한 경우 **만들기**를 클릭하여 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-125">When you have specified these options, click **Create** to create your database.</span></span>

   ![Azure portal][AZ03]

1. <span data-ttu-id="9d48d-127">데이터베이스를 만든 경우 Azure **대시보드** 뿐 아니라 **모든 리소스** 및 **Azure Cosmos DB** 페이지에도 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-127">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="9d48d-128">해당 위치 중 하나에서 데이터베이스를 클릭하여 캐시에 대한 속성 페이지를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-128">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Azure portal][AZ04]

1. <span data-ttu-id="9d48d-130">데이터베이스에 대한 속성 페이지가 표시되면 **액세스 키**를 클릭하고 데이터베이스에 대한 URI 및 액세스 키를 복사합니다. 이러한 값은 Spring Boot 응용 프로그램에서 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-130">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Azure portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="9d48d-132">Spring Initializr를 사용하여 간단한 Spring Boot 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="9d48d-132">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="9d48d-133"><https://start.spring.io/>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-133">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="9d48d-134">**Java**에서 **Maven** 프로젝트를 생성한다고 지정하고, 응용 프로그램 **그룹** 및 **아티팩트** 이름을 입력한 다음, **Spring Boot** 버전을 지정하고 **프로젝트를 생성**하는 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-134">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, specify your **Spring Boot** version, and then click the button to **Generate Project**.</span></span>

   > [!IMPORTANT]
   >
   > <span data-ttu-id="9d48d-135">이 문서의 단계를 완료하는 데 사용할 Spring Boot 버전 2.0.n의 API에 몇가지 호환성이 손상되는 변경이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-135">There were several breaking changes to the APIs in Spring Boot version 2.0.n, which will be used to complete the steps in this article.</span></span> <span data-ttu-id="9d48d-136">그러나 이 자습서의 단계를 완료하기 위해 Spring Boot 1.5.n 버전 중 하나를 사용할 수 있으며 필요한 경우 차이점이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-136">You can still use one of the Spring Boot 1.5.n versions to complete the steps in this tutorial, and the differences will be highlighted when necessary.</span></span>
   >

   ![기본 Spring Initializr 옵션][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="9d48d-138">Spring Initializr는 **그룹** 및 **아티팩트** 이름을 사용하여 패키지 이름을 만듭니다(예: *com.example.wintiptoysdata*).</span><span class="sxs-lookup"><span data-stu-id="9d48d-138">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoysdata*.</span></span>
   >

1. <span data-ttu-id="9d48d-139">메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-139">When prompted, download the project to a path on your local computer.</span></span>

   ![사용자 지정 Spring Boot 프로젝트 다운로드][SI02]

1. <span data-ttu-id="9d48d-141">로컬 시스템에서 파일의 압축을 푼 후에 단순한 Spring Boot 응용 프로그램을 편집할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-141">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![사용자 지정 Spring Boot 프로젝트 파일][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="9d48d-143">Azure Spring Boot Starter를 사용하도록 Spring Boot 앱 구성</span><span class="sxs-lookup"><span data-stu-id="9d48d-143">Configure your Spring Boot app to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="9d48d-144">앱의 디렉터리에서 *pom.xml* 파일을 찾습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="9d48d-144">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="9d48d-145">또는</span><span class="sxs-lookup"><span data-stu-id="9d48d-145">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![pom.xml 파일 찾기][PM01]

1. <span data-ttu-id="9d48d-147">텍스트 편집기에서 *pom.xml* 파일을 열고 다음 줄을 `<dependencies>` 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-147">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>2.0.4</version>
   </dependency>
   ```

   ![pom.xml 파일 편집][PM02]

   > [!IMPORTANT]
   >
   > <span data-ttu-id="9d48d-149">Spring Boot 1.5.n 버전 중 하나를 사용하여 이 자습서를 완료하고자 하는 경우, Azure Cosmos DB 스타터의 이전 버전을 지정해야 합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="9d48d-149">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to specify the older version of the Azure Cosmos DB starter; for example:</span></span>
   >
   > ```xml
   > <dependency>
   >   <groupId>com.microsoft.azure</groupId>
   >   <artifactId>azure-documentdb-spring-boot-starter</artifactId>
   >   <version>0.1.4</version>
   > </dependency>
   > ```

1. <span data-ttu-id="9d48d-150">Spring Boot 버전이 Spring Initializr를 사용하여 응용 프로그램을 만들 때 선택한 버전인지 확인합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="9d48d-150">Verify that the Spring Boot version is the version that you chose when you created your application with the Spring Initializr; for example:</span></span>

   ```xml
   <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.0.1.RELEASE</version>
      <relativePath/>
   </parent>
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="9d48d-151">Spring Boot 1.5.n 버전 중 하나를 사용하여 이 자습서를 완료하고자 하는 경우, 올바른 버전을 검증해야 합니다. 예: `<version>1.5.14.RELEASE</version>`.</span><span class="sxs-lookup"><span data-stu-id="9d48d-151">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to verify the correct version; for example: `<version>1.5.14.RELEASE</version>`.</span></span>
   >

1. <span data-ttu-id="9d48d-152">*pom.xml* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-152">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="9d48d-153">Azure Cosmos DB를 사용하도록 Spring Boot 앱 구성</span><span class="sxs-lookup"><span data-stu-id="9d48d-153">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="9d48d-154">앱의 *리소스* 디렉터리에서 *application.properties* 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-154">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.properties`

   <span data-ttu-id="9d48d-155">또는</span><span class="sxs-lookup"><span data-stu-id="9d48d-155">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.properties`

   ![application.properties 파일 찾기][RE01]

1. <span data-ttu-id="9d48d-157">텍스트 편집기에서 *application.properties* 파일을 찾고 파일에 다음 줄을 추가하고 샘플 값을 데이터베이스의 적절한 속성으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-157">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![application.properties 파일 편집][RE02]

1. <span data-ttu-id="9d48d-159">*application.properties* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-159">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="9d48d-160">기본 데이터베이스 기능을 구현하는 샘플 코드 추가</span><span class="sxs-lookup"><span data-stu-id="9d48d-160">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="9d48d-161">이 섹션에서는 사용자 데이터 저장을 위해 두 가지 Java 클래스를 만든 다음, 기본 응용 프로그램 클래스를 수정하여 사용자 클래스의 인스턴스를 만들고 데이터베이스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-161">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the user class and save it to your database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="9d48d-162">사용자 데이터를 저장하기 위한 기본 클래스 정의</span><span class="sxs-lookup"><span data-stu-id="9d48d-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="9d48d-163">기본 응용 프로그램 Java 파일과 동일한 디렉터리에 *User.java*라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-163">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="9d48d-164">텍스트 편집기에서 *User.java* 파일을 다음 줄을 파일에 추가하여 데이터베이스에서 값을 저장하고 검색하는 일반 사용자 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-164">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoysdata;

   // Define a generic User class.
   public class User {
      private String id;
      private String firstName;
      private String lastName;
   
      public User() {
      }
   
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }
   
      public void setId(String id) {
         this.id = id;
      }
   
      public String getFirstName() {
         return firstName;
      }
   
      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }
   
      public String getLastName() {
         return lastName;
      }
   
      public void setLastName(String lastName) {
         this.lastName = lastName;
      }
   
      @Override
      public String toString() {
         return String.format("User: %s %s %s", id, firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="9d48d-165">*User.java* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-165">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="9d48d-166">데이터 리포지토리 인터페이스 정의</span><span class="sxs-lookup"><span data-stu-id="9d48d-166">Define a data repository interface</span></span>

1. <span data-ttu-id="9d48d-167">기본 응용 프로그램 Java 파일과 동일한 디렉터리에 *UserRepository.java*라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-167">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="9d48d-168">텍스트 편집기에서 *UserRepository.java* 파일을 열고 파일에 다음 줄을 추가하여 기본 DocumentDB 리포지토리 인터페이스를 확장하는 사용자 리포지토리 인터페이스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-168">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoysdata;
   
   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> { } 
   ```

1. <span data-ttu-id="9d48d-169">*UserRepository.java* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-169">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="9d48d-170">기본 응용 프로그램 클래스 수정</span><span class="sxs-lookup"><span data-stu-id="9d48d-170">Modify the main application class</span></span>

1. <span data-ttu-id="9d48d-171">앱의 패키지 디렉터리에서 기본 응용 프로그램 Java 파일을 찾습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="9d48d-171">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="9d48d-172">또는</span><span class="sxs-lookup"><span data-stu-id="9d48d-172">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![응용 프로그램 Java 파일 찾기][JV01]

1. <span data-ttu-id="9d48d-174">텍스트 편집기에서 응용 프로그램 Java 파일을 열고 다음 줄을 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-174">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.example.wingtiptoysdata;

   // These imports are required for the application.
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   // These imports are only used to create an ID for this example.
   import java.util.Date;
   import java.text.SimpleDateFormat;

   @SpringBootApplication
   public class wingtiptoysdataApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;

      public static void main(String[] args) {
         // Execute the command line runner.
         SpringApplication.run(wingtiptoysdataApplication.class, args);
         System.exit(0);
      }

      public void run(String... args) throws Exception {
         // Create a simple date/time ID.
         SimpleDateFormat userId = new SimpleDateFormat("yyyyMMddHHmmssSSS");
         Date currentDate = new Date();

         // Create a new User class.
         final User testUser = new User(userId.format(currentDate), "Gena", "Soto");

         // For this example, remove all of the existing records.
         repository.deleteAll();

         // Save the User class to the Azure database.
         repository.save(testUser);
      
         // Retrieve the database record for the User class you just saved by ID.
         // final User result = repository.findOne(testUser.getId());
         final User result = repository.findById(testUser.getId()).get();

         // Display the results of the database record retrieval.
         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

   > [!IMPORTANT]
   >
   > <span data-ttu-id="9d48d-175">Spring Boot 1.5.n 버전 중 하나를 사용하여 이 자습서를 완료하고자 하는 경우, `final User result = repository.findById(testUser.getId()).get();` 구문을 `final User result = repository.findOne(testUser.getId());`로 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-175">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to replace the `final User result = repository.findById(testUser.getId()).get();` syntax with `final User result = repository.findOne(testUser.getId());`.</span></span>
   >

1. <span data-ttu-id="9d48d-176">기본 응용 프로그램 Java 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-176">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="9d48d-177">앱 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="9d48d-177">Build and test your app</span></span>

1. <span data-ttu-id="9d48d-178">명령 프롬프트를 열고 디렉터리를 *pom.xml* 파일이 위치한 폴더로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="9d48d-178">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="9d48d-179">또는</span><span class="sxs-lookup"><span data-stu-id="9d48d-179">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="9d48d-180">Maven을 사용하여 Spring Boot 응용 프로그램을 빌드하고 실행합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="9d48d-180">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="9d48d-181">응용 프로그램에 여러 런타임 메시지가 표시되고 다음 예와 같은 메시지가 표시되어 값을 성공적으로 저장하고 데이터베이스에서 검색했음을 나타내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-181">Your application will display several runtime messages, and it will display a message like the following examples to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ```
   User: 20170724025215132 Gena Soto
   ```

   ![응용 프로그램에서 성공적인 출력][JV02]

1. <span data-ttu-id="9d48d-183">선택 사항: 콘텐츠를 보기 위해 **데이터 탐색기**를 클릭하고 표시된 목록에서 항목을 선택하여 데이터베이스의 속성 페이지에서 Azure Cosmos DB의 콘텐츠를 보도록 Azure Portal을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-183">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Data Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![문서 탐색기를 사용하여 데이터 보기][JV03]

## <a name="next-steps"></a><span data-ttu-id="9d48d-185">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9d48d-185">Next steps</span></span>

<span data-ttu-id="9d48d-186">Azure Cosmos DB 및 Java를 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d48d-186">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="9d48d-187">[Azure Cosmos DB 설명서]</span><span class="sxs-lookup"><span data-stu-id="9d48d-187">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="9d48d-188">[Azure Cosmos DB: Java 및 Azure Portal을 사용하여 문서 데이터베이스 만들기][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="9d48d-188">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="9d48d-189">[Azure Cosmos DB SQL API용 Spring 데이터]</span><span class="sxs-lookup"><span data-stu-id="9d48d-189">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="9d48d-190">Azure에서 Spring Boot 응용 프로그램을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d48d-190">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* <span data-ttu-id="9d48d-191">[Azure의 Spring Boot Document DB Starter]</span><span class="sxs-lookup"><span data-stu-id="9d48d-191">[Spring Boot Document DB Starter for Azure]</span></span>

* [<span data-ttu-id="9d48d-192">Azure App Service에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="9d48d-192">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="9d48d-193">Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="9d48d-193">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="9d48d-194">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9d48d-194">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="9d48d-195">**[Spring Framework]** 는 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만드는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-195">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="9d48d-196">해당 플랫폼을 기반으로 하여 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 응용 프로그램을 만드는 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-196">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="9d48d-197">Spring Boot을 시작하는 개발자를 도우려면 <https://github.com/spring-guides/>에서 몇 가지 샘플 Spring Boot 패키지를 사용할 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-197">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="9d48d-198">기본 Spring Boot 프로젝트 목록에서 선택하는 것 외에도 **[Spring Initializr]** 를 통해 사용자 지정 Spring Boot 응용 프로그램을 만들기 시작하는 개발자에게 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9d48d-198">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Azure Cosmos DB 설명서]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Java 개발자용 Azure]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Azure Cosmos DB SQL API용 Spring 데이터]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Azure의 Spring Boot Document DB Starter]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
[Spring Boot Document DB Starter for Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
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

[AZ01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV03.png
