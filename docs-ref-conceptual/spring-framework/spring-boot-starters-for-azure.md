---
title: "Azure용 Spring Boot Starter"
description: "이 문서에서는 Azure에 사용할 수 있는 다양한 Spring Boot Starter를 설명 합니다."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: robmcm
ms.openlocfilehash: ba5829407d03d275784a3a458d88ea47ac8494b8
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/06/2017
---
# <a name="spring-boot-starters-for-azure"></a>Azure용 Spring Boot Starter

이 문서에서는 Microsoft Azure 작업을 위해 Java 개발자에게 통합 기능을 제공하는 [Spring Initializr]의 여러 Spring Boot Starter에 대해 설명합니다.

![Azure Spring Boot Starter][spring-boot-starters]

현재 다음 Spring Boot Starter를 Azure에 사용할 수 있습니다.

* **[Azure Support](#azure-support)**

   Azure Services(예: Service Bus, Storage, Active Directory 등)에 대한 자동 구성 지원을 제공합니다.

* **[Azure Active Directory](#azure-active-directory)**

   인증을 위해 Spring Security와 Azure Active Directory의 통합 지원을 제공합니다.

* **[Azure Key Vault](#azure-key-vault)**

   Azure Key Vault Secrets와의 통합을 위한 Spring 값 주석 처리 지원을 제공합니다.

* **[Azure Storage](#azure-storage)**

   Azure Storage 서비스에 대한 Spring Boot 지원을 제공합니다.

<a name="azure-support"></a>
## <a name="azure-support"></a>Azure Support

이 Spring Boot Starter는 Azure Services(예: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault)에 대한 자동 구성 지원을 제공합니다.

이 스타터가 제공하는 여러 Azure 기능을 사용하는 방법의 예는 다음을 참조하세요.

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples>

이 스타터를 Spring Boot 프로젝트에 추가할 때는 *pom.xml* 파일에서 다음을 변경합니다.

* 다음 속성을 `<properties>` 요소에 추가합니다.

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* 기본 `spring-boot-starter` 종속성은 다음으로 바뀝니다.

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* 다음 섹션이 파일에 추가됩니다.

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-active-directory"></a>
## <a name="azure-active-directory"></a>Azure Active Directory

이 Spring Boot Starter는 인증을 위해 Azure Active Directory와의 통합을 제공하기 위해 Spring Security에 대한 자동 구성 지원을 제공합니다.

이 스타터가 제공하는 Azure Active Directory 기능을 사용하는 방법의 예는 다음을 참조하세요.

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample>

이 스타터를 Spring Boot 프로젝트에 추가할 때는 *pom.xml* 파일에서 다음을 변경합니다.

* 다음 속성을 `<properties>` 요소에 추가합니다.

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* 기본 `spring-boot-starter` 종속성은 다음으로 바뀝니다.

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* 다음 섹션이 파일에 추가됩니다.

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-key-vault"></a>
## <a name="azure-key-vault"></a>Azure Key Vault

이 Spring Boot Starter는 Azure Key Vault Secrets와의 통합을 위한 Spring 값 주석 처리 지원을 제공합니다.

이 스타터가 제공하는 Azure Key Vault 기능을 사용하는 방법의 예는 다음을 참조하세요.

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample>

이 스타터를 Spring Boot 프로젝트에 추가할 때는 *pom.xml* 파일에서 다음을 변경합니다.

* 다음 속성을 `<properties>` 요소에 추가합니다.

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* 기본 `spring-boot-starter` 종속성은 다음으로 바뀝니다.

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* 다음 섹션이 파일에 추가됩니다.

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-storage"></a>
## <a name="azure-storage"></a>Azure Storage

이 Spring Boot Starter는 Azure Storage services에 대한 Spring Boot 통합 지원을 제공합니다.

이 스타터가 제공하는 Azure Storage 기능을 사용하는 방법의 예는 다음을 참조하세요.

* [Azure Storage에 Spring Boot Starter를 사용하는 방법](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample>

이 스타터를 Spring Boot 프로젝트에 추가할 때는 *pom.xml* 파일에서 다음을 변경합니다.

* 다음 속성을 `<properties>` 요소에 추가합니다.

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* 기본 `spring-boot-starter` 종속성은 다음으로 바뀝니다.

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* 다음 섹션이 파일에 추가됩니다.

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

## <a name="next-steps"></a>다음 단계

Azure에서 [Spring Boot] 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [Azure의 Spring]을 참조하세요.

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.

자체 Spring Boot 응용 프로그램을 시작하는 데 도움이 필요하면 https://start.spring.io/에서 **Spring Initializr**를 참조하세요.

<!-- URL List -->

[Java 개발자용 Azure]: https://docs.microsoft.com/java/azure/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Azure의 Spring]: https://docs.microsoft.com/java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
