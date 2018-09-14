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
ms.openlocfilehash: 1eb0e7d7a718a1c106adebbf89011f6e3fa1504e
ms.sourcegitcommit: c2019ba6da6c7c28b17b5a85f89e49bb5e570ba4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "44040251"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a><span data-ttu-id="0e938-103">Java 기반 MicroProfile 서비스를 Azure Web App for Containers에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-103">Deploy a Java-based MicroProfile service to Azure Web App for Containers</span></span>

<span data-ttu-id="0e938-104">MicroProfile은 매우 작은 Java 응용 프로그램을 빌드하여 [Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/)와 같은 서비스에 빠르고 쉽게 배포할 수 있는 훌륭한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-104">MicroProfile is a great way to build exceedingly tiny Java applications that can be quickly and easily deployed to services such as [Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/).</span></span> <span data-ttu-id="0e938-105">이 자습서에서는 간단한 MicroProfile 기반 마이크로 서비스를 만든 다음에 Docker 컨테이너로 컨테이너화하여 [Azure Container Registry](https://azure.microsoft.com/services/container-registry/)로 배포하고, Azure Web App for Containers를 사용하여 호스팅하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-105">In this tutorial we will create a simple MicroProfile-based microservice that is then containerized into a Docker container, deployed into an [Azure Container Registry](https://azure.microsoft.com/services/container-registry/), and then hosted using Azure Web App for Containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="0e938-106">Docker 컨테이너 이미지가 자체 실행 가능(즉, 런타임을 포함)한 경우, 이 절차는MicroProfile.io의 모든 구현을 사용하여 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-106">This procedure works with any implementation of MicroProfile.io as long the Docker container image is self-executable (i.e. includes the runtime).</span></span>

<span data-ttu-id="0e938-107">더 구체적으로는, 이 예제에서는 [Payara Micro](https://www.payara.fish/payara_micro) 및 [MicroProfile 1.3](https://microprofile.io/)을 사용하여 매우 작은 Java war 파일(작성자 컴퓨터에서 5,085 바이트)을 만들고 Docker 이미지(약 174 메가바이트)로 패키지화합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-107">More concretely, this sample makes use of [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile 1.3](https://microprofile.io/) to create a tiny Java war file (5,085 bytes on the authors machine), and then packages it up into a Docker image (which is approximately 174 megabytes).</span></span> <span data-ttu-id="0e938-108">이 Docker 이미지는 이 웹앱의 완전히 컨테이너화된 배포에 필요한 모든 것을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-108">This Docker image contains everything necessary for a fully-containerised deployment of this webapp.</span></span>

<span data-ttu-id="0e938-109">Docker가 작동하는 방식 때문에 Docker가 차이점(매우 작음)을 업로드하기 때문에 응용 프로그램 소스 코드가 변경될 때마다 전체 174 메가 바이트 Docker 이미지를 다시 배포할 필요가 없는 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-109">Because of the way Docker works, it is often the case that the entire 174 megabyte Docker image does not need to be redeployed whenever the application source code is changed, as Docker will only upload the differences (which is significantly smaller).</span></span> <span data-ttu-id="0e938-110">따라서 CI/CD 파이프라인을 통해 MicroProfile 응용 프로그램의 새 릴리스를 실행하는 프로세스가 매우 효율적이고 신속하게 이루어지며 마찰을 줄이고 신속한 개발 반복을 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-110">This makes the process of executing a new release of a MicroProfile application via a CI/CD pipeline extremely efficient and quick, reducing friction and enabling rapid development iteration.</span></span>

<span data-ttu-id="0e938-111">먼저 로컬에서 코드를 생성하고 실행하여 이 자습서를 수행한 다음, Azure에 웹앱으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-111">We will work through this tutorial firstly by creating and running the code locally, and then we will deploy this as a web app on Azure.</span></span> <span data-ttu-id="0e938-112">두 경우 모두에서 작업을 단순화하고 표준화하기 위해 Docker를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-112">In both cases we will depend on Docker to simplify and standardize our efforts.</span></span> <span data-ttu-id="0e938-113">시작하기 전에 Docker 컨테이너를 저장하기 위해 Azure Container Registry를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-113">Before we begin, we will create an Azure Container Registry to store our Docker containers in.</span></span>

## <a name="creating-an-azure-container-registry"></a><span data-ttu-id="0e938-114">Azure Container Registry 만들기</span><span class="sxs-lookup"><span data-stu-id="0e938-114">Creating an Azure Container Registry</span></span>

<span data-ttu-id="0e938-115">Azure Container Registry를 만들기 위해 [Azure Portal](http://portal.azure.com)을 사용할 것이지만 Azure CLI와 같은 다른 선택 사항이 있음에 유의하십시오.</span><span class="sxs-lookup"><span data-stu-id="0e938-115">We will use the [Azure Portal](http://portal.azure.com) for creating the Azure Container Registry, but note that there are alternate choices such as the Azure CLI.</span></span> <span data-ttu-id="0e938-116">새 Azure Container Registry를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-116">Follow the steps below to create a new Azure Container Registry:</span></span>

1. <span data-ttu-id="0e938-117">[Azure Portal](http://portal.azure.com)에 로그인하여 새 Azure 컨테이너 레지스트리 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-117">Log in to the [Azure Portal](http://portal.azure.com) and create a new Azure Container Registry resource.</span></span> <span data-ttu-id="0e938-118">레지스트리 이름(이 이름은 `pom.xml`에서 `docker.registry`속성으로 설정해야 함에 유의합니다)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-118">Provide a registry name (note that this is the name that should be set as the `docker.registry` property in `pom.xml`).</span></span> <span data-ttu-id="0e938-119">기본값을 원하는 대로 변경한 다음 '만들기'를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-119">Change the defaults as you wish, and then click 'create'.</span></span>

1. <span data-ttu-id="0e938-120">컨테이너 레지스트리가 실행되면('작성'을 클릭한 후 약 30초 후), 컨테이너 레지스트리를 클릭하고 왼쪽 메뉴 영역의 '액세스 키' 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-120">Once the container registry is live (which is about 30 seconds after clicking 'create'), click on the container registry, and click on the 'Access keys' link in the left-menu area.</span></span> <span data-ttu-id="0e938-121">여기에서 '관리 사용자' 설정을 활성화하여, 이 컨테이너 레지스트리를 컴퓨터(Docker 컨테이너 푸시)에서 액세스하고 또한 곧 설치할 Azure Web Apps for Containers 인스턴스에서 액세스할 수 있도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-121">In here, you need to enable the 'admin user' setting, so that this container registry can be accessed from our machines (to push docker containers into), and also to enable access from the Azure Web Apps for Containers instance we will setup soon.</span></span>

1. <span data-ttu-id="0e938-122">'액세스 키' 영역에 있는 동안, `username` 및 `password` 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-122">Whilst you are in the 'Access keys' area, note the `username` and `password` values.</span></span> <span data-ttu-id="0e938-123">이것들을 우리의 글로벌 Maven `settings.xml` 파일에 복사하여 붙여넣을 것입니다(Maven 설정에 대한 자세한 정보는 [Apache Maven Project](https://maven.apache.org/settings.html) 웹 사이트를 참조합니다).</span><span class="sxs-lookup"><span data-stu-id="0e938-123">We will copy / paste these into our global Maven `settings.xml` file  (for more information on Maven settings, refer to the [Apache Maven Project](https://maven.apache.org/settings.html) website).</span></span> <span data-ttu-id="0e938-124">참조를 위해, 작성자 시스템에 `${user.home}/.m2/settings.xml` 파일의 난독 처리된 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-124">For reference, here is an obfuscated version of the `${user.home}/.m2/settings.xml` file on the authors system:</span></span>

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

<span data-ttu-id="0e938-125">이를 완료했으므로, 우리는 MicroProfile 응용 프로그램을 로컬에서 빌드하고 실행하는 것으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-125">Now that this is complete, we can move on with building and running our MicroProfile application locally.</span></span>

## <a name="creating-our-microprofile-application"></a><span data-ttu-id="0e938-126">MicroProfile 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="0e938-126">Creating our MicroProfile application</span></span>

<span data-ttu-id="0e938-127">이 예제는 GitHub에서 사용할 수 있는 예제 응용 프로그램을 기반으로 하므로, 코드를 복제한 다음 코드 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-127">This example is based on a sample application available on GitHub, so we will clone that and then step through the code.</span></span> <span data-ttu-id="0e938-128">컴퓨터에 코드를 복제하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-128">Follow the steps below to get the code cloned onto your machine:</span></span>

1. `git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git`
1. `cd microprofile-docker-helloworld`

<span data-ttu-id="0e938-129">이 디렉터리에는 Maven 빌드 도구가 사용하는 형식으로 프로젝트를 지정하는 데 사용되는 `pom.xml` 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-129">In this directory there is a `pom.xml` file that is used to specify the project in the format used by the Maven build tool.</span></span> <span data-ttu-id="0e938-130">이 파일은 사용자 고유의 요구에 맞게 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-130">This file can be edited to suit your own needs.</span></span> <span data-ttu-id="0e938-131">특히, Azure Container Registry가 설정되었을 때 `docker.registry` 및 `docker.name` 속성이 `docker.registry` 및 `docker.name`로 변경되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-131">In particular, the `docker.registry` and `docker.name` properties should be changed to the `docker.registry` and `docker.name` created when the Azure Container Registry was setup.</span></span>

<span data-ttu-id="0e938-132">이 디렉터리에서 확인할 다른 파일은 아래에서 재생되는 Dockerfile입니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-132">Another file of note in this directory is the Dockerfile, which is reproduced below:</span></span>

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

<span data-ttu-id="0e938-133">이 Dockerfile은 단순히 Payara Micro Docker Container를 기반으로 새 Docker 컨테이너를 만들고 빌드 프로세스의 일부로 생성된 .war 파일 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-133">This Dockerfile simply creates a new Docker container based on the Payara Micro Docker Container, and copies in the .war file that is created as part of our build process.</span></span> <span data-ttu-id="0e938-134">이는 또한 Docker 컨테이너 내에서 실행되면 서비스에 액세스할 수 있도록 8080 포트를 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-134">It also exposes port 8080 so that we may access the service once it is up and running within a Docker container.</span></span>

<span data-ttu-id="0e938-135">`src` 디렉터리를 살펴보면 결국 `Application` 클래스가 아래에 재생되었음을 발견하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-135">Diving into the `src` directory, we will eventually discover the `Application` class reproduced below:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

<span data-ttu-id="0e938-136">`@ApplicationPath("/api")` 주석은 이 마이크로 서비스의 기본 엔드포인트를 지정합니다. 즉, 모든 엔드포인트가 특정 REST 엔드포인트에 액세스하는 데 필요한 나머지 URL보다 앞에 오도록 `/api`를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-136">The `@ApplicationPath("/api")` annotation specifies the base endpoint for this microservice - that is, that all endpoints will have `/api` preceed the rest of the URL required to access any specific REST endpoint.</span></span>

<span data-ttu-id="0e938-137">`api` 패키지 내에는 `API`로 명명된 클래스가 있으며 다음 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-137">Inside the `api` package is a class named `API`, which contains the following code:</span></span>

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

<span data-ttu-id="0e938-138">`@Path("/helloworld")` 주석을 사용하여, `Application` 클래스에 지정된 `/api`와 결합 될 때, 이 REST 엔드포인트가 `/api/helloworld`임을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-138">Through the use of the `@Path("/helloworld")` annotation, we can see that this REST endpoint, when combined with the `/api` specified in the `Application` class, will be `/api/helloworld`.</span></span> <span data-ttu-id="0e938-139">HTTP GET 요청을 사용하여 이 엔드포인트을 호출하면 메서드에서 text/html을 생성하며 실제로는 단순히 하드 코딩된 문자열인 "Hello, world!"라는 사실을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-139">When this endpoint is called using an HTTP GET request, we can see that the method will produce text/html, and in fact it is simply a hard-coded string "Hello, world!".</span></span>

<span data-ttu-id="0e938-140">이제 MicroProfile를 사용하여 마이크로 서비스를 만드는 데 필요한 모든 코드를 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-140">We have now covered all the code required to create a microservice using MicroProfile.</span></span> <span data-ttu-id="0e938-141">이제 Maven을 사용하여 빌드하고, Docker 컨테이너로 컨테이너화하여 로컬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-141">We can now use Maven to build it, containerize it into a Docker container, and run it locally.</span></span> <span data-ttu-id="0e938-142">이 작업은 다음 단계를 수행하여 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-142">We can do that with the following steps:</span></span>

1. <span data-ttu-id="0e938-143">`mvn clean package`를 실행하고 성공적으로 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-143">Run `mvn clean package` and wait until it successfully completes.</span></span>

1. <span data-ttu-id="0e938-144">`docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`을 실행, 예를 들어 `docker.registry`가 `jogilescr.azurecr.io`이고 `docker.name`이 `samples/docker-helloworld`인 경우, `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`입니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-144">Run `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`, for example, `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`, if your `docker.registry` is `jogilescr.azurecr.io` and `docker.name` is `samples/docker-helloworld`.</span></span>

1. <span data-ttu-id="0e938-145">웹 브라우저에서 [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) 및 [http://localhost:8080/health](http://localhost:8080/health)에 액세스해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="0e938-145">Try accessing [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) and [http://localhost:8080/health](http://localhost:8080/health) in your web browser.</span></span> <span data-ttu-id="0e938-146">"Hello, world!"</span><span class="sxs-lookup"><span data-stu-id="0e938-146">If you see the expected "Hello, world!"</span></span> <span data-ttu-id="0e938-147">응답(및 [/health](http://localhost:8080/health) 엔드포인트 상태 관련 정보)이 성공적으로 나타난다면, MicroProfile 응용 프로그램이 로컬 컴퓨터에 성공적으로 배포한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-147">response (and health-related information for the [/health](http://localhost:8080/health) endpoint), you have successfully deployed the MicroProfile application on your local machine.</span></span>

## <a name="pushing-to-the-azure-container-registry"></a><span data-ttu-id="0e938-148">Azure Container Registry로 푸시하기</span><span class="sxs-lookup"><span data-stu-id="0e938-148">Pushing to the Azure Container Registry</span></span>

<span data-ttu-id="0e938-149">이제 로컬 시스템에서 MicroProfile 응용 프로그램을 성공적으로 빌드하고 실행했으므로 다음 단계는 이 컨테이너를 컨테이너 레지스트리에 푸시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-149">Now that we have successfully built and run our MicroProfile application on our local machine, the next step is to push this container into our container registry.</span></span> <span data-ttu-id="0e938-150">이 자습서에서는 Azure Container Registry를 사용하지만 모든 컨테이너 레지스트리가 작동합니다(`pom.xml` 파일을 편집하여 관련 위치를 가리키는 경우).</span><span class="sxs-lookup"><span data-stu-id="0e938-150">In this tutorial we are using the Azure Container Registry, but any container registry will work (as long as the `pom.xml` file is edited to point to the relevant location).</span></span>

1. <span data-ttu-id="0e938-151">`mvn clean package`를 실행하여 클린, 컴파일하고 로컬 docker 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-151">Run `mvn clean package` to clean, compile, and create a local docker image.</span></span>
2. <span data-ttu-id="0e938-152">Azure Container Registry에 푸시하기 위해 `mvn dockerfile:push`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-152">Run `mvn dockerfile:push` to push to the Azure Container Registry.</span></span>

<span data-ttu-id="0e938-153">이 단계에서 Docker 컨테이너 이미지를 Azure Container Registry에 업로드했으나 Azure Web App for Containers 인스턴스에 배포해야 하므로 아직 실행되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-153">At this stage you now have your docker container image uploaded to the Azure Container Registry, but it is not yet running as we now have to deploy it into an Azure Web App for Containers instance.</span></span> <span data-ttu-id="0e938-154">이제는 이 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-154">We will now do that.</span></span>

## <a name="creating-an-azure-web-app-for-containers-instance"></a><span data-ttu-id="0e938-155">Web App for Containers 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="0e938-155">Creating an Azure Web App for Containers instance</span></span>

1. <span data-ttu-id="0e938-156">[ Azure 포털 ](http://portal.azure.com)로 돌아가서 새 Web App for Containers 인스턴스를 만듭니다(메뉴의 '웹 + 모바일' 제목 아래에 있음).</span><span class="sxs-lookup"><span data-stu-id="0e938-156">Return to the [Azure Portal](http://portal.azure.com) and create a new Web App for Containers instance (located under the 'Web + Mobile' heading in the menu).</span></span> <span data-ttu-id="0e938-157">몇 가지 주의사항을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-157">A few pointers:</span></span>

   1. <span data-ttu-id="0e938-158">여기에 지정한 이름은 웹 응용 프로그램의 공용 URL이 됩니다(원하는 경우 나중에 사용자 정의 도메인을 추가할 수 있음). 따라서 쉽게 기억할 수 있는 이름을 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-158">The name you specify here will be the public URL of the web app (although a custom domain can be added later if desired), so it is a good idea to pick a name that you can easily remember.</span></span>

   1. <span data-ttu-id="0e938-159">'컨테이너 구성' 섹션으로 이동하면 '이미지 소스'에 대해 'Azure Container Registry'를 선택한 다음 드롭 다운 목록에서 올바른 이미지를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-159">When you get to the 'Configure container' section, you can select 'Azure Container Registry' for the 'Image source', and then select the correct image from the drop-down lists.</span></span>

   1. <span data-ttu-id="0e938-160">'시작 파일' 필드에 값을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-160">You do not need to specify any value in the 'Startup File' field.</span></span>

1. <span data-ttu-id="0e938-161">인스턴스가 생성되면(다시 한번 말하면 매우 빠름) 클릭하고 '응용 프로그램 설정' 메뉴 항목을 클릭하십시오.</span><span class="sxs-lookup"><span data-stu-id="0e938-161">Once the instance is created (again, it is very quick), click on it and then click on the 'Application Settings' menu item.</span></span> <span data-ttu-id="0e938-162">여기서 키가 `WEBSITES_PORT`이고 값이 `8080`인 새 응용 프로그램 설정을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-162">In here you need to add a new application setting, where the key is `WEBSITES_PORT` and the value is `8080`.</span></span> <span data-ttu-id="0e938-163">Azure에게 컨테이너에서 노출시키고자 하는 포트를 알려주게 되고, 외부적으로는 포트 80에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-163">This tells Azure which port you want to expose in the container, and it will be mapped to port 80 externally.</span></span>

1. <span data-ttu-id="0e938-164">또는 'Docker 컨테이너' 링크를 클릭하고 '지속적인 배포'를 활성화하면 Azure Container Registry 이미지를 업데이트할 때마다 Azure Web App for Containers 인스턴스에서 자동으로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-164">Optionally, click on the 'Docker Container' link, and enable 'Continuous Deployment', so that whenever you update the Azure Container Registry image it is automatically updated in the Azure Web App for Containers instance.</span></span>

1. <span data-ttu-id="0e938-165">`http://<appname>.azurewebsites.net/microprofile/api/helloworld`, `http://<appname>.azurewebsites.net/health`에서 Azure 호스트 인스턴스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-165">You should be able to access the Azure-hosted instances at `http://<appname>.azurewebsites.net/microprofile/api/helloworld` and `http://<appname>.azurewebsites.net/health`.</span></span>

## <a name="summary"></a><span data-ttu-id="0e938-166">요약</span><span class="sxs-lookup"><span data-stu-id="0e938-166">Summary</span></span>

<span data-ttu-id="0e938-167">이 자습서를 통해 간단한 MicroProfile 기반의 마이크로 서비스를 생성하고 Docker 컨테이너로 컨테이너화한 다음 로컬로 실행하여 Azure에 게시했습니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-167">Through this tutorial we have stepped through the process of creating a simple MicroProfile-based microservice, containerized it into a Docker container, and we have run it locally and published it to Azure.</span></span> <span data-ttu-id="0e938-168">더 유용한 기능을 제공하기 위해 마이크로 서비스를 확장하는 것은 이 자습서의 범위를 벗어나지만, 인터넷에는 MicroProfile에 대한 풍부한 자습서와 조언이 있으며 [MicroProfile.io](https://microprofile.io/)에서 더 많은 내용을 검토할 것을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="0e938-168">Extending our microservice to provide more useful functionality is outside the scope of this tutorial, but there is a wealth of tutorials and advice on MicroProfile on the internet, and readers are encouraged to review [MicroProfile.io](https://microprofile.io/) for more content.</span></span>
