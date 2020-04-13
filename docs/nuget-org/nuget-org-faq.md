---
title: NuGet.org często zadawane pytania
description: Typowe pytania i odpowiedzi dotyczące pracy z galerią NuGet.
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 915f6e4cfc0b21d2b10006c62e8230720d07ce74
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428906"
---
# <a name="nugetorg-frequently-asked-questions"></a>NuGet.org często zadawane pytania

## <a name="license-terms"></a>Postanowienia licencyjne

**Jakie są domyślne postanowienia licencyjne, jeśli pakiet nie zawiera określonych informacji o licencji?**

Każdy pakiet jest regulowany przez warunki, które są dołączone do pakietu. Użytkownik powinien zapoznać się z obowiązującymi warunkami przed uzyskaniem dostępu do pakietów, pobraniem lub nabyciem ich. Na NuGet.org użyj łącza **Informacje o licencji** na stronie pakietu.

Jeśli pakiet nie określa warunków licencjonowania, skontaktuj się z właścicielem pakietu bezpośrednio za pomocą łącza **Skontaktuj się z właścicielami** na stronie NuGet.org pakiet. Firma Microsoft nie udziela licencji na żadne prawa własności intelektualnej od zewnętrznych dostawców pakietów i nie ponosi odpowiedzialności za informacje dostarczone przez osoby trzecie.

## <a name="managing-packages-on-nugetorg"></a>Zarządzanie pakietami na NuGet.org

**Czy mogę edytować metadane pakietu po jego przesłaniu?**

NuGet zaleca podpisanie wszystkich pakietów. Zasada projektowania podpisywania pakietów jest, że podpisana zawartość pakietu musi być niezmienne, który obejmuje nuspec. Edytowanie metadanych pakietu powoduje zmiany w nuspec, unieważniając istniejące podpisy. Zaleca się modyfikowanie istniejących przepływów pracy, aby nie wymagać edycji metadanych pakietu po utworzeniu pakietu.

Należy zauważyć, że zależności wymienione dla pakietu są generowane automatycznie z samego pakietu i nie można edytować.

Ponadto przesyłanie pakietów do [int.nugettest.org](https://int.nugettest.org) to świetny sposób na przetestowanie i sprawdzenie poprawności pakietu bez udostępniania pakietu w galerii publicznej. Punkt końcowy interfejsu API:https://apiint.nugettest.org/v3/index.json

**Czy mogę usunąć pakiet opublikowany w NuGet.org?**

Ogólnie rzecz biorąc nie obsługujemy usuwania pakietu opublikowanego w celu NuGet.org. Dowiedz się więcej o naszych [zasadach usuwania pakietów](policies/deleting-packages.md).

**Czy można zarezerwować nazwy pakietów, które zostaną opublikowane w przyszłości?**

Tak. Możesz zarezerwować identyfikatory dla pakietów na [NuGet.org,](https://www.nuget.org/) żądając prefiksu identyfikatora pakietu dla swojego konta. Aby zażądać prefiksu identyfikatora pakietu, postępuj zgodnie z instrukcjami [zawartymi](id-prefix-reservation.md)w dokumentacji .

**Jak ubiegać się o własność pakietów?**

Zobacz [Zarządzanie właścicielami pakietów w NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).

**Jak poradzić sobie z właścicielem pakietu, który narusza moją licencję na oprogramowanie?**

Zachęcamy społeczność NuGet do współpracy w celu rozwiązania wszelkich sporów, które mogą pojawić się między właścicielami pakietów a właścicielami innego oprogramowania. Stworzyliśmy proces [rozstrzygania sporów,](policies/dispute-resolution.md) który należy wykonać, zanim poprosimy administratorów NuGet.org o wstawienie się.

**Czy zaleca się przesyłanie pakietów testowych do NuGet.org?**

Do celów testowych można użyć [int.nugettest.org](https://int.nugettest.org)lub alternatywnych publicznych serwerów NuGet, takich jak [myget.org](https://myget.org) lub [Azure DevOps.](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/)

Należy pamiętać, że pakiety przesłane do int.nugettest.org mogą nie zostać zachowane.

**Jaki jest maksymalny rozmiar pakietów, które mogę przesłać do NuGet.org?**

NuGet.org umożliwia pakiety do 250 MB, ale zalecamy przechowywanie pakietów poniżej 1 MB, jeśli to możliwe i używanie zależności do łączenia pakietów. Zgodnie z zasadą pakiety zawierają tylko jeden zestaw, aby uniknąć kolizji.

NuGet używa protokołu HTTP do pobierania pakietów, więc większe pakiety mają większe prawdopodobieństwo nieudanych instalacji niż mniejsze.

Istnieje możliwość współużytkowanie zależności między wieloma pakietami, dzięki czemu całkowity rozmiar pobierania dla konsumentów pakietów NuGet mniejsze.

Zależności są głównie statyczne i nigdy się nie zmieniają. Podczas naprawiania błędu w kodzie zależności mogą nie wymagać aktualizacji. Jeśli pakiet zależności, kończy się reshipping większych pakietów za każdym razem. Dzieląc pakiety NuGet na powiązane zależności, uaktualnienia są znacznie bardziej szczegółowe dla konsumentów pakietu.

## <a name="nugetorg-not-accessible"></a>NuGet.org niedostępne

**Dlaczego nie mogę pobierać pakietów z NuGet.org lub przesyłać pakietów?**

Najpierw upewnij się, że używasz najnowszych wersji nuget. Jeśli ta wersja nadal nie powiedzie się, [skontaktuj się z pomocą techniczną](https://www.nuget.org/policies/Contact) i podaj dodatkowe informacje dotyczące rozwiązywania problemów z połączeniem, w tym:

- Wersja programu NuGet, którego używasz
- Źródła pakietów, których używasz
- Dziennik przywracania ze szczegółową szczegółowością
- Ślady MTR lub Fiddler (patrz poniżej)
- Twój obszar geograficzny
- Czy komputer znajduje się za serwerem proxy czy zaporą?
- Czy komputer znajduje się w centrum danych dostawców chmury (Azure, AWS itp.)? Jeśli tak, podaj nazwę dostawcy i regionu.

*Aby uchwycić MTR:*

- Pobierz [WinMTR](https://sourceforge.net/projects/winmtr/files/WinMTR-v092.zip/download).
- Wprowadź `api.nuget.org` jako nazwę hosta i kliknij przycisk **Start**.
- Poczekaj, aż kolumna **Wysłane** zostanie >= 100.

    ![Przechwytywanie MTR](media/mtr.png)

- Kopiowanie tekstu do schowka.

*Aby uchwycić Fiddler:*

- Zainstaluj najnowszą wersję [fiddler](https://www.telerik.com/download/fiddler).
- Uruchom Fiddler i wyłącz przechwytywanie ruchu za pomocą menu **Przechwytywanie ruchu > plik.**
- Usuń wszystkie sesje (zaznacz wszystkie elementy na liście, naciśnij klawisz **Delete).**
- Skonfiguruj Fiddlera do przechwytywania ruchu HTTPS, sprawdzając **odszyfrowywanie ruchu HTTPS** na karcie **HTTPS** w menu **Narzędzia > Fiddler...**
- Zamknij program Visual Studio.
- Włącz menu **Przechwytywanie ruchu > plików.**
- Uruchom program Visual Studio lub nuget.exe .exe i wykonaj akcje, które nie działają. Ruch generowany przez te akcje powinny być wyświetlane w Fiddler.
- Po uruchomieniu akcji użyj **funkcji File > Save > All Sessions** do przechowywania przechwyconych sesji.

Uwaga: może być wymagane ustawienie `HTTP_PROXY` zmiennej `http://127.0.0.1:8888` środowiskowej do routingu ruchu NuGet za pośrednictwem fiddler.

Jeśli to się nie powiedzie, wypróbuj [wskazówki wymienione w tym poście StackOverflow](https://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

## <a name="nugetorg-account-management"></a>zarządzanie NuGet.org kontami

### <a name="how-to-recover-nugetorg-password-login"></a>Jak odzyskać NuGet.org login z hasłem?

Należy pamiętać, że [NuGet.org Logowanie hasłem zostało przerwane,](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) a jedynym sposobem zalogowania się do NuGet.org jest osobiste konto Microsoft (MSA) lub konto Usługi Azure Active Directory (AAD). Jednak w przypadku, gdy nie możesz uzyskać dostępu do powiązanych kont MSA/AAD, może być konieczne użycie hasła logowania do odzyskiwania konta NuGet.org. W tej sytuacji wykonaj poniższe kroki.
- **Wymaganie:** Musisz mieć dostęp do wiadomości e-mail skojarzonej z kontem, dla którego musisz odzyskać hasło.
- Przejdź do [strony Nie pamiętałem hasła](https://www.nuget.org/account/ForgotPassword)
- Wprowadź adres **e-mail** skojarzony z kontem NuGet.org, który chcesz odzyskać.
- Kliknij przycisk **Wyślij.**
- Otrzymasz wiadomość e-mail na określone konto adresu e-mail z linkiem do zresetowania hasła. Kliknij ten link i ustaw nowe hasło. Jeśli nie możesz znaleźć poczty, sprawdź folder "śmieci".
- Po zakończeniu możesz teraz zalogować się przy użyciu nazwy użytkownika/hasła na NuGet.
- Aby zalogować się przy użyciu nazwy użytkownika/hasła, użyj linku **Zaloguj się za pomocą Nuget.org konta** na stronie logowania [NuGet.org](https://www.nuget.org/users/account/LogOn).

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Które konto Microsoft jest połączone z moim kontem NuGet.org?

Jeśli nie pamiętasz, które konto Microsoft jest powiązane z Twoim kontem NuGet.org, wykonaj poniższe czynności, aby uzyskać pomoc.
1. Przejdź do [NuGet.org strony logowania](https://www.nuget.org/users/account/LogOn) i kliknij **łącze Potrzebujesz pomocy, logując się?**
1. Spowoduje to wyświetlenie wyskakującym oknie dialogowym pomocy. Wykonaj czynności opisane w tym oknie dialogowym, aby zrozumieć skojarzone konta Microsoft dla twojego konta NuGet.org.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Jak zmienić konto Microsoft, którego używam do NuGet.org logowania?
Jeśli chcesz zmienić konto Microsoft dla NuGet.org użytkownika, wykonaj poniższe czynności. Załóżmy, że `account1@outlook.com` Twoje konto Microsoft z pocztą e-mail jest skojarzone z Twoim kontem NuGet.org z nazwą użytkownika. `MyNuGetAccount` Chcesz zmienić login na inne konto Microsoft za pomocą poczty e-mail`account2@outlook.com`
1. Zaloguj się przy użyciu **aktualnie skojarzonego konta Microsoft,** czyli `account1@outlook.com` na [stronie logowania](https://www.nuget.org/users/account/LogOn) po kliknięciu przycisku Zaloguj się za pomocą firmy **Microsoft**.
1. Po zalogowaniu się przejdź na stronę [ustawień konta.](https://www.nuget.org/account)
1. Rozwiń sekcję **dla konta logowania**. Kliknij przycisk **Zmień konto.**
1. Zostaniesz przekierowany do strony logowania microsoft. Zaloguj się za pomocą konta, na które chcesz zmienić skojarzenie na `account2@outlook.com`tj. **Uwaga:** może być konieczne **kliknięcie przycisku Wyloguj się i zalogowanie się przy innym koncie** podczas przepływu logowania, aby móc zalogować się przy pomocy innego konta Microsoft.
1. Jeśli widzisz błąd, jak poniżej, zobacz [Konto Microsoft jest połączone z innym kontem NuGet.org, aby](#microsoft-account-is-linked-with-another-nugetorg-account) uzyskać więcej szczegółów.
    >_Nie można zaktualizować konta Microsoft za <account2@outlook.com>pomocą 'account2'. Może się to zdarzyć, jeśli jest już połączony z innym kontem NuGet. Aby uzyskać więcej informacji, skontaktuj się z pomocą techniczną._

1. Po pomyślnym zalogowaniu się za pomocą drugiego konta zostaniesz przekierowany z powrotem na stronę ustawień konta NuGet.org, a teraz powinieneś zobaczyć nowe konto Microsoft skojarzone jako konto logowania. W przyszłości należy użyć tego konta podczas logowania się do NuGet.org.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Konto Microsoft jest połączone z innym kontem NuGet.org.

Jeśli próbowałeś zmienić swój login firmy Microsoft i zobaczyłeś błąd poniżej:
> _Nie można zaktualizować konta Microsoft za <account2@outlook.com>pomocą 'account2'. Może się to zdarzyć, jeśli jest już połączony z innym kontem NuGet. Aby uzyskać więcej informacji, skontaktuj się z pomocą techniczną._

Powiedzmy, że próbowałeś zmienić `account1@outlook.com` login konta Microsoft z `MyNuGetAccount1` NuGet.org użytkownika z `account2@outlook.com`nazwą użytkownika na inne konto Microsoft z pocztą e-mail . I widzisz błąd powyżej.

**Co oznacza powyższy błąd?**

Oznacza to, że istnieje inny NuGet.org konto, które jest skojarzone z kontem Microsoft, które próbujesz zmienić `<account2@outlook.com>` na czyli w powyższym przykładzie konto `MyNuGetAccount2`Microsoft z pocztą e-mail jest skojarzone z innym kontem NuGet.org z, powiedzmy, nazwą użytkownika .

Nie można zmienić skojarzonego logowania za pomocą konta Microsoft połączonego z innym kontem NuGet.org.

**Zapomniałem, że mam inne konto NuGet.org, jak mogę dowiedzieć się, które konto NuGet.org jest?**

Zaloguj się za pomocą drugiego konta Microsoft na [stronie logowania](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "strona logowania"). Spowoduje to zalogowanie użytkownika do konta NuGet.org, które jest obecnie skojarzone z drugim kontem Microsoft. Następnie można wyświetlić przekazane pakiety i wykonać zarządzanie kontem na tym koncie.

**Nie dbam o to drugie konto NuGet.org, chcę zmienić login dla pierwszego NuGet.org konta za pomocą drugiego konta Microsoft. Co mam zrobić?**

Jeśli nie chcesz dbać o drugie konto NuGet.org i nadal chcesz ponownie użyć skojarzonego konta Microsoft z pocztą e-mail `account2@outlook.com`. 

Skojarzenia między kontem Microsoft a kontem NuGet.org można zwolnić, usuwając konto NuGet.org.
1. Wykonaj kroki, aby [usunąć użytkownika](#how-to-delete-my-nugetorg-account) dla drugiego `MyNuGetAccount2`konta NuGet.org . 
1. Po usunięciu tego konta można ponowić próbę zmiany logowania do [konta Microsoft](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**Czekaj, zależy mi też na tym drugim koncie. Nie chcę stracić tego konta, ale zmienić moje powiązane loginy do konta dla pierwszego konta.**

Musisz utworzyć / użyć trzeciego konta Microsoft, powiedzmy, z pocztą e-mail `account3@outlook.com`. 
1. Najpierw należy zalogować się za `account2@outlook.com` pomocą drugiego konta Microsoft, na NuGet.org. Wykonaj powyższe kroki, aby zmienić skojarzone logowania i skojarzyć trzecie konto Microsoft z tym kontem NuGet.org.
1. Po zakończeniu, drugie konto `account2@outlook.com` Microsoft z pocztą e-mail może być `MyNuGetAccount1`powiązane z pierwszym kontem NuGet.org, . Wykonaj te same kroki powyżej, aby zmienić loginy microsoft do drugiego konta Microsoft.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Logowanie się za pomocą konta Microsoft pokazuje, że mój adres e-mail jest połączony z innym kontem Microsoft

Jeśli próbowałeś zalogować się za pomocą konta `account1@outlook.com` Microsoft, powiedzmy, za pomocą poczty e-mail i zobaczysz błąd, taki jak poniżej:
> _Konto z pocztąaccount1@outlook.come-mail ' ' jest połączone z innym kontem Microsoft._
>
> _Jeśli chcesz zaktualizować połączone konto Microsoft, możesz to zrobić na stronie ustawień konta._

**Co oznacza powyższy błąd?**

Gdy konto jest tworzone w NuGet.org, z tym kontem jest skojarzony adres e-mail komunikacji. Zwykle jest to taki sam adres e-mail używany dla skojarzonego konta Microsoft. Można jednak określić inny adres e-mail do komunikacji. Tak więc, technicznie, możesz mieć inne konto `account2@outlook.com` Microsoft, powiedzmy, że jest połączony `account1@outlook.com`z kontem NuGet.org z adresem e-mail komunikacji jako .

Tak więc powyższy błąd oznacza, że istnieje już NuGet.org `account1@outlook.com` konto z adresem e-mail komunikacji, ale jest skojarzony z innym kontem Microsoft z pocztą e-mail, **która nie** `account1@outlook.com`jest .

**Jak znaleźć konto Microsoft połączone z tym kontem NuGet.org?**

Aby dowiedzieć się, które konto Microsoft jest połączone z kontem NuGet.org, należy `account1@outlook.com`użyć przepływu [pomocy logowania,](#which-microsoft-account-is-linked-to-my-nugetorg-account) aby dowiedzieć się, które konto Microsoft jest połączone z kontem NuGet.org za pomocą adresu e-mail .

**Chcę zastąpić to konto za pomocą mojego konta Microsoft**

Wykonaj czynności opisane w sekcji [Nie można użyć logowania microsoftu, jak odzyskać sekcję NuGet.org konto,](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) aby skojarzyć konto Microsoft z istniejącym kontem NuGet.org.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Nie można użyć microsoft login, jak mogę odzyskać konto NuGet.org?

Jeśli użytkownik próbował skorzystać z [pomocy dotyczącej logowania](#which-microsoft-account-is-linked-to-my-nugetorg-account) i nie ma dostępu do konta Microsoft skojarzonego z twoim kontem NuGet.org, wykonaj poniższe czynności, aby połączyć nowe konto Microsoft z kontem NuGet.org.
1. **Wymaganie:** Będziesz potrzebować dostępu do konta Microsoft, które nie jest skojarzone z istniejącymi kontami NuGet.org. Jeśli go nie masz, możesz go [utworzyć.](https://signup.live.com)
2. Jeśli nie pamiętasz nazwy użytkownika i hasła do swojego konta NuGet.org, wykonaj [czynności, aby odzyskać login hasłem.](#how-to-recover-nugetorg-password-login)
3. [Zaloguj się do NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) przy użyciu loginu nazwy użytkownika/hasła.
4. Po zalogowaniu się zostanie wyświetlone okno dialogowe wyświetlane poniżej. Jest to okno dialogowe wycofywania haseł.
5. **UWAGA:** Zignoruj instrukcję logowania za pomocą określonego konta Microsoft. Teraz możesz połączyć swoje konto NuGet.org z dowolnym innym loginem firmy Microsoft.
6. Kliknij przycisk **Zaloguj się za pomocą firmy Microsoft** i zaloguj się za pomocą konta Microsoft, do którego masz dostęp, jak wspomniano w kroku 1.
7. Twoje konto zostanie teraz połączone z nowym kontem Microsoft, za pomocą którego można zalogować się do NuGet.org w przyszłości.

    ![Okno dialogowe łącza msa](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Jak przekształcić konto NuGet.org w organizację?

Jeśli chcesz przekształcić swoje konto w organizację, a to konto jest już skojarzone z logowaniem do konta Microsoft, wykonaj kroki podane w dokumentacji dla [organizacji nuget org](organizations-on-nuget-org.md).

Jeśli jednak twoje konto NuGet.org nie jest skojarzone/połączone z kontem Microsoft, możesz wykonać poniższe czynności, aby przekształcić to konto w organizację.
1. **Wymaganie:** Musisz najpierw utworzyć indywidualne konto w NuGet.org, aby było używane jako administrator na koncie org. Jeśli go nie masz, [utwórz nowe konto NuGet.org](individual-accounts.md)
2. Wykonaj [kroki, aby odzyskać login do hasła](#how-to-recover-nugetorg-password-login) do konta NuGet.org, jeśli nie masz do niego loginu hasłem, jeśli to zrobisz, pomiń ten krok.
3. [Zaloguj się do NuGet.org](https://www.nuget.org/users/account/LogOnNuGetAccount) przy użyciu loginu nazwy użytkownika/hasła.
4. Po zalogowaniu się zostanie wyświetlone okno dialogowe wyświetlane poniżej. Jest to okno dialogowe wycofywania haseł. 
    > [!Important]
    > Zignoruj to okno dialogowe, **nie** klikaj przycisku **Zaloguj się za pomocą firmy Microsoft.**

5. Przejdź [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform)do . Umożliwi to konwersję konta NuGet.org na org bez łączenia się z kontem Microsoft.
6. Określ nazwę użytkownika administratora dla konta osobistego NuGet.org/konto utworzone w kroku 1.
7. Postępuj zgodnie z instrukcjami, aby zakończyć transformację tego konta w organizacji.

    ![Okno dialogowe łącza msa](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>NuGet.org problemy z logowaniem dla kont usługi AAD z niezarządzaną dzierżawą?

Jeśli podczas przepływu logowania do domeny konta e-mail@yourdomain.comwidzisz błąd, który następuje poniżej, zapoznaj się z poniższymi czynnościami, aby odzyskać NuGet.org konto.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**Co to jest niezarządzane rzeczy stanu podczas logowania? I dlaczego tak się dzieje teraz?** 

Twoje konto wydaje się być wcześniej zarejestrowane jako osobiste konto Microsoft i działało poprawnie, jednak teraz wydaje się, że Twoje konto zostało zarejestrowane jako dzierżawa "Niezarządzane" w usłudze Azure Active Directory (usługa tożsamości, której używamy do uwierzytelniania kont Microsoft). 

Może się tak zdarzyć, jeśli ty lub @yourdomain.com ktoś z Twojej organizacji (z adresem e-mail) zarejestrowany w jednej ze zintegrowanych usług AAD lub zrobił [samoobsługowe zarejestrowanie dla usługi Azure Active Directory,](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-self-service-signup)która tworzy taką dzierżawę "Niezarządzane" dla używanej domeny konta Microsoft(@yourdomain.com w Twoim przypadku). 

**Co mogę zrobić, aby odzyskać swoje konto?**

W tej chwili nie istnieje sposób dla nas (NuGet.org) do uwierzytelniania kont z takich "Niezarządzanych" kont dzierżawy w usłudze Azure Active Directory. Szukamy lepszego sposobu uwierzytelniania takich kont.

Jeśli chcesz zalogować się do NuGet.org za@yourdomain.compomocą konta Microsoft( ), ty (lub administrator w Twojej firmie) będziesz musiał rościć sobie@yourdomain.comprawo własności do usługi AAD, wykonując sprawdzanie poprawności DNS w celu uwierzytelnienia użytkowników z adresem e-mail " ". Wykonaj kroki dotyczące [przejęcia administratora domen udokumentowane](https://docs.microsoft.com/azure/active-directory/users-groups-roles/domains-admin-takeover) przez usługę Azure Active Directory. Gdy to zrobisz, twój normalny login powinien zacząć działać.

**Nie chcę tego robić, jaki jest inny sposób odzyskania mojego konta?**

Można [utworzyć](https://www.microsoft.com/account) nowe konto Microsoft (z wiadomością @yourdomain.come-mail **nie** skojarzoną z ). Wykonaj czynności podane w sekcji [odzyskaj konto NuGet.org.](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account)

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Jak zmienić nazwę użytkownika konta NuGet.org?

Nie można. Zgodnie z zasadami nie zezwalamy na zmianę nazw użytkowników. Ponadto jest to przełomowa zmiana dla użytkowników, którzy mogli [zdefiniować zasady zaufania pakietu na podstawie właściciela pakietu.](../consume-packages/installing-signed-packages.md#trust-package-owners) Jedynym sposobem zmiany nazwy użytkownika jest utworzenie nowego konta z żądaną nazwą użytkownika. Zalecamy usunięcie istniejącego konta przed utworzeniem nowego konta, w przeciwnym razie nie będzie można ponownie użyć zarejestrowanego konta Microsoft.
> [!Important]
> Usunięcie użytkownika nadal będzie **rezerwować** `username`plik . Nie będzie można ponownie użyć tej samej nazwy użytkownika i **obejmuje to zmianę obudowy**. Na przykład, jeśli utworzono `mycoolname` użytkownika z nazwą `MyCoolName`użytkownika i chcesz to zmienić (zmiany wielkości liter), nie będzie to możliwe po usunięciu użytkownika.

Wykonaj czynności podane w [sekcji usuń konto NuGet.org](#how-to-delete-my-nugetorg-account) i zarejestruj nowe [konto](individual-accounts.md) z poprawną nazwą użytkownika.

### <a name="how-to-delete-my-nugetorg-account"></a>Jak usunąć konto NuGet.org?

Aby usunąć swoje konto, należy pamiętać, że zalecamy przeniesienie własności wszelkich pakietów, w których jesteś jedynym właścicielem. Możesz dowiedzieć się więcej o [zarządzaniu właścicielami pakietów,](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg) jak to zrobić. Pomoże nam to również przyspieszyć twoją prośbę.

Jeśli chcesz przekształcić swoje konto w organizację, wykonaj kroki podane w [przekształcić konto NuGet.org w organizację.](#how-to-transform-my-nugetorg-account-to-an-organization)

> [!Important]
> Usunięcie użytkownika spowoduje:
>  1. Twoja nazwa użytkownika zostanie zarezerwowana i nikt nie będzie mógł jej ponownie użyć do utworzenia konta indywidualnego lub konta organizacji.
>  1. Odwołaj skojarzone klucze interfejsu API. 
>  1. Usuń konto jako właściciela dla wszystkich pakietów podrzędnych.
>  1. Rozłączaj wszystkie istniejące wcześniej rezerwacje prefiksów identyfikatorów z tym kontem.
>  1. Usuń konto jako członka dowolnej organizacji.

Wykonaj następujące kroki, aby kontynuować usuwanie konta.
1. [Zaloguj się do NuGet.org](https://www.nuget.org/users/account/LogOn) za pomocą konta, które chcesz usunąć.
2. Kliknij ten adres [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete) URL: i wykonaj kroki, aby przesłać żądanie usunięcia konta.

Nasza obsługa klienta przetworzy to żądanie i wykona usunięcie konta.
