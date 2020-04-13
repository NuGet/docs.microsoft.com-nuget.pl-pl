---
title: Omówienie witryny NuGet.org
description: Omówienie witryny NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427522"
---
# <a name="overview-of-nugetorg"></a><span data-ttu-id="723c7-103">Omówienie witryny NuGet.org</span><span class="sxs-lookup"><span data-stu-id="723c7-103">Overview of NuGet.org</span></span>

<span data-ttu-id="723c7-104">NuGet.org jest publicznym hostem pakietów NuGet, które są codziennie zatrudniane przez miliony deweloperów platformy .NET i .NET Core.</span><span class="sxs-lookup"><span data-stu-id="723c7-104">NuGet.org is a public host of NuGet packages that are employed by millions of .NET and .NET Core developers every day.</span></span>

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a><span data-ttu-id="723c7-105">Rola NuGet.org w ekosystemie NuGet</span><span class="sxs-lookup"><span data-stu-id="723c7-105">Role of NuGet.org in the NuGet ecosystem</span></span>

<span data-ttu-id="723c7-106">W swojej roli jako gospodarza publicznego, NuGet.org sam utrzymuje centralne repozytorium ponad 100.000 unikalnych pakietów w [nuget.org](https://www.nuget.org). NuGet.org nie jest jedynym możliwym hostem dla pakietów.</span><span class="sxs-lookup"><span data-stu-id="723c7-106">In its role as a public host, NuGet.org itself maintains the central repository of over 100,000 unique packages at [nuget.org](https://www.nuget.org). NuGet.org is not the only possible host for packages.</span></span> <span data-ttu-id="723c7-107">Technologia NuGet umożliwia również hostowania pakietów prywatnie w chmurze (na przykład w usłudze Azure DevOps), w sieci prywatnej, a nawet tylko w lokalnym systemie plików.</span><span class="sxs-lookup"><span data-stu-id="723c7-107">The NuGet technology also enables you to host packages privately in the cloud (such as on Azure DevOps), on a private network, or even on just your local file system.</span></span> <span data-ttu-id="723c7-108">Jeśli jesteś zainteresowany inną opcją hosta lub hostingu, zobacz [Hostowanie własnych kanałów NuGet](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="723c7-108">If you are interested in a different host or hosting option, see [Hosting your own NuGet feeds](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="723c7-109">NuGet.org, podobnie jak każdy host pakietów NuGet, służy jako punkt połączenia między *twórcami pakietów* a *konsumentami pakietów.*</span><span class="sxs-lookup"><span data-stu-id="723c7-109">NuGet.org, like any host for NuGet packages, serves as the point of connection between package *creators* and package *consumers*.</span></span> <span data-ttu-id="723c7-110">Twórcy twórz przydatne pakiety NuGet i publikują je.</span><span class="sxs-lookup"><span data-stu-id="723c7-110">Creators build useful NuGet packages and publish them.</span></span> <span data-ttu-id="723c7-111">Następnie konsumenci wyszukują przydatne i kompatybilne pakiety na dostępnych hostach, pobierając i włączając te pakiety do swoich projektów.</span><span class="sxs-lookup"><span data-stu-id="723c7-111">Consumers then search for useful and compatible packages on accessible hosts, downloading and including those packages in their projects.</span></span> <span data-ttu-id="723c7-112">Po zainstalowaniu w projekcie interfejsy API pakietów są dostępne dla pozostałej części kodu projektu.</span><span class="sxs-lookup"><span data-stu-id="723c7-112">Once installed in a project, the packages' APIs are available to the rest of the project code.</span></span>

![Relacje między twórcami pakietów, hostami pakietów i odbiorcami pakietów](media/nuget-roles.png)

## <a name="accounts"></a><span data-ttu-id="723c7-114">Konta</span><span class="sxs-lookup"><span data-stu-id="723c7-114">Accounts</span></span>

<span data-ttu-id="723c7-115">Aby opublikować pakiety na NuGet.org, należy najpierw utworzyć [indywidualne konto (użytkownika).](individual-accounts.md)</span><span class="sxs-lookup"><span data-stu-id="723c7-115">To publish packages on NuGet.org, you first create an [individual (user) account](individual-accounts.md).</span></span> <span data-ttu-id="723c7-116">To staje się twoją tożsamością na NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="723c7-116">This becomes your identity on NuGet.org.</span></span>

<span data-ttu-id="723c7-117">NuGet.org umożliwia również utworzenie konta [organizacji](organizations-on-nuget-org.md).</span><span class="sxs-lookup"><span data-stu-id="723c7-117">NuGet.org also allows you to create an [organization account](organizations-on-nuget-org.md).</span></span> <span data-ttu-id="723c7-118">Konto organizacji ma co najmniej jedno konto pojedyncze jako jej członkowie.</span><span class="sxs-lookup"><span data-stu-id="723c7-118">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="723c7-119">Członkowie mogą zarządzać zestawem pakietów przy zachowaniu jednej tożsamości dla własności.</span><span class="sxs-lookup"><span data-stu-id="723c7-119">Members can manage a set of packages while maintaining a single identity for ownership.</span></span> <span data-ttu-id="723c7-120">Za pośrednictwem indywidualnego konta możesz być członkiem dowolnej liczby organizacji.</span><span class="sxs-lookup"><span data-stu-id="723c7-120">Through your individual account, you can be a member of any number of organizations.</span></span>

<span data-ttu-id="723c7-121">Pakiet może należeć do konta organizacji, tak jak może należeć do indywidualnego konta.</span><span class="sxs-lookup"><span data-stu-id="723c7-121">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="723c7-122">Konsumenci pakietów nie widzą żadnej różnicy między kontem indywidualnym `owners`lub kontem organizacji: oba są wyświetlane jako pakiet.</span><span class="sxs-lookup"><span data-stu-id="723c7-122">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="api-keys"></a><span data-ttu-id="723c7-123">Klucze interfejsu API</span><span class="sxs-lookup"><span data-stu-id="723c7-123">API keys</span></span>

<span data-ttu-id="723c7-124">Po opublikowaniu pakietu NuGet *(.nupkg* file) publikujesz go w NuGet.org przy użyciu interfejsu wiersza polecenia nuget.exe lub interfejsu wiersza polecenia dotnet.exe wraz z [kluczem interfejsu API](scoped-api-keys.md) uzyskanym z NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="723c7-124">Once you have a NuGet package (*.nupkg* file) to publish, you publish it to NuGet.org using either the nuget.exe CLI or the dotnet.exe CLI, along with an [API key](scoped-api-keys.md) acquired from NuGet.org.</span></span>

<span data-ttu-id="723c7-125">Podczas [publikowania pakietu](../create-packages/creating-a-package.md)należy dołączyć wartość klucza interfejsu API do polecenia CLI.</span><span class="sxs-lookup"><span data-stu-id="723c7-125">When you [publish a package](../create-packages/creating-a-package.md), you include the API key value in the CLI command.</span></span>

## <a name="id-prefixes"></a><span data-ttu-id="723c7-126">Prefiksy identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="723c7-126">ID prefixes</span></span>

<span data-ttu-id="723c7-127">Publikując pakiety, możesz zarezerwować i chronić swoją tożsamość, [rezerwując prefiksy identyfikatorów](id-prefix-reservation.md).</span><span class="sxs-lookup"><span data-stu-id="723c7-127">When you publish packages, you can reserve and protect your identity by [reserving ID prefixes](id-prefix-reservation.md).</span></span> <span data-ttu-id="723c7-128">Podczas instalowania pakietu, konsumenci pakietów są dostarczane z dodatkowymi informacjami wskazującymi, że pakiet, który zużywają nie jest zwodnicze w jego właściwości identyfikujące.</span><span class="sxs-lookup"><span data-stu-id="723c7-128">When installing a package, package consumers are provided with additional information indicating that the package they are consuming is not deceptive in its identifying properties.</span></span>

## <a name="api-endpoint-for-nugetorg"></a><span data-ttu-id="723c7-129">Punkt końcowy interfejsu API dla NuGet.org</span><span class="sxs-lookup"><span data-stu-id="723c7-129">API endpoint for NuGet.org</span></span>

<span data-ttu-id="723c7-130">Aby użyć NuGet.org jako repozytorium pakietów z klientami NuGet, należy użyć następującego punktu końcowego interfejsu API systemu V3:</span><span class="sxs-lookup"><span data-stu-id="723c7-130">To use NuGet.org as a package repository with NuGet clients, you should use the following V3 API endpoint:</span></span> 

`https://api.nuget.org/v3/index.json`

<span data-ttu-id="723c7-131">Starsi klienci mogą nadal używać protokołu V2, aby dotrzeć do NuGet.org. Należy jednak pamiętać, że klienci NuGet 3.0 lub nowsi będą mieli wolniejszą i mniej niezawodną usługę przy użyciu protokołu V2:</span><span class="sxs-lookup"><span data-stu-id="723c7-131">Older clients can still use the V2 protocol to reach NuGet.org. However, please note, NuGet clients 3.0 or later will have slower and less reliable service using the V2 protocol:</span></span>

<span data-ttu-id="723c7-132">`https://www.nuget.org/api/v2`**(V2 prototcol jest przestarzały!**)</span><span class="sxs-lookup"><span data-stu-id="723c7-132">`https://www.nuget.org/api/v2` (**The V2 prototcol is deprecated!**)</span></span>
