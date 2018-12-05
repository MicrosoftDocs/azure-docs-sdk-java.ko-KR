---
title: Java CA 저장소에 Azure 루트 인증서 추가
description: Java CA(인증 기관) 루트 인증서(cacerts) 저장소에 Microsoft Azure용 CA 인증서를 추가하는 방법에 대해 알아봅니다.
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/13/2018
ms.author: robmcm
ms.openlocfilehash: 477cb9347255928f8583af8fbe4ea90a42ce6c18
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339047"
---
# <a name="adding-a-root-certificate-to-the-java-ca-certificates-store"></a><span data-ttu-id="4a888-103">Java CA 인증서 저장소에 루트 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="4a888-103">Adding a root certificate to the Java CA certificates store</span></span>

<span data-ttu-id="4a888-104">Azure 서비스(예: Azure Service Bus)를 사용하는 응용 프로그램은 Baltimore CyberTrust Root 인증서를 신뢰해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-104">Applications that use Azure services (such as Azure Service Bus) need to trust the Baltimore CyberTrust root certificate.</span></span> <span data-ttu-id="4a888-105">이 인증서는 시스템에 이미 설치되어 있을 수도 있지만, 이 자습서의 단계에서는 오라클의  **keytool**을 사용하여 Java CA(cacerts) 저장소에 Azure 서비스에 사용할 필요한 CA(인증 기관) 루트 인증서를 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-105">This certificate may already be installed on your system, but if it is not, the steps in this tutorial will show you how to use Oracle's **keytool** to add the required certificate authority (CA) root certificate to the Java CA certificate (cacerts) store that you will use for Azure services.</span></span>

<span data-ttu-id="4a888-106">오라클의 keytool 유틸리티는 _키 및 인증서 관리 도구_이며, 개발자는 Java에서 사용할 신뢰할 수 있는 인증서 목록을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-106">Oracle's keytool utility is a _Key and Certificate Management Tool_, which allows developers to manage the list of trusted certificates for use with Java.</span></span> <span data-ttu-id="4a888-107">JDK를 압축하고 Azure 프로젝트의 **approot** 폴더에 추가하기 전에 keytool을 사용하여 CA 인증서를 추가하거나 keytool을 사용하여 인증서를 추가하는 Azure 시작 작업을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-107">You can use keytool to add the CA certificate before zipping your JDK and adding it to your Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool to add the certificate.</span></span>

<span data-ttu-id="4a888-108">2013년 4월 15일부터 Azure는 GTE CyberTrust Global Root 인증서에서 Baltimore CyberTrust Root 인증서로 마이그레이션을 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-108">Beginning April 15, 2013, Azure began migrating from the GTE CyberTrust Global root certificate to the Baltimore CyberTrust root certificate.</span></span> <span data-ttu-id="4a888-109">다음 단계에서는 keytool을 사용하여 Java CA 인증서(cacerts) 저장소에 Baltimore CyberTrust 루트 인증서를 추가하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-109">The following steps show you how to use keytool to add the Baltimore CyberTrust root certificate to your Java CA certificate (cacerts) store.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="4a888-110">이 문서의 단계를 사용하여 다른 신뢰할 수 있는 인증 기관의 루트 인증서를 신뢰하도록 Java SDK를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-110">You can use the steps in this article to configure your Java SDK to trust the root certificates from other trusted certificate authorities.</span></span> <span data-ttu-id="4a888-111">예를 들어, [GeoTrust 루트 인증서](http://www.geotrust.com/resources/root-certificates/)의 인증서 목록에서 루트 인증서를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-111">For example, you might choose a root certificate from the list of certificates at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span></span>
> 

## <a name="determining-which-root-certificates-are-installed"></a><span data-ttu-id="4a888-112">어떤 루트 인증서가 설치되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="4a888-112">Determining which root certificates are installed</span></span>

<span data-ttu-id="4a888-113">Baltimore 인증서가 cacerts 저장소에 이미 설치되어 있을 수 있으므로 다음 단계를 사용하여 이미 설치되어 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-113">The Baltimore certificate might already be installed in your cacerts store, so you need to use the following steps to determine if it has already been installed.</span></span>

1. <span data-ttu-id="4a888-114">관리자 명령 프롬프트에서 JDK의 **jdk\jre\lib \security** 폴더로 이동한 후 다음 명령을 실행하여 시스템에 설치된 인증서를 나열하십시오.</span><span class="sxs-lookup"><span data-stu-id="4a888-114">At an administrator command prompt, navigate to your JDK's **jdk\jre\lib\security** folder, and then run the following command to list the certificates that are installed on your system:</span></span>

   ```shell
   keytool -list -keystore cacerts
   ```

1. <span data-ttu-id="4a888-115">저장소 암호를 묻는 경우, 기본 암호는 **changeit**입니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-115">If you are prompted for the store password, the default password is **changeit**.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="4a888-116">저장소 암호를 변경하려면 <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>의 keytool 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a888-116">If you want to change the store password, see the keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>
   > 

1. <span data-ttu-id="4a888-117">`d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`의 지문 인증서가 보이지 않으면, 다음 섹션의 단계를 사용하여 인증서를 다운로드하고 설치하십시오.</span><span class="sxs-lookup"><span data-stu-id="4a888-117">If you do not see the certificate with the thumbprint of `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, use the steps in the following section to download and install the certificate.</span></span>

## <a name="to-add-a-root-certificate-to-the-cacerts-store"></a><span data-ttu-id="4a888-118">cacerts 저장소에 루트 인증서를 추가하려면</span><span class="sxs-lookup"><span data-stu-id="4a888-118">To add a root certificate to the cacerts store</span></span>

1. <span data-ttu-id="4a888-119"><https://cacert.omniroot.com/bc2025.crt>에서 Baltimore CyberTrust 루트 인증서를 다운로드하고, **.cer** 확장자로 **jdk\jre\lib\security** 폴더에 로컬 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-119">Download the Baltimore CyberTrust root certificate from <https://cacert.omniroot.com/bc2025.crt>, and save to a local file with extension **.cer** in your **jdk\jre\lib\security** folder.</span></span> <span data-ttu-id="4a888-120">본 예에서는 Baltimore CyberTrust 루트 인증서 파일을 **bc2025.cer**로 다운로드한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-120">For this example, assume that you downloaded the Baltimore CyberTrust root certificate file as **bc2025.cer**.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="4a888-121">Baltimore CyberTrust 루트 인증서의 시리얼 번호는 `02:00:00:b9`이며, SHA1 지문은 `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`입니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-121">The Baltimore CyberTrust root certificate has a serial number of `02:00:00:b9`, and a SHA1 thumbprint of `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.</span></span>
   > 

2. <span data-ttu-id="4a888-122">다음 명령을 사용하여 cacerts 저장소로 인증서를 가져오기 합니다:</span><span class="sxs-lookup"><span data-stu-id="4a888-122">Import the certificate to the cacerts store by using the following command:</span></span>

   ```shell
   keytool -keystore cacerts -importcert -alias bc2025ca -file bc2025.cer
   ```
   <span data-ttu-id="4a888-123">위치:</span><span class="sxs-lookup"><span data-stu-id="4a888-123">Where:</span></span>

   |  <span data-ttu-id="4a888-124">매개 변수</span><span class="sxs-lookup"><span data-stu-id="4a888-124">Parameter</span></span>   |                              <span data-ttu-id="4a888-125">설명</span><span class="sxs-lookup"><span data-stu-id="4a888-125">Description</span></span>                               |
   |--------------|------------------------------------------------------------------------|
   | `keystore`   | <span data-ttu-id="4a888-126">인증서 저장소 지정.</span><span class="sxs-lookup"><span data-stu-id="4a888-126">Specifies the certificate store.</span></span>                                       |
   | `importcert` | <span data-ttu-id="4a888-127">인증서를 가져오고 있다는 것을 지정.</span><span class="sxs-lookup"><span data-stu-id="4a888-127">Specifies that you are importing a certificate.</span></span>                        |
   | `alias`      | <span data-ttu-id="4a888-128">해당 인증서의 별칭을 지정.</span><span class="sxs-lookup"><span data-stu-id="4a888-128">Specifies an alias for the certificate.</span></span>                                |
   | `file`       | <span data-ttu-id="4a888-129">가져오기 하는 루트 인증서의 파일명을 지정.</span><span class="sxs-lookup"><span data-stu-id="4a888-129">Specifies the filename of the root certificate that you are importing.</span></span> |


3. <span data-ttu-id="4a888-130">인증서를 신뢰하라는 메시지가 뜨면 지문을 `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`로 검증하고, 지문이 올바른 경우 **y**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-130">If you are prompted to trust the certificate, verify the thumbprint as `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, and type **y** if the thumbprint is correct.</span></span>

4. <span data-ttu-id="4a888-131">다음 명령을 실행하여 CA 인증서를 가져왔는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-131">Run the following command to ensure the CA certificate has been successfully imported:</span></span>

   ```shell
   keytool -list -keystore cacerts
   ```

<span data-ttu-id="4a888-132">JDK에 루트 인증서를 성공적으로 추가한 후에는 JDK의 내용을 압축하여 Azure 프로젝트의  **approot** 폴더에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-132">After you have successfully added the root certificate to your JDK, you can zip the contents of JDK and add it to your Azure project's **approot** folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a888-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4a888-133">Next steps</span></span>

<span data-ttu-id="4a888-134">keytool 유틸리티에 대한 자세한 내용은, <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4a888-134">For more information about the keytool utility, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>

<span data-ttu-id="4a888-135">Java에 대한 자세한 내용은 [Java 개발자용 Azure](/java/azure)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a888-135">For more information about Java, see [Azure for Java developers](/java/azure).</span></span>

<!-- For more information about the root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx). -->

<span data-ttu-id="4a888-136">Azure에서 개발하는 경우 사용 가능한 지원되는 JDK에 대한 자세한 내용은 <https://aka.ms/azure-jdks>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a888-136">For more information about the supported JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>