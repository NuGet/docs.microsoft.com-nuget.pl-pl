---
title: Informacje o wersji narzędzia NuGet 1,3
description: Informacje o wersji programu NuGet 1,3, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 45d5caa46d532670e370b81f675663b3c5aaaa95
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825265"
---
# <a name="nuget-13-release-notes"></a>Informacje o wersji narzędzia NuGet 1,3

[Informacje o wersji pakietu nuget 1,2](../release-notes/nuget-1.2.md) | [Informacje o wersji narzędzia NuGet 1,4](../release-notes/nuget-1.4.md)

Pakiet NuGet 1,3 został wydaną 25 kwietnia 2011.

## <a name="new-features"></a>Nowe funkcje

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Usprawnione Tworzenie pakietów z integracją z serwerem symboli

Zespół NuGet współpracujący z osób na [SymbolSource.org](http://www.symbolsource.org/) , aby zaoferować naprawdę prosty sposób publikowania źródeł i plików PDB wraz z pakietem. Dzięki temu klienci pakietu mogą przechodzić do źródła pakietu w debugerze. Aby uzyskać więcej informacji, przeczytaj artykuł [Tworzenie i publikowanie pakietu symboli](../create-packages/symbol-packages.md) w łatwy sposób publikowania pakietów NuGet ze źródłami. Możesz również obejrzeć prezentację na żywo tej funkcji jako część pakietu NuGet, z głębokości Porozmawiaj pod adresem Mix11. Ta funkcja jest w pełni zademonstrowana, zaczynając od 20-minutowego znaku wideo.

### <a name="open-packagepage-command"></a>Polecenie `Open-PackagePage`

To polecenie ułatwia dostęp do strony projektu dla pakietu z poziomu konsoli Menedżera pakietów. Dostępne są również opcje umożliwiające otwarcie adresu URL licencji i strony Zgłoś nadużycie dla pakietu.
Składnia polecenia jest następująca:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

Opcja `-PassThru` służy do zwracania wartości określonego adresu URL.

Przykłady:

    PM> Open-PackagePage Ninject

Otwiera przeglądarkę do adresu URL projektu określonego w pakiecie Ninject.

    PM> Open-PackagePage Ninject -License

Otwiera przeglądarkę do adresu URL licencji określonego w pakiecie Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Otwiera przeglądarkę do adresu URL w bieżącym źródle pakietu używanym do zgłaszania nadużycia dla określonego pakietu.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Przypisuje adres URL licencji do zmiennej, $url bez otwierania adresu URL w przeglądarce.

### <a name="performance-improvements"></a>Usprawnienia wydajności

W programie NuGet 1,3 wprowadzono wiele ulepszeń wydajności. Pakiet NuGet 1,3 pozwala uniknąć pobierania tej samej wersji pakietu wielokrotnie przez uwzględnienie lokalnej pamięci podręcznej dla poszczególnych użytkowników. Dostęp do pamięci podręcznej można uzyskać i wyczyścić za pomocą okna dialogowego ustawień Menedżera pakietów:

![Okno dialogowe Opcje NuGet z ustawieniami pamięci podręcznej pakietów](./media/nuget-options.png)

Inne ulepszenia wydajności obejmują dodawanie obsługi kompresji HTTP i zwiększanie szybkości instalacji pakietów w programie Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Programy Visual Studio i NuGet. exe używają tej samej listy źródeł pakietów

Przed pakietem NuGet 1,3 Lista źródeł pakietów używanych przez narzędzia NuGet. exe i dodatek NuGet Visual Studio nie zostały zapisane w tym samym miejscu. Pakiet NuGet 1,3 używa teraz tej samej listy w obu miejscach. Lista jest przechowywana w `NuGet.Config` i przechowywana w folderze AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>NuGet. exe domyślnie ignoruje pliki i foldery, które zaczynają się od "."

Aby program NuGet działał poprawnie z systemami kontroli źródła, takimi jak Subversion i Mercurial, NuGet. exe ignoruje foldery i pliki, które zaczynają się od znaku "." podczas tworzenia pakietów. Można to zastąpić przy użyciu dwóch nowych flag:

* __-NoDefaultExcludes__ służy do przesłonięcia tego ustawienia i uwzględnienia wszystkich plików.
* __-Exclude__ służy do dodawania innych plików/folderów do wykluczenia przy użyciu wzorca. Na przykład, aby wykluczyć wszystkie pliki z rozszerzeniem. bak.

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Uwaga: wzorzec nie jest domyślnie cykliczny._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Obsługa projektów WiX i .NET Micro Framework

Dzięki wkładom społecznościowym pakiet NuGet obejmuje obsługę typów projektów WiX oraz .NET Micro Framework.

## <a name="bug-fixes"></a>Poprawki błędów

Aby zapoznać się z pełną listą poprawek błędów, przejrzyj [Narzędzie śledzenia problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Poprawki błędów warto zauważyć

* Pakiety z plikami źródłowymi działają zarówno w witrynach internetowych, jak i w projektach aplikacji sieci Web.
W przypadku witryn sieci Web pliki źródłowe są kopiowane do folderu `App_Code`
