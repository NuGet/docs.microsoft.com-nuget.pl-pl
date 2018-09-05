---
title: Informacje o wersji 1.8 NuGet
description: Informacje o wersji programu NuGet 1.8, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ff6d12606b1bed479e63eebccd978ff9cd4a7faf
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546624"
---
# <a name="nuget-18-release-notes"></a>Informacje o wersji 1.8 NuGet

[Informacje o wersji NuGet 1.7](../release-notes/nuget-1.7.md) | [informacjach o wersji NuGet w wersji 2.0](../release-notes/nuget-2.0.md)

NuGet 1.8 została wydana 23 maja 2012.

## <a name="known-installation-issue"></a>Problem z instalacją znane
Jeśli używasz programu VS 2010 z dodatkiem SP1, możesz napotkać błąd instalacji podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.

Obejście polega na po prostu Odinstaluj NuGet, a następnie zainstalować go z galerii rozszerzeń programu VS.  Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) uzyskać więcej informacji, lub [przejdź bezpośrednio do poprawki programu VS](http://bit.ly/vsixcertfix).

Uwaga: Jeśli program Visual Studio nie pozwalają na odinstalować rozszerzenie (przycisk Odinstaluj jest wyłączony), prawdopodobnie musisz ponownie program Visual Studio za pomocą polecenia "Uruchom jako Administrator".

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 niezgodne w systemie Windows XP poprawkę opublikowane

Wkrótce po opublikowaniu NuGet 1.8 został dowiedzieliśmy się, że zmiana kryptografii 1.8 Przerwano użytkowników dla Windows XP.

Ponieważ firma Microsoft wydała poprawkę rozwiązującą ten problem.  Aktualizowanie NuGet za pomocą galerii rozszerzeń programu Visual Studio, otrzymasz tej poprawki.

## <a name="features"></a>Funkcje

### <a name="satellite-packages-for-localized-resources"></a>Pakiety satelity dla zlokalizowane zasoby
NuGet 1.8 teraz obsługuje możliwość tworzenia oddzielne pakiety do zlokalizowanych zasobów, podobne do funkcji zestawu satelickiego programu .NET Framework.  Pakiet satelitarnej jest tworzony w taki sam sposób, jak każdy inny pakiet NuGet dodając kilka Konwencji:

* Satelitarne pakietu identyfikator i nazwa pliku powinna zawierać sufiks, który pasuje do jednej ze standardowych [kulturze ciągów używanych przez program .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* W jego `.nuspec` pliku pakietu satelitarnej należy zdefiniować element języka przy użyciu tego samego ciąg kultury, używane w identyfikatorze
* Pakiet satelitarnej należy zdefiniować zależności w jego `.nuspec` plik, aby jego pakiet core, który jest po prostu pakiet o tym samym identyfikatorze minus sufiksu języka.  Pakiet podstawowego musi być dostępny w repozytorium dla pomyślnej instalacji.

Aby zainstalować pakiet z zlokalizowane zasoby, deweloper jawnie wybiera zlokalizowanego pakietu z repozytorium. W chwili obecnej galerii pakietów NuGet nie daje dowolnego rodzaju specjalnego traktowania, aby pakiety satelity.

![Okno dialogowe Menedżer pakietów z pacakges zlokalizowane](./media/dlg-w-loc-packs.png)

Ponieważ pakiet satelitarnej zawiera zależność do jego pakiet podstawowego, satelitarne i core pakiety są pobierane do folderu pakietów NuGet i zainstalowane.

![Folder Packages z zlokalizowanych pakietów](./media/fldr-loc-packs.png)

Ponadto podczas instalowania pakietu satelity, NuGet rozpoznaje również konwencji nazewnictwa ciąg kultury i następnie kopiuje zestawu zlokalizowanych zasobów w podfolderach poprawny pakiet podstawowego, dzięki czemu mogą być pobierane przez program .NET Framework.

![Folder pakietu Core za pomocą folderu skopiowanego zasobu](./media/fldr-copied-loc.png)

Istniejącą usterkę należy pamiętać, za pomocą pakietów satelitarnej jest NuGet nie kopiuje zlokalizowane zasoby do `bin` folder dla projektów witryny sieci Web.  Ten problem zostanie rozwiązany w kolejnej wersji programu NuGet.

Pełny przykład ukazujące sposób tworzenia i używania pakietów satelickich, zobacz [ https://github.com/NuGet/SatellitePackageSample ](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Zgoda Przywracanie pakietu
W 1.8 NuGet możemy określić podwaliny pod Projekt wdrożenia do obsługi ważnych ograniczenie Przywracanie pakietu, aby chronić prywatność użytkowników. To ograniczenie nie wymaga deweloperów tworzących projektów i rozwiązań, które są przy użyciu funkcji przywracania pakietów jawnie zgody, aby utworzyć pakiet przywracania przez przejście do trybu online, pobrać pakiety ze źródeł skonfigurowanym pakietu.

Istnieją 2 sposoby na to zgody. Pierwszy znajdują się w pakietu Menedżera okna dialogowego konfiguracji jak pokazano poniżej.  Ta metoda jest przeznaczone głównie dla deweloperów maszyn.

![Okno dialogowe konfiguracji Menedżera pakietów](./media/pr-consent-configdlg.png)

Druga metoda jest należy ustawić środowisko zmiennej "EnableNuGetPackageRestore" na wartość "true".  Ta metoda jest przeznaczona dla instalacji nienadzorowanej maszyn, takich jak serwery ciągłą Integrację lub kompilację.

Teraz jak wspomniano powyżej, firma Microsoft ma tylko określić podwaliny pod Projekt wdrożenia dla tej funkcji w NuGet 1.8.  W praktyce oznacza to, że gdy dodaliśmy całą logikę do włączenia tej funkcji jest nie jest obecnie wymuszana w tej wersji. Zostaną włączone, jednak w ciągu następnych wersji programu NuGet, więc Chcieliśmy, aby uświadomić możesz go tak szybko, jak to możliwe, aby odpowiednio skonfigurować środowiska i w związku z tym nie wpływać na gdy Rozpoczniemy wymuszać ograniczenia zgody.

Aby uzyskać więcej informacji, zobacz [wpis w blogu zespołu](http://blog.nuget.org/20120518/package-restore-and-consent.html) na temat tej funkcji.

### <a name="nugetexe-performance-improvements"></a>Ulepszenia wydajności nuget.exe
Po zmodyfikowaniu polecenie instalacji, aby pobrać i zainstalować pakiety w sposób równoległy, NuGet 1.8 zapewniają znacznej poprawy wydajności do nuget.exe — i przywracanie pakietu rozszerzenia.  Wysokiego poziomu testowanie pokazuje, że wydajność w przypadku instalowania pakietów 6 do projektu zwiększa się o około 35% w NuGet 1.8.  Zwiększenie liczby pakietów do 25 przedstawia bardziej wydajne około 60%.

## <a name="bug-fixes"></a>Poprawki błędów
NuGet 1.8 zawiera sporo poprawki błędów, z naciskiem na konsoli Menedżera pakietów i przepływ pracy przywracania pakietów, szczególnie w przypadku, w odniesieniu do integracji systemu Windows 8 Express i zgody przywracania pakietu.
Aby uzyskać pełną listę prac elementy rozwiązane w NuGet 1.8, widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
