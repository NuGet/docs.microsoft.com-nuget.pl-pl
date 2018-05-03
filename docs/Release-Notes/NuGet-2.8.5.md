---
title: Informacje o wersji NuGet 2.8.5
description: Informacje o wersji programu NuGet 2.8.5 tym — znane problemy, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-285-release-notes"></a>Informacje o wersji NuGet 2.8.5

[Informacje o wersji NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 informacje o wersji](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 wydanej w dniu 30 marca 2015 roku. Jest to aktualizacja pomocnicza do naszej 2.8.3 VSIX niektóre docelowe poprawki.

W tej wersji dodano obsługę dla okna dialogowego Menedżer pakietów NuGet [DNX docelowej Framework monikerów](https://github.com/aspnet/dnx).  Te nowe monikerów framework, które są obsługiwane następujące:

* **core50** — "base" target framework moniker (TFM) zgodny z Core CLR.
* **dnx452** — A TFM aplikacji określonym na podstawie DNX przy użyciu 4.5.2 pełnej wersji platformy
* **dnx46** — A TFM aplikacji określonym na podstawie DNX przy użyciu 4.6 pełnej wersji platformy
* **dnxcore50** — A TFM aplikacji określonym na podstawie środowiska DNX za pomocą wersji Core 5.0 Framework

Jeden błąd został rozwiązany tego uniemożliwił pakietów instalacji do projektów języka FSharp prawidłowo:

https://nuget.codeplex.com/workitem/4400