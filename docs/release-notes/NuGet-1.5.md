---
title: 1,5 raza więcej wersji NuGet
description: Informacje o wersji programu NuGet 1.5, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548728"
---
# <a name="nuget-15-release-notes"></a>1,5 raza więcej wersji NuGet

[Informacje o wersji NuGet 1.4](../release-notes/nuget-1.4.md) | [informacjach o wersji NuGet w wersji 1.6](../release-notes/nuget-1.6.md)

NuGet w wersji 1.5 został wydany 30 sierpnia 2011 r.

## <a name="features"></a>Funkcje

### <a name="project-templates-with-preinstalled-nuget-packages"></a>Szablony projektów za pomocą pakietów NuGet wstępnie zainstalowane
Podczas tworzenia nowego szablonu projektu ASP.NET MVC 3, biblioteki skryptów jQuery zawarty w projekcie faktycznie umieszczone tam przez instalowanie pakietów NuGet.

Szablon projektu platformy ASP.NET MVC 3 zawiera zestaw pakietów NuGet, które mają zostać zainstalowane podczas wywoływania szablonu projektu. Ta możliwość uwzględnienia pakietów NuGet za pomocą szablonu projektu jest teraz funkcją NuGet, _wszelkie_ szablonu projektu mogą teraz korzystać z.

Aby uzyskać więcej informacji na temat tej funkcji, przeczytaj ten [wpis na blogu autorstwa dla deweloperów funkcji](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).

### <a name="explicit-assembly-references"></a>Odwołania do zestawów jawne

Dodano nową `<references />` element używany jawnie określić zestawy, które w ramach pakietu powinny istnieć odwołania.

Jeśli na przykład dodaj następujący kod:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

A następnie tylko `xunit.dll` i `xunit.extensions.dll` będzie odwoływać się z odpowiednią [podfolder framework/profile](../reference/nuspec.md#explicit-assembly-references) z `lib` folderu nawet wtedy, gdy istnieją inne zestawy w folderze.

Jeśli ten element zostanie pominięty, a następnie stosuje zwykłe zachowanie stosowane, czyli odwołać się do każdego zestawu w `lib` folderu.

__Do czego służy ta funkcja?__

Ta funkcja obsługuje tylko zestawy czasu projektowania. Na przykład korzystając z kontraktów kodu, zestawów umowy muszą być obok zestawów środowiska uruchomieniowego, które mogą rozszerzyć, aby je znaleźć programu Visual Studio, ale zestawy kontraktu nie powinien rzeczywiście odwoływać się do projektu i nie powinien być skopiowany do `bin` folderu.

Podobnie funkcja może służyć do dla struktur testów jednostek, takich jak XUnit, które należy jego zestawy narzędzi do znajdujące się obok zestawów środowiska uruchomieniowego, ale wyłączone z odwołaniami do projektów.

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a>Dodano możliwość Wyklucz pliki zawarte w .nuspec
`<file>` Elemencie `.nuspec` pliku może służyć do określonego pliku lub zestawu plików przy użyciu symboli wieloznacznych. Korzystając z symbolem wieloznacznym, nie istnieje żaden sposób, aby wykluczyć określony podzbiór dołączone pliki. Na przykład załóżmy, że chcesz, aby wszystkie pliki tekstowe, w folderze, z wyjątkiem jeden z nich.

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

Lub użyj symbolu wieloznacznego, aby wykluczyć zestaw plików, takich jak wszystkie pliki kopii zapasowej

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a>Usuwanie pakietów, korzystając z okna dialogowego monituje o usunięcie zależności
Podczas odinstalowywania pakietu z zależnościami, wyświetli NuGet, dzięki czemu usuwanie zależności pakietu wraz z pakietu.

![Usuwanie pakietów zależnych](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a>`Get-Package` polecenie poprawy
`Get-Package` Polecenie obsługuje teraz `-ProjectName` parametru. To polecenie

    Get-Package –ProjectName A

zostanie wyświetlona lista wszystkich pakietów zainstalowany w projekcie A.

### <a name="support-for-proxies-that-require-authentication"></a>Obsługa serwerów proxy, które wymagają uwierzytelniania
Gdy za pomocą narzędzia NuGet za serwerem proxy, który wymaga uwierzytelniania, NuGet będzie teraz powodować wyświetlenie monitu o poświadczenia serwera proxy. Wprowadzanie poświadczeń umożliwia rozszerzenie NuGet, aby nawiązać połączenie z repozytorium zdalnego.

### <a name="support-for-repositories-that-require-authentication"></a>Obsługa repozytoria, które wymagają uwierzytelniania
Pakiet NuGet obsługuje obecnie nawiązywania połączenia z [repozytoriów prywatnych](../hosting-packages/local-feeds.md) wymagające basic lub uwierzytelnianie NTLM.

Obsługa uwierzytelniania szyfrowanego zostanie dodana w przyszłej wersji.

### <a name="performance-improvements-to-the-nugetorg-repository"></a>Ulepszenia wydajności w repozytorium nuget.org
Wprowadziliśmy kilka ulepszeń wydajności do galerii nuget.org, aby utworzyć pakiet sporządzanie list i szybsze wyszukiwanie.

### <a name="solution-dialog-project-filtering"></a>Filtrowanie projektu okna dialogowego rozwiązań
W poziomie rozwiązania okna dialogowego, monitując o jakie projektów zainstalować możemy wyświetlić tylko projekty, które są zgodne z wybranym pakietem.

### <a name="package-release-notes"></a>Informacje o wersji pakietu
Pakiety NuGet teraz obejmują wsparcie dla wersji. Informacje o wersji przedstawiać tylko się podczas wyświetlania _aktualizacje_ pakietu, więc nie ma sensu je dodać do swojej pierwszej wersji.

![Informacje o wersji na karcie Aktualizacje](./media/manage-nuget-packages-release-notes.png)

Aby dodać informacje o wersji do pakietu, należy użyć nowego `<releaseNotes />` elementu metadanych w pliku NuSpec.

### <a name="nuspec-ltfiles-gt-improvement"></a>.nuspec & ltfiles /&gt; poprawy
`.nuspec` Pliku teraz umożliwia pusty `<files />` element, który informuje nuget.exe Aby nie zawiera plików w pakiecie.

## <a name="bug-fixes"></a>Poprawki błędów
NuGet w wersji 1.5 miał daje w sumie 107 stałej elementów roboczych. 103 te zostały oznaczone jako błędy.

Aby uzyskać pełną listę prac elementy rozwiązane w NuGet w wersji 1.5, widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Poprawki błędów warte odnotowania:

* [Problem 1273](http://nuget.codeplex.com/workitem/1273): wprowadzone `packages.config` większą kontrolę wersji, przyjazne sortowanie alfabetyczne pakietów i usuwając dodatkowych spacji.
* [Problem 844](http://nuget.codeplex.com/workitem/844): numery wersji są teraz znormalizowane tak, aby `Install-Package 1.0` działa na pakiet z wersją `1.0.0`.
* [Problem 1060](http://nuget.codeplex.com/workitem/1060): podczas tworzenia pakietu przy użyciu nuget.exe, `-Version` Flaga zastąpienia `<version />` elementu.
