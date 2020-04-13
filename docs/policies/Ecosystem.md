---
title: Omówienie ekosystemu NuGet
description: Kompleksowe zasoby w ekosystemie NuGet, w tym źródła NuGet, projekty nuget firmy innych niż Microsoft, narzędzia i materiały szkoleniowe.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 31243076f36f6ff274c4377c1773ea59dda8c834
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495504"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a><span data-ttu-id="cd14d-103">Omówienie ekosystemu NuGet</span><span class="sxs-lookup"><span data-stu-id="cd14d-103">An overview of the NuGet ecosystem</span></span>

<span data-ttu-id="cd14d-104">Od czasu wprowadzenia w 2010 r. NuGet przedstawił wielką szansę na ulepszenie i automatyzację różnych aspektów procesów programisty.</span><span class="sxs-lookup"><span data-stu-id="cd14d-104">Since it's introduction in 2010, NuGet has presented a great opportunity to improve and automate different aspects of the development processes.</span></span>

<span data-ttu-id="cd14d-105">Ponieważ NuGet jest open source w ramach licencji [apache apache v2,](http://choosealicense.com/licenses/apache/)inne projekty mogą korzystać NuGet i firmy mogą budować wsparcie dla niego w swoich produktach.</span><span class="sxs-lookup"><span data-stu-id="cd14d-105">Because NuGet is open source under a permissive [Apache v2 license](http://choosealicense.com/licenses/apache/), other projects can leverage NuGet and companies can build support for it in their products.</span></span> <span data-ttu-id="cd14d-106">Niezależnie od tego, czy chodzi o projekty typu open source, czy o tworzenie aplikacji w przedsiębiorstwie, NuGet i inne aplikacje oparte na nuget i wokół niego zapewniają szeroki ekosystem narzędzi do ulepszania procesu tworzenia oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="cd14d-106">Whether for open-source projects or enterprise application development, NuGet and other applications built on and around NuGet provide a broad ecosystem of tools for improving your software development process.</span></span>

<span data-ttu-id="cd14d-107">Wszystkie te projekty są w stanie wprowadzać innowacje dzięki wkładowi deweloperów.</span><span class="sxs-lookup"><span data-stu-id="cd14d-107">All of these projects are able to innovate because of developer contributions.</span></span> <span data-ttu-id="cd14d-108">Podobnie jak przyczyniasz się do NuGet się, również przyczynić się do tych projektów, zgłaszając wady i nowe pomysły funkcji, dostarczanie opinii, pisanie dokumentacji i przyczyniając się do kodu, gdzie to możliwe.</span><span class="sxs-lookup"><span data-stu-id="cd14d-108">Just as you contribute to NuGet itself, also make contribution to these projects by reporting defects and new feature ideas, providing feedback, writing documentation, and contributing code where possible.</span></span>

## <a name="net-foundation-projects"></a><span data-ttu-id="cd14d-109">Projekty Fundacji .NET</span><span class="sxs-lookup"><span data-stu-id="cd14d-109">.NET Foundation projects</span></span>

<span data-ttu-id="cd14d-110">NuGet zapewnia bezpłatny system zarządzania pakietami open source dla platformy dewelopera firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cd14d-110">NuGet provides a free, open source package management system for the Microsoft development platform.</span></span> <span data-ttu-id="cd14d-111">Składa się z kilku narzędzi klienta, a także zestaw usług, które składają się na [oficjalnej Galerii NuGet](http://www.nuget.org).</span><span class="sxs-lookup"><span data-stu-id="cd14d-111">It consists of a few client tools as well as the set of services that comprise the [official NuGet Gallery](http://www.nuget.org).</span></span> <span data-ttu-id="cd14d-112">Połączone tworzą projekt NuGet, który jest zarządzany przez [.NET Foundation](http://www.dotnetfoundation.org/).</span><span class="sxs-lookup"><span data-stu-id="cd14d-112">Combined, these form the NuGet project which is governed by the [.NET Foundation](http://www.dotnetfoundation.org/).</span></span>

<span data-ttu-id="cd14d-113">Organizacja NuGet zawiera różne repozytoria w usłudze GitHub.</span><span class="sxs-lookup"><span data-stu-id="cd14d-113">The NuGet Organization contains various repositories on GitHub.</span></span> <span data-ttu-id="cd14d-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home)zawiera przegląd wszystkich repozytoriów i gdzie można znaleźć różne składniki NuGet.</span><span class="sxs-lookup"><span data-stu-id="cd14d-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) gives an overview of all the repositories and where to find the various NuGet components.</span></span>

## <a name="microsoft-projects"></a><span data-ttu-id="cd14d-115">Projekty firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="cd14d-115">Microsoft projects</span></span>

<span data-ttu-id="cd14d-116">Firma Microsoft w znacznym stopniu przyczyniła się do rozwoju NuGet.</span><span class="sxs-lookup"><span data-stu-id="cd14d-116">Microsoft has contributed extensively to the development of NuGet.</span></span> <span data-ttu-id="cd14d-117">Wszystkie wkłady pracowników firmy Microsoft są również open source i są przekazywane (w tym prawa autorskie) do .NET Foundation.</span><span class="sxs-lookup"><span data-stu-id="cd14d-117">All contributions made by Microsoft employees are also open source and are donated (including copyrights) to the .NET Foundation.</span></span>

## <a name="non-microsoft-projects"></a><span data-ttu-id="cd14d-118">Projekty inne niż Microsoft</span><span class="sxs-lookup"><span data-stu-id="cd14d-118">Non-Microsoft projects</span></span>

<span data-ttu-id="cd14d-119">Wiele innych osób i firm wniósł znaczący wkład w ekosystem NuGet.</span><span class="sxs-lookup"><span data-stu-id="cd14d-119">Many other individuals and companies have made significant contributions to the NuGet ecosystem.</span></span> <span data-ttu-id="cd14d-120">Każdy projekt wymieniony w tym miejscu może mieć inną licencję niż podstawowe składniki NuGet, więc upewnij się, że postanowienia licencyjne są dopuszczalne przed użyciem:</span><span class="sxs-lookup"><span data-stu-id="cd14d-120">Each project listed here may have a different license than the core NuGet components, so confirm that the license terms are acceptable prior to use:</span></span>

- [<span data-ttu-id="cd14d-121">AppVeyor CI</span><span class="sxs-lookup"><span data-stu-id="cd14d-121">AppVeyor CI</span></span>](https://www.appveyor.com/)
- [<span data-ttu-id="cd14d-122">Artefakty</span><span class="sxs-lookup"><span data-stu-id="cd14d-122">Artifactory</span></span>](https://www.jfrog.com/artifactory/)
- [<span data-ttu-id="cd14d-123">BoxStarter (Początek skrzynki)</span><span class="sxs-lookup"><span data-stu-id="cd14d-123">BoxStarter</span></span>](http://boxstarter.org/)
- [<span data-ttu-id="cd14d-124">Czekoladowy</span><span class="sxs-lookup"><span data-stu-id="cd14d-124">Chocolatey</span></span>](https://chocolatey.org/)
- [<span data-ttu-id="cd14d-125">CoApp (CoApp)</span><span class="sxs-lookup"><span data-stu-id="cd14d-125">CoApp</span></span>](http://coapp.org/)
- [<span data-ttu-id="cd14d-126">Żywiciele JetBrains</span><span class="sxs-lookup"><span data-stu-id="cd14d-126">JetBrains ReSharper</span></span>](https://resharper-plugins.jetbrains.com/)
- [<span data-ttu-id="cd14d-127">JetBrains TeamCity</span><span class="sxs-lookup"><span data-stu-id="cd14d-127">JetBrains TeamCity</span></span>](https://www.jetbrains.com/teamcity/)
- [<span data-ttu-id="cd14d-128">Klondike</span><span class="sxs-lookup"><span data-stu-id="cd14d-128">Klondike</span></span>](https://github.com/themotleyfool/Klondike)
- [<span data-ttu-id="cd14d-129">MinimalNugetServer (MinimalNugetServer)</span><span class="sxs-lookup"><span data-stu-id="cd14d-129">MinimalNugetServer</span></span>](https://github.com/TanukiSharp/MinimalNugetServer)
- [<span data-ttu-id="cd14d-130">MyGet (lub NuGet-as-a-service)</span><span class="sxs-lookup"><span data-stu-id="cd14d-130">MyGet (or NuGet-as-a-service)</span></span>](http://www.myget.org/)
- [<span data-ttu-id="cd14d-131">Eksplorator pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="cd14d-131">NuGet Package Explorer</span></span>](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [<span data-ttu-id="cd14d-132">Serwer NuGet</span><span class="sxs-lookup"><span data-stu-id="cd14d-132">NuGet Server</span></span>](http://nugetserver.net/)
- [<span data-ttu-id="cd14d-133">OśmiornicaDeploy</span><span class="sxs-lookup"><span data-stu-id="cd14d-133">OctopusDeploy</span></span>](https://octopus.com/)
- [<span data-ttu-id="cd14d-134">Paket (paket)</span><span class="sxs-lookup"><span data-stu-id="cd14d-134">Paket</span></span>](https://fsprojects.github.io/Paket/)
- [<span data-ttu-id="cd14d-135">ProGet (Inedo)</span><span class="sxs-lookup"><span data-stu-id="cd14d-135">ProGet (Inedo)</span></span>](http://inedo.com/proget)
- [<span data-ttu-id="cd14d-136">skrypty</span><span class="sxs-lookup"><span data-stu-id="cd14d-136">scriptcs</span></span>](http://scriptcs.net/)
- [<span data-ttu-id="cd14d-137">Sharpdevelop</span><span class="sxs-lookup"><span data-stu-id="cd14d-137">SharpDevelop</span></span>](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [<span data-ttu-id="cd14d-138">Sonatype Nexus</span><span class="sxs-lookup"><span data-stu-id="cd14d-138">Sonatype Nexus</span></span>](http://www.sonatype.com/nexus-repository-sonatype)
- [<span data-ttu-id="cd14d-139">Źródło symbolu</span><span class="sxs-lookup"><span data-stu-id="cd14d-139">SymbolSource</span></span>](http://www.symbolsource.org/Public)
- [<span data-ttu-id="cd14d-140">Xamarin i MonoDevelop</span><span class="sxs-lookup"><span data-stu-id="cd14d-140">Xamarin and MonoDevelop</span></span>](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a><span data-ttu-id="cd14d-141">Inne narzędzia oparte na nuget</span><span class="sxs-lookup"><span data-stu-id="cd14d-141">Other NuGet-based utilities</span></span>

<span data-ttu-id="cd14d-142">Są to narzędzia i narzędzia zbudowane na NuGet:</span><span class="sxs-lookup"><span data-stu-id="cd14d-142">These are tools and utilities built on NuGet:</span></span>

- <span data-ttu-id="cd14d-143">[Rozszerzenia Glimpse](http://getglimpse.com/Packages) (wtyczki to pakiety)</span><span class="sxs-lookup"><span data-stu-id="cd14d-143">[Glimpse Extensions](http://getglimpse.com/Packages) (plug-ins are packages)</span></span>
- [<span data-ttu-id="cd14d-144">NuGetMustHaves.com</span><span class="sxs-lookup"><span data-stu-id="cd14d-144">NuGetMustHaves.com</span></span>](http://nugetmusthaves.com/)
- <span data-ttu-id="cd14d-145">[Sad](http://www.orchardproject.net/) (moduły CMS są pobierane z kanału NuGet w wersji 1 hostowanego w Galerii Sadów)</span><span class="sxs-lookup"><span data-stu-id="cd14d-145">[Orchard](http://www.orchardproject.net/) (CMS modules are fetched from a v1 NuGet feed hosted in the Orchard Gallery)</span></span>
- [<span data-ttu-id="cd14d-146">Implementacja języka Java serwera NuGet Server</span><span class="sxs-lookup"><span data-stu-id="cd14d-146">Java implementation of NuGet Server</span></span>](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- <span data-ttu-id="cd14d-147">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting nowych publikacji pakiet)</span><span class="sxs-lookup"><span data-stu-id="cd14d-147">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting new package publications)</span></span>
- <span data-ttu-id="cd14d-148">[DefinitelyTyped](http://definitelytyped.org/) ([Automatyczne](https://github.com/DefinitelyTyped/NugetAutomation/) [definicje](http://www.nuget.org/packages?q=DefinitelyTyped)typuScript opublikowane w NuGet )</span><span class="sxs-lookup"><span data-stu-id="cd14d-148">[DefinitelyTyped](http://definitelytyped.org/) ([Automatic](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Type [Definitions published to NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))</span></span>

## <a name="training-materials-and-references"></a><span data-ttu-id="cd14d-149">Materiały szkoleniowe i referencje</span><span class="sxs-lookup"><span data-stu-id="cd14d-149">Training materials and references</span></span>

<span data-ttu-id="cd14d-150">Korzystanie z nowego narzędzia lub technologii zwykle wiąże się z krzywą uczenia się.</span><span class="sxs-lookup"><span data-stu-id="cd14d-150">Using a new tool or technology usually comes with a learning curve.</span></span> <span data-ttu-id="cd14d-151">Na szczęście dla Ciebie, NuGet nie ma stromej krzywej uczenia się to wszystko!</span><span class="sxs-lookup"><span data-stu-id="cd14d-151">Luckily for you, NuGet has no steep learning curve it all!</span></span> <span data-ttu-id="cd14d-152">W rzeczywistości każdy może [szybko zacząć konsumować pakiety.](../quickstart/use-a-package.md)</span><span class="sxs-lookup"><span data-stu-id="cd14d-152">In fact, anyone can [get started consuming packages](../quickstart/use-a-package.md) quickly.</span></span>

<span data-ttu-id="cd14d-153">To powiedziawszy, tworzenie pakietów, a zwłaszcza dobre pakiety, wraz z obejmując NuGet w zautomatyzowanych procesów kompilacji i wdrażania, wymaga spędzenia trochę więcej czasu z następujących zasobów:</span><span class="sxs-lookup"><span data-stu-id="cd14d-153">That said, authoring packages–and especially good packages–along with  embracing NuGet in automated build and deployment processes, requires spending a little more time with the following resources:</span></span>

- [<span data-ttu-id="cd14d-154">NuGet Blog</span><span class="sxs-lookup"><span data-stu-id="cd14d-154">NuGet Blog</span></span>](http://blog.nuget.org/)
- [<span data-ttu-id="cd14d-155">Zespół NuGet na Twitterze,@nuget</span><span class="sxs-lookup"><span data-stu-id="cd14d-155">NuGet team on Twitter, @nuget</span></span>](http://twitter.com/nuget)
- <span data-ttu-id="cd14d-156">Książki:</span><span class="sxs-lookup"><span data-stu-id="cd14d-156">Books:</span></span>
  - [<span data-ttu-id="cd14d-157">Apress Pro NuGet</span><span class="sxs-lookup"><span data-stu-id="cd14d-157">Apress Pro NuGet</span></span>](http://bit.ly/ProNuGet)
  - [<span data-ttu-id="cd14d-158">NuGet 2 Podstawowe elementy</span><span class="sxs-lookup"><span data-stu-id="cd14d-158">NuGet 2 Essentials</span></span>](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a><span data-ttu-id="cd14d-159">Dokumentacja dla poszczególnych opakowań</span><span class="sxs-lookup"><span data-stu-id="cd14d-159">Documentation for individual packages</span></span>

<span data-ttu-id="cd14d-160">[NuDoq](http://nudoq.org) zapewnia prosty dostęp i aktualizacje i dokumentację dla pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="cd14d-160">[NuDoq](http://nudoq.org) provides straightforward access and updates and documentation for NuGet packages.</span></span>

<span data-ttu-id="cd14d-161">NuDoq regularnie sonduje serwer galerii nuget.org w celu uzyskania najnowszych aktualizacji pakietów, rozpakowuje i przetwarza pliki dokumentacji biblioteki oraz odpowiednio aktualizuje witrynę.</span><span class="sxs-lookup"><span data-stu-id="cd14d-161">NuDoq regularly polls the nuget.org gallery server for the latest package updates, unpacks and processes the library documentation files, and updates the site accordingly.</span></span>

## <a name="adding-your-project"></a><span data-ttu-id="cd14d-162">Dodawanie projektu</span><span class="sxs-lookup"><span data-stu-id="cd14d-162">Adding your project</span></span>

<span data-ttu-id="cd14d-163">Jeśli masz projekt ekosystemu NuGet, który byłby cennym dodatkiem do tej strony, prześlij żądanie ściągnięcia z edycją na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="cd14d-163">If you have a NuGet ecosystem project that would be a valuable addition to this page, please  submit a pull request with an edit to this page.</span></span>
