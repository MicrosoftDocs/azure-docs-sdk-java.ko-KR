---
title: Azure Web Apps의 Maven 플러그 인을 사용하여 Azure Container Registry의 Spring Boot 앱을 Azure App Service에 배포하는 방법
description: 이 자습서는 Maven 플러그 인을 사용하여 Azure App Service에 Azure Container Registry의 Spring Boot 응용 프로그램을 배포하는 단계를 설명합니다.
services: container-registry
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: e84960ebf79b89b2430924016a429518a935d086
ms.sourcegitcommit: 9d9e2fa97ebd95a699adcb58e82c3fc0882f0a24
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2018
ms.locfileid: "49315937"
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a><span data-ttu-id="ef73a-103">Azure Web Apps의 Maven 플러그 인을 사용하여 Azure Container Registry의 Spring Boot 앱을 Azure App Service에 배포하는 방법</span><span class="sxs-lookup"><span data-stu-id="ef73a-103">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app in Azure Container Registry to Azure App Service</span></span>

<span data-ttu-id="ef73a-104">이 문서에서는 Azure Container Registry에 샘플 [Spring Boot] 응용 프로그램을 배포하고 Azure Web Apps용 Maven 플러그인을 사용하여 Azure App Service에 응용 프로그램을 배포하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-104">This article demonstrates how to deploy a sample [Spring Boot] application to Azure Container Registry, and then use the Maven Plugin for Azure Web Apps to deploy your application to Azure App Service.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="ef73a-105">[Apache Maven](http://maven.apache.org/)에서 Azure Web Apps용 Maven 플러그인은 Maven 프로젝트에 Azure App Service의 원활한 통합을 제공하고 Azure App Service에 웹앱을 배포하는 개발자를 위한 프로세스를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-105">The Maven Plugin for Azure Web Apps for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>
> 
> <span data-ttu-id="ef73a-106">Azure Web Apps의 Maven 플러그 인은 현재 미리 보기로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="ef73a-107">지금은 FTP 게시만 지원되지만 향후에 기능이 추가될 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="ef73a-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ef73a-108">Prerequisites</span></span>

<span data-ttu-id="ef73a-109">이 자습서의 단계를 완료하려면 다음 필수 조건이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="ef73a-110">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="ef73a-111">[Azure CLI(명령줄 인터페이스)]</span><span class="sxs-lookup"><span data-stu-id="ef73a-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="ef73a-112">최신 [JDK(Java Development Kit)], 버전 1.7 이상</span><span class="sxs-lookup"><span data-stu-id="ef73a-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="ef73a-113">Apache의 [Maven] 빌드 도구(버전 3)</span><span class="sxs-lookup"><span data-stu-id="ef73a-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="ef73a-114">[Git] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ef73a-114">A [Git] client.</span></span>
* <span data-ttu-id="ef73a-115">[Docker] 클라이언트</span><span class="sxs-lookup"><span data-stu-id="ef73a-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ef73a-116">이 자습서의 가상화 요구 사항으로 인해 가상 머신에는 이 문서의 단계를 따를 수 없습니다. 따라서 가상화 기능이 사용하도록 설정된 물리적 컴퓨터를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="ef73a-117">Docker 웹앱에 샘플 Spring Boot 복제</span><span class="sxs-lookup"><span data-stu-id="ef73a-117">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="ef73a-118">이 섹션에서는 컨테이너화된 Spring Boot 응용 프로그램을 복제하고 로컬로 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="ef73a-119">명령 프롬프트 또는 터미널 창을 열고 Spring Boot 응용 프로그램을 저장할 로컬 디렉터리를 만들고 해당 디렉터리로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="ef73a-119">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="ef73a-120">-- 또는 --</span><span class="sxs-lookup"><span data-stu-id="ef73a-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="ef73a-121">[Spring Boot on Docker 시작] 샘플 프로젝트를 방금 만든 디렉터리에 복제합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="ef73a-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone -b https://github.com/spring-guides/gs-spring-boot-docker
   ```

1. <span data-ttu-id="ef73a-122">디렉터리를 완료된 프로젝트로 변경합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="ef73a-122">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="ef73a-123">Maven을 사용하여 JAR 파일을 빌드합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="ef73a-123">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="ef73a-124">웹앱을 만들면 Maven을 사용하여 웹앱을 시작합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="ef73a-124">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="ef73a-125">웹 브라우저를 사용하여 로컬로 이동하여 웹앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="ef73a-126">예를 들어, curl을 사용할 수 있는 경우 다음 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-126">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="ef73a-127">**Hello Docker World** 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-127">You should see the following message displayed: **Hello Docker World**</span></span>

   ![로컬로 샘플 앱 찾아보기][SB01]

> [!NOTE]
>
> <span data-ttu-id="ef73a-129">Docker를 로컬에서 사용하는 경우 포트 2375의 localhost에 연결할 수 없다는 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-129">When you are using Docker locally, you may see an error which states that you cannot connect to localhost on port 2375.</span></span> <span data-ttu-id="ef73a-130">이 경우 TLS 없이 로컬에서 Docker를 사용하도록 설정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-130">If this happens, you may need to enable using Docker locally without TLS.</span></span> <span data-ttu-id="ef73a-131">이렇게 하려면 Docker 설정을 열고 **TLS 없이 TCP://localhost:2375에 데몬 노출** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-131">To do so, open your Docker settings and check the option to **Expose daemon on TCP://localhost:2375 without TLS**.</span></span>
>
> ![로컬 TCP 포트 2375에서 Docker 데몬 노출][TL01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="ef73a-133">Azure 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="ef73a-133">Create an Azure service principal</span></span>

<span data-ttu-id="ef73a-134">이 섹션에서는 컨테이너를 Azure에 배포할 때 Maven 플러그 인에서 사용하는 Azure 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-134">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="ef73a-135">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-135">Open a command prompt.</span></span>

2. <span data-ttu-id="ef73a-136">Azure CLI를 사용하여 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-136">Sign into your Azure account by using the Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="ef73a-137">지시에 따라 로그인 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-137">Follow the instructions to complete the sign-in process.</span></span>

3. <span data-ttu-id="ef73a-138">Azure 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="ef73a-138">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="ef73a-139">위치:</span><span class="sxs-lookup"><span data-stu-id="ef73a-139">Where:</span></span>

   | <span data-ttu-id="ef73a-140">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ef73a-140">Parameter</span></span>  |                    <span data-ttu-id="ef73a-141">설명</span><span class="sxs-lookup"><span data-stu-id="ef73a-141">Description</span></span>                     |
   |------------|----------------------------------------------------|
   | `uuuuuuuu` | <span data-ttu-id="ef73a-142">서비스 주체에 대한 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-142">Specifies the user name for the service principal.</span></span> |
   | `pppppppp` | <span data-ttu-id="ef73a-143">서비스 주체에 대한 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-143">Specifies the password for the service principal.</span></span>  |


4. <span data-ttu-id="ef73a-144">Azure는 다음 예제와 유사한 JSON로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-144">Azure responds with JSON that resembles the following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="ef73a-145">컨테이너를 Azure에 배포하도록 Maven 플러그 인을 구성하는 경우 이 JSON 응답의 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-145">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="ef73a-146">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` 및 `tttttttt`는 다음 섹션에서 Maven `settings.xml` 파일을 구성할 때 이러한 값을 해당 요소에 쉽게 매핑할 수 있도록 이 예제에서 사용되는 자리 표시자 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-146">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="ef73a-147">Azure CLI를 사용하여 Azure Container Registry 만들기</span><span class="sxs-lookup"><span data-stu-id="ef73a-147">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="ef73a-148">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-148">Open a command prompt.</span></span>

1. <span data-ttu-id="ef73a-149">Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-149">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="ef73a-150">이 문서에서 사용할 Azure 리소스에 대한 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-150">Create a resource group for the Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="ef73a-151">이 예제에서 `wingtiptoysresources`를 리소스 그룹의 고유 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-151">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="ef73a-152">Spring Boot 앱의 리소스 그룹에서 개인 Azure Container Registry를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-152">Create a private Azure container registry in the resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="ef73a-153">이 예제에서 `wingtiptoysregistry`를 컨테이너 레지스트리의 고유 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-153">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="ef73a-154">컨테이너 레지스트리에 대한 암호를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-154">Retrieve the password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="ef73a-155">Azure는 암호로 응답합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="ef73a-155">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a><span data-ttu-id="ef73a-156">Maven 설정에 Azure Container Registry 및 Azure 서비스 주체 추가</span><span class="sxs-lookup"><span data-stu-id="ef73a-156">Add your Azure container registry and Azure service principal to your Maven settings</span></span>

1. <span data-ttu-id="ef73a-157">텍스트 편집기에서 Maven `settings.xml` 파일을 엽니다. 이 파일은 다음 예제와 같은 경로에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-157">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

2. <span data-ttu-id="ef73a-158">이 문서의 이전 섹션에서 *settings.xml* 파일의 `<servers>` 컬렉션에 Azure Container Registry 액세스 설정을 추가합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="ef73a-158">Add your Azure Container Registry access settings from the previous section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="ef73a-159">위치:</span><span class="sxs-lookup"><span data-stu-id="ef73a-159">Where:</span></span>

   |   <span data-ttu-id="ef73a-160">요소</span><span class="sxs-lookup"><span data-stu-id="ef73a-160">Element</span></span>    |                                 <span data-ttu-id="ef73a-161">설명</span><span class="sxs-lookup"><span data-stu-id="ef73a-161">Description</span></span>                                  |
   |--------------|------------------------------------------------------------------------------|
   |    `<id>`    |         <span data-ttu-id="ef73a-162">개인 Azure Container Registry 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-162">Contains the name of your private Azure container registry.</span></span>          |
   | `<username>` |         <span data-ttu-id="ef73a-163">개인 Azure Container Registry 이름을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-163">Contains the name of your private Azure container registry.</span></span>          |
   | `<password>` | <span data-ttu-id="ef73a-164">이 문서의 이전 섹션에서 검색된 암호를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-164">Contains the password you retrieved in the previous section of this article.</span></span> |


3. <span data-ttu-id="ef73a-165">*settings.xml* 파일의 `<servers>` 컬렉션에 이 문서의 이전 섹션에 있는 Azure 서비스 주체 설정을 추가합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="ef73a-165">Add your Azure service principal settings from an earlier section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="ef73a-166">위치:</span><span class="sxs-lookup"><span data-stu-id="ef73a-166">Where:</span></span>

   |     <span data-ttu-id="ef73a-167">요소</span><span class="sxs-lookup"><span data-stu-id="ef73a-167">Element</span></span>     |                                                                                   <span data-ttu-id="ef73a-168">설명</span><span class="sxs-lookup"><span data-stu-id="ef73a-168">Description</span></span>                                                                                   |
   |-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `<id>`      |                                <span data-ttu-id="ef73a-169">Azure에 웹앱을 배포할 때 Maven을 사용하여 보안 설정을 조회하는 고유한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-169">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>                                |
   |   `<client>`    |                                                             <span data-ttu-id="ef73a-170">서비스 사용자의 `appId` 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-170">Contains the `appId` value from your service principal.</span></span>                                                             |
   |   `<tenant>`    |                                                            <span data-ttu-id="ef73a-171">서비스 사용자의 `tenant` 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-171">Contains the `tenant` value from your service principal.</span></span>                                                             |
   |     `<key>`     |                                                           <span data-ttu-id="ef73a-172">서비스 사용자의 `password` 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-172">Contains the `password` value from your service principal.</span></span>                                                            |
   | `<environment>` | <span data-ttu-id="ef73a-173">대상 Azure 클라우드 환경을 정의합니다. 이 예에서는 `AZURE`입니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-173">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="ef73a-174">(환경의 전체 목록은 [Azure Web Apps의 Maven 플러그 인] 설명서에서 제공됩니다.)</span><span class="sxs-lookup"><span data-stu-id="ef73a-174">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span> |


4. <span data-ttu-id="ef73a-175">*settings.xml* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-175">Save and close the *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a><span data-ttu-id="ef73a-176">Docker 컨테이너 이미지 빌드 및 Azure Container Registry에 푸시</span><span class="sxs-lookup"><span data-stu-id="ef73a-176">Build your Docker container image and push it to your Azure container registry</span></span>

1. <span data-ttu-id="ef73a-177">Spring Boot 응용 프로그램의 완료된 프로젝트 디렉터리로 이동합니다. (예: "*C:\SpringBoot\gs-spring-boot-docker\complete*" 또는 "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") 텍스트 편집기를 사용하여 *pom.xml* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-177">Navigate to the completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

2. <span data-ttu-id="ef73a-178">*pom.xml* 파일의 `<properties>` 컬렉션을 이 자습서의 이전 섹션에서 사용한 Azure Container Registry의 로그인 서버 값으로 업데이트합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="ef73a-178">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="ef73a-179">위치:</span><span class="sxs-lookup"><span data-stu-id="ef73a-179">Where:</span></span>

   |           <span data-ttu-id="ef73a-180">요소</span><span class="sxs-lookup"><span data-stu-id="ef73a-180">Element</span></span>           |                                                                       <span data-ttu-id="ef73a-181">설명</span><span class="sxs-lookup"><span data-stu-id="ef73a-181">Description</span></span>                                                                       |
   |-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
   | `<azure.containerRegistry>` |                                              <span data-ttu-id="ef73a-182">개인 Azure Container Registry의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-182">Specifies the name of your private Azure container registry.</span></span>                                               |
   |   `<docker.image.prefix>`   | <span data-ttu-id="ef73a-183">개인 컨테이너 레지스트리의 이름에 ".azurecr.io"를 추가하여 파생되는 개인 Azure Container Registry의 URL을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-183">Specifies the URL of your private Azure container registry, which is derived by appending ".azurecr.io" to the name of your private container registry.</span></span> |


3. <span data-ttu-id="ef73a-184">*pom.xml* 파일에서 Docker 플러그 인의 `<plugin>`이 이 자습서의 이전 단계에서 로그인 서버 주소 및 레지스트리 이름에 대한 올바른 속성을 포함하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-184">Verify that `<plugin>` for the Docker plugin in your *pom.xml* file contains the correct properties for the login server address and registry name from the previous step in this tutorial.</span></span> <span data-ttu-id="ef73a-185">예: </span><span class="sxs-lookup"><span data-stu-id="ef73a-185">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="ef73a-186">위치:</span><span class="sxs-lookup"><span data-stu-id="ef73a-186">Where:</span></span>

   |     <span data-ttu-id="ef73a-187">요소</span><span class="sxs-lookup"><span data-stu-id="ef73a-187">Element</span></span>     |                                       <span data-ttu-id="ef73a-188">설명</span><span class="sxs-lookup"><span data-stu-id="ef73a-188">Description</span></span>                                       |
   |-----------------|-----------------------------------------------------------------------------------------|
   |  `<serverId>`   |  <span data-ttu-id="ef73a-189">개인 Azure Container Registry의 이름을 포함하는 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-189">Specifies the property which contains name of your private Azure container registry.</span></span>   |
   | `<registryUrl>` | <span data-ttu-id="ef73a-190">개인 Azure Container Registry의 URL을 포함하는 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-190">Specifies the property which contains the URL of your private Azure container registry.</span></span> |


4. <span data-ttu-id="ef73a-191">Spring Boot 응용 프로그램의 완성된 프로젝트 디렉터리로 이동하고 다음 명령을 실행하여 응용 프로그램을 다시 빌드하고 Azure Container Registry에 컨테이너를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-191">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

5. <span data-ttu-id="ef73a-192">선택 사항: [Azure Portal]로 이동하고 컨테이너 레지스트리에서 **gs-spring-boot-docker**라는 Docker 컨테이너 이미지가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-192">OPTIONAL: Browse to the [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Azure Portal에서 컨테이너 확인][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a><span data-ttu-id="ef73a-194">pom.xml을 사용자 지정하고 컨테이너를 Azure에 빌드하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-194">Customize your pom.xml, then build and deploy your container to Azure</span></span>

<span data-ttu-id="ef73a-195">텍스트 편집기에서 Spring Boot 응용 프로그램에 대한 `pom.xml` 파일을 열고 `azure-webapp-maven-plugin`에 대한 `<plugin>` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-195">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="ef73a-196">이 요소는 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-196">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="ef73a-197">Maven 플러그 인에 대해 수정할 수 있는 여러 값이 있으며 이러한 각 요소에 대한 자세한 설명을 [Azure Web Apps의 Maven 플러그 인] 설명서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-197">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="ef73a-198">즉, 이 문서에서 강조 표시된 값은 여러 개입니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-198">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="ef73a-199">요소</span><span class="sxs-lookup"><span data-stu-id="ef73a-199">Element</span></span> | <span data-ttu-id="ef73a-200">설명</span><span class="sxs-lookup"><span data-stu-id="ef73a-200">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="ef73a-201">[Azure Web Apps의 Maven 플러그 인] 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-201">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="ef73a-202">[Maven 중앙 리포지토리](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22)에 나열된 버전을 검사하여 최신 버전을 사용하고 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-202">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<authentication>` | <span data-ttu-id="ef73a-203">Azure에 대한 인증 정보를 지정합니다. 이 예제에서는 `azure-auth`이 포함된 `<serverId>` 요소를 포함합니다. Maven에서는 해당 값을 사용하여 이 문서의 이전 섹션에 정의된 Maven *settings.xml* 파일에서 Azure 서비스 주체 값을 조회합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-203">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="ef73a-204">대상 리소스 그룹, 즉, 이 예에서 `wingtiptoysresources`을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-204">Specifies the target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="ef73a-205">리소스 그룹이 아직 존재하지 않는 경우 배포 중에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-205">The resource group will be created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="ef73a-206">웹앱에 대한 대상 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-206">Specifies the target name for your web app.</span></span> <span data-ttu-id="ef73a-207">이 예제에서는 대상 이름은 `maven-linux-app-${maven.build.timestamp}`이며 이 예제에서 충돌을 피하기 위해 여기에 `${maven.build.timestamp}` 접미사가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-207">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="ef73a-208">(타임스탬프는 선택 사항입니다. 앱 이름에 대한 고유한 문자열을 지정할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="ef73a-208">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="ef73a-209">대상 지역을 지정합니다. 이 예제에서는 `westus`입니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-209">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="ef73a-210">(전체 목록은 [Azure Web Apps의 Maven 플러그 인] 설명서에서 제공됩니다.)</span><span class="sxs-lookup"><span data-stu-id="ef73a-210">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<containerSettings>` | <span data-ttu-id="ef73a-211">컨테이너의 이름 및 URL을 포함하는 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-211">Specifies the properties which contain the name and URL of your container.</span></span> |
| `<appSettings>` | <span data-ttu-id="ef73a-212">Maven에 대한 고유한 설정을 지정하여 Azure에 웹앱을 배포할 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-212">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="ef73a-213">이 예제에서 `<property>` 요소는 앱에 대한 포트를 지정하는 자식 요소의 이름/값 쌍을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-213">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span> |

> [!NOTE]
>
> <span data-ttu-id="ef73a-214">이 예제에서 기본값의 포트를 변경하는 경우 포트 번호를 변경하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-214">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

1. <span data-ttu-id="ef73a-215">*pom.xml* 파일을 변경한 경우 이전에 사용하던 명령 프롬프트 또는 터미널 창에서 Maven를 사용하여 JAR 파일을 다시 작성합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="ef73a-215">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="ef73a-216">Maven을 사용하여 Azure에 웹앱을 배포합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="ef73a-216">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="ef73a-217">Maven은 Azure에 웹앱을 배포합니다. 웹앱이 아직 없는 경우 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-217">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ef73a-218">*pom.xml* 파일의 `<region>` 요소에서 지정한 지역이 배포를 시작할 때 서버를 충분히 사용할 수 없는 경우 다음 예제와 비슷한 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-218">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="ef73a-219">이 경우에 다른 지역을 지정하고 Maven 명령을 다시 실행하여 응용 프로그램을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-219">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="ef73a-220">웹을 배포하면 [Azure Portal]을 사용하여 작업을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-220">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="ef73a-221">웹앱은 **App Services**에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-221">Your web app will be listed in **App Services**:</span></span>

   ![Azure Portal App Services에 나열된 웹앱][AP01]

* <span data-ttu-id="ef73a-223">웹앱의 URL은 웹앱의 **개요**에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef73a-223">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![웹앱의 URL 확인][AP02]

## <a name="next-steps"></a><span data-ttu-id="ef73a-225">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef73a-225">Next steps</span></span>

<span data-ttu-id="ef73a-226">이 문서에서 설명하는 다양한 기술에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef73a-226">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="ef73a-227">[Azure Web Apps의 Maven 플러그 인]</span><span class="sxs-lookup"><span data-stu-id="ef73a-227">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="ef73a-228">Azure CLI에서 Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="ef73a-228">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="ef73a-229">Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="ef73a-229">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="ef73a-230">Maven 설정 참조</span><span class="sxs-lookup"><span data-stu-id="ef73a-230">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="ef73a-231">[Maven의 Docker 플러그 인]</span><span class="sxs-lookup"><span data-stu-id="ef73a-231">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure CLI(명령줄 인터페이스)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure Portal]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Azure Web Apps의 Maven 플러그 인]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service/containers/tutorial-custom-docker-image
[Docker]: https://www.docker.com/
[Maven의 Docker 플러그 인]: https://github.com/spotify/docker-maven-plugin
[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker 시작]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP02.png
[TL01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/TL01.png
