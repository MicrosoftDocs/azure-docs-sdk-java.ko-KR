---
title: Eclipse용 Azure 도구 키트를 사용하여 Docker 컨테이너 게시
description: Eclipse용 Azure 도구 키트를 사용하여 Docker 컨테이너로 Microsoft Azure에 웹앱을 게시하는 방법을 알아봅니다.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 4eb159bef52b384de32ada18937b0b9a47a93afc
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61590790"
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="a700e-103">Eclipse용 Azure 도구 키트를 사용하여 웹앱을 Docker 컨테이너로 게시</span><span class="sxs-lookup"><span data-stu-id="a700e-103">Publish a web app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="a700e-104">Docker 컨테이너는 웹 애플리케이션을 배포하는 데 널리 사용되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="a700e-105">개발자는 Docker 컨테이너를 통해 모든 프로젝트 파일과 종속성을 서버에 배포할 단일 패키지로 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="a700e-106">Eclipse용 Azure 도구 키트는 Microsoft Azure에 배포를 위한 *Docker 컨테이너로 게시* 기능을 추가함으로써 Java 개발자들을 위해 이 프로세스를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-106">The Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="a700e-107">이 문서에서는 Azure에 애플리케이션을 Docker 컨테이너로 게시하는 데 필요한 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="a700e-108">Docker에 대한 자세한 내용은 [Docker 웹 사이트]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a700e-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="a700e-109">Docker 컨테이너를 사용하여 Azure에 웹앱 게시</span><span class="sxs-lookup"><span data-stu-id="a700e-109">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="a700e-110">Eclipse의 웹앱 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="a700e-111">**Docker 컨테이너로 게시**를 시작하려면 다음 방법 중 하나를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="a700e-111">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="a700e-112">**탐색기** 보기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**를 클릭한 다음 **Docker 컨테이너로 게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-112">In the **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![탐색기 보기 Docker 컨테이너 명령으로 게시][PUB01]

   * <span data-ttu-id="a700e-114">Eclipse 도구 모음에서 **게시** 단추를 클릭한 다음 **Docker 컨테이너로 게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-114">On the Eclipse toolbar, click the **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Eclipse 도구 모음 Docker 컨테이너 명령으로 게시][PUB02]
      
   <span data-ttu-id="a700e-116">**Azure에 Docker 컨테이너 배포** 마법사가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-116">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Azure에 Docker 컨테이너 배포 마법사][PUB03]

3. <span data-ttu-id="a700e-118">**이미지 이름 입력, 아티팩트의 경로 선택 및 사용할 Docker 호스트 확인** 창에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-118">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span>

   <span data-ttu-id="a700e-119">a.</span><span class="sxs-lookup"><span data-stu-id="a700e-119">a.</span></span> <span data-ttu-id="a700e-120">**Docker 이미지 이름** 상자에서 Docker 호스트에 사용할 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-120">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="a700e-121">(마법사에서 이름을 자동으로 만들지만 사용자가 수정할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="a700e-121">(The wizard automatically creates a name, but you can modify it.)</span></span>

   <span data-ttu-id="a700e-122">b.</span><span class="sxs-lookup"><span data-stu-id="a700e-122">b.</span></span> <span data-ttu-id="a700e-123">**호스트** 영역에 사용자가 이미 만든 Docker 호스트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-123">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="a700e-124">다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-124">Do either of the following:</span></span>

   * <span data-ttu-id="a700e-125">기존 Docker 호스트가 있는 경우 웹앱을 해당 호스트에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-125">If you have an existing Docker host, you can deploy your web app to it.</span></span>
   * <span data-ttu-id="a700e-126">새 Docker 호스트를 만들려면 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-126">To create a new Docker host, click **Add**.</span></span>  
      
      <span data-ttu-id="a700e-127">**Docker 호스트 만들기** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-127">The **Create Docker Host** dialog box opens.</span></span>

   ![Azure에 Docker 컨테이너 배포 마법사][PUB04a]

4. <span data-ttu-id="a700e-129">**새 가상 머신 구성** 창에서 Docker 호스트에 대한 다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-129">In the **Configure the new virtual machine** window, specify the following options for your Docker host.</span></span> <span data-ttu-id="a700e-130">(마법사에서 대부분의 옵션을 자동으로 생성하지만 사용자가 수정할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="a700e-130">(The wizard automatically generates most of the options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="a700e-131">a.</span><span class="sxs-lookup"><span data-stu-id="a700e-131">a.</span></span> <span data-ttu-id="a700e-132">**이름**: Docker 호스트의 고유 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-132">**Name**: Enter a unique name for the Docker host.</span></span> <span data-ttu-id="a700e-133">(이전에 지정한 Docker 이미지 이름과 다릅니다.)</span><span class="sxs-lookup"><span data-stu-id="a700e-133">(It is not the same as the Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="a700e-134">b.</span><span class="sxs-lookup"><span data-stu-id="a700e-134">b.</span></span> <span data-ttu-id="a700e-135">**구독**: 호스트에 사용하는 Azure 구독을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-135">**Subscription**: Enter the Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="a700e-136">다.</span><span class="sxs-lookup"><span data-stu-id="a700e-136">c.</span></span> <span data-ttu-id="a700e-137">**지역**: 호스트가 배치될 지리적 지역을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-137">**Region**: Enter the geographical region where your host is located.</span></span>

   <span data-ttu-id="a700e-138">d.</span><span class="sxs-lookup"><span data-stu-id="a700e-138">d.</span></span> <span data-ttu-id="a700e-139">**호스트 OS 및 크기** 탭에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-139">On the **Host OS and Size** tab:</span></span> 
   * <span data-ttu-id="a700e-140">**호스트 OS**: 호스트를 포함할 가상 머신의 운영 체제를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-140">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span>
   * <span data-ttu-id="a700e-141">**크기**: 호스트의 가상 컴퓨터 크기를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-141">**Size**: Enter the virtual-machine size for your host.</span></span>

   <span data-ttu-id="a700e-142">e.</span><span class="sxs-lookup"><span data-stu-id="a700e-142">e.</span></span> <span data-ttu-id="a700e-143">**리소스 그룹** 탭에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-143">On the **Resource Group** tab:</span></span> 
   * <span data-ttu-id="a700e-144">**새 리소스 그룹**: 호스트에 대한 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-144">**New resource group**: Create a new resource group for your host.</span></span>
   * <span data-ttu-id="a700e-145">**기존 리소스 그룹**: Azure 계정에서 기존 리소스 그룹을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="a700e-146">f.</span><span class="sxs-lookup"><span data-stu-id="a700e-146">f.</span></span> <span data-ttu-id="a700e-147">**네트워크** 탭에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-147">On the **Network** tab:</span></span> 
   * <span data-ttu-id="a700e-148">**새 가상 네트워크**: 호스트에 대한 새 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-148">**New virtual network**: Create a new virtual network for your host.</span></span>
   * <span data-ttu-id="a700e-149">**기존 가상 네트워크**: Azure 계정에서 기존 가상 네트워크를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="a700e-150">g.</span><span class="sxs-lookup"><span data-stu-id="a700e-150">g.</span></span> <span data-ttu-id="a700e-151">**저장소** 탭에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-151">On the **Storage** tab:</span></span> 
   * <span data-ttu-id="a700e-152">**새 스토리지 계정**: 호스트에 대한 새 스토리지 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-152">**New storage account**: Create a new storage account for your host.</span></span>
   * <span data-ttu-id="a700e-153">**기존 스토리지 계정**: Azure 계정에서 기존 스토리지 계정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="a700e-154">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-154">Click **Next**.</span></span>

6. <span data-ttu-id="a700e-155">**로그인 자격 증명 및 포트 설정 구성** 창에서 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-155">In the **Configure log in credentials and port settings** window, select one of the following options:</span></span>

   * <span data-ttu-id="a700e-156">**Azure Key Vault에서 자격 증명 가져오기**: Azure 구독에 저장되어 있는 이전 자격 증명 세트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span> 

   >[!NOTE]
   ><span data-ttu-id="a700e-157">특정 계정 또는 서비스 주체로 만든 Azure Key Vault는 구독을 공유하는 다른 계정 또는 서비스 주체에서 자동으로 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="a700e-158">다른 계정 또는 서비스 주체가 Key Vault를 사용하도록 허용하려면 Azure Portal을 사용하여 계정 또는 서비스 주체를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-158">To allow another account or service principal to use the Key Vault, you must use the Azure portal to add the account or service principal.</span></span>
   >

   * <span data-ttu-id="a700e-159">**새 로그인 자격 증명**: 새 로그인 자격 증명 세트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="a700e-160">이 옵션을 선택하는 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-160">If you select this option, do the following:</span></span> 
    
     * <span data-ttu-id="a700e-161">**VM 자격 증명** 탭에서 Docker 호스트의 가상 컴퓨터 로그인 자격 증명에 대해 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-161">On the **VM Credentials** tab, choose one of the following options for the virtual-machine login credentials of your Docker host:</span></span> 

       * <span data-ttu-id="a700e-162">**사용자 이름**: 가상 머신 로그인 자격 증명의 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-162">**Username**: Enter the username for your virtual machine login credentials.</span></span> 
       * <span data-ttu-id="a700e-163">**암호** 및 **확인**: 가상 머신 로그인 자격 증명의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-163">**Password** and **Confirm**: Enter the password for your virtual machine login credentials.</span></span> 
       * <span data-ttu-id="a700e-164">**SSH**: Docker 호스트에 사용할 SSH(Secure Shell) 설정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-164">**SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="a700e-165">다음 옵션 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-165">You can choose from the following options:</span></span> 
          * <span data-ttu-id="a700e-166">**없음**: 가상 머신에서 SSH 연결을 허용하지 않게 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span> 
          * <span data-ttu-id="a700e-167">**자동 생성**: SSH를 통해 연결하는 데 필요한 설정을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-167">**Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span> 
          * <span data-ttu-id="a700e-168">**디렉터리에서 가져오기**: 이전에 저장된 SSH 설정 세트를 포함하는 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="a700e-169">디렉터리에 다음 두 파일이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-169">The directory must contain the following two files:</span></span> 
             * <span data-ttu-id="a700e-170">*id_rsa*: 사용자의 RSA ID가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-170">*id_rsa*: Contains the RSA identification for a user.</span></span> 
             * <span data-ttu-id="a700e-171">*id_rsa.pub*: 인증에 사용되는 RSA 공개 키를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-171">*id_rsa.pub*: Contains the RSA public key that is used for authentication.</span></span> 
        
         ![Docker 호스트 만들기][PUB05]

     * <span data-ttu-id="a700e-173">**Docker 디먼 자격 증명** 탭에서 다음 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-173">On the **Docker Daemon Credentials** tab, specify the following options:</span></span> 

       * <span data-ttu-id="a700e-174">**Docker 디먼 포트**: Docker 호스트의 고유한 TCP 포트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-174">**Docker Daemon port**: Enter the unique TCP port for your Docker host.</span></span> 
       * <span data-ttu-id="a700e-175">**TLS 보안**: Docker 호스트의 전송 계층 보안 설정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-175">**TLS Security**: Enter the Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="a700e-176">다음 옵션 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-176">You can choose from the following options:</span></span> 
          * <span data-ttu-id="a700e-177">**없음**: 가상 머신에서 TLS 연결을 허용하지 않게 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span> 
          * <span data-ttu-id="a700e-178">**자동 생성**: TLS를 통해 연결하는 데 필요한 설정을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-178">**Auto-generate**: Automatically creates the requisite settings for connecting via TLS.</span></span> 
          * <span data-ttu-id="a700e-179">**디렉터리에서 가져오기**: 이전에 저장된 TLS 설정 세트를 포함하는 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="a700e-180">구체적으로 말하면 디렉터리에 다음 6개의 파일이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-180">More specifically, the directory must contain the following six files:</span></span> 
             * <span data-ttu-id="a700e-181">*ca.pem* 및 *ca key.pem*: TLS 인증 기관의 인증서와 공개 키가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-181">*ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.</span></span> 
             * <span data-ttu-id="a700e-182">*cert.pem* 및 *key.pem*: TLS 인증에 사용할 클라이언트 인증서와 공개 키가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-182">*cert.pem* and *key.pem*: Contain the client certificate and public key that is used for TLS authentication.</span></span> 
             * <span data-ttu-id="a700e-183">*server.pem* 및 *server-key.pem*: 호스트의 서버 인증서와 공개 키가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-183">*server.pem* and *server-key.pem*: Contain the server certificate and public key for the host.</span></span> 

         ![Docker 호스트 만들기][PUB06]

7. <span data-ttu-id="a700e-185">이전 정보를 모두 입력한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-185">After you have entered all of the preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="a700e-186">**Azure에 Docker 컨테이너 배포** 마법사에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-186">In the **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Azure에 Docker 컨테이너 배포 마법사][PUB07]

9. <span data-ttu-id="a700e-188">**만들 Docker 컨테이너 구성** 창에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-188">In the **Configure the Docker container to be created** window, do the following:</span></span>

   <span data-ttu-id="a700e-189">a.</span><span class="sxs-lookup"><span data-stu-id="a700e-189">a.</span></span> <span data-ttu-id="a700e-190">**Docker 컨테이너 이름** 상자에서 Docker 컨테이너에 사용할 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-190">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="a700e-191">b.</span><span class="sxs-lookup"><span data-stu-id="a700e-191">b.</span></span> <span data-ttu-id="a700e-192">다음 Docker 이미지 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-192">Choose one of the following Docker images:</span></span> 

   * <span data-ttu-id="a700e-193">**미리 정의된 Docker 이미지**: Azure에서 기존 Docker 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span> 

     >[!NOTE]
     ><span data-ttu-id="a700e-194">이 상자의 Docker 이미지 목록은 Azure 도구 키트가 패치하도록 구성된 여러 이미지로 구성되어 있어 아티팩트가 자동으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-194">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span>
     >

   * <span data-ttu-id="a700e-195">**사용자 지정 Dockerfile**: 로컬 컴퓨터에서 이전에 저장된 Dockerfile을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

     >[!NOTE]
     ><span data-ttu-id="a700e-196">고유 Dockerfile을 배포하려는 개발자를 위한 고급 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-196">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="a700e-197">그러나 이 기능은 Dockerfile을 올바르게 빌드하기 위해 이 옵션을 사용하는 개발자에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-197">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="a700e-198">Azure 도구 키트는 사용자 지정 Dockerfile에 있는 콘텐츠의 유효성을 검사하지 않으므로, Dockerfile에 문제가 있으면 배포에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-198">The Azure Toolkit does not validate the content in a custom Dockerfile, so the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="a700e-199">또한 Azure 도구 키트에서는 사용자 지정 Dockerfile에 웹앱 아티팩트가 포함되어야 하므로 HTTP 연결을 열려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-199">In addition, the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, and it will attempt to open an HTTP connection.</span></span> <span data-ttu-id="a700e-200">개발자가 다른 아티팩트 형식을 게시하는 경우 배포 후에 무해한 오류가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>
     >

   <span data-ttu-id="a700e-201">다.</span><span class="sxs-lookup"><span data-stu-id="a700e-201">c.</span></span> <span data-ttu-id="a700e-202">**포트 설정**: Docker 컨테이너에 사용할 고유한 TCP 포트 바인딩을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-202">**Port settings**: Enter the unique TCP port binding for your Docker container.</span></span>

      ![만들 Docker 컨테이너 구성 창][PUB08]

10. <span data-ttu-id="a700e-204">앞의 단계를 모두 완료한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-204">After you have completed all of the preceding steps, click **Finish**.</span></span>

<span data-ttu-id="a700e-205">Azure 도구 키트가 Docker 컨테이너에서 Azure에 웹앱을 배포하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a700e-205">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a700e-206">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a700e-206">Next steps</span></span>

<span data-ttu-id="a700e-207">Docker의 추가 리소스는 공식 [Docker 웹 사이트]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a700e-207">For additional resources for Docker, see the official [Docker website].</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Docker 웹 사이트]: https://www.docker.com/
[Docker website]: https://www.docker.com/

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