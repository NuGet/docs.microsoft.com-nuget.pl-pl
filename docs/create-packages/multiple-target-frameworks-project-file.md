---
title: Wiele elementów docelowych dla pakietów NuGet w pliku projektu
description: Opis różnych metod ukierunkowanych na wiele wersji .NET Framework z jednego pakietu NuGet.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 8c1d8a479747f6f7bce388c1555589543c8824a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020057"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="87c3f-103">Obsługa wielu wersji .NET Framework w pliku projektu</span><span class="sxs-lookup"><span data-stu-id="87c3f-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="87c3f-104">Podczas pierwszego tworzenia projektu zalecamy utworzenie .NET Standard biblioteki klas, ponieważ zapewnia ona zgodność z najszerszym zakresem zużywanych projektów.</span><span class="sxs-lookup"><span data-stu-id="87c3f-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="87c3f-105">Korzystając z .NET Standard, domyślnie dodawana jest [Obsługa wielu platform](/dotnet/standard/library-guidance/cross-platform-targeting) do biblioteki platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="87c3f-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="87c3f-106">Jednak w niektórych scenariuszach może być również konieczne dołączenie kodu, który jest przeznaczony dla konkretnej struktury.</span><span class="sxs-lookup"><span data-stu-id="87c3f-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="87c3f-107">W tym artykule pokazano, jak to zrobić dla projektów w [stylu zestawu SDK](../resources/check-project-format.md) .</span><span class="sxs-lookup"><span data-stu-id="87c3f-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="87c3f-108">W przypadku projektów w stylu zestawu SDK można skonfigurować obsługę wielu platform docelowych ([TFM](/dotnet/standard/frameworks)) w pliku projektu, a następnie użyć `dotnet pack` programu lub `msbuild /t:pack` , aby utworzyć pakiet.</span><span class="sxs-lookup"><span data-stu-id="87c3f-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="87c3f-109">Interfejs wiersza polecenia NuGet. exe nie obsługuje projektów typu "pakowanie" w stylu zestawu SDK, `dotnet pack` dlatego `msbuild /t:pack`należy używać tylko lub.</span><span class="sxs-lookup"><span data-stu-id="87c3f-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="87c3f-110">Zalecamy [uwzględnienie wszystkich właściwości](../reference/msbuild-targets.md#pack-target) , które zwykle znajdują się w `.nuspec` pliku w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="87c3f-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="87c3f-111">Aby dowiedzieć się więcej na temat wielu wersji .NET Framework w projekcie w stylu innym niż zestaw SDK, zobacz [Obsługa wielu .NET Framework wersji](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="87c3f-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="87c3f-112">Utwórz projekt obsługujący wiele wersji .NET Framework</span><span class="sxs-lookup"><span data-stu-id="87c3f-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="87c3f-113">Utwórz nową bibliotekę klas .NET Standard w programie Visual Studio lub Użyj `dotnet new classlib`.</span><span class="sxs-lookup"><span data-stu-id="87c3f-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="87c3f-114">Zalecamy utworzenie biblioteki klas .NET Standard w celu uzyskania najlepszej zgodności.</span><span class="sxs-lookup"><span data-stu-id="87c3f-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="87c3f-115">Edytuj plik *. csproj* , aby obsługiwał Platformy docelowe.</span><span class="sxs-lookup"><span data-stu-id="87c3f-115">Edit the *.csproj* file to support the target frameworks.</span></span> <span data-ttu-id="87c3f-116">Na przykład zmień</span><span class="sxs-lookup"><span data-stu-id="87c3f-116">For example, change</span></span>
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   <span data-ttu-id="87c3f-117">na:</span><span class="sxs-lookup"><span data-stu-id="87c3f-117">to:</span></span>
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   <span data-ttu-id="87c3f-118">Upewnij się, że zmienisz element XML zmieniony z wartości pojedynczej na plural (Dodaj "s" do tagów Otwórz i Zamknij).</span><span class="sxs-lookup"><span data-stu-id="87c3f-118">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="87c3f-119">Jeśli masz dowolny kod, który działa tylko w jednej TFM, możesz użyć `#if NET45` lub `#if NETSTANDARD20` , aby oddzielić kod zależny od TFM.</span><span class="sxs-lookup"><span data-stu-id="87c3f-119">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD20` to separate TFM-dependent code.</span></span> <span data-ttu-id="87c3f-120">(Aby uzyskać więcej informacji, zobacz [jak to zrobić](/dotnet/core/tutorials/libraries#how-to-multitarget).) Na przykład można użyć następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="87c3f-120">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

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

4. <span data-ttu-id="87c3f-121">Dodaj dowolne metadane NuGet do właściwości *. csproj* jako programu MSBuild.</span><span class="sxs-lookup"><span data-stu-id="87c3f-121">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="87c3f-122">Aby uzyskać listę dostępnych metadanych pakietu i nazw właściwości programu MSBuild, zobacz [pakiet Target](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="87c3f-122">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="87c3f-123">Zobacz również [kontrolowanie elementów zależnych](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="87c3f-123">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="87c3f-124">Jeśli chcesz oddzielić właściwości związane z kompilacją z metadanych NuGet, możesz użyć innej `PropertyGroup`lub umieścić właściwości NuGet w innym pliku i użyć `Import` dyrektywy MSBuild do dołączenia.</span><span class="sxs-lookup"><span data-stu-id="87c3f-124">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="87c3f-125">`Directory.Build.Props`i `Directory.Build.Targets` są również obsługiwane począwszy od programu MSBuild 15,0.</span><span class="sxs-lookup"><span data-stu-id="87c3f-125">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="87c3f-126">Teraz można używać `dotnet pack` elementów i wyników *. nupkg* , które są zarówno .NET Standard 2,0, jak i .NET Framework 4,5.</span><span class="sxs-lookup"><span data-stu-id="87c3f-126">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="87c3f-127">Oto plik *. csproj* , który jest generowany przy użyciu powyższych kroków i zestaw .NET Core SDK 2,2.</span><span class="sxs-lookup"><span data-stu-id="87c3f-127">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="87c3f-128">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="87c3f-128">See also</span></span>

* [<span data-ttu-id="87c3f-129">Jak określić Platformy docelowe</span><span class="sxs-lookup"><span data-stu-id="87c3f-129">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="87c3f-130">Obsługiwane rozwiązania międzyplatformowe</span><span class="sxs-lookup"><span data-stu-id="87c3f-130">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
