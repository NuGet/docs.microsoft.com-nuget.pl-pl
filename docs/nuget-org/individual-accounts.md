---
title: Indywidualne konta
description: Poszczególne acccounts w witrynie NuGet.org są wymagane do publikowania pakietów
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427558"
---
# <a name="individual-accounts"></a><span data-ttu-id="232d5-103">Indywidualne konta</span><span class="sxs-lookup"><span data-stu-id="232d5-103">Individual accounts</span></span>

<span data-ttu-id="232d5-104">Należy utworzyć indywidualne konta do publikowania i zarządzania pakietami w witrynie NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="232d5-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="232d5-105">Indywidualne konta i kont organizacji</span><span class="sxs-lookup"><span data-stu-id="232d5-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="232d5-106">Kontem osoby (użytkownik) jest swoją tożsamość w witrynie NuGet.org i może należeć do dowolnej liczby organizacji.</span><span class="sxs-lookup"><span data-stu-id="232d5-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="232d5-107">Pakiet może należeć do organizacji, takich jak mogą należeć do indywidualnych kont.</span><span class="sxs-lookup"><span data-stu-id="232d5-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="232d5-108">Konsumentów pakietu nie jest widoczna różnica między indywidualne konto lub konta organizacji: oba są wyświetlane jako pakiet `owners`.</span><span class="sxs-lookup"><span data-stu-id="232d5-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="232d5-109">Konto organizacji ma co najmniej jeden z indywidualnych kont jako elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="232d5-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="232d5-110">Członkowie mogą zarządzać zestaw pakietów przy zachowaniu jednej tożsamości dla własności.</span><span class="sxs-lookup"><span data-stu-id="232d5-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="232d5-111">Dodaj nowe konto indywidualne</span><span class="sxs-lookup"><span data-stu-id="232d5-111">Add a new individual account</span></span>

<span data-ttu-id="232d5-112">Aby utworzyć konto w witrynie NuGet.org, musisz mieć konto usługi Azure Active Directory (AAD) lub osobistego konta Microsoft (MSA).</span><span class="sxs-lookup"><span data-stu-id="232d5-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="232d5-113">Jeśli nie masz, możesz to zrobić [tworzenie](https://signup.live.com) jeden.</span><span class="sxs-lookup"><span data-stu-id="232d5-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="232d5-114">Wykonaj poniższe kroki, jeśli masz konto MSA lub usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="232d5-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="232d5-115">Przejdź do [strony logowania w witrynie NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="232d5-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="232d5-116">Kliknij pozycję **Zaloguj się przy użyciu Microsoft** przycisku.</span><span class="sxs-lookup"><span data-stu-id="232d5-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="232d5-117">Wprowadź szczegóły konta usługi Azure Active Directory lub konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="232d5-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="232d5-118">Kliknij **tak** zaakceptowania uprawnień do *NuGet.org* aplikacji.</span><span class="sxs-lookup"><span data-stu-id="232d5-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Przyznawanie uprawnień do NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="232d5-120">Nastąpi przekierowanie do *nuget.org*oraz pytanie zarejestrować nazwę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="232d5-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="232d5-121">Określ nazwę użytkownika w polu wejściowym.</span><span class="sxs-lookup"><span data-stu-id="232d5-121">Specify the username in the input box.</span></span> <span data-ttu-id="232d5-122">Należy pamiętać, że nazwa użytkownika **jest** zamierzone, Zapisz poufne i nie można zmienić ani zmienić nazwy później.</span><span class="sxs-lookup"><span data-stu-id="232d5-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Podaj nazwę użytkownika w witrynie NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="232d5-124">Kliknij przycisk **zarejestrować** przycisku.</span><span class="sxs-lookup"><span data-stu-id="232d5-124">Click the **Register** button.</span></span>

<span data-ttu-id="232d5-125">Masz teraz konto NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="232d5-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="232d5-126">Zarządzanie kontami można wykonywać na [ustawienia konta](https://www.nuget.org/account) strony.</span><span class="sxs-lookup"><span data-stu-id="232d5-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>
