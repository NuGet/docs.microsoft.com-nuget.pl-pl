---
title: Informacje o wersji NuGet 2.8.6 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "Informacje o wersji programu NuGet 2.8.6 tym — znane problemy, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 2.8.6 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f33c1edd3ef703a8cd97b7bdd97c37e12426aafa
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-286-release-notes"></a>Informacje o wersji NuGet 2.8.6

[Informacje o wersji NuGet 2.8.5](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 informacje o wersji](../release-notes/nuget-2.8.7.md)

Została wydana NuGet 2.8.6 20 lipca 2015 roku jako pomocnicza aktualizacji do naszej 2.8.5 VSIX niektóre docelowe poprawki i ulepszenia umożliwiające obsługę pakietów, które mogą być dostarczone z obsługą modelu programowania platformy uniwersalnej systemu Windows do systemu Windows 10.

Ta wersja rozszerzenia Menedżera pakietów NuGet zapewnia obsługę programu Visual Studio 2013 tylko.

W tej wersji okno dialogowe Menedżer pakietów NuGet nie dodano obsługę:

* Wprowadzono Moniker platformy docelowej UAP do obsługi systemu Windows 10 dla deweloperów aplikacji.
* Punkty końcowe w wersji 3 protokołu NuGet
* Obsługa [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) atrybut właściwość protocolVersion w źródłach repozytoriów. Wartość domyślna to "2"
* Nastąpi powrót do zdalnego repozytorium, jeśli wersja wymagany pakiet nie jest dostępny w lokalnej pamięci podręcznej