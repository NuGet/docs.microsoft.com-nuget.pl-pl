---
title: "Tworzenie pakietów NuGet natywnego | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Szczegóły dotyczące tworzenia natywnych pakietów NuGet, które zawiera kod w języku C++ zamiast kodu zarządzanego do użycia w projektach C++."
keywords: "Natywnego pakietów NuGet, pakiety NuGet C++, pakiety kodu natywnego, przeznaczonych dla projektów C++"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 71f4eca411d520630ca7d77165b8f03cd32af290
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="creating-native-packages"></a><span data-ttu-id="8e379-104">Tworzenie pakietów natywnego</span><span class="sxs-lookup"><span data-stu-id="8e379-104">Creating native packages</span></span>

<span data-ttu-id="8e379-105">Natywny pakiet zawiera natywny kod C++ zamiast kodu zarządzanego, dzięki któremu można używać w projektach C++.</span><span class="sxs-lookup"><span data-stu-id="8e379-105">A native package contains native C++ code instead of managed code, allowing it to be used within C++ projects.</span></span> <span data-ttu-id="8e379-106">(Zobacz [natywnego pakietów C++](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages) w sekcji Consume.)</span><span class="sxs-lookup"><span data-stu-id="8e379-106">(See [Native C++ Packages](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages) in the Consume section.)</span></span>

<span data-ttu-id="8e379-107">Było dostępne w projektach C++, pakietu musi wskazywać `native` framework.</span><span class="sxs-lookup"><span data-stu-id="8e379-107">To be consumable in a C++ project, a package must target the `native` framework.</span></span> <span data-ttu-id="8e379-108">Obecnie nie ma żadnych numery wersji skojarzony z tym framework jako NuGet traktuje wszystkie projekty C++ takie same.</span><span class="sxs-lookup"><span data-stu-id="8e379-108">At present there are not any version numbers associated with this framework as NuGet treats all C++ projects the same.</span></span>

> [!Note]
> <span data-ttu-id="8e379-109">Należy uwzględnić *natywnego* w `<tags>` części Twojego `.nuspec` aby inni deweloperzy znaleźć pakietu, wyszukując na ten znacznik.</span><span class="sxs-lookup"><span data-stu-id="8e379-109">Be sure to include *native* in the `<tags>` section of your `.nuspec` to help other developers find your package by searching on that tag.</span></span>

<span data-ttu-id="8e379-110">Natywny pakietów NuGet przeznaczonych dla `native` następnie zapewnić pliki w `\build`, `\content`, i `\tools` folderów; `\lib` nie jest używany w tym przypadku (NuGet nie można bezpośrednio dodać odwołania do projektu C++).</span><span class="sxs-lookup"><span data-stu-id="8e379-110">Native NuGet packages targeting `native` then provide files in `\build`, `\content`, and `\tools` folders; `\lib` is not used in this case (NuGet cannot directly add references to a C++ project).</span></span> <span data-ttu-id="8e379-111">Pakiet mogą również obejmować cele i pliki właściwości w `\build` czy NuGet automatycznie zostaną zaimportowane do projektów używające pakietu.</span><span class="sxs-lookup"><span data-stu-id="8e379-111">A package may also include targets and props files in `\build` that NuGet will automatically import into projects that consume the package.</span></span> <span data-ttu-id="8e379-112">Te pliki muszą nosić nazwy taki sam jak identyfikator pakietu z `.targets` i/lub `.props` rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="8e379-112">Those files must be named the same as the package ID with the `.targets` and/or `.props` extensions.</span></span> <span data-ttu-id="8e379-113">Na przykład [cpprestsdk](https://nuget.org/packages/cpprestsdk/) pakiet zawiera `cpprestsdk.targets` pliku w jego `\build` folderu.</span><span class="sxs-lookup"><span data-stu-id="8e379-113">For example, the [cpprestsdk](https://nuget.org/packages/cpprestsdk/) package includes a `cpprestsdk.targets` file in its `\build` folder.</span></span>

<span data-ttu-id="8e379-114">`\build` Folderu może służyć do wszystkich pakietów NuGet i nie tylko natywny pakietów.</span><span class="sxs-lookup"><span data-stu-id="8e379-114">The `\build` folder can be used for all NuGet packages and not just native packages.</span></span> <span data-ttu-id="8e379-115">`\build` Folderu uwzględnia docelowych platform, tak jak `\content`, `\lib`, i `\tools` folderów.</span><span class="sxs-lookup"><span data-stu-id="8e379-115">The `\build` folder respects target frameworks just like the `\content`, `\lib`, and `\tools` folders.</span></span> <span data-ttu-id="8e379-116">Oznacza to, można utworzyć `\build\net40` folderu i `\build\net45` folder i NuGet zaimportuje odpowiednie pliki właściwości i obiektów docelowych w projekcie.</span><span class="sxs-lookup"><span data-stu-id="8e379-116">This means you can create a `\build\net40` folder and a `\build\net45` folder and NuGet will import the appropriate props and targets files into the project.</span></span> <span data-ttu-id="8e379-117">(Użycie skryptów programu PowerShell do importowania docelowych elementów MSBuild nie jest wymagane.)</span><span class="sxs-lookup"><span data-stu-id="8e379-117">(Use of PowerShell scripts to import MSBuild targets is not needed.)</span></span>
