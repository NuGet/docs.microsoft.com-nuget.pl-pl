---
title: Informacje o wersji narzędzia NuGet 1,5
description: Informacje o wersji programu NuGet 1,5, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 940a19cdc485d611d03b52ee3102bc95a78a36bb
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383352"
---
# <a name="nuget-15-release-notes"></a>Informacje o wersji narzędzia NuGet 1,5

[Informacje o wersji pakietu nuget 1,4](../release-notes/nuget-1.4.md) | [Informacje o wersji narzędzia NuGet 1,6](../release-notes/nuget-1.6.md)

Pakiet NuGet 1,5 został wydaną 30 sierpnia 2011.

## <a name="features"></a>Funkcje

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Szablony projektów ze wstępnie zainstalowanymi pakietami NuGet
Podczas tworzenia nowego szablonu projektu ASP.NET MVC 3, biblioteki skryptów jQuery zawarte w projekcie są w rzeczywistości umieszczane w tym miejscu przez zainstalowanie pakietów NuGet.

Szablon projektu ASP.NET MVC 3 zawiera zestaw pakietów NuGet, które są instalowane podczas wywoływania szablonu projektu. Ta możliwość dołączania pakietów NuGet z szablonem projektu to teraz funkcja NuGet, którą _każdy_ szablon projektu może teraz korzystać z programu.

Aby uzyskać więcej informacji na temat tej funkcji, przeczytaj ten [wpis w blogu przez dewelopera tej funkcji](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Jawne odwołania do zestawów

Dodano nowy element `<references />` używany do jawnego określania zestawów, do których należy odwoływać się w pakiecie.

Na przykład, jeśli dodasz następujące elementy:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Następnie tylko `xunit.dll` i `xunit.extensions.dll` będą przywoływane z odpowiedniego [podfolderu Framework/profile](../reference/nuspec.md#explicit-assembly-references) folderu `lib`, nawet jeśli istnieją inne zestawy w folderze.

W przypadku pominięcia tego elementu stosowane jest zwykłe zachowanie, które polega na odwoływaniu się do każdego zestawu w folderze `lib`.

__Do czego służy ta funkcja?__

Ta funkcja obsługuje tylko zestawy w czasie projektowania. Na przykład w przypadku korzystania z kontraktów kodu zestawy kontraktu muszą znajdować się obok zestawów środowiska uruchomieniowego, które rozszerzają się, aby program Visual Studio mógł je znaleźć, ale w przypadku zestawów kontraktu nie należy odwoływać się do tego projektu i nie należy go kopiować do folderu `bin`.

Podobnie funkcja może być używana do dla platform testów jednostkowych, takich jak XUnit, które wymagają, aby zestawy narzędzi były zlokalizowane obok zestawów środowiska uruchomieniowego, ale nie zostały wykluczone z odwołań do projektu.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Dodano możliwość wykluczania plików z pliku. nuspec
Element `<file>` w pliku `.nuspec` może służyć do dołączania określonego pliku lub zestawu plików przy użyciu symbolu wieloznacznego. Gdy jest używany symbol wieloznaczny, nie ma możliwości wykluczenia określonego podzestawu dołączonych plików. Załóżmy na przykład, że chcesz, aby wszystkie pliki tekstowe w folderze z wyjątkiem określonego.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

Użyj średników do określenia wielu plików.

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

Lub Użyj symbolu wieloznacznego, aby wykluczyć zestaw plików, takich jak wszystkie pliki kopii zapasowej

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Usuwanie pakietów przy użyciu okna dialogowego z komunikatem o usunięciu zależności
Podczas odinstalowywania pakietu z zależnościami program NuGet monituje o usunięcie zależności pakietu wraz z pakietem.

![Usuwanie pakietów zależnych](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>udoskonalenie polecenia `Get-Package`
Polecenie `Get-Package` obsługuje teraz parametr `-ProjectName`. Więc polecenie

    Get-Package –ProjectName A

wyświetli listę wszystkich pakietów zainstalowanych w projekcie A.

### <a name="support-for-proxies-that-require-authentication"></a>Obsługa serwerów proxy, które wymagają uwierzytelniania
W przypadku korzystania z programu NuGet za serwerem proxy wymagającym uwierzytelniania pakiet NuGet będzie teraz monitował o poświadczenia serwera proxy. Wprowadzenie poświadczeń umożliwia NuGet łączenie się ze zdalnym repozytorium.

### <a name="support-for-repositories-that-require-authentication"></a>Obsługa repozytoriów wymagających uwierzytelniania
Pakiet NuGet obsługuje teraz łączenie z [repozytoriami prywatnymi](../hosting-packages/local-feeds.md) , które wymagają uwierzytelniania podstawowego lub NTLM.

Obsługa uwierzytelniania szyfrowanego zostanie dodana w przyszłym wydaniu.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Udoskonalenia wydajności repozytorium nuget.org
Wprowadziliśmy kilka ulepszeń wydajności w galerii nuget.org, aby przyspieszyć tworzenie i wyszukiwanie pakietów.

### <a name="solution-dialog-project-filtering"></a>Filtrowanie projektu okna dialogowego rozwiązania
W oknie dialogowym na poziomie rozwiązania po wyświetleniu monitu o projekty, które mają zostać zainstalowane, wyświetlane są tylko projekty zgodne z wybranym pakietem.

### <a name="package-release-notes"></a>Informacje o wersji pakietu
Pakiety NuGet zawierają teraz obsługę informacji o wersji. Informacje o wersji są wyświetlane tylko podczas wyświetlania _aktualizacji_ pakietu, więc nie ma sensu, aby dodać je do swojej pierwszej wersji.

![Informacje o wersji na karcie Aktualizacje](./media/manage-nuget-packages-release-notes.png)

Aby dodać informacje o wersji do pakietu, Użyj nowego elementu `<releaseNotes />` Metadata w pliku NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>nuspec & ltfiles/&gt;
Plik `.nuspec` teraz zezwala na pusty element `<files />`, który informuje plik NuGet. exe, aby nie dołączać żadnego pliku w pakiecie.

## <a name="bug-fixes"></a>Poprawki błędów
Pakiet NuGet 1,5 zawiera łącznie 107 elementów roboczych. 103 z tych elementów zostało oznaczonych jako błędy.

Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 1,5, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Poprawki błędów warto zauważyć:

* [Problem 1273](http://nuget.codeplex.com/workitem/1273): `packages.config` większą liczbę kontroli wersji, sortując pakiety alfabetycznie i usuwając dodatkowe odstępy.
* [Problem 844](http://nuget.codeplex.com/workitem/844): numery wersji są teraz znormalizowane, tak aby `Install-Package 1.0` działały w pakiecie z wersją `1.0.0`.
* [Problem 1060](http://nuget.codeplex.com/workitem/1060): podczas tworzenia pakietu przy użyciu NuGet. exe flaga `-Version` zastępuje element `<version />`.
