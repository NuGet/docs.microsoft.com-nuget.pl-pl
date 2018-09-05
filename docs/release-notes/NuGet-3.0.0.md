---
title: Informacje o wersji 3.0 NuGet
description: Informacje o wersji programu NuGet 3.0.0 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551866"
---
# <a name="nuget-30-release-notes"></a>Informacje o wersji 3.0 NuGet

[Informacje o wersji programu NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [informacjach o wersji NuGet 3.1](../release-notes/nuget-3.1.md)

NuGet 3.0 został wydany 20 lipca 2015 roku jako rozszerzenie pakietu Visual Studio 2015. Przeprowadziliśmy się do świadczenia tej wersji programu Visual Studio, tak aby pełnego środowiska pracy zaktualizowanych pakietów NuGet 3.0 będą dostępne dla nowych użytkowników programu Visual Studio. Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.

Firma Microsoft zaleca tych deweloperów, które mają dostęp do aktualizacji galerii programu Visual Studio do najnowszej wersji, która jest dostępna, ponieważ obecnie publikujemy aktualizacji wkrótce po wydaniu programu Visual Studio 2015, który zawiera obsługę programowania aplikacji dla systemu Windows 10.

W sumie możemy zamknięte 240 problemy w wersji 3.0 i możesz przejrzeć [pełną listę problemów w usłudze GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).

## <a name="known-issues"></a>Znane problemy

Wiele znanych problemów dostarczone w tej wersji, a wszystkie te elementy zostały usunięte w wersji 3.1 zaplanowanego postoju wersji systemu Windows 10 na 29 lipca.  Jesteś w stanie zaktualizować rozszerzenia programu Visual Studio z galerii na lub po tej dacie, aby rozwiązać te znane problemy.

*  Tłumaczenie nie jest dostępna do etykiety "Nie pokazuj ponownie", w oknie Podgląd i etykiety "Autorzy" w oknie Opis pakietu.
*  Podczas pracy nad projektem przy użyciu serwera TFS kontroli źródła NuGet nie może przedstawiać Menedżera pakietów interfejsu użytkownika, jeśli plik Nuget.Config jest oznaczony jako tylko do odczytu.
   * **Obejście** wyewidencjonować plik z serwera TFS.
*  Tekst w kolorze żółtym "bar ponowne uruchomienie" w oknie programu NuGet Powershell nie jest widoczny, gdy używasz ciemnego motywu programu Visual Studio.
   * **Obejście** Użyj motyw jasny programu Visual Studio.


## <a name="summary-of-top-issues-resolved"></a>Podsumowanie Najważniejsze problemy rozwiązane

* [Aktualizacja sieci częste wywołania podczas odświeżania okno Menedżera pakietów](https://github.com/NuGet/Home/issues/515)
* [Opóźnione przewijania zainstalowanym zmiana na widok w Menedżerze pakietów](https://github.com/NuGet/Home/issues/519)
* [Wywołania sieciowe powinien zostać uruchomiony na wątku w tle](https://github.com/NuGet/Home/issues/516)
* [Dodano pole wyboru "Nie pokazuj okna (wersja zapoznawcza)"](https://github.com/NuGet/Home/issues/566)
* [Dodano proces ograniczania przepustowości, aby zmniejszyć obciążenie procesora](https://github.com/NuGet/Home/issues/356)
* Ulepszona obsługa odwołanie do biblioteki w przypadku klas przenośna
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [Usługa autouzupełniania była uwzględniana wielkość liter](https://github.com/NuGet/Home/issues/198)
* [Aktualizacja ponownie wprowadzić poświadczenia uwierzytelniania podstawowego](https://github.com/NuGet/Home/issues/456)
* [Rejestrowanie udoskonalone błędów](https://github.com/NuGet/Home/issues/407)
* [Powershell Ulepszone komunikaty o błędach podczas wywoływania pakiet aktualizacji](https://github.com/NuGet/Home/issues/5)
* [Naprawiono link "Dowiedz się więcej na temat opcji", aby uniknąć awarii w systemie Windows 10](https://github.com/NuGet/Home/issues/822)
* [Pamiętaj ustawienie pola wyboru wersji wstępnej](https://github.com/NuGet/Home/issues/732)
* [Zbieranie ulepszoną wydajność przez buforowanie wyników w projektach w rozwiązaniu](https://github.com/NuGet/Home/issues/721)
* [Wiele pakietów można gromadzić równolegle](https://github.com/NuGet/Home/issues/713)
* [Usunięte install-package-force polecenia](https://github.com/NuGet/Home/issues/697)

Można nadzorować [naszym blogu](http://blog.nuget.org) więcej postępu i anonse uzyskując chcesz zaoferować wsparcie dla programowania systemu Windows 10.