---
title: Wielokierunkowe dla pakietów NuGet w pliku projektu
description: Opis różnych metod do docelowych wielu wersji programu .NET Framework z jednego pakietu NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1d23759433efb405fa5f0035049befced2c43d6b
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380678"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="f67a6-103">Obsługa wielu wersji programu .NET Framework w pliku projektu</span><span class="sxs-lookup"><span data-stu-id="f67a6-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="f67a6-104">Podczas pierwszego tworzenia projektu zaleca się utworzenie biblioteki klas .NET Standard, ponieważ zapewnia zgodność z najszerszym zakresem projektów zużywających.</span><span class="sxs-lookup"><span data-stu-id="f67a6-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="f67a6-105">Korzystając ze standardu .NET Standard, domyślnie dodajesz [obsługę między platformami](/dotnet/standard/library-guidance/cross-platform-targeting) do biblioteki .NET.</span><span class="sxs-lookup"><span data-stu-id="f67a6-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="f67a6-106">Jednak w niektórych scenariuszach może być również konieczne dołączenie kodu, który jest przeznaczony dla określonej struktury.</span><span class="sxs-lookup"><span data-stu-id="f67a6-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="f67a6-107">W tym artykule pokazano, jak to zrobić dla projektów [w stylu SDK.](../resources/check-project-format.md)</span><span class="sxs-lookup"><span data-stu-id="f67a6-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="f67a6-108">W przypadku projektów w stylu zestawu SDK można skonfigurować obsługę wielu struktur docelowych `dotnet pack` [(TFM)](/dotnet/standard/frameworks)w pliku projektu, a następnie użyć lub `msbuild /t:pack` utworzyć pakiet.</span><span class="sxs-lookup"><span data-stu-id="f67a6-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="f67a6-109">nuget.exe CLI nie obsługuje pakowania projektów w stylu zestawu SDK, więc należy używać `dotnet pack` tylko lub `msbuild /t:pack`.</span><span class="sxs-lookup"><span data-stu-id="f67a6-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="f67a6-110">Zaleca się [uwzględnić wszystkie właściwości,](../reference/msbuild-targets.md#pack-target) które `.nuspec` są zwykle w pliku w pliku projektu zamiast.</span><span class="sxs-lookup"><span data-stu-id="f67a6-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="f67a6-111">Aby kierować reklamy na wiele wersji programu .NET Framework w projekcie w stylu nienawiązanym do zestawu SDK, zobacz [Obsługa wielu wersji programu .NET Framework](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="f67a6-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="f67a6-112">Tworzenie projektu obsługującego wiele wersji programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="f67a6-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="f67a6-113">Utwórz nową bibliotekę klas .NET Standard `dotnet new classlib`w programie Visual Studio lub użyj .</span><span class="sxs-lookup"><span data-stu-id="f67a6-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="f67a6-114">Zaleca się utworzenie biblioteki klas .NET Standard w celu zapewnienia najlepszej zgodności.</span><span class="sxs-lookup"><span data-stu-id="f67a6-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="f67a6-115">Edytuj plik *csproj,* aby obsługiwać struktury docelowe.</span><span class="sxs-lookup"><span data-stu-id="f67a6-115">Edit the *.csproj* file to support the target frameworks.</span></span> <span data-ttu-id="f67a6-116">Na przykład zmień</span><span class="sxs-lookup"><span data-stu-id="f67a6-116">For example, change</span></span>
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   <span data-ttu-id="f67a6-117">na:</span><span class="sxs-lookup"><span data-stu-id="f67a6-117">to:</span></span>
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   <span data-ttu-id="f67a6-118">Upewnij się, że zmieniono element XML z liczby pojedynczej na mnogą (dodaj "s" do znaczników otwartych i zamkniętych).</span><span class="sxs-lookup"><span data-stu-id="f67a6-118">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="f67a6-119">Jeśli masz dowolny kod, który działa tylko w `#if NET45` jednym `#if NETSTANDARD2_0` TFM, można użyć lub oddzielić kod zależny od TFM.</span><span class="sxs-lookup"><span data-stu-id="f67a6-119">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD2_0` to separate TFM-dependent code.</span></span> <span data-ttu-id="f67a6-120">(Aby uzyskać więcej informacji, zobacz [Jak multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) Na przykład można użyć następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="f67a6-120">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. <span data-ttu-id="f67a6-121">Dodaj wszystkie metadane NuGet, które chcesz do *.csproj* jako MSBuild właściwości.</span><span class="sxs-lookup"><span data-stu-id="f67a6-121">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="f67a6-122">Aby uzyskać listę dostępnych metadanych pakietu i nazwy właściwości MSBuild, zobacz [miejsce docelowego pakowania](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="f67a6-122">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="f67a6-123">Zobacz też [Kontrolowanie zasobów zależności](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="f67a6-123">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="f67a6-124">Jeśli chcesz oddzielić właściwości związane z kompilacją z metadanych `PropertyGroup`NuGet, możesz użyć innego , lub umieścić właściwości `Import` NuGet w innym pliku i użyć dyrektywy MSBuild, aby ją uwzględnić.</span><span class="sxs-lookup"><span data-stu-id="f67a6-124">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="f67a6-125">`Directory.Build.Props`i `Directory.Build.Targets` są również obsługiwane począwszy od MSBuild 15.0.</span><span class="sxs-lookup"><span data-stu-id="f67a6-125">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="f67a6-126">Teraz użyj `dotnet pack` i wynikowy *.nupkg* jest przeznaczony zarówno dla platformy .NET Standard 2.0, jak i .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="f67a6-126">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="f67a6-127">Oto plik *csproj,* który jest generowany przy użyciu poprzednich kroków i .NET Core SDK 2.2.</span><span class="sxs-lookup"><span data-stu-id="f67a6-127">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="f67a6-128">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f67a6-128">See also</span></span>

* [<span data-ttu-id="f67a6-129">Jak określić struktury docelowe</span><span class="sxs-lookup"><span data-stu-id="f67a6-129">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="f67a6-130">Obsługiwane rozwiązania międzyplatformowe</span><span class="sxs-lookup"><span data-stu-id="f67a6-130">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
