---
title: Żądania danych użytkownika
description: Zasady dla żądania eksportu danych użytkownika i delete
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: 595a47da59c9b2672a10fc0f19e528c36a790134
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.contentlocale: pl-PL
ms.lasthandoff: 05/04/2018
---
# <a name="user-data-requests"></a><span data-ttu-id="1d1f4-103">Żądania danych użytkownika</span><span class="sxs-lookup"><span data-stu-id="1d1f4-103">User Data Requests</span></span>

<span data-ttu-id="1d1f4-104">nuget.org użytkownicy mogą przesyłać żądania usunięcia informacji i żądań eksportu informacji za pośrednictwem [nuget.org](https://www.nuget.org). Oba typy są przesyłane w formie obsługę żądań i są wykonywane przez administratorów nuget.org w ciągu 30 dni.</span><span class="sxs-lookup"><span data-stu-id="1d1f4-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="1d1f4-105">Następujące dane użytkownika jest bezpośrednio dostępny za pośrednictwem nuget.org:</span><span class="sxs-lookup"><span data-stu-id="1d1f4-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="1d1f4-106">Dane, takie jak adres e-mail, konto logowania obraz profilu i ustawień powiadomień e-mail związanych z kontem</span><span class="sxs-lookup"><span data-stu-id="1d1f4-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="1d1f4-107">Klucze należących do interfejsu API</span><span class="sxs-lookup"><span data-stu-id="1d1f4-107">Owned API Keys</span></span>
* <span data-ttu-id="1d1f4-108">Lista pakietów należące do firmy</span><span class="sxs-lookup"><span data-stu-id="1d1f4-108">List of owned packages</span></span>

<span data-ttu-id="1d1f4-109">Te dane nie jest uwzględniony w dane wyeksportowane za pomocą żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="1d1f4-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="1d1f4-110">Identyfikowanie danych klienta</span><span class="sxs-lookup"><span data-stu-id="1d1f4-110">Identifying customer data</span></span>

<span data-ttu-id="1d1f4-111">Dane klienta może być zidentyfikowany jako nazwy kont użytkowników nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1d1f4-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="1d1f4-112">Usuwanie danych klienta</span><span class="sxs-lookup"><span data-stu-id="1d1f4-112">Deleting customer data</span></span>

<span data-ttu-id="1d1f4-113">Żądanie usuwania danych użytkownika z nuget.org:</span><span class="sxs-lookup"><span data-stu-id="1d1f4-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="1d1f4-114">Użytkownik musi zalogować się do [nuget.org](https://www.nuget.org)</span><span class="sxs-lookup"><span data-stu-id="1d1f4-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="1d1f4-115">Użytkownik musi przesłać żądanie dla swojego konta do usunięcia [nuget.org/account/delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="1d1f4-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="1d1f4-116">Użytkownicy, którzy są jedynymi właścicielami pakietów zaleca się znaleźć właścicieli nowej przed zapytaniem, jego konto usunięte.</span><span class="sxs-lookup"><span data-stu-id="1d1f4-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="1d1f4-117">Jeśli własność pakietu nie został przeniesiony, pakiet NuGet jest nieznajdujące się na liście, i w związku z tym nie jest już dostępne w zapytaniach wyszukiwania w programie Visual Studio lub w witrynie sieci Web nuget.org.</span><span class="sxs-lookup"><span data-stu-id="1d1f4-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="1d1f4-118">Przed usunięciem konta, Administratorzy nuget.org pracują z użytkownika o znalezienie właścicieli nowych pakietów, w których są właścicielami.</span><span class="sxs-lookup"><span data-stu-id="1d1f4-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="1d1f4-119">Akcja usuwania konta zostało zakończone przez administratora nuget.org w ciągu 30 dni od daty żądania.</span><span class="sxs-lookup"><span data-stu-id="1d1f4-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="1d1f4-120">Po usunięciu konta jest usunięte wszystkie dane użytkownika z systemu nuget.org i są podejmowane następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="1d1f4-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="1d1f4-121">Usunięto konto staje się wyrejestrować z nuget.org</span><span class="sxs-lookup"><span data-stu-id="1d1f4-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="1d1f4-122">Wszystkie należące do kluczy interfejsu API są usuwane.</span><span class="sxs-lookup"><span data-stu-id="1d1f4-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="1d1f4-123">Wszystkie zastrzeżone przestrzenie nazw są wydawane</span><span class="sxs-lookup"><span data-stu-id="1d1f4-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="1d1f4-124">Zostaną usunięte wszystkie własność pakietu</span><span class="sxs-lookup"><span data-stu-id="1d1f4-124">Any package ownership are removed</span></span>

<span data-ttu-id="1d1f4-125">Pakiety należące do firmy są *nie* usunięte.</span><span class="sxs-lookup"><span data-stu-id="1d1f4-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="1d1f4-126">Chociaż nieznajdujące się na liście wyników wyszukiwania, pozostają dostępne za pośrednictwem Przywracanie pakietu do projektów, które zależą od nich.</span><span class="sxs-lookup"><span data-stu-id="1d1f4-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="1d1f4-127">Eksportowanie danych klienta</span><span class="sxs-lookup"><span data-stu-id="1d1f4-127">Exporting customer data</span></span>

<span data-ttu-id="1d1f4-128">Po zalogowaniu do nuget.org, użytkownik może przesłać żądanie eksportu za pośrednictwem [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span><span class="sxs-lookup"><span data-stu-id="1d1f4-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="1d1f4-129">Dane wyeksportowane ma zostać udostępnione w ciągu 48 godzin dla użytkownika do pobrania za pośrednictwem obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d1f4-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="1d1f4-130">Po 48 godzin dostępu wygasa, a użytkownik musi przesłać nowe żądanie eksportu, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="1d1f4-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="1d1f4-131">Wyeksportowane dane obejmują:</span><span class="sxs-lookup"><span data-stu-id="1d1f4-131">The exported data includes:</span></span>

* <span data-ttu-id="1d1f4-132">Żądania pomocy technicznej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="1d1f4-132">The user's support requests</span></span>
* <span data-ttu-id="1d1f4-133">Akcje użytkownika (opublikować pakietu, Utwórz konto) jako utrwalone w dziennikach inspekcji</span><span class="sxs-lookup"><span data-stu-id="1d1f4-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="1d1f4-134">Informacje o użytkowniku, jak utrwalone w dziennikach usług IIS</span><span class="sxs-lookup"><span data-stu-id="1d1f4-134">Any user information as persisted in the IIS logs</span></span>
