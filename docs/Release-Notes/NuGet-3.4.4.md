---
title: Informacje o wersji NuGet 3.4.4 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6f0aa9bb-75e5-429d-9954-3cb41a909c14
description: "Informacje o wersji programu NuGet 3.4.4 tym — znane problemy, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 3.4.4 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 51ddb918d2269990588e9cba4d15ffeb878de5f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-344-release-notes"></a>Informacje o wersji NuGet 3.4.4

[Informacje o wersji NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [informacje o wersji 3.5 Beta NuGet](../release-notes/nuget-3.5-Beta.md)

Głównym celem tej wersji zostało ulepszenia jakości 3.4.3 wersji nuget.exe kilka poprawki z rozszerzeniem programu Visual Studio.

Możesz pobrać zarówno VSIX, jak i nuget.exe [tutaj](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Pełny wykaz zmian](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Lista problemów](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Zmiany

- Ulepszenia pakietu: Ulepszenia pakowanie symboli, pakowanie z `project.json` i więcej [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Wyświetlanie wyjątku po awarii, znajdowanie projekty w poleceniu aktualizacji [\#605] (https://github.com/NuGet/NuGet.Client/pull/605
- Typ pakietu do odczytu z wejścia `.nuspec` i `project.json` podczas pakowania [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Należy NuGet.Shared nie w projekcie. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Użyj limit wypychania jako limitu czasu odpowiedzi HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Nie ma plików pakietu wraz z czasem przyszłych ich przypadków użycia [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- Aktualizowanie `NuGet.Core.dll` wersji 2.12.0, aby rozwiązać problem XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- Obsługuje./NuGet.CommandLine.XPlat - v \<szczegółowości\> \<tryb\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Wyświetl wystąpił błąd podczas przywracania bez `project.json` lub `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Ustalenie wersje zależności wymagane wersje różnią się [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)