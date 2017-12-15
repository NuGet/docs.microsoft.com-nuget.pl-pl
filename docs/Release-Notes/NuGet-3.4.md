---
title: Informacje o wersji NuGet 3.4 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 80a429f5-7569-4349-ad7f-4fe9218eac23
description: "Informacje o wersji programu NuGet 3.4, w tym znanych problemów, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 3.4 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 911e4377ad9c8b1f865b0721f43ff73b62df6d1e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 informacje o wersji

[Informacje o wersji 3.4 RC NuGet](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 informacje o wersji](../release-notes/nuget-3.4.1.md)

NuGet 3.4 jako część programu Visual Studio 2015 Update 2 i Visual Studio 15 Preview wersji wydanej 30 marca 2016 i został skompilowany z kilka rozwiązań w umysły:

*  Obsługa Platform
*  Ulepszenia wydajności
*  Drobne ulepszenia interfejsu użytkownika

Następujące funkcje zostały wcześniej dodane w wersji RC i zostały zaktualizowane lub zakończona w wersji 3.4:

## <a name="new-features"></a>Nowe funkcje

* Klienci NuGet obsługuje teraz, kodowania zawartości gzip z repozytoriami
* Obsługa baz danych PDB z pakietów w projektach xproj
* Akcje w elemencie contentFiles kompilacji pomocy technicznej dla systemów iOS i Android
* Obsługa krótkich nazw netstandard i netstandardapp monikerów framework

## <a name="new-user-interface-features"></a>Nowe funkcje interfejsu użytkownika

* Znaczący wzrost wydajności szczególnie na kartach zainstalowane aktualizacje i Konsoliduj
* Źródła agregowania wszystkie źródła pakietów jest dostępna w programie scalanie wynik wyszukiwania właściwego
* Zainstalowane i aktualizacje kartach teraz są posortowane alfabetycznie
* Dodaje przycisk Odśwież, która umożliwia wyszukiwanie, którego chcesz odświeżyć
* Najnowsze opcje kompilacji w górnej części listy wersji

## <a name="updates-and-improvements"></a>Aktualizacje i usprawnienia

* Pakiety, do którego odwołuje się `project.json` , która ma zmiennoprzecinkową wersji nie będzie aktualizowany przy każdej kompilacji. Zamiast tego zostanie zaktualizowana tylko wtedy, gdy wymusić przywracanie, czyszczenia, odbudować lub zmodyfikować `project.json`.
* źródłach repozytoriów nuget.org już zostało wymuszone w konfiguracji projektu, korzystając z interfejsu użytkownika konfiguracji NuGet.
* NuGet już przywraca pakietów w udostępnionych projektów nie zapisuje plik blokady.
* Firma Microsoft została ulepszona awarii sieci, a następnie spróbuj ponownie obsługi dla serwerów jest nieosiągalny lub powolne na odpowiedź.
* Klawiatura i mysz zachowania ulegają poprawie w Interfejsie użytkownika Menedżera pakietów programu Visual Studio.
* Obsługujemy teraz najnowszej `project.json` schematu w DNX.

## <a name="breaking-changes"></a>Fundamentalne zmiany

* Numery wersji pakietu są teraz znormalizowane do formatu *głównych*. *drobne*. *poprawka*-*wstępnej* poszczególnych głównych i pomocnicze i poprawki są traktowane jako liczby całkowite i upuść żadnych zera wiodące.  Wstępna informacje są traktowane jako ciąg, a żadne zmiany nie są stosowane do niego. Numery te są używane w zapytaniach klientów NuGet i udostępniony przez usługę nuget.org wyszukiwania.  Więcej informacji znajduje się w Docs NuGet w obszarze [wersji wstępnej](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Znane problemy

* **Problem:** użytkownicy v1511 systemu Windows 10 mogą wystąpić problemy lub nawet awarii programu Visual Studio przy użyciu programu Powershell w programie Visual Studio w następujących scenariuszach:
    * Instalowanie / Odinstalowywanie pakiety, które mają install.ps1 / uninstall.ps1 skryptów
    * Ładowanie projektów, które mają skrypt init.ps1 (na przykład EntityFramework)
    * Publikowanie zawartości sieci web

* **Obejście problemu:** upewnij się, że instalacji systemu Windows 10 ma najnowsze poprawki zastosowane, expecially styczeń 2016 r. (KB 3124263) lub późniejszą aktualizację.  Szczegółowe informacje są dostępne na [problem GitHub #1638](http://github.com/nuget/home/issues/1638)

* **Problem:** Przekierowania protokołu NuGet w wersji 2 są przerwane.
Niestandardowe repozytoria NuGet, które przekierowują żądania do alternatywnego hosta, nie uznają żądania przekierowania.
* **Obejście problemu:** Aby obejść ten problem, należy skonfigurować identyfikator URI repozytorium pakietów w ustawieniach, aby wskazać lokalizację serwera po przekierowaniu.
Aby uzyskać więcej informacji, zobacz [żądania ściągnięcia GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).

W dalszym ciągu do śledzenia problemów w naszej listy problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)