---
title: Informacje o wersji narzędzia NuGet 3.4.4
description: Informacje o wersji programu NuGet 3.4.4, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780222"
---
# <a name="nuget-344-release-notes"></a>Informacje o wersji narzędzia NuGet 3.4.4

Informacje o wersji narzędzia [NuGet 3.4.3](../release-notes/nuget-3.4.3.md)  |  [NuGet 3,5 — informacje o wersji beta](../release-notes/nuget-3.5-Beta.md)

Głównym celem tej wersji była poprawa jakości 3.4.3 wersji nuget.exe z kilkoma poprawkami do rozszerzenia programu Visual Studio.

W [tym miejscu](https://dist.nuget.org/index.html)możesz pobrać zarówno VSIX, jak i nuget.exe.

## <a name="344-rtm-2016-05-19"></a>[3.4.4 — RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Pełny dziennik zmian](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Lista problemów](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Zmiany

- Udoskonalenia pakietu: ulepszenia symboli pakowania, pakowanie z `project.json` i więcej [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606)
- Wyświetl wyjątek, jeśli wystąpił błąd podczas znajdowania projektów w poleceniu Update [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605
- Odczytaj typ pakietu z danych wejściowych `.nuspec` i `project.json` przy pakowaniu [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)
- Utwórz pakiet NuGet. Udostępnianie nie jest projektem. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Użyj limitu czasu wypychania jako limitu czasu odpowiedzi HTTP [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599)
- Pliki pakietu z przyszłymi czasami nie będą używane [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)
- Aktualizowanie `NuGet.Core.dll` wersji do 2.12.0 w celu naprawienia problemu XML [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)
- Support./NuGet.commandline.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)
- Wyświetl błąd przywracania bez `project.json` lub `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590)
- Naprawianie wersji zależności, gdy wymagane są różne wersje [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)