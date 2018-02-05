---
title: "Azure Key Vault에 Spring Boot Starter를 사용하는 방법"
description: "Azure Key Vault 스타터에 Spring Boot Initializer 앱을 구성하는 방법을 알아봅니다."
services: key-vault
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/29/2017
ms.author: robmcm
ms.openlocfilehash: 165a108147ef5ef7575820bbb6c2ee526888f722
ms.sourcegitcommit: 558d875e9a255deb5b83b3f1646bd1dd9eee0a0d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a><span data-ttu-id="e05ce-103">Azure Key Vault에 Spring Boot Starter를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="e05ce-103">How to use the Spring Boot Starter for Azure Key Vault</span></span>

## <a name="overview"></a><span data-ttu-id="e05ce-104">개요</span><span class="sxs-lookup"><span data-stu-id="e05ce-104">Overview</span></span>

<span data-ttu-id="e05ce-105">이 문서에서는 **[Spring Initializr]**를 사용하여 앱을 만드는 방법을 보여 줍니다. 여기서는 Spring Boot Starter를 Azure Key Vault에 사용하여 키 자격 증명 모음에 비밀 형태로 저장된 연결 문자열을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-105">This article demonstrates creating an app with the **[Spring Initializr]** which uses the Spring Boot Starter for Azure Key Vault to retrieve a connection string that is stored as a secret in a key vault.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e05ce-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e05ce-106">Prerequisites</span></span>

<span data-ttu-id="e05ce-107">이 문서의 단계를 수행하기 위해 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="e05ce-108">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정{]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="e05ce-109">[JDK(Java Development Kit)](http://www.oracle.com/technetwork/java/javase/downloads/), 버전 1.7 이상</span><span class="sxs-lookup"><span data-stu-id="e05ce-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="e05ce-110">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="e05ce-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-the-spring-initialzr"></a><span data-ttu-id="e05ce-111">Spring Initialzr를 사용하여 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="e05ce-111">Create an app using the Spring Initialzr</span></span>

1. <span data-ttu-id="e05ce-112"><https://start.spring.io/>로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="e05ce-113">**Java**에서 **Maven** 프로젝트를 생성한다고 지정하고, 응용 프로그램에 대한 **그룹** 및 **아티팩트** 이름을 입력한 다음 Spring Initializr의 **정식 버전으로 전환**하는 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![그룹 및 아티팩트 이름 지정][secrets-01]

1. <span data-ttu-id="e05ce-115">**Azure** 섹션까지 아래로 스크롤하고 **Azure Key Vault**의 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-115">Scroll down to the **Azure** section and check the box for **Azure Key Vault**.</span></span>

   ![Azure Key Vault 스타터 선택][secrets-02]

1. <span data-ttu-id="e05ce-117">페이지 하단까지 스크롤하고 버튼을 클릭하여 **프로젝트를 생성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-117">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Spring Boot 프로젝트 생성][secrets-03]

1. <span data-ttu-id="e05ce-119">메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-119">When prompted, download the project to a path on your local computer.</span></span>

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a><span data-ttu-id="e05ce-120">Azure에 로그인하고 사용할 구독 선택</span><span class="sxs-lookup"><span data-stu-id="e05ce-120">Sign into Azure and select the subscription to use</span></span>

1. <span data-ttu-id="e05ce-121">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-121">Open a command prompt.</span></span>

1. <span data-ttu-id="e05ce-122">Azure CLI를 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-122">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="e05ce-123">지시에 따라 로그인 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-123">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="e05ce-124">구독 나열:</span><span class="sxs-lookup"><span data-stu-id="e05ce-124">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="e05ce-125">Azure가 구독 목록을 반환하며 사용하려는 구독의 GUID를 복사해야 합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-125">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="e05ce-126">다음 예제처럼 Azure에 사용하려는 계정의 GUID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-126">Specify the GUID for the account you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-and-configure-a-new-azure-key-vault-using-the-azure-cli"></a><span data-ttu-id="e05ce-127">Azure CLI를 사용하여 새 Azure Key Vault 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="e05ce-127">Create and configure a new Azure Key Vault using the Azure CLI</span></span>

1. <span data-ttu-id="e05ce-128">다음 예제처럼 키 자격 증명 모음에사용할 Azure 리소스에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-128">Create a resource group for the Azure resources you will use for your key vault; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="e05ce-129">위치:</span><span class="sxs-lookup"><span data-stu-id="e05ce-129">Where:</span></span>
   | <span data-ttu-id="e05ce-130">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e05ce-130">Parameter</span></span> | <span data-ttu-id="e05ce-131">설명</span><span class="sxs-lookup"><span data-stu-id="e05ce-131">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="e05ce-132">리소스 그룹의 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-132">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="e05ce-133">리소스 그룹을 호스팅할 [Azure 지역](https://azure.microsoft.com/regions/)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-133">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="e05ce-134">Azure CLI가 다음 에제처럼 리소스 그룹 만들기 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-134">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

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

1. <span data-ttu-id="e05ce-135">응용 프로그램 등록에서 Azure 서비스 주체를 만듭니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-135">Create an Azure service principal from your application registration; for example:</span></span>
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   | <span data-ttu-id="e05ce-136">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e05ce-136">Parameter</span></span> | <span data-ttu-id="e05ce-137">설명</span><span class="sxs-lookup"><span data-stu-id="e05ce-137">Description</span></span> |
   |---|---|
   | `id` | <span data-ttu-id="e05ce-138">앞의 응용 프로그램 등록에서 GUID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-138">Specifies the GUID from your application registration earlier.</span></span> |

   <span data-ttu-id="e05ce-139">Azure CLI 가 *appId* 및 *암호*가 포함된 JSON 상태 메시지를 반환합니다. 이 항목은 나중에 클라이언트 ID와 클라이언트 암호로 사용됩니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-139">The Azure CLI will return a JSON status message that contains the *appId* and *password*, which you will use later as the client id and client password; for example:</span></span>

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

1. <span data-ttu-id="e05ce-140">리소스 그룹에서 새 키 자격 증명 모음을 만듭니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-140">Create a new key vault in the resource group; for example:</span></span>
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   <span data-ttu-id="e05ce-141">위치:</span><span class="sxs-lookup"><span data-stu-id="e05ce-141">Where:</span></span>
   | <span data-ttu-id="e05ce-142">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e05ce-142">Parameter</span></span> | <span data-ttu-id="e05ce-143">설명</span><span class="sxs-lookup"><span data-stu-id="e05ce-143">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="e05ce-144">키 자격 증명 모음의 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-144">Specifies a unique name for your key vault.</span></span> |
   | `location` | <span data-ttu-id="e05ce-145">리소스 그룹을 호스팅할 [Azure 지역](https://azure.microsoft.com/regions/)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-145">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |
   | `enabled-for-deployment` | <span data-ttu-id="e05ce-146">[키 자격 증명 모음 배포 옵션](https://docs.microsoft.com/en-us/cli/azure/keyvault)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-146">Specifies the [key vault deployment option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `enabled-for-disk-encryption` | <span data-ttu-id="e05ce-147">[키 자격 증명 모음 암호화 옵션](https://docs.microsoft.com/en-us/cli/azure/keyvault)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-147">Specifies the [key vault encryption option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `enabled-for-template-deployment` | <span data-ttu-id="e05ce-148">[키 자격 증명 모음 암호화 옵션](https://docs.microsoft.com/en-us/cli/azure/keyvault)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-148">Specifies the [key vault encryption option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `sku` | <span data-ttu-id="e05ce-149">[키 자격 증명 모음 SKU 옵션](https://docs.microsoft.com/en-us/cli/azure/keyvault)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-149">Specifies the [key vault SKU option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `query` | <span data-ttu-id="e05ce-150">이 자습서를 완료하는 데 필요한 키 자격 증명 모은 URI인 값을 응답에서 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-150">Specifies a value to retrieve from the response, which is the key vault URI that you will need to complete this tutorial.</span></span> |

   <span data-ttu-id="e05ce-151">Azure CLI가 나중에 사용하게 되는 키 자격 증명 모음의 URI를 표시합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-151">The Azure CLI will display the URI for key vault, which you will use later; for example:</span></span>  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

1. <span data-ttu-id="e05ce-152">앞서 만든 Azure 서비스 주체의 액세스 정책을 설정합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-152">Set the access policy for the Azure service principal you created earlier; for example:</span></span>
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   <span data-ttu-id="e05ce-153">위치:</span><span class="sxs-lookup"><span data-stu-id="e05ce-153">Where:</span></span>
   | <span data-ttu-id="e05ce-154">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e05ce-154">Parameter</span></span> | <span data-ttu-id="e05ce-155">설명</span><span class="sxs-lookup"><span data-stu-id="e05ce-155">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="e05ce-156">앞의 키 자격 증명 모음 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-156">Specifies your key vault name from earlier.</span></span> |
   | `secret-permission` | <span data-ttu-id="e05ce-157">키 자격 증명 모음에 대해 [보안 정책](https://docs.microsoft.com/en-us/cli/azure/keyvault)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-157">Specifies the [security policies](https://docs.microsoft.com/en-us/cli/azure/keyvault) for your key vault.</span></span> |
   | `object-id` | <span data-ttu-id="e05ce-158">앞의 응용 프로그램 등록에서 GUID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-158">Specifies the GUID for your application registration from earlier.</span></span> |

   <span data-ttu-id="e05ce-159">Azure CLI가 다음 예제처럼 보안 정책 만들기 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-159">The Azure CLI will display the results of your security policy creation; for example:</span></span>  

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

1. <span data-ttu-id="e05ce-160">새 키 자격 증명 모음에 비밀을 저장합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-160">Store a secret in your new key vault; for example:</span></span>
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   <span data-ttu-id="e05ce-161">위치:</span><span class="sxs-lookup"><span data-stu-id="e05ce-161">Where:</span></span>
   | <span data-ttu-id="e05ce-162">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e05ce-162">Parameter</span></span> | <span data-ttu-id="e05ce-163">설명</span><span class="sxs-lookup"><span data-stu-id="e05ce-163">Description</span></span> |
   |---|---|
   | `vault-name` | <span data-ttu-id="e05ce-164">앞의 키 자격 증명 모음 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-164">Specifies your key vault name from earlier.</span></span> |
   | `name` | <span data-ttu-id="e05ce-165">비밀 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-165">Specifies the name of your secret.</span></span> |
   | `value` | <span data-ttu-id="e05ce-166">비밀 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-166">Specifies the value of your secret.</span></span> |

   <span data-ttu-id="e05ce-167">Azure CLI가 다음 예제처럼 비밀 만들기 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-167">The Azure CLI will display the results of your secret creation; for example:</span></span>  

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

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="e05ce-168">Spring Boot 응용 프로그램 구성 및 컴파일</span><span class="sxs-lookup"><span data-stu-id="e05ce-168">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="e05ce-169">앞서 디렉터리에 다운로드한 Spring Boot 프로젝트 아카이브 파일에서 파일을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-169">Extract the files from the Spring Boot project archive files that you downloaded earlier into a directory.</span></span>

1. <span data-ttu-id="e05ce-170">프로젝트에서 *src/main/resources* 폴더로 이동하고 텍스트 편집기에서 *application.properties* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-170">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="e05ce-171">이 자습서의 앞부분에서 완료한 단계의 값을 사용하여 키 자격 증명 모음의 값을 추가합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-171">Add the values for your key vault using values from the steps that you completed earlier in this tutorial; for example:</span></span>
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   <span data-ttu-id="e05ce-172">위치:</span><span class="sxs-lookup"><span data-stu-id="e05ce-172">Where:</span></span>
   | <span data-ttu-id="e05ce-173">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e05ce-173">Parameter</span></span> | <span data-ttu-id="e05ce-174">설명</span><span class="sxs-lookup"><span data-stu-id="e05ce-174">Description</span></span> |
   |---|---|
   | `azure.keyvault.uri` | <span data-ttu-id="e05ce-175">키 자격 증명 모음을 만든 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-175">Specifies the URI from when you created your key vault.</span></span> |
   | `azure.keyvault.client-id` | <span data-ttu-id="e05ce-176">서비스 주체를 만들 때 *appId* GUID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-176">Specifies the *appId* GUID from when you created your service principal.</span></span> |
   | `azure.keyvault.client-key` | <span data-ttu-id="e05ce-177">서비스 주체를 만들 때 *암호* GUID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-177">Specifies the *password* GUID from when you created your service principal.</span></span> |

1. <span data-ttu-id="e05ce-178">프로젝트의 기본 소스 코드 파일로 이동합니다. 예를 들어 */src/main/java/com/wingtiptoys/secrets*입니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-178">Navigate to the main source code file of your project; for example: */src/main/java/com/wingtiptoys/secrets*.</span></span>

1. <span data-ttu-id="e05ce-179">텍스트 편집기의 파일에서 *SecretsApplication.java* 같은 응용 프로그램의 기본 Java 파일을 열고 다음 줄을 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-179">Open the application's main Java file in a file in a text editor; for example: *SecretsApplication.java*, and add the following lines to the file:</span></span>

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
   <span data-ttu-id="e05ce-180">이 코드 예제는 키 자격 증명 모음에서 연결 문자열을 검색하고 명령줄에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-180">This code example retrieves the connection string from the key vault and displays it to the command line.</span></span>

1. <span data-ttu-id="e05ce-181">Java 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-181">Save and close the Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="e05ce-182">앱 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="e05ce-182">Build and test your app</span></span>

1. <span data-ttu-id="e05ce-183">Spring Boot 앱에 대한 *pom.xml* 파일이 있는 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-183">Navigate to the directory where the *pom.xml* file for your Spring Boot app is located:</span></span>

1. <span data-ttu-id="e05ce-184">Maven을 사용하여 Spring Boot 응용 프로그램을 빌드합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-184">Build your Spring Boot application with Maven; for example:</span></span>

   ```bash
   mvn clean package
   ```

   <span data-ttu-id="e05ce-185">Maven이 빌드의 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-185">Maven will display the results of your build.</span></span>

   ![Spring Boot 응용 프로그램 빌드 상태][build-application-01]

1. <span data-ttu-id="e05ce-187">Maven에서 Spring Boot 응용 프로그램을 실행합니다. 응용 프로그램이 키 자격 증명 모음의 연결 문자열을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e05ce-187">Run your Spring Boot application with Maven; the application will display the connection string from your key vault.</span></span> <span data-ttu-id="e05ce-188">예: </span><span class="sxs-lookup"><span data-stu-id="e05ce-188">For example:</span></span>

   ```bash
   mvn spring-boot:run
   ```

   ![Spring Boot 런타임 메시지][build-application-02]

## <a name="next-steps"></a><span data-ttu-id="e05ce-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e05ce-190">Next steps</span></span>

<span data-ttu-id="e05ce-191">Azure Key Vaults를 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e05ce-191">For more information about using Azure Key Vaults, see the following articles:</span></span>

* <span data-ttu-id="e05ce-192">[Key Vault 설명서].</span><span class="sxs-lookup"><span data-stu-id="e05ce-192">[Key Vault Documentation].</span></span>

* <span data-ttu-id="e05ce-193">[Azure Key Vault 시작]</span><span class="sxs-lookup"><span data-stu-id="e05ce-193">[Get started with Azure Key Vault]</span></span>

<span data-ttu-id="e05ce-194">Azure에서 Spring Boot 응용 프로그램을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e05ce-194">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="e05ce-195">Azure App Service에 Spring Boot 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="e05ce-195">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="e05ce-196">Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="e05ce-196">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="e05ce-197">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e05ce-197">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Key Vault 설명서]: /azure/key-vault/
[Azure Key Vault 시작]: /azure/key-vault/key-vault-get-started
[Java 개발자용 Azure]: https://docs.microsoft.com/java/azure/
[체험판 Azure 계정{]: https://azure.microsoft.com/pricing/free-trial/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[secrets-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-01.png
[secrets-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-02.png
[secrets-03]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-03.png

[build-application-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-01.png
[build-application-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-02.png
