---
title: polecenia NuGet interfejsu wiersza polecenia platformy DotNet
description: Krótkie odniesienie do polecenia związane z NuGet, za pomocą interfejsu wiersza polecenia dotnet.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: cc99b327c0edb4aeb573dfa8c2f9b9dba7b8cc38
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426001"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="1f117-103">polecenia interfejsu wiersza polecenia platformy DotNet</span><span class="sxs-lookup"><span data-stu-id="1f117-103">dotnet CLI commands</span></span>

<span data-ttu-id="1f117-104">`dotnet` Interfejsu wiersza polecenia (CLI), która jest uruchamiana w Windows, Mac OS X i Linux, oferuje pewną liczbę podstawowych poleceń, takich jak instalowanie, przywracania i publikowania pakietów.</span><span class="sxs-lookup"><span data-stu-id="1f117-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="1f117-105">Jeśli dotnet odpowiada potrzebom użytkownika, nie jest konieczne użycie `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="1f117-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="1f117-106">Przykłady użycia tych poleceń, aby korzystanie z pakietów, zobacz [instalowania i zarządzania pakietami przy użyciu interfejsu wiersza polecenia platformy dotnet](../consume-packages/install-use-packages-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1f117-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="1f117-107">Przykłady korzystania z tych poleceń do tworzenia pakietów, zobacz [tworzenie i publikowanie pakietu przy użyciu interfejsu wiersza polecenia platformy dotnet]... / quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1f117-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI]../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="1f117-108">Pełne polecenie odwołania na `dotnet` interfejsu wiersza polecenia, zobacz [narzędzi interfejsu wiersza polecenia (CLI) platformy .NET Core](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="1f117-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="1f117-109">Użycie pakietu</span><span class="sxs-lookup"><span data-stu-id="1f117-109">Package consumption</span></span>

- <span data-ttu-id="1f117-110">[**polecenia DotNet Dodaj pakiet**](/dotnet/core/tools/dotnet-add-package): Dodaje odwołania do pakietu do pliku projektu, a następnie uruchamia `dotnet restore` do zainstalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="1f117-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="1f117-111">[**polecenia DotNet, usuń pakiet**](/dotnet/core/tools/dotnet-remove-package): Usuwa odwołanie do pakietu z pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="1f117-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="1f117-112">[**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Przywraca zależności i narzędzia do projektu.</span><span class="sxs-lookup"><span data-stu-id="1f117-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="1f117-113">Począwszy od NuGet 4.0, spowoduje to uruchomienie tego samego kodu jako `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="1f117-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="1f117-114">[**Zmienne lokalne nuget DotNet**](/dotnet/core/tools/dotnet-nuget-locals): Wyświetla lokalizacje *globalnymi pakietami*, *pamięci podręcznej http*, i *temp* foldery i czyści zawartość tych folderów.</span><span class="sxs-lookup"><span data-stu-id="1f117-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="1f117-115">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="1f117-115">Package creation</span></span>

- <span data-ttu-id="1f117-116">[**pakietu DotNet**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Pakiety kodu do pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="1f117-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="1f117-117">Począwszy od NuGet 4.0, spowoduje to uruchomienie tego samego kodu jako `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="1f117-117">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="1f117-118">[**wypychane nuget DotNet**](/dotnet/core/tools/dotnet-nuget-push): Wypycha pakietu do serwera i publikuje go dotyczy nuget.org, Visual Studio Team Services i innych firm serwery NuGet.</span><span class="sxs-lookup"><span data-stu-id="1f117-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="1f117-119">[**Usuń DotNet nuget**](/dotnet/core/tools/dotnet-nuget-delete): Usuwa lub unlists pakietu z hosta dotyczy nuget.org, Visual Studio Team Services i innych firm serwery NuGet.</span><span class="sxs-lookup"><span data-stu-id="1f117-119">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
