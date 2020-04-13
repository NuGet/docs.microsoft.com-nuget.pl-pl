---
title: Format NuGet PackageReference (odwołania do pakietów w plikach projektu)
description: Szczegółowe informacje na temat wnioskowania pakietu NuGet w plikach projektu obsługiwanych przez nuget 4.0+ i VS2017 oraz .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428871"
---
# <a name="package-references-packagereference-in-project-files"></a>Odwołania do pakietów (PackageReference) w plikach projektu

Odwołania do pakietu, `PackageReference` za pomocą węzła, zarządzać zależnościami NuGet bezpośrednio `packages.config` w plikach projektu (w przeciwieństwie do oddzielnego pliku). Za pomocą PackageReference, jak to się nazywa, nie wpływa na inne aspekty NuGet; na przykład ustawienia `NuGet.config` w plikach (w tym źródła pakietów) są nadal stosowane, jak wyjaśniono w [typowych konfiguracjach NuGet](configuring-nuget-behavior.md).

Za pomocą PackageReference można również użyć MSBuild warunki, aby wybrać odwołania do pakietu na platformę docelową lub innych grup. Umożliwia również szczegółową kontrolę nad zależnościami i przepływem zawartości. (Zobacz więcej szczegółów [NuGet pack i restore jako obiekty docelowe MSBuild).)](../reference/msbuild-targets.md)

## <a name="project-type-support"></a>Obsługa typów projektów

Domyślnie PackageReference jest używany dla projektów .NET Core, .NET Standard i projektów platformy uniwersalnej systemu Windows przeznaczonych dla systemu Windows 10 Build 15063 (Creators Update) i nowszych, z wyjątkiem projektów platformy uniwersalnej systemu Windows++ platformy uniwersalnej systemu Windows. Projekty programu .NET Framework obsługują packagereference, ale obecnie domyślnie `packages.config`. Aby użyć PackageReference, należy przeprowadzić `packages.config` [migrację](../consume-packages/migrate-packages-config-to-package-reference.md) zależności z pliku projektu, a następnie usunąć plik packages.config.

ASP.NET aplikacje przeznaczone dla pełnego programu .NET Framework obejmują tylko [ograniczoną obsługę](https://github.com/NuGet/Home/issues/5877) packagereference. Typy projektów języka C++ i JavaScript nie są obsługiwane.

## <a name="adding-a-packagereference"></a>Dodawanie packagereference

Dodaj zależność w pliku projektu przy użyciu następującej składni:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Kontrolowanie wersji zależności

Konwencja określająca wersję pakietu jest taka sama, `packages.config`jak w przypadku korzystania z:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

W powyższym przykładzie 3.6.0 oznacza dowolną wersję, która jest >= 3.6.0 z preferencją dla najniższej wersji, zgodnie z opisem w [wersji pakietu](../concepts/package-versioning.md#version-ranges).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Korzystanie z packagereference dla projektu bez packagereferences

Zaawansowane: Jeśli nie masz żadnych pakietów zainstalowanych w projekcie (nie PackageReferences w pliku projektu i bez pliku packages.config), ale chcesz, aby projekt został przywrócony jako styl PackageReference, można ustawić właściwość projektu RestoreProjectStyle do PackageReference w pliku projektu.

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

Może to być przydatne, jeśli odwołujesz się do projektów, które są PackageReference stylu (istniejące csproj lub SDK stylu projektów). Umożliwi to pakiety, które te projekty odnoszą się do, aby być "przechodnie" odwołuje się do projektu.

## <a name="packagereference-and-sources"></a>PackageReference i źródła

W projektach PackageReference przechodnie wersje zależności są rozpoznawane w czasie przywracania. W związku z tym w PackageReference projektów wszystkie źródła muszą być dostępne dla wszystkich przywraca. 

## <a name="floating-versions"></a>Wersje pływające

[Wersje przestawne](../concepts/dependency-resolution.md#floating-versions) `PackageReference`są obsługiwane z:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Kontrolowanie zasobów zależności

Może być przy użyciu zależności wyłącznie jako uprzęży rozwoju i nie może chcieć udostępnić, że do projektów, które będą korzystać z pakietu. W tym scenariuszu `PrivateAssets` można użyć metadanych do kontrolowania tego zachowania.

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

| Tag | Opis | Wartość domyślna |
| --- | --- | --- |
| Zestawy dołączane | Aktywa te zostaną zużyte | all |
| WykluczAzestawy | Aktywa te nie będą zużywane | brak |
| Zestawy prywatne | Te zasoby zostaną zużyte, ale nie będą przepływać do projektu nadrzędnego | contentfiles;analizatory;kompilacja |

Dopuszczalne wartości dla tych znaczników są następujące, z wieloma wartościami `all` `none` oddzielonymi średnikiem, z wyjątkiem i które muszą być wyświetlane same w sobie:

| Wartość | Opis |
| --- | ---
| kompilowanie | Zawartość folderu `lib` i określa, czy projekt może kompilować względem zestawów w folderze |
| środowisko uruchomieniowe | Zawartość `lib` folderu `runtimes` i i określa, czy te zestawy zostaną skopiowane do katalogu wyjściowego kompilacji |
| contentFiles | Zawartość folderu `contentfiles` |
| kompilacja | `.props`i `.targets` w `build` folderze |
| buildMultitargeting | *(4.0)* `.props` `.targets` oraz `buildMultitargeting` w folderze, w celu ukierunkowania na |
| buildTransitive | *(5.0+)* `.props` `.targets` i `buildTransitive` w folderze, dla zasobów, które przepływają przechodnie do dowolnego projektu zużywającego. Zobacz stronę [funkcji.](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) |
| Analizatory | Analizatory .NET |
| natywne | Zawartość folderu `native` |
| brak | Żadne z powyższych są używane. |
| all | Wszystkie powyższe (z wyjątkiem) `none` |

W poniższym przykładzie wszystko oprócz plików zawartości z pakietu będzie używane przez projekt i wszystko z wyjątkiem plików zawartości i analizatorów będzie przepływać do projektu nadrzędnego.

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

Należy zauważyć, że `build` ponieważ `PrivateAssets`nie jest dołączony do , cele i rekwizyty *będą* przepływać do projektu nadrzędnego. Należy wziąć pod uwagę, na przykład, że powyższe odwołanie jest używane w projekcie, który tworzy pakiet NuGet o nazwie AppLogger. AppLogger może korzystać z `Contoso.Utility.UsefulStuff`obiektów docelowych i rekwizytów z , podobnie jak projekty, które korzystają z AppLogger.

> [!NOTE]
> Gdy `developmentDependency` jest `true` ustawiona `.nuspec` w pliku, oznacza to pakiet jako zależność tylko dla deweloperów, co uniemożliwia pakiet zostanie uwzględniony jako zależność w innych pakietach. Z PackageReference *(NuGet 4.8+)* ta flaga oznacza również, że będzie wykluczać zasoby kompilacji z kompilacji. Aby uzyskać więcej informacji, zobacz [RozwójZależność obsługi packagereference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).

## <a name="adding-a-packagereference-condition"></a>Dodawanie warunku PackageReference

Warunek służy do kontrolowania, czy pakiet jest dołączony, gdzie warunki można użyć dowolnej zmiennej MSBuild lub zmiennej zdefiniowanej w pliku obiektów docelowych lub props. Jednak obecnie tylko zmienna `TargetFramework` jest obsługiwana.

Załóżmy na przykład, `netstandard1.4` że kierujesz reklamy, a także `net452` `net452`masz zależność, która ma zastosowanie tylko do . W takim przypadku nie `netstandard1.4` chcesz, aby projekt, który zużywa pakiet, aby dodać tę niepotrzebną zależność. Aby temu zapobiec, należy określić warunek w następujący sposób: `PackageReference`

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Pakiet zbudowany przy użyciu tego projektu pokaże, że Newtonsoft.Json jest `net452` uwzględniony jako zależność tylko dla obiektu docelowego:

![Wynik zastosowania warunku na PackageReference z VS2017](media/PackageReference-Condition.png)

Warunki mogą być również `ItemGroup` stosowane na poziomie i `PackageReference` będą miały zastosowanie do wszystkich elementów dla dzieci:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>GeneratePathProperty

Ta funkcja jest dostępna w wersji NuGet **5.0** lub wyższej oraz w programie Visual Studio 2019 **16.0** lub wyższym.

Czasami pożądane jest odwoływanie się do plików w pakiecie z obiektu docelowego MSBuild.
W `packages.config` projektach opartych pakiety są instalowane w folderze względem pliku projektu. Jednak w PackageReference pakiety są [używane](../concepts/package-installation-process.md) z globalnego folderu *pakietów,* które mogą się różnić od komputera do komputera.

Aby wypełnić tę lukę, NuGet wprowadził właściwość, która wskazuje lokalizację, z której pakiet zostanie wykorzystany.

Przykład:

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

Ponadto NuGet automatycznie wygeneruje właściwości dla pakietów zawierających folder narzędzi.

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

Właściwości MSBuild i tożsamości pakietów nie mają tych samych ograniczeń, więc tożsamość pakietu musi zostać zmieniona `Pkg`na przyjazną nazwę MSBuild, poprzedzony wyrazem .
Aby sprawdzić dokładną nazwę wygenerowanej właściwości, przyjrzyj się wygenerowanemu plikowi [nuget.g.props.](../reference/msbuild-targets.md#restore-outputs)

## <a name="nuget-warnings-and-errors"></a>Ostrzeżenia i błędy NuGet

*Ta funkcja jest dostępna w wersji NuGet **4.3** lub wyższej oraz w programie Visual Studio 2017 **15.3** lub wyższym.*

W przypadku wielu scenariuszy pakowania i przywracania wszystkie ostrzeżenia i `NU****`błędy NuGet są kodowane i zaczynają się od . Wszystkie ostrzeżenia i błędy NuGet są wymienione w dokumentacji [referencyjnej.](../reference/errors-and-warnings.md)

NuGet przestrzega następujących właściwości ostrzeżenia:

- `TreatWarningsAsErrors`, potraktuj wszystkie ostrzeżenia jako błędy
- `WarningsAsErrors`, traktować określone ostrzeżenia jako błędy
- `NoWarn`, ukryj określone ostrzeżenia, obejmujące cały projekt lub pakiet.

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

Chociaż zaleca się, aby rozwiązać wszystkie ostrzeżenia NuGet podczas pakietu i przywrócić operacje, w niektórych sytuacjach pomijając je jest uzasadnione.
Aby pominąć projekt ostrzegawczy w szerokim zakresie, należy rozważyć wykonanie:

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

Czasami ostrzeżenia dotyczą tylko określonego pakietu na wykresie. Możemy wybrać, aby pominąć to ostrzeżenie `NoWarn` bardziej selektywnie, dodając na PackageReference elementu. 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Pomijanie ostrzeżeń pakietu NuGet w programie Visual Studio

W programie Visual Studio można również [pominąć ostrzeżenia](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) za pośrednictwem IDE.

## <a name="locking-dependencies"></a>Blokowanie zależności

*Ta funkcja jest dostępna w wersji NuGet **4.9** lub wyższej oraz w programie Visual Studio 2017 **15.9** lub wyższym.*

Dane wejściowe do nuget restore to zestaw odwołań do pakietu z pliku projektu (zależności najwyższego poziomu lub bezpośrednie), a dane wyjściowe są pełnym zamknięciem wszystkich zależności pakietu, w tym zależności przechodnich. NuGet próbuje zawsze produkować takie same pełne zamknięcie zależności pakietu, jeśli lista danych wejściowych PackageReference nie uległa zmianie. Istnieją jednak pewne scenariusze, w których nie jest w stanie tego zrobić. Przykład:

* W przypadku korzystania `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`z wersji przestawnych, takich jak . Podczas gdy intencją w tym miejscu jest float do najnowszej wersji na każdym przywracaniu pakietów, istnieją scenariusze, w których użytkownicy wymagają wykresu, aby zablokować do określonej najnowszej wersji i float do nowszej wersji, jeśli są dostępne, na jawny gest.
* Opublikowano nowszą wersję pakietu pasującego wymagania dotyczące wersji PackageReference. Na przykład 

  * Dzień 1: jeśli `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` określono, ale wersje dostępne w repozytoriach NuGet były 4.1.0, 4.2.0 i 4.3.0. W takim przypadku NuGet rozpoznałby do 4.1.0 (najbliższa minimalna wersja)

  * Dzień 2: Wersja 4.0.0 zostanie opublikowana. NuGet znajdzie teraz dokładne dopasowanie i rozpocznie rozwiązywanie do 4.0.0

* Dana wersja pakietu jest usuwana z repozytorium. Chociaż nuget.org nie zezwala na usuwanie pakietów, nie wszystkie repozytoria pakietów mają te ograniczenia. Powoduje to, że NuGet znalezienie najlepszego dopasowania, gdy nie można rozwiązać do usuniętej wersji.

### <a name="enabling-lock-file"></a>Włączanie pliku blokady

Aby utrwalić pełne zamknięcie zależności pakietu można wyrazić zgodę na funkcję pliku `RestorePackagesWithLockFile` blokady, ustawiając właściwość MSBuild dla projektu:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Jeśli ta właściwość jest ustawiona, NuGet `packages.lock.json` restore wygeneruje plik blokady - plik w katalogu głównym projektu, który zawiera listę wszystkich zależności pakietu. 

> [!Note]
> Gdy projekt `packages.lock.json` ma plik w katalogu głównym, plik blokady jest zawsze `RestorePackagesWithLockFile` używany z przywracania, nawet jeśli właściwość nie jest ustawiona. Innym sposobem wyrażenia zgody na tę funkcję jest utworzenie `packages.lock.json` fikcyjnego pustego pliku w katalogu głównym projektu.

### <a name="restore-behavior-with-lock-file"></a>`restore`zachowanie z plikiem blokady
Jeśli plik blokady jest obecny dla projektu, NuGet `restore`używa tego pliku blokady do uruchomienia . NuGet wykonuje szybkie sprawdzanie, czy były jakieś zmiany w zależności pakietu, jak wspomniano w pliku projektu (lub plików projektów zależnych) i jeśli nie było żadnych zmian po prostu przywraca pakiety wymienione w pliku blokady. Nie ma ponownej oceny zależności pakietu.

Jeśli NuGet wykryje zmianę w zdefiniowanych zależności, jak wspomniano w pliku projektu(-ów), ponownie ocenia wykres pakietu i aktualizuje plik blokady, aby odzwierciedlić nowe zamknięcie pakietu dla projektu.

W przypadku ciągłej integracji/ciągłego wdrażania i innych scenariuszy, w których nie chcesz `lockedmode` zmieniać `true`zależności pakietów na bieżąco, można to zrobić, ustawiając na:

W przypadku pliku dotnet.exe uruchom:

```
> dotnet.exe restore --locked-mode
```

Dla msbuild.exe, uruchom:

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Można również ustawić tę warunkową właściwość MSBuild w pliku projektu:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Jeśli tryb zablokowany `true`jest , przywracanie przywróci dokładne pakiety wymienione w pliku blokady lub zakończy się niepowodzeniem, jeśli zaktualizowano zdefiniowane zależności pakietów dla projektu po utworzeniu pliku blokady.

### <a name="make-lock-file-part-of-your-source-repository"></a>Przeksztą do repozytorium źródłowego pliku blokady
Jeśli budujesz aplikację, plik wykonywalny i projekt, o którym mowa jest na początku łańcucha zależności, a następnie zaewidencjonuj plik blokady do repozytorium kodu źródłowego, dzięki czemu NuGet może z niego korzystać podczas przywracania.

Jednak jeśli projekt jest projekt biblioteki, które nie są dostarczane lub wspólny projekt kodu, od którego zależą inne projekty, **nie należy** zaewidencjonować pliku blokady jako część kodu źródłowego. Nie ma żadnych szkód w zachowaniu pliku blokady, ale zablokowane zależności pakietu dla wspólnego projektu kodu nie mogą być używane, jak wymieniono w pliku blokady, podczas przywracania/kompilacji projektu, który zależy od tego projektu wspólnego kodu.

Na przykład:

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

Jeśli `ProjectA` ma zależność `PackageX` od `2.0.0` wersji, `ProjectB` a także `PackageX` `1.0.0`odwołuje się do `ProjectB` wersji, a następnie `PackageX` `1.0.0`plik blokady dla wyświetli zależność od wersji . Jednak po `ProjectA` zbudowaniu jego plik blokady `PackageX` będzie **`2.0.0`** zawierał zależność od wersji, a **nie** `1.0.0` wymienioną w pliku blokady dla `ProjectB`. W związku z tym plik blokady wspólnego projektu kodu ma niewiele do powiedzenia na temat pakietów rozwiązanych dla projektów, które zależą od niego.

### <a name="lock-file-extensibility"></a>Rozszerzalność pliku blokady

Można kontrolować różne zachowania przywracania za pomocą pliku blokady, jak opisano poniżej:

| NuGet.exe, opcja | dotnet, opcja | Opcja równoważna MSBuild | Opis |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | Decyduje się na użycie pliku blokady. |
| `-LockedMode` | `--locked-mode` | Tryb RestoreLockedMode | Włącza tryb zablokowany do przywracania. Jest to przydatne w scenariuszach ciągłej integracji/ciągłego wdrażania, w których mają być powtarzalne kompilacje.|   
| `-ForceEvaluate` | `--force-evaluate` | Wartość RestoreForceE | Ta opcja jest przydatna w przypadku pakietów z wersją przestawną zdefiniowaną w projekcie. Domyślnie przywracanie NuGet nie zaktualizuje wersji pakietu automatycznie przy każdym przywracanie, chyba że uruchomisz przywracanie za pomocą tej opcji. |
| `-LockFilePath` | `--lock-file-path` | Ścieżka pliku NuGetLock | Definiuje niestandardową lokalizację pliku blokady dla projektu. Domyślnie NuGet `packages.lock.json` obsługuje w katalogu głównym. Jeśli masz wiele projektów w tym samym katalogu, NuGet obsługuje plik blokady specyficzne dla projektu`packages.<project_name>.lock.json` |
