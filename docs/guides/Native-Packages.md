---
title: Tworzenie natywnych pakietów NuGet
description: Szczegółowe informacje na temat tworzenia natywnych pakietów NuGet, które zawierają kod języka C++ zamiast kodu zarządzanego, do użycia w projektach C++.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 2a95fca2ce5496512627e913273e5b66128e34c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774210"
---
# <a name="creating-native-packages"></a>Tworzenie pakietów natywnych

Pakiet macierzysty zawiera natywne dane binarne zamiast zestawów zarządzanych, umożliwiając ich używanie w projektach C++ (lub podobnych). (Zobacz [natywne pakiety C++](../consume-packages/finding-and-choosing-packages.md#native-c-packages) w sekcji Używanie).

Aby można było korzystać z projektu C++, pakiet musi być celem `native` struktury. Obecnie nie ma żadnych numerów wersji skojarzonych z tym środowiskiem, ponieważ pakiet NuGet traktuje wszystkie projekty C++ w ten sam sposób.

> [!Note]
> Upewnij się, że w sekcji Twojego tematu znajduje się kod *macierzysty* , `<tags>` `.nuspec` Aby pomóc innym deweloperom znaleźć swój pakiet, wyszukując ten tag.

Natywne pakiety NuGet `native` , które umożliwiają udostępnienie plików w `\build` , `\content` , i `\tools` folderów; `\lib` nie są używane w tym przypadku (NuGet nie może bezpośrednio dodawać odwołań do projektu C++). Pakiet może zawierać również elementy docelowe i pliki props w `\build` tym pakiecie NuGet zostaną automatycznie zaimportowane do projektów, które zużywają pakiet. Te pliki muszą mieć taką samą nazwę jak identyfikator pakietu z `.targets` rozszerzeniami i/lub `.props` . Na przykład pakiet [cpprestsdk](https://nuget.org/packages/cpprestsdk/) zawiera `cpprestsdk.targets` plik w `\build` folderze.

Ten `\build` folder może być używany dla wszystkich pakietów NuGet, a nie tylko dla pakietów natywnych. `\build`Folder uwzględnia Platformy docelowe, podobnie jak `\content` `\lib` foldery, i `\tools` . Oznacza to, że można utworzyć `\build\net40` folder i `\build\net45` folder, a plik NuGet zaimportuje odpowiednie elementy props i targets do projektu. (Użycie skryptów programu PowerShell do importowania obiektów docelowych MSBuild nie jest konieczne).
