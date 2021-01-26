---
title: Informacje o wersji pakietu NuGet 3.2.1
description: Informacje o wersji programu NuGet 3.2.1, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776522"
---
# <a name="nuget-321-release-notes"></a>Informacje o wersji pakietu NuGet 3.2.1

Informacje o wersji narzędzia [NuGet 3,2](../release-notes/nuget-3.2.md)  |  [Informacje o wersji narzędzia NuGet 3,3](../release-notes/nuget-3.3.md)

Program NuGet 3.2.1 dla wiersza polecenia został zwolniony 12 października 2015 z kilkuą optymalizacji i poprawek dla wersji 3,2 i jest dostępny z [dist.NuGet.org](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Ulepszenia

* Pakiet NuGet używa teraz pliku konfiguracji z oryginalną wielkością liter `NuGet.Config` .  Jest to ważne w przypadku systemów operacyjnych z uwzględnieniem wielkości liter [1427](https://github.com/NuGet/Home/issues/1427)
* Przywracanie NuGet zignoruje teraz środowiska DNX projekty ( `*.xproj` ), które powinny być przetwarzane przy użyciu `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Zoptymalizowane wykorzystanie sieci podczas pracy z `index.json` danymi rejestracji pakietu i ich pakietów [1426](https://github.com/NuGet/Home/issues/1426)
* Ulepszona obsługa pobierania zasobów jest bardziej niezawodna w przypadku usług w wersji 2 [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Poprawki

* Aktualizacja NuGet prawidłowo aktualizuje `.csproj` / `.vcxproj` odwołania [1483](https://github.com/NuGet/Home/issues/1483)
* Teraz uniemożliwiamy utworzenie lokalnego folderu. NuGet, gdy nie można zlokalizować SpecialFolders. UserProfile [1531](https://github.com/NuGet/Home/issues/1531)
* Ulepszona obsługa pakietów w lokalnej pamięci podręcznej, które są uszkodzone podczas pobierania [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Pełna lista problemów rozwiązanych w przypadku rozszerzenia wiersza polecenia i programu Visual Studio znajduje się w obszarze [kontrolnym](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) NuGet GitHub 3.2.1

## <a name="known-issues"></a>Znane problemy

Będziemy nadal śledzić problemy na naszej liście problemów usługi GitHub, którą można znaleźć w witrynie: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)