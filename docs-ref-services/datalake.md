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
ms.openlocfilehash: ebbadff83e1e081153f0ae376fb71d6607e63f15
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799799"
---
# <a name="azure-data-lake-store-libraries-for-java"></a>Java용 Azure Data Lake Store 라이브러리

## <a name="overview"></a>개요

[Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview)를 사용하여 분석하기 위해 단일 위치에서 모든 크기, 형식 및 수집 속도 데이터를 캡처합니다.

Data Lake Store를 시작하려면 [Java를 사용하여 Azure Data Lake Store 시작](/azure/data-lake-store/data-lake-store-get-started-java-sdk)을 참조하세요.


## <a name="client-library"></a>클라이언트 라이브러리

클라이언트 라이브러리를 사용하여 파일을 읽거나 쓰고, 권한과 메타데이터를 설정하고, Data Lake Store의 파일과 디렉터리를 관리합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

## <a name="example"></a>예

정규화된 도메인 이름과 OAuth2 액세스 토큰에서 Data Lake 클라이언트를 만든 다음, Data Lake에서 파일을 만들고 씁니다.

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
> [클라이언트 API 탐색](/java/api/overview/azure/datalakestore/client)


## <a name="management-api"></a>관리 API

관리 API를 사용하여 Data Lake Store 계정, 방화벽 규칙 및 신뢰할 수 있는 ID 공급자를 관리합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-store</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/java/api/overview/azure/datalakestore/management)

## <a name="samples"></a>샘플

[Azure Data Lake 시작][1] 

[1]: https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started

앱에서 사용할 수 있는 [Azure Data Lake Store용 Java 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=java&term=lake)를 추가로 탐색합니다.
