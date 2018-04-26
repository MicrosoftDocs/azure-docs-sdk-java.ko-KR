---
title: Java용 Azure Data Lake Store 라이브러리
description: Java용 Data Lake Store 라이브러리에 대한 참조 설명서
keywords: Azure, Java, SDK, API, 빅 데이터, Data Lake
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: bcd1fd17759f7d171006d7b2126019d00d06d1db
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="azure-data-lake-store-libraries-for-java"></a><span data-ttu-id="1d82d-104">Java용 Azure Data Lake Store 라이브러리</span><span class="sxs-lookup"><span data-stu-id="1d82d-104">Azure Data Lake Store libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="1d82d-105">개요</span><span class="sxs-lookup"><span data-stu-id="1d82d-105">Overview</span></span>

<span data-ttu-id="1d82d-106">[Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview)를 사용하여 분석하기 위해 단일 위치에서 모든 크기, 형식 및 수집 속도 데이터를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="1d82d-106">Capture data of any size, type, and ingestion speed in a single place for analytics with [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

<span data-ttu-id="1d82d-107">Data Lake Store를 시작하려면 [Java를 사용하여 Azure Data Lake Store 시작](/azure/data-lake-store/data-lake-store-get-started-java-sdk)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1d82d-107">To get started with Data Lake Store, see [Get started with Azure Data Lake Store using Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).</span></span>


## <a name="client-library"></a><span data-ttu-id="1d82d-108">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="1d82d-108">Client library</span></span>

<span data-ttu-id="1d82d-109">클라이언트 라이브러리를 사용하여 파일을 읽거나 쓰고, 권한과 메타데이터를 설정하고, Data Lake Store의 파일과 디렉터리를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1d82d-109">Read and write files, set permissions and metadata, and manage files and directories in Data Lake Store with the client library.</span></span>

<span data-ttu-id="1d82d-110">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d82d-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="1d82d-111">예</span><span class="sxs-lookup"><span data-stu-id="1d82d-111">Example</span></span>

<span data-ttu-id="1d82d-112">정규화된 도메인 이름과 OAuth2 액세스 토큰에서 Data Lake 클라이언트를 만든 다음, Data Lake에서 파일을 만들고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="1d82d-112">Create a Data Lake client from a fully qualified domain name and OAuth2 access token, then create a file in Data Lake and write to it.</span></span>

```java
// AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);
ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

// create directory
client.createDirectory("/a/b/w");
        
// create file and write some content
String filename = "/a/b/c.txt";
OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
PrintStream out = new PrintStream(stream);
for (int i = 1; i <= 10; i++) {
    out.println("This is line #" + i);
    out.format("This is the same line (%d), but using formatted output. %n", i);
}
out.close();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="1d82d-113">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="1d82d-113">Explore the Client APIs</span></span>](/java/api/overview/azure/datalakestore/client)


## <a name="management-api"></a><span data-ttu-id="1d82d-114">관리 API</span><span class="sxs-lookup"><span data-stu-id="1d82d-114">Management API</span></span>

<span data-ttu-id="1d82d-115">관리 API를 사용하여 Data Lake Store 계정, 방화벽 규칙 및 신뢰할 수 있는 ID 공급자를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="1d82d-115">Use the management API to manage Data Lake Store accounts, firewall rules, and trusted identity providers.</span></span>

<span data-ttu-id="1d82d-116">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1d82d-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-store</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="1d82d-117">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="1d82d-117">Explore the Management APIs</span></span>](/java/api/overview/azure/datalakestore/management)

## <a name="samples"></a><span data-ttu-id="1d82d-118">샘플</span><span class="sxs-lookup"><span data-stu-id="1d82d-118">Samples</span></span>

<span data-ttu-id="1d82d-119">[Azure Data Lake 시작][1]</span><span class="sxs-lookup"><span data-stu-id="1d82d-119">[Azure Data Lake Get Started][1]</span></span> 

[1]: https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started

<span data-ttu-id="1d82d-120">앱에서 사용할 수 있는 [Azure Data Lake Store용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=lake)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="1d82d-120">Explore more [sample Java code for Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake) you can use in your apps.</span></span>
