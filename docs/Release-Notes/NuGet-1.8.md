---
title: Informacje o wersji NuGet 1.8 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr 1.8 NuGet."
keywords: NuGet 1.8 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 139c30e29d8148eab7298329a07d8e412259e595
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-18-release-notes"></a>Informacje o wersji 1.8 NuGet

[Informacje o wersji NuGet 1.7](../release-notes/nuget-1.7.md) | [NuGet 2.0 informacje o wersji](../release-notes/nuget-2.0.md)

NuGet 1.8 został wydany 23 maj 2012.

## <a name="known-installation-issue"></a>Znane problem
Jeśli korzystasz z VS 2010 z dodatkiem SP1, możesz napotkać błąd instalacji podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.

Obejście jest po prostu odinstalować NuGet, a następnie zainstaluj go z galerii rozszerzeń programu VS.  Zobacz [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) uzyskać więcej informacji, lub [przejdź bezpośrednio do poprawki VS](http://bit.ly/vsixcertfix).

Uwaga: Jeśli program Visual Studio nie pozwalają na odinstalować rozszerzenia (przycisk Odinstaluj jest wyłączony), następnie prawdopodobnie konieczne ponowne uruchomienie programu Visual Studio za pomocą polecenia "Uruchom jako Administrator".

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 niezgodne z systemem Windows XP, poprawki opublikowane

Wkrótce po NuGet 1.8 został zwolniony, dowiedzieliśmy się, że zmiana kryptografii 1.8 spowodowało przerwanie użytkowników w systemie Windows XP.

Ponieważ firma Microsoft wydała poprawkę rozwiązującą ten problem.  Aktualizacja NuGet za pośrednictwem galerii rozszerzeń programu Visual Studio, pojawi się tej poprawki.

## <a name="features"></a>Funkcje

### <a name="satellite-packages-for-localized-resources"></a>Pakiety satelity dla zlokalizowanych zasobów
NuGet 1.8 obsługuje teraz możliwość tworzenia oddzielne pakiety zlokalizowane zasoby, podobnie do funkcji satelickie zestawu programu .NET Framework.  Pakiet satelity jest tworzony w taki sam sposób jak inny pakiet NuGet dodając kilka Konwencji:

* Satelita pakietu identyfikator i nazwa pliku powinna zawierać sufiks, który pasuje do jednej ze standardowych [kultury ciągów używanych przez program .NET Framework](http://msdn.microsoft.com/goglobal/bb896001.aspx).
* W jego `.nuspec` pliku pakietu satelity należy zdefiniować element języka z tej samej ciąg kultury używany w Identyfikatorach
* Pakiet satelity należy zdefiniować zależności w jego `.nuspec` pliku do jego pakietu core, to po prostu pakiet o tym samym identyfikatorze minus sufiks języka.  Pakiet podstawowy musi być dostępny w repozytorium dla pomyślnej instalacji.

Aby zainstalować pakiet z zlokalizowanych zasobów, deweloper jawnie wybiera zlokalizowanego pakietu z repozytorium. Obecnie galerii NuGet nie daje dowolnego rodzaju szczególnego traktowania do pakietów satelity.

![Okno dialogowe Menedżera pakietów z pacakges zlokalizowanych](./media/dlg-w-loc-packs.png)

Ponieważ pakietu satelity zawiera listę zależności do pakietu core, zarówno satelity i podstawowe pakiety są pobierane do folderu pakietów NuGet i zainstalowane.

![Folder pakiety z pakietami zlokalizowanych](./media/fldr-loc-packs.png)

Ponadto podczas instalowania pakietu satelity, NuGet również rozpoznaje konwencji nazewnictwa ciąg kultury i następnie kopiuje zestawu zlokalizowanych zasobów do poprawne podfolderu w pakiecie core, dzięki czemu mogą być pobierane przez program .NET Framework.

![Podstawowe folderu pakietu z folderu skopiowanego zasobu](./media/fldr-copied-loc.png)

Jedną istniejącą usterkę zauważyć z pakietami satelity jest NuGet nie kopiuje zlokalizowanych zasobów do `bin` folderu dla projektów witryny sieci Web.  Ten problem zostanie rozwiązany w następnej wersji programu NuGet.

Dla kompletnego przykładu pokazuje sposób tworzenia i używania pakietów satelity, zobacz [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample).

### <a name="package-restore-consent"></a>Zgody przywracania pakietu
W 1.8 NuGet możemy ustanowić przygotowuje obsługi ważne ograniczenia na Przywracanie pakietu, aby chronić prywatność użytkowników. To ograniczenie wymaga deweloperom tworzenie projektów i rozwiązań, które używają Przywracanie pakietu do jawnie wyrażenia zgody na przywracanie pakietów na przechodzenie do trybu online, aby pobrać pakiety ze źródeł pakietów skonfigurowanych.

Istnieją 2 sposoby zapewnienia tej zgody. Pierwszy znajdują się w pakiet Menedżera okna dialogowego konfiguracji jak pokazano poniżej.  Ta metoda jest przeznaczone głównie dla deweloperów maszyn.

![Okno dialogowe konfiguracji Menedżera pakietów](./media/pr-consent-configdlg.png)

Druga metoda jest ustawiona środowiska zmiennej "EnableNuGetPackageRestore" na wartość "true".  Ta metoda jest przeznaczona dla instalacji nienadzorowanej maszyny, takich jak serwery CI lub kompilacji.

Teraz jak już wspomniano, firma Microsoft ma tylko określone przygotowuje tej funkcji w NuGet 1.8.  W praktyce oznacza to, że podczas dodaliśmy wszystkie logiki, aby włączyć funkcję jest obecnie wymuszone w tej wersji. Zostanie włączona, jednak w następnej wersji programu NuGet, więc możemy się go jak najszybciej, aby odpowiednio skonfigurować środowiska i w związku z tym nie występować po Rozpoczniemy wymuszenia ograniczenia zgody.

Aby uzyskać więcej informacji, zobacz [wpis w blogu zespołu](http://blog.nuget.org/20120518/package-restore-and-consent.html) tę funkcję.

### <a name="nugetexe-performance-improvements"></a>Ulepszenia wydajności nuget.exe
Zmieniając polecenia instalacji, aby pobrać i zainstalować pakiety równolegle NuGet 1.8 wprowadzono znacznej poprawy wydajności nuget.exe — i przez Przywracanie pakietu rozszerzenia.  Wysokiego poziomu testowania pokazuje, że wydajność w przypadku instalowania pakietów 6 w projekcie zwiększa się o około 35% w NuGet 1.8.  Zwiększenie liczby pakietów do 25 zawiera bardziej wydajne około 60%.

## <a name="bug-fixes"></a>Poprawki błędów
NuGet 1.8 zawiera kilka poprawek, ze szczególnym uwzględnieniem konsoli Menedżera pakietów i przepływ pracy przywracania pakietu, szczególnie, co wiąże się zgody przywracania pakietu i integracja z systemem Windows 8 Express.
Pełną listę prac elementów usunięto w wersji NuGet 1.8, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
