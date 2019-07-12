---
title: NuGet.org Frequently-Asked Questions
description: Typowe pytania i odpowiedzi dotyczące pracy z galerii pakietów NuGet.
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: fd846632e7a1f5c49fa72d75b18e51cfc7539949
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67841956"
---
# <a name="nugetorg-frequently-asked-questions"></a>Często zadawane pytania NuGet.org

## <a name="license-terms"></a>Postanowienia licencyjne

**Co to są licencji domyślne warunki Jeśli pakiet nie zawierają określone informacje o licencji?**

Każdy pakiet jest regulowane przez postanowienia, które są dołączone do pakietu. Zastosowanie postanowień licencyjnych przed przystąpieniem do uzyskiwania dostępu do, pobieranie lub uzyskiwanie wszelkich pakietów, które należy przejrzeć. W witrynie nuget.org, użyj **informacji o licencji** łącze na stronie pakiet.

Jeśli pakiet nie określa warunki licencji, skontaktuj się z właścicielem pakietu bezpośrednio przy użyciu **skontaktuj się z właścicielami** łącze na stronie nuget.org pakietu. Microsoft nie licencji jakiejkolwiek własności intelektualnej dla Ciebie od dostawców pakietów innych firm, a nie jest odpowiedzialny za otrzymane od innych firm.

## <a name="managing-packages-on-nugetorg"></a>Zarządzanie pakietami w witrynie NuGet.org

**Po zakończeniu przekazywania można edytować metadane pakietów?**

NuGet zaleca wszystkich pakietów, były podpisane. Zasady projektowania podpisywanie pakietów jest, że podpisanych pakietów zawartości musi być niezmienne, która obejmuje nuspec. Edytowanie metadanych pakietu powoduje zmiany nuspec, powodując unieważnienie istniejące podpisy. Zaleca się zmodyfikowanie istniejących przepływów pracy, by nie wymagała ona edytować metadane pakietu, po utworzeniu pakietu.

Należy pamiętać, że składników zależnych wymienionych dla pakietu są generowane automatycznie na podstawie pakietu i nie można edytować.

Ponadto przekazywania pakietów do [int.nugettest.org](https://int.nugettest.org) to świetny sposób testować i weryfikować pakietu bez konieczności szukania pakietu dostępne w publicznej galerii. Punkt końcowy interfejsu API: https://apiint.nugettest.org/v3/index.json

**Czy mogę usunąć pakiet, który został opublikowany w witrynie NuGet.org**

Ogólnie rzecz biorąc nie obsługujemy usunięcie pakietu publikowane w witrynie NuGet.org. Dowiedz się więcej o naszych [zasady dotyczące usuwania pakietów](policies/deleting-packages.md).

**Czy jest możliwe do zarezerwowania nazwy pakietów, które mają zostać opublikowane w przyszłości?**

Tak. Możesz zarezerwować identyfikatorów pakietów na [nuget.org](https://www.nuget.org/) przez zażądanie prefiks Identyfikatora pakietu dla swojego konta. Aby zażądać prefiks Identyfikatora pakietu, postępuj zgodnie z instrukcjami [dokumentacji](id-prefix-reservation.md).

**Jak oświadczenia własności dla pakietów?**

Zobacz [właścicieli pakietu zarządzania w witrynie nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).

**Sposób postępowania z właścicielem pakietu, który narusza mojej licencji na oprogramowanie**

Firma Microsoft zachęca do społeczności NuGet, aby współpracują ze sobą w celu rozwiązania wszelkich sporów, które mogą wystąpić między właścicieli pakietu i innego oprogramowania. Firma Microsoft ma specjalnie [proces rozstrzygania sporów](policies/dispute-resolution.md) do wykonania przed zadaniem intercede administratorom nuget.org.

**Jest zalecane, aby przekazać mój pakietów testowych do nuget.org?**

Do celów testowych możesz użyć [int.nugettest.org](https://int.nugettest.org), lub alternatywne publiczne serwery NuGet, takich jak [portalu myget.org](https://myget.org) lub [DevOps platformy Azure](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Należy pamiętać, że pakiety przekazywane do int.nugettest.org mogą nie zostać zachowane.

**Co to jest maksymalny rozmiar pakietów, który mogę przesłać do repozytorium nuget.org?**

zapewnia pakietów nuget.org do 250MB, ale firma Microsoft zaleca się utrzymywanie pakietów w obszarze 1MB, jeśli jest to możliwe i połączyć ze sobą pakietów przy użyciu zależności. Jako ogólną regułę można przyjąć pakiety zawierają tylko jeden zestaw w celu uniknięcia kolizji.

NuGet korzysta z protokołu HTTP do pobierania pakietów, więc pakiety większe prawdopodobieństwo instalacje zakończone niepowodzeniem niż mniejsze.

Istnieje możliwość udostępniania zależności między kilka pakietów, dzięki czemu rozmiar pobieranych elementów całkowita dla konsumentów pakiety NuGet mniejsze.

Zależności są głównie statyczne i nigdy nie zmiany. Podczas naprawiania usterki w kodzie, zależności nie wymagają zaktualizowania. Jeśli dołączenie zależności znajdą reshipping większych pakiety za każdym razem, gdy. Dzieląc pakiety NuGet na powiązane zależności, uaktualnienia są znacznie bardziej szczegółowych dla konsumentów pakietu.

## <a name="nugetorg-not-accessible"></a>nie jest dostępny w witrynie nuget.org

**Dlaczego nie można pobrać pakiety z lub Przekaż pakiety na stronie nuget.org?**

Najpierw upewnij się, że używasz najnowszej wersji pakietu nuget. Jeśli ta wersja nadal nie będzie działać, [się z pomocą techniczną](https://www.nuget.org/policies/Contact) i podaj dodatkowe połączenie, rozwiązywanie problemów z informacji, takich jak:

- Wersji używasz pakietu NuGet
- Źródła pakietów, których używasz
- Dziennik przywracania z szczegółowy poziom szczegółowości
- MTR lub dane śledzenia programu Fiddler (patrz poniżej)
- Obszar geograficzny
- Czy ten komputer jest używany serwer proxy lub Zapora?
- Jest na swojej maszynie, znajdującej się w centrum danych dostawcy chmury (Azure, AWS itp.)? Jeśli tak, podaj nazwę dostawcy i region.

*Aby przechwycić MTR:*

- Pobierz WinMTR z [http://winmtr.net/download/](http://winmtr.net/)
- Wprowadź `api.nuget.org` jako nazwę hosta i kliknij przycisk **Start**.
- Poczekaj, aż **wysłane** kolumna jest > = 100.

    ![Capturing MTR](media/mtr.png)

- Kopiuj tekst do Schowka.

*Aby przechwycić programu Fiddler:*

- Zainstaluj najnowszą wersję [Fiddler](http://www.telerik.com/download/fiddler).
- Uruchom narzędzie Fiddler i Wyłącz Przechwytywanie ruchu sieciowego przy użyciu **Plik > Przechwytywanie ruchu** menu.
- Usuń wszystkie sesje (Zaznacz wszystkie elementy na liście, naciśnij klawisz **Usuń** klucza).
- Konfigurowanie narzędzia Fiddler do przechwytywania ruchu HTTPS, sprawdzając **odszyfrować realizuje nasłuchu** w **HTTPS** karcie **Narzędzia > Opcje programu Fiddler...**  menu.
- Zamknij program Visual Studio.
- Włącz **Plik > Przechwytywanie ruchu** menu.
- Uruchom program Visual Studio lub nuget.exe .exe i wykonywać akcje, które nie działają. Ruch generowany przez te akcje powinien wyświetlany w narzędziu Fiddler.
- Po akcje zostały uruchomione, użyj **Plik > Zapisz > wszystkie sesje** do przechowywania przechwyconego sesji.

Uwaga: może być konieczne można ustawić `HTTP_PROXY` zmiennej środowiskowej, aby `http://127.0.0.1:8888` routing ruchu NuGet za pomocą programu Fiddler.

Jeśli się nie powiedzie, spróbuj [porady wymienione w tym wpisie w witrynie StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

## <a name="nugetorg-account-management"></a>Zarządzanie kontami nuget.org

### <a name="how-to-recover-nugetorg-password-login"></a>Jak odzyskać adres nuget.org hasło logowania?

Należy pamiętać, że [nuget.org hasła logowania nie jest już](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html) i jest jedynym sposobem, aby zalogować się do repozytorium nuget.org, za pomocą osobistego konta Microsoft (MSA) lub konta usługi Azure Active Directory (AAD). Jednak w przypadku, gdy nie można uzyskać dostęp do skojarzonego konta MSA/AAD może być konieczne na potrzeby odzyskiwania konta nuget.org hasło logowania. W takiej sytuacji wykonaj poniższe kroki.
- **Wymaganie:** Musisz mieć dostęp do poczty e-mail, który jest skojarzony z kontem, dla których potrzebujesz do odzyskania hasła.
- Przejdź do [nie pamiętam hasła strony](https://www.nuget.org/account/ForgotPassword)
- Wprowadź **e-mail** adres, który jest skojarzony z kontem nuget.org, które chcesz odzyskać.
- Kliknij przycisk **wysyłania** przycisku.
- Otrzymasz wiadomość e-mail do konta adres podany adres e-mail z linkiem do zresetowania hasła. Kliknięcie tego linku, a następnie ustawić nowe hasło. Jeśli sprawdzanie poczty nie można odnaleźć folderu "wiadomości-śmieci".
- Po zakończeniu możesz teraz Zaloguj się przy użyciu nazwy użytkownika i hasła dla narzędzia NuGet.
- Aby zalogować się za pomocą nazwy użytkownika/hasła, należy użyć **Zaloguj się przy użyciu konta Nuget.org** link [strony logowania w witrynie nuget.org](https://www.nuget.org/users/account/LogOn).

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Konto Microsoft, które jest połączony z moim kontem nuget.org?

Jeśli pamiętasz, konto Microsoft, które jest skojarzony z Twoim kontem nuget.org, wykonaj poniższe kroki, aby uzyskać pomoc.
1. Przejdź do [strony logowania w witrynie nuget.org](https://www.nuget.org/users/account/LogOn) i kliknij pozycję **potrzebujesz pomocy z logowaniem?** łącza.
1. Spowoduje to wyświetlenie możesz pole wyskakującego okna dialogowego, aby uzyskać pomoc. Wykonaj kroki opisane w tym oknie dialogowym zrozumienie skojarzonych kont firmy Microsoft dla swojego konta w witrynie nuget.org.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Jak zmienić konto Microsoft, używane do logowania w witrynie nuget.org?
Jeśli chcesz zmienić konto Microsoft dla użytkownika w witrynie nuget.org, wykonaj następujące czynności. Załóżmy, że umożliwia swojego konta Microsoft z adresem e-mail `account1@outlook.com` jest skojarzony z Twoim kontem nuget.org, przy użyciu nazwy użytkownika `MyNuGetAccount`. Aby zmienić nazwy logowania do innego konta Microsoft z adresem e-mail `account2@outlook.com`
1. Zaloguj się przy użyciu **aktualnie skojarzone konto Microsoft** tj `account1@outlook.com` na [strony logowania](https://www.nuget.org/users/account/LogOn) po kliknięciu przycisku **Zaloguj się przy użyciu Microsoft**.
1. Po zalogowaniu przejdź do swojej [ustawienia konta](https://www.nuget.org/account) strony.
1. Rozwiń sekcję Aby uzyskać **konto logowania**. Kliknij pozycję **Zmień konto** przycisku.
1. Teraz nastąpi przekierowanie do strony logowania firmy microsoft. Zaloguj się przy użyciu konta, które chcesz zmienić to skojarzenie, aby `account2@outlook.com`. **Uwaga**: może być konieczne kliknięcie **Zaloguj się poza i zaloguj się przy użyciu innego konta** podczas logowania w usłudze flow, aby móc zalogować się za pomocą innego konta Microsoft.
1. Jeśli zostanie wyświetlony błąd, na przykład poniżej, zobacz [konto Microsoft jest połączony z innym kontem nuget.org](#microsoft-account-is-linked-with-another-nugetorg-account) Aby uzyskać więcej informacji.
    >_Nie można zaktualizować konta Microsoft z "account2 <account2@outlook.com>". Może się to zdarzyć, jeśli został już połączony z innym kontem NuGet. Aby uzyskać więcej informacji, skontaktuj się z pomocą techniczną._

1. Po pomyślnym zalogowaniu przy użyciu drugiego konta, nastąpi przekierowanie do strony ustawień konta usługi nuget.org i zostaną wyświetlone nowe konto Microsoft skojarzone z konta logowania. Idąc dalej, możesz należy używać tego konta podczas logowania się do repozytorium nuget.org.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Konto Microsoft jest połączony z innym kontem nuget.org.

Jeśli nastąpiła zmiana identyfikatora logowania firmy Microsoft i wystąpił poniższy błąd:
> _Nie można zaktualizować konta Microsoft z "account2 <account2@outlook.com>". Może się to zdarzyć, jeśli został już połączony z innym kontem NuGet. Aby uzyskać więcej informacji, skontaktuj się z pomocą techniczną._

Załóżmy, że chcesz zmienić firmy Microsoft umożliwia konta logowania z `account1@outlook.com` nuget.org użytkownika przy użyciu nazwy użytkownika `MyNuGetAccount1` do innego konta Microsoft z adresem e-mail `account2@outlook.com`. I zobacz Powyższy błąd.

**Co oznacza Powyższy błąd?**

Oznacza to, że istnieje inne konto nuget.org, który jest skojarzony z kontem Microsoft próby Zmień ją na przykład w powyżej przykładzie konto Microsoft z adresem e-mail `<account2@outlook.com>` jest skojarzony z innym kontem nuget.org z nazwy użytkownika i powiedz, `MyNuGetAccount2`.

Nie można zmienić logowania skojarzone z kontem Microsoft, który jest połączony z kontem różnych nuget.org.

**Pamiętam, że miałem innego konta w witrynie nuget.org, jak sprawdzić, które konto nuget.org jest?**

Zaloguj się przy użyciu drugiego konta Microsoft na [strony logowania](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "strony logowania"). Możesz rejestrować pod uwagę nuget.org, która jest aktualnie powiązany z drugiego konta Microsoft. Można wyświetlić przekazany pakietów i zarządzać kontem na tym koncie.

**I nie są istotne tego drugiego konta nuget.org, chcę zmienić moją nazwę logowania dla pierwszego konta nuget.org przy użyciu drugiego konta Microsoft. Co zrobić?**

Jeśli chcesz nie interesują drugiego konta nuget.org i nadal chcesz ponownie użyć skojarzone konto Microsoft z adresem e-mail `account2@outlook.com`. 

Aby zwalniać skojarzenie konta Microsoft i nuget.org, usuwanie konta nuget.org.
1. Postępuj zgodnie z instrukcjami, aby [usunąć użytkownika](#how-to-delete-my-nugetorg-account) dla drugiego konta nuget.org `MyNuGetAccount2`. 
1. Po usunięciu tego konta będzie można ponowić próbę kroki, aby [zmienić identyfikator logowania konta Microsoft](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login).

**Czas oczekiwania, czas ważna tego drugiego konta zbyt. Chcę, aby utracić tego konta, ale Zmień moje nazw skojarzone konto logowania dla pierwszego konta.**

Konieczne będzie utworzenie/użycie innego konta Microsoft, powiedz, za pomocą adresu e-mail `account3@outlook.com`. 
1. Należy najpierw zaloguj się przy użyciu konta Microsoft drugi `account2@outlook.com` w witrynie nuget.org. Wykonaj powyższe kroki, aby zmienić skojarzone nazwy logowania i skojarzyć trzeci konto Microsoft przy użyciu tego konta w witrynie nuget.org.
1. Po zakończeniu drugiego konta Microsoft z adresem e-mail `account2@outlook.com` może być skojarzony z kontem pierwszego nuget.org `MyNuGetAccount1`. Te same czynności powyżej, aby zmienić nazwy logowania firmy microsoft do drugiego konta Microsoft.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Logowanie się przy użyciu konta Microsoft przedstawiono ze mną Mój adres e-mail jest połączony z innym kontem Microsoft

Jeśli próbowano zalogować się przy użyciu konta Microsoft powiedzieć, za pomocą adresu e-mail `account1@outlook.com` i zostanie wyświetlony błąd, takich jak poniżej:
> _Konto z adresem e-mail 'account1@outlook.com"jest połączony z innym kontem microsoft._
>
> _Jeśli chcesz zaktualizować połączonego konta Microsoft możesz to zrobić na stronie ustawień konta._

**Co oznacza Powyższy błąd?**

Po utworzeniu konta w witrynie nuget.org, jest adresem e-mail komunikacji powiązanej z tym kontem. Jest to zazwyczaj taki sam jak adres e-mail, który służy do skojarzonego konta Microsoft. Można określić inny adres e-mail do komunikacji. W związku z technicznego punktu widzenia, mogą istnieć innej firmy Microsoft do konta, na przykład za pomocą `account2@outlook.com` połączonego konta nuget.org przy użyciu adresu e-mail komunikacji jako `account1@outlook.com`.

Aby Powyższy błąd oznacza, że istnieje już konto nuget.org przy użyciu adresu e-mail komunikacji `account1@outlook.com` , ale jest skojarzony z innym kontem Microsoft, za pomocą adresu e-mail **, który nie jest** `account1@outlook.com`.

**Jak znaleźć konto jest połączone z tym kontem nuget.org firmy Microsoft?**

Należy używać [Zaloguj się w Pomocy](#which-microsoft-account-is-linked-to-my-nugetorg-account) przepływu, aby ustalić, które konto Microsoft jest połączony z kontem nuget.org, za pomocą adresu e-mail `account1@outlook.com`.

**Czy chcesz zastąpić tego konta, przy użyciu konta Microsoft**

Postępuj zgodnie z instrukcjami w [nie można użyć nazwy logowania firmy microsoft, jak odzyskanie konta nuget.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) sekcji, aby skojarzyć swoje konto Microsoft z istniejącym kontem nuget.org.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Nie można użyć nazwy logowania firmy microsoft, jak odzyskanie konta nuget.org?

Jeśli chcesz wypróbować, przy użyciu [Zaloguj się w Pomocy](#which-microsoft-account-is-linked-to-my-nugetorg-account) i nie masz dostępu do konta Microsoft, który jest skojarzony z Twoim kontem nuget.org, wykonaj poniższe kroki, aby połączyć nowe konto Microsoft ze swoim kontem nuget.org.
1. **Wymaganie**: Konieczne będzie dostęp do konta Microsoft, który nie jest skojarzona z wszystkie istniejące konta usługi nuget.org. Jeśli nie masz, możesz to zrobić [tworzenie](https://signup.live.com) jeden.
2. Jeśli pamiętasz nazwy użytkownika i hasła dla konta usługi nuget.org, postępuj zgodnie z [kroki w celu odzyskania hasła identyfikatora logowania](#how-to-recover-nugetorg-password-login).
3. [Zaloguj się na stronie nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) przy użyciu identyfikatora logowania nazwy użytkownika i hasła.
4. Po zalogowaniu zobaczysz okno podręczne okno dialogowe, Pokaż rozmiarze, takich jak poniżej. To okno dialogowe przerwaniu hasła.
5. **UWAGA**: Zignoruj instrukcji, aby zalogować się przy użyciu określonego konta Microsoft. Możliwe jest łączenie konta nuget.org do innych logowania firmy Microsoft.
6. Kliknij przycisk **Zaloguj się przy użyciu Microsoft** i zaloguj się przy użyciu konta Microsoft, musisz mieć dostęp do, zgodnie z opisem w kroku 1.
7. Konta będą teraz łączone do tego nowego konta Microsoft, można użyć do zalogowania się do repozytorium nuget.org w przyszłości.

    ![Okno dialogowe MSA łącza](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Jak przekształcić Moje konto nuget.org do organizacji?

Jeśli chcesz przekształcić swoje konto do organizacji, a to konto jest już skojarzony z identyfikatora logowania konta Microsoft, wykonaj kroki podane w dokumentacji dotyczącej [organizacje w organizacji nuget](organizations-on-nuget-org.md).

Jeśli jednak nuget.org konto użytkownika nie jest skojarzony/połączony z kontem Microsoft, możesz wykonać poniższe kroki, aby przekształcić tego konta do organizacji.
1. **Wymaganie**: Musisz mieć indywidualne konto, najpierw utworzone w witrynie nuget.org, ma być używany jako administrator na koncie organizacji. Jeśli nie masz, [Utwórz nowe konto w witrynie nuget.org](individual-accounts.md)
2. Postępuj zgodnie z [kroki w celu odzyskania hasła identyfikatora logowania](#how-to-recover-nugetorg-password-login) dla konta usługi nuget.org, jeśli nie masz hasła logowania, jeśli Pomiń ten krok.
3. [Zaloguj się na stronie nuget.org](https://www.nuget.org/users/account/LogOnNuGetAccount) przy użyciu identyfikatora logowania nazwy użytkownika i hasła.
4. Po zalogowaniu zobaczysz okno podręczne okno dialogowe, Pokaż rozmiarze, takich jak poniżej. To okno dialogowe przerwaniu hasła. 
    > [!Important]
    > Ignoruj to okno dialogowe **nie** kliknij **Zaloguj się przy użyciu microsoft** przycisku.

5. Przejdź do [ https://www.nuget.org/account/transform ](https://www.nuget.org/account/transform). Pozwoli to można przekonwertować konta nuget.org do organizacji, bez łączenia się z kontem Microsoft.
6. Podaj nazwę użytkownika administratora konta osobiste nuget.org/konto utworzone w kroku 1.
7. Postępuj zgodnie z instrukcjami, aby ukończyć przekształcania tego konta do organizacji.

    ![Okno dialogowe MSA łącza](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>nuget.org problemy podczas logowania do konta usługi AAD z niezarządzanej dzierżawy?

Jeśli zostanie wyświetlony błąd taki jak poniżej podczas przepływu logowania przy użyciu konta domeny poczty e-mail (@yourdomain.com), zobacz poniższe kroki, aby odzyskać konto w witrynie nuget.org.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**Co to jest ta rzecz stanie niezarządzanym podczas logowania? I dlaczego jest to teraz dzieje?** 

Twoje konto wydaje się, że wcześniej zostać zarejestrowana jako osobiste konto Microsoft i to wszystko działa prawidłowo, jednak teraz wygląda konta został zarejestrowany jako dzierżawę "Niezarządzany" w usłudze Azure Active Directory (tożsamość usługi używane do uwierzytelniania Konta Microsoft). 

To może być spowodowane tym, jeśli ktoś z organizacji (przy użyciu @yourdomain.com adres e-mail) zarejestrowane przy użyciu jednej z usług zintegrowane usługi AAD lub czy [Samoobsługowe tworzenie konta usługi Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup), tworzy takie " Niezarządzane"dzierżawy dla domeny używane konto Microsoft (@yourdomain.com w Twoim przypadku). 

**Co można zrobić na odzyskanie konta?**

W tej chwili nie ma sposobu uwierzytelniania konta z takiego konta dzierżawy "Niezarządzany" w usłudze Azure Active directory dla nas (nuget.org). Firma Microsoft chcą lepszy sposób uwierzytelniania tych kont.

Jeśli chcesz zalogować się na stronie nuget.org z Twoim kontem Microsoft (@yourdomain.com), użytkownik (lub administratora w Twojej firmie) musi przejąć własność usługi AAD, wykonując weryfikacji DNS w celu uwierzytelniania użytkowników za pomocą adresu e-mail "@yourdomain.com". Wykonaj poniższe kroki, aby uzyskać [przejęcia przez administratora domeny](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover) udokumentowane przez usługę Azure Active directory. Po zakończeniu tej operacji normalne identyfikatora logowania powinny działać.

**Nie chcę to zrobić wszystkie, co to jest inny sposób, aby odzyskanie konta?**

Możesz [tworzenie](https://www.microsoft.com/en-us/account) nowe konto Microsoft (Dzięki wiadomościom e-mail **nie** skojarzone z @yourdomain.com). Wykonaj kroki podane w [odzyskanie konta nuget.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account) sekcji.

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Jak zmienić Moja nazwa użytkownika konta nuget.org?

To nie jest możliwe. Jako polityką firma Microsoft nie zezwalają na zmianę nazwy użytkowników jeszcze wdrożone. Jest jedynym sposobem, aby zmienić swoją nazwę użytkownika do utworzenia nowego konta z żądaną nazwą użytkownika. Zaleca się usuwanie istniejącego konta, przed utworzeniem nowej, w przeciwnym razie nie będzie możliwe ponowne wykorzystanie zarejestrowanego konta Microsoft.
> [!Important]
> Usuwanie użytkownika, będzie nadal **zarezerwować** `username`. Nie można ponownie ponownie użyć tej samej nazwy użytkownika i **obejmuje to zmianę obudowy**. Na przykład jeśli użytkownik został utworzony przy użyciu nazwy użytkownika `mycoolname` i chcesz zmienić, aby `MyCoolName`(zmiany wielkości liter), nie będzie możliwe po usunięciu użytkownika.

Wykonaj kroki podane w [usunąć swoje konto w witrynie nuget.org](#how-to-delete-my-nugetorg-account) sekcji i [zarejestrować nowe konto](individual-accounts.md) z prawidłową nazwę użytkownika.

### <a name="how-to-delete-my-nugetorg-account"></a>Jak usunąć swoje konto w witrynie nuget.org?

Można usunąć konto, należy pamiętać, że firma Microsoft zaleca przenieść własność dowolnego pakietu, gdzie jesteś jedynym właścicielem. Przeczytaj więcej o [Zarządzanie właścicielami pakietu](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg) o tym, jak to zrobić. Ułatwi to również nam przyspieszyć Twojego żądania.

Jeśli szukasz Przekształć swoje konto do organizacji, wykonaj kroki podane w [Przekształcanie konto nuget.org, aby organizacja](#how-to-transform-my-nugetorg-account-to-an-organization).

> [!Important]
> Usunięcie użytkownika spowoduje następujące czynności:
>  1. Twoja nazwa użytkownika będzie zarezerwowana i nie będzie można ponownie użyć go, aby utworzyć indywidualne konto lub konta organizacji
>  1. Odwołaj skojarzone klucze interfejsu API. 
>  1. Usuń konto jako właściciela dla dowolnego pakietu podrzędnego.
>  1. Usuń skojarzenie wszystkie rezerwacje prefiks Identyfikatora wcześniej celowe przy użyciu tego konta.
>  1. Usuń konto jest członkiem dowolnej organizacji.

Wykonaj poniższe kroki, aby kontynuować usuwanie kont.
1. [Zaloguj się na stronie nuget.org](https://www.nuget.org/users/account/LogOn) przy użyciu konta, którą chcesz usunąć.
2. Kliknij ten adres url: [ https://www.nuget.org/account/delete ](https://www.nuget.org/account/delete) i postępuj zgodnie z instrukcjami, aby przesłać żądanie usunięcia konta.

Nasz dział obsługi klienta będzie przetwarzania tego żądania i usuwanie kont.
