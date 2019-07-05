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
# <a name="configure-microprofile-by-using-azure-key-vault"></a>Azure Key Vault를 사용하여 MicroProfile 구성

이 문서에서는 [MicroProfile](http://microprofile.io) 애플리케이션을 구성하여 [Azure 키 자격 증명 모음](https://azure.microsoft.com/services/key-vault/)에서 비밀을 검색하는 방법을 보여줍니다. 이 프로세스에서는 [MicroProfile 구성 API](https://microprofile.io/project/eclipse/microprofile-config)를 사용하여 Azure 키 자격 증명 모음으로의 직접 연결을 만듭니다. MicroProfile Config API를 사용하여 개발자는 구성 데이터를 검색하고 마이크로 서비스에 주입하는 데 있어서의 표준 API의 이점을 누릴 수 있습니다.

시작하기 전에, Azure Key Vault와 MicroProfile Config API의 조합을 통해 우리가 작성할 수 있는 코드를 신속하게 빠르게 살펴보도록 합니다. 다음은 `@Inject` 및 `@ConfigProperty`로 주석 처리 된 클래스 필드의 코드 조각입니다. 주석에 지정된 *이름*은 Azure Key Vault에서 조회할 속성의 이름이고 *defaultValue*는 키가 발견되지 않은 경우 설정되는 것입니다. 결과 키 자격 증명 모음에 저장된 값 또는 기본값이 자동으로 런타임 시 필드에 삽입됩니다. 이 동작은 더 이상 생성자 및 설정 메서드에서 값을 전달할 필요가 없도록 하므로 개발자의 삶을 편리하게 할 수 있습니다. MicroProfile이 대신 이 작업을 처리합니다.

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

필요에 따라 비밀을 요청하기 위해 MicroProfile 구성에 직접 액세스할 수도 있습니다. 예:

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

이 예제 코드에서는 [Payara Micro](https://www.payara.fish/payara_micro) 및 [MicroProfile](https://microprofile.io/)을 사용하여 컴퓨터에서 로컬로 실행할 수 있는 작은 Java 웹 애플리케이션 요구 사항(WAR) 파일을 만듭니다. Azure에 코드를 고정시키거나 푸시하는 방법을 보여주지는 않지만, 이 문서의 끝 부분에 있는 섹션은 이것을 설명하는 다른 유용한 자습서에 대한 링크를 제공합니다.

이 예제에서는 사용자의 키 자격 증명 모음에 대한 구성 소스 (MicroProfile 구성 API 사용)를 생성하는 무료 및 오픈 소스 라이브러리를 사용합니다. [프로젝트 GitHub 페이지](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault)에서 이 라이브러리에 대해 자세히 알아보고 코드를 검토할 수 있습니다. 라이브러리를 사용하는 경우 이 자습서의 코드는 라이브러리 구성에 초점을 맞추고 코드에 키를 주입할 수 있습니다. Azure 관련 코드를 작성할 필요가 없습니다.

키 자격 증명 모음 리소스를 만드는 것으로 시작하여 로컬 시스템에서 이 코드를 실행하려면 다음 섹션의 지침을 따릅니다.

## <a name="create-a-key-vault-resource"></a>키 자격 증명 모음 리소스 만들기

이 섹션에서는, 키 자격 증명 모음 리소스를 만들고 하나의 비밀로 채우기 위해 Azure CLI를 사용합니다.

1. Azure 서비스 주체를 만듭니다. 이 단계에서는 키 자격 증명 모음에 액세스하기 위한 클라이언트 ID 및 키를 제공합니다.

    ```bash
    az login
    az account set --subscription <subscription_id>

    az ad sp create-for-rbac --name <service_principal_name>
    ```

    *microprofile-keyvault-service-principal*을 사용하여 이전 단계의 *\<service_principal_name>* 을 바꾸어 보겠습니다. Azure의 응답은 다음과 유사합니다.

    ```json
    {
      "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
      "displayName": "microprofile-keyvault-service-principal",
      "name": "http://microprofile-keyvault-service-principal",
      "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
      "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
    }
    ```

    여기에서 특히 유의할 점은 *appId* 및 *암호* 값입니다. 이 값들은 문서의 뒷부분에서 *클라이언트 ID* 및 *키*로 사용할 수 있습니다.

1. (선택 사항) 이제 서비스 주체를 생성했으므로, 리소스 그룹을 만들 수 있습니다. 사용하려는 리소스 그룹이 이미 있다면 이 단계를 건너뛰어도 됩니다. 리소스 그룹 위치 목록을 얻으려면 `az account list-locations`를 호출하고 해당 목록의 *이름* 값을 사용하여 리소스 그룹을 작성해야 하는 위치를 지정할 수 있습니다.

    ```bash
    # In this tutorial, "westus" is the resource group location
    # and "jg-test" is the resource group name.
    az group create -l <resource_group_location> -n <resource_group_name>
    ```

1. 키 자격 증명 모음 리소스를 만듭니다. 키 자격 증명 모음 이름을 사용하여 나중에 키 자격 증명 모음을 참조하므로, 기억하기 쉬운 이름을 선택해야 합니다.

    ```bash
    az keyvault create --name <your_keyvault_name>            \
                      --resource-group <your_resource_group> \
                      --location <location>                  \
                      --enabled-for-deployment true          \
                      --enabled-for-disk-encryption true     \
                      --enabled-for-template-deployment true \
                      --sku standard
    ```

1. 앞서 생성한 서비스 주체에 대해 적절한 사용 권한을 부여해야 키 자격 증명 모음 비밀에 액세스할 수 있습니다. 다음 코드의 appId 값은 1단계에서 서비스 주체를 만들었을 때의 *appId* 값입니다. 즉, 1단계의 *appId*는 *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*였지만, 터미널 출력의 해당 값을 사용해야 합니다.

    ```bash
    az keyvault set-policy --name <your_keyvault_name>   \
                          --secret-permission get list  \
                          --spn <your_sp_appId_created_in_step1>
    ```

1. 이제 키 자격 증명 모음에 비밀을 푸시할 수 있습니다. *demo-key* 키 이름을 사용하고 키 값을 *demo-value*로 설정합니다.

    ```bash
    az keyvault secret set --name demo-key      \
                           --value demo-value   \
                           --vault-name <your_keyvault_name>  
    ```

이것으로 끝입니다. 이제 단일 비밀을 사용하여 Azure에서 실행되는 키 자격 증명 모음을 얻었습니다. 이제 이 리포지토리를 복제하고 앱에서 이 리소스를 사용하도록 구성할 수 있습니다.

## <a name="get-up-and-running-locally"></a>시작하여 로컬로 실행

이 예제는 GitHub에서 사용할 수 있는 예제 애플리케이션을 기반으로 하므로, 애플리케이션을 복제한 다음, 코드 단계를 따릅니다. 

1. 다음 명령을 입력하여 컴퓨터에 코드를 복제합니다.

    `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

    `cd microprofile-configsource-keyvault`

1. *src/main/resources/META-INF/microprofile-config.properties*로 이동하고, *microprofile config.properties* 파일에서 이전 단계에서의 값을 사용하여 속성을 변경합니다.

1. `mvn clean package payara-micro:start`를 사용하여 서버를 구동합니다.

1. 웹 브라우저에서 [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config)에 액세스해 보십시오. 키 자격 증명 모음에서 값을 읽는 간단한 응답을 볼 수 있습니다.

## <a name="summary"></a>요약

이 애플리케이션 예제는 MicroProfile 구성 API, Azure Key Vault 및 무료 및 오픈 소스 [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) 라이브러리를 함께 사용하여 MicroProfile 웹 서비스에 구성 데이터와 비밀 정보를 쉽게 주입할 수 있도록 합니다.
