---
title: "Java용 Azure 라이브러리 시작"
description: "Azure 구독을 사용하여 Java용 Azure 라이브러리의 기본적인 사용을 시작합니다."
keywords: "Azure에서 Java, SDK, API, 인증, 시작"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: get-started-article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: b1e10b79-f75e-4605-aecd-eed64873e2d3
ms.openlocfilehash: c9b654ea927563e8255f5d189ddc84733a1202e2
ms.sourcegitcommit: 30d502b3150fa14bcc1251f5f88c7c0dd83e531e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2017
---
# <a name="get-started-with-the-azure-libraries-for-java"></a><span data-ttu-id="02d15-104">Java용 Azure 라이브러리 시작</span><span class="sxs-lookup"><span data-stu-id="02d15-104">Get started with the Azure libraries for Java</span></span>

<span data-ttu-id="02d15-105">이 가이드에서는 Azure 서비스 사용자를 사용하여 개발 환경을 설정하고, Java용 Azure 라이브러리를 사용하여 Azure 구독에서 리소스를 만들고 사용하는 샘플 코드를 실행하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-105">This guide walks you through setting up a development environment with an Azure service principal and running sample code that creates and uses resources in your Azure subscription using the Azure libraries for Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02d15-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="02d15-106">Prerequisites</span></span>

- <span data-ttu-id="02d15-107">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="02d15-107">An Azure account.</span></span> <span data-ttu-id="02d15-108">계정이 없으면 [체험 계정을 얻습니다](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="02d15-108">If you don't have one , [get a free trial](https://azure.microsoft.com/free/)</span></span>
- <span data-ttu-id="02d15-109">[Azure Cloud Shell](https://docs.microsoft.coms/azure/cloud-shell/quickstart) 또는 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="02d15-109">[Azure Cloud Shell](https://docs.microsoft.coms/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>
- <span data-ttu-id="02d15-110">[Java 8](https://www.azul.com/downloads/zulu/)(Azure Cloud Shell에 포함되어 있음)</span><span class="sxs-lookup"><span data-stu-id="02d15-110">[Java 8](https://www.azul.com/downloads/zulu/) (included in Azure Cloud Shell)</span></span>
- <span data-ttu-id="02d15-111">[Maven 3](http://maven.apache.org/download.cgi)(Azure Cloud Shell에 포함되어 있음)</span><span class="sxs-lookup"><span data-stu-id="02d15-111">[Maven 3](http://maven.apache.org/download.cgi) (included in Azure Cloud Shell)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="02d15-112">인증 설정</span><span class="sxs-lookup"><span data-stu-id="02d15-112">Set up authentication</span></span>

<span data-ttu-id="02d15-113">이 자습서에서 샘플 코드를 실행하려면 Azure 구독에 대한 읽기 및 만들기 권한이 Java 응용 프로그램에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-113">Your Java application needs read and create permissions in your Azure subscription to run the sample code in this tutorial.</span></span> <span data-ttu-id="02d15-114">서비스 사용자를 만들고 해당 자격 증명을 사용하여 실행되도록 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-114">Create a service principal and configure your application to run with its credentials.</span></span> <span data-ttu-id="02d15-115">서비스 사용자는 앱에서 실행하는 데 필요한 권한만 부여하는 ID와 연결되는 비대화형 계정을 만드는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-115">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="02d15-116">[Azure CLI 2.0을 사용하여 서비스 사용자를 만들고](/cli/azure/create-an-azure-service-principal-azure-cli) 출력을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-116">[Create a service principal using the Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli) and capture the output.</span></span> <span data-ttu-id="02d15-117">암호 인수에 `MY_SECURE_PASSWORD` 대신 [보안 암호](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy)를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-117">You'll need to provide a [secure password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) in the password argument instead of `MY_SECURE_PASSWORD`.</span></span>


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```

<span data-ttu-id="02d15-118">다음으로 시스템의 텍스트 파일에 다음 예제를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-118">Next, copy the following into a text file on your system:</span></span>

```text
# sample management library properties file
subscription=########-####-####-####-############
client=########-####-####-####-############
key=XXXXXXXXXXXXXXXX
tenant=########-####-####-####-############
managementURI=https\://management.core.windows.net/
baseURL=https\://management.azure.com/
authURL=https\://login.windows.net/
graphURL=https\://graph.windows.net/
```

<span data-ttu-id="02d15-119">상위 4개 값을 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-119">Replace the top four values with the following:</span></span>

- <span data-ttu-id="02d15-120">subscription: Azure CLI 2.0에서 `az account show`의 *id* 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-120">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="02d15-121">client: 서비스 사용자 출력에서 가져온 출력의 *appId* 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-121">client: use the *appId* value from the output taken from a service principal output.</span></span>
- <span data-ttu-id="02d15-122">key: 서비스 사용자 출력의 *password* 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-122">key: use the *password* value from the service principal output .</span></span>
- <span data-ttu-id="02d15-123">tenant: 서비스 사용자 출력의 *tenant* 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-123">tenant: use the *tenant* value from the service principal output.</span></span>

<span data-ttu-id="02d15-124">코드에서 읽을 수 있는 시스템의 안전한 위치에 이 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-124">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="02d15-125">셸에서 인증 파일의 전체 경로가 포함된 `AZURE_AUTH_LOCATION` 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-125">Set an environment variable `AZURE_AUTH_LOCATION` with the full path to the authentication file in your shell.</span></span>    

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

## <a name="create-a-new-maven-project"></a><span data-ttu-id="02d15-126">새 Maven 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="02d15-126">Create a new Maven project</span></span>

> [!NOTE]
> <span data-ttu-id="02d15-127">이 가이드에서는 Maven 빌드 도구를 사용하여 샘플 코드를 빌드하고 실행하지만, Gradle과 같은 다른 빌드 도구도 Java용 Azure 라이브러리에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-127">This guide uses Maven build tool to build and run the sample code, but other build tools such as Gradle also work with the Azure libraries for Java.</span></span> 

<span data-ttu-id="02d15-128">명령줄에서 시스템의 새 디렉터리에 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-128">Create a Maven project from the command line in a new directory on your system:</span></span>

```
mkdir java-azure-test
cd java-azure-test
mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp  \ 
-DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

<span data-ttu-id="02d15-129">이렇게 하면 `testAzureApp` 폴더 아래에 기본 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-129">This creates a basic Maven project under the `testAzureApp` folder.</span></span> <span data-ttu-id="02d15-130">`pom.xml` 프로젝트에 다음 항목을 추가하여 이 자습서의 샘플 코드에서 사용되는 라이브러리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-130">Add the following entries into the project `pom.xml` to import the libraries used in the sample code in this tutorial.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.0.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

<span data-ttu-id="02d15-131">최상위 `project` 요소 아래에 `build` 항목을 추가하여 [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/)을 통해 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-131">Add a `build` entry under the top-level `project` element to use the [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/) to run the samples:</span></span>

```XML
<build>
    <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.testAzureApp.AzureApp</mainClass>
            </configuration>
        </plugin>
    </plugins>
</build>
 ```
   
## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="02d15-132">Linux 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="02d15-132">Create a Linux virtual machine</span></span>

<span data-ttu-id="02d15-133">프로젝트의 `src/main/java` 디렉터리에 `AzureApp.java`라는 새 파일을 만들고 다음 코드 블록에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-133">Create a new file named `AzureApp.java` in the project's `src/main/java` directory and paste in the following block of code.</span></span> <span data-ttu-id="02d15-134">`userName` 및 `sshKey` 변수를 컴퓨터에 대한 실제 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-134">Update the `userName` and `sshKey` variables with real values for your machine.</span></span> <span data-ttu-id="02d15-135">이 코드에서는 미국 동부 Azure 지역에서 실행되는 `sampleResourceGroup` 리소스 그룹에 `testLinuxVM`이라는 새 Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-135">The code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleResourceGroup` running in the US East Azure region.</span></span>

```java
package com.fabrikam.testAzureApp;

import com.microsoft.azure.management.Azure;
import com.microsoft.azure.management.compute.VirtualMachine;
import com.microsoft.azure.management.compute.KnownLinuxVirtualMachineImage;
import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
import com.microsoft.azure.management.appservice.WebApp;
import com.microsoft.azure.management.storage.StorageAccount;
import com.microsoft.azure.management.storage.SkuName;
import com.microsoft.azure.management.storage.StorageAccountKey;
import com.microsoft.azure.management.sql.SqlDatabase;
import com.microsoft.azure.management.sql.SqlServer;
import com.microsoft.azure.management.resources.fluentcore.arm.Region;
import com.microsoft.azure.management.resources.fluentcore.utils.SdkContext;

import com.microsoft.rest.LogLevel;

import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

import java.io.File;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class AzureApp {

    public static void main(String[] args) {

        final String userName = "YOUR_VM_USERNAME";
        final String sshKey = "YOUR_PUBLIC_SSH_KEY";

        try {

            // use the properties file with the service principal information to authenticate
            // change the name of the environment variable if you used a different name in the previous step
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));    
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();
           
            // create a Ubuntu virtual machine in a new resource group 
            VirtualMachine linuxVM = azure.virtualMachines().define("testLinuxVM")
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup("sampleVmResourceGroup")
                    .withNewPrimaryNetwork("10.0.0.0/24")
                    .withPrimaryPrivateIpAddressDynamic()
                    .withoutPrimaryPublicIpAddress()
                    .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                    .withRootUsername(userName)
                    .withSsh(sshKey)
                    .withUnmanagedDisks()
                    .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
                    .create();   

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
}
```

<span data-ttu-id="02d15-136">명령줄에서 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-136">Run the sample from the command line:</span></span>

```
mvn compile exec:java
```

<span data-ttu-id="02d15-137">SDK에서 기본 호출을 Azure REST API로 설정하여 가상 컴퓨터 및 해당 리소스를 구성할 때 콘솔에서 일부 REST 요청과 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-137">You'll see some REST requests and responses in the console as the SDK makes the underlying calls to the Azure REST API to configure the virtual machine and its resources.</span></span> <span data-ttu-id="02d15-138">프로그램이 완료되면 Azure CLI 2.0을 사용하여 구독의 가상 컴퓨터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-138">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="02d15-139">코드가 작동하는지 확인했으면 CLI를 사용하여 VM과 해당 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-139">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="02d15-140">GitHub 리포지토리에서 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="02d15-140">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="02d15-141">`AzureApp.java`의 main 메서드를 아래 코드로 바꾸고, 이 코드를 실행하기 전에 `appName` 변수를 고유한 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-141">Replace the main method in `AzureApp.java` with the one below, updating the `appName` variable to a unique value before running the code.</span></span> <span data-ttu-id="02d15-142">이 코드에서는 공용 GitHub 리포지토리의 `master` 분기에 있는 웹 응용 프로그램을 체험 가격 책정 계층에서 실행되는 새 [Azure App Service 웹앱](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-142">This code deploys a web application from the `master` branch in a public GitHub repo into a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free pricing tier.</span></span>

```java
    public static void main(String[] args) {
        try {

            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            final String appName = "YOUR_APP_NAME";

            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            WebApp app = azure.webApps().define(appName)
                    .withRegion(Region.US_WEST2)
                    .withNewResourceGroup("sampleWebResourceGroup")
                    .withNewWindowsPlan(PricingTier.FREE_F1)
                    .defineSourceControl()
                    .withPublicGitRepository(
                            "https://github.com/Azure-Samples/app-service-web-java-get-started")
                    .withBranch("master")
                    .attach()
                    .create();

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
```

<span data-ttu-id="02d15-143">Maven을 사용하기 전에 다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-143">Run the code as before using Maven:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="02d15-144">CLI를 사용하여 응용 프로그램을 가리키는 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-144">Open a browser pointed to the application using the CLI:</span></span>

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```

<span data-ttu-id="02d15-145">배포를 확인한 후 구독에서 웹앱을 제거하고 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-145">Remove the web app and plan from your subscription once you've verified the deployment.</span></span>

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-a-sql-database"></a><span data-ttu-id="02d15-146">SQL 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="02d15-146">Connect to a SQL database</span></span>

<span data-ttu-id="02d15-147">`AzureApp.java`의 현재 main 메서드를 `dbPassword` 변수에 대한 실제 값을 설정하는 아래 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-147">Replace the current main method in `AzureApp.java` with the code below, setting a real value for the `dbPassword` variable.</span></span>
<span data-ttu-id="02d15-148">이 코드에서는 원격 액세스를 허용하는 방화벽 규칙이 있는 새 SQL 데이터베이스를 만든 다음 SQL Database JBDC 드라이버를 사용하여 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-148">This code creates a new SQL database with a firewall rule allowing remote access,  and then connects to it using the SQL Database JBDC driver.</span></span> 

```java

    public static void main(String args[])
    {
        // create the db using the management libraries
        try {
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            final String adminUser = SdkContext.randomResourceName("db",8);
            final String sqlServerName = SdkContext.randomResourceName("sql",10);
            final String sqlDbName = SdkContext.randomResourceName("dbname",8);
            final String dbPassword = "YOUR_PASSWORD_HERE";


            SqlServer sampleSQLServer = azure.sqlServers().define(sqlServerName)
                            .withRegion(Region.US_EAST)
                            .withNewResourceGroup("sampleSqlResourceGroup")
                            .withAdministratorLogin(adminUser)
                            .withAdministratorPassword(dbPassword)
                            .withNewFirewallRule("0.0.0.0","255.255.255.255")
                            .create();

            SqlDatabase sampleSQLDb = sampleSQLServer.databases().define(sqlDbName).create();

            // assemble the connection string to the database
            final String domain = sampleSQLServer.fullyQualifiedDomainName();
            String url = "jdbc:sqlserver://"+ domain + ":1433;" +
                    "database=" + sqlDbName +";" +
                    "user=" + adminUser+ "@" + sqlServerName + ";" +
                    "password=" + dbPassword + ";" +
                    "encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";

            // connect to the database, create a table and insert a entry into it
            Connection conn = DriverManager.getConnection(url);

            String createTable = "CREATE TABLE CLOUD ( name varchar(255), code int);";
            String insertValues = "INSERT INTO CLOUD (name, code ) VALUES ('Azure', 1);";
            String selectValues = "SELECT * FROM CLOUD";
            Statement createStatement = conn.createStatement();
            createStatement.execute(createTable);
            Statement insertStatement = conn.createStatement();
            insertStatement.execute(insertValues);
            Statement selectStatement = conn.createStatement();
            ResultSet rst = selectStatement.executeQuery(selectValues);

            while (rst.next()) {
                System.out.println(rst.getString(1) + " "
                        + rst.getString(2));
            }


        } catch (Exception e) {
            System.out.println(e.getMessage());
            System.out.println(e.getStackTrace().toString());
        }
    }
```
<span data-ttu-id="02d15-149">명령줄에서 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-149">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="02d15-150">그런 다음 CLI를 사용하여 리소스를 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-150">Then clean up the resources using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="02d15-151">새 저장소 계정에 Blob 쓰기</span><span class="sxs-lookup"><span data-stu-id="02d15-151">Write a blob into a new storage account</span></span>

<span data-ttu-id="02d15-152">`AzureApp.java`의 현재 main 메서드를 아래 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-152">Replace the current main method in `AzureApp.java` with the code below.</span></span> <span data-ttu-id="02d15-153">이 코드에서는 [Azure 저장소 계정](https://docs.microsoft.com/azure/storage/storage-introduction)을 만든 다음 Java용 Azure Storage 라이브러리를 사용하여 클라우드에 새 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-153">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Java to create a new text file in the cloud.</span></span>

```java
    public static void main(String[] args) {

        try {

            // use the properties file with the service principal information to authenticate
            // change the name of the environment variable if you used a different name in the previous step
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            // create a new storage account
            String storageAccountName = SdkContext.randomResourceName("st",8);
            StorageAccount storage = azure.storageAccounts().define(storageAccountName)
                        .withRegion(Region.US_WEST2)
                        .withNewResourceGroup("sampleStorageResourceGroup")
                        .create();

            // create a storage container to hold the file
            List<StorageAccountKey> keys = storage.getKeys();
            final String storageConnection = "DefaultEndpointsProtocol=https;"
                   + "AccountName=" + storage.name()
                   + ";AccountKey=" + keys.get(0).value()
                    + ";EndpointSuffix=core.windows.net";

            CloudStorageAccount account = CloudStorageAccount.parse(storageConnection);
            CloudBlobClient serviceClient = account.createCloudBlobClient();

            // Container name must be lower case.
            CloudBlobContainer container = serviceClient.getContainerReference("helloazure");
            container.createIfNotExists();

            // Make the container public
            BlobContainerPermissions containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // write a blob to the container
            CloudBlockBlob blob = container.getBlockBlobReference("helloazure.txt");
            blob.uploadText("hello Azure");

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
}
```

<span data-ttu-id="02d15-154">명령줄에서 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-154">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="02d15-155">Azure Portal 또는 [Azure Storage 탐색기](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs)를 사용하여 저장소 계정에서 `helloazure.txt` 파일을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-155">You can browse for the `helloazure.txt` file in your storage account through the Azure portal or with [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span></span>

<span data-ttu-id="02d15-156">CLI를 사용하여 저장소 계정을 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-156">Clean up the storage account using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="02d15-157">더 많은 샘플 탐색</span><span class="sxs-lookup"><span data-stu-id="02d15-157">Explore more samples</span></span>

<span data-ttu-id="02d15-158">Java용 Azure 관리 라이브러리를 사용하여 리소스를 관리하고 작업을 자동화하는 방법에 대한 자세한 내용은 [가상 컴퓨터](java-sdk-azure-virtual-machine-samples.md), [웹앱](java-sdk-azure-web-apps-samples.md) 및 [SQL 데이터베이스](java-sdk-azure-sql-database-samples.md)에 대한 샘플 코드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02d15-158">To learn more about how to use the Azure management libraries for Java to manage resources and automate tasks, see our sample code for [virtual machines](java-sdk-azure-virtual-machine-samples.md), [web apps](java-sdk-azure-web-apps-samples.md) and [SQL database](java-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference-and-release-notes"></a><span data-ttu-id="02d15-159">참조 및 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="02d15-159">Reference and release notes</span></span>

<span data-ttu-id="02d15-160">[참조](http://docs.microsoft.com/java/api)는 모든 패키지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-160">A [reference](http://docs.microsoft.com/java/api) is available for all packages.</span></span>

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="02d15-161">도움말 가져오기 및 피드백 제공</span><span class="sxs-lookup"><span data-stu-id="02d15-161">Get help and give feedback</span></span>

<span data-ttu-id="02d15-162">[Stack Overflow(영문)](http://stackoverflow.com/questions/tagged/azure+java)의 커뮤니티에 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-162">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span></span> <span data-ttu-id="02d15-163">[GitHub 프로젝트](https://github.com/Azure/azure-sdk-for-java)에서 Java용 Azure 라이브러리에 대한 버그 및 열기 문제를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="02d15-163">Report bugs and open issues against the Azure libraries for Java on the [project GitHub](https://github.com/Azure/azure-sdk-for-java).</span></span>