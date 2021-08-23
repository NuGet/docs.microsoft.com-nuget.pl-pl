---
title: Najlepsze rozwiązania dotyczące bezpiecznego łańcucha dostaw oprogramowania
description: Najlepsze rozwiązania dotyczące zabezpieczania łańcucha dostaw oprogramowania przy użyciu NuGet & GitHub.
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 4575d4779ed90150cec667489c85875b7fb87a8d
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726980"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>Najlepsze rozwiązania dotyczące bezpiecznego łańcucha dostaw oprogramowania

Open Source jest wszędzie. Znajduje się w wielu zastrzeżonych bazach kodu i projektach społecznościowych. W przypadku organizacji i użytkowników indywidualnych pytanie nie dotyczy tego, czy korzystasz z kodu open source, ale z jakiego kodu open source korzystasz i ile.

Jeśli nie wiesz, co znajduje się w łańcuchu dostaw oprogramowania, potencjalna luka w zabezpieczeniach jednej z Twoich zależności może być krytycznym zagrożeniem, przez co Ty i Twoi klienci będziecie narażeni na potencjalne naruszenia. W tym dokumencie bardziej zagłębimy się w znaczenie terminu "łańcuch dostaw oprogramowania", przyczynę jego znaczenia i sposób zabezpieczania łańcucha dostaw projektu przy użyciu najlepszych rozwiązań.

![The State of the Octoverse 2020 - Open Source](media/opensource-percent.png)

## <a name="dependencies"></a>Zależności 

Termin łańcuch dostaw oprogramowania odnosi się do wszystkiego, co wchodzi do oprogramowania i skąd pochodzi. To zależności i właściwości zależności, od których zależy łańcuch dostaw oprogramowania. Zależność to to, czego wymaga oprogramowanie do uruchomienia. Może to być kod, pliki binarne lub inne składniki, z których pochodzą, takie jak repozytorium lub menedżer pakietów.

Zawiera on informacje o tym, kto napisał kod, kiedy został dodany, w jaki sposób został przejmowany pod uwagę pod względami bezpieczeństwa, znane luki w zabezpieczeniach, obsługiwane wersje, informacje o licencjach i wszystkie elementy, które go dotykają w dowolnym momencie procesu.

Łańcuch dostaw obejmuje również inne części stosu poza pojedynczą aplikacją, takie jak skrypty kompilacji i pakowania lub oprogramowanie, które uruchamia infrastrukturę, na których opiera się aplikacja.

## <a name="vulnerabilities"></a>Luki w zabezpieczeniach

Obecnie zależności oprogramowania są bardzo pervasive. Dość często w projektach używa się setek zależności typu open source dla funkcji, których nie trzeba pisać samodzielnie. Może to oznaczać, że większość aplikacji składa się z kodu, który nie został przez Ciebie autorstwa. 

![Stan października 2020 r. — zależności](media/dependencies.png)

Możliwe luki w zabezpieczeniach w zależnościach od innych firm lub typu open source to prawdopodobnie zależności, którymi nie można sterować tak ściśle jak pisany kod, co może tworzyć potencjalne zagrożenia bezpieczeństwa w łańcuchu dostaw.

Jeśli jedna z tych zależności ma lukę w zabezpieczeniach, istnieje również prawdopodobieństwo, że istnieje luka w zabezpieczeniach. Może to być straszne, ponieważ jedna z zależności może ulec zmianie bez Twojej wiedzy. Nawet jeśli luka w zabezpieczeniach istnieje obecnie w zależności, ale nie można jej wykorzystać, można ją wykorzystać w przyszłości. 

Możliwość wykorzystania pracy tysięcy deweloperów i autorów bibliotek typu open source oznacza, że tysiące bibliotek może efektywnie współtwarzyć bezpośrednio w kodzie produkcyjnym. Na Twój produkt, za pośrednictwem łańcucha dostaw oprogramowania, wpływają niewprawkowane luki w zabezpieczeniach, błędy złych ludzi, a nawet złośliwe ataki na zależności.

## <a name="supply-chain-compromises"></a>Naruszenia łańcucha dostaw

Tradycyjna definicja łańcucha dostaw pochodzi z produkcji. jest to łańcuch procesów wymaganych do ich produkcji i dostarczania. Obejmuje planowanie, dostarczanie materiałów, produkcja i sprzedaż detaliczną. Łańcuch dostaw oprogramowania jest podobny, z wyjątkiem tego, że zamiast materiałów jest to kod. Zamiast produkcji, jest to rozwój. Zamiast zagłębiać się w ore z ziemi, kod jest pozytywowany od dostawców, komercyjnych lub open source, a ogólnie rzecz biorąc, kod typu open source pochodzi z repozytoriów. Dodanie kodu z repozytorium oznacza, że produkt jest zależny od tego kodu.

Jednym z przykładów ataku łańcucha dostaw oprogramowania jest celowe dodanie złośliwego kodu do zależności przy użyciu łańcucha dostaw tej zależności w celu dystrybucji kodu do ofiar. Ataki na łańcuch dostaw są prawdziwe. Istnieje wiele metod ataku na łańcuch dostaw, od bezpośredniego wstawiania złośliwego kodu jako nowego współautora, przez przejęcie konta współautora bez zacałowania innych osób, a nawet naruszenia klucza podpisywania w celu rozpowszechniania oprogramowania, które nie jest oficjalnie częścią zależności.

Atak łańcucha dostaw oprogramowania rzadko stanowi cel końcowy, a raczej początek możliwości wstawienia złośliwego oprogramowania lub zapewnienia tylnego dostępu w przyszłości.

![Stan października 2020 r. — cykl życia luk w zabezpieczeniach](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>Oprogramowanie bez zainstalowanej wersji

Obecnie użycie open source jest znaczące i nie należy spodziewać się, że spowolnienie w dowolnym momencie. Ze względu na to, że nie zamierzamy przestać korzystać z oprogramowania open source, zagrożeniem dla bezpieczeństwa łańcucha dostaw jest oprogramowanie nieoprawione. Jak można rozwiązać ryzyko związane z luką w zabezpieczeniach w zależności od projektu?

- **Znajomość tego, co znajduje się w Twoim środowisku.** Wymaga to odnajdywania zależności i zależności przechodniej w celu zrozumienia ryzyka związanego z tymi zależnościami, takich jak luki w zabezpieczeniach lub ograniczenia licencjonowania.
- **Zarządzanie zależnościami.** Po odkryeniu nowej luki w zabezpieczeniach należy określić, czy ma to wpływ, a jeśli tak, zaktualizować do najnowszej dostępnej wersji i poprawki zabezpieczeń. Jest to szczególnie ważne, aby przejrzeć zmiany, które wprowadzają nowe zależności, lub regularnie przeprowadzać inspekcję starszych zależności.
- **Monitorowanie łańcucha dostaw.** Odbywa się to przez inspekcję posiadanych kontrolek do zarządzania zależnościami. Pomoże to wymusić bardziej restrykcyjne warunki, które zostaną spełnione dla zależności.

![The State of the Octoverse 2020 - Advisories](media/advisories.png)

Zostaną pokrytą różnymi narzędziami i technikami NuGet i GitHub, których można obecnie używać do zarządzania potencjalnymi zagrożeniami w projekcie. 

## <a name="knowing-what-is-in-your-environment"></a>Znajomość tego, co znajduje się w Twoim środowisku

### <a name="nuget-dependency-graph"></a>NuGet wykres zależności

**📦 Konsument pakietu**

Możesz wyświetlić swoje NuGet w projekcie, patrząc bezpośrednio na odpowiedni plik projektu.

Zwykle znajduje się on w jednym z dwóch miejsc:

-   [`packages.config`](../reference/packages-config.md) — znajduje się w katalogu głównym projektu.
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) — znajduje się w pliku projektu. 

W zależności od metody zarządzania zależnościami NuGet można również użyć funkcji Visual Studio, aby wyświetlić zależności bezpośrednio w [programie Eksplorator rozwiązań](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer) lub [NuGet Menedżer pakietów](../consume-packages/install-use-packages-visual-studio.md).

W przypadku środowisk interfejsu wiersza polecenia możesz użyć polecenia , aby wyświetlić listę zależności [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) projektu lub rozwiązania. 

Aby uzyskać więcej informacji na temat NuGet zależności, [zobacz następującą dokumentację.](../consume-packages/overview-and-workflow.md)

### <a name="github-dependency-graph"></a>Wykres zależności usługi GitHub 

**📦 Pakiet dla konsumentów | 📦🖊 Autor pakietu**

Możesz użyć GitHub zależności, aby zobaczyć pakiety, od których zależy projekt, oraz repozytoria, które od niego zależą. Może to pomóc w zobaczeniu wszelkich luk w zabezpieczeniach wykrytych w jego zależnościach.

Aby uzyskać więcej informacji GitHub zależności repozytorium, [zobacz następującą dokumentację.](https://github.co/dependency-graph)

### <a name="dependency-versions"></a>Wersje zależności

**📦 Pakiet dla konsumentów | 📦🖊 Autor pakietu**

Aby zapewnić bezpieczny łańcuch dostaw zależności, należy upewnić się, że wszystkie narzędzia & zależności są regularnie aktualizowane do najnowszej stabilnej wersji, ponieważ często obejmują one najnowsze funkcje i poprawki zabezpieczeń do znanych luk w zabezpieczeniach. Zależności mogą obejmować kod, od których korzystasz, używane pliki binarne, używane narzędzia i inne składniki. Może to obejmować:

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [Środowisko uruchomieniowe zestawu SDK & .NET](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [Pakiety NuGet](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>Zarządzanie zależnościami

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>NuGet przestarzałe i narażone na zagrożenia zależności

**📦 Pakiet dla konsumentów | 📦🖊 Autor pakietu**

Za pomocą interfejsu wiersza [polecenia dotnet można](/dotnet/core/tools/dotnet-list-package) wyświetlić listę wszelkich znanych przestarzałych lub narażonych zależności, które mogą się pojawić w projekcie lub rozwiązaniu. Możesz użyć polecenia lub , aby podać listę znanych `dotnet list package --deprecated` wyerenowania lub luk w `dotnet list package --vulnerable` zabezpieczeniach.

### <a name="github-vulnerable-dependencies"></a>GitHub zależności narażone na zagrożenia

**📦 Pakiet dla konsumentów | 📦🖊 Autor pakietu**

Jeśli projekt jest hostowany na platformie GitHub, możesz użyć usługi [GitHub Security,](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) aby znaleźć luki w zabezpieczeniach i błędy w projekcie, a dependabot naprawi je, otwierając żądanie ściągnięcie względem bazy kodu. 

Wychwytanie zależności narażonych na zagrożenia przed ich wprowadzeniem jest jednym z celem ruchu ["Shift Left".](https://en.wikipedia.org/wiki/Shift-left_testing) Możliwość zawierania informacji o zależnościach, takich jak licencja, zależności przechodnie i wiek zależności, właśnie to ułatwia.

Aby uzyskać więcej informacji na temat alertów funkcji Dependabot & aktualizacji zabezpieczeń, [zobacz następującą dokumentację.](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies)

### <a name="nuget-feeds"></a>NuGet informacyjne

**📦 Konsument pakietu**

W przypadku korzystania z & prywatnych NuGet źródła danych pakiet można pobrać z dowolnego źródła danych. Aby upewnić się, że kompilacja jest przewidywalna i bezpieczna przed znanymi atakami, takimi jak błąd [zależności,](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)najlepszym rozwiązaniem jest znajomość określonych źródeł danych, z których pochodzą pakiety. W celu ochrony można użyć pojedynczego kanału informacyjnego lub prywatnego źródła danych z możliwościami nadrzędnego.

Aby uzyskać więcej informacji na temat zabezpieczania źródeł danych pakietów, zobacz [3 Ways to Mitigate Risk When Using Private Package Feeds (3 Sposoby](https://azure.microsoft.com/resources/3-ways-to-mitigate-risk-using-private-package-feeds/)ograniczania ryzyka w przypadku korzystania z prywatnych źródeł danych pakietów).

### <a name="client-trust-policies"></a>Zasady zaufania klienta

**📦 Konsument pakietu**

Istnieją zasady, z którymi można się zrezygnować, wymagając podpisania pakietów, których używasz. Dzięki temu można ufać autorowi pakietu, o ile został on podpisany, lub ufać pakietowi, jeśli jest on własnością określonego użytkownika lub konta podpisanego przez NuGet.org.

Aby skonfigurować zasady zaufania klienta, [zapoznaj się z następującą dokumentacją.](../consume-packages/installing-signed-packages.md)

### <a name="lock-files"></a>Blokowanie plików

**📦 Konsument pakietów**

Pliki blokady przechowują skrót zawartości pakietu. Jeśli skrót zawartości pakietu, który chcesz zainstalować, pasuje do pliku blokady, zapewni to powtarzalność pakietu.

Aby włączyć pliki blokady, [zobacz następującą dokumentację.](../consume-packages/package-references-in-project-files.md#locking-dependencies)

## <a name="monitor-your-supply-chain"></a>Monitorowanie łańcucha dostaw

### <a name="github-secret-scanning"></a>Skanowanie wpisów tajnych usługi GitHub

**📦🖊 Tworzenie pakietu**

GitHub repozytoria w poszukiwaniu kluczy interfejsu API NuGet, aby zapobiec fałszywemu użyciu wpisów tajnych, które zostały przypadkowo zatwierdzone. 

Aby dowiedzieć się więcej na temat skanowania pod kluczami tajnymi, zobacz About secret scanning (Informacje [o skanowaniu tajnym).](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)

### <a name="author-package-signing"></a>Tworzenie podpisywania pakietów

**📦🖊 Tworzenie pakietu**

[Podpisywanie autora](../reference/signed-packages-reference.md) umożliwia autorowi pakietu sygnaturę tożsamości na pakiecie, a użytkownik może sprawdzić, czy pochodzi od Ciebie. Chroni to przed naruszeniami zawartości i służy jako pojedyncze źródło prawdziwych informacji o pochodzeniu pakietu i autentyczności pakietu. W połączeniu z zasadami zaufania klienta można sprawdzić, czy pakiet pochodzi od określonego autora.

Aby podpisania pakietu przez autora, zobacz [Podpisywanie pakietu](../create-packages/sign-a-package.md).

### <a name="two-factor-authentication-2fa"></a>Two-Factor uwierzytelniania (2FA)

**📦🖊 Tworzenie pakietu**

Włączenie uwierzytelniania dwuskładnikowego (2FA) może dodać dodatkową warstwę zabezpieczeń podczas logowania się do konta [usługi GitHub](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) lub publicznego repozytorium pakietów [NuGet.org.](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa) Zaleca się włączenie uwierzytelniania dwuskładnikowego w celu ochrony konta.

### <a name="package-id-prefix-reservation"></a>Rezerwowanie prefiksów identyfikatorów pakietów 

**📦🖊 Tworzenie pakietu**

Aby chronić tożsamość pakietów, można zarezerwować prefiks identyfikatora pakietu z odpowiednią przestrzenią nazw, aby skojarzyć pasującego właściciela, jeśli prefiks identyfikatora pakietu prawidłowo spełnia [określone kryteria](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria). 

Aby dowiedzieć się więcej na temat rezerwowania prefiksów identyfikatorów, zobacz [Rezerwacja prefiksów identyfikatorów pakietów](../nuget-org/id-prefix-reservation.md).

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>Wycofaniu i wycofaniu pakietu narażonego na zagrożenia

**📦🖊 Tworzenie pakietu**

Aby chronić ekosystem pakietów .NET, gdy masz świadomość luki w zabezpieczeniach w pakiecie, który został przez Ciebie autorstwa, jak najlepiej, aby wycofać i wyeksskrybować pakiet, aby był ukryty przed użytkownikami wyszukując pakiety. Jeśli używasz pakietu, który jest przestarzały i nie znajduje się na liście, należy unikać używania pakietu.

Aby dowiedzieć się, jak wyeznać i wycofać pakiet z listy, zapoznaj się z następującą dokumentacją dotyczącą wyeznania pakietów jako przestarzałych [i cokończenia ich na liście.](../nuget-org/policies/deleting-packages.md#unlisting-a-package) [](../nuget-org/deprecate-packages.md)

## <a name="summary"></a>Podsumowanie

Łańcuch dostaw oprogramowania to wszystko, co wchodzi w jego kod lub ma na nie wpływ. Mimo że naruszenia łańcucha dostaw są prawdziwe i rosną w popularności, nadal są rzadkie; Dlatego najważniejszą rzeczą, jaką można zrobić, jest ochrona łańcucha dostaw przez świadomość **zależności,** zarządzanie zależnościami i **monitorowanie łańcucha dostaw.**

Poznaliśmy różne metody, NuGet i [](/learn/modules/maintain-secure-repository-github/) GitHub, które są dostępne dzisiaj, aby skuteczniej wyświetlać i monitorować łańcuch dostaw oraz zarządzać nim.

Aby uzyskać więcej informacji na temat zabezpieczania oprogramowania na świecie, zobacz [The State of the Octoverse 2020 Security Report (Stan raportu zabezpieczeń octoverse 2020).](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf)
