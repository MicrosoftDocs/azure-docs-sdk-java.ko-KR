---
title: Azure용 Spring Boot Starter
description: 이 문서에서는 Azure에 사용할 수 있는 다양한 Spring Boot Starter를 설명 합니다.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 678d4b279cecb83c95b3bf0f6bcdf1581924aa62
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893504"
---
# <a name="spring-boot-starters-for-azure"></a><span data-ttu-id="25748-103">Azure용 Spring Boot Starter</span><span class="sxs-lookup"><span data-stu-id="25748-103">Spring Boot Starters for Azure</span></span>

<span data-ttu-id="25748-104">이 문서에서는 Microsoft Azure 작업을 위해 Java 개발자에게 통합 기능을 제공하는 [Spring Initializr]의 여러 Spring Boot Starter에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-104">This article describes the various Spring Boot Starters for the [Spring Initializr] that provide Java developers with integration features for working with Microsoft Azure.</span></span>

![Azure Spring Boot Starter][spring-boot-starters]

<span data-ttu-id="25748-106">현재 다음 Spring Boot Starter를 Azure에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="25748-106">The following Spring Boot Starters are currently available for Azure:</span></span>

* <span data-ttu-id="25748-107">**[Azure Support](#azure-support)**</span><span class="sxs-lookup"><span data-stu-id="25748-107">**[Azure Support](#azure-support)**</span></span>

   <span data-ttu-id="25748-108">Azure Services(예: Service Bus, Storage, Active Directory 등)에 대한 자동 구성 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-108">Provides auto-configuration support for Azure Services; e.g. Service Bus, Storage, Active Directory, etc.</span></span>

* <span data-ttu-id="25748-109">**[Azure Active Directory](#azure-active-directory)**</span><span class="sxs-lookup"><span data-stu-id="25748-109">**[Azure Active Directory](#azure-active-directory)**</span></span>

   <span data-ttu-id="25748-110">인증을 위해 Spring Security와 Azure Active Directory의 통합 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-110">Provides integration support for Spring Security with Azure Active Directory for authentication.</span></span>

* <span data-ttu-id="25748-111">**[Azure Key Vault](#azure-key-vault)**</span><span class="sxs-lookup"><span data-stu-id="25748-111">**[Azure Key Vault](#azure-key-vault)**</span></span>

   <span data-ttu-id="25748-112">Azure Key Vault Secrets와의 통합을 위한 Spring 값 주석 처리 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-112">Provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

* <span data-ttu-id="25748-113">**[Azure Storage](#azure-storage)**</span><span class="sxs-lookup"><span data-stu-id="25748-113">**[Azure Storage](#azure-storage)**</span></span>

   <span data-ttu-id="25748-114">Azure Storage 서비스에 대한 Spring Boot 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-114">Provides Spring Boot support for Azure Storage services.</span></span>

<a name="azure-support"></a>
## <a name="azure-support"></a><span data-ttu-id="25748-115">Azure Support</span><span class="sxs-lookup"><span data-stu-id="25748-115">Azure Support</span></span>

<span data-ttu-id="25748-116">이 Spring Boot Starter는 Azure Services(예: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault)에 대한 자동 구성 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-116">This Spring Boot Starter provides auto-configuration support for Azure Services; for example: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etc.</span></span>

<span data-ttu-id="25748-117">이 스타터가 제공하는 여러 Azure 기능을 사용하는 방법의 예는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25748-117">For examples of how to use the various Azure features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples>

<span data-ttu-id="25748-118">이 스타터를 Spring Boot 프로젝트에 추가할 때는 *pom.xml* 파일에서 다음을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-118">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="25748-119">다음 속성을 `<properties>` 요소에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-119">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="25748-120">기본 `spring-boot-starter` 종속성은 다음으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="25748-120">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* <span data-ttu-id="25748-121">다음 섹션이 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="25748-121">The following section is added to the file:</span></span>

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
## <a name="azure-active-directory"></a><span data-ttu-id="25748-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25748-122">Azure Active Directory</span></span>

<span data-ttu-id="25748-123">이 Spring Boot Starter는 인증을 위해 Azure Active Directory와의 통합을 제공하기 위해 Spring Security에 대한 자동 구성 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-123">This Spring Boot Starter provides auto-configuration support for Spring Security in order to provide integration with Azure Active Directory for authentication.</span></span>

<span data-ttu-id="25748-124">이 스타터가 제공하는 Azure Active Directory 기능을 사용하는 방법의 예는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25748-124">For examples of how to use the Azure Active Directory features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample>

<span data-ttu-id="25748-125">이 스타터를 Spring Boot 프로젝트에 추가할 때는 *pom.xml* 파일에서 다음을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-125">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="25748-126">다음 속성을 `<properties>` 요소에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-126">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="25748-127">기본 `spring-boot-starter` 종속성은 다음으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="25748-127">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="25748-128">다음 섹션이 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="25748-128">The following section is added to the file:</span></span>

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
## <a name="azure-key-vault"></a><span data-ttu-id="25748-129">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="25748-129">Azure Key Vault</span></span>

<span data-ttu-id="25748-130">이 Spring Boot Starter는 Azure Key Vault Secrets와의 통합을 위한 Spring 값 주석 처리 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-130">This Spring Boot Starter provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

<span data-ttu-id="25748-131">이 스타터가 제공하는 Azure Key Vault 기능을 사용하는 방법의 예는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25748-131">For examples of how to use the Azure Key Vault features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample>

<span data-ttu-id="25748-132">이 스타터를 Spring Boot 프로젝트에 추가할 때는 *pom.xml* 파일에서 다음을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-132">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="25748-133">다음 속성을 `<properties>` 요소에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-133">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="25748-134">기본 `spring-boot-starter` 종속성은 다음으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="25748-134">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="25748-135">다음 섹션이 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="25748-135">The following section is added to the file:</span></span>

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
## <a name="azure-storage"></a><span data-ttu-id="25748-136">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="25748-136">Azure Storage</span></span>

<span data-ttu-id="25748-137">이 Spring Boot Starter는 Azure Storage services에 대한 Spring Boot 통합 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-137">This Spring Boot Starter provides Spring Boot integration support for Azure Storage services.</span></span>

<span data-ttu-id="25748-138">이 스타터가 제공하는 Azure Storage 기능을 사용하는 방법의 예는 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25748-138">For examples of how to use the Azure Storage features that are provided by this starter, see the following:</span></span>

* [<span data-ttu-id="25748-139">Azure Storage에 Spring Boot Starter를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="25748-139">How to use the Spring Boot Starter for Azure Storage</span></span>](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample>

<span data-ttu-id="25748-140">이 스타터를 Spring Boot 프로젝트에 추가할 때는 *pom.xml* 파일에서 다음을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-140">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="25748-141">다음 속성을 `<properties>` 요소에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="25748-141">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="25748-142">기본 `spring-boot-starter` 종속성은 다음으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="25748-142">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="25748-143">다음 섹션이 파일에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="25748-143">The following section is added to the file:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="25748-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="25748-144">Next steps</span></span>

<span data-ttu-id="25748-145">Azure에서 [Spring Boot] 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [Azure의 Spring]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25748-145">For more information about using [Spring Boot] applications on Azure, see [Spring on Azure].</span></span>

<span data-ttu-id="25748-146">Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Java 개발자용 Azure] 및 [Visual Studio Team Services용 Java 도구]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25748-146">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="25748-147">자체 Spring Boot 애플리케이션을 시작하는 데 도움이 필요하면 https://start.spring.io/에서 **Spring Initializr**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="25748-147">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<!-- URL List -->

[Java 개발자용 Azure]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Visual Studio Team Services용 Java 도구]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Azure의 Spring]: https://docs.microsoft.com/java/azure/spring-framework/
[Spring on Azure]: https://docs.microsoft.com/java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
