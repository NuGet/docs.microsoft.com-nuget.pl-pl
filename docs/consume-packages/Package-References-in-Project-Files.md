---
title: Formatu NuGet PackageReference (odwołania do pakietu w plikach projektu)
description: Szczegółowe informacje na temat formatu NuGet PackageReference w plikach projektu jako obsługiwane przez NuGet 4.0 + i programu VS 2017 i platformy .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c2dfce8de6b28aaee99e3d5ab75cd28950a8cb0f
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812840"
---
# <a name="package-references-packagereference-in-project-files"></a>Odwołania do pakietu (PackageReference) w plikach projektu

Pakiet odwołań, za pomocą `PackageReference` węzła, zarządzanie zależnościami NuGet bezpośrednio z poziomu plików projektu (w przeciwieństwie do oddzielnego `packages.config` pliku). Za pomocą funkcji PackageReference, ponieważ jest to, nie ma wpływu na inne aspekty pakietu nuget; na przykład ustawienia w `NuGet.config` plików (w tym źródeł pakietów) nadal są stosowane zgodnie z objaśnieniem w [Konfigurowanie zachowania pakietu NuGet](configuring-nuget-behavior.md).

Za pomocą funkcji PackageReference umożliwia także warunki MSBuild do wyboru na platformę docelową, konfiguracji, platforma lub inne grupy będzie odwoływał się pakiet. Umożliwia ona również szczegółową kontrolę nad tym zależności i zawartości przepływu. (Aby uzyskać więcej informacji, zobacz [NuGet pakowanie i przywrócić jako elementów docelowych MSBuild](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Obsługa typu projektu

Domyślnie PackageReference jest używany dla projektów .NET Core, .NET Standard projektów i projektów platformy UWP przeznaczonych dla systemu Windows 10 kompilacja 15063 (Aktualizacja dla twórców) lub nowszy, z wyjątkiem projektów platformy UWP w języku C++. Projektów programu .NET framework obsługuje PackageReference, ale obecnie domyślnie `packages.config`. Aby użyć funkcji PackageReference, [migracji](../reference/migrate-packages-config-to-package-reference.md) zależności z `packages.config` do pliku projektu, a następnie usuń packages.config.

Aplikacje ASP.NET przeznaczone dla pełny program .NET Framework zawierają tylko [ograniczoną obsługę](https://github.com/NuGet/Home/issues/5877) dla funkcji PackageReference. C++i typów projektów języka JavaScript nie są obsługiwane.

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
Zaawansowane: Jeśli ma żadnych pakietów zainstalowany w projekcie (nie składnika PackageReferences w pliku projektu) i Brak pliku packages.config, ale Project, które ma zostać przywrócone jako styl PackageReference w projekcie można ustawić właściwości projektu RestoreProjectStyle PackageReference plik.
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

## <a name="locking-dependencies"></a>Blokowanie zależności
*Ta funkcja jest dostępna z NuGet **4.9** lub w górę i w programie Visual Studio 2017 **15.9** lub nowszej.*

Dane wejściowe, aby przywracanie pakietów NuGet jest zestaw odwołania do pakietu z pliku projektu (zależności najwyższego poziomu lub direct) i dane wyjściowe są pełne zamknięcie wszystkie zależności pakietów wraz z zależnościami przechodnie. NuGet próbuje zawsze powodowało tego samego pełne zamknięcie zależności pakietów, jeśli lista wejściowa PackageReference nie uległy zmianie. Jednak istnieją pewne scenariusze, w którym nie jest w stanie to zrobić. Na przykład:

* Gdy używasz liczb zmiennoprzecinkowych wersji, takich jak `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`. Natomiast tutaj jest float do najnowszej wersji podczas każdego przywracania pakietów, istnieją scenariusze, w której użytkownicy wymagają wykresu zostanie zablokowane do niektórych najnowszej wersji, a wartość zmiennoprzecinkowa do nowszej wersji, jeśli to możliwe, na jawne gestu.
* Nowsza wersja pakietu zgodnego PackageReference wymagania dotyczące wersji została opublikowana. Na przykład 

  * Dzień 1: Jeśli określono `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` , ale wersje dostępne w repozytoria NuGet 4.1.0, 4.2.0 i 4.3.0. W tym przypadku NuGet czy problem został rozwiązany w celu 4.1.0 (najbliższym minimalna wersja)

  * Dzień 2: Zostanie opublikowany w wersji 4.0.0. NuGet teraz zostanie znalezione dokładne dopasowanie i uruchomienia rozpoznawania 4.0.0

* Wersja dany pakiet zostanie usunięty z repozytorium. Chociaż nuget.org nie zezwala na usunięcia pakietu, nie wszystkie repozytoria pakietu ma tego ograniczenia. Skutkuje to znajdowanie najlepsze dopasowanie, gdy nie można rozpoznać usuniętych wersji NuGet.

### <a name="enabling-lock-file"></a>Włączenie pliku blokady
Aby zachować pełną zamknięcia zależności pakietów, które użytkownik może wyrazić zgodę na funkcji blokowania plików, ustawiając właściwość MSBuild `RestorePackagesWithLockFile` dla projektu:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Jeśli ta właściwość jest ustawiona, przywracanie pakietów NuGet, spowoduje wygenerowanie pliku blokady - `packages.lock.json` pliku w katalogu głównym projektu, który znajduje się wykaz zależności pakietów. 

> [!Note]
> Gdy projekt ma `packages.lock.json` plik w jego katalogu głównego pliku blokady jest zawsze używane przy użyciu przywracania nawet wtedy, gdy właściwość `RestorePackagesWithLockFile` nie jest ustawiona. Dlatego inny sposób, aby wyrazić zgodę na tę funkcję, jest utworzenie pustego fikcyjnego `packages.lock.json` pliku w katalogu głównym projektu.

### <a name="restore-behavior-with-lock-file"></a>`restore` zachowanie przy użyciu pliku blokady
Jeśli plik blokady jest obecny dla projektu, NuGet używa tego pliku blokady, aby uruchomić `restore`. NuGet jest szybkie sprawdzenie, czy wystąpiły wszelkie zmiany w zależności pakietów, jak wspomniano wcześniej w pliku projektu (lub pliki projektów zależnych), a jeśli nie wprowadzono żadnych zmian po prostu przywraca pakiety wymienione w pliku blokady. Nie ma żadnych ponownej oceny zależności pakietów.

Jeśli NuGet wykryje zmianę w zdefiniowanych zależności, jak wspomniano w plikach projektu, ponownie ocenia wykres pakietu i aktualizuje plik blokady w celu odzwierciedlenia nowego zamknięcia pakietu dla projektu.

Ciągła Integracja/ciągłe dostarczanie i inne scenariusze, w których nie chcesz zmienić zależności pakietów na bieżąco, możesz to zrobić, ustawiając `lockedmode` do `true`:

Aby uzyskać dotnet.exe Uruchom polecenie:
```
> dotnet.exe restore --locked-mode
```

Aby uzyskać msbuild.exe Uruchom polecenie:
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Można również ustawić właściwość ta warunkowe MSBuild w pliku projektu:
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Jeśli w trybie zablokowanym `true`, przywracania będzie przywrócić dokładnie pakiety wymienione w pliku blokady lub się nie powieść, jeśli zaktualizowane zależności pakietu zdefiniowanych dla projektu, po utworzeniu pliku blokady.

### <a name="make-lock-file-part-of-your-source-repository"></a>Blokowanie pliku częścią repozytorium źródłowym
Jeśli tworzysz aplikację, plik wykonywalny, a projekt jest na początku łańcuch zależności następnie zaewidencjonuj pliku blokady do repozytorium kodu źródłowego tak, aby wprowadzić NuGet z niego korzystać podczas przywracania.

Jednakże jeśli projekt jest projekt biblioteki, które nie dostarczaj lub wspólnej projekt kodu, na które inne projekty zależą od tego, możesz **nie powinien** Zaewidencjonuj pliku blokady jako część kodu źródłowego. Nie przynosi żadnych szkód w ochronie pliku blokady, ale zależności pakietu zablokowany dla wspólnego projektu kodu nie można używać, zgodnie z zaleceniami z pliku blokady podczas przywracania/kompilacji projektu, który zależy od tego projektu wspólnego kodu.

Np.
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
Jeśli `ProjectA` zależny od `PackageX` wersji `2.0.0` i odwołujący się `ProjectB` zależy `PackageX` wersji `1.0.0`, następnie blokada pliku `ProjectB` będzie wyświetlana zależność `PackageX` Wersja `1.0.0`. Jednak, gdy `ProjectA` powstała blokady plik będzie zawierać zależności na `PackageX` wersji **`2.0.0`** i **nie** `1.0.0` wymienionych w pliku blokady `ProjectB`. W związku z tym plik blokady wspólnego projektu kodu ma nieco powiedzieć za pośrednictwem pakietów dla projektów, które zależą od niej.

### <a name="lock-file-extensibility"></a>Rozszerzalność pliku blokady
Aby sterować różnych zachowań przywracania za pomocą pliku blokady, zgodnie z poniższym opisem:

| Opcja | Opcji równoważne MSBuild | 
|:---  |:--- |
| `--use-lock-file` | Bootstraps korzystanie z pliku blokady dla projektu. Można również ustawić `RestorePackagesWithLockFile` właściwość w pliku projektu | 
| `--locked-mode` | Włącza zablokowany tryb przywracania. Jest to przydatne w scenariuszach ciągłej integracji/ciągłego wdrażania, w której chcesz uzyskać powtarzalnych kompilacji. Może to być również przez ustawienie `RestoreLockedMode` właściwości programu MSBuild `true` |  
| `--force-evaluate` | Ta opcja jest przydatna przy użyciu pakietów przy użyciu wersji zmiennoprzecinkowy zdefiniowane w projekcie. Domyślnie, przywracanie pakietów NuGet nie może zaktualizować wersję pakietu automatycznie po każdym przywracania, chyba że uruchomieniu przywracania z `--force-evaluate` opcji. |
| `--lock-file-path` | Definiuje blokady niestandardowych lokalizacji plików dla projektu. Można to również osiągnąć przez ustawienie właściwości programu MSBuild `NuGetLockFilePath`. Domyślnie obsługuje NuGet `packages.lock.json` w katalogu głównym. Jeśli masz wiele projektów w tym samym katalogu NuGet obsługuje pliku blokady określonego projektu `packages.<project_name>.lock.json` |
