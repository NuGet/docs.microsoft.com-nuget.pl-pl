---
title: NuGet 3.0 RC2 — informacje o wersji
description: Informacje o wersji programu NuGet 3.0 w wersji RC2 tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545824"
---
# <a name="nuget-30-rc2-release-notes"></a>NuGet 3.0 RC2 — informacje o wersji

[Informacje o wersji programu NuGet 3.0 RC](../release-notes/nuget-3.0-RC.md) | [informacjach o wersji NuGet 3.0](../release-notes/nuget-3.0.0.md)

NuGet 3.0 w wersji RC2 został wydany 3 czerwca 2015 jako tymczasowy wydania dostępne z w galerii Visual Studio 2015 rozszerzenia i [Codeplex](https://nuget.codeplex.com/releases/view/615507). Ta wersja ma kilka ważnych poprawek błędów i ulepszenia wydajności, które będziemy mieli świadomość były ważne, aby zwolnić przed ukończone wersji programu Visual Studio 2015. Ta wersja rozszerzenia NuGet jest dostępna tylko dla programu Visual Studio 2015.

W sumie możemy zamknięcia 158 problemów w tej wersji, i możesz przejrzeć [pełną listę problemów w usłudze GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).

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

Pobierz ten [aktualizacji do rozszerzenie NuGet](https://nuget.codeplex.com/releases/view/615507) z witryny Codeplex i można nadzorować [naszym blogu](http://blog.nuget.org) więcej postępu i anonsów dla pakietów NuGet 3.0!