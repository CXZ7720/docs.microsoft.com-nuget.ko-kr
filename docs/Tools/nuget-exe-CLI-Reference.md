---
title: "NuGet CLI (명령줄 인터페이스) 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d777c424-0cf3-4bc0-8abd-7ca16c22192b
description: "Nuget.exe CLI에 대 한 명령줄 참조 인덱스"
keywords: "nuget.exe 참조 인덱스, nuget.exe 명령줄 인터페이스, nuget.exe CLI, nuget 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3d1c3585d8bbf4c9bd9b50c8167e860594a42055
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-cli-reference"></a>NuGet CLI 참조

NuGet 명령줄 인터페이스 (CLI) `nuget.exe`, NuGet 설치, 생성, 게시 및 프로젝트 파일을 변경 하지 않고 패키지를 관리 하는 기능 전체 범위를 제공 합니다.

모든 명령을 사용 하려면 명령 창을 열고 또는 bash 셸은, 다음 실행 `nuget` 명령 한 적절 한 옵션을 같은 순서로 `nuget help pack` (도움말을 보려면 팩 명령에).

## <a name="installing-nugetexe"></a>Nuget.exe를 설치합니다.

[!INCLUDE[install-cli](../includes/install-cli.md)]

## <a name="availability"></a>가용성

- Windows에서 모든 명령을 사용할 수 있습니다.
- 모든 명령을 작업할 [nuget.exe 모노에서 실행 중인](../guides/install-nuget.md#mac-osx-and-linux) 에 대 한 표시 된 위치를 제외 하 고 `pack`, `restore`, 및 `update`합니다.
- `pack`, `restore`, `delete`, `locals`, 및 `push` 명령을 Mac 및 Linux를 통해 사용할 수 있습니다는 [dotnet CLI](dotnet-Commands.md)합니다. 

## <a name="commands-and-applicability"></a>명령 및 적용 가능성

사용 가능한 명령 및 패키지 만들기, 패키지 소비 및/또는 호스트에는 패키지를 게시에 적용 되는지 여부.

| 일반적인 명령 | 해당 하는 역할 | NuGet 버전 | 설명 | 
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | 만들기 | 2.7+ | NuGet 패키지를 만들어 한 `.nuspec` 또는 프로젝트 파일입니다. 모노를 실행 하는 경우 프로젝트 파일에서 패키지를 만드는 지원 되지 않습니다. |
| [push](cli-ref-push.md) | 게시 | 모두 | 패키지 원본에는 패키지를 게시합니다. |
| [구성](cli-ref-config.md) | 모두 | 모두 | NuGet 구성 값을 가져오거나 설정 합니다. |
| [도움말 또는?](cli-ref-help.md) | 모두 | 모두 | 도움말 정보 또는 명령에 대 한 도움말을 표시 합니다. |
| [지역 변수](cli-ref-locals.md) | 소비 | 3.3+ | 지웁니다 또는 다양 한 캐시 또는 전역 패키지 폴더를 패키지를 나열 하거나 해당 폴더를 식별 합니다. |
| [restore](cli-ref-restore.md) | 소비 | 2.7+ | 사용 중인 패키지 참조 형식에서 참조 하는 모든 패키지를 복원 합니다. 모노를 실행할 때 PackageReference 형식을 사용 하 여 패키지를 복원 지원 되지 않습니다. | 
| [setapikey](cli-ref-setapikey.md) | 게시와 소비 | 모두 | 해당 패키지 원본에 대 한 액세스 키가 필요한 경우 지정 된 패키지 소스에 대 한 API 키를 저장 합니다. |
| [사양](cli-ref-spec.md) | 만들기 | 모두 | 생성 된 `.nuspec` 파일을 Visual Studio 프로젝트에서 파일을 생성 하는 경우 토큰을 사용 합니다. |


| 보조 명령 | 해당 하는 역할 | NuGet 버전 | 설명 | 
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | 게시 | 3.3+ | 계층 레이아웃을 사용 하 여 HTTP가 아닌 패키지 소스에 패키지를 추가 합니다. HTTP 소스에 사용할 *푸시*합니다. |
| [delete](cli-ref-delete.md) | 게시 | 모두 | 패키지 소스에서 패키지를 unlists 또는 제거 합니다. |
| [init](cli-ref-init.md) | 만들기 | 3.3+ | 계층 레이아웃을 사용 하 여 패키지 원본 폴더에서 패키지를 추가 합니다. |
| [설치](cli-ref-install.md) | 소비 | 모두 | 설치 패키지를 현재 프로젝트 하지만 프로젝트를 수정 하거나 파일을 참조할지 않습니다. |
| [list](cli-ref-list.md) | 아마도 게시 사용 | 모두 | 지정된 된 원본에서 패키지를 표시합니다. |
| [미러](cli-ref-mirror.md) | 게시 | 3.2 +에서 사용 되지 않습니다. | 패키지 및 종속성 원본에서 대상 저장소에 반영 됩니다. |
| [원본](cli-ref-sources.md) | 소비, 게시 | 모두 | 구성 파일에서 패키지 소스를 관리합니다. |
| [업데이트](cli-ref-update.md) | 소비 | 모두 | 사용 가능한 최신 버전에는 프로젝트의 패키지를 업데이트합니다. 모노에서 실행할 때 지원 되지 않습니다. |

다양 한 명령이 확인 사용의 다양 한 [환경 변수](cli-ref-environment-variables.md)합니다.

적용할 수 역할로 NuGet CLI 명령:

| 역할 | 명령 |
| --- | --- |
| 소비 | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` | 
| 만들기 | `config`, `help`, `init`, `pack`, `spec` |
| 게시 | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

예를 들어 개발자가 관련된 패키지, 사용 된 NuGet 명령의 해당 하위를 이해만 필요 합니다.

> [!Note]
> 명령 옵션 이름은 대/소문자를 구분 하지 않습니다. 사용 되지 않는 옵션에에서 포함 되지 않은이 참조와 같은 `NoPrompt` (으로 대체 `NonInteractive`) 및 `Verbose` (교체 `Verbosity`).