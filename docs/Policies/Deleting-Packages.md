---
title: "nuget.org에서 NuGet 패키지 삭제 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a348ca2e-0a5d-40ad-ba33-9bb37e1d980b
description: "nuget.org에서 패키지를 제외하는 정책; 패키지가 다른 정책을 위반하는 경우를 제외하고 영구 삭제가 지원되지 않습니다."
keywords: "NuGet 패키지 삭제, NuGet 패키지 제외, 패키지 사용 금지"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 331979bdc3703ddbeff18e2bd0e6b0a17551e68b
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="deleting-packages"></a>패키지 삭제

nuget.org에서는 패키지를 영구적으로 삭제하도록 지원하지 않습니다. 이렇게 하면 특히 패키지 복원을 포함하는 빌드 워크플로를 사용하여 패키지의 사용 가능성에 따라 모든 프로젝트를 중단합니다.

nuget.org에서는 패키지를 *제외*하도록 지원하지 않습니다. 이 기능은 웹 사이트의 패키지 관리 페이지에서 수행될 수 있습니다. 제외된 패키지는 nuget.org 또는 Visual Studio UI에 표시되지 않으며 검색 결과에도 표시되지 않습니다. 그러나 패키지 복원을 지원하는 정확한 버전 번호를 사용하여 제외된 패키지를 다운로드하고 설치할 수 있습니다. 또한 다음과 같은 특정 시나리오에서 제외된 패키지를 계속 검색할 수 있습니다.

- 버전 또는 종속성 제약 조건과 일치하는 최신 사용 가능한 패키지가 제외된 패키지인 경우 부동 버전을 사용하는 패키지 복원(예: `1.0.0-*`)
- 카탈로그를 통한 패키지의 복제(카탈로그에 제외된 패키지가 포함된 경우)

## <a name="exceptions"></a>예외

저작권 침해 및 잠재적으로 위험한 콘텐츠와 같은 예외적인 상황에 NuGet 팀에서 패키지를 수동으로 삭제할 수 있습니다. [NuGet 갤러리](http://www.nuget.org)를 통해 지원 요청을 제출하여 프로세스를 시작합니다.

## <a name="prohibited-use"></a>사용 금지

패키지가 다음 조건 중 하나를 충족하는 경우 공용 NuGet 갤러리에서 허용되지 않으며 토론 없이 즉시 제거됩니다. 그러나 패키지 소유자는 제거되었다는 알림을 받습니다.

- 맬웨어, 애드웨어 또는 어떠한 종류의 스파이웨어가 포함됩니다.
- 개발자의 워크스테이션 또는 해당 조직을 손상시키도록 설계되었습니다.
- 저작권을 침해하거나 라이선스를 위반합니다.
- 위법 콘텐츠가 포함됩니다.
- 생산성 0인 콘텐츠가 있는 패키지를 포함하여 패키지 식별자를 점유하는 데 사용됩니다. 패키지에는 코드가 포함되어야 합니다. 또는 소유자는 실제로 제품을 제공할 사람에게 식별자를 제공해야 합니다.
- 갤러리가 수행하도록 명시적으로 설계되지 않은 작업을 수행하도록 합니다.

이러한 항목에 위반되는 패키지를 찾는 경우 패키지 세부 정보 페이지에서 **신고하기** 링크를 클릭하고 보고서를 제출합니다.

NuGet 팀 및 .NET Foundation은 언제든지 이러한 조건을 변경할 권리를 갖습니다.