---
title: Informacje o wersji NuGet 3.2.1
description: Informacje o wersji programu NuGet 3.2.1 tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548193"
---
# <a name="nuget-321-release-notes"></a>Informacje o wersji NuGet 3.2.1

[Informacje o wersji NuGet 3.2](../release-notes/nuget-3.2.md) | [informacjach o wersji NuGet 3.3](../release-notes/nuget-3.3.md)

Rozwiązanie NuGet 3.2.1 dla wiersza polecenia został wydany 12 października 2015 za pomocą kliku optymalizacji i poprawek w wersji 3.2 i jest dostępny w [dist.nuget.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Ulepszenia

* NuGet teraz używa pliku konfiguracji z oryginalnego wielkość liter w wyrazie `NuGet.Config`.  Jest to ważne w systemach operacyjnych z uwzględnieniem wielkości liter [1427](https://github.com/NuGet/Home/issues/1427)
* Przywracanie pakietów NuGet teraz będzie ignorować projektami środowiska dnx (`*.xproj`) powinny zostać przetworzone za pomocą `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Zoptymalizowane pod kątem wykorzystania sieci, podczas pracy z `index.json` i utworzyć pakiet danych rejestracyjnych [1426](https://github.com/NuGet/Home/issues/1426)
* Pobieranie zasobów ulepszone obsługi się bardziej niezawodne usługi w wersji 2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Poprawki

* Aktualizacja NuGet poprawnie aktualizacji `.csproj` / `.vcxproj` odwołania [1483](https://github.com/NuGet/Home/issues/1483)
* Teraz uniemożliwia folderem lokalnym .nuget tworzone podczas SpecialFolders.UserProfile nie można odnaleźć [1531](https://github.com/NuGet/Home/issues/1531)
* Ulepszona obsługa pakietów w lokalnej pamięci podręcznej, które są uszkodzone podczas pobierania [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Pełną listę problemów rozwiązanych dla rozszerzenia programu wiersza polecenia i programu Visual Studio można znaleźć w witrynie NuGet GitHub [3.2.1 punkt kontrolny](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Znane problemy

W dalszym ciągu śledzenia problemów na naszej liście problemów GitHub, który znajduje się w temacie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)