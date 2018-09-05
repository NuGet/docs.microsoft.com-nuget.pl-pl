---
title: Informacje o wersji 3.4 RC NuGet
description: Informacje o wersji programu NuGet 3.4 RC obejmuje znane problemy, poprawki błędów, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546757"
---
# <a name="nuget-34-rc-release-notes"></a>Informacje o wersji 3.4 RC NuGet

[Informacje o wersji NuGet 3.3](../release-notes/nuget-3.3.md) | [informacjach o wersji NuGet 3.4](../release-notes/nuget-3.4.md)

NuGet 3.4-RC został wydany 3 marca 2016 wraz z Visual Studio 2015 Update 2 RC i został skompilowany przy użyciu kilku założenia w umysłów:

* Obsługa wielu Platform
* Ulepszenia wydajności
* Drobne ulepszenia interfejsu użytkownika

Następujące funkcje są dostępne w tej wersji RC, kolejne zaplanowane 3.4 ostatecznej wersji.

## <a name="new-features"></a>Nowe funkcje

* Klienci programu NuGet teraz obsługuje gzip kodowania zawartości z repozytoriów
* Obsługa plików PDB z pakietów w kompilowanych projektach xproj
* Obsługa systemów iOS i Android akcji kompilowania w systemach elementu contentFiles
* Obsługa netstandard i netstandardapp monikerów framework

## <a name="new-user-interface-features"></a>Nowe funkcje interfejsu użytkownika

* Znaczne ulepszenia wydajności zwłaszcza na kartach zainstalowany, aktualizacji i Konsolidacja
* Zainstalowany i karty aktualizacje teraz są sortowane alfabetycznie
* Dodaje przycisk odświeżania, która umożliwia wyszukiwanie do odświeżenia

## <a name="updates-and-improvements"></a>Aktualizacje i ulepszenia

* Pakiety, do którego odwołuje się `project.json` , które mają zmiennoprzecinkowy wersji nie będzie aktualizowana przy każdej kompilacji. Zamiast tego zostanie zaktualizowana tylko wtedy, gdy zmuszeni do przywrócenia, czyszczenia, odbudować lub zmodyfikować `project.json`.
* źródeł repozytorium nuget.org już jest zmuszony do konfiguracji projektu, korzystając z interfejsu użytkownika konfiguracji NuGet.
* NuGet nie są już pakiety w udostępnionych projektach ani zapisuje plik blokady.
* Firma Microsoft może udoskonalenia awarii sieci, a następnie ponów próbę obsługi dla serwerów niedostępne lub powolne odpowiedzi.
* Klawiatura i mysz zachowania ulegają poprawie w Interfejsie użytkownika Menedżera pakietów Visual Studio.
* Obsługujemy teraz najnowsze `project.json` schemat środowiska DNX.

## <a name="known-issues"></a>Znane problemy

W dalszym ciągu śledzenia problemów na naszej liście problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)