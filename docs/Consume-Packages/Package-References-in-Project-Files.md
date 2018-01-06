---
title: NuGet PackageReference w plikach projektu programu Visual Studio | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "Szczegółowe informacje o NuGet PackageReference w plikach projektu obsługiwana przez NuGet 4.0 + i VS2017"
keywords: "Zależności pakietów NuGet, odwołania do pakietu, projektu packages.config pliki, PackageReference, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 275957c94e4a4bb45f359cd48816acf4f286ebad
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="package-references-packagereference-in-project-files"></a>Odwołania do pakietu (PackageReference) w plikach projektu

Pakiet odwołań, za pomocą `PackageReference` węzła, umożliwiają zarządzanie zależności NuGet bezpośrednio w ramach plików projektu, zamiast konieczności oddzielnego `packages.config` lub `project.json` pliku. Ta metoda nie ma wpływu na inne aspekty NuGet; na przykład ustawienia w `NuGet.Config` plików (w tym źródeł pakietów) nadal są stosowane zgodnie z objaśnieniem w [Konfigurowanie zachowania NuGet](Configuring-NuGet-Behavior.md).

> [!Important]
> Obecnie odwołania do pakietu są obsługiwane w Visual Studio 2017 tylko dla projektów .NET Core, .NET Standard projektów i projekty platformy UWP przeznaczonych dla systemu Windows 10 kompilacji 15063 (twórców aktualizacji).

`PackageReference` Podejście pozwala na warunki MSBuild umożliwia wybieranie odwołania do pakietu dla platformy docelowej, konfiguracji, platformy lub inne grupy. Umożliwia on również precyzyjną kontrolę nad zależności i zawartości przepływu. Pod względem zachowania i [rozpoznawania zależności](Dependency-Resolution.md), jest taka sama jak `project.json`.

Więcej szczegółów o integracji programu MSBuild z odwołaniami do pakietu w plikach projektu, zobacz [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../schema/msbuild-targets.md).

## <a name="adding-a-packagereference"></a>Dodawanie PackageReference

Dodawanie zależności w pliku projektu, używając następującej składni:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Kontrolowanie wersję zależności

Konwencja określania wersji pakietu jest taka sama jak przy użyciu `packages.config` lub `project.json`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

W powyższym przykładzie 3.6.0 oznacza dowolną wersję, którą jest > = 3.6.0, z preferencją dla Najniższa wersja zgodnie z opisem na [wersji pakietu](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="floating-versions"></a>Liczby zmiennoprzecinkowe wersji

[Liczby zmiennoprzecinkowe wersji](../consume-packages/dependency-resolution.md#floating-versions) są obsługiwane z `PackageReference`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Kontrolowanie zależności zasobów

Mogą używać zależność wyłącznie jako kontroler programowanie i może nie należy udostępniać który do projektów, które będą korzystać z pakietu. W tym scenariuszu można użyć `PrivateAssets` metadanych do kontroli tego zachowania.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Następujących tagów metadanych kontrolować zależności zasobów:

| Tag | Opis | Wartość domyślna |
| --- | --- | --- |
| IncludeAssets | Te zasoby będą używane. | wszystkie |
| ExcludeAssets | Te zasoby nie będą używane. | brak | 
| PrivateAssets | Te zasoby będą działały, ale nie będą przepływać do projektu nadrzędnego | pliki; analizatorów kompilacji |


Dopuszczalne wartości tych tagów są następujące, z wieloma wartościami oddzielone średnikami z wyjątkiem z `all` i `none` której musi występować samodzielnie:

| Wartość | Opis |
| --- | ---
| Kompilacji | Zawartość `lib` folderu |
| środowisko uruchomieniowe | Zawartość `runtime` folderu |
| Pliki | Zawartość `contentfiles` folderu |
| kompilacja | Właściwości i elementów docelowych w `build` folderu |
| Analizatory | Analizatory .NET |
| natywne | Zawartość `native` folderu |
| brak | Żadne z powyższych są używane. |
| wszystkie | Wszystkie powyższe (z wyjątkiem `none`) |

W poniższym przykładzie wszystkie elementy z wyjątkiem plików zawartości z pakietu może być zużyte przez projekt i wszystkie elementy z wyjątkiem plików zawartości i analizatorów będą przepływać do projektu nadrzędnego.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Należy pamiętać, że ponieważ `build` nie wchodzi z `PrivateAssets`, elementów docelowych i właściwości *będzie* przepływu projektu nadrzędnego. Należy wziąć pod uwagę, na przykład, że powyższe odwołania jest używana w projekt, który tworzy pakiet NuGet o nazwie AppLogger. Cele i właściwości, z jaką może wykorzystać AppLogger `Contoso.Utility.UsefulStuff`, jak można projektów używające AppLogger.

## <a name="adding-a-packagereference-condition"></a>Dodawanie warunku PackageReference

W przypadku użycia warunku do formantu, czy pakiet jest uwzględnione, których warunki, można użyć dowolnej zmiennej MSBuild lub zmienna zdefiniowana w pliku elementów docelowych lub właściwości. Jednak w chwili obecnej tylko `TargetFramework` zmiennej jest obsługiwana.

Na przykład docelowych `netstandard1.4` oraz `net452` , ale ma zależność, która ma zastosowanie tylko do `net452`. W takim przypadku nie mają `netstandard1.4` projektu, który zużywa pakietu, aby dodać Zależność ta niepotrzebne. Aby tego uniknąć, należy określić warunek na `PackageReference` w następujący sposób:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

Pakiet, który został utworzony przy użyciu tego projektu zostanie pokazują, że Newtonsoft.json jest uwzględniona jako zależności tylko w przypadku `net452` docelowych:

![Wynik zastosowania warunek na PackageReference z VS2017](media/PackageReference-Condition.png)

Warunki można stosować na `ItemGroup` poziomu i będą stosowane do wszystkich obiektów podrzędnych `PackageReference` elementy:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
