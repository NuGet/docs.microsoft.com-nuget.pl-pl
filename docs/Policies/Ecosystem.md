---
title: "Omówienie ekosystemu NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Kompleksowe zasoby w ekosystemie NuGet, w tym źródeł NuGet, Microsoft NuGet projektów, narzędzia i materiałów szkoleniowych."
keywords: "Ekosystem NuGet, Microsoft NuGet projektów, NuGet typu open source, narzędzia NuGet, materiałów szkoleniowych NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c1e457c034f239fbea4e75f24851ea38182a294
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>Omówienie ekosystemu NuGet

Ponieważ chodzi o wprowadzenie w 2010, NuGet ma przedstawione dużą możliwość poprawić i zautomatyzować różnych aspektów procesami programowania.

Ponieważ NuGet jest typu open source podlegający ograniczająca [licencji Apache w wersji 2](http://choosealicense.com/licenses/apache/), mogą korzystać z innych projektów NuGet i przedsiębiorstwa mogą tworzyć obsługę w swoich produktach. NuGet i inne aplikacje zbudowane na i wokół NuGet dla projektów open source lub rozwoju aplikacji przedsiębiorstwa, podaj szerokim ekosystemem narzędzi dla poprawy z procesem tworzenia oprogramowania.

Wszystkie te projekty mogą innowacji z powodu wkładów developer. Tak samo, jak współtworzyć NuGet samego, również przyczynić się do tych projektów wady raportowania i nowe pomysły funkcji zwrotnych, pisanie dokumentacji i współtworzenia kodu, gdy jest to możliwe.

## <a name="net-foundation-projects"></a>Projekty .NET foundation

NuGet zapewnia system zarządzania pakiet wolnego typu open source platformy programistycznej Microsoft. Składa się z kilku narzędzi klienta, a także zestaw usług wchodzących w skład [oficjalnego galerii NuGet](http://www.nuget.org). Połączone, te tworzą projektu NuGet, który podlega [.NET Foundation](http://www.dotnetfoundation.org/).

Organizacja NuGet zawiera różne repozytoria w witrynie GitHub. [https://github.com/Nuget/Home](https://github.com/Nuget/Home) zapewnia przegląd wszystkich repozytoriów i gdzie można znaleźć różne składniki NuGet.

## <a name="microsoft-projects"></a>Projekty Microsoft

Microsoft przyczynił się często do tworzenia programu NuGet. Wszystkie wkład pracowników firmy Microsoft są także otworzyć źródła i przekazywana (w tym prawa autorskie) .NET Foundation.

## <a name="non-microsoft-projects"></a>Projekty inne niż firmy Microsoft

Wiele osób i firm dokonano znaczących wkładów ekosystemem NuGet. Każdy projekt wymienione w tym miejscu może mieć licencję innego niż podstawowe składniki NuGet, aby potwierdzić, że postanowienia licencyjne są dopuszczalne przed użyciem:

- [AppVeyor elementu konfiguracji](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (lub NuGet jako usługa)](http://www.myget.org/)
- [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet Server](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype węzła](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin i MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Inne narzędzia oparte na NuGet

Są to narzędzi oparty na NuGet:

- [Glimpse rozszerzenia](http://getglimpse.com/Packages) (dodatki plug-in są pakiety)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (modułów CMS pobrane z v1 NuGet źródła danych obsługiwane galerii Orchard)
- [Środowisko Java NuGet serwera](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting nowy pakiet publikacji)
- [DefinitelyTyped](http://definitelytyped.org/) ([automatyczne](https://github.com/DefinitelyTyped/NugetAutomation/) typu TypeScript [definicje opublikowane NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>Aktualizowanie materiałów szkoleniowych i odwołań

Za pomocą nowego narzędzia lub technologii zwykle zawiera naukę. Szczęście NuGet, ma problemy z ich opanowaniem nauki krzywą wszystko! W rzeczywistości, każdy użytkownik może [rozpocząć korzystanie z pakietów](../quickstart/use-a-package.md) szybko.

Który powiedział, tworzenie pakietów — i szczególnie dobre pakiety — wraz z obejmujący NuGet w zautomatyzowanych procesów kompilacji i wdrożenia, wymaga nieco więcej czasu z następującymi zasobami wydatków:

- [NuGet Blog](http://blog.nuget.org/)
- [Zespół NuGet w serwisie Twitter,@nuget](http://twitter.com/nuget)
- Książki:
  - [NuGet Apress Pro](http://bit.ly/ProNuGet)
  - [NuGet 2 Essentials](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Dokumentacja dla poszczególnych pakietów

[NuDoq](http://nudoq.org) zawiera proste dostępu, aktualizacji i dokumentację dla pakietów NuGet.

NuDoq regularnie odpytuje serwer galerii nuget.org najnowsze aktualizacje pakietu, wypakowuje przetwarza pliki dokumentacji biblioteki i odpowiednio aktualizację w lokacji.

## <a name="adding-your-project"></a>Dodawanie projektu

Jeśli masz projektu ekosystem NuGet, która byłaby cenne dodanie do tej strony, Prześlij żądanie ściągnięcia edycji do tej strony.
