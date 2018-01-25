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
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="75f70-104">Konfigurowanie Przywracanie pakietu z Team Foundation Build</span><span class="sxs-lookup"><span data-stu-id="75f70-104">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="75f70-105">Ten artykuł zawiera szczegółowy przewodnik na temat pod kątem przywracania pakietów w ramach [Team Services Build](/vsts/build-release/index) zarówno dla Git i kontroli wersji programu Team Services.</span><span class="sxs-lookup"><span data-stu-id="75f70-105">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="75f70-106">Chociaż ten przewodnik jest specyficzna dla scenariusza za pomocą programu Visual Studio Team Services, również zastosować do innych kontroli wersji i kompilacji systemu.</span><span class="sxs-lookup"><span data-stu-id="75f70-106">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="75f70-107">Dotyczy:</span><span class="sxs-lookup"><span data-stu-id="75f70-107">Applies To:</span></span>

- <span data-ttu-id="75f70-108">W dowolnej wersji programu TFS niestandardowych projektów MSBuild</span><span class="sxs-lookup"><span data-stu-id="75f70-108">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="75f70-109">Team Foundation Server 2012 lub starszy</span><span class="sxs-lookup"><span data-stu-id="75f70-109">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="75f70-110">Team Foundation kompilacji procesu szablonów niestandardowych migracji do programu TFS 2013 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="75f70-110">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="75f70-111">Szablony procesu kompilacji z zestawem funkcji Przywracanie Nuget</span><span class="sxs-lookup"><span data-stu-id="75f70-111">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="75f70-112">Jeśli używasz programu Visual Studio Team Services lub Team Foundation Server 2013 z jego szablony procesu kompilacji, odbywa się Przywracanie pakietu automatycznych jako część procesu kompilacji.</span><span class="sxs-lookup"><span data-stu-id="75f70-112">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="75f70-113">Metody ogólne</span><span class="sxs-lookup"><span data-stu-id="75f70-113">The general approach</span></span>

<span data-ttu-id="75f70-114">Zaletą przy użyciu narzędzia NuGet to, że można go uniknąć sprawdzanie w danych binarnych systemu kontroli wersji.</span><span class="sxs-lookup"><span data-stu-id="75f70-114">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="75f70-115">Jest to szczególnie interesujące, jeśli używasz [rozproszonych kontroli wersji](http://en.wikipedia.org/wiki/Distributed_revision_control) systemu, takich jak git ponieważ deweloperzy muszą Klonuj repozytorium całego, łącznie z pełną historię przed uruchomieniem pracując lokalnie.</span><span class="sxs-lookup"><span data-stu-id="75f70-115">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="75f70-116">Sprawdzanie w danych binarnych może spowodować znaczne repozytorium rozrostu jako pliki binarne są zwykle przechowywane bez zmian kompresji.</span><span class="sxs-lookup"><span data-stu-id="75f70-116">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="75f70-117">Obsługiwał NuGet [Przywracanie pakietów](../consume-packages/package-restore.md) jako część kompilacji długi czas teraz.</span><span class="sxs-lookup"><span data-stu-id="75f70-117">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="75f70-118">Poprzedniej implementacji wystąpił problem kurczaka jajecznych pakietów, które chcesz rozszerzyć proces kompilacji, ponieważ NuGet przywrócić pakiety podczas kompilowania projektu.</span><span class="sxs-lookup"><span data-stu-id="75f70-118">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="75f70-119">Jednak program MSBuild nie zezwala na rozszerzanie kompilacji podczas kompilacji; co można argumentowało tego problemu w programie MSBuild, ale I argumentowało, że jest to problemu związanego z używaniem.</span><span class="sxs-lookup"><span data-stu-id="75f70-119">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="75f70-120">W zależności od tego, które aspekt należy rozszerzyć może być za późno można zarejestrować do czasu, który zostanie przywrócony do pakietu.</span><span class="sxs-lookup"><span data-stu-id="75f70-120">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="75f70-121">Utrwalenie tego problemu jest upewnienie się, że pakiety zostaną przywrócone jako pierwszy krok w procesie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="75f70-121">The cure to this problem is making sure that packages are restored as the first step in the build process.</span></span> <span data-ttu-id="75f70-122">NuGet 2.7 + ułatwia to uproszczona wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="75f70-122">NuGet 2.7+ makes this easy via a simplified command line:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="75f70-123">Podczas procesu kompilacji przywraca pakiety przed zbudowaniem kod, nie trzeba zaewidencjonowania `.targets` plików</span><span class="sxs-lookup"><span data-stu-id="75f70-123">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="75f70-124">Pakiety musi tworzyć umożliwia ładowanie w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="75f70-124">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="75f70-125">W przeciwnym razie może nadal chcesz zaewidencjonować `.targets` pliki, aby inni deweloperzy mogą po prostu otwórz rozwiązanie, bez konieczności przywrócenia pakietów najpierw.</span><span class="sxs-lookup"><span data-stu-id="75f70-125">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="75f70-126">Następujący projekt pokaz pokazano, jak skonfigurować kompilacji w taki sposób, który `packages` folderów i `.targets` pliki nie muszą mieć zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="75f70-126">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="75f70-127">On również pokazano, jak skonfigurować automatyczne kompilacji w usłudze Team Foundation dla tego projektu próbki.</span><span class="sxs-lookup"><span data-stu-id="75f70-127">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="75f70-128">Struktura repozytorium</span><span class="sxs-lookup"><span data-stu-id="75f70-128">Repository structure</span></span>

<span data-ttu-id="75f70-129">Nasze projektu pokaz to narzędzie proste wiersza polecenia, które używa argumentu wiersza polecenia do zapytania usługi Bing.</span><span class="sxs-lookup"><span data-stu-id="75f70-129">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="75f70-130">Dotyczy programu .NET Framework 4 i używa wielu [pakiety BCL](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), i [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="75f70-130">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="75f70-131">Struktura repozytorium wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="75f70-131">The structure of the repository looks as follows:</span></span>

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

<span data-ttu-id="75f70-132">Widać, że firma Microsoft nie zaewidencjonowania `packages` folderu lub any `.targets` plików.</span><span class="sxs-lookup"><span data-stu-id="75f70-132">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="75f70-133">Firma Microsoft jednak zaewidencjonowania `nuget.exe` jest wymagana podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="75f70-133">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="75f70-134">Następujące powszechnie używane konwencje możemy został zaewidencjonowany w udostępnionej `tools` folderu.</span><span class="sxs-lookup"><span data-stu-id="75f70-134">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="75f70-135">Kod źródłowy jest w obszarze `src` folderu.</span><span class="sxs-lookup"><span data-stu-id="75f70-135">The source code is under the `src` folder.</span></span> <span data-ttu-id="75f70-136">Mimo że nasze pokaz używa tylko pojedyncze rozwiązanie, należy sobie wyobrazić, że ten folder zawiera więcej niż jedno rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="75f70-136">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="75f70-137">Pliki ignorowanych</span><span class="sxs-lookup"><span data-stu-id="75f70-137">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="75f70-138">Obecnie [znaną usterką w kliencie programu NuGet](https://nuget.codeplex.com/workitem/4072) który powoduje, że klient nadal dodawać `packages` folder z kontrolą wersji.</span><span class="sxs-lookup"><span data-stu-id="75f70-138">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="75f70-139">Obejście tego problemu jest wyłączenie integracji kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="75f70-139">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="75f70-140">Aby to zrobić, musisz `Nuget.Config ` w pliku `.nuget` folderu, który jest zbliżony do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="75f70-140">In order to do that, you'll need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="75f70-141">Ten folder nie istnieje, należy go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="75f70-141">If this folder doesn't exist yet, you'll need to create it.</span></span> <span data-ttu-id="75f70-142">W [ `Nuget.Config` ](../consume-packages/configuring-nuget-behavior.md), dodaj następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="75f70-142">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="75f70-143">Do komunikowania się do systemu kontroli wersji, że firma Microsoft nie opcje do wyboru w **pakiety** folderów, również po dodaniu ignorowania plików dla obu git (`.gitignore`) oraz TF kontroli wersji (`.tfignore`).</span><span class="sxs-lookup"><span data-stu-id="75f70-143">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="75f70-144">Te pliki w tym artykule opisano wzorców plików, których nie chcesz do zaewidencjonowania.</span><span class="sxs-lookup"><span data-stu-id="75f70-144">These files describes patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="75f70-145">`.gitignore` Pliku wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="75f70-145">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages

<span data-ttu-id="75f70-146">`.gitignore` Plik jest [bardzo zaawansowane](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="75f70-146">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="75f70-147">Na przykład, jeśli chcesz zazwyczaj nie zaewidencjonowania zawartość `packages` folder, ale chcesz przejść z poprzednich wskazówek kontroli `.targets` plików może mieć następujące reguły, zamiast tego:</span><span class="sxs-lookup"><span data-stu-id="75f70-147">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="75f70-148">To powoduje wyłączenie wszystkich `packages` folderów jednak zostanie ponownie obejmują wszystkie zawarte `.targets` plików.</span><span class="sxs-lookup"><span data-stu-id="75f70-148">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="75f70-149">W systemie można znaleźć szablonu dla `.gitignore` pliki, które jest w szczególny sposób dopasowane do potrzeb deweloperów programu Visual Studio [tutaj](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="75f70-149">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="75f70-150">Kontrola wersji TF obsługuje mechanizm bardzo podobne za pośrednictwem [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) pliku.</span><span class="sxs-lookup"><span data-stu-id="75f70-150">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="75f70-151">Składnia jest praktycznie:</span><span class="sxs-lookup"><span data-stu-id="75f70-151">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages

## <a name="buildproj"></a><span data-ttu-id="75f70-152">build.proj</span><span class="sxs-lookup"><span data-stu-id="75f70-152">build.proj</span></span>

<span data-ttu-id="75f70-153">W naszym pokaz możemy przechowywać proces kompilacji dość proste.</span><span class="sxs-lookup"><span data-stu-id="75f70-153">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="75f70-154">Utworzymy projektu MSBuild, która tworzy wszystkie rozwiązania oraz zapewnienie, że pakiety są przywracane przed kompilacją rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="75f70-154">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="75f70-155">Ten projekt będzie mieć trzy obiektów docelowych z konwencjonalnej `Clean`, `Build` i `Rebuild` oraz nowy cel `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="75f70-155">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="75f70-156">`Build` i `Rebuild` zależą od obiektów docelowych `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="75f70-156">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="75f70-157">Dzięki temu, że można jednocześnie uruchomić `Build` i `Rebuild` i zależne od pakietów przywracana.</span><span class="sxs-lookup"><span data-stu-id="75f70-157">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="75f70-158">`Clean`, `Build` i `Rebuild` wywołania odpowiedniego docelowego MSBuild we wszystkich plikach w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="75f70-158">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="75f70-159">`RestorePackages` Wywołuje docelowej `nuget.exe` dla każdego pliku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="75f70-159">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="75f70-160">Jest to zrobić za pomocą [MSBuild na przetwarzanie wsadowe funkcji](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="75f70-160">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="75f70-161">Wynik wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="75f70-161">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="75f70-162">Konfigurowanie kompilację zespołową</span><span class="sxs-lookup"><span data-stu-id="75f70-162">Configuring Team Build</span></span>

<span data-ttu-id="75f70-163">Team Build oferuje różne szablony procesu.</span><span class="sxs-lookup"><span data-stu-id="75f70-163">Team Build offers various process templates.</span></span> <span data-ttu-id="75f70-164">Dla tej prezentacji firma Microsoft korzysta z programu Team Foundation Service.</span><span class="sxs-lookup"><span data-stu-id="75f70-164">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="75f70-165">Jednak w przypadku instalacji lokalnych programu TFS będzie bardzo podobne.</span><span class="sxs-lookup"><span data-stu-id="75f70-165">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="75f70-166">Git i kontroli wersji TF ma różnych szablonów Team Build, czynności będą się różnić w zależności od systemu kontroli wersji, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="75f70-166">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="75f70-167">W obu przypadkach należy wybiera build.proj jako projekt, który chcesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="75f70-167">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="75f70-168">Po pierwsze Przyjrzyjmy się szablon procesu git.</span><span class="sxs-lookup"><span data-stu-id="75f70-168">First, let's look at the process template for git.</span></span> <span data-ttu-id="75f70-169">W szablonie git na podstawie wybrano kompilacji za pomocą właściwości `Solution to build`:</span><span class="sxs-lookup"><span data-stu-id="75f70-169">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Proces kompilacji dla git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="75f70-171">Należy pamiętać, że ta właściwość jest lokalizacja w repozytorium.</span><span class="sxs-lookup"><span data-stu-id="75f70-171">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="75f70-172">Ponieważ naszych `build.proj` jest w folderze głównym, po prostu użyliśmy `build.proj`.</span><span class="sxs-lookup"><span data-stu-id="75f70-172">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="75f70-173">Jeśli plik kompilacji zostanie umieszczony w folderze o nazwie `tools`, wartość będzie wynosić `tools\build.proj`.</span><span class="sxs-lookup"><span data-stu-id="75f70-173">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="75f70-174">W szablonie kontroli wersji TF projekt jest wybrany za pomocą właściwości `Projects`:</span><span class="sxs-lookup"><span data-stu-id="75f70-174">In the TF version control template the project is selected via the property `Projects`:</span></span>

![Proces kompilacji dla programu TFVC](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="75f70-176">W przeciwieństwie do narzędzia git, na podstawie szablonu TF kontroli wersji obsługuje wyboru (przycisk z wielokropkiem po prawej stronie).</span><span class="sxs-lookup"><span data-stu-id="75f70-176">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="75f70-177">Dlatego w celu uniknięcia błędów pisowni Sugerujemy użyć do wybrania projektu.</span><span class="sxs-lookup"><span data-stu-id="75f70-177">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>