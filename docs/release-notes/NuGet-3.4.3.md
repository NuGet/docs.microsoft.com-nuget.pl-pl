---
title: Informacje o wersji narzędzia NuGet 3.4.3
description: Informacje o wersji NuGet 3.4.3, w tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549168"
---
# <a name="nuget-343-release-notes"></a>Informacje o wersji narzędzia NuGet 3.4.3

[Informacje o wersji NuGet 3.4.2](../release-notes/nuget-3.4.2.md) | [informacjach o wersji NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

Narzędzia NuGet 3.4.3 została wydana 22 kwietnia 2016 r. Aby rozwiązać wiele problemów, które zostały zidentyfikowane w wersji 3.4 i kolejnych.

Możesz pobrać VSIX i nuget.exe [tutaj](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Aktualizacje i ulepszenia

* Poprawiono niezawodność programu Visual Studio. Usunęliśmy kilka problemów w pakiecie NuGet, który spowodował awarię w programie Visual Studio.

## <a name="fixes"></a>Poprawki

* Rozwiązano niektóre problemy z autoryzacją nuget prywatny chroniony hasłem, źródła danych.
* Rozwiązano problem wokół nie będzie w stanie przywracania PCL z `project.json` za pomocą środowiska uruchomieniowe określona.
* Niektórzy klienci zostały przekroczone sporadycznych błędów podczas instalowania pakietów. To teraz został rozwiązany w tej wersji.
* Rozwiązano problem powodujący niepowodzenia przywracania w języku C + +/ CLI projekty przy użyciu `project.json`.
* Niektóre pakiety (np. ModernHttpClient) gdzie brakiem rozpakowano poprawnie zastosowania nuget w rozwiązaniu mono. To teraz został rozwiązany w tej wersji.

Aby uzyskać pełną listę poprawek i udoskonaleń w tej wersji, zapoznaj się z listy problemów dotyczących [tutaj](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).