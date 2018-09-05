---
title: Informacje o wersji NuGet 2.8.5
description: Informacje o wersji programu NuGet 2.8.5 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548628"
---
# <a name="nuget-285-release-notes"></a>Informacje o wersji NuGet 2.8.5

[Informacje o wersji programu NuGet 2.8.3](../release-notes/nuget-2.8.3.md) | [informacjach o wersji NuGet 2.8.6](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 został wydany 30 marca 2015 r. Jest aktualizację pomocniczą do naszych wersji 2.8.3 VSIX z niektórymi docelowe poprawki.

W tej wersji dodano obsługę dla okna dialogowego Menedżer pakietów NuGet [środowiska DNX Target Framework monikerów](https://github.com/aspnet/dnx).  Te nowe krótkie nazwy framework, które są obsługiwane, obejmują:

* **core50** — "base" docelowe moniker struktury (TFM), która jest zgodna z Core CLR.
* **dnx452** — TFM specyficzne dla środowiska DNX na podstawie używających 4.5.2 pełną wersję platformy
* **dnx46** — TFM specyficzne dla środowiska DNX na podstawie używających 4.6 pełną wersję platformy
* **dnxcore50** — TFM: specyficzne dla środowiska DNX na podstawie aplikacji przy użyciu wersji Core 5.0 framework

Jeden błąd został naprawiony tego uniemożliwił pakietów instalacji do projektów języka FSharp prawidłowo:

https://nuget.codeplex.com/workitem/4400