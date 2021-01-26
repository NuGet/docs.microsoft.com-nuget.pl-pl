---
title: Informacje o wersji narzędzia NuGet 2.8.2
description: Informacje o wersji programu NuGet 2.8.2, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780372"
---
# <a name="nuget-282-release-notes"></a>Informacje o wersji narzędzia NuGet 2.8.2

Informacje o wersji narzędzia [NuGet 2.8.1](../release-notes/nuget-2.8.1.md)  |  [Informacje o wersji narzędzia NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

Pakiet NuGet 2.8.2 został opublikowany w dniu 22 maja 2014.  W tej wersji uwzględniono tylko zmiany w nuget.exe wierszu polecenia, pakiet NuGet. Server i inne pakiety NuGet.  Wydanie nie zawiera zaktualizowanego rozszerzenia programu Visual Studio lub rozszerzenia WebMatrix.

## <a name="notable-updates"></a>Ważne aktualizacje

Najbardziej ważne aktualizacje zostały nuget.exe w wierszu polecenia i pakiecie NuGet. Server (dla własnych źródeł NuGet).

### <a name="important-nugetexe-bug-fixes"></a>Ważne poprawki nuget.exe błędów

1. [nuget.exe wypychanie nie powiedzie się i kontynuuje ponawianie próby](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe push nie wysyła prawidłowo poświadczeń uwierzytelniania podstawowego](https://nuget.codeplex.com/workitem/4109)
1. [ Wypychanienuget.exe nie będzie podążać za przekierowaniem tymczasowym](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Ważna Poprawka błędu NuGet. serwer

1. [Niepoprawna wartość IsAbsoluteLatestVersion zwrócona przez NuGet. serwer](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Zaktualizowano pakiety

nuget.exe wiersza polecenia i NuGet. poprawki serwera są dostarczane jako aktualizacje pakietu NuGet.  Dodano również inne pakiety z 2.8.2.

Oto lista zaktualizowanych pakietów:

1. [NuGet. Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet. CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet. Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (pakiet, a nie rozszerzenie)

## <a name="all-changes"></a>Wszystkie zmiany
Wystąpiły 10 problemów rozwiązanych w wydaniu. Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 2.8.2, zobacz [Śledzenie problemów NuGet dla tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
