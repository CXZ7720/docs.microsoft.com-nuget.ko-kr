---
title: NuGet에서 UI 컨트롤을 패키지하는 방법
description: Visual Studio 및 Blend 디자이너에 필요한 메타데이터 및 지원되는 파일을 포함하여 UWP 또는 WPF 컨트롤을 포함하는 NuGet 패키지를 만드는 방법입니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: fc6ab9e45d18807a6d69bb50ad5bac94b662a638
ms.sourcegitcommit: 80c1a37d8794e9219e310a21a6a6885a65d24e53
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2018
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="87206-103">NuGet 패키지인 UI 컨트롤 만들기</span><span class="sxs-lookup"><span data-stu-id="87206-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="87206-104">Visual Studio 2017에서 NuGet 패키지에서 제공하는 UWP 및 WPF 컨트롤에 추가된 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87206-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="87206-105">이 가이드는 [ExtensionSDKasNuGetPackage 샘플](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)을 사용하여 UWP 컨트롤의 컨텍스트에서 이러한 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="87206-106">달리 언급하지 않는 한 WPF 컨트롤에도 동일한 내용이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87206-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87206-107">전제 조건</span><span class="sxs-lookup"><span data-stu-id="87206-107">Prerequisites</span></span>

1. <span data-ttu-id="87206-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="87206-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="87206-109">[UWP 패키지를 만드는](create-uwp-packages.md) 방법 이해</span><span class="sxs-lookup"><span data-stu-id="87206-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="87206-110">라이브러리 레이아웃 생성</span><span class="sxs-lookup"><span data-stu-id="87206-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="87206-111">이 내용은 UWP 컨트롤에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87206-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="87206-112">`GenerateLibraryLayout` 속성을 설정하면 프로젝트 빌드 출력이 nuspec의 개별 파일 항목 없이, 패키지할 준비가 된 레이아웃에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="87206-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="87206-113">프로젝트 속성에서 빌드 탭으로 이동하여 “라이브러리 레이아웃 생성” 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="87206-114">그러면 프로젝트 파일이 수정되고 현재 선택된 빌드 구성 및 플랫폼에 대해 `GenerateLibraryLayout` 플래그가 true로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="87206-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="87206-115">또는 프로젝트 파일을 편집하여 첫 번째 무조건 속성 그룹에 `<GenerateLibraryLayout>true</GenerateLibraryLayout>`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="87206-116">그러면 빌드 구성 및 플랫폼에 상관없이 속성이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87206-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="87206-117">XAML 컨트롤에 도구 상자/자산 창 지원 추가</span><span class="sxs-lookup"><span data-stu-id="87206-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="87206-118">Visual Studio 및 Blend의 자산 창에 있는 XAML 디자이너의 도구 상자에 XAML 컨트롤을 표시하려면 패키지 프로젝트의 `tools` 폴더 루트에 `VisualStudioToolsManifest.xml` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87206-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="87206-119">컨트롤을 도구 상자 또는 자산 창에서 표시하지 않아도 되는 경우 이 파일이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="87206-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="87206-120">파일의 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="87206-120">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="87206-121">다음은 각 문자에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="87206-121">where:</span></span>

- <span data-ttu-id="87206-122">*your_package_file*: `ManagedPackage.winmd`와 같은 컨트롤 파일의 이름입니다("ManagedPackage"는 이 예제에 사용되고 다른 의미가 없음).</span><span class="sxs-lookup"><span data-stu-id="87206-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="87206-123">*vs_category*: Visual Studio 디자이너의 도구 상자에서 컨트롤이 표시되어야 하는 그룹의 레이블입니다.</span><span class="sxs-lookup"><span data-stu-id="87206-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="87206-124">`VSCategory`는 컨트롤을 도구 상자에 표시하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="87206-125">*blend_category*: Blend 디자이너의 자산 창에서 컨트롤이 표시되어야 하는 그룹의 레이블입니다.</span><span class="sxs-lookup"><span data-stu-id="87206-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="87206-126">`BlendCategory`는 컨트롤을 자산에 표시하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="87206-127">*type_full_name_n*: `ManagedPackage.MyCustomControl`과 같은 네임스페이스를 포함하여 각 컨트롤의 정규화된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="87206-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="87206-128">점 양식은 관리 및 네이티브 형식에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87206-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="87206-129">고급 시나리오에서 단일 패키지에 여러 컨트롤 어셈블리가 포함되는 경우 `<FileList>` 내에 여러 `<File>` 요소가 포함될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87206-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="87206-130">컨트롤을 별도 범주로 구성하려는 경우 단일 `<File>` 내에 여러 `<ToolboxItems>` 노드가 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87206-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="87206-131">다음 예제에서 `ManagedPackage.winmd`에서 구현된 컨트롤은 "관리 패키지"라는 그룹의 Visual Studio 및 Blend에 표시되고 "MyCustomControl"은 해당 그룹에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="87206-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="87206-132">이러한 이름은 모두 임의로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="87206-132">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Visual Studio에서 표시되는 예제 컨트롤](media/UWP-control-vs-toolbox.png)

![Blend에서 표시되는 예제 컨트롤](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="87206-135">도구 상자/자산 창에서 확인하려는 모든 컨트롤을 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="87206-136">`Namespace.ControlName` 형식으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="87206-137">컨트롤에 사용자 지정 아이콘 추가</span><span class="sxs-lookup"><span data-stu-id="87206-137">Add custom icons to your controls</span></span>

<span data-ttu-id="87206-138">도구 상자/자산 창에서 사용자 지정 아이콘을 표시하려면 이미지를 프로젝트 또는 "Namespace.ControlName.extension"이라는 해당 `design.dll` 프로젝트에 추가하고 빌드 작업을 "포함 리소스"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="87206-139">지원되는 형식은 `.png`, `.jpg`, `.jpeg`, `.gif` 및 `.bmp`입니다.</span><span class="sxs-lookup"><span data-stu-id="87206-139">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="87206-140">권장된 이미지 크기는 64x64픽셀입니다.</span><span class="sxs-lookup"><span data-stu-id="87206-140">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="87206-141">아래 예제에서 프로젝트에는 "ManagedPackage.MyCustomControl.png"라는 이미지 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87206-141">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![프로젝트에서 사용자 지정 아이콘 설정](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="87206-143">네이티브 컨트롤의 경우 `design.dll` 프로젝트에서 리소스로 아이콘을 삽입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-143">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="87206-144">특정 Windows 플랫폼 버전 지원</span><span class="sxs-lookup"><span data-stu-id="87206-144">Support specific Windows platform versions</span></span>

<span data-ttu-id="87206-145">UWP 패키지에는 앱을 설치할 수 있는 OS 버전의 상한 및 하한 경계를 정의하는 TargetPlatformVersion(TPV) 및 TargetPlatformMinVersion(TPMinV)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87206-145">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="87206-146">나아가 TPV는 앱을 빌드할 SDK의 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-146">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="87206-147">UWP 패키지를 작성할 때 이러한 속성을 고려하세요. 앱에 정의된 플랫폼 버전의 범위 밖에서 API를 사용하면 런타임 시 빌드에 실패하거나 앱이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-147">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="87206-148">예를 들어 TPMinV 컨트롤 패키지를 Windows 10 Anniversary Edition(10.0, 빌드 14393)으로 설정했다고 가정해 보겠습니다. 따라서 패키지가 낮은 해당 범위와 일치하는 UWP 프로젝트에서만 사용되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-148">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="87206-149">패키지를 UWP 프로젝트에서 사용할 수 있도록 허용하려면 다음 폴더 이름을 가진 컨트롤을 패키지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-149">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="87206-150">NuGet은 사용하는 프로젝트의 TPMinV를 자동으로 확인하고 Windows 10 Anniversary Edition(10.0, 빌드 14393)보다 이전 버전인 경우 설치에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-150">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="87206-151">WPF의 경우 .NET Framework v4.6.1 이상을 대상으로 하는 프로젝트에서 WPF 컨트롤 패키지를 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-151">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="87206-152">이를 적용하려면 다음 폴더 이름으로 컨트롤을 패키지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-152">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="87206-153">디자인 타임 지원 추가</span><span class="sxs-lookup"><span data-stu-id="87206-153">Add design-time support</span></span>

<span data-ttu-id="87206-154">속성 검사자에서 컨트롤 속성이 표시되는 위치를 구성하려면 사용자 지정 표시기 등을 추가하고, `design.dll` 파일을 `lib\uap10.0.14393\Design` 폴더에 대상 플랫폼에 적합하도록 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-154">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="87206-155">또한 **[템플릿 편집 > 복사본 편집](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** 기능이 작동하도록 하려면 `<your_assembly_name>\Themes` 폴더에서 병합되는 `Generic.xaml` 및 리소스가 포함되어야 합니다(실제 어셈블리 이름 사용).</span><span class="sxs-lookup"><span data-stu-id="87206-155">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="87206-156">(이 파일은 컨트롤의 런타임 동작에 아무런 영향을 주지 않습니다.) 따라서 폴더 구조는 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="87206-156">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="87206-157">WPF의 경우 .NET Framework v4.6.1 이상을 대상으로 하는 프로젝트에서 WPF 컨트롤 패키지를 사용하는 예를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-157">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="87206-158">기본적으로 컨트롤 속성은 속성 검사자의 기타 범주에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="87206-158">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="87206-159">문자열 및 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="87206-159">Use strings and resources</span></span>

<span data-ttu-id="87206-160">패키지에 문자열 리소스(`.resw`)를 포함할 수 있으며 해당 리소스를 컨트롤 또는 사용 중인 UWP 프로젝트에서 사용할 수 있습니다. `.resw` 파일의 **빌드 작업** 속성을 **PRIResource**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="87206-160">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="87206-161">예를 들어 ExtensionSDKasNuGetPackage 샘플에서 [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87206-161">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="87206-162">이 내용은 UWP 컨트롤에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="87206-162">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="87206-163">참고 항목</span><span class="sxs-lookup"><span data-stu-id="87206-163">See also</span></span>

- [<span data-ttu-id="87206-164">UWP 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="87206-164">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="87206-165">ExtensionSDKasNuGetPackage 샘플</span><span class="sxs-lookup"><span data-stu-id="87206-165">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)