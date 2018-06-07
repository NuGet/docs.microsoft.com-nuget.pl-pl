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
# <a name="creating-native-packages"></a><span data-ttu-id="eb7fb-103">Tworzenie pakietów natywnego</span><span class="sxs-lookup"><span data-stu-id="eb7fb-103">Creating native packages</span></span>

<span data-ttu-id="eb7fb-104">Natywny pakiet zawiera natywny kod C++ zamiast kodu zarządzanego, dzięki któremu można używać w projektach C++.</span><span class="sxs-lookup"><span data-stu-id="eb7fb-104">A native package contains native C++ code instead of managed code, allowing it to be used within C++ projects.</span></span> <span data-ttu-id="eb7fb-105">(Zobacz [natywnego pakietów C++](../consume-packages/finding-and-choosing-packages.md#native-c-packages) w sekcji Consume.)</span><span class="sxs-lookup"><span data-stu-id="eb7fb-105">(See [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-c-packages) in the Consume section.)</span></span>

<span data-ttu-id="eb7fb-106">Było dostępne w projektach C++, pakietu musi wskazywać `native` framework.</span><span class="sxs-lookup"><span data-stu-id="eb7fb-106">To be consumable in a C++ project, a package must target the `native` framework.</span></span> <span data-ttu-id="eb7fb-107">Obecnie nie ma żadnych numery wersji skojarzony z tym framework jako NuGet traktuje wszystkie projekty C++ takie same.</span><span class="sxs-lookup"><span data-stu-id="eb7fb-107">At present there are not any version numbers associated with this framework as NuGet treats all C++ projects the same.</span></span>

> [!Note]
> <span data-ttu-id="eb7fb-108">Należy uwzględnić *natywnego* w `<tags>` części Twojego `.nuspec` aby inni deweloperzy znaleźć pakietu, wyszukując na ten znacznik.</span><span class="sxs-lookup"><span data-stu-id="eb7fb-108">Be sure to include *native* in the `<tags>` section of your `.nuspec` to help other developers find your package by searching on that tag.</span></span>

<span data-ttu-id="eb7fb-109">Natywny pakietów NuGet przeznaczonych dla `native` następnie zapewnić pliki w `\build`, `\content`, i `\tools` folderów; `\lib` nie jest używany w tym przypadku (NuGet nie można bezpośrednio dodać odwołania do projektu C++).</span><span class="sxs-lookup"><span data-stu-id="eb7fb-109">Native NuGet packages targeting `native` then provide files in `\build`, `\content`, and `\tools` folders; `\lib` is not used in this case (NuGet cannot directly add references to a C++ project).</span></span> <span data-ttu-id="eb7fb-110">Pakiet mogą również obejmować cele i pliki właściwości w `\build` czy NuGet automatycznie zostaną zaimportowane do projektów używające pakietu.</span><span class="sxs-lookup"><span data-stu-id="eb7fb-110">A package may also include targets and props files in `\build` that NuGet will automatically import into projects that consume the package.</span></span> <span data-ttu-id="eb7fb-111">Te pliki muszą nosić nazwy taki sam jak identyfikator pakietu z `.targets` i/lub `.props` rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="eb7fb-111">Those files must be named the same as the package ID with the `.targets` and/or `.props` extensions.</span></span> <span data-ttu-id="eb7fb-112">Na przykład [cpprestsdk](https://nuget.org/packages/cpprestsdk/) pakiet zawiera `cpprestsdk.targets` pliku w jego `\build` folderu.</span><span class="sxs-lookup"><span data-stu-id="eb7fb-112">For example, the [cpprestsdk](https://nuget.org/packages/cpprestsdk/) package includes a `cpprestsdk.targets` file in its `\build` folder.</span></span>

<span data-ttu-id="eb7fb-113">`\build` Folderu może służyć do wszystkich pakietów NuGet i nie tylko natywny pakietów.</span><span class="sxs-lookup"><span data-stu-id="eb7fb-113">The `\build` folder can be used for all NuGet packages and not just native packages.</span></span> <span data-ttu-id="eb7fb-114">`\build` Folderu uwzględnia docelowych platform, tak jak `\content`, `\lib`, i `\tools` folderów.</span><span class="sxs-lookup"><span data-stu-id="eb7fb-114">The `\build` folder respects target frameworks just like the `\content`, `\lib`, and `\tools` folders.</span></span> <span data-ttu-id="eb7fb-115">Oznacza to, można utworzyć `\build\net40` folderu i `\build\net45` folder i NuGet zaimportuje odpowiednie pliki właściwości i obiektów docelowych w projekcie.</span><span class="sxs-lookup"><span data-stu-id="eb7fb-115">This means you can create a `\build\net40` folder and a `\build\net45` folder and NuGet will import the appropriate props and targets files into the project.</span></span> <span data-ttu-id="eb7fb-116">(Użycie skryptów programu PowerShell do importowania docelowych elementów MSBuild nie jest wymagane.)</span><span class="sxs-lookup"><span data-stu-id="eb7fb-116">(Use of PowerShell scripts to import MSBuild targets is not needed.)</span></span>
