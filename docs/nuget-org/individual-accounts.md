---
title: Indywidualne konta — NuGet.org
description: Do publikowania pakietów NuGet.org konta na poszczególnych kontach
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: d032b69f6eb4cbd3687ca60190c15aed9b7a4d79
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323898"
---
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="42f26-103">Indywidualne konta na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="42f26-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="42f26-104">Musisz utworzyć indywidualne konto, aby publikować pakiety i zarządzać nimi na NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="42f26-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="42f26-105">Indywidualne konta a konta organizacji</span><span class="sxs-lookup"><span data-stu-id="42f26-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="42f26-106">Twoje indywidualne konto (użytkownika) jest Twoją tożsamością na NuGet.org i może być członkiem dowolnej liczby organizacji.</span><span class="sxs-lookup"><span data-stu-id="42f26-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="42f26-107">Pakiet może należeć do konta organizacji, tak jak może należeć do pojedynczego konta.</span><span class="sxs-lookup"><span data-stu-id="42f26-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="42f26-108">Użytkownicy pakietu nie widzą żadnej różnicy między indywidualnym kontem a kontem organizacji: oba elementy są wyświetlane jako pakiet `owners` .</span><span class="sxs-lookup"><span data-stu-id="42f26-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="42f26-109">Konto organizacji ma co najmniej jedno indywidualne konto jako jego członków.</span><span class="sxs-lookup"><span data-stu-id="42f26-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="42f26-110">Te elementy członkowskie mogą zarządzać zestawem pakietów przy zachowaniu jednej tożsamości na własność.</span><span class="sxs-lookup"><span data-stu-id="42f26-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="42f26-111">Dodawanie nowego indywidualnego konta</span><span class="sxs-lookup"><span data-stu-id="42f26-111">Add a new individual account</span></span>

<span data-ttu-id="42f26-112">Aby utworzyć konto NuGet.org, musisz mieć konto osobiste konto Microsoft (MSA) lub konto Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="42f26-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="42f26-113">Jeśli jej nie masz, możesz [ją](https://signup.live.com) utworzyć.</span><span class="sxs-lookup"><span data-stu-id="42f26-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="42f26-114">Wykonaj poniższe kroki, jeśli masz konto MSA lub AAD.</span><span class="sxs-lookup"><span data-stu-id="42f26-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="42f26-115">Przejdź do [strony NuGet.org logowania.](https://www.nuget.org/users/account/LogOn)</span><span class="sxs-lookup"><span data-stu-id="42f26-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="42f26-116">Kliknij przycisk **Zaloguj się przy użyciu konta Microsoft** przycisku.</span><span class="sxs-lookup"><span data-stu-id="42f26-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="42f26-117">Wprowadź szczegóły konto Microsoft lub Azure Active Directory konta.</span><span class="sxs-lookup"><span data-stu-id="42f26-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="42f26-118">Kliknij przycisk **Tak,** aby zaakceptować uprawnienia, które mają *być nadane NuGet.org* aplikacji.</span><span class="sxs-lookup"><span data-stu-id="42f26-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![Udzielanie uprawnień NuGet.org](media/nuget-org-permissions.png)

1. <span data-ttu-id="42f26-120">Nastąpi przekierowanie do witryny *nuget.org* i zostanie poproszony o zarejestrowanie nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="42f26-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="42f26-121">Określ nazwę użytkownika w polu wejściowym.</span><span class="sxs-lookup"><span data-stu-id="42f26-121">Specify the username in the input box.</span></span> <span data-ttu-id="42f26-122">Pamiętaj, że  w nazwie użytkownika jest zróżnicowana wielkość liter i nie można jej później zmienić ani zmienić jej nazwy.</span><span class="sxs-lookup"><span data-stu-id="42f26-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![Określ nazwę użytkownika na NuGet.org](media/nuget-org-register.png) 

1. <span data-ttu-id="42f26-124">Kliknij przycisk **Zarejestruj.**</span><span class="sxs-lookup"><span data-stu-id="42f26-124">Click the **Register** button.</span></span>

<span data-ttu-id="42f26-125">Masz teraz konto NuGet.org konto.</span><span class="sxs-lookup"><span data-stu-id="42f26-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="42f26-126">Zarządzanie kontami można wykonywać na [stronie ustawień](https://www.nuget.org/account) konta.</span><span class="sxs-lookup"><span data-stu-id="42f26-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="42f26-127">Włączanie uwierzytelniania dwuskładnikowego (2FA)</span><span class="sxs-lookup"><span data-stu-id="42f26-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="42f26-128">Uwierzytelnianie dwuskładnikowe (2FA) to dodatkowa warstwa zabezpieczeń używana podczas logowania się do witryn internetowych lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="42f26-128">Two-factor authentication, or 2FA, is an extra layer of security used when logging into websites or apps.</span></span> <span data-ttu-id="42f26-129">W przypadku uwierzytelniania 2FA musisz zalogować się przy użyciu konta Microsoft (MSA) i podać inną formę uwierzytelniania, do których tylko Ty znasz lub do których masz dostęp.</span><span class="sxs-lookup"><span data-stu-id="42f26-129">With 2FA, you have to log in with your Microsoft Account (MSA) and provide another form of authentication that only you know or have access to.</span></span> <span data-ttu-id="42f26-130">Aby lepiej chronić konto, włącz uwierzytelnianie dwuskładnikowe (zalecane).</span><span class="sxs-lookup"><span data-stu-id="42f26-130">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="42f26-131">Po zalogowaniu się na koncie otwórz swój profil i wybierz pozycję **Włącz w** obszarze **Konto logowania.**</span><span class="sxs-lookup"><span data-stu-id="42f26-131">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![Włączanie funkcji 2FA](media/nuget-org-register-2fa.png)

   <span data-ttu-id="42f26-133">Zostanie wyświetlony komunikat informujący o tym, że przy następnym zalogowaniu się do usługi *nuget.org* zostanie wyświetlony monit o dodatkowe poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="42f26-133">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="42f26-134">Aby ukończyć uwierzytelnianie w tej chwili, wyloguj się, a następnie zaloguj się ponownie.</span><span class="sxs-lookup"><span data-stu-id="42f26-134">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="42f26-135">Po zalogowaniu wybierz tekst lub wiadomość e-mail jako drugą formę uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="42f26-135">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="42f26-136">Sprawdź numer telefonu lub adres e-mail skojarzony już z Twoim konto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="42f26-136">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="42f26-137">Może być konieczne wprowadzenie nowego numeru telefonu lub adresu e-mail dla konta.</span><span class="sxs-lookup"><span data-stu-id="42f26-137">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="42f26-138">Jeśli tak, wprowadź wymagane informacje zgodnie z instrukcjami, a następnie kliknij przycisk **Dalej.**</span><span class="sxs-lookup"><span data-stu-id="42f26-138">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![Włącz funkcję 2FA i wprowadź numer telefonu](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="42f26-140">Sprawdź urządzenie lub konto e-mail i wprowadź właśnie wysłany kod.</span><span class="sxs-lookup"><span data-stu-id="42f26-140">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![Włącz funkcję 2FA i wprowadź kod](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="42f26-142">Postępuj zgodnie z dodatkowymi instrukcjami, aby ukończyć uwierzytelnianie dwuskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="42f26-142">Follow any additional instructions to complete Two-factor authentication.</span></span>

> [!Tip]
> <span data-ttu-id="42f26-143">Włączenie funkcji 2FA dla konta NuGet.org nie ma wpływu na ustawienia uwierzytelniania dla innych kont lub usług, które mogą być połączone z usługą konto Microsoft używaną do logowania się do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="42f26-143">Enabling 2FA for your NuGet.org account does not impact authentication settings for other accounts or services that may be linked to the Microsoft account you use to login to NuGet.org.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="42f26-144">Usuwanie NuGet.org konta</span><span class="sxs-lookup"><span data-stu-id="42f26-144">Delete a NuGet.org account</span></span>

<span data-ttu-id="42f26-145">Aby uzyskać pomoc w zakresie dodatkowych zadań związanych z kontem, takich jak usuwanie konta NuGet.org, zobacz [NuGet.org zarządzania kontami.](/nuget/nuget-org/nuget-org-faq#nuget.org-account-management)</span><span class="sxs-lookup"><span data-stu-id="42f26-145">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](/nuget/nuget-org/nuget-org-faq#nuget.org-account-management).</span></span>
