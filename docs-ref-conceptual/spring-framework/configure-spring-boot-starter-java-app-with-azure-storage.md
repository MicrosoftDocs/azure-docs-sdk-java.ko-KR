---
title: Azure Storage에 Spring Boot Starter를 사용하는 방법
description: Azure Storage 스타터에 Spring Boot Initializer 앱을 구성하는 방법을 알아봅니다.
services: storage
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: a1f35df5939a51fa5ce50c29752226b6c7649a9d
ms.sourcegitcommit: 1c1412ad5d8960975c3fc7fd3d1948152ef651ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57335386"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a><span data-ttu-id="9a4f2-103">Azure Storage에 Spring Boot Starter를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9a4f2-103">How to use the Spring Boot Starter for Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="9a4f2-104">개요</span><span class="sxs-lookup"><span data-stu-id="9a4f2-104">Overview</span></span>

<span data-ttu-id="9a4f2-105">이 문서에서는 **Spring Initializr**을 사용하여 사용자 정의 애플리케이션을 만든 다음 애플리케이션에 Azure 저장소 스타터를 추가하고 애플리케이션을 사용하여 Azure 저장소 계정에 BLOB를 업로드하는 방법을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-105">This article walks you through creating a custom application using the **Spring Initializr**, then adding the Azure storage starter to your application, and then using your application to upload a blob to your Azure storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a4f2-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9a4f2-106">Prerequisites</span></span>

<span data-ttu-id="9a4f2-107">이 문서의 단계를 수행하기 위해 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="9a4f2-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)을 활성화하거나 [체험판 Azure 계정](https://azure.microsoft.com/pricing/free-trial/)에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9a4f2-109">[Azure CLI(명령줄 인터페이스)](http://docs.microsoft.com/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="9a4f2-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="9a4f2-110">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="9a4f2-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="9a4f2-111">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="9a4f2-112">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="9a4f2-112">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="9a4f2-113">이 문서의 단계를 완료하려면 Spring Boot 버전 2.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-113">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-storage-account-and-blob-container-for-your-application"></a><span data-ttu-id="9a4f2-114">애플리케이션에 대 한 Azure Storage 계정 및 Blob 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="9a4f2-114">Create an Azure Storage Account and blob container for your application</span></span>

1. <span data-ttu-id="9a4f2-115"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-115">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="9a4f2-116">**+리소스 만들기**를 클릭한 다음 **저장소**를 클릭하고 **저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-116">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Azure Storage 계정 만들기][IMG01]

1. <span data-ttu-id="9a4f2-118">**네임스페이스 만들기** 페이지에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-118">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="9a4f2-119">저장소 계정에 대한 URI의 일부가 되는 고유한 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-119">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="9a4f2-120">예: **wingtiptoysstorage**를 **이름**에 입력한 경우 URI는 *wingtiptoysstorage.core.windows.net*입니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-120">For example: if you entered **wingtiptoysstorage** for the **Name**, the URI would be *wingtiptoysstorage.core.windows.net*.</span></span>
   * <span data-ttu-id="9a4f2-121">**계정 종류**에 **Blob storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-121">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="9a4f2-122">저장소 계정의 **위치**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-122">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="9a4f2-123">저장소 계정에 사용하려는 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-123">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="9a4f2-124">저장소 계정에 새 **리소스 그룹**을 만들지 아니면 기존 리소스 그룹을 선택할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-124">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>

   ![Azure Storage 계정 옵션을 지정합니다.][IMG02]

1. <span data-ttu-id="9a4f2-126">위에 열거된 이러한 옵션을 지정한 경우 **만들기**를 클릭하여 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-126">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

1. <span data-ttu-id="9a4f2-127">Azure portal에서 저장소 계정을 만든 경우 **Blob**을 클릭하고 **+컨테이너**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-127">When the Azure portal has created your storage account, click **Blobs**, then click **+Container**.</span></span>

   ![Blob 컨테이너 만들기][IMG03]

1. <span data-ttu-id="9a4f2-129">Blob 컨테이너에 대한 **이름**을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-129">Enter a **Name** for your blob container, and then click **OK**.</span></span>

   ![Blob 컨테이너 옵션 지정][IMG04]

1. <span data-ttu-id="9a4f2-131">Azure portal은 Blob 컨테이너 생성 후 이를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-131">The Azure portal will list your blob container after is has been created.</span></span>

   ![Blob 컨테이너 목록 검토][IMG05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="9a4f2-133">Spring Initializr를 사용하여 간단한 Spring Boot 애플리케이션 만들기</span><span class="sxs-lookup"><span data-stu-id="9a4f2-133">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="9a4f2-134"><https://start.spring.io/>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-134">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="9a4f2-135">다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-135">Specify the following options:</span></span>

   * <span data-ttu-id="9a4f2-136">**Java**를 사용하는 **Maven** 프로젝트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-136">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="9a4f2-137">2.0 이상의 **Spring Boot** 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-137">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="9a4f2-138">애플리케이션에 대한 **그룹** 및 **아티팩트** 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-138">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="9a4f2-139">**Web** 종속성 추가</span><span class="sxs-lookup"><span data-stu-id="9a4f2-139">Add the **Web** dependency.</span></span>

      ![기본 Spring Initializr 옵션][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="9a4f2-141">Spring Initializr는 **그룹** 및 **아티팩트** 이름을 사용하여 패키지 이름을 만듭니다(예: *com.wingtiptoys.storage*).</span><span class="sxs-lookup"><span data-stu-id="9a4f2-141">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.storage*.</span></span>
   >

1. <span data-ttu-id="9a4f2-142">위에 열거된 이러한 옵션을 지정한 경우 **프로젝트 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-142">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="9a4f2-143">메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-143">When prompted, download the project to a path on your local computer.</span></span>

   ![Spring 프로젝트 다운로드][SI02]

1. <span data-ttu-id="9a4f2-145">로컬 시스템에서 파일의 압축을 푼 후에 단순한 Spring Boot 애플리케이션을 편집할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-145">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-storage-starter"></a><span data-ttu-id="9a4f2-146">Azure Storage Starter를 사용하도록 Spring Boot 앱 구성</span><span class="sxs-lookup"><span data-stu-id="9a4f2-146">Configure your Spring Boot app to use the Azure Storage starter</span></span>

1. <span data-ttu-id="9a4f2-147">앱의 루트 디렉터리에서 *pom.xml* 파일을 찾습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="9a4f2-147">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\pom.xml`

   <span data-ttu-id="9a4f2-148">또는</span><span class="sxs-lookup"><span data-stu-id="9a4f2-148">-or-</span></span>

   `/users/example/home/storage/pom.xml`

1. <span data-ttu-id="9a4f2-149">텍스트 편집기에서 *pom.xml* 파일을 열고 `<dependencies>` 목록에 Spring Cloud Azure Storage starter를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-149">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Storage starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-azure-starter-storage</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![pom.xml 파일을 편집합니다.][SI03]

1. <span data-ttu-id="9a4f2-151">*pom.xml* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-151">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="9a4f2-152">Azure 자격 증명 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="9a4f2-152">Create an Azure Credential File</span></span>

1. <span data-ttu-id="9a4f2-153">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-153">Open a command prompt.</span></span>

1. <span data-ttu-id="9a4f2-154">Spring Boot 앱의 *리소스* 디렉터리로 이동합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="9a4f2-154">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\storage\src\main\resources
   ```

   <span data-ttu-id="9a4f2-155">또는</span><span class="sxs-lookup"><span data-stu-id="9a4f2-155">-or-</span></span>

   ```shell
   cd /users/example/home/storage/src/main/resources
   ```

1. <span data-ttu-id="9a4f2-156">Azure 계정 로그인:</span><span class="sxs-lookup"><span data-stu-id="9a4f2-156">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="9a4f2-157">구독 나열:</span><span class="sxs-lookup"><span data-stu-id="9a4f2-157">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="9a4f2-158">Azure가 구독 목록을 반환하며 사용하려는 구독의 GUID를 복사해야 합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-158">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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
   ```

1. <span data-ttu-id="9a4f2-159">Azure에 사용하려는 구독에 대한 GUID를 지정합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="9a4f2-159">Specify the GUID for the subscription you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="9a4f2-160">Azure 자격 증명 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="9a4f2-160">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="9a4f2-161">이 명령은 *my.azureauth* 파일을 *리소스* 디렉터리에 다음 예제와 유사하게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-161">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-storage-account"></a><span data-ttu-id="9a4f2-162">Azure Storage 계정을 사용하도록 Spring Boot 앱 구성</span><span class="sxs-lookup"><span data-stu-id="9a4f2-162">Configure your Spring Boot app to use your Azure Storage account</span></span>

1. <span data-ttu-id="9a4f2-163">앱의 *리소스* 디렉터리에서 *application.properties* 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-163">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\resources\application.properties`

   <span data-ttu-id="9a4f2-164">또는</span><span class="sxs-lookup"><span data-stu-id="9a4f2-164">-or-</span></span>

   `/users/example/home/storage/src/main/resources/application.properties`

2. <span data-ttu-id="9a4f2-165">텍스트 편집기에서 *application.properties* 파일을 찾고 다음 줄을 추가하고 샘플 값을 저장소 계정의 적절한 속성으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-165">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your storage account:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.storage.account=wingtiptoysstorage
   ```
   <span data-ttu-id="9a4f2-166">위치:</span><span class="sxs-lookup"><span data-stu-id="9a4f2-166">Where:</span></span>

   |                   <span data-ttu-id="9a4f2-167">필드</span><span class="sxs-lookup"><span data-stu-id="9a4f2-167">Field</span></span>                   |                                            <span data-ttu-id="9a4f2-168">설명</span><span class="sxs-lookup"><span data-stu-id="9a4f2-168">Description</span></span>                                            |
   |-------------------------------------------|---------------------------------------------------------------------------------------------------|
   | `spring.cloud.azure.credential-file-path` |            <span data-ttu-id="9a4f2-169">이 자습서의 앞부분에서 만든 Azure 자격 증명 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-169">Specifies Azure credential file that you created earlier in this tutorial.</span></span>             |
   |    `spring.cloud.azure.resource-group`    |           <span data-ttu-id="9a4f2-170">Azure 저장소 계정을 포함하는 Azure 리소스 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-170">Specifies the Azure Resource Group that contains your Azure Storage account.</span></span>            |
   |        `spring.cloud.azure.region`        | <span data-ttu-id="9a4f2-171">Azure 저장소 계정을 만들 때 지정한 지리적 영역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-171">Specifies the geographical region that you specified when you created your Azure Storage account.</span></span> |
   |   `spring.cloud.azure.storage.account`    |            <span data-ttu-id="9a4f2-172">이 자습서의 앞부분에서 만든 Azure 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-172">Specifies Azure Storage account that you created earlier in this tutorial.</span></span>             |


3. <span data-ttu-id="9a4f2-173">*application.properties* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-173">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-azure-storage-functionality"></a><span data-ttu-id="9a4f2-174">기본 Azure 저장소 기능을 구현하는 샘플 코드 추가</span><span class="sxs-lookup"><span data-stu-id="9a4f2-174">Add sample code to implement basic Azure storage functionality</span></span>

<span data-ttu-id="9a4f2-175">이 섹션에서는 Azure 저장소 계정에서 Blob를 저장하는 데 필요한 Java 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-175">In this section, you create the necessary Java classes for storing a blob in your Azure storage account.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="9a4f2-176">기본 애플리케이션 클래스 수정</span><span class="sxs-lookup"><span data-stu-id="9a4f2-176">Modify the main application class</span></span>

1. <span data-ttu-id="9a4f2-177">앱의 패키지 디렉터리에서 기본 애플리케이션 Java 파일을 찾습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="9a4f2-177">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\StorageApplication.java`

   <span data-ttu-id="9a4f2-178">또는</span><span class="sxs-lookup"><span data-stu-id="9a4f2-178">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/StorageApplication.java`

1. <span data-ttu-id="9a4f2-179">텍스트 편집기에서 애플리케이션 Java 파일을 열고 다음 줄을 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-179">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

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

1. <span data-ttu-id="9a4f2-180">기본 애플리케이션 Java 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-180">Save and close the main application Java file.</span></span>

### <a name="add-a-web-controller-class"></a><span data-ttu-id="9a4f2-181">웹 컨트롤러 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="9a4f2-181">Add a web controller class</span></span>

1. <span data-ttu-id="9a4f2-182">앱의 패키지 디렉터리에 *WebController.java*라는 새 Java 파일을 작성합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="9a4f2-182">Create a new Java file named *WebController.java* in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\WebController.java`

   <span data-ttu-id="9a4f2-183">또는</span><span class="sxs-lookup"><span data-stu-id="9a4f2-183">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/WebController.java`

1. <span data-ttu-id="9a4f2-184">텍스트 편집기에서 웹 컨트롤러 Java 파일을 열고 다음 줄을 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-184">Open the web controller Java file in a text editor, and add the following lines to the file:</span></span>

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

   <span data-ttu-id="9a4f2-185">여기서 `@Value("blob://[container]/[blob]")` 구문은 데이터를 저장할 컨테이너 및 Blob의 이름을 각각 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-185">Where the `@Value("blob://[container]/[blob]")` syntax respectively defines the names of the container and blob where you want to store the data.</span></span>

1. <span data-ttu-id="9a4f2-186">웹 컨트롤러 Java 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-186">Save and close the web controller Java file.</span></span>

1. <span data-ttu-id="9a4f2-187">명령 프롬프트를 열고 디렉터리를 *pom.xml* 파일이 위치한 폴더로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="9a4f2-187">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\storage`

   <span data-ttu-id="9a4f2-188">또는</span><span class="sxs-lookup"><span data-stu-id="9a4f2-188">-or-</span></span>

   `cd /users/example/home/storage`

1. <span data-ttu-id="9a4f2-189">Maven을 사용하여 Spring Boot 애플리케이션을 빌드하고 실행합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="9a4f2-189">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="9a4f2-190">애플리케이션이 실행되면, 애플리케이션을 테스트하기 위해 *curl*을 사용할 수 있습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="9a4f2-190">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   <span data-ttu-id="9a4f2-191">a.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-191">a.</span></span> <span data-ttu-id="9a4f2-192">파일의 내용을 업데이트하려면 POST 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-192">Send a POST request to update a file's contents:</span></span>

      ```shell
      curl -X POST -H "Content-Type: text/plain" -d "Hello World" http://localhost:8080/
      ```

      <span data-ttu-id="9a4f2-193">파일이 업데이트되었다는 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-193">You should see a response that the file was updated.</span></span>

   <span data-ttu-id="9a4f2-194">b.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-194">b.</span></span> <span data-ttu-id="9a4f2-195">파일의 내용을 확인하려면 GET 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-195">Send a GET request to verify the file's contents:</span></span>

      ```shell
      curl -X GET http://localhost:8080/
      ```

     <span data-ttu-id="9a4f2-196">게시한 "Hello World" 텍스트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-196">You should see the "Hello World" text that you posted.</span></span>

## <a name="summary"></a><span data-ttu-id="9a4f2-197">요약</span><span class="sxs-lookup"><span data-stu-id="9a4f2-197">Summary</span></span>

<span data-ttu-id="9a4f2-198">이 자습서에서는 **[Spring Initializr]** 를 사용하여 새로운 Java 애플리케이션을 만들었으며, 애플리케이션에 Azure 스토리지 스타터를 추가했고 BLOB를 Azure 스토리지 계정에 업로드하도록 애플리케이션을 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-198">In this tutorial, you created a new Java application using the **[Spring Initializr]**, added the Azure storage starter to your application, and then configured your application to upload a blob to your Azure storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a4f2-199">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9a4f2-199">Next steps</span></span>

<span data-ttu-id="9a4f2-200">Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-200">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a4f2-201">Azure의 Spring</span><span class="sxs-lookup"><span data-stu-id="9a4f2-201">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="9a4f2-202">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9a4f2-202">Additional Resources</span></span>

<span data-ttu-id="9a4f2-203">Microsoft Azure에서 사용할 수 있는 다른 Spring Boot Starter에 대한 자세한 내용은 [Azure용 Spring Boot Starter](spring-boot-starters-for-azure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-203">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="9a4f2-204">Spring Boot 애플리케이션에서 호출할 수 있는 다른 Azure Storage API에 관한 상세 정보는 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a4f2-204">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="9a4f2-205">Java에서 Azure Blob Storage를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9a4f2-205">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="9a4f2-206">Java에서 Azure Queue Storage를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9a4f2-206">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="9a4f2-207">Java에서 Azure Table Storage를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9a4f2-207">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="9a4f2-208">Java에서 Azure File Storage를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="9a4f2-208">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)

<!-- IMG List -->

[IMG01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-01.png
[IMG02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-02.png
[IMG03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-03.png
[IMG04]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-04.png
[IMG05]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-03.png
