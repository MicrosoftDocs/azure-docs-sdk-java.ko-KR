---
title: "Java용 Azure Active Directory 라이브러리"
description: "Java용 Azure Active Directory 클라이언트 및 관리 라이브러리에 대한 참조 설명서"
keywords: "Azure, Java, SDK, API, SQL, 인증 AAD, Active Directory, Graph, OAuth 2.0"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: active-directory
ms.openlocfilehash: 6226cf0f94b6403ac81ff344eba022420f5e20ea
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2017
---
# <a name="azure-active-directory-libraries-for-java"></a><span data-ttu-id="af8da-104">Java용 Azure Active Directory 라이브러리</span><span class="sxs-lookup"><span data-stu-id="af8da-104">Azure Active Directory libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="af8da-105">개요</span><span class="sxs-lookup"><span data-stu-id="af8da-105">Overview</span></span>

<span data-ttu-id="af8da-106">[Azure Active Directory](/azure/active-directory/active-directory-whatis)를 사용하여 사용자를 로그온하고 응용 프로그램 및 API에 대한 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="af8da-106">Sign-on users and control access to applications and APIs with [Azure Active Directory](/azure/active-directory/active-directory-whatis).</span></span>

<span data-ttu-id="af8da-107">Azure AD를 시작하려면 [Azure AD에서 Java 웹앱 로그인 및 로그아웃](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af8da-107">To get started with Azure AD, see [Java web app sign-in and sign-out with Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="af8da-108">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="af8da-108">Client library</span></span>

<span data-ttu-id="af8da-109">[Java용 ADAL(Active Directory Authentication Library)](https://github.com/AzureAD/azure-activedirectory-library-for-java)을 사용하여 OAuth2, OpenID Connect 또는 Active Directory Graph 인증 및 [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="af8da-109">Configure OAuth2, OpenID Connect, or Active Directory Graph authentication and [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) single-sign on with the [Azure Active Directory authentication library (ADAL) for Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).</span></span>

<span data-ttu-id="af8da-110">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af8da-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="af8da-111">예제</span><span class="sxs-lookup"><span data-stu-id="af8da-111">Example</span></span>

<span data-ttu-id="af8da-112">Azure Active Directory의 [Graph API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api)를 사용하여 Active Directory 테넌트에서 사용자에 대한 JWT(JSON Web Token)를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="af8da-112">Retrieve a JSON Web Token (JWT) for a user in your an Active Directory tenant using Azure Active Directory's [Graph API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api).</span></span> <span data-ttu-id="af8da-113">그런 다음 이 토큰을 사용하여 응용 프로그램 또는 API를 통해 해당 사용자를 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af8da-113">This token can then be used to authenticate the user with an application or API.</span></span>

```java
ExecutorService service = Executors.newFixedThreadPool(1);
AuthenticationContext context = new AuthenticationContext(AUTHORITY, false, service);
Future<AuthenticationResult> future = context.acquireToken(
    "https://graph.windows.net", YOUR_TENANT_ID, username, password,
    null);
AuthenticationResult result = future.get();
System.out.println("Access Token - " + result.getAccessToken());
System.out.println("Refresh Token - " + result.getRefreshToken());
System.out.println("ID Token - " + result.getIdToken());
```

## <a name="management-api"></a><span data-ttu-id="af8da-114">관리 API</span><span class="sxs-lookup"><span data-stu-id="af8da-114">Management API</span></span>

<span data-ttu-id="af8da-115">관리 API를 사용하여 [역할 기반 액세스 제어](/azure/active-directory/role-based-access-control-what-is)를 구성하고 ID(예: 사용자 및 [서비스 사용자](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects))를 해당 역할에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="af8da-115">Configure [role based access control](/azure/active-directory/role-based-access-control-what-is) and assign identities (such as users and [service principals](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects)) to those roles with the management API.</span></span> 

<span data-ttu-id="af8da-116">`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af8da-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-graph-rbac</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="af8da-117">예제</span><span class="sxs-lookup"><span data-stu-id="af8da-117">Example</span></span> 

<span data-ttu-id="af8da-118">새 서비스 사용자를 만들고 참가자 역할을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="af8da-118">Create a new service principal and assign it the Contributor role.</span></span>

```java
ServicePrincipal sp = Azure.servicePrincipals().define(spName)
    .withNewApplication("http://" + spName)
    .create();
RoleAssignment roleAssignment2 = authenticated.roleAssignments()
    .define("contribRoleAssignment")
    .forServicePrincipal(sp)
    .withBuiltInRole(BuiltInRole.CONTRIBUTOR)
    .withSubscriptionScope("862f67bc-d3ae-4243-bec7-3da6dca77717")
    .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="af8da-119">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="af8da-119">Explore the Management APIs</span></span>](/java/api/overview/azure/activedirectory/managementapi)


## <a name="samples"></a><span data-ttu-id="af8da-120">샘플</span><span class="sxs-lookup"><span data-stu-id="af8da-120">Samples</span></span>

<span data-ttu-id="af8da-121">[그룹, 사용자 및 역할 관리](https://github.com/Azure-Samples/aad-java-browse-graph-and-manage-roles)  </span><span class="sxs-lookup"><span data-stu-id="af8da-121">[Manage groups, users, and roles](https://github.com/Azure-Samples/aad-java-browse-graph-and-manage-roles)  </span></span>  
<span data-ttu-id="af8da-122">[Java 웹앱에서 사용자 로그인 및 로그아웃(영문)](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  </span><span class="sxs-lookup"><span data-stu-id="af8da-122">[Sign-in and sign-out users in a Java web app](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  </span></span>  
<span data-ttu-id="af8da-123">[명령줄 앱을 사용하여 Azure AD에서 API 액세스(영문)](https://github.com/Azure-Samples/active-directory-java-native-headless) </span><span class="sxs-lookup"><span data-stu-id="af8da-123">[Access an API with Azure AD using a command line app](https://github.com/Azure-Samples/active-directory-java-native-headless) </span></span>  
[<span data-ttu-id="af8da-124">Java 웹앱에서 활성 AD Graph API 호출(영문)</span><span class="sxs-lookup"><span data-stu-id="af8da-124">Call the Active AD Graph API from your Java web app</span></span>](https://github.com/Azure-Samples/active-directory-java-graphapi-web/)  

<span data-ttu-id="af8da-125">앱에서 사용할 수 있는 [Azure AD용 Java 샘플 코드](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="af8da-125">Explore more [sample Java code for Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java) you can use in your apps.</span></span>