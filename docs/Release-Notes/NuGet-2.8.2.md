---
title: Informacje o wersji NuGet 2.8.2 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: bb547f5d-3c0e-4721-b2c7-3fc7e09c34de
description: "Informacje o wersji programu NuGet 2.8.2 tym — znane problemy, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 2.8.2 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 221b8970663ca80a986fc3ee542b99971c5e2018
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-282-release-notes"></a>Informacje o wersji NuGet 2.8.2

[Informacje o wersji NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 informacje o wersji](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 wydanej w dniu 22 maja 2014.  Ta wersja uwzględnione tylko zmiany nuget.exe wiersza polecenia, pakiet NuGet.Server i inne pakiety NuGet.  Wersja nie zawiera zaktualizowane rozszerzenie programu Visual Studio lub rozszerzenia programu WebMatrix.

## <a name="notable-updates"></a>Ważne aktualizacje.

Najbardziej znaczące aktualizacje zostały nuget.exe wiersza polecenia i pakietu NuGet.Server (dla siebie źródeł danych NuGet).

### <a name="important-nugetexe-bug-fixes"></a>Nuget.exe ważne poprawki błędów

1. [nuget.exe wypychania nie powiedzie się i przechowuje ponawianie próby](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe wypychania nie wysyła poprawnie poświadczenia uwierzytelniania podstawowego](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe wypychania nie wykonaj Przekierowanie tymczasowe](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>Poprawka błędu NuGet.Server ważne

1. [Niewłaściwą wartość zwrócona przez NuGet.Server IsAbsoluteLatestVersion](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>Pakiety aktualizacji

Nuget.exe wiersza polecenia i NuGet.Server poprawki są dostarczane jako aktualizacji pakietu NuGet.  Brak innych pakietów, zaktualizowane 2.8.2 również.

Poniżej przedstawiono listę zaktualizowanych pakietów:

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (pakietu, nie rozszerzenia)

## <a name="all-changes"></a>Wszystkie zmiany
Wystąpiły problemy 10 w wersji. Pełną listę prac elementów usunięto w wersji NuGet 2.8.2, sprawdź widok [NuGet Tracker problem w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).
