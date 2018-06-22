---
title: NuGet에 대 한.NET 컴파일러 플랫폼 분석기 형식
description: API 또는 라이브러리를 구현하는 NuGet 패키지를 포함하여 패키지되고 배포되는 .NET 분석기 규칙입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: dc5896631fa3b15dcc1b84b054cb532d56193f36
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818388"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="d9d96-103">NuGet 분석기 형식</span><span class="sxs-lookup"><span data-stu-id="d9d96-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="d9d96-104">.NET 컴파일러 플랫폼 (라고도 "Roslyn") 만들 수 [분석기](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) 검사 하는 코드의 의미 및 구문 트리를 기록할 때.</span><span class="sxs-lookup"><span data-stu-id="d9d96-104">The .NET Compiler Platform (also known as "Roslyn") allow developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="d9d96-105">개발자는 이를 통해 특정 API 또는 라이브러리의 사용을 안내하는 데 도움이 되는 도구와 같은 도메인 특정 분석 도구를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-105">This provides developers with a way to create and domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="d9d96-106">자세한 내용은 [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub Wiki에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="d9d96-107">또한 MSDN Magazine의 [Roslyn을 사용하여 API에 대한 라이브 코드 분석기 작성](https://msdn.microsoft.com/magazine/dn879356.aspx) 문서도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9d96-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="d9d96-108">분석기 자체는 일반적으로 문제의 API 또는 라이브러리를 구현하는 NuGet 패키지의 일부로 패키지되어 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="d9d96-109">좋은 예제에 대해서는 다음 콘텐츠가 포함된 [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) 패키지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9d96-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="d9d96-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="d9d96-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="d9d96-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="d9d96-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="d9d96-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="d9d96-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="d9d96-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="d9d96-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="d9d96-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="d9d96-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="d9d96-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="d9d96-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="d9d96-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="d9d96-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="d9d96-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="d9d96-117">tools\install.ps1</span></span>
- <span data-ttu-id="d9d96-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="d9d96-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="d9d96-119">여기서 볼 수 있듯이 패키지의 `analyzers` 폴더에 분석기 DLL을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="d9d96-120">분석기 구현에 레거시 FxCop 규칙을 사용하지 않도록 설정하기 위해 포함된 props 파일은 `build` 폴더에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="d9d96-121">`packages.config`를 사용하여 프로젝트를 지원하는 설치 및 제거 스크립트는 `tools`에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="d9d96-122">또한 이 패키지에는 플랫폼 특정 요구 사항이 없으므로 `platform` 폴더가 생략됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="d9d96-123">분석기 경로 형식</span><span class="sxs-lookup"><span data-stu-id="d9d96-123">Analyzers path format</span></span>

<span data-ttu-id="d9d96-124">`analyzers` 폴더의 사용은 경로의 지정자에서 빌드 시간 대신 개발 호스트 종속성을 설명한다는 점을 제외하고는 [대상 프레임워크](../create-packages/supporting-multiple-target-frameworks.md)에 사용되는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="d9d96-125">일반적인 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}}/{analyzer_name}.dll

- <span data-ttu-id="d9d96-126">**framework_name**: 포함된 DLL에서 실행해야 하는 .NET Framework의 *선택적* API 노출 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-126">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="d9d96-127">Roslyn은 분석기를 실행할 수 있는 유일한 호스트이므로 `dotnet`은 현재 유효한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="d9d96-128">대상을 지정하지 않으면 DLL이 *모든* 대상에 적용된다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="d9d96-129">**supported_language**: DLL이 적용되는 언어로서 `cs`(C#), `vb`(Visual Basic) 및 `fs`(F#) 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="d9d96-130">언어는 해당 언어를 사용하는 프로젝트에만 분석기가 로드되어야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="d9d96-131">언어를 지정하지 않으면 DLL이 분석기를 지원하는 *모든* 언어에 적용된다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-131">If no language is specified then DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="d9d96-132">**analyzer_name**: 분석기의 DLL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="d9d96-133">DLL 이외의 추가 파일이 필요하며 대상 또는 속성 파일을 통해 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="d9d96-134">스크립트 설치 및 제거</span><span class="sxs-lookup"><span data-stu-id="d9d96-134">Install and uninstall scripts</span></span>

<span data-ttu-id="d9d96-135">사용자의 프로젝트에서 `packages.config`를 사용하는 경우 분석기를 선택하는 MSBuild 스크립트가 작동하지 않으므로 아래에서 설명한 `install.ps1` 및 `uninstall.ps1`이 `tools` 폴더에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9d96-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="d9d96-136">**install.ps1 파일 내용**</span><span class="sxs-lookup"><span data-stu-id="d9d96-136">**install.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


<span data-ttu-id="d9d96-137">**uninstall.ps1 파일 내용**</span><span class="sxs-lookup"><span data-stu-id="d9d96-137">**uninstall.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```