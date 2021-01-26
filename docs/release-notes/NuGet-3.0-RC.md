---
title: Informacje o wersji narzędzia NuGet 3,0 RC
description: Informacje o wersji programu NuGet 3,0 RC, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776573"
---
# <a name="nuget-30-rc-release-notes"></a>Informacje o wersji narzędzia NuGet 3,0 RC

Informacje o wersji programu [NuGet 3,0 beta](../release-notes/nuget-3.0-beta.md)  |  [Informacje o wersji narzędzia NuGet 3,0 RC2](../release-notes/nuget-3.0-RC2.md)

Pakiet NuGet 3,0 RC został zwolniony 29 kwietnia 2015 z wersją Visual Studio 2015 RC. W tej wersji wprowadzono wiele ważnych poprawek usterek, ulepszeń wydajności i aktualizacji w celu obsługi nowych platform.  Jest on dostępny tylko dla programu Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Dalsze koncentracje na wydajności

Stabilność i wydajność zapytań NuGet nadal jest aktywnym tematem, na którym koncentrujemy się.  W tej wersji należy zacząć wyświetlać bardzo szybkie operacje wyszukiwania w interfejsie użytkownika i witrynie programu NuGet.  Monitorujemy usługę i używamy usługi, aby można było dalej dostroić te operacje.

## <a name="significant-issues-resolved"></a>Znaczne problemy rozwiązane

Aby zapewnić stabilizację klientów programu NuGet, firma Microsoft rozwiązała wiele problemów w ramach tej wersji.  Poniżej przedstawiono krótką listę niektórych ważniejszych problemów, które zostały rozwiązane:

* W ramach zmiany nazwy platformy K dla ASP.NET 5, monikery struktury zostały zaktualizowane w celu obsługi [linku](https://github.com/NuGet/Home/issues/215) środowiska DNX i dnxcore
* Dodano dokumentację pomocy z linków w [linku](https://github.com/NuGet/Home/issues/232) interfejsu użytkownika programu Visual Studio
* Ulepszona obsługa złożonych odwołań w `.nuspec` połączeniu z odwołaniami do struktury rozdzielonych przecinkami [](https://github.com/NuGet/Home/issues/276)
* Stała obsługa [łącza](https://github.com/NuGet/Home/issues/253) dla kultur japońskich
* Zaktualizowano klienta, aby zezwolić na używanie przez ASP.NET 5 projektów [nowych punktów](https://github.com/NuGet/Home/issues/219) końcowych v3
* Zaktualizowano w celu lepszego obsługi folderu pakietów z [linkiem](https://github.com/NuGet/Home/issues/56) kontroli źródła
* Stałe wsparcie dla [linku](https://github.com/NuGet/Home/issues/17) pakietów satelitarnych
* Poprawiono obsługę [linku](https://github.com/NuGet/Home/issues/18) do plików zawartości specyficznej dla platformy

## <a name="github-presence-overhaul"></a>Remonty obecności usługi GitHub

Wprowadziliśmy pewne zmiany w [repozytoriach kodu źródłowego w serwisie GitHub](http://github.com/nuget/home).  Jeśli masz problemy z klientem programu Visual Studio NuGet, poleceniami programu PowerShell lub wykonywalnym wierszem polecenia, można rejestrować te problemy i monitorować ich postęp na naszej [liście problemów z repozytorium głównym usługi GitHub](http://github.com/nuget/home/issues).  Śledzimy problemy z galerią w naszym [repozytorium GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Bądź na bieżąco

Obserwuj [nasz blog](http://blog.nuget.org) , aby uzyskać więcej informacji na temat postępu i anonsów dla programu NuGet 3,0!