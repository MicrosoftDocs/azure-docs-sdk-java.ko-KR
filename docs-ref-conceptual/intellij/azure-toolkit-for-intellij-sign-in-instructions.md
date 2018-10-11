---
title: IntelliJ용 Azure 도구 키트에 대한 로그인 지침
description: IntelliJ용 Azure 도구 키트를 사용하여 Microsoft Azure에 로그인하는 방법을 알아봅니다.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 4e24dac285fa38bad4293f1cce2830242c2fe151
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893204"
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a>IntelliJ용 Azure 도구 키트에 대한 로그인 지침

IntelliJ용 Azure 도구 키트는 Azure 계정에 로그인하는 두 가지 방법을 제공합니다.

  * **자동**: 자동으로 Azure 계정에 로그인하는 데 사용할 수 있는 자격 증명 파일을 만듭니다.
  * **대화형**: Azure 계정에 로그인할 때마다 Azure 자격 증명을 입력합니다.

다음 섹션에서는 각 방법을 사용하는 방법을 설명합니다.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-automatically"></a>Azure 계정에 자동으로 로그인

이 섹션에서는 서비스 주체 데이터를 포함하는 자격 증명 파일을 만드는 과정을 안내합니다. 이 프로세스를 완료하면 Eclipse에서는 사용자가 프로젝트를 열 때마다 해당 자격 증명 파일을 사용해서 자동으로 Azure에 자동으로 로그인합니다.

1. IntelliJ IDEA로 프로젝트를 엽니다.

1. **도구** 메뉴에서 **Azure**를 가리킨 다음, **Azure 로그인**을 클릭합니다.

   ![IntelliJ Azure 로그인 명령][A01]

1. **Azure 로그인** 창에서 **자동**을 선택한 다음 **새로 만들기**를 클릭합니다.

   ![선택한 자동을 통한 Azure 로그인 창][A02]

1. **Azure 로그인 대화 상자** 창에서 Azure 자격 증명을 입력한 다음, **로그인**을 클릭합니다.

   ![Azure 로그인 대화 상자 창][A03]

1. **인증 파일 만들기** 창에서 사용할 구독을 선택하고 대상 디렉터리를 선택한 다음, **시작**을 클릭합니다.

   ![인증 파일 만들기 창][A04]

1. **서비스 주체 만들기 상태** 대화 상자에서 파일을 성공적으로 만든 후 **확인**을 클릭합니다.

   ![서비스 주체 만들기 상태 대화 상자][A05]

1. **Azure 로그인** 창에서 **로그인**을 클릭합니다.

   ![Azure 로그인 대화 상자][A06]

1. **구독 선택** 대화 상자에서 사용하려는 구독을 선택한 다음, **확인**을 클릭합니다.

   ![구독 선택 대화 상자][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>자동으로 로그인한 후 Azure 계정에서 로그아웃

이전 단계를 사용하여 계정을 구성한 후에는 Azure 도구 키트는 IntelliJ IDEA를 다시 시작할 때마다 Azure 계정에 자동으로 로그인합니다. 그러나 Azure 계정에서 로그아웃하고 Azure 도구 키트가 자동으로 로그인하지 않도록 하려면 다음을 수행합니다.

1. IntelliJ IDEA에서 **도구** 메뉴에서 **Azure**를 가리킨 다음, **Azure 로그아웃**을 클릭합니다.

   ![IntelliJ Azure 로그아웃 명령][L01]

1. **Azure 로그아웃** 확인 창에서 **예**를 클릭합니다.

   ![Azure 로그아웃 확인 창][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a>기존 자격 증명 파일을 사용하여 자동으로 Azure 계정에 로그인

IntelliJ IDEA를 사용할 때 Azure 계정에서 로그아웃하는 경우 기존 자격 증명 파일을 사용하여 계정에 자동으로 다시 로그인해야 합니다. 기존 자격 증명을 사용하도록 Eclipse용 Azure 도구 키트를 구성하려면 다음을 수행합니다.

1. IntelliJ IDEA로 프로젝트를 엽니다.

1. **도구** 메뉴에서 **Azure**를 가리킨 다음, **Azure 로그인**을 클릭합니다.

   ![IntelliJ Azure 로그인 명령][A01]

1. **Azure 로그인** 창에서 **자동**을 선택한 다음 **찾아보기**를 클릭합니다.

   ![선택한 자동을 통한 Azure 로그인 창][A02]

1. **인증 파일 선택** 대화 상자에서 이전에 만든 자격 증명 파일을 선택한 다음, **선택**을 클릭합니다.

   ![인증 파일 선택 대화 상자][A08]

1. **Azure 로그인** 창에서 **로그인**을 클릭합니다.

   ![선택한 자동을 통한 Azure 로그인 창][A06]

1. **구독 선택** 대화 상자에서 사용하려는 구독을 선택한 다음, **확인**을 클릭합니다.

   ![구독 선택 대화 상자][A07]

## <a name="sign-in-to-your-azure-account-interactively"></a>대화형으로 Azure 계정에 로그인

Azure 자격 증명을 수동으로 입력하여 Azure에 로그인하려면 다음을 수행합니다.

1. IntelliJ IDEA로 프로젝트를 엽니다.

1. **도구**를 클릭하고 **Azure**를 가리킨 다음, **Azure 로그인**을 클릭합니다.

   ![IntelliJ Azure 로그인 명령][I01]

1. **Azure 로그인** 창에서 **대화형**을 선택한 다음 **로그인**을 클릭합니다.

   ![선택한 대화형을 사용한 Azure 로그인 창][I02]

1. **Azure 로그인** 대화 상자가 나타나면 Azure 자격 증명을 입력한 다음, **로그인**을 클릭합니다.

   ![Azure 로그인 대화 상자 창][I03]

1. **구독 선택** 대화 상자에서 사용하려는 구독을 선택한 다음, **확인**을 클릭합니다.

   ![구독 선택 대화 상자][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>대화형으로 로그인한 후 Azure 계정에서 로그아웃

이전 단계를 사용하여 계정을 구성한 후에는 IntelliJ IDEA를 다시 시작할 때마다 Azure 계정에서 자동으로 로그아웃됩니다. 그러나 IntelliJ IDEA를 다시 시작하지 *않고* Azure 계정에서 로그아웃하려면 다음을 수행합니다.

1. IntelliJ IDEA에서 **도구** 메뉴에서 **Azure**를 가리킨 다음, **Azure 로그아웃**을 클릭합니다.

   ![IntelliJ Azure 로그아웃 명령][L01]

1. **Azure 로그아웃** 확인 창에서 **예**를 클릭합니다.

   ![Azure 로그아웃 확인 창][L02]

## <a name="next-steps"></a>다음 단계

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

<!-- IMG List -->

[I01]: media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
