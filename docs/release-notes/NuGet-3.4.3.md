---
title: Informacje o wersji narzędzia NuGet 3.4.3
description: Informacje o wersji programu NuGet 3.4.3, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776463"
---
# <a name="nuget-343-release-notes"></a>Informacje o wersji narzędzia NuGet 3.4.3

Informacje o wersji narzędzia [NuGet 3.4.2](../release-notes/nuget-3.4.2.md)  |  [Informacje o wersji narzędzia NuGet 3.4.4](../release-notes/nuget-3.4.4.md)

3.4.3 NuGet została wydana 22 kwietnia 2016, aby rozwiązać kilka problemów, które zostały zidentyfikowane w 3,4 i kolejnych wersjach.

W [tym miejscu](https://dist.nuget.org/index.html)możesz pobrać zarówno VSIX, jak i nuget.exe.

## <a name="updates-and-improvements"></a>Aktualizacje i ulepszenia

* Ulepszona niezawodność programu Visual Studio. W programie NuGet rozwiązano pewne problemy, które spowodowały awarie w programie Visual Studio.

## <a name="fixes"></a>Poprawki

* Rozwiązano pewne problemy z autoryzacją za pomocą prywatnych źródeł danych NuGet chronionych hasłem.
* Rozwiązano problem polegający na tym, że nie można przywrócić programu PCL z programu `project.json` przy użyciu określonych środowisk uruchomieniowych.
* Niektórzy klienci byli w nieprzerwanych awariach podczas instalowania pakietów. Ten problem został rozwiązany w tej wersji.
* Rozwiązano problem, który spowodował błędy przywracania w projektach C++/CLI z `project.json` .
* Niektóre pakiety (np. ModernHttpClient), które nie są rozpakowane prawidłowo w przypadku używania NuGet w programie mono. Ten problem został rozwiązany w tej wersji.

Aby zapoznać się z pełną listą poprawek i ulepszeń w tej wersji, zapoznaj się z listą problemów w [tym miejscu](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).