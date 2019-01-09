---
title: Azure Redis Cache를 사용하도록 Spring Boot Initializer 앱 구성
description: Spring Initializer를 사용하여 만든 Spring Boot 애플리케이션을 구성하여 Azure Redis Cache를 사용하여 클라우드에서 Redis를 사용합니다.
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: cache
ms.tgt_pltfrm: cache-redis
ms.topic: article
ms.workload: na
ms.openlocfilehash: 4b720cf4639a12c6dd8cc5040107c1b52de6f642
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991407"
---
# <a name="configure-a-spring-boot-initializer-app-to-use-redis-in-the-cloud-with-azure-redis-cache"></a><span data-ttu-id="ef7b5-103">Azure Redis Cache를 사용하여 클라우드에서 Redis를 사용하도록 Spring Boot Initializer 앱 구성</span><span class="sxs-lookup"><span data-stu-id="ef7b5-103">Configure a Spring Boot Initializer app to use Redis in the cloud with Azure Redis Cache</span></span>

<span data-ttu-id="ef7b5-104">이 문서에서는 Azure Portal을 사용하여 클라우드에서 Redis Cache를 만들고, **[Spring Initializr]** 를 사용하여 사용자 지정 애플리케이션을 만든 다음 Redis Cache를 사용하여 데이터를 저장하고 검색하는 Java 웹 애플리케이션을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-104">This article walks you through creating a Redis cache in the cloud using the Azure portal, then using the **[Spring Initializr]** to create a custom application, and then creating a Java web application that stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef7b5-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ef7b5-105">Prerequisites</span></span>

<span data-ttu-id="ef7b5-106">이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-106">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="ef7b5-107">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="ef7b5-108">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="ef7b5-108">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="ef7b5-109">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-109">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="ef7b5-110">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="ef7b5-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="ef7b5-111">Spring Initializr를 사용하여 사용자 지정 애플리케이션 만들기</span><span class="sxs-lookup"><span data-stu-id="ef7b5-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="ef7b5-112"><https://start.spring.io/>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="ef7b5-113">**Java**에서 **Maven** 프로젝트를 생성한다고 지정하고, 애플리케이션에 대한 **그룹** 및 **아티팩트** 이름을 입력한 다음 Spring Initializr의 **정식 버전으로 전환**하는 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![기본 Spring Initializr 옵션][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="ef7b5-115">Spring Initializr는 **그룹** 및 **아티팩트** 이름을 사용하여 패키지 이름을 만듭니다(예: *com.contoso.myazuredemo*).</span><span class="sxs-lookup"><span data-stu-id="ef7b5-115">The Spring Initializr will use the **Group** and **Aritifact** names to create the package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="ef7b5-116">**웹** 섹션까지 아래로 스크롤하고 **웹**의 확인란을 선택한 다음 **NoSQL** 섹션까지 아래로 스크롤하고 **Redis**의 확인란을 선택하고 페이지 아래쪽으로 스크롤한 다음 **프로젝트를 생성**하는 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-116">Scroll down to the **Web** section and check the box for **Web**, then scroll down to the **NoSQL** section and check the box for **Redis**, then scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![전체 Spring Initializr 옵션][SI02]

1. <span data-ttu-id="ef7b5-118">메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-118">When prompted, download the project to a path on your local computer.</span></span>

   ![사용자 지정 Spring Boot 프로젝트 다운로드][SI03]

1. <span data-ttu-id="ef7b5-120">로컬 시스템에서 파일의 압축을 푼 후에 사용자 지정 Spring Boot 애플리케이션을 편집할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-120">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![사용자 지정 Spring Boot 프로젝트 파일][SI04]

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="ef7b5-122">Azure에 Redis 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="ef7b5-122">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="ef7b5-123">Azure Portal(<https://portal.azure.com/>)이동하고 **+새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-123">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure portal][AZ01]

1. <span data-ttu-id="ef7b5-125">**데이터베이스**를 클릭하고 **Redis Cache**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-125">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Azure portal][AZ02]

1. <span data-ttu-id="ef7b5-127">**새 Redis Cache** 페이지에서 다음 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-127">On the **New Redis Cache** page, specify the following information:</span></span>

   * <span data-ttu-id="ef7b5-128">캐시에 대한 **DNS 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-128">Enter the **DNS name** for your cache.</span></span>
   * <span data-ttu-id="ef7b5-129">**구독**, **리소스 그룹**, **위치** 및 **가격 책정 계층**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-129">Specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span>
   * <span data-ttu-id="ef7b5-130">이 자습서에서는 **포트 6379 차단 해제**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-130">For this tutorial, choose **Unblock port 6379**.</span></span>

   > [!NOTE]
   >
   > <span data-ttu-id="ef7b5-131">Redis 캐시와 함께 SSL을 사용할 수 있지만 Jedis와 같은 다른 Redis 클라이언트를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-131">You can use SSL with Redis caches, but you would need to use a different Redis client like Jedis.</span></span> <span data-ttu-id="ef7b5-132">자세한 내용은 [Java와 함께 Azure Redis Cache를 사용하는 방법][Redis Cache with Java]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-132">For more information, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>
   >

   <span data-ttu-id="ef7b5-133">이러한 옵션을 지정한 경우 **만들기**를 클릭하여 캐시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-133">When you have specified these options, click **Create** to create your cache.</span></span>

   ![Azure portal][AZ03]

1. <span data-ttu-id="ef7b5-135">캐시가 완료되면 Azure **대시보드**뿐만 아니라 **모든 리소스** 및 **Redis Caches** 페이지에서도 나열된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-135">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="ef7b5-136">해당 위치 중 하나에서 캐시를 클릭하여 캐시의 속성 페이지를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-136">You can click on your cache on any of those locations to open the properties page for your cache.</span></span>

   ![Azure portal][AZ04]

1. <span data-ttu-id="ef7b5-138">캐시의 속성 목록이 포함된 페이지가 표시되면 **액세스 키**를 클릭하고 캐시의 액세스 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-138">When the page that contains the list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Azure portal][AZ05]

## <a name="configure-your-custom-spring-boot-to-use-your-redis-cache"></a><span data-ttu-id="ef7b5-140">Redis Cache를 사용하도록 사용자 지정 Spring Boot 구성</span><span class="sxs-lookup"><span data-stu-id="ef7b5-140">Configure your custom Spring Boot to use your Redis Cache</span></span>

1. <span data-ttu-id="ef7b5-141">앱의 *리소스* 디렉터리에서 *application.properties* 파일을 찾거나 아직 없는 경우 해당 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-141">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![application.properties 파일 찾기][RE01]

1. <span data-ttu-id="ef7b5-143">텍스트 편집기에서 *application.properties* 파일을 찾고 파일에 다음 줄을 추가하고 샘플 값을 캐시의 적절한 속성으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-143">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties from your cache:</span></span>

   ```yaml
   # Specify the DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify the port for your Redis cache.
   spring.redis.port=6379

   # Specify the access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![application.properties 파일 편집][RE02]

   > [!NOTE] 
   > 
   > <span data-ttu-id="ef7b5-145">SSL을 활성화하는 Jedis와 같은 다른 Redis 클라이언트를 사용하는 경우 *application.properties* 파일에서 사용하고자 하는 SSL과 포트 6380을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-145">If you were using a different Redis client like Jedis that enables SSL, you would specify that you want to use SSL in your *application.properties* file and use port 6380.</span></span> <span data-ttu-id="ef7b5-146">예: </span><span class="sxs-lookup"><span data-stu-id="ef7b5-146">For example:</span></span>
   > 
   > ```yaml
   > # Specify the DNS URI of your Redis cache.
   > spring.redis.host=myspringbootcache.redis.cache.windows.net
   > # Specify the access key for your Redis cache.
   > spring.redis.password=57686f6120447564652c2049495320526f636b73=
   > # Specify that you want to use SSL.
   > spring.redis.ssl=true
   > # Specify the SSL port for your Redis cache.
   > spring.redis.port=6380
   > ```
   > 
   > <span data-ttu-id="ef7b5-147">자세한 내용은 [Java와 함께 Azure Redis Cache를 사용하는 방법][Redis Cache with Java]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-147">For more information, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span> 
   > 

1. <span data-ttu-id="ef7b5-148">*application.properties* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-148">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="ef7b5-149">패키지의 소스 폴더 아래에서 *controller*라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-149">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="ef7b5-150">또는</span><span class="sxs-lookup"><span data-stu-id="ef7b5-150">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="ef7b5-151">*컨트롤러* 폴더에 *HelloController.java*라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-151">Create a new file named *HelloController.java* in the *controller* folder.</span></span> <span data-ttu-id="ef7b5-152">텍스트 편집기에서 파일을 열고 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-152">Open the file in a text editor and add the following code to it:</span></span>

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.data.redis.core.StringRedisTemplate;
   import org.springframework.data.redis.core.ValueOperations;

   @RestController
   public class HelloController {
   
      @Autowired
      private StringRedisTemplate template;

      @RequestMapping("/")
      // Define the Hello World controller.
      public String hello() {
      
         ValueOperations<String, String> ops = this.template.opsForValue();

         // Add a Hello World string to your cache.
         String key = "greeting";
         if (!this.template.hasKey(key)) {
             ops.set(key, "Hello World!");
         }

         // Return the string from your cache.
         return ops.get(key);
      }
   }
   ```
   
   <span data-ttu-id="ef7b5-153">여기에서 `com.contoso.myazuredemo`를 프로젝트의 패키지 이름으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-153">Where you will need to replace `com.contoso.myazuredemo` with the package name for your project.</span></span>

1. <span data-ttu-id="ef7b5-154">*HelloController.java* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-154">Save and close the *HelloController.java* file.</span></span>

1. <span data-ttu-id="ef7b5-155">Maven을 사용하여 Spring Boot 애플리케이션을 빌드하고 실행합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="ef7b5-155">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="ef7b5-156">웹 브라우저를 통해 http://localhost:8080으로 이동하여 웹앱을 테스트하거나 사용 가능한 curl이 있는 경우 다음 예제와 같이 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-156">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="ef7b5-157">샘플 컨트롤러에서 "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="ef7b5-157">You should see the "Hello World!"</span></span> <span data-ttu-id="ef7b5-158">메시지가 표시되어야 합니다. 이 메시지는 Redis Cache에서 동적으로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-158">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef7b5-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef7b5-159">Next steps</span></span>

<span data-ttu-id="ef7b5-160">Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-160">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ef7b5-161">Azure의 Spring</span><span class="sxs-lookup"><span data-stu-id="ef7b5-161">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="ef7b5-162">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ef7b5-162">Additional Resources</span></span>

<span data-ttu-id="ef7b5-163">Azure에서 Spring Boot 애플리케이션을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-163">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="ef7b5-164">Azure App Service에 Spring Boot 애플리케이션 배포</span><span class="sxs-lookup"><span data-stu-id="ef7b5-164">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="ef7b5-165">Azure Container Service의 Kubernetes 클러스터에 Spring Boot 애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="ef7b5-165">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="ef7b5-166">Java와 함께 Azure를 사용하는 방법에 관한 자세한 정보는 [Java 개발자용 Azure]와 [Azure DevOps 및 Java 사용하기]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-166">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="ef7b5-167">Azure에서 Java로 Redis Cache를 시작하는 방법에 대한 자세한 내용은 [Java에서 Azure Redis Cache를 사용하는 방법][Redis Cache with Java]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-167">For more information about getting started using Redis Cache with Java on Azure, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>

<span data-ttu-id="ef7b5-168">**[Spring Framework]** 는 Java 개발자가 엔터프라이즈 수준의 애플리케이션을 만드는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-168">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="ef7b5-169">해당 플랫폼을 기반으로 하여 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 애플리케이션을 만드는 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-169">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="ef7b5-170">Spring Boot을 시작하는 개발자를 도우려면 <https://github.com/spring-guides/>에서 몇 가지 샘플 Spring Boot 패키지를 사용할 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-170">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="ef7b5-171">기본 Spring Boot 프로젝트 목록에서 선택하는 것 외에도 **[Spring Initializr]** 를 통해 사용자 지정 Spring Boot 애플리케이션을 만들기 시작하는 개발자에게 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ef7b5-171">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Java 개발자용 Azure]: /java/azure/
[Azure for Java Developers]: /java/azure/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Azure DevOps 및 Java 사용하기]: /azure/devops/java/
[Working with Azure DevOps and Java]: /azure/devops/java/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Redis Cache with Java]: /azure/redis-cache/cache-java-get-started

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ01.png
[AZ02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ02.png
[AZ03]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ03.png
[AZ04]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ04.png
[AZ05]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ05.png

[SI01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI01.png
[SI02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI02.png
[SI03]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI03.png
[SI04]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI04.png

[RE01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/RE01.png
[RE02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/RE02.png
