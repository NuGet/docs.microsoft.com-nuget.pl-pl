---
title: Omówienie ekosystemu NuGet
description: Komplet materiałów należący do ekosystemu NuGet, w tym źródeł NuGet, projekty NuGet firmy Microsoft, narzędzi i materiałów szkoleniowych.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 31243076f36f6ff274c4377c1773ea59dda8c834
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548147"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a><span data-ttu-id="cabfb-103">Omówienie ekosystemu NuGet</span><span class="sxs-lookup"><span data-stu-id="cabfb-103">An overview of the NuGet ecosystem</span></span>

<span data-ttu-id="cabfb-104">Ponieważ jest wprowadzenie w 2010 r., NuGet przedstawiono znakomita szansa, aby poprawić i automatyzowanie różnych aspektów korzystania z procesami opracowywania.</span><span class="sxs-lookup"><span data-stu-id="cabfb-104">Since it's introduction in 2010, NuGet has presented a great opportunity to improve and automate different aspects of the development processes.</span></span>

<span data-ttu-id="cabfb-105">Ponieważ NuGet jest typu open source podlegający permissive [licencja v2 Apache](http://choosealicense.com/licenses/apache/), inne projekty mogą korzystać z NuGet i firmy można tworzyć pomoc techniczną dla swoich produktów.</span><span class="sxs-lookup"><span data-stu-id="cabfb-105">Because NuGet is open source under a permissive [Apache v2 license](http://choosealicense.com/licenses/apache/), other projects can leverage NuGet and companies can build support for it in their products.</span></span> <span data-ttu-id="cabfb-106">Dla projektów typu open source lub rozwoju aplikacji dla przedsiębiorstw, NuGet i inne aplikacje utworzone na oraz wokół NuGet zapewniają szeroką ekosystemu narzędzi dla poprawy procesu opracowywania oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="cabfb-106">Whether for open-source projects or enterprise application development, NuGet and other applications built on and around NuGet provide a broad ecosystem of tools for improving your software development process.</span></span>

<span data-ttu-id="cabfb-107">Wszystkie te projekty mogą wprowadzać innowacje z powodu wkładów dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="cabfb-107">All of these projects are able to innovate because of developer contributions.</span></span> <span data-ttu-id="cabfb-108">Tak samo, jak współtworzyć NuGet sam, również wkład w tych projektach raportowania usterek i nowe pomysły dotyczące funkcji, opinii, pisanie dokumentacji i współtworzenia, jeśli jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="cabfb-108">Just as you contribute to NuGet itself, also make contribution to these projects by reporting defects and new feature ideas, providing feedback, writing documentation, and contributing code where possible.</span></span>

## <a name="net-foundation-projects"></a><span data-ttu-id="cabfb-109">Projekty .NET foundation</span><span class="sxs-lookup"><span data-stu-id="cabfb-109">.NET Foundation projects</span></span>

<span data-ttu-id="cabfb-110">NuGet zapewnia system zarządzania pakietami bezpłatnej, typu open source dla platformy programowania firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cabfb-110">NuGet provides a free, open source package management system for the Microsoft development platform.</span></span> <span data-ttu-id="cabfb-111">Składa się z kilku narzędzi klienckich, a także zestaw usług, wchodzące w skład [oficjalna Galeria NuGet](http://www.nuget.org).</span><span class="sxs-lookup"><span data-stu-id="cabfb-111">It consists of a few client tools as well as the set of services that comprise the [official NuGet Gallery](http://www.nuget.org).</span></span> <span data-ttu-id="cabfb-112">W połączeniu, tworzą one projektu NuGet, który podlega [.NET Foundation](http://www.dotnetfoundation.org/).</span><span class="sxs-lookup"><span data-stu-id="cabfb-112">Combined, these form the NuGet project which is governed by the [.NET Foundation](http://www.dotnetfoundation.org/).</span></span>

<span data-ttu-id="cabfb-113">Organizacja NuGet zawiera różne repozytoriów w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="cabfb-113">The NuGet Organization contains various repositories on GitHub.</span></span> <span data-ttu-id="cabfb-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) zawiera przegląd wszystkich repozytoriów i gdzie można znaleźć różnych składników NuGet.</span><span class="sxs-lookup"><span data-stu-id="cabfb-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) gives an overview of all the repositories and where to find the various NuGet components.</span></span>

## <a name="microsoft-projects"></a><span data-ttu-id="cabfb-115">Projekty programu Microsoft</span><span class="sxs-lookup"><span data-stu-id="cabfb-115">Microsoft projects</span></span>

<span data-ttu-id="cabfb-116">Microsoft przyczynił się często do tworzenia pakietu nuget.</span><span class="sxs-lookup"><span data-stu-id="cabfb-116">Microsoft has contributed extensively to the development of NuGet.</span></span> <span data-ttu-id="cabfb-117">Wszystkie współtworzoną przez pracowników firmy Microsoft są także "open source" i wymagania (w tym prawa autorskie) .NET Foundation.</span><span class="sxs-lookup"><span data-stu-id="cabfb-117">All contributions made by Microsoft employees are also open source and are donated (including copyrights) to the .NET Foundation.</span></span>

## <a name="non-microsoft-projects"></a><span data-ttu-id="cabfb-118">Projekty inne niż firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="cabfb-118">Non-Microsoft projects</span></span>

<span data-ttu-id="cabfb-119">Wiele innych użytkowników indywidualnych i firm dokonano znaczących ekosystemem NuGet.</span><span class="sxs-lookup"><span data-stu-id="cabfb-119">Many other individuals and companies have made significant contributions to the NuGet ecosystem.</span></span> <span data-ttu-id="cabfb-120">Każdy projekt wymienione w tym miejscu mogą mieć licencję innego niż podstawowe składniki NuGet, więc upewnij się, że postanowienia licencyjne są dopuszczalne przed użyciem:</span><span class="sxs-lookup"><span data-stu-id="cabfb-120">Each project listed here may have a different license than the core NuGet components, so confirm that the license terms are acceptable prior to use:</span></span>

- [<span data-ttu-id="cabfb-121">AppVeyor ciągłej integracji</span><span class="sxs-lookup"><span data-stu-id="cabfb-121">AppVeyor CI</span></span>](https://www.appveyor.com/)
- [<span data-ttu-id="cabfb-122">Artifactory</span><span class="sxs-lookup"><span data-stu-id="cabfb-122">Artifactory</span></span>](https://www.jfrog.com/artifactory/)
- [<span data-ttu-id="cabfb-123">BoxStarter</span><span class="sxs-lookup"><span data-stu-id="cabfb-123">BoxStarter</span></span>](http://boxstarter.org/)
- [<span data-ttu-id="cabfb-124">Chocolatey</span><span class="sxs-lookup"><span data-stu-id="cabfb-124">Chocolatey</span></span>](https://chocolatey.org/)
- [<span data-ttu-id="cabfb-125">CoApp</span><span class="sxs-lookup"><span data-stu-id="cabfb-125">CoApp</span></span>](http://coapp.org/)
- [<span data-ttu-id="cabfb-126">JetBrains ReSharper</span><span class="sxs-lookup"><span data-stu-id="cabfb-126">JetBrains ReSharper</span></span>](https://resharper-plugins.jetbrains.com/)
- [<span data-ttu-id="cabfb-127">JetBrains TeamCity</span><span class="sxs-lookup"><span data-stu-id="cabfb-127">JetBrains TeamCity</span></span>](https://www.jetbrains.com/teamcity/)
- [<span data-ttu-id="cabfb-128">Klondike</span><span class="sxs-lookup"><span data-stu-id="cabfb-128">Klondike</span></span>](https://github.com/themotleyfool/Klondike)
- [<span data-ttu-id="cabfb-129">MinimalNugetServer</span><span class="sxs-lookup"><span data-stu-id="cabfb-129">MinimalNugetServer</span></span>](https://github.com/TanukiSharp/MinimalNugetServer)
- [<span data-ttu-id="cabfb-130">MyGet (lub NuGet jako usługa)</span><span class="sxs-lookup"><span data-stu-id="cabfb-130">MyGet (or NuGet-as-a-service)</span></span>](http://www.myget.org/)
- [<span data-ttu-id="cabfb-131">NuGet Package Explorer</span><span class="sxs-lookup"><span data-stu-id="cabfb-131">NuGet Package Explorer</span></span>](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [<span data-ttu-id="cabfb-132">NuGet Server</span><span class="sxs-lookup"><span data-stu-id="cabfb-132">NuGet Server</span></span>](http://nugetserver.net/)
- [<span data-ttu-id="cabfb-133">OctopusDeploy</span><span class="sxs-lookup"><span data-stu-id="cabfb-133">OctopusDeploy</span></span>](https://octopus.com/)
- [<span data-ttu-id="cabfb-134">Paket</span><span class="sxs-lookup"><span data-stu-id="cabfb-134">Paket</span></span>](https://fsprojects.github.io/Paket/)
- [<span data-ttu-id="cabfb-135">ProGet (Inedo)</span><span class="sxs-lookup"><span data-stu-id="cabfb-135">ProGet (Inedo)</span></span>](http://inedo.com/proget)
- [<span data-ttu-id="cabfb-136">scriptcs</span><span class="sxs-lookup"><span data-stu-id="cabfb-136">scriptcs</span></span>](http://scriptcs.net/)
- [<span data-ttu-id="cabfb-137">SharpDevelop</span><span class="sxs-lookup"><span data-stu-id="cabfb-137">SharpDevelop</span></span>](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [<span data-ttu-id="cabfb-138">Sonatype Nexus</span><span class="sxs-lookup"><span data-stu-id="cabfb-138">Sonatype Nexus</span></span>](http://www.sonatype.com/nexus-repository-sonatype)
- [<span data-ttu-id="cabfb-139">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="cabfb-139">SymbolSource</span></span>](http://www.symbolsource.org/Public)
- [<span data-ttu-id="cabfb-140">Xamarin i programu MonoDevelop</span><span class="sxs-lookup"><span data-stu-id="cabfb-140">Xamarin and MonoDevelop</span></span>](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a><span data-ttu-id="cabfb-141">Inne narzędzia oparte na pakietach NuGet</span><span class="sxs-lookup"><span data-stu-id="cabfb-141">Other NuGet-based utilities</span></span>

<span data-ttu-id="cabfb-142">Są to narzędzia i programy narzędziowe oparta na NuGet:</span><span class="sxs-lookup"><span data-stu-id="cabfb-142">These are tools and utilities built on NuGet:</span></span>

- <span data-ttu-id="cabfb-143">[Poznaj rozszerzenia](http://getglimpse.com/Packages) (dodatki plug-in są pakiety)</span><span class="sxs-lookup"><span data-stu-id="cabfb-143">[Glimpse Extensions](http://getglimpse.com/Packages) (plug-ins are packages)</span></span>
- [<span data-ttu-id="cabfb-144">NuGetMustHaves.com</span><span class="sxs-lookup"><span data-stu-id="cabfb-144">NuGetMustHaves.com</span></span>](http://nugetmusthaves.com/)
- <span data-ttu-id="cabfb-145">[Orchard](http://www.orchardproject.net/) (moduły CMS pobrane z v1 NuGet źródła danych hostowanej w galerii witryny systemu Orchard)</span><span class="sxs-lookup"><span data-stu-id="cabfb-145">[Orchard](http://www.orchardproject.net/) (CMS modules are fetched from a v1 NuGet feed hosted in the Orchard Gallery)</span></span>
- [<span data-ttu-id="cabfb-146">Implementacja języka Java serwer NuGet</span><span class="sxs-lookup"><span data-stu-id="cabfb-146">Java implementation of NuGet Server</span></span>](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- <span data-ttu-id="cabfb-147">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter, bot tweeting nowy pakiet publikacji)</span><span class="sxs-lookup"><span data-stu-id="cabfb-147">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting new package publications)</span></span>
- <span data-ttu-id="cabfb-148">[DefinitelyTyped](http://definitelytyped.org/) ([automatyczne](https://github.com/DefinitelyTyped/NugetAutomation/) typów TypeScript [publikowane definicje NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))</span><span class="sxs-lookup"><span data-stu-id="cabfb-148">[DefinitelyTyped](http://definitelytyped.org/) ([Automatic](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Type [Definitions published to NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))</span></span>

## <a name="training-materials-and-references"></a><span data-ttu-id="cabfb-149">Materiały szkoleniowe i odwołań</span><span class="sxs-lookup"><span data-stu-id="cabfb-149">Training materials and references</span></span>

<span data-ttu-id="cabfb-150">Zazwyczaj przy użyciu nowego narzędzia lub technologia jest powiązana z nauki.</span><span class="sxs-lookup"><span data-stu-id="cabfb-150">Using a new tool or technology usually comes with a learning curve.</span></span> <span data-ttu-id="cabfb-151">Na szczęście, NuGet ma nie wymaga początkowo dużej ilości nauki krzywą to wszystko!</span><span class="sxs-lookup"><span data-stu-id="cabfb-151">Luckily for you, NuGet has no steep learning curve it all!</span></span> <span data-ttu-id="cabfb-152">W rzeczywistości, każda osoba może [rozpocząć korzystanie z pakietów](../quickstart/use-a-package.md) szybko.</span><span class="sxs-lookup"><span data-stu-id="cabfb-152">In fact, anyone can [get started consuming packages](../quickstart/use-a-package.md) quickly.</span></span>

<span data-ttu-id="cabfb-153">Który mówi, tworzenie pakietów — i szczególnie dobra pakietów — wraz z założeń NuGet w zautomatyzowane procesy kompilowania i wdrażania, wymaga wydatków nieco więcej czasu, z następującymi zasobami:</span><span class="sxs-lookup"><span data-stu-id="cabfb-153">That said, authoring packages–and especially good packages–along with  embracing NuGet in automated build and deployment processes, requires spending a little more time with the following resources:</span></span>

- [<span data-ttu-id="cabfb-154">NuGet Blog</span><span class="sxs-lookup"><span data-stu-id="cabfb-154">NuGet Blog</span></span>](http://blog.nuget.org/)
- [<span data-ttu-id="cabfb-155">NuGet zespołu w serwisie Twitter @nuget</span><span class="sxs-lookup"><span data-stu-id="cabfb-155">NuGet team on Twitter, @nuget</span></span>](http://twitter.com/nuget)
- <span data-ttu-id="cabfb-156">Książki:</span><span class="sxs-lookup"><span data-stu-id="cabfb-156">Books:</span></span>
  - [<span data-ttu-id="cabfb-157">NuGet Apress Pro</span><span class="sxs-lookup"><span data-stu-id="cabfb-157">Apress Pro NuGet</span></span>](http://bit.ly/ProNuGet)
  - [<span data-ttu-id="cabfb-158">NuGet 2 Essentials</span><span class="sxs-lookup"><span data-stu-id="cabfb-158">NuGet 2 Essentials</span></span>](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a><span data-ttu-id="cabfb-159">Dokumentacja dla poszczególnych pakietów</span><span class="sxs-lookup"><span data-stu-id="cabfb-159">Documentation for individual packages</span></span>

<span data-ttu-id="cabfb-160">[NuDoq](http://nudoq.org) zapewnia prosty dostęp, aktualizacje i dokumentację dla pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="cabfb-160">[NuDoq](http://nudoq.org) provides straightforward access and updates and documentation for NuGet packages.</span></span>

<span data-ttu-id="cabfb-161">NuDoq regularnie sonduje serwer galerii nuget.org, aby uzyskać najnowsze aktualizacje pakietu, wypakowuje przetwarza pliki dokumentacji biblioteki i w związku z tym aktualizację w lokacji.</span><span class="sxs-lookup"><span data-stu-id="cabfb-161">NuDoq regularly polls the nuget.org gallery server for the latest package updates, unpacks and processes the library documentation files, and updates the site accordingly.</span></span>

## <a name="adding-your-project"></a><span data-ttu-id="cabfb-162">Dodawanie projektu</span><span class="sxs-lookup"><span data-stu-id="cabfb-162">Adding your project</span></span>

<span data-ttu-id="cabfb-163">Jeśli masz projekt ekosystem NuGet, które będą przydatne dodanie do tej strony, Prześlij żądanie ściągnięcia z edycji do tej strony.</span><span class="sxs-lookup"><span data-stu-id="cabfb-163">If you have a NuGet ecosystem project that would be a valuable addition to this page, please  submit a pull request with an edit to this page.</span></span>
