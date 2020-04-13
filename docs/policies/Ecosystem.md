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
# <a name="an-overview-of-the-nuget-ecosystem"></a>Omówienie ekosystemu NuGet

Od czasu wprowadzenia w 2010 r. NuGet przedstawił wielką szansę na ulepszenie i automatyzację różnych aspektów procesów programisty.

Ponieważ NuGet jest open source w ramach licencji [apache apache v2,](http://choosealicense.com/licenses/apache/)inne projekty mogą korzystać NuGet i firmy mogą budować wsparcie dla niego w swoich produktach. Niezależnie od tego, czy chodzi o projekty typu open source, czy o tworzenie aplikacji w przedsiębiorstwie, NuGet i inne aplikacje oparte na nuget i wokół niego zapewniają szeroki ekosystem narzędzi do ulepszania procesu tworzenia oprogramowania.

Wszystkie te projekty są w stanie wprowadzać innowacje dzięki wkładowi deweloperów. Podobnie jak przyczyniasz się do NuGet się, również przyczynić się do tych projektów, zgłaszając wady i nowe pomysły funkcji, dostarczanie opinii, pisanie dokumentacji i przyczyniając się do kodu, gdzie to możliwe.

## <a name="net-foundation-projects"></a>Projekty Fundacji .NET

NuGet zapewnia bezpłatny system zarządzania pakietami open source dla platformy dewelopera firmy Microsoft. Składa się z kilku narzędzi klienta, a także zestaw usług, które składają się na [oficjalnej Galerii NuGet](http://www.nuget.org). Połączone tworzą projekt NuGet, który jest zarządzany przez [.NET Foundation](http://www.dotnetfoundation.org/).

Organizacja NuGet zawiera różne repozytoria w usłudze GitHub. [https://github.com/Nuget/Home](https://github.com/Nuget/Home)zawiera przegląd wszystkich repozytoriów i gdzie można znaleźć różne składniki NuGet.

## <a name="microsoft-projects"></a>Projekty firmy Microsoft

Firma Microsoft w znacznym stopniu przyczyniła się do rozwoju NuGet. Wszystkie wkłady pracowników firmy Microsoft są również open source i są przekazywane (w tym prawa autorskie) do .NET Foundation.

## <a name="non-microsoft-projects"></a>Projekty inne niż Microsoft

Wiele innych osób i firm wniósł znaczący wkład w ekosystem NuGet. Każdy projekt wymieniony w tym miejscu może mieć inną licencję niż podstawowe składniki NuGet, więc upewnij się, że postanowienia licencyjne są dopuszczalne przed użyciem:

- [AppVeyor CI](https://www.appveyor.com/)
- [Artefakty](https://www.jfrog.com/artifactory/)
- [BoxStarter (Początek skrzynki)](http://boxstarter.org/)
- [Czekoladowy](https://chocolatey.org/)
- [CoApp (CoApp)](http://coapp.org/)
- [Żywiciele JetBrains](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer (MinimalNugetServer)](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (lub NuGet-as-a-service)](http://www.myget.org/)
- [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [Serwer NuGet](http://nugetserver.net/)
- [OśmiornicaDeploy](https://octopus.com/)
- [Paket (paket)](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [skrypty](http://scriptcs.net/)
- [Sharpdevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [Źródło symbolu](http://www.symbolsource.org/Public)
- [Xamarin i MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Inne narzędzia oparte na nuget

Są to narzędzia i narzędzia zbudowane na NuGet:

- [Rozszerzenia Glimpse](http://getglimpse.com/Packages) (wtyczki to pakiety)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Sad](http://www.orchardproject.net/) (moduły CMS są pobierane z kanału NuGet w wersji 1 hostowanego w Galerii Sadów)
- [Implementacja języka Java serwera NuGet Server](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting nowych publikacji pakiet)
- [DefinitelyTyped](http://definitelytyped.org/) ([Automatyczne](https://github.com/DefinitelyTyped/NugetAutomation/) [definicje](http://www.nuget.org/packages?q=DefinitelyTyped)typuScript opublikowane w NuGet )

## <a name="training-materials-and-references"></a>Materiały szkoleniowe i referencje

Korzystanie z nowego narzędzia lub technologii zwykle wiąże się z krzywą uczenia się. Na szczęście dla Ciebie, NuGet nie ma stromej krzywej uczenia się to wszystko! W rzeczywistości każdy może [szybko zacząć konsumować pakiety.](../quickstart/use-a-package.md)

To powiedziawszy, tworzenie pakietów, a zwłaszcza dobre pakiety, wraz z obejmując NuGet w zautomatyzowanych procesów kompilacji i wdrażania, wymaga spędzenia trochę więcej czasu z następujących zasobów:

- [NuGet Blog](http://blog.nuget.org/)
- [Zespół NuGet na Twitterze,@nuget](http://twitter.com/nuget)
- Książki:
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [NuGet 2 Podstawowe elementy](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Dokumentacja dla poszczególnych opakowań

[NuDoq](http://nudoq.org) zapewnia prosty dostęp i aktualizacje i dokumentację dla pakietów NuGet.

NuDoq regularnie sonduje serwer galerii nuget.org w celu uzyskania najnowszych aktualizacji pakietów, rozpakowuje i przetwarza pliki dokumentacji biblioteki oraz odpowiednio aktualizuje witrynę.

## <a name="adding-your-project"></a>Dodawanie projektu

Jeśli masz projekt ekosystemu NuGet, który byłby cennym dodatkiem do tej strony, prześlij żądanie ściągnięcia z edycją na tej stronie.
