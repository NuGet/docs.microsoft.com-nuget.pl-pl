---
title: Informacje o wersji narzędzia NuGet 3.4.2
description: Informacje o wersji programu NuGet 3.4.2, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780258"
---
# <a name="nuget-342-release-notes"></a>Informacje o wersji narzędzia NuGet 3.4.2

Informacje o wersji pakietu [NuGet](../release-notes/nuget-3.4.1.md)  |  [Informacje o wersji narzędzia NuGet 3.4.3](../release-notes/nuget-3.4.3.md)

Program NuGet 3.4.2 został zwolniony 8 kwietnia 2016, aby rozwiązać kilka problemów, które zostały zidentyfikowane w wersji 3,4 i.

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC jest teraz dostępny

W [tym miejscu](https://dist.nuget.org/index.html)możesz pobrać wersję release candidate nuget.exe 3.4.2.

## <a name="updates-and-improvements"></a>Aktualizacje i ulepszenia

* Znacznie Ulepszono wydajność aktualizacji w konkretnym scenariuszu, w przypadku których aktualizacje na pakietach ze szczegółowymi wykresami zależności zajęły dużo czasu i zawiesiły program Visual Studio.
* Przywracanie NuGet bez ruchu sieciowego to 2,5 x – trzykrotnie w programie Visual Studio.
* Oprócz tej zmiany Rozwiązano problem polegający na tym, że po pobraniu liczby aktualizacji w interfejsie użytkownika programu VS nastąpiło dwukrotne naciśnięcie sieci. Było to częściowo odpowiedzialne za niektóre problemy z limitem czasu w przypadku klientów w wersji 3.4/Object.
* Dodano obsługę ustawienia no_proxy

## <a name="fixes"></a>Poprawki

* Rozwiązano problem polegający na tym, że brak źródła nuget.org w ustawieniach lub konfiguracji NuGet po uaktualnieniu do programu.
* Rozwiązano problem polegający na tym, że wielkość liter zmieni się na FindPackagesById w Artifactoryach.
* Rozwiązano problem związany z standardem FIPS, który spowodował błędy przywracania NuGet z nuget.exe.
* Naprawiono awarię podczas przeglądania źródeł z nieprawidłowym adresem URL ikony.
* Rozwiązano problemy z scalaniem wersji i wpisów ze wszystkich źródeł.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Znane problemy w programie 3.4.2 Windows x86 — wiersz polecenia (RC)

Te problemy zostaną rozwiązane na wczesny tydzień przed osiągnięciem wersji RTM.

*  Uruchomienie przywracania NuGet w rozwiązaniu zakończy się niepowodzeniem, jeśli plik rozwiązania zostanie umieszczony w niższej hierarchii folderów niż pliki projektu.
*  Uruchamianie polecenia usuwania NuGet w pakiecie przy użyciu źródła danych v2 zakończy się niepowodzeniem. Zamiast tego należy użyć kanału informacyjnego v3.


Aby zapoznać się z pełną listą poprawek i ulepszeń w tej wersji, zapoznaj się z listą problemów w [tym miejscu](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).