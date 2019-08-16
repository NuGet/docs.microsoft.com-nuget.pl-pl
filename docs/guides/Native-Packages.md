---
title: Tworzenie natywnych pakietów NuGet
description: Szczegółowe informacje na temat tworzenia natywnych pakietów C++ NuGet, które zawierają kod zamiast kodu zarządzanego, C++ do użycia w projektach.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e0ec5323f7be53bef6637ad69540a66abbf22711
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520598"
---
# <a name="creating-native-packages"></a>Tworzenie pakietów natywnych

Pakiet macierzysty zawiera natywne dane binarne zamiast zestawów zarządzanych, umożliwiając ich używanie w C++ projektach (lub podobnych). (Zobacz [pakiety C++ natywne](../consume-packages/finding-and-choosing-packages.md#native-c-packages) w sekcji Korzystanie).

Aby można było go używać w C++ projekcie, pakiet musi być celem `native` struktury. Obecnie nie ma żadnych numerów wersji skojarzonych z tym środowiskiem, ponieważ pakiet NuGet traktuje wszystkie C++ projekty w taki sam sposób.

> [!Note]
> Upewnij się, że w `<tags>` sekcji Twojego `.nuspec` tematu znajduje się kod macierzysty, aby pomóc innym deweloperom znaleźć swój pakiet, wyszukując ten tag.

Natywne pakiety `native` NuGet, które umożliwiają udostępnianie plików `\content`w `\build`, `\tools` i folderów; nie jest używany w tym przypadku (NuGet nie może bezpośrednio dodać odwołań do C++ projektu). `\lib` Pakiet może zawierać również elementy docelowe i pliki props w `\build` tym pakiecie NuGet zostaną automatycznie zaimportowane do projektów, które zużywają pakiet. Te pliki muszą mieć taką samą nazwę jak identyfikator pakietu z `.targets` rozszerzeniami i/lub. `.props` Na przykład pakiet [cpprestsdk](https://nuget.org/packages/cpprestsdk/) zawiera `cpprestsdk.targets` plik w `\build` folderze.

Ten `\build` folder może być używany dla wszystkich pakietów NuGet, a nie tylko dla pakietów natywnych. Folder uwzględnia Platformy docelowe `\content`, podobnie jak foldery, `\lib`i `\tools`. `\build` Oznacza to, że można utworzyć `\build\net40` folder `\build\net45` i folder, a plik NuGet zaimportuje odpowiednie elementy props i targets do projektu. (Użycie skryptów programu PowerShell do importowania obiektów docelowych MSBuild nie jest konieczne).
