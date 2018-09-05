---
title: Informacje o wersji 3.4 NuGet
description: Informacje o wersji programu NuGet 3.4, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551194"
---
# <a name="nuget-34-release-notes"></a>Informacje o wersji 3.4 NuGet

[Informacje o wersji 3.4 RC NuGet](../release-notes/nuget-3.4-RC.md) | [informacjach o wersji NuGet 3.4.1](../release-notes/nuget-3.4.1.md)

NuGet 3.4 jako część programu Visual Studio 2015 Update 2 i programu Visual Studio 15 (wersja zapoznawcza) wersji wydanej 30 marca 2016 r. i został skompilowany przy użyciu kilku założenia w umysłów:

* Obsługa wielu Platform
* Ulepszenia wydajności
* Drobne ulepszenia interfejsu użytkownika

Następujące funkcje zostały wcześniej dodane w wersji RC i zostały zaktualizowane lub ukończone w wersji 3.4:

## <a name="new-features"></a>Nowe funkcje

* Klienci programu NuGet teraz obsługuje gzip kodowania zawartości z repozytoriów
* Obsługa plików PDB z pakietów w kompilowanych projektach xproj
* Obsługa systemów iOS i Android akcji kompilowania w systemach elementu contentFiles
* Obsługa netstandard i netstandardapp monikerów framework

## <a name="new-user-interface-features"></a>Nowe funkcje interfejsu użytkownika

* Znaczne ulepszenia wydajności zwłaszcza na kartach zainstalowany, aktualizacji i Konsolidacja
* Łączny źródło wszystkich źródeł pakietów jest dostępne ze scalaniem wynik właściwego wyszukiwania
* Zainstalowany i karty aktualizacje teraz są sortowane alfabetycznie
* Dodaje przycisk odświeżania, która umożliwia wyszukiwanie do odświeżenia
* Najnowsze opcje kompilacji w górnej części listy wersji

## <a name="updates-and-improvements"></a>Aktualizacje i ulepszenia

* Pakiety, do którego odwołuje się `project.json` , które mają zmiennoprzecinkowy wersji nie będzie aktualizowana przy każdej kompilacji. Zamiast tego zostanie zaktualizowana tylko wtedy, gdy zmuszeni do przywrócenia, czyszczenia, odbudować lub zmodyfikować `project.json`.
* źródeł repozytorium nuget.org już jest zmuszony do konfiguracji projektu, korzystając z interfejsu użytkownika konfiguracji NuGet.
* NuGet nie są już pakiety w udostępnionych projektach ani zapisuje plik blokady.
* Firma Microsoft może udoskonalenia awarii sieci, a następnie ponów próbę obsługi dla serwerów niedostępne lub powolne odpowiedzi.
* Klawiatura i mysz zachowania ulegają poprawie w Interfejsie użytkownika Menedżera pakietów Visual Studio.
* Obsługujemy teraz najnowsze `project.json` schemat środowiska DNX.

## <a name="breaking-changes"></a>Fundamentalne zmiany

* Numery wersji pakietu teraz są znormalizowane zgodnie z formatem *głównych*. *drobne*. *poprawka*-*wstępnej* wszystkich głównych i niewielkie i patch są traktowane jako liczby całkowite i usunąć wszelkie zer wiodących.  Wstępne informacje są traktowane jako ciąg i są do niego zastosowane żadne zmiany. Numery te są używane w zapytaniach przez klientów NuGet i wyszukiwania w usłudze nuget.org dostępne.  Więcej szczegółów można znaleźć w dokumentacji systemu NuGet w obszarze [wersji wstępnych](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Znane problemy

* **Problem:** użytkownicy v1511 systemu Windows 10, mogą wystąpić problemy lub nawet awarii programu Visual Studio przy użyciu programu Powershell w programie Visual Studio w następujących scenariuszach:
    * Instalowanie / Odinstalowywanie pakietów, które mają install.ps1 / uninstall.ps1 skryptów
    * Ładowanie projektów, które mają skrypt init.ps1 (na przykład EntityFramework)
    * Publikowanie zawartości sieci web

* **Obejście:** upewnić się, że Twoja instalacja systemu Windows 10 najnowszych poprawek, które są stosowane, expecially styczeń 2016 r. (KB 3124263) lub nowsza aktualizacja.  Więcej informacji jest dostępnych na [problem w usłudze GitHub #1638](http://github.com/nuget/home/issues/1638)

* **Problem:** Przekierowania protokołu NuGet w wersji 2 są przerwane.
Niestandardowe repozytoria NuGet, które przekierowują żądania do alternatywnego hosta, nie uznają żądania przekierowania.
* **Obejście:** Aby obejść ten problem, skonfiguruj identyfikator URI repozytorium pakietów w ustawieniach, aby wskazać lokalizację serwera po przekierowaniu.
Aby uzyskać więcej informacji, zobacz [żądania ściągnięcia serwisu GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).

W dalszym ciągu śledzenia problemów na naszej liście problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)