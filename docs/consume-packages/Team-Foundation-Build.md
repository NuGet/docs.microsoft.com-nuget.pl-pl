---
title: Przewodnik po przywracaniu pakietów NuGet za pomocą programu Team Foundation Build
description: Przewodnik dotyczący sposobu przywracania pakietu NuGet przy użyciu programu Team Foundation Build (zarówno TFS, jak i Visual Studio Team Services).
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a86a58f8afb4b0f1affeddd47d6c5606fb465757
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611002"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Konfigurowanie przywracania pakietu przy użyciu Team Foundation Build

Ten artykuł zawiera szczegółowy przewodnik dotyczący sposobu przywracania pakietów w ramach [kompilacji usługi Team Services](/vsts/build-release/index) zarówno dla kontroli wersji usług git, jak i Team Services.

Chociaż ten przewodnik jest specyficzny dla scenariusza używania Visual Studio Team Services, pojęcia dotyczą także innych systemów kontroli wersji i kompilacji.

Dotyczy:

- Niestandardowe projekty programu MSBuild działające w dowolnej wersji programu TFS
- Team Foundation Server 2012 lub starszy
- Niestandardowe szablony procesu programu Team Foundation Build migrowane do programu TFS 2013 lub nowszego
- Kompiluj szablony procesów z usuniętymi funkcjami przywracania NuGet

Jeśli używasz Visual Studio Team Services lub Team Foundation Server 2013 z szablonami procesu kompilacji, automatyczne przywracanie pakietów odbywa się w ramach procesu kompilacji.

## <a name="the-general-approach"></a>Ogólne podejście

Zaletą korzystania z programu NuGet jest możliwość użycia go w celu uniknięcia ewidencjonowania plików binarnych w systemie kontroli wersji.

Jest to szczególnie przydatne, jeśli używasz [rozproszonego systemu kontroli wersji](https://en.wikipedia.org/wiki/Distributed_revision_control) , takiego jak Git, ponieważ deweloperzy muszą sklonować całe repozytorium, w tym pełną historię, zanim będą mogli rozpocząć pracę lokalnie. Ewidencjonowanie plików binarnych może spowodować znaczące przeładowanie repozytorium, ponieważ pliki binarne są zwykle przechowywane bez kompresji różnicowej.

Pakiet NuGet obsługuje teraz [przywracanie pakietów](../consume-packages/package-restore.md) w ramach kompilacji przez długi czas. W poprzedniej implementacji wystąpił problem z kurczakami i jajami dla pakietów, które chcą zwiększyć proces kompilacji, ponieważ pakiety NuGet zostały przywrócone podczas kompilowania projektu. Jednak MSBuild nie zezwala na rozszerzanie kompilacji podczas kompilacji; może to spowodować, że ten problem wystąpił w programie MSBuild, ale może to być problem. W zależności od tego, który aspekt należy zwiększyć, może być zbyt późny do zarejestrowania przez czas przywrócenia pakietu.

Odjęcie tego problemu polega na tym, że pakiety są przywracane jako pierwszy krok w procesie kompilacji:

```cli
nuget restore path\to\solution.sln
```

Gdy proces kompilacji przywraca pakiety przed skompilowaniem kodu, nie musisz ewidencjonować plików `.targets`

> [!Note]
> Pakiety muszą zostać utworzone w celu umożliwienia ładowania w programie Visual Studio. W przeciwnym razie można nadal chcieć zaewidencjonować pliki `.targets` tak, aby inni deweloperzy mogli po prostu otworzyć rozwiązanie bez konieczności wcześniejszego przywrócenia pakietów.

W poniższym projekcie demonstracyjnym pokazano, jak skonfigurować kompilację w taki sposób, że `packages` foldery i pliki `.targets` nie muszą być zaewidencjonowane. Przedstawiono w nim również sposób konfigurowania zautomatyzowanej kompilacji na Team Foundation Service dla tego przykładowego projektu.

## <a name="repository-structure"></a>Struktura repozytorium

Nasze projekty demonstracyjne to proste narzędzie wiersza polecenia, które używa argumentu wiersza polecenia do wysyłania zapytań do usługi Bing. Jest ona przeznaczona dla .NET Framework 4 i używa wielu [pakietów BCL](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.NET. http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft. BCL](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft. BCL. Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)i [Microsoft. BCL. Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).

Struktura repozytorium wygląda następująco:

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

Można zobaczyć, że nie zaewidencjonowano — w folderze `packages` ani w żadnym pliku `.targets`.

Mamy jednak zaewidencjonować `nuget.exe`, co jest niezbędne podczas kompilacji. Zgodnie z powszechnie używanymi konwencjami została sprawdzona w folderze udostępnionym `tools`.

Kod źródłowy znajduje się w folderze `src`. Mimo że w tej wersji demonstracyjnej używane jest tylko jedno rozwiązanie, można w łatwy sposób przypuśćć, że ten folder zawiera więcej niż jedno rozwiązanie.

### <a name="ignore-files"></a>Pliki ignorowanych

> [!Note]
> [W kliencie NuGet jest obecnie znana usterka](https://nuget.codeplex.com/workitem/4072) , która powoduje, że klient nadal dodaje folder `packages` do kontroli wersji. Obejście polega na wyłączeniu integracji kontroli źródła. Aby to zrobić, potrzebny jest plik `Nuget.Config ` w folderze `.nuget`, który jest równoległy do Twojego rozwiązania. Jeśli ten folder jeszcze nie istnieje, należy go utworzyć. W [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md)Dodaj następującą zawartość:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

Aby komunikować się z kontrolą wersji, której nie chcemy zaewidencjonować folderów **pakietów** , dodaliśmy również ignorowanie plików zarówno dla narzędzia git (`.gitignore`) jak i kontroli wersji TF (`.tfignore`). Te pliki opisują wzorce plików, których nie chcesz zaewidencjonować.

Plik `.gitignore` wygląda następująco:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

Plik `.gitignore` jest [całkiem wydajny](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Na przykład jeśli chcesz zwykle nie zaewidencjonować zawartości folderu `packages`, ale chcesz przejść do poprzedniej wskazówki dotyczącej sprawdzania w plikach `.targets`, można użyć następującej reguły:

    packages
    !packages/**/*.targets

Spowoduje to wykluczenie wszystkich `packages` folderów, ale spowoduje ponowne uwzględnienie wszystkich zawartych `.targets` plików. W ten sposób można znaleźć szablon `.gitignore` plików, które są specjalnie dostosowane do [potrzeb deweloperów programu](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)Visual Studio.

System kontroli wersji TF obsługuje bardzo podobny mechanizm za pośrednictwem pliku [. tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) . Składnia jest praktycznie taka sama:

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>Kompilacja. proj

W naszej wersji demonstracyjnej proces kompilacji jest dość prosty. Utworzymy projekt MSBuild, który kompiluje wszystkie rozwiązania, a jednocześnie upewnia się, że pakiety są przywracane przed skompilowaniem rozwiązań.

Ten projekt będzie miał trzy `Clean`konwencjonalne elementy docelowe, `Build` i `Rebuild` oraz nowy `RestorePackages`docelowy.

- Elementy `Build` i `Rebuild` są zależne od `RestorePackages`. Gwarantuje to, że można uruchamiać `Build` i `Rebuild` i polegać na przywracaniu pakietów.
- `Clean`, `Build` i `Rebuild` wywołać odpowiednie obiekty docelowe programu MSBuild dla wszystkich plików rozwiązania.
- Obiekt docelowy `RestorePackages` wywołuje `nuget.exe` dla każdego pliku rozwiązania. Jest to realizowane przy użyciu [funkcji wsadowych programu MSBuild](/visualstudio/msbuild/msbuild-batching).

Wynik będzie wyglądać następująco:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a>Konfigurowanie kompilacji zespołu

Kompilacja zespołowa oferuje różne szablony procesów. Na potrzeby tej demonstracji używamy Team Foundation Service. Instalacje lokalne programu TFS będą bardzo podobne.

System kontroli wersji Git i TF ma inne szablony kompilacji zespołu, więc poniższe kroki będą się różnić w zależności od używanego systemu kontroli wersji. W obu przypadkach wystarczy wybrać kompilację Build. proj jako projekt, który chcesz skompilować.

Najpierw przyjrzyjmy się szablonowi procesu do usługi git. W szablonie opartym na git kompilacja jest wybierana za pośrednictwem właściwości `Solution to build`:

![Proces kompilacji dla narzędzia Git](media/PackageRestoreTeamBuildGit.png)

Należy pamiętać, że ta właściwość jest lokalizacją w repozytorium. Ponieważ nasze `build.proj` znajduje się w katalogu głównym, korzystamy z `build.proj`. Jeśli plik kompilacji zostanie umieszczony w folderze o nazwie `tools`, wartość zostanie `tools\build.proj`.

W szablonie kontroli wersji TF projekt jest wybierany za pośrednictwem właściwości `Projects`:

![Proces kompilacji dla TFVC](media/PackageRestoreTeamBuildTFVC.png)

W przeciwieństwie do szablonu opartego na usłudze git Kontrola wersji TF obsługuje selektory (przycisk po prawej stronie z trzema kropkami). Aby uniknąć błędów wpisywania, zalecamy użycie ich do wybrania projektu.
