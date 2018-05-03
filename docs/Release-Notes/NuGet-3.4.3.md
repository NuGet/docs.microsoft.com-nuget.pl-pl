---
title: Informacje o wersji NuGet 3.4.3
description: Informacje o wersji programu NuGet 3.4.3 tym — znane problemy, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6c25d3b678e6e72eca3e1157f91a75bfa8cbb18e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-343-release-notes"></a>Informacje o wersji NuGet 3.4.3

[Informacje o wersji NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 informacje o wersji](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 został wydany 22 kwietnia 2016 r., aby rozwiązać pewne problemy, które zostały zidentyfikowane w 3.4 i późniejszych wersjach.

Możesz pobrać zarówno VSIX, jak i nuget.exe [tutaj](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aktualizacje i usprawnienia

* Większą niezawodność programu Visual Studio. Naprawiono problemy w NuGet, który spowodował awarię programu Visual Studio.

## <a name="fixes"></a>Poprawki

* Usunięto niektóre problemy z autoryzacją nuget prywatny chroniony hasłem źródeł danych.
* Rozwiązano problem wokół nie będą mogli przywrócić PCL z `project.json` z określonych środowisk uruchomieniowych.
* Niektórzy klienci były uruchomione w sporadycznych błędów podczas instalowania pakietów. Teraz, ten problem został naprawiony w tej wersji.
* Rozwiązano problem powodujący błędy przywracania w języku C + +/ CLI projektów z `project.json`.
* Niektóre pakiety (np. ModernHttpClient) gdy nie jest rozpakowane poprawnie Jeśli używasz nuget mono. Teraz, ten problem został naprawiony w tej wersji.

Aby uzyskać pełną listę poprawek i ulepszenia w tej wersji, zapoznaj się z listy problemów dotyczących [tutaj](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).