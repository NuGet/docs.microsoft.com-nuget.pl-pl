---
title: Informacje o wersji NuGet 2.8.5 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 60b96b2e-2a61-4f10-b5ad-3299f5a6d453
description: "Informacje o wersji programu NuGet 2.8.5 tym — znane problemy, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 2.8.5 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3b297704968b8423f60e9de08e27860dc375c019
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
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