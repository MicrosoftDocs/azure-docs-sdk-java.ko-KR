---
title: Java용 Azure 관리 라이브러리를 사용하여 인증
description: Java용 Azure 관리 라이브러리에 서비스 사용자를 인증합니다.
keywords: Azure, Java, SDK, API, Maven, Gradle, 인증, Active Directory, 서비스 사용자
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 10f457e3-578b-4655-8cd1-51339226ee7d
ms.openlocfilehash: 88354039ad98050f5dee2e7eeadf7f399cd36014
ms.sourcegitcommit: 0f38ef9ad64cffdb7b2e9e966224dfd0af251b0f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703386"
---
# <a name="authenticate-with-the-azure-libraries-for-java"></a><span data-ttu-id="dd54c-104">Java용 Azure 라이브러리를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="dd54c-104">Authenticate with the Azure libraries for Java</span></span> 

## <a name="connect-to-services-with-connection-strings"></a><span data-ttu-id="dd54c-105">연결 문자열을 사용하여 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="dd54c-105">Connect to services with connection strings</span></span>

<span data-ttu-id="dd54c-106">대부분의 Azure 서비스 라이브러리는 인증에 연결 문자열 또는 보안 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-106">Most Azure service libraries use a connection string or secure key for authentication.</span></span> <span data-ttu-id="dd54c-107">예를 들어 SQL Database에는 JDBC 연결 문자열에 사용자 이름과 암호 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-107">For example, SQL Database includes username and password information in the JDBC connection string:</span></span>

```java
String url = "jdbc:sqlserver://myazuredb.database.windows.net:1433;" + 
        "database=testjavadb;" + 
        "user=myazdbuser;" +
        "password=myazdbpass;" +
        "encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
        Connection conn = DriverManager.getConnection(url);
```

<span data-ttu-id="dd54c-108">Azure Storage는 저장소 키를 사용하여 응용 프로그램에 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-108">Azure Storage uses a storage key to authorize the application:</span></span>

```java
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName 
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";
```

<span data-ttu-id="dd54c-109">서비스 연결 문자열은 [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/sql-api-java-application#UseService), [Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started) 및 [Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues)와 같은 다른 Azure 서비스를 인증하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-109">Service connection strings are used to authenticate to other Azure services like [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/sql-api-java-application#UseService), [Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started), and [Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues).</span></span> <span data-ttu-id="dd54c-110">Azure Portal 또는 CLI를 사용하여 연결 문자열을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-110">You can get the connection strings using the Azure portal or the CLI.</span></span>  <span data-ttu-id="dd54c-111">또한 Java용 Azure 관리 라이브러리를 사용하여 코드에서 연결 문자열을 작성하는 리소스를 쿼리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-111">You can also use the Azure management libraries for Java to query resources to build connection strings in your code.</span></span> 

<span data-ttu-id="dd54c-112">예를 들어 다음 코드에서는 관리 라이브러리를 사용하여 저장소 계정 연결 문자열을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-112">For example, this code uses the management libraries to create a storage account connection string:</span></span>

```java
// create a new storage account
StorageAccount storage = azure.storageAccounts().getByResourceGroup("myResourceGroup","myStorageAccount");

// create a storage container to hold the file
List<StorageAccountKey> keys = storage.getKeys();
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.name()
        + ";AccountKey=" + keys.get(0).value()
        + ";EndpointSuffix=core.windows.net";
```

<span data-ttu-id="dd54c-113">다른 라이브러리에서는 권한이 부여된 자격 증명을 사용하여 응용 프로그램 실행 권한을 부여하는 [서비스 사용자](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)를 통해 응용 프로그램을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-113">Other libraries require your application to run with a [service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) authorizing the application to run with granted credentials.</span></span> <span data-ttu-id="dd54c-114">이 구성은 아래에서 나열하는 관리 라이브러리에 대한 개체 기반 인증 단계와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-114">This configuration is similar to the object-based authentication steps for the management library listed below.</span></span>

<a name="mgmt-auth"></a>

##  <a name="authenticate-with-the-azure-management-libraries-for-java"></a><span data-ttu-id="dd54c-115">Java용 Azure 관리 라이브러리를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="dd54c-115">Authenticate with the Azure management libraries for Java</span></span>

<span data-ttu-id="dd54c-116">Java 관리 라이브러리를 사용하여 리소스를 만들고 관리할 때 Azure를 통해 응용 프로그램을 인증하는 데에는 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-116">Two options are available to authenticate your application with Azure when using the Java management libraries to create and manage resources.</span></span>

### <a name="authenticate-with-an-applicationtokencredentials-object"></a><span data-ttu-id="dd54c-117">ApplicationTokenCredentials 개체를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="dd54c-117">Authenticate with an ApplicationTokenCredentials object</span></span>

<span data-ttu-id="dd54c-118">`ApplicationTokenCredentials`의 인스턴스를 만들어 코드 내의 최상위 `Azure` 개체에 서비스 사용자 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-118">Create an instance of `ApplicationTokenCredentials` to supply the service principal credentials to the top-level `Azure` object from inside your code.</span></span>

```java
import com.microsoft.azure.credentials.ApplicationTokenCredentials;
import com.microsoft.azure.AzureEnvironment;

// ...

ApplicationTokenCredentials credentials = new ApplicationTokenCredentials(client, 
        tenant,
        key, 
        AzureEnvironment.AZURE);
        
Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credentials)
        .withDefaultSubscription();
```

<span data-ttu-id="dd54c-119">`client`, `tenant` 및 `key`는 [파일 기반 인증](#mgmt-file)에 사용되는 것과 동일한 서비스 사용자 값입니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-119">The `client`, `tenant` and `key` are the same service principal values used with [file-based authentication](#mgmt-file).</span></span> <span data-ttu-id="dd54c-120">`AzureEnvironment.AZURE` 값은 Azure 공용 클라우드에 대한 자격 증명을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-120">The `AzureEnvironment.AZURE` value creates credentials against the Azure public cloud.</span></span> <span data-ttu-id="dd54c-121">다른 클라우드에 액세스해야 하는 경우 이 값을 다른 값으로 변경합니다(예: `AzureEnvironment.AZURE_GERMANY`).</span><span class="sxs-lookup"><span data-stu-id="dd54c-121">Change this to a different value if you need to access another cloud (for example, `AzureEnvironment.AZURE_GERMANY`).</span></span>  

 <span data-ttu-id="dd54c-122">환경 변수 또는 [Key Vault](/azure/key-vault/key-vault-whatis)와 같은 비밀 관리 저장소에서 서비스 사용자 값을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-122">Read the service principal values from environment variables or a secret management store like [Key Vault](/azure/key-vault/key-vault-whatis).</span></span> <span data-ttu-id="dd54c-123">자격 증명이 실수로 버전 제어 기록에 노출되지 않도록 이러한 값은 코드에서 일반 텍스트 문자열로 설정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="dd54c-123">Avoid setting these values as cleartext strings in your code to prevent accidentally exposing credentials in your version control history.</span></span>   

<a name="mgmt-file"></a>

### <a name="file-based-authentication-preview"></a><span data-ttu-id="dd54c-124">파일 기반 인증(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="dd54c-124">File based authentication (Preview)</span></span>

<span data-ttu-id="dd54c-125">가장 간단한 인증 방법은 다음 형식을 사용하여 [Azure 서비스 사용자](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)에 대한 자격 증명을 포함하는 속성 파일을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-125">The simplest way to authenticate is to create a properties file that contains credentials for an [Azure service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) using the following format:</span></span>

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

- <span data-ttu-id="dd54c-126">subscription: Azure CLI 2.0에서 `az account show`의 *id* 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-126">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="dd54c-127">client: 응용 프로그램을 실행하기 위해 만든 서비스 사용자에서 가져온 출력의 *appId* 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-127">client: use the *appId* value from the output taken from a service principal created to run the application.</span></span> <span data-ttu-id="dd54c-128">앱에 대한 서비스 사용자가 없는 경우 [Azure CLI 2.0을 사용하여 서비스 사용자를 만듭니다](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dd54c-128">If you don't have a service principal for your app, [create one with the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span></span>
- <span data-ttu-id="dd54c-129">key: 서비스 사용자 만들기 CLI 출력의 *password* 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-129">key: use the *password* value from the service principal create CLI output</span></span> 
- <span data-ttu-id="dd54c-130">tenant: 서비스 사용자 만들기 CLI 출력의 *tenant* 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-130">tenant: use the *tenant* value from the service principal create CLI output</span></span>

<span data-ttu-id="dd54c-131">코드에서 읽을 수 있는 시스템의 안전한 위치에 이 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-131">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="dd54c-132">셸에서 파일의 전체 경로가 포함된 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-132">Set an environment variable with the full path to the file in your shell:</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="dd54c-133">`Azure` 진입점 개체를 만들어 라이브러리 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-133">Create the entry point `Azure` object to start working with the libraries.</span></span> <span data-ttu-id="dd54c-134">환경 변수를 통해 속성 파일의 위치를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="dd54c-134">Read the location of the properties file through the environment variable.</span></span>

```java
// pull in the location of the authenticaiton properties file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```



