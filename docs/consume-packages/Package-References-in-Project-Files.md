---
title: Format PackageReference pakietu NuGet (odwołania do pakietu w plikach projektu)
description: Szczegóły dotyczące odszukania pakietów NuGet w plikach projektu obsługiwanych przez pakiety NuGet 4.0+ i VS2017 oraz .NET Core 2.0
author: nkolev92
ms.author: nikolev
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c7b963352e0e9640844a213767a58c883ed0eeb9
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323716"
---
# <a name="package-references-packagereference-in-project-files"></a>Odwołania do pakietu ( `PackageReference` ) w plikach projektu

Odwołania do pakietu, używając węzła, zarządzają zależnościami NuGet bezpośrednio w plikach `PackageReference` projektu (w przeciwieństwie do oddzielnego `packages.config` pliku). Wywoływanie funkcji PackageReference nie ma wpływu na inne aspekty narzędzia NuGet. na przykład ustawienia w plikach (w tym źródła pakietów) są nadal stosowane, jak wyjaśniono w `NuGet.Config` tece [Common NuGet configurations (Typowe konfiguracje nuGet).](configuring-nuget-behavior.md)

Za pomocą funkcji PackageReference można również użyć warunków programu MSBuild, aby wybrać odwołania do pakietu na platformę docelową lub inne grupowania. Umożliwia również ujednolicać kontrolę nad zależnościami i przepływem zawartości. (Zobacz , aby uzyskać więcej szczegółów [na temat pakietu NuGet i przywracania jako obiektów docelowych MSBuild).](../reference/msbuild-targets.md)

## <a name="project-type-support"></a>Obsługa typów projektów

Domyślnie packageReference jest używany dla projektów platformy .NET Core, projektów platformy .NET Standard i projektów platformy UWP przeznaczonych dla programu Windows 10 Build 15063 (aktualizacja dla twórców) i nowszych, z wyjątkiem projektów platformy UWP w języku C++. .NET Framework obsługują packageReference, ale obecnie domyślnie są to `packages.config` . Aby użyć packageReference, [zmigruj](../consume-packages/migrate-packages-config-to-package-reference.md) zależności z do pliku projektu, a `packages.config` następnie usuń packages.config.

ASP.NET przeznaczone dla pełnego .NET Framework obejmują tylko [ograniczoną obsługę](https://github.com/NuGet/Home/issues/5877) packageReference. Typy projektów C++ i JavaScript nie są obsługiwane.

## <a name="adding-a-packagereference"></a>Dodawanie packageReference

Dodaj zależność w pliku projektu przy użyciu następującej składni:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Kontrolowanie wersji zależności

Konwencja określania wersji pakietu jest taka sama jak w przypadku korzystania z programu `packages.config` :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

W powyższym przykładzie wersja 3.6.0 oznacza dowolną wersję, która jest >=3.6.0 z preferencjami dla najniższej wersji, zgodnie z opisem w tece [Wersje pakietu](../concepts/package-versioning.md#version-ranges).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Używanie packageReference dla projektu bez packageReferences

Zaawansowane: jeśli w projekcie nie ma zainstalowanych pakietów (nie ma żadnych odczekań PackageReferences w pliku projektu ani pliku packages.config), ale chcesz, aby projekt został przywrócony jako styl PackageReference, możesz ustawić właściwość Project RestoreProjectStyle na PackageReference w pliku projektu.

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

Może to być przydatne, jeśli odwołujesz się do projektów w stylu PackageReference (istniejących projektów w stylu csproj lub SDK). Dzięki temu pakiety, do których odwołują się te projekty, będą "przechodnie", do których odwołuje się projekt.

## <a name="packagereference-and-sources"></a>PackageReference i źródła

W projektach PackageReference wersje zależności przechodniej są rozwiązywane podczas przywracania. W związku z tym w projektach PackageReference wszystkie źródła muszą być dostępne dla wszystkich przywracania. 

## <a name="floating-versions"></a>Wersje zmiennoprzecinkowe

[Wersje zmiennoprzecinkowe](../concepts/dependency-resolution.md#floating-versions) są obsługiwane za pomocą programu `PackageReference` :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Kontrolowanie zasobów zależności

Zależność może być wyłącznie usługą dewelopera i nie chcesz jej ujawniać w projektach, które będą korzystać z pakietu. W tym scenariuszu można kontrolować `PrivateAssets` to zachowanie za pomocą metadanych.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Następujące tagi metadanych kontrolują zasoby zależności:

| Tag | Description | Wartość domyślna |
| --- | --- | --- |
| IncludeAssets | Te zasoby zostaną zużyte | all |
| ExcludeAssets | Te zasoby nie będą używane | brak |
| PrivateAssets | Te zasoby zostaną zużyte, ale nie będą przepływać do projektu nadrzędnego | contentfiles;analyzers;build |

Dopuszczalne wartości dla tych tagów są następujące: wiele wartości rozdzielonych średnikami z wyjątkiem i , `all` które muszą być wyświetlane `none` samodzielnie:

| Wartość | Opis |
| --- | ---
| kompilowanie | Zawartość folderu `lib` i określa, czy projekt można skompilować względem zestawów w folderze |
| środowisko uruchomieniowe | Zawartość folderu i i określa, czy te zestawy zostaną skopiowane do `lib` `runtimes` katalogu wyjściowego kompilacji |
| contentFiles | Zawartość `contentfiles` folderu |
| kompilacja | `.props` i `.targets` w `build` folderze |
| buildMultitargeting | *(4.0)* i w folderze do określania `.props` `.targets` celu między `buildMultitargeting` platformami |
| buildTransitive | *(5.0+)* `.props` i `.targets` w `buildTransitive` folderze dla zasobów, które są przechodnie do dowolnego projektu zużywającego zasoby. Zobacz stronę [funkcji.](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) |
| Analizatory | Analizatory .NET |
| natywne | Zawartość `native` folderu |
| brak | Żadne z powyższych nie są używane. |
| all | Wszystkie powyższe (z wyjątkiem `none` ) |

W poniższym przykładzie wszystkie elementy oprócz plików zawartości z pakietu będą używane przez projekt, a wszystkie elementy oprócz plików zawartości i analizatorów będą przepływać do projektu nadrzędnego.

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

Należy pamiętać, że ponieważ element nie jest dołączony do elementu , obiekty docelowe i `build` `PrivateAssets` rekwizyty *będą* przepływać do projektu nadrzędnego. Rozważmy na przykład, że powyższe odwołanie jest używane w projekcie, który tworzy pakiet NuGet o nazwie AppLogger. Program AppLogger może korzystać z obiektów docelowych i obiektów prop z `Contoso.Utility.UsefulStuff` , podobnie jak projekty, które zużywają program AppLogger.

> [!NOTE]
> Jeśli w pliku jest ustawiona wartość , oznacza to pakiet jako zależność tylko do projektowania, co uniemożliwia uwzględnianie pakietu jako zależności w `developmentDependency` `true` innych `.nuspec` pakietach. W przypadku pakietu PackageReference *(NuGet 4.8+)* ta flaga oznacza również, że wyklucza z kompilacji zasoby czasu kompilacji. Aby uzyskać więcej informacji, zobacz [DevelopmentDependency support for PackageReference (Obsługa zależności dla packageReference).](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)

## <a name="adding-a-packagereference-condition"></a>Dodawanie warunku PackageReference

Można użyć warunku do kontrolowania, czy pakiet jest dołączony, gdzie warunki mogą używać dowolnej zmiennej MSBuild lub zmiennej zdefiniowanej w pliku obiektów docelowych lub props. Jednak obecnie obsługiwana jest `TargetFramework` tylko zmienna .

Załóżmy na przykład, że cel jest docelowy, ale ma zależność, która `netstandard1.4` ma zastosowanie tylko do `net452` . `net452` W takim przypadku nie chcesz, aby projekt, który zużywa `netstandard1.4` pakiet, dodać tę niepotrzebną zależność. Aby temu zapobiec, należy określić warunek w `PackageReference` następujący sposób:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Pakiet sbudowaną przy użyciu tego projektu pokaże, że Newtonsoft.Jsjest uwzględniony jako zależność tylko dla obiektu `net452` docelowego:

![Wynik zastosowania warunku w pakiecie PackageReference w programie VS2017](media/PackageReference-Condition.png)

Warunki można również stosować na `ItemGroup` poziomie i dotyczyć wszystkich elementów `PackageReference` kluczowych:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>GeneratePathProperty

Ta funkcja jest dostępna w pniu NuGet **5.0** lub jego wersji 5.0 lub jego wersji Visual Studio 2019 **16.0** lub jego wersji.

Czasami pożądane jest odwołanie do plików w pakiecie z obiektu docelowego MSBuild.
W `packages.config` projektach opartych pakiety są instalowane w folderze względem pliku projektu. Jednak w przypadku packageReference [](../concepts/package-installation-process.md) pakiety są używane z folderu *global-packages,* który może się różnić w zależności od komputera.

Aby wypełnić tę lukę, program NuGet wprowadził właściwość, która wskazuje lokalizację, z której zostanie zużyty pakiet.

Przykład:

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

Ponadto narzędzie NuGet automatycznie wygeneruje właściwości dla pakietów zawierających folder narzędzi.

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

Właściwości i tożsamości pakietów programu MSBuild nie mają tych samych ograniczeń, dlatego tożsamość pakietu musi zostać zmieniona na przyjazną nazwę msBuild poprzedzoną słowem `Pkg` .
Aby sprawdzić dokładną nazwę wygenerowanej właściwości, przyjrzyj się [wygenerowanemu plikowi nuget.g.props.](../reference/msbuild-targets.md#restore-outputs)

## <a name="packagereference-aliases"></a>PackageReference Aliases

W niektórych rzadkich przypadkach różne pakiety będą zawierać klasy w tej samej przestrzeni nazw. Począwszy od wersji NuGet 5.7 & Visual Studio 2019 Update 7, równoważnej wnioskowi ProjectReference, packageReference obsługuje funkcję [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases) .
Domyślnie aliasy nie są udostępniane. Jeśli określono alias, *wszystkie* zestawy pochodzące z pakietu z adnotacjami muszą być przywołyne przy użyciu aliasu.

Przykładowe użycie można sprawdzić w folderze [NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample)

W pliku projektu określ aliasy w następujący sposób:

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

W kodzie użyj go w następujący sposób:

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

## <a name="nuget-warnings-and-errors"></a>Ostrzeżenia i błędy nuGet

*Ta funkcja jest dostępna w pniu NuGet **4.3** lub jego wersji i Visual Studio 2017 **15.3** lub jego wersji.*

W przypadku wielu scenariuszy pakowania i przywracania wszystkie ostrzeżenia i błędy NuGet są kodowane i zaczynają się od `NU****` . Wszystkie ostrzeżenia i błędy programu NuGet są wymienione w [dokumentacji referencyjnej.](../reference/errors-and-warnings.md)

NuGet obserwuje następujące właściwości ostrzeżenia:

- `TreatWarningsAsErrors`, traktuj wszystkie ostrzeżenia jako błędy
- `WarningsAsErrors`, traktuj określone ostrzeżenia jako błędy
- `NoWarn`— ukrywa określone ostrzeżenia dla całego projektu lub całego pakietu.

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

### <a name="suppressing-nuget-warnings"></a>Pomijanie ostrzeżeń nuGet

Chociaż zaleca się rozwiązanie wszystkich ostrzeżeń NuGet podczas operacji pakowania i przywracania, w niektórych sytuacjach ich pomijanie jest uzasadnione.
Aby pominąć projekt ostrzeżenia w całym projekcie, rozważ wykonanie:

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

Czasami ostrzeżenia dotyczą tylko określonego pakietu w grafie. Możemy bardziej selektywnie pominąć to ostrzeżenie, dodając element `NoWarn` w pozycji PackageReference. 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Pomijanie ostrzeżeń pakietu NuGet w Visual Studio

W przypadku Visual Studio można również [pominąć ostrzeżenia za](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) pośrednictwem środowiska IDE.

## <a name="locking-dependencies"></a>Blokowanie zależności

*Ta funkcja jest dostępna w pniu NuGet **4.9** lub jego wersji i Visual Studio 2017 w wersji **15.9** lub powyższej.*

Dane wejściowe przywracania pakietów NuGet to zestaw odwołań do pakietów z pliku projektu (zależności najwyższego poziomu lub bezpośrednie), a dane wyjściowe są pełnym zamknięciem wszystkich zależności pakietu, w tym zależności przechodniej. Program NuGet próbuje zawsze utworzyć to samo pełne zamknięcie zależności pakietów, jeśli wejściowa lista PackageReference nie zmieniła się. Istnieją jednak pewne scenariusze, w których nie jest to możliwe. Na przykład:

* W przypadku używania wersji zmiennoprzecinowych, takich jak `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` . W tym przypadku celem jest przesłonięcia do najnowszej wersji przy każdym przywróceniu pakietów, jednak istnieją scenariusze, w których użytkownicy wymagają, aby graf był zablokowany dla określonej najnowszej wersji i zmiennoprzecinkowy do nowszej wersji, jeśli jest dostępny, przy jawnym gestie.
* Opublikowano nowszą wersję pakietu pasującą do wymagań dotyczących wersji packageReference. Na przykład 

  * Dzień 1: jeśli określono wersję, ale wersje dostępne w repozytoriach `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` NuGet to 4.1.0, 4.2.0 i 4.3.0. W tym przypadku rozwiązanie NuGet zostanie rozpoznane jako 4.1.0 (najbliższa minimalna wersja)

  * Dzień 2. Opublikowanie wersji 4.0.0. NuGet teraz znajdzie dokładne dopasowanie i rozpocznie rozpoznawanie do 4.0.0

* Danej wersji pakietu jest usuwana z repozytorium. Chociaż nuget.org nie zezwala na usunięcie pakietów, nie wszystkie repozytoria pakietów mają takie ograniczenia. Powoduje to znalezienie najlepszego dopasowania przez program NuGet, gdy nie można go rozpoznać do usuniętej wersji.

### <a name="enabling-lock-file"></a>Włączanie pliku blokady

Aby utrwalić pełne zamknięcie zależności pakietów, możesz wyrazić zgodę na funkcję pliku blokady, ustawiając właściwość MSBuild `RestorePackagesWithLockFile` dla projektu:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Jeśli ta właściwość jest ustawiona, przywracanie NuGet wygeneruje plik blokady — plik w katalogu głównym projektu, który zawiera listę `packages.lock.json` wszystkich zależności pakietów. 

> [!Note]
> Gdy plik projektu znajduje się w katalogu głównym, plik blokady jest zawsze używany z `packages.lock.json` przywracaniem, nawet jeśli właściwość nie jest `RestorePackagesWithLockFile` ustawiona. Innym sposobem, aby wyrazić zgodę na tę funkcję, jest utworzenie fikcyjnego pustego pliku w `packages.lock.json` katalogu głównym projektu.

### <a name="restore-behavior-with-lock-file"></a>`restore` zachowanie w przypadku pliku blokady
Jeśli w projekcie znajduje się plik blokady, program NuGet używa tego pliku blokady do uruchomienia pliku `restore` . Program NuGet szybko sprawdza, czy w zależnościach pakietu zostały wprowadzone jakieś zmiany, jak wspomniano w pliku projektu (lub w plikach projektów zależnych), a jeśli nie zostały wprowadzone żadne zmiany, przywraca tylko pakiety wymienione w pliku blokady. Nie ma możliwości ponownej oceny zależności pakietów.

Jeśli program NuGet wykryje zmianę zdefiniowanych zależności, jak wspomniano w plikach projektu, ponownie oceni wykres pakietu i aktualizuje plik blokady, aby odzwierciedlić nowe zamknięcie pakietu dla projektu.

W przypadku scenariuszy z ciasną/cd i innymi scenariuszami, w których nie chcesz zmieniać zależności pakietów na bieżąco, możesz to zrobić, ustawiając `lockedmode` na `true` :

Aby dotnet.exe, uruchom:

```
> dotnet.exe restore --locked-mode
```

Aby msbuild.exe, uruchom:

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Możesz również ustawić tę warunkową właściwość MSBuild w pliku projektu:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Jeśli tryb zablokowany to , przywracanie spowoduje przywrócenie dokładnych pakietów wymienionych w pliku blokady lub niepowodzenie w przypadku zaktualizowania zdefiniowanych zależności pakietu dla projektu po utworzeniu `true` pliku blokady.

### <a name="make-lock-file-part-of-your-source-repository"></a>Make lock file part of your source repository (Blokowanie pliku w repozytorium źródłowym)
Jeśli tworzyć aplikację, plik wykonywalny i projekt, których dotyczy ten projekt, znajdują się na początku łańcucha zależności, należy zaewidencjonić plik blokady w repozytorium kodu źródłowego, aby nuGet można było z niego korzystać podczas przywracania.

Jeśli jednak projekt jest projektem biblioteki, którego nie wysyłasz, lub wspólnym projektem  kodu, od którego zależą inne projekty, nie należy sprawdzać pliku blokady jako części kodu źródłowego. Przechowywanie pliku blokady nie ma żadnych szkód, ale zablokowane zależności pakietu dla wspólnego projektu kodu mogą nie być używane, jak podano w pliku blokady, podczas przywracania/kompilowania projektu, który zależy od tego wspólnego projektu kodu.

Na przykład:

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

Jeśli ma zależność od wersji, a także odwołania, które zależą od wersji , plik blokady dla pliku będzie `ProjectA` `PackageX` `2.0.0` `ProjectB` `PackageX` `1.0.0` `ProjectB` zawierał zależność od `PackageX` wersji `1.0.0` . Jednak podczas budowana wersja pliku blokady będzie zawierać zależność od wersji, a nie jak podano w `ProjectA` pliku blokady dla programu `PackageX` **`2.0.0`**  `1.0.0` `ProjectB` . W związku z tym plik blokady wspólnego projektu kodu ma niewiele informacji o pakietach rozpoznanych dla projektów, które od niego zależą.

### <a name="lock-file-extensibility"></a>Blokowanie rozszerzalności plików

Możesz kontrolować różne zachowania przywracania za pomocą pliku blokady, jak opisano poniżej:

| NuGet.exe opcji | dotnet option (opcja dotnet) | Równoważna opcja msBuild | Opis |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | Decyduje się na użycie pliku blokady. |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | Włącza tryb zablokowany dla przywracania. Jest to przydatne w scenariuszach z ciasną/cd, w których chcesz tworzyć powtarzalne kompilacje.|   
| `-ForceEvaluate` | `--force-evaluate` | RestoreForceEvaluate | Ta opcja jest przydatna w przypadku pakietów z wersją zmiennoprzecową zdefiniowaną w projekcie. Domyślnie przywracanie NuGet nie aktualizuje wersji pakietu automatycznie przy każdym przywróceniu, chyba że zostanie uruchomione przywracanie przy użyciu tej opcji. |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | Definiuje niestandardową lokalizację pliku blokady dla projektu. Domyślnie program NuGet obsługuje `packages.lock.json` program w katalogu głównym. Jeśli masz wiele projektów w tym samym katalogu, nuGet obsługuje plik blokady specyficzny dla projektu `packages.<project_name>.lock.json` |

## <a name="assettargetfallback"></a>AssetTargetFallback

Właściwość umożliwia określenie dodatkowych zgodnych wersji struktury dla projektów, do których odwołuje się projekt, i pakietów `AssetTargetFallback` NuGet, które są używane przez projekt.

Jeśli określisz zależność pakietu przy użyciu funkcji , ale ten pakiet nie zawiera zasobów, które są zgodne ze platformą docelową projektów, właściwość `PackageReference` zostanie w pełni `AssetTargetFallback` wyeksp czasowa. Zgodność przywoływanego pakietu jest ponownie sprawdzana przy użyciu każdej struktury docelowej określonej w pliku `AssetTargetFallback` .
W przypadku odwołania do lub za pośrednictwem , zostanie podniesione ostrzeżenie `project` `package` `AssetTargetFallback` [NU1701.](../reference/errors-and-warnings/NU1701.md)

Zapoznaj się z tabelą poniżej, aby zapoznać się z przykładami wpływu `AssetTargetFallback` na zgodność.

| Project framework | AssetTargetFallback | Struktury pakietów | Wynik |
|-------------------|---------------------|--------------------|--------|
|  .NET Framework 4.7.2 | | .NET Standard 2.0 | .NET Standard 2.0 |
| Aplikacja .NET Core 3.1 | | .NET Standard 2.0, .NET Framework 4.7.2 | .NET Standard 2.0 |
| Aplikacja .NET Core 3.1 | |  .NET Framework 4.7.2 | Niezgodne, niepowodzenie z [`NU1202`](../reference/errors-and-warnings/NU1202.md) |
| Aplikacja .NET Core 3.1 | net472;net471 |  .NET Framework 4.7.2 | .NET Framework 4.7.2 z [`NU1701`](../reference/errors-and-warnings/NU1701.md) |

Za pomocą ogranicznika można określić `;` wiele platform. Aby dodać platformę rezerwową, możesz wykonać następujące czynności:

```xml
<AssetTargetFallback Condition=" '$(TargetFramework)'=='netcoreapp3.1' ">
    $(AssetTargetFallback);net472;net471
</AssetTargetFallback>
```

Jeśli chcesz zastąpić wartość, możesz pozostawić ją bez dodawania `$(AssetTargetFallback)` do istniejących `AssetTargetFallback` wartości.

> [!NOTE]
> Jeśli używasz projektu opartego na zestawie SDK platformy [.NET,](/dotnet/core/sdk)skonfigurowane są odpowiednie wartości i nie trzeba `$(AssetTargetFallback)` ich ustawiać ręcznie.
>
> `$(PackageTargetFallback)` była wcześniejszą funkcją, która próbowała rozwiązać to wyzwanie, ale jest zasadniczo uszkodzona i *nie* powinna być używana. Aby przeprowadzić `$(PackageTargetFallback)` migrację `$(AssetTargetFallback)` z do , wystarczy zmienić nazwę właściwości.
