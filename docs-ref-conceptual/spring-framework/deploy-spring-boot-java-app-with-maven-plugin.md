---
title: "Maven 및 Azure를 사용하여 Spring Boot 앱을 클라우드에 배포"
description: "Azure Web Apps의 Maven 플러그 인을 사용하여 Spring Boot 앱을 클라우드에 배포하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 17c358317d1b96521de87f263a92fa2d7c0ff26c
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-web-apps"></a><span data-ttu-id="8cc33-103">Azure Web Apps의 Maven 플러그 인을 사용하여 Spring Boot 앱을 클라우드에 배포</span><span class="sxs-lookup"><span data-stu-id="8cc33-103">Deploy a Spring Boot app to the cloud using the Maven Plugin for Azure Web Apps</span></span>

<span data-ttu-id="8cc33-104">이 문서에서는 Azure Web Apps의 Maven 플러그 인을 사용하여 Azure App Services에 샘플 Spring Boot 응용 프로그램을 배포하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-104">This article demonstrates using the Maven Plugin for Azure Web Apps to deploy a sample Spring Boot application to Azure App Services.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="8cc33-105">[Apache Maven](http://maven.apache.org/)에서 [Azure Web Apps의 Maven 플러그 인](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin)은 Maven 프로젝트에 Azure App Service의 원활한 통합을 제공하고 Azure App Service에 웹앱을 배포하는 개발자를 위한 프로세스를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-105">The [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>
> 
> <span data-ttu-id="8cc33-106">Azure Web Apps의 Maven 플러그 인은 현재 미리 보기로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="8cc33-107">지금은 FTP 게시만 지원되지만 향후에 기능이 추가될 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="8cc33-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8cc33-108">Prerequisites</span></span>

<span data-ttu-id="8cc33-109">이 자습서의 단계를 완료하려면 다음 필수 조건이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="8cc33-110">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정{]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="8cc33-111">[Azure CLI(명령줄 인터페이스)]</span><span class="sxs-lookup"><span data-stu-id="8cc33-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="8cc33-112">최신 [JDK(Java Development Kit)], 버전 1.7 이상</span><span class="sxs-lookup"><span data-stu-id="8cc33-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="8cc33-113">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="8cc33-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="8cc33-114">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="8cc33-114">A [Git] client.</span></span>

## <a name="clone-the-sample-spring-boot-web-app"></a><span data-ttu-id="8cc33-115">샘플 Spring Boot 웹앱 복제</span><span class="sxs-lookup"><span data-stu-id="8cc33-115">Clone the sample Spring Boot web app</span></span>

<span data-ttu-id="8cc33-116">이 섹션에서는 완료된 Spring Boot 응용 프로그램을 복제하고 로컬로 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-116">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="8cc33-117">명령 프롬프트 또는 터미널 창을 열고 Spring Boot 응용 프로그램을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8cc33-117">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="8cc33-118">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="8cc33-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="8cc33-119">[Spring Boot 시작하기] 샘플 프로젝트를 만든 디렉터리에 복제합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8cc33-119">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="8cc33-120">디렉터리를 완료된 프로젝트로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8cc33-120">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="8cc33-121">Maven을 사용하여 JAR 파일을 빌드합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8cc33-121">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="8cc33-122">웹앱을 만들면 Maven을 사용하여 웹앱을 시작합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8cc33-122">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="8cc33-123">웹 브라우저를 사용하여 로컬로 이동하여 웹앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-123">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="8cc33-124">예를 들어, curl을 사용할 수 있는 경우 다음 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-124">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="8cc33-125">다음과 같이 **Greetings from Spring Boot!**라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-125">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="8cc33-126">Azure 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="8cc33-126">Create an Azure service principal</span></span>

<span data-ttu-id="8cc33-127">이 섹션에서는 웹앱을 Azure에 배포할 때 Maven 플러그 인에서 사용하는 Azure 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-127">In this section, you create an Azure service principal that the Maven plugin uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="8cc33-128">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-128">Open a command prompt.</span></span>

1. <span data-ttu-id="8cc33-129">Azure CLI를 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-129">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="8cc33-130">지시에 따라 로그인 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-130">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="8cc33-131">Azure 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="8cc33-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="8cc33-132">여기서 `uuuuuuuu`는 사용자 이름이고 `pppppppp`는 서비스 사용자에 대한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-132">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="8cc33-133">Azure는 다음 예제와 유사한 JSON로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-133">Azure responds with JSON that resembles the following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="8cc33-134">웹앱을 Azure에 배포하도록 Maven 플러그 인을 구성하는 경우 이 JSON 응답의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-134">You will use the values from this JSON response when you configure the Maven plugin to deploy your web app to Azure.</span></span> <span data-ttu-id="8cc33-135">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` 및 `tttttttt`는 다음 섹션에서 Maven `settings.xml` 파일을 구성할 때 이러한 값을 해당 요소에 쉽게 매핑할 수 있도록 이 예제에서 사용되는 자리 표시자 값입니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-135">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="8cc33-136">Azure 서비스 주체를 사용하도록 Maven 구성</span><span class="sxs-lookup"><span data-stu-id="8cc33-136">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="8cc33-137">이 섹션에서는 Maven에서 웹앱을 Azure에 배포할 때 사용할 인증을 구성하기 위해 Azure 서비스 주체의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-137">In this section, you use the values from your Azure service principal to configure the authentication that Maven uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="8cc33-138">텍스트 편집기에서 Maven `settings.xml` 파일을 엽니다. 이 파일은 다음 예제와 같은 경로에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-138">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="8cc33-139">*settings.xml* 파일의 `<servers>` 컬렉션에 이 자습서의 이전 섹션에 있는 Azure 서비스 주체 설정을 추가합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8cc33-139">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="8cc33-140">위치:</span><span class="sxs-lookup"><span data-stu-id="8cc33-140">Where:</span></span>
   | <span data-ttu-id="8cc33-141">요소</span><span class="sxs-lookup"><span data-stu-id="8cc33-141">Element</span></span> | <span data-ttu-id="8cc33-142">설명</span><span class="sxs-lookup"><span data-stu-id="8cc33-142">Description</span></span> |
   |---|---|
   | `<id>` | <span data-ttu-id="8cc33-143">Azure에 웹앱을 배포할 때 Maven을 사용하여 보안 설정을 조회하는 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-143">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span> |
   | `<client>` | <span data-ttu-id="8cc33-144">서비스 사용자의 `appId` 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-144">Contains the `appId` value from your service principal.</span></span> |
   | `<tenant>` | <span data-ttu-id="8cc33-145">서비스 사용자의 `tenant` 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-145">Contains the `tenant` value from your service principal.</span></span> |
   | `<key>` | <span data-ttu-id="8cc33-146">서비스 사용자의 `password` 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-146">Contains the `password` value from your service principal.</span></span> |
   | `<environment>` | <span data-ttu-id="8cc33-147">대상 Azure 클라우드 환경을 정의합니다. 이 예에서는 `AZURE`입니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-147">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="8cc33-148">(환경의 전체 목록은 [Azure Web Apps의 Maven 플러그 인] 설명서에서 제공됩니다.)</span><span class="sxs-lookup"><span data-stu-id="8cc33-148">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |

1. <span data-ttu-id="8cc33-149">*settings.xml* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-149">Save and close the *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-to-azure"></a><span data-ttu-id="8cc33-150">선택 사항: 웹앱을 Azure에 배포하기 전에 pom.xml 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="8cc33-150">OPTIONAL: Customize your pom.xml before deploying your web app to Azure</span></span>

<span data-ttu-id="8cc33-151">텍스트 편집기에서 Spring Boot 응용 프로그램에 대한 `pom.xml` 파일을 열고 `azure-webapp-maven-plugin`에 대한 `<plugin>` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-151">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="8cc33-152">이 요소는 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-152">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="8cc33-153">Maven 플러그 인에 대해 수정할 수 있는 여러 값이 있으며 이러한 각 요소에 대한 자세한 설명을 [Azure Web Apps의 Maven 플러그 인] 설명서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-153">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="8cc33-154">즉, 이 문서에서 강조 표시된 값은 여러 개입니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-154">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="8cc33-155">요소</span><span class="sxs-lookup"><span data-stu-id="8cc33-155">Element</span></span> | <span data-ttu-id="8cc33-156">설명</span><span class="sxs-lookup"><span data-stu-id="8cc33-156">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="8cc33-157">[Azure Web Apps의 Maven 플러그 인] 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-157">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="8cc33-158">[Maven 중앙 리포지토리](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22)에 나열된 버전을 검사하여 최신 버전을 사용하고 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-158">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<authentication>` | <span data-ttu-id="8cc33-159">Azure에 대한 인증 정보를 지정합니다. 이 예제에서는 `azure-auth`이 포함된 `<serverId>` 요소를 포함합니다. Maven에서는 해당 값을 사용하여 이 문서의 이전 섹션에 정의된 Maven *settings.xml* 파일에서 Azure 서비스 주체 값을 조회합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-159">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="8cc33-160">대상 리소스 그룹, 즉, 이 예에서 `maven-plugin`을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-160">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="8cc33-161">리소스 그룹이 아직 존재하지 않는 경우 배포 중에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-161">The resource group is created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="8cc33-162">웹앱에 대한 대상 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-162">Specifies the target name for your web app.</span></span> <span data-ttu-id="8cc33-163">이 예제에서는 대상 이름은 `maven-web-app-${maven.build.timestamp}`이며 이 예제에서 충돌을 피하기 위해 여기에 `${maven.build.timestamp}` 접미사가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-163">In this example, the target name is `maven-web-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="8cc33-164">(타임스탬프는 선택 사항입니다. 앱 이름에 대한 고유한 문자열을 지정할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="8cc33-164">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="8cc33-165">대상 지역을 지정합니다. 이 예제에서는 `westus`입니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-165">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="8cc33-166">(전체 목록은 [Azure Web Apps의 Maven 플러그 인] 설명서에서 제공됩니다.)</span><span class="sxs-lookup"><span data-stu-id="8cc33-166">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<javaVersion>` | <span data-ttu-id="8cc33-167">웹앱에 Java 런타임 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-167">Specifies the Java runtime version for your web app.</span></span> <span data-ttu-id="8cc33-168">(전체 목록은 [Azure Web Apps의 Maven 플러그 인] 설명서에서 제공됩니다.)</span><span class="sxs-lookup"><span data-stu-id="8cc33-168">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<deploymentType>` | <span data-ttu-id="8cc33-169">웹앱의 배포 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="8cc33-170">지금은 `ftp`만 지원되지만 다른 배포 형식의 지원을 개발 중입니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-170">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span> |
| `<resources>` | <span data-ttu-id="8cc33-171">Maven이 Azure에 웹앱을 배포할 때 사용하는 리소스 및 대상을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-171">Specifies resources and target destinations which Maven uses when deploying your web app to Azure.</span></span> <span data-ttu-id="8cc33-172">이 예제에서 두 개의 `<resource>` 요소는 Maven이 웹앱에 JAR 파일을 배포하고 Spring Boot 프로젝트에서 *web.config* 파일을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-172">In this example, two `<resource>` elements specify that Maven will deploy the JAR file for your web app and the *web.config* file from the Spring Boot project.</span></span> |

## <a name="build-and-deploy-your-web-app-to-azure"></a><span data-ttu-id="8cc33-173">Azure에 웹앱 빌드 및 배포</span><span class="sxs-lookup"><span data-stu-id="8cc33-173">Build and deploy your web app to Azure</span></span>

<span data-ttu-id="8cc33-174">이 문서의 이전 섹션에서 설정을 모두 구성했으면 웹앱을 Azure에 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-174">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="8cc33-175">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-175">To do so, use the following steps:</span></span>

1. <span data-ttu-id="8cc33-176">*pom.xml* 파일을 변경한 경우 이전에 사용하던 명령 프롬프트 또는 터미널 창에서 Maven를 사용하여 JAR 파일을 다시 작성합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8cc33-176">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="8cc33-177">Maven을 사용하여 Azure에 웹앱을 배포합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8cc33-177">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="8cc33-178">Maven은 Azure에 웹앱을 배포합니다. 웹앱이 아직 없는 경우 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-178">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

<span data-ttu-id="8cc33-179">웹을 배포하면 [Azure Portal]을 사용하여 작업을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-179">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="8cc33-180">웹앱은 **App Services**에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-180">Your web app will be listed in **App Services**:</span></span>

   ![Azure Portal App Services에 나열된 웹앱][AP01]

* <span data-ttu-id="8cc33-182">웹앱의 URL은 웹앱의 **개요**에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="8cc33-182">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8cc33-184">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8cc33-184">Next steps</span></span>

<span data-ttu-id="8cc33-185">이 문서에서 설명하는 다양한 기술에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8cc33-185">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="8cc33-186">[Azure Web Apps의 Maven 플러그 인]</span><span class="sxs-lookup"><span data-stu-id="8cc33-186">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="8cc33-187">Azure CLI에서 Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="8cc33-187">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="8cc33-188">Azure Web Apps의 Maven 플러그 인을 사용하여 컨테이너화된 Spring Boot 앱을 Azure에 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="8cc33-188">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="8cc33-189">Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="8cc33-189">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="8cc33-190">Maven 설정 참조</span><span class="sxs-lookup"><span data-stu-id="8cc33-190">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[체험판 Azure 계정{]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot 시작하기]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Azure Web Apps의 Maven 플러그 인]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
