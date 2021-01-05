---
title: Format PackageReference NuGet (odwołania do pakietów w plikach projektu)
description: Szczegóły dotyczące PackageReference NuGet w plikach projektu, które są obsługiwane przez narzędzia NuGet 4.0 + i program VS2017 i .NET Core 2,0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 1127e7aee27d57abd5f14dd3bea82dfff3ba6d93
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699782"
---
# <a name="package-references-packagereference-in-project-files"></a>Odwołania do pakietów (PackageReference) w plikach projektu

Odwołania do pakietów, używanie `PackageReference` węzła, zarządzanie zależnościami NuGet bezpośrednio w plikach projektu (w przeciwieństwie do oddzielnego `packages.config` pliku). Przy użyciu PackageReference, gdy jest wywoływana, nie ma wpływu na inne aspekty NuGet; na przykład ustawienia w `NuGet.config` plikach (w tym źródła pakietów) są nadal stosowane, jak wyjaśniono w [typowych konfiguracjach NuGet](configuring-nuget-behavior.md).

Za pomocą PackageReference można także użyć warunków MSBuild, aby wybrać odwołania do pakietów dla platformy docelowej lub innych grup. Umożliwia również precyzyjne sterowanie zależnościami i przepływem zawartości. (Zobacz, aby uzyskać więcej szczegółów na temat [pakietu NuGet i przywracania jako elementy docelowe programu MSBuild](../reference/msbuild-targets.md)).

## <a name="project-type-support"></a>Obsługa typu projektu

Domyślnie PackageReference jest używany dla projektów .NET Core, projektów .NET Standard i projektów platformy UWP przeznaczonych dla systemu Windows 10 Build 15063 (Aktualizacja dla twórców) i nowszych, z wyjątkiem projektów C++ platformy UWP. Projekty .NET Framework obsługują PackageReference, ale obecnie domyślnie `packages.config` . Aby użyć PackageReference, [Migruj](../consume-packages/migrate-packages-config-to-package-reference.md) zależności z `packages.config` do pliku projektu, a następnie usuń packages.config.

ASP.NET aplikacje obsługujące pełną .NET Framework obejmują tylko [ograniczoną obsługę](https://github.com/NuGet/Home/issues/5877) PackageReference. Typy projektów C++ i JavaScript nie są obsługiwane.

## <a name="adding-a-packagereference"></a>Dodawanie elementu PackageReference

Dodaj zależność w pliku projektu przy użyciu następującej składni:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Kontrolowanie wersji zależności

Konwencja określania wersji pakietu jest taka sama jak w przypadku użycia `packages.config` :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

W powyższym przykładzie 3.6.0 oznacza dowolną wersję, która jest >= 3.6.0 z preferencją dla najniższej wersji, zgodnie z opisem w temacie [przechowywanie wersji pakietu](../concepts/package-versioning.md#version-ranges).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Używanie PackageReference dla projektu bez składnika packagereferences

Zaawansowane: Jeśli nie masz żadnych pakietów zainstalowanych w projekcie (nie składnika packagereferences w pliku projektu i nie packages.config pliku), ale chcesz, aby projekt został przywrócony jako styl PackageReference, można ustawić właściwość projektu RestoreProjectStyle na PackageReference w pliku projektu.

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

Może to być przydatne, jeśli odwołują się do projektów, które są PackageReference w stylu (istniejące projekty csproj lub zestawu SDK). Spowoduje to włączenie pakietów, do których odwołują się te projekty, do których odwołuje się projekt.

## <a name="packagereference-and-sources"></a>PackageReference i źródła

W projektach PackageReference, przechodnie wersje zależności są rozwiązywane w czasie przywracania. W związku z tym w projektach PackageReference wszystkie źródła muszą być dostępne dla wszystkich operacji przywracania. 

## <a name="floating-versions"></a>Wersje zmiennoprzecinkowe

[Wersje zmiennoprzecinkowe](../concepts/dependency-resolution.md#floating-versions) są obsługiwane za pomocą `PackageReference` :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Kontrolowanie zasobów zależności

Można używać zależności wyłącznie jako zespołu programistycznego i może nie chcieć ujawniać projektów, które będą korzystać z pakietu. W tym scenariuszu można użyć `PrivateAssets` metadanych do kontrolowania tego zachowania.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Następujące znaczniki metadanych kontrolują elementy zależne:

| Tag | Description | Wartość domyślna |
| --- | --- | --- |
| IncludeAssets | Te zasoby zostaną wykorzystane | all |
| ExcludeAssets | Te zasoby nie będą używane | brak |
| PrivateAssets | Te zasoby będą wykorzystane, ale nie będą przepływać do projektu nadrzędnego | contentfiles; analizatory; kompilacja |

Wartości dozwolone dla tych tagów są następujące, z wieloma wartościami oddzielonymi średnikami z wyjątkiem `all` i, `none` które muszą być wyświetlane przez siebie:

| Wartość | Opis |
| --- | ---
| kompilowanie | Zawartość `lib` folderu i kontroluje, czy projekt może być kompilowany względem zestawów w folderze |
| środowisko uruchomieniowe | Zawartość `lib` `runtimes` folderu i i kontroluje, czy te zestawy zostaną skopiowane do katalogu wyjściowego kompilacji |
| contentFiles | Zawartość `contentfiles` folderu |
| kompilacja | `.props` i `.targets` w `build` folderze |
| buildMultitargeting | *(4,0)* `.props` i `.targets` w `buildMultitargeting` folderze, dla celów określania wartości docelowej między platformami |
| buildTransitive | *(5.0 +)* `.props` i `.targets` w `buildTransitive` folderze, dla zasobów, które są przesyłane przechodniie do dowolnego, zużywanego projektu. Zobacz stronę [funkcji](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) . |
| Analizatory | Analizatory .NET |
| natywne | Zawartość `native` folderu |
| brak | Żadne z powyższych nie jest używane. |
| all | Wszystkie powyższe (z wyjątkiem `none` ) |

W poniższym przykładzie wszystko, z wyjątkiem plików zawartości z pakietu, będzie używane przez projekt, a wszystko z wyjątkiem plików zawartości i analizatorów przepływa do projektu nadrzędnego.

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

Należy pamiętać, że `build` `PrivateAssets` element targets i props *będzie* przepływać do projektu nadrzędnego, ponieważ nie jest zawarty w elemencie. Rozważmy na przykład, że odwołanie powyżej jest używane w projekcie, który kompiluje pakiet NuGet o nazwie AppLogger. AppLogger może zużywać elementy docelowe i wartości z `Contoso.Utility.UsefulStuff` , jak w przypadku projektów, które zużywają AppLogger.

> [!NOTE]
> Gdy `developmentDependency` jest ustawiona na `true` w `.nuspec` pliku, oznacza to pakiet jako zależność tylko do programowania, co uniemożliwi uwzględnienie pakietu jako zależności w innych pakietach. W przypadku PackageReference *(NuGet 4.8 +)* ta flaga oznacza również, że wykluczają się zasoby czasu kompilacji z kompilacji. Aby uzyskać więcej informacji, zobacz [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).

## <a name="adding-a-packagereference-condition"></a>Dodawanie warunku PackageReference

Możesz użyć warunku, aby określić, czy pakiet jest uwzględniony, gdzie warunki mogą używać dowolnej zmiennej MSBuild lub zmiennej zdefiniowanej w pliku TARGETS lub props. Jednak obecnie `TargetFramework` obsługiwana jest tylko zmienna.

Załóżmy na przykład, że jesteś elementem docelowym, `netstandard1.4` `net452` a także masz zależność, która ma zastosowanie tylko do `net452` . W takim przypadku nie chcesz, `netstandard1.4` aby projekt zużywał pakiet, aby dodać niepotrzebną zależność. Aby tego uniknąć, należy określić warunek w następujący sposób `PackageReference` :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Pakiet skompilowany przy użyciu tego projektu będzie pokazywał, że Newtonsoft.Json jest uwzględniany jako zależność tylko dla `net452` elementu docelowego:

![Wynik zastosowania warunku na PackageReference z program VS2017](media/PackageReference-Condition.png)

Warunki mogą być również stosowane na `ItemGroup` poziomie i będą miały zastosowanie do wszystkich `PackageReference` elementów podrzędnych:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>GeneratePathProperty

Ta funkcja jest dostępna w programie NuGet **5,0** lub nowszym oraz z programem Visual Studio 2019 **16,0** lub nowszym.

Czasami należy odwoływać się do plików w pakiecie z elementu docelowego programu MSBuild.
W `packages.config` projektach opartych na programie pakiety są instalowane w folderze względem pliku projektu. Jednak w PackageReference pakiety są [używane](../concepts/package-installation-process.md) z folderu *Global-Packages* , który może się różnić w zależności od maszyny do komputera.

Aby połączyć ten odstęp, pakiet NuGet wprowadził Właściwość wskazującą lokalizację, z której będzie korzystać pakiet.

Przykład:

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

Dodatkowo NuGet automatycznie generuje właściwości dla pakietów zawierających folder Tools.

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

Właściwości programu MSBuild i tożsamości pakietów nie mają tych samych ograniczeń, więc tożsamość pakietu musi zostać zmieniona na przyjazną nazwę MSBuild, poprzedzoną prefiksem `Pkg` .
Aby sprawdzić dokładną nazwę wygenerowanej właściwości, zobacz wygenerowany plik [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) .

## <a name="packagereference-aliases"></a>Aliasy PackageReference

W niektórych rzadkich przypadkach różne pakiety będą zawierać klasy znajdujące się w tej samej przestrzeni nazw. Począwszy od programu NuGet 5,7 & Visual Studio 2019 Update 7, równoważne z elementu ProjectReference, PackageReference obsługuje [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases) .
Domyślnie nie są udostępniane żadne aliasy. Po określeniu aliasu *wszystkie* zestawy pochodzące z pakietu zawierającego adnotacje muszą być przywoływane z aliasem.

Przykładowe użycie można sprawdzić pod adresem [NuGet\Samples](https://github.com/NuGet/Samples/tree/master/PackageReferenceAliasesExample)

W pliku projektu Określ aliasy w następujący sposób:

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

i w kodzie używają go w następujący sposób:

```cs
extern alias ExampleAlias;

namespace PackageReferenceAliasesExample
{
...
        {
            var version = ExampleAlias.NuGet.Versioning.NuGetVersion.Parse("5.0.0");
            Console.WriteLine($"Version : {version}");
        }
...
}

```

## <a name="nuget-warnings-and-errors"></a>Ostrzeżenia i błędy NuGet

*Ta funkcja jest dostępna w programie NuGet **4,3** lub nowszym oraz z programem Visual Studio 2017 **15,3** lub nowszym.*

W przypadku wielu scenariuszy pakietów i przywracania wszystkie ostrzeżenia i błędy NuGet są kodowane i zaczynają się od `NU****` . Wszystkie ostrzeżenia i błędy programu NuGet są wymienione w dokumentacji [referencyjnej](../reference/errors-and-warnings.md) .

Pakiet NuGet obserwuje następujące właściwości ostrzegawcze:

- `TreatWarningsAsErrors`Traktuj wszystkie ostrzeżenia jako błędy
- `WarningsAsErrors`Traktuj konkretne ostrzeżenia jako błędy
- `NoWarn`ukrywanie określonych ostrzeżeń, całego projektu lub całego pakietu.

Przykłady:

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a>Pomijanie ostrzeżeń NuGet

Chociaż zaleca się, aby wszystkie ostrzeżenia NuGet były rozwiązywane podczas operacji pakietu i przywracania, w niektórych sytuacjach jest to uzasadnione.
Aby pominąć ostrzeżenia na poziomie projektu, rozważ wykonanie:

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

Czasami ostrzeżenia dotyczą tylko określonego pakietu na grafie. Możemy zrezygnować z pominięcia tego ostrzeżenia przez dodanie `NoWarn` elementu PackageReference. 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Pomijanie ostrzeżeń pakietu NuGet w programie Visual Studio

W programie Visual Studio można także [pominąć ostrzeżenia](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) za pomocą środowiska IDE.

## <a name="locking-dependencies"></a>Blokowanie zależności

*Ta funkcja jest dostępna w programie NuGet **4,9** lub nowszym oraz z programem Visual Studio 2017 **15,9** lub nowszym.*

Dane wejściowe do przywracania NuGet to zbiór odwołań do pakietów z pliku projektu (zależności najwyższego poziomu lub bezpośrednie), a dane wyjściowe to pełny zamknięcie wszystkich zależności pakietu, w tym zależności przechodnie. Pakiet NuGet próbuje zawsze utworzyć to samo pełne zamknięcie zależności pakietów, jeśli lista wejściowa PackageReference nie została zmieniona. Jednak istnieją pewne scenariusze, w których nie można tego zrobić. Na przykład:

* W przypadku korzystania z wersji zmiennoprzecinkowych, takich jak `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` . Gdy zachodzi taka potrzeba, aby przepływać do najnowszej wersji przy każdym przywracaniu pakietów, istnieją scenariusze, w których użytkownicy wymagają, aby wykres był zablokowany do określonej najnowszej wersji i przepływał do nowszej wersji, o ile jest dostępny, przy jawnym gestie.
* Opublikowana jest nowsza wersja pakietu spełniająca wymagania dotyczące wersji PackageReference. Na przykład 

  * Dzień 1: Jeśli określono `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` , ale wersje dostępne w repozytoriach NuGet zostały 4.1.0, 4.2.0 i 4.3.0. W takim przypadku pakiet NuGet zostałby rozpoznany jako 4.1.0 (Najbliższa wersja minimalna)

  * Dzień 2: wersja 4.0.0 zostaje opublikowana. Pakiet NuGet znajdzie teraz dokładne dopasowanie i zacznie rozwiązywać 4.0.0

* Dana wersja pakietu jest usuwana z repozytorium. Chociaż nuget.org nie zezwala na usuwanie pakietów, te ograniczenia nie są dostępne dla wszystkich repozytoriów pakietów. Spowoduje to znalezienie najlepszego dopasowania przez pakiet NuGet, gdy nie można rozwiązać go do usuniętej wersji.

### <a name="enabling-lock-file"></a>Włączanie pliku blokady

W celu utrwalenia pełnego zamknięcia zależności pakietu można wybrać funkcję blokowania pliku przez ustawienie właściwości MSBuild `RestorePackagesWithLockFile` dla projektu:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Jeśli ta właściwość jest ustawiona, przywracanie NuGet wygeneruje plik blokady pliku `packages.lock.json` w katalogu głównym projektu, który zawiera listę wszystkich zależności pakietu. 

> [!Note]
> Gdy projekt zawiera `packages.lock.json` plik w katalogu głównym, plik blokady jest zawsze używany z przywracaniem, nawet jeśli właściwość `RestorePackagesWithLockFile` nie jest ustawiona. Innym sposobem na zgodę na tę funkcję jest utworzenie fikcyjnego pustego `packages.lock.json` pliku w katalogu głównym projektu.

### <a name="restore-behavior-with-lock-file"></a>`restore` zachowanie z plikiem blokady
Jeśli plik blokady jest obecny dla projektu, NuGet używa tego pliku blokady do uruchomienia `restore` . Program NuGet sprawdza, czy w zależnościach pakietu zostały wprowadzone jakiekolwiek zmiany, jak wspomniano w pliku projektu (lub w plikach projektów zależnych) i czy nie wprowadzono żadnych zmian, po prostu przywraca pakiety wymienione w pliku blokady. Nie ma potrzeby ponownej oceny zależności pakietów.

Jeśli NuGet wykryje zmianę zdefiniowanych zależności, jak wspomniano w plikach projektu, ponownie oblicza Graf pakietu i aktualizuje plik blokady w celu odzwierciedlenia nowego zamknięcia pakietu dla projektu.

W przypadku ciągłej integracji/ciągłego wdrażania i innych scenariuszy, w których nie chcesz zmienić zależności pakietu na bieżąco, możesz to zrobić, ustawiając następujące polecenie `lockedmode` `true` :

W przypadku dotnet.exe Uruchom polecenie:

```
> dotnet.exe restore --locked-mode
```

W przypadku msbuild.exe Uruchom polecenie:

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Możesz również ustawić tę właściwość warunkowego programu MSBuild w pliku projektu:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

W przypadku opcji Tryb zablokowany `true` przywracanie spowoduje przywrócenie dokładnych pakietów wymienionych w pliku blokady lub niepowodzenie w przypadku zaktualizowania zdefiniowanych zależności pakietu dla projektu po utworzeniu pliku blokady.

### <a name="make-lock-file-part-of-your-source-repository"></a>Utwórz część pliku blokady w repozytorium źródłowym
W przypadku kompilowania aplikacji plik wykonywalny i projekt w danym momencie znajdują się na początku łańcucha zależności, a następnie należy zaewidencjonować plik blokady do repozytorium kodu źródłowego, aby pakiet NuGet mógł go używać podczas przywracania.

Jeśli jednak projekt jest projektem biblioteki, który nie jest dostarczany lub wspólny projekt kodu, od którego zależą inne projekty, **nie należy** ewidencjonować pliku blokady jako części kodu źródłowego. Nie ma szkody w zachowaniu pliku blokady, ale zablokowane zależności pakietu dla wspólnego projektu kodu nie mogą być używane, jak wymieniono w pliku blokady podczas przywracania/kompilowania projektu, który zależy od tego projektu Common-Code.

Na przykład:

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

Jeśli `ProjectA` ma zależność od `PackageX` wersji `2.0.0` , a także odwołania, `ProjectB` które są zależne od `PackageX` wersji `1.0.0` , plik blokady `ProjectB` zostanie wystawiony zależności od `PackageX` wersji `1.0.0` . Jednak po `ProjectA` skompilowaniu jego plik blokady będzie zawierał zależność od `PackageX` wersji **`2.0.0`** , a **nie** `1.0.0` tak jak na liście w pliku blokady dla `ProjectB` . W ten sposób plik blokady wspólnego projektu kodu ma niewielki stan dla projektów, które są od niego zależne.

### <a name="lock-file-extensibility"></a>Zablokuj rozszerzalność plików

Można kontrolować różne zachowania przywracania za pomocą pliku blokady zgodnie z poniższym opisem:

| Opcja NuGet.exe | Opcja dotnet | Odpowiednik opcji programu MSBuild | Opis |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | Umożliwia użycie pliku blokady. |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | Włącza tryb zablokowany do przywracania. Jest to przydatne w scenariuszach ciągłej integracji/ciągłego wdrażania.|   
| `-ForceEvaluate` | `--force-evaluate` | RestoreForceEvaluate | Ta opcja jest przydatna w przypadku pakietów z wersją zmiennoprzecinkową zdefiniowaną w projekcie. Domyślnie przywracanie pakietu NuGet nie będzie automatycznie aktualizować wersji programu przy każdym przywracaniu, chyba że zostanie uruchomiony przycisk Przywróć z tą opcją. |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | Definiuje niestandardową lokalizację pliku blokady dla projektu. Domyślnie pakiet NuGet obsługuje `packages.lock.json` w katalogu głównym. Jeśli masz wiele projektów w tym samym katalogu, pakiet NuGet obsługuje plik blokady specyficzny dla projektu `packages.<project_name>.lock.json` |
