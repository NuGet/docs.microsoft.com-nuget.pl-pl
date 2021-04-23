---
title: Omówienie witryny NuGet.org
description: Omówienie witryny NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 2dac6ebd6367f3ed1a5ef9e81d843867a4a22f62
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901879"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="a13a6-103">Omówienie witryny NuGet.org</span><span class="sxs-lookup"><span data-stu-id="a13a6-103">Overview of NuGet.org</span></span>

<span data-ttu-id="a13a6-104">NuGet.org to publiczny host pakietów NuGet, które są codziennie stosowane przez miliony deweloperów .NET i .NET Core.</span><span class="sxs-lookup"><span data-stu-id="a13a6-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="a13a6-105">Rola NuGet.org w ekosystemie NuGet</span><span class="sxs-lookup"><span data-stu-id="a13a6-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="a13a6-106">W swojej roli jako host publiczny NuGet.org obsługuje centralne repozytorium ponad 100 000 unikatowych pakietów w nuget.org [.](https://www.nuget.org) NuGet.org nie jest jedynym możliwym hostem pakietów.</span><span class="sxs-lookup"><span data-stu-id="a13a6-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="a13a6-107">Technologia NuGet umożliwia również hostować pakiety prywatnie w chmurze (na przykład w usłudze Azure DevOps), w sieci prywatnej, a nawet tylko w lokalnym systemie plików.</span><span class="sxs-lookup"><span data-stu-id="a13a6-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="a13a6-108">Jeśli interesuje Cię inny host lub opcja hostingu, zobacz [Hosting your own NuGet feeds (Hostowanie własnych źródeł danych NuGet).](../hosting-packages/overview.md)</span><span class="sxs-lookup"><span data-stu-id="a13a6-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="a13a6-109">NuGet.org, tak jak każdy host pakietów NuGet, służy jako punkt połączenia między twórcami pakietów a *ich* *odbiorcami.*</span><span class="sxs-lookup"><span data-stu-id="a13a6-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="a13a6-110">Twórcy skompilowali przydatne pakiety NuGet i opublikowali je.</span><span class="sxs-lookup"><span data-stu-id="a13a6-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="a13a6-111">Następnie użytkownicy wyszukują przydatne i zgodne pakiety na dostępnych hostach, pobierając i uwzględniając te pakiety w swoich projektach.</span><span class="sxs-lookup"><span data-stu-id="a13a6-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="a13a6-112">Po zainstalowaniu w projekcie interfejsy API pakietów są dostępne dla pozostałej części kodu projektu.</span><span class="sxs-lookup"><span data-stu-id="a13a6-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Relacja między twórcami pakietów, hostami pakietów i konsumentami pakietów](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="a13a6-114">Konta</span><span class="sxs-lookup"><span data-stu-id="a13a6-114">Accounts</span></span>

<span data-ttu-id="a13a6-115">Aby opublikować pakiety NuGet.org, należy najpierw utworzyć [indywidualne konto (użytkownika).](individual-accounts.md)</span><span class="sxs-lookup"><span data-stu-id="a13a6-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="a13a6-116">Stanie się to Twoją tożsamością NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="a13a6-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="a13a6-117">NuGet.org umożliwia również utworzenie konta [organizacji.](organizations-on-nuget-org.md)</span><span class="sxs-lookup"><span data-stu-id="a13a6-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="a13a6-118">Konto organizacji ma co najmniej jedno indywidualne konto jako jego członków.</span><span class="sxs-lookup"><span data-stu-id="a13a6-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="a13a6-119">Członkowie mogą zarządzać zestawem pakietów przy zachowaniu jednej tożsamości na własność.</span><span class="sxs-lookup"><span data-stu-id="a13a6-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="a13a6-120">Za pomocą indywidualnego konta możesz być członkiem dowolnej liczby organizacji.</span><span class="sxs-lookup"><span data-stu-id="a13a6-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="a13a6-121">Pakiet może należeć do konta organizacji, tak jak może należeć do pojedynczego konta.</span><span class="sxs-lookup"><span data-stu-id="a13a6-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="a13a6-122">Odbiorcy pakietów nie widzą żadnej różnicy między indywidualnym kontem a kontem organizacji: oba elementy są wyświetlane jako pakiet `owners` .</span><span class="sxs-lookup"><span data-stu-id="a13a6-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="a13a6-123">Klucze interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a13a6-123">API keys</span></span>

<span data-ttu-id="a13a6-124">Po opublikowaniu pakietu NuGet (pliku *.nupkg)* należy opublikować go w programie NuGet.org przy użyciu interfejsu wiersza polecenia programu nuget.exe lub interfejsu wiersza polecenia programu dotnet.exe, a także klucza interfejsu [API](scoped-api-keys.md) uzyskanego z usługi NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="a13a6-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="a13a6-125">Podczas [publikowania pakietu wartość](../create-packages/creating-a-package.md)klucza interfejsu API jest uwzględniana w poleceniu interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a13a6-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="a13a6-126">Prefiksy identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="a13a6-126">ID prefixes</span></span>

<span data-ttu-id="a13a6-127">Podczas publikowania pakietów można zarezerwować i chronić swoją tożsamość, [rezerwując prefiksy identyfikatorów](id-prefix-reservation.md).</span><span class="sxs-lookup"><span data-stu-id="a13a6-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="a13a6-128">Podczas instalowania pakietu odbiorcy pakietów są dostarczani z dodatkowymi informacjami wskazującymi, że pakiet, z których są oni oni konsumujący, nie jest złudny w jego właściwościach identyfikujących.</span><span class="sxs-lookup"><span data-stu-id="a13a6-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="a13a6-129">Punkt końcowy interfejsu API dla NuGet.org</span><span class="sxs-lookup"><span data-stu-id="a13a6-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="a13a6-130">Aby używać NuGet.org jako repozytorium pakietów z klientami NuGet, należy użyć następującego punktu końcowego interfejsu API w wersji 3:</span><span class="sxs-lookup"><span data-stu-id="a13a6-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="a13a6-131">Starsi klienci mogą nadal używać protokołu V2 w celu osiągnięcia NuGet.org. Należy jednak pamiętać, że klienci NuGet w wersji 3.0 lub nowszej będą mieć wolniejsze i mniej niezawodne usługi korzystające z protokołu V2:</span><span class="sxs-lookup"><span data-stu-id="a13a6-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="a13a6-132">`https://www.nuget.org/api/v2` (Protokół **V2 jest przestarzały!**)</span><span class="sxs-lookup"><span data-stu-id="a13a6-132">`https://www.nuget.org/api/v2` (**The V2 protocol is deprecated!**)</span></span>
