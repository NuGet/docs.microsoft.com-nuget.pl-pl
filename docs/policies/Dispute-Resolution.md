---
title: Rozwiązywanie sporów nazwa pakietu NuGet
description: Proces rozwiązywanie sporów między związane z znakowania, znaków towarowych i innych konfliktów wydawcy pakietu NuGet.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: f7749dec0726162f122db91397e9581cfad23890
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817548"
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="382c3-103">Rozwiązywanie sporów nazwy pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="382c3-103">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="382c3-104">W tym artykule przedstawiono proces zalecane rozwiązanie członkom społeczności, rozwiązywanie sporów z innych wydawców NuGet.</span><span class="sxs-lookup"><span data-stu-id="382c3-104">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="382c3-105">Na przykład załóżmy, że Northwind Traders sprawia, że systemu CRM, dla którego zapewniają sterowników klienta jako MSI do pobrania z witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="382c3-105">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="382c3-106">Irena, niezależnie od dewelopera wymaga ułatwić korzystanie z biblioteki klienta firmy Northwind i konwertuje go na pakietu NuGet o nazwie `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="382c3-106">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="382c3-107">Później Northwind chce utworzyć oficjalnego pakietu NuGet w swoich własnych ich biblioteki klienta i w związku z tym chcesz rozstrzygania własność firmy Irena nazwę pakietu.</span><span class="sxs-lookup"><span data-stu-id="382c3-107">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="382c3-108">W tym scenariuszu Irena nie wydaje się być działające z zamiarów zły, ale raczej obsługuje narzędzia i klientów firmy Northwind, podając własne czasu i kod.</span><span class="sxs-lookup"><span data-stu-id="382c3-108">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="382c3-109">W tym samym czasie Northwind jest uzasadnione właścicielem nazwy Northwind.</span><span class="sxs-lookup"><span data-stu-id="382c3-109">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="382c3-110">Wykonując z procesem opisanym niżej Northwind i Irena mogą współdziałać ze sobą odpowiedniego rozwiązania, ponieważ zarówno zainteresowani obsługująca społeczności deweloperów.</span><span class="sxs-lookup"><span data-stu-id="382c3-110">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="382c3-111">Zwykle nie jest niezbędna dla zespołu NuGet do angażowania; Współpraca zwykle działa się najlepiej.</span><span class="sxs-lookup"><span data-stu-id="382c3-111">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="382c3-112">W rzeczywistości co sporów zespołu NuGet uwagi do daty została działał bez zespołu konieczności przekazać ocenie.</span><span class="sxs-lookup"><span data-stu-id="382c3-112">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>

## <a name="process"></a><span data-ttu-id="382c3-113">Proces</span><span class="sxs-lookup"><span data-stu-id="382c3-113">Process</span></span>

1. <span data-ttu-id="382c3-114">Skontaktuj się z właściciele pakietu masz sporów przy użyciu **właścicieli skontaktuj się z** łącze na stronie Szczegóły pakietu.</span><span class="sxs-lookup"><span data-stu-id="382c3-114">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="382c3-115">Opis problemu w rodzaju i w sposób bezpośredni.</span><span class="sxs-lookup"><span data-stu-id="382c3-115">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="382c3-116">Wyślij kopię wiadomości [ support@nuget.org ](mailto:support@nuget.org) tak, aby NuGet i .NET Foundation wiedzą z sporów.</span><span class="sxs-lookup"><span data-stu-id="382c3-116">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="382c3-117">Poczekaj maksymalnie 30 dni rozwiązanie problemu, a następnie powiadom [ support@nuget.org ](mailto:support@nuget.org) ponownie.</span><span class="sxs-lookup"><span data-stu-id="382c3-117">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="382c3-118">Nuget.org zespołem pomocy technicznej będzie angażowanie i spróbuj pracy za pośrednictwem sporów z obu stron.</span><span class="sxs-lookup"><span data-stu-id="382c3-118">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
