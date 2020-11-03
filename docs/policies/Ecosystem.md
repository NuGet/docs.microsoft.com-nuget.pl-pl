---
title: Omówienie ekosystemu NuGet
description: Kompleksowe zasoby ekosystemu NuGet, w tym źródła NuGet, projekty, narzędzia i materiały szkoleniowe inne niż firmy Microsoft.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 165587fb64be5a5f4dbfdece7dc3a1e6402b733e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237429"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>Omówienie ekosystemu NuGet

Ponieważ jest to wprowadzenie w 2010, pakiet NuGet przedstawił doskonałą okazję do ulepszania i automatyzowania różnych aspektów procesów programistycznych.

Ponieważ pakiet NuGet jest typu open source w ramach dowolnej [licencji Apache v2](http://choosealicense.com/licenses/apache/), inne projekty mogą korzystać z narzędzia NuGet, a firmy mogą tworzyć do nich pomoc techniczną. Bez względu na to, czy w przypadku projektów typu "open source", jak i programowania aplikacji korporacyjnych, NuGet i innych aplikacji opartych na oprogramowaniu NuGet, można uzyskać obszerny ekosystem narzędzi do ulepszania procesu tworzenia oprogramowania.

Wszystkie te projekty mogą wprowadzać innowacje ze względu na udziały deweloperów. Podobnie jak w przypadku współtworzenia oprogramowania NuGet, należy również udostępnić te projekty, zgłaszając wady i nowe pomysły dotyczące funkcji, dostarczając Opinie, pisząc dokumentację i tworząc kod, tam gdzie to możliwe.

## <a name="net-foundation-projects"></a>Projekty .NET Foundation

Pakiet NuGet oferuje bezpłatne system zarządzania pakietami typu open source dla platformy programistycznej Microsoft. Składa się z kilku narzędzi klienckich, a także zestawu usług wchodzących w skład [oficjalnej galerii NuGet](http://www.nuget.org). Łącznie, te tworzą projekt NuGet, który podlega [platformie .NET Foundation](http://www.dotnetfoundation.org/).

Organizacja NuGet zawiera różne repozytoria w serwisie GitHub. [https://github.com/Nuget/Home](https://github.com/Nuget/Home) zawiera przegląd wszystkich repozytoriów i lokalizacji, w których można znaleźć różne składniki NuGet.

## <a name="microsoft-projects"></a>Projekty firmy Microsoft

Firma Microsoft przyczyniła się do rozwoju programu NuGet. Wszystkie wkłady wykonywane przez pracowników firmy Microsoft są również otwarte i są oddzielone (łącznie z prawami autorskimi) do programu .NET Foundation.

## <a name="non-microsoft-projects"></a>Projekty inne niż firmy Microsoft

Wiele innych osób i firm wprowadziło znaczące wkłady do ekosystemu NuGet. Każdy projekt wymieniony w tym miejscu może mieć inną licencję niż podstawowe składniki NuGet, dlatego należy upewnić się, że warunki licencji są akceptowane przed użyciem:

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Narzędzia Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains Resharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (lub NuGet jako usługa)](http://www.myget.org/)
- [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [Serwer NuGet](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin i MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Inne narzędzia oparte na narzędziu NuGet

Oto narzędzia i narzędzia utworzone na serwerze NuGet:

- [Rozszerzenia możliwość wypróbowania innowacyjnego](http://getglimpse.com/Packages) (wtyczki są pakietami)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Sadu](http://www.orchardproject.net/) (moduły CMS są pobierane z kanału informacyjnego programu NuGet V1 hostowanego w galerii sadu)
- [Implementacja języka Java serwera NuGet](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (publikacje nowych pakietów w usłudze Twitter bot)
- [DefinitelyTyped](http://definitelytyped.org/) ([Automatyczne](https://github.com/DefinitelyTyped/NugetAutomation/) definicje typów TypeScript [publikowane w NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>Materiały szkoleniowe i odwołania

Korzystanie z nowego narzędzia lub technologii zwykle obejmuje krzywą uczenia się. Na szczęście dla Ciebie, NuGet nie ma bardzo szczegółowej krzywej szkoleniowej. W rzeczywistości każda osoba może szybko rozpocząć [Korzystanie z pakietów](../quickstart/install-and-use-a-package-in-visual-studio.md) .

Oznacza to, że pakiety autorskie — i szczególnie dobre pakiety — wraz z pakietem NuGet w zautomatyzowanym procesie kompilowania i wdrażania, wymagają nieco więcej czasu z następującymi zasobami:

- [Blog narzędzia NuGet](http://blog.nuget.org/)
- [Zespół NuGet w serwisie Twitter, @nuget](http://twitter.com/nuget)
- Stad
  - [Pakiet NuGet Apress Pro](http://bit.ly/ProNuGet)
  - [Pakiet NuGet 2](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Dokumentacja poszczególnych pakietów

[NuDoq](http://nudoq.org) zapewnia prosty dostęp i aktualizacje oraz dokumentację dla pakietów NuGet.

NuDoq regularnie sonduje serwer galerii nuget.org w celu uzyskania najnowszych aktualizacji pakietu, rozpakuje i przetwarza pliki dokumentacji biblioteki i odpowiednio aktualizuje lokację.

## <a name="adding-your-project"></a>Dodawanie projektu

Jeśli masz projekt ekosystemu NuGet, który będzie cennym dodatkiem do tej strony, Prześlij żądanie ściągnięcia z edytowaniem na tej stronie.