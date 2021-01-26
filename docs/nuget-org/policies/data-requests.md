---
title: Żądania danych użytkownika
description: Zasady żądania eksportu i usuwania danych użytkownika
author: JonDouglas
ms.author: jodou
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: e0ec429469a992c9558d1635890fd568398206a1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775728"
---
# <a name="user-data-requests"></a><span data-ttu-id="8b242-103">Żądania danych użytkownika</span><span class="sxs-lookup"><span data-stu-id="8b242-103">User Data Requests</span></span>

<span data-ttu-id="8b242-104">nuget.org użytkownicy mogą przesyłać żądania usunięcia informacji oraz żądania eksportu informacji za poorednictwem [NuGet.org](https://www.nuget.org). Oba typy są przesyłane w formie żądań pomocy technicznej i są wykonywane przez administratorów nuget.org w ciągu 30 dni.</span><span class="sxs-lookup"><span data-stu-id="8b242-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="8b242-105">Następujące dane użytkownika są bezpośrednio dostępne za pomocą nuget.org:</span><span class="sxs-lookup"><span data-stu-id="8b242-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="8b242-106">Dane dotyczące konta, takie jak adres e-mail, konto logowania, obraz profilu i ustawienia powiadomień e-mail</span><span class="sxs-lookup"><span data-stu-id="8b242-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="8b242-107">Posiadane klucze interfejsu API</span><span class="sxs-lookup"><span data-stu-id="8b242-107">Owned API Keys</span></span>
* <span data-ttu-id="8b242-108">Lista posiadanych pakietów</span><span class="sxs-lookup"><span data-stu-id="8b242-108">List of owned packages</span></span>

<span data-ttu-id="8b242-109">Te dane nie są uwzględniane w danych wyeksportowanych przez żądanie obsługi.</span><span class="sxs-lookup"><span data-stu-id="8b242-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="8b242-110">Identyfikowanie danych klienta</span><span class="sxs-lookup"><span data-stu-id="8b242-110">Identifying customer data</span></span>

<span data-ttu-id="8b242-111">Dane klienta można zidentyfikować jako nazwy kont użytkowników nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8b242-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="8b242-112">Usuwanie danych klienta</span><span class="sxs-lookup"><span data-stu-id="8b242-112">Deleting customer data</span></span>

<span data-ttu-id="8b242-113">Aby zażądać usunięcia danych użytkownika z nuget.org:</span><span class="sxs-lookup"><span data-stu-id="8b242-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="8b242-114">Użytkownik musi zalogować się do [NuGet.org](https://www.nuget.org)</span><span class="sxs-lookup"><span data-stu-id="8b242-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="8b242-115">Użytkownik musi przesłać żądanie usunięcia konta [NuGet.org/Account/Delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="8b242-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="8b242-116">Użytkownicy, którzy są jedynymi właścicielami pakietów, są zachęcani do znajdowania nowych właścicieli przed zapytaniem, czy konto zostało usunięte.</span><span class="sxs-lookup"><span data-stu-id="8b242-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="8b242-117">Jeśli własność pakietu nie zostanie przetransferowana, pakiet NuGet nie zostanie wystawiony i w związku z tym nie jest już dostępny w zapytaniach wyszukiwania w programie Visual Studio ani w witrynie sieci Web nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8b242-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="8b242-118">Przed usunięciem konta Administratorzy nuget.org współpracują z użytkownikiem, aby znaleźć nowych właścicieli dla pakietów, których są właścicielami.</span><span class="sxs-lookup"><span data-stu-id="8b242-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="8b242-119">Akcja usuwania konta jest wykonywana przez administratora nuget.org w ciągu 30 dni od daty żądania.</span><span class="sxs-lookup"><span data-stu-id="8b242-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="8b242-120">Po usunięciu konta wszystkie dane użytkownika są usuwane z systemu nuget.org i są wykonywane następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="8b242-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="8b242-121">Usunięte konto zostanie wyrejestrowane z nuget.org</span><span class="sxs-lookup"><span data-stu-id="8b242-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="8b242-122">Wszystkie należące do siebie klucze interfejsu API są usuwane</span><span class="sxs-lookup"><span data-stu-id="8b242-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="8b242-123">Wszystkie zastrzeżone przestrzenie nazw są wydane</span><span class="sxs-lookup"><span data-stu-id="8b242-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="8b242-124">Wszystkie prawa własności pakietu są usuwane</span><span class="sxs-lookup"><span data-stu-id="8b242-124">Any package ownership are removed</span></span>

<span data-ttu-id="8b242-125">Należące do nich pakiety *nie* są usuwane.</span><span class="sxs-lookup"><span data-stu-id="8b242-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="8b242-126">Mimo że nie są one wystawione na podstawie wyników wyszukiwania, są one dostępne za pośrednictwem przywracania pakietów do projektów, które są od nich zależne.</span><span class="sxs-lookup"><span data-stu-id="8b242-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="8b242-127">Eksportowanie danych klienta</span><span class="sxs-lookup"><span data-stu-id="8b242-127">Exporting customer data</span></span>

<span data-ttu-id="8b242-128">Po zalogowaniu się do nuget.org użytkownik może przesłać żądanie eksportu za pomocą [NuGet.org/policies/Contact](https://www.nuget.org/policies/Contact)</span><span class="sxs-lookup"><span data-stu-id="8b242-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="8b242-129">Dane eksportowane są udostępniane przez 48 godzin do użytkownika w celu pobrania przez obiekt blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8b242-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="8b242-130">Po 48 godzinach dostępu wygasa i użytkownik musi przesłać nowe żądanie eksportu zgodnie z wymaganiami.</span><span class="sxs-lookup"><span data-stu-id="8b242-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="8b242-131">Eksportowane dane obejmują:</span><span class="sxs-lookup"><span data-stu-id="8b242-131">The exported data includes:</span></span>

* <span data-ttu-id="8b242-132">Żądania obsługi użytkownika</span><span class="sxs-lookup"><span data-stu-id="8b242-132">The user's support requests</span></span>
* <span data-ttu-id="8b242-133">Akcje użytkownika (publikowanie pakietu, tworzenie konta) jako utrwalone w dziennikach inspekcji</span><span class="sxs-lookup"><span data-stu-id="8b242-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="8b242-134">Wszelkie informacje o użytkowniku jako utrwalone w dziennikach usług IIS</span><span class="sxs-lookup"><span data-stu-id="8b242-134">Any user information as persisted in the IIS logs</span></span>
