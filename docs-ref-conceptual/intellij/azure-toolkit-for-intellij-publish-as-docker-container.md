---
title: "IntelliJ용 Azure 도구 키트를 사용하여 Docker 컨테이너 게시"
description: "IntelliJ용 Azure 도구 키트를 사용하여 Docker 컨테이너로 Microsoft Azure에 웹앱을 게시하는 방법을 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: f92040b34b9897d9feea8d2ec5e8748e75fff7f7
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>IntelliJ용 Azure 도구 키트를 사용하여 웹앱을 Docker 컨테이너로 게시

Docker 컨테이너는 웹 응용 프로그램을 배포하는 데 널리 사용되는 방법입니다. 개발자는 Docker 컨테이너를 통해 모든 프로젝트 파일과 종속성을 서버에 배포할 단일 패키지로 통합할 수 있습니다. IntelliJ용 Azure 도구 키트는 Microsoft Azure에 배포를 위한 *Docker 컨테이너로 게시* 기능을 추가함으로써 Java 개발자들을 위해 이 프로세스를 간소화합니다. 이 문서에서는 Azure에 응용 프로그램을 Docker 컨테이너로 게시하는 데 필요한 단계를 안내합니다.

> [!NOTE]
>
> Docker에 대한 자세한 내용은 [Docker 웹 사이트]를 참조하세요.
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Docker 컨테이너를 사용하여 Azure에 웹앱 게시

> [!NOTE]
> * 웹앱을 게시하려면 배포 준비된 아티팩트를 만들어야 합니다. 자세한 내용은 [아티팩트 만들기에 대한 추가 정보](#artifacts) 섹션을 참조하세요.
>
> * 배포 마법사를 한 번 이상 완료한 후 마법사를 다시 실행하는 경우 사용자 설정의 대부분은 기본값으로 사용됩니다.
>

1. IntelliJ의 웹앱 프로젝트를 엽니다.

2. **Docker 컨테이너로 게시**를 시작하려면 다음 방법 중 하나를 사용하세요.

   * **프로젝트** 도구 창에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**를 클릭한 다음 **Docker 컨테이너로 게시**를 클릭합니다.

      ![Docker 컨테이너 명령으로 게시][PUB01]

   * IntelliJ 도구 모음에서 **그룹 게시** 단추를 클릭한 다음 **Docker 컨테이너로 게시**를 클릭합니다.

      ![Docker 컨테이너 명령으로 게시][PUB02]  
    **Azure에 Docker 컨테이너 배포** 마법사가 열립니다.

   ![Azure에 Docker 컨테이너 배포 마법사][PUB03]

3. **이미지 이름 입력, 아티팩트의 경로 선택 및 사용할 Docker 호스트 확인** 창에서 다음을 수행합니다. 

   a. **Docker 이미지 이름** 상자에서 Docker 호스트에 사용할 고유한 이름을 입력합니다. (마법사에서 이름을 자동으로 만들지만 사용자가 수정할 수 있습니다.) 

   나. **호스트** 영역에 사용자가 이미 만든 Docker 호스트가 표시됩니다. 다음 중 하나를 수행합니다. 
      * 기존 Docker 호스트가 있는 경우 웹앱을 해당 호스트에 배포할 수 있습니다.
      * Docker 호스트를 만들려면 녹색 더하기 기호(**+**)를 클릭합니다.  
       **Docker 호스트 만들기** 대화 상자가 열립니다. 

      ![Azure에 Docker 컨테이너 배포 마법사][PUB04a]

4. **새 가상 머신 구성** 창에서 Docker 호스트에 대한 다음 정보를 제공합니다. (마법사에서 대부분의 정보를 자동으로 생성하지만 사용자가 수정할 수 있습니다.) 

   a. **이름** 상자에서 Docker 호스트에 사용할 고유한 이름을 입력합니다. (이전에 지정한 Docker 이미지 이름과 다릅니다.) 
    
   나. **구독** 상자에서 호스트에 사용하는 Azure 구독을 입력합니다. 
      
   다. **지역** 상자에서 호스트가 배치될 지리적 지역을 입력합니다.
      
   d. **OS 및 크기** 탭에서 다음을 수행합니다.      
      * **호스트 OS**: 호스트를 포함할 가상 머신의 운영 체제를 입력합니다. 
      * **크기**: 호스트의 가상 컴퓨터 크기를 입력합니다.   
       
   e. **리소스 그룹** 탭에서 다음 중 하나를 선택합니다.      
      * **새 리소스 그룹**: 호스트에 사용할 리소스 그룹을 만듭니다.
      * **기존 리소스 그룹**: Azure 계정에서 기존 리소스 그룹을 지정합니다. 
       
   f. **네트워크** 탭에서 다음 중 하나를 선택합니다.      
      * **새 가상 네트워크**: 호스트에 사용할 가상 네트워크를 만듭니다.
      * **기존 가상 네트워크**: Azure 계정에서 기존 가상 네트워크를 지정합니다. 
       
   g. **저장소** 탭에서 다음 중 하나를 선택합니다.      
      * **새 저장소 계정**: 호스트에 사용할 저장소 계정을 만듭니다.
      * **기존 저장소 계정**: Azure 계정에서 기존 저장소 계정을 지정합니다.
       
5. **다음**을 클릭합니다.  
     **로그인 자격 증명 및 포트 설정 구성** 창이 열립니다.

      ![로그인 자격 증명 및 포트 설정 구성 창][PUB05]

6. 다음 옵션 중 하나를 선택합니다.

      * **Azure Key Vault에서 자격 증명 가져오기**: Azure 구독에 저장되어 있는 이전에 저장한 자격 증명 집합을 지정합니다.

          > [!NOTE]
          > 특정 계정 또는 서비스 주체로 만든 Azure Key Vault는 구독을 공유하는 다른 계정 또는 서비스 주체에서 자동으로 액세스할 수 없습니다. 다른 계정 또는 서비스 주체가 Key Vault를 사용하도록 허용하려면 Azure Portal을 사용하여 계정 또는 서비스 주체를 추가해야 합니다.

      * **새 로그인 자격 증명**: 새 로그인 자격 증명 집합을 만듭니다. 이 옵션을 선택하는 경우 다음을 수행합니다.

        a. **VM 자격 증명** 탭에서 Docker 호스트의 가상 컴퓨터 로그인 자격 증명에 대한 다음 정보를 제공합니다. * **Username**: 가상 컴퓨터 로그인 자격 증명에 대한 사용자 이름을 입력합니다.
             * **암호** 및 **확인**: 가상 컴퓨터 로그인 자격 증명에 사용할 암호를 입력합니다.
             * **SSH**: Docker 호스트에 사용할 SSH(Secure Shell) 설정을 입력합니다. 다음 옵션 중 하나를 선택할 수 있습니다. * **None**: 가상 머신이 SSH 연결을 허용하지 않도록 지정합니다.
                * **자동 생성**: SSH를 통해 연결하는 데 필요한 설정을 자동으로 만듭니다.
                * **디렉터리에서 가져오기**: 이전에 저장된 SSH 설정 집합을 포함하는 디렉터리를 지정할 수 있습니다. 디렉터리에 다음 두 파일이 포함되어야 합니다.
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        나. **Docker 데몬 액세스** 탭에서 다음 정보를 제공합니다.

          ![Docker 호스트 만들기][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. 필요한 정보를 입력한 후 **마침**을 클릭합니다.  
    **Azure에 Docker 컨테이너 배포** 마법사가 다시 나타납니다.

   ![Azure에 Docker 컨테이너 배포 마법사][PUB07]

8. **다음**을 클릭합니다.  
    **만들 Docker 컨테이너 구성** 창이 열립니다.

   ![만들 Docker 컨테이너 구성 창][PUB08]

9. **만들 Docker 컨테이너를 구성** 창에서 다음 정보를 제공합니다. 

   a. **Docker 컨테이너 이름** 상자에서 Docker 컨테이너에 사용할 고유한 이름을 입력합니다.

   나. 다음 Docker 이미지 중 하나를 선택합니다. 

      * **미리 정의된 Docker 이미지**: Azure에서 기존 Docker 이미지를 지정합니다. 

        > [!NOTE]
        > 이 상자의 Docker 이미지 목록은 Azure 도구 키트가 패치하도록 구성된 여러 이미지로 구성되어 있어 아티팩트가 자동으로 배포됩니다. 

      * **사용자 지정 Dockerfile**: 로컬 컴퓨터에서 이전에 저장된 Dockerfile을 지정합니다.

        > [!NOTE]
        > 고유 Dockerfile을 배포하려는 개발자를 위한 고급 기능입니다. 그러나 이 기능은 Dockerfile을 올바르게 빌드하기 위해 이 옵션을 사용하는 개발자에 따라 달라집니다. Azure 도구 키트는 사용자 지정 Dockerfile에 있는 콘텐츠의 유효성을 검사하지 않으므로, Dockerfile에 문제가 있으면 배포에 실패할 수 있습니다. 또한 Azure 도구 키트에서는 사용자 지정 Dockerfile에 웹앱 아티팩트가 포함되어야 하므로 HTTP 연결을 열려고 시도합니다. 개발자가 다른 아티팩트 형식을 게시하는 경우 배포 후에 무해한 오류가 표시될 수도 있습니다.

   다. **포트 설정** 상자에서 Docker 컨테이너에 사용할 고유한 TCP 포트 바인딩을 입력합니다. 

10. 앞의 단계를 완료한 후 **마침**을 클릭합니다. 

Azure 도구 키트가 Docker 컨테이너에서 Azure에 웹앱을 배포하기 시작합니다. IntelliJ를 백그라운드에서 배포하도록 구성한 경우 외에는 **Azure에 배포** 진행률 표시줄이 나타납니다. 

![배포 진행률 표시줄][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>아티팩트 가져오기에 대한 추가 정보

배포 준비된 아티팩트를 만들려면 다음을 수행합니다.

1. IntelliJ의 웹앱 프로젝트를 엽니다.

2. **파일**을 클릭한 다음 **프로젝트 구조**를 클릭합니다.

   ![프로젝트 구조 명령][ART01]

3. 아티팩트를 추가하려면 녹색 더하기 기호(**+**)를 클릭한 다음 **웹 응용 프로그램: 보관**을 클릭합니다.

   ![“웹 응용 프로그램: 보관” 명령][ART02]

4. **이름** 상자에서 아티팩트에 사용할 이름을 입력한 다음(*.war* 확장자는 포함하지 않음) **확인**을 클릭합니다.

   ![아티팩트 이름 상자][ART03]

IntelliJ에서 아티팩트를 만드는 데 관한 자세한 내용은 JetBrains 웹 사이트의 [아티팩트 구성]을 참조하세요.

## <a name="next-steps"></a>다음 단계

Docker의 추가 리소스는 공식 [Docker 웹 사이트]를 참조하세요.

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Docker 웹 사이트]: https://www.docker.com/
[아티팩트 구성]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
