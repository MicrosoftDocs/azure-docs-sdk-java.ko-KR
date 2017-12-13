---
title: "Java 개발자용 Azure 관리 라이브 가이드"
description: "Azure에서 클라우드 리소스를 관리하기 위해 Java용 Java 관리 라이브러리를 사용하기 위한 패턴 및 개념입니다."
keywords: "Azure, Java, SDK, API, Maven, Gradle, 인증, Active Directory, 서비스 사용자"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: f452468b-7aae-4944-abad-0b1aaf19170d
ms.openlocfilehash: 8b52981ddfaadb7227cea4c7df014011196339cb
ms.sourcegitcommit: 1f6a80e067a8bdbbb4b2da2e2145fda73d5fe65a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="patterns-and-best-practices-for-development-with-the-azure-libraries-for-java"></a><span data-ttu-id="245cf-104">Java용 Azure 라이브러리를 통한 개발 패턴 및 모범 사례</span><span class="sxs-lookup"><span data-stu-id="245cf-104">Patterns and best practices for development with the Azure libraries for Java</span></span> 

<span data-ttu-id="245cf-105">이 문서에서는 프로젝트에서 Java용 Azure 라이브러리를 사용할 때의 여러 패턴과 모범 사례를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-105">This article lists a series of patterns and best practices when using the Azure libraries for Java in your projects.</span></span> <span data-ttu-id="245cf-106">이러한 패턴 및 지침을 통해 개발하면 코드 유지 관리 작업을 줄이고 향후 업데이트에서 더 간편하게 다른 리소스를 관리 라이브러리에 추가하거나 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-106">Develop with these patterns and guidelines to reduce the amount of code to maintain and make it easier to add or configure additional resources in future updates to the management libraries.</span></span>

## <a name="build-resources-through-a-fluent-interface"></a><span data-ttu-id="245cf-107">흐름 인터페이스를 통해 리소스 빌드</span><span class="sxs-lookup"><span data-stu-id="245cf-107">Build resources through a fluent interface</span></span>

<span data-ttu-id="245cf-108">흐름 인터페이스는 개체의 특성을 올바르게 구성하는 메서드 체인을 사용하여 개체를 만드는 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-108">A fluent interface is a pattern that creates objects using a method chain that correctly configures the object's attributes.</span></span> <span data-ttu-id="245cf-109">예를 들어 Azure Storage 계정을 새로 만드는 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-109">For example, to create a new Azure Storage account</span></span>

```java
StorageAccount storage = azure.storageAccounts().define(storageAccountName)
    .withRegion(region)
    .withNewResourceGroup(resourceGroup)
    .create();
```

<span data-ttu-id="245cf-110">메서드 체인을 진행할 때 IDE에서 다음과 같은 흐름 대화를 호출하는 메서드를 제안합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-110">As you go through the method chain, your IDE suggests the next method to call in the fluent conversation.</span></span>   

![흐름 체인을 통한 IntelliJ 명령 완료 작업을 보여 주는 GIF](media/intelliJFluent.gif)

<span data-ttu-id="245cf-112">정의되는 Azure 리소스가 인식되는 한 IDE에서 제안하는 메서드를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-112">Chain the methods suggested by the IDE as long as they make sense for the Azure resource being defined.</span></span> <span data-ttu-id="245cf-113">체인에 필요한 메서드가 누락되면 IDE에서 오류와 함께 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-113">If you are missing a required method in the chain your IDE will highlight it with an error.</span></span>

## <a name="resource-collections"></a><span data-ttu-id="245cf-114">리소스 컬렉션</span><span class="sxs-lookup"><span data-stu-id="245cf-114">Resource collections</span></span>

<span data-ttu-id="245cf-115">관리 라이브러리에는 리소스를 만들고 업데이트하는 최상위 수준의 `com.microsoft.azure.management.Azure` 개체를 통한 단일 진입점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-115">The management library has a single point of entry through the top-level `com.microsoft.azure.management.Azure` object to create and update resources.</span></span> <span data-ttu-id="245cf-116">`Azure` 개체에 정의된 리소스 컬렉션 메서드를 사용하여 사용할 리소스 종류를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-116">Select which type of resources to work with using the resource collection methods defined in the `Azure` object.</span></span> <span data-ttu-id="245cf-117">예를 들어 SQL Database의 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-117">For example, SQL Database:</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName)
    .withAdministratorLogin(administratorLogin)
    .withAdministratorPassword(administratorPassword)
    .create();
```

## <a name="lists-and-iterations"></a><span data-ttu-id="245cf-118">목록 및 반복</span><span class="sxs-lookup"><span data-stu-id="245cf-118">Lists and iterations</span></span>

<span data-ttu-id="245cf-119">각 리소스 컬렉션에는 현재 구독에 있는 해당 리소스의 모든 인스턴스를 반환하는 `list()` 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-119">Each resource collection has a `list()` method to return every instance of that resource in your current subscription.</span></span> <span data-ttu-id="245cf-120">예를 들어 `azure.sqlServers().list()`는 구독의 모든 SQL 데이터베이스를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-120">For example, `azure.sqlServers().list()` returns all SQL databases in the subscription.</span></span>

<span data-ttu-id="245cf-121">`listByResourceGroup(String groupname)` 메서드를 사용하여 반환된 List의 범위를 특정 [Azure 리소스 그룹](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-121">Use the `listByResourceGroup(String groupname)` method to scope the returned List to a specific [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span></span>  

<span data-ttu-id="245cf-122">일반 `List<T>`와 마찬가지로 반환된 `PagedList<T>` 컬렉션을 검색하고 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-122">Search and iterate over the returned `PagedList<T>` collection just as you would a normal `List<T>`:</span></span>

```java
PagedList<VirtualMachine> vms = azure.virtualMachines().list();
for (VirtualMachine vm : vms) {
    System.out.println("Found virtual machine with ID " + vm.id());
}
```   

## <a name="collections-returned-from-queries"></a><span data-ttu-id="245cf-123">쿼리에서 반환되는 컬렉션</span><span class="sxs-lookup"><span data-stu-id="245cf-123">Collections returned from queries</span></span>

<span data-ttu-id="245cf-124">관리 라이브러리는 결과의 구조에 따라 쿼리에서 특정 컬렉션 형식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-124">The management libraries return specific collection types from queries based on the structure of the results.</span></span>

- <span data-ttu-id="245cf-125">`List<T>`: 순서가 지정되지 않았지만 쉽게 검색하고 반복할 수 있는 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-125">`List<T>`: Unordered data that is easy to search and iterate over.</span></span>
- <span data-ttu-id="245cf-126">`Map<T>`: 고유 키가 있는 키/값 쌍이지만 반드시 고유한 값은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-126">`Map<T>`: Maps are key/value pairs with unique keys, but not necessarily unique values.</span></span> <span data-ttu-id="245cf-127">Map의 예로 App Service 웹앱에 대한 앱 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-127">An example of a Map would be app settings for an App Service Web App.</span></span>
- <span data-ttu-id="245cf-128">`Set<T>`: 고유한 키와 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-128">`Set<T>`: Sets have unique keys and values.</span></span> <span data-ttu-id="245cf-129">Set의 예로 고유 식별자(키)와 고유 네트워크 구성(값)이 모두 있는 가상 컴퓨터에 연결된 네트워크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-129">An example of a Set would be networks attached to a virtual machine, which would have both an unique identifier (the key) and a unique network configuration (the value).</span></span>

## <a name="actionable-verbs"></a><span data-ttu-id="245cf-130">실행 가능한 동사</span><span class="sxs-lookup"><span data-stu-id="245cf-130">Actionable verbs</span></span>

<span data-ttu-id="245cf-131">이름에 동사가 있는 메서드는 Azure에서 즉시로 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-131">Methods with verbs in their names take immediate action in Azure.</span></span> <span data-ttu-id="245cf-132">이러한 메서드는 동기적으로 작동하고 완료될 때까지 현재 스레드의 실행을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-132">These methods work synchronously and block execution in the current thread until they complete.</span></span> 

| <span data-ttu-id="245cf-133">동사</span><span class="sxs-lookup"><span data-stu-id="245cf-133">Verb</span></span>   |  <span data-ttu-id="245cf-134">샘플 사용</span><span class="sxs-lookup"><span data-stu-id="245cf-134">Sample Usage</span></span> |
|--------|---------------|
| <span data-ttu-id="245cf-135">create</span><span class="sxs-lookup"><span data-stu-id="245cf-135">create</span></span> | `azure.virtualMachines().create(listOfVMCreatables)` |
| <span data-ttu-id="245cf-136">apply</span><span class="sxs-lookup"><span data-stu-id="245cf-136">apply</span></span>  | `virtualMachineScaleSet.update().withCapacity(6).apply()` |
| <span data-ttu-id="245cf-137">delete</span><span class="sxs-lookup"><span data-stu-id="245cf-137">delete</span></span> | `azure.disks().deleteById(id)` | 
| <span data-ttu-id="245cf-138">list</span><span class="sxs-lookup"><span data-stu-id="245cf-138">list</span></span>   | `azure.sqlServers().list()` | 
| <span data-ttu-id="245cf-139">get</span><span class="sxs-lookup"><span data-stu-id="245cf-139">get</span></span>    | `VirtualMachine vm  = azure.virtualMachines().getByResourceGroup(group, vmName)` |

>[!NOTE]
> <span data-ttu-id="245cf-140">`define()` 및 `update()`는 동사이지만 `create()` 또는 `apply()`가 뒤에 나오지 않으면 차단하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-140">`define()` and `update()` are verbs but do not block unless followed by a `create()` or `apply()`.</span></span>
 
<span data-ttu-id="245cf-141">이러한 메서드 중 일부의 비동기 버전은 [Reactive eXtension(영문)](https://github.com/ReactiveX/RxJava)을 사용하여 `Async` 접미사와 함께 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-141">Asynchronous versions of some of these  methods exist with the `Async` suffix using [Reactive extensions](https://github.com/ReactiveX/RxJava).</span></span> 

<span data-ttu-id="245cf-142">일부 개체에는 Azure에서 리소스의 상태를 변경하는 다른 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-142">Some objects have other methods with that change the state of the resource in Azure.</span></span> <span data-ttu-id="245cf-143">예를 들어 `VirtualMachine`의 `restart()`와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-143">For example, `restart()` on a `VirtualMachine`.</span></span>

```java
VirtualMachine vmToRestart = azure.getVirtualMachines().getById(id);
vmToRestart.restart();
```
<span data-ttu-id="245cf-144">이러한 메서드는 항상 비동기 버전을 가지고 있는 것은 아니며, 완료될 때까지 해당 스레드의 실행을 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-144">These methods do not always have asynchronous versions and will block execution on their thread until they complete.</span></span>

<a name="Creatables"></a>

## <a name="lazy-resource-creation"></a><span data-ttu-id="245cf-145">지연 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="245cf-145">Lazy resource creation</span></span>

<span data-ttu-id="245cf-146">Azure 리소스를 만들 때 새 리소스가 아직 존재하지 않는 다른 리소스에 종속되면 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-146">A challenge when creating Azure resources arises when a new resource depends on another resource that doesn't yet exist.</span></span> <span data-ttu-id="245cf-147">이 시나리오의 예로, 새 가상 컴퓨터를 만들 때 공용 IP 주소를 예약하고 디스크를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-147">An example of this scenario is reserving a public IP address and setting up a disk when creating a new virtual machine.</span></span> <span data-ttu-id="245cf-148">주소 예약 또는 디스크 만들기를 확인하지 않으려는 경우 가상 컴퓨터를 만들 때 이러한 리소스가 있는지 확인만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-148">You don't want to verify reserving the address or the creating the disk, you just want to ensure the virtual machine has those resources when it is created.</span></span>

<span data-ttu-id="245cf-149">`Creatable<T>` 개체를 사용하면 구독에 Azure 리소스를 만들 때까지 기다리지 않고 코드에서 사용할 수 있도록 이러한 리소스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-149">`Creatable<T>` objects let you define Azure resources for use in your code without waiting around for them to be created in your subscription.</span></span> <span data-ttu-id="245cf-150">관리 라이브러리는 `Creatable<T>` 개체가 필요할 때까지 기다린 후에 이러한 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-150">The management libraries defer creating  `Creatable<T>` objects until they are needed.</span></span>

<span data-ttu-id="245cf-151">`define()` 동사를 통해 Azure 리소스에 대한 `Creatable<T>` 개체를 생성하는 예제는 다음과 같습니다:</span><span class="sxs-lookup"><span data-stu-id="245cf-151">Generate `Creatable<T>` objects for Azure resources through the `define()` verb:</span></span>

```java
Creatable<PublicIPAddress> publicIPAddressCreatable = azure.publicIPAddresses().define(publicIPAddressName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName);
```

<span data-ttu-id="245cf-152">이 예제에서 `Creatable<PublicIPAddress>`로 정의된 Azure 리소스는 이 코드를 실행할 때는 아직 구독에 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-152">The Azure resource defined by the `Creatable<PublicIPAddress>` in this example does not yet exist in your subscription when this code executes.</span></span>  <span data-ttu-id="245cf-153">`publicIPAddressCreatable` 개체를 사용하여 이 IP 주소가 있는 다른 Azure 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-153">Use the `publicIPAddressCreatable` object to create other Azure resources with this IP address.</span></span> 

```java
Creatable<VirtualMachine> vmCreatable = azure.virtualMachines().define("creatableVM")
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
```

<span data-ttu-id="245cf-154">개체를 사용하여 정의된 리소스가 Azure에서 `create()`를 사용하여 빌드될 때 구독에 `Creatable<T>` 리소스가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-154">The `Creatable<T>` resources are generated in your subscription when any resource that is defined using the object is built in Azure using `create()`.</span></span> <span data-ttu-id="245cf-155">IP 주소 및 가상 컴퓨터 예제를 계속하는 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-155">Continuing the IP address and virtual machine example:</span></span>

```java
CreatedResources<VirtualMachine> virtualMachine = azure.virtualMachines().create(vmCreatable);
```

<span data-ttu-id="245cf-156">`Creatable<T>`를 `create()` 호출에 전달하면 단일 리소스 개체 대신 `CreatedResources` 개체가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-156">Passing the `Creatable<T>` to `create()` calls returns a `CreatedResources` object instead of a single resource object.</span></span>  <span data-ttu-id="245cf-157">`CreatedResources<T>` 개체를 사용하면 호출에서 형식화된 리소스 외에도 `create()` 호출로 만든 모든 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-157">The `CreatedResources<T>` object lets you access all resources created by the `create()` call, not just the typed resource in the call.</span></span> <span data-ttu-id="245cf-158">위의 예제에서 만든 가상 컴퓨터에 대해 Azure에서 만든 공용 IP 주소에 액세스하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-158">To access the public IP address created in Azure for the virtual machine created in the above example:</span></span>

```java
PublicIPAddress pip = (PublicIPAddress) virtualMachine.createdRelatedResource(publicIPAddressCreatable.key());
```    

## <a name="exception-handling"></a><span data-ttu-id="245cf-159">예외 처리</span><span class="sxs-lookup"><span data-stu-id="245cf-159">Exception handling</span></span>

<span data-ttu-id="245cf-160">관리 라이브러리의 Exception 클래스는 `com.microsoft.rest.RestException`을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-160">The management libraries' Exception classes extend `com.microsoft.rest.RestException`.</span></span> <span data-ttu-id="245cf-161">관련된 `try` 문 뒤에 `catch (RestException exception)` 블록이 있는 관리 라이브러리에서 생성된 예외를 catch합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-161">Catch exceptions generated by the management libraries with a `catch (RestException exception)` block after the relevant `try` statement.</span></span>

## <a name="logs-and-trace"></a><span data-ttu-id="245cf-162">로그 및 추적</span><span class="sxs-lookup"><span data-stu-id="245cf-162">Logs and trace</span></span>

<span data-ttu-id="245cf-163">`withLogLevel()`을 사용하여 `Azure` 진입점 개체를 빌드할 때 관리 라이브러리에서 로깅의 양을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-163">Configure the amount of logging from the management library when you build the entry point `Azure` object using `withLogLevel()`.</span></span> <span data-ttu-id="245cf-164">다음과 같은 추적 수준이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-164">The following trace levels exist:</span></span>

| <span data-ttu-id="245cf-165">추적 수준</span><span class="sxs-lookup"><span data-stu-id="245cf-165">Trace level</span></span> | <span data-ttu-id="245cf-166">사용되는 로깅</span><span class="sxs-lookup"><span data-stu-id="245cf-166">Logging enabled</span></span> 
| ------------ | ---------------
| <span data-ttu-id="245cf-167">com.microsoft.rest.LogLevel.NONE</span><span class="sxs-lookup"><span data-stu-id="245cf-167">com.microsoft.rest.LogLevel.NONE</span></span> | <span data-ttu-id="245cf-168">출력 없음</span><span class="sxs-lookup"><span data-stu-id="245cf-168">No output</span></span>
| <span data-ttu-id="245cf-169">com.microsoft.rest.LogLevel.BASIC</span><span class="sxs-lookup"><span data-stu-id="245cf-169">com.microsoft.rest.LogLevel.BASIC</span></span> | <span data-ttu-id="245cf-170">기본 REST 호출, 응답 코드 및 시간에 URL을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-170">Logs the URLs to underlying REST calls, response codes and times</span></span>
| <span data-ttu-id="245cf-171">com.microsoft.rest.LogLevel.BODY</span><span class="sxs-lookup"><span data-stu-id="245cf-171">com.microsoft.rest.LogLevel.BODY</span></span> | <span data-ttu-id="245cf-172">BASIC의 모든 항목 및 REST 호출에 대한 요청/응답 본문</span><span class="sxs-lookup"><span data-stu-id="245cf-172">Everything in BASIC plus request and response bodies for the REST calls</span></span>
| <span data-ttu-id="245cf-173">com.microsoft.rest.LogLevel.HEADERS</span><span class="sxs-lookup"><span data-stu-id="245cf-173">com.microsoft.rest.LogLevel.HEADERS</span></span> | <span data-ttu-id="245cf-174">BASIC의 모든 항목 및 REST 호출에 대한 요청/응답 헤더</span><span class="sxs-lookup"><span data-stu-id="245cf-174">Everything in BASIC plus the request and response headers REST calls</span></span>
| <span data-ttu-id="245cf-175">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span><span class="sxs-lookup"><span data-stu-id="245cf-175">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span></span> | <span data-ttu-id="245cf-176">BODY 및 HEADERS 로그 수준 둘 다의 모든 항목</span><span class="sxs-lookup"><span data-stu-id="245cf-176">Everything in both BODY and HEADERS log level</span></span>

<span data-ttu-id="245cf-177">[Log4J 2(영문)](https://logging.apache.org/log4j/2.x/)와 같은 로깅 프레임워크에 출력을 기록해야 하는 경우 [SLF4J 로깅 구현(영문)](https://www.slf4j.org/manual.html)을 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="245cf-177">Bind a [SLF4J logging implementation](https://www.slf4j.org/manual.html) if you need to log output to a logging framework like [Log4J 2](https://logging.apache.org/log4j/2.x/).</span></span>