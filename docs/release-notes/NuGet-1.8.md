---
title: Informacje o wersji narzędzia NuGet 1,8
description: Informacje o wersji programu NuGet 1,8, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8dd0fff88424c516d8b894412d07dcc53af19265
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777106"
---
# <a name="nuget-18-release-notes"></a>Informacje o wersji narzędzia NuGet 1,8

Informacje o wersji narzędzia [NuGet 1,7](../release-notes/nuget-1.7.md)  |  [Informacje o wersji narzędzia NuGet 2,0](../release-notes/nuget-2.0.md)

Pakiet NuGet 1,8 został wydaną 23 maja 2012.

## <a name="known-installation-issue"></a>Znany problem z instalacją
W przypadku korzystania z programu VS 2010 z dodatkiem SP1 można napotkać błąd instalacji podczas próby uaktualnienia narzędzia NuGet, jeśli jest zainstalowana starsza wersja.

Obejście polega na prostu odinstalować pakiet NuGet, a następnie zainstalować go z galerii rozszerzeń programu VS.  Zobacz <https://support.microsoft.com/kb/2581019> , aby uzyskać więcej informacji, lub [Przejdź bezpośrednio do poprawki programu vs](http://bit.ly/vsixcertfix).

Uwaga: Jeśli program Visual Studio nie zezwoli na odinstalowanie rozszerzenia (przycisk Odinstaluj jest wyłączony), prawdopodobnie trzeba będzie ponownie uruchomić program Visual Studio za pomocą polecenia "Uruchom jako administrator".

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>Program NuGet 1,8 niezgodny z systemem Windows XP, Poprawka opublikowana

Wkrótce po wydaniu programu NuGet 1,8 zapoznaj się ze zmianą kryptografii w 1,8 niezłamanych użytkowników w systemie Windows XP.

Od czasu wydania poprawki, która rozwiązuje ten problem.  Dzięki aktualizacji pakietu NuGet za pomocą galerii rozszerzeń programu Visual Studio otrzymujesz tę poprawkę.

## <a name="features"></a>Funkcje

### <a name="satellite-packages-for-localized-resources"></a>Pakiety satelickie dla zlokalizowanych zasobów
Program NuGet 1,8 obsługuje teraz możliwość tworzenia oddzielnych pakietów dla zlokalizowanych zasobów, podobnie jak w przypadku zestawów satelitarnych .NET Framework.  Pakiet satelitarny jest tworzony w taki sam sposób jak każdy inny pakiet NuGet z dodaniem kilku Konwencji:

* Identyfikator pakietu satelickiego i nazwa pliku powinny zawierać sufiks zgodny z jednym z standardowych [ciągów kultur używanych przez .NET Framework](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).
* W swoim `.nuspec` pliku pakiet satelitarny powinien definiować element języka z tym samym ciągiem kultury użytym w identyfikatorze
* Pakiet satelitarny powinien definiować zależność w jej `.nuspec` pliku z pakietem podstawowym, który jest po prostu pakietem o takim samym identyfikatorze minus sufiks języka.  Aby instalacja powiodła się, pakiet podstawowy musi być dostępny w repozytorium.

Aby zainstalować pakiet z zlokalizowanymi zasobami, deweloper jawnie wybiera zlokalizowany pakiet z repozytorium. W tej chwili Galeria NuGet nie zapewnia żadnego specjalnego traktowania pakietów satelitarnych.

![Okno dialogowe Menedżera pakietów z zlokalizowaną pacakges](./media/dlg-w-loc-packs.png)

Ze względu na to, że pakiet satelicki zawiera zależność od pakietu podstawowego, pakiety satelickie i podstawowe są pobierane do folderu pakiety NuGet i instalowane.

![Folder pakietów z zlokalizowanymi pakietami](./media/fldr-loc-packs.png)

Ponadto podczas instalowania pakietu satelity program NuGet rozpoznaje także konwencję nazewnictwa ciągów kulturowych, a następnie kopiuje zlokalizowany zestaw zasobów do poprawnego podfolderu w ramach pakietu podstawowego, dzięki czemu może być wybrany przez .NET Framework.

![Podstawowy folder pakietu ze skopiowanym folderem zasobów](./media/fldr-copied-loc.png)

Jedną z istniejących usterek, które należy zwrócić do pakietów satelitarnych, jest to, że NuGet nie kopiuje zlokalizowanych zasobów do `bin` folderu dla projektów witryny sieci Web.  Ten problem zostanie rozwiązany w następnej wersji programu NuGet.

Aby uzyskać kompletny przykład pokazujący sposób tworzenia i używania pakietów satelitarnych, zobacz [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample) .

### <a name="package-restore-consent"></a>Wyrażanie zgody na przywracanie pakietu
W pakiecie NuGet 1,8 podstawę do obsługi ważnego ograniczenia dotyczącego przywracania pakietów, aby chronić prywatność użytkowników. To ograniczenie wymaga, aby deweloperzy tworzący projekty i rozwiązania korzystające z przywracania pakietów mogli jawnie wyrazić zgodę na pobieranie pakietów ze skonfigurowanych źródeł pakietów do trybu online.

Istnieją 2 sposoby zapewnienia tej zgody. Pierwszy można znaleźć w oknie dialogowym konfiguracji Menedżera pakietów, jak pokazano poniżej.  Ta metoda jest przeznaczona głównie dla maszyn deweloperskich.

![Okno dialogowe konfiguracji Menedżera pakietów](./media/pr-consent-configdlg.png)

Druga metoda polega na ustawieniu zmiennej środowiskowej "EnableNuGetPackageRestore" na wartość "true".  Ta metoda jest przeznaczona dla maszyn nienadzorowanych, takich jak serwery CI lub serwer kompilacji.

Teraz, zgodnie z powyższymi przepisami, podstawę dla tej funkcji w programie NuGet 1,8.  Praktycznie oznacza to, że podczas dodawania wszystkich logiki w celu włączenia tej funkcji nie jest ona obecnie wymuszana w tej wersji. Zostanie ona włączona, jednak w następnej wersji programu NuGet, dlatego chcemy wiedzieć, jak najszybciej, tak szybko, jak to możliwe, aby można było odpowiednio skonfigurować środowiska i nie wpłynie to na to, kiedy zacznie wymuszać ograniczenie zgody.

Aby uzyskać więcej informacji, zobacz [wpis w blogu zespołu](http://blog.nuget.org/20120518/package-restore-and-consent.html) dotyczący tej funkcji.

### <a name="nugetexe-performance-improvements"></a>Udoskonalenia wydajności nuget.exe
Modyfikując polecenie instalacji, aby pobrać i zainstalować pakiety równolegle, pakiet NuGet 1,8 zapewnia znaczną poprawę wydajności nuget.exe — i przez przywrócenie pakietu rozszerzenia.  Testowanie wysokiego poziomu pokazuje, że wydajność instalowania 6 pakietów w projekcie usprawnia się o około 35% w pakiecie NuGet 1,8.  Zwiększenie liczby pakietów na 25 pokazuje wzrost wydajności dotyczący około 60%.

## <a name="bug-fixes"></a>Poprawki błędów
Pakiet NuGet 1,8 zawiera kilka poprawek błędów z naciskiem na konsolę Menedżera pakietów i przepływ pracy przywracania pakietów, szczególnie w odniesieniu do zgody na przywracanie pakietów i integrację systemu Windows 8 Express.
Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 1,8, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).