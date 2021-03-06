---
title: NuGet CLI 서명 명령
description: Nuget.exe 서명 명령에 대 한 참조
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: e941a9f34058f5ebed13a8f68c8cfa23ba5fb6d1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546365"
---
# <a name="sign-command-nuget-cli"></a>sign 명령(NuGet CLI)

**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 4.6 +

인증서를 사용 하 여 첫 번째 인수를 일치 하는 모든 패키지에 서명 합니다. 주체 이름 또는 지문을 제공 하 여 인증서 저장소에 설치 된 인증서 또는 파일에서 개인 키를 사용 하 여 인증서를 가져올 수 있습니다.

아직.NET Core, mono, 또는 Windows 이외의 플랫폼에서에서 패키지 서명이 지원 되지 않습니다.

## <a name="usage"></a>사용법

```cli
nuget sign <package(s)> [options]
```

여기서 `<package(s)>` 는 하나 이상의 `.nupkg` 파일입니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| CertificateFingerprint | 인증서에 대 한 로컬 인증서 저장소를 검색에 사용 된 인증서의 SHA-1(secure 지문을 지정 합니다. |
| CertificatePassword | 필요한 경우 인증서 암호를 지정 합니다. 인증서가 암호로 보호 없는 암호를 제공 하지만 명령을 암호를 묻는 런타임에 경우가 아니면-비 대화형 옵션에 전달 됩니다. |
| CertificatePath | 패키지에 서명 하는 데 사용할 인증서 파일 경로 지정 합니다. |
| CertificateStoreLocation | X.509 인증서 저장소를 사용 하 여 인증서에 대 한 검색의 이름을 지정 합니다. 기본값은 "CurrentUser", 현재 사용자가 사용 되는 X.509 인증서 저장소입니다. -CertificateSubjectName 또는-CertificateFingerprint 옵션을 통해 인증서를 지정 하는 경우이 옵션을 사용할 해야 합니다. |
| CertificateStoreName | 인증서를 검색 하는 데 X.509 인증서 저장소의 이름을 지정 합니다. 기본값은 "My", 개인 인증서용 X.509 인증서 저장소입니다. -CertificateSubjectName 또는-CertificateFingerprint 옵션을 통해 인증서를 지정 하는 경우이 옵션을 사용할 해야 합니다. |
| CertificateSubjectName | 인증서에 대 한 로컬 인증서 저장소를 검색 하는 데 사용 되는 인증서의 주체 이름을 지정 합니다.  검색은 다른 주체 값에 관계 없이 해당 문자열이 포함 된 주체 이름을 가진 모든 인증서를 찾습니다는 제공된 된 값을 사용 하 여 대/소문자 구분 문자열 비교.  인증서 저장소 CertificateStoreName-및-CertificateStoreLocation 옵션에 지정할 수 있습니다. |
| ConfigFile | NuGet 구성 파일을 적용 합니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | 고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| HashAlgorithm | 패키지에 서명 하는 데 사용할 해시 알고리즘입니다. 기본값은 SHA256입니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| OutputDirectory | 서명된 된 패키지를 저장할 디렉터리를 지정 합니다. 기본적으로 서명된 된 패키지는 원본 패키지를 덮어씁니다. |
| 덮어쓰기 | 전환 덮어쓸 경우 현재 서명 해야 합니다. 기본적으로 패키지 서명을 이미 있으면 명령이 실패 합니다. |
| Timestamper | RFC 3161 타임 스탬프 서버 URL입니다. |
| TimestampHashAlgorithm | RFC 3161 타임 스탬프 서버에서 사용할 해시 알고리즘입니다. 기본값은 SHA256입니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |

## <a name="examples"></a>예제

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```