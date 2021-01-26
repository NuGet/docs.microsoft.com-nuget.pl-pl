---
title: Informacje o wersji narzędzia NuGet 2.8.1
description: Informacje o wersji programu NuGet 2.8.1, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776764"
---
# <a name="nuget-281-release-notes"></a>Informacje o wersji narzędzia NuGet 2.8.1

Informacje o wersji narzędzia [NuGet 2,8](../release-notes/nuget-2.8.md)  |  [Informacje o wersji narzędzia NuGet 2.8.2](../release-notes/nuget-2.8.2.md)

Pakiet NuGet 2.8.1 został opublikowany 2 kwietnia 2014.

## <a name="notable-features-in-the-release"></a>Istotne funkcje w wersji

### <a name="support-for-windows-phone-81-projects"></a>Obsługa projektów Windows Phone 8,1
Ta wersja obsługuje teraz następujące nowe monikery platformy docelowej, które mogą być używane do celów projektów Windows Phone 8,1:

* WindowsPhone81/WP81 (dla projektów Windows Phone opartych na programie Silverlight)
* WindowsPhoneApp81/WPA81 (dla projektów aplikacji Windows Phone opartych na WinRT)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Aktualizacja rozszerzenia WebMatrix narzędzia NuGet
W tej wersji zostanie zaktualizowany klient NuGet znaleziony w programie WebMatrix do [NuGet. Core.](https://www.nuget.org/packages/Nuget.Core/2.6.1) Co ważniejsze, aktualizacja "ACS Core" umożliwia klientowi WebMatrix zainstalowanie pakietów NuGet, które zawierają nowsze wersje `.nuspec` schematu, w tym pakiety nuget ASP.NET.

Aby uzyskać więcej informacji na temat aktualizacji rozszerzenia WebMatrix, zobacz te szczegółowe informacje o [wersji](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Poprawki błędów
Oprócz tych funkcji Ta wersja programu NuGet zawiera inne poprawki błędów. Wystąpiło 16 łącznych problemów rozwiązanych w wydaniu. Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 2.8.1, zobacz [Śledzenie problemów NuGet dla tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Wysyłka przy użyciu programu Visual Studio "14" CTP
W programie Visual Studio "14" CTP wydanej 3 czerwca 2014, pakiet NuGet 2.8.1 jest dostarczany w tym polu. Funkcje, które obsługuje, pozostają w wartości nominalnej z innymi 2.8.1 VSIX, takimi jak jeden dla Visual Studio 2013.
