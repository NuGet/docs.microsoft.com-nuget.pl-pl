---
title: Informacje o wersji 1.3 NuGet
description: Informacje o wersji programu NuGet 1.3 tym znanych problemów, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c0284fe0afb11bf6465897132cccd160674ea3e1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821151"
---
# <a name="nuget-13-release-notes"></a>Informacje o wersji 1.3 NuGet

[Informacje o wersji NuGet 1.2](../release-notes/nuget-1.2.md) | [NuGet 1.4 informacje o wersji](../release-notes/nuget-1.4.md)

NuGet 1.3 został wydany 25 kwietnia 2011.

## <a name="new-features"></a>Nowe funkcje

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Prostsze tworzenie pakietu z integracją serwera symboli

Zespół NuGet we współpracy z pracowników w [SymbolSource.org](http://www.symbolsource.org/) oferowanie naprawdę prosty sposób publikowania źródeł, a w pliku PDB wraz z pakietem. Umożliwia klientom pakietu krok do źródła pakietu w debugerze. Aby uzyskać więcej informacji, przeczytaj [tworzenie i publikowanie pakietu symboli](../create-packages/symbol-packages.md) łatwy sposób, aby opublikować pakiety NuGet ze źródła. Można również obejrzeć na żywo pokaz tej funkcji jako część programu NuGet szczegółowo porozmawiać na Mix11. Ta funkcja jest pełni wykazać, zaczynając od znaku 20 minut wideo.

### <a name="open-packagepage-command"></a>`Open-PackagePage` polecenie

Tego polecenia można łatwo uzyskać dostęp do strony projektu dla pakietu z poziomu konsoli Menedżera pakietów. Umożliwia także opcje, aby otworzyć adres URL licencji i na stronie nadużycia raportów dla pakietu.
Składnia polecenia jest następująca:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru` Opcja służy do zwracania wartości określonego adresu URL.

Przykłady:

    PM> Open-PackagePage Ninject

Otwiera w przeglądarce adres URL projektu określony w pakiecie Ninject.

    PM> Open-PackagePage Ninject -License

Otwiera w przeglądarce adres URL licencji określony w pakiecie Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Otwiera w przeglądarce adres URL w bieżącym źródle pakietów używane do zgłaszania nadużyć dla określonego pakietu.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Przypisuje adres URL licencji do zmiennej $url bez otwierania adresu URL w przeglądarce.

### <a name="performance-improvements"></a>Usprawnienia wydajności

NuGet 1.3 wprowadzono wiele ulepszeń wydajności. NuGet 1.3 pozwala uniknąć pobierania tej samej wersji pakietu wiele razy przy tym pamięci podręcznej użytkownika lokalnego. Można uzyskać dostępu do pamięci podręcznej i wyczyszczone za pomocą okna dialogowego Ustawienia Menedżera pakietów:

![Okno dialogowe Opcje NuGet z ustawień pamięci podręcznej pakietu](./media/nuget-options.png)

Inne ulepszenia wydajności obejmują dodawanie obsługi kompresji HTTP i poprawy szybkości instalacji pakietu w programie Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio i nuget.exe korzysta z tej samej listy źródeł pakietu

Przed NuGet 1.3 lista źródeł pakietów używane przez nuget.exe i NuGet programu Visual Studio dodatku nie były przechowywane w tym samym miejscu. NuGet 1.3 obecnie korzysta z tej samej listy w obu miejscach. Listy są przechowywane w `NuGet.Config` i przechowywane w folderze AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe ignoruje pliki i foldery, które zaczynają się "." domyślnie

W celu NuGet działają prawidłowo w przypadku systemów kontroli źródła, takie Podwersją i Mercurial, nuget.exe ignoruje folderów i plików, które zaczynają się '.' znaków, podczas tworzenia pakietów. Tę wartość można zastąpić przy użyciu dwóch nowych flag:

* __-NoDefaultExcludes__ służy do zastąpienia tego ustawienia i obejmują wszystkie pliki.
* __— Wyklucz__ służy do dodawania inne pliki/foldery do wykluczenia, za pomocą wzorca. Na przykład, aby wykluczyć wszystkie pliki z rozszerzeniem "bak"

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Uwaga: wzorzec nie jest cykliczne domyślnie._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Wsparcie dla projektów WiX i .NET Micro Framework

Dzięki użyciu społeczność NuGet obsługuje WiX typów projektów, a także Micro .NET Framework.

## <a name="bug-fixes"></a>Poprawki błędów

Aby zapoznać się z pełną listą poprawki, Wyświetl [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Poprawki błędów warto zauważyć

* Pakiety z plikami źródłowymi działa w obu witryn sieci Web i projekty aplikacji sieci Web.
Dla witryn sieci Web, pliki źródłowe zostają skopiowane do `App_Code` folderu
