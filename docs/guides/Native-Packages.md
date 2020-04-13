---
title: Tworzenie natywnych pakietów NuGet
description: Szczegóły dotyczące tworzenia natywnych pakietów NuGet, który zawiera kod C++ zamiast kodu zarządzanego, do użycia w projektach języka C++.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e0ec5323f7be53bef6637ad69540a66abbf22711
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "69520598"
---
# <a name="creating-native-packages"></a>Tworzenie pakietów natywnych

Pakiet macierzysty zawiera natywne pliki binarne zamiast zarządzanych zestawów, dzięki czemu można go używać w projektach języka C++ (lub podobnych). (Zobacz [natywne pakiety C++](../consume-packages/finding-and-choosing-packages.md#native-c-packages) w sekcji Zużycie).

Aby być materiałów eksploatacyjnych w projekcie Języka `native` C++, pakiet musi być ukierunkowany na platformę. Obecnie nie istnieją żadne numery wersji skojarzone z tej struktury, jak NuGet traktuje wszystkie projekty C++ takie same.

> [!Note]
> Pamiętaj, aby uwzględnić `<tags>` `.nuspec` *natywne* w sekcji, aby pomóc innym deweloperom znaleźć pakiet, wyszukując na tym tagu.

`native` Natywne kierowanie pakietów `\build` `\content`NuGet `\tools` następnie zapewniają pliki w , i folderach; `\lib` nie jest używany w tym przypadku (NuGet nie można bezpośrednio dodać odwołania do projektu C++). Pakiet może również zawierać obiekty docelowe i props plików, w `\build` tym NuGet automatycznie zaimportuje do projektów, które korzystają z pakietu. Pliki te muszą być nazwane taką samą jak identyfikator pakietu z `.targets` rozszerzeniami i/lub `.props` rozszerzeniami. Na przykład pakiet [cpprestsdk](https://nuget.org/packages/cpprestsdk/) `cpprestsdk.targets` zawiera plik `\build` w swoim folderze.

Folder `\build` może być używany dla wszystkich pakietów NuGet, a nie tylko pakietów natywnych. Folder `\build` jest zgodny z ramami `\content` `\lib`docelowymi, podobnie jak foldery i `\tools` foldery. Oznacza to, że `\build\net40` można `\build\net45` utworzyć folder i folder i NuGet zaimportuje odpowiednie rekwizyty i pliki docelowe do projektu. (Użycie skryptów programu PowerShell do importowania obiektów docelowych MSBuild nie jest potrzebne).
