---
title: Azure Storage에 Spring Boot Starter를 사용하는 방법
description: Azure Storage 스타터에 Spring Boot Initializer 앱을 구성하는 방법을 알아봅니다.
services: storage
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 09/10/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: 4838b6dbd354ad941df12933dddfa7f3e7eef905
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799969"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a>Azure Storage에 Spring Boot Starter를 사용하는 방법

## <a name="overview"></a>개요

이 문서에서는 **Spring Initializr**을 사용하여 사용자 정의 응용 프로그램을 만든 다음 응용 프로그램에 Azure 저장소 스타터를 추가하고 응용 프로그램을 사용하여 Azure 저장소 계정에 BLOB를 업로드하는 방법을 안내합니다.

## <a name="prerequisites"></a>필수 조건

이 문서의 단계를 수행하기 위해 다음 필수 구성 요소가 필요합니다.

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [체험판 Azure 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.
* [Azure CLI(명령줄 인터페이스)](http://docs.microsoft.com/cli/azure/overview)
* 최신 [JDK(Java Development Kit)](http://www.oracle.com/technetwork/java/javase/downloads/), 버전 1.7 이상
* [Apache Maven](http://maven.apache.org/), 버전 3.0 이상

> [!IMPORTANT]
>
> 이 문서의 단계를 완료하려면 Spring Boot 버전 2.0 이상이 필요합니다.
>

## <a name="create-an-azure-storage-account-and-blob-container-for-your-application"></a>응용 프로그램에 대 한 Azure Storage 계정 및 Blob 컨테이너 만들기

1. <https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.

1. **+리소스 만들기**를 클릭한 다음 **저장소**를 클릭하고 **저장소 계정**을 클릭합니다.

   ![Azure Storage 계정 만들기][IMG01]

1. **네임스페이스 만들기** 페이지에서 다음 정보를 입력합니다.

   * 저장소 계정에 대한 URI의 일부가 되는 고유한 **이름**을 입력합니다. 예: **wingtiptoysstorage**를 **이름**에 입력한 경우 URI는 *wingtiptoysstorage.core.windows.net*입니다.
   * **계정 종류**에 **Blob storage**를 선택합니다.
   * 저장소 계정의 **위치**를 지정합니다.
   * 저장소 계정에 사용하려는 **구독**을 선택합니다.
   * 저장소 계정에 새 **리소스 그룹**을 만들지 아니면 기존 리소스 그룹을 선택할지를 지정합니다.

   ![Azure Storage 계정 옵션을 지정합니다.][IMG02]

1. 위에 열거된 이러한 옵션을 지정한 경우 **만들기**를 클릭하여 저장소 계정을 만듭니다.

1. Azure portal에서 저장소 계정을 만든 경우 **Blob**을 클릭하고 **+컨테이너**를 클릭합니다.

   ![Blob 컨테이너 만들기][IMG03]

1. Blob 컨테이너에 대한 **이름**을 입력하고 **확인**을 클릭합니다.

   ![Blob 컨테이너 옵션 지정][IMG04]

1. Azure portal은 Blob 컨테이너 생성 후 이를 나열 합니다.

   ![Blob 컨테이너 목록 검토][IMG05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Spring Initializr를 사용하여 간단한 Spring Boot 응용 프로그램 만들기

1. <https://start.spring.io/>로 이동합니다.

1. 다음 옵션을 지정합니다.

   * **Java**를 사용하는 **Maven** 프로젝트를 생성합니다.
   * 2.0 이상의 **Spring Boot** 버전을 지정합니다.
   * 응용 프로그램에 대한 **그룹** 및 **아티팩트** 이름을 지정합니다.
   * **Web** 종속성 추가

      ![기본 Spring Initializr 옵션][SI01]

   > [!NOTE]
   >
   > Spring Initializr는 **그룹** 및 **아티팩트** 이름을 사용하여 패키지 이름을 만듭니다(예: *com.wingtiptoys.storage*).
   >

1. 위에 열거된 이러한 옵션을 지정한 경우 **프로젝트 만들기**를 클릭합니다.

1. 메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.

   ![Spring 프로젝트 다운로드][SI02]

1. 로컬 시스템에서 파일의 압축을 푼 후에 단순한 Spring Boot 응용 프로그램을 편집할 준비를 합니다.

## <a name="configure-your-spring-boot-app-to-use-the-azure-storage-starter"></a>Azure Storage Starter를 사용하도록 Spring Boot 앱 구성

1. 앱의 루트 디렉터리에서 *pom.xml* 파일을 찾습니다. 예:

   `C:\SpringBoot\storage\pom.xml`

   또는

   `/users/example/home/storage/pom.xml`

1. 텍스트 편집기에서 *pom.xml* 파일을 열고 `<dependencies>` 목록에 Spring Cloud Azure Storage starter를 추가합니다.

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-azure-starter-storage</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![pom.xml 파일을 편집합니다.][SI03]

1. *pom.xml* 파일을 저장하고 닫습니다.

## <a name="create-an-azure-credential-file"></a>Azure 자격 증명 파일 만들기

1. 명령 프롬프트를 엽니다.

1. Spring Boot 앱의 *리소스* 디렉터리로 이동합니다. 예:

   ```shell
   cd C:\SpringBoot\storage\src\main\resources
   ```

   또는

   ```shell
   cd /users/example/home/storage/src/main/resources
   ```

1. Azure 계정 로그인:

   ```azurecli
   az login
   ```

1. 구독 나열:

   ```azurecli
   az account list
   ```
   Azure가 구독 목록을 반환하며 사용하려는 구독의 GUID를 복사해야 합니다. 예를 들어 다음과 같습니다.

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "11111111-1111-1111-1111-111111111111",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "22222222-2222-2222-2222-222222222222",
       "user": {
         "name": "gena.soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]

1. Specify the GUID for the subscription you want to use with Azure; for example:

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. Azure 자격 증명 파일 만들기

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   이 명령은 *my.azureauth* 파일을 *리소스* 디렉터리에 다음 예제와 유사하게 만듭니다.

   ```json
   {
     "clientId": "33333333-3333-3333-3333-333333333333",
     "clientSecret": "44444444-4444-4444-4444-444444444444",
     "subscriptionId": "11111111-1111-1111-1111-111111111111",
     "tenantId": "22222222-2222-2222-2222-222222222222",
     "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
     "resourceManagerEndpointUrl": "https://management.azure.com/",
     "activeDirectoryGraphResourceId": "https://graph.windows.net/",
     "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
     "galleryEndpointUrl": "https://gallery.azure.com/",
     "managementEndpointUrl": "https://management.core.windows.net/"
   }
   ```

## <a name="configure-your-spring-boot-app-to-use-your-azure-storage-account"></a>Azure Storage 계정을 사용하도록 Spring Boot 앱 구성

1. 앱의 *리소스* 디렉터리에서 *application.properties* 파일을 찾습니다.

   `C:\SpringBoot\storage\src\main\resources\application.properties`

   또는

   `/users/example/home/storage/src/main/resources/application.properties`

2. 텍스트 편집기에서 *application.properties* 파일을 찾고 다음 줄을 추가하고 샘플 값을 저장소 계정의 적절한 속성으로 바꿉니다.

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.storage.account=wingtiptoysstorage
   ```
   위치:

   |                   필드                   |                                            설명                                            |
   |-------------------------------------------|---------------------------------------------------------------------------------------------------|
   | `spring.cloud.azure.credential-file-path` |            이 자습서의 앞부분에서 만든 Azure 자격 증명 파일을 지정합니다.             |
   |    `spring.cloud.azure.resource-group`    |           Azure 저장소 계정을 포함하는 Azure 리소스 그룹을 지정합니다.            |
   |        `spring.cloud.azure.region`        | Azure 저장소 계정을 만들 때 지정한 지리적 영역을 지정합니다. |
   |   `spring.cloud.azure.storage.account`    |            이 자습서의 앞부분에서 만든 Azure 저장소 계정을 지정합니다.             |


3. *application.properties* 파일을 저장하고 닫습니다.

## <a name="add-sample-code-to-implement-basic-azure-storage-functionality"></a>기본 Azure 저장소 기능을 구현하는 샘플 코드 추가

이 섹션에서는 Azure 저장소 계정에서 Blob를 저장하는 데 필요한 Java 클래스를 만듭니다.

### <a name="modify-the-main-application-class"></a>기본 응용 프로그램 클래스 수정

1. 앱의 패키지 디렉터리에서 기본 응용 프로그램 Java 파일을 찾습니다. 예:

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\StorageApplication.java`

   또는

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/StorageApplication.java`

1. 텍스트 편집기에서 응용 프로그램 Java 파일을 열고 다음 줄을 파일에 추가합니다.

   ```java
   package com.wingtiptoys.storage;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class StorageApplication {
      public static void main(String[] args) {
         SpringApplication.run(StorageApplication.class, args);
      }
   }
   ```

1. 기본 응용 프로그램 Java 파일을 저장하고 닫습니다.

### <a name="add-a-web-controller-class"></a>웹 컨트롤러 클래스 추가

1. 앱의 패키지 디렉터리에 *WebController.java*라는 새 Java 파일을 작성합니다. 예:

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\WebController.java`

   또는

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/WebController.java`

1. 텍스트 편집기에서 웹 컨트롤러 Java 파일을 열고 다음 줄을 파일에 추가합니다.

   ```java
   package com.wingtiptoys.storage;

   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.core.io.Resource;
   import org.springframework.core.io.WritableResource;
   import org.springframework.util.StreamUtils;
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RestController;

   import java.io.IOException;
   import java.io.OutputStream;
   import java.nio.charset.Charset;

   @RestController
   public class WebController {

      @Value("blob://test/myfile.txt")
      private Resource blobFile;

      @GetMapping(value = "/")
      public String readBlobFile() throws IOException {
         return StreamUtils.copyToString(
            this.blobFile.getInputStream(),
            Charset.defaultCharset()) + "\n";
      }

      @PostMapping(value = "/")
      public String writeBlobFile(@RequestBody String data) throws IOException {
         try (OutputStream os = ((WritableResource) this.blobFile).getOutputStream()) {
            os.write(data.getBytes());
         }
         return "File was updated.\n";
      }
   }
   ```

   여기서 `@Value("blob://[container]/[blob]")` 구문은 데이터를 저장할 컨테이너 및 Blob의 이름을 각각 정의합니다.

1. 웹 컨트롤러 Java 파일을 저장하고 닫습니다.

1. 명령 프롬프트를 열고 디렉터리를 *pom.xml* 파일이 위치한 폴더로 변경합니다. 예:

   `cd C:\SpringBoot\storage`

   또는

   `cd /users/example/home/storage`

1. Maven을 사용하여 Spring Boot 응용 프로그램을 빌드하고 실행합니다. 예:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. 응용 프로그램이 실행되면, 응용 프로그램을 테스트하기 위해 *curl*을 사용할 수 있습니다. 예:

   a. 파일의 내용을 업데이트하려면 POST 요청을 보냅니다.

      ```shell
      curl -X POST -H "Content-Type: text/plain" -d "Hello World" http://localhost:8080/
      ```

      파일이 업데이트되었다는 응답이 표시됩니다.

   b. 파일의 내용을 확인하려면 GET 요청을 보냅니다.

      ```shell
      curl -X GET http://localhost:8080/
      ```

     게시한 "Hello World" 텍스트가 표시됩니다.

## <a name="next-steps"></a>다음 단계

Microsoft Azure에서 사용할 수 있는 다른 Spring Boot Starter에 대한 자세한 내용은 [Azure용 Spring Boot Starter](spring-boot-starters-for-azure.md)를 참조하세요.

Azure 기능과 Spring 기반 응용 프로그램 통합에 대한 다른 정보는 [Azure의 Spring 프레임워크](/java/azure/spring-framework/)를 참조하세요.

Spring Boot 응용 프로그램에서 호출할 수 있는 다른 Azure Storage API에 관한 상세 정보는 다음 문서를 참조하세요.
* [Java에서 Azure Blob Storage를 사용하는 방법](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [Java에서 Azure Queue Storage를 사용하는 방법](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [Java에서 Azure Table Storage를 사용하는 방법](/azure/cosmos-db/table-storage-how-to-use-java)
* [Java에서 Azure File Storage를 사용하는 방법](/azure/storage/files/storage-java-how-to-use-file-storage)

<!-- IMG List -->

[IMG01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-01.png
[IMG02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-02.png
[IMG03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-03.png
[IMG04]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-04.png
[IMG05]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-03.png
