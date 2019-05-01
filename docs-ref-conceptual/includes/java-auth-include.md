---
ms.openlocfilehash: 0a9b06932baa51c3cf003a4485a3a25261ffe91d
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592513"
---
<span data-ttu-id="841c4-101">[인증 파일](../java-sdk-azure-authenticate.md#mgmt-file)을 만들고 명령줄에서 파일의 전체 경로가 포함된 `AZURE_AUTH_LOCATION` 환경 변수를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="841c4-101">Create an [authentication file](../java-sdk-azure-authenticate.md#mgmt-file) and export an environment variable `AZURE_AUTH_LOCATION` on the command line with the full path to the file.</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azure.auth
```

<span data-ttu-id="841c4-102">인증 파일은 Azure 리소스를 정의, 생성 및 구성하기 위해 관리 라이브러리에서 사용되는 `Azure` 진입점 개체를 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="841c4-102">The authentication file is used to configure the entry point `Azure` object used by the management libraries to define, create, and configure Azure resources.</span></span>

```java
// pull in the location of the security file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```

<span data-ttu-id="841c4-103">Java용 Azure 관리 라이브러리를 사용하는 경우 인증 옵션에 대해 [자세히 알아보세요](../java-sdk-azure-authenticate.md#mgmt-auth).</span><span class="sxs-lookup"><span data-stu-id="841c4-103">[Learn more](../java-sdk-azure-authenticate.md#mgmt-auth) about authentication options when using the Azure management libraries for Java.</span></span>