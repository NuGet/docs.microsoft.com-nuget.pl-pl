---
title: Usuwanie pakietów NuGet z repozytorium nuget.org
description: Zasady dotyczące unlisting pakiety z witryny nuget.org; trwałego usunięcia nie jest obsługiwane z wyjątkiem na pakiety naruszyć innych zasad.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 901eb09711a6e32740c70829028da66b782870a0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548131"
---
# <a name="deleting-packages"></a><span data-ttu-id="2daeb-103">Usuwanie pakietów</span><span class="sxs-lookup"><span data-stu-id="2daeb-103">Deleting packages</span></span>

<span data-ttu-id="2daeb-104">nuget.org nie obsługuje trwałe usuwanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="2daeb-104">nuget.org does not support permanent deletion of packages.</span></span> <span data-ttu-id="2daeb-105">To spowoduje przerwanie każdego projektu, w zależności od dostępności pakietu, szczególnie w przypadku przepływów pracy kompilacji, które obejmują Przywracanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="2daeb-105">Doing so would break every project depending on the availability of the package, especially with build workflows that involve package restore.</span></span>

<span data-ttu-id="2daeb-106">nuget.org jest obsługuje *unlisting* pakietu, co można zrobić na stronie pakiet zarządzania, w witrynie sieci web.</span><span class="sxs-lookup"><span data-stu-id="2daeb-106">nuget.org does supports *unlisting* a package, which can be done in the package management page on the web site.</span></span> <span data-ttu-id="2daeb-107">Nieznajdujące się na liście pakietów nie są wyświetlane w witrynie nuget.org, lub w interfejsie użytkownika programu Visual Studio i nie są wyświetlane w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2daeb-107">Unlisted packages don't appear on nuget.org or in the Visual Studio UI, and do not appear in search results.</span></span> <span data-ttu-id="2daeb-108">Nieznajdujące się na liście pakietów, jednak nadal można pobrać i zainstalować za pomocą numeru wersji dokładnie, która obsługuje Przywracanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="2daeb-108">Unlisted packages, however, can still be downloaded and installed by using an exact version number, which supports package restore.</span></span> <span data-ttu-id="2daeb-109">Ponadto nieznajdujące się na liście pakietów, może nadal odnalezionych w następujących scenariuszach określonych:</span><span class="sxs-lookup"><span data-stu-id="2daeb-109">In addition, unlisted packages may still be discovered in the following specific scenarios:</span></span>

- <span data-ttu-id="2daeb-110">Pakiet przywracania przy użyciu wersji zmiennoprzecinkowego (na przykład `1.0.0-*`), gdy najnowszy pakiet dopasowania ograniczenia wersji lub zależności jest pakietu nieznajdujące się na liście.</span><span class="sxs-lookup"><span data-stu-id="2daeb-110">Package restore using floating versions (for example, `1.0.0-*`), if the latest available package matching the version or dependency constraints is an unlisted package.</span></span>
- <span data-ttu-id="2daeb-111">Replikacja pakietów w wykazie (jak katalog zawiera również nieznajdujące się na liście pakietów).</span><span class="sxs-lookup"><span data-stu-id="2daeb-111">Replication of packages through the catalog (as the catalog also contains unlisted packages).</span></span>

## <a name="exceptions"></a><span data-ttu-id="2daeb-112">Wyjątki</span><span class="sxs-lookup"><span data-stu-id="2daeb-112">Exceptions</span></span>

<span data-ttu-id="2daeb-113">W sytuacjach wyjątkowych, takich jak naruszenie praw autorskich i potencjalnie niebezpieczną zawartość pakietów można je usunąć ręcznie przez zespół programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="2daeb-113">In exceptional situations such as copyright infringement and potentially harmful content, packages can be deleted manually by the NuGet team.</span></span> <span data-ttu-id="2daeb-114">Prześlij żądanie pomocy technicznej za pośrednictwem [galerii pakietów NuGet](http://www.nuget.org) do rozpoczęcia procesu.</span><span class="sxs-lookup"><span data-stu-id="2daeb-114">Submit a support request through [NuGet Gallery](http://www.nuget.org) to start the process.</span></span>

## <a name="prohibited-use"></a><span data-ttu-id="2daeb-115">Zabronione korzystanie</span><span class="sxs-lookup"><span data-stu-id="2daeb-115">Prohibited use</span></span>

<span data-ttu-id="2daeb-116">Pakiety, które spełniają dowolne z poniższych kryteriów nie są dozwolone w publicznej galerii pakietów NuGet i zostaną natychmiast usunięte bez dyskusji.</span><span class="sxs-lookup"><span data-stu-id="2daeb-116">Packages that meet any of the following criteria are not allowed on the public NuGet gallery and will be immediately removed without discussion.</span></span> <span data-ttu-id="2daeb-117">Jednak pakietu będą właścicielami, otrzymywać powiadomienia o usunięciu.</span><span class="sxs-lookup"><span data-stu-id="2daeb-117">Package owners will, however, be notified of the removal.</span></span>

- <span data-ttu-id="2daeb-118">Zawiera złośliwego oprogramowania, oprogramowaniem reklamowym lub dowolnych programów szpiegujących.</span><span class="sxs-lookup"><span data-stu-id="2daeb-118">Contains malware, adware, or any kind of spyware.</span></span>
- <span data-ttu-id="2daeb-119">Są przeznaczone do negatywnie wpłynąć na stacji roboczej dewelopera lub jego organizację.</span><span class="sxs-lookup"><span data-stu-id="2daeb-119">Are designed to harm a developer's workstation or their organization.</span></span>
- <span data-ttu-id="2daeb-120">Narusza prawa autorskie lub narusza licencji.</span><span class="sxs-lookup"><span data-stu-id="2daeb-120">Infringes copyrights or violates licenses.</span></span>
- <span data-ttu-id="2daeb-121">Zawartość jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="2daeb-121">Contains illegal content.</span></span>
- <span data-ttu-id="2daeb-122">Są używane do squat dotyczące identyfikatorów pakietu, w tym pakietów, które ma zero produktywność zawartości.</span><span class="sxs-lookup"><span data-stu-id="2daeb-122">Are being used to squat on package identifiers, including packages that have zero productive content.</span></span> <span data-ttu-id="2daeb-123">Pakiety mogą zawierać kod lub właściciele należy przyznać identyfikator do osoby, która faktycznie zawiera produktu do wysłania.</span><span class="sxs-lookup"><span data-stu-id="2daeb-123">Packages must contain code or the owners must concede the identifier to someone who actually has a product to ship.</span></span>
- <span data-ttu-id="2daeb-124">Spróbuj spowodować galerii, zadania, które nie zostały jawnie ustalono, aby zrobić.</span><span class="sxs-lookup"><span data-stu-id="2daeb-124">Attempt to make the gallery do something that it's not explicitly designed to do.</span></span>

<span data-ttu-id="2daeb-125">Jeśli znajdziesz pakietu, który narusza dowolnego z tych elementów, kliknij przycisk **Zgłoś nadużycie** łącze na stronie szczegółów pakietu i przesłać raport.</span><span class="sxs-lookup"><span data-stu-id="2daeb-125">If you find a package that is in violation of any of these items, click the **Report Abuse** link on the package details page and submit a report.</span></span>

<span data-ttu-id="2daeb-126">Należy pamiętać, że zespół NuGet i .NET Foundation zastrzega sobie prawo w dowolnym momencie zmienić te kryteria.</span><span class="sxs-lookup"><span data-stu-id="2daeb-126">Note that the NuGet team and the .NET Foundation reserves the right to change these criteria at any time.</span></span>
