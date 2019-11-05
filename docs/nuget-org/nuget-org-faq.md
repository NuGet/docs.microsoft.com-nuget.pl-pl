---
title: Często zadawane pytania NuGet.org
description: Często zadawane pytania i odpowiedzi dotyczące pracy z galerią NuGet.
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e2b6a64b8010f16d0fc33cca437b348d8f784fd7
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610509"
---
# <a name="nugetorg-frequently-asked-questions"></a>Często zadawane pytania NuGet.org

## <a name="license-terms"></a>Postanowienia licencyjne

**Jakie są domyślne postanowienia licencyjne, jeśli pakiet nie zawiera określonych informacji o licencji?**

Każdy pakiet podlega postanowieniom zawartym w pakiecie. Przed uzyskaniem dostępu do, pobraniem lub uzyskaniem jakichkolwiek pakietów należy przejrzeć odpowiednie warunki. W witrynie NuGet.org Użyj linku **Informacje o licencji** na stronie pakiet.

Jeśli pakiet nie określa postanowień licencyjnych, skontaktuj się z właścicielem pakietu bezpośrednio, korzystając z linku **właściciele kontaktu** na stronie pakietu NuGet.org. Firma Microsoft nie udziela licencji jakiejkolwiek własności intelektualnej od dostawców pakietów innych firm i nie ponosi odpowiedzialności za informacje udostępniane przez strony trzecie.

## <a name="managing-packages-on-nugetorg"></a>Zarządzanie pakietami na NuGet.org

**Czy mogę edytować metadane pakietu po ich przekazaniu?**

Pakiet NuGet zaleca wszystkie pakiety, które mają być podpisane. Zasada projektowania podpisywania pakietów polega na tym, że zawartość podpisanego pakietu musi być niezmienna, która obejmuje nuspec. Edytowanie metadanych pakietu skutkuje zmianami w nuspec, unieważnienie istniejących sygnatur. Zalecamy modyfikowanie istniejących przepływów pracy, aby nie wymagały edytowania metadanych pakietu po utworzeniu pakietu.

Należy zauważyć, że zależności wymienione dla pakietu są generowane automatycznie na podstawie samego pakietu i nie można ich edytować.

Ponadto przekazywanie pakietów do [int.nugettest.org](https://int.nugettest.org) jest doskonałym sposobem testowania i weryfikowania pakietu bez udostępniania pakietu w publicznej galerii. Punkt końcowy interfejsu API: https://apiint.nugettest.org/v3/index.json

**Czy mogę usunąć pakiet opublikowany do NuGet.org?**

Ogólnie rzecz biorąc, nie obsługujemy usuwania pakietu opublikowanego w NuGet.org. Przeczytaj więcej na temat naszych [zasad usuwania pakietów](policies/deleting-packages.md).

**Czy można zarezerwować nazwy pakietów, które będą publikowane w przyszłości?**

Tak. Identyfikatory pakietów na [NuGet.org](https://www.nuget.org/) można zarezerwować, żądając prefiksu identyfikatora pakietu dla Twojego konta. Aby zażądać prefiksu identyfikatora pakietu, postępuj zgodnie z instrukcjami w [dokumentacji](id-prefix-reservation.md).

**Jak mogę przejąć prawa własności dla pakietów?**

Zobacz [Zarządzanie właścicielami pakietów w witrynie NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).

**Jak mogę się z właścicielem pakietu, który narusza moją licencję na oprogramowanie?**

Zachęcamy społeczność programu NuGet do współpracy ze sobą w celu rozwiązania wszelkich sporów, które mogą powstać między właścicielami pakietu i właścicielami innego oprogramowania. Przed zapytaniem administratorów NuGet.org o intercede, został przygotowany proces rozstrzygania [sporów](policies/dispute-resolution.md) .

**Czy zalecamy przekazanie moich pakietów testowych do NuGet.org?**

Do celów testowych można używać [int.nugettest.org](https://int.nugettest.org)lub alternatywnych publicznych serwerów NuGet, takich jak [MyGet.org](https://myget.org) lub [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Zwróć uwagę, że pakiety przekazane do int.nugettest.org mogą nie zostać zachowane.

**Jaki jest maksymalny rozmiar pakietów, które mogę przekazać do NuGet.org?**

NuGet.org zezwala na pakiety do 250 MB, ale zalecamy utrzymywanie pakietów z 1 MB, jeśli to możliwe, i używanie zależności do łączenia pakietów ze sobą. Jako zasada elementu kciuka pakiety zawierają tylko jeden zestaw, aby uniknąć kolizji.

Pakiet NuGet korzysta z protokołu HTTP do pobierania pakietów, dlatego większe pakiety mają większe prawdopodobieństwo niepowodzenia instalacji niż mniejsze.

Istnieje możliwość współdzielenia zależności między wieloma pakietami, dzięki czemu łączny rozmiar plików dla klientów pakietów NuGet jest mniejszy.

Zależności są głównie statyczne i nigdy nie zmieniają się. W przypadku naprawienia usterki w kodzie zależności mogą nie być aktualizowane. W przypadku współdzielenia zależności należy zawsze przedostawować większe pakiety za każdym razem. Dzieląc pakiety NuGet na powiązane zależności, uaktualnienia są znacznie bardziej szczegółowe dla użytkowników pakietu.

## <a name="nugetorg-not-accessible"></a>NuGet.org niedostępne

**Dlaczego nie można pobrać pakietów z pakietów ani przekazać ich do NuGet.org?**

Najpierw upewnij się, że korzystasz z najnowszych wersji programu NuGet. Jeśli ta wersja będzie nadal kończyć się niepowodzeniem, [skontaktuj się z pomocą techniczną](https://www.nuget.org/policies/Contact) i podaj dodatkowe informacje dotyczące rozwiązywania problemów z połączeniem:

- Używana wersja programu NuGet
- Używane źródła pakietów
- Dziennik przywracania z szczegółowym szczegółowośćem
- MTR lub ślady programu Fiddler (patrz poniżej)
- Obszar geograficzny
- Czy komputer znajduje się za serwerem proxy czy zaporą?
- Czy Twoja maszyna znajduje się w centrum danych dostawców chmury (Azure, AWS itp.)? Jeśli tak, podaj nazwę dostawcy i region.

*Aby przechwycić MTR:*

- Pobierz [winmtr](https://sourceforge.net/projects/winmtr/files/WinMTR-v092.zip/download).
- Wprowadź `api.nuget.org` jako nazwę hosta, a następnie kliknij przycisk **Uruchom**.
- Zaczekaj na > **wysłanej** kolumny = 100.

    ![Przechwytywanie MTR](media/mtr.png)

- Kopiuj tekst do Schowka.

*Aby przechwycić programu Fiddler:*

- Zainstaluj najnowszą wersję programu [programu Fiddler](https://www.telerik.com/download/fiddler).
- Uruchom programu Fiddler i Wyłącz przechwytywanie ruchu za pomocą menu **plik > przechwytywanie ruchu** .
- Usuń wszystkie sesje (zaznacz wszystkie elementy na liście, a następnie naciśnij klawisz **delete** ).
- Skonfiguruj programu Fiddler do przechwytywania ruchu HTTPS przez sprawdzenie **odszyfrowywania ruchu https** na karcie **https** **narzędzi > programu Fiddler opcje..** .
- Zamknij program Visual Studio.
- Włącz menu **ruch > przechwytywania plików** .
- Uruchom program Visual Studio lub NuGet. exe. exe i wykonaj akcje, które nie działają. Ruch generowany przez te akcje powinien być widoczny w programu Fiddler.
- Po uruchomieniu akcji Użyj **pliku > zapisz > wszystkie sesje** do przechowywania przechwyconych sesji.

Uwaga: może być konieczne ustawienie zmiennej środowiskowej `HTTP_PROXY` na `http://127.0.0.1:8888` do routingu ruchu NuGet za pomocą programu Fiddler.

Jeśli to się nie powiedzie, wypróbuj [porady wymienione w tym wpisie StackOverflow](https://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

## <a name="nugetorg-account-management"></a>Zarządzanie kontami NuGet.org

### <a name="how-to-recover-nugetorg-password-login"></a>Jak odzyskać logowanie za NuGet.org hasła?

Należy pamiętać, że [Logowanie przy użyciu hasła NuGet.org zostało wycofane](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) i jedynym sposobem zalogowania się do usługi NuGet.org jest konto usługi konto Microsoft (MSA) lub Azure Active Directory (AAD). Jeśli jednak nie masz dostępu do skojarzonych kont MSA/AAD, może być konieczne użycie logowania za pomocą hasła w celu odzyskania konta usługi NuGet.org. W tej sytuacji postępuj zgodnie z poniższymi instrukcjami.
- **Wymaganie:** Musisz mieć dostęp do wiadomości e-mail, która jest skojarzona z kontem, dla którego jest wymagane odzyskanie hasła.
- Przejdź do [strony zapomnianego hasła](https://www.nuget.org/account/ForgotPassword)
- Wprowadź adres **e-mail** skojarzony z kontem NuGet.org, które chcesz odzyskać.
- Kliknij przycisk **Wyślij** .
- Zostanie wysłana wiadomość e-mail do określonego konta adresu e-mail z linkiem umożliwiającym zresetowanie hasła. Kliknij ten link, a następnie ustaw nowe hasło. Jeśli nie możesz znaleźć wiadomości e-mail, sprawdź folder wiadomości-śmieci.
- Po wykonaniu tych czynności możesz teraz zalogować się przy użyciu nazwy użytkownika/hasła w programie NuGet.
- Aby zalogować się przy użyciu nazwy użytkownika/hasła, Użyj linku **Zaloguj się przy użyciu konta NuGet.org** na [stronie logowania usługi NuGet.org](https://www.nuget.org/users/account/LogOn).

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Która konto Microsoft jest połączona z moim kontem NuGet.org?

Jeśli nie pamiętasz, która konto Microsoft jest skojarzona z kontem NuGet.org, wykonaj poniższe kroki, aby uzyskać pomoc.
1. Przejdź do [strony logowania NuGet.org](https://www.nuget.org/users/account/LogOn) i kliknij opcję **potrzebna pomoc w logowaniu?**
1. Spowoduje to wyświetlenie okna dialogowego podręcznego w celu uzyskania pomocy. Postępuj zgodnie z instrukcjami w tym oknie dialogowym, aby zrozumieć skojarzone konto Microsoft konta usługi NuGet.org.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Jak zmienić konto Microsoft używany na potrzeby logowania NuGet.org?
Jeśli chcesz zmienić konto Microsoft dla użytkownika NuGet.org, wykonaj poniższe kroki. Umożliwia rozmówienie konto Microsoft za pomocą poczty e-mail `account1@outlook.com` jest skojarzony z kontem NuGet.org z nazwą użytkownika `MyNuGetAccount`. Chcesz zmienić nazwę logowania na inną konto Microsoft za pomocą poczty e-mail `account2@outlook.com`
1. Zaloguj się przy użyciu **obecnie skojarzonych konto Microsoft** , na przykład `account1@outlook.com` na [stronie logowania](https://www.nuget.org/users/account/LogOn) po kliknięciu **Zaloguj się przy użyciu konta Microsoft**.
1. Po zalogowaniu przejdź do strony [ustawień konta](https://www.nuget.org/account) .
1. Rozwiń sekcję dla **konta logowania**. Kliknij przycisk **Zmień konto** .
1. Nastąpi przekierowanie do strony logowania firmy Microsoft. Zaloguj się przy użyciu konta, na które chcesz zmienić skojarzenie, na przykład `account2@outlook.com`. **Uwaga**: aby móc zalogować się przy użyciu innego konto Microsoft, może być konieczne kliknięcie przycisku **Wyloguj i zalogowanie się przy użyciu innego konta** .
1. Jeśli zobaczysz błąd podobny do poniższego, zobacz [konto Microsoft jest połączony z innym kontem NuGet.org](#microsoft-account-is-linked-with-another-nugetorg-account) , aby uzyskać więcej szczegółów.
    >_Nie można zaktualizować konto Microsoft przy użyciu "account2 <account2@outlook.com>". Taka sytuacja może wystąpić, jeśli jest już połączona z innym kontem NuGet. Skontaktuj się z pomocą techniczną, aby uzyskać więcej informacji._

1. Po pomyślnym zalogowaniu się przy użyciu drugiego konta nastąpi przekierowanie z powrotem do strony ustawień konta NuGet.org, a następnie zobaczysz nowe konto Microsoft skojarzone jako konto logowania. Przechodzenie do przodu powinno być używane podczas logowania się do usługi NuGet.org.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Konto Microsoft jest połączony z innym kontem NuGet.org.

Jeśli podjęto próbę zmiany nazwy logowania firmy Microsoft i wystąpił następujący błąd:
> _Nie można zaktualizować konto Microsoft przy użyciu "account2 <account2@outlook.com>". Taka sytuacja może wystąpić, jeśli jest już połączona z innym kontem NuGet. Skontaktuj się z pomocą techniczną, aby uzyskać więcej informacji._

Pozwala na to, że podjęto próbę zmiany konto Microsoft logowaniu z `account1@outlook.com` dla użytkownika NuGet.org o nazwie username `MyNuGetAccount1` na inny konto Microsoft z wiadomościami e-mail `account2@outlook.com`. Zobaczysz błąd powyżej.

**Co oznacza błąd powyżej?**

Oznacza to, że istnieje inne konto NuGet.org, które jest skojarzone z konto Microsoftem, które próbujesz zmienić. w powyższym przykładzie konto Microsoft z wiadomościami e-mail `<account2@outlook.com>` jest skojarzona z innym kontem NuGet.org przy użyciu nazwy użytkownika, powiedzmy, @no__ t-1.

Nie można zmienić skojarzonej nazwy logowania na konto Microsoft, która jest połączona z innym kontem NuGet.org.

**Nie pamiętam innego konta NuGet.org, w jaki sposób mogę sprawdzić, które konto NuGet.org jest?**

Zaloguj się przy użyciu drugiego konto Microsoft na [stronie logowania](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "Strona logowania"). Spowoduje to zalogowanie się do konta NuGet.org, które jest aktualnie skojarzone z drugim konto Microsoft. Następnie można wyświetlić przekazane pakiety i wykonać Zarządzanie kontem na tym koncie.

**Nie myślę o tym drugim koncie usługi NuGet.org, chcę zmienić nazwę logowania dla pierwszego konta usługi NuGet.org z drugim konto Microsoft. Co mam zrobić?**

Jeśli chcesz, aby nie zadbać o drugie konto NuGet.org i nadal chcesz ponownie używać skojarzonych konto Microsoft z wiadomościami e-mail `account2@outlook.com`. 

Skojarzenie można zwolnić między konto Microsoft i konta NuGet.org przez usunięcie konta NuGet.org.
1. Postępuj zgodnie z instrukcjami, aby [usunąć użytkownika](#how-to-delete-my-nugetorg-account) dla drugiego konta NuGet.org `MyNuGetAccount2`. 
1. Po usunięciu tego konta możesz ponowić procedurę, aby [zmienić konto Microsoft logowanie](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**Poczekaj, pamiętaj o tym drugim koncie. Nie chcę stracić tego konta, ale Zmień moje nazwy logowania skojarzonego konta na pierwsze.**

Musisz utworzyć lub użyć trzeciego konto Microsoft, powiedzmy, używając poczty e-mail `account3@outlook.com`. 
1. Najpierw należy zalogować się przy użyciu drugiego konto Microsoft, `account2@outlook.com` w NuGet.org. Postępuj zgodnie z powyższymi krokami, aby zmienić skojarzone nazwy logowania i skojarzyć trzecią konto Microsoft z tym kontem NuGet.org.
1. Po wykonaniu tej czynności drugi konto Microsoft z wiadomościami e-mail `account2@outlook.com` będzie bezpłatny do skojarzenia z pierwszym kontem NuGet.org, `MyNuGetAccount1`. Wykonaj te same kroki, aby zmienić nazwy logowania firmy Microsoft na drugą konto Microsoft.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Zalogowanie się za pomocą konto Microsoft pokazuje, że mój adres e-mail jest połączony z innym konto Microsoft

Jeśli podjęto próbę zalogowania się przy użyciu konto Microsoft, powiedzmy, używając adresu e-mail `account1@outlook.com` i zobaczysz błąd podobny do poniższego:
> _Konto z adresem e-mail "account1@outlook.com" jest połączone z innym kontem Microsoft._
>
> _Jeśli chcesz zaktualizować połączone konto Microsoft, możesz to zrobić na stronie Ustawienia konta._

**Co oznacza błąd powyżej?**

Po utworzeniu konta w usłudze NuGet.org istnieje adres e-mail komunikacji skojarzony z tym kontem. Jest to zazwyczaj takie samo, jak adres e-mail używany dla skojarzonych konto Microsoft. Można jednak wybrać inny adres e-mail na potrzeby komunikacji. Dlatego technicznie możesz mieć różne konto Microsoft, poinformowanie o `account2@outlook.com` połączonej z kontem NuGet.org z adresem e-mail komunikacji jako `account1@outlook.com`.

Ten błąd oznacza, że już istnieje konto NuGet.org o adresie e-mail komunikacji `account1@outlook.com`, ale jest ono skojarzone z innym konto Microsoft za pomocą wiadomości e-mail **, która nie jest** `account1@outlook.com`.

**Jak mogę znaleźć, która konto Microsoft jest połączona z tym kontem NuGet.org?**

Aby ustalić, która konto Microsoft jest połączona z kontem NuGet.org przy użyciu adresu e-mail `account1@outlook.com`, należy użyć przepływu pomocy dotyczącego [logowania](#which-microsoft-account-is-linked-to-my-nugetorg-account) .

**Chcę przesłonić to konto za pomocą konto Microsoft**

Wykonaj kroki opisane w sekcji [nie można użyć logowania do firmy Microsoft, jak odzyskać sekcję konta NuGet.org,](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) aby skojarzyć konto Microsoft z istniejącym kontem NuGet.org.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Nie można użyć identyfikatora logowania firmy Microsoft, jak odzyskać konto NuGet.org?

Jeśli podjęto próbę skorzystania z [pomocy przy logowaniu](#which-microsoft-account-is-linked-to-my-nugetorg-account) i nie masz dostępu do konto Microsoft skojarzonej z Twoim kontem usługi NuGet.org, wykonaj poniższe kroki, aby połączyć nowe konto Microsoft z kontem NuGet.org.
1. **Wymaganie**: będzie potrzebny dostęp do konto Microsoft, który nie jest skojarzony z żadnym z istniejących kont NuGet.org. Jeśli go nie masz, możesz go [utworzyć](https://signup.live.com) .
2. Jeśli nie pamiętasz nazwy użytkownika i hasła do konta usługi NuGet.org, postępuj zgodnie z instrukcjami, [Aby odzyskać logowanie](#how-to-recover-nugetorg-password-login)przy użyciu hasła.
3. [Zaloguj się do NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) przy użyciu nazwy użytkownika/hasła logowania.
4. Po zalogowaniu zostanie wyświetlone okno podręczne wyświetlane poniżej. To jest okno dialogowe niekontynuacja hasła.
5. **Uwaga**: zignoruj instrukcję, aby zalogować się przy użyciu podanej konto Microsoft. Teraz możesz połączyć konto NuGet.org z innymi identyfikatorami logowania firmy Microsoft.
6. Kliknij przycisk **Zaloguj się przy użyciu konta Microsoft** i zaloguj się przy użyciu konto Microsoft, do którego masz dostęp, jak wspomniano w kroku 1.
7. Twoje konto zostanie teraz połączone z nowym konto Microsoft, którego możesz użyć do zalogowania się do usługi NuGet.org.

    ![Okno dialogowe linku MSA](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Jak przekształcić moje konto NuGet.org w organizację?

Jeśli chcesz przekształcić konto w organizację, a to konto jest już skojarzone z logowaniem konto Microsoft, wykonaj kroki podane w dokumentacji dotyczącej [organizacji na platformie NuGet](organizations-on-nuget-org.md).

Jeśli jednak konto NuGet.org nie jest skojarzone/połączone z konto Microsoft, możesz wykonać poniższe kroki, aby przekształcić to konto w organizację.
1. **Wymaganie**: musisz najpierw utworzyć konto w usłudze NuGet.org, które będzie używane jako administrator na koncie organizacji. Jeśli go nie masz, [Utwórz nowe konto NuGet.org](individual-accounts.md)
2. Wykonaj [kroki w celu odzyskania hasła logowania](#how-to-recover-nugetorg-password-login) do konta usługi NuGet.org, jeśli nie masz dla niego hasła logowania, Pomiń ten krok.
3. [Zaloguj się do NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) przy użyciu nazwy użytkownika/hasła logowania.
4. Po zalogowaniu zostanie wyświetlone okno podręczne wyświetlane poniżej. To jest okno dialogowe niekontynuacja hasła. 
    > [!Important]
    > Zignoruj to okno dialogowe, **nie** klikaj przycisku **Zaloguj się przy użyciu konta Microsoft** .

5. Przejdź do [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform). Umożliwi to konwertowanie konta NuGet.org na organizacji bez łączenia się z konto Microsoft.
6. Określ nazwę użytkownika administratora dla konta osobistego NuGet.org/konto utworzone w kroku 1.
7. Postępuj zgodnie z instrukcjami, aby zakończyć transformację tego konta w organizacji.

    ![Okno dialogowe linku MSA](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>NuGet.org problemy z logowaniem dla kont usługi AAD z niezarządzaną dzierżawą?

Jeśli zobaczysz błąd podobny do poniższego podczas przepływu logowania przy użyciu domeny konta e-mail (@yourdomain.com), zobacz poniższe kroki, aby odzyskać konto NuGet.org.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**Co to jest stan niezarządzany podczas logowania? Co się dzieje teraz?** 

Twoje konto prawdopodobnie zostało wcześniej zarejestrowane jako konto Microsoft osobiste i działało prawidłowo, jednak teraz wygląda na to, że Twoje konto zostało zarejestrowane jako dzierżawa "niezarządzana" w Azure Active Directory (usługa tożsamości używana do uwierzytelniania Konta Microsoft). 

Mogło to nastąpić, jeśli ty lub ktoś z Twojej organizacji (o adresie e-mail @yourdomain.com) zarejestrowano w jednej z usług zintegrowanych z usługą AAD lub zakończyło się samoobsługowym [rejestracją w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-self-service-signup), co tworzy taką niezarządzaną dzierżawę dla użyto konto Microsoft domeny (@yourdomain.com w Twoim przypadku). 

**Co mogę zrobić, aby odzyskać moje konto?**

W tej chwili nie istnieje Metoda (NuGet.org) do uwierzytelniania kont z takimi niezarządzanymi kontami dzierżaw w usłudze Azure Active Directory. Przeglądamy do lepszego sposobu uwierzytelniania takich kont.

Jeśli chcesz zalogować się do usługi NuGet.org przy użyciu konto Microsoft (@yourdomain.com), użytkownik (lub administrator w firmie) będzie musiał przejąć prawo własności do usługi AAD, wykonując weryfikację DNS w celu uwierzytelnienia użytkowników z adresem e-mail "@yourdomain.com". Postępuj zgodnie z instrukcjami dla [domen przejęcia przez administratora](https://docs.microsoft.com/azure/active-directory/users-groups-roles/domains-admin-takeover) przez usługę Azure Active Directory. Po wykonaniu tej czynności normalne logowanie powinno zacząć działać.

**Nie chcę nic robić, co jest innym sposobem na odzyskanie mojego konta?**

Można [utworzyć](https://www.microsoft.com/account) nowy konto Microsoft (z adresem e-mail, który **nie** jest skojarzony z @yourdomain.com). Wykonaj czynności podane w sekcji [Odzyskiwanie konta NuGet.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) .

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Jak mogę zmienić nazwy użytkownika konta NuGet.org?

Nie możesz. Zgodnie z zasadami nie zezwalamy na zmianę nazw użytkowników. Jedynym sposobem zmiany nazwy użytkownika jest utworzenie nowego konta z odpowiednią nazwą użytkownika. Zalecamy usunięcie istniejących kont przed utworzeniem nowego konta. w przeciwnym razie nie będzie można ponownie użyć zarejestrowanych konto Microsoft.
> [!Important]
> Usunięcie użytkownika nadal **rezerwuje** `username`. Nie będziesz w stanie ponownie ponownie używać tej samej nazwy użytkownika i **obejmuje ona zmianę wielkości liter**. Jeśli na przykład utworzono użytkownika o nazwie użytkownika `mycoolname` i chcesz zmienić go na `MyCoolName` (zmiany wielkości liter), nie będzie możliwe po usunięciu użytkownika.

Wykonaj czynności podane w sekcji [usuwanie konta NuGet.org](#how-to-delete-my-nugetorg-account) i [Zarejestruj nowe konto](individual-accounts.md) o prawidłowej nazwie użytkownika.

### <a name="how-to-delete-my-nugetorg-account"></a>Jak usunąć konto NuGet.org?

Aby usunąć konto, należy pamiętać, że zalecamy przeniesienie własności wszelkich pakietów, w których jesteś jedynym właścicielem. Więcej informacji na temat [zarządzania właścicielami pakietów](https://docs.microsoft.com/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg) można znaleźć w artykule na temat tego, jak to zrobić. Pomoże to również przyspieszyć Twoje żądanie.

Jeśli zamierzasz przekształcić Twoje konto w organizację, wykonaj czynności podane w [sekcji przekształcanie mojego konta NuGet.org w organizacji](#how-to-transform-my-nugetorg-account-to-an-organization).

> [!Important]
> Usunięcie użytkownika spowoduje następujące skutki:
>  1. Twoja nazwa użytkownika będzie zastrzeżona i nie będzie można jej ponownie używać do tworzenia konta pojedynczego lub konta organizacji
>  1. Odwołaj skojarzone klucze interfejsu API. 
>  1. Usuń konto jako właściciela dla wszystkich pakietów podrzędnych.
>  1. Usuń skojarzenie wszystkich wcześniej istniejących rezerwacji prefiksów identyfikatorów z tym kontem.
>  1. Usuń konto jako członka każdej organizacji.

Wykonaj następujące kroki, aby kontynuować usuwanie konta.
1. [Zaloguj się do NuGet.org](https://www.nuget.org/users/account/LogOn) przy użyciu konta, które chcesz usunąć.
2. Kliknij ten adres URL: [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete) i postępuj zgodnie z instrukcjami, aby przesłać żądanie usunięcia konta.

Nasza obsługa klienta będzie przetwarzać to żądanie i przeprowadzać usuwanie konta.
