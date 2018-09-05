---
title: Informacje o wersji NuGet 2.8.2
description: Informacje o wersji programu NuGet 2.8.2 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551151"
---
# <a name="nuget-282-release-notes"></a>Informacje o wersji NuGet 2.8.2

[Informacje o wersji NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [informacje o wersji programu NuGet 2.8.3](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 została wydana 22 maja 2014 r.  W tej wersji uwzględnione tylko zmiany wiersza polecenia nuget.exe, pakiet NuGet.Server i inne pakiety NuGet.  Wersja nie zawiera rozszerzenia programu WebMatrix lub zaktualizowane rozszerzenie programu Visual Studio.

## <a name="notable-updates"></a>Znaczące zmiany

Najbardziej znaczące zmiany były związane z wiersza polecenia nuget.exe oraz pakiet NuGet.Server (na potrzeby samodzielnie hostowane kanały informacyjne NuGet).

### <a name="important-nugetexe-bug-fixes"></a>Nuget.exe ważne poprawki błędów

1. [nuget.exe wypychania nie powiedzie się i utrzymuje ponawianie próby](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe wypychania nie wysyła poprawne poświadczenia uwierzytelniania podstawowego](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe wypychania nie wykonaj przekierowania tymczasowego](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Naprawienie usterki NuGet.Server ważne

1. [Nieprawidłowa wartość zwrócona przez NuGet.Server IsAbsoluteLatestVersion](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Zaktualizowano pakiety

Wiersza polecenia nuget.exe oraz NuGet.Server poprawki są dostarczane jako aktualizacje pakietu NuGet.  Wystąpiły inne pakiety aktualizowane przy użyciu 2.8.2 także.

Poniżej przedstawiono listę zaktualizowanych pakietów:

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (pakiet, nie rozszerzenia)

## <a name="all-changes"></a>Wszystkie zmiany
Wystąpiły problemy 10, które zostały rozwiązane w wydaniu. Pełną listę prac elementy rozwiązane w NuGet 2.8.2, sprawdź widok [NuGet narzędzie do śledzenia problemów w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
