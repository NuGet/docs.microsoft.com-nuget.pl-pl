---
title: Informacje o wersji programu NuGet 3.0 RC
description: Informacje o wersji programu NuGet 3.0 RC obejmuje znane problemy, poprawki błędów, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551722"
---
# <a name="nuget-30-rc-release-notes"></a>Informacje o wersji programu NuGet 3.0 RC

[Informacje o wersji programu NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 — informacje o wersji](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC został wydany 29 kwietnia 2015 w wersji Visual Studio 2015 RC. Ta wersja ma wiele ważnych poprawek błędów, ulepszeń wydajności i aktualizacji do obsługi nowych platform.  Jest on dostępny tylko dla programu Visual Studio 2015.

### <a name="continued-focus-on-performance"></a>Ciągłe dążenie do wydajności

Stabilności i wydajności kwerend NuGet nadal aktualnie gorący temat wśród, koncentrujemy się na.  W tej wersji należy zacząć wyświetlić operacje bardzo szybkie wyszukiwanie w NuGet interfejsu użytkownika i witryny sieci Web.  Firma Microsoft monitorowania usługi i sposobie korzystania z usługi tak, aby umożliwić nam dostosować te operacje.

## <a name="significant-issues-resolved"></a>Istotne problemy rozwiązane

W celu stabilizacji klientom programu NuGet, rozwiązaliśmy wiele problemów w ramach tej wersji.  Poniżej przedstawiono tylko krótkie listami niektóre najważniejsze zagadnienia, które są rozwiązane:

* W ramach zmiany nazwy K framework programu ASP.NET 5, monikerów framework zostały zaktualizowane do obsługi środowiska dnx i dnxcore [łącza](https://github.com/NuGet/Home/issues/215)
* Dodano dokumentacji pomocy z poziomu linków w interfejsie użytkownika programu Visual Studio [łącza](https://github.com/NuGet/Home/issues/232)
* Lepiej obsługi złożonych odwołań w `.nuspec` za pomocą odwołania rozdzielonych przecinkami [łącza](https://github.com/NuGet/Home/issues/276)
* Naprawiono obsługę japoński kultur [łącza](https://github.com/NuGet/Home/issues/253)
* Zaktualizowanego klienta, aby umożliwić projektów ASP.NET 5, aby używać nowych v3 punktów końcowych [łącza](https://github.com/NuGet/Home/issues/219)
* Zaktualizowano w celu lepszego uchwyt folder packages z kontrolą źródła [łącza](https://github.com/NuGet/Home/issues/56)
* Naprawiono obsługę satelitarnej pakietów [łącza](https://github.com/NuGet/Home/issues/17)
* Poprawiona obsługa dla określonej platformy, pliki zawartości [łącza](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>Kontrolę obecności usługi GitHub

Wprowadziliśmy pewne zmiany do naszych [źródła repozytoriów w serwisie GitHub](http://github.com/nuget/home).  Jeśli masz problemy z klienta programu NuGet w programie Visual Studio, poleceń programu Powershell lub wiersza polecenia pliku wykonywalnego można rejestrować tych problemów i monitorować ich postęp na naszych [listę problemów w repozytorium GitHub głównej](http://github.com/nuget/home/issues).  Śledzimy problemy z galerii w naszym [repozytorium GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Obserwuj na bieżąco

Można nadzorować [naszym blogu](http://blog.nuget.org) więcej postępu i anonsów dla pakietów NuGet 3.0!