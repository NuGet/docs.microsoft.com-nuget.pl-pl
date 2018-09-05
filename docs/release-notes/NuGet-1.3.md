---
title: Informacje o wersji 1.3 NuGet
description: Informacje o wersji programu NuGet 1.3, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551354"
---
# <a name="nuget-13-release-notes"></a>Informacje o wersji 1.3 NuGet

[Informacje o wersji NuGet 1.2](../release-notes/nuget-1.2.md) | [informacjach o wersji NuGet 1.4](../release-notes/nuget-1.4.md)

NuGet 1.3 został wydany 25 kwietnia 2011.

## <a name="new-features"></a>Nowe funkcje

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Prostsze tworzenie pakietu za pomocą integracji serwera symboli

Zespół NuGet użyły spamerzy na [SymbolSource.org](http://www.symbolsource.org/) zaoferować bardzo prosty sposób publikowania Twoich źródeł i pliku PDB firmy wraz z pakietu. Dzięki temu konsumentów pakietu wkraczać do źródła pakietu w debugerze. Aby uzyskać więcej informacji, przeczytaj [tworzenie i publikowanie pakietu symboli](../create-packages/symbol-packages.md) prosty sposób, aby opublikować pakiety NuGet ze źródłami. Możesz też obejrzeć na żywo pokaz działania tej funkcji w ramach pakietu nuget szczegółowo mówić o Mix11. Ta funkcja jest w pełni wykazane zaczynając od znaku 20 minut filmu wideo.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Polecenie

To polecenie można łatwo uzyskać dostęp do strony projektu dla pakietu z poziomu konsoli Menedżera pakietów. Umożliwia także opcje, aby otworzyć adres URL licencji i strony nadużycie raportu dla pakietu.
Składnia polecenia jest następująca:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru` Opcja jest używana w celu zwrócenia wartości z określonego adresu URL.

Przykłady:

    PM> Open-PackagePage Ninject

Otworzy w przeglądarce adres URL projektu określony w pakiecie Ninject.

    PM> Open-PackagePage Ninject -License

Otworzy w przeglądarce adres URL licencji określony w pakiecie Ninject.

    PM> Open-PackagePage Ninject -ReportAbuse

Otworzy w przeglądarce adres URL w bieżącym źródle pakietu umożliwia zgłaszanie nadużyć dla określonego pakietu.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Przypisuje adres URL licencji do zmiennej $url, bez konieczności otwierania adresu URL w przeglądarce.

### <a name="performance-improvements"></a>Usprawnienia wydajności

NuGet 1.3 wprowadzono wiele ulepszeń wydajności. NuGet 1.3 eliminuje pobieranie tę samą wersję pakietu wiele razy przy tym pamięci podręcznej użytkownika lokalnego. Pamięci podręcznej, można uzyskać dostęp i wyczyszczone za pomocą okna dialogowego Ustawienia Menedżera pakietów:

![Okno dialogowe Opcje NuGet za pomocą ustawienia pamięci podręcznej pakietu](./media/nuget-options.png)

Inne ulepszenia wydajności obejmują dodawanie obsługi kompresji HTTP i zwiększanie prędkości instalacji pakietów w programie Visual Studio.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Program Visual Studio i nuget.exe korzysta z tej samej listy źródeł pakietów

Przed NuGet 1.3 listę źródeł pakietów używane przez nuget.exe i NuGet programu Visual Studio dodatek nie były przechowywane w tym samym miejscu. NuGet 1.3 teraz używa tej samej listy w obu miejscach. Listy są przechowywane w `NuGet.Config` i przechowywane w folderze AppData.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe ignoruje pliki i foldery, które zaczyna się "." domyślnie

Aby można było wprowadzić NuGet działają prawidłowo w przypadku systemów kontroli źródła, takiego rozwiązania Subversion i Mercurial, nuget.exe ignoruje folderów i plików, które zaczyna się "." znaków podczas tworzenia pakietów. Tę wartość można zastąpić przy użyciu dwóch nowych flag:

* __-NoDefaultExcludes__ jest używany, aby zastąpić to ustawienie i Dołącz wszystkie pliki.
* __— Wyłączyć z wyszukiwania__ służy do dodawania inne pliki/foldery do wykluczenia, przy użyciu wzorca. Na przykład, aby wykluczyć wszystkie pliki z rozszerzeniem pliku ".bak"

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Uwaga: wzorzec nie jest cykliczna domyślnie._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>Wsparcie dla projektów WiX i .NET Framework wczesnych

Dzięki rozłożeniu kod wniesiony przez społeczność NuGet obsługuje typy projektów WiX, a także Micro .NET Framework.

## <a name="bug-fixes"></a>Poprawki błędów

Aby uzyskać pełną listę poprawek można znaleźć [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Poprawki błędów warte odnotowania

* Pakiety z plikami źródłowymi działać w obu witryn sieci Web i w projektach aplikacji sieci Web.
Dla witryn sieci Web, pliki źródłowe są kopiowane do `App_Code` folderu
