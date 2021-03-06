---
title: NuGet 패키지 서명
description: 서명된 패키지를 사용하여 콘텐츠 무결성 검사를 활성화하는 방법을 설명합니다.
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: c598461831323ecfcc5da3877df71bd8d69557f6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551980"
---
# <a name="signing-nuget-packages"></a>NuGet 패키지 서명

패키지 서명은 패키지가 생성된 후 수정되지 않았는지 확인하는 프로세스입니다.

## <a name="prerequisites"></a>전제 조건

1. 서명할 패키지(`.nupkg` 파일)입니다. [패키지 만들기](creating-a-package.md)를 참조하세요.

1. nuget.exe 4.6.0 이상. [NuGet CLI 설치](../install-nuget-client-tools.md#nugetexe-cli) 방법을 참조하세요.

1. [코드 서명 인증서](../reference/signed-packages-reference.md#get-a-code-signing-certificate).

## <a name="sign-a-package"></a>패키지 서명

패키지에 서명하려면 [nuget 기호](../tools/cli-ref-sign.md)를 사용하세요.

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

명령 참조에서 설명한 것처럼 인증서 저장소에 있는 인증서나 파일의 인증서를 사용할 수 있습니다.

### <a name="common-problems-when-signing-a-package"></a>패키지에 서명 시 발생하는 일반적인 문제

- 인증서가 코드 서명에 적합하지 않습니다. 지정된 인증서에 적절한 확장 키 사용(EKU 1.3.6.1.5.5.7.3.3)이 있어야 합니다.
- 인증서가 RSA SHA-256 서명 알고리즘 또는 공개 키 2048비트 이상과 같은 기본 요구 사항을 충족하지 않습니다.
- 인증서가 만료 또는 해지되었습니다.
- 타임스탬프 서버가 인증서 요구 사항을 충족하지 않습니다.

> [!Note]
> 서명 인증서가 만료된 경우 서명된 패키지에 서명이 유효하다는 것을 확인해 주는 타임스탬프가 포함되어 있어야 합니다. 타임스탬프 없이 서명할 경우 서명 작업 시 [경고 NU3002](../reference/errors-and-warnings/NU3002.md)가 발생합니다.

## <a name="verify-a-signed-package"></a>서명된 패키지 확인

특정 패키지의 서명 정보를 확인하려면 [nuget verify](../tools/cli-ref-verify.md)를 사용합니다.

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a>서명된 패키지 설치

서명된 패키지는 특별한 조치 없이 설치할 수 있지만 패키지가 서명된 이후에 내용이 수정된 경우 설치가 차단되고 [오류 NU3008](../reference/errors-and-warnings/NU3008.md)이 발생합니다.

> [!Warning]
> 신뢰할 수 없는 인증서로 서명된 패키지는 서명되지 않은 것으로 간주되고, 다른 서명되지 않은 패키지처럼 경고나 오류 없이 설치됩니다.

## <a name="see-also"></a>참고 항목

[서명된 패키지 참조](../reference/Signed-Packages-Reference.md)
