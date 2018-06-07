---
title: Usunięcie pakietów NuGet z nuget.org
description: Zasady unlisting pakietów z nuget.org; trwałe usuwanie nie jest obsługiwany z wyjątkiem na pakiety narusza inne zasady.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 84a27c16968fa55ff1929db1adf98b8242a64fcf
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816995"
---
# <a name="deleting-packages"></a><span data-ttu-id="2225b-103">Usunięcie pakietów</span><span class="sxs-lookup"><span data-stu-id="2225b-103">Deleting packages</span></span>

<span data-ttu-id="2225b-104">nuget.org nie obsługuje trwałe usuwanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="2225b-104">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="2225b-105">W ten sposób spowoduje przerwanie każdy projekt w zależności od dostępności pakietu, szczególnie w przypadku przepływów pracy kompilacji, które obejmują Przywracanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="2225b-105">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="2225b-106">obsługuje jest nuget.org *unlisting* pakietu, można to zrobić na stronie pakiet zarządzania w witrynie sieci web.</span><span class="sxs-lookup"><span data-stu-id="2225b-106">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="2225b-107">Nieznajdujące się na liście pakietów nie są wyświetlane na nuget.org lub w interfejsie użytkownika programu Visual Studio i nie są wyświetlane w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2225b-107">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="2225b-108">Nieznajdujące się na liście pakietów, jednak nadal można pobrać i zainstalować przy użyciu numeru dokładnej wersji, która obsługuje Przywracanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="2225b-108">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="2225b-109">Ponadto nieznajdujące się na liście pakietów nadal są wykrywane w następujących scenariuszach określonych:</span><span class="sxs-lookup"><span data-stu-id="2225b-109">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="2225b-110">Przywracanie przestawne wersji pakietów (na przykład `1.0.0-*`), jeśli jest to najnowsza wersja pakietu dostępne dopasowania ograniczenia wersji lub zależności to pakiet nieznajdujące się na liście.</span><span class="sxs-lookup"><span data-stu-id="2225b-110">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="2225b-111">Replikacja pakietów za pomocą wykazu (zgodnie z katalogu zawiera również nieznajdujące się na liście pakietów).</span><span class="sxs-lookup"><span data-stu-id="2225b-111">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="2225b-112">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="2225b-112">Exceptions</span></span>

<span data-ttu-id="2225b-113">W sytuacjach wyjątkowych, takich jak praw autorskich i potencjalnie niebezpieczną zawartość pakiety mogą zostać usunięte ręcznie przez zespół NuGet.</span><span class="sxs-lookup"><span data-stu-id="2225b-113">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="2225b-114">Prześlij żądanie pomocy technicznej za pośrednictwem [galerii NuGet](http://www.nuget.org) do rozpoczęcia procesu.</span><span class="sxs-lookup"><span data-stu-id="2225b-114">Submit a support request through [NuGet Gallery](http://www.nuget.org) to start the process.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="2225b-115">Zabronione użycie</span><span class="sxs-lookup"><span data-stu-id="2225b-115">Prohibited use</span></span>

<span data-ttu-id="2225b-116">Pakiety, które jest spełnienie któregoś z następujących kryteriów nie są dozwolone w publicznej galerii NuGet i zostaną natychmiast usunięte bez dyskusji.</span><span class="sxs-lookup"><span data-stu-id="2225b-116">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="2225b-117">Jednak pakiet zostanie właścicieli, otrzymywać powiadomienia o usunięciu.</span><span class="sxs-lookup"><span data-stu-id="2225b-117">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="2225b-118">Zawiera złośliwego oprogramowania, programów z reklamami lub dowolnego rodzaju programów szpiegujących.</span><span class="sxs-lookup"><span data-stu-id="2225b-118">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="2225b-119">Mają na celu negatywnie wpłynąć na stacji roboczej dewelopera lub organizacji.</span><span class="sxs-lookup"><span data-stu-id="2225b-119">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="2225b-120">Narusza prawa autorskie lub narusza licencji.</span><span class="sxs-lookup"><span data-stu-id="2225b-120">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="2225b-121">Zawartość niedozwolona.</span><span class="sxs-lookup"><span data-stu-id="2225b-121">Contains illegal content.</span></span>
- <span data-ttu-id="2225b-122">Są używane do squat na identyfikatorach pakietu, w tym pakietów, które ma zerowy produktywności zawartości.</span><span class="sxs-lookup"><span data-stu-id="2225b-122">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="2225b-123">Pakiety musi zawierać kod lub właściciele należy przyznać identyfikator do osoby, która faktycznie zawiera produktu do wysłania.</span><span class="sxs-lookup"><span data-stu-id="2225b-123">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="2225b-124">Próba utworzenia czymś, które nie są jawnie zostało zaprojektowane do galerii.</span><span class="sxs-lookup"><span data-stu-id="2225b-124">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="2225b-125">Jeśli pakiet, który narusza te elementy, kliknij przycisk **zgłaszania nadużyć** łącze na stronie szczegółów pakietu i przesłać raportu.</span><span class="sxs-lookup"><span data-stu-id="2225b-125">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="2225b-126">Należy pamiętać, że zespół NuGet i .NET Foundation zastrzega sobie prawo w dowolnym momencie zmienić te kryteria.</span><span class="sxs-lookup"><span data-stu-id="2225b-126">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
