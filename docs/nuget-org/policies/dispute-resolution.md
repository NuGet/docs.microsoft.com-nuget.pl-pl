---
title: Nazwa pakietu NuGet rozstrzyganie sporu
description: Proces rozwiązywania sporów między wydawcami pakietów NuGet związanymi z marką, znakami towarowymi i innymi sytuacjami związanymi z konfliktem.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: d9ed7de95a1f38ea2c288b28958519b1dff0e595
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775661"
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="a1cde-103">Rozwiązywanie sporów dotyczących nazw pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="a1cde-103">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="a1cde-104">Ten artykuł zawiera zalecany proces rozwiązywania problemów z członkami społeczności w celu rozwiązywania sporów z innymi wydawcami programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="a1cde-104">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="a1cde-105">Załóżmy na przykład, że firma Northwind Traders tworzy system CRM, dla którego udostępnia sterowniki klientów jako plik MSI do pobrania z witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a1cde-105">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="a1cde-106">W firmie Nancy niezależny deweloper chce ułatwić korzystanie z biblioteki klienta Northwind i przekształcić ją w pakiet NuGet o nazwie `NorthwindTraders.Client` .</span><span class="sxs-lookup"><span data-stu-id="a1cde-106">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="a1cde-107">Później firma Northwind chce utworzyć urzędowy pakiet NuGet własny dla swojej biblioteki klienckiej, a tym samym zachodzić na spór Nancy na własność nazwy pakietu.</span><span class="sxs-lookup"><span data-stu-id="a1cde-107">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="a1cde-108">W tym scenariuszu Nancy nie działa z nieprawidłowymi intencjami, ale raczej obsługuje narzędzia i klientów Northwind, tworząc własny czas i kod.</span><span class="sxs-lookup"><span data-stu-id="a1cde-108">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="a1cde-109">W tym samym czasie Northwind jest uprawnionym właścicielem nazwy Northwind.</span><span class="sxs-lookup"><span data-stu-id="a1cde-109">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="a1cde-110">Postępując zgodnie z poniższym procesem, Northwind i Nancy mogą współdziałać z odpowiednimi rozwiązaniami, ponieważ obie osoby chcą obsługiwać społeczność deweloperów.</span><span class="sxs-lookup"><span data-stu-id="a1cde-110">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="a1cde-111">Zwykle nie jest to konieczne, aby zespół NuGet stał się zainteresowany; Współpraca zwykle działa najlepiej.</span><span class="sxs-lookup"><span data-stu-id="a1cde-111">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span>

## <a name="process"></a><span data-ttu-id="a1cde-112">Proces</span><span class="sxs-lookup"><span data-stu-id="a1cde-112">Process</span></span>

1. <span data-ttu-id="a1cde-113">Skontaktuj się z właścicielami pakietu, korzystając z linku **skontaktuj się z właścicielem** na stronie Szczegóły pakietu.</span><span class="sxs-lookup"><span data-stu-id="a1cde-113">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="a1cde-114">Wyjaśnij swój problem w rodzaju i bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="a1cde-114">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="a1cde-115">Wyślij kopię wiadomości w [support@nuget.org](mailto:support@nuget.org) taki sposób, aby NuGet i .NET Foundation były świadome sporu.</span><span class="sxs-lookup"><span data-stu-id="a1cde-115">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="a1cde-116">Poczekaj maksymalnie 30 dni na rozwiązanie, a następnie Powiadom [support@nuget.org](mailto:support@nuget.org) ponownie.</span><span class="sxs-lookup"><span data-stu-id="a1cde-116">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="a1cde-117">Zespół pomocy technicznej nuget.org będzie uczestniczyć w pracy, a następnie spróbuje przeprowadzić Cię przez spór z obiema stronami.</span><span class="sxs-lookup"><span data-stu-id="a1cde-117">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
