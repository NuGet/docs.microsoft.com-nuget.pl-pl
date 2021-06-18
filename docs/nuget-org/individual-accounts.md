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
# <a name="individual-accounts-on-nugetorg"></a>Indywidualne konta na NuGet.org

Musisz utworzyć indywidualne konto, aby publikować pakiety i zarządzać nimi na NuGet.org.

## <a name="individual-accounts-vs-organization-accounts"></a>Indywidualne konta a konta organizacji

Twoje indywidualne konto (użytkownika) jest Twoją tożsamością na NuGet.org i może być członkiem dowolnej liczby organizacji. Pakiet może należeć do konta organizacji, tak jak może należeć do pojedynczego konta. Użytkownicy pakietu nie widzą żadnej różnicy między indywidualnym kontem a kontem organizacji: oba elementy są wyświetlane jako pakiet `owners` .

Konto organizacji ma co najmniej jedno indywidualne konto jako jego członków. Te elementy członkowskie mogą zarządzać zestawem pakietów przy zachowaniu jednej tożsamości na własność.

## <a name="add-a-new-individual-account"></a>Dodawanie nowego indywidualnego konta

Aby utworzyć konto NuGet.org, musisz mieć konto osobiste konto Microsoft (MSA) lub konto Azure Active Directory (AAD). Jeśli jej nie masz, możesz [ją](https://signup.live.com) utworzyć. Wykonaj poniższe kroki, jeśli masz konto MSA lub AAD.

1. Przejdź do [strony NuGet.org logowania.](https://www.nuget.org/users/account/LogOn)

1. Kliknij przycisk **Zaloguj się przy użyciu konta Microsoft** przycisku.

1. Wprowadź szczegóły konto Microsoft lub Azure Active Directory konta.

1. Kliknij przycisk **Tak,** aby zaakceptować uprawnienia, które mają *być nadane NuGet.org* aplikacji.

   ![Udzielanie uprawnień NuGet.org](media/nuget-org-permissions.png)

1. Nastąpi przekierowanie do witryny *nuget.org* i zostanie poproszony o zarejestrowanie nazwy użytkownika.

1. Określ nazwę użytkownika w polu wejściowym. Pamiętaj, że  w nazwie użytkownika jest zróżnicowana wielkość liter i nie można jej później zmienić ani zmienić jej nazwy.

   ![Określ nazwę użytkownika na NuGet.org](media/nuget-org-register.png) 

1. Kliknij przycisk **Zarejestruj.**

Masz teraz konto NuGet.org konto. Zarządzanie kontami można wykonywać na [stronie ustawień](https://www.nuget.org/account) konta.

## <a name="enable-two-factor-authentication-2fa"></a>Włączanie uwierzytelniania dwuskładnikowego (2FA)

Uwierzytelnianie dwuskładnikowe (2FA) to dodatkowa warstwa zabezpieczeń używana podczas logowania się do witryn internetowych lub aplikacji. W przypadku uwierzytelniania 2FA musisz zalogować się przy użyciu konta Microsoft (MSA) i podać inną formę uwierzytelniania, do których tylko Ty znasz lub do których masz dostęp. Aby lepiej chronić konto, włącz uwierzytelnianie dwuskładnikowe (zalecane).

1. Po zalogowaniu się na koncie otwórz swój profil i wybierz pozycję **Włącz w** obszarze **Konto logowania.**

   ![Włączanie funkcji 2FA](media/nuget-org-register-2fa.png)

   Zostanie wyświetlony komunikat informujący o tym, że przy następnym zalogowaniu się do usługi *nuget.org* zostanie wyświetlony monit o dodatkowe poświadczenia.

2. Aby ukończyć uwierzytelnianie w tej chwili, wyloguj się, a następnie zaloguj się ponownie.

3. Po zalogowaniu wybierz tekst lub wiadomość e-mail jako drugą formę uwierzytelniania.

   Sprawdź numer telefonu lub adres e-mail skojarzony już z Twoim konto Microsoft. Może być konieczne wprowadzenie nowego numeru telefonu lub adresu e-mail dla konta. Jeśli tak, wprowadź wymagane informacje zgodnie z instrukcjami, a następnie kliknij przycisk **Dalej.**

   ![Włącz funkcję 2FA i wprowadź numer telefonu](media/nuget-org-sign-in-2fa.png)

4. Sprawdź urządzenie lub konto e-mail i wprowadź właśnie wysłany kod.

   ![Włącz funkcję 2FA i wprowadź kod](media/nuget-org-enter-code-2fa.png)

5. Postępuj zgodnie z dodatkowymi instrukcjami, aby ukończyć uwierzytelnianie dwuskładnikowe.

> [!Tip]
> Włączenie funkcji 2FA dla konta NuGet.org nie ma wpływu na ustawienia uwierzytelniania dla innych kont lub usług, które mogą być połączone z usługą konto Microsoft używaną do logowania się do NuGet.org.

## <a name="delete-a-nugetorg-account"></a>Usuwanie NuGet.org konta

Aby uzyskać pomoc w zakresie dodatkowych zadań związanych z kontem, takich jak usuwanie konta NuGet.org, zobacz [NuGet.org zarządzania kontami.](/nuget/nuget-org/nuget-org-faq#nuget.org-account-management)
