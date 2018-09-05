---
title: polecenia NuGet DotNet
description: Krótkie odniesienie do polecenia związane z NuGet, za pomocą interfejsu wiersza polecenia dotnet.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546319"
---
# <a name="dotnet-commands"></a><span data-ttu-id="88c2c-103">polecenia DotNet</span><span class="sxs-lookup"><span data-stu-id="88c2c-103">dotnet commands</span></span>

<span data-ttu-id="88c2c-104">`dotnet` Interfejsu wiersza polecenia, który jest uruchamiany w Windows, Mac OS X i Linux, oferuje pewną liczbę poleceń nuget.exe podstawowe, zgodnie z poniższymi.</span><span class="sxs-lookup"><span data-stu-id="88c2c-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="88c2c-105">Jeśli dotnet odpowiada potrzebom użytkownika, nie jest konieczne użycie `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="88c2c-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="88c2c-106">Aby uzyskać pełne informacje na temat `dotnet`, zobacz [narzędzi interfejsu wiersza polecenia (CLI) platformy .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="88c2c-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="88c2c-107">Użycie pakietu</span><span class="sxs-lookup"><span data-stu-id="88c2c-107">Package consumption</span></span>

- <span data-ttu-id="88c2c-108">[**polecenia DotNet Dodaj pakiet**](/dotnet/core/tools/dotnet-add-package): Dodaje odwołanie do pakietu do pliku projektu, a następnie uruchamia `dotnet restore` do zainstalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="88c2c-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="88c2c-109">[**polecenia DotNet, usuń pakiet**](/dotnet/core/tools/dotnet-remove-package): Usuwa odwołanie do pakietu z pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="88c2c-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="88c2c-110">[**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): przywraca zależności i narzędzia do projektu.</span><span class="sxs-lookup"><span data-stu-id="88c2c-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="88c2c-111">Począwszy od NuGet 4.0, spowoduje to uruchomienie tego samego kodu jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="88c2c-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="88c2c-112">[**Zmienne lokalne nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): Wyświetla lokalizacje *globalnymi pakietami*, *pamięci podręcznej http*, i *temp* folderów i czyści zawartość te foldery.</span><span class="sxs-lookup"><span data-stu-id="88c2c-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="88c2c-113">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="88c2c-113">Package creation</span></span>

- <span data-ttu-id="88c2c-114">[**pakietu DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): pakiety kodu do pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="88c2c-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="88c2c-115">Począwszy od NuGet 4.0, spowoduje to uruchomienie tego samego kodu jako `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="88c2c-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="88c2c-116">[**wypychane nuget DotNet**](/dotnet/core/tools/dotnet-nuget-push): wypychanie pakietu do serwera i publikuje go dotyczy nuget.org, Visual Studio Team Services i innych firm serwery NuGet.</span><span class="sxs-lookup"><span data-stu-id="88c2c-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="88c2c-117">[**Usuń DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): usuwa lub unlists pakietu z hosta dotyczy nuget.org, Visual Studio Team Services i innych firm serwery NuGet.</span><span class="sxs-lookup"><span data-stu-id="88c2c-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
