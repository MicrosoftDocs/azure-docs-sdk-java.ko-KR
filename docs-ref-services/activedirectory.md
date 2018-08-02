---
title: Java용 Azure Active Directory 라이브러리
description: Java용 Azure Active Directory 클라이언트 및 관리 라이브러리에 대한 참조 설명서
keywords: Azure, Java, SDK, API, SQL, 인증 AAD, Active Directory, Graph, OAuth 2.0
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: active-directory
ms.openlocfilehash: e51334b4f13ffc457d4dec1785257dcff1b56b08
ms.sourcegitcommit: c4238cffdf6c6f7ac8725673260a34a38c566f58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39418978"
---
# <a name="azure-active-directory-libraries-for-java"></a>Java용 Azure Active Directory 라이브러리

## <a name="overview"></a>개요

[Azure Active Directory](/azure/active-directory/active-directory-whatis)를 사용하여 사용자를 로그온하고 응용 프로그램 및 API에 대한 액세스를 제어합니다.

Azure AD를 시작하려면 [Azure AD에서 Java 웹앱 로그인 및 로그아웃](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java)을 참조하세요.

## <a name="client-library"></a>클라이언트 라이브러리

[Java용 ADAL(Active Directory Authentication Library)](https://github.com/AzureAD/azure-activedirectory-library-for-java)을 사용하여 OAuth2, OpenID Connect 또는 Active Directory Graph 인증 및 [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) Single Sign-On을 구성합니다.

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 클라이언트 라이브러리를 사용합니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="example"></a>예

Azure Active Directory의 [Graph API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api)를 사용하여 Active Directory 테넌트에서 사용자에 대한 JWT(JSON Web Token)를 검색합니다. 그런 다음 이 토큰을 사용하여 응용 프로그램 또는 API를 통해 해당 사용자를 인증할 수 있습니다.

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

## <a name="management-api"></a>관리 API

관리 API를 사용하여 [역할 기반 액세스 제어](/azure/active-directory/role-based-access-control-what-is)를 구성하고 ID(예: 사용자 및 [서비스 사용자](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects))를 해당 역할에 할당합니다. 

`pom.xml` Maven 파일에 [종속성을 추가](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies)하여 프로젝트에서 관리 API를 사용합니다.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-graph-rbac</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a>예 

새 서비스 사용자를 만들고 참가자 역할을 지정합니다.

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
> [관리 API 탐색](/java/api/overview/azure/activedirectory/management)


## <a name="samples"></a>샘플

[그룹, 사용자 및 역할 관리](https://github.com/Azure-Samples/aad-java-manage-users-groups-and-roles)    
[Java 웹앱에서 사용자 로그인 및 로그아웃(영문)](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)    
[명령줄 앱을 사용하여 Azure AD에서 API 액세스(영문)](https://github.com/Azure-Samples/active-directory-java-native-headless)   
[Java 웹앱에서 활성 AD Graph API 호출(영문)](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  

앱에서 사용할 수 있는 [Azure AD용 Java 샘플 코드](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java)를 추가로 탐색합니다.
