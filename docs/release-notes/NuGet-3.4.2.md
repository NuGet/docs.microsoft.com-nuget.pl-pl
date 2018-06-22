---
title: Informacje o wersji NuGet 3.4.2
description: Informacje o wersji programu NuGet 3.4.2 tym — znane problemy, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 88d29a84e280433663ab6c1c04ae16e1329420f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819669"
---
# <a name="nuget-342-release-notes"></a>Informacje o wersji NuGet 3.4.2

[Informacje o wersji NuGet 3.4.1](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 informacje o wersji](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 został wydany 8 kwietnia 2016, aby rozwiązać pewne problemy, które zostały zidentyfikowane w wersji 3.4 i 3.4.1 wersji.

## <a name="nugetexe-342-rc-is-now-available"></a>RC nuget.exe 3.4.2 jest teraz dostępna

Można pobrać wersji release candidate nuget.exe 3.4.2 [tutaj](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aktualizacje i usprawnienia

* Firma Microsoft ma znaczne zwiększenie wydajności aktualizacji w konkretnych sytuacji, gdy aktualizacje dla pakietów wykresami zależności bezpośrednich przez bardzo długi czas i zawiesił Visual Studio.
* Przywracanie nuget bez ruch sieciowy jest 2,5 x – 3 x szybsze w programie Visual Studio.
* Oprócz tej zmiany został rozwiązany problem gdzie możemy zostały naciśnięcie sieci dwa razy, gdy liczba pobierania aktualizacji w Interfejsie użytkownika programu VS. To jest częściowo odpowiedzialny za niektórzy klienci problemów limitu czasu w wersji 3.4/3.4.1.
* Dodano obsługę ustawienie no_proxy

## <a name="fixes"></a>Poprawki

* Rozwiązano problem, na którym nuget.org źródła brakowało w ustawieniach NuGet lub konfiguracji po zaktualizowaniu do 3.4.1.
* Rozwiązano problem, w którym zmiany wielkości liter FindPackagesById w 3.4.1 dzieli Artifactory.
* Rozwiązany problem z FIPS powodujący błędy z Przywracanie NuGet z nuget.exe.
* Stała awarii podczas przeglądania źródła z ikoną nieprawidłowy adres URL.
* Rozwiązane problemy z scalania wersji i pozycje "Wszystkie źródła".

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Znane problemy w 3.4.2 wiersza polecenia systemu Windows x86 (RC)

Wczesne następnym tygodniu przed możemy trafień RTM będzie rozwiązać te problemy.

*  Uruchomione Przywracanie nuget dla rozwiązania zakończy się niepowodzeniem, jeśli plik rozwiązania znajduje się w hierarchii folderów niższe niż pliki projektu.
*  Polecenia usuwania nuget na pakiet za pomocą kanału informacyjnego V2 zakończy się niepowodzeniem. Zamiast tego użyj V3 źródła danych.


Aby uzyskać pełną listę poprawek i ulepszenia w tej wersji, zapoznaj się z listy problemów dotyczących [tutaj](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).