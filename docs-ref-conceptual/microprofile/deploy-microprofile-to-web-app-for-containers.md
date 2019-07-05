---
title: Java 기반 MicroProfile 서비스를 Azure Web App for Containers에 배포합니다.
description: Docker 및 Azure Web App for Containers를 사용하는 MicroProfile 서비스를 배포하는 방법 알아보기
services: container-registry;app-service
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: container-registry;app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 4ecfbf92bc30bc491c991e30111cce8375da7f1a
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533597"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a><span data-ttu-id="ab454-103">Java 기반 MicroProfile 서비스를 Azure Web App for Containers에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-103">Deploy a Java-based MicroProfile service to Azure Web App for Containers</span></span>

<span data-ttu-id="ab454-104">MicroProfile은 작은 Java 애플리케이션을 빌드하여 [Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/)와 같은 서비스에 빠르고 쉽게 배포할 수 있는 훌륭한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-104">MicroProfile is a great way to build exceedingly small Java applications that you can quickly and easily deploy to services such as [Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/).</span></span> <span data-ttu-id="ab454-105">이 자습서에서는 간단한 MicroProfile 기반 마이크로 서비스를 만든 다음에 Docker 컨테이너로 컨테이너화하여 [Azure 컨테이너 레지스트리 인스턴스](https://azure.microsoft.com/services/container-registry/)로 배포하고, Azure Web App for Containers를 사용하여 호스팅하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-105">In this tutorial, you create a simple, MicroProfile-based microservice that you containerize into a Docker container, deploy to an [Azure container registry instance](https://azure.microsoft.com/services/container-registry/), and then host by using Azure Web App for Containers.</span></span>

> [!NOTE]
> <span data-ttu-id="ab454-106">Docker 컨테이너 이미지가 자체 실행 가능(즉, 이미지가 런타임을 포함)한 경우, 이 절차는MicroProfile.io의 모든 구현을 사용하여 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-106">This procedure works with any implementation of MicroProfile.io, as long the Docker container image is self-executable (that is, the image includes the runtime).</span></span>

<span data-ttu-id="ab454-107">이 샘플에서는 [Payara Micro](https://www.payara.fish/payara_micro) 및 [MicroProfile 1.3](https://microprofile.io/)을 사용하여 작은(약 5,000바이트) Java 웹 애플리케이션 요구 사항(WAR) 파일을 만든 다음 이를 약 174MB의 Docker 이미지로 패키지화합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-107">In this sample, you use [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile 1.3](https://microprofile.io/) to create a small (approximately 5,000 bytes) Java web application requirement (WAR) file, and then package it into a Docker image of approximately 174 megabytes (MB).</span></span> <span data-ttu-id="ab454-108">이 Docker 이미지는 이 웹앱의 완전히 컨테이너화된 배포에 필요한 모든 것을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-108">The Docker image contains everything necessary for a fully containerized deployment of the web app.</span></span>

<span data-ttu-id="ab454-109">Docker는 차이점(크기가 훨씬 작음)만 업로드하기 때문에 애플리케이션 소스 코드가 변경될 때마다 전체 174MB Docker 이미지를 다시 배포할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-109">An entire 174 MB Docker image doesn't need to be redeployed whenever the application source code is changed, because Docker uploads only the differences (which are significantly smaller).</span></span> <span data-ttu-id="ab454-110">따라서 CI/CD 파이프라인을 통해 MicroProfile 애플리케이션의 새 릴리스를 실행하는 프로세스가 매우 효율적이고 신속하게 이루어지며 마찰을 줄이고 신속한 개발 반복을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-110">Consequently, the process of executing a new release of a MicroProfile application via a CI/CD pipeline is extremely efficient and quick, reducing friction and enabling rapid development iteration.</span></span>

<span data-ttu-id="ab454-111">먼저 이 자습서를 따라 로컬에서 코드를 생성하고 실행하여, Azure에 웹앱으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-111">You'll work through this tutorial by first creating and running the code locally and then deploying it as a web app on Azure.</span></span> <span data-ttu-id="ab454-112">두 단계 모두에서 작업을 단순화하고 표준화하기 위해 Docker를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-112">In both phases, you can depend on Docker to simplify and standardize your efforts.</span></span> <span data-ttu-id="ab454-113">시작하기 전에 Docker 컨테이너 저장을 위해 Azure 컨테이너 레지스트리 인스턴스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-113">Before you begin, you'll create an Azure container registry instance for storing your Docker containers.</span></span>

## <a name="create-an-azure-container-registry-instance"></a><span data-ttu-id="ab454-114">Azure 컨테이너 레지스트리 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="ab454-114">Create an Azure container registry instance</span></span>

<span data-ttu-id="ab454-115">[Azure Portal](http://portal.azure.com)을 사용하여 Azure 컨테이너 레지스트리 인스턴스를 만들 수 있지만 Azure CLI와 같은 다른 선택 사항도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-115">You can use the [Azure portal](http://portal.azure.com) to create the Azure container registry instance, but there are other choices also, such as the Azure CLI.</span></span> <span data-ttu-id="ab454-116">새 Azure 컨테이너 레지스트리를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-116">To create a new Azure container registry instance, do the following:</span></span>

1. <span data-ttu-id="ab454-117">[Azure Portal](http://portal.azure.com)에 로그인하여 새 Azure 컨테이너 레지스트리 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-117">Sign in to the [Azure portal](http://portal.azure.com) and create a new Azure container registry resource.</span></span> <span data-ttu-id="ab454-118">레지스트리 이름(이 이름은 *pom.xml*에서 `docker.registry`속성으로 설정되어야 함)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-118">Provide a registry name (this name should be set as the `docker.registry` property in the *pom.xml* file).</span></span> <span data-ttu-id="ab454-119">기본값을 원하는 대로 변경한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-119">Change the defaults as you want, and then select **Create**.</span></span>

1. <span data-ttu-id="ab454-120">약 30초 후에 컨테이너 레지스트리 인스턴스가 활성화되면 컨테이너 레지스트리 인스턴스를 선택한 다음 왼쪽 창에서 **액세스 키** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-120">In about 30 seconds, when the container registry instance is live, select the container registry instance and then, in the left pane, select the **Access keys** link.</span></span> 

    <span data-ttu-id="ab454-121">*관리 사용자* 설정을 사용하도록 설정해야 컴퓨터에서 이 컨테이너 레지스트리 인스턴스에 액세스하여 Docker 컨테이너를 컨테이너에 밀어넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-121">Be sure to enable the *admin user* setting, so that you can access this container registry instance from your machines and push Docker containers into it.</span></span> <span data-ttu-id="ab454-122">또한 이렇게 하면 곧 설정할 컨테이너 인스턴스에 대 한 Azure 웹앱에서 액세스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-122">Doing so also enables access from the Azure Web App for Containers instance that you'll set up soon.</span></span>

1. <span data-ttu-id="ab454-123">**액세스 키** 창에서 **사용자 이름** 및 **비밀번호** 값을 복사하여 전역 Maven *settings.xml* 파일에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-123">In the **Access keys** pane, copy the **username** and **password** values and paste them into your global Maven *settings.xml* file.</span></span> <span data-ttu-id="ab454-124">Maven 설정에 대한 자세한 내용은 [Apache Maven Project](https://maven.apache.org/settings.html) 웹 사이트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-124">For more information about Maven settings, go to the [Apache Maven Project](https://maven.apache.org/settings.html) website.</span></span> 

   <span data-ttu-id="ab454-125">참조용으로 예제 *${user.home}/.m2/settings.xml* 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-125">For your reference, here's an example of the *${user.home}/.m2/settings.xml* file:</span></span>

    ```xml
    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          https://maven.apache.org/xsd/settings-1.0.0.xsd">
        <servers>
          <server>
            <id>jogilescr.azurecr.io</id>
            <username>jogilescr</username>
            <password>ojoirshois.this-isn't-real.hrihslirhlishrglih</password>
          </server>
        </servers>
    </settings>
    ```

<span data-ttu-id="ab454-126">컨테이너 레지스트리 인스턴스를 만들었으므로 이제 MicroProfile 애플리케이션을 빌드하고 로컬에서 실행하는 것으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-126">Now that you've created your container registry instance, you can move on to building and running your MicroProfile application locally.</span></span>

## <a name="create-your-microprofile-application"></a><span data-ttu-id="ab454-127">MicroProfile 애플리케이션 만들기</span><span class="sxs-lookup"><span data-stu-id="ab454-127">Create your MicroProfile application</span></span>

<span data-ttu-id="ab454-128">이 예제 코드는 GitHub에서 사용할 수 있는 응용 프로그램 예제를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-128">This example code is based on a sample application that's available on GitHub.</span></span> <span data-ttu-id="ab454-129">컴퓨터에 코드를 복제하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-129">To clone the code onto your machine, enter the following commands:</span></span>

```
git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git

cd microprofile-docker-helloworld
```

<span data-ttu-id="ab454-130">이 디렉터리에는 Maven 빌드 도구가 사용하는 형식으로 프로젝트를 지정하는 데 사용되는 *pom.xml* 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-130">This directory contains a *pom.xml* file that you use to specify the project in the format that's used by the Maven build tool.</span></span> <span data-ttu-id="ab454-131">사용자 고유의 요구에 맞게 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-131">You can edit the file to suit your own needs.</span></span> <span data-ttu-id="ab454-132">특히 Azure 컨테이너 레지스트리 인스턴스를 설정할 때 생성된 `docker.registry` 및 `docker.name` 속성을 `docker.registry` 및 `docker.name` 속성으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-132">In particular, the `docker.registry` and `docker.name` properties should be changed to the `docker.registry` and `docker.name` properties that were created when you set up the Azure container registry instance.</span></span>

<span data-ttu-id="ab454-133">이 디렉터리에서 확인할 다른 파일은 아래에서 재생되는 Dockerfile입니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-133">Another file of note in this directory is the Dockerfile, which is reproduced below:</span></span>

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

<span data-ttu-id="ab454-134">Dockerfile은 Payara 마이크로 Docker 컨테이너를 기반으로 하는 새 Docker 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-134">The Dockerfile creates a new Docker container that's based on the Payara Micro Docker Container.</span></span> <span data-ttu-id="ab454-135">빌드 프로세스의 일부로 생성된 WAR 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-135">It copies in the WAR file that was created as part of your build process.</span></span> <span data-ttu-id="ab454-136">이는 또한 Docker 컨테이너 내에서 실행되면 서비스에 액세스할 수 있도록 8080 포트를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-136">It also exposes port 8080 so that you can access the service after it's up and running within a Docker container.</span></span>

<span data-ttu-id="ab454-137">*src* 디렉터리를 열면 여기서 재현된 `Application` 클래스를 발견하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-137">When you open the *src* directory, you'll eventually discover the `Application` class that's reproduced here:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

<span data-ttu-id="ab454-138">*@ApplicationPath("/api")* 주석은 이 마이크로 서비스에 대한 베이스 엔드포인트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-138">The *@ApplicationPath("/api")* annotation specifies the base endpoint for this microservice.</span></span> <span data-ttu-id="ab454-139">즉, 모든 엔드포인트에 대해 */api*는 특정 REST 엔드포인트에 액세스하는 데 필요한 URL의 나머지 부분의 앞에 옵니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-139">That is, for all endpoints, */api* precedes the rest of the URL that's required to access any specific REST endpoint.</span></span>

<span data-ttu-id="ab454-140">*api* 패키지 내에는 `API`로 명명된 클래스가 있으며 이는 다음 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-140">Inside the *api* package is a class named `API`, which contains the following code:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld.api;

import javax.enterprise.context.ApplicationScoped;
import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;

import static javax.ws.rs.core.MediaType.TEXT_HTML;

@ApplicationScoped
@Path("/")
public class API {

    @GET
    @Path("/helloworld")
    @Produces(TEXT_HTML)
    public String info() {
        return "Hello, world!";
    }
}
```

<span data-ttu-id="ab454-141">*@Path("/ helloworld")* 주석을 사용하면 `Application` 클래스에 지정된 */api*와 결합되면 이 REST 엔드포인트가 */api/helloworld*가 됨을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-141">Through the use of the *@Path("/helloworld")* annotation, you can see that this REST endpoint, when it's combined with the */api* that's specified in the `Application` class, will be */api/helloworld*.</span></span> <span data-ttu-id="ab454-142">HTTP GET 요청을 사용하여 이 엔드포인트를 호출하면 메서드에서 text/html을 생성하며 실제로는 단순히 하드 코딩된 문자열인 "Hello, world!"라는 사실을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-142">When you call this endpoint by using an HTTP GET request, you can see that the method produces text/html and, in fact, it's simply a hard-coded string, "Hello, world!"</span></span>

<span data-ttu-id="ab454-143">지금까지 이 문서에서는 MicroProfile을 사용하여 마이크로 서비스를 만드는 데 필요한 모든 코드에 대해 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-143">So far, this article has covered all the code that's required for you to create a microservice by using MicroProfile.</span></span> <span data-ttu-id="ab454-144">이제 다음을 수행하여 Maven을 사용하여 빌드하고, Docker 컨테이너로 컨테이너화하여 로컬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-144">You can now use Maven to build it, containerize it into a Docker container, and run it locally by doing the following:</span></span>

1. <span data-ttu-id="ab454-145">`mvn clean package`를 실행하고, 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-145">Run `mvn clean package`, and wait until it is complete.</span></span>

1. <span data-ttu-id="ab454-146">`docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-146">Run `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`.</span></span> <span data-ttu-id="ab454-147">예를 들어, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*를 실행하며, 여기서 *\<docker.registry>* 는 *jogilescr.azurecr.io*이며 *\<docker.name>* 은 *samples/docker-helloworld*입니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-147">For example, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, where *\<docker.registry>* is *jogilescr.azurecr.io* and *\<docker.name>* is *samples/docker-helloworld*.</span></span>

1. <span data-ttu-id="ab454-148">웹 브라우저에서 [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) 및 [http://localhost:8080/health](http://localhost:8080/health)에 액세스해 보세요.</span><span class="sxs-lookup"><span data-stu-id="ab454-148">Try to access [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) and [http://localhost:8080/health](http://localhost:8080/health) in your web browser.</span></span> <span data-ttu-id="ab454-149">"Hello, world!"</span><span class="sxs-lookup"><span data-stu-id="ab454-149">If you see the expected "Hello, world!"</span></span> <span data-ttu-id="ab454-150">라는 응답(및 [/health](http://localhost:8080/health) 엔드포인트 상태 관련 정보)이 성공적으로 나타난다면, MicroProfile 애플리케이션이 로컬 컴퓨터에 성공적으로 배포한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-150">response (and health-related information for the [/health](http://localhost:8080/health) endpoint), you've successfully deployed the MicroProfile application on your local machine.</span></span>

## <a name="push-the-container-to-the-azure-container-registry-instance"></a><span data-ttu-id="ab454-151">Azure 컨테이너 레지스트리에 컨테이너 이미지 푸시</span><span class="sxs-lookup"><span data-stu-id="ab454-151">Push the container to the Azure container registry instance</span></span>

<span data-ttu-id="ab454-152">이제 로컬 시스템에서 MicroProfile 애플리케이션을 성공적으로 빌드하고 실행했으므로 이 컨테이너를 컨테이너 레지스트리 인스턴스에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-152">Now that you've successfully built and run your MicroProfile application on your local machine, push this container to your container registry instance.</span></span> 

> [!NOTE]
> <span data-ttu-id="ab454-153">이 문서는 Azure 컨테이너 레지스트리 인스턴스를 사용하지만, *pom.xml* 파일이 관련 위치를 가리키도록 편집되었다면 모든 컨테이너 레지스트리 인스턴스는 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-153">Although this article uses an Azure container registry instance, any container registry instance should work, as long as the *pom.xml* file is edited to point to the relevant location.</span></span>

1. <span data-ttu-id="ab454-154">`mvn clean package`를 실행하여 로컬 Docker 이미지를 클린, 컴파일하고 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-154">To clean, compile, and create a local Docker image, run `mvn clean package`.</span></span>
2. <span data-ttu-id="ab454-155">Azure 컨테이너 레지스트리 인스턴스에 컨테이너를 푸시하려면 `mvn dockerfile:push`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-155">To push the container to the Azure container registry instance, run `mvn dockerfile:push`.</span></span>

<span data-ttu-id="ab454-156">이제 Docker 컨테이너 이미지가 Azure 컨테이너 레지스트리 인스턴스에 업로드되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-156">You now have your Docker container image uploaded to the Azure container registry instance.</span></span> <span data-ttu-id="ab454-157">그러나 아직 실행되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-157">However, it's not yet running.</span></span> <span data-ttu-id="ab454-158">이제 Azure Web App for Containers 인스턴스에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-158">You now have to deploy it to an Azure Web App for Containers instance.</span></span> 

## <a name="create-an-azure-web-app-for-containers-instance"></a><span data-ttu-id="ab454-159">Azure Web App for Containers 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="ab454-159">Create an Azure Web App for Containers instance</span></span>

1. <span data-ttu-id="ab454-160">[Azure Portal](http://portal.azure.com)의 왼쪽 창에서 **웹 + 모바일**을 선택하고 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-160">In the [Azure portal](http://portal.azure.com), in the left pane, select **Web + Mobile**, and then do the following:</span></span>

   <span data-ttu-id="ab454-161">a.</span><span class="sxs-lookup"><span data-stu-id="ab454-161">a.</span></span> <span data-ttu-id="ab454-162">이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-162">Specify a name.</span></span> <span data-ttu-id="ab454-163">이름은 웹앱의 공개 URL이 되므로 쉽게 기억할 수 있는 이름을 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-163">The name will become the public URL of the web app, so it's a good idea to pick a name that you can easily remember.</span></span> <span data-ttu-id="ab454-164">원하는 경우 나중에 사용자 지정 도메인 이름을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-164">You can add a custom domain name later, if you want.</span></span>

   <span data-ttu-id="ab454-165">b.</span><span class="sxs-lookup"><span data-stu-id="ab454-165">b.</span></span> <span data-ttu-id="ab454-166">**컨테이너 구성** 섹션의 **이미지 소스**에서 **Azure Container Registry**를 선택한 다음, 드롭 다운 목록에서 올바른 이미지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-166">In the **Configure container** section, under **Image source**, select **Azure Container Registry** and then, in the drop-down list, select the correct image.</span></span>

   <span data-ttu-id="ab454-167">다.</span><span class="sxs-lookup"><span data-stu-id="ab454-167">c.</span></span> <span data-ttu-id="ab454-168">**시작 파일** 필드에 값을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-168">You don't need to specify a value in the **Startup File** field.</span></span>

1. <span data-ttu-id="ab454-169">인스턴스를 만든 후 선택한 다음 **애플리케이션 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-169">After you've created the instance, select it, and then select **Application Settings**.</span></span> <span data-ttu-id="ab454-170">**키**에 **WEBSITES_PORT**를 입력, **값**에 **8080**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-170">For **Key**, enter **WEBSITES_PORT**, and for **Value**, enter **8080**.</span></span> <span data-ttu-id="ab454-171">이러한 설정은 어떤 포트를 컨테이너에 노출할 것인지와 이를 외부적으로 80 포트에 매핑할 것을 Azure에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-171">These settings tell Azure which port to expose in the container and to map it to port 80 externally.</span></span>

1. <span data-ttu-id="ab454-172">(선택 사항) **Docker 컨테이너** 링크를 선택한 다음 **지속적인 배포**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-172">(Optional) Select the **Docker Container** link, and then enable **Continuous Deployment**.</span></span> <span data-ttu-id="ab454-173">이렇게 하면 Azure 컨테이너 레지스트리 인스턴스 이미지를 업데이트할 때마다 Azure Web App for Containers 인스턴스에서 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-173">By doing so, whenever you update the Azure container registry instance image, it's automatically updated in the Azure Web App for Containers instance.</span></span>

1. <span data-ttu-id="ab454-174">이제 `http://<appname>.azurewebsites.net/microprofile/api/helloworld`, `http://<appname>.azurewebsites.net/health`에서 Azure 호스트 인스턴스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-174">You should now be able to access the Azure-hosted instances at `http://<appname>.azurewebsites.net/microprofile/api/helloworld` and `http://<appname>.azurewebsites.net/health`.</span></span>

## <a name="summary"></a><span data-ttu-id="ab454-175">요약</span><span class="sxs-lookup"><span data-stu-id="ab454-175">Summary</span></span>

<span data-ttu-id="ab454-176">이 자습서를 통해 간단한 MicroProfile 기반의 마이크로 서비스를 생성하고 Docker 컨테이너로 컨테이너화한 다음 로컬로 실행하여 Azure에 게시했습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-176">In this tutorial, you've stepped through the process of creating a simple MicroProfile-based microservice, containerized it into a Docker container, run it locally, and published it to Azure.</span></span> <span data-ttu-id="ab454-177">유용한 추가 기능을 제공하려면 마이크로 서비스를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-177">You can extend your microservice to provide additional useful functionality.</span></span> <span data-ttu-id="ab454-178">자세한 내용은 [MicroProfile.io](https://microprofile.io/)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ab454-178">For more information, go to [MicroProfile.io](https://microprofile.io/).</span></span>
