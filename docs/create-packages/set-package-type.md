---
title: Ustaw typ pakietu NuGet
description: W tym artykule opisano typy pakietów, aby wskazać przeznaczenie pakietu.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 8a3ba6af19125b75af17cab8c093e89485e20324
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843534"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="7eb40-103">Ustaw typ pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="7eb40-103">Set a NuGet package type</span></span>

<span data-ttu-id="7eb40-104">Nuget 3.5 + pakiety mogą być oznaczone określonym *typ pakietu* do wskazania jego przeznaczenia.</span><span class="sxs-lookup"><span data-stu-id="7eb40-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="7eb40-105">Domyślnie nie jest oznaczona za pomocą typu, w tym wszystkie pakiety utworzone w starszych wersjach programu NuGet, pakietów `Dependency` typu.</span><span class="sxs-lookup"><span data-stu-id="7eb40-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="7eb40-106">`Dependency` pakiety typu Dodaj zasoby kompilacji lub czasu wykonywania bibliotek i aplikacji, a można zainstalować w dowolnym typem projektu (przy założeniu, że są one zgodne).</span><span class="sxs-lookup"><span data-stu-id="7eb40-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="7eb40-107">`DotnetCliTool` rozszerzenia są pakiety typu [wiersz polecenia dotnet](/dotnet/articles/core/tools/index) i są wywoływane z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="7eb40-107">`DotnetCliTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="7eb40-108">Takie pakiety można zainstalować tylko w projektach .NET Core i nie mają wpływu na operacje przywracania.</span><span class="sxs-lookup"><span data-stu-id="7eb40-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="7eb40-109">Więcej informacji na temat tych rozszerzeń-projekt są dostępne w [rozszerzalność platformy .NET Core](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="7eb40-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="7eb40-110">Pakiety typu niestandardowego Użyj identyfikatora dowolnego typu, który jest zgodny z tych samych zasad format jako pakiet identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="7eb40-110">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="7eb40-111">Dowolny typ inny niż `Dependency` i `DotnetCliTool`, jednak nie są rozpoznawane przez Menedżera pakietów NuGet w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7eb40-111">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="7eb40-112">Typy pakietów są ustawiane w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="7eb40-112">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="7eb40-113">Jest najlepszym rozwiązaniem dla zapewnienia zgodności, aby *nie* jawnie ustawionej `Dependency` wpisz i zamiast polegać na NuGet, zakładając, że tego typu, gdy typ nie jest określony.</span><span class="sxs-lookup"><span data-stu-id="7eb40-113">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="7eb40-114">`.nuspec`: Wskazuje typ pakietu we `packageTypes\packageType` węźle `<metadata>` elementu:</span><span class="sxs-lookup"><span data-stu-id="7eb40-114">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
