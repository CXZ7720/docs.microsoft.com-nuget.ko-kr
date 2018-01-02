---
title: "NuGet CLI delete 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Nuget.exe delete 명령에 대 한 참조"
keywords: "nuget 참조를 삭제, 삭제 패키지 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a>delete 명령 (NuGet CLI)

**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 모든

삭제 하거나 unlists 패키지 소스에서 패키지 합니다. Nuget.org를 delete 명령에 대 한 [패키지 unlists](../policies/Deleting-Packages.md)합니다.

## <a name="usage"></a>용도

```
nuget delete <packageID> <packageVersion> [options]
```

여기서 `<packageID>` 및 `<packageVersion>` 정확 하 게 패키지를 삭제 하거나 unlist 식별 합니다. 정확한 동작은 소스에 따라 달라 집니다. 로컬 폴더에 대 한 예를 들어, 패키지가 삭제 되었습니다. nuget.org에 대 한 패키지는 나열 되지 않습니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| apiKey | 대상 저장소에 대 한 API 키입니다. 없음, 1에 지정 된 경우 *%AppData%\NuGet\NuGet.Config* 사용 됩니다. |
| ConfigFile | *(2.5 +)*  NuGet 구성 파일을 적용 합니다. 지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다. |
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| 비 대화형 | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 소스 | 서버 URL을 지정합니다. Nuget.org의 URL은 `https://api.nuget.org/v3/index.json`합니다. 개인 피드 대신 호스트 이름, 예를 들어 *%hostname%/api/v3*합니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *세부 (2.5 이상)*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```