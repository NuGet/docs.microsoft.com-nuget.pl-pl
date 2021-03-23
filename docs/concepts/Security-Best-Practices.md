---
title: Najlepsze rozwiązania dotyczące bezpiecznego łańcucha dostaw oprogramowania
description: Najlepsze rozwiązania dotyczące zabezpieczania łańcucha dostaw oprogramowania przy użyciu narzędzia NuGet & GitHub.
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: e0f235d99e41e23a4551fbf7577f6c42e3381f5b
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859229"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>Najlepsze rozwiązania dotyczące bezpiecznego łańcucha dostaw oprogramowania

"Open source" jest wszędzie. Znajduje się w wielu zastrzeżonych bazach kodu i projektach społecznościowych. W przypadku organizacji i osób indywidualnych pytanie nie jest związane z tym, czy jesteś, czy nie używasz kodu open source, ale jaki jest używany kod Open Source i ile.

Jeśli nie masz informacji o tym, co znajduje się w łańcuchu podaży oprogramowania, usterka nadrzędna w jednej z Twoich zależności może być dla Ciebie krytyczna, sprawiać, że klient jest narażony na potencjalne zagrożenia. W tym dokumencie będziemy szczegółowe więcej informacji o tym, co oznacza termin "łańcuch dostaw oprogramowania", przyczynę i sposób zabezpieczania łańcucha dostaw projektu z najlepszymi rozwiązaniami.

![Stan Octoverse 2020-Open Source](media/opensource-percent.png)

## <a name="dependencies"></a>Zależności 

Termin łańcucha dostaw oprogramowania służy do odwoływania się do wszystkich elementów, które znajdują się w oprogramowaniu i skąd pochodzą. Są to zależności i właściwości zależności, od których zależy łańcuch dostaw oprogramowania. Zależność to to, co musi być uruchamiane w oprogramowaniu. Może to być kod, pliki binarne lub inne składniki oraz miejsce, z którego pochodzą, takie jak repozytorium lub Menedżer pakietów.

Obejmuje to, kto napisał kod, kiedy został wniesiony, jak został on sprawdzony pod kątem problemów z zabezpieczeniami, znanych luk w zabezpieczeniach, obsługiwanych wersji, informacji o licencjach i niemal wszystkich elementów, które dotykają go w dowolnym momencie.

Łańcuch dostaw obejmuje również inne części stosu niż pojedyncze aplikacje, takie jak skrypty kompilacji i pakowania lub oprogramowanie, na których bazuje aplikacja.

## <a name="vulnerabilities"></a>Luki w zabezpieczeniach

Obecnie zależności oprogramowania są rozpowszechnione. Istnieje bardzo częste dla projektów, które umożliwiają korzystanie z setek zależności typu open source dla funkcji, które nie były jeszcze przeznaczone do pisania. Może to oznaczać, że większość aplikacji składa się z kodu, który nie został utworzony. 

![Stan Octoverse 2020 — zależności](media/dependencies.png)

Możliwe luki w zabezpieczeniach innych firm lub w zależności od źródła, są najprawdopodobniej niezależnie od tego, jak napisano kod, co może spowodować potencjalne zagrożenia bezpieczeństwa w łańcuchu dostaw.

Jeśli jedna z tych zależności ma lukę w zabezpieczeniach, prawdopodobnie masz również lukę w zabezpieczeniach. Może to być Scary, ponieważ jedna z zależności może ulec zmianie bez wiedzy użytkownika. Nawet jeśli w danej chwili istnieje luka w zabezpieczeniach, ale nie jest ona wykorzystywana, może ona być wykorzystywana w przyszłości. 

Możliwość korzystania z tysięcy deweloperów typu "open source" i autorów biblioteki oznacza, że tysiące obcych elementów mogą efektywnie współtworzyć bezpośrednio z kodem produkcyjnym. Produkt, za pomocą łańcucha dostaw oprogramowania, ma wpływ nienaruszone luki, nieszkodliwe błędy lub nawet złośliwe ataki na zależności.

## <a name="supply-chain-compromises"></a>Kompromisy dotyczące łańcucha dostaw

Tradycyjna definicja łańcucha dostaw pochodzi z produkcji; jest to łańcuch procesów wymaganych do wypróbowania i dostarczenia elementu. Obejmuje to planowanie, dostawę materiałów, produkcję i sprzedaż detaliczną. Łańcuch dostaw oprogramowania jest podobny, z wyjątkiem przypadków, gdy nie są materiałami, jest to kod. Zamiast produkcji, jest to programowanie. Zamiast przeszukiwanie stosów rudy od podstaw, kod jest pochodzący od dostawców, komercyjnych lub Open Source, a ogólnie rzecz biorąc, kod typu open source pochodzi z repozytoriów. Dodanie kodu z repozytorium oznacza, że produkt przyjmuje zależność od tego kodu.

Przykład ataku w łańcuchu dostaw oprogramowania występuje, gdy złośliwy kod jest celowo całkowicie dodawany do zależności, przy użyciu łańcucha dostaw tej zależności do dystrybuowania kodu do ofiar. Ataki łańcucha dostaw są prawdziwe. Istnieje wiele metod ataku łańcucha dostaw, bezpośrednio wstawiając złośliwy kod jako nowy współautor, aby przejąć konto współautora bez innych obserwowanie, lub nawet narażać klucz podpisywania w celu dystrybucji oprogramowania, które nie jest oficjalnie częścią tej zależności.

Atak łańcucha dostaw oprogramowania polega na tym, że rzadko jest to cel końcowy, a tym samym na początku szansa, że osoba atakująca może wstawić złośliwe oprogramowanie lub tylne wejście do przyszłego dostępu.

![Stan Octoverse 2020 — cykl życia luki w zabezpieczeniach](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>Niepoprawione oprogramowanie

Korzystanie z programu Open Source dzisiaj jest istotne i nie jest oczekiwane wkrótce. Z uwagi na to, że nie będziemy zatrzymywać korzystania z oprogramowania "open source", zagrożenie związane z zabezpieczeniami łańcucha jest Niepoprawione. Jak to zrobić, jak można rozwiązać ryzyko związane z usterką w zależności od projektu?

- **Zapoznaj się z informacjami w Twoim środowisku.** Wymaga to odnajdywania zależności i wszelkich zależności przechodnich, aby zrozumieć ryzyko tych zależności, takich jak luki w zabezpieczeniach lub ograniczenia licencjonowania.
- **Zarządzanie zależnościami.** Po wykryciu nowej luki w zabezpieczeniach należy określić, czy ma to wpływ, a jeśli tak, należy zaktualizować najnowszą wersję i poprawkę zabezpieczeń. Jest to szczególnie ważne, aby przejrzeć zmiany, które wprowadzają nowe zależności lub regularnie przeprowadzają inspekcję starszych zależności.
- **Monitoruj łańcuch dostaw.** W tym celu należy przeprowadzić inspekcję kontrolowanych kontrolek w celu zarządzania zależnościami. Pomoże to wymusić spełnienie bardziej restrykcyjnych warunków dla zależności.

![Stan Octoverse 2020-Advisors](media/advisories.png)

Będziemy omawiać różne narzędzia i techniki, które zapewnia pakiet NuGet i GitHub, których możesz użyć dzisiaj do rozwiązywania potencjalnych zagrożeń w projekcie. 

## <a name="knowing-what-is-in-your-environment"></a>Informacje o tym, co jest w Twoim środowisku

### <a name="nuget-dependency-graph"></a>Wykres zależności NuGet

**📦 Odbiorca pakietu**

Możesz wyświetlić zależności NuGet w projekcie, patrząc bezpośrednio na odpowiedni plik projektu.

Jest to zazwyczaj dostępne w jednym z dwóch miejsc:

-   [`packages.config`](../reference/packages-config.md) — Znajduje się w katalogu głównym projektu.
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) — Znajduje się w pliku projektu. 

W zależności od metody używanej do zarządzania zależnościami NuGet można także użyć programu Visual Studio, aby wyświetlić zależności bezpośrednio w programie [Eksplorator rozwiązań](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer) lub [Menedżera pakietów NuGet](../consume-packages/install-use-packages-visual-studio.md).

W przypadku środowisk interfejsu wiersza polecenia można użyć [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) polecenie, aby wyświetlić listę zależności projektu lub rozwiązania. 

Aby uzyskać więcej informacji na temat zarządzania zależnościami NuGet, [Zobacz następującą dokumentację](../consume-packages/overview-and-workflow.md).

### <a name="github-dependency-graph"></a>Wykres zależności usługi GitHub 

**📦 Odbiorca pakietu | 📦🖊 Autor pakietu**

Możesz użyć grafu zależności usługi GitHub, aby zobaczyć pakiety, od których zależy projekt, oraz repozytoria, które są od niego zależne. Może to pomóc w znalezieniu luk w zabezpieczeniach.

Więcej informacji o zależnościach repozytorium GitHub znajduje się w [następującej dokumentacji](https://github.co/dependency-graph).

### <a name="dependency-versions"></a>Wersje zależności

**📦 Odbiorca pakietu | 📦🖊 Autor pakietu**

Aby zapewnić bezpieczny łańcuch dostaw zależności, należy upewnić się, że wszystkie zależności & narzędzia są regularnie aktualizowane do najnowszej stabilnej wersji, ponieważ będą często obejmować najnowsze funkcje i poprawki zabezpieczeń znanych luk w zabezpieczeniach. Twoje zależności mogą obejmować kod, od którego jest zależny, pliki binarne, z których korzystasz oraz inne składniki. Może to obejmować:

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [Środowisko uruchomieniowe & .NET SDK](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [Pakiety NuGet](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>Zarządzanie zależnościami

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>Przestarzałe i zagrożone rozwiązania NuGet

**📦 Odbiorca pakietu | 📦🖊 Autor pakietu**

Możesz użyć [interfejsu wiersza polecenia dotnet](/dotnet/core/tools/dotnet-list-package) , aby wyświetlić wszystkie znane przestarzałe lub zagrożone zależności, które mogą znajdować się w projekcie lub rozwiązaniu. Możesz użyć polecenia lub, `dotnet list package --deprecated` `dotnet list package --vulnerable` Aby dostarczyć listę znanych przestarzałych lub luk w zabezpieczeniach.

### <a name="github-vulnerable-dependencies"></a>Zależności narażone na usługi GitHub

**📦 Odbiorca pakietu | 📦🖊 Autor pakietu**

Jeśli projekt jest hostowany w serwisie GitHub, możesz wykorzystać [zabezpieczenia usługi GitHub](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) , aby znaleźć luki w zabezpieczeniach i błędy w projekcie, a Dependabot naprawi je, otwierając żądanie ściągnięcia względem bazy kodu. 

Przechwycenie zależnych zależności przed wprowadzeniem jest jednym z celów przenoszenia przesunięcia w [lewo](https://en.wikipedia.org/wiki/Shift-left_testing) . W ten sposób można uzyskać informacje o zależnościach, takich jak ich licencja, zależności przechodnie i wiek.

Aby uzyskać więcej informacji na temat alertów Dependabot & aktualizacji zabezpieczeń, [Zobacz następującą dokumentację](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies).

### <a name="nuget-feeds"></a>Źródła danych NuGet

**📦 Odbiorca pakietu**

W przypadku korzystania z wielu & publicznych danych prywatnych źródeł NuGet, można pobrać pakiet z dowolnego źródła. Aby upewnić się, że kompilacja jest przewidywalna i zabezpieczona przed znanymi atakami, takimi jak [nieporozumienie zależności](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610), wiedząc, z których konkretnych źródeł pochodzą Twoje pakiety, to najlepsze rozwiązanie. Do ochrony można użyć pojedynczego źródła danych lub prywatnego kanału informacyjnego.

Aby uzyskać więcej informacji na temat zabezpieczania kanałów informacyjnych pakietu, zobacz [trzy sposoby zmniejszania ryzyka podczas korzystania z prywatnych źródeł pakietów](https://azure.microsoft.com/en-us/resources/3-ways-to-mitigate-risk-using-private-package-feeds/).

### <a name="client-trust-policies"></a>Zasady zaufania klienta

**📦 Odbiorca pakietu**

Istnieją zasady, w których można wybrać, które pakiety mają być podpisane. Pozwala to na ufanie autorowi pakietu, o ile jest on podpisany, lub zaufaniem do pakietu, jeśli jest własnością określonego użytkownika lub konta, które jest repozytorium podpisane przez NuGet.org.

Aby skonfigurować zasady zaufania klienta, [zapoznaj się z poniższą dokumentacją](../consume-packages/installing-signed-packages.md).

### <a name="lock-files"></a>Zablokuj pliki

**📦 Odbiorca pakietu**

Pliki blokad przechowują skrót zawartości pakietu. Jeśli skrót zawartości pakietu, który chcesz zainstalować, jest zgodny z plikiem blokady, zagwarantuje powtarzalność opakowania.

Aby włączyć pliki blokad, [zapoznaj się z poniższą dokumentacją](../consume-packages/package-references-in-project-files.md#locking-dependencies).

## <a name="monitor-your-supply-chain"></a>Monitorowanie łańcucha dostaw

### <a name="github-secret-scanning"></a>Skanowanie wpisów tajnych usługi GitHub

**📦🖊 Autor pakietu**

W witrynie GitHub są skanowane repozytoria kluczy interfejsu API NuGet, które uniemożliwiają fałszywe użycie wpisów tajnych, które zostały przypadkowo zatwierdzone. 

Aby dowiedzieć się więcej o skanowaniu tajnym, zobacz [Informacje o skanowaniu tajnym](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning).

### <a name="author-package-signing"></a>Tworzenie podpisywania pakietu

**📦🖊 Autor pakietu**

[Podpisywanie autora](../reference/signed-packages-reference.md) pozwala autorowi pakietu na sygnaturę w pakiecie i dla konsumenta, aby go zweryfikować. Chroni to przed naruszeniem zawartości i służy jako pojedyncze Źródło prawdziwie informacji o pochodzeniu pakietu i autentyczności pakietu. W połączeniu z zasadami zaufania klienta można zweryfikować pakiet pochodzący od określonego autora.

Aby utworzyć Podpisz pakiet, zobacz [Podpisz pakiet](../create-packages/sign-a-package.md).

### <a name="two-factor-authentication-2fa"></a>Uwierzytelnianie Two-Factor (funkcji 2FA)

**📦🖊 Autor pakietu**

Włączenie uwierzytelniania dwuskładnikowego (funkcji 2FA) może dodać dodatkową warstwę zabezpieczeń podczas [logowania do konta usługi GitHub](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) lub [repozytorium pakietu publicznego NuGet.org](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa). Zaleca się włączenie uwierzytelniania dwuskładnikowego w celu ochrony Twojego konta.

### <a name="package-id-prefix-reservation"></a>Rezerwowanie prefiksów identyfikatorów pakietów 

**📦🖊 Autor pakietu**

Aby chronić tożsamość pakietów, można zarezerwować prefiks identyfikatora pakietu z odpowiednią przestrzenią nazw w celu skojarzenia pasującego właściciela, jeśli prefiks identyfikatora pakietu jest prawidłowo objęty [określonymi kryteriami](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria). 

Aby dowiedzieć się więcej o sposobie rezerwowania prefiksów, zobacz temat [rezerwacja prefiksów identyfikatora pakietu](../nuget-org/id-prefix-reservation.md).

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>Wycofanie i wycofanie listy zagrożonego pakietu

**📦🖊 Autor pakietu**

Aby zapewnić ochronę ekosystemu pakietu .NET w przypadku wystąpienia luki w zabezpieczeniach w pakiecie, który został utworzony, należy się zaniechać i wycofać z listy pakietów, aby był on ukryty przed użytkownikami wyszukiwania pakietów. Jeśli używasz pakietu, który jest przestarzały i nie jest wystawiony, należy unikać używania pakietu.

Aby dowiedzieć się, jak wycofać i rozpakować pakiet, zapoznaj się [z](../nuget-org/deprecate-packages.md) poniższą dokumentacją dotyczącą wycofywania i [wystawiania pakietów](../nuget-org/policies/deleting-packages.md#unlisting-a-package).

## <a name="summary"></a>Podsumowanie

Łańcuch dostaw oprogramowania to wszystko, co powoduje lub wpływa na kod. Mimo że kompromisy między łańcuchami dostaw są prawdziwe i rosnące w popularności, nadal są rzadkie; Dzięki temu możesz chronić łańcuch dostaw **, uwzględniając zależności, zarządzanie zależnościami** i **monitorowanie łańcucha dostaw.**

Znasz różne metody zapewniane przez narzędzia NuGet i [GitHub](/learn/modules/maintain-secure-repository-github/) , które są obecnie dostępne dla Ciebie, aby zwiększyć efektywność wyświetlania i monitorowania łańcucha dostaw oraz zarządzania nim.

Aby uzyskać więcej informacji na temat zabezpieczania oprogramowania na całym świecie, zobacz [stan raportu zabezpieczeń systemu Octoverse 2020](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf).
