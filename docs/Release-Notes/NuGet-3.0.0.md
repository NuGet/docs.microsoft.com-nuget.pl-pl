---
title: Informacje o wersji NuGet 3.0 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji programu NuGet 3.0.0 tym — znane problemy, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 3.0.0 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 65251b28093d2ac275053b8bfef6620e16e3fb4a
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-30-release-notes"></a>Informacje o wersji 3.0 NuGet

[Informacje o wersji NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 informacje o wersji](../release-notes/nuget-3.1.md)

NuGet 3.0 został wydany 20 lipca 2015 roku jako rozszerzenie pakietu programu Visual Studio 2015. Firma Microsoft przypisany do dostarczania tej wersji w programie Visual Studio, dzięki czemu kompleksowe środowisko NuGet 3.0 zaktualizowane będzie dostępna dla nowych użytkowników programu Visual Studio. Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.

Firma Microsoft zaleca tych projektantów, którzy mają dostęp do galerii Visual Studio aktualizacji do najnowszej wersji, która jest dostępna, ponieważ będziemy publikowania aktualizacji wkrótce po wydaniu programu Visual Studio 2015, który zawiera obsługę programowania Windows 10.

Łącznie, możemy zamknięte 240 problemów w wersji 3.0 i możesz przejrzeć [pełną listę problemów w serwisie GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Znane problemy

Wiele znanych problemów dostarczone w tej wersji, a wszystkie te elementy zostały usunięte w naszym zaplanowane wersji 3.1 się z wersji systemu Windows 10 w lipcu 29.  Jesteś w stanie zaktualizować rozszerzenia programu Visual Studio z galerii na lub po tym dniu, aby rozwiązać te znane problemy.

*  Nie podano tłumaczenia etykiety "Nie pokazuj ponownie" w oknie Podgląd i etykiety "Autorzy" w oknie Opis pakietu.
*  Gdy pracę nad projektem za pomocą TFS kontroli źródła, NuGet nie może przedstawić Menedżera pakietów interfejsu użytkownika, jeśli plik Nuget.Config jest oznaczony jako tylko do odczytu.
   * **Obejście** wyewidencjonować plik z TFS.
*  Tekst w żółty "pasek ponowne uruchomienie" w oknie programu NuGet Powershell nie jest widoczny, gdy używasz ciemny motyw programu Visual Studio.
   * **Obejście** Użyj motywu jasny Visual Studio.


## <a name="summary-of-top-issues-resolved"></a>Podsumowanie Najważniejsze problemy rozwiązane

* [Wywołuje zaktualizować częste sieci, gdy odświeża okno Menedżera pakietów](https://github.com/NuGet/Home/issues/515)
* [Opóźnienie przewijania zainstalowanym zmiana na widok w Menedżerze pakietów](https://github.com/NuGet/Home/issues/519)
* [Wywołania sieci powinny być uruchamiane w wątku w tle](https://github.com/NuGet/Home/issues/516)
* [Dodano pola wyboru "Nie pokazuj okna podglądu"](https://github.com/NuGet/Home/issues/566)
* [Dodano procesu ograniczania przepustowości, aby zmniejszyć obciążenie procesora](https://github.com/NuGet/Home/issues/356)
* Ulepszona obsługa odwołania portable klasy biblioteki
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Funkcji AutoComplete usługa została z uwzględnieniem wielkości liter](https://github.com/NuGet/Home/issues/198)
* [Aktualizacja ponowne wprowadzenie poświadczeń uwierzytelniania podstawowego](https://github.com/NuGet/Home/issues/456)
* [Rejestrowanie udoskonalone błędów](https://github.com/NuGet/Home/issues/407)
* [Ulepszone środowiska powershell komunikaty o błędach podczas wywoływania metody pakietu aktualizacji](https://github.com/NuGet/Home/issues/5)
* [Stałe link "Dowiedz się więcej na temat opcji", aby uniknąć awarii w systemie Windows 10](https://github.com/NuGet/Home/issues/822)
* [Pamiętaj ustawienie pola wyboru wersji wstępnej](https://github.com/NuGet/Home/issues/732)
* [Ulepszone zbieranie wydajności przez buforowanie wyników wielu projektów w rozwiązaniu](https://github.com/NuGet/Home/issues/721)
* [Można zbierać równolegle wielu pakietów](https://github.com/NuGet/Home/issues/713)
* [Usunięte install-package-force polecenia](https://github.com/NuGet/Home/issues/697)

Można śledzić na [naszym blogu](http://blog.nuget.org) więcej i anonsów uzyskując gotowy do świadczenia pomocy technicznej do tworzenia aplikacji systemu Windows 10.