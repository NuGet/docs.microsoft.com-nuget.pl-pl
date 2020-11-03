---
title: Pojedyncze konta — NuGet.org
description: Poszczególne acccounts na NuGet.org są wymagane do publikowania pakietów
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7951b3db0cdcaee0a1eb955a5bf6fedce24c79c9
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237617"
---
# <a name="individual-accounts-on-nugetorg"></a>Indywidualne konta w witrynie NuGet.org

Musisz utworzyć pojedyncze konto, aby opublikować pakiety i zarządzać nimi w witrynie NuGet.org.

## <a name="individual-accounts-vs-organization-accounts"></a>Konta poszczególnych kont i organizacji

Twoje konto użytkownika (użytkownik) jest Twoją tożsamością w systemie NuGet.org i może być członkiem dowolnej liczby organizacji. Pakiet może należeć do konta organizacji, takie jak może należeć do pojedynczego konta. Odbiorcy pakietu nie widzą żadnych różnic między kontem pojedynczym ani kontem organizacji: są one wyświetlane jako pakiet `owners` .

Konto organizacji ma co najmniej jedno pojedyncze konto jako jego członków. Ci członkowie mogą zarządzać zestawem pakietów przy zachowaniu pojedynczej tożsamości dla własności.

## <a name="add-a-new-individual-account"></a>Dodaj nowe konto indywidualne

Aby utworzyć konto usługi NuGet.org, musisz mieć konto usługi Personal konto Microsoft (MSA) lub Azure Active Directory (AAD). Jeśli go nie masz, możesz go [utworzyć](https://signup.live.com) . Jeśli masz konto MSA lub AAD, wykonaj następujące czynności.

1. Przejdź do [strony logowania NuGet.org](https://www.nuget.org/users/account/LogOn).

1. Kliknij przycisk **Zaloguj się przy użyciu konta Microsoft** .

1. Wprowadź szczegóły konta konto Microsoft lub Azure Active Directory.

1. Kliknij przycisk **tak** , aby zaakceptować uprawnienia nadawane aplikacji *NuGet.org* .

   ![Nadawanie uprawnień NuGet.org](media/nuget-org-permissions.png)

1. Nastąpi przekierowanie do *NuGet.org* i prośba o zarejestrowanie nazwy użytkownika.

1. Określ nazwę użytkownika w polu wejściowym. Należy pamiętać, że nazwa **użytkownika uwzględnia wielkość liter i** nie można zmienić jej nazwy.

   ![Określ nazwę użytkownika w NuGet.org](media/nuget-org-register.png) 

1. Kliknij przycisk **zarejestruj** .

Masz już konto NuGet.org. Zarządzanie kontem można przeprowadzić na stronie [Ustawienia konta](https://www.nuget.org/account) .

## <a name="enable-two-factor-authentication-2fa"></a>Włącz uwierzytelnianie dwuskładnikowe (funkcji 2FA)

Uwierzytelnianie dwuskładnikowe lub funkcji 2FA to dodatkowa warstwa zabezpieczeń używana podczas rejestrowania w witrynach sieci Web lub aplikacjach. Korzystając z funkcji 2FA, musisz zalogować się przy użyciu konta Microsoft (MSA) i udostępnić inną formę uwierzytelniania, który jest tylko znany lub ma dostęp do programu. Aby lepiej chronić Twoje konto, Włącz uwierzytelnianie dwuskładnikowe (zalecane).

1. Po zalogowaniu się na koncie Otwórz swój profil i wybierz pozycję **Włącz** w obszarze **konto logowania** .

   ![Włącz funkcji 2FA](media/nuget-org-register-2fa.png)

   Zobaczysz komunikat informujący o tym, że przy następnym logowaniu do usługi *NuGet.org* zostanie wyświetlony monit o podanie dodatkowych poświadczeń.

2. Aby w tym momencie ukończyć uwierzytelnianie, Wyloguj się, a następnie zaloguj się ponownie.

3. Po zalogowaniu wybierz opcję tekst lub wiadomość e-mail jako drugą formę uwierzytelniania.

   Sprawdź numer telefonu lub adres e-mail, który jest już skojarzony z konto Microsoft. Może być konieczne wprowadzenie nowego numeru telefonu lub adresu e-mail dla Twojego konta. W takim przypadku wprowadź wymagane informacje zgodnie z instrukcją, a następnie kliknij przycisk **dalej** .

   ![Włącz funkcji 2FA](media/nuget-org-sign-in-2fa.png)

4. Sprawdź urządzenie lub konto e-mail, a następnie wprowadź kod, który właśnie został wysłany.

   ![Włącz funkcji 2FA](media/nuget-org-enter-code-2fa.png)

5. Postępuj zgodnie z dodatkowymi instrukcjami, aby przeprowadzić uwierzytelnianie dwuskładnikowe.

> [!Tip]
> Włączenie funkcji 2FA dla konta NuGet.org nie ma wpływu na ustawienia uwierzytelniania dla innych kont lub usług, które mogą być połączone z konto Microsoft używanym do logowania się do usługi NuGet.org.

## <a name="delete-a-nugetorg-account"></a>Usuwanie konta NuGet.org

Aby uzyskać pomoc dotyczącą dodatkowych zadań związanych z kontem, takich jak usuwanie konta usługi NuGet.org, zobacz [Zarządzanie kontem NuGet.org](nuget-org-faq.md#nugetorg-account-management).
