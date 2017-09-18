---
title: "IntelliJ용 Azure 도구 키트를 사용하여 Docker 컨테이너 게시"
description: "IntelliJ용 Azure 도구 키트를 사용하여 Docker 컨테이너로 Microsoft Azure에 웹앱을 게시하는 방법을 알아봅니다."
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
ms.openlocfilehash: 2d94dfa4467bc79d6155321a9966358b79e9e960
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="36b47-103">IntelliJ용 Azure 도구 키트를 사용하여 웹앱을 Docker 컨테이너로 게시</span><span class="sxs-lookup"><span data-stu-id="36b47-103">Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="36b47-104">Docker 컨테이너는 웹 응용 프로그램을 배포하는 데 널리 사용되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="36b47-105">개발자는 Docker 컨테이너를 통해 모든 프로젝트 파일과 종속성을 서버에 배포할 단일 패키지로 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="36b47-106">IntelliJ용 Azure 도구 키트는 Microsoft Azure에 배포를 위한 *Docker 컨테이너로 게시* 기능을 추가함으로써 Java 개발자들을 위해 이 프로세스를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="36b47-107">이 문서에서는 Azure에 응용 프로그램을 Docker 컨테이너로 게시하는 데 필요한 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="36b47-108">Docker에 대한 자세한 내용은 [Docker 웹 사이트]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36b47-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="36b47-109">Docker 컨테이너를 사용하여 Azure에 웹앱 게시</span><span class="sxs-lookup"><span data-stu-id="36b47-109">Publish your web app to Azure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="36b47-110">웹앱을 게시하려면 배포 준비된 아티팩트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-110">To publish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="36b47-111">자세한 내용은 [아티팩트 만들기에 대한 추가 정보](#artifacts) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36b47-111">To learn more, see the [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="36b47-112">배포 마법사를 한 번 이상 완료한 후 마법사를 다시 실행하는 경우 사용자 설정의 대부분은 기본값으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-112">After you have completed the deployment wizard at least once, most of your settings are used as defaults when you run the wizard again.</span></span>
>

1. <span data-ttu-id="36b47-113">IntelliJ의 웹앱 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="36b47-114">**Docker 컨테이너로 게시**를 시작하려면 다음 방법 중 하나를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="36b47-114">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="36b47-115">**프로젝트** 도구 창에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Azure**를 클릭한 다음 **Docker 컨테이너로 게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-115">In the **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Docker 컨테이너 명령으로 게시][PUB01]

   * <span data-ttu-id="36b47-117">IntelliJ 도구 모음에서 **그룹 게시** 단추를 클릭한 다음 **Docker 컨테이너로 게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-117">On the IntelliJ toolbar, click the **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="36b47-118">![Docker 컨테이너 명령으로 게시][PUB02]</span><span class="sxs-lookup"><span data-stu-id="36b47-118">![The Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="36b47-119">**Azure에 Docker 컨테이너 배포** 마법사가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-119">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Azure에 Docker 컨테이너 배포 마법사][PUB03]

3. <span data-ttu-id="36b47-121">**이미지 이름 입력, 아티팩트의 경로 선택 및 사용할 Docker 호스트 확인** 창에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-121">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span> 

   <span data-ttu-id="36b47-122">a.</span><span class="sxs-lookup"><span data-stu-id="36b47-122">a.</span></span> <span data-ttu-id="36b47-123">**Docker 이미지 이름** 상자에서 Docker 호스트에 사용할 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-123">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="36b47-124">(마법사에서 이름을 자동으로 만들지만 사용자가 수정할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="36b47-124">(The wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="36b47-125">b.</span><span class="sxs-lookup"><span data-stu-id="36b47-125">b.</span></span> <span data-ttu-id="36b47-126">**호스트** 영역에 사용자가 이미 만든 Docker 호스트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-126">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="36b47-127">다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-127">Do either of the following:</span></span> 
      * <span data-ttu-id="36b47-128">기존 Docker 호스트가 있는 경우 웹앱을 해당 호스트에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-128">If you have an existing Docker host, you can deploy your web app to it.</span></span>
      * <span data-ttu-id="36b47-129">Docker 호스트를 만들려면 녹색 더하기 기호(**+**)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-129">To create a Docker host, click the green plus sign (**+**).</span></span>  
       <span data-ttu-id="36b47-130">**Docker 호스트 만들기** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-130">The **Create Docker Host** dialog box opens.</span></span> 

      ![Azure에 Docker 컨테이너 배포 마법사][PUB04a]

4. <span data-ttu-id="36b47-132">**새 가상 컴퓨터 구성** 창에서 Docker 호스트에 대한 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-132">In the **Configure the new virtual machine** window, provide the following information about your Docker host.</span></span> <span data-ttu-id="36b47-133">(마법사에서 대부분의 정보를 자동으로 생성하지만 사용자가 수정할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="36b47-133">(The wizard automatically generates most of the information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="36b47-134">a.</span><span class="sxs-lookup"><span data-stu-id="36b47-134">a.</span></span> <span data-ttu-id="36b47-135">**이름** 상자에서 Docker 호스트에 사용할 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-135">In the **Name** box, enter a unique name for the Docker host.</span></span> <span data-ttu-id="36b47-136">(이전에 지정한 Docker 이미지 이름과 다릅니다.)</span><span class="sxs-lookup"><span data-stu-id="36b47-136">(It is not the same as the Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="36b47-137">b.</span><span class="sxs-lookup"><span data-stu-id="36b47-137">b.</span></span> <span data-ttu-id="36b47-138">**구독** 상자에서 호스트에 사용하는 Azure 구독을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-138">In the **Subscription** box, enter the Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="36b47-139">c.</span><span class="sxs-lookup"><span data-stu-id="36b47-139">c.</span></span> <span data-ttu-id="36b47-140">**지역** 상자에서 호스트가 배치될 지리적 지역을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-140">In the **Region** box, enter the geographical region where your host is located.</span></span>
      
   <span data-ttu-id="36b47-141">d.</span><span class="sxs-lookup"><span data-stu-id="36b47-141">d.</span></span> <span data-ttu-id="36b47-142">**OS 및 크기** 탭에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-142">On the **OS and Size** tab, do the following:</span></span>      
      * <span data-ttu-id="36b47-143">**호스트 OS**: 호스트를 포함할 가상 컴퓨터의 운영 체제를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-143">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="36b47-144">**크기**: 호스트의 가상 컴퓨터 크기를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-144">**Size**: Enter the virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="36b47-145">e.</span><span class="sxs-lookup"><span data-stu-id="36b47-145">e.</span></span> <span data-ttu-id="36b47-146">**리소스 그룹** 탭에서 다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-146">On the **Resource Group** tab, select either of the following:</span></span>      
      * <span data-ttu-id="36b47-147">**새 리소스 그룹**: 호스트에 사용할 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="36b47-148">**기존 리소스 그룹**: Azure 계정에서 기존 리소스 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="36b47-149">f.</span><span class="sxs-lookup"><span data-stu-id="36b47-149">f.</span></span> <span data-ttu-id="36b47-150">**네트워크** 탭에서 다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-150">On the **Network** tab, select either of the following:</span></span>      
      * <span data-ttu-id="36b47-151">**새 가상 네트워크**: 호스트에 사용할 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="36b47-152">**기존 가상 네트워크**: Azure 계정에서 기존 가상 네트워크를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="36b47-153">g.</span><span class="sxs-lookup"><span data-stu-id="36b47-153">g.</span></span> <span data-ttu-id="36b47-154">**저장소** 탭에서 다음 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-154">On the **Storage** tab, select either of the following:</span></span>      
      * <span data-ttu-id="36b47-155">**새 저장소 계정**: 호스트에 사용할 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="36b47-156">**기존 저장소 계정**: Azure 계정에서 기존 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="36b47-157">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-157">Click **Next**.</span></span>  
     <span data-ttu-id="36b47-158">**로그인 자격 증명 및 포트 설정 구성** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-158">The **Configure log in credentials and port settings** window opens.</span></span>

      ![로그인 자격 증명 및 포트 설정 구성 창][PUB05]

6. <span data-ttu-id="36b47-160">다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-160">Select one of the following options:</span></span>

      * <span data-ttu-id="36b47-161">**Azure Key Vault에서 자격 증명 가져오기**: Azure 구독에 저장되어 있는 이전에 저장한 자격 증명 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="36b47-162">특정 계정 또는 서비스 주체로 만든 Azure Key Vault는 구독을 공유하는 다른 계정 또는 서비스 주체에서 자동으로 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="36b47-163">다른 계정 또는 서비스 주체가 Key Vault를 사용하도록 허용하려면 Azure Portal을 사용하여 계정 또는 서비스 주체를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-163">To allow another account or service principal to use the key vault, you must use the Azure portal to add the account or service principal.</span></span>

      * <span data-ttu-id="36b47-164">**새 로그인 자격 증명**: 새 로그인 자격 증명 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="36b47-165">이 옵션을 선택하는 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-165">If you select this option, do the following:</span></span>

        <span data-ttu-id="36b47-166">a.</span><span class="sxs-lookup"><span data-stu-id="36b47-166">a.</span></span> <span data-ttu-id="36b47-167">**VM 자격 증명** 탭에서 Docker 호스트의 가상 컴퓨터 로그인 자격 증명에 대한 다음 정보를 제공합니다. * **Username**: 가상 컴퓨터 로그인 자격 증명에 대한 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-167">On the **VM Credentials** tab, provide the following information for the virtual-machine login credentials of your Docker host: * **Username**: Enter the username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="36b47-168">* **암호** 및 **확인**: 가상 컴퓨터 로그인 자격 증명에 사용할 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-168">* **Password** and **Confirm**: Enter the password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="36b47-169">* **SSH**: Docker 호스트에 사용할 SSH(Secure Shell) 설정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-169">* **SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="36b47-170">다음 옵션 중 하나를 선택할 수 있습니다. * **None**: 가상 컴퓨터가 SSH 연결을 허용하지 않도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-170">You can select one of the following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="36b47-171">* **자동 생성**: SSH를 통해 연결하는 데 필요한 설정을 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-171">* **Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="36b47-172">* **디렉터리에서 가져오기**: 이전에 저장된 SSH 설정 집합을 포함하는 디렉터리를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-172">* **Import from directory**: Allows you to specify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="36b47-173">디렉터리에 다음 두 파일이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-173">The directory must contain the following two files:</span></span>
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        <span data-ttu-id="36b47-174">b.</span><span class="sxs-lookup"><span data-stu-id="36b47-174">b.</span></span> <span data-ttu-id="36b47-175">**Docker 데몬 액세스** 탭에서 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-175">On the **Docker Daemon Access** tab, provide the following information:</span></span>

          ![Docker 호스트 만들기][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="36b47-177">필요한 정보를 입력한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-177">After you have entered the required information, click **Finish**.</span></span>  
    <span data-ttu-id="36b47-178">**Azure에 Docker 컨테이너 배포** 마법사가 다시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-178">The **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Azure에 Docker 컨테이너 배포 마법사][PUB07]

8. <span data-ttu-id="36b47-180">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-180">Click **Next**.</span></span>  
    <span data-ttu-id="36b47-181">**만들 Docker 컨테이너 구성** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-181">The **Configure the Docker container to be created** window opens.</span></span>

   ![만들 Docker 컨테이너 구성 창][PUB08]

9. <span data-ttu-id="36b47-183">**만들 Docker 컨테이너를 구성** 창에서 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-183">In the **Configure the Docker container to be created** window, provide the following information:</span></span> 

   <span data-ttu-id="36b47-184">a.</span><span class="sxs-lookup"><span data-stu-id="36b47-184">a.</span></span> <span data-ttu-id="36b47-185">**Docker 컨테이너 이름** 상자에서 Docker 컨테이너에 사용할 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-185">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="36b47-186">b.</span><span class="sxs-lookup"><span data-stu-id="36b47-186">b.</span></span> <span data-ttu-id="36b47-187">다음 Docker 이미지 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-187">Choose one of the following Docker images:</span></span> 

      * <span data-ttu-id="36b47-188">**미리 정의된 Docker 이미지**: Azure에서 기존 Docker 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="36b47-189">이 상자의 Docker 이미지 목록은 Azure 도구 키트가 패치하도록 구성된 여러 이미지로 구성되어 있어 아티팩트가 자동으로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-189">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="36b47-190">**사용자 지정 Dockerfile**: 로컬 컴퓨터에서 이전에 저장된 Dockerfile을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="36b47-191">고유 Dockerfile을 배포하려는 개발자를 위한 고급 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-191">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="36b47-192">그러나 이 기능은 Dockerfile을 올바르게 빌드하기 위해 이 옵션을 사용하는 개발자에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-192">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="36b47-193">Azure 도구 키트는 사용자 지정 Dockerfile에 있는 콘텐츠의 유효성을 검사하지 않으므로, Dockerfile에 문제가 있으면 배포에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-193">Because the Azure Toolkit does not validate the content in a custom Dockerfile, the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="36b47-194">또한 Azure 도구 키트에서는 사용자 지정 Dockerfile에 웹앱 아티팩트가 포함되어야 하므로 HTTP 연결을 열려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-194">In addition, because the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, it attempts to open an HTTP connection.</span></span> <span data-ttu-id="36b47-195">개발자가 다른 아티팩트 형식을 게시하는 경우 배포 후에 무해한 오류가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="36b47-196">c.</span><span class="sxs-lookup"><span data-stu-id="36b47-196">c.</span></span> <span data-ttu-id="36b47-197">**포트 설정** 상자에서 Docker 컨테이너에 사용할 고유한 TCP 포트 바인딩을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-197">In the **Port settings** box, enter the unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="36b47-198">앞의 단계를 완료한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-198">After you have completed the preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="36b47-199">Azure 도구 키트가 Docker 컨테이너에서 Azure에 웹앱을 배포하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-199">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> <span data-ttu-id="36b47-200">IntelliJ를 백그라운드에서 배포하도록 구성한 경우 외에는 **Azure에 배포** 진행률 표시줄이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-200">Unless you have configured IntelliJ to be deployed in the background, a **Deploying to Azure** progress bar appears.</span></span> 

![배포 진행률 표시줄][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="36b47-202">아티팩트 가져오기에 대한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="36b47-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="36b47-203">배포 준비된 아티팩트를 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-203">To create a deployment-ready artifact, do the following:</span></span>

1. <span data-ttu-id="36b47-204">IntelliJ의 웹앱 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="36b47-205">**파일**을 클릭한 다음 **프로젝트 구조**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-205">Click **File**, and then click **Project Structure**.</span></span>

   ![프로젝트 구조 명령][ART01]

3. <span data-ttu-id="36b47-207">아티팩트를 추가하려면 녹색 더하기 기호(**+**)를 클릭한 다음 **웹 응용 프로그램: 보관**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-207">To add an artifact, click the green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![“웹 응용 프로그램: 보관” 명령][ART02]

4. <span data-ttu-id="36b47-209">**이름** 상자에서 아티팩트에 사용할 이름을 입력한 다음(*.war* 확장자는 포함하지 않음) **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="36b47-209">In the **Name** box, enter a name for your artifact (do not include the *.war* extension), and then click **OK**.</span></span>

   ![아티팩트 이름 상자][ART03]

<span data-ttu-id="36b47-211">IntelliJ에서 아티팩트를 만드는 데 관한 자세한 내용은 JetBrains 웹 사이트의 [아티팩트 구성]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36b47-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on the JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36b47-212">다음 단계</span><span class="sxs-lookup"><span data-stu-id="36b47-212">Next steps</span></span>

<span data-ttu-id="36b47-213">Docker의 추가 리소스는 공식 [Docker 웹 사이트]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="36b47-213">For additional resources for Docker, see the official [Docker website].</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

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