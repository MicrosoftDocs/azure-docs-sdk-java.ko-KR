---
title: Maven을 사용하여 5분 내 Azure에 Java 웹앱 배포 | Microsoft Docs
description: Maven을 사용하여 빌드된 Java 앱을 Azure에 만들고 배포합니다.
services: app-service\web
documentationcenter: ''
author: rloutlaw
manager: douge
editor: ''
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: routlaw
ms.openlocfilehash: 70b508118c50b75693e2d746dc1e2919c827cb29
ms.sourcegitcommit: 0f38ef9ad64cffdb7b2e9e966224dfd0af251b0f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703546"
---
# <a name="create-and-deploy-a-java-app-to-azure-with-maven"></a>Maven을 사용하여 Azure에 Java 앱 생성 및 배포

이 빠른 시작은 [Apache Maven](http://maven.apache.org) 및 Azure CLI를 사용하여 몇 분 만에 [Azure App Service](/azure/app-service/app-service-value-prop-what-is)에 간단한 Java 웹앱을 만들고 배포하는 데 도움이 됩니다.

## <a name="before-you-begin"></a>시작하기 전에

시작하기 전에 다음 항목을 설치합니다.

- [Git](https://git-scm.com/)
- [Java 8](https://www.azul.com/downloads/zulu/)
- [Maven 3](http://maven.apache.org/download.cgi)
- [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)

Azure 구독이 아직 없는 경우 시작하기 전에 [체험 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.

## <a name="get-the-sample-code"></a>샘플 코드 가져오기

로컬 컴퓨터에 샘플 앱 리포지토리를 복제합니다. 이 샘플은 앱을 로컬로 테스트하고 Azure App Service에 샘플을 배포하는 데 도움이 되는 `pom.xml` 프로젝트에 추가 Maven 구성이 포함된 간단한 JSP 응용 프로그램입니다.

```
git clone https://github.com/Azure-Samples/app-service-maven
```

## <a name="run-the-app-locally"></a>로컬에서 앱 실행

명령 프롬프트를 열고 Maven을 사용하여 앱을 빌드하고 로컬 [Tomcat](https://tomcat.apache.org) 웹 컨테이너에서 실행합니다. 

```
cd app-service-maven
mvn package
mvn tomcat7:run-war
```

웹 브라우저를 열고 http://localhost:8080으로 이동하여 앱을 미리보기 합니다:

  ![Java 샘플 앱의 Hello World 출력](media/maven-quickstart/java-app-hello-world-output.png)

## <a name="log-in-to-azure"></a>Azure에 로그인

`az login`을 사용하여 Azure CLI에 로그인합니다. 이 빠른 시작에서는 CLI를 사용하여 앱을 호스팅하는 데 필요한 Azure 리소스를 쿼리하고 만듭니다.
   
```azurecli
az login
```

## <a name="create-a-resource-group"></a>리소스 그룹 만들기   

[az group create](/cli/azure/group#create)를 사용하여 리소스 그룹을 만듭니다. Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.

```azurecli
az group create --location "East US" --name myResourceGroup
```

`---location`에 사용할 수 있는 가능한 값을 보려면 [az appservice list-locations](/cli/azure/appservice#list-locations) 명령을 사용합니다.

## <a name="create-an-app-service-plan"></a>App Service 플랜 만들기

[az appservice plan create](/cli/azure/appservice/plan#create)를 사용하여 **체험** [App Service 계획](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)을 만듭니다. App Service 계획은 계획에서 실행되는 모든 웹앱에서 공유하는 리소스를 할당합니다.


```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

App Service 계획이 준비되면 Azure CLI에서 다음 예제와 비슷한 정보를 표시합니다.

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


## <a name="create-a-web-app"></a>웹앱 만들기

[az webapp create](/cli/azure/appservice/web#create) Azure CLI 명령을 사용하여 계획의 리소스를 사용하는 웹앱을 만듭니다. 웹앱 정의는 코드를 배포할 공간 및 실행 중인 앱에 액세스하기 위한 URL을 제공합니다.

아래 명령에서 <appname> 자리 표시자를 고유한 앱 이름으로 바꿉니다. <appname>은 웹앱의 기본 호스트 이름에 사용됩니다. <appname>이 고유하지 않으면 "지정된 이름의 웹 사이트가 이미 있습니다."라는 친숙한 오류 메시지가 표시됩니다.

```azurecli
az webapp create --name appname --resource-group myResourceGroup --plan my-free-appservice-plan
```

웹앱이 만들어지면 Azure CLI에서 다음 예제와 비슷한 정보를 표시합니다.

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

## <a name="configure-java-and-tomcat"></a>Java 및 Tomcat 구성

[az webapp config](/cli/azure/appservice/web#config) Azure CLI 명령을 사용하여 Java 및 Tomcat을 사용하도록 웹앱을 구성합니다. 아래 예제에서는 Java 8 및 [Apache Tomcat 8.5](http://tomcat.apache.org/)를 실행하여 앱을 실행하도록 App Service를 구성합니다.

```azurecli
az webapp config set \ 
--name appname \
--resource-group myResourceGroup \
--java-container TOMCAT \
--java-version 1.8.0_73  \
--java-container-version 8.5
```

## <a name="configure-maven"></a>Maven 구성 

샘플의 Maven `pom.xml`에는 FTP로 Azure에 샘플을 전송하는 구성이 포함되어 있지만, 자신의 웹앱에 배포하도록 해당 구성을 사용자 지정해야 합니다. [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles)를 사용하여 App Service 자격 증명을 검색합니다.

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

`az-settings.xml` 파일의 자리 표시자를 출력의 암호, 사용자 이름 및 FTP 호스트 이름으로 바꿉니다. 사용자 이름에 CLI 출력의 이스케이프된 값 대신 하나의 `\` 문자만 사용해야 합니다.
   
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

## <a name="deploy-the-sample-application"></a>샘플 응용 프로그램 배포

`az-settings.xml` 파일의 구성을 사용하는 Maven의 `-s` 매개 변수를 사용하여 샘플을 Azure에 배포합니다.

```
mvn install -s az-settings.xml
```

## <a name="browse-to-web-app"></a>웹앱으로 이동

Azure에서 실행되는 샘플 보기:

```azurecli
az webapp browse --name appname --resource-group myResourceGroup
```

## <a name="update-the-app"></a>앱 업데이트

텍스트 편집기를 사용하여 `src/main/webapp/index.jsp`를 열고 기존 JSP를 아래 코드로 바꿉니다.

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

Maven으로 업데이트 배포:

```
mvn clean package
mvn install -s az-settings.xml
```

앱을 다시 배포한 후 브라우저를 새로 고쳐 변경 내용을 확인합니다.

## <a name="manage-your-new-azure-app"></a>새 Azure 앱 관리

Azure Portal로 이동하여 방금 만든 웹앱을 살펴봅니다.

이 작업을 수행하려면 [https://portal.azure.com](https://portal.azure.com)에 로그인합니다.

왼쪽 메뉴에서 **App Service**를 클릭한 다음 Azure 웹앱의 이름을 클릭합니다.

 ![포털의 웹앱 목록에서 앱 선택](media/azure-app-service-portal.png)

트래픽을 보내기 위해 앱에 대해 `curl`을 실행하여 모니터링을 테스트합니다.

```bash
curl http://<appname>.azurewebsites.net/?[1-30]
```

몇 분 후에 모니터링에서 요청 작업이 표시됩니다.

 ![Azure Portal에서 모니터링](media/java-app-monitoring.png)

## <a name="clean-up-resources"></a>리소스 정리

이 가이드에서 만든 리소스를 모두 제거하려면 다음 명령을 실행합니다.

```azurecli
az group delete --name myResrouceGroup
```

## <a name="next-steps"></a>다음 단계

[Azure Java 샘플](https://azure.microsoft.com/resources/samples/?term=java)의 전체 목록을 찾아봅니다.
