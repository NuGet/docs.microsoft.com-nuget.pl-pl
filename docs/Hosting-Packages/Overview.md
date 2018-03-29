---
title: Omówienie Hosting NuGet własnych źródeł | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Przegląd otwiera do obsługi własnych źródeł danych pakietu NuGet lub galerie lokalnie lub zdalnie.
keywords: NuGet źródła danych, Galeria NuGet pakietu niestandardowego źródła danych, NuGet.Server
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 242404caa12f17ea359a13d574379b34f13f2e40
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="742a8-104">Hosting NuGet własnych źródeł danych</span><span class="sxs-lookup"><span data-stu-id="742a8-104">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="742a8-105">Zamiast wprowadzania publicznie dostępnych pakietów, można zwolnić pakietów się tylko ograniczone odbiorców, takich jak organizacji lub grupy roboczej.</span><span class="sxs-lookup"><span data-stu-id="742a8-105">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="742a8-106">Ponadto niektóre firmy mogą chcieć ograniczyć innych firm, które ma być biblioteki ich deweloperzy mogą przy użyciu, a w związku z tym bezpośrednie tych deweloperzy ma być rysowany od źródła pakietu ograniczone zamiast nuget.org.</span><span class="sxs-lookup"><span data-stu-id="742a8-106">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="742a8-107">W tym celu NuGet obsługuje Konfigurowanie źródła pakietów prywatnych w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="742a8-107">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="742a8-108">Lokalne źródła danych: pakiety są po prostu dotyczącymi odpowiedniego sieciowego udziału plików, najlepiej przy użyciu `nuget init` i `nuget add` tworzenia struktury hierarchicznej folder (NuGet 3.3 +).</span><span class="sxs-lookup"><span data-stu-id="742a8-108">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="742a8-109">Aby uzyskać więcej informacji, zobacz [lokalnych źródeł danych](../hosting-packages/local-feeds.md).</span><span class="sxs-lookup"><span data-stu-id="742a8-109">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="742a8-110">NuGet.Server: Pakiety są udostępniane za pomocą lokalnego serwera HTTP.</span><span class="sxs-lookup"><span data-stu-id="742a8-110">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="742a8-111">Aby uzyskać więcej informacji, zobacz [NuGet.Server](../hosting-packages/nuget-server.md).</span><span class="sxs-lookup"><span data-stu-id="742a8-111">For details, see [NuGet.Server](../hosting-packages/nuget-server.md).</span></span>
- <span data-ttu-id="742a8-112">Galeria NuGet: Pakiety znajdują się na serwerze Internetu za pomocą [projektu galerii NuGet](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (witryną github.com).</span><span class="sxs-lookup"><span data-stu-id="742a8-112">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="742a8-113">Galeria NuGet zawiera Zarządzanie użytkownikami i funkcje, takie jak szeroką gamę interfejsu użytkownika, który umożliwia wyszukiwanie i Przeglądanie pakietów z poziomu przeglądarki, podobnie jak nuget.org sieci web.</span><span class="sxs-lookup"><span data-stu-id="742a8-113">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="742a8-114">Dostępne są również kilka innych NuGet hosting produkty, które obsługują zdalnego prywatnych źródeł danych, takie jak następujące:</span><span class="sxs-lookup"><span data-stu-id="742a8-114">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="742a8-115">[Visual Studio Team Services pakietu zarządzania](https://www.visualstudio.com/docs/package/nuget/publish), która jest również dostępna na Team Foundation Server 2017 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="742a8-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="742a8-116">MyGet</span><span class="sxs-lookup"><span data-stu-id="742a8-116">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="742a8-117">[ProGet](http://inedo.com/proget) z Inedo</span><span class="sxs-lookup"><span data-stu-id="742a8-117">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- <span data-ttu-id="742a8-118">[Serwer NuGet](http://nugetserver.net/), projekt społeczności z Inedo</span><span class="sxs-lookup"><span data-stu-id="742a8-118">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="742a8-119">[Serwer NuGet (otwórz źródłowy)](http://nuget-server.net), podobnie jak w Inedo NuGet serwera implementację open source</span><span class="sxs-lookup"><span data-stu-id="742a8-119">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="742a8-120">[Artifactory](https://www.jfrog.com/artifactory/) z JFrog.</span><span class="sxs-lookup"><span data-stu-id="742a8-120">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="742a8-121">[Węzła](http://www.sonatype.org/nexus/) z Sonatype.</span><span class="sxs-lookup"><span data-stu-id="742a8-121">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="742a8-122">[TeamCity](https://www.jetbrains.com/teamcity/) z JetBrains.</span><span class="sxs-lookup"><span data-stu-id="742a8-122">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="742a8-123">Niezależnie od tego, jak znajdują się pakiety, możesz uzyskać do nich dostęp przez dodanie ich do listy dostępnych źródeł w `NuGet.Config`.</span><span class="sxs-lookup"><span data-stu-id="742a8-123">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="742a8-124">Można to zrobić w programie Visual Studio zgodnie z opisem w [źródła pakietów](../tools/package-manager-ui.md#package-sources), lub z wiersza polecenia przy użyciu [ `nuget sources` ](../tools/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="742a8-124">This can be done in Visual Studio as described in [Package Sources](../tools/package-manager-ui.md#package-sources), or from the command line using [`nuget sources`](../tools/cli-ref-sources.md).</span></span> <span data-ttu-id="742a8-125">Ścieżka do źródła może być nazwą ścieżki lokalnej folderu, Nazwa sieciowa lub adres URL.</span><span class="sxs-lookup"><span data-stu-id="742a8-125">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>
