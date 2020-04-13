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
# <a name="individual-accounts-on-nugetorg"></a>Indywidualne konta na NuGet.org

Musisz utworzyć indywidualne konto, aby publikować pakiety i zarządzać nimi w NuGet.org.

## <a name="individual-accounts-vs-organization-accounts"></a>Konta indywidualne a konta organizacji

Twoje indywidualne konto (użytkownika) jest Twoją tożsamością w NuGet.org i może być członkiem dowolnej liczby organizacji. Pakiet może należeć do konta organizacji, tak jak może należeć do indywidualnego konta. Konsumenci pakietów nie widzą żadnej różnicy między kontem indywidualnym `owners`lub kontem organizacji: oba są wyświetlane jako pakiet.

Konto organizacji ma co najmniej jedno konto pojedyncze jako jej członkowie. Te elementy członkowskie mogą zarządzać zestawem pakietów przy zachowaniu jednej tożsamości dla własności.

## <a name="add-a-new-individual-account"></a>Dodawanie nowego konta indywidualnego

Aby utworzyć konto NuGet.org, musisz mieć osobiste konto Microsoft (MSA) lub konto usługi Azure Active Directory (AAD). Jeśli go nie masz, możesz go [utworzyć.](https://signup.live.com) Wykonaj następujące kroki, jeśli masz konto MSA lub AAD.

1. Przejdź do [strony logowania NuGet.org](https://www.nuget.org/users/account/LogOn).

1. Kliknij przycisk **Zaloguj się za pomocą firmy Microsoft.**

1. Wprowadź szczegóły konta Microsoft lub usługi Azure Active Directory.

1. Kliknij przycisk **Tak,** aby zaakceptować uprawnienia, które mają być przyznane aplikacji *NuGet.org.*

   ![Udzielanie uprawnień do NuGet.org](media/nuget-org-permissions.png)

1. Zostaniesz przekierowany do *nuget.org*i poproszony o zarejestrowanie nazwy użytkownika.

1. Określ nazwę użytkownika w polu wprowadzania. Należy pamiętać, że nazwa użytkownika **jest** rozróżniana wielkość liter i nie można zmienić lub zmienić nazwy później.

   ![Określ nazwę użytkownika na NuGet.org](media/nuget-org-register.png) 

1. Kliknij przycisk **Zarejestruj** się.

Masz teraz konto NuGet.org. Zarządzanie kontem można wykonać na stronie [ustawień konta.](https://www.nuget.org/account)

## <a name="enable-two-factor-authentication-2fa"></a>Włącz uwierzytelnianie dwuskładnikowe (2FA)

Uwierzytelnianie dwuskładnikowe lub 2FA to dodatkowa warstwa zabezpieczeń używana podczas logowania do witryn sieci Web lub aplikacji. Dzięki 2FA musisz zalogować się za pomocą konta Microsoft (MSA) i podać inną formę uwierzytelniania, do której tylko ty znasz lub do której masz dostęp. Aby lepiej chronić swoje konto, włącz uwierzytelnianie dwuskładnikowe (zalecane).

1. Po zalogowaniu się na swoje konto otwórz swój profil i wybierz **włącz** w obszarze **Konto logowania**.

   ![Włącz 2FA](media/nuget-org-register-2fa.png)

   Zostanie wyświetlony komunikat informujący, że przy następnym logowanie się do *nuget.org*zostanie wyświetlony monit o podanie dodatkowych poświadczeń.

2. Aby zakończyć uwierzytelnianie w tej chwili, wyloguj się, a następnie zaloguj się ponownie.

3. Po zalogowaniu się wybierz tekst lub wiadomość e-mail jako drugą formę uwierzytelniania.

   Sprawdź numer telefonu lub wiadomość e-mail, która jest już skojarzona z Twoim kontem Microsoft. Może być konieczne wprowadzenie nowego numeru telefonu lub wiadomości e-mail dla swojego konta. Jeśli tak, wprowadź wymagane informacje zgodnie z instrukcją i kliknij przycisk **Dalej**.

   ![Włącz 2FA](media/nuget-org-sign-in-2fa.png)

4. Sprawdź swoje urządzenie lub konto e-mail i wprowadź kod, który właśnie został wysłany.

   ![Włącz 2FA](media/nuget-org-enter-code-2fa.png)

5. Postępuj zgodnie z dodatkowymi instrukcjami, aby ukończyć uwierzytelnianie dwuskładnikowe.

> [!Tip]
> Włączenie 2FA dla konta NuGet.org nie ma wpływu na ustawienia uwierzytelniania dla innych kont lub usług, które mogą być połączone z kontem Microsoft używanym do logowania się do NuGet.org.

## <a name="delete-a-nugetorg-account"></a>Usuwanie konta NuGet.org

Aby uzyskać pomoc dotyczącą dodatkowych zadań związanych z kontem, takich jak usuwanie konta NuGet.org, zobacz [NuGet.org zarządzanie kontem](nuget-org-faq.md#nugetorg-account-management).
