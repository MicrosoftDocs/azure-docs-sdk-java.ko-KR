---
title: Azure Key Vault를 사용하여 MicroProfile 구성
description: Azure Key Vault를 사용하여 MicroProfile 웹 서비스에 비밀을 주입하는 방법 알아보기
services: key-vault
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: c405711813176823f2ddee6b4002f75c2b25fdb5
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533620"
---
# <a name="configure-microprofile-by-using-azure-key-vault"></a><span data-ttu-id="b74a5-103">Azure Key Vault를 사용하여 MicroProfile 구성</span><span class="sxs-lookup"><span data-stu-id="b74a5-103">Configure MicroProfile by using Azure Key Vault</span></span>

<span data-ttu-id="b74a5-104">이 문서에서는 [MicroProfile](http://microprofile.io) 애플리케이션을 구성하여 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/)에서 비밀을 검색하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-104">This article demonstrates how to configure a [MicroProfile](http://microprofile.io) application to retrieve secrets from an [Azure key vault](https://azure.microsoft.com/services/key-vault/).</span></span> <span data-ttu-id="b74a5-105">이 프로세스에서는 [MicroProfile 구성 API](https://microprofile.io/project/eclipse/microprofile-config)를 사용하여 Azure 키 자격 증명 모음으로의 직접 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-105">In this process, you use the [MicroProfile Config APIs](https://microprofile.io/project/eclipse/microprofile-config) to create a direct connection to an Azure key vault.</span></span> <span data-ttu-id="b74a5-106">MicroProfile Config API를 사용하여 개발자는 구성 데이터를 검색하고 마이크로 서비스에 주입하는 데 있어서의 표준 API의 이점을 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-106">As a developer, by using the MicroProfile Config APIs, you benefit from a standard API for retrieving and injecting configuration data into their microservices.</span></span>

<span data-ttu-id="b74a5-107">시작하기 전에, Azure Key Vault와 MicroProfile Config API의 조합을 통해 우리가 작성할 수 있는 코드를 신속하게 빠르게 살펴보도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-107">Before you start, take a quick look at what a combination of Azure Key Vault and the MicroProfile Config API enables you to write in your code.</span></span> <span data-ttu-id="b74a5-108">다음은 `@Inject` 및 `@ConfigProperty`로 주석 처리 된 클래스 필드의 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-108">The following code snippet is of a field in a class that's annotated with `@Inject` and `@ConfigProperty`.</span></span> <span data-ttu-id="b74a5-109">주석에 지정된 *이름*은 Azure Key Vault에서 조회할 속성의 이름이고 *defaultValue*는 키가 발견되지 않은 경우 설정되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-109">The *name* that's specified in the annotation is the name of the property to look up in your key vault, and the *defaultValue* is what will be set if the key is not discovered.</span></span> <span data-ttu-id="b74a5-110">결과 키 자격 증명 모음에 저장된 값 또는 기본값이 자동으로 런타임 시 필드에 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-110">The result is that the value that's stored in the key vault, or the default value, is injected automatically into the field at runtime.</span></span> <span data-ttu-id="b74a5-111">이 동작은 더 이상 생성자 및 설정 메서드에서 값을 전달할 필요가 없도록 하므로 개발자의 삶을 편리하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-111">This action can simplify your life, because you no longer need to pass values around in constructors and setter methods.</span></span> <span data-ttu-id="b74a5-112">MicroProfile이 대신 이 작업을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-112">Instead, MicroProfile handles this task.</span></span>

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

<span data-ttu-id="b74a5-113">필요에 따라 비밀을 요청하기 위해 MicroProfile 구성에 직접 액세스할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-113">To request secrets, as necessary, you can also access the MicroProfile config directly.</span></span> <span data-ttu-id="b74a5-114">예:</span><span class="sxs-lookup"><span data-stu-id="b74a5-114">For example:</span></span>

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

<span data-ttu-id="b74a5-115">이 예제 코드에서는 [Payara Micro](https://www.payara.fish/payara_micro) 및 [MicroProfile](https://microprofile.io/)을 사용하여 컴퓨터에서 로컬로 실행할 수 있는 작은 Java 웹 애플리케이션 요구 사항(WAR) 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-115">This sample code uses [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile](https://microprofile.io/) to create a tiny Java web application requirement (WAR) file that you can run locally on your machine.</span></span> <span data-ttu-id="b74a5-116">Azure에 코드를 고정시키거나 푸시하는 방법을 보여주지는 않지만, 이 문서의 끝 부분에 있는 섹션은 이것을 설명하는 다른 유용한 자습서에 대한 링크를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-116">It doesn't demonstrate how to Dockerize or push the code to Azure, but the section at the end of this article has links to other useful tutorials that explain this.</span></span>

<span data-ttu-id="b74a5-117">이 예제에서는 사용자의 키 자격 증명 모음에 대한 구성 소스 (MicroProfile 구성 API 사용)를 생성하는 무료 및 오픈 소스 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-117">The sample uses a free and open source library that creates a config source (using the MicroProfile Config API) in your key vault.</span></span> <span data-ttu-id="b74a5-118">[프로젝트 GitHub 페이지](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault)에서 이 라이브러리에 대해 자세히 알아보고 코드를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-118">To learn more about this library and review the code, see the [project GitHub page](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span></span> <span data-ttu-id="b74a5-119">라이브러리를 사용하는 경우 이 자습서의 코드는 라이브러리 구성에 초점을 맞추고 코드에 키를 주입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-119">If you use the library, the code in this tutorial can simply focus on the configuration of the library and then inject keys into your code.</span></span> <span data-ttu-id="b74a5-120">Azure 관련 코드를 작성할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-120">You don't need to write any Azure-specific code.</span></span>

<span data-ttu-id="b74a5-121">키 자격 증명 모음 리소스를 만드는 것으로 시작하여 로컬 시스템에서 이 코드를 실행하려면 다음 섹션의 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-121">To run this code on your local machine, starting with creating a key vault resource, follow the instructions in the next sections.</span></span>

## <a name="create-a-key-vault-resource"></a><span data-ttu-id="b74a5-122">키 자격 증명 모음 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="b74a5-122">Create a key vault resource</span></span>

<span data-ttu-id="b74a5-123">이 섹션에서는, 키 자격 증명 모음 리소스를 만들고 하나의 비밀로 채우기 위해 Azure CLI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-123">In this section, you use the Azure CLI to create a key vault resource and populate it with one secret.</span></span>

1. <span data-ttu-id="b74a5-124">Azure 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-124">Create an Azure service principal.</span></span> <span data-ttu-id="b74a5-125">이 단계에서는 키 자격 증명 모음에 액세스하기 위한 클라이언트 ID 및 키를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-125">This step gives you the client ID and key that you need to access your key vault:</span></span>

    ```bash
    az login
    az account set --subscription <subscription_id>

    az ad sp create-for-rbac --name <service_principal_name>
    ```

    <span data-ttu-id="b74a5-126">*microprofile-keyvault-service-principal*을 사용하여 이전 단계의 *\<service_principal_name>* 을 바꾸어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-126">Let's use *microprofile-keyvault-service-principal* to replace *\<service_principal_name>* in the preceding step.</span></span> <span data-ttu-id="b74a5-127">Azure의 응답은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-127">The response from Azure would be similar to the following:</span></span>

    ```json
    {
      "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
      "displayName": "microprofile-keyvault-service-principal",
      "name": "http://microprofile-keyvault-service-principal",
      "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
      "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
    }
    ```

    <span data-ttu-id="b74a5-128">여기에서 특히 유의할 점은 *appId* 및 *암호* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-128">Of particular note here are the *appId* and *password* values.</span></span> <span data-ttu-id="b74a5-129">이 값들은 문서의 뒷부분에서 *클라이언트 ID* 및 *키*로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-129">You'll use them later in this article as *client ID* and *key*.</span></span>

1. <span data-ttu-id="b74a5-130">(선택 사항) 이제 서비스 주체를 생성했으므로, 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-130">(Optional) Now that you've created a service principal, you can create a resource group.</span></span> <span data-ttu-id="b74a5-131">사용하려는 리소스 그룹이 이미 있다면 이 단계를 건너뛰어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-131">If you already have a resource group that you want to use, you can skip this step.</span></span> <span data-ttu-id="b74a5-132">리소스 그룹 위치 목록을 얻으려면 `az account list-locations`를 호출하고 해당 목록의 *이름* 값을 사용하여 리소스 그룹을 작성해야 하는 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-132">To get a list of resource group locations, you can call `az account list-locations` and use the *name* value from that list to specify where the resource group should be created.</span></span>

    ```bash
    # In this tutorial, "westus" is the resource group location
    # and "jg-test" is the resource group name.
    az group create -l <resource_group_location> -n <resource_group_name>
    ```

1. <span data-ttu-id="b74a5-133">키 자격 증명 모음 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-133">Create a key vault resource.</span></span> <span data-ttu-id="b74a5-134">키 자격 증명 모음 이름을 사용하여 나중에 키 자격 증명 모음을 참조하므로, 기억하기 쉬운 이름을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-134">You'll use your key vault name to refer to the key vault later, so be sure to choose a memorable name.</span></span>

    ```bash
    az keyvault create --name <your_keyvault_name>            \
                      --resource-group <your_resource_group> \
                      --location <location>                  \
                      --enabled-for-deployment true          \
                      --enabled-for-disk-encryption true     \
                      --enabled-for-template-deployment true \
                      --sku standard
    ```

1. <span data-ttu-id="b74a5-135">앞서 생성한 서비스 주체에 대해 적절한 사용 권한을 부여해야 키 자격 증명 모음 비밀에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-135">Grant the appropriate permissions to the service principal that you created earlier, so that it can access the key vault secrets.</span></span> <span data-ttu-id="b74a5-136">다음 코드의 appId 값은 1단계에서 서비스 주체를 만들었을 때의 *appId* 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-136">The appId value in the following code is the *appId* value from step 1, where you created the service principal.</span></span> <span data-ttu-id="b74a5-137">즉, 1단계의 *appId*는 *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*였지만, 터미널 출력의 해당 값을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-137">That is, the *appId* in step 1 was *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, but you should use the value from your own terminal output.</span></span>

    ```bash
    az keyvault set-policy --name <your_keyvault_name>   \
                          --secret-permission get list  \
                          --spn <your_sp_appId_created_in_step1>
    ```

1. <span data-ttu-id="b74a5-138">이제 키 자격 증명 모음에 비밀을 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-138">Now you can push a secret into your key vault.</span></span> <span data-ttu-id="b74a5-139">*demo-key* 키 이름을 사용하고 키 값을 *demo-value*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-139">Use the key name *demo-key*, and set the value of the key to *demo-value*:</span></span>

    ```bash
    az keyvault secret set --name demo-key      \
                           --value demo-value   \
                           --vault-name <your_keyvault_name>  
    ```

<span data-ttu-id="b74a5-140">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-140">That's it!</span></span> <span data-ttu-id="b74a5-141">이제 단일 비밀을 사용하여 Azure에서 실행되는 키 자격 증명 모음을 얻었습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-141">You now have a key vault running in Azure with a single secret.</span></span> <span data-ttu-id="b74a5-142">이제 이 리포지토리를 복제하고 앱에서 이 리소스를 사용하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-142">You can now clone this repo and configure it to use this resource in your app.</span></span>

## <a name="get-up-and-running-locally"></a><span data-ttu-id="b74a5-143">시작하여 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="b74a5-143">Get up and running locally</span></span>

<span data-ttu-id="b74a5-144">이 예제는 GitHub에서 사용할 수 있는 예제 애플리케이션을 기반으로 하므로, 애플리케이션을 복제한 다음, 코드 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-144">This example is based on a sample application that's available on GitHub, so you'll clone that application and then step through the code.</span></span> 

1. <span data-ttu-id="b74a5-145">다음 명령을 입력하여 컴퓨터에 코드를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-145">Clone the code onto your machine by entering the following commands:</span></span>

    `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

    `cd microprofile-configsource-keyvault`

1. <span data-ttu-id="b74a5-146">*src/main/resources/META-INF/microprofile-config.properties*로 이동하고, *microprofile config.properties* 파일에서 이전 단계에서의 값을 사용하여 속성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-146">Go to *src/main/resources/META-INF/microprofile-config.properties*, and then change the properties in the *microprofile-config.properties* file by using the values from the previous steps.</span></span>

1. <span data-ttu-id="b74a5-147">`mvn clean package payara-micro:start`를 사용하여 서버를 구동합니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-147">Try running the server by using `mvn clean package payara-micro:start`.</span></span>

1. <span data-ttu-id="b74a5-148">웹 브라우저에서 [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config)에 액세스해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="b74a5-148">Try accessing [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) in your web browser.</span></span> <span data-ttu-id="b74a5-149">키 자격 증명 모음에서 값을 읽는 간단한 응답을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-149">You should see a simple response that demonstrates values that are being read from your key vault.</span></span>

## <a name="summary"></a><span data-ttu-id="b74a5-150">요약</span><span class="sxs-lookup"><span data-stu-id="b74a5-150">Summary</span></span>

<span data-ttu-id="b74a5-151">이 애플리케이션 예제는 MicroProfile 구성 API, Azure Key Vault 및 무료 및 오픈 소스 [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) 라이브러리를 함께 사용하여 MicroProfile 웹 서비스에 구성 데이터와 비밀 정보를 쉽게 주입할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b74a5-151">This sample application combines the MicroProfile Config API, Azure Key Vault, and the free and open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) library to enable easy injection of configuration data and secrets into your MicroProfile web services.</span></span>
