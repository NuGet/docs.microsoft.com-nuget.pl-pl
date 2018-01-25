---
title: "Rozwiązywanie sporów nazwa pakietu NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Proces rozwiązywanie sporów między związane z znakowania, znaków towarowych i innych konfliktów wydawcy pakietu NuGet."
keywords: "Sporów pakietu NuGet, rozwiązywanie sporów NuGet, proces rozpoznawania sporów"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 589fe4e7d2b05f3d589dcc70e78e7199d7e717c8
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="63b02-104">Rozwiązywanie sporów nazwy pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="63b02-104">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="63b02-105">W tym artykule przedstawiono proces zalecane rozwiązanie członkom społeczności, rozwiązywanie sporów z innych wydawców NuGet.</span><span class="sxs-lookup"><span data-stu-id="63b02-105">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="63b02-106">Na przykład załóżmy, że Northwind Traders sprawia, że systemu CRM, dla którego zapewniają sterowników klienta jako MSI do pobrania z witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="63b02-106">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="63b02-107">Irena, niezależnie od dewelopera wymaga ułatwić korzystanie z biblioteki klienta firmy Northwind i konwertuje go na pakietu NuGet o nazwie `NorthwindTraders.Client`.</span><span class="sxs-lookup"><span data-stu-id="63b02-107">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="63b02-108">Później Northwind chce utworzyć oficjalnego pakietu NuGet w swoich własnych ich biblioteki klienta i w związku z tym chcesz rozstrzygania własność firmy Irena nazwę pakietu.</span><span class="sxs-lookup"><span data-stu-id="63b02-108">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="63b02-109">W tym scenariuszu Irena nie wydaje się być działające z zamiarów zły, ale raczej obsługuje narzędzia i klientów firmy Northwind, podając własne czasu i kod.</span><span class="sxs-lookup"><span data-stu-id="63b02-109">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="63b02-110">W tym samym czasie Northwind jest uzasadnione właścicielem nazwy Northwind.</span><span class="sxs-lookup"><span data-stu-id="63b02-110">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="63b02-111">Wykonując z procesem opisanym niżej Northwind i Irena mogą współdziałać ze sobą odpowiedniego rozwiązania, ponieważ zarówno zainteresowani obsługująca społeczności deweloperów.</span><span class="sxs-lookup"><span data-stu-id="63b02-111">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="63b02-112">Zwykle nie jest niezbędna dla zespołu NuGet do angażowania; Współpraca zwykle działa się najlepiej.</span><span class="sxs-lookup"><span data-stu-id="63b02-112">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="63b02-113">W rzeczywistości co sporów zespołu NuGet uwagi do daty została działał bez zespołu konieczności przekazać ocenie.</span><span class="sxs-lookup"><span data-stu-id="63b02-113">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>

## <a name="process"></a><span data-ttu-id="63b02-114">Proces</span><span class="sxs-lookup"><span data-stu-id="63b02-114">Process</span></span>

1. <span data-ttu-id="63b02-115">Skontaktuj się z właściciele pakietu masz sporów przy użyciu **właścicieli skontaktuj się z** łącze na stronie Szczegóły pakietu.</span><span class="sxs-lookup"><span data-stu-id="63b02-115">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="63b02-116">Opis problemu w rodzaju i w sposób bezpośredni.</span><span class="sxs-lookup"><span data-stu-id="63b02-116">Explain your issue in a kind and direct manner.</span></span>
1. <span data-ttu-id="63b02-117">Wyślij kopię wiadomości [ support@nuget.org ](mailto:support@nuget.org) tak, aby NuGet i .NET Foundation wiedzą z sporów.</span><span class="sxs-lookup"><span data-stu-id="63b02-117">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
1. <span data-ttu-id="63b02-118">Poczekaj maksymalnie 30 dni rozwiązanie problemu, a następnie powiadom [ support@nuget.org ](mailto:support@nuget.org) ponownie.</span><span class="sxs-lookup"><span data-stu-id="63b02-118">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="63b02-119">Nuget.org zespołem pomocy technicznej będzie angażowanie i spróbuj pracy za pośrednictwem sporów z obu stron.</span><span class="sxs-lookup"><span data-stu-id="63b02-119">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
