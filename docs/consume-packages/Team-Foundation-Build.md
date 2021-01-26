---
title: Przewodnik po przywracaniu pakietów NuGet za pomocą programu Team Foundation Build
description: Przewodnik dotyczący sposobu przywracania pakietu NuGet przy użyciu programu Team Foundation Build (zarówno TFS, jak i Visual Studio Team Services).
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 8b993106d439dc137fbe040b51fda373539de81a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774994"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="d0526-103">Konfigurowanie przywracania pakietu przy użyciu Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="d0526-103">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="d0526-104">Ten artykuł zawiera szczegółowy przewodnik dotyczący sposobu przywracania pakietów w ramach [kompilacji usługi Team Services](/vsts/build-release/index) zarówno dla kontroli wersji usług git, jak i Team Services.</span><span class="sxs-lookup"><span data-stu-id="d0526-104">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="d0526-105">Chociaż ten przewodnik jest specyficzny dla scenariusza używania Visual Studio Team Services, pojęcia dotyczą także innych systemów kontroli wersji i kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d0526-105">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="d0526-106">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="d0526-106">Applies To:</span></span>

- <span data-ttu-id="d0526-107">Niestandardowe projekty programu MSBuild działające w dowolnej wersji programu TFS</span><span class="sxs-lookup"><span data-stu-id="d0526-107">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="d0526-108">Team Foundation Server 2012 lub starszy</span><span class="sxs-lookup"><span data-stu-id="d0526-108">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="d0526-109">Niestandardowe szablony procesu programu Team Foundation Build migrowane do programu TFS 2013 lub nowszego</span><span class="sxs-lookup"><span data-stu-id="d0526-109">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="d0526-110">Kompiluj szablony procesów z usuniętymi funkcjami przywracania NuGet</span><span class="sxs-lookup"><span data-stu-id="d0526-110">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="d0526-111">Jeśli używasz Visual Studio Team Services lub Team Foundation Server 2013 z szablonami procesu kompilacji, automatyczne przywracanie pakietów odbywa się w ramach procesu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d0526-111">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="d0526-112">Ogólne podejście</span><span class="sxs-lookup"><span data-stu-id="d0526-112">The general approach</span></span>

<span data-ttu-id="d0526-113">Zaletą korzystania z programu NuGet jest możliwość użycia go w celu uniknięcia ewidencjonowania plików binarnych w systemie kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="d0526-113">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="d0526-114">Jest to szczególnie przydatne, jeśli używasz [rozproszonego systemu kontroli wersji](https://en.wikipedia.org/wiki/Distributed_revision_control) , takiego jak Git, ponieważ deweloperzy muszą sklonować całe repozytorium, w tym pełną historię, zanim będą mogli rozpocząć pracę lokalnie.</span><span class="sxs-lookup"><span data-stu-id="d0526-114">This is especially interesting if you are using a [distributed version control](https://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="d0526-115">Ewidencjonowanie plików binarnych może spowodować znaczące przeładowanie repozytorium, ponieważ pliki binarne są zwykle przechowywane bez kompresji różnicowej.</span><span class="sxs-lookup"><span data-stu-id="d0526-115">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="d0526-116">Pakiet NuGet obsługuje teraz [przywracanie pakietów](../consume-packages/package-restore.md) w ramach kompilacji przez długi czas.</span><span class="sxs-lookup"><span data-stu-id="d0526-116">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="d0526-117">W poprzedniej implementacji wystąpił problem z kurczakami i jajami dla pakietów, które chcą zwiększyć proces kompilacji, ponieważ pakiety NuGet zostały przywrócone podczas kompilowania projektu.</span><span class="sxs-lookup"><span data-stu-id="d0526-117">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="d0526-118">Jednak MSBuild nie zezwala na rozszerzanie kompilacji podczas kompilacji; może to spowodować, że ten problem wystąpił w programie MSBuild, ale może to być problem.</span><span class="sxs-lookup"><span data-stu-id="d0526-118">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="d0526-119">W zależności od tego, który aspekt należy zwiększyć, może być zbyt późny do zarejestrowania przez czas przywrócenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="d0526-119">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="d0526-120">Odjęcie tego problemu polega na tym, że pakiety są przywracane jako pierwszy krok w procesie kompilacji:</span><span class="sxs-lookup"><span data-stu-id="d0526-120">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="d0526-121">Gdy proces kompilacji przywraca pakiety przed skompilowaniem kodu, nie musisz ewidencjonować `.targets` plików</span><span class="sxs-lookup"><span data-stu-id="d0526-121">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="d0526-122">Pakiety muszą zostać utworzone w celu umożliwienia ładowania w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0526-122">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="d0526-123">W przeciwnym razie można nadal chcieć zaewidencjonować `.targets` pliki, aby inni deweloperzy mogli po prostu otworzyć rozwiązanie bez konieczności wcześniejszego przywrócenia pakietów.</span><span class="sxs-lookup"><span data-stu-id="d0526-123">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="d0526-124">W poniższym projekcie demonstracyjnym pokazano, jak skonfigurować kompilację w taki sposób, aby `packages` `.targets` nie trzeba było ewidencjonować folderów i plików.</span><span class="sxs-lookup"><span data-stu-id="d0526-124">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="d0526-125">Przedstawiono w nim również sposób konfigurowania zautomatyzowanej kompilacji na Team Foundation Service dla tego przykładowego projektu.</span><span class="sxs-lookup"><span data-stu-id="d0526-125">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="d0526-126">Struktura repozytorium</span><span class="sxs-lookup"><span data-stu-id="d0526-126">Repository structure</span></span>

<span data-ttu-id="d0526-127">Nasze projekty demonstracyjne to proste narzędzie wiersza polecenia, które używa argumentu wiersza polecenia do wysyłania zapytań do usługi Bing.</span><span class="sxs-lookup"><span data-stu-id="d0526-127">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="d0526-128">Jest ona przeznaczona dla .NET Framework 4 i używa wielu [pakietów BCL](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.NET. http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft. BCL](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft. BCL. Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)i [Microsoft. BCL. Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="d0526-128">It targets the .NET Framework 4 and uses many of the [BCL packages](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="d0526-129">Struktura repozytorium wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="d0526-129">The structure of the repository looks as follows:</span></span>

```
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
```

<span data-ttu-id="d0526-130">Można zobaczyć, że nie zaznaczono `packages` folderu ani `.targets` plików.</span><span class="sxs-lookup"><span data-stu-id="d0526-130">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="d0526-131">Mamy jednak zaewidencjonować, że jest to `nuget.exe` konieczne podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d0526-131">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="d0526-132">Zgodnie z powszechnie używanymi konwencjami została sprawdzona w folderze udostępnionym `tools` .</span><span class="sxs-lookup"><span data-stu-id="d0526-132">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="d0526-133">Kod źródłowy znajduje się w `src` folderze.</span><span class="sxs-lookup"><span data-stu-id="d0526-133">The source code is under the `src` folder.</span></span> <span data-ttu-id="d0526-134">Mimo że w tej wersji demonstracyjnej używane jest tylko jedno rozwiązanie, można w łatwy sposób przypuśćć, że ten folder zawiera więcej niż jedno rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="d0526-134">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="d0526-135">Pliki ignorowanych</span><span class="sxs-lookup"><span data-stu-id="d0526-135">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="d0526-136">[W kliencie NuGet jest obecnie znana usterka](https://nuget.codeplex.com/workitem/4072) , która powoduje, że klient nadal dodaje `packages` folder do kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="d0526-136">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="d0526-137">Obejście polega na wyłączeniu integracji kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="d0526-137">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="d0526-138">W tym celu potrzebny `Nuget.Config ` jest plik w  `.nuget` folderze, który jest równoległy do Twojego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d0526-138">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="d0526-139">Jeśli ten folder jeszcze nie istnieje, należy go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="d0526-139">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="d0526-140">W programie [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) Dodaj następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="d0526-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="d0526-141">Aby komunikować się z kontrolą wersji, której nie chcemy zaewidencjonować folderów **pakietów** , dodaliśmy również ignorowanie plików zarówno dla narzędzia Git ( `.gitignore` ), jak i kontroli wersji TF ( `.tfignore` ).</span><span class="sxs-lookup"><span data-stu-id="d0526-141">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="d0526-142">Te pliki opisują wzorce plików, których nie chcesz zaewidencjonować.</span><span class="sxs-lookup"><span data-stu-id="d0526-142">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="d0526-143">`.gitignore`Plik wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="d0526-143">The `.gitignore` file looks as follows:</span></span>

```
syntax: glob
*.user
*.suo
bin
obj
packages
*.nupkg
project.lock.json
project.assets.json
```

<span data-ttu-id="d0526-144">`.gitignore`Plik jest [całkiem wydajny](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="d0526-144">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="d0526-145">Na przykład, jeśli chcesz zwykle nie zaewidencjonować zawartości `packages` folderu, ale chcesz przejść do poprzedniej wskazówki dotyczącej sprawdzania `.targets` plików, można użyć następującej reguły:</span><span class="sxs-lookup"><span data-stu-id="d0526-145">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

```
packages
!packages/**/*.targets
```

<span data-ttu-id="d0526-146">Spowoduje to wykluczenie wszystkich `packages` folderów, ale spowoduje ponowne uwzględnienie wszystkich zawartych `.targets` plików.</span><span class="sxs-lookup"><span data-stu-id="d0526-146">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="d0526-147">W ten sposób można znaleźć szablon `.gitignore` plików, które są specjalnie dostosowane do potrzeb deweloperów programu Visual Studio. [](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)</span><span class="sxs-lookup"><span data-stu-id="d0526-147">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="d0526-148">System kontroli wersji TF obsługuje bardzo podobny mechanizm za pośrednictwem pliku [. tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) .</span><span class="sxs-lookup"><span data-stu-id="d0526-148">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="d0526-149">Składnia jest praktycznie taka sama:</span><span class="sxs-lookup"><span data-stu-id="d0526-149">The syntax is virtually the same:</span></span>

```
*.user
*.suo
bin
obj
packages
*.nupkg
project.lock.json
project.assets.json
```

## <a name="buildproj"></a><span data-ttu-id="d0526-150">Kompilacja. proj</span><span class="sxs-lookup"><span data-stu-id="d0526-150">build.proj</span></span>

<span data-ttu-id="d0526-151">W naszej wersji demonstracyjnej proces kompilacji jest dość prosty.</span><span class="sxs-lookup"><span data-stu-id="d0526-151">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="d0526-152">Utworzymy projekt MSBuild, który kompiluje wszystkie rozwiązania, a jednocześnie upewnia się, że pakiety są przywracane przed skompilowaniem rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="d0526-152">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="d0526-153">Ten projekt będzie miał trzy konwencjonalne cele `Clean` , `Build` a także `Rebuild` nowy element docelowy `RestorePackages` .</span><span class="sxs-lookup"><span data-stu-id="d0526-153">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="d0526-154">`Build`Elementy i `Rebuild` są zależne od `RestorePackages` .</span><span class="sxs-lookup"><span data-stu-id="d0526-154">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="d0526-155">Dzięki temu można uruchamiać `Build` i `Rebuild` korzystać z pakietów, które są przywracane.</span><span class="sxs-lookup"><span data-stu-id="d0526-155">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="d0526-156">`Clean``Build`i `Rebuild` Wywołaj odpowiednie obiekty docelowe programu MSBuild we wszystkich plikach rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d0526-156">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="d0526-157">`RestorePackages`Obiekt docelowy wywołuje `nuget.exe` każdy plik rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d0526-157">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="d0526-158">Jest to realizowane przy użyciu [funkcji wsadowych programu MSBuild](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="d0526-158">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="d0526-159">Wynik będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="d0526-159">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="d0526-160">Konfigurowanie kompilacji zespołu</span><span class="sxs-lookup"><span data-stu-id="d0526-160">Configuring Team Build</span></span>

<span data-ttu-id="d0526-161">Kompilacja zespołowa oferuje różne szablony procesów.</span><span class="sxs-lookup"><span data-stu-id="d0526-161">Team Build offers various process templates.</span></span> <span data-ttu-id="d0526-162">Na potrzeby tej demonstracji używamy Team Foundation Service.</span><span class="sxs-lookup"><span data-stu-id="d0526-162">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="d0526-163">Instalacje lokalne programu TFS będą bardzo podobne.</span><span class="sxs-lookup"><span data-stu-id="d0526-163">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="d0526-164">System kontroli wersji Git i TF ma inne szablony kompilacji zespołu, więc poniższe kroki będą się różnić w zależności od używanego systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="d0526-164">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="d0526-165">W obu przypadkach wystarczy wybrać kompilację Build. proj jako projekt, który chcesz skompilować.</span><span class="sxs-lookup"><span data-stu-id="d0526-165">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="d0526-166">Najpierw przyjrzyjmy się szablonowi procesu do usługi git.</span><span class="sxs-lookup"><span data-stu-id="d0526-166">First, let's look at the process template for git.</span></span> <span data-ttu-id="d0526-167">W szablonie opartym na git kompilacja jest wybierana za pośrednictwem właściwości `Solution to build` :</span><span class="sxs-lookup"><span data-stu-id="d0526-167">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Proces kompilacji dla narzędzia Git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="d0526-169">Należy pamiętać, że ta właściwość jest lokalizacją w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="d0526-169">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="d0526-170">Ponieważ nasz `build.proj` element znajduje się w katalogu głównym, został po prostu użyty `build.proj` .</span><span class="sxs-lookup"><span data-stu-id="d0526-170">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="d0526-171">Jeśli plik kompilacji zostanie umieszczony w folderze o nazwie `tools` , wartość będzie równa `tools\build.proj` .</span><span class="sxs-lookup"><span data-stu-id="d0526-171">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="d0526-172">W szablonie kontroli wersji TF projekt jest wybierany za pośrednictwem właściwości `Projects` :</span><span class="sxs-lookup"><span data-stu-id="d0526-172">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Proces kompilacji dla TFVC](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="d0526-174">W przeciwieństwie do szablonu opartego na usłudze git Kontrola wersji TF obsługuje selektory (przycisk po prawej stronie z trzema kropkami).</span><span class="sxs-lookup"><span data-stu-id="d0526-174">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="d0526-175">Aby uniknąć błędów wpisywania, zalecamy użycie ich do wybrania projektu.</span><span class="sxs-lookup"><span data-stu-id="d0526-175">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
