---
title: Ustawianie typu pakietu NuGet
description: W tym artykule opisano typy pakietów, aby wskazać zamierzone użycie pakietu.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230827"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="7d970-103">Ustawianie typu pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="7d970-103">Set a NuGet package type</span></span>

<span data-ttu-id="7d970-104">Z NuGet 3.5+, pakiety mogą być oznaczone określonego *typu pakietu,* aby wskazać jego przeznaczenie.</span><span class="sxs-lookup"><span data-stu-id="7d970-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="7d970-105">Pakiety nie są oznaczone typem, w tym wszystkie pakiety `Dependency` utworzone z wcześniejszymi wersjami NuGet, domyślnie typu.</span><span class="sxs-lookup"><span data-stu-id="7d970-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="7d970-106">`Dependency`pakiety typu dodać zasoby kompilacji lub wykonywania do bibliotek i aplikacji i mogą być instalowane w dowolnym typie projektu (przy założeniu, że są one zgodne).</span><span class="sxs-lookup"><span data-stu-id="7d970-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="7d970-107">`DotnetTool`pakiety typów są rozszerzeniami do [dotnet CLI](/dotnet/articles/core/tools/index) i są wywoływane z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="7d970-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="7d970-108">Takie pakiety mogą być instalowane tylko w projektach .NET Core i nie mają wpływu na operacje przywracania.</span><span class="sxs-lookup"><span data-stu-id="7d970-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="7d970-109">Więcej szczegółów na temat tych rozszerzeń dla projektu są dostępne w dokumentacji [rozszerzalności .NET Core.](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)</span><span class="sxs-lookup"><span data-stu-id="7d970-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="7d970-110">`Template`pakiety typów zapewniają [niestandardowe szablony,](/dotnet/core/tools/custom-templates) które mogą być używane do tworzenia plików lub projektów, takich jak aplikacja, usługa, narzędzie lub biblioteka klas.</span><span class="sxs-lookup"><span data-stu-id="7d970-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="7d970-111">Niestandardowe pakiety typów używają dowolnego identyfikatora typu, który jest zgodny z regułami tego samego formatu co identyfikatory pakietów.</span><span class="sxs-lookup"><span data-stu-id="7d970-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="7d970-112">Każdy typ `Dependency` inny `DotnetTool`niż i , jednak nie są rozpoznawane przez Menedżera pakietów NuGet w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d970-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="7d970-113">Typy pakietów `.nuspec` są ustawiane w pliku.</span><span class="sxs-lookup"><span data-stu-id="7d970-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="7d970-114">Najlepiej jest dla zgodności z powrotem, aby *nie* jawnie ustawić `Dependency` typ i zamiast polegać na NuGet przy założeniu, że ten typ, gdy nie określono typu.</span><span class="sxs-lookup"><span data-stu-id="7d970-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="7d970-115">`.nuspec`: Wskazać typ pakietu `packageTypes\packageType` w `<metadata>` węźle pod elementem:</span><span class="sxs-lookup"><span data-stu-id="7d970-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
