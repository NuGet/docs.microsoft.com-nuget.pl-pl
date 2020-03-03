---
title: Ustaw typ pakietu NuGet
description: Opisuje typy pakietów, aby wskazać zamierzone użycie pakietu.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230827"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="2322b-103">Ustaw typ pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="2322b-103">Set a NuGet package type</span></span>

<span data-ttu-id="2322b-104">W przypadku programu NuGet 3.5 + pakiety można oznaczyć przy użyciu określonego *typu pakietu* , aby wskazać jego zamierzone użycie.</span><span class="sxs-lookup"><span data-stu-id="2322b-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="2322b-105">Pakiety, które nie są oznaczone jako typu, w tym wszystkie pakiety utworzone przy użyciu wcześniejszych wersji programu NuGet, domyślnie są typu `Dependency`.</span><span class="sxs-lookup"><span data-stu-id="2322b-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="2322b-106">pakiety typu `Dependency` umożliwiają dodawanie zasobów kompilacji lub czasu wykonywania do bibliotek i aplikacji, które można zainstalować w dowolnym typie projektu (przy założeniu, że są one zgodne).</span><span class="sxs-lookup"><span data-stu-id="2322b-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="2322b-107">pakiety typu `DotnetTool` są rozszerzeniami [interfejsu wiersza polecenia dotnet](/dotnet/articles/core/tools/index) i są wywoływane z wiersza poleceń.</span><span class="sxs-lookup"><span data-stu-id="2322b-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="2322b-108">Takie pakiety można instalować tylko w projektach .NET Core i nie mają wpływu na operacje przywracania.</span><span class="sxs-lookup"><span data-stu-id="2322b-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="2322b-109">Więcej informacji na temat tych rozszerzeń dla poszczególnych projektów można znaleźć w dokumentacji [rozszerzalności platformy .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) .</span><span class="sxs-lookup"><span data-stu-id="2322b-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="2322b-110">pakiety typu `Template` udostępniają [niestandardowe szablony](/dotnet/core/tools/custom-templates) , których można użyć do tworzenia plików lub projektów, takich jak aplikacja, usługa, narzędzie lub Biblioteka klas.</span><span class="sxs-lookup"><span data-stu-id="2322b-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="2322b-111">Pakiety typu niestandardowego używają dowolnego identyfikatora typu, który jest zgodny z tymi samymi regułami formatowania co identyfikatory pakietów.</span><span class="sxs-lookup"><span data-stu-id="2322b-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="2322b-112">Jednak żaden typ inny niż `Dependency` i `DotnetTool`nie jest rozpoznawany przez Menedżera pakietów NuGet w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2322b-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="2322b-113">Typy pakietów są ustawiane w pliku `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="2322b-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="2322b-114">Najlepiej, aby zapewnić zgodność z poprzednimi wersjami, aby *nie* ustawiać jawnie typu `Dependency` i zamiast tego polegać na NuGet przy założeniu, że typ nie jest określony.</span><span class="sxs-lookup"><span data-stu-id="2322b-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="2322b-115">`.nuspec`: wskaż typ pakietu w węźle `packageTypes\packageType` pod elementem `<metadata>`:</span><span class="sxs-lookup"><span data-stu-id="2322b-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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
