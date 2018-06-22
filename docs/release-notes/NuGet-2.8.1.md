---
title: Informacje o wersji 2.8.1 NuGet
description: Informacje o wersji programu NuGet 2.8.1 tym — znane problemy, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8787aee36d31ed5d8071b35a8c243823029d135f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820524"
---
# <a name="nuget-281-release-notes"></a>Informacje o wersji 2.8.1 NuGet

[Informacje o wersji NuGet 2.8](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 informacje o wersji](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 został wydany 2 kwietnia 2014 r.

## <a name="notable-features-in-the-release"></a>Ważne funkcje w wersji

### <a name="support-for-windows-phone-81-projects"></a>Obsługa systemu Windows Phone 8.1 projektów
Ta wersja obsługuje teraz następujące nowe docelowej framework monikerów które mogą być używane do projektów docelowych systemu Windows Phone 8.1:

* WindowsPhone81 / WP81 (dla projektów Silverlight systemem Windows Phone)
* WindowsPhoneApp81 / WPA81 (dla projektów opartych na WinRT aplikacji Windows Phone)

### <a name="update-of-the-nuget-webmatrix-extension"></a>Aktualizowanie NuGet rozszerzenia programu WebMatrix
Ta wersja aktualizacji klienta NuGet w program WebMatrix w celu [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1, a z funkcji takich jak XDT przekształcenia. Co więcej, 2.6.1 aktualizacja core umożliwia klienta programu WebMatrix można zainstalować pakietów NuGet, które znajdują się nowsze wersje `.nuspec` schemat, który zawiera pakiety ASP.NET NuGet.

Aby uzyskać więcej informacji na temat aktualizacji rozszerzenia programu WebMatrix, zobacz te określone [informacje o wersji](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Poprawki błędów
Oprócz tych funkcji ta wersja programu NuGet zawiera inne poprawki błędów. Znaleziono 16 całkowita problemy rozwiązane w wersji. Pełną listę prac elementów usunięto w wersji NuGet 2.8.1, sprawdź widok [NuGet Tracker problem w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Reshipping z programem Visual Studio "14" CTP
W wersji CTP programu Visual Studio "14" wydanej w dniu 2014 3 czerwca NuGet 2.8.1 jest dostarczany w polu. Funkcje, obsługuje on pozostają w par z innych 2.8.1 VSIXes, takich jak dla programu Visual Studio 2013.
