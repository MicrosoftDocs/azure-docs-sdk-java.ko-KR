---
title: Java용 Azure 라이브러리 시작
description: Azure 클라우드 리소스를 만들어 연결하여 Java 애플리케이션에서 사용하는 방법에 대해 알아봅니다.
keywords: Azure, Java, SDK, API, 인증, 시작
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: get-started-article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: b1e10b79-f75e-4605-aecd-eed64873e2d3
ms.openlocfilehash: fdf0334a8796d636a1968943cc34d7ae98d6361c
ms.sourcegitcommit: c2019ba6da6c7c28b17b5a85f89e49bb5e570ba4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "44040261"
---
# <a name="get-started-with-cloud-development-using-java-on-azure"></a><span data-ttu-id="9af03-104">Azure 에서 Java를 이용하여 클라우드 개발 시작</span><span class="sxs-lookup"><span data-stu-id="9af03-104">Get started with cloud development using Java on Azure</span></span>

<span data-ttu-id="9af03-105">이 가이드에서는 Java에서 Azure 개발을 위한 개발 환경 설정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-105">This guide walks you through setting up a development environment for Azure development in Java.</span></span> <span data-ttu-id="9af03-106">그런 다음, 몇 가지 Azure 리소스를 만들고 연결하여 파일 업로드, 웹 애플리케이션 배포 같은 기본 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-106">You'll then create some Azure resources and connect them to to perform some basic tasks, like uploading a file or deploying a web application.</span></span> <span data-ttu-id="9af03-107">마치고 나면 자체 Java 애플리케이션에서 Azure Services를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-107">When you're done, you'll be ready to start using Azure services in your own Java applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9af03-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9af03-108">Prerequisites</span></span>

- <span data-ttu-id="9af03-109">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="9af03-109">An Azure account.</span></span> <span data-ttu-id="9af03-110">계정이 없으면 [체험 계정을 얻습니다](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9af03-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>
- <span data-ttu-id="9af03-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) 또는 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="9af03-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>
- <span data-ttu-id="9af03-112">[Java 8](https://www.azul.com/downloads/zulu/)(Azure Cloud Shell에 포함되어 있음)</span><span class="sxs-lookup"><span data-stu-id="9af03-112">[Java 8](https://www.azul.com/downloads/zulu/) (included in Azure Cloud Shell)</span></span>
- <span data-ttu-id="9af03-113">[Maven 3](http://maven.apache.org/download.cgi)(Azure Cloud Shell에 포함되어 있음)</span><span class="sxs-lookup"><span data-stu-id="9af03-113">[Maven 3](http://maven.apache.org/download.cgi) (included in Azure Cloud Shell)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="9af03-114">인증 설정</span><span class="sxs-lookup"><span data-stu-id="9af03-114">Set up authentication</span></span>

<span data-ttu-id="9af03-115">이 자습서에서 샘플 코드를 실행하려면 Azure 구독에 대한 읽기 및 만들기 권한이 Java 애플리케이션에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-115">Your Java application needs read and create permissions in your Azure subscription to run the sample code in this tutorial.</span></span> <span data-ttu-id="9af03-116">서비스 사용자를 만들고 해당 자격 증명을 사용하여 실행되도록 애플리케이션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-116">Create a service principal and configure your application to run with its credentials.</span></span> <span data-ttu-id="9af03-117">서비스 사용자는 앱에서 실행하는 데 필요한 권한만 부여하는 ID와 연결되는 비대화형 계정을 만드는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-117">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="9af03-118">[Azure CLI 2.0을 사용하여 서비스 사용자를 만들고](/cli/azure/create-an-azure-service-principal-azure-cli) 출력을 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-118">[Create a service principal using the Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli) and capture the output.</span></span> <span data-ttu-id="9af03-119">암호 인수에 `MY_SECURE_PASSWORD` 대신 [보안 암호](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-119">Provide a [secure password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) in the password argument instead of `MY_SECURE_PASSWORD`.</span></span> <span data-ttu-id="9af03-120">암호는 8~16자이고 다음 4개 기준 중 3개 이상에 부합해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-120">Your password must be 8 to 16 characters and match at least 3 out of the 4 following criteria:</span></span>

* <span data-ttu-id="9af03-121">소문자 포함</span><span class="sxs-lookup"><span data-stu-id="9af03-121">Include lowercase characters</span></span>
* <span data-ttu-id="9af03-122">대문자 포함</span><span class="sxs-lookup"><span data-stu-id="9af03-122">Include uppercase characters</span></span>
* <span data-ttu-id="9af03-123">숫자 포함</span><span class="sxs-lookup"><span data-stu-id="9af03-123">Include numbers</span></span>
* <span data-ttu-id="9af03-124">@ # $ % ^ & \*-_! 기호 중 하나 포함</span><span class="sxs-lookup"><span data-stu-id="9af03-124">Include one of the following symbols: @ # $ % ^ & \* - _ !</span></span> <span data-ttu-id="9af03-125">+ = [ ] { } | \ : ‘ , .</span><span class="sxs-lookup"><span data-stu-id="9af03-125">+ = [ ] { } | \ : ‘ , .</span></span> <span data-ttu-id="9af03-126">?</span><span class="sxs-lookup"><span data-stu-id="9af03-126">?</span></span> <span data-ttu-id="9af03-127">/ \` ~ “ ( ) ;</span><span class="sxs-lookup"><span data-stu-id="9af03-127">/ \` ~ “ ( ) ;</span></span>


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

<span data-ttu-id="9af03-128">다음 형식으로 답장 제공:</span><span class="sxs-lookup"><span data-stu-id="9af03-128">Which gives you a reply in the following format:</span></span>

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

<span data-ttu-id="9af03-129">다음으로 시스템의 텍스트 파일에 다음 예제를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-129">Next, copy the following into a text file on your system:</span></span>

```text
# sample management library properties file
subscription=ssssssss-ssss-ssss-ssss-ssssssssssss
client=cccccccc-cccc-cccc-cccc-cccccccccccc
key=kkkkkkkkkkkkkkkk
tenant=tttttttt-tttt-tttt-tttt-tttttttttttt
managementURI=https\://management.core.windows.net/
baseURL=https\://management.azure.com/
authURL=https\://login.windows.net/
graphURL=https\://graph.windows.net/
```

<span data-ttu-id="9af03-130">상위 4개 값을 다음과 같이 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-130">Replace the top four values with the following:</span></span>

- <span data-ttu-id="9af03-131">subscription: Azure CLI 2.0에서 `az account show`의 *id* 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-131">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="9af03-132">client: 서비스 사용자 출력에서 가져온 출력의 *appId* 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-132">client: use the *appId* value from the output taken from a service principal output.</span></span>
- <span data-ttu-id="9af03-133">key: 서비스 사용자 출력의 *password* 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-133">key: use the *password* value from the service principal output.</span></span>
- <span data-ttu-id="9af03-134">tenant: 서비스 사용자 출력의 *tenant* 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-134">tenant: use the *tenant* value from the service principal output.</span></span>

<span data-ttu-id="9af03-135">코드에서 읽을 수 있는 시스템의 안전한 위치에 JSON 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-135">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="9af03-136">향후 코드에서 이 파일을 사용할 수 있으므로 이 문서에서 애플리케이션의 외부에 저장해 두는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-136">You may use this file for future code so it's recommended to store it somewhere external to the application in this article.</span></span>

<span data-ttu-id="9af03-137">셸에서 인증 파일의 전체 경로가 포함된 `AZURE_AUTH_LOCATION` 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-137">Set an environment variable `AZURE_AUTH_LOCATION` with the full path to the authentication file in your shell.</span></span>   

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="9af03-138">Windows 환경에서 작업할 경우 변수를 시스템 속성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-138">If you're working in a windows environment, add the variable to your system properties.</span></span> <span data-ttu-id="9af03-139">관리자 권한으로 PowerShell 창을 열고 두 번째 변수를 파일 경로로 바꾼 후 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-139">Open a PowerShell window with administrator privledges and, after replacing the second variable with the path to your file, enter the following command:</span></span>

```powershell
setx AZURE_AUTH_LOCATION "C:\<fullpath>\azureauth.properties" /m
```

## <a name="tooling"></a><span data-ttu-id="9af03-140">도구</span><span class="sxs-lookup"><span data-stu-id="9af03-140">Tooling</span></span>

### <a name="create-a-new-maven-project"></a><span data-ttu-id="9af03-141">새 Maven 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="9af03-141">Create a new Maven project</span></span>

> [!NOTE]
> <span data-ttu-id="9af03-142">이 가이드에서는 Maven 빌드 도구를 사용하여 샘플 코드를 빌드하고 실행하지만, Gradle과 같은 다른 빌드 도구도 Java용 Azure 라이브러리에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-142">This guide uses Maven build tool to build and run the sample code, but other build tools such as Gradle also work with the Azure libraries for Java.</span></span> 

<span data-ttu-id="9af03-143">명령줄에서 시스템의 새 디렉터리에 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-143">Create a Maven project from the command line in a new directory on your system:</span></span>

```
mkdir java-azure-test
cd java-azure-test
mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=AzureApp  \ 
-DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

<span data-ttu-id="9af03-144">이렇게 하면 `testAzureApp` 폴더 아래에 기본 Maven 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-144">This creates a basic Maven project under the `testAzureApp` folder.</span></span> <span data-ttu-id="9af03-145">`pom.xml` 프로젝트에 다음 항목을 추가하여 이 자습서의 샘플 코드에서 사용되는 라이브러리를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-145">Add the following entries into the project `pom.xml` to import the libraries used in the sample code in this tutorial.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.0.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

<span data-ttu-id="9af03-146">최상위 `project` 요소 아래에 `build` 항목을 추가하여 [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/)을 통해 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-146">Add a `build` entry under the top-level `project` element to use the [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/) to run the samples:</span></span>

```XML
<build>
    <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.AzureApp</mainClass>
            </configuration>
        </plugin>
    </plugins>
</build>
 ```

### <a name="install-the-azure-toolkit-for-intellij"></a><span data-ttu-id="9af03-147">IntelliJ용 Azure 도구 키트 설치</span><span class="sxs-lookup"><span data-stu-id="9af03-147">Install the Azure Toolkit for Intellij</span></span>

<span data-ttu-id="9af03-148">[Azure 도구 키트](intellij/azure-toolkit-for-intellij-installation.md)는 웹앱이나 API를 프로그래밍 방식으로 설치하지만 현재 다른 개발 유형에는 사용하고 있지 않은 경우에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-148">The [Azure toolkit](intellij/azure-toolkit-for-intellij-installation.md) is necessary if you're going to be deploying web apps or APIs programmatically but is not currently used for any other kinds of development.</span></span> <span data-ttu-id="9af03-149">다음은 설치 프로세스에 대한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-149">The following is a summary of the installation process.</span></span> <span data-ttu-id="9af03-150">자세한 절차는 [IntelliJ용 Azure 도구 키트 설치](intellij/azure-toolkit-for-intellij-installation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9af03-150">For detailed stpes, visit [Installing the Azure Toolkit for IntelliJ](intellij/azure-toolkit-for-intellij-installation.md).</span></span>

<span data-ttu-id="9af03-151">**파일** 메뉴를 선택한 다음 **설정...** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-151">Select the **File** menu and then select **Settings...**.</span></span> 

<span data-ttu-id="9af03-152">**저장소 찾아보기...** 를 선택하고 “Azure”를 검색한 다음 **Intellij용 Azure 도구 키트**를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-152">Select **Browse repositories...** and then search "Azure" and install the **Azure toolkit for Intellij**.</span></span>

<span data-ttu-id="9af03-153">Intellij를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-153">Restart Intellij.</span></span>

### <a name="install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="9af03-154">Eclipse용 Azure 도구 키트 설치</span><span class="sxs-lookup"><span data-stu-id="9af03-154">Install the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="9af03-155">[Azure 도구 키트](eclipse/azure-toolkit-for-eclipse.md)는 웹앱이나 API를 프로그래밍 방식으로 설치하지만 현재 다른 개발 유형에는 사용하고 있지 않은 경우에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-155">The [Azure toolkit](eclipse/azure-toolkit-for-eclipse.md) is necessary if you're going to be deploying web apps or APIs programmatically but is not currently used for any other kinds of development.</span></span> <span data-ttu-id="9af03-156">다음은 설치 프로세스에 대한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-156">The following is a summary of the installation process.</span></span> <span data-ttu-id="9af03-157">자세한 절차는 [Eclipse용 Azure 도구 키트 설치](eclipse/azure-toolkit-for-eclipse.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9af03-157">For detailed stpes, visit [Installing the Azure Toolkit for Eclipse](eclipse/azure-toolkit-for-eclipse.md).</span></span>

<span data-ttu-id="9af03-158">**도움말** 메뉴를 선택하고 **새 소프트웨어 설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-158">Select the **Help** menu and then select **Install New software**.</span></span>

<span data-ttu-id="9af03-159">**작업:** 필드에 `http://dl.microsoft.com/eclipse`를 입력하고 Enter를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-159">In the **Work with:** field enter `http://dl.microsoft.com/eclipse` and press enter.</span></span>

<span data-ttu-id="9af03-160">그런 다음 **Java용 Azure 도구 키트** 옆의 확인란을 선택하고 **필요한 소프트웨어를 설치하는 동안 모든 업데이트 사이트 문의** 확인란의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-160">Then, select the checkbox next to **Azure toolkit for Java** and uncheck the checkbox for **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="9af03-161">이제 다음을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-161">Then select next.</span></span>

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="9af03-162">Linux 가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="9af03-162">Create a Linux virtual machine</span></span>

<span data-ttu-id="9af03-163">프로젝트의 `src/main/java/com/fabirkam` 디렉터리에 `AzureApp.java`라는 새 파일을 만들고 다음 코드 블록에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-163">Create a new file named `AzureApp.java` in the project's `src/main/java/com/fabirkam` directory and paste in the following block of code.</span></span> <span data-ttu-id="9af03-164">`userName` 및 `sshKey` 변수를 컴퓨터에 대한 실제 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-164">Update the `userName` and `sshKey` variables with real values for your machine.</span></span> <span data-ttu-id="9af03-165">이 코드에서는 미국 동부 Azure 지역에서 실행되는 `sampleResourceGroup` 리소스 그룹에 `testLinuxVM`이라는 새 Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-165">The code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleResourceGroup` running in the US East Azure region.</span></span>

```java
package com.fabrikam;

import com.microsoft.azure.management.Azure;
import com.microsoft.azure.management.compute.VirtualMachine;
import com.microsoft.azure.management.compute.KnownLinuxVirtualMachineImage;
import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
import com.microsoft.azure.management.appservice.WebApp;
import com.microsoft.azure.management.storage.StorageAccount;
import com.microsoft.azure.management.storage.SkuName;
import com.microsoft.azure.management.storage.StorageAccountKey;
import com.microsoft.azure.management.sql.SqlDatabase;
import com.microsoft.azure.management.sql.SqlServer;
import com.microsoft.azure.management.resources.fluentcore.arm.Region;
import com.microsoft.azure.management.resources.fluentcore.utils.SdkContext;

import com.microsoft.rest.LogLevel;

import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

import java.io.File;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class AzureApp {

    public static void main(String[] args) {

        final String userName = "YOUR_VM_USERNAME";
        final String sshKey = "YOUR_PUBLIC_SSH_KEY";

        try {

            // use the properties file with the service principal information to authenticate
            // change the name of the environment variable if you used a different name in the previous step
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));    
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();
           
            // create a Ubuntu virtual machine in a new resource group 
            VirtualMachine linuxVM = azure.virtualMachines().define("testLinuxVM")
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup("sampleVmResourceGroup")
                    .withNewPrimaryNetwork("10.0.0.0/24")
                    .withPrimaryPrivateIPAddressDynamic()
                    .withoutPrimaryPublicIPAddress()
                    .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                    .withRootUsername(userName)
                    .withSsh(sshKey)
                    .withUnmanagedDisks()
                    .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
                    .create();   

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
}
```

<span data-ttu-id="9af03-166">명령줄에서 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-166">Run the sample from the command line:</span></span>

```
mvn compile exec:java
```

<span data-ttu-id="9af03-167">SDK에서 기본 호출을 Azure REST API로 설정하여 가상 머신 및 해당 리소스를 구성할 때 콘솔에서 일부 REST 요청과 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-167">You'll see some REST requests and responses in the console as the SDK makes the underlying calls to the Azure REST API to configure the virtual machine and its resources.</span></span> <span data-ttu-id="9af03-168">프로그램이 완료되면 Azure CLI 2.0을 사용하여 구독의 가상 머신을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-168">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="9af03-169">코드가 작동하는지 확인했으면 CLI를 사용하여 VM과 해당 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-169">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="9af03-170">GitHub 리포지토리에서 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="9af03-170">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="9af03-171">`AzureApp.java`의 main 메서드를 아래 코드로 바꾸고, 이 코드를 실행하기 전에 `appName` 변수를 고유한 값으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-171">Replace the main method in `AzureApp.java` with the one below, updating the `appName` variable to a unique value before running the code.</span></span> <span data-ttu-id="9af03-172">이 코드에서는 공용 GitHub 리포지토리의 `master` 분기에 있는 웹 애플리케이션을 체험 가격 책정 계층에서 실행되는 새 [Azure App Service 웹앱](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-172">This code deploys a web application from the `master` branch in a public GitHub repo into a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free pricing tier.</span></span>

```java
    public static void main(String[] args) {
        try {

            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            final String appName = "YOUR_APP_NAME";

            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            WebApp app = azure.webApps().define(appName)
                    .withRegion(Region.US_WEST2)
                    .withNewResourceGroup("sampleWebResourceGroup")
                    .withNewWindowsPlan(PricingTier.FREE_F1)
                    .defineSourceControl()
                    .withPublicGitRepository(
                            "https://github.com/Azure-Samples/app-service-web-java-get-started")
                    .withBranch("master")
                    .attach()
                    .create();

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
```

<span data-ttu-id="9af03-173">Maven을 사용하기 전에 다음 코드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-173">Run the code as before using Maven:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="9af03-174">CLI를 사용하여 애플리케이션을 가리키는 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-174">Open a browser pointed to the application using the CLI:</span></span>

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```

<span data-ttu-id="9af03-175">배포를 확인한 후 구독에서 웹앱을 제거하고 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-175">Remove the web app and plan from your subscription once you've verified the deployment.</span></span>

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a><span data-ttu-id="9af03-176">Azure SQL Database에 연결</span><span class="sxs-lookup"><span data-stu-id="9af03-176">Connect to an Azure SQL database</span></span>

<span data-ttu-id="9af03-177">`AzureApp.java`의 현재 main 메서드를 `dbPassword` 변수에 대한 실제 값을 설정하는 아래 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-177">Replace the current main method in `AzureApp.java` with the code below, setting a real value for the `dbPassword` variable.</span></span>
<span data-ttu-id="9af03-178">이 코드에서는 원격 액세스를 허용하는 방화벽 규칙이 있는 새 SQL 데이터베이스를 만든 다음 SQL Database JBDC 드라이버를 사용하여 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-178">This code creates a new SQL database with a firewall rule allowing remote access,  and then connects to it using the SQL Database JBDC driver.</span></span> 

```java

    public static void main(String args[])
    {
        // create the db using the management libraries
        try {
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            final String adminUser = SdkContext.randomResourceName("db",8);
            final String sqlServerName = SdkContext.randomResourceName("sql",10);
            final String sqlDbName = SdkContext.randomResourceName("dbname",8);
            final String dbPassword = "YOUR_PASSWORD_HERE";


            SqlServer sampleSQLServer = azure.sqlServers().define(sqlServerName)
                            .withRegion(Region.US_EAST)
                            .withNewResourceGroup("sampleSqlResourceGroup")
                            .withAdministratorLogin(adminUser)
                            .withAdministratorPassword(dbPassword)
                            .withNewFirewallRule("0.0.0.0","255.255.255.255")
                            .create();

            SqlDatabase sampleSQLDb = sampleSQLServer.databases().define(sqlDbName).create();

            // assemble the connection string to the database
            final String domain = sampleSQLServer.fullyQualifiedDomainName();
            String url = "jdbc:sqlserver://"+ domain + ":1433;" +
                    "database=" + sqlDbName +";" +
                    "user=" + adminUser+ "@" + sqlServerName + ";" +
                    "password=" + dbPassword + ";" +
                    "encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";

            // connect to the database, create a table and insert a entry into it
            Connection conn = DriverManager.getConnection(url);

            String createTable = "CREATE TABLE CLOUD ( name varchar(255), code int);";
            String insertValues = "INSERT INTO CLOUD (name, code ) VALUES ('Azure', 1);";
            String selectValues = "SELECT * FROM CLOUD";
            Statement createStatement = conn.createStatement();
            createStatement.execute(createTable);
            Statement insertStatement = conn.createStatement();
            insertStatement.execute(insertValues);
            Statement selectStatement = conn.createStatement();
            ResultSet rst = selectStatement.executeQuery(selectValues);

            while (rst.next()) {
                System.out.println(rst.getString(1) + " "
                        + rst.getString(2));
            }


        } catch (Exception e) {
            System.out.println(e.getMessage());
            System.out.println(e.getStackTrace().toString());
        }
    }
```
<span data-ttu-id="9af03-179">명령줄에서 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-179">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="9af03-180">그런 다음 CLI를 사용하여 리소스를 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-180">Then clean up the resources using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="9af03-181">새 저장소 계정에 Blob 쓰기</span><span class="sxs-lookup"><span data-stu-id="9af03-181">Write a blob into a new storage account</span></span>

<span data-ttu-id="9af03-182">`AzureApp.java`의 현재 main 메서드를 아래 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-182">Replace the current main method in `AzureApp.java` with the code below.</span></span> <span data-ttu-id="9af03-183">이 코드에서는 [Azure 스토리지 계정](https://docs.microsoft.com/azure/storage/storage-introduction)을 만든 다음 Java용 Azure Storage 라이브러리를 사용하여 클라우드에 새 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-183">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Java to create a new text file in the cloud.</span></span>

```java
public static void main(String[] args) {

    try {

        // use the properties file with the service principal information to authenticate
        // change the name of the environment variable if you used a different name in the previous step
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
                .withLogLevel(LogLevel.BASIC)
                .authenticate(credFile)
                .withDefaultSubscription();

        // create a new storage account
        String storageAccountName = SdkContext.randomResourceName("st",8);
        StorageAccount storage = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_WEST2)
                    .withNewResourceGroup("sampleStorageResourceGroup")
                    .create();

        // create a storage container to hold the file
        List<StorageAccountKey> keys = storage.getKeys();
        final String storageConnection = "DefaultEndpointsProtocol=https;"
                + "AccountName=" + storage.name()
                + ";AccountKey=" + keys.get(0).value()
                + ";EndpointSuffix=core.windows.net";

        CloudStorageAccount account = CloudStorageAccount.parse(storageConnection);
        CloudBlobClient serviceClient = account.createCloudBlobClient();

        // Container name must be lower case.
        CloudBlobContainer container = serviceClient.getContainerReference("helloazure");
        container.createIfNotExists();

        // Make the container public
        BlobContainerPermissions containerPermissions = new BlobContainerPermissions();
        containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
        container.uploadPermissions(containerPermissions);

        // write a blob to the container
        CloudBlockBlob blob = container.getBlockBlobReference("helloazure.txt");
        blob.uploadText("hello Azure");

    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }
    }
}
```

<span data-ttu-id="9af03-184">명령줄에서 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-184">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="9af03-185">Azure Portal 또는 [Azure Storage 탐색기](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs)를 사용하여 스토리지 계정에서 `helloazure.txt` 파일을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-185">You can browse for the `helloazure.txt` file in your storage account through the Azure portal or with [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span></span>

<span data-ttu-id="9af03-186">CLI를 사용하여 저장소 계정을 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-186">Clean up the storage account using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="9af03-187">더 많은 샘플 탐색</span><span class="sxs-lookup"><span data-stu-id="9af03-187">Explore more samples</span></span>

<span data-ttu-id="9af03-188">Java용 Azure 관리 라이브러리를 사용하여 리소스를 관리하고 작업을 자동화하는 방법에 대한 자세한 내용은 [가상 머신](java-sdk-azure-virtual-machine-samples.md), [웹앱](java-sdk-azure-web-apps-samples.md) 및 [SQL 데이터베이스](java-sdk-azure-sql-database-samples.md)에 대한 샘플 코드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9af03-188">To learn more about how to use the Azure management libraries for Java to manage resources and automate tasks, see our sample code for [virtual machines](java-sdk-azure-virtual-machine-samples.md), [web apps](java-sdk-azure-web-apps-samples.md) and [SQL database](java-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference-and-release-notes"></a><span data-ttu-id="9af03-189">참조 및 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="9af03-189">Reference and release notes</span></span>

<span data-ttu-id="9af03-190">[참조](http://docs.microsoft.com/java/api)는 모든 패키지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-190">A [reference](http://docs.microsoft.com/java/api) is available for all packages.</span></span>

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="9af03-191">도움말 가져오기 및 피드백 제공</span><span class="sxs-lookup"><span data-stu-id="9af03-191">Get help and give feedback</span></span>

<span data-ttu-id="9af03-192">[Stack Overflow(영문)](http://stackoverflow.com/questions/tagged/azure+java)의 커뮤니티에 질문을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-192">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span></span> <span data-ttu-id="9af03-193">[GitHub 프로젝트](https://github.com/Azure/azure-sdk-for-java)에서 Java용 Azure 라이브러리에 대한 버그 및 열기 문제를 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="9af03-193">Report bugs and open issues against the Azure libraries for Java on the [project GitHub](https://github.com/Azure/azure-sdk-for-java).</span></span>
