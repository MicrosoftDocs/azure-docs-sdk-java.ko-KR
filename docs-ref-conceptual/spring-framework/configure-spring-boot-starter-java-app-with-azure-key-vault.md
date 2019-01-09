---
title: Azure Key Vault에 Spring Boot Starter를 사용하는 방법
description: Azure Key Vault 스타터에 Spring Boot Initializer 앱을 구성하는 방법을 알아봅니다.
services: key-vault
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 78dadcf93bfc57ab669271495393fa9ba164c89d
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991367"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a><span data-ttu-id="12062-103">Azure Key Vault에 Spring Boot Starter를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="12062-103">How to use the Spring Boot Starter for Azure Key Vault</span></span>

## <a name="overview"></a><span data-ttu-id="12062-104">개요</span><span class="sxs-lookup"><span data-stu-id="12062-104">Overview</span></span>

<span data-ttu-id="12062-105">이 문서에서는 **[Spring Initializr]** 를 사용하여 앱을 만드는 방법을 보여 줍니다. 여기서는 Spring Boot Starter를 Azure Key Vault에 사용하여 키 자격 증명 모음에 비밀 형태로 저장된 연결 문자열을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Key Vault to retrieve a connection string that is stored as a secret in a key vault.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12062-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="12062-106">Prerequisites</span></span>

<span data-ttu-id="12062-107">이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="12062-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12062-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="12062-109">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="12062-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="12062-110">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12062-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="12062-111">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="12062-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="12062-112">Spring Initialzr를 사용하여 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="12062-112">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="12062-113"><https://start.spring.io/>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-113">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="12062-114">**Java**에서 **Maven** 프로젝트를 생성한다고 지정하고, 애플리케이션에 대한 **그룹** 및 **아티팩트** 이름을 입력한 다음 Spring Initializr의 **정식 버전으로 전환**하는 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-114">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![그룹 및 아티팩트 이름 지정][secrets-01]

1. <span data-ttu-id="12062-116">**Azure** 섹션까지 아래로 스크롤하고 **Azure Key Vault**의 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-116">Scroll down to the **Azure** section and check the box for **Azure Key Vault**.</span></span>

   ![Azure Key Vault 스타터 선택][secrets-02]

1. <span data-ttu-id="12062-118">페이지 하단까지 스크롤하고 버튼을 클릭하여 **프로젝트를 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-118">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Spring Boot 프로젝트 생성][secrets-03]

1. <span data-ttu-id="12062-120">메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-120">When prompted, download the project to a path on your local computer.</span></span>

## <a name="sign-into-azure"></a><span data-ttu-id="12062-121">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="12062-121">Sign into Azure</span></span>

1. <span data-ttu-id="12062-122">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="12062-122">Open a command prompt.</span></span>

1. <span data-ttu-id="12062-123">Azure CLI를 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-123">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="12062-124">지시에 따라 로그인 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-124">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="12062-125">구독 나열:</span><span class="sxs-lookup"><span data-stu-id="12062-125">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="12062-126">Azure가 구독 목록을 반환하며 사용하려는 구독의 GUID를 복사해야 합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12062-126">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="12062-127">다음 예제처럼 Azure에 사용하려는 계정의 GUID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-127">Specify the GUID for the account you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-a-new-azure-key-vault"></a><span data-ttu-id="12062-128">새 Azure Key Vault 만들기</span><span class="sxs-lookup"><span data-stu-id="12062-128">Create a new Azure Key Vault</span></span>

1. <span data-ttu-id="12062-129">다음 예제처럼 키 자격 증명 모음에사용할 Azure 리소스에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12062-129">Create a resource group for the Azure resources you will use for your key vault; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="12062-130">위치:</span><span class="sxs-lookup"><span data-stu-id="12062-130">Where:</span></span>

   | <span data-ttu-id="12062-131">매개 변수</span><span class="sxs-lookup"><span data-stu-id="12062-131">Parameter</span></span> | <span data-ttu-id="12062-132">설명</span><span class="sxs-lookup"><span data-stu-id="12062-132">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="12062-133">리소스 그룹의 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-133">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="12062-134">리소스 그룹을 호스팅할 [Azure 지역](https://azure.microsoft.com/regions/)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-134">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="12062-135">Azure CLI가 다음 에제처럼 리소스 그룹 만들기 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-135">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

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

2. <span data-ttu-id="12062-136">애플리케이션 등록에서 Azure 서비스 주체를 만듭니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12062-136">Create an Azure service principal from your application registration; for example:</span></span>
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   <span data-ttu-id="12062-137">위치:</span><span class="sxs-lookup"><span data-stu-id="12062-137">Where:</span></span>

   | <span data-ttu-id="12062-138">매개 변수</span><span class="sxs-lookup"><span data-stu-id="12062-138">Parameter</span></span> | <span data-ttu-id="12062-139">설명</span><span class="sxs-lookup"><span data-stu-id="12062-139">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="12062-140">Azure 서비스 주체에 대한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-140">Specifies the name for your Azure service principal.</span></span> |

   <span data-ttu-id="12062-141">Azure CLI 가 *appId* 및 *암호*가 포함된 JSON 상태 메시지를 반환합니다. 이 항목은 나중에 클라이언트 ID와 클라이언트 암호로 사용됩니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12062-141">The Azure CLI will return a JSON status message that contains the *appId* and *password*, which you will use later as the client id and client password; for example:</span></span>

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

3. <span data-ttu-id="12062-142">리소스 그룹에서 새 키 자격 증명 모음을 만듭니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12062-142">Create a new key vault in the resource group; for example:</span></span>
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   <span data-ttu-id="12062-143">위치:</span><span class="sxs-lookup"><span data-stu-id="12062-143">Where:</span></span>

   | <span data-ttu-id="12062-144">매개 변수</span><span class="sxs-lookup"><span data-stu-id="12062-144">Parameter</span></span> | <span data-ttu-id="12062-145">설명</span><span class="sxs-lookup"><span data-stu-id="12062-145">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="12062-146">키 자격 증명 모음의 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-146">Specifies a unique name for your key vault.</span></span> |
   | `location` | <span data-ttu-id="12062-147">리소스 그룹을 호스팅할 [Azure 지역](https://azure.microsoft.com/regions/)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-147">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |
   | `enabled-for-deployment` | <span data-ttu-id="12062-148">[키 자격 증명 모음 배포 옵션](/cli/azure/keyvault)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-148">Specifies the [key vault deployment option](/cli/azure/keyvault).</span></span> |
   | `enabled-for-disk-encryption` | <span data-ttu-id="12062-149">[키 자격 증명 모음 암호화 옵션](/cli/azure/keyvault)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-149">Specifies the [key vault encryption option](/cli/azure/keyvault).</span></span> |
   | `enabled-for-template-deployment` | <span data-ttu-id="12062-150">[키 자격 증명 모음 암호화 옵션](/cli/azure/keyvault)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-150">Specifies the [key vault encryption option](/cli/azure/keyvault).</span></span> |
   | `sku` | <span data-ttu-id="12062-151">[키 자격 증명 모음 SKU 옵션](/cli/azure/keyvault)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-151">Specifies the [key vault SKU option](/cli/azure/keyvault).</span></span> |
   | `query` | <span data-ttu-id="12062-152">이 자습서를 완료하는 데 필요한 키 자격 증명 모은 URI인 값을 응답에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-152">Specifies a value to retrieve from the response, which is the key vault URI that you will need to complete this tutorial.</span></span> |

   <span data-ttu-id="12062-153">Azure CLI가 나중에 사용하게 되는 키 자격 증명 모음의 URI를 표시합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12062-153">The Azure CLI will display the URI for key vault, which you will use later; for example:</span></span>  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

4. <span data-ttu-id="12062-154">앞서 만든 Azure 서비스 주체의 액세스 정책을 설정합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12062-154">Set the access policy for the Azure service principal you created earlier; for example:</span></span>
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   <span data-ttu-id="12062-155">위치:</span><span class="sxs-lookup"><span data-stu-id="12062-155">Where:</span></span>

   | <span data-ttu-id="12062-156">매개 변수</span><span class="sxs-lookup"><span data-stu-id="12062-156">Parameter</span></span> | <span data-ttu-id="12062-157">설명</span><span class="sxs-lookup"><span data-stu-id="12062-157">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="12062-158">앞의 키 자격 증명 모음 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-158">Specifies your key vault name from earlier.</span></span> |
   | `secret-permission` | <span data-ttu-id="12062-159">키 자격 증명 모음에 대해 [보안 정책](/cli/azure/keyvault)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-159">Specifies the [security policies](/cli/azure/keyvault) for your key vault.</span></span> |
   | `spn` | <span data-ttu-id="12062-160">앞의 애플리케이션 등록에서 GUID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-160">Specifies the GUID for your application registration from earlier.</span></span> |

   <span data-ttu-id="12062-161">Azure CLI가 다음 예제처럼 보안 정책 만들기 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-161">The Azure CLI will display the results of your security policy creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "location": "westus",
     "name": "wingtiptoyskeyvault",
     "properties": {
       ...
       ... (A long list of values will be displayed here.)
       ...
     },
     "resourceGroup": "wingtiptoysresources",
     "tags": {},
     "type": "Microsoft.KeyVault/vaults"
   }
   ```

5. <span data-ttu-id="12062-162">새 키 자격 증명 모음에 비밀을 저장합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12062-162">Store a secret in your new key vault; for example:</span></span>
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   <span data-ttu-id="12062-163">위치:</span><span class="sxs-lookup"><span data-stu-id="12062-163">Where:</span></span>

   | <span data-ttu-id="12062-164">매개 변수</span><span class="sxs-lookup"><span data-stu-id="12062-164">Parameter</span></span> | <span data-ttu-id="12062-165">설명</span><span class="sxs-lookup"><span data-stu-id="12062-165">Description</span></span> |
   |---|---|
   | `vault-name` | <span data-ttu-id="12062-166">앞의 키 자격 증명 모음 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-166">Specifies your key vault name from earlier.</span></span> |
   | `name` | <span data-ttu-id="12062-167">비밀 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-167">Specifies the name of your secret.</span></span> |
   | `value` | <span data-ttu-id="12062-168">비밀 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-168">Specifies the value of your secret.</span></span> |

   <span data-ttu-id="12062-169">Azure CLI가 다음 예제처럼 비밀 만들기 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-169">The Azure CLI will display the results of your secret creation; for example:</span></span>  

   ```json
   {
     "attributes": {
       "created": "2017-12-01T09:00:16+00:00",
       "enabled": true,
       "expires": null,
       "notBefore": null,
       "recoveryLevel": "Purgeable",
       "updated": "2017-12-01T09:00:16+00:00"
     },
     "contentType": null,
     "id": "https://wingtiptoyskeyvault.vault.azure.net/secrets/connectionString/123456789abcdef123456789abcdef",
     "kid": null,
     "managed": null,
     "tags": {
       "file-encoding": "utf-8"
     },
     "value": "jdbc:sqlserver://wingtiptoys.database.windows.net:1433;database=DATABASE;"
   }
   ```

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="12062-170">앱 구성 및 컴파일</span><span class="sxs-lookup"><span data-stu-id="12062-170">Configure and compile your app</span></span>

1. <span data-ttu-id="12062-171">앞서 디렉터리에 다운로드한 Spring Boot 프로젝트 아카이브 파일에서 파일을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-171">Extract the files from the Spring Boot project archive files that you downloaded earlier into a directory.</span></span>

2. <span data-ttu-id="12062-172">프로젝트에서 *src/main/resources* 폴더로 이동하고 텍스트 편집기에서 *application.properties* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="12062-172">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

3. <span data-ttu-id="12062-173">이 자습서의 앞부분에서 완료한 단계의 값을 사용하여 키 자격 증명 모음의 값을 추가합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12062-173">Add the values for your key vault using values from the steps that you completed earlier in this tutorial; for example:</span></span>
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   <span data-ttu-id="12062-174">위치:</span><span class="sxs-lookup"><span data-stu-id="12062-174">Where:</span></span>

   |          <span data-ttu-id="12062-175">매개 변수</span><span class="sxs-lookup"><span data-stu-id="12062-175">Parameter</span></span>          |                                 <span data-ttu-id="12062-176">설명</span><span class="sxs-lookup"><span data-stu-id="12062-176">Description</span></span>                                 |
   |-----------------------------|-----------------------------------------------------------------------------|
   |    `azure.keyvault.uri`     |           <span data-ttu-id="12062-177">키 자격 증명 모음을 만든 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-177">Specifies the URI from when you created your key vault.</span></span>           |
   | `azure.keyvault.client-id`  |  <span data-ttu-id="12062-178">서비스 주체를 만들 때 *appId* GUID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-178">Specifies the *appId* GUID from when you created your service principal.</span></span>   |
   | `azure.keyvault.client-key` | <span data-ttu-id="12062-179">서비스 주체를 만들 때 *암호* GUID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-179">Specifies the *password* GUID from when you created your service principal.</span></span> |


4. <span data-ttu-id="12062-180">프로젝트의 기본 소스 코드 파일로 이동합니다. 예를 들어 */src/main/java/com/wingtiptoys/secrets*입니다.</span><span class="sxs-lookup"><span data-stu-id="12062-180">Navigate to the main source code file of your project; for example: */src/main/java/com/wingtiptoys/secrets*.</span></span>

5. <span data-ttu-id="12062-181">텍스트 편집기에서 애플리케이션의 메인 Java 파일(예: *SecretsApplication.java*)을 열어 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-181">Open the application's main Java file in a file in a text editor; for example: *SecretsApplication.java*, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.secrets;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class SecretsApplication implements CommandLineRunner {

      @Value("${connectionString}")
      private String connectionString;

      public static void main(String[] args) {
         SpringApplication.run(SecretsApplication.class, args);
      }

      public void run(String... varl) throws Exception {
         System.out.println(String.format("\nConnection String stored in Azure Key Vault:\n%s\n",connectionString));
      }
   }
   ```
   <span data-ttu-id="12062-182">이 코드 예제는 키 자격 증명 모음에서 연결 문자열을 검색하고 명령줄에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-182">This code example retrieves the connection string from the key vault and displays it to the command line.</span></span>

6. <span data-ttu-id="12062-183">Java 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="12062-183">Save and close the Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="12062-184">앱 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="12062-184">Build and test your app</span></span>

1. <span data-ttu-id="12062-185">Spring Boot 앱에 대한 *pom.xml* 파일이 있는 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-185">Navigate to the directory where the *pom.xml* file for your Spring Boot app is located:</span></span>

1. <span data-ttu-id="12062-186">Maven을 사용하여 Spring Boot 애플리케이션을 빌드합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="12062-186">Build your Spring Boot application with Maven; for example:</span></span>

   ```bash
   mvn clean package
   ```

   <span data-ttu-id="12062-187">Maven이 빌드의 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-187">Maven will display the results of your build.</span></span>

   ![Spring Boot 애플리케이션 빌드 상태][build-application-01]

1. <span data-ttu-id="12062-189">Maven에서 Spring Boot 애플리케이션을 실행합니다. 애플리케이션이 키 자격 증명 모음의 연결 문자열을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-189">Run your Spring Boot application with Maven; the application will display the connection string from your key vault.</span></span> <span data-ttu-id="12062-190">예: </span><span class="sxs-lookup"><span data-stu-id="12062-190">For example:</span></span>

   ```bash
   mvn spring-boot:run
   ```

   ![Spring Boot 런타임 메시지][build-application-02]

## <a name="summary"></a><span data-ttu-id="12062-192">요약</span><span class="sxs-lookup"><span data-stu-id="12062-192">Summary</span></span>

<span data-ttu-id="12062-193">이 자습서에서는 **[Spring Initializr]** 를 사용하여 새 Java 웹 애플리케이션을 만들었으며, 민감한 정보를 저장하기 위해 Azure Key Vault를 만들었고 Azure Key Vault를 통해 정보를 검색하도록 애플리케이션을 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="12062-193">In this tutorial, you created a new Java web application using the **[Spring Initializr]**, created an Azure Key Vault to store sensitive information, and then configured your application to retrieve information from your key vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12062-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="12062-194">Next steps</span></span>

<span data-ttu-id="12062-195">Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="12062-195">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="12062-196">Azure의 Spring</span><span class="sxs-lookup"><span data-stu-id="12062-196">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="12062-197">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="12062-197">Additional Resources</span></span>

<span data-ttu-id="12062-198">Azure Key Vaults를 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12062-198">For more information about using Azure Key Vaults, see the following articles:</span></span>

* <span data-ttu-id="12062-199">[Key Vault 설명서].</span><span class="sxs-lookup"><span data-stu-id="12062-199">[Key Vault Documentation].</span></span>

* <span data-ttu-id="12062-200">[Azure Key Vault 시작]</span><span class="sxs-lookup"><span data-stu-id="12062-200">[Get started with Azure Key Vault]</span></span>

<span data-ttu-id="12062-201">Azure에서 Spring Boot 애플리케이션을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12062-201">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="12062-202">Azure App Service에 Spring Boot 애플리케이션 배포</span><span class="sxs-lookup"><span data-stu-id="12062-202">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="12062-203">Azure Container Service의 Kubernetes 클러스터에 Spring Boot 애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="12062-203">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="12062-204">Java와 함께 Azure를 사용하는 방법에 관한 자세한 정보는 [Java 개발자용 Azure]와 [Azure DevOps 및 Java 사용하기]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12062-204">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<!-- URL List -->

[Key Vault 설명서]: /azure/key-vault/
[Key Vault Documentation]: /azure/key-vault/
[Azure Key Vault 시작]: /azure/key-vault/key-vault-get-started
[Get started with Azure Key Vault]: /azure/key-vault/key-vault-get-started
[Java 개발자용 Azure]: /java/azure/
[Azure for Java Developers]: /java/azure/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Azure DevOps 및 Java 사용하기]: /azure/devops/
[Working with Azure DevOps and Java]: /azure/devops/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[secrets-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-01.png
[secrets-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-02.png
[secrets-03]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-03.png

[build-application-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-01.png
[build-application-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-02.png
