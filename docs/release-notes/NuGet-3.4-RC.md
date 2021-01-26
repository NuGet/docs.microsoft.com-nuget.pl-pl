---
title: Pakiet NuGet 3,4 — Informacje o wersji RC
description: Informacje o wersji programu NuGet 3,4 RC, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780242"
---
# <a name="nuget-34-rc-release-notes"></a>Pakiet NuGet 3,4 — Informacje o wersji RC

Informacje o wersji narzędzia [NuGet 3,3](../release-notes/nuget-3.3.md)  |  [Informacje o wersji narzędzia NuGet 3,4](../release-notes/nuget-3.4.md)

Pakiet NuGet 3,4-RC został wydana 3 marca, 2016 obok programu Visual Studio 2015 Update 2 RC i został skompilowany za pomocą kilku założenia w zdanie:

* Obsługa wielu platform
* Usprawnienia wydajności
* Ulepszenia pomocniczych interfejsów użytkownika

W tej wersji RC dostępne są następujące funkcje z zaplanowanymi wersjami ostateczną 3,4.

## <a name="new-features"></a>Nowe funkcje

* Klienci NuGet obsługują teraz kodowanie zawartości gzip z repozytoriów
* Obsługa plików PDB z pakietów w projektach xproj
* Obsługa akcji kompilacji dla systemów iOS i Android w elemencie contentFiles
* Obsługa krótkich monikerów struktury netstandardapp

## <a name="new-user-interface-features"></a>Nowe funkcje interfejsu użytkownika

* Znaczące ulepszenia wydajności dotyczące kart zainstalowanych, aktualizacji i konsolidowania
* Karty zainstalowane i aktualizacje są teraz sortowane alfabetycznie
* Dodano przycisk odświeżania, który umożliwia odświeżenie wyszukiwania

## <a name="updates-and-improvements"></a>Aktualizacje i ulepszenia

* Pakiety, do których się odwołują `project.json` , mają przepływającą wersję, nie będą aktualizowane dla każdej kompilacji. Zamiast tego zostaną one zaktualizowane tylko wtedy, gdy zostanie wymuszone przywrócenie, oczyszczenie, odbudowanie lub zmodyfikowanie `project.json` .
* źródła repozytorium nuget.org nie są już wymuszane w konfiguracji projektu podczas korzystania z interfejsu użytkownika konfiguracji NuGet.
* Pakiet NuGet nie przywraca już pakietów w projektach udostępnionych ani nie zapisuje pliku blokady.
* Ulepszono awarię sieci i obsługę ponownych prób w przypadku nieosiągalnych lub wolnych serwerów.
* W interfejsie użytkownika Menedżera pakietów programu Visual Studio Ulepszono zachowania klawiatury i myszy.
* Teraz obsługujemy najnowszy `project.json` schemat w programie środowiska DNX.

## <a name="known-issues"></a>Znane problemy

Będziemy nadal śledzić problemy na naszej liście problemów usługi GitHub, którą można znaleźć w witrynie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)