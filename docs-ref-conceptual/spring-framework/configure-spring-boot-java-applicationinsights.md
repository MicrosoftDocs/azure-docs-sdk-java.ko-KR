---
title: Azure Application Insights SpringBoot Starter를 사용하도록 Spring Boot 이니셜라이져 앱 구성
description: Appliaction Insights SpringBoot Starter를 사용하도록 Spring Initializer를 사용하여 만든 Spring Boot 애플리케이션을 구성합니다.
services: Application-Insights
documentationcenter: java
author: dhaval24
manager: alexklim
editor: ''
ms.assetid: ''
ms.author: dhdoshi
ms.date: 12/19/2018
ms.devlang: java
ms.service: Azure Monitor
ms.tgt_pltfrm: application-insights
ms.topic: article
ms.workload: na
ms.openlocfilehash: f69cdcc5b479e83b230f23a8a76f96284a1b785b
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991437"
---
# <a name="configure-a-spring-boot-initializer-app-to-use-application-insights"></a><span data-ttu-id="8479e-103">Application Insights를 사용하도록 Spring Boot Initializer 앱 구성</span><span class="sxs-lookup"><span data-stu-id="8479e-103">Configure a Spring Boot Initializer app to use Application Insights</span></span>

<span data-ttu-id="8479e-104">이 문서에서는 **[Spring Initializr]** 를 사용하여 Spring Boot 애플리케이션을 만드는 과정을 보여줍니다. 이는 클라우드에서 Java 애플리케이션의 종단 간 모니터링을 위해 Azure Application Insights Spring Boot Starter를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-104">This article walks you through creating a Spring Boot application using **[Spring Initializr]**, that uses Azure Application Insights Spring Boot Starter for end-to-end monitoring of Java applications on cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8479e-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8479e-105">Prerequisites</span></span>

<span data-ttu-id="8479e-106">이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-106">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="8479e-107">Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="8479e-108">지원되는 JDK(Java Development Kit)</span><span class="sxs-lookup"><span data-stu-id="8479e-108">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="8479e-109">Azure에서 개발하는 경우 사용할 수 있는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8479e-109">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="8479e-110">[Apache Maven](http://maven.apache.org/), 버전 3.0 이상</span><span class="sxs-lookup"><span data-stu-id="8479e-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="8479e-111">Spring Initializr를 사용하여 사용자 지정 애플리케이션 만들기</span><span class="sxs-lookup"><span data-stu-id="8479e-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="8479e-112">[https://start.spring.io/](https://start.spring.io/)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-112">Browse to [https://start.spring.io/](https://start.spring.io/).</span></span>

1. <span data-ttu-id="8479e-113">**Java**에서 **Maven** 프로젝트를 생성한다고 지정하고, 애플리케이션에 대한 **그룹** 및 **아티팩트** 이름을 입력한 다음, 종속성 섹션에서 웹 종속성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then select web dependency in the dependenies section.</span></span>

   ![기본 Spring Initializr 옵션][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="8479e-115">Spring Initializr는 **그룹** 및 **아티팩트** 이름을 사용하여 패키지 이름을 만듭니다(예: *com.example.demo*).</span><span class="sxs-lookup"><span data-stu-id="8479e-115">The Spring Initializr will use the **Group** and **Artifact** names to create the package name; for example: *com.example.demo*.</span></span>
   >

1. <span data-ttu-id="8479e-116">**프로젝트 생성** 버튼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-116">Click the button to **Generate Project**.</span></span>

1. <span data-ttu-id="8479e-117">메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-117">When prompted, download the project to a path on your local computer.</span></span>

1. <span data-ttu-id="8479e-118">로컬 시스템에서 파일의 압축을 푼 후에 사용자 지정 Spring Boot 애플리케이션을 편집할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-118">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![사용자 지정 Spring Boot 프로젝트 파일][SI02]

## <a name="create-an-application-insights-resource-on-azure"></a><span data-ttu-id="8479e-120">Azure에서 Application Insights 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="8479e-120">Create an Application Insights Resource on Azure</span></span>

1. <span data-ttu-id="8479e-121">Azure Portal(<https://portal.azure.com/>)이동하고 **+새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-121">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure portal][AZ01]

1. <span data-ttu-id="8479e-123">**관리 도구**를 클릭하고 **Application Insights**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-123">Click **Management Tools**, and then click **Application Insights**.</span></span>

   ![Azure portal][AZ02]

1. <span data-ttu-id="8479e-125">**새 Application Insights 리소스** 페이지에서 다음 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-125">On the **New Application Insights Resource** page, specify the following information:</span></span>

   * <span data-ttu-id="8479e-126">Application Insights 리소스 **이름**을 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="8479e-126">Enter the **Name** for your Application Insights resource.</span></span>
   * <span data-ttu-id="8479e-127">Java 웹 애플리케이션에 대한 **애플리케이션 종류**를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-127">Choose the **Application Type** to Java Web Application.</span></span>
   * <span data-ttu-id="8479e-128">**구독**, **리소스 그룹** 및 **위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-128">Specify your **Subscription**, **Resource group** and **Location**.</span></span>
   * <span data-ttu-id="8479e-129">Azure Portal에서 리소스를 고정하려면 대시보드 옵션에 고정을 선택하십시오.</span><span class="sxs-lookup"><span data-stu-id="8479e-129">Select Pin to dashboard option, if you would like to pin the resource on your Azure portal.</span></span>

   <span data-ttu-id="8479e-130">이러한 옵션을 지정한 경우 **만들기**를 클릭하여 Application Insights 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-130">When you have specified these options, click **Create** to create your Application Insights resource.</span></span>

   ![Azure portal][AZ03]

1. <span data-ttu-id="8479e-132">리소스가 생성되면 Azure **대시보드**뿐만 아니라 **모든 리소스** 페이지에서도 나열된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-132">Once your resource has been created, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources** pages.</span></span> <span data-ttu-id="8479e-133">Application Insights 리소스의 개요 페이지를 열려면 해당 위치 중 하나에서 리소스를 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-133">You can click on your resource on any of those locations to open the overview page of the Application Insights resource.</span></span> <span data-ttu-id="8479e-134">이 개요 페이지에서 **계측 키**를 복사합니다. 합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-134">From this overview page please copy the **instrumentation key**.</span></span>

   ![Azure portal][AZ04]

## <a name="configure-your-downloaded-spring-boot-application-to-use-application-insights"></a><span data-ttu-id="8479e-136">Application Insights를 사용하여 다운로드한 Spring Boot 애플리케이션 구성</span><span class="sxs-lookup"><span data-stu-id="8479e-136">Configure your downloaded Spring Boot Application to use Application Insights</span></span>

1. <span data-ttu-id="8479e-137">앱의 루트 디렉터리에 *POM.xml* 파일 찾고, 해당 종속성 섹션에서 다음 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-137">Locate the *POM.xml* file in the root directory of your app, and add the following dependency in its dependencies section.</span></span> 

```XML
 <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-spring-boot-starter</artifactId>
    <version>1.1.1</version>
</dependency>
```

1. <span data-ttu-id="8479e-138">앱의 *리소스* 디렉터리에서 *application.properties* 파일을 찾거나 아직 없는 경우 해당 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-138">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![application.properties 파일 찾기][RE01]

1. <span data-ttu-id="8479e-140">텍스트 편집기에서 *application.properties* 파일을 찾고 파일에 다음 줄을 추가하고 샘플 값을 적절한 자격 증명으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-140">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties with appropriate credentials:</span></span>

   ```yaml
   # Specify the instrumentation key of your Application Insights resource.
   azure.application-insights.instrumentation-key=[your ikey from the resource]
   # Specify the name of your springboot application. This can be any logical name you would like to give to your app.
   spring.application.name=[your app name]
   ```

   <span data-ttu-id="8479e-141">Application Insights를 세부적으로 조정하는 방법은 [Application Insights Springboot 스타터 추가 정보](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-141">For more ways to fine tune Application Insights please refer to [Application Insights Springboot starter readme](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="8479e-142">다른 Application Insights 계측 키(</span><span class="sxs-lookup"><span data-stu-id="8479e-142">You can use different Application Insights instrumentation keys (i.e</span></span> <span data-ttu-id="8479e-143">즉,다른 리소스)를 PROD, DEV와 같은 다른 프로필에 사용할 수 있습니다. 자세한 내용은 [Spring Boot Profile 특정 속성]을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-143">different resources) for different profiles like PROD, DEV etc. Please refer to [Spring Boot Profile Specific Properties] for additional information.</span></span> 

1. <span data-ttu-id="8479e-144">*application.properties* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-144">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="8479e-145">패키지의 소스 폴더 아래에서 *controller*라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-145">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `D:\Microsoft\demo\src\main\java\com\example\demo\controller`

   <span data-ttu-id="8479e-146">또는</span><span class="sxs-lookup"><span data-stu-id="8479e-146">-or-</span></span>

   `/users/example/home/demo/src/main/java/com/example/demo/controller`

1. <span data-ttu-id="8479e-147">*컨트롤러* 폴더에 *TestController.java*라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-147">Create a new file named *TestController.java* in the *controller* folder.</span></span> <span data-ttu-id="8479e-148">텍스트 편집기에서 파일을 열고 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-148">Open the file in a text editor and add the following code to it:</span></span>

   ```java
    package com.example.demo;

    import com.microsoft.applicationinsights.TelemetryClient;
    import java.io.IOException;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;
    import com.microsoft.applicationinsights.telemetry.Duration;

    @RestController
    @RequestMapping("/sample")
    public class TestController {

        @Autowired
        TelemetryClient telemetryClient;

        @GetMapping("/hello")
        public String hello() {

            //track a custom event  
            telemetryClient.trackEvent("Sending a custom event...");

            //trace a custom trace
            telemetryClient.trackTrace("Sending a custom trace....");

            //track a custom metric
            telemetryClient.trackMetric("custom metric", 1.0);

            //track a custom dependency
            telemetryClient.trackDependency("SQL", "Insert", new Duration(0, 0, 1, 1, 1), true);

            return "hello";
        }
    }
   ```

   <span data-ttu-id="8479e-149">여기에서 `com.example.demo`를 프로젝트의 패키지 이름으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-149">Where you will need to replace `com.example.demo` with the package name for your project.</span></span>

1. <span data-ttu-id="8479e-150">*TestController.java* 파일을 저장 후 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-150">Save and close the *TestController.java* file.</span></span>

1. <span data-ttu-id="8479e-151">Maven을 사용하여 Spring Boot 애플리케이션을 빌드하고 실행합니다. 예:</span><span class="sxs-lookup"><span data-stu-id="8479e-151">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="8479e-152">웹 브라우저를 통해 http://localhost:8080/sample/hello으로 이동하여 웹앱을 테스트하거나 사용 가능한 curl이 있는 경우 다음 예제와 같이 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-152">Test the web app by browsing to http://localhost:8080/sample/hello using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080/sample/hello
   ```

   <span data-ttu-id="8479e-153">"hello!"가</span><span class="sxs-lookup"><span data-stu-id="8479e-153">You should see the "hello!"</span></span> <span data-ttu-id="8479e-154">샘플 컨트롤러에 메시지로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-154">message from your sample controller displayed.</span></span> <span data-ttu-id="8479e-155">Application Insights는이 요청을 자동으로 수집하여 컨트롤러 로직에 지정된 대로 사용자 지정 이벤트, 사용자 지정 메트릭, 사용자 지정 종속성 및 사용자 지정 추적과 연관된 원격 분석 항목으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-155">Application Insights will automatically collect this request and send it as a telemetry item with it's associated custom event, custom metric, custom dependency and custom trace as specified in the controller logic.</span></span> 

   <span data-ttu-id="8479e-156">몇 초 후 Azure Portal에 데이터가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-156">After a few seconds you should see the data on Azure portal.</span></span> 

   ![Azure Portal][AZ05]

   <span data-ttu-id="8479e-158">애플리케이션 맵 타일을 클릭하면 고급 구성 요소와 상호 작용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-158">You can click on Application Map tile to view high level components and their interaction with each other.</span></span> <span data-ttu-id="8479e-159">이는 전체 애플리케이션의 고급 개요를 볼 수 있는 권장되는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-159">This is a recommended place to get a high level overview of entire application.</span></span> <span data-ttu-id="8479e-160">각 Spring Boot 마이크로서비스는 spring 애플리케이션 이름으로 인식됩니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-160">Each Spring Boot Microservice is recognized by the spring application name.</span></span> <span data-ttu-id="8479e-161">따라서 설정하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-161">Please remember to set it.</span></span>

   ![Azure Portal][AZ08] 

## <a name="configure-springboot-application-to-send-log4j-logs-to-application-insights"></a><span data-ttu-id="8479e-163">Springboot Application을 log4j 로그를 Application Insights로 보내도록 구성</span><span class="sxs-lookup"><span data-stu-id="8479e-163">Configure Springboot Application to send log4j logs to Application Insights</span></span>

1. <span data-ttu-id="8479e-164">프로젝트의 POM.xml 파일을 수정하고 종속성 섹션을 다음으로 추가/수정</span><span class="sxs-lookup"><span data-stu-id="8479e-164">Modify the POM.xml file of the project and add/modify the dependencies section with following.</span></span> 

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-log4j2</artifactId>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-spring-boot-starter</artifactId>
        <version>1.1.1</version>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-logging-log4j2</artifactId>
        <version>2.1.1</version>
    </dependency>
</dependencies>
```

2. <span data-ttu-id="8479e-165">*pom.xml* 파일을 저장하고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-165">Save and close the *POM.xml* file.</span></span>

3. <span data-ttu-id="8479e-166">\Src\main\resources 폴더에 새 파일 *log4j2.xml*을 만들고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-166">In \src\main\resources folder, create a new file *log4j2.xml* and configure it.</span></span> <span data-ttu-id="8479e-167">예: </span><span class="sxs-lookup"><span data-stu-id="8479e-167">For example:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<Configuration packages="com.microsoft.applicationinsights.log4j.v2">
  <Properties>
    <Property name="LOG_PATTERN">
      %d{yyyy-MM-dd HH:mm:ss.SSS} %5p ${hostName} --- [%15.15t] %-40.40c{1.} : %m%n%ex
    </Property>
  </Properties>
  <Appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
    <ApplicationInsightsAppender name="aiAppender">
    </ApplicationInsightsAppender>
  </Appenders>
  <Loggers>
    <Root level="trace">
      <AppenderRef ref="Console"  />
      <AppenderRef ref="aiAppender"  />
    </Root>
  </Loggers>
</Configuration>
```
4. <span data-ttu-id="8479e-168">Spring Boot 애플리케이션을 위와 같이 다시 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-168">Build and run the Spring Boot application again as shown above.</span></span> 

<span data-ttu-id="8479e-169">몇 초 내로 모든 spring 로그가 Azure 포털에서 사용가능한 것으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-169">Within few seconds, you should see all the spring logs being available on Azure Portal.</span></span> 

![Azure Portal][AZ06]

<span data-ttu-id="8479e-171">Analytics 포털에서 상세한 로그 메시지를 보고 분석할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-171">You can even look at the detailed log messages and do analysis on Analytics Portal.</span></span> 

![Azure Portal][AZ07]

## <a name="next-steps"></a><span data-ttu-id="8479e-173">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8479e-173">Next steps</span></span>

<span data-ttu-id="8479e-174">Spring과 Azure에 대한 자세한 사항은 Azure의 Spring 설명서 센터를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-174">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8479e-175">Azure의 Spring</span><span class="sxs-lookup"><span data-stu-id="8479e-175">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="8479e-176">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="8479e-176">Additional Resources</span></span>

<span data-ttu-id="8479e-177">Azure에서 Spring Boot 애플리케이션을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8479e-177">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="8479e-178">Azure App Service에 Spring Boot 애플리케이션 배포</span><span class="sxs-lookup"><span data-stu-id="8479e-178">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="8479e-179">Azure Container Service의 Kubernetes 클러스터에 Spring Boot 애플리케이션 실행</span><span class="sxs-lookup"><span data-stu-id="8479e-179">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="8479e-180">Application Insight는 외부 종속성 및 들어오는 요청과의 상관 관계의 자동 컬렉션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-180">Application Insights supports automatic collection of external dependencies and its correlation with incoming requests.</span></span> <span data-ttu-id="8479e-181">이제 Oracle, MsSQL, MySQL, Redis의 자동 컬렉션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-181">Currently we support autocollection of Oracle, MsSQL, MySQL and Redis.</span></span> <span data-ttu-id="8479e-182">자동 컬렉션 활성화에 대한 자세한 내용은 [ Application Insights Java 에이전트 사용 방법](/azure/application-insights/app-insights-java-agent) 을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="8479e-182">For more details on enabling autocollection please follow the article [how to use Application Insights Java agent](/azure/application-insights/app-insights-java-agent).</span></span>

<span data-ttu-id="8479e-183">Azure Application Insights 및 모니터링 기능에 대한 자세한 내용은 **[Application Insights]** 홈페이지를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="8479e-183">For more information about Azure Application Insights, and it's monitoring capabilities, see the **[Application Insights]** home page.</span></span>

<span data-ttu-id="8479e-184">Application Insights Spring Boot Starter의 추가 구성 정보에 대한 자세한 내용은 이 [링크](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="8479e-184">For more information about additional configuration details of Application Insights Spring Boot Starter, please refer to this [link](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span></span>

<span data-ttu-id="8479e-185">기능 요청 및 잠재적 버그에 대해서는 [GitHub](https://github.com/Microsoft/ApplicationInsights-Java/issues) 리포지토리에서 문제를 제기하십시오.</span><span class="sxs-lookup"><span data-stu-id="8479e-185">For feature requests and potential bugs, please open issues on our [GitHub](https://github.com/Microsoft/ApplicationInsights-Java/issues) repository.</span></span>

<span data-ttu-id="8479e-186">Java와 함께 Azure를 사용하는 방법에 관한 자세한 정보는 [Java 개발자용 Azure]와 [Azure DevOps 및 Java 사용하기]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8479e-186">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="8479e-187">**[Spring Framework]** 는 Java 개발자가 엔터프라이즈 수준의 애플리케이션을 만드는 데 도움이 되는 오픈 소스 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-187">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="8479e-188">해당 플랫폼을 기반으로 하여 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 애플리케이션을 만드는 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-188">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="8479e-189">Spring Boot을 시작하는 개발자를 도우려면 [https://github.com/spring-guides/](https://github.com/spring-guides/)에서 몇 가지 샘플 Spring Boot 패키지를 사용할 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-189">To help developers get started with Spring Boot, several sample Spring Boot packages are available at [https://github.com/spring-guides/](https://github.com/spring-guides/).</span></span> <span data-ttu-id="8479e-190">기본 Spring Boot 프로젝트 목록에서 선택하는 것 외에도 **[Spring Initializr]** 를 통해 사용자 지정 Spring Boot 애플리케이션을 만들기 시작하는 개발자에게 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8479e-190">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Java 개발자용 Azure]: /java/azure/
[Azure for Java Developers]: /java/azure/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Azure DevOps 및 Java 사용하기]: /azure/devops/
[Working with Azure DevOps and Java]: /azure/devops/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Profile 특정 속성]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Boot Profile Specific Properties]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Application Insights]: /azure/application-insights/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource.png
[AZ02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource_2.png
[AZ03]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource_3.png
[AZ04]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Get_IKey.png
[AZ05]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/OverviewBladeResults.png
[AZ06]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Search_and_traces.png
[AZ07]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/traces_details.png
[AZ08]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/AppMap.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/spring_start.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/After_extract.png

[RE01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/applicationproperties_loc.png
[RE02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/applicationinsightsproperties.png
