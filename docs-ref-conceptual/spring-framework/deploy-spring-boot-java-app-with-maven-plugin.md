---
title: Maven 및 Azure를 사용하여 Spring Boot JAR 파일 앱을 클라우드에 배포
description: Linux용 Azure Web Apps의 Maven 플러그 인을 사용하여 Spring Boot 앱을 클라우드에 배포하는 방법에 대해 알아봅니다.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.author: robmcm;kevinzha;brborges
ms.date: 10/04/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: 36afcc764c1cb984779518ddec004ecbfa1b7c57
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48876397"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a><span data-ttu-id="bdf9c-103">Linux에 Azure App Service에 Spring Boot JAR 파일 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="bdf9c-103">Deploy a Spring Boot JAR file web app to Azure App Service on Linux</span></span>

<span data-ttu-id="bdf9c-104">이 문서에서는 [Azure App Service Web Apps용 Maven Plugin](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme)을 사용하여 Java SE JAR로 패키지된 Spring Boot 응용 프로그램을 [Linux의 Azure App Service](https://docs.microsoft.com/en-us/azure/app-service/containers/)에 배포하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-104">This article demonstrates using the [Maven Plugin for Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) to deploy a Spring Boot application packaged as a Java SE JAR to [Azure App Service on Linux](https://docs.microsoft.com/en-us/azure/app-service/containers/).</span></span> <span data-ttu-id="bdf9c-105">앱의 의존성, 런타임 및 구성을 배포 가능한 단일 아티팩트에 통합하려면 [Tomcat 및 WAR 파일](/azure/app-service/containers/quickstart-java) 상 Java SE 배포를 선택하십시오.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-105">Choose Java SE deployment over [Tomcat and WAR files](/azure/app-service/containers/quickstart-java) when you want to consolidate your app's depedencies, runtime, and configuration into a single deployable artifact.</span></span>


<span data-ttu-id="bdf9c-106">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-106">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdf9c-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="bdf9c-107">Prerequisites</span></span>

<span data-ttu-id="bdf9c-108">이 자습서의 단계를 완료하려면 다음이 설치 및 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-108">To complete the steps in this tutorial, you'll need to have the following installed and configured:</span></span>

* <span data-ttu-id="bdf9c-109">[Azure CLI](/cli/azure/), 로컬로 또는 [Azure Cloud Shell](https://shell.azure.com)을 통해.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-109">The [Azure CLI](/cli/azure/), either locally or through [Azure Cloud Shell](https://shell.azure.com).</span></span>
* <span data-ttu-id="bdf9c-110">[JDK(Java Development Kit)](https://www.azul.com/downloads/azure-only/zulu/), 버전 1.7 이상</span><span class="sxs-lookup"><span data-stu-id="bdf9c-110">[Java Development Kit (JDK)](https://www.azul.com/downloads/azure-only/zulu/), version 1.7 or later.</span></span>
* <span data-ttu-id="bdf9c-111">Apache [Maven](https://maven.apache.org/), 버전 3).</span><span class="sxs-lookup"><span data-stu-id="bdf9c-111">Apache's [Maven](https://maven.apache.org/), Version 3).</span></span>
* <span data-ttu-id="bdf9c-112">[Git](https://git-scm.com/downloads) 클라이언트</span><span class="sxs-lookup"><span data-stu-id="bdf9c-112">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="clone-the-sample-app"></a><span data-ttu-id="bdf9c-113">샘플 앱 복제</span><span class="sxs-lookup"><span data-stu-id="bdf9c-113">Clone the sample app</span></span>

<span data-ttu-id="bdf9c-114">이 섹션에서는 완료된 Spring Boot 응용 프로그램을 복제하고 로컬로 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-114">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="bdf9c-115">명령 프롬프트 또는 터미널 창을 열고 Spring Boot 응용 프로그램을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="bdf9c-115">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="bdf9c-116">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="bdf9c-116">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="bdf9c-117">[Spring Boot 시작하기] 샘플 프로젝트를 만든 디렉터리에 복제합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="bdf9c-117">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="bdf9c-118">디렉터리를 완료된 프로젝트로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="bdf9c-118">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="bdf9c-119">Maven을 사용하여 JAR 파일을 빌드합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="bdf9c-119">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="bdf9c-120">웹앱을 만들면 Maven을 사용하여 웹앱을 시작합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="bdf9c-120">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="bdf9c-121">웹 브라우저를 사용하여 로컬로 이동하여 웹앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-121">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="bdf9c-122">예를 들어, curl을 사용할 수 있는 경우 다음 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-122">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="bdf9c-123">다음과 같이 **Greetings from Spring Boot!** 라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-123">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="configure-maven-plugin-for-azure-app-service"></a><span data-ttu-id="bdf9c-124">Azure App Service용 Maven 플러그인 구성</span><span class="sxs-lookup"><span data-stu-id="bdf9c-124">Configure Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="bdf9c-125">이 섹션에서는 Maven이 Linux의 Azure App Service에 앱을 배포할 수 있도록 Spring Boot프로젝트 `pom.xml`를 구성할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-125">In this section, you will configure the the Spring Boot project `pom.xml` so that Maven can deploy the app to Azure App Service on Linux.</span></span>

1. <span data-ttu-id="bdf9c-126">코드 편집기에서 `pom.xml`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-126">Open `pom.xml` in a code editor.</span></span>

1. <span data-ttu-id="bdf9c-127">pom.xml의 `<build>` 섹션에서 `<plugins>` 태그 안에 다음 `<plugin>` 항목을 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-127">In the `<build>` section of the pom.xml, add the following `<plugin>` entry inside the `<plugins>` tag.</span></span>

   ```xml
  <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.4.0</version>
    <configuration>
      <deploymentType>jar</deploymentType>

      <!-- configure app to run on port 80, required by App Service -->
      <appSettings>
        <property> 
          <name>JAVA_OPTS</name> 
          <value>-Dserver.port=80</value> 
        </property> 
      </appSettings>

      <!-- Web App information -->
      <resourceGroup>${RESOURCEGROUP_NAME}</resourceGroup>
      <appName>${WEBAPP_NAME}</appName>
      <region>${REGION}</region>  

      <!-- Java Runtime Stack for Web App on Linux-->
      <linuxRuntime>jre8</linuxRuntime>
    </configuration>
  </plugin>
  ```

1. <span data-ttu-id="bdf9c-128">플러그인 구성에서 다음 자리 표시자를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-128">Update the following placeholders in the plugin configuration:</span></span>

| <span data-ttu-id="bdf9c-129">Placeholder</span><span class="sxs-lookup"><span data-stu-id="bdf9c-129">Placeholder</span></span> | <span data-ttu-id="bdf9c-130">설명</span><span class="sxs-lookup"><span data-stu-id="bdf9c-130">Description</span></span> |
| ----------- | ----------- |
| `RESOURCEGROUP_NAME` | <span data-ttu-id="bdf9c-131">웹앱을 만들 새 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-131">Name for the new resource group in which to create your web app.</span></span> <span data-ttu-id="bdf9c-132">앱의 모든 리소스를 한 그룹에 배치하여 다 함께 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-132">By putting all the resources for an app in a group, you can manage them together.</span></span> <span data-ttu-id="bdf9c-133">예를 들어 리소스 그룹을 삭제하면 앱과 연결된 모든 리소스가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-133">For example, deleting the resource group would delete all resources associated with the app.</span></span> <span data-ttu-id="bdf9c-134">이 값을 고유한 새 리소스 그룹(예: *TestResources*)으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-134">Update this value with a unique new resource group name, for example, *TestResources*.</span></span> <span data-ttu-id="bdf9c-135">이 리소스 그룹 이름을 사용하여 이후 섹션에서 모든 Azure 리소스를 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-135">You will use this resource group name to clean up all Azure resources in a later section.</span></span> |
| `WEBAPP_NAME` | <span data-ttu-id="bdf9c-136">앱 이름은 Azure(WEBAPP_NAME.azurewebsites.net)에 배포할 때 웹앱에 대한 호스트 이름의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-136">The app name will be part the host name for the web app when deployed to Azure (WEBAPP_NAME.azurewebsites.net).</span></span> <span data-ttu-id="bdf9c-137">이 값을 Java 앱을 호스팅할 새 Azure 웹앱의 고유 이름(예: *contoso*)으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-137">Update this value with a unique name for the new Azure web app, which will host your Java app, for example *contoso*.</span></span> |
| `REGION` | <span data-ttu-id="bdf9c-138">웹앱이 호스팅되는 Azure 지역입니다(예: `westus2`).</span><span class="sxs-lookup"><span data-stu-id="bdf9c-138">An Azure region where the web app is hosted, for example `westus2`.</span></span> <span data-ttu-id="bdf9c-139">`az account list-locations` 명령을 사용하여 Cloud Shell 또는 CLI에서 지역 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-139">You can get a list of regions from the Cloud Shell or CLI using the `az account list-locations` command.</span></span> |

<span data-ttu-id="bdf9c-140">구성 옵션의 전체 목록을 [GitHub의 Maven 플러그 인 참조](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-140">A full list of configuration options can be found in the [Maven plugin reference on GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).</span></span>

## <a name="install-and-log-in-to-azure-cli"></a><span data-ttu-id="bdf9c-141">Azure CLI 설치 및 로그인</span><span class="sxs-lookup"><span data-stu-id="bdf9c-141">Install and log in to Azure CLI</span></span>

<span data-ttu-id="bdf9c-142">Maven Plugin이 Spring Boot 응용프로그램을 배포하도록 하는 가장 간단하고 쉬운 방법은 [ Azure CLI](https://docs.microsoft.com/cli/azure/)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-142">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](https://docs.microsoft.com/cli/azure/).</span></span>

1. <span data-ttu-id="bdf9c-143">Azure CLI를 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-143">Sign into your Azure account by using the Azure CLI:</span></span>
   
   ```shell
   az login
   ```
   
   <span data-ttu-id="bdf9c-144">지시에 따라 로그인 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-144">Follow the instructions to complete the sign-in process.</span></span>

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="bdf9c-145">Azure에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="bdf9c-145">Deploy the app to Azure</span></span>

<span data-ttu-id="bdf9c-146">이 문서의 이전 섹션에서 설정을 모두 구성했으면 웹앱을 Azure에 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-146">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="bdf9c-147">이렇게 하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-147">To do so, use the following steps:</span></span>

1. <span data-ttu-id="bdf9c-148">*pom.xml* 파일을 변경한 경우 이전에 사용하던 명령 프롬프트 또는 터미널 창에서 Maven를 사용하여 JAR 파일을 다시 작성합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="bdf9c-148">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="bdf9c-149">Maven을 사용하여 Azure에 웹앱을 배포합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="bdf9c-149">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="bdf9c-150">Maven은 Azure에 웹앱을 배포합니다. 웹앱이나 웹앱 플랜이 아직 없는 경우 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-150">Maven will deploy your web app to Azure; if the web app or web app plan does not already exist, it will be created for you.</span></span>

<span data-ttu-id="bdf9c-151">웹을 배포하면 [Azure Portal]을 사용하여 작업을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-151">When your web has been deployed, you will be able to manage it through the [Azure portal].</span></span>

* <span data-ttu-id="bdf9c-152">웹앱은 **App Services**에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-152">Your web app will be listed in **App Services**:</span></span>

   ![Azure Portal App Services에 나열된 웹앱][AP01]

* <span data-ttu-id="bdf9c-154">웹앱의 URL은 웹앱의 **개요**에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-154">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![웹앱의 URL 확인][AP02]

<span data-ttu-id="bdf9c-156">`localhost` 대신 포털의 웹앱 URL을 사용하여 이전과 동일한 cURL 명령을 사용하여 배포가 성공적으로 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-156">Verify that the deployment was successful by using the same cURL command as before, using your web app URL from the Portal instead of `localhost`.</span></span> <span data-ttu-id="bdf9c-157">다음과 같이 **Greetings from Spring Boot!** 라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-157">You should see the following message displayed: **Greetings from Spring Boot!**</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bdf9c-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bdf9c-158">Next steps</span></span>

<span data-ttu-id="bdf9c-159">이 문서에서 설명하는 다양한 기술에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bdf9c-159">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="bdf9c-160">[Azure Web Apps의 Maven 플러그 인]</span><span class="sxs-lookup"><span data-stu-id="bdf9c-160">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="bdf9c-161">Azure Web Apps의 Maven 플러그 인을 사용하여 컨테이너화된 Spring Boot 앱을 Azure에 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="bdf9c-161">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="bdf9c-162">Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="bdf9c-162">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="bdf9c-163">Maven 설정 참조</span><span class="sxs-lookup"><span data-stu-id="bdf9c-163">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
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
