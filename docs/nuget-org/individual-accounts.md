---
title: Indywidualne konta
description: Poszczególne acccounts na NuGet.org są wymagane do publikowania pakietów
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: c88b88015bd6d5bae4789765126c0a3dec527e24
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419856"
---
# <a name="individual-accounts"></a><span data-ttu-id="7b827-103">Indywidualne konta</span><span class="sxs-lookup"><span data-stu-id="7b827-103">Individual accounts</span></span>

<span data-ttu-id="7b827-104">Musisz utworzyć pojedyncze konto, aby opublikować pakiety i zarządzać nimi w witrynie NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="7b827-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="7b827-105">Konta poszczególnych kont i organizacji</span><span class="sxs-lookup"><span data-stu-id="7b827-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="7b827-106">Twoje konto użytkownika (użytkownik) jest Twoją tożsamością w systemie NuGet.org i może być członkiem dowolnej liczby organizacji.</span><span class="sxs-lookup"><span data-stu-id="7b827-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="7b827-107">Pakiet może należeć do konta organizacji, takie jak może należeć do pojedynczego konta.</span><span class="sxs-lookup"><span data-stu-id="7b827-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="7b827-108">Odbiorcy pakietu nie widzą żadnych różnic między kontem pojedynczym ani kontem organizacji: są one wyświetlane jako `owners`pakiet.</span><span class="sxs-lookup"><span data-stu-id="7b827-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="7b827-109">Konto organizacji ma co najmniej jedno pojedyncze konto jako jego członków.</span><span class="sxs-lookup"><span data-stu-id="7b827-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="7b827-110">Ci członkowie mogą zarządzać zestawem pakietów przy zachowaniu pojedynczej tożsamości dla własności.</span><span class="sxs-lookup"><span data-stu-id="7b827-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="7b827-111">Dodaj nowe konto indywidualne</span><span class="sxs-lookup"><span data-stu-id="7b827-111">Add a new individual account</span></span>

<span data-ttu-id="7b827-112">Aby utworzyć konto usługi NuGet.org, musisz mieć konto usługi Personal konto Microsoft (MSA) lub Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="7b827-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="7b827-113">Jeśli go nie masz, możesz go [utworzyć](https://signup.live.com) .</span><span class="sxs-lookup"><span data-stu-id="7b827-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="7b827-114">Jeśli masz konto MSA lub AAD, wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="7b827-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="7b827-115">Przejdź do [strony logowania NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="7b827-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="7b827-116">Kliknij przycisk **Zaloguj się przy użyciu konta Microsoft** .</span><span class="sxs-lookup"><span data-stu-id="7b827-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="7b827-117">Wprowadź szczegóły konta konto Microsoft lub Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7b827-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="7b827-118">Kliknij przycisk **tak** , aby zaakceptować uprawnienia nadawane aplikacji *NuGet.org* .</span><span class="sxs-lookup"><span data-stu-id="7b827-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Nadawanie uprawnień NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="7b827-120">Nastąpi przekierowanie do *NuGet.org*i prośba o zarejestrowanie nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7b827-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="7b827-121">Określ nazwę użytkownika w polu wejściowym.</span><span class="sxs-lookup"><span data-stu-id="7b827-121">Specify the username in the input box.</span></span> <span data-ttu-id="7b827-122">Należy pamiętać, że nazwa **użytkownika uwzględnia** wielkość liter i nie można zmienić jej nazwy.</span><span class="sxs-lookup"><span data-stu-id="7b827-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Określ nazwę użytkownika w NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="7b827-124">Kliknij przycisk **zarejestruj** .</span><span class="sxs-lookup"><span data-stu-id="7b827-124">Click the **Register** button.</span></span>

<span data-ttu-id="7b827-125">Masz już konto NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="7b827-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="7b827-126">Zarządzanie kontem można przeprowadzić na stronie [Ustawienia konta](https://www.nuget.org/account) .</span><span class="sxs-lookup"><span data-stu-id="7b827-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="7b827-127">Włącz uwierzytelnianie dwuskładnikowe (funkcji 2FA)</span><span class="sxs-lookup"><span data-stu-id="7b827-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="7b827-128">Aby lepiej chronić Twoje konto, Włącz uwierzytelnianie dwuskładnikowe (zalecane).</span><span class="sxs-lookup"><span data-stu-id="7b827-128">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="7b827-129">Po zalogowaniu się na koncie Otwórz swój profil i wybierz pozycję **Włącz** w obszarze **konto logowania**.</span><span class="sxs-lookup"><span data-stu-id="7b827-129">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![Włącz funkcji 2FA](media/nuget-org-register-2fa.png)

   <span data-ttu-id="7b827-131">Zobaczysz komunikat informujący o tym, że przy następnym logowaniu do usługi *NuGet.org*zostanie wyświetlony monit o podanie dodatkowych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="7b827-131">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="7b827-132">Aby w tym momencie ukończyć uwierzytelnianie, Wyloguj się, a następnie zaloguj się ponownie.</span><span class="sxs-lookup"><span data-stu-id="7b827-132">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="7b827-133">Po zalogowaniu wybierz opcję tekst lub wiadomość e-mail jako drugą formę uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="7b827-133">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="7b827-134">Sprawdź numer telefonu lub adres e-mail, który jest już skojarzony z konto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7b827-134">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="7b827-135">Może być konieczne wprowadzenie nowego numeru telefonu lub adresu e-mail dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="7b827-135">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="7b827-136">W takim przypadku wprowadź wymagane informacje zgodnie z instrukcją, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7b827-136">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![Włącz funkcji 2FA](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="7b827-138">Sprawdź urządzenie lub konto e-mail, a następnie wprowadź kod, który właśnie został wysłany.</span><span class="sxs-lookup"><span data-stu-id="7b827-138">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![Włącz funkcji 2FA](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="7b827-140">Postępuj zgodnie z dodatkowymi instrukcjami, aby przeprowadzić uwierzytelnianie dwuskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="7b827-140">Follow any additional instructions to complete Two-factor authentication.</span></span>
