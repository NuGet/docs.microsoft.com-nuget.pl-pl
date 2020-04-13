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
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="22d21-103">Konfigurowanie przywracania pakietu za pomocą team foundation build</span><span class="sxs-lookup"><span data-stu-id="22d21-103">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="22d21-104">Ten artykuł zawiera szczegółowe wskazówki dotyczące przywracania pakietów w ramach [team services kompilacji](/vsts/build-release/index) zarówno dla Git i Team Services kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="22d21-104">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="22d21-105">Chociaż ten instruktaż jest specyficzny dla scenariusza korzystania z programu Visual Studio Team Services, pojęcia dotyczą również innych systemów kontroli wersji i kompilacji.</span><span class="sxs-lookup"><span data-stu-id="22d21-105">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="22d21-106">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="22d21-106">Applies To:</span></span>

- <span data-ttu-id="22d21-107">Niestandardowe projekty MSBuild uruchomione w dowolnej wersji usługi TFS</span><span class="sxs-lookup"><span data-stu-id="22d21-107">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="22d21-108">Team Foundation Server 2012 lub wcześniejszy</span><span class="sxs-lookup"><span data-stu-id="22d21-108">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="22d21-109">Szablony procesów kompilacji niestandardowych fundacji zespołu zmigrowane do usługi TFS 2013 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="22d21-109">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="22d21-110">Tworzenie szablonów procesów z usuniętą funkcją przywracania nuget</span><span class="sxs-lookup"><span data-stu-id="22d21-110">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="22d21-111">Jeśli używasz programu Visual Studio Team Services lub Team Foundation Server 2013 z jego szablonów procesu kompilacji, automatyczne przywracanie pakietu odbywa się w ramach procesu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="22d21-111">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="22d21-112">Ogólne podejście</span><span class="sxs-lookup"><span data-stu-id="22d21-112">The general approach</span></span>

<span data-ttu-id="22d21-113">Zaletą korzystania z NuGet jest to, że można go używać, aby uniknąć sprawdzania w plikach binarnych do systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="22d21-113">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="22d21-114">Jest to szczególnie interesujące, jeśli używasz rozproszonego systemu [kontroli wersji,](https://en.wikipedia.org/wiki/Distributed_revision_control) takiego jak git, ponieważ deweloperzy muszą sklonować całe repozytorium, w tym pełną historię, zanim będą mogli rozpocząć pracę lokalnie.</span><span class="sxs-lookup"><span data-stu-id="22d21-114">This is especially interesting if you are using a [distributed version control](https://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="22d21-115">Zaewidencjonowanie w plikach binarnych może spowodować znaczne nadęcie repozytorium, ponieważ pliki binarne są zazwyczaj przechowywane bez kompresji różnicowej.</span><span class="sxs-lookup"><span data-stu-id="22d21-115">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="22d21-116">NuGet obsługuje [przywracanie pakietów](../consume-packages/package-restore.md) jako część kompilacji przez długi czas.</span><span class="sxs-lookup"><span data-stu-id="22d21-116">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="22d21-117">Poprzednia implementacja miała problem z kurczakiem i jajem dla pakietów, które chcesz rozszerzyć proces kompilacji, ponieważ NuGet przywrócono pakiety podczas tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="22d21-117">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="22d21-118">Jednak MSBuild nie zezwala na rozszerzanie kompilacji podczas kompilacji; można argumentować, że jest to problem w MSBuild, ale chciałbym twierdzić, że jest to nieodłączny problem.</span><span class="sxs-lookup"><span data-stu-id="22d21-118">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="22d21-119">W zależności od tego, który aspekt należy rozszerzyć może być za późno, aby zarejestrować się do czasu, gdy pakiet zostanie przywrócony.</span><span class="sxs-lookup"><span data-stu-id="22d21-119">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="22d21-120">Lekarstwem na ten problem jest upewnienie się, że pakiety są przywracane jako pierwszy krok w procesie kompilacji:</span><span class="sxs-lookup"><span data-stu-id="22d21-120">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="22d21-121">Gdy proces kompilacji przywraca pakiety przed utworzeniem kodu, nie `.targets` trzeba zaewidencjonować plików</span><span class="sxs-lookup"><span data-stu-id="22d21-121">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="22d21-122">Pakiety muszą być autorstwa, aby umożliwić ładowanie w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="22d21-122">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="22d21-123">W przeciwnym razie nadal można `.targets` zaewidencjonować pliki, aby inni deweloperzy mogli po prostu otworzyć rozwiązanie bez konieczności przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="22d21-123">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="22d21-124">Poniższy projekt demonstracyjny pokazuje, jak skonfigurować `packages` kompilację `.targets` w taki sposób, aby foldery i pliki nie musiały być zaewidencjonowane.</span><span class="sxs-lookup"><span data-stu-id="22d21-124">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="22d21-125">Pokazuje również, jak skonfigurować zautomatyzowaną kompilację w usłudze Team Foundation dla tego przykładowego projektu.</span><span class="sxs-lookup"><span data-stu-id="22d21-125">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="22d21-126">Struktura repozytorium</span><span class="sxs-lookup"><span data-stu-id="22d21-126">Repository structure</span></span>

<span data-ttu-id="22d21-127">Nasz projekt demonstracyjny to proste narzędzie wiersza polecenia, które używa argumentu wiersza polecenia do wykonywania zapytań bing.</span><span class="sxs-lookup"><span data-stu-id="22d21-127">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="22d21-128">Jest przeznaczony dla programu .NET Framework 4 i używa wielu [pakietów BCL](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)i [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="22d21-128">It targets the .NET Framework 4 and uses many of the [BCL packages](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="22d21-129">Struktura repozytorium wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="22d21-129">The structure of the repository looks as follows:</span></span>

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

<span data-ttu-id="22d21-130">Widać, że nie sprawdziliśmy `packages` ani żadnych `.targets` plików.</span><span class="sxs-lookup"><span data-stu-id="22d21-130">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="22d21-131">Mamy jednak sprawdzone w `nuget.exe` jak to jest potrzebne podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="22d21-131">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="22d21-132">Zgodnie z powszechnie używanymi konwencjami zaewidencjonowaliśmy go w folderze udostępnionym. `tools`</span><span class="sxs-lookup"><span data-stu-id="22d21-132">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="22d21-133">Kod źródłowy znajduje `src` się w folderze.</span><span class="sxs-lookup"><span data-stu-id="22d21-133">The source code is under the `src` folder.</span></span> <span data-ttu-id="22d21-134">Chociaż nasze demo używa tylko jednego rozwiązania, można łatwo sobie wyobrazić, że ten folder zawiera więcej niż jedno rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="22d21-134">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="22d21-135">Pliki ignorowanych</span><span class="sxs-lookup"><span data-stu-id="22d21-135">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="22d21-136">Obecnie istnieje [znany błąd w kliencie NuGet,](https://nuget.codeplex.com/workitem/4072) który powoduje, że klient nadal dodać `packages` folder do kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="22d21-136">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="22d21-137">Obejście jest wyłączenie integracji kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="22d21-137">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="22d21-138">Aby to zrobić, potrzebujesz `Nuget.Config ` pliku w `.nuget` folderze, który jest równoległy do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="22d21-138">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="22d21-139">Jeśli ten folder jeszcze nie istnieje, należy go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="22d21-139">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="22d21-140">W [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md)obszarze dodaj następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="22d21-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="22d21-141">Aby przekazać do kontroli wersji, że nie zamierzamy zaewidencjonować **foldery pakietów,** `.gitignore`dodaliśmy również ignoruj`.tfignore`pliki zarówno dla git ( ), jak również kontroli wersji TF ( ).</span><span class="sxs-lookup"><span data-stu-id="22d21-141">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="22d21-142">Pliki te opisują wzorce plików, których nie chcesz zaewidencjonować.</span><span class="sxs-lookup"><span data-stu-id="22d21-142">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="22d21-143">Plik `.gitignore` wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="22d21-143">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

<span data-ttu-id="22d21-144">Plik `.gitignore` jest [dość potężny](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="22d21-144">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="22d21-145">Na przykład, jeśli zazwyczaj nie chcesz zaewidencjonować zawartości `packages` folderu, ale chcesz `.targets` przejść z poprzednimi wskazówkami dotyczącymi zaewidencjonowania plików, możesz mieć następującą regułę:</span><span class="sxs-lookup"><span data-stu-id="22d21-145">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="22d21-146">Spowoduje to `packages` wykluczenie wszystkich folderów, ale `.targets` spowoduje ponowne uwzględnić wszystkie zawarte pliki.</span><span class="sxs-lookup"><span data-stu-id="22d21-146">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="22d21-147">Nawiasem mówiąc, można znaleźć `.gitignore` szablon dla plików, który jest specjalnie dostosowany do potrzeb deweloperów programu Visual Studio [tutaj](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="22d21-147">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="22d21-148">Kontrola wersji TF obsługuje bardzo podobny mechanizm za pośrednictwem pliku [.tfignore.](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control)</span><span class="sxs-lookup"><span data-stu-id="22d21-148">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="22d21-149">Składnia jest praktycznie taka sama:</span><span class="sxs-lookup"><span data-stu-id="22d21-149">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a><span data-ttu-id="22d21-150">build.proj</span><span class="sxs-lookup"><span data-stu-id="22d21-150">build.proj</span></span>

<span data-ttu-id="22d21-151">W przypadku naszego demo proces budowania jest dość prosty.</span><span class="sxs-lookup"><span data-stu-id="22d21-151">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="22d21-152">Utworzymy projekt MSBuild, który tworzy wszystkie rozwiązania, upewniając się, że pakiety zostaną przywrócone przed utworzeniem rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="22d21-152">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="22d21-153">Projekt ten będzie miał `Clean`trzy `Build` `Rebuild` konwencjonalne cele, `RestorePackages`a także nowy cel.</span><span class="sxs-lookup"><span data-stu-id="22d21-153">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="22d21-154">Zarówno `Build` `Rebuild` i cele `RestorePackages`zależą od .</span><span class="sxs-lookup"><span data-stu-id="22d21-154">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="22d21-155">Dzięki temu można zarówno `Build` uruchomić `Rebuild` i polegać na pakiety są przywracane.</span><span class="sxs-lookup"><span data-stu-id="22d21-155">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="22d21-156">`Clean`i `Build` `Rebuild` wywołać odpowiedni obiekt docelowy MSBuild we wszystkich plikach rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="22d21-156">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="22d21-157">Obiekt `RestorePackages` docelowy `nuget.exe` wywołuje dla każdego pliku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="22d21-157">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="22d21-158">Jest to realizowane przy użyciu [funkcji wsadowego MSBuild.](/visualstudio/msbuild/msbuild-batching)</span><span class="sxs-lookup"><span data-stu-id="22d21-158">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="22d21-159">Wynik wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="22d21-159">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="22d21-160">Konfigurowanie kompilacji zespołu</span><span class="sxs-lookup"><span data-stu-id="22d21-160">Configuring Team Build</span></span>

<span data-ttu-id="22d21-161">Team Build oferuje różne szablony procesów.</span><span class="sxs-lookup"><span data-stu-id="22d21-161">Team Build offers various process templates.</span></span> <span data-ttu-id="22d21-162">W tej demonstracji używamy usługi Team Foundation Service.</span><span class="sxs-lookup"><span data-stu-id="22d21-162">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="22d21-163">Instalacje lokalne TFS będą jednak bardzo podobne.</span><span class="sxs-lookup"><span data-stu-id="22d21-163">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="22d21-164">Git i TF Version Control mają różne szablony team build, więc następujące kroki będą się różnić w zależności od używanego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="22d21-164">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="22d21-165">W obu przypadkach wszystko, czego potrzebujesz, to wybranie build.proj jako projektu, który chcesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="22d21-165">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="22d21-166">Najpierw przyjrzyjmy się szablonowi procesu dla git.</span><span class="sxs-lookup"><span data-stu-id="22d21-166">First, let's look at the process template for git.</span></span> <span data-ttu-id="22d21-167">W szablonie opartym na git `Solution to build`kompilacja jest wybierana za pośrednictwem właściwości:</span><span class="sxs-lookup"><span data-stu-id="22d21-167">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Proces budowania dla git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="22d21-169">Obiekt znajduje się w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="22d21-169">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="22d21-170">Ponieważ `build.proj` nasz jest w korzeniu, po prostu użyliśmy `build.proj`.</span><span class="sxs-lookup"><span data-stu-id="22d21-170">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="22d21-171">Jeśli umieścisz plik kompilacji `tools`w folderze `tools\build.proj`o nazwie , wartość będzie .</span><span class="sxs-lookup"><span data-stu-id="22d21-171">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="22d21-172">W szablonie kontroli wersji TF projekt `Projects`jest wybierany za pośrednictwem właściwości:</span><span class="sxs-lookup"><span data-stu-id="22d21-172">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Proces budowania dla TFVC](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="22d21-174">W przeciwieństwie do szablonu opartego na git, kontrola wersji TF obsługuje selektory (przycisk po prawej stronie z trzema kropkami).</span><span class="sxs-lookup"><span data-stu-id="22d21-174">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="22d21-175">Tak więc, aby uniknąć błędów pisania, zalecamy użycie ich do wybrania projektu.</span><span class="sxs-lookup"><span data-stu-id="22d21-175">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
