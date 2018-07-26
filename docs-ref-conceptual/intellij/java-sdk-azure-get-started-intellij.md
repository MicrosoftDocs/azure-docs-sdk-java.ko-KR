---
title: Intellij를 사용하여 Java용 Azure 시작
description: Azure 구독을 사용하여 Java용 Azure 라이브러리의 기본적인 사용을 시작합니다.
keywords: Azure, Java, SDK, API, 인증, 시작
services: ''
documentationcenter: java
author: roygara
manager: timlt
editor: ''
ms.assetid: ''
ms.author: v-rogara
ms.date: 02/01/2018
ms.devlang: java
ms.prod: azure
ms.service: multiple
ms.topic: get-started-article
ms.technology: azure
ms.openlocfilehash: 5c122b09d9d431ddcec667e61230eb53968c52e7
ms.sourcegitcommit: 720c2eaf66532d277015610ec375c71e934d9ee6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
ms.locfileid: "29065500"
---
# <a name="get-started-with-the-azure-libraries-using-intellij"></a>Intellij를 사용하여 Azure 라이브러리 시작

이 가이드에서는 개발 환경 설정과 Java 용 Azure 라이브러리 사용을 안내합니다. Azure를 통해 인증하는 서비스 주체를 만들고 구독에서 Azure 리소스를 만들어 사용하는 특정 샘플 코드를 실행하게 됩니다. Intellij 사용은 Azure를 통한 Java 개발에서 선택 사항입니다. Maven 통합이 있는 모든 IDE가 작동합니다. 또는 IDE를 사용하지 않으려면 Mave을 사용하여 명령줄에서 코드를 실행할 수 있습니다.

## <a name="prerequisites"></a>필수 조건

- Azure 계정. 계정이 없으면 [체험 계정을 얻습니다](https://azure.microsoft.com/free/).
- [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) 또는 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)
- [Intellij](https://www.jetbrains.com/idea/)의 안정적인 최신 버전

## <a name="set-up-authentication"></a>인증 설정

이 자습서에서 샘플 코드를 실행하려면 Azure 구독에 대한 읽기 및 만들기 권한이 Java 응용 프로그램에 필요합니다. 서비스 사용자를 만들고 해당 자격 증명을 사용하여 실행되도록 응용 프로그램을 구성합니다. 서비스 주체는 앱에서 실행하는 데 필요한 권한만 부여하는 ID와 연결되는 비대화형 계정을 만드는 방법을 제공합니다.

계정 자격 증명을 직접 사용하지 않고 구독에서 리소스를 만들어 업데이트하기 위해 [서비스 주체를 만들어](/cli/azure/create-an-azure-service-principal-azure-cli) 코드 권한을 부여합니다. 출력을 캡처할 수 있는지 확인합니다. 암호 인수에 `MY_SECURE_PASSWORD` 대신 [보안 암호](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy)를 제공합니다. 암호는 8~16자이고 다음 4개 기준 중 3개 이상에 부합해야 합니다.

* 소문자 포함
* 대문자 포함
* 숫자 포함
* @ # $ % ^ & *-_! 기호 중 하나 포함 + = [ ] { } | \ : ‘ , . ? / ` ~ “ ( ) ;


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

다음 형식으로 답장 제공:

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

다음으로 시스템의 텍스트 파일에 다음 예제를 복사합니다.

```text
# sample management library properties file
subscription=ssssssss-ssss-ssss-ssss-ssssssssssss
client=cccccccc-cccc-cccc-cccc-cccccccccccc
key=kkkkkkkkkkkkkkkk
tenant=tttttttt-tttt-tttt-tttt-tttttttttttt
managementURI=https\://management.core.windows.net/
baseURL=https\://management.azure.com/
authURL=https\://login.windows.net/
graphURL=https\://graph.windows.net/
```

상위 4개 값을 다음과 같이 바꿉니다.

- subscription: Azure CLI 2.0에서 `az account show`의 *id* 값을 사용합니다.
- client: 서비스 사용자 출력에서 가져온 출력의 *appId* 값을 사용합니다.
- key: 서비스 사용자 출력의 *password* 값을 사용합니다.
- tenant: 서비스 사용자 출력의 *tenant* 값을 사용합니다.

코드에서 읽을 수 있는 시스템의 안전한 위치에 이 파일을 저장합니다. 향후 코드에서 이 파일을 사용할 수 있으므로 이 문서에서 응용 프로그램의 외부에 저장해 두는 것이 좋습니다. 

셸에서 인증 파일의 전체 경로가 포함된 `AZURE_AUTH_LOCATION` 환경 변수를 설정합니다.  

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

Windows 환경에서 작업할 경우 변수를 시스템 속성에 추가합니다. 관리자 권한으로 PowerShell 창을 열고 두 번째 변수를 파일 경로로 바꾼 후 다음 명령을 입력합니다.

```powershell
setx AZURE_AUTH_LOCATION "C:\<fullpath>\azureauth.properties" /m
```

## <a name="create-a-new-maven-project"></a>새 Maven 프로젝트 만들기

> [!NOTE]
> 이 가이드에서는 Maven 빌드 도구를 사용하여 샘플 코드를 빌드하고 실행하지만, Gradle과 같은 다른 빌드 도구도 Java용 Azure 라이브러리에서 작동합니다. 

Intellij를 열고 파일 > 새로 만들기 > 프로젝트...를 선택합니다. 그러면 다음 화면으로 진행합니다.

GroupID에 "com.fabrikam"을 입력하고 원하는 아티팩트 ID를 입력합니다.

마지막 화면으로 진행하고 프로젝트 만들기를 만칩니다.

이제 pom.xml 파일을 엽니다. 그리고 다음 코드를 추가합니다.

```XML
<dependencies>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
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
</dependencies>
```

pom.xml을 저장합니다.
   
## <a name="install-the-azure-toolkit-for-intellij"></a>IntelliJ용 Azure 도구 키트를 설치합니다.

[Azure 도구 키트](azure-toolkit-for-intellij-installation.md)는 웹앱이나 API를 프로그래밍 방식으로 설치하지만 현재 다른 개발 유형에는 사용하고 있지 않은 경우에 필요합니다. 다음은 설치 프로세스에 대한 요약입니다. 자세한 절차는 [IntelliJ용 Azure 도구 키트 설치](azure-toolkit-for-intellij-installation.md)를 참조하세요.

**파일** 메뉴를 선택한 다음 **설정...** 을 선택합니다. 

**저장소 찾아보기...** 를 선택하고 “Azure”를 검색한 다음 **Intellij용 Azure 도구 키트**를 설치합니다.

Intellij를 다시 시작합니다.

## <a name="create-a-linux-virtual-machine"></a>Linux 가상 머신 만들기

프로젝트의 `src/main/java` 디렉터리에 `AzureApp.java`라는 새 파일을 만들고 다음 코드 블록에 붙여넣습니다. `userName` 및 `sshKey` 변수를 컴퓨터에 대한 실제 값으로 업데이트합니다. 이 코드에서는 미국 동부 Azure 지역에서 실행되는 `sampleResourceGroup` 리소스 그룹에 `testLinuxVM`이라는 새 Linux VM을 만듭니다.

`sshkey`를 만들기 위해 Azure Cloud Shell을 열고 `ssh-keygen -t rsa -b 2048`을 입력합니다. 파일 이름을 입력하고 .public 파일에 액세스하여 키를 가져옵니다. 이 키는 다음 코드에서 사용하며 복사하여 `sshKey` 변수에 붙여 넣습니다.

```java

import com.microsoft.azure.management.Azure;
import com.microsoft.azure.management.compute.VirtualMachine;
import com.microsoft.azure.management.compute.KnownLinuxVirtualMachineImage;
import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
import com.microsoft.azure.management.appservice.PricingTier;
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
import java.util.List;

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
                    .withPrimaryPrivateIPAddressDynamic()
                    .withoutPrimaryPublicIPAddress()
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


SDK에서 기본 호출을 Azure REST API로 설정하여 가상 머신 및 해당 리소스를 구성할 때 콘솔에서 일부 REST 요청과 응답이 표시됩니다. 프로그램이 완료되면 Azure CLI 2.0을 사용하여 구독의 가상 머신을 확인합니다.

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

코드가 작동하는지 확인했으면 CLI를 사용하여 VM과 해당 리소스를 삭제합니다.

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a>GitHub 리포지토리에서 웹앱 배포

`AzureApp.java`의 main 메서드를 아래 코드로 바꾸고, 이 코드를 실행하기 전에 `appName` 변수를 고유한 값으로 업데이트합니다. 이 코드에서는 공용 GitHub 리포지토리의 `master` 분기에 있는 웹 응용 프로그램을 체험 가격 책정 계층에서 실행되는 새 [Azure App Service 웹앱](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)으로 배포합니다.

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

Maven을 사용하기 전에 다음 코드를 실행합니다.

CLI를 사용하여 응용 프로그램을 가리키는 브라우저를 엽니다.

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```
배포를 확인한 후 구독에서 웹앱을 제거하고 계획합니다.

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a>Azure SQL Database에 연결

`AzureApp.java`의 현재 main 메서드를 `dbPassword` 변수에 대한 실제 값을 설정하는 아래 코드로 바꿉니다.
이 코드에서는 원격 액세스를 허용하는 방화벽 규칙이 있는 새 SQL 데이터베이스를 만든 다음 SQL Database JBDC 드라이버를 사용하여 연결합니다. 

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
명령줄에서 샘플을 실행합니다.

```
mvn clean compile exec:java
```

그런 다음 CLI를 사용하여 리소스를 정리합니다.

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a>새 저장소 계정에 Blob 쓰기

`AzureApp.java`의 현재 main 메서드를 아래 코드로 바꿉니다. 이 코드에서는 [Azure 저장소 계정](https://docs.microsoft.com/azure/storage/storage-introduction)을 만든 다음 Java용 Azure Storage 라이브러리를 사용하여 클라우드에 새 텍스트 파일을 만듭니다.

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

명령줄에서 샘플을 실행합니다.

Azure Portal 또는 [Azure Storage 탐색기](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs)를 사용하여 저장소 계정에서 `helloazure.txt` 파일을 찾아볼 수 있습니다.

CLI를 사용하여 저장소 계정을 정리합니다.

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a>더 많은 샘플 탐색

Java용 Azure 관리 라이브러리를 사용하여 리소스를 관리하고 작업을 자동화하는 방법에 대한 자세한 내용은 [가상 머신](../java-sdk-azure-virtual-machine-samples.md), [웹앱](../java-sdk-azure-web-apps-samples.md) 및 [SQL 데이터베이스](../java-sdk-azure-sql-database-samples.md)에 대한 샘플 코드를 참조하세요.

## <a name="reference-and-release-notes"></a>참조 및 릴리스 정보

[참조](http://docs.microsoft.com/java/api)는 모든 패키지에서 사용할 수 있습니다.

## <a name="get-help-and-give-feedback"></a>도움말 가져오기 및 피드백 제공

[Stack Overflow(영문)](http://stackoverflow.com/questions/tagged/azure+java)의 커뮤니티에 질문을 게시합니다. [GitHub 프로젝트](https://github.com/Azure/azure-sdk-for-java)에서 Java용 Azure 라이브러리에 대한 버그 및 열기 문제를 보고합니다.
