---
title: Konta indywidualne - NuGet.org
description: Do publikowania pakietów wymagane są indywidualne konta na NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7951b3db0cdcaee0a1eb955a5bf6fedce24c79c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429018"
---
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="0bd8e-103">Indywidualne konta na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="0bd8e-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="0bd8e-104">Musisz utworzyć indywidualne konto, aby publikować pakiety i zarządzać nimi w NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="0bd8e-105">Konta indywidualne a konta organizacji</span><span class="sxs-lookup"><span data-stu-id="0bd8e-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="0bd8e-106">Twoje indywidualne konto (użytkownika) jest Twoją tożsamością w NuGet.org i może być członkiem dowolnej liczby organizacji.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="0bd8e-107">Pakiet może należeć do konta organizacji, tak jak może należeć do indywidualnego konta.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="0bd8e-108">Konsumenci pakietów nie widzą żadnej różnicy między kontem indywidualnym `owners`lub kontem organizacji: oba są wyświetlane jako pakiet.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="0bd8e-109">Konto organizacji ma co najmniej jedno konto pojedyncze jako jej członkowie.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="0bd8e-110">Te elementy członkowskie mogą zarządzać zestawem pakietów przy zachowaniu jednej tożsamości dla własności.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="0bd8e-111">Dodawanie nowego konta indywidualnego</span><span class="sxs-lookup"><span data-stu-id="0bd8e-111">Add a new individual account</span></span>

<span data-ttu-id="0bd8e-112">Aby utworzyć konto NuGet.org, musisz mieć osobiste konto Microsoft (MSA) lub konto usługi Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="0bd8e-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="0bd8e-113">Jeśli go nie masz, możesz go [utworzyć.](https://signup.live.com)</span><span class="sxs-lookup"><span data-stu-id="0bd8e-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="0bd8e-114">Wykonaj następujące kroki, jeśli masz konto MSA lub AAD.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="0bd8e-115">Przejdź do [strony logowania NuGet.org](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="0bd8e-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="0bd8e-116">Kliknij przycisk **Zaloguj się za pomocą firmy Microsoft.**</span><span class="sxs-lookup"><span data-stu-id="0bd8e-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="0bd8e-117">Wprowadź szczegóły konta Microsoft lub usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="0bd8e-118">Kliknij przycisk **Tak,** aby zaakceptować uprawnienia, które mają być przyznane aplikacji *NuGet.org.*</span><span class="sxs-lookup"><span data-stu-id="0bd8e-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Udzielanie uprawnień do NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="0bd8e-120">Zostaniesz przekierowany do *nuget.org*i poproszony o zarejestrowanie nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="0bd8e-121">Określ nazwę użytkownika w polu wprowadzania.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-121">Specify the username in the input box.</span></span> <span data-ttu-id="0bd8e-122">Należy pamiętać, że nazwa użytkownika **jest** rozróżniana wielkość liter i nie można zmienić lub zmienić nazwy później.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Określ nazwę użytkownika na NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="0bd8e-124">Kliknij przycisk **Zarejestruj** się.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-124">Click the **Register** button.</span></span>

<span data-ttu-id="0bd8e-125">Masz teraz konto NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="0bd8e-126">Zarządzanie kontem można wykonać na stronie [ustawień konta.](https://www.nuget.org/account)</span><span class="sxs-lookup"><span data-stu-id="0bd8e-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="0bd8e-127">Włącz uwierzytelnianie dwuskładnikowe (2FA)</span><span class="sxs-lookup"><span data-stu-id="0bd8e-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="0bd8e-128">Uwierzytelnianie dwuskładnikowe lub 2FA to dodatkowa warstwa zabezpieczeń używana podczas logowania do witryn sieci Web lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-128">Two-factor authentication, or 2FA, is an extra layer of security used when logging into websites or apps.</span></span> <span data-ttu-id="0bd8e-129">Dzięki 2FA musisz zalogować się za pomocą konta Microsoft (MSA) i podać inną formę uwierzytelniania, do której tylko ty znasz lub do której masz dostęp.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-129">With 2FA, you have to log in with your Microsoft Account (MSA) and provide another form of authentication that only you know or have access to.</span></span> <span data-ttu-id="0bd8e-130">Aby lepiej chronić swoje konto, włącz uwierzytelnianie dwuskładnikowe (zalecane).</span><span class="sxs-lookup"><span data-stu-id="0bd8e-130">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="0bd8e-131">Po zalogowaniu się na swoje konto otwórz swój profil i wybierz **włącz** w obszarze **Konto logowania**.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-131">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![Włącz 2FA](media/nuget-org-register-2fa.png)

   <span data-ttu-id="0bd8e-133">Zostanie wyświetlony komunikat informujący, że przy następnym logowanie się do *nuget.org*zostanie wyświetlony monit o podanie dodatkowych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-133">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="0bd8e-134">Aby zakończyć uwierzytelnianie w tej chwili, wyloguj się, a następnie zaloguj się ponownie.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-134">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="0bd8e-135">Po zalogowaniu się wybierz tekst lub wiadomość e-mail jako drugą formę uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-135">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="0bd8e-136">Sprawdź numer telefonu lub wiadomość e-mail, która jest już skojarzona z Twoim kontem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-136">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="0bd8e-137">Może być konieczne wprowadzenie nowego numeru telefonu lub wiadomości e-mail dla swojego konta.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-137">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="0bd8e-138">Jeśli tak, wprowadź wymagane informacje zgodnie z instrukcją i kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-138">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![Włącz 2FA](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="0bd8e-140">Sprawdź swoje urządzenie lub konto e-mail i wprowadź kod, który właśnie został wysłany.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-140">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![Włącz 2FA](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="0bd8e-142">Postępuj zgodnie z dodatkowymi instrukcjami, aby ukończyć uwierzytelnianie dwuskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-142">Follow any additional instructions to complete Two-factor authentication.</span></span>

> [!Tip]
> <span data-ttu-id="0bd8e-143">Włączenie 2FA dla konta NuGet.org nie ma wpływu na ustawienia uwierzytelniania dla innych kont lub usług, które mogą być połączone z kontem Microsoft używanym do logowania się do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="0bd8e-143">Enabling 2FA for your NuGet.org account does not impact authentication settings for other accounts or services that may be linked to the Microsoft account you use to login to NuGet.org.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="0bd8e-144">Usuwanie konta NuGet.org</span><span class="sxs-lookup"><span data-stu-id="0bd8e-144">Delete a NuGet.org account</span></span>

<span data-ttu-id="0bd8e-145">Aby uzyskać pomoc dotyczącą dodatkowych zadań związanych z kontem, takich jak usuwanie konta NuGet.org, zobacz [NuGet.org zarządzanie kontem](nuget-org-faq.md#nugetorg-account-management).</span><span class="sxs-lookup"><span data-stu-id="0bd8e-145">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](nuget-org-faq.md#nugetorg-account-management).</span></span>
