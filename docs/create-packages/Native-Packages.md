---
title: Tworzenie pakietów NuGet natywne
description: Szczegółowe informacje o tworzeniu natywnych pakiety NuGet zawiera kod języka C++, zamiast kodu zarządzanego dla używać w projektach C++.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: f054a1cae7328d3e910d11ac1bfc5f98505e5879
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546536"
---
# <a name="creating-native-packages"></a>Tworząc pakiety natywne

Natywne pakiet zawiera natywny kod C++ zamiast kodu zarządzanego, dzięki któremu można używać w projektach C++. (Zobacz [pakiety natywne C++](../consume-packages/finding-and-choosing-packages.md#native-c-packages) w sekcji zużywania.)

Aby być w użyciu w projekcie języka C++, musi być przeznaczony dla pakietu `native` framework. Obecnie nie ma żadnych numery wersji skojarzony z tym framework jako NuGet traktuje wszystkich projektów w języku C++ takie same.

> [!Note]
> Należy uwzględnić *natywnych* w `<tags>` części Twojej `.nuspec` pomagające deweloperom w innych znaleźć pakiet, wyszukując według tego tagu.

Pakiety natywne NuGet określanie wartości docelowej `native` podajemy pliki w `\build`, `\content`, i `\tools` folderów; `\lib` nie jest używany w tym przypadku (NuGet bezpośrednio nie można dodać odwołania do projektu w języku C++). Pakiet może również obejmować cele i pliki właściwości w `\build` NuGet spowoduje automatyczne importowanie w projektach korzystających z pakietu. Te pliki muszą nosić taki sam jak identyfikator pakietu z `.targets` i/lub `.props` rozszerzenia. Na przykład [cpprestsdk](https://nuget.org/packages/cpprestsdk/) pakiet zawiera `cpprestsdk.targets` pliku w jego `\build` folderu.

`\build` Folderu może służyć do wszystkich pakietów NuGet i nie tylko natywny pakietów. `\build` Folderu szanuje platform docelowych, podobnie jak `\content`, `\lib`, i `\tools` folderów. Oznacza to, możesz utworzyć `\build\net40` folder i `\build\net45` NuGet i folderu zostaną zaimportowane odpowiednie pliki cele i właściwości do projektu. (Użyj skryptów programu PowerShell do importowania elementów docelowych MSBuild jest zbędny).
