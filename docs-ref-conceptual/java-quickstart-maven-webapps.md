---
title: "Maven을 사용하여 5분 내 Azure에 Java 웹앱 배포 | Microsoft Docs"
description: "Maven을 사용하여 빌드된 Java 앱을 Azure에 만들고 배포합니다."
services: app-service\web
documentationcenter: 
author: rloutlaw
manager: douge
editor: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: routlaw
ms.openlocfilehash: 1adc0a104ba22bcd353664e68323165890e46c64
ms.sourcegitcommit: 30d502b3150fa14bcc1251f5f88c7c0dd83e531e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2017
---
# <a name="create-and-deploy-a-java-app-to-azure-with-maven"></a><span data-ttu-id="39bc2-103">Maven을 사용하여 Azure에 Java 앱 생성 및 배포</span><span class="sxs-lookup"><span data-stu-id="39bc2-103">Create and deploy a Java app to Azure with Maven</span></span>

<span data-ttu-id="39bc2-104">이 빠른 시작은 [Apache Maven](http://maven.apache.org) 및 Azure CLI를 사용하여 몇 분 만에 [Azure App Service](/azure/app-service/app-service-value-prop-what-is)에 간단한 Java 웹앱을 만들고 배포하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-104">This quickstart helps you create and deploy a simple Java web app to [Azure App Service](/azure/app-service/app-service-value-prop-what-is) in just a few minutes using [Apache Maven](http://maven.apache.org) and the Azure CLI.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="39bc2-105">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="39bc2-105">Before you begin</span></span>

<span data-ttu-id="39bc2-106">시작하기 전에 다음 항목을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-106">Before you start, set up the following:</span></span>

- [<span data-ttu-id="39bc2-107">Git</span><span class="sxs-lookup"><span data-stu-id="39bc2-107">Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="39bc2-108">Java 8</span><span class="sxs-lookup"><span data-stu-id="39bc2-108">Java 8</span></span>](https://www.azul.com/downloads/zulu/)
- [<span data-ttu-id="39bc2-109">Maven 3</span><span class="sxs-lookup"><span data-stu-id="39bc2-109">Maven 3</span></span>](http://maven.apache.org/download.cgi)
- [<span data-ttu-id="39bc2-110">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="39bc2-110">Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-az-cli2)

<span data-ttu-id="39bc2-111">Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="get-the-sample-code"></a><span data-ttu-id="39bc2-112">샘플 코드 가져오기</span><span class="sxs-lookup"><span data-stu-id="39bc2-112">Get the sample code</span></span>

<span data-ttu-id="39bc2-113">로컬 컴퓨터에 샘플 앱 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-113">Clone the sample app repository to your local machine.</span></span> <span data-ttu-id="39bc2-114">이 샘플은 앱을 로컬로 테스트하고 Azure App Service에 샘플을 배포하는 데 도움이 되는 `pom.xml` 프로젝트에 추가 Maven 구성이 포함된 간단한 JSP 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-114">The sample is a simple JSP application with additional Maven configuration in the project `pom.xml` to test the app locally and help deploy the sample to Azure App Service.</span></span>

```
git clone https://github.com/Azure-Samples/app-service-maven
```

## <a name="run-the-app-locally"></a><span data-ttu-id="39bc2-115">로컬에서 앱 실행</span><span class="sxs-lookup"><span data-stu-id="39bc2-115">Run the app locally</span></span>

<span data-ttu-id="39bc2-116">명령 프롬프트를 열고 Maven을 사용하여 앱을 빌드하고 로컬 [Tomcat](https://tomcat.apache.org) 웹 컨테이너에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-116">Open a command prompt and use Maven to build the app and run it in a local [Tomcat](https://tomcat.apache.org) web container.</span></span> 

```
cd app-service-maven
mvn package
mvn tomcat7:run-war
```

<span data-ttu-id="39bc2-117">웹 브라우저를 열고 http://localhost:8080 으로 이동하여 앱을 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-117">Open a web browser and navigate to http://localhost:8080 to preview the app:</span></span>

  ![Java 샘플 앱의 Hello World 출력](media/maven-quickstart/java-app-hello-world-output.png)

## <a name="log-in-to-azure"></a><span data-ttu-id="39bc2-119">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="39bc2-119">Log in to Azure</span></span>

<span data-ttu-id="39bc2-120">`az login`을 사용하여 Azure CLI에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-120">Log in to the Azure CLI with `az login`.</span></span> <span data-ttu-id="39bc2-121">이 빠른 시작에서는 CLI를 사용하여 앱을 호스팅하는 데 필요한 Azure 리소스를 쿼리하고 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-121">This quickstart uses the CLI to query and create the Azure resources needed to host the app.</span></span>
   
```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="39bc2-122">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="39bc2-122">Create a resource group</span></span>   

<span data-ttu-id="39bc2-123">[az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-123">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="39bc2-124">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-124">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

```azurecli
az group create --location "East US" --name myResourceGroup
```

<span data-ttu-id="39bc2-125">`---location`에 사용할 수 있는 가능한 값을 보려면 [az appservice list-locations](/cli/azure/appservice#list-locations) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-125">To see other possible values you can use for `---location`, use [az appservice list-locations](/cli/azure/appservice#list-locations)</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="39bc2-126">App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="39bc2-126">Create an App Service plan</span></span>

<span data-ttu-id="39bc2-127">[az appservice plan create](/cli/azure/appservice/plan#create)를 사용하여 **체험** [App Service 계획](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-127">Create a **FREE** [App Service plan](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) using [az appservice plan create](/cli/azure/appservice/plan#create).</span></span> <span data-ttu-id="39bc2-128">App Service 계획은 계획에서 실행되는 모든 웹앱에서 공유하는 리소스를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-128">App Service plans allocate resources shared across all web apps running in the plan.</span></span>


```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="39bc2-129">App Service 계획이 준비되면 Azure CLI에서 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-129">When the App Service Plan is ready, the Azure CLI shows information similar to the following example:</span></span>

```json
{
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/my-free-appservice-plan",
    "location": "East US",
    "sku": {
    "capacity": 1,
    "family": "S",
    "name": "S1",
    "tier": "Standard"
    },
    "status": "Ready",
    "type": "Microsoft.Web/serverfarms"
}
```


## <a name="create-a-web-app"></a><span data-ttu-id="39bc2-130">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="39bc2-130">Create a web app</span></span>

<span data-ttu-id="39bc2-131">[az webapp create](/cli/azure/appservice/web#create) Azure CLI 명령을 사용하여 계획의 리소스를 사용하는 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-131">Create a web app that uses the plan's resources using the Azure CLI [az webapp create](/cli/azure/appservice/web#create) command.</span></span> <span data-ttu-id="39bc2-132">웹앱 정의는 코드를 배포할 공간 및 실행 중인 앱에 액세스하기 위한 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-132">The web app definition provides a space to deploy the code to and a URL to access the app once it's running.</span></span>

<span data-ttu-id="39bc2-133">아래 명령에서 <appname> 자리 표시자를 고유한 앱 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-133">In the command below substitute your own unique app name where you see the <appname> placeholder.</span></span> <span data-ttu-id="39bc2-134"><appname>은 웹앱의 기본 호스트 이름에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-134">The <appname> is used in the default hostname for the web app.</span></span> <span data-ttu-id="39bc2-135"><appname>이 고유하지 않으면 "지정된 이름의 웹 사이트가 이미 있습니다."라는 친숙한 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-135">If <appname> is not unique, you get the friendly error message "Website with given name already exists."</span></span>

```azurecli
az webapp create --name appname --resource-group myResourceGroup --plan my-free-appservice-plan
```

<span data-ttu-id="39bc2-136">웹앱이 만들어지면 Azure CLI에서 다음 예제와 비슷한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-136">When the Web App has been created, the Azure CLI shows information similar to the following example.1</span></span>

```json
{
    "clientAffinityEnabled": true,
    "defaultHostName": "<appname>.azurewebsites.net",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<appname>",
    "isDefaultContainer": null,
    "kind": "app",
    "location": "East US",
    "name": "<app_name>",
    "repositorySiteName": "<app_name>",
    "reserved": true,
    "resourceGroup": "myResourceGroup",
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/my-free-appservice-plan",
    "state": "Running",
    "type": "Microsoft.Web/sites",
}
```

## <a name="configure-java-and-tomcat"></a><span data-ttu-id="39bc2-137">Java 및 Tomcat 구성</span><span class="sxs-lookup"><span data-stu-id="39bc2-137">Configure Java and Tomcat</span></span>

<span data-ttu-id="39bc2-138">[az webapp config](/cli/azure/appservice/web#config) Azure CLI 명령을 사용하여 Java 및 Tomcat을 사용하도록 웹앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-138">Configure the web app to use Java and Tomcat using the Azure CLI's [az webapp config](/cli/azure/appservice/web#config) command.</span></span> <span data-ttu-id="39bc2-139">아래 예제에서는 Java 8 및 [Apache Tomcat 8.5](http://tomcat.apache.org/)를 실행하여 앱을 실행하도록 App Service를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-139">The example below configures App Service to run Java 8 and [Apache Tomcat 8.5](http://tomcat.apache.org/) to run the app.</span></span>

```azurecli
az webapp config set \ 
--name appname \
--resource-group myResourceGroup \
--java-container TOMCAT \
--java-version 1.8.0_73  \
--java-container-version 8.5
```

## <a name="configure-maven"></a><span data-ttu-id="39bc2-140">Maven 구성</span><span class="sxs-lookup"><span data-stu-id="39bc2-140">Configure Maven</span></span> 

<span data-ttu-id="39bc2-141">샘플의 Maven `pom.xml`에는 FTP로 Azure에 샘플을 전송하는 구성이 포함되어 있지만, 자신의 웹앱에 배포하도록 해당 구성을 사용자 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-141">The sample's Maven `pom.xml` includes configuration to FTP the sample into Azure, but you'll need to customize it to deploy to your own web app.</span></span> <span data-ttu-id="39bc2-142">[az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles)를 사용하여 App Service 자격 증명을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-142">Retreive your App Seevice credentials with [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles):</span></span>

```azurecli
az webapp deployment list-publishing-profiles  \
--name appname \ 
--resource-group myResourceGroup  \
--query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" 
```

```json
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-045.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "appname\\$appname"
  }
]
```

<span data-ttu-id="39bc2-143">`az-settings.xml` 파일의 자리 표시자를 출력의 암호, 사용자 이름 및 FTP 호스트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-143">Replace the placeholders in the `az-settings.xml` file with password, username, and FTP hostname from the output.</span></span> <span data-ttu-id="39bc2-144">사용자 이름에 CLI 출력의 이스케이프된 값 대신 하나의 `\` 문자만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-144">Make sure to only use one `\` character in the username instead of the escaped value from the CLI output.</span></span>
   
```XML
...
    <server>
      <id>azure-hello-world</id>
      <username>appname\$appname</username>
      <password>aBcDeFgHiJkLmNoPqRsTuVwXyZ</password>
    </server>
...
   <configuration>
     <fromFile>${basedir}/target/AzureAppDemo-0.0.1-SNAPSHOT.war</fromFile>
     <url>ftp://waws-prod-blu-045.ftp.azurewebsites.windows.net/site/wwwroot</url>
     <toFile>webapps/ROOT.war</toFile>
     <serverId>azure-hello-world</serverId>
   </configuration>
...
```

## <a name="deploy-the-sample-application"></a><span data-ttu-id="39bc2-145">샘플 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="39bc2-145">Deploy the sample application</span></span>

<span data-ttu-id="39bc2-146">`az-settings.xml` 파일의 구성을 사용하는 Maven의 `-s` 매개 변수를 사용하여 샘플을 Azure에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-146">Deploy with sample to Azure, using Maven's `-s` parameter to use the configuration in the `az-settings.xml` file.</span></span>

```
mvn install -s az-settings.xml
```

## <a name="browse-to-web-app"></a><span data-ttu-id="39bc2-147">웹앱으로 이동</span><span class="sxs-lookup"><span data-stu-id="39bc2-147">Browse to web app</span></span>

<span data-ttu-id="39bc2-148">Azure에서 실행되는 샘플 보기:</span><span class="sxs-lookup"><span data-stu-id="39bc2-148">View the sample running in Azure:</span></span>

```azurecli
az webapp browse --name appname --resource-group myResourceGroup
```

## <a name="update-the-app"></a><span data-ttu-id="39bc2-149">앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="39bc2-149">Update the app</span></span>

<span data-ttu-id="39bc2-150">텍스트 편집기를 사용하여 `src/main/webapp/index.jsp`를 열고 기존 JSP를 아래 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-150">Using a text editor, open `src/main/webapp/index.jsp`, and replace the existing JSP with the one below.</span></span>

```html
<%--
  Copyright (c) Microsoft Corporation. All rights reserved.
  Licensed under the MIT License. See License.txt in the project root for
  license information.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java"  import="java.util.Date" %>
<html>
<head>
  <title>Azure Samples Hello World</title>
</head>
<body>
  <H1>Hello Azure!</H1>
   Current time is: <%= new Date() %>
</body>
</html>
```

<span data-ttu-id="39bc2-151">Maven으로 업데이트 배포:</span><span class="sxs-lookup"><span data-stu-id="39bc2-151">Deploy the update with Maven:</span></span>

```
mvn clean package
mvn install -s az-settings.xml
```

<span data-ttu-id="39bc2-152">앱을 다시 배포한 후 브라우저를 새로 고쳐 변경 내용을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-152">Refresh your browser after the app redeploys to view your changes.</span></span>

## <a name="manage-your-new-azure-app"></a><span data-ttu-id="39bc2-153">새 Azure 앱 관리</span><span class="sxs-lookup"><span data-stu-id="39bc2-153">Manage your new Azure app</span></span>

<span data-ttu-id="39bc2-154">Azure Portal로 이동하여 방금 만든 웹앱을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-154">Go to the Azure portal to take a look at the web app you just created.</span></span>

<span data-ttu-id="39bc2-155">이 작업을 수행하려면 [https://portal.azure.com](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-155">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="39bc2-156">왼쪽 메뉴에서 **App Service**를 클릭한 다음 Azure 웹앱의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-156">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

 ![포털의 웹앱 목록에서 앱 선택](media/azure-app-service-portal.png)

<span data-ttu-id="39bc2-158">트래픽을 보내기 위해 앱에 대해 `curl`을 실행하여 모니터링을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-158">Test the monitoring by running `curl` against the app to send some traffic.</span></span>

```bash
curl http://<appname>.azurewebsites.net/?[1-30]
```

<span data-ttu-id="39bc2-159">몇 분 후에 모니터링에서 요청 작업이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-159">You'll see the request activity in the monitoring after a couple of minutes.</span></span>

 ![Azure Portal에서 모니터링](media/java-app-monitoring.png)

## <a name="clean-up-resources"></a><span data-ttu-id="39bc2-161">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="39bc2-161">Clean up resources</span></span>

<span data-ttu-id="39bc2-162">이 가이드에서 만든 리소스를 모두 제거하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-162">To remove all the resources created in this guide, run the following command:</span></span>

```azurecli
az group delete --name myResrouceGroup
```

## <a name="next-steps"></a><span data-ttu-id="39bc2-163">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39bc2-163">Next steps</span></span>

<span data-ttu-id="39bc2-164">[Azure Java 샘플](https://azure.microsoft.com/resources/samples/?term=java)의 전체 목록을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="39bc2-164">Browse the full list of [Azure Java samples](https://azure.microsoft.com/resources/samples/?term=java).</span></span>