---
title: polecenia NuGet dotNet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Krótkie odwołanie poleceń związanych z NuGet przy użyciu interfejsu wiersza polecenia platformy dotnet."
keywords: polecenia NuGet DotNet dotnet, przywracania dotnet, zmienne lokalne nuget dotnet, dotnet nuget wypychania, pakowanie dotnet nuget delete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2851938cd43b35454d8e4ad595fbd93229d4dd72
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/20/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="d8256-104">polecenia dotNet</span><span class="sxs-lookup"><span data-stu-id="d8256-104">dotNet commands</span></span>

<span data-ttu-id="d8256-105">`dotnet` Interfejsu wiersza polecenia, co jest uruchomiony na systemu Windows, Mac OS X i Linux, zawiera pewną liczbę poleceń podstawowych nuget.exe wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="d8256-105">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="d8256-106">Jeśli dotnet odpowiada potrzebom użytkownika, nie jest konieczne użycie `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="d8256-106">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="d8256-107">Aby uzyskać pełne informacje na `dotnet`, zobacz [narzędzi interfejsu wiersza polecenia (CLI) platformy .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="d8256-107">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="d8256-108">Użycie pakietu</span><span class="sxs-lookup"><span data-stu-id="d8256-108">Package consumption</span></span>

- <span data-ttu-id="d8256-109">[**DotNet Dodaj pakiet**](/dotnet/core/tools/dotnet-add-package): Dodaje odwołanie pakietu do pliku projektu, a następnie uruchamia `dotnet restore` do zainstalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="d8256-109">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="d8256-110">[**DotNet usunąć pakiet**](/dotnet/core/tools/dotnet-remove-package): Usuwa odwołanie do pakietu z pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="d8256-110">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="d8256-111">[**Przywracanie DotNet**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): przywraca zależności i narzędzia do projektu.</span><span class="sxs-lookup"><span data-stu-id="d8256-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="d8256-112">Począwszy od NuGet 4.0 uruchomienie tego samego kodu jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="d8256-112">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="d8256-113">[**Zmienne lokalne nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): usuwa lub wyświetla ich listę zasobów lokalnych NuGet pamięci podręcznej żądania http, tymczasowego pamięci podręcznej i folderu pakietów globalne dla komputera.</span><span class="sxs-lookup"><span data-stu-id="d8256-113">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as the http-request cache, the temporary cache, and the machine-wide global packages folder.</span></span>

## <a name="package-creation"></a><span data-ttu-id="d8256-114">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="d8256-114">Package creation</span></span>

- <span data-ttu-id="d8256-115">[**Pakiet DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pakiety kodu do pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="d8256-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="d8256-116">Począwszy od NuGet 4.0 uruchomienie tego samego kodu jako `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="d8256-116">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="d8256-117">[**wypychania nuget DotNet**](/dotnet/core/tools/dotnet-nuget-push): wypchnięcia pakietu na serwerze i publikuje ją dotyczy nuget.org, Visual Studio Team Services i serwery NuGet innych firm.</span><span class="sxs-lookup"><span data-stu-id="d8256-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="d8256-118">[**Usuń DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): usuwa lub unlists pakietu z hosta i mające zastosowanie do nuget.org, Visual Studio Team Services i serwery NuGet innych firm.</span><span class="sxs-lookup"><span data-stu-id="d8256-118">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
