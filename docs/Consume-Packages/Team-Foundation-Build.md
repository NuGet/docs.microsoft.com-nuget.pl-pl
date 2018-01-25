---
title: "Wskazówki pakietu NuGet Przywracanie z Team Foundation Build | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Przewodnik jak przywracanie z z Team Foundation Build (TFS i Visual Studio Team Services) pakietów NuGet."
keywords: "Przywracanie pakietu NuGet, NuGet i TFS, NuGet i programu VSTS systemów kompilacji NuGet, team foundation build, niestandardowych projektów MSBuild, tworzenia chmury, ciągłej integracji"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a90b4bb9bd3a5b9200179ab16f16b276abcda981
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a>Konfigurowanie Przywracanie pakietu z Team Foundation Build

Ten artykuł zawiera szczegółowy przewodnik na temat pod kątem przywracania pakietów w ramach [Team Services Build](/vsts/build-release/index) zarówno dla Git i kontroli wersji programu Team Services.

Chociaż ten przewodnik jest specyficzna dla scenariusza za pomocą programu Visual Studio Team Services, również zastosować do innych kontroli wersji i kompilacji systemu.

Dotyczy:

- W dowolnej wersji programu TFS niestandardowych projektów MSBuild
- Team Foundation Server 2012 lub starszy
- Team Foundation kompilacji procesu szablonów niestandardowych migracji do programu TFS 2013 lub nowszej
- Szablony procesu kompilacji z zestawem funkcji Przywracanie Nuget

Jeśli używasz programu Visual Studio Team Services lub Team Foundation Server 2013 z jego szablony procesu kompilacji, odbywa się Przywracanie pakietu automatycznych jako część procesu kompilacji.

## <a name="the-general-approach"></a>Metody ogólne

Zaletą przy użyciu narzędzia NuGet to, że można go uniknąć sprawdzanie w danych binarnych systemu kontroli wersji.

Jest to szczególnie interesujące, jeśli używasz [rozproszonych kontroli wersji](http://en.wikipedia.org/wiki/Distributed_revision_control) systemu, takich jak git ponieważ deweloperzy muszą Klonuj repozytorium całego, łącznie z pełną historię przed uruchomieniem pracując lokalnie. Sprawdzanie w danych binarnych może spowodować znaczne repozytorium rozrostu jako pliki binarne są zwykle przechowywane bez zmian kompresji.

Obsługiwał NuGet [Przywracanie pakietów](../consume-packages/package-restore.md) jako część kompilacji długi czas teraz. Poprzedniej implementacji wystąpił problem kurczaka jajecznych pakietów, które chcesz rozszerzyć proces kompilacji, ponieważ NuGet przywrócić pakiety podczas kompilowania projektu. Jednak program MSBuild nie zezwala na rozszerzanie kompilacji podczas kompilacji; co można argumentowało tego problemu w programie MSBuild, ale I argumentowało, że jest to problemu związanego z używaniem. W zależności od tego, które aspekt należy rozszerzyć może być za późno można zarejestrować do czasu, który zostanie przywrócony do pakietu.

Utrwalenie tego problemu jest upewnienie się, że pakiety zostaną przywrócone jako pierwszy krok w procesie kompilacji. NuGet 2.7 + ułatwia to uproszczona wiersza polecenia:

```cli
nuget restore path\to\solution.sln
```

Podczas procesu kompilacji przywraca pakiety przed zbudowaniem kod, nie trzeba zaewidencjonowania `.targets` plików

> [!Note]
> Pakiety musi tworzyć umożliwia ładowanie w programie Visual Studio. W przeciwnym razie może nadal chcesz zaewidencjonować `.targets` pliki, aby inni deweloperzy mogą po prostu otwórz rozwiązanie, bez konieczności przywrócenia pakietów najpierw.

Następujący projekt pokaz pokazano, jak skonfigurować kompilacji w taki sposób, który `packages` folderów i `.targets` pliki nie muszą mieć zaewidencjonowania. On również pokazano, jak skonfigurować automatyczne kompilacji w usłudze Team Foundation dla tego projektu próbki.

## <a name="repository-structure"></a>Struktura repozytorium

Nasze projektu pokaz to narzędzie proste wiersza polecenia, które używa argumentu wiersza polecenia do zapytania usługi Bing. Dotyczy programu .NET Framework 4 i używa wielu [pakiety BCL](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), i [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).

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

Widać, że firma Microsoft nie zaewidencjonowania `packages` folderu lub any `.targets` plików.

Firma Microsoft jednak zaewidencjonowania `nuget.exe` jest wymagana podczas kompilacji. Następujące powszechnie używane konwencje możemy został zaewidencjonowany w udostępnionej `tools` folderu.

Kod źródłowy jest w obszarze `src` folderu. Mimo że nasze pokaz używa tylko pojedyncze rozwiązanie, należy sobie wyobrazić, że ten folder zawiera więcej niż jedno rozwiązanie.

### <a name="ignore-files"></a>Pliki ignorowanych

> [!Note]
> Obecnie [znaną usterką w kliencie programu NuGet](https://nuget.codeplex.com/workitem/4072) który powoduje, że klient nadal dodawać `packages` folder z kontrolą wersji. Obejście tego problemu jest wyłączenie integracji kontroli źródła. Aby to zrobić, musisz `Nuget.Config ` w pliku `.nuget` folderu, który jest zbliżony do rozwiązania. Ten folder nie istnieje, należy go utworzyć. W [ `Nuget.Config` ](../consume-packages/configuring-nuget-behavior.md), dodaj następującą zawartość:

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

Do komunikowania się do systemu kontroli wersji, że firma Microsoft nie opcje do wyboru w **pakiety** folderów, również po dodaniu ignorowania plików dla obu git (`.gitignore`) oraz TF kontroli wersji (`.tfignore`). Te pliki w tym artykule opisano wzorców plików, których nie chcesz do zaewidencjonowania.

`.gitignore` Pliku wygląda następująco:

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages

`.gitignore` Plik jest [bardzo zaawansowane](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html). Na przykład, jeśli chcesz zazwyczaj nie zaewidencjonowania zawartość `packages` folder, ale chcesz przejść z poprzednich wskazówek kontroli `.targets` plików może mieć następujące reguły, zamiast tego:

    packages
    !packages/**/*.targets

To powoduje wyłączenie wszystkich `packages` folderów jednak zostanie ponownie obejmują wszystkie zawarte `.targets` plików. W systemie można znaleźć szablonu dla `.gitignore` pliki, które jest w szczególny sposób dopasowane do potrzeb deweloperów programu Visual Studio [tutaj](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).

Kontrola wersji TF obsługuje mechanizm bardzo podobne za pośrednictwem [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) pliku. Składnia jest praktycznie:

    *.user
    *.suo
    bin
    obj
    packages

## <a name="buildproj"></a>build.proj

W naszym pokaz możemy przechowywać proces kompilacji dość proste. Utworzymy projektu MSBuild, która tworzy wszystkie rozwiązania oraz zapewnienie, że pakiety są przywracane przed kompilacją rozwiązania.

Ten projekt będzie mieć trzy obiektów docelowych z konwencjonalnej `Clean`, `Build` i `Rebuild` oraz nowy cel `RestorePackages`.

- `Build` i `Rebuild` zależą od obiektów docelowych `RestorePackages`. Dzięki temu, że można jednocześnie uruchomić `Build` i `Rebuild` i zależne od pakietów przywracana.
- `Clean`, `Build` i `Rebuild` wywołania odpowiedniego docelowego MSBuild we wszystkich plikach w rozwiązaniu.
- `RestorePackages` Wywołuje docelowej `nuget.exe` dla każdego pliku rozwiązania. Jest to zrobić za pomocą [MSBuild na przetwarzanie wsadowe funkcji](/visualstudio/msbuild/msbuild-batching).

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

## <a name="configuring-team-build"></a>Konfigurowanie kompilację zespołową

Team Build oferuje różne szablony procesu. Dla tej prezentacji firma Microsoft korzysta z programu Team Foundation Service. Jednak w przypadku instalacji lokalnych programu TFS będzie bardzo podobne.

Git i kontroli wersji TF ma różnych szablonów Team Build, czynności będą się różnić w zależności od systemu kontroli wersji, którego używasz. W obu przypadkach należy wybiera build.proj jako projekt, który chcesz utworzyć.

Po pierwsze Przyjrzyjmy się szablon procesu git. W szablonie git na podstawie wybrano kompilacji za pomocą właściwości `Solution to build`:

![Proces kompilacji dla git](media/PackageRestoreTeamBuildGit.png)

Należy pamiętać, że ta właściwość jest lokalizacja w repozytorium. Ponieważ naszych `build.proj` jest w folderze głównym, po prostu użyliśmy `build.proj`. Jeśli plik kompilacji zostanie umieszczony w folderze o nazwie `tools`, wartość będzie wynosić `tools\build.proj`.

W szablonie kontroli wersji TF projekt jest wybrany za pomocą właściwości `Projects`:

![Proces kompilacji dla programu TFVC](media/PackageRestoreTeamBuildTFVC.png)

W przeciwieństwie do narzędzia git, na podstawie szablonu TF kontroli wersji obsługuje wyboru (przycisk z wielokropkiem po prawej stronie). Dlatego w celu uniknięcia błędów pisowni Sugerujemy użyć do wybrania projektu.