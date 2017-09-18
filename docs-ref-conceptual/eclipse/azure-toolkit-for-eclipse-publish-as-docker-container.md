---
title: "Eclipse용 Azure 도구 키트를 사용하여 Docker 컨테이너 게시"
description: "Eclipse용 Azure 도구 키트를 사용하여 Docker 컨테이너로 Microsoft Azure에 웹앱을 게시하는 방법을 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 4f074e2ca6f4c623fc4c7ef1df818a8b3ef5e451
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Eclipse용 Azure 도구 키트를 사용하여 웹앱을 Docker 컨테이너로 게시

Docker 컨테이너는 웹 응용 프로그램을 배포하는 데 널리 사용되는 방법입니다. 개발자는 Docker 컨테이너를 통해 모든 프로젝트 파일과 종속성을 서버에 배포할 단일 패키지로 통합할 수 있습니다. Eclipse용 Azure 도구 키트는 Microsoft Azure에 배포를 위한 *Docker 컨테이너로 게시* 기능을 추가함으로써 Java 개발자들을 위해 이 프로세스를 간소화합니다. 이 문서에서는 Azure에 응용 프로그램을 Docker 컨테이너로 게시하는 데 필요한 단계를 안내합니다.

> [!NOTE]
> Docker에 대한 자세한 내용은 [Docker 웹 사이트]를 참조하세요.
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Docker 컨테이너를 사용하여 Azure에 웹앱 게시

1. Eclipse의 웹앱 프로젝트를 엽니다.

1. **Docker 컨테이너로 게시**를 시작하려면 다음 방법 중 하나를 사용하세요.

   * **탐색기** 보기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**를 클릭한 다음 **Docker 컨테이너로 게시**를 클릭합니다.

      ![탐색기 보기 Docker 컨테이너 명령으로 게시][PUB01]

   * Eclipse 도구 모음에서 **게시** 단추를 클릭한 다음 **Docker 컨테이너로 게시**를 클릭합니다.

      ![Eclipse 도구 모음 Docker 컨테이너 명령으로 게시][PUB02]
      
   **Azure에 Docker 컨테이너 배포** 마법사가 열립니다.

   ![Azure에 Docker 컨테이너 배포 마법사][PUB03]

1. **이미지 이름 입력, 아티팩트의 경로 선택 및 사용할 Docker 호스트 확인** 창에서 다음을 수행합니다.

   a. **Docker 이미지 이름** 상자에서 Docker 호스트에 사용할 고유한 이름을 입력합니다. (마법사에서 이름을 자동으로 만들지만 사용자가 수정할 수 있습니다.)

   b. **호스트** 영역에 사용자가 이미 만든 Docker 호스트가 표시됩니다. 다음 중 하나를 수행합니다.

   * 기존 Docker 호스트가 있는 경우 웹앱을 해당 호스트에 배포할 수 있습니다.
   * 새 Docker 호스트를 만들려면 **추가**를 클릭합니다.  
      
      **Docker 호스트 만들기** 대화 상자가 열립니다.

   ![Azure에 Docker 컨테이너 배포 마법사][PUB04a]

1. **새 가상 컴퓨터 구성** 창에서 Docker 호스트에 대한 다음 옵션을 지정합니다. (마법사에서 대부분의 옵션을 자동으로 생성하지만 사용자가 수정할 수 있습니다.)

   a. **이름**: Docker 호스트의 고유 이름을 입력합니다. (이전에 지정한 Docker 이미지 이름과 다릅니다.)

   b. **구독**: 호스트에 사용하는 Azure 구독을 입력합니다.

   c. **지역**: 호스트가 배치될 지리적 지역을 입력합니다.

   d. **호스트 OS 및 크기** 탭에서 다음을 수행합니다. 
   * **호스트 OS**: 호스트를 포함할 가상 컴퓨터의 운영 체제를 입력합니다.
   * **크기**: 호스트의 가상 컴퓨터 크기를 입력합니다.

   e. **리소스 그룹** 탭에서 다음을 수행합니다. 
   * **새 리소스 그룹**: 호스트에 사용할 새 리소스 그룹을 만듭니다.
   * **기존 리소스 그룹**: Azure 계정에서 기존 리소스 그룹을 입력합니다.

   f. **네트워크** 탭에서 다음을 수행합니다. 
   * **새 가상 네트워크**: 호스트에 사용할 새 가상 네트워크를 만듭니다.
   * **기존 가상 네트워크**: Azure 계정에서 기존 가상 네트워크를 입력합니다.

   g. **저장소** 탭에서 다음을 수행합니다. 
   * **새 저장소 계정**: 호스트에 사용할 새 저장소 계정을 만듭니다.
   * **기존 저장소 계정**: Azure 계정에서 기존 저장소 계정을 입력합니다.

1. **다음**을 누릅니다.

1. **로그인 자격 증명 및 포트 설정 구성** 창에서 다음 옵션 중 하나를 선택합니다.

   * **Azure Key Vault에서 자격 증명 가져오기**: Azure 구독에 저장되어 있는 이전에 저장한 자격 증명 집합을 지정합니다. 

   >[!NOTE]
   >특정 계정 또는 서비스 주체로 만든 Azure Key Vault는 구독을 공유하는 다른 계정 또는 서비스 주체에서 자동으로 액세스할 수 없습니다. 다른 계정 또는 서비스 주체가 Key Vault를 사용하도록 허용하려면 Azure Portal을 사용하여 계정 또는 서비스 주체를 추가해야 합니다.
   >

   * **새 로그인 자격 증명**: 새 로그인 자격 증명 집합을 만듭니다. 이 옵션을 선택하는 경우 다음을 수행합니다. 
    
      * **VM 자격 증명** 탭에서 Docker 호스트의 가상 컴퓨터 로그인 자격 증명에 대해 다음 옵션 중 하나를 선택합니다. 

         * **사용자 이름**: 가상 컴퓨터 로그인 자격 증명의 사용자 이름을 지정합니다. 
         * **암호** 및 **확인**: 가상 컴퓨터 로그인 자격 증명에 사용할 암호를 입력합니다. 
         * **SSH**: Docker 호스트에 사용할 SSH(Secure Shell) 설정을 입력합니다. 다음 옵션 중에서 선택할 수 있습니다. 
            * **없음**: 가상 컴퓨터에서 SSH 연결을 허용하지 않게 지정합니다. 
            * **자동 생성**: SSH를 통해 연결하는 데 필요한 설정을 자동으로 만듭니다. 
            * **디렉터리에서 가져오기**: 이전에 저장된 SSH 설정 집합을 포함하는 디렉터리를 지정합니다. 디렉터리에 다음 두 파일이 포함되어야 합니다. 
               * *id_rsa*: 사용자의 RSA ID가 포함됩니다. 
               * *id_rsa.pub*: 인증에 사용되는 RSA 공개 키를 포함합니다. 
        
         ![Docker 호스트 만들기][PUB05]

      * **Docker 디먼 자격 증명** 탭에서 다음 옵션을 지정합니다. 

         * **Docker 디먼 포트**: Docker 호스트의 고유한 TCP 포트를 입력합니다. 
         * **TLS 보안**: Docker 호스트의 전송 계층 보안 설정을 입력합니다. 다음 옵션 중에서 선택할 수 있습니다. 
            * **없음**: 가상 컴퓨터에서 TLS 연결을 허용하지 않게 지정합니다. 
            * **자동 생성**: TLS를 통해 연결하는 데 필요한 설정을 자동으로 만듭니다. 
            * **디렉터리에서 가져오기**: 이전에 저장된 TLS 설정 집합을 포함하는 디렉터리를 지정합니다. 구체적으로 말하면 디렉터리에 다음 6개의 파일이 포함되어야 합니다. 
               * *ca.pem* 및 *ca-key.pem*: TLS 인증 기관의 인증서와 공개 키가 포함되어 있습니다. 
               * *cert.pem* 및 *key.pem*: TLS 인증에 사용할 클라이언트 인증서와 공개 키가 포함되어 있습니다. 
               * *server.pem* 및 *server-key.pem*: 호스트의 서버 인증서와 공개 키가 포함되어 있습니다. 

         ![Docker 호스트 만들기][PUB06]

1. 이전 정보를 모두 입력한 후 **마침**을 클릭합니다.

1. **Azure에 Docker 컨테이너 배포** 마법사에서 **다음**을 클릭합니다.

   ![Azure에 Docker 컨테이너 배포 마법사][PUB07]

1. **만들 Docker 컨테이너 구성** 창에서 다음을 수행합니다.

   a. **Docker 컨테이너 이름** 상자에서 Docker 컨테이너에 사용할 고유한 이름을 입력합니다.

   b. 다음 Docker 이미지 중 하나를 선택합니다. 

      * **미리 정의된 Docker 이미지**: Azure에서 기존 Docker 이미지를 지정합니다. 

      >[!NOTE]
      >이 상자의 Docker 이미지 목록은 Azure 도구 키트가 패치하도록 구성된 여러 이미지로 구성되어 있어 아티팩트가 자동으로 배포됩니다.
      >

      * **사용자 지정 Dockerfile**: 로컬 컴퓨터에서 이전에 저장된 Dockerfile을 지정합니다.

      >[!NOTE]
      >고유 Dockerfile을 배포하려는 개발자를 위한 고급 기능입니다. 그러나 이 기능은 Dockerfile을 올바르게 빌드하기 위해 이 옵션을 사용하는 개발자에 따라 달라집니다. Azure 도구 키트는 사용자 지정 Dockerfile에 있는 콘텐츠의 유효성을 검사하지 않으므로, Dockerfile에 문제가 있으면 배포에 실패할 수 있습니다. 또한 Azure 도구 키트에서는 사용자 지정 Dockerfile에 웹앱 아티팩트가 포함되어야 하므로 HTTP 연결을 열려고 시도합니다. 개발자가 다른 아티팩트 형식을 게시하는 경우 배포 후에 무해한 오류가 표시될 수도 있습니다.
      >

   c. **포트 설정**: Docker 컨테이너에 사용할 고유한 TCP 포트 바인딩을 입력합니다.

      ![만들 Docker 컨테이너 구성 창][PUB08]

1. 앞의 단계를 모두 완료한 후 **마침**을 클릭합니다.

Azure 도구 키트가 Docker 컨테이너에서 Azure에 웹앱을 배포하기 시작합니다. 

## <a name="next-steps"></a>다음 단계

Docker의 추가 리소스는 공식 [Docker 웹 사이트]를 참조하세요.

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Docker 웹 사이트]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png