---
title: Azure Event Hub를 사용하여 Apache Kafka에 대한 Spring Boot Starter를 사용하는 방법
description: Azure Event Hub를 사용하는 Azure Kafka를 사용하도록 Spring Boot Initializer를 사용하여 만든 응용 프로그램을 구성하는 방법에 대해 알아봅니다.
services: event-hubs
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 09/10/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: 85fe1d9c56530b716a1f1750713f4c87d43dfad3
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799959"
---
# <a name="how-to-use-the-spring-boot-starter-for-apache-kafka-with-azure-event-hubs"></a><span data-ttu-id="c1648-103">Azure Event Hub를 사용하여 Apache Kafka에 대한 Spring Boot Starter를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="c1648-103">How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="c1648-104">개요</span><span class="sxs-lookup"><span data-stu-id="c1648-104">Overview</span></span>

<span data-ttu-id="c1648-105">이 문서에서는 Azure Event Hub와 함께 [Apache Kafka]를 사용하도록 Spring Boot Initializer로 만든 Java 기반 Spring Cloud Stream Binder를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-105">This article demonstrates how to configure a Java-based Spring Cloud Stream Binder created with the Spring Boot Initializer to use [Apache Kafka] with Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1648-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c1648-106">Prerequisites</span></span>

<span data-ttu-id="c1648-107">이 문서의 단계를 수행하기 위해 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="c1648-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c1648-109">[JDK(Java Development Kit)](http://www.oracle.com/technetwork/java/javase/downloads/), 버전 1.7 이상</span><span class="sxs-lookup"><span data-stu-id="c1648-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="c1648-110">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="c1648-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="c1648-111">이 문서의 단계를 완료하려면 Spring Boot 버전 2.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-111">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a><span data-ttu-id="c1648-112">Azure Portal을 사용하여 Azure Event Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="c1648-112">Create an Azure Event Hub using the Azure portal</span></span>

### <a name="create-an-azure-event-hub-namespace"></a><span data-ttu-id="c1648-113">Event Hub 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="c1648-113">Create an Azure Event Hub Namespace</span></span>

1. <span data-ttu-id="c1648-114"><https://portal.azure.com/>에서 Azure Portal을 찾아 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-114">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="c1648-115">**+리소스 생성**을 클릭하고 **사물 인터넷**을 클릭한 다음, **Event Hub**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-115">Click **+Create a resource**, then **Internet of Things**, and then click **Event Hubs**.</span></span>

   ![Event Hub 네임스페이스 만들기][IMG01]

1. <span data-ttu-id="c1648-117">**네임스페이스 만들기** 페이지에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-117">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="c1648-118">이벤트 허브 네임스페이스에 대한 URI의 일부가 되는 고유한 **이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-118">Enter a unique **Name**, which will become part of the URI for your event hub namespace.</span></span> <span data-ttu-id="c1648-119">예: **wingtiptoys**를 **이름**에 입력한 경우 URI는 *wingtiptoys.servicebus.windows.net*입니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-119">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.</span></span>
   * <span data-ttu-id="c1648-120">이벤트 허브 네임스페이스에 대한 **가격 책정 계층**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-120">Choose a **Pricing tier** for your event hub namespace.</span></span>
   * <span data-ttu-id="c1648-121">네임스페이스에 대해 **Kafka 사용**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-121">Specify **Enable Kafka** for your namespace.</span></span>
   * <span data-ttu-id="c1648-122">네임스페이스에 사용하려는 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-122">Choose the **Subscription** you want to use for your namespace.</span></span>
   * <span data-ttu-id="c1648-123">네임스페이스에 새 **리소스 그룹**을 만들지 아니면 기존 리소스 그룹을 선택할지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-123">Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.</span></span>
   * <span data-ttu-id="c1648-124">이벤트 허브 네임 스페이스에 대한 **위치**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-124">Specify the **Location** for your event hub namespace.</span></span>

   ![Azure Event Hub 네임스페이스 옵션을 지정합니다.][IMG02]

1. <span data-ttu-id="c1648-126">위에 열거된 이러한 옵션을 지정한 경우 **만들기**를 클릭하여 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-126">When you have specified the options listed above, click **Create** to create your namespace.</span></span>

### <a name="create-an-azure-event-hub-in-your-namespace"></a><span data-ttu-id="c1648-127">네임스페이스에 Event Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="c1648-127">Create an Azure Event Hub in your namespace</span></span>

1. <span data-ttu-id="c1648-128"><https://portal.azure.com/>에서 Azure Portal로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-128">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="c1648-129">**모든 리소스**를 클릭한 다음, 만든 네임스페이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-129">Click **All resources**, and then click the namespace that you created.</span></span>

   ![Event Hub 네임스페이스 선택하기][IMG03]

1. <span data-ttu-id="c1648-131">**Event Hub**를 클릭하고 **+Event Hub**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-131">Click **Event Hubs**, and then click **+Event Hub**.</span></span>

   ![새 Azure 이벤트 허브 추가][IMG04]

1. <span data-ttu-id="c1648-133">**이벤트 허브 작성** 페이지에서 이벤트 허브에 대해 고유한 **이름**을 입력한 다음 **작성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-133">On the **Create Event Hub** page, enter a unique **Name** for your Event Hub, and then click **Create**.</span></span>

   ![Azure 이벤트 허브 만들기][IMG05]

1. <span data-ttu-id="c1648-135">이벤트 허브를 만들면 **Event Hub** 페이지에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-135">When your Event Hub has been created, it will be listed on the **Event Hubs** page.</span></span>

   ![Azure 이벤트 허브 만들기][IMG06]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="c1648-137">Spring Initializr를 사용하여 간단한 Spring Boot 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="c1648-137">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="c1648-138"><https://start.spring.io/>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-138">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="c1648-139">다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-139">Specify the following options:</span></span>

   * <span data-ttu-id="c1648-140">**Java**를 사용하는 **Maven** 프로젝트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-140">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="c1648-141">2.0 이상의 **Spring Boot** 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-141">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="c1648-142">응용 프로그램에 대한 **그룹** 및 **아티팩트** 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-142">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="c1648-143">**Web** 종속성 추가</span><span class="sxs-lookup"><span data-stu-id="c1648-143">Add the **Web** dependency.</span></span>

      ![기본 Spring Initializr 옵션][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="c1648-145">Spring Initializr는 **그룹** 및 **아티팩트** 이름을 사용하여 패키지 이름을 만듭니다(예: *com.wingtiptoys.kafka*).</span><span class="sxs-lookup"><span data-stu-id="c1648-145">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.kafka*.</span></span>
   >

1. <span data-ttu-id="c1648-146">위에 열거된 이러한 옵션을 지정한 경우 **프로젝트 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-146">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="c1648-147">메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-147">When prompted, download the project to a path on your local computer.</span></span>

   ![Spring 프로젝트 다운로드][SI02]

1. <span data-ttu-id="c1648-149">로컬 시스템에서 파일의 압축을 푼 후에 단순한 Spring Boot 응용 프로그램을 편집할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-149">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-spring-cloud-kafka-stream-and-azure-event-hub-starters"></a><span data-ttu-id="c1648-150">Cloud Kafka Stream 및 Azure Event Hub starter를 사용하도록 Spring Boot 앱 구성</span><span class="sxs-lookup"><span data-stu-id="c1648-150">Configure your Spring Boot app to use the Spring Cloud Kafka Stream and Azure Event Hub starters</span></span>

1. <span data-ttu-id="c1648-151">앱의 루트 디렉터리에서 *pom.xml* 파일을 찾습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c1648-151">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\kafka\pom.xml`

   <span data-ttu-id="c1648-152">또는</span><span class="sxs-lookup"><span data-stu-id="c1648-152">-or-</span></span>

   `/users/example/home/kafka/pom.xml`

1. <span data-ttu-id="c1648-153">텍스트 편집기에서 *pom.xml* 파일을 열고 `<dependencies>` 목록에 Spring Cloud Kafka Stream 및 Azure Event Hub starter를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-153">Open the *pom.xml* file in a text editor, and add the Spring Cloud Kafka Stream and Azure Event Hub starters to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-stream-kafka</artifactId>
      <version>2.0.1.RELEASE</version>
   </dependency>
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-starter-eventhub</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![pom.xml 파일을 편집합니다.][SI03]

1. <span data-ttu-id="c1648-155">*pom.xml* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-155">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="c1648-156">Azure 자격 증명 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="c1648-156">Create an Azure Credential File</span></span>

1. <span data-ttu-id="c1648-157">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-157">Open a command prompt.</span></span>

1. <span data-ttu-id="c1648-158">Spring Boot 앱의 *리소스* 디렉터리로 이동합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c1648-158">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   <span data-ttu-id="c1648-159">또는</span><span class="sxs-lookup"><span data-stu-id="c1648-159">-or-</span></span>

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. <span data-ttu-id="c1648-160">Azure 계정 로그인:</span><span class="sxs-lookup"><span data-stu-id="c1648-160">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="c1648-161">구독 나열:</span><span class="sxs-lookup"><span data-stu-id="c1648-161">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="c1648-162">Azure가 구독 목록을 반환하며 사용하려는 구독의 GUID를 복사해야 합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-162">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="c1648-163">Azure 자격 증명 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="c1648-163">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="c1648-164">이 명령은 *my.azureauth* 파일을 *리소스* 디렉터리에 다음 예제와 유사하게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-164">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a><span data-ttu-id="c1648-165">Azure Event Hub를 사용하도록 Spring Boot 앱 구성</span><span class="sxs-lookup"><span data-stu-id="c1648-165">Configure your Spring Boot app to use your Azure Event Hub</span></span>

1. <span data-ttu-id="c1648-166">앱의 *리소스* 디렉터리에서 *application.properties* 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-166">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   <span data-ttu-id="c1648-167">또는</span><span class="sxs-lookup"><span data-stu-id="c1648-167">-or-</span></span>

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. <span data-ttu-id="c1648-168">텍스트 편집기에서 *application.properties* 파일을 찾고 다음 줄을 추가하고 샘플 값을 이벤트 허브의 적절한 속성으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-168">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace

   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   ```
   <span data-ttu-id="c1648-169">위치:</span><span class="sxs-lookup"><span data-stu-id="c1648-169">Where:</span></span>

   |                       <span data-ttu-id="c1648-170">필드</span><span class="sxs-lookup"><span data-stu-id="c1648-170">Field</span></span>                       |                                                                                   <span data-ttu-id="c1648-171">설명</span><span class="sxs-lookup"><span data-stu-id="c1648-171">Description</span></span>                                                                                    |
   |---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `spring.cloud.azure.credential-file-path`     |                                                    <span data-ttu-id="c1648-172">이 자습서의 앞부분에서 만든 Azure 자격 증명 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-172">Specifies Azure credential file that you created earlier in this tutorial.</span></span>                                                    |
   |        `spring.cloud.azure.resource-group`        |                                                      <span data-ttu-id="c1648-173">Azure 이벤트 허브를 포함하는 Azure 리소스 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-173">Specifies the Azure Resource Group that contains your Azure Event Hub.</span></span>                                                      |
   |            `spring.cloud.azure.region`            |                                           <span data-ttu-id="c1648-174">Azure 이벤트 허브를 만들 때 지정한 지리적 영역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-174">Specifies the geographical region that you specified when you created your Azure Event Hub.</span></span>                                            |
   |      `spring.cloud.azure.eventhub.namespace`      |                                          <span data-ttu-id="c1648-175">Azure 이벤트 허브 네임스페이스를 만들 때 지정한 고유 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-175">Specifies the unique name that you specified when you created your Azure Event Hub Namespace.</span></span>                                           |
   | `spring.cloud.stream.bindings.input.destination`  |                            <span data-ttu-id="c1648-176">입력 대상 Azure Event Hub를 지정합니다.이 자습서에서는 이 자습서의 앞부분에서 만든 허브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-176">Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.</span></span>                            |
   |    `spring.cloud.stream.bindings.input.group `    | <span data-ttu-id="c1648-177">Azure Event Hub에서 소비자 그룹을 지정합니다. Azure Event Hub를 만들 때 생성된 기본 소비자 그룹을 사용하려면 '$Default'로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-177">Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub.</span></span> |
   | `spring.cloud.stream.bindings.output.destination` |                               <span data-ttu-id="c1648-178">출력 대상 Azure Event Hub를 지정합니다.이 자습서에서는 입력 대상과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-178">Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.</span></span>                               |


3. <span data-ttu-id="c1648-179">*application.properties* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-179">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a><span data-ttu-id="c1648-180">기본 이벤트 허브 기능을 구현하는 샘플 코드 추가</span><span class="sxs-lookup"><span data-stu-id="c1648-180">Add sample code to implement basic event hub functionality</span></span>

<span data-ttu-id="c1648-181">이 섹션에서는 이벤트를 이벤트 허브에 보내는 데 필요한 Java 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-181">In this section, you create the necessary Java classes for sending events to your event hub.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="c1648-182">기본 응용 프로그램 클래스 수정</span><span class="sxs-lookup"><span data-stu-id="c1648-182">Modify the main application class</span></span>

1. <span data-ttu-id="c1648-183">앱의 패키지 디렉터리에서 기본 응용 프로그램 Java 파일을 찾습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c1648-183">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\kafka\src\main\java\com\wingtiptoys\kafka\KafkaApplication.java`

   <span data-ttu-id="c1648-184">또는</span><span class="sxs-lookup"><span data-stu-id="c1648-184">-or-</span></span>

   `/users/example/home/kafka/src/main/java/com/wingtiptoys/kafka/KafkaApplication.java`

1. <span data-ttu-id="c1648-185">텍스트 편집기에서 응용 프로그램 Java 파일을 열고 다음 줄을 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-185">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.kafka;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class KafkaApplication {
      public static void main(String[] args) {
         SpringApplication.run(KafkaApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="c1648-186">기본 응용 프로그램 Java 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-186">Save and close the main application Java file.</span></span>


### <a name="create-a-new-class-for-the-source-connector"></a><span data-ttu-id="c1648-187">원본 커넥터에 대한 새 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="c1648-187">Create a new class for the source connector</span></span>

1. <span data-ttu-id="c1648-188">앱의 패키지 디렉터리에 *KafkaSource.java*라는 새 Java 파일을 만듭니다. 그리고 파일 텍스트 편집기에서 해당 파일을 열고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-188">Create a new Java file named *KafkaSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.kafka;

   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RequestParam;
   import org.springframework.web.bind.annotation.RestController;

   @EnableBinding(Source.class)
   @RestController
   public class KafkaSource {
      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String sendMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```

1. <span data-ttu-id="c1648-189">*KafkaSource.java* 파일을 저장 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-189">Save and close the *KafkaSource.java* file.</span></span>

### <a name="create-a-new-class-for-the-sink-connector"></a><span data-ttu-id="c1648-190">싱크 커넥터에 대한 새 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="c1648-190">Create a new class for the sink connector</span></span>

1. <span data-ttu-id="c1648-191">앱의 패키지 디렉터리에 *KafkaSink.java*라는 새 Java 파일을 만듭니다. 그리고 파일 텍스트 편집기에서 해당 파일을 열고 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-191">Create a new Java file named *KafkaSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.kafka;

   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;

   @EnableBinding(Sink.class)
   public class KafkaSink {
      private static final Logger LOGGER = LoggerFactory.getLogger(KafkaSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message) {
         LOGGER.info("New message received: " + message);
      }
   }
   ```

1. <span data-ttu-id="c1648-192">*KafkaSink.java* 파일을 저장 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-192">Save and close the *KafkaSink.java* file.</span></span>

## <a name="build-and-test-your-application"></a><span data-ttu-id="c1648-193">응용 프로그램 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="c1648-193">Build and test your application</span></span>

1. <span data-ttu-id="c1648-194">명령 프롬프트를 열고 디렉터리를 *pom.xml* 파일이 위치한 폴더로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c1648-194">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\kafka`

   <span data-ttu-id="c1648-195">또는</span><span class="sxs-lookup"><span data-stu-id="c1648-195">-or-</span></span>

   `cd /users/example/home/kafka`

1. <span data-ttu-id="c1648-196">Maven을 사용하여 Spring Boot 응용 프로그램을 빌드하고 실행합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c1648-196">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="c1648-197">응용 프로그램이 실행되면, 응용 프로그램을 테스트하기 위해 *curl*을 사용할 수 있습니다. 예:</span><span class="sxs-lookup"><span data-stu-id="c1648-197">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   <span data-ttu-id="c1648-198">응용 프로그램 로그에 "hello"가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-198">You should see "hello" posted to your application's logs.</span></span> <span data-ttu-id="c1648-199">예: </span><span class="sxs-lookup"><span data-stu-id="c1648-199">For example:</span></span>

   ```shell
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka version : 1.0.2
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka commitId : 2a121f7b1d402825
   [wingtiptoyshub.container-0-C-1] INFO com.wingtiptoys.kafka.KafkaSink - New message received: hello
   ```


> [!NOTE]
> 
> <span data-ttu-id="c1648-200">테스트를 위해 *KafkaSource.java*를 수정하여 다음 예제와 같은 간단한 HTML 양식을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-200">For testing purposes, you could modify your *KafkaSource.java* so that it contains a simple HTML form like the following example:</span></span>
> 
> ```java
> package com.wingtiptoys.kafka;
>    
> import org.springframework.beans.factory.annotation.Autowired;
> import org.springframework.cloud.stream.annotation.EnableBinding;
> import org.springframework.cloud.stream.messaging.Source;
> import org.springframework.messaging.support.GenericMessage;
> import org.springframework.web.bind.annotation.GetMapping;
> import org.springframework.web.bind.annotation.PostMapping;
> import org.springframework.web.bind.annotation.RequestBody;
> import org.springframework.web.bind.annotation.RequestParam;
> import org.springframework.web.bind.annotation.RestController;
> 
> @EnableBinding(Source.class)
> @RestController
> public class KafkaSource {
>   @Autowired
>   private Source source;
> 
>   @GetMapping("/")
>   public String sendForm() {
>     return "<html><body>" +
>       "<form action=\"/messages\" method=\"post\">" +
>       "<input type=\"text\" name=\"text\">" +
>       "<input type=\"submit\">" +
>       "</form></body><html>";
>     }
> 
>   @PostMapping("/messages")
>   public String sendMessage(@RequestBody String message) {
>     this.source.output().send(new GenericMessage<>(message));
>     return message;
>   }
> }
> ```
> 
> <span data-ttu-id="c1648-201">이렇게 하면 웹 브라우저를 사용하여 응용 프로그램을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-201">This will allow you to use a web browser to test your application:</span></span>
> 
> ![웹 브라우저를 사용하여 응용 프로그램 테스트][TB01]
> 
> <span data-ttu-id="c1648-203">폼을 제출할 때 응용 프로그램에 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-203">When you submit the form, your application will display the results:</span></span>
> 
> ![웹 브라우저 내 응용 프로그램 응답][TB02]
> 

## <a name="next-steps"></a><span data-ttu-id="c1648-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c1648-205">Next steps</span></span>

<span data-ttu-id="c1648-206">Event Hub 스트림 바인더 및 Apache Kafka에 대한 Azure 지원에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1648-206">For more information about Azure support for Event Hub Stream Binder and Apache Kafka, see the following articles:</span></span>

* [<span data-ttu-id="c1648-207">Azure Event Hubs 정의</span><span class="sxs-lookup"><span data-stu-id="c1648-207">What is Azure Event Hubs?</span></span>](/azure/event-hubs/event-hubs-about)

* [<span data-ttu-id="c1648-208">Apache Kafka용 Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="c1648-208">Azure Event Hubs for Apache Kafka</span></span>](/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview)

* [<span data-ttu-id="c1648-209">Azure Portal을 사용하여 Event Hubs 네임스페이스 및 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="c1648-209">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>](/azure/event-hubs/event-hubs-create)

* [<span data-ttu-id="c1648-210">Apache Kafka 지원 이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="c1648-210">Create Apache Kafka enabled event hubs</span></span>](/azure/event-hubs/event-hubs-create-kafka-enabled)

<span data-ttu-id="c1648-211">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1648-211">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="c1648-212">**[Spring Framework]** 는 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만드는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-212">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="c1648-213">해당 플랫폼을 기반으로 하여 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 응용 프로그램을 만드는 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-213">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="c1648-214">Spring Boot을 시작하는 개발자를 도우려면 <https://github.com/spring-guides/>에서 몇 가지 샘플 Spring Boot 패키지를 사용할 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-214">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="c1648-215">기본 Spring Boot 프로젝트 목록에서 선택하는 것 외에도 **[Spring Initializr]** 를 통해 사용자 지정 Spring Boot 응용 프로그램을 만들기 시작하는 개발자에게 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c1648-215">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Apache Kafka]: http://kafka.apache.org
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-03.png

[TB01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-01.png
[TB02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-02.png
