---
title: Informacje o wersji narzędzia NuGet 2.8.6
description: Informacje o wersji programu NuGet 2.8.6, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776697"
---
# <a name="nuget-286-release-notes"></a>Informacje o wersji narzędzia NuGet 2.8.6

Informacje o wersji narzędzia [NuGet 2.8.5](../release-notes/nuget-2.8.5.md)  |  [Informacje o wersji narzędzia NuGet 2.8.7](../release-notes/nuget-2.8.7.md)

Pakiet NuGet 2.8.6 został wydany 20 lipca 2015 jako drobna aktualizacja naszego 2.8.5 VSIX z niektórymi skierowanymi poprawkami i ulepszeniami dotyczącymi pakietów, które mogą być dostarczane z obsługą systemu Windows 10 platformy UWP Development model.

Ta wersja rozszerzenia Menedżera pakietów NuGet zapewnia obsługę tylko Visual Studio 2013.

W tej wersji okno dialogowe Menedżera pakietów NuGet obsługiwało Dodawanie do:

* Wprowadzono moniker platformy docelowej UAP do obsługi programowania aplikacji systemu Windows 10.
* Punkty końcowe protokołu NuGet w wersji 3
* Obsługa [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atrybutu protocolVersion w źródłach repozytorium. Wartość domyślna to "2"
* Powracanie do zdalnego repozytorium, jeśli wymagana wersja pakietu nie jest dostępna w lokalnej pamięci podręcznej