---
title: Maven 및 Azure를 사용하여 Spring Boot 앱을 클라우드에 배포
description: Azure Web Apps의 Maven 플러그 인을 사용하여 Spring Boot 앱을 클라우드에 배포하는 방법에 대해 알아봅니다.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.assetid: ''
ms.author: robmcm;kevinzha;brborges
ms.date: 06/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: d58cafe3456150069ec8572c101c62d1b2c29c5d
ms.sourcegitcommit: e1a5d9687e006e8bf12d11747d45cf130a2c82af
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2018
ms.locfileid: "42703362"
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-app-service"></a><span data-ttu-id="c65f2-103">Azure Apps Service의 Maven 플러그 인을 사용하여 Spring Boot 앱을 클라우드에 배포</span><span class="sxs-lookup"><span data-stu-id="c65f2-103">Deploy a Spring Boot app to the cloud using the Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="c65f2-104">이 문서에서는 Azure App Service Web Apps의 Maven 플러그 인을 사용하여 샘플 Spring Boot 응용 프로그램을 배포하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-104">This article demonstrates using the Maven Plugin for Azure App Service Web Apps to deploy a sample Spring Boot application.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="c65f2-105">[Apache Maven](http://maven.apache.org/)에서 Azure Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme)용 [Maven 플러그인은 Maven 프로젝트에 Azure App Service의 원활한 통합을 제공하고, 개발자가 Azure App Service에 웹앱을 배포하는 프로세스를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-105">The [Maven Plugin for Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>

<span data-ttu-id="c65f2-106">Maven 플러그인을 사용하기 전에 Maven Central에서 사용 가능한 플러그인 최신 버전을 확인합니다: [ ![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22)</span><span class="sxs-lookup"><span data-stu-id="c65f2-106">Before using the Maven plugin, check on Maven Central for the latest available version of the plugin: [![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22)</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c65f2-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c65f2-107">Prerequisites</span></span>

<span data-ttu-id="c65f2-108">이 자습서의 단계를 완료하려면 다음 필수 조건이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-108">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="c65f2-109">Azure 구독; Azure 구독이 아직 없는 경우 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-109">An Azure subscription; if you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c65f2-110">[Azure CLI(명령줄 인터페이스)]</span><span class="sxs-lookup"><span data-stu-id="c65f2-110">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="c65f2-111">최신 [JDK(Java Development Kit)], 버전 1.7 이상</span><span class="sxs-lookup"><span data-stu-id="c65f2-111">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="c65f2-112">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="c65f2-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="c65f2-113">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="c65f2-113">A [Git] client.</span></span>

## <a name="clone-the-sample-spring-boot-web-app"></a><span data-ttu-id="c65f2-114">샘플 Spring Boot 웹앱 복제</span><span class="sxs-lookup"><span data-stu-id="c65f2-114">Clone the sample Spring Boot web app</span></span>

<span data-ttu-id="c65f2-115">이 섹션에서는 완료된 Spring Boot 응용 프로그램을 복제하고 로컬로 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-115">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="c65f2-116">명령 프롬프트 또는 터미널 창을 열고 Spring Boot 응용 프로그램을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c65f2-116">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="c65f2-117">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="c65f2-117">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="c65f2-118">[Spring Boot 시작하기] 샘플 프로젝트를 만든 디렉터리에 복제합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c65f2-118">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="c65f2-119">디렉터리를 완료된 프로젝트로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c65f2-119">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="c65f2-120">Maven을 사용하여 JAR 파일을 빌드합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c65f2-120">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c65f2-121">웹앱을 만들면 Maven을 사용하여 웹앱을 시작합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c65f2-121">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="c65f2-122">웹 브라우저를 사용하여 로컬로 이동하여 웹앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-122">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="c65f2-123">예를 들어, curl을 사용할 수 있는 경우 다음 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-123">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="c65f2-124">다음과 같이 **Greetings from Spring Boot!** 라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-124">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="adjust-project-for-war-based-deployment-on-azure-app-service"></a><span data-ttu-id="c65f2-125">Azure App Service에 WAR 기반 배포에 대한 프로젝트를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-125">Adjust project for WAR-based deployment on Azure App Service</span></span>

<span data-ttu-id="c65f2-126">이 섹션에서는 기본적으로 Tomcat을 런타임으로 제공하는 Azure App Service에 WAR 파일로 배포할 Spring Boot 프로젝트를 신속하게 조정하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-126">In this section we will quickly adjust the Spring Boot project to be deployed as a WAR file on Azure App Service, which provides Tomcat as the runtime by default.</span></span> <span data-ttu-id="c65f2-127">이 작업을 위해서는 두 가지 파일이 수정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-127">For this to work, there are two files to be modified:</span></span>

- <span data-ttu-id="c65f2-128">Maven `pom.xml` 파일</span><span class="sxs-lookup"><span data-stu-id="c65f2-128">The Maven `pom.xml` file</span></span>
- <span data-ttu-id="c65f2-129">`Application` Java 클래스</span><span class="sxs-lookup"><span data-stu-id="c65f2-129">The `Application` Java class</span></span>

<span data-ttu-id="c65f2-130">Maven 설정부터 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-130">Let's start with the Maven settings:</span></span>

1. <span data-ttu-id="c65f2-131">`pom.xml` 열기</span><span class="sxs-lookup"><span data-stu-id="c65f2-131">Open `pom.xml`</span></span>

1. <span data-ttu-id="c65f2-132">맨 위에 있는 `<artifactId>` 정의 바로 뒤에 `<packaging>war</packaging>` 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-132">Add `<packaging>war</packaging>` right after the `<artifactId>` definition at the top:</span></span>
   ```xml
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.springframework</groupId>
    <artifactId>gs-spring-boot</artifactId>

    <packaging>war</packaging>
   ```

1. <span data-ttu-id="c65f2-133">다음 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-133">Add the following dependency:</span></span>
   ```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
   ```

<span data-ttu-id="c65f2-134">이제 `Application` 클래스를 열고, IDE가 새 종속성을 이미 선택했으면, 다음과 같이 수정을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-134">Now open the class `Application`, hopefully after your IDE has already picked up the new dependencies, and proceed with the following modifications:</span></span>

1. <span data-ttu-id="c65f2-135">클래스 응용프로그램을 `SpringBootServletInitializer`의 서브 클래스로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-135">Make class Application a subclass of `SpringBootServletInitializer`:</span></span>
   ```java
   @SpringBootApplication
   public class Application extends SpringBootServletInitializer {
     // ...
   }
   ```

1. <span data-ttu-id="c65f2-136">응용프로그램 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-136">Add the following method to the Application class:</span></span>
   ```java
       @Override
       protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
           return application.sources(Application.class);
       }
   ```

<span data-ttu-id="c65f2-137">이제 응용프로그램은 Tomcat 및 다른 Servlet 런타임(예: Jetty)에 배포될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-137">Your application is now ready to be deployed to Tomcat and any other Servlet runtime (e.g. Jetty).</span></span>

## <a name="add-the-maven-plugin-for-azure-app-service-web-apps"></a><span data-ttu-id="c65f2-138">Azure App Service Web Apps용 Maven 플러그인 추가</span><span class="sxs-lookup"><span data-stu-id="c65f2-138">Add the Maven Plugin for Azure App Service Web Apps</span></span>

<span data-ttu-id="c65f2-139">이 섹션에서는 Azure App Service Web Apps에 이 응용프로그램의 전체 배포를 자동화하는 Maven 플러그인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-139">In this section, we will add a Maven plugin that will automate the entire deployment of this application into Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="c65f2-140">`pom.xml`을 다시 한 번 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-140">Open `pom.xml` once again.</span></span>

1. <span data-ttu-id="c65f2-141">`<properties>` 내에서, `maven.build.timestamp.format` 속성으로 사용자 지정 타임스탬프 형식을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-141">Inside `<properties>`, set a custom timestamp format with the property `maven.build.timestamp.format`.</span></span> <span data-ttu-id="c65f2-142">Azure App Service는 응용프로그램의 공개 URL을 생성하기 때문에, 이 설정은 배포 이름을 생성하고 다른 사용자의 실시간 배포와의 충돌을 피하기 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-142">Because Azure App Service creates a public URL for your application, this setting will be used to generate the name of your deployment, and avoid conflict with other users' live deployments.</span></span>
   ```xml
    <properties>
        <java.version>1.8</java.version>
        <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
    </properties>
   ```

1. <span data-ttu-id="c65f2-143">`<plugins>` 요소에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-143">In the `<plugins>` element, add the following:</span></span>
   ```xml
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
    </plugin>
   ```

<span data-ttu-id="c65f2-144">이러한 설정을 통해, 귀하의 Maven 프로젝트는 이제 실시간으로 Azure App Service Web App에 배포될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-144">With these settings, your Maven project is now ready for live deployment to Azure App Service Web App.</span></span>

## <a name="install-and-log-in-to-azure-cli"></a><span data-ttu-id="c65f2-145">Azure CLI 설치 및 로그인</span><span class="sxs-lookup"><span data-stu-id="c65f2-145">Install and log in to Azure CLI</span></span>

<span data-ttu-id="c65f2-146">Maven Plugin이 Spring Boot 응용프로그램을 배포하도록 하는 가장 간단하고 쉬운 방법은 [ Azure CLI](https://docs.microsoft.com/cli/azure/)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-146">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](https://docs.microsoft.com/cli/azure/).</span></span> <span data-ttu-id="c65f2-147">설치되어 있는지 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="c65f2-147">Make sure you have it installed.</span></span>

1. <span data-ttu-id="c65f2-148">Azure CLI를 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-148">Sign into your Azure account by using the Azure CLI:</span></span>
   
   ```shell
   az login
   ```
   
   <span data-ttu-id="c65f2-149">지시에 따라 로그인 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-149">Follow the instructions to complete the sign-in process.</span></span>

## <a name="optionally-customize-pomxml-before-deploying"></a><span data-ttu-id="c65f2-150">또는 배포 전에 pom.xml을 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-150">Optionally, customize pom.xml before deploying</span></span>

<span data-ttu-id="c65f2-151">텍스트 편집기에서 Spring Boot 응용 프로그램에 대한 `pom.xml` 파일을 열고 `azure-webapp-maven-plugin`에 대한 `<plugin>` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-151">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="c65f2-152">이 요소는 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-152">This element should resemble the following example:</span></span>

   ```xml
  <plugins>
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
      <configuration>
         <resourceGroup>maven-projects</resourceGroup>
         <appName>${project.artifactId}-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>war</deploymentType>
      </configuration>
    </plugin>
  </plugins>
   ```

<span data-ttu-id="c65f2-153">Maven 플러그 인에 대해 수정할 수 있는 여러 값이 있으며 이러한 각 요소에 대한 자세한 설명을 [Azure Web Apps의 Maven 플러그 인] 설명서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-153">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="c65f2-154">즉, 이 문서에서 강조 표시된 값은 여러 개입니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-154">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="c65f2-155">요소</span><span class="sxs-lookup"><span data-stu-id="c65f2-155">Element</span></span> | <span data-ttu-id="c65f2-156">설명</span><span class="sxs-lookup"><span data-stu-id="c65f2-156">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="c65f2-157">[Azure Web Apps의 Maven 플러그 인] 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-157">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="c65f2-158">[Maven 중앙 리포지토리](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22)에 나열된 버전을 검사하여 최신 버전을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-158">Verify the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="c65f2-159">대상 리소스 그룹, 즉, 이 예에서 `maven-plugin`을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-159">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="c65f2-160">리소스 그룹이 아직 존재하지 않는 경우 배포 중에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-160">The resource group is created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="c65f2-161">웹앱에 대한 대상 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-161">Specifies the target name for your web app.</span></span> <span data-ttu-id="c65f2-162">이 예제에서는 대상 이름은 `maven-web-app-${maven.build.timestamp}`이며 이 예제에서 충돌을 피하기 위해 여기에 `${maven.build.timestamp}` 접미사가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-162">In this example, the target name is `maven-web-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="c65f2-163">(타임스탬프는 선택 사항입니다. 앱 이름에 대한 고유한 문자열을 지정할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="c65f2-163">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="c65f2-164">대상 지역을 지정합니다. 이 예제에서는 `westus`입니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-164">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="c65f2-165">(전체 목록은 [Azure Web Apps의 Maven 플러그 인] 설명서에서 제공됩니다.)</span><span class="sxs-lookup"><span data-stu-id="c65f2-165">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<javaVersion>` | <span data-ttu-id="c65f2-166">웹앱에 Java 런타임 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-166">Specifies the Java runtime version for your web app.</span></span> <span data-ttu-id="c65f2-167">(전체 목록은 [Azure Web Apps의 Maven 플러그 인] 설명서에서 제공됩니다.)</span><span class="sxs-lookup"><span data-stu-id="c65f2-167">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<deploymentType>` | <span data-ttu-id="c65f2-168">웹앱의 배포 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-168">Specifies deployment type for your web app.</span></span> <span data-ttu-id="c65f2-169">기본값은 `war`입니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-169">Default is `war`.</span></span> |

## <a name="build-and-deploy-your-web-app-to-azure"></a><span data-ttu-id="c65f2-170">Azure에 웹앱 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="c65f2-170">Build and deploy your web app to Azure</span></span>

<span data-ttu-id="c65f2-171">이 문서의 이전 섹션에서 설정을 모두 구성했으면 웹앱을 Azure에 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-171">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="c65f2-172">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-172">To do so, use the following steps:</span></span>

1. <span data-ttu-id="c65f2-173">*pom.xml* 파일을 변경한 경우 이전에 사용하던 명령 프롬프트 또는 터미널 창에서 Maven를 사용하여 JAR 파일을 다시 작성합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c65f2-173">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c65f2-174">Maven을 사용하여 Azure에 웹앱을 배포합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c65f2-174">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="c65f2-175">Maven은 Azure에 웹앱을 배포합니다. 웹앱이 아직 없는 경우 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-175">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

<span data-ttu-id="c65f2-176">웹을 배포하면 [Azure Portal]을 사용하여 작업을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-176">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="c65f2-177">웹앱은 **App Services**에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-177">Your web app will be listed in **App Services**:</span></span>

   ![Azure Portal App Services에 나열된 웹앱][AP01]

* <span data-ttu-id="c65f2-179">웹앱의 URL은 웹앱의 **개요**에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="c65f2-179">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![웹앱의 URL 확인][AP02]

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="c65f2-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c65f2-181">Next steps</span></span>

<span data-ttu-id="c65f2-182">이 문서에서 설명하는 다양한 기술에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c65f2-182">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="c65f2-183">[Azure Web Apps의 Maven 플러그 인]</span><span class="sxs-lookup"><span data-stu-id="c65f2-183">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="c65f2-184">Azure CLI에서 Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="c65f2-184">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="c65f2-185">Azure Web Apps의 Maven 플러그 인을 사용하여 컨테이너화된 Spring Boot 앱을 Azure에 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="c65f2-185">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="c65f2-186">Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="c65f2-186">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="c65f2-187">Maven 설정 참조</span><span class="sxs-lookup"><span data-stu-id="c65f2-187">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot 시작하기]: https://github.com/spring-guides/gs-spring-boot
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Azure Web Apps의 Maven 플러그 인]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme
[Maven Plugin for Azure Web Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
