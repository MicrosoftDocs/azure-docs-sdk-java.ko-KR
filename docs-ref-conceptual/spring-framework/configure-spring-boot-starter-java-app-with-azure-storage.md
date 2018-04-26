---
title: Azure Storage에 Spring Boot Starter를 사용하는 방법
description: Azure Storage 스타터에 Spring Boot Initializer 앱을 구성하는 방법을 알아봅니다.
services: storage
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: yungez;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: e10ecfb7f6d705aa3ccffc49d354d1019f7f1a0b
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a><span data-ttu-id="192d5-103">Azure Storage에 Spring Boot Starter를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="192d5-103">How to use the Spring Boot Starter for Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="192d5-104">개요</span><span class="sxs-lookup"><span data-stu-id="192d5-104">Overview</span></span>

<span data-ttu-id="192d5-105">이 문서에서는 **Spring Initializr**를 사용하여 사용자 지정 응용 프로그램을 만든 다음 해당 응용 프로그램을 사용하여 Azure Storage에 액세스하는 방법을 살펴봅니다. </span><span class="sxs-lookup"><span data-stu-id="192d5-105">This article walks you through creating a custom application using the **Spring Initializr**, and then using that application to access Azure storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="192d5-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="192d5-106">Prerequisites</span></span>

<span data-ttu-id="192d5-107">이 문서의 단계를 수행하기 위해 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="192d5-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [무료 Azure 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="192d5-109">[Azure CLI(명령줄 인터페이스)](http://docs.microsoft.com/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="192d5-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="192d5-110">최신 [JDK(Java Development Kit)](http://www.oracle.com/technetwork/java/javase/downloads/), 버전 1.7 이상</span><span class="sxs-lookup"><span data-stu-id="192d5-110">An up-to-date [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="192d5-111">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="192d5-111">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="192d5-112">Spring Initializr를 사용하여 사용자 지정 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="192d5-112">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="192d5-113"><https://start.spring.io/>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-113">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="192d5-114">**Java**에서 **Maven** 프로젝트를 생성한다고 지정하고, 응용 프로그램에 대한 **그룹** 및 **아티팩트** 이름을 입력한 다음 Spring Initializr의 **정식 버전으로 전환**하는 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-114">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![기본 Spring Initializr 옵션](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-basic.png)

   > [!NOTE]
   >
   > <span data-ttu-id="192d5-116">Spring Initializr는 **그룹** 및 **아티팩트** 이름을 사용하여 패키지 이름을 만듭니다(예: *com.contoso.wingtiptoysdemo*).</span><span class="sxs-lookup"><span data-stu-id="192d5-116">The Spring Initializr will use the **Group** and **Aritifact** names to create the package name; for example: *com.contoso.wingtiptoysdemo*.</span></span>
   >

1. <span data-ttu-id="192d5-117">**Azure** 섹션까지 아래로 스크롤하고 **Azure Storage**의 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-117">Scroll down to the **Azure** section and check the box for **Azure Storage**.</span></span>

   ![전체 Spring Initializr 옵션](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-advanced.png)

1. <span data-ttu-id="192d5-119">페이지 하단까지 스크롤하고 버튼을 클릭하여 **프로젝트를 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![전체 Spring Initializr 옵션](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-generate.png)

1. <span data-ttu-id="192d5-121">메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-121">When prompted, download the project to a path on your local computer.</span></span>

   ![사용자 지정 Spring Boot 프로젝트 다운로드](media/configure-spring-boot-starter-java-app-with-azure-storage/download-app.png)

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a><span data-ttu-id="192d5-123">Azure에 로그인하고 사용할 구독 선택</span><span class="sxs-lookup"><span data-stu-id="192d5-123">Sign into Azure and select the subscription to use</span></span>

1. <span data-ttu-id="192d5-124">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-124">Open a command prompt.</span></span>

1. <span data-ttu-id="192d5-125">Azure CLI를 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-125">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="192d5-126">지시에 따라 로그인 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-126">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="192d5-127">구독 나열:</span><span class="sxs-lookup"><span data-stu-id="192d5-127">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="192d5-128">Azure가 구독 목록을 반환하며 사용하려는 구독의 GUID를 복사해야 합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-128">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "ssssssss-ssss-ssss-ssss-ssssssssssss",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "tttttttt-tttt-tttt-tttt-tttttttttttt",
       "user": {
         "name": "contoso@microsoft.com",
         "type": "user"
       }
     }
   ]
   ```

1. <span data-ttu-id="192d5-129">다음 예제처럼 Azure에 사용하려는 계정의 GUID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-129">Specify the GUID for the account you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="192d5-130">Azure Storage 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="192d5-130">Create an Azure Storage account</span></span>

1. <span data-ttu-id="192d5-131">이 문서에서 사용할 Azure 리소스에 대한 리소스 그룹을 만듭니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-131">Create a resource group for the Azure resources you will use in this article; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="192d5-132">위치:</span><span class="sxs-lookup"><span data-stu-id="192d5-132">Where:</span></span>
   | <span data-ttu-id="192d5-133">매개 변수</span><span class="sxs-lookup"><span data-stu-id="192d5-133">Parameter</span></span> | <span data-ttu-id="192d5-134">설명</span><span class="sxs-lookup"><span data-stu-id="192d5-134">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="192d5-135">리소스 그룹의 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-135">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="192d5-136">리소스 그룹을 호스팅할 [Azure 지역](https://azure.microsoft.com/regions/)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-136">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="192d5-137">Azure CLI가 다음 에제처럼 리소스 그룹 만들기 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-137">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/resourceGroups/wingtiptoysresources",
     "location": "westus",
     "managedBy": null,
     "name": "wingtiptoysresources",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```

1. <span data-ttu-id="192d5-138">Spring Boot 앱에 대한 리소스 그룹에서 Azure Storage 계정을 만듭니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-138">Create an Azure storage account in the in the resource group for your Spring Boot app; for example:</span></span>
   ```azurecli
   az storage account create --name wingtiptoysstorage --resource-group wingtiptoysresources --location westus --sku Standard_LRS
   ```
   <span data-ttu-id="192d5-139">위치:</span><span class="sxs-lookup"><span data-stu-id="192d5-139">Where:</span></span>
   | <span data-ttu-id="192d5-140">매개 변수</span><span class="sxs-lookup"><span data-stu-id="192d5-140">Parameter</span></span> | <span data-ttu-id="192d5-141">설명</span><span class="sxs-lookup"><span data-stu-id="192d5-141">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="192d5-142">저장소 계정에 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-142">Specifies a unique name for your storage account.</span></span> |
   | `resource-group` | <span data-ttu-id="192d5-143">이전 단계에서 만든 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-143">Specifies the name of the resource group group you created in the previous step.</span></span> |
   | `location` | <span data-ttu-id="192d5-144">저장소 계정을 호스팅할 [Azure 지역](https://azure.microsoft.com/regions/)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-144">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your storage account will be hosted.</span></span> |
   | `sku` | <span data-ttu-id="192d5-145">`Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS` 중 하나를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-145">Specifies one of the following: `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS`.</span></span> |

   <span data-ttu-id="192d5-146">Azure가 프로비전 상태를 포함하는 긴 JSON 문자열을 반환합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-146">Azure will return a long JSON string which contains the provisioning state; for example: |</span></span>
   
   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "identity": null,
     "kind": "Storage"
       ...
       ... (A long list of values will be displayed here.)
       ...
     "statusOfPrimary": "available",
     "statusOfSecondary": null,
     "tags": {},
     "type": "Microsoft.Storage/storageAccounts"
   }
   ```

1. <span data-ttu-id="192d5-147">저장소 계정에 대한 연결 문자열을 검색합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-147">Retrieve the connection string for your storage account; for example:</span></span>
   ```azurecli
   az storage account show-connection-string --name wingtiptoysstorage --resource-group wingtiptoysresources
   ```
   <span data-ttu-id="192d5-148">위치:</span><span class="sxs-lookup"><span data-stu-id="192d5-148">Where:</span></span>
   | <span data-ttu-id="192d5-149">매개 변수</span><span class="sxs-lookup"><span data-stu-id="192d5-149">Parameter</span></span> | <span data-ttu-id="192d5-150">설명</span><span class="sxs-lookup"><span data-stu-id="192d5-150">Description</span></span> |
   | ---|---|
   | `name` | <span data-ttu-id="192d5-151">이전 단계에서 만든 저장소 계정의 고유 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-151">Specifies a unique name of the storage account you created in previous steps.</span></span> |
   | `resource-group` | <span data-ttu-id="192d5-152">이전 단계에서 만든 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-152">Specifies the name of the resource group you created in previous steps.</span></span> |

   <span data-ttu-id="192d5-153">Azure가 저장소 계정에 대한 연결 문자열을 포함하는 JSON 문자열을 반환합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-153">Azure will return a JSON string which contains the connection string for your storage account; for example:</span></span>

   ```json
   {
     "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz=="
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="192d5-154">Spring Boot 응용 프로그램 구성 및 컴파일</span><span class="sxs-lookup"><span data-stu-id="192d5-154">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="192d5-155">디렉터리에 다운로드한 프로젝트 아카이브에서 파일을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-155">Extract the files from the downloaded project archive into a directory.</span></span>

1. <span data-ttu-id="192d5-156">프로젝트에서 *src/main/resources* 폴더로 이동하고 텍스트 편집기에서 *application.properties* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-156">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="192d5-157">저장소 계정의 키를 추가합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-157">Add the key for your storage account; for example:</span></span>
   ```yaml
   azure.storage.connection-string=DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz==
   ```

1. <span data-ttu-id="192d5-158">프로젝트에서 */src/main/java/com/example/wingtiptoysdemo* 폴더로 이동하고 텍스트 편집기에서 *WingtiptoysdemoApplication.java* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-158">Navigate to the */src/main/java/com/example/wingtiptoysdemo* folder in your project and open the *WingtiptoysdemoApplication.java* file in a text editor.</span></span>

1. <span data-ttu-id="192d5-159">기존 Java 코드를 컨테이너의 Blob를 나열하는 다음 예제로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-159">Replace the existing Java code with the following example that lists the blobs in a container:</span></span>

   ```java
   package com.example.wingtiptoysdemo;

   import com.microsoft.azure.storage.*;
   import com.microsoft.azure.storage.blob.*;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   import java.net.URISyntaxException;

   @SpringBootApplication
   public class WingtiptoysdemoApplication implements CommandLineRunner {

      @Autowired
      private CloudStorageAccount cloudStorageAccount;

      final String containerName = "mycontainer";

      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysdemoApplication.class, args);
      }

      public void run(String... var1)
             throws URISyntaxException, StorageException {
          // Create a container (if it does not exist).
          createContainerIfNotExists(containerName);
          // Upload a blob to the container.
          uploadTextBlob(containerName);
      }

      private void createContainerIfNotExists(String containerName)
            throws URISyntaxException, StorageException {
         try
         {
            // Create a blob client.
            final CloudBlobClient blobClient = cloudStorageAccount.createCloudBlobClient();
            // Get a reference to a container. (Name must be lower case.)
            final CloudBlobContainer container = blobClient.getContainerReference(containerName);
            // Create the container if it does not exist.
            container.createIfNotExists();
         }
         catch (Exception e)
         {
            // Output the stack trace.
            e.printStackTrace();
         }
      }

      private void uploadTextBlob(String containerName)
            throws URISyntaxException, StorageException {
         try
         {
            // Create a blob client.
            final CloudBlobClient blobClient = cloudStorageAccount.createCloudBlobClient();
            // Get a reference to a container. (Name must be lower case.)
            final CloudBlobContainer container = blobClient.getContainerReference(containerName);
            // Get a blob reference for a text file.
            CloudBlockBlob blob = container.getBlockBlobReference("test.txt");
            // Upload some text into the blob.
            blob.uploadText("Hello World!");
         }
         catch (Exception e)
         {
            // Output the stack trace.
            e.printStackTrace();
         }
      }
   }
   ```
   > [!NOTE]
   >
   > <span data-ttu-id="192d5-160">위의 예제는 *application.properties* 파일에서 정의된 저장소 계정 설정을 자동으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-160">The above example autowires the storage account settings that you defined in the *application.properties* file.</span></span>
   >

1. <span data-ttu-id="192d5-161">응용 프로그램 컴파일 및 실행:</span><span class="sxs-lookup"><span data-stu-id="192d5-161">Compile and run the application:</span></span>
   ```shell
   mvn clean package spring-boot:run
   ```
   
   <span data-ttu-id="192d5-162">응용 프로그램이 컨테이너를 만들고 텍스트 파일을 Blob 형태로 컨테이너에 업로드합니다. 이것은 [Azure Portal](https://portal.azure.com)의 저장소 계정 아래 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-162">The application will create a container and upload a text file as a blob to the container, which will be listed under your storage account in the [Azure portal](https://portal.azure.com).</span></span>

   ![Azure Portal에서 blob 나열](media/configure-spring-boot-starter-java-app-with-azure-storage/list-blobs-in-portal.png)

   > [!NOTE]
   > 
   > <span data-ttu-id="192d5-164">응용 프로그램을 컴파일할 때 다음 오류 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-164">When you compile your application, you might see the following error message:</span></span>
   > 
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[INFO] BUILD FAILURE`<br/>
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[INFO] Total time: 2.616 s`<br/>
   > `[INFO] Finished at: 2017-11-11T13:14:15Z`<br/>
   > `[INFO] Final Memory: 26M/213M`<br/>
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[ERROR] Failed to execute goal org.apache.maven.plugins:maven-surefire-plugin:2`<br/>
   > `.18.1:test (default-test) on project wingtiptoysdemo: Execution default-test of`<br/>
   > `goal org.apache.maven.plugins:maven-surefire-plugin:2.18.1:test failed: The for`<br/>
   > `ked VM terminated without properly saying goodbye. VM crash or System.exit called?`<br/>
   > `[ERROR] Command was /bin/sh -c cd /home/robert/SpringBoot/wingtiptoysdemo && /u`<br/>
   > `sr/lib/jvm/java-8-openjdk-amd64/jre/bin/java -jar /home/robert/SpringBoot/wingt`<br/>
   > `iptoysdemo/target/surefire/surefirebooter6371623993063346766.jar /home/robert/S`<br/>
   > `pringBoot/wingtiptoysdemo/target/surefire/surefire5107893623933537917tmp /home/`<br/>
   > `robert/SpringBoot/wingtiptoysdemo/target/surefire/surefire_01414159391084128068tmp`<br/>
   > `[ERROR] -> [Help 1]`<br/>
   > 
   > <span data-ttu-id="192d5-165">이 경우 Maven Surefire 테스트를 사용하지 않게 설정할 수 있습니다. 이를 위해 다음 플러그인 항목을 *pom.xml* 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="192d5-165">If this happens, you might want to disable the Maven Surefire testing; to do so, add the following plugin entry in your *pom.xml* file:</span></span>
   > 
   > ```xml
   > <plugin>
   >   <groupId>org.apache.maven.plugins</groupId>
   >   <artifactId>maven-surefire-plugin</artifactId>
   >   <version>2.20.1</version>
   >   <configuration>
   >     <skipTests>true</skipTests>
   >   </configuration>
   > </plugin>
   > ```
   > 

## <a name="next-steps"></a><span data-ttu-id="192d5-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="192d5-166">Next steps</span></span>

<span data-ttu-id="192d5-167">Microsoft Azure에서 사용할 수 있는 다른 Spring Boot Starter에 대한 자세한 내용은 [Azure용 Spring Boot Starter](spring-boot-starters-for-azure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="192d5-167">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="192d5-168">Azure 기능과 Spring 기반 응용 프로그램 통합에 대한 다른 정보는 [Azure의 Spring 프레임워크](/java/azure/spring-framework/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="192d5-168">For additional information about integrating Azure functionality into your Spring-based applications, see [Spring Framework on Azure](/java/azure/spring-framework/).</span></span>

<span data-ttu-id="192d5-169">Spring Boot 응용 프로그램에서 호출할 수 있는 다른 Azure Storage API에 관한 상세 정보는 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="192d5-169">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="192d5-170">Java에서 Azure Blob Storage를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="192d5-170">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="192d5-171">Java에서 Azure Queue Storage를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="192d5-171">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="192d5-172">Java에서 Azure Table Storage를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="192d5-172">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="192d5-173">Java에서 Azure File Storage를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="192d5-173">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)
