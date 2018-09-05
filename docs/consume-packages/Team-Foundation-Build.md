---
title: Wskazówki dotyczące przywracania pakietów NuGet z programem Team Foundation Build
description: Przewodnik dotyczący sposobu pakietu NuGet do przywracania za pomocą programu Team Foundation Build (TFS i Visual Studio Team Services).
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0e69491525fce03e504d9d455bee2718510c83c2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549888"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Konfigurowanie przywracania pakietów w programie Team Foundation Build

Ten artykuł zawiera szczegółowy przewodnik na temat sposobu przywracania pakietów w ramach [Team Services Build](/vsts/build-release/index) zarówno dla usług Git i kontroli wersji serwera Team Services.

Chociaż w tym instruktażu jest specyficzne dla scenariusza za pomocą programu Visual Studio Team Services, również dotyczyć innych kontroli wersji i tworzenie systemów.

Dotyczy:

- Niestandardowe projekty MSBuild, uruchamiane w dowolnej wersji programu TFS
- Team Foundation Server 2012 lub starszy
- Team Foundation tworzenia procesu szablonów niestandardowych migracji do programu TFS 2013 lub nowszym
- Szablony procesu kompilacji za pomocą funkcji Przywracanie pakietów Nuget

Jeśli używasz programu Visual Studio Team Services lub programu Team Foundation Server 2013 z jego szablony procesu kompilacji, jako część procesu kompilacji odbywa się Przywracanie pakietu automatyczne.

## <a name="the-general-approach"></a>Metody ogólne

Zaletą za pomocą narzędzia NuGet jest, że umożliwia ona Unikaj ewidencjonowania plików binarnych do systemu kontroli wersji.

Jest to szczególnie interesujące, jeśli używasz [rozproszonej kontroli wersji](http://en.wikipedia.org/wiki/Distributed_revision_control) systemu, takich jak git, ponieważ deweloperzy muszą sklonować całego repozytorium, łącznie z pełną historią, przed uruchomieniem trybu pracy — lokalnie. Ewidencjonowanie plików binarnych może spowodować przeładowanie znaczące repozytorium, jak pliki binarne są zazwyczaj przechowywane bez kompresji delta.

NuGet ma obsługiwane [Trwa przywracanie pakietów](../consume-packages/package-restore.md) jako część kompilacji długi czas teraz. Poprzedniej implementacji wystąpił problem kurczaka egg pakietów, które chcesz rozszerzyć proces kompilacji, ponieważ NuGet przywrócono pakiety podczas kompilowania projektu. Jednak program MSBuild nie zezwala na rozszerzanie kompilacji podczas kompilacji; jeden można dokumentu uważają że problemu w programie MSBuild, ale czy będzie dokumentu uważają, że jest to problem nieprzerwaną pracę. Zależności od tego, z którym aspektem należy rozszerzyć może być za późno do zarejestrowania przez razem, gdy pakiet zostanie przywrócony.

Utrwalenie tego problemu jest upewniając się, że pakiety zostaną przywrócone jako pierwszy krok w procesie kompilacji:

```cli
nuget restore path\to\solution.sln
```

Podczas procesu kompilacji, przywraca pakietów przed kompilacją kod, nie ma potrzeby ewidencjonowania `.targets` plików

> [!Note]
> Pakiety musi zostać utworzona, aby umożliwić ładowanie w programie Visual Studio. W przeciwnym razie może nadal chcesz zaewidencjonować `.targets` plików tak, aby inni deweloperzy mogą po prostu otwórz rozwiązanie, bez konieczności przywrócenia pakietów, najpierw.

Następujący projekt demonstracyjny pokazuje, jak Konfigurowanie kompilacji w taki sposób, który `packages` folderów i `.targets` pliki nie muszą zostać zaewidencjonowany. Pokazano również, jak skonfigurować kompilację automatyczną na Team Foundation Service dla tego przykładowego projektu.

## <a name="repository-structure"></a>Struktura repozytorium

Nasz projekt demonstracyjny to narzędzie wiersza polecenia proste, które używa argumentu wiersza polecenia do wykonywania zapytań w usłudze Bing. Jest przeznaczony dla .NET Framework 4 i używa wielu takich [pakietów BCL](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), i [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).

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

Widać, że firma Microsoft nie został zaewidencjonowany `packages` folder ani żaden `.targets` plików.

Firma Microsoft jednak zaewidencjonowania `nuget.exe` potrzeb podczas kompilacji. Zgodnie z powszechnie używane konwencje firma Microsoft została sprawdzona jej obszarze udostępnionego `tools` folderu.

Kod źródłowy znajduje się w obszarze `src` folderu. Mimo że naszą wersję demonstracyjną, używa tylko jednego rozwiązania, możesz sobie wyobrazić, że ten folder zawiera więcej niż jedno rozwiązanie.

### <a name="ignore-files"></a>Pliki ignorowanych

> [!Note]
> Ma obecnie [znaną usterką w kliencie programu NuGet](https://nuget.codeplex.com/workitem/4072) , powoduje, że klient nadal dodawać `packages` folderu do kontroli wersji. Obejście tego problemu jest wyłączyć integrację kontroli źródła. Aby to zrobić, należy `Nuget.Config ` w pliku `.nuget` folder, który jest zbliżony do rozwiązania. Ten folder nie istnieje, należy go utworzyć. W [ `Nuget.Config` ](../consume-packages/configuring-nuget-behavior.md), dodaj następującą zawartość:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

Do komunikacji z kontroli wersji, nie musimy zamiarem ewidencjonowania **pakietów** folderów, dodaliśmy także, ignorowania plików dla obu git (`.gitignore`) oraz kontrola wersji TF (`.tfignore`). Pliki te opisują wzorce plików, których nie chcesz, aby warunkowo.

`.gitignore` Pliku wygląda następująco:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

`.gitignore` Plik jest [bardzo wydajny](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Na przykład, jeśli chcesz ogólnie nie ewidencjonowania zawartość `packages` folder, ale ma pod ręką wcześniejszych wskazówkach sprawdzania `.targets` plików może mieć następujące reguły, zamiast tego:

    packages
    !packages/**/*.targets

To powoduje wyłączenie wszystkich `packages` folderów ale będzie ponownie obejmują wszystkie zawarte `.targets` plików. Przy okazji można znaleźć szablonu dla `.gitignore` pliki, które jest w szczególny sposób dopasowane do potrzeb deweloperów programu Visual Studio [tutaj](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

Kontrola wersji TF obsługuje bardzo podobny mechanizm, za pośrednictwem [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) pliku. Składnia jest praktycznie taki sam:

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a>Build.Proj

Nasz pokaz przechowujemy procesu kompilacji stosunkowo proste. Utworzymy projektu programu MSBuild, który tworzy wszystkie rozwiązania, pamiętając, że pakiety zostaną przywrócone przed kompilacją rozwiązania.

Ten projekt będzie mieć trzy elementy docelowe konwencjonalne `Clean`, `Build` i `Rebuild` oraz nowy obiekt docelowy `RestorePackages`.

- `Build` i `Rebuild` zależą od obiektów docelowych `RestorePackages`. Daje to pewność, że można jednocześnie uruchomić `Build` i `Rebuild` i zależą od pakietów przywracana.
- `Clean`, `Build` i `Rebuild` Wywołaj odpowiedni element docelowy programu MSBuild na wszystkie pliki rozwiązania.
- `RestorePackages` Miejsce docelowe wywołuje `nuget.exe` dla każdego pliku rozwiązania. Jest to realizowane przy użyciu [MSBuild na partie funkcji](/visualstudio/msbuild/msbuild-batching).

Wynik będzie wyglądać w następujący sposób:

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

## <a name="configuring-team-build"></a>Konfigurowanie Team Build

Kompilacja zespołowa oferuje różne szablony procesów. W tej prezentacji używamy programu Team Foundation Service. Instalacje środowiska lokalnego serwera TFS będzie odbywać się bardzo podobne.

Git i kontrola wersji TF mają różne szablony kompilacji zespołowej, dlatego poniższe kroki różnią się w zależności od tego, którego systemu kontroli wersji używasz. W obu przypadkach wystarczy to wybranie build.proj jako projekt, który chcesz skompilować.

Najpierw Przyjrzyjmy się z szablonem procesu dla usługi git. W szablonie usługi git, na podstawie kompilacji jest wybierany za pomocą właściwości `Solution to build`:

![Proces kompilacji dla systemu git](media/PackageRestoreTeamBuildGit.png)

Należy pamiętać, że ta właściwość ma miejsce w repozytorium. Ponieważ naszych `build.proj` jest w katalogu głównym, po prostu użyliśmy `build.proj`. Jeśli plik kompilacji jest umieścić w folderze o nazwie `tools`, wartość będzie wynosić `tools\build.proj`.

W szablonie Kontrola wersji TF projekt jest wybrany za pomocą właściwości `Projects`:

![Proces kompilacji w przypadku repozytorium TFVC](media/PackageRestoreTeamBuildTFVC.png)

W przeciwieństwie do usługi git, na podstawie szablonu TF Kontrola wersji obsługuje formanty wyboru (przycisk z wielokropkiem na stronie po prawej stronie). Tak, aby uniknąć błędów pisowni Sugerujemy za pomocą wybierz projekt.
