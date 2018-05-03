---
title: Informacje o wersji 3.4 RC NuGet
description: Informacje o wersji programu NuGet 3.4 RC tym znanych problemów, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e40d685a5256fdfee818f0cc1f1bc352c698f3c2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-34-rc-release-notes"></a>Informacje o wersji 3.4 RC NuGet

[Informacje o wersji NuGet 3.3](../release-notes/nuget-3.3.md) | [NuGet 3.4 informacje o wersji](../release-notes/nuget-3.4.md)

NuGet 3.4-RC został wydany 3 marca 2016 obok programu Visual Studio 2015 Update 2 RC i został skompilowany z kilka rozwiązań w umysły:

* Obsługa Platform
* Ulepszenia wydajności
* Drobne ulepszenia interfejsu użytkownika

Następujące funkcje są dostępne w tej wersji RC z planowane 3.4 ostatecznej wersji.

## <a name="new-features"></a>Nowe funkcje

* Klienci NuGet obsługuje teraz, kodowania zawartości gzip z repozytoriami
* Obsługa baz danych PDB z pakietów w projektach xproj
* Akcje w elemencie contentFiles kompilacji pomocy technicznej dla systemów iOS i Android
* Obsługa krótkich nazw netstandard i netstandardapp monikerów framework

## <a name="new-user-interface-features"></a>Nowe funkcje interfejsu użytkownika

* Znaczący wzrost wydajności szczególnie na kartach zainstalowane aktualizacje i Konsoliduj
* Zainstalowane i aktualizacje kartach teraz są posortowane alfabetycznie
* Dodaje przycisk Odśwież, która umożliwia wyszukiwanie, którego chcesz odświeżyć

## <a name="updates-and-improvements"></a>Aktualizacje i usprawnienia

* Pakiety, do którego odwołuje się `project.json` , która ma zmiennoprzecinkową wersji nie będzie aktualizowany przy każdej kompilacji. Zamiast tego zostanie zaktualizowana tylko wtedy, gdy wymusić przywracanie, czyszczenia, odbudować lub zmodyfikować `project.json`.
* źródłach repozytoriów nuget.org już zostało wymuszone w konfiguracji projektu, korzystając z interfejsu użytkownika konfiguracji NuGet.
* NuGet już przywraca pakietów w udostępnionych projektów nie zapisuje plik blokady.
* Firma Microsoft została ulepszona awarii sieci, a następnie spróbuj ponownie obsługi dla serwerów jest nieosiągalny lub powolne na odpowiedź.
* Klawiatura i mysz zachowania ulegają poprawie w Interfejsie użytkownika Menedżera pakietów programu Visual Studio.
* Obsługujemy teraz najnowszej `project.json` schematu w DNX.

## <a name="known-issues"></a>Znane problemy

W dalszym ciągu śledzenie problemów w naszej listy problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)