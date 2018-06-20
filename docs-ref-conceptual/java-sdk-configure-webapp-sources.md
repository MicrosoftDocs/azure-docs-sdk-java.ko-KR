---
title: Java를 사용하여 웹앱 배포 구성 | Microsoft Docs
description: Java용 Azure SDK를 사용하여 Git 또는 FTP Azure App Service 배포를 구성하는 Java 샘플 코드
author: rloutlaw
manager: douge
ms.assetid: 833e9c78-1e50-4c23-a611-f73a2f0c2983
ms.service: Azure
ms.devlang: java
ms.topic: article
ms.date: 03/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 910d1e43c9942d6402aeccb8757ba819b7453dab
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931189"
---
# <a name="configure-azure-app-service-deployment-sources-from-your-java-applications"></a><span data-ttu-id="c520e-103">Java 응용 프로그램에서 Azure App Service 배포 원본 구성</span><span class="sxs-lookup"><span data-stu-id="c520e-103">Configure Azure App Service deployment sources from your Java applications</span></span>

<span data-ttu-id="c520e-104">[이 샘플 ](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel)에서는 각각 서로 다른 배포 원본을 사용하는 단일 [ Azure App Service ](https://docs.microsoft.com/azure/app-service/) 계획에서 네 가지 응용 프로그램에 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-104">[This sample](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) deploys code to four applications in a single [Azure App Service](https://docs.microsoft.com/azure/app-service/) plan, each using a different deployment source.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="c520e-105">샘플 실행</span><span class="sxs-lookup"><span data-stu-id="c520e-105">Run the sample</span></span>

<span data-ttu-id="c520e-106">[인증 파일](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md)을 만들고 컴퓨터에서 파일의 전체 경로가 포함된 `AZURE_AUTH_LOCATION` 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="c520e-107">그런 후 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps.git
cd app-service-java-configure-deployment-sources-for-web-apps
mvn clean compile exec:java
```

<span data-ttu-id="c520e-108">[GitHub에서 전체 샘플 코드(영문)](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java)를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-108">View the [complete sample code on GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="c520e-109">Azure를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="c520e-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-app-service-app-running-apache-tomcat"></a><span data-ttu-id="c520e-110">Apache Tomcat을 실행하는 App Service 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="c520e-110">Create a App Service app running Apache Tomcat</span></span>

```java
// create a new Standard app service plan and create a single Java 8/Tomcat 8 app in it
WebApp app1 = azure.webApps().define(app1Name)
             .withNewResourceGroup(rgName)
             .withNewAppServicePlan(planName)
             .withRegion(Region.US_WEST)
             .withPricingTier(AppServicePricingTier.STANDARD_S1)
             .withJavaVersion(JavaVersion.JAVA_8_NEWEST)
             .withWebContainer(WebContainer.TOMCAT_8_0_NEWEST)
             .create();
```

<span data-ttu-id="c520e-111">`withJavaVersion()` 및 `withWebContainer()`는 Tomcat 8을 사용하여 HTTP 요청을 처리하도록 App Service를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-111">`withJavaVersion()` and `withWebContainer()` configure App Service to serve HTTP requests using Tomcat 8.</span></span>

## <a name="deploy-a-java-application-using-ftp"></a><span data-ttu-id="c520e-112">FTP를 사용하여 Java 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="c520e-112">Deploy a Java application using FTP</span></span>
```java
// pass the PublishingProfile that contains FTP information to a helper method 
uploadFileToFtp(app1.getPublishingProfile(), "helloworld.war", 
      ManageWebAppSourceControl.class.getResourceAsStream("/helloworld.war"));

// Use the FTP classes in the Apache Commons library to connect to Azure using 
// the information from the PublishingProfile
private static void uploadFileToFtp(PublishingProfile profile, String fileName, InputStream file) throws Exception {
        FTPClient ftpClient = new FTPClient();
        String[] ftpUrlSegments = profile.ftpUrl().split("/", 2);
        String server = ftpUrlSegments[0];
        // Tomcat will deploy WAR files uploaded to this directory.
        String path = "./site/wwwroot/webapps"; 

        // FTP the build WAR to Azure
        ftpClient.connect(server);
        ftpClient.login(profile.ftpUsername(), profile.ftpPassword());
        ftpClient.setFileType(FTP.BINARY_FILE_TYPE);
        ftpClient.changeWorkingDirectory(path);
        ftpClient.storeFile(fileName, file);
        ftpClient.disconnect();
}
```

<span data-ttu-id="c520e-113">이 코드는 WAR 파일을 `/site/wwwroot/webapps` 디렉터리에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-113">This code uploads a WAR file to the `/site/wwwroot/webapps` directory.</span></span> <span data-ttu-id="c520e-114">Tomcat은 기본적으로 App Service에서 이 디렉터리에 배치된 WAR 파일을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-114">Tomcat deploys WAR files placed in this directory by default in App Service.</span></span>

## <a name="deploy-a-java-application-from-a-local-git-repo"></a><span data-ttu-id="c520e-115">로컬 Git 리포지토리에서 Java 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="c520e-115">Deploy a Java application from a local Git repo</span></span>

```java
// get the publishing profile from the App Service webapp
PublishingProfile profile = app2.getPublishingProfile();

// create a new Git repo in the sample directory under src/main/resources 
Git git = Git
    .init()
    .setDirectory(new File(ManageWebAppSourceControl.class.getResource("/azure-samples-appservice-helloworld/").getPath()))
    .call();
git.add().addFilepattern(".").call();
// add the files in the sample app to an initial commit
git.commit().setMessage("Initial commit").call(); 

// push the commit using the Azure Git remote URL and credentials in the publishing profile
PushCommand command = git.push();
command.setRemote(profile.gitUrl()); 
command.setCredentialsProvider(new UsernamePasswordCredentialsProvider(profile.gitUsername(), profile.gitPassword()));
command.setRefSpecs(new RefSpec("master:master")); 
command.setForce(true);
command.call();
```      

<span data-ttu-id="c520e-116">이 코드는 [JGit](https://eclipse.org/jgit/) 라이브러리를 사용하여 `src/main/resources/azure-samples-appservice-helloworld` 폴더에 새 Git 리포지토리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-116">This code uses the [JGit](https://eclipse.org/jgit/) libraries to create a new Git repo in the `src/main/resources/azure-samples-appservice-helloworld` folder.</span></span> <span data-ttu-id="c520e-117">그런 다음 샘플에서 폴더의 모든 파일을 초기 커밋에 추가하고 웹앱의 `PublishingProfile`에 있는 Git 배포 정보를 사용하여 커밋을 Azure로 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-117">The sample then adds all files in the folder to an initial commit and pushes the commit to Azure using Git deployment information from the webapp's `PublishingProfile`.</span></span> 

>[!NOTE]
> <span data-ttu-id="c520e-118">리포지토리에 있는 파일의 레이아웃은 Azure App Service에서 `/site/wwwroot/` 디렉터리 아래에 배포된 파일을 원하는 방식과 정확히 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-118">The layout of the files in the repo must match exactly how you want the files deployed under the `/site/wwwroot/` directory in Azure App Service.</span></span>

## <a name="deploy-an-application-from-a-public-git-repo"></a><span data-ttu-id="c520e-119">공용 Git 리포지토리에서 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="c520e-119">Deploy an application from a public Git repo</span></span>

```java
// deploy a .NET sample app from a public GitHub repo into a new webapp
WebApp app3 = azure.webApps().define(app3Name)
                .withNewResourceGroup(rgName)
                .withExistingAppServicePlan(plan)
                .defineSourceControl()
                .withPublicGitRepository(
                   "https://github.com/Azure-Samples/app-service-web-dotnet-get-started")
                .withBranch("master")
                .attach()
                .create();
 ```

 <span data-ttu-id="c520e-120">App Service 런타임에서 리포지토리의 `master` 분기에 있는 최신 코드를 사용하여 .NET 프로젝트를 자동으로 빌드하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-120">The App Service runtime automatically builds and deploys the .NET project using the latest code on the `master` branch of the repo.</span></span>

## <a name="continuous-deployment-from-a-github-repo"></a><span data-ttu-id="c520e-121">GitHub 리포지토리에서 지속적인 배포</span><span class="sxs-lookup"><span data-stu-id="c520e-121">Continuous deployment from a GitHub repo</span></span>

```java
// deploy the application whenever you push a new commit or merge a pull request into your master branch
WebApp app4 = azure.webApps()
                    .define(app4Name)
                    .withExistingResourceGroup(rgName)
                    .withExistingAppServicePlan(plan)
                    // Uncomment the following lines to turn on continuous deployment scenario
                    //.defineSourceControl()
                    //    .withContinuouslyIntegratedGitHubRepository("username", "reponame")
                    //    .withBranch("master")
                    //    .withGitHubAccessToken("YOUR GITHUB PERSONAL TOKEN")
                    //    .attach()
                    .create();
```  

<span data-ttu-id="c520e-122">`username` 및 `reponame` 값은 GitHub에서 사용되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-122">The `username` and `reponame` values are the ones used in GitHub.</span></span> <span data-ttu-id="c520e-123">리포지토리 읽기 권한이 있는 [GitHub 개인용 액세스 토큰을 만들어](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) `withGitHubAccessToken`에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-123">[Create a GitHub personal access token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) with repo read permissions and pass it to `withGitHubAccessToken`.</span></span> 


## <a name="sample-explanation"></a><span data-ttu-id="c520e-124">샘플 설명</span><span class="sxs-lookup"><span data-stu-id="c520e-124">Sample explanation</span></span>

<span data-ttu-id="c520e-125">샘플에서는 새로 만든 [표준](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) App Service 계획에서 실행되는 Java 8 및 Tomcat 8을 사용하여 첫 번째 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-125">The sample creates the first application using Java 8 and Tomcat 8 running in a newly created [Standard](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) App Service plan.</span></span> <span data-ttu-id="c520e-126">그런 다음 코드에서 `PublishingProfile` 개체의 정보를 사용하여 WAR 파일을 FTP로 보내고, Tomcat에서 이를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-126">The code then FTPs a WAR file using the information in the `PublishingProfile` object and Tomcat deploys it.</span></span>

<span data-ttu-id="c520e-127">두 번째 응용 프로그램은 첫 번째 응용 프로그램과 동일한 계획에서 사용되며 Java 8/Tomcat 8 응용 프로그램으로도 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-127">The second application uses in the same plan as the first and is also configured as a Java 8/Tomcat 8 application.</span></span> <span data-ttu-id="c520e-128">JGit 라이브러리에서 App Service에 매핑되는 디렉터리 구조에 압축되지 않은 Java 웹 응용 프로그램을 포함하는 폴더에 새 Git 리포지토리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-128">The JGit libraries create a new Git repository in a folder that contains an unpacked Java web application in a directory structure that maps to App Service.</span></span> <span data-ttu-id="c520e-129">새 커밋에서 새 Git 리포지토리에 폴더의 파일들을 추가하고, Git에서는 웹앱의 `PublishingProfile`에서 제공하는 원격 URL과 사용자 이름/암호를 사용하여 커밋을 Azure로 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-129">A new commit adds the files in the folder to the new Git repo, and Git pushes the commit to Azure with a remote URL and username/password provided by the webapp's `PublishingProfile`.</span></span>

<span data-ttu-id="c520e-130">세 번째 응용 프로그램은 Java 및 Tomcat용으로 구성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-130">The third application is not configured for Java and Tomcat.</span></span> <span data-ttu-id="c520e-131">대신 공용 GitHub 리포지토리의 .NET 샘플은 원본에서 직접 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-131">Instead, a .NET sample in a public GitHub repo is deployed directly from source.</span></span>

<span data-ttu-id="c520e-132">네 번째 응용 프로그램은 변경 내용을 푸시하거나 GitHub 리포지토리의 마스터 분기로 끌어오기 요청을 병합할 때마다 마스터 분기에 코드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-132">The fourth application deploys the code in your master branch every time you push changes or merge a pull request into the GitHub repo's master branch.</span></span>

| <span data-ttu-id="c520e-133">샘플에 사용되는 클래스</span><span class="sxs-lookup"><span data-stu-id="c520e-133">Class used in sample</span></span> | <span data-ttu-id="c520e-134">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c520e-134">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="c520e-135">WebApp</span><span class="sxs-lookup"><span data-stu-id="c520e-135">WebApp</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_app) | <span data-ttu-id="c520e-136">`azure.webApps().define()....create()` 흐름 체인에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-136">Created from the `azure.webApps().define()....create()` fluent chain.</span></span> <span data-ttu-id="c520e-137">App Service 웹앱과 앱에 필요한 모든 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-137">Creates a App Service web app and any resources needed for the app.</span></span> <span data-ttu-id="c520e-138">대부분의 메서드는 구성 세부 정보에 대한 개체를 쿼리하지만, `restart()`와 같은 동사 메서드는 웹앱의 상태를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-138">Most methods query the object for configuration details, but verb methods like `restart()` change the state of the webapp.</span></span>
| [<span data-ttu-id="c520e-139">WebContainer</span><span class="sxs-lookup"><span data-stu-id="c520e-139">WebContainer</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_container) | <span data-ttu-id="c520e-140">Java 웹 컨테이너를 실행하는 WebApp을 정의할 때 `withWebContainer()`에 대한 매개 변수로 사용되는 정적 공용 필드가 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-140">Class with static public fields used as paramters to `withWebContainer()` when defining a WebApp running a Java webcontainer.</span></span> <span data-ttu-id="c520e-141">Jetty 및 Tomcat 버전을 모두 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-141">Has choices for both Jetty and Tomcat versions.</span></span>
| [<span data-ttu-id="c520e-142">PublishingProfile</span><span class="sxs-lookup"><span data-stu-id="c520e-142">PublishingProfile</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._publishing_profile) | <span data-ttu-id="c520e-143">`getPublishingProfile()` 메서드를 사용하여 WebApp 개체를 통해 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-143">Obtained through a WebApp object using the `getPublishingProfile()` method.</span></span> <span data-ttu-id="c520e-144">배포 사용자 이름 및 암호(Azure 계정 또는 서비스 사용자 자격 증명과는 별개임)를 포함한 FTP 및 Git 배포 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-144">Contains FTP and Git deployment information, including deployment username and password (which is separate from Azure account or service principal credentials).</span></span>
| [<span data-ttu-id="c520e-145">AppServicePlan</span><span class="sxs-lookup"><span data-stu-id="c520e-145">AppServicePlan</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_plan) | <span data-ttu-id="c520e-146">`azure.appServices().appServicePlans().getByResourceGroup()`에서 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-146">Returned by `azure.appServices().appServicePlans().getByResourceGroup()`.</span></span> <span data-ttu-id="c520e-147">메서드는 계획에서 실행되는 웹앱의 용량, 계층 및 수를 확인하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-147">Methods are availble to check the capacity, tier, and number of web apps running in the plan.</span></span>
| [<span data-ttu-id="c520e-148">AppServicePricingTier</span><span class="sxs-lookup"><span data-stu-id="c520e-148">AppServicePricingTier</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_pricing_tier) | <span data-ttu-id="c520e-149">App Service 계층을 나타내는 정적 공용 필드가 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-149">Class with static public fields representing App Service tiers.</span></span> <span data-ttu-id="c520e-150">`withPricingTier()`를 사용하여 앱을 만드는 동안 또는 `azure.appServices().appServicePlans().define()`을 통해 계획을 정의할 때 직접 계획 계층 인라인을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-150">Used to define a plan tier in-line during app creation with `withPricingTier()` or directly when defining a plan via `azure.appServices().appServicePlans().define()`</span></span>
| [<span data-ttu-id="c520e-151">JavaVersion</span><span class="sxs-lookup"><span data-stu-id="c520e-151">JavaVersion</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._java_version) | <span data-ttu-id="c520e-152">App Service에서 지원하는 Java 버전을 나타내는 정적 공용 필드가 있는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-152">Class with static public fields representing Java versions supported by App Service.</span></span> <span data-ttu-id="c520e-153">새 웹앱을 만들 때 `define()...create()` 체인에서 `withJavaVersion()`과 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c520e-153">Used with `withJavaVersion()` during the `define()...create()` chain when creating a new webapp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c520e-154">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c520e-154">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]