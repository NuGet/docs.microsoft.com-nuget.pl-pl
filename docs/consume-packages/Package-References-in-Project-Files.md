---
title: Formatu NuGet PackageReference (odwołania do pakietu w plikach projektu)
description: Szczegółowe informacje na temat formatu NuGet PackageReference w plikach projektu jako obsługiwane przez NuGet 4.0 + i programu VS 2017 i platformy .NET Core 2.0
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 48930701f1bb5f13718505b85b293f38d37d19fb
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508351"
---
# <a name="package-references-packagereference-in-project-files"></a>Odwołania do pakietu (PackageReference) w plikach projektu

Pakiet odwołań, za pomocą `PackageReference` węzła, zarządzanie zależnościami NuGet bezpośrednio z poziomu plików projektu (w przeciwieństwie do oddzielnego `packages.config` pliku). Za pomocą funkcji PackageReference, ponieważ jest to, nie ma wpływu na inne aspekty pakietu nuget; na przykład ustawienia w `NuGet.Config` plików (w tym źródeł pakietów) nadal są stosowane zgodnie z objaśnieniem w [Konfigurowanie zachowania pakietu NuGet](configuring-nuget-behavior.md).

Za pomocą funkcji PackageReference umożliwia także warunki MSBuild do wyboru na platformę docelową, konfiguracji, platforma lub inne grupy będzie odwoływał się pakiet. Umożliwia ona również szczegółową kontrolę nad tym zależności i zawartości przepływu. (Aby uzyskać więcej informacji, zobacz [NuGet pakowanie i przywrócić jako elementów docelowych MSBuild](../reference/msbuild-targets.md).)

Domyślnie PackageReference jest używany dla projektów .NET Core, .NET Standard projektów i projektów platformy UWP przeznaczonych dla systemu Windows 10 kompilacja 15063 (Aktualizacja dla twórców) lub nowszy, z wyjątkiem projektów platformy UWP w języku C++. Projekty programu .NET framework pełnej obsługi PackageReference, ale obecnie domyślnie `packages.config`. Aby korzystać z funkcji PackageReference, migracja zależności z `packages.config` do pliku projektu, a następnie usuń packages.config.

## <a name="adding-a-packagereference"></a>Dodawanie odwołanie PackageReference

Dodawanie zależności w pliku projektu przy użyciu następującej składni:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Kontrolowanie wersja zależności

Konwencja określania wersję pakietu jest taka sama jak, korzystając z `packages.config`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

W powyższym przykładzie 3.6.0 oznacza dowolną wersję, którą jest > = 3.6.0 z preferencją dla Najniższa wersja zgodnie z opisem na [przechowywanie wersji pakietów](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Za pomocą funkcji PackageReference dla projektu z nie składnika PackageReferences
Zaawansowane: Jeśli ma żadnych pakietów zainstalowany w projekcie (nie składnika PackageReferences w pliku projektu) i Brak pliku packages.config, ale Project, które ma zostać przywrócone jako styl PackageReference, możesz ustawić właściwość projektu RestoreProjectStyle do odwołania PackageReference w plik projektu.
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
Może to być przydatne, jeśli odwołujesz się projekty, które są PackageReference różne (istniejącego pliku csproj lub projektów w stylu zestawu SDK). Spowoduje to włączenie pakiety, które projekty dotyczą przywoływanie "przechodnio" w projekcie.

## <a name="floating-versions"></a>Wersje

[Wersje](../consume-packages/dependency-resolution.md#floating-versions) są obsługiwane w przypadku `PackageReference`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Kontrolowanie zależności zasobów

Być może używasz zależność wyłącznie jako kontroler rozwoju i nie chcieć ujawnić, do projektów, które będą korzystać z pakietu. W tym scenariuszu można użyć `PrivateAssets` metadanych w celu kontrolowania tego zachowania.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Następujące tagi metadanych kontrolować zasoby zależności:

| Tag | Opis | Wartość domyślna |
| --- | --- | --- |
| IncludeAssets | Te zasoby będą używane. | wszystkie |
| ExcludeAssets | Te zasoby nie będą używane. | brak |
| PrivateAssets | Te zasoby będą używane, ale nie będzie przepływać do projektu nadrzędnego | contentfiles;analyzers;build |

Dopuszczalnych wartości dla tych tagów, są w następujący sposób, przy użyciu wielu wartości, rozdzielając je średnikiem z wyjątkiem za pomocą `all` i `none` której musi znajdować się w sobie:

| Wartość | Opis |
| --- | ---
| Kompilacji | Zawartość `lib` folder i formanty czy projektu można kompilować dla zestawów w folderze |
| środowisko uruchomieniowe | Zawartość `lib` i `runtimes` folder i formanty czy te zestawy będzie kopiowana do kompilacji katalogu wyjściowego |
| Pliki | Zawartość `contentfiles` folderu |
| kompilacja | Właściwości i elementów docelowych w `build` folderu |
| Analizatory | Analizatory platformy .NET |
| natywne | Zawartość `native` folderu |
| brak | Żadne z powyższych są używane. |
| wszystkie | Wszystkie powyższe (z wyjątkiem `none`) |

W poniższym przykładzie wszystkim, z wyjątkiem plików zawartości z pakietu może być używane przez projekt i wszystkim, z wyjątkiem analizatory i pliki zawartości będą przepływać do projektu nadrzędnego.

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

Należy pamiętać, że ponieważ `build` nie znajduje się za pomocą `PrivateAssets`, cele i właściwości *będzie* przepływ do nadrzędnego projektu. Należy wziąć pod uwagę, na przykład, że odwołanie powyżej jest używany w projekcie, który tworzy pakiet NuGet o nazwie AppLogger. AppLogger mogą wykorzystywać obiektów docelowych i właściwości z `Contoso.Utility.UsefulStuff`, tak jak w projektach korzystających z AppLogger.

## <a name="adding-a-packagereference-condition"></a>Dodawanie warunku PackageReference

Możesz użyć warunek do kontroli, czy pakiet jest uwzględnione, w przypadku, gdy warunki, można użyć dowolnej zmiennej programu MSBuild lub zmienną zdefiniowaną w pliku elementów docelowych lub właściwości. Jednak w obecnie tylko `TargetFramework` zmienna jest obsługiwana.

Załóżmy na przykład, gdy elementem docelowym `netstandard1.4` także `net452` , ale ma zależność, która ma zastosowanie tylko do `net452`. W takim przypadku nie ma `netstandard1.4` projektu, który zużywa pakietu do dodania tej zależności niepotrzebne. Aby temu zapobiec, określamy warunek na `PackageReference` w następujący sposób:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Pakiet, który został skompilowany przy użyciu tego projektu pokaże, że pakiet Newtonsoft.Json jest uwzględniany jako zależności tylko w przypadku `net452` docelowej:

![Wynik zastosowania warunku na PackageReference za pomocą programu VS 2017](media/PackageReference-Condition.png)

Warunki mogą być również stosowane przy `ItemGroup` poziomu i będą stosowane do wszystkich obiektów podrzędnych `PackageReference` elementy:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
