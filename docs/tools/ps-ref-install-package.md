---
title: NuGet에서 Install-package PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 Install-package PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: e7ddf9ad97cbb4ec9cfc8b01f366511239f41416
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546028"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Visual Studio의 패키지 관리자 콘솔)

*내에서 명령에 설명 합니다 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows의 Visual Studio에서 합니다. 일반 PowerShell Install-package 명령에 대 한 참조를 [PowerShell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)합니다.*

프로젝트에 패키지 및 해당 종속성을 설치합니다.

## <a name="syntax"></a>구문

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

Nuget 2.8 + `Install-Package` 프로젝트에서 기존 패키지를 다운 그레이드할 수 있습니다. 예를 들어 Microsoft.AspNet.MVC 5.1.0-rc1 설치 된 경우 다음 명령을 다운 그레이드 하 고 5.0.0에:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| ID | (필수) 설치 패키지의 식별자입니다. (*3.0 이상*) 경로 또는 URL 식별자 수는 `packages.config` 파일 또는 `.nupkg` 파일입니다. -Id 자체 스위치는 선택 사항입니다. |
| IgnoreDependencies | 이 패키지에만 및 해당 종속성 없습니다를 설치 합니다. |
| ProjectName | 기본 프로젝트에 기본적으로 패키지를 설치 하는 프로젝트입니다. |
| 소스 | 검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다. 생략 하면 `Install-Package` 현재 선택된 된 패키지 소스를 검색 합니다. |
| 버전 | 를 설치 하려면 패키지 버전을 최신 버전을 기본값으로 설정 합니다. |
| IncludePrerelease | 시험판 패키지 설치를 고려합니다. 생략 하면 안정적인 패키지만 간주 됩니다. |
| FileConflictAction | 덮어쓰거나 프로젝트에서 참조 하는 기존 파일을 무시 하 라는 메시지가 표시 되는 경우 수행할 동작입니다. 가능한 값은 *덮어쓰기, Ignore, None, OverwriteAll*, 및 *(3.0 이상)* *IgnoreAll*합니다. |
| DependencyVersion | 다음 중 하나일 수 있습니다를 사용 하려면 종속성 패키지의 버전:<br/><ul><li>*가장 낮은* (기본값): 가장 낮은 버전</li><li>*HighestPatch*: 가장 낮은 주요, 가장 낮은 부 최고 패치 버전</li><li>*HighestMinor*: 가장 낮은 주 버전, 가장 높은 보조, 최고의 패치</li><li>*가장 높은* (매개 변수 없이 사용 하 여 업데이트 패키지에 대 한 기본값): 가장 높은 버전</li></ul>사용 하 여 기본 값을 설정할 수 있습니다 합니다 [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) 에서 설정 된 `Nuget.Config` 파일. |
| WhatIf | 실제로 설치를 수행 하지 않고 명령을 실행할 때 발생할 상황을 보여 줍니다. |

이러한 매개 변수 중 파이프라인 입력 하거나 와일드 카드 문자 허용 합니다.

## <a name="common-parameters"></a>일반 매개 변수

`Install-Package` 다음을 지원 합니다 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, 자세한 정보 표시, WarningAction, WarningVariable.

## <a name="examples"></a>예제

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
