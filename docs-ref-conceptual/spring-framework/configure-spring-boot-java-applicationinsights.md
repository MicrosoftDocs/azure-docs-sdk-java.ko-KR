---
title: Azure Application Insights SpringBoot Starter를 사용하도록 Spring Boot 이니셜라이져 앱 구성
description: Appliaction Insights SpringBoot Starter를 사용하도록 Spring Initializer를 사용하여 만든 Spring Boot 응용프로그램을 구성합니다.
services: Application-Insights
documentationcenter: java
author: dhaval24
manager: alexklim
editor: ''
ms.assetid: ''
ms.author: dhdoshi
ms.date: 05/19/2018
ms.devlang: java
ms.service: Azure Monitor
ms.tgt_pltfrm: application-insights
ms.topic: article
ms.workload: na
ms.openlocfilehash: 0e57bfb304185b8b98dedfdecb2e0374c4a72fe5
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090776"
---
# <a name="configure-a-spring-boot-initializer-app-to-use-application-insights"></a>Application Insights를 사용하도록 Spring Boot Initializer 앱 구성

이 문서에서는 **[Spring Initializr]** 를 사용하여 Spring Boot 응용프로그램을 만드는 과정을 보여줍니다. 이는 클라우드에서 Java 응용 프로그램의 종단 간 모니터링을 위해 Azure Application Insights Spring Boot Starter를 사용합니다.

> [!NOTE]
> 
> *이 스타터는 현재 **베타(공개 미리 보기)* <em>상태입니다.</em>

## <a name="prerequisites"></a>필수 조건

이 문서의 단계를 완료하려면 다음 필수 구성 요소가 필요합니다.

* Azure 구독. Azure 구독이 아직 없는 경우 [MSDN 구독자 혜택]을 활성화하거나 [체험판 Azure 계정]에 등록할 수 있습니다.
* JDK(Java Development Kit), 버전 1.7 및 1.8
* [Apache Maven](http://maven.apache.org/), 버전 3.0 이상

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Spring Initializr를 사용하여 사용자 지정 응용 프로그램 만들기

1. [https://start.spring.io/](https://start.spring.io/)으로 이동합니다.

1. **Java**에서 **Maven** 프로젝트를 생성한다고 지정하고, 응용 프로그램에 대한 **그룹** 및 **아티팩트** 이름을 입력한 다음, 종속성 섹션에서 웹 종속성을 선택합니다. 

   ![기본 Spring Initializr 옵션][SI01]

   > [!NOTE]
   >
   > Spring Initializr는 **그룹** 및 **아티팩트** 이름을 사용하여 패키지 이름을 만듭니다(예: *com.example.demo*).
   >

1. **프로젝트 생성** 버튼을 클릭합니다.

1. 메시지가 표시되면 로컬 컴퓨터의 경로에 프로젝트를 다운로드합니다.

1. 로컬 시스템에서 파일의 압축을 푼 후에 사용자 지정 Spring Boot 응용 프로그램을 편집할 준비를 합니다.

   ![사용자 지정 Spring Boot 프로젝트 파일][SI02]

## <a name="create-an-application-insights-resource-on-azure"></a>Azure에서 Application Insights 리소스 만들기

1. Azure Portal(<https://portal.azure.com/>)이동하고 **+새로 만들기**를 클릭합니다.

   ![Azure portal][AZ01]

1. **관리 도구**를 클릭하고 **Application Insights**를 클릭합니다.

   ![Azure portal][AZ02]

1. **새 Application Insights 리소스** 페이지에서 다음 정보를 지정합니다.

   * Application Insights 리소스 **이름**을 입력하세요.
   * Java 웹 응용 프로그램에 대한 **응용 프로그램 종류**를 설정합니다.
   * **구독**, **리소스 그룹** 및 **위치**를 선택합니다.
   * Azure Portal에서 리소스를 고정하려면 대시보드 옵션에 고정을 선택하십시오.

   이러한 옵션을 지정한 경우 **만들기**를 클릭하여 Application Insights 리소스를 만듭니다.

   ![Azure portal][AZ03]

1. 리소스가 생성되면 Azure **대시보드**뿐만 아니라 **모든 리소스** 페이지에서도 나열된 것을 확인할 수 있습니다. Application Insights 리소스의 개요 페이지를 열려면 해당 위치 중 하나에서 리소스를 클릭할 수 있습니다. 이 개요 페이지에서 **계측 키**를 복사합니다. 합니다.

   ![Azure portal][AZ04]

## <a name="configure-your-downloaded-spring-boot-application-to-use-application-insights"></a>Application Insights를 사용하여 다운로드한 Spring Boot 응용 프로그램 구성

1. 앱의 루트 디렉터리에 *POM.xml* 파일 찾고, 해당 종속성 섹션에서 다음 종속성을 추가합니다. 

```XML
 <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-spring-boot-starter</artifactId>
    <version>1.0.0-BETA</version>
</dependency>
```

1. 앱의 *리소스* 디렉터리에서 *application.properties* 파일을 찾거나 아직 없는 경우 해당 파일을 만듭니다.

   ![application.properties 파일 찾기][RE01]

1. 텍스트 편집기에서 *application.properties* 파일을 찾고 파일에 다음 줄을 추가하고 샘플 값을 적절한 자격 증명으로 바꿉니다.

   ```yaml
   # Specify the instrumentation key of your Application Insights resource.
   azure.application-insights.instrumentation-key=[your ikey from the resource]
   # Specify the name of your springboot application. This can be any logical name you would like to give to your app.
   spring.application.name=[your app name]
   ```

   Application Insights를 세부적으로 조정하는 방법은 [Application Insights Springboot 스타터 추가 정보](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md)를 참조합니다.

   > [!NOTE]
   > 
   > 다른 Application Insights 계측 키( 즉,다른 리소스)를 PROD, DEV와 같은 다른 프로필에 사용할 수 있습니다. 자세한 내용은 [Spring Boot Profile 특정 속성]을 참조합니다. 

1. *application.properties* 파일을 저장하고 닫습니다.

1. 패키지의 소스 폴더 아래에서 *controller*라는 폴더를 만듭니다.

   `D:\Microsoft\demo\src\main\java\com\example\demo\controller`

   또는

   `/users/example/home/demo/src/main/java/com/example/demo/controller`

1. *컨트롤러* 폴더에 *TestController.java*라는 새 파일을 만듭니다. 텍스트 편집기에서 파일을 열고 다음 코드를 추가합니다.

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

   여기에서 `com.example.demo`를 프로젝트의 패키지 이름으로 바꾸어야 합니다.

1. *TestController.java* 파일을 저장 후 닫습니다.

1. Maven을 사용하여 Spring Boot 응용 프로그램을 빌드하고 실행합니다. 예:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. 웹 브라우저를 통해 http://localhost:8080/sample/hello으로 이동하여 웹앱을 테스트하거나 사용 가능한 curl이 있는 경우 다음 예제와 같이 구문을 사용합니다.

   ```shell
   curl http://localhost:8080/sample/hello
   ```

   "hello!"가 샘플 컨트롤러에 메시지로 나타납니다. Application Insights는이 요청을 자동으로 수집하여 컨트롤러 로직에 지정된 대로 사용자 지정 이벤트, 사용자 지정 메트릭, 사용자 지정 종속성 및 사용자 지정 추적과 연관된 원격 분석 항목으로 보냅니다. 

   몇 초 후 Azure Portal에 데이터가 표시됩니다. 

   ![Azure Portal][AZ05]

   응용 프로그램 맵 타일을 클릭하면 고급 구성 요소와 상호 작용을 볼 수 있습니다. 이는 전체 응용 프로그램의 고급 개요를 볼 수 있는 권장되는 방법입니다. 각 Spring Boot 마이크로서비스는 spring 응용 프로그램 이름으로 인식됩니다. 따라서 설정하도록 합니다.

   ![Azure Portal][AZ08] 

## <a name="configure-springboot-application-to-send-log4j-logs-to-application-insights"></a>Springboot Application을 log4j 로그를 Application Insights로 보내도록 구성

1. 프로젝트의 POM.xml 파일을 수정하고 종속성 섹션을 다음으로 추가/수정 

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
        <version>1.0.0-BETA</version>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-logging-log4j2</artifactId>
        <version>2.1.1</version>
    </dependency>
</dependencies>
```

2. *pom.xml* 파일을 저장하고 닫습니다.

3. \Src\main\resources 폴더에 새 파일 *log4j2.xml*을 만들고 구성합니다. 예: 

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
4. Spring Boot 응용 프로그램을 위와 같이 다시 빌드하고 실행합니다. 

몇 초 내로 모든 spring 로그가 Azure 포털에서 사용가능한 것으로 나타납니다. 

![Azure Portal][AZ06]

Analytics 포털에서 상세한 로그 메시지를 보고 분석할 수도 있습니다. 

![Azure Portal][AZ07]

## <a name="next-steps"></a>다음 단계

Azure에서 Spring Boot 응용 프로그램을 사용 하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

* [Azure App Service에 Spring Boot 응용 프로그램 배포](deploy-spring-boot-java-web-app-on-azure.md)

* [Azure Container Service의 Kubernetes 클러스터에 Spring Boot 응용 프로그램 실행](deploy-spring-boot-java-app-on-kubernetes.md)

Application Insight는 외부 종속성 및 들어오는 요청과의 상관 관계의 자동 컬렉션을 지원합니다. 이제 Oracle, MsSQL, MySQL, Redis의 자동 컬렉션을 지원합니다. 자동 컬렉션 활성화에 대한 자세한 내용은 [ Application Insights Java 에이전트 사용 방법](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-java-agent) 을 참조하십시오.

Azure Application Insights 및 모니터링 기능에 대한 자세한 내용은 **[Application Insights]** 홈페이지를 참조하십시오.

Application Insights Spring Boot Starter의 추가 구성 정보에 대한 자세한 내용은 이 [링크](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md)를 참조하십시오.

기능 요청 및 잠재적 버그에 대해서는 [GitHub](https://github.com/Microsoft/ApplicationInsights-Java/issues) 리포지토리에서 문제를 제기하십시오.

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.

**[Spring Framework]** 는 Java 개발자가 엔터프라이즈 수준의 응용 프로그램을 만드는 데 도움이 되는 오픈 소스 솔루션입니다. 해당 플랫폼을 기반으로 하여 빌드되는 인기 있는 프로젝트 중 하나가 [Spring Boot]입니다. 이 프로젝트는 독립 실행형 Java 응용 프로그램을 만드는 간단한 방법을 제공합니다. Spring Boot을 시작하는 개발자를 도우려면 [https://github.com/spring-guides/](https://github.com/spring-guides/)에서 몇 가지 샘플 Spring Boot 패키지를 사용할 있습니다. 기본 Spring Boot 프로젝트 목록에서 선택하는 것 외에도 **[Spring Initializr]** 를 통해 사용자 지정 Spring Boot 응용 프로그램을 만들기 시작하는 개발자에게 도움을 줍니다.

<!-- URL List -->

[Java 개발자용 Azure]: https://docs.microsoft.com/java/azure/
[체험판 Azure 계정]: https://azure.microsoft.com/pricing/free-trial/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/
[MSDN 구독자 혜택]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Profile 특정 속성]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Application Insights]: https://docs.microsoft.com/en-us/azure/application-insights/

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
