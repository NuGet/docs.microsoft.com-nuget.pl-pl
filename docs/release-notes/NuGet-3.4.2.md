---
title: Informacje o wersji NuGet 3.4.2
description: Informacje o wersji programu NuGet 3.4.2 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4c8aa75df822ca5b2f1c4bd274272218f16ad917
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549154"
---
# <a name="nuget-342-release-notes"></a>Informacje o wersji NuGet 3.4.2

[Informacje o wersji NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [informacjach o wersji NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 została wydana 8 kwietnia 2016, aby rozwiązać wiele problemów, które zostały zidentyfikowane w 3.4 i 3.4.1 wydania.

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC jest teraz dostępna

Możesz pobrać wersję Release candidate programu nuget.exe 3.4.2 [tutaj](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aktualizacje i ulepszenia

* Znacznie ulepszyliśmy wydajności aktualizacji konkretnego scenariusza, w którym aktualizacje w pakietach za pomocą wykresów zależności głębokiego bardzo dużo czasu i nieuruchamianie programu Visual Studio.
* Przywracanie pakietów nuget bez ruch sieciowy jest 2,5 x — 3 x szybciej w programie Visual Studio.
* Poza tą zmianą usunęliśmy problem gdzie możemy zostały osiągnięcia sieci dwa razy, gdy jest to pobieranie aktualizacji licznik w Interfejsie użytkownika programu VS. Taka konfiguracja była częściowo odpowiada dla niektórych klientów problemy dotyczące limitu czasu w 3.4/3.4.1.
* Dodano obsługę ustawienia no_proxy

## <a name="fixes"></a>Poprawki

* Rozwiązano problem, w którym źródło nuget.org brakowało w NuGet ustawienia lub konfiguracji po aktualizacji do 3.4.1.
* Rozwiązano problem, w którym zmiany wielkości liter do FindPackagesById 3.4.1 przerywa Artifactory.
* Rozwiązany problem z trybem FIPS powodującą błędy dzięki funkcji przywracania NuGet za pomocą nuget.exe.
* Naprawiono awarię podczas przeglądania źródła za pomocą adresu URL nieprawidłowa ikona.
* Rozwiązane problemy ze scalaniem wersje i wpisy z "Wszystkie źródła".

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Znane problemy w 3.4.2 Windows x86 wiersza polecenia (RC)

Te problemy zostaną naprawione wczesne Następny tydzień przed osiągnęliśmy RTM.

*  Uruchomione Przywracanie nuget dla rozwiązania zakończy się niepowodzeniem, jeśli plik rozwiązania jest umieszczany w hierarchię folderów niższe niż pliki projektu.
*  Uruchomienie polecenia delete nuget na pakiet przy użyciu źródła danych w wersji 2 nie powiedzie się. Zamiast tego użyj wersji 3 źródła danych.


Aby uzyskać pełną listę poprawek i udoskonaleń w tej wersji, zapoznaj się z listy problemów dotyczących [tutaj](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).