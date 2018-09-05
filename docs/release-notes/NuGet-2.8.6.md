---
title: Informacje o wersji NuGet 2.8.6
description: Informacje o wersji programu NuGet 2.8.6 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546494"
---
# <a name="nuget-286-release-notes"></a>Informacje o wersji NuGet 2.8.6

[Informacje o wersji NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [informacjach o wersji NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 został wydany 20 lipca 2015 roku jako aktualizację pomocniczą do naszych 2.8.5 VSIX z niektórymi docelowe poprawek i udoskonaleń do obsługi pakietów, które mogą być dostarczane z obsługą model programowania platformy uniwersalnej systemu Windows do systemu Windows 10.

Ta wersja rozszerzenia Menedżera pakietów NuGet zapewniają obsługę programu Visual Studio 2013 tylko.

W tej wersji okno Menedżera pakietów NuGet nie dodano dla pomocy technicznej:

* Wprowadzono UAP krótką nazwę platformy docelowej do obsługi systemu Windows 10 dla deweloperów aplikacji.
* Punkty końcowe programu NuGet protocol w wersji 3
* Obsługa [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) właściwość protocolVersion atrybutu w źródłach repozytoriów. Wartość domyślna to "2"
* Nastąpi powrót do repozytorium zdalnego, jeśli wersja wymagany pakiet nie jest dostępna w lokalnej pamięci podręcznej