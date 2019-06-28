---
title: Żądania danych użytkownika
description: Zasady dla żądania eksportu danych użytkownika i Usuń
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427513"
---
# <a name="user-data-requests"></a><span data-ttu-id="b78e8-103">Żądania danych użytkownika</span><span class="sxs-lookup"><span data-stu-id="b78e8-103">User Data Requests</span></span>

<span data-ttu-id="b78e8-104">nuget.org, użytkownicy będą mogli wysyłać żądania usunięcia informacji i żądań eksportu informacji za pośrednictwem [nuget.org](https://www.nuget.org). Oba typy są przesyłane w formie obsługę żądań i są wykonywane przez administratorów nuget.org w ciągu 30 dni.</span><span class="sxs-lookup"><span data-stu-id="b78e8-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="b78e8-105">Następujące dane użytkownika są bezpośrednio dostępne za pośrednictwem nuget.org:</span><span class="sxs-lookup"><span data-stu-id="b78e8-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="b78e8-106">Konto powiązanych danych, takich jak adres e-mail konta logowania, zdjęcie profilowe i ustawienia powiadomień e-mail</span><span class="sxs-lookup"><span data-stu-id="b78e8-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="b78e8-107">Klucze interfejsu API należące do firmy</span><span class="sxs-lookup"><span data-stu-id="b78e8-107">Owned API Keys</span></span>
* <span data-ttu-id="b78e8-108">Lista pakietów należące do firmy</span><span class="sxs-lookup"><span data-stu-id="b78e8-108">List of owned packages</span></span>

<span data-ttu-id="b78e8-109">Te dane nie są objęte dane wyeksportowane za pomocą żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="b78e8-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="b78e8-110">Identyfikowanie danych klienta</span><span class="sxs-lookup"><span data-stu-id="b78e8-110">Identifying customer data</span></span>

<span data-ttu-id="b78e8-111">Dane klienta mogą zostać określone jako nazwy kont użytkowników w witrynie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b78e8-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="b78e8-112">Usuwanie danych klienta</span><span class="sxs-lookup"><span data-stu-id="b78e8-112">Deleting customer data</span></span>

<span data-ttu-id="b78e8-113">Aby zażądać usuwania danych użytkownika z witryny nuget.org:</span><span class="sxs-lookup"><span data-stu-id="b78e8-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="b78e8-114">Użytkownik musi zalogować się do [nuget.org](https://www.nuget.org)</span><span class="sxs-lookup"><span data-stu-id="b78e8-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="b78e8-115">Użytkownik musi przesłać żądanie do swojego konta do usunięcia [nuget.org/account/delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="b78e8-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="b78e8-116">Użytkownicy, którzy są właścicielami jedyny pakietów zaleca się znaleźć nowym właścicielom przed zadaniem ich konta usunięte.</span><span class="sxs-lookup"><span data-stu-id="b78e8-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="b78e8-117">Jeśli własność pakietu nie są przesyłane, pakiet NuGet jest nieznajdujące się na liście, i w rezultacie nie jest już dostępna w zapytaniach wyszukiwania w programie Visual Studio lub w witrynie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b78e8-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="b78e8-118">Przed usunięciem konta administratorów nuget.org pracować użytkownika o znalezienie nowym właścicielom pakietów, które są właścicielami.</span><span class="sxs-lookup"><span data-stu-id="b78e8-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="b78e8-119">Nuget.org administrator wykonać akcję usuwania konta w ciągu 30 dni od daty żądania.</span><span class="sxs-lookup"><span data-stu-id="b78e8-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="b78e8-120">Po usunięciu konta jest usunięte wszystkie dane użytkownika z systemu nuget.org, i są podejmowane następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="b78e8-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="b78e8-121">Usunięte konto staje się wyrejestrować z repozytorium nuget.org</span><span class="sxs-lookup"><span data-stu-id="b78e8-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="b78e8-122">Wszystkie należące do kluczy interfejsu API są usuwane.</span><span class="sxs-lookup"><span data-stu-id="b78e8-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="b78e8-123">Wszystkie obszary nazw zastrzeżonych zostaną zwolnione.</span><span class="sxs-lookup"><span data-stu-id="b78e8-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="b78e8-124">Własność dowolnego pakietu są usuwane.</span><span class="sxs-lookup"><span data-stu-id="b78e8-124">Any package ownership are removed</span></span>

<span data-ttu-id="b78e8-125">Pakiety należące do firmy są *nie* usunięte.</span><span class="sxs-lookup"><span data-stu-id="b78e8-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="b78e8-126">Chociaż nieznajdujące się na liście wyników wyszukiwania, pozostają dostępne za pośrednictwem Przywracanie pakietu do projektów, które zależą od nich.</span><span class="sxs-lookup"><span data-stu-id="b78e8-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="b78e8-127">Eksportowanie danych klienta</span><span class="sxs-lookup"><span data-stu-id="b78e8-127">Exporting customer data</span></span>

<span data-ttu-id="b78e8-128">Po zalogowaniu się w witrynie nuget.org, użytkownik może przesłać żądanie eksportu za pośrednictwem [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span><span class="sxs-lookup"><span data-stu-id="b78e8-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="b78e8-129">Eksportowanie danych ma zostać udostępnione w ciągu 48 godzin do użytkownika do pobrania za pośrednictwem obiektu Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b78e8-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="b78e8-130">Po upływie 48 godzin dostępu wygasa, a użytkownik musi przesłać nowe żądanie eksportu, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="b78e8-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="b78e8-131">Wyeksportowane dane obejmują:</span><span class="sxs-lookup"><span data-stu-id="b78e8-131">The exported data includes:</span></span>

* <span data-ttu-id="b78e8-132">Żądania pomocy technicznej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="b78e8-132">The user's support requests</span></span>
* <span data-ttu-id="b78e8-133">Czynności wykonywanych przez użytkownika (publikowanie pakietu, Utwórz konto) jako utrwalone w dziennikach inspekcji</span><span class="sxs-lookup"><span data-stu-id="b78e8-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="b78e8-134">Informacje o użytkowniku jako utrwalone w dziennikach usług IIS</span><span class="sxs-lookup"><span data-stu-id="b78e8-134">Any user information as persisted in the IIS logs</span></span>
