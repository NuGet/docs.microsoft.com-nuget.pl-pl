---
title: polecenia NuGet dotNet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "Krótkie odwołanie poleceń związanych z NuGet przy użyciu interfejsu wiersza polecenia platformy dotnet."
keywords: polecenia NuGet DotNet dotnet, przywracania dotnet, zmienne lokalne nuget dotnet, dotnet nuget wypychania, pakowanie dotnet nuget delete
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ff4779f46db102f1384650d82118b34fedd4413
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="dotnet-commands"></a><span data-ttu-id="1263d-104">polecenia dotNet</span><span class="sxs-lookup"><span data-stu-id="1263d-104">dotNet commands</span></span>

<span data-ttu-id="1263d-105">DotNet interfejsu wiersza polecenia, uruchamiany na systemu Windows, Mac OS X i Linux, zawiera pewną liczbę poleceń podstawowych nuget.exe wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="1263d-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="1263d-106">W przypadku, gdy dotnet zawiera żądanego polecenia, nie jest konieczne do pobrania nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="1263d-106">Where dotnet provides the desired commands, it is not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="1263d-107">[**Pakiet DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pakiety kodu dla zestawu SDK NETCore projekty do pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="1263d-107">[**dotnet pack**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs code for NETCore SDK projects into a NuGet package.</span></span> <span data-ttu-id="1263d-108">Należy używać innych typów projektów[`nuget pack`](cli-ref-pack.md)</span><span class="sxs-lookup"><span data-stu-id="1263d-108">All other project types should use [`nuget pack`](cli-ref-pack.md)</span></span>
- <span data-ttu-id="1263d-109">[**Przywracanie DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): przywraca zależności i narzędzia do projektu.</span><span class="sxs-lookup"><span data-stu-id="1263d-109">[**dotnet restore**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="1263d-110">Począwszy od NuGet 4.0 uruchomienie tego samego kodu jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="1263d-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="1263d-111">[**Zmienne lokalne nuget DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): usuwa lub wyświetla ich listę zasobów lokalnych NuGet, takich jak http żądania pamięci podręcznej, tymczasowego pamięci podręcznej lub folderu pakietów globalne dla komputera.</span><span class="sxs-lookup"><span data-stu-id="1263d-111">[**dotnet nuget locals**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="1263d-112">[**wypychania nuget DotNet**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): wypchnięcia pakietu na serwerze i publikuje ją dotyczy nuget.org, Visual Studio Team Services lub żadnych innych serwerów NuGet.</span><span class="sxs-lookup"><span data-stu-id="1263d-112">[**dotnet nuget push**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="1263d-113">[**Usuń DotNet nuget**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): usuwa lub unlists pakietu z serwera, dotyczy nuget.org, Visual Studio Team Services lub żadnych innych serwerów NuGet.</span><span class="sxs-lookup"><span data-stu-id="1263d-113">[**dotnet nuget delete**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
