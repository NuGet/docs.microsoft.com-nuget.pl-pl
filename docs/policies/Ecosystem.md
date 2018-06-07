---
title: Omówienie ekosystemu NuGet
description: Kompleksowe zasoby w ekosystemie NuGet, w tym źródeł NuGet, Microsoft NuGet projektów, narzędzia i materiałów szkoleniowych.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 52edc29fe8e9ec8927844a71a01e4983e47b1ce0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818181"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a><span data-ttu-id="ece85-103">Omówienie ekosystemu NuGet</span><span class="sxs-lookup"><span data-stu-id="ece85-103">An overview of the NuGet ecosystem</span></span>

<span data-ttu-id="ece85-104">Ponieważ chodzi o wprowadzenie w 2010, NuGet ma przedstawione dużą możliwość poprawić i zautomatyzować różnych aspektów procesami programowania.</span><span class="sxs-lookup"><span data-stu-id="ece85-104">Since it's introduction in 2010, NuGet has presented a great opportunity to improve and automate different aspects of the development processes.</span></span>

<span data-ttu-id="ece85-105">Ponieważ NuGet jest typu open source podlegający ograniczająca [licencji Apache w wersji 2](http://choosealicense.com/licenses/apache/), mogą korzystać z innych projektów NuGet i przedsiębiorstwa mogą tworzyć obsługę w swoich produktach.</span><span class="sxs-lookup"><span data-stu-id="ece85-105">Because NuGet is open source under a permissive [Apache v2 license](http://choosealicense.com/licenses/apache/), other projects can leverage NuGet and companies can build support for it in their products.</span></span> <span data-ttu-id="ece85-106">NuGet i inne aplikacje zbudowane na i wokół NuGet dla projektów open source lub rozwoju aplikacji przedsiębiorstwa, podaj szerokim ekosystemem narzędzi dla poprawy z procesem tworzenia oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="ece85-106">Whether for open-source projects or enterprise application development, NuGet and other applications built on and around NuGet provide a broad ecosystem of tools for improving your software development process.</span></span>

<span data-ttu-id="ece85-107">Wszystkie te projekty mogą innowacji z powodu wkładów developer.</span><span class="sxs-lookup"><span data-stu-id="ece85-107">All of these projects are able to innovate because of developer contributions.</span></span> <span data-ttu-id="ece85-108">Tak samo, jak współtworzyć NuGet samego, również przyczynić się do tych projektów wady raportowania i nowe pomysły funkcji zwrotnych, pisanie dokumentacji i współtworzenia kodu, gdy jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="ece85-108">Just as you contribute to NuGet itself, also make contribution to these projects by reporting defects and new feature ideas, providing feedback, writing documentation, and contributing code where possible.</span></span>

## <a name="net-foundation-projects"></a><span data-ttu-id="ece85-109">Projekty .NET foundation</span><span class="sxs-lookup"><span data-stu-id="ece85-109">.NET Foundation projects</span></span>

<span data-ttu-id="ece85-110">NuGet zapewnia system zarządzania pakiet wolnego typu open source platformy programistycznej Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ece85-110">NuGet provides a free, open source package management system for the Microsoft development platform.</span></span> <span data-ttu-id="ece85-111">Składa się z kilku narzędzi klienta, a także zestaw usług wchodzących w skład [oficjalnego galerii NuGet](http://www.nuget.org).</span><span class="sxs-lookup"><span data-stu-id="ece85-111">It consists of a few client tools as well as the set of services that comprise the [official NuGet Gallery](http://www.nuget.org).</span></span> <span data-ttu-id="ece85-112">Połączone, te tworzą projektu NuGet, który podlega [.NET Foundation](http://www.dotnetfoundation.org/).</span><span class="sxs-lookup"><span data-stu-id="ece85-112">Combined, these form the NuGet project which is governed by the [.NET Foundation](http://www.dotnetfoundation.org/).</span></span>

<span data-ttu-id="ece85-113">Organizacja NuGet zawiera różne repozytoria w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="ece85-113">The NuGet Organization contains various repositories on GitHub.</span></span> <span data-ttu-id="ece85-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) Zawiera omówienie wszystkie repozytoria i gdzie można znaleźć różne składniki NuGet.</span><span class="sxs-lookup"><span data-stu-id="ece85-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) gives an overview of all the repositories and where to find the various NuGet components.</span></span>

## <a name="microsoft-projects"></a><span data-ttu-id="ece85-115">Projekty Microsoft</span><span class="sxs-lookup"><span data-stu-id="ece85-115">Microsoft projects</span></span>

<span data-ttu-id="ece85-116">Microsoft przyczynił się często do tworzenia programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="ece85-116">Microsoft has contributed extensively to the development of NuGet.</span></span> <span data-ttu-id="ece85-117">Wszystkie wkład pracowników firmy Microsoft są także otworzyć źródła i przekazywana (w tym prawa autorskie) .NET Foundation.</span><span class="sxs-lookup"><span data-stu-id="ece85-117">All contributions made by Microsoft employees are also open source and are donated (including copyrights) to the .NET Foundation.</span></span>

## <a name="non-microsoft-projects"></a><span data-ttu-id="ece85-118">Projekty inne niż firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="ece85-118">Non-Microsoft projects</span></span>

<span data-ttu-id="ece85-119">Wiele osób i firm dokonano znaczących wkładów ekosystemem NuGet.</span><span class="sxs-lookup"><span data-stu-id="ece85-119">Many other individuals and companies have made significant contributions to the NuGet ecosystem.</span></span> <span data-ttu-id="ece85-120">Każdy projekt wymienione w tym miejscu może mieć licencję innego niż podstawowe składniki NuGet, aby potwierdzić, że postanowienia licencyjne są dopuszczalne przed użyciem:</span><span class="sxs-lookup"><span data-stu-id="ece85-120">Each project listed here may have a different license than the core NuGet components, so confirm that the license terms are acceptable prior to use:</span></span>

- [<span data-ttu-id="ece85-121">AppVeyor elementu konfiguracji</span><span class="sxs-lookup"><span data-stu-id="ece85-121">AppVeyor CI</span></span>](https://www.appveyor.com/)
- [<span data-ttu-id="ece85-122">Artifactory</span><span class="sxs-lookup"><span data-stu-id="ece85-122">Artifactory</span></span>](https://www.jfrog.com/artifactory/)
- [<span data-ttu-id="ece85-123">BoxStarter</span><span class="sxs-lookup"><span data-stu-id="ece85-123">BoxStarter</span></span>](http://boxstarter.org/)
- [<span data-ttu-id="ece85-124">Chocolatey</span><span class="sxs-lookup"><span data-stu-id="ece85-124">Chocolatey</span></span>](https://chocolatey.org/)
- [<span data-ttu-id="ece85-125">CoApp</span><span class="sxs-lookup"><span data-stu-id="ece85-125">CoApp</span></span>](http://coapp.org/)
- [<span data-ttu-id="ece85-126">JetBrains ReSharper</span><span class="sxs-lookup"><span data-stu-id="ece85-126">JetBrains ReSharper</span></span>](https://resharper-plugins.jetbrains.com/)
- [<span data-ttu-id="ece85-127">JetBrains TeamCity</span><span class="sxs-lookup"><span data-stu-id="ece85-127">JetBrains TeamCity</span></span>](https://www.jetbrains.com/teamcity/)
- [<span data-ttu-id="ece85-128">Klondike</span><span class="sxs-lookup"><span data-stu-id="ece85-128">Klondike</span></span>](https://github.com/themotleyfool/Klondike)
- [<span data-ttu-id="ece85-129">MinimalNugetServer</span><span class="sxs-lookup"><span data-stu-id="ece85-129">MinimalNugetServer</span></span>](https://github.com/TanukiSharp/MinimalNugetServer)
- [<span data-ttu-id="ece85-130">MyGet (lub NuGet jako usługa)</span><span class="sxs-lookup"><span data-stu-id="ece85-130">MyGet (or NuGet-as-a-service)</span></span>](http://www.myget.org/)
- [<span data-ttu-id="ece85-131">NuGet Package Explorer</span><span class="sxs-lookup"><span data-stu-id="ece85-131">NuGet Package Explorer</span></span>](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [<span data-ttu-id="ece85-132">NuGet Server</span><span class="sxs-lookup"><span data-stu-id="ece85-132">NuGet Server</span></span>](http://nugetserver.net/)
- [<span data-ttu-id="ece85-133">OctopusDeploy</span><span class="sxs-lookup"><span data-stu-id="ece85-133">OctopusDeploy</span></span>](https://octopus.com/)
- [<span data-ttu-id="ece85-134">Paket</span><span class="sxs-lookup"><span data-stu-id="ece85-134">Paket</span></span>](https://fsprojects.github.io/Paket/)
- [<span data-ttu-id="ece85-135">ProGet (Inedo)</span><span class="sxs-lookup"><span data-stu-id="ece85-135">ProGet (Inedo)</span></span>](http://inedo.com/proget)
- [<span data-ttu-id="ece85-136">scriptcs</span><span class="sxs-lookup"><span data-stu-id="ece85-136">scriptcs</span></span>](http://scriptcs.net/)
- [<span data-ttu-id="ece85-137">SharpDevelop</span><span class="sxs-lookup"><span data-stu-id="ece85-137">SharpDevelop</span></span>](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [<span data-ttu-id="ece85-138">Sonatype węzła</span><span class="sxs-lookup"><span data-stu-id="ece85-138">Sonatype Nexus</span></span>](http://www.sonatype.com/nexus-repository-sonatype)
- [<span data-ttu-id="ece85-139">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="ece85-139">SymbolSource</span></span>](http://www.symbolsource.org/Public)
- [<span data-ttu-id="ece85-140">Xamarin i MonoDevelop</span><span class="sxs-lookup"><span data-stu-id="ece85-140">Xamarin and MonoDevelop</span></span>](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a><span data-ttu-id="ece85-141">Inne narzędzia oparte na NuGet</span><span class="sxs-lookup"><span data-stu-id="ece85-141">Other NuGet-based utilities</span></span>

<span data-ttu-id="ece85-142">Są to narzędzi oparty na NuGet:</span><span class="sxs-lookup"><span data-stu-id="ece85-142">These are tools and utilities built on NuGet:</span></span>

- <span data-ttu-id="ece85-143">[Glimpse rozszerzenia](http://getglimpse.com/Packages) (dodatki plug-in są pakiety)</span><span class="sxs-lookup"><span data-stu-id="ece85-143">[Glimpse Extensions](http://getglimpse.com/Packages) (plug-ins are packages)</span></span>
- [<span data-ttu-id="ece85-144">NuGetMustHaves.com</span><span class="sxs-lookup"><span data-stu-id="ece85-144">NuGetMustHaves.com</span></span>](http://nugetmusthaves.com/)
- <span data-ttu-id="ece85-145">[Orchard](http://www.orchardproject.net/) (modułów CMS pobrane z v1 NuGet źródła danych obsługiwane galerii Orchard)</span><span class="sxs-lookup"><span data-stu-id="ece85-145">[Orchard](http://www.orchardproject.net/) (CMS modules are fetched from a v1 NuGet feed hosted in the Orchard Gallery)</span></span>
- [<span data-ttu-id="ece85-146">Środowisko Java NuGet serwera</span><span class="sxs-lookup"><span data-stu-id="ece85-146">Java implementation of NuGet Server</span></span>](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- <span data-ttu-id="ece85-147">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting nowy pakiet publikacji)</span><span class="sxs-lookup"><span data-stu-id="ece85-147">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting new package publications)</span></span>
- <span data-ttu-id="ece85-148">[DefinitelyTyped](http://definitelytyped.org/) ([automatyczne](https://github.com/DefinitelyTyped/NugetAutomation/) typu TypeScript [definicje opublikowane NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))</span><span class="sxs-lookup"><span data-stu-id="ece85-148">[DefinitelyTyped](http://definitelytyped.org/) ([Automatic](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Type [Definitions published to NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))</span></span>

## <a name="training-materials-and-references"></a><span data-ttu-id="ece85-149">Aktualizowanie materiałów szkoleniowych i odwołań</span><span class="sxs-lookup"><span data-stu-id="ece85-149">Training materials and references</span></span>

<span data-ttu-id="ece85-150">Za pomocą nowego narzędzia lub technologii zwykle zawiera naukę.</span><span class="sxs-lookup"><span data-stu-id="ece85-150">Using a new tool or technology usually comes with a learning curve.</span></span> <span data-ttu-id="ece85-151">Szczęście NuGet, ma problemy z ich opanowaniem nauki krzywą wszystko!</span><span class="sxs-lookup"><span data-stu-id="ece85-151">Luckily for you, NuGet has no steep learning curve it all!</span></span> <span data-ttu-id="ece85-152">W rzeczywistości, każdy użytkownik może [rozpocząć korzystanie z pakietów](../quickstart/use-a-package.md) szybko.</span><span class="sxs-lookup"><span data-stu-id="ece85-152">In fact, anyone can [get started consuming packages](../quickstart/use-a-package.md) quickly.</span></span>

<span data-ttu-id="ece85-153">Który powiedział, tworzenie pakietów — i szczególnie dobre pakiety — wraz z obejmujący NuGet w zautomatyzowanych procesów kompilacji i wdrożenia, wymaga nieco więcej czasu z następującymi zasobami wydatków:</span><span class="sxs-lookup"><span data-stu-id="ece85-153">That said, authoring packages–and especially good packages–along with  embracing NuGet in automated build and deployment processes, requires spending a little more time with the following resources:</span></span>

- [<span data-ttu-id="ece85-154">NuGet Blog</span><span class="sxs-lookup"><span data-stu-id="ece85-154">NuGet Blog</span></span>](http://blog.nuget.org/)
- [<span data-ttu-id="ece85-155">Zespół NuGet w serwisie Twitter, @nuget</span><span class="sxs-lookup"><span data-stu-id="ece85-155">NuGet team on Twitter, @nuget</span></span>](http://twitter.com/nuget)
- <span data-ttu-id="ece85-156">Książki:</span><span class="sxs-lookup"><span data-stu-id="ece85-156">Books:</span></span>
  - [<span data-ttu-id="ece85-157">NuGet Apress Pro</span><span class="sxs-lookup"><span data-stu-id="ece85-157">Apress Pro NuGet</span></span>](http://bit.ly/ProNuGet)
  - [<span data-ttu-id="ece85-158">NuGet 2 Essentials</span><span class="sxs-lookup"><span data-stu-id="ece85-158">NuGet 2 Essentials</span></span>](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a><span data-ttu-id="ece85-159">Dokumentacja dla poszczególnych pakietów</span><span class="sxs-lookup"><span data-stu-id="ece85-159">Documentation for individual packages</span></span>

<span data-ttu-id="ece85-160">[NuDoq](http://nudoq.org) zawiera proste dostępu, aktualizacji i dokumentację dla pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="ece85-160">[NuDoq](http://nudoq.org) provides straightforward access and updates and documentation for NuGet packages.</span></span>

<span data-ttu-id="ece85-161">NuDoq regularnie odpytuje serwer galerii nuget.org najnowsze aktualizacje pakietu, wypakowuje przetwarza pliki dokumentacji biblioteki i odpowiednio aktualizację w lokacji.</span><span class="sxs-lookup"><span data-stu-id="ece85-161">NuDoq regularly polls the nuget.org gallery server for the latest package updates, unpacks and processes the library documentation files, and updates the site accordingly.</span></span>

## <a name="adding-your-project"></a><span data-ttu-id="ece85-162">Dodawanie projektu</span><span class="sxs-lookup"><span data-stu-id="ece85-162">Adding your project</span></span>

<span data-ttu-id="ece85-163">Jeśli masz projektu ekosystem NuGet, która byłaby cenne dodanie do tej strony, Prześlij żądanie ściągnięcia edycji do tej strony.</span><span class="sxs-lookup"><span data-stu-id="ece85-163">If you have a NuGet ecosystem project that would be a valuable addition to this page, please  submit a pull request with an edit to this page.</span></span>
