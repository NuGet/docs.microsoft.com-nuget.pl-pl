---
title: Tworzenie pakietów NuGet macierzystego
description: Szczegóły dotyczące tworzenia natywnych pakietów NuGet, które zawiera kod w języku C++ zamiast kodu zarządzanego do użycia w projektach C++.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 086084bdfae5eace0b0a6aab17140a1fa48ae977
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817063"
---
# <a name="creating-native-packages"></a>Tworzenie pakietów natywnego

Natywny pakiet zawiera natywny kod C++ zamiast kodu zarządzanego, dzięki któremu można używać w projektach C++. (Zobacz [natywnego pakietów C++](../consume-packages/finding-and-choosing-packages.md#native-c-packages) w sekcji Consume.)

Było dostępne w projektach C++, pakietu musi wskazywać `native` framework. Obecnie nie ma żadnych numery wersji skojarzony z tym framework jako NuGet traktuje wszystkie projekty C++ takie same.

> [!Note]
> Należy uwzględnić *natywnego* w `<tags>` części Twojego `.nuspec` aby inni deweloperzy znaleźć pakietu, wyszukując na ten znacznik.

Natywny pakietów NuGet przeznaczonych dla `native` następnie zapewnić pliki w `\build`, `\content`, i `\tools` folderów; `\lib` nie jest używany w tym przypadku (NuGet nie można bezpośrednio dodać odwołania do projektu C++). Pakiet mogą również obejmować cele i pliki właściwości w `\build` czy NuGet automatycznie zostaną zaimportowane do projektów używające pakietu. Te pliki muszą nosić nazwy taki sam jak identyfikator pakietu z `.targets` i/lub `.props` rozszerzenia. Na przykład [cpprestsdk](https://nuget.org/packages/cpprestsdk/) pakiet zawiera `cpprestsdk.targets` pliku w jego `\build` folderu.

`\build` Folderu może służyć do wszystkich pakietów NuGet i nie tylko natywny pakietów. `\build` Folderu uwzględnia docelowych platform, tak jak `\content`, `\lib`, i `\tools` folderów. Oznacza to, można utworzyć `\build\net40` folderu i `\build\net45` folder i NuGet zaimportuje odpowiednie pliki właściwości i obiektów docelowych w projekcie. (Użycie skryptów programu PowerShell do importowania docelowych elementów MSBuild nie jest wymagane.)
