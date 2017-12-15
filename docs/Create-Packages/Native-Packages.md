---
title: "Tworzenie pakietów NuGet natywnego | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 7a70d748-efe2-4f8f-a3fd-67ddb0f6214e
description: "Szczegóły dotyczące tworzenia natywnych pakietów NuGet, które zawiera kod w języku C++ zamiast kodu zarządzanego do użycia w projektach C++."
keywords: "Natywnego pakietów NuGet, pakiety NuGet C++, pakiety kodu natywnego, przeznaczonych dla projektów C++"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fa5baaa6ecbad0f5f6dd85d657679ffbbbc8a47a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="creating-native-packages"></a>Tworzenie pakietów natywnego

Natywny pakiet zawiera natywny kod C++ zamiast kodu zarządzanego, dzięki któremu można używać w projektach C++. (Zobacz [natywnego pakietów C++](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages) w sekcji Consume.)

Było dostępne w projektach C++, pakietu musi wskazywać `native` framework. Obecnie nie ma żadnych numery wersji skojarzony z tym framework jako NuGet traktuje wszystkie projekty C++ takie same.

> [!Note]
> Należy uwzględnić *natywnego* w `<tags>` części Twojego `.nuspec` aby inni deweloperzy znaleźć pakietu, wyszukując na ten znacznik.

Natywny pakietów NuGet przeznaczonych dla `native` następnie zapewnić pliki w `\build`, `\content`, i `\tools` folderów; `\lib` nie jest używany w tym przypadku (NuGet nie można bezpośrednio dodać odwołania do projektu C++). Pakiet mogą również obejmować cele i pliki właściwości w `\build` czy NuGet automatycznie zostaną zaimportowane do projektów używające pakietu. Te pliki muszą nosić nazwy taki sam jak identyfikator pakietu z `.targets` i/lub `.props` rozszerzenia. Na przykład [cpprestsdk](https://nuget.org/packages/cpprestsdk/) pakiet zawiera `cpprestsdk.targets` pliku w jego `\build` folderu.

`\build` Folderu może służyć do wszystkich pakietów NuGet i nie tylko natywny pakietów. `\build` Folderu uwzględnia docelowych platform, tak jak `\content`, `\lib`, i `\tools` folderów. Oznacza to, można utworzyć `\build\net40` folderu i `\build\net45` folder i NuGet zaimportuje odpowiednie pliki właściwości i obiektów docelowych w projekcie. (Użycie skryptów programu PowerShell do importowania docelowych elementów MSBuild nie jest wymagane.)
