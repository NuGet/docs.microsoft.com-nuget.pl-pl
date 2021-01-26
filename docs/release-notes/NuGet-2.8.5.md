---
title: Informacje o wersji narzędzia NuGet 2.8.5
description: Informacje o wersji programu NuGet 2.8.5, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780360"
---
# <a name="nuget-285-release-notes"></a>Informacje o wersji narzędzia NuGet 2.8.5

Informacje o wersji narzędzia [NuGet 2.8.3](../release-notes/nuget-2.8.3.md)  |  [Informacje o wersji narzędzia NuGet 2.8.6](../release-notes/nuget-2.8.6.md)

2.8.5 NuGet wydano 30 marca 2015. Jest to drobna aktualizacja naszego 2.8.3 VSIX z niektórymi poprawkami.

W tej wersji dodano okno dialogowe obsługa Menedżera pakietów NuGet dla [monikerów platformy docelowej środowiska DNX](https://github.com/aspnet/dnx).  Te nowe monikery struktury, które są obsługiwane, obejmują:

* **core50** — moniker platformy docelowej "Base" (TFM), który jest zgodny z rdzeniem CLR.
* **dnx452** -A TFM specyficzne dla aplikacji opartych na środowiska dnxch przy użyciu pełnej wersji 4.5.2 platformy
* **dnx46** -A TFM specyficzne dla aplikacji opartych na środowiska dnxach przy użyciu pełnej wersji 4,6 platformy
* **dnxcore50** -A TFM specyficzne dla aplikacji opartych na środowiska DNX przy użyciu podstawowej wersji 5,0 platformy

Rozwiązano problem polegający na tym, że uniemożliwiło zainstalowanie pakietów w projektach FSharp:

https://nuget.codeplex.com/workitem/4400