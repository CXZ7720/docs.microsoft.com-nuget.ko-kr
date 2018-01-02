---
title: "Visual Studio 2015를 사용하여 .NET Standard NuGet 패키지 만들기 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "NuGet 3.x 및 Visual Studio 2015를 사용하여 .NET Standard NuGet 패키지를 만드는 종단 간 연습입니다."
keywords: "패키지 만들기, .NET Standard 패키지, .NET Standard 매핑 테이블"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a912c27e1873d60426f2147995f69e2dcc433ca9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a>Visual Studio 2015를 사용하여 .NET Standard 패키지 만들기

*NuGet 3.x에 적용됩니다. NuGet 4.x 이상을 사용하려면 [Visual Studio 2017을 사용하여 .NET Standard 패키지 만들기](../guides/create-net-standard-packages-vs2017.md)를 참조하세요.*

[.NET Standard 라이브러리](https://docs.microsoft.com/dotnet/articles/standard/library)는 모든 .NET 런타임에서 사용할 수 있도록 만들어진 .NET API의 공식 사양이며, 이에 따라 .NET 생태계에서 더 균일하게 설정됩니다. .NET Standard 라이브러리는 워크로드와는 별도로 구현할 모든 .NET 플랫폼에 대해 균일한 BCL(기본 클래스 라이브러리) API 집합을 정의합니다. 개발자가 모든 .NET 런타임에서 사용할 수 있는 PCL을 생성할 수 있으며, 공유 코드에서 플랫폼별 조건부 컴파일 지시문을 제거하지 않더라도 이를 줄일 수 있습니다.

이 가이드에서는 .NET Standard 라이브러리 1.4를 대상으로 하는 NuGet 패키지를 만드는 과정을 안내합니다. 이 패키지는 .NET Framework 4.6.1, 유니버설 Windows 플랫폼 10, .NET Core 및 Mono/Xamarin에서 작동합니다. 자세한 내용은 이 항목의 뒷부분에 있는 [.NET Standard 매핑 테이블](#net-standard-mapping-table)을 참조하세요.

1. [필수 구성 요소](#pre-requisites)
1. [클래스 라이브러리 프로젝트 만들기](#create-the-class-library-project)
1. [.nuspec 파일 만들기 및 업데이트](#create-and-update-the-nuspec-file)
1. [구성 요소 패키징](#package-the-component)
1. [추가 옵션](#additional-options)
1. [.NET Standard 매핑 테이블](#net-standard-mapping-table)
1. [관련 항목](#related-topics)


## <a name="pre-requisites"></a>필수 구성 요소

1. Visual Studio 2015 - [visualstudio.com](https://www.visualstudio.com/)에서 추가 비용 없이 Community 버전을 설치합니다. Professional 및 Enterprise 버전도 사용할 수 있습니다.
1. .NET Core - [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849)에서 Visual Studio 2015용 템플릿 및 다른 도구와 함께 .NET Core를 설치합니다.
1. NuGet CLI - [nuget.org/downloads](https://nuget.org/downloads)에서 최신 버전의 nuget.exe를 다운로드하여 원하는 위치에 저장합니다. 그런 다음 해당 위치를 PATH 환경 변수에 추가합니다(아직 없는 경우).

> [!Note]
> nuget.exe는 설치 관리자가 아니라 CLI 도구 자체이므로 브라우저에서 다운로드한 파일을 실행하는 대신 저장해야 합니다.



## <a name="create-the-class-library-project"></a>클래스 라이브러리 프로젝트 만들기

1. Visual Studio의 **파일> 새로 만들기> 프로젝트**에서 **Visual C# > Windows** 노드를 차례로 펼치고, **클래스 라이브러리(이식 가능)**를 선택하고, 이름을 AppLogger로 변경한 다음, [확인]을 클릭합니다.

    ![새 클래스 라이브러리 프로젝트 만들기](media/NetStandard-NewProject.png)

1. **이식 가능한 클래스 라이브러리 추가** 대화 상자가 표시되면 `.NET Framework 4.6` 및 `ASP.NET Core 1.0` 옵션을 선택합니다.
1. [솔루션 탐색기]에서 `AppLogger (Portable)`을 마우스 오른쪽 단추로 클릭하고, **속성**을 선택하고, **라이브러리** 탭을 선택한 다음, **대상 지정** 섹션에서 **.NET 플랫폼 표준을 대상으로 지정**을 클릭합니다. 그러면 확인 메시지가 표시되며, 드롭다운 목록에서 `.NET Standard 1.4`를 선택할 수 있습니다.

    ![대상을 .NET Standard 1.4로 설정](media/NetStandard-ChangeTarget.png)

1. **빌드** 탭을 클릭하고, **구성**을 `Release`로 변경하고, **XML 문서 파일** 확인란을 선택합니다.
1. 구성 요소에 다음과 같은 코드를 추가합니다.

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. 프로젝트를 빌드하고([릴리스] 구성 사용), DLL 및 XML 파일이 bin\Release 폴더 내에 생성되는지 확인합니다.

## <a name="create-and-update-the-nuspec-file"></a>.nuspec 파일 만들기 및 업데이트

1. 명령 프롬프트를 열고, `.sln` 파일이 있는 위치에서 한 수준 아래의 `AppLogg.csproj` 폴더로 이동한 다음, NuGet `spec` 명령을 실행하여 초기 `AppLogger.nuspec` 파일을 만듭니다.

```
nuget spec
```

1. 편집기에서 `AppLogger.nuspec`을 열고 YOUR_NAME을 적절한 값으로 바꿔 다음과 일치하도록 업데이트합니다. 특히 `<id>` 값은 nuget.org 전체에서 고유해야 합니다([패키지 만들기](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)에서 설명한 명명 규칙 참조). 또한 작성자 및 설명 태그도 업데이트해야 합니다. 그렇지 않으면 압축 단계에서 오류가 발생합니다.

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. 참조 어셈블리를 `.nuspec` 파일, 즉 라이브러리의 DLL 및 IntelliSense XML 파일에 추가합니다.

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. 솔루션을 마우스 오른쪽 단추로 클릭하고 **솔루션 빌드**를 선택하여 패키지에 대한 모든 파일을 생성합니다.


## <a name="package-the-component"></a>구성 요소 패키징

완료된 `.nuspec`에서 패키지에 포함되어야 하는 모든 파일을 참조하면 `pack` 명령을 실행할 준비가 되었습니다.

```
nuget pack AppLogger.nuspec
```

그러면 `AppLogger.YOUR_NAME.1.0.0.nupkg`가 생성됩니다. [NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)와 같은 도구에서 이 파일을 열고 모든 노드를 펼치면 다음과 같은 내용이 표시됩니다.

![AppLogger 패키지를 보여 주는 NuGet 패키지 탐색기](media/NetStandard-PackageExplorer.png)

> [!Tip]
> `.nupkg` 파일은 확장명이 다른 ZIP 파일일 뿐입니다. `.nupkg`를 `.zip`으로 변경하여 패키지 내용을 검사할 수도 있지만 패키지를 nuget.org에 업로드하려면 먼저 확장명을 복원해야 합니다.

다른 개발자가 패키지를 사용할 수 있게 하려면 [패키지 게시](../create-packages/publish-a-package.md)의 지침을 따르세요.

`pack`에는 Mac OS X에서 Mono 4.4.2가 필요하며, Linux 시스템에서는 작동하지 않습니다. 또한 Mac에서는 `.nuspec` 파일의 Windows 경로 이름을 Unix 스타일 경로로 변환해야 합니다.

## <a name="additional-options"></a>추가 옵션

다음 섹션에서는 NuGet 패키지를 만들기 위한 추가 옵션으로 이동합니다.

- [종속성 선언](#declaring-dependencies)
- [여러 대상 프레임워크 지원](#supporting-multiple-target-frameworks)
- [MSBuild용 targets 및 props 추가](#adding-targets-and-props-for-msbuild)
- [지역화된 패키지 만들기](#creating-localized-packages)
- [추가 정보 추가](#adding-a-readme)

### <a name="declaring-dependencies"></a>종속성 선언

다른 NuGet 패키지에 대한 종속성이 있는 경우 `<dependencies>` 요소에서 `<group>` 요소를 사용하여 해당 패키지를 나열합니다. 예를 들어 NewtonSoft.Json 8.0.3 이상에 대한 종속성을 선언하려면 다음을 추가합니다.

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

여기서 *version* 특성의 구문은 버전 8.0.3 이상을 사용할 수 있음을 나타냅니다. 다른 버전 범위를 지정하려면 [패키지 버전 관리](../reference/package-versioning.md)를 참조하세요.

### <a name="supporting-multiple-target-frameworks"></a>여러 대상 프레임워크 지원

.NET Standard 1.4에서 사용할 수 없는 .NET Framework 4.6.2의 API를 활용하려고 한다고 가정해 보겠습니다. 이렇게 하려면 먼저 조건부 컴파일 또는 공유 프로젝트를 사용하여 라이브러리가 .NET 4.6.2용으로 컴파일되는지 확인합니다. (Visual Studio에서 NetCore 프로젝트를 만들고, 여러 프레임워크 섹션에 선택한 프레임워크를 추가한 다음, 빌드할 수 있습니다.) 다음으로, 다음과 같이 간단한 규칙 기반 작업 디렉터리 기술을 사용하여 패키지를 만듭니다.

1. `.nuspec` 파일이 포함된 프로젝트의 루트 폴더에서 `lib`라는 폴더를 만듭니다.
1. `lib` 내에서 지원하려는 각 플랫폼에 대한 폴더를 만듭니다.

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. `.nuspec` 파일에서 `package` 노드 아래에 `files` 노드를 추가하고, 와일드카드를 사용하여 `lib`에 있는 파일을 참조합니다. **참고:** 토큰 대체는 규칙 기반 작업 디렉터리 접근 방식에서 지원되지 않으므로 리터럴 값으로 바꿉니다.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. `nuget pack AppLogger.spec`을 사용하여 패키지를 다시 만듭니다.

이 기술의 사용에 대한 자세한 내용은 [여러 .NET Framework 버전 지원](../create-packages/supporting-multiple-target-frameworks.md)을 참조하세요.

### <a name="adding-targets-and-props-for-msbuild"></a>MSBuild용 targets 및 props 추가

경우에 따라 패키지를 사용하는 프로젝트에 사용자 지정 빌드 대상 또는 속성(예: 빌드하는 동안 사용자 지정 도구 또는 프로세스 실행)을 추가할 수 있습니다. 이렇게 하려면 아래 단계에서 설명한 대로 `\build` 폴더에 파일을 추가합니다. NuGet에서 \build 파일이 포함된 패키지를 설치하는 경우 .targets 및 .props 파일을 가리키는 MSBuild 요소를 프로젝트 파일에 추가합니다.

> [!Note]
> `project.json`을 사용하는 경우 대상이 프로젝트에는 추가되지 않지만 `project.lock.json`을 통해 사용될 수 있게 됩니다.


1. `.nuspec` 파일이 포함된 프로젝트 폴더에서 `build`라는 폴더를 만듭니다.
1. `build` 내에서 지원되는 각 폴더를 만들고 해당 위치 내에 `.targets` 및 `.props` 파일을 배치합니다.

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. `.nuspec` 파일에서 `package` 노드 아래에 `files` 노드를 추가하고, 와일드카드를 사용하여 `build`에 있는 파일을 참조합니다.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. `nuget pack AppLogger.nuspec`을 사용하여 패키지를 다시 만듭니다.

자세한 내용은 [패키지에 MSBuild props 및 targets 포함](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)을 참조하세요.


### <a name="creating-localized-packages"></a>지역화된 패키지 만들기

지역화된 라이브러리 버전을 만들려면 서로 다른 로캘에 대해 별도의 패키지를 만들거나 단일 패키지 내에 지역화된 리소스 어셈블리를 포함할 수 있습니다. 독일어와 이탈리아어에 대해 후자의 방법을 수행하는 방법은 다음과 같습니다.

1. `lib` 아래의 각 대상 프레임워크 폴더 내에서 영어 기본값 이외의 지원되는 각 언어에 대한 폴더를 만듭니다. 이러한 폴더에 리소스 어셈블리와 지역화된 IntelliSense XML 파일을 배치할 수 있습니다. 예:

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. `.nuspec` 파일에서 `<files>` 노드에 있는 다음 파일을 참조합니다.

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. `nuget pack AppLogger.nuspec`을 사용하여 패키지를 다시 만듭니다.


### <a name="adding-a-readme"></a>추가 정보 추가

패키지의 루트에 `readme.txt` 파일이 포함되면 패키지를 직접 설치할 때 Visual Studio에서 이를 표시합니다.

> [!Note]
> 종속성으로 설치된 패키지 또는 .NET Core 프로젝트에 대한 추가 정보 파일은 표시되지 않습니다.


이렇게 하려면 `readme.txt` 파일을 만들어 프로젝트 루트 폴더에 배치하고 `.nuspec` 파일에서 이를 참조합니다.

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a>.NET Standard 매핑 테이블

|플랫폼 이름 |Alias|
|--------------|-----|
|.NET 표준 | netstandard| 1.0| 1.1| 1.2| 1.3| 1.4| 1.5| 1.6|
|.NET Core | netcoreapp| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| 1.0|
|.NET Framework| net| 4.5| 4.5.1| 4.6| 4.6.1| 4.6.2| 4.6.3|
|Mono/Xamarin 플랫폼| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;|
|유니버설 Windows 플랫폼| uap| &#x2192;| &#x2192;| &#x2192;| &#x2192;|10.0|
|창| win| &#x2192;| 8.0| 8.1|
|Windows Phone| wpa| &#x2192;| &#x2192;|8.1|
|Windows Phone Silverlight| wp| 8.0|



## <a name="related-topics"></a>관련 항목

- [.nuspec 참조](../schema/nuspec.md)
- [기호 패키지](../create-packages/symbol-packages.md)
- [패키지 버전 관리](../reference/package-versioning.md)
- [여러 .NET Framework 버전 지원](../create-packages/supporting-multiple-target-frameworks.md)
- [패키지에 MSBuild props 및 targets 포함](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [지역화된 패키지 만들기](../create-packages/creating-localized-packages.md)
- [.NET Standard 라이브러리 설명서](https://docs.microsoft.com/dotnet/articles/standard/library)
- [.NET Framework에서 .NET Core로 이식](https://docs.microsoft.com/dotnet/articles/core/porting/index)