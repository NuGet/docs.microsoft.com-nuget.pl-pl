---
title: Informacje o wersji NuGet 3.4.4
description: Informacje o wersji programu NuGet 3.4.4 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547476"
---
# <a name="nuget-344-release-notes"></a>Informacje o wersji NuGet 3.4.4

[Informacje o wersji NuGet 3.4.3](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 Beta wersji](../release-notes/nuget-3.5-Beta.md)

Głównym celem tej wersji Ustaliliśmy jakości 3.4.3 wersję nuget.exe kilka poprawki z rozszerzeniem programu Visual Studio.

Możesz pobrać VSIX i nuget.exe [tutaj](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Pełny dziennik zmian](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Lista problemów](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Zmiany

- Ulepszenia pakietu: Ulepszenia pakowanie symboli, pakowanie przy użyciu `project.json` i więcej [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Wyświetlanie wyjątku po awarii, znajdowanie projekty w poleceniu aktualizacji [\#605](https://github.com/NuGet/NuGet.Client/pull/605)
- Odczytaj typ pakietu z danych wejściowych `.nuspec` i `project.json` podczas pakowania [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Należy NuGet.Shared, nie w projekcie. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Użyj czasu wypychania jako limit czasu odpowiedzi HTTP [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Pliki pakietu przy użyciu godzin w przyszłości nie będzie ich czasy używane [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- Aktualizowanie `NuGet.Core.dll` wersji 2.12.0, aby rozwiązać problem XML [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- Obsługuje./NuGet.CommandLine.XPlat - v \<szczegółowości\> \<tryb\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Wyświetlanie wystąpił błąd podczas przywracania bez `project.json` lub `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Ustalenie wersjami zależności wymagane wersje różnią się [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)