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
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>Obsługa wielu wersji programu .NET Framework w pliku projektu

Podczas pierwszego tworzenia projektu zaleca się utworzenie biblioteki klas .NET Standard, ponieważ zapewnia zgodność z najszerszym zakresem projektów zużywających. Korzystając ze standardu .NET Standard, domyślnie dodajesz [obsługę między platformami](/dotnet/standard/library-guidance/cross-platform-targeting) do biblioteki .NET. Jednak w niektórych scenariuszach może być również konieczne dołączenie kodu, który jest przeznaczony dla określonej struktury. W tym artykule pokazano, jak to zrobić dla projektów [w stylu SDK.](../resources/check-project-format.md)

W przypadku projektów w stylu zestawu SDK można skonfigurować obsługę wielu struktur docelowych `dotnet pack` [(TFM)](/dotnet/standard/frameworks)w pliku projektu, a następnie użyć lub `msbuild /t:pack` utworzyć pakiet.

> [!NOTE]
> nuget.exe CLI nie obsługuje pakowania projektów w stylu zestawu SDK, więc należy używać `dotnet pack` tylko lub `msbuild /t:pack`. Zaleca się [uwzględnić wszystkie właściwości,](../reference/msbuild-targets.md#pack-target) które `.nuspec` są zwykle w pliku w pliku projektu zamiast. Aby kierować reklamy na wiele wersji programu .NET Framework w projekcie w stylu nienawiązanym do zestawu SDK, zobacz [Obsługa wielu wersji programu .NET Framework](supporting-multiple-target-frameworks.md).

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>Tworzenie projektu obsługującego wiele wersji programu .NET Framework

1. Utwórz nową bibliotekę klas .NET Standard `dotnet new classlib`w programie Visual Studio lub użyj .

   Zaleca się utworzenie biblioteki klas .NET Standard w celu zapewnienia najlepszej zgodności.

2. Edytuj plik *csproj,* aby obsługiwać struktury docelowe. Na przykład zmień
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   na:
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   Upewnij się, że zmieniono element XML z liczby pojedynczej na mnogą (dodaj "s" do znaczników otwartych i zamkniętych).

3. Jeśli masz dowolny kod, który działa tylko w `#if NET45` jednym `#if NETSTANDARD2_0` TFM, można użyć lub oddzielić kod zależny od TFM. (Aby uzyskać więcej informacji, zobacz [Jak multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) Na przykład można użyć następującego kodu:

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

4. Dodaj wszystkie metadane NuGet, które chcesz do *.csproj* jako MSBuild właściwości.

   Aby uzyskać listę dostępnych metadanych pakietu i nazwy właściwości MSBuild, zobacz [miejsce docelowego pakowania](../reference/msbuild-targets.md#pack-target). Zobacz też [Kontrolowanie zasobów zależności](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

   Jeśli chcesz oddzielić właściwości związane z kompilacją z metadanych `PropertyGroup`NuGet, możesz użyć innego , lub umieścić właściwości `Import` NuGet w innym pliku i użyć dyrektywy MSBuild, aby ją uwzględnić. `Directory.Build.Props`i `Directory.Build.Targets` są również obsługiwane począwszy od MSBuild 15.0.

5. Teraz użyj `dotnet pack` i wynikowy *.nupkg* jest przeznaczony zarówno dla platformy .NET Standard 2.0, jak i .NET Framework 4.5.

Oto plik *csproj,* który jest generowany przy użyciu poprzednich kroków i .NET Core SDK 2.2.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>Zobacz też

* [Jak określić struktury docelowe](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [Obsługiwane rozwiązania międzyplatformowe](/dotnet/standard/library-guidance/cross-platform-targeting)
