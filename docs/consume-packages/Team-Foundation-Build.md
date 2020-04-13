---
title: Przewodnik po przywróceniu pakietu NuGet z kompilacją Team Foundation
description: Przewodnik jak NuGet przywracanie pakietu z Team Foundation Build (zarówno TFS i Visual Studio Team Services).
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a86a58f8afb4b0f1affeddd47d6c5606fb465757
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "73611002"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Konfigurowanie przywracania pakietu za pomocą team foundation build

Ten artykuł zawiera szczegółowe wskazówki dotyczące przywracania pakietów w ramach [team services kompilacji](/vsts/build-release/index) zarówno dla Git i Team Services kontroli wersji.

Chociaż ten instruktaż jest specyficzny dla scenariusza korzystania z programu Visual Studio Team Services, pojęcia dotyczą również innych systemów kontroli wersji i kompilacji.

Dotyczy:

- Niestandardowe projekty MSBuild uruchomione w dowolnej wersji usługi TFS
- Team Foundation Server 2012 lub wcześniejszy
- Szablony procesów kompilacji niestandardowych fundacji zespołu zmigrowane do usługi TFS 2013 lub nowszej
- Tworzenie szablonów procesów z usuniętą funkcją przywracania nuget

Jeśli używasz programu Visual Studio Team Services lub Team Foundation Server 2013 z jego szablonów procesu kompilacji, automatyczne przywracanie pakietu odbywa się w ramach procesu kompilacji.

## <a name="the-general-approach"></a>Ogólne podejście

Zaletą korzystania z NuGet jest to, że można go używać, aby uniknąć sprawdzania w plikach binarnych do systemu kontroli wersji.

Jest to szczególnie interesujące, jeśli używasz rozproszonego systemu [kontroli wersji,](https://en.wikipedia.org/wiki/Distributed_revision_control) takiego jak git, ponieważ deweloperzy muszą sklonować całe repozytorium, w tym pełną historię, zanim będą mogli rozpocząć pracę lokalnie. Zaewidencjonowanie w plikach binarnych może spowodować znaczne nadęcie repozytorium, ponieważ pliki binarne są zazwyczaj przechowywane bez kompresji różnicowej.

NuGet obsługuje [przywracanie pakietów](../consume-packages/package-restore.md) jako część kompilacji przez długi czas. Poprzednia implementacja miała problem z kurczakiem i jajem dla pakietów, które chcesz rozszerzyć proces kompilacji, ponieważ NuGet przywrócono pakiety podczas tworzenia projektu. Jednak MSBuild nie zezwala na rozszerzanie kompilacji podczas kompilacji; można argumentować, że jest to problem w MSBuild, ale chciałbym twierdzić, że jest to nieodłączny problem. W zależności od tego, który aspekt należy rozszerzyć może być za późno, aby zarejestrować się do czasu, gdy pakiet zostanie przywrócony.

Lekarstwem na ten problem jest upewnienie się, że pakiety są przywracane jako pierwszy krok w procesie kompilacji:

```cli
nuget restore path\to\solution.sln
```

Gdy proces kompilacji przywraca pakiety przed utworzeniem kodu, nie `.targets` trzeba zaewidencjonować plików

> [!Note]
> Pakiety muszą być autorstwa, aby umożliwić ładowanie w programie Visual Studio. W przeciwnym razie nadal można `.targets` zaewidencjonować pliki, aby inni deweloperzy mogli po prostu otworzyć rozwiązanie bez konieczności przywracania pakietów.

Poniższy projekt demonstracyjny pokazuje, jak skonfigurować `packages` kompilację `.targets` w taki sposób, aby foldery i pliki nie musiały być zaewidencjonowane. Pokazuje również, jak skonfigurować zautomatyzowaną kompilację w usłudze Team Foundation dla tego przykładowego projektu.

## <a name="repository-structure"></a>Struktura repozytorium

Nasz projekt demonstracyjny to proste narzędzie wiersza polecenia, które używa argumentu wiersza polecenia do wykonywania zapytań bing. Jest przeznaczony dla programu .NET Framework 4 i używa wielu [pakietów BCL](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)i [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).

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

Widać, że nie sprawdziliśmy `packages` ani żadnych `.targets` plików.

Mamy jednak sprawdzone w `nuget.exe` jak to jest potrzebne podczas kompilacji. Zgodnie z powszechnie używanymi konwencjami zaewidencjonowaliśmy go w folderze udostępnionym. `tools`

Kod źródłowy znajduje `src` się w folderze. Chociaż nasze demo używa tylko jednego rozwiązania, można łatwo sobie wyobrazić, że ten folder zawiera więcej niż jedno rozwiązanie.

### <a name="ignore-files"></a>Pliki ignorowanych

> [!Note]
> Obecnie istnieje [znany błąd w kliencie NuGet,](https://nuget.codeplex.com/workitem/4072) który powoduje, że klient nadal dodać `packages` folder do kontroli wersji. Obejście jest wyłączenie integracji kontroli źródła. Aby to zrobić, potrzebujesz `Nuget.Config ` pliku w `.nuget` folderze, który jest równoległy do rozwiązania. Jeśli ten folder jeszcze nie istnieje, należy go utworzyć. W [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md)obszarze dodaj następującą zawartość:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

Aby przekazać do kontroli wersji, że nie zamierzamy zaewidencjonować **foldery pakietów,** `.gitignore`dodaliśmy również ignoruj`.tfignore`pliki zarówno dla git ( ), jak również kontroli wersji TF ( ). Pliki te opisują wzorce plików, których nie chcesz zaewidencjonować.

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

Plik `.gitignore` jest [dość potężny](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Na przykład, jeśli zazwyczaj nie chcesz zaewidencjonować zawartości `packages` folderu, ale chcesz `.targets` przejść z poprzednimi wskazówkami dotyczącymi zaewidencjonowania plików, możesz mieć następującą regułę:

    packages
    !packages/**/*.targets

Spowoduje to `packages` wykluczenie wszystkich folderów, ale `.targets` spowoduje ponowne uwzględnić wszystkie zawarte pliki. Nawiasem mówiąc, można znaleźć `.gitignore` szablon dla plików, który jest specjalnie dostosowany do potrzeb deweloperów programu Visual Studio [tutaj](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

Kontrola wersji TF obsługuje bardzo podobny mechanizm za pośrednictwem pliku [.tfignore.](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) Składnia jest praktycznie taka sama:

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>build.proj

W przypadku naszego demo proces budowania jest dość prosty. Utworzymy projekt MSBuild, który tworzy wszystkie rozwiązania, upewniając się, że pakiety zostaną przywrócone przed utworzeniem rozwiązań.

Projekt ten będzie miał `Clean`trzy `Build` `Rebuild` konwencjonalne cele, `RestorePackages`a także nowy cel.

- Zarówno `Build` `Rebuild` i cele `RestorePackages`zależą od . Dzięki temu można zarówno `Build` uruchomić `Rebuild` i polegać na pakiety są przywracane.
- `Clean`i `Build` `Rebuild` wywołać odpowiedni obiekt docelowy MSBuild we wszystkich plikach rozwiązań.
- Obiekt `RestorePackages` docelowy `nuget.exe` wywołuje dla każdego pliku rozwiązania. Jest to realizowane przy użyciu [funkcji wsadowego MSBuild.](/visualstudio/msbuild/msbuild-batching)

Wynik wygląda następująco:

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

Team Build oferuje różne szablony procesów. W tej demonstracji używamy usługi Team Foundation Service. Instalacje lokalne TFS będą jednak bardzo podobne.

Git i TF Version Control mają różne szablony team build, więc następujące kroki będą się różnić w zależności od używanego systemu kontroli wersji. W obu przypadkach wszystko, czego potrzebujesz, to wybranie build.proj jako projektu, który chcesz utworzyć.

Najpierw przyjrzyjmy się szablonowi procesu dla git. W szablonie opartym na git `Solution to build`kompilacja jest wybierana za pośrednictwem właściwości:

![Proces budowania dla git](media/PackageRestoreTeamBuildGit.png)

Obiekt znajduje się w repozytorium. Ponieważ `build.proj` nasz jest w korzeniu, po prostu użyliśmy `build.proj`. Jeśli umieścisz plik kompilacji `tools`w folderze `tools\build.proj`o nazwie , wartość będzie .

W szablonie kontroli wersji TF projekt `Projects`jest wybierany za pośrednictwem właściwości:

![Proces budowania dla TFVC](media/PackageRestoreTeamBuildTFVC.png)

W przeciwieństwie do szablonu opartego na git, kontrola wersji TF obsługuje selektory (przycisk po prawej stronie z trzema kropkami). Tak więc, aby uniknąć błędów pisania, zalecamy użycie ich do wybrania projektu.
