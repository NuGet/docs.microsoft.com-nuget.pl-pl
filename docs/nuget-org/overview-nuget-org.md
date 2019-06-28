---
title: Omówienie NuGet.org
description: Omówienie NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427522"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="bb37a-103">Omówienie NuGet.org</span><span class="sxs-lookup"><span data-stu-id="bb37a-103">Overview of NuGet.org</span></span>

<span data-ttu-id="bb37a-104">NuGet.org jest hostem publicznych pakietów NuGet, które są wykorzystywane przez miliony deweloperów platformy .NET i .NET Core, każdego dnia.</span><span class="sxs-lookup"><span data-stu-id="bb37a-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="bb37a-105">Rola NuGet.org należący do ekosystemu NuGet</span><span class="sxs-lookup"><span data-stu-id="bb37a-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="bb37a-106">W roli jako publiczny hosta NuGet.org, sam przechowuje centralne repozytorium ponad 100 000 pakietów unikatowy w [nuget.org](https://www.nuget.org). NuGet.org nie jest możliwa tylko hosta dla pakietów.</span><span class="sxs-lookup"><span data-stu-id="bb37a-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="bb37a-107">Technologia NuGet można również do hostowania pakietów przez użytkowników w chmurze (takie jak na DevOps platformy Azure), w sieci prywatnej lub nawet po prostu lokalnego systemu plików.</span><span class="sxs-lookup"><span data-stu-id="bb37a-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="bb37a-108">Jeśli interesuje Cię inny host lub opcji hostingu, zobacz [hostingu źródła NuGet](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="bb37a-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="bb37a-109">NuGet.org, takich jak dowolnego hosta, w przypadku pakietów NuGet służy jako punkt połączenia między pakietu *twórców* i pakietu *konsumentów*.</span><span class="sxs-lookup"><span data-stu-id="bb37a-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="bb37a-110">Twórcy tworzenie przydatne pakietów NuGet i opublikuj je.</span><span class="sxs-lookup"><span data-stu-id="bb37a-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="bb37a-111">Konsumenci Wyszukaj pakiety przydatne i są zgodne na hostach dostępny, pobieranie oraz w swoich projektach, takich jak te pakiety.</span><span class="sxs-lookup"><span data-stu-id="bb37a-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="bb37a-112">Po zainstalowaniu w projekcie, interfejsy API te pakiety są dostępne w pozostałej części kodu projektu.</span><span class="sxs-lookup"><span data-stu-id="bb37a-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Relacja między pakietu dla twórców, hosty pakietu oraz klientów pakietu](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="bb37a-114">Konta</span><span class="sxs-lookup"><span data-stu-id="bb37a-114">Accounts</span></span>

<span data-ttu-id="bb37a-115">Aby opublikować pakiety w witrynie NuGet.org, należy najpierw utworzyć [konta osoby (użytkownik)](individual-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="bb37a-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="bb37a-116">Staje się on swoją tożsamość w witrynie NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="bb37a-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="bb37a-117">NuGet.org umożliwia również tworzenie [konto organizacji](organizations-on-nuget-org.md).</span><span class="sxs-lookup"><span data-stu-id="bb37a-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="bb37a-118">Konto organizacji ma co najmniej jeden z indywidualnych kont jako elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="bb37a-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="bb37a-119">Zestaw pakietów przy zachowaniu jednej tożsamości dla własności mogą zarządzać elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="bb37a-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="bb37a-120">Za pomocą indywidualnego konta może być członkiem dowolnej liczby organizacji.</span><span class="sxs-lookup"><span data-stu-id="bb37a-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="bb37a-121">Pakiet może należeć do organizacji, takich jak mogą należeć do indywidualnych kont.</span><span class="sxs-lookup"><span data-stu-id="bb37a-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="bb37a-122">Konsumentów pakietu nie jest widoczna różnica między indywidualne konto lub konta organizacji: oba są wyświetlane jako pakiet `owners`.</span><span class="sxs-lookup"><span data-stu-id="bb37a-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="bb37a-123">Klucze interfejsu API</span><span class="sxs-lookup"><span data-stu-id="bb37a-123">API keys</span></span>

<span data-ttu-id="bb37a-124">Po utworzeniu pakietu NuGet ( *.nupkg* plików) do publikowania, opublikujesz go w witrynie NuGet.org, przy użyciu interfejsu wiersza polecenia nuget.exe lub dotnet.exe interfejsu wiersza polecenia, wraz z [klucz interfejsu API](scoped-api-keys.md) uzyskanych z repozytorium NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="bb37a-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="bb37a-125">Gdy użytkownik [publikowanie pakietu](../create-packages/creating-a-package.md), wartość klucza interfejsu API są objęte polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="bb37a-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="bb37a-126">Identyfikator prefiksów</span><span class="sxs-lookup"><span data-stu-id="bb37a-126">ID prefixes</span></span>

<span data-ttu-id="bb37a-127">Podczas publikowania pakietów, możesz zarezerwować i chronić swoją tożsamość za [rezerwowanie prefiksów identyfikator](id-prefix-reservation.md).</span><span class="sxs-lookup"><span data-stu-id="bb37a-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="bb37a-128">Podczas instalowania pakietu, konsumentów pakietu znajdują się dodatkowe informacje, co oznacza, że pakiet, w którym są one używania nie oszukańczym w jego właściwościach identyfikacyjne.</span><span class="sxs-lookup"><span data-stu-id="bb37a-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="bb37a-129">Punkt końcowy interfejsu API dla NuGet.org</span><span class="sxs-lookup"><span data-stu-id="bb37a-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="bb37a-130">Aby użyć NuGet.org jako repozytorium pakietów NuGet klientów, należy użyć następujący punkt końcowy interfejsu API w wersji 3:</span><span class="sxs-lookup"><span data-stu-id="bb37a-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="bb37a-131">Starsi klienci mogą nadal używać protokołu V2 nawiązać NuGet.org. Jednak należy pamiętać, NuGet klientów 3.0 lub nowszej odniesie wolniej, a mniej niezawodnej usługi przy użyciu protokołu V2:</span><span class="sxs-lookup"><span data-stu-id="bb37a-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="bb37a-132">`https://www.nuget.org/api/v2` (**Protokół w wersji 2 jest przestarzała!** )</span><span class="sxs-lookup"><span data-stu-id="bb37a-132">`https://www.nuget.org/api/v2` (**The V2 prototcol is deprecated!**)</span></span>
