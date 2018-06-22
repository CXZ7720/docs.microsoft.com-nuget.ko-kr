---
title: NuGet 2.8.2 릴리스 정보
description: NuGet 2.8.2 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a004c250d60a4ed1ca8dede1e83b2a68e10299bf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821332"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="237e1-103">NuGet 2.8.2 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="237e1-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="237e1-104">[NuGet 2.8.1 릴리스 정보](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 릴리스 정보](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="237e1-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="237e1-105">NuGet 2.8.2 2014 년 5 월 22 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="237e1-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="237e1-106">이 릴리스에서 명령줄 nuget.exe, NuGet.Server 패키지 및 기타 NuGet 패키지에 대 한 변경만 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="237e1-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="237e1-107">릴리스는 업데이트 된 Visual Studio 확장명 또는 WebMatrix 확장 포함 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="237e1-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="237e1-108">주목할 만한 업데이트</span><span class="sxs-lookup"><span data-stu-id="237e1-108">Notable Updates</span></span>

<span data-ttu-id="237e1-109">가장 주목할 만한 업데이트 명령줄 nuget.exe 및 자체 호스트 된 NuGet 피드) (용 NuGet.Server 패키지에 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="237e1-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="237e1-110">Nuget.exe 중요 한 버그 수정</span><span class="sxs-lookup"><span data-stu-id="237e1-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="237e1-111">nuget.exe 푸시 실패 하 고 다시 시도 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="237e1-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="237e1-112">nuget.exe 푸시 기본 인증 자격 증명을 올바르게 전송 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="237e1-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="237e1-113">nuget.exe 푸시 임시 리디렉션 수행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="237e1-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="237e1-114">중요 한 NuGet.Server 버그 수정</span><span class="sxs-lookup"><span data-stu-id="237e1-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="237e1-115">NuGet.Server 반환한 IsAbsoluteLatestVersion의 잘못 된 값</span><span class="sxs-lookup"><span data-stu-id="237e1-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="237e1-116">업데이트 패키지</span><span class="sxs-lookup"><span data-stu-id="237e1-116">Packages Updated</span></span>

<span data-ttu-id="237e1-117">Nuget.exe 명령줄 및 NuGet.Server 수정에 NuGet 패키지에 대 한 업데이트로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="237e1-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="237e1-118">다른 패키지도 2.8.2로 업데이트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="237e1-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="237e1-119">업데이트 된 패키지 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="237e1-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="237e1-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="237e1-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="237e1-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="237e1-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="237e1-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="237e1-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="237e1-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="237e1-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="237e1-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (패키지, 확장명이 아닌)</span><span class="sxs-lookup"><span data-stu-id="237e1-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="237e1-125">모든 변경 내용</span><span class="sxs-lookup"><span data-stu-id="237e1-125">All Changes</span></span>
<span data-ttu-id="237e1-126">릴리스가 10 읽어 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="237e1-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="237e1-127">작업의 전체 목록에 대 한 항목에서에서 수정 된 NuGet 2.8.2, 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)합니다.</span><span class="sxs-lookup"><span data-stu-id="237e1-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>