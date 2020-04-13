---
title: Żądania danych użytkownika
description: Zasady żądania eksportowania i usuwania danych użytkownika
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427513"
---
# <a name="user-data-requests"></a><span data-ttu-id="9cf0f-103">Żądania danych użytkownika</span><span class="sxs-lookup"><span data-stu-id="9cf0f-103">User Data Requests</span></span>

<span data-ttu-id="9cf0f-104">nuget.org użytkownicy mogą przesyłać żądania usuwania informacji i żądania eksportu informacji za pośrednictwem [nuget.org](https://www.nuget.org). Oba typy są przesyłane w formie żądań pomocy technicznej i są wykonywane przez administratorów nuget.org w ciągu 30 dni.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="9cf0f-105">Następujące dane użytkownika są bezpośrednio dostępne za pośrednictwem nuget.org:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="9cf0f-106">Dane związane z kontem, takie jak adres e-mail, konto logowania, zdjęcie profilowe i ustawienia powiadomień e-mail</span><span class="sxs-lookup"><span data-stu-id="9cf0f-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="9cf0f-107">Posiadane klucze interfejsu API</span><span class="sxs-lookup"><span data-stu-id="9cf0f-107">Owned API Keys</span></span>
* <span data-ttu-id="9cf0f-108">Lista posiadanych pakietów</span><span class="sxs-lookup"><span data-stu-id="9cf0f-108">List of owned packages</span></span>

<span data-ttu-id="9cf0f-109">Te dane nie są uwzględniane w danych eksportowanych za pośrednictwem żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="9cf0f-110">Identyfikowanie danych klientów</span><span class="sxs-lookup"><span data-stu-id="9cf0f-110">Identifying customer data</span></span>

<span data-ttu-id="9cf0f-111">Dane klientów można zidentyfikować jako nuget.org nazwy kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="9cf0f-112">Usuwanie danych klienta</span><span class="sxs-lookup"><span data-stu-id="9cf0f-112">Deleting customer data</span></span>

<span data-ttu-id="9cf0f-113">Aby zażądać usunięcia danych użytkownika z nuget.org:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="9cf0f-114">Użytkownik musi zalogować się do [nuget.org](https://www.nuget.org)</span><span class="sxs-lookup"><span data-stu-id="9cf0f-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="9cf0f-115">Użytkownik musi przesłać żądanie usunięcia swojego konta [nuget.org/account/delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="9cf0f-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="9cf0f-116">Użytkownicy, którzy są jedynymi właścicielami pakietów, są zachęcani do znalezienia nowych właścicieli przed prośbą o usunięcie konta.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="9cf0f-117">Jeśli własność pakietu nie jest przenoszona, pakiet NuGet jest niepubliczny i w rezultacie nie jest już dostępny w kwerendach wyszukiwania w programie Visual Studio lub w nuget.org stronie internetowej.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="9cf0f-118">Przed usunięciem konta administratorzy nuget.org współpracują z użytkownikiem w celu znalezienia nowych właścicieli pakietów, których są właścicielami.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="9cf0f-119">Akcja usuwania konta jest wypełniana przez administratora nuget.org w ciągu 30 dni od daty żądania.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="9cf0f-120">Po usunięciu konta wszystkie dane użytkownika zostaną usunięte z systemu nuget.org i podejmowane są następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="9cf0f-121">Usunięte konto zostanie wyrejestrowane za pomocą nuget.org</span><span class="sxs-lookup"><span data-stu-id="9cf0f-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="9cf0f-122">Wszystkie posiadane klucze interfejsu API są usuwane</span><span class="sxs-lookup"><span data-stu-id="9cf0f-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="9cf0f-123">Wszystkie zarezerwowane przestrzenie nazw są zwalniane</span><span class="sxs-lookup"><span data-stu-id="9cf0f-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="9cf0f-124">Wszelkie własności pakietu są usuwane</span><span class="sxs-lookup"><span data-stu-id="9cf0f-124">Any package ownership are removed</span></span>

<span data-ttu-id="9cf0f-125">Posiadane pakiety *nie* są usuwane.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="9cf0f-126">Mimo że nie są one publikowane w wynikach wyszukiwania, pozostają dostępne za pośrednictwem przywracania pakietu do projektów, które od nich zależą.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="9cf0f-127">Eksportowanie danych klientów</span><span class="sxs-lookup"><span data-stu-id="9cf0f-127">Exporting customer data</span></span>

<span data-ttu-id="9cf0f-128">Po zalogowaniu się do nuget.org użytkownik może przesłać żądanie eksportu za pośrednictwem [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span><span class="sxs-lookup"><span data-stu-id="9cf0f-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="9cf0f-129">Eksportowane dane są udostępniane przez 48 godzin użytkownikowi do pobrania za pośrednictwem obiektu blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="9cf0f-130">Po 48 godzinach dostęp wygasa, a użytkownik musi przesłać nowe żądanie eksportu w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="9cf0f-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="9cf0f-131">Wyeksportowane dane obejmują:</span><span class="sxs-lookup"><span data-stu-id="9cf0f-131">The exported data includes:</span></span>

* <span data-ttu-id="9cf0f-132">Żądania pomocy technicznej użytkownika</span><span class="sxs-lookup"><span data-stu-id="9cf0f-132">The user's support requests</span></span>
* <span data-ttu-id="9cf0f-133">Akcje użytkownika (publikuj pakiet, utwórz konto) w dziennikach inspekcji</span><span class="sxs-lookup"><span data-stu-id="9cf0f-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="9cf0f-134">Wszelkie informacje o użytkowniku, które zostały utrwalone w dziennikach usługi IIS</span><span class="sxs-lookup"><span data-stu-id="9cf0f-134">Any user information as persisted in the IIS logs</span></span>
