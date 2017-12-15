---
title: Informacje o wersji NuGet 2.8.1 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: eebbbae4-fc6a-4c05-9102-4ec66b4c64a4
description: "Informacje o wersji programu NuGet 2.8.1 tym — znane problemy, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 2.8.1 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ac33369644d312591bfe8c06540935b2c6063c5d
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
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
