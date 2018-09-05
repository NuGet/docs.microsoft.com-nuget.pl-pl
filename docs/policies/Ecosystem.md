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
# <a name="an-overview-of-the-nuget-ecosystem"></a>Omówienie ekosystemu NuGet

Ponieważ jest wprowadzenie w 2010 r., NuGet przedstawiono znakomita szansa, aby poprawić i automatyzowanie różnych aspektów korzystania z procesami opracowywania.

Ponieważ NuGet jest typu open source podlegający permissive [licencja v2 Apache](http://choosealicense.com/licenses/apache/), inne projekty mogą korzystać z NuGet i firmy można tworzyć pomoc techniczną dla swoich produktów. Dla projektów typu open source lub rozwoju aplikacji dla przedsiębiorstw, NuGet i inne aplikacje utworzone na oraz wokół NuGet zapewniają szeroką ekosystemu narzędzi dla poprawy procesu opracowywania oprogramowania.

Wszystkie te projekty mogą wprowadzać innowacje z powodu wkładów dla deweloperów. Tak samo, jak współtworzyć NuGet sam, również wkład w tych projektach raportowania usterek i nowe pomysły dotyczące funkcji, opinii, pisanie dokumentacji i współtworzenia, jeśli jest to możliwe.

## <a name="net-foundation-projects"></a>Projekty .NET foundation

NuGet zapewnia system zarządzania pakietami bezpłatnej, typu open source dla platformy programowania firmy Microsoft. Składa się z kilku narzędzi klienckich, a także zestaw usług, wchodzące w skład [oficjalna Galeria NuGet](http://www.nuget.org). W połączeniu, tworzą one projektu NuGet, który podlega [.NET Foundation](http://www.dotnetfoundation.org/).

Organizacja NuGet zawiera różne repozytoriów w serwisie GitHub. [https://github.com/Nuget/Home](https://github.com/Nuget/Home) zawiera przegląd wszystkich repozytoriów i gdzie można znaleźć różnych składników NuGet.

## <a name="microsoft-projects"></a>Projekty programu Microsoft

Microsoft przyczynił się często do tworzenia pakietu nuget. Wszystkie współtworzoną przez pracowników firmy Microsoft są także "open source" i wymagania (w tym prawa autorskie) .NET Foundation.

## <a name="non-microsoft-projects"></a>Projekty inne niż firmy Microsoft

Wiele innych użytkowników indywidualnych i firm dokonano znaczących ekosystemem NuGet. Każdy projekt wymienione w tym miejscu mogą mieć licencję innego niż podstawowe składniki NuGet, więc upewnij się, że postanowienia licencyjne są dopuszczalne przed użyciem:

- [AppVeyor ciągłej integracji](https://www.appveyor.com/)
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
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin i programu MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Inne narzędzia oparte na pakietach NuGet

Są to narzędzia i programy narzędziowe oparta na NuGet:

- [Poznaj rozszerzenia](http://getglimpse.com/Packages) (dodatki plug-in są pakiety)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (moduły CMS pobrane z v1 NuGet źródła danych hostowanej w galerii witryny systemu Orchard)
- [Implementacja języka Java serwer NuGet](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (Twitter, bot tweeting nowy pakiet publikacji)
- [DefinitelyTyped](http://definitelytyped.org/) ([automatyczne](https://github.com/DefinitelyTyped/NugetAutomation/) typów TypeScript [publikowane definicje NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>Materiały szkoleniowe i odwołań

Zazwyczaj przy użyciu nowego narzędzia lub technologia jest powiązana z nauki. Na szczęście, NuGet ma nie wymaga początkowo dużej ilości nauki krzywą to wszystko! W rzeczywistości, każda osoba może [rozpocząć korzystanie z pakietów](../quickstart/use-a-package.md) szybko.

Który mówi, tworzenie pakietów — i szczególnie dobra pakietów — wraz z założeń NuGet w zautomatyzowane procesy kompilowania i wdrażania, wymaga wydatków nieco więcej czasu, z następującymi zasobami:

- [NuGet Blog](http://blog.nuget.org/)
- [NuGet zespołu w serwisie Twitter @nuget](http://twitter.com/nuget)
- Książki:
  - [NuGet Apress Pro](http://bit.ly/ProNuGet)
  - [NuGet 2 Essentials](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Dokumentacja dla poszczególnych pakietów

[NuDoq](http://nudoq.org) zapewnia prosty dostęp, aktualizacje i dokumentację dla pakietów NuGet.

NuDoq regularnie sonduje serwer galerii nuget.org, aby uzyskać najnowsze aktualizacje pakietu, wypakowuje przetwarza pliki dokumentacji biblioteki i w związku z tym aktualizację w lokacji.

## <a name="adding-your-project"></a>Dodawanie projektu

Jeśli masz projekt ekosystem NuGet, które będą przydatne dodanie do tej strony, Prześlij żądanie ściągnięcia z edycji do tej strony.
