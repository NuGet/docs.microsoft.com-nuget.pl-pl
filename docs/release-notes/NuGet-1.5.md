---
title: Informacje o wersji narzędzia NuGet 1,5
description: Informacje o wersji programu NuGet 1,5, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c9946f3d8cf545ec14f842c40105743c231b4b72
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777097"
---
# <a name="nuget-15-release-notes"></a>Informacje o wersji narzędzia NuGet 1,5

Informacje o wersji narzędzia [NuGet 1,4](../release-notes/nuget-1.4.md)  |  [Informacje o wersji narzędzia NuGet 1,6](../release-notes/nuget-1.6.md)

Pakiet NuGet 1,5 został wydaną 30 sierpnia 2011.

## <a name="features"></a>Funkcje

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Szablony projektów ze wstępnie zainstalowanymi pakietami NuGet
Podczas tworzenia nowego szablonu projektu ASP.NET MVC 3, biblioteki skryptów jQuery zawarte w projekcie są w rzeczywistości umieszczane w tym miejscu przez zainstalowanie pakietów NuGet.

Szablon projektu ASP.NET MVC 3 zawiera zestaw pakietów NuGet, które są instalowane podczas wywoływania szablonu projektu. Ta możliwość dołączania pakietów NuGet z szablonem projektu to teraz funkcja NuGet, którą _każdy_ szablon projektu może teraz korzystać z programu.

Aby uzyskać więcej informacji na temat tej funkcji, przeczytaj ten [wpis w blogu przez dewelopera tej funkcji](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Jawne odwołania do zestawów

Dodano nowy `<references />` element służący do jawnego określania, które zestawy w pakiecie mają być przywoływane.

Na przykład, jeśli dodasz następujące elementy:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Następnie tylko `xunit.dll` i `xunit.extensions.dll` zostanie przywoływany z odpowiedniego [podfolderu Framework/profile](../reference/nuspec.md#explicit-assembly-references) folderu, `lib` nawet jeśli istnieją inne zestawy w folderze.

W przypadku pominięcia tego elementu stosowane jest zwykłe zachowanie, które jest odwołaniem do każdego zestawu w `lib` folderze.

__Do czego służy ta funkcja?__

Ta funkcja obsługuje tylko zestawy w czasie projektowania. Na przykład w przypadku korzystania z kontraktów kodu zestawy umów muszą znajdować się obok zestawów środowiska uruchomieniowego, które rozszerzają się, aby program Visual Studio mógł je znaleźć, ale w przypadku zestawów kontraktu nie należy odwoływać się do tego projektu i nie należy go kopiować do `bin` folderu.

Podobnie funkcja może być używana do dla platform testów jednostkowych, takich jak XUnit, które wymagają, aby zestawy narzędzi były zlokalizowane obok zestawów środowiska uruchomieniowego, ale nie zostały wykluczone z odwołań do projektu.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Dodano możliwość wykluczania plików z pliku. nuspec
`<file>`Element w `.nuspec` pliku może służyć do dołączania określonego pliku lub zestawu plików przy użyciu symbolu wieloznacznego. Gdy jest używany symbol wieloznaczny, nie ma możliwości wykluczenia określonego podzestawu dołączonych plików. Załóżmy na przykład, że chcesz, aby wszystkie pliki tekstowe w folderze z wyjątkiem określonego.

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


### <a name="get-package-command-improvement"></a>`Get-Package` udoskonalenie poleceń
`Get-Package`Polecenie obsługuje teraz `-ProjectName` parametr. Więc polecenie

```
Get-Package –ProjectName A
```

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

Aby dodać informacje o wersji do pakietu, Użyj nowego `<releaseNotes />` elementu metadanych w pliku NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>nuspec &ltfiles/ &gt; ulepszanie
`.nuspec`Plik umożliwia teraz pusty `<files />` element, który informuje nuget.exe nie dołączać żadnego pliku w pakiecie.

## <a name="bug-fixes"></a>Poprawki błędów
Pakiet NuGet 1,5 zawiera łącznie 107 elementów roboczych. 103 z tych elementów zostało oznaczonych jako błędy.

Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 1,5, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Poprawki błędów warto zauważyć:

* [Problem 1273](http://nuget.codeplex.com/workitem/1273): wprowadzono `packages.config` większą liczbę kontroli wersji, sortując pakiety alfabetycznie i usuwając dodatkowe odstępy.
* [Problem 844](http://nuget.codeplex.com/workitem/844): numery wersji są teraz znormalizowane, aby `Install-Package 1.0` działały w pakiecie z wersją `1.0.0` .
* [Problem 1060](http://nuget.codeplex.com/workitem/1060): podczas tworzenia pakietu przy użyciu nuget.exe `-Version` Flaga zastępuje `<version />` element.
