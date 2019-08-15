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
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>Obsługa wielu wersji .NET Framework w pliku projektu

Podczas pierwszego tworzenia projektu zalecamy utworzenie .NET Standard biblioteki klas, ponieważ zapewnia ona zgodność z najszerszym zakresem zużywanych projektów. Korzystając z .NET Standard, domyślnie dodawana jest [Obsługa wielu platform](/dotnet/standard/library-guidance/cross-platform-targeting) do biblioteki platformy .NET. Jednak w niektórych scenariuszach może być również konieczne dołączenie kodu, który jest przeznaczony dla konkretnej struktury. W tym artykule pokazano, jak to zrobić dla projektów w [stylu zestawu SDK](../resources/check-project-format.md) .

W przypadku projektów w stylu zestawu SDK można skonfigurować obsługę wielu platform docelowych ([TFM](/dotnet/standard/frameworks)) w pliku projektu, a następnie użyć `dotnet pack` programu lub `msbuild /t:pack` , aby utworzyć pakiet.

> [!NOTE]
> Interfejs wiersza polecenia NuGet. exe nie obsługuje projektów typu "pakowanie" w stylu zestawu SDK, `dotnet pack` dlatego `msbuild /t:pack`należy używać tylko lub. Zalecamy [uwzględnienie wszystkich właściwości](../reference/msbuild-targets.md#pack-target) , które zwykle znajdują się w `.nuspec` pliku w pliku projektu. Aby dowiedzieć się więcej na temat wielu wersji .NET Framework w projekcie w stylu innym niż zestaw SDK, zobacz [Obsługa wielu .NET Framework wersji](supporting-multiple-target-frameworks.md).

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>Utwórz projekt obsługujący wiele wersji .NET Framework

1. Utwórz nową bibliotekę klas .NET Standard w programie Visual Studio lub Użyj `dotnet new classlib`.

   Zalecamy utworzenie biblioteki klas .NET Standard w celu uzyskania najlepszej zgodności.

2. Edytuj plik *. csproj* , aby obsługiwał Platformy docelowe. Na przykład zmień
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   na:
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   Upewnij się, że zmienisz element XML zmieniony z wartości pojedynczej na plural (Dodaj "s" do tagów Otwórz i Zamknij).

3. Jeśli masz dowolny kod, który działa tylko w jednej TFM, możesz użyć `#if NET45` lub `#if NETSTANDARD20` , aby oddzielić kod zależny od TFM. (Aby uzyskać więcej informacji, zobacz [jak to zrobić](/dotnet/core/tutorials/libraries#how-to-multitarget).) Na przykład można użyć następującego kodu:

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

4. Dodaj dowolne metadane NuGet do właściwości *. csproj* jako programu MSBuild.

   Aby uzyskać listę dostępnych metadanych pakietu i nazw właściwości programu MSBuild, zobacz [pakiet Target](../reference/msbuild-targets.md#pack-target). Zobacz również [kontrolowanie elementów zależnych](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

   Jeśli chcesz oddzielić właściwości związane z kompilacją z metadanych NuGet, możesz użyć innej `PropertyGroup`lub umieścić właściwości NuGet w innym pliku i użyć `Import` dyrektywy MSBuild do dołączenia. `Directory.Build.Props`i `Directory.Build.Targets` są również obsługiwane począwszy od programu MSBuild 15,0.

5. Teraz można używać `dotnet pack` elementów i wyników *. nupkg* , które są zarówno .NET Standard 2,0, jak i .NET Framework 4,5.

Oto plik *. csproj* , który jest generowany przy użyciu powyższych kroków i zestaw .NET Core SDK 2,2.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>Zobacz także

* [Jak określić Platformy docelowe](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [Obsługiwane rozwiązania międzyplatformowe](/dotnet/standard/library-guidance/cross-platform-targeting)
