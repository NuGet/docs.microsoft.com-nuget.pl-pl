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
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="2edf6-103">Konfigurowanie przywracania pakietów w programie Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="2edf6-103">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="2edf6-104">Ten artykuł zawiera szczegółowy przewodnik na temat sposobu przywracania pakietów w ramach [Team Services Build](/vsts/build-release/index) zarówno dla usług Git i kontroli wersji serwera Team Services.</span><span class="sxs-lookup"><span data-stu-id="2edf6-104">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="2edf6-105">Chociaż w tym instruktażu jest specyficzne dla scenariusza za pomocą programu Visual Studio Team Services, również dotyczyć innych kontroli wersji i tworzenie systemów.</span><span class="sxs-lookup"><span data-stu-id="2edf6-105">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="2edf6-106">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="2edf6-106">Applies To:</span></span>

- <span data-ttu-id="2edf6-107">Niestandardowe projekty MSBuild, uruchamiane w dowolnej wersji programu TFS</span><span class="sxs-lookup"><span data-stu-id="2edf6-107">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="2edf6-108">Team Foundation Server 2012 lub starszy</span><span class="sxs-lookup"><span data-stu-id="2edf6-108">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="2edf6-109">Team Foundation tworzenia procesu szablonów niestandardowych migracji do programu TFS 2013 lub nowszym</span><span class="sxs-lookup"><span data-stu-id="2edf6-109">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="2edf6-110">Szablony procesu kompilacji za pomocą funkcji Przywracanie pakietów Nuget</span><span class="sxs-lookup"><span data-stu-id="2edf6-110">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="2edf6-111">Jeśli używasz programu Visual Studio Team Services lub programu Team Foundation Server 2013 z jego szablony procesu kompilacji, jako część procesu kompilacji odbywa się Przywracanie pakietu automatyczne.</span><span class="sxs-lookup"><span data-stu-id="2edf6-111">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="2edf6-112">Metody ogólne</span><span class="sxs-lookup"><span data-stu-id="2edf6-112">The general approach</span></span>

<span data-ttu-id="2edf6-113">Zaletą za pomocą narzędzia NuGet jest, że umożliwia ona Unikaj ewidencjonowania plików binarnych do systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="2edf6-113">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="2edf6-114">Jest to szczególnie interesujące, jeśli używasz [rozproszonej kontroli wersji](http://en.wikipedia.org/wiki/Distributed_revision_control) systemu, takich jak git, ponieważ deweloperzy muszą sklonować całego repozytorium, łącznie z pełną historią, przed uruchomieniem trybu pracy — lokalnie.</span><span class="sxs-lookup"><span data-stu-id="2edf6-114">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="2edf6-115">Ewidencjonowanie plików binarnych może spowodować przeładowanie znaczące repozytorium, jak pliki binarne są zazwyczaj przechowywane bez kompresji delta.</span><span class="sxs-lookup"><span data-stu-id="2edf6-115">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="2edf6-116">NuGet ma obsługiwane [Trwa przywracanie pakietów](../consume-packages/package-restore.md) jako część kompilacji długi czas teraz.</span><span class="sxs-lookup"><span data-stu-id="2edf6-116">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="2edf6-117">Poprzedniej implementacji wystąpił problem kurczaka egg pakietów, które chcesz rozszerzyć proces kompilacji, ponieważ NuGet przywrócono pakiety podczas kompilowania projektu.</span><span class="sxs-lookup"><span data-stu-id="2edf6-117">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="2edf6-118">Jednak program MSBuild nie zezwala na rozszerzanie kompilacji podczas kompilacji; jeden można dokumentu uważają że problemu w programie MSBuild, ale czy będzie dokumentu uważają, że jest to problem nieprzerwaną pracę.</span><span class="sxs-lookup"><span data-stu-id="2edf6-118">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="2edf6-119">Zależności od tego, z którym aspektem należy rozszerzyć może być za późno do zarejestrowania przez razem, gdy pakiet zostanie przywrócony.</span><span class="sxs-lookup"><span data-stu-id="2edf6-119">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="2edf6-120">Utrwalenie tego problemu jest upewniając się, że pakiety zostaną przywrócone jako pierwszy krok w procesie kompilacji:</span><span class="sxs-lookup"><span data-stu-id="2edf6-120">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="2edf6-121">Podczas procesu kompilacji, przywraca pakietów przed kompilacją kod, nie ma potrzeby ewidencjonowania `.targets` plików</span><span class="sxs-lookup"><span data-stu-id="2edf6-121">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="2edf6-122">Pakiety musi zostać utworzona, aby umożliwić ładowanie w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2edf6-122">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="2edf6-123">W przeciwnym razie może nadal chcesz zaewidencjonować `.targets` plików tak, aby inni deweloperzy mogą po prostu otwórz rozwiązanie, bez konieczności przywrócenia pakietów, najpierw.</span><span class="sxs-lookup"><span data-stu-id="2edf6-123">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="2edf6-124">Następujący projekt demonstracyjny pokazuje, jak Konfigurowanie kompilacji w taki sposób, który `packages` folderów i `.targets` pliki nie muszą zostać zaewidencjonowany.</span><span class="sxs-lookup"><span data-stu-id="2edf6-124">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="2edf6-125">Pokazano również, jak skonfigurować kompilację automatyczną na Team Foundation Service dla tego przykładowego projektu.</span><span class="sxs-lookup"><span data-stu-id="2edf6-125">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="2edf6-126">Struktura repozytorium</span><span class="sxs-lookup"><span data-stu-id="2edf6-126">Repository structure</span></span>

<span data-ttu-id="2edf6-127">Nasz projekt demonstracyjny to narzędzie wiersza polecenia proste, które używa argumentu wiersza polecenia do wykonywania zapytań w usłudze Bing.</span><span class="sxs-lookup"><span data-stu-id="2edf6-127">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="2edf6-128">Jest przeznaczony dla .NET Framework 4 i używa wielu takich [pakietów BCL](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), i [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="2edf6-128">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="2edf6-129">Struktura repozytorium wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="2edf6-129">The structure of the repository looks as follows:</span></span>

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

<span data-ttu-id="2edf6-130">Widać, że firma Microsoft nie został zaewidencjonowany `packages` folder ani żaden `.targets` plików.</span><span class="sxs-lookup"><span data-stu-id="2edf6-130">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="2edf6-131">Firma Microsoft jednak zaewidencjonowania `nuget.exe` potrzeb podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="2edf6-131">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="2edf6-132">Zgodnie z powszechnie używane konwencje firma Microsoft została sprawdzona jej obszarze udostępnionego `tools` folderu.</span><span class="sxs-lookup"><span data-stu-id="2edf6-132">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="2edf6-133">Kod źródłowy znajduje się w obszarze `src` folderu.</span><span class="sxs-lookup"><span data-stu-id="2edf6-133">The source code is under the `src` folder.</span></span> <span data-ttu-id="2edf6-134">Mimo że naszą wersję demonstracyjną, używa tylko jednego rozwiązania, możesz sobie wyobrazić, że ten folder zawiera więcej niż jedno rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="2edf6-134">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="2edf6-135">Pliki ignorowanych</span><span class="sxs-lookup"><span data-stu-id="2edf6-135">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="2edf6-136">Ma obecnie [znaną usterką w kliencie programu NuGet](https://nuget.codeplex.com/workitem/4072) , powoduje, że klient nadal dodawać `packages` folderu do kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="2edf6-136">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="2edf6-137">Obejście tego problemu jest wyłączyć integrację kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="2edf6-137">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="2edf6-138">Aby to zrobić, należy `Nuget.Config ` w pliku `.nuget` folder, który jest zbliżony do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2edf6-138">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="2edf6-139">Ten folder nie istnieje, należy go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="2edf6-139">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="2edf6-140">W [ `Nuget.Config` ](../consume-packages/configuring-nuget-behavior.md), dodaj następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="2edf6-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="2edf6-141">Do komunikacji z kontroli wersji, nie musimy zamiarem ewidencjonowania **pakietów** folderów, dodaliśmy także, ignorowania plików dla obu git (`.gitignore`) oraz kontrola wersji TF (`.tfignore`).</span><span class="sxs-lookup"><span data-stu-id="2edf6-141">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="2edf6-142">Pliki te opisują wzorce plików, których nie chcesz, aby warunkowo.</span><span class="sxs-lookup"><span data-stu-id="2edf6-142">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="2edf6-143">`.gitignore` Pliku wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="2edf6-143">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

<span data-ttu-id="2edf6-144">`.gitignore` Plik jest [bardzo wydajny](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="2edf6-144">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="2edf6-145">Na przykład, jeśli chcesz ogólnie nie ewidencjonowania zawartość `packages` folder, ale ma pod ręką wcześniejszych wskazówkach sprawdzania `.targets` plików może mieć następujące reguły, zamiast tego:</span><span class="sxs-lookup"><span data-stu-id="2edf6-145">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="2edf6-146">To powoduje wyłączenie wszystkich `packages` folderów ale będzie ponownie obejmują wszystkie zawarte `.targets` plików.</span><span class="sxs-lookup"><span data-stu-id="2edf6-146">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="2edf6-147">Przy okazji można znaleźć szablonu dla `.gitignore` pliki, które jest w szczególny sposób dopasowane do potrzeb deweloperów programu Visual Studio [tutaj](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="2edf6-147">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="2edf6-148">Kontrola wersji TF obsługuje bardzo podobny mechanizm, za pośrednictwem [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) pliku.</span><span class="sxs-lookup"><span data-stu-id="2edf6-148">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="2edf6-149">Składnia jest praktycznie taki sam:</span><span class="sxs-lookup"><span data-stu-id="2edf6-149">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a><span data-ttu-id="2edf6-150">Build.Proj</span><span class="sxs-lookup"><span data-stu-id="2edf6-150">build.proj</span></span>

<span data-ttu-id="2edf6-151">Nasz pokaz przechowujemy procesu kompilacji stosunkowo proste.</span><span class="sxs-lookup"><span data-stu-id="2edf6-151">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="2edf6-152">Utworzymy projektu programu MSBuild, który tworzy wszystkie rozwiązania, pamiętając, że pakiety zostaną przywrócone przed kompilacją rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2edf6-152">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="2edf6-153">Ten projekt będzie mieć trzy elementy docelowe konwencjonalne `Clean`, `Build` i `Rebuild` oraz nowy obiekt docelowy `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="2edf6-153">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="2edf6-154">`Build` i `Rebuild` zależą od obiektów docelowych `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="2edf6-154">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="2edf6-155">Daje to pewność, że można jednocześnie uruchomić `Build` i `Rebuild` i zależą od pakietów przywracana.</span><span class="sxs-lookup"><span data-stu-id="2edf6-155">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="2edf6-156">`Clean`, `Build` i `Rebuild` Wywołaj odpowiedni element docelowy programu MSBuild na wszystkie pliki rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2edf6-156">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="2edf6-157">`RestorePackages` Miejsce docelowe wywołuje `nuget.exe` dla każdego pliku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2edf6-157">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="2edf6-158">Jest to realizowane przy użyciu [MSBuild na partie funkcji](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="2edf6-158">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="2edf6-159">Wynik będzie wyglądać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2edf6-159">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="2edf6-160">Konfigurowanie Team Build</span><span class="sxs-lookup"><span data-stu-id="2edf6-160">Configuring Team Build</span></span>

<span data-ttu-id="2edf6-161">Kompilacja zespołowa oferuje różne szablony procesów.</span><span class="sxs-lookup"><span data-stu-id="2edf6-161">Team Build offers various process templates.</span></span> <span data-ttu-id="2edf6-162">W tej prezentacji używamy programu Team Foundation Service.</span><span class="sxs-lookup"><span data-stu-id="2edf6-162">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="2edf6-163">Instalacje środowiska lokalnego serwera TFS będzie odbywać się bardzo podobne.</span><span class="sxs-lookup"><span data-stu-id="2edf6-163">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="2edf6-164">Git i kontrola wersji TF mają różne szablony kompilacji zespołowej, dlatego poniższe kroki różnią się w zależności od tego, którego systemu kontroli wersji używasz.</span><span class="sxs-lookup"><span data-stu-id="2edf6-164">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="2edf6-165">W obu przypadkach wystarczy to wybranie build.proj jako projekt, który chcesz skompilować.</span><span class="sxs-lookup"><span data-stu-id="2edf6-165">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="2edf6-166">Najpierw Przyjrzyjmy się z szablonem procesu dla usługi git.</span><span class="sxs-lookup"><span data-stu-id="2edf6-166">First, let's look at the process template for git.</span></span> <span data-ttu-id="2edf6-167">W szablonie usługi git, na podstawie kompilacji jest wybierany za pomocą właściwości `Solution to build`:</span><span class="sxs-lookup"><span data-stu-id="2edf6-167">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Proces kompilacji dla systemu git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="2edf6-169">Należy pamiętać, że ta właściwość ma miejsce w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="2edf6-169">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="2edf6-170">Ponieważ naszych `build.proj` jest w katalogu głównym, po prostu użyliśmy `build.proj`.</span><span class="sxs-lookup"><span data-stu-id="2edf6-170">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="2edf6-171">Jeśli plik kompilacji jest umieścić w folderze o nazwie `tools`, wartość będzie wynosić `tools\build.proj`.</span><span class="sxs-lookup"><span data-stu-id="2edf6-171">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="2edf6-172">W szablonie Kontrola wersji TF projekt jest wybrany za pomocą właściwości `Projects`:</span><span class="sxs-lookup"><span data-stu-id="2edf6-172">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Proces kompilacji w przypadku repozytorium TFVC](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="2edf6-174">W przeciwieństwie do usługi git, na podstawie szablonu TF Kontrola wersji obsługuje formanty wyboru (przycisk z wielokropkiem na stronie po prawej stronie).</span><span class="sxs-lookup"><span data-stu-id="2edf6-174">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="2edf6-175">Tak, aby uniknąć błędów pisowni Sugerujemy za pomocą wybierz projekt.</span><span class="sxs-lookup"><span data-stu-id="2edf6-175">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
