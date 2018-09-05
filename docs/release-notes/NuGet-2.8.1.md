---
title: Informacje o wersji NuGet 2.8.1
description: Informacje o wersji programu NuGet 2.8.1 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545242"
---
# <a name="nuget-281-release-notes"></a>Informacje o wersji NuGet 2.8.1

[Informacje o wersji NuGet 2.8](../release-notes/nuget-2.8.md) | [informacjach o wersji NuGet 2.8.2](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 został wydany 2 kwietnia 2014 r.

## <a name="notable-features-in-the-release"></a>Ważne funkcje w wersji

### <a name="support-for-windows-phone-81-projects"></a>Obsługa systemu Windows Phone 8.1 projektów
Ta wersja obsługuje teraz następujące nowe target framework monikerów, które może służyć do projektów docelowych Windows Phone 8.1:

* WindowsPhone81 / WP81 (dla projektów Windows Phone opartych na technologii Silverlight)
* WindowsPhoneApp81 / WPA81 (w przypadku projektów opartych na WinRT aplikacji Windows Phone)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Aktualizuj rozszerzenie NuGet w programie WebMatrix
W tej wersji aktualizacji klienta programu NuGet w programie WebMatrix można [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 i wiąże z funkcji takich jak XDT przekształcenia. Co ważniejsze, 2.6.1 aktualizacja core umożliwia instalowanie pakietów NuGet, które znajdują się nowsze wersje klienta programu WebMatrix `.nuspec` schemat, który zawiera pakiety ASP.NET NuGet.

Aby uzyskać więcej informacji na temat aktualizacji rozszerzenia programu WebMatrix, zobacz te, które są określone [informacje o wersji](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Poprawki błędów
Poza tymi funkcjami w tej wersji programu NuGet zawiera inne poprawki błędów. Wystąpiły 16 Suma problemów, które zostały rozwiązane w wydaniu. Pełną listę prac elementy rozwiązane w NuGet 2.8.1, sprawdź widok [NuGet narzędzie do śledzenia problemów w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reshipping z programem Visual Studio "14" CTP
W wersji CTP programu Visual Studio "14" wydana w czerwcu 2014 3rd NuGet 2.8.1 jest dostarczany w polu. Funkcje, ale obsługuje pozostają w par przy użyciu innych 2.8.1 VSIXes, takiego jak Visual Studio 2013.
