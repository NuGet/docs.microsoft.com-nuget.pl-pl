---
title: Informacje o wersji NuGet 3.2.1
description: Informacje o wersji programu NuGet 3.2.1 tym — znane problemy, poprawki, dodatkowe funkcje i dcr.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 039fabaaacfdffd76fa88ff8183548e97cd4719b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-321-release-notes"></a>Informacje o wersji NuGet 3.2.1

[Informacje o wersji NuGet 3.2](../release-notes/nuget-3.2.md) | [NuGet 3.3 informacje o wersji](../release-notes/nuget-3.3.md)

NuGet 3.2.1 dla wiersza polecenia został wydany 12 października 2015 z kilku optymalizacji i poprawek w wersji 3.2 i jest dostępny w [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Ulepszenia

* Teraz NuGet używa pliku konfiguracji z oryginalnego wielkość liter w wyrazie `NuGet.Config`.  Jest to ważne w systemach operacyjnych z uwzględnieniem wielkości liter [1427](https://github.com/NuGet/Home/issues/1427)
* Przywracanie NuGet zignoruje teraz projektów środowiska dnx (`*.xproj`) powinny być przetwarzane z `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Zoptymalizowanych pod kątem wykorzystania sieci, podczas pracy z `index.json` i pakietu danych rejestracji [1426](https://github.com/NuGet/Home/issues/1426)
* Obsługa być bardziej niezawodne z usługami w wersji 2 pobierania ulepszona zasobów [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Poprawki

* Aktualizacja NuGet poprawnie aktualizuje `.csproj` / `.vcxproj` odwołania [1483](https://github.com/NuGet/Home/issues/1483)
* Teraz uniemożliwia folder .nuget lokalnych podczas SpecialFolders.UserProfile nie można odnaleźć [1531](https://github.com/NuGet/Home/issues/1531)
* Ulepszona obsługa pakietów w lokalnej pamięci podręcznej, które są uszkodzone podczas pobierania [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Pełną listę problemów skierowana dla rozszerzenia wiersza polecenia i Visual Studio można znaleźć w witrynie NuGet GitHub [3.2.1 punktu kontrolnego](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Znane problemy

W dalszym ciągu śledzenie problemów w naszej listy problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)