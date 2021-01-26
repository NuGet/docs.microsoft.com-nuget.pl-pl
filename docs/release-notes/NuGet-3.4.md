---
title: Informacje o wersji narzędzia NuGet 3,4
description: Informacje o wersji programu NuGet 3,4, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776414"
---
# <a name="nuget-34-release-notes"></a>Informacje o wersji narzędzia NuGet 3,4

Pakiet [NuGet 3,4 — informacje](../release-notes/nuget-3.4-RC.md)  |  o wersji RC [Informacje o wersji pakietu NuGet](../release-notes/nuget-3.4.1.md)

Pakiet NuGet 3,4 został zwolniony 30 marca 2016 w ramach programu Visual Studio 2015 Update 2 i programu Visual Studio 15 Preview i został skompilowany za pomocą kilku założenia w zdanie:

* Obsługa wielu platform
* Usprawnienia wydajności
* Ulepszenia pomocniczych interfejsów użytkownika

Następujące funkcje zostały wcześniej dodane do wersji RC i zostały zaktualizowane lub ukończone dla wydania 3,4:

## <a name="new-features"></a>Nowe funkcje

* Klienci NuGet obsługują teraz kodowanie zawartości gzip z repozytoriów
* Obsługa plików PDB z pakietów w projektach xproj
* Obsługa akcji kompilacji dla systemów iOS i Android w elemencie contentFiles
* Obsługa krótkich monikerów struktury netstandardapp

## <a name="new-user-interface-features"></a>Nowe funkcje interfejsu użytkownika

* Znaczące ulepszenia wydajności dotyczące kart zainstalowanych, aktualizacji i konsolidowania
* Zagregowane Źródło "wszystkie źródła pakietów" jest dostępne z prawidłowym scalaniem wyników wyszukiwania
* Karty zainstalowane i aktualizacje są teraz sortowane alfabetycznie
* Dodano przycisk odświeżania, który umożliwia odświeżenie wyszukiwania
* Najnowsze opcje kompilacji w górnej części listy wersji

## <a name="updates-and-improvements"></a>Aktualizacje i ulepszenia

* Pakiety, do których się odwołują `project.json` , mają przepływającą wersję, nie będą aktualizowane dla każdej kompilacji. Zamiast tego zostaną one zaktualizowane tylko wtedy, gdy zostanie wymuszone przywrócenie, oczyszczenie, odbudowanie lub zmodyfikowanie `project.json` .
* źródła repozytorium nuget.org nie są już wymuszane w konfiguracji projektu podczas korzystania z interfejsu użytkownika konfiguracji NuGet.
* Pakiet NuGet nie przywraca już pakietów w projektach udostępnionych ani nie zapisuje pliku blokady.
* Ulepszono awarię sieci i obsługę ponownych prób w przypadku nieosiągalnych lub wolnych serwerów.
* W interfejsie użytkownika Menedżera pakietów programu Visual Studio Ulepszono zachowania klawiatury i myszy.
* Teraz obsługujemy najnowszy `project.json` schemat w programie środowiska DNX.

## <a name="breaking-changes"></a>Zmiany powodujące niezgodność

* Numery wersji pakietu są teraz znormalizowane w formacie *głównym*. *pomocnicze*. *poprawka* - *wersja wstępna*   Każda z głównych, pomocniczych i poprawek jest traktowana jako liczba całkowita i upuszczania wiodących zer.  Informacje o wersji wstępnej są traktowane jako ciąg i nie są do niego stosowane żadne zmiany. Te liczby są używane w zapytaniach przez klientów NuGet i wyszukiwaniech dostarczonych przez usługę nuget.org.  Więcej informacji można znaleźć w dokumentacji pakietu NuGet w obszarze [wersje wstępne](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Znane problemy

* **Problem:** Użytkownicy systemu Windows 10 v1511 mogą napotkać problemy, a nawet program Visual Studio w programie PowerShell w programie Visual Studio w następujących scenariuszach:
    * Instalowanie/Odinstalowywanie pakietów, które mają skrypty install.ps1/uninstall.ps1
    * Ładowanie projektów, które mają skrypt init.ps1 (na przykład EntityFramework)
    * Publikowanie zawartości sieci Web

* **Obejście problemu:** Upewnij się, że w instalacji systemu Windows 10 zostały zastosowane najnowsze poprawki, expecially 2016 stycznia (KB 3124263) lub nowszą.  Więcej szczegółów można znaleźć w witrynie [GitHub #1638](http://github.com/nuget/home/issues/1638)

* **Problem:** Przekierowania protokołu NuGet w wersji 2 są przerwane.
Niestandardowe repozytoria NuGet, które przekierowują żądania do alternatywnego hosta, nie uznają żądania przekierowania.
* **Obejście problemu:**  Aby obejść ten problem, należy skonfigurować identyfikator URI repozytorium pakietów w ustawieniach, aby wskazywał lokalizację serwera przekierowanego.
Aby uzyskać więcej informacji, zobacz [#387 żądania ściągnięcia usługi GitHub](https://github.com/NuGet/NuGet.Client/pull/387).

Będziemy nadal śledzić problemy na naszej liście problemów usługi GitHub, którą można znaleźć w witrynie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)