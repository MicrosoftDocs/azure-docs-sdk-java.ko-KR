---
title: Azure Key Vault에 Spring Boot Starter를 사용하는 방법
description: Azure Key Vault 스타터에 Spring Boot Initializer 앱을 구성하는 방법을 알아봅니다.
services: key-vault
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: a2734fc08f2f59f64ba6c6c20ff18d75070b68d5
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090716"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a>Azure Key Vault에 Spring Boot Starter를 사용하는 방법

## <a name="overview"></a>개요

이 문서에서는 **[Spring Initializr]** 를 사용하여 앱을 만드는 방법을 보여 줍니다. 여기서는 Spring Boot Starter를 Azure Key Vault에 사용하여 키 자격 증명 모음에 비밀 형태로 저장된 연결 문자열을 검색합니다.

## <a name="prerequisites"></a>필수 조건

이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.
* [JDK(Java Development Kit)](http://www.oracle.com/technetwork/java/javase/downloads/), 버전 1.7 이상
* [Apache Maven](http://maven.apache.org/), 버전 3.0 이상

## <a name="create-an-app-using-the-spring-initialzr"></a>Spring Initialzr를 사용하여 앱 만들기

1. <https://start.spring.io/>로 이동합니다.

1. **Java**에서 **Maven** 프로젝트를 생성한다고 지정하고, 응용 프로그램에 대한 **그룹** 및 **아티팩트** 이름을 입력한 다음 Spring Initializr의 **정식 버전으로 전환**하는 링크를 클릭합니다.

   ![그룹 및 아티팩트 이름 지정][secrets-01]

1. **Azure** 섹션까지 아래로 스크롤하고 **Azure Key Vault**의 확인란을 선택합니다.

   ![Azure Key Vault 스타터 선택][secrets-02]

1. 페이지 하단까지 스크롤하고 버튼을 클릭하여 **프로젝트를 생성**합니다.

   ![Spring Boot 프로젝트 생성][secrets-03]

1. 메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a>Azure에 로그인하고 사용할 구독 선택

1. 명령 프롬프트를 엽니다.

1. Azure CLI를 사용하여 Azure 계정에 로그인합니다.

   ```azurecli
   az login
   ```
   지시에 따라 로그인 프로세스를 완료합니다.

1. 구독 나열:

   ```azurecli
   az account list
   ```
   Azure가 구독 목록을 반환하며 사용하려는 구독의 GUID를 복사해야 합니다. 예를 들어 다음과 같습니다.

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

1. 다음 예제처럼 Azure에 사용하려는 계정의 GUID를 지정합니다.

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-and-configure-a-new-azure-key-vault-using-the-azure-cli"></a>Azure CLI를 사용하여 새 Azure Key Vault 만들기 및 구성

1. 다음 예제처럼 키 자격 증명 모음에사용할 Azure 리소스에 대한 리소스 그룹을 만듭니다.
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   위치:

   | 매개 변수 | 설명 |
   |---|---|
   | `name` | 리소스 그룹의 고유한 이름을 지정합니다. |
   | `location` | 리소스 그룹을 호스팅할 [Azure 지역](https://azure.microsoft.com/regions/)을 지정합니다. |

   Azure CLI가 다음 에제처럼 리소스 그룹 만들기 결과를 표시합니다.  

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

2. 응용 프로그램 등록에서 Azure 서비스 주체를 만듭니다. 예를 들어 다음과 같습니다.
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   위치:

   | 매개 변수 | 설명 |
   |---|---|
   | `name` | Azure 서비스 주체에 대한 이름을 지정합니다. |

   Azure CLI 가 *appId* 및 *암호*가 포함된 JSON 상태 메시지를 반환합니다. 이 항목은 나중에 클라이언트 ID와 클라이언트 암호로 사용됩니다. 예를 들어 다음과 같습니다.

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

3. 리소스 그룹에서 새 키 자격 증명 모음을 만듭니다. 예를 들어 다음과 같습니다.
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   위치:

   | 매개 변수 | 설명 |
   |---|---|
   | `name` | 키 자격 증명 모음의 고유한 이름을 지정합니다. |
   | `location` | 리소스 그룹을 호스팅할 [Azure 지역](https://azure.microsoft.com/regions/)을 지정합니다. |
   | `enabled-for-deployment` | [키 자격 증명 모음 배포 옵션](https://docs.microsoft.com/en-us/cli/azure/keyvault)을 지정합니다. |
   | `enabled-for-disk-encryption` | [키 자격 증명 모음 암호화 옵션](https://docs.microsoft.com/en-us/cli/azure/keyvault)을 지정합니다. |
   | `enabled-for-template-deployment` | [키 자격 증명 모음 암호화 옵션](https://docs.microsoft.com/en-us/cli/azure/keyvault)을 지정합니다. |
   | `sku` | [키 자격 증명 모음 SKU 옵션](https://docs.microsoft.com/en-us/cli/azure/keyvault)을 지정합니다. |
   | `query` | 이 자습서를 완료하는 데 필요한 키 자격 증명 모은 URI인 값을 응답에서 검색합니다. |

   Azure CLI가 나중에 사용하게 되는 키 자격 증명 모음의 URI를 표시합니다. 예를 들어 다음과 같습니다.  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

4. 앞서 만든 Azure 서비스 주체의 액세스 정책을 설정합니다. 예를 들어 다음과 같습니다.
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   위치:

   | 매개 변수 | 설명 |
   |---|---|
   | `name` | 앞의 키 자격 증명 모음 이름을 지정합니다. |
   | `secret-permission` | 키 자격 증명 모음에 대해 [보안 정책](https://docs.microsoft.com/en-us/cli/azure/keyvault)을 지정합니다. |
   | `spn` | 앞의 응용 프로그램 등록에서 GUID를 지정합니다. |

   Azure CLI가 다음 예제처럼 보안 정책 만들기 결과를 표시합니다.  

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

5. 새 키 자격 증명 모음에 비밀을 저장합니다. 예를 들어 다음과 같습니다.
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   위치:

   | 매개 변수 | 설명 |
   |---|---|
   | `vault-name` | 앞의 키 자격 증명 모음 이름을 지정합니다. |
   | `name` | 비밀 이름을 지정합니다. |
   | `value` | 비밀 값을 지정합니다. |

   Azure CLI가 다음 예제처럼 비밀 만들기 결과를 표시합니다.  

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

## <a name="configure-and-compile-your-spring-boot-application"></a>Spring Boot 응용 프로그램 구성 및 컴파일

1. 앞서 디렉터리에 다운로드한 Spring Boot 프로젝트 아카이브 파일에서 파일을 추출합니다.

2. 프로젝트에서 *src/main/resources* 폴더로 이동하고 텍스트 편집기에서 *application.properties* 파일을 엽니다.

3. 이 자습서의 앞부분에서 완료한 단계의 값을 사용하여 키 자격 증명 모음의 값을 추가합니다. 예를 들어 다음과 같습니다.
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   위치:

   |          매개 변수          |                                 설명                                 |
   |-----------------------------|-----------------------------------------------------------------------------|
   |    `azure.keyvault.uri`     |           키 자격 증명 모음을 만든 URI를 지정합니다.           |
   | `azure.keyvault.client-id`  |  서비스 주체를 만들 때 *appId* GUID를 지정합니다.   |
   | `azure.keyvault.client-key` | 서비스 주체를 만들 때 *암호* GUID를 지정합니다. |


4. 프로젝트의 기본 소스 코드 파일로 이동합니다. 예를 들어 */src/main/java/com/wingtiptoys/secrets*입니다.

5. 텍스트 편집기의 파일에서 *SecretsApplication.java* 같은 응용 프로그램의 기본 Java 파일을 열고 다음 줄을 파일에 추가합니다.

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
   이 코드 예제는 키 자격 증명 모음에서 연결 문자열을 검색하고 명령줄에 표시합니다.

6. Java 파일을 저장하고 닫습니다.

## <a name="build-and-test-your-app"></a>앱 빌드 및 테스트

1. Spring Boot 앱에 대한 *pom.xml* 파일이 있는 디렉터리로 이동합니다.

1. Maven을 사용하여 Spring Boot 응용 프로그램을 빌드합니다. 예를 들어 다음과 같습니다.

   ```bash
   mvn clean package
   ```

   Maven이 빌드의 결과를 표시합니다.

   ![Spring Boot 응용 프로그램 빌드 상태][build-application-01]

1. Maven에서 Spring Boot 응용 프로그램을 실행합니다. 응용 프로그램이 키 자격 증명 모음의 연결 문자열을 표시합니다. 예: 

   ```bash
   mvn spring-boot:run
   ```

   ![Spring Boot 런타임 메시지][build-application-02]

## <a name="next-steps"></a>다음 단계

Azure Key Vaults를 사용하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Key Vault 설명서].

* [Azure Key Vault 시작]

Azure에서 Spring Boot 응용 프로그램을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Azure App Service에 Spring Boot 응용 프로그램 배포](deploy-spring-boot-java-web-app-on-azure.md)

* [Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 실행](deploy-spring-boot-java-app-on-kubernetes.md)

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.

<!-- URL List -->

[Key Vault 설명서]: /azure/key-vault/
[Azure Key Vault 시작]: /azure/key-vault/key-vault-get-started
[Java 개발자용 Azure]: https://docs.microsoft.com/java/azure/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
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
