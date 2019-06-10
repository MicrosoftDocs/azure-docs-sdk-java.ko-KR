---
title: Azure App Service on Linux를 통해 Spring 및 Cosmos DB를 사용하는 방법
description: 이 문서에서는 Azure App Service on Linux에서 Java 웹앱을 빌드, 구성, 배포, 문제 해결 및 확장하는 프로세스를 단계별로 연습합니다.
documentationcenter: java
author: bmitchell287
ms.author: brendm; joshuapa
ms.date: 4/24/2019
ms.devlang: java
ms.service: app-service, cosmos-db
ms.topic: article
ms.openlocfilehash: 5d209c0670d6f4265b1237e7b8cff45faa9bb5d8
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2019
ms.locfileid: "64568636"
---
# <a name="how-to-use-spring-and-cosmos-db-with-app-service-on-linux"></a><span data-ttu-id="8f3b3-103">Azure App Service on Linux를 통해 Spring 및 Cosmos DB를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="8f3b3-103">How to use Spring and Cosmos DB with App Service on Linux</span></span>

## <a name="overview"></a><span data-ttu-id="8f3b3-104">개요</span><span class="sxs-lookup"><span data-stu-id="8f3b3-104">Overview</span></span>

<span data-ttu-id="8f3b3-105">이 문서에서는 Azure App Service on Linux에서 Java 웹앱을 빌드, 구성, 배포, 문제 해결 및 확장하는 프로세스를 단계별로 연습합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-105">This article will walk you through the process of building, configuring, deploying, troubleshooting, and scaling Java Web apps in Azure App Service on Linux.</span></span>

<span data-ttu-id="8f3b3-106">즉, 다음 구성 요소의 사용법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-106">It will demonstrate the usage of the following components:</span></span>

- [<span data-ttu-id="8f3b3-107">Azure Cosmos DB SQL API를 사용하는 Spring Boot Starter</span><span class="sxs-lookup"><span data-stu-id="8f3b3-107">Spring Boot Starter with the Azure Cosmos DB SQL API</span></span>](configure-spring-boot-starter-java-app-with-cosmos-db.md)
- [<span data-ttu-id="8f3b3-108">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8f3b3-108">Azure Cosmos DB</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/sql-api-introduction)
- [<span data-ttu-id="8f3b3-109">App Service Linux</span><span class="sxs-lookup"><span data-stu-id="8f3b3-109">App Service Linux</span></span>](https://docs.microsoft.com/en-us/azure/app-service/containers/app-service-linux-intro)

## <a name="prerequisites"></a><span data-ttu-id="8f3b3-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8f3b3-110">Prerequisites</span></span>

<span data-ttu-id="8f3b3-111">이 문서의 단계를 수행하기 위해 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-111">The following prerequisites are required in order to follow the steps in this article:</span></span>

- <span data-ttu-id="8f3b3-112">Java 웹앱을 클라우드에 배포하려면 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-112">In order to deploy a Java Web app to cloud, you need an Azure subscription.</span></span> <span data-ttu-id="8f3b3-113">Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 Azure 계정]((https://azure.microsoft.com/pricing/free-trial/))에 가입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-113">If you do not already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account]((https://azure.microsoft.com/pricing/free-trial/)).</span></span>
- [<span data-ttu-id="8f3b3-114">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8f3b3-114">Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
- [<span data-ttu-id="8f3b3-115">Java 8 JDK</span><span class="sxs-lookup"><span data-stu-id="8f3b3-115">Java 8 JDK</span></span>](https://docs.microsoft.com/java/azure/jdk/java-jdk-install)
- [<span data-ttu-id="8f3b3-116">Maven 3</span><span class="sxs-lookup"><span data-stu-id="8f3b3-116">Maven 3</span></span>](http://maven.apache.org/)

## <a name="clone-the-sample-java-web-app-repository"></a><span data-ttu-id="8f3b3-117">샘플 Java 웹앱 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="8f3b3-117">Clone the Sample Java Web App Repository</span></span>
<span data-ttu-id="8f3b3-118">이 연습을 위해 [Spring Boot](https://spring.io/projects/spring-boot), [Spring Data for Cosmos DB](https://docs.microsoft.com/en-us/java/azure/spring-framework/configure-spring-boot-starter-java-app-with-cosmos-db?view=azure-java-stable) 및 [Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/sql-api-introduction)를 사용하여 빌드된 Java 애플리케이션인 Spring Todo 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-118">For this exercise you'll be using the Spring Todo app, which is a Java application built using [Spring Boot](https://spring.io/projects/spring-boot), [Spring Data for Cosmos DB](https://docs.microsoft.com/en-us/java/azure/spring-framework/configure-spring-boot-starter-java-app-with-cosmos-db?view=azure-java-stable) and [Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/sql-api-introduction).</span></span>
1. <span data-ttu-id="8f3b3-119">Spring Todo 앱을 복제하고 **.prep** 폴더의 내용을 복사하여 프로젝트를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-119">Clone the Spring Todo app and copy the contents of the **.prep** folder to initialize the project:</span></span>

    <span data-ttu-id="8f3b3-120">Bash의 경우:</span><span class="sxs-lookup"><span data-stu-id="8f3b3-120">For bash:</span></span>
    ```bash
    git clone --recurse-submodules https://github.com/Azure-Samples/e2e-java-experience-in-app-service-linux-part-2.git
    yes | cp -rf .prep/* .
    ```

    <span data-ttu-id="8f3b3-121">Windows의 경우:</span><span class="sxs-lookup"><span data-stu-id="8f3b3-121">For Windows:</span></span>
    ```cmd
    git clone --recurse-submodules https://github.com/Azure-Samples/e2e-java-experience-in-app-service-linux-part-2.git
    cd e2e-java-experience-in-app-service-linux-part-2
    xcopy .prep /f /s /e /y
    ```

2. <span data-ttu-id="8f3b3-122">디렉터리를 복제된 리포지토리의 다음 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-122">Change the directory to the following folder in the cloned repo:</span></span>

   ```bash
   cd initial\spring-todo-app
   ``` 
## <a name="create-an-azure-cosmos-db-from-azure-cli"></a><span data-ttu-id="8f3b3-123">Azure CLI에서 Azure Cosmos DB를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-123">Create an Azure Cosmos DB from Azure CLI</span></span>

1. <span data-ttu-id="8f3b3-124">Azure CLI에 로그인하고 구독 ID를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-124">Login to your Azure CLI, and set your subscription id.</span></span>

    ```bash
    az login
    ```

2. <span data-ttu-id="8f3b3-125">필요한 경우 구독 ID를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-125">Set the subscription id if needed.</span></span>
    ```bash
    az account set -s <your-subscription-id>
    ```

3. <span data-ttu-id="8f3b3-126">Azure 리소스 그룹을 만들고 리소스 그룹 이름을 나중에 사용할 수 있도록 메모합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-126">Create an Azure resource group, and write down the resource group name for later use.</span></span>

    ```bash
    az group create -n <your-azure-group-name> \
    -l <your-resource-group-region>
    ```

4. <span data-ttu-id="8f3b3-127">Cosmos DB를 생성하고 GlobalDocumentDB 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-127">Create the Cosmos DB and specify the type as GlobalDocumentDB.</span></span>
<span data-ttu-id="8f3b3-128">Cosmos DB의 이름은 소문자만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-128">The name of the Cosmos DB must use only lower case letters.</span></span> <span data-ttu-id="8f3b3-129">응답에서 `documentEndpoint` 필드에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-129">Make sure to note the `documentEndpoint` field in the response.</span></span> <span data-ttu-id="8f3b3-130">이 필드는 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-130">You'll need this later.</span></span>

    ```bash
    az cosmosdb create --kind GlobalDocumentDB \
        -g <your-azure-group-name> \
        -n <your-azure-COSMOS-DB-name-in-lower-case-letters>
     ```

4. <span data-ttu-id="8f3b3-131">Azure Cosmos DB 키를 가져오고 `primaryMasterKey` 값을 나중에 사용할 수 있도록 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-131">Get your Azure Cosmos DB keys, record the `primaryMasterKey` value for later use.</span></span>

    ```bash
    az cosmosdb list-keys -g <your-azure-group-name> -n <your-azure-COSMOSDB-name>
    ```

## <a name="build-and-run-the-app-locally"></a><span data-ttu-id="8f3b3-132">로컬로 앱 빌드 및 실행</span><span class="sxs-lookup"><span data-stu-id="8f3b3-132">Build and Run the App Locally</span></span>

1. <span data-ttu-id="8f3b3-133">선택한 콘솔 내에서, 이 문서의 앞부분에서 수집한 Azure 및 Cosmos DB 연결 정보를 사용하여 다음 코드 섹션과 같은 환경 변수를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-133">Within your console of choice configure the environment variables shown in the following code sections with the Azure and Cosmos DB connection information you gathered previously in this article.</span></span> <span data-ttu-id="8f3b3-134">**WEBAPP_NAME** 변수에 고유한 이름 및 **REGION** 변수에 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-134">You'll need to provide a unique name for **WEBAPP_NAME** and value for the **REGION** variables.</span></span>

<span data-ttu-id="8f3b3-135">Linux(Bash)의 경우:</span><span class="sxs-lookup"><span data-stu-id="8f3b3-135">For Linux (Bash):</span></span>

```bash
export COSMOSDB_URI=<put-your-COSMOS-DB-documentEndpoint-URI-here>
export COSMOSDB_KEY=<put-your-COSMOS-DB-primaryMasterKey-here>
export COSMOSDB_DBNAME=<put-your-COSMOS-DB-name-here>
export RESOURCEGROUP_NAME=<put-your-resource-group-name-here>
export WEBAPP_NAME=<put-your-Webapp-name-here>
export REGION=<put-your-REGION-here>
```

<span data-ttu-id="8f3b3-136">Windows(Command Prompt)의 경우:</span><span class="sxs-lookup"><span data-stu-id="8f3b3-136">For Windows (Command Prompt):</span></span>
```cmd
set COSMOSDB_URI=<put-your-COSMOS-DB-documentEndpoint-URI-here>
set COSMOSDB_KEY=<put-your-COSMOS-DB-primaryMasterKey-here>
set COSMOSDB_DBNAME=<put-your-COSMOS-DB-name-here>
set RESOURCEGROUP_NAME=<put-your-resource-group-name-here>
set WEBAPP_NAME=<put-your-Webapp-name-here>
set REGION=<put-your-REGION-here>
```

> [!NOTE]
> <span data-ttu-id="8f3b3-137">스크립트를 사용하여 해당 변수를 프로비저닝하려면 .prep 디렉터리의 Bash용 템플릿을 복사하여 시작점으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-137">If you'd like to provision these variables with a script, there is a template for Bash in the .prep directory that you can copy and use as a starting point.</span></span>

2. <span data-ttu-id="8f3b3-138">디렉터리를 다음으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-138">Change the directory to the following:</span></span>

    ```bash
    cd initial/spring-todo-app
    ``` 
 
3. <span data-ttu-id="8f3b3-139">다음 명령을 사용하여 Spring Todo 앱을 로컬로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-139">Run the Spring Todo app locally with the following command:</span></span>

    ```bash
    mvn package spring-boot:run
    ```

4. <span data-ttu-id="8f3b3-140">애플리케이션이 시작된 후 여기서 Spring Todo 앱에 액세스하여 배포의 유효성을 검사할 수 있습니다. [http://localhost:8080/](http://localhost:8080/).</span><span class="sxs-lookup"><span data-stu-id="8f3b3-140">Once the application has started,you can validate the deployment by accessing the Spring Todo app here: [http://localhost:8080/](http://localhost:8080/).</span></span>

 ![로컬로 실행 중인 Spring 앱][SCDB01]

## <a name="deploy-to-app-service-linux"></a><span data-ttu-id="8f3b3-142">App Service Linux에 배포</span><span class="sxs-lookup"><span data-stu-id="8f3b3-142">Deploy to App Service Linux</span></span>

1. <span data-ttu-id="8f3b3-143">이전에 리포지토리의 **initial/spring-todo-app** 디렉터리에 복사한 pom.xml 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-143">Open the pom.xml file that you previously copied to the **initial/spring-todo-app** directory of the repository.</span></span> <span data-ttu-id="8f3b3-144">아래의 pom.xml 파일과 같이 [Azure App Service용 Maven 플러그인](https://github.com/Microsoft/azure-maven-plugins/blob/develop/azure-webapp-maven-plugin/README.md)이 포함되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-144">Ensure that the [Maven Plugin for Azure App Service](https://github.com/Microsoft/azure-maven-plugins/blob/develop/azure-webapp-maven-plugin/README.md) is included as seen in the pom.xml file below.</span></span> <span data-ttu-id="8f3b3-145">버전이 **1.6.0**으로 설정되지 않은 경우 값을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-145">If the version is not set to **1.6.0** then update the value.</span></span>

```xml
<plugins> 

    <!--*************************************************-->
    <!-- Deploy to Java SE in App Service Linux           -->
    <!--*************************************************-->
       
    <plugin>
        <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-webapp-maven-plugin</artifactId>
            <version>1.6.0</version>
            <configuration>
            <deploymentType>jar</deploymentType>
            
            <!-- Web App information -->
            <resourceGroup>${RESOURCEGROUP_NAME}</resourceGroup>
            <appName>${WEBAPP_NAME}</appName>
            <region>${REGION}</region>
            
            <!-- Java Runtime Stack for Web App on Linux-->
            <linuxRuntime>jre8</linuxRuntime>
            
            <appSettings>
                <property>
                    <name>COSMOSDB_URI</name>
                    <value>${COSMOSDB_URI}</value>
                </property>
                <property>
                    <name>COSMOSDB_KEY</name>
                    <value>${COSMOSDB_KEY}</value>
                </property>
                <property>
                    <name>COSMOSDB_DBNAME</name>
                    <value>${COSMOSDB_DBNAME}</value>
                </property>
                <property>
                    <name>JAVA_OPTS</name>
                    <value>-Dserver.port=80</value>
                </property>
            </appSettings>
            
        </configuration>
    </plugin>            
    ...
</plugins>
```

2. <span data-ttu-id="8f3b3-146">App Service Linux의 Java SE에 배포</span><span class="sxs-lookup"><span data-stu-id="8f3b3-146">Deploy to Java SE in App Service Linux</span></span>

    ```bash
    mvn azure-webapp:deploy
    ```

```bash
// Deploy
bash-3.2$ mvn azure-webapp:deploy
[INFO] Scanning for projects...
[INFO] 
[INFO] ------------------------------------------------------------------------
[INFO] Building spring-todo-app 2.0-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] --- azure-webapp-maven-plugin:1.6.0:deploy (default-cli) @ spring-todo-app ---
[INFO] Authenticate with Azure CLI 2.0
[INFO] Target Web App doesnt exist. Creating a new one...
[INFO] Creating App Service Plan 'ServicePlan11111111-1111-1111'...
[INFO] Successfully created App Service Plan.
[INFO] Successfully created Web App.
[INFO] Trying to deploy artifact to spring-todo-app...
[INFO] Successfully deployed the artifact to https://spring-todo-app.azurewebsites.net
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 02:19 min
[INFO] Finished at: 2018-10-28T15:32:03-07:00
[INFO] Final Memory: 50M/574M
[INFO] ------------------------------------------------------------------------
```

3. <span data-ttu-id="8f3b3-147">App Service Linux의 Java SE에서 실행 중인 웹앱을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-147">Browse to your web app running on Java SE in App Service Linux:</span></span>

    ```bash
    https://<WEBAPP_NAME>.azurewebsites.net
    ```

![Azure App Service on Linux에서 실행 중인 Spring 앱][SCDB02]

## <a name="troubleshoot-spring-todo-app-on-azure-by-viewing-logs"></a><span data-ttu-id="8f3b3-149">로그를 확인하여 Azure에서 Spring Todo 앱 문제 해결</span><span class="sxs-lookup"><span data-stu-id="8f3b3-149">Troubleshoot Spring Todo App on Azure by Viewing Logs</span></span>

1. <span data-ttu-id="8f3b3-150">Linux의 Azure App Service에서 배포된 Java 웹앱에 대한 로그를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-150">Configure logs for the deployed Java Web app in Azure App Service in Linux:</span></span>

    ```bash
    az webapp log config --name ${WEBAPP_NAME} \
     --resource-group ${RESOURCEGROUP_NAME} \
     --web-server-logging filesystem
    ```
2. <span data-ttu-id="8f3b3-151">로컬 컴퓨터에서 Java 웹앱 원격 로그 스트림을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-151">Open Java Web app remote log stream from a local machine:</span></span>

    ```bash
    az webapp log tail --name ${WEBAPP_NAME} \
     --resource-group ${RESOURCEGROUP_NAME}
     ```

```bash
bash-3.2$ az webapp log tail --name ${WEBAPP_NAME}  --resource-group ${RESOURCEGROUP_NAME}
2018-10-28T22:50:17  Welcome, you are now connected to log-streaming service.
2018-10-28T22:44:56.265890407Z   _____                               
2018-10-28T22:44:56.265930308Z   /  _  \ __________ _________   ____  
2018-10-28T22:44:56.265936008Z  /  /_\  \___   /  |  \_  __ \_/ __ \ 
2018-10-28T22:44:56.265940308Z /    |    \/    /|  |  /|  | \/\  ___/ 
2018-10-28T22:44:56.265944408Z \____|__  /_____ \____/ |__|    \___  >
2018-10-28T22:44:56.265948508Z         \/      \/                  \/ 
2018-10-28T22:44:56.265952508Z A P P   S E R V I C E   O N   L I N U X
2018-10-28T22:44:56.265956408Z Documentation: http://aka.ms/webapp-linux
2018-10-28T22:44:56.266260910Z Setup openrc ...
2018-10-28T22:44:57.396926506Z Service `hwdrivers needs non existent service dev
2018-10-28T22:44:57.397294409Z  * Caching service dependencies ... [ ok ]
2018-10-28T22:44:57.474152273Z Starting ssh service...
...
...
2018-10-28T22:46:13.432160734Z [INFO] AnnotationMBeanExporter - Registering beans for JMX exposure on startup
2018-10-28T22:46:13.744859424Z [INFO] TomcatWebServer - Tomcat started on port(s): 80 (http) with context path ''
2018-10-28T22:46:13.783230205Z [INFO] TodoApplication - Started TodoApplication in 57.209 seconds (JVM running for 70.815)
2018-10-28T22:46:14.887366993Z 2018-10-28 22:46:14.887  INFO 198 --- [p-nio-80-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring FrameworkServlet 'dispatcherServlet'
2018-10-28T22:46:14.887637695Z [INFO] DispatcherServlet - FrameworkServlet 'dispatcherServlet': initialization started
2018-10-28T22:46:14.998479907Z [INFO] DispatcherServlet - FrameworkServlet 'dispatcherServlet': initialization completed in 111 ms

2018-10-28T22:49:20.572059062Z Sun Oct 28 22:49:20 GMT 2018 GET ======= /api/todolist =======
2018-10-28T22:49:25.850543080Z Sun Oct 28 22:49:25 GMT 2018 DELETE ======= /api/todolist/{4f41ab03-1b12-4131-a920-fe5dfec106ca} ======= 
2018-10-28T22:49:26.047126614Z Sun Oct 28 22:49:26 GMT 2018 GET ======= /api/todolist =======
2018-10-28T22:49:30.201740227Z Sun Oct 28 22:49:30 GMT 2018 POST ======= /api/todolist ======= Milk
2018-10-28T22:49:30.413468872Z Sun Oct 28 22:49:30 GMT 2018 GET ======= /api/todolist =======


```

3. <span data-ttu-id="8f3b3-152">완료된 경우 [e2e-java-experience-in-app-service-linux-part-2/complete](https://github.com/Azure-Samples/e2e-java-experience-in-app-service-linux-part-2/tree/master/complete)의 코드에 대해 결과를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-152">When you are finished, you can check your results against the code in [e2e-java-experience-in-app-service-linux-part-2/complete](https://github.com/Azure-Samples/e2e-java-experience-in-app-service-linux-part-2/tree/master/complete).</span></span>


## <a name="scale-out-the-spring-todo-app"></a><span data-ttu-id="8f3b3-153">Spring Todo 앱 확장</span><span class="sxs-lookup"><span data-stu-id="8f3b3-153">Scale out the Spring Todo App</span></span>

1. <span data-ttu-id="8f3b3-154">Azure CLI를 사용하여 Java 웹앱을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-154">Scale out Java Web app using Azure CLI:</span></span>

    ```bash
    az appservice plan update --number-of-workers 2 \
      --name ${WEBAPP_PLAN_NAME} \
      --resource-group ${RESOURCEGROUP_NAME}
    ```

## <a name="next-steps"></a><span data-ttu-id="8f3b3-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f3b3-155">Next steps</span></span>

- [<span data-ttu-id="8f3b3-156">App Service Linux 개발자 가이드의 Java</span><span class="sxs-lookup"><span data-stu-id="8f3b3-156">Java in App Service Linux dev guide</span></span>](https://docs.microsoft.com/en-us/azure/app-service/containers/app-service-linux-java)
- <span data-ttu-id="8f3b3-157">[Java 개발자를 위한 Azure](https://docs.microsoft.com/en-us/java/azure/) Spring 및 Azure에 대해 자세히 알아보려면 Azure 설명서 센터의 Spring을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-157">[Azure for Java Developers](https://docs.microsoft.com/en-us/java/azure/) To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8f3b3-158">Azure의 Spring</span><span class="sxs-lookup"><span data-stu-id="8f3b3-158">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="8f3b3-159">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8f3b3-159">Additional Resources</span></span>

<span data-ttu-id="8f3b3-160">Azure에서 Spring Boot 애플리케이션을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-160">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="8f3b3-161">Azure App Service에 Spring Boot 애플리케이션 배포</span><span class="sxs-lookup"><span data-stu-id="8f3b3-161">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="8f3b3-162">Azure Container Service의 Kubernetes 클러스터에 Spring Boot 애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="8f3b3-162">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="8f3b3-163">Java와 함께 Azure를 사용하는 방법에 관한 자세한 정보는 [Java 개발자를 위한 Azure]와 [Azure DevOps 및 Java 사용하기]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-163">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="8f3b3-164">**[Spring Framework]** 는 Java 개발자가 엔터프라이즈 수준의 애플리케이션을 만드는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-164">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="8f3b3-165">해당 플랫폼을 기반으로 하여 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 애플리케이션을 만드는 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-165">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="8f3b3-166">Spring Boot을 시작하는 개발자를 도우려면 <https://github.com/spring-guides/>에서 몇 가지 샘플 Spring Boot 패키지를 사용할 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-166">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="8f3b3-167">기본 Spring Boot 프로젝트 목록에서 선택하는 것 외에도 **[Spring Initializr]** 를 통해 사용자 지정 Spring Boot 애플리케이션을 만들기 시작하는 개발자에게 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b3-167">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Java 개발자를 위한 Azure]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Build a SQL API app with Java]: /azure/cosmos-db/create-sql-api-java 
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Boot Document DB Starter for Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Azure DevOps 및 Java 사용하기]: https://azure.microsoft.com/services/devops/java/
[Working with Azure DevOps and Java]: https://azure.microsoft.com/services/devops/java/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SCDB01]: ./media/configure-spring-app-with-cosmos-db-on-app-service-linux/SCDB01.png
[SCDB02]: ./media/configure-spring-app-with-cosmos-db-on-app-service-linux/SCDB02.png
