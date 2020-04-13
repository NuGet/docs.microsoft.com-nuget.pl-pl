---
title: Rezerwacja prefiksu identyfikatora
description: Opis funkcji prefiksu prefiksu prefiksu i przewodnik autora.
author: karann-msft
ms.author: karann
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: da464cc44d8c874e13c0cdfab871f31e643b577f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610489"
---
# <a name="package-id-prefix-reservation"></a>Rezerwowanie prefiksów identyfikatorów pakietów

Właściciele pakietów mogą rezerwować i chronić swoją tożsamość, rezerwując prefiksy identyfikatorów. Konsumenci pakietów są dostarczane z dodatkowymi informacjami, gdy pakiety, które są używane nie są zwodnicze w ich właściwości identyfikujące. 

[nuget.org](https://www.nuget.org/) i Visual Studio 2017 w wersji 15.4 lub nowszej pokazują wizualny wskaźnik dla pakietów, które są przesyłane przez właścicieli z prefiksem identyfikatora zarezerwowanego pakietu, o ile pakiet jest zgodny ze wzorcem nazewnictwa zastrzeżonego identyfikatora. Poniższa dokumentacja wyjaśnia, co oznacza rezerwacja prefiksu identyfikatora i jak właściciel może ubiegać się o prefiks identyfikatora.

## <a name="id-prefix-reservation-details"></a>Szczegóły rezerwacji prefiksu identyfikatora

Gdy prefiks identyfikatora pakietu jest zarezerwowany, kilka rzeczy dzieje się w galerii [nuget.org,](https://www.nuget.org/) a także w programie Visual Studio. Ponadto istnieją zaawansowane scenariusze, które są obsługiwane przez rezerwacje prefiksu identyfikatora, takie jak ustawianie prefiksu jako "public", delegowanie podzbiorów prefiksów do wielu właścicieli.

### <a name="id-prefix-reservation-on-nugetorg"></a>Rezerwacja prefiksu identyfikatora w nuget.org

Gdy prefiks jest zarezerwowany na [nuget.org,](https://www.nuget.org/)nastąpi następujące czynności:

1. Rezerwacja prefiksu jest skojarzona z właścicielem lub zestawem właścicieli na [nuget.org](https://www.nuget.org/).

1. Za każdym razem, gdy pakiet jest przesyłany do [nuget.org](https://www.nuget.org/) o identyfikatorze zgodnym z prefiksem zastrzeżonego identyfikatora, pakiet jest odrzucany, chyba że pochodzi od właściciela(ów), który zarezerwował prefiks identyfikatora.

1. Każdy pakiet, który pasuje do zastrzeżonego prefiksu identyfikatora i pochodzi od właścicieli, którzy zarezerwowali prefiks identyfikatora, będzie miał wskaźnik wizualny w programie Visual Studio 2017 w wersji 15.4 lub nowszej oraz [na nuget.org](https://www.nuget.org/) wskazujący, że pakiet znajduje się pod zastrzeżonym prefiksem identyfikatora. Dotyczy to zarówno nowych zgłoszeń pakietów, jak i istniejących pakietów pod właścicielami. **Uwaga:** Wskaźnik w programie Visual Studio pojawia się tylko wtedy, gdy jako źródło pakietu wybrano pojedynczy kanał.

1. Wszystkie wcześniej istniejące pakiety, które pasują do zastrzeżonego prefiksu identyfikatora, ale *nie* są własnością właściciela zarezerwowanego prefiksu, pozostaną niezmienione (nie będą niepubliczne, ale nie będą również miały wskaźnika wizualnego). Ponadto właściciele tych pakietów nadal będą mogli przesyłać nowe wersje do pakietu.

Zmiany te są oparte na następujących warunkach i nakładają kilka dodatkowych ograniczeń:

- Tylko jeden właściciel pakietu musi mieć zarezerwowany prefiks dla wskaźnika wizualnego do wyświetlenia (dla pakietów z wieloma właścicielami).

- Jeśli istnieje więcej niż jeden właściciel pakietu, w którym jeden lub więcej właścicieli ma zarezerwowany prefiks, a jeden lub więcej właścicieli nie ma zastrzeżonego prefiksu, tylko właściciele z zastrzeżonym prefiksem mogą usunąć innych właścicieli z zastrzeżonym prefiksem. Właściciele, którzy nie mają zarezerwowanego prefiksu, nie mogą usuwać właścicieli z zarezerwowanym prefiksem. Nadal mogą usuwać innych właścicieli, którzy również nie mają zarezerwowanego prefiksu.

- Gdy pakiet ma wskaźnik wizualny, *powinien zawsze* mieć wskaźnik wizualny (gwarantujący, że co najmniej jeden właściciel z zastrzeżonym prefiksem zawsze pozostanie właścicielem)

### <a name="advanced-prefix-reservation-scenarios"></a>Zaawansowane scenariusze rezerwacji prefiksów

Istnieje kilka bardziej zaawansowanych scenariuszy rezerwacji prefiksów opisanych poniżej, w tym delegowanie subprefix i oznaczanie prefiksów jako publicznych. Poniżej znajdują się bardziej zaawansowane rezerwacje prefiksów, które można dokonać. 

- Podczas rezerwacji prefiksu właściciel może zażądać delegowania podzbiorów prefiksu (lub prefiksu) do innych właścicieli. Na przykład, jeśli '[Microsoft](https://www.nuget.org/profiles/microsoft)' jest właścicielem firmy Microsoft. \*', ale '[aspnet](https://www.nuget.org/profiles/aspnet)' chce zarezerwować 'Microsoft.AspNet. \*', '[Microsoft](https://www.nuget.org/profiles/microsoft)' może delegować polecenie 'Microsoft.AspNet. \*" na konto [aspnet.](https://www.nuget.org/profiles/aspnet)

- Podczas rezerwacji prefiksu właściciel może wybrać, aby udostępnić prefiks publicznych. Spowoduje to nadal dać im wskaźnik wizualny pokazujący, że pakiet pochodzi z zastrzeżonego prefiksu, ale **nie** będzie blokować przyszłych zgłoszeń pakietu w prefiksie dla dowolnego właściciela. Jest to przydatne w przypadku projektów typu open source z wieloma współautorami — górni lub podstawowi współautorzy mogą mieć zarezerwowany prefiks, ale nadal może być otwarty dla wszystkich współautorów. 

### <a name="prefix-reservation-visual-indicator"></a>Wskaźnik wizualny rezerwacji prefiksów

Gdy pakiet pochodzi z zarezerwowanego prefiksu, zobaczysz poniższe wskaźniki wizualne w galerii [nuget.org](https://www.nuget.org/) i w programie Visual Studio 2017 w wersji 15.4 lub nowszej:

**Galeria nuget.org**![galeria nuget.org
](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Proces aplikacji rezerwacji prefiksu identyfikatora

1. Przejrzyj kryteria akceptacji [rezerwacji identyfikatora prefiksu](#id-prefix-reservation-criteria).

2. Określ prefiksy, które chcesz zarezerwować, oprócz wszystkich [zaawansowanych scenariuszy rezerwacji prefiksów,](#advanced-prefix-reservation-scenarios) które mogą być wymagane.

3. Wyślij wiadomość [account@nuget.org](mailto:account@nuget.org) e-mail z nazwą wyświetlaną właściciela na [nuget.org](https://www.nuget.org/), a także wszelkie zarezerwowane prefiksy, o które prosisz. Jeśli delegujesz podzbiory prefiksów wielu właścicielom, upewnij się, że wymieniasz wszystkie nazwy wyświetlane właściciela i podzbiory prefiksów.

Po złożeniu wniosku użytkownik zostanie powiadomiony o przyjęciu lub odrzuceniu (z kryteriami, które spowodowały odrzucenie). Być może będziemy musieli zadać dodatkowe pytania identyfikujące, aby potwierdzić tożsamość właściciela.

### <a name="id-prefix-reservation-criteria"></a>Kryteria rezerwacji prefiksu identyfikatora

Podczas przeglądania dowolnej aplikacji dla rezerwacji prefiksu identyfikatora zespół [nuget.org](https://www.nuget.org/) oceni aplikację pod kątem poniższych kryteriów. Nie wszystkie kryteria muszą być spełnione, aby przedrostek został zarezerwowany, ale wniosek może zostać odrzucony, jeżeli nie ma istotnych dowodów na to, że kryteria są spełnione (z podanym wyjaśnieniem):

1. Czy prefiks identyfikatora pakietu prawidłowo i wyraźnie identyfikuje właściciela pakietu?

1. Czy właściciel pakietu [włączył 2FA dla swojego konta NuGet.org?](individual-accounts.md#enable-two-factor-authentication-2fa)

1. Czy znaczna liczba pakietów, które zostały już przesłane przez właściciela w prefiksie identyfikatora pakietu?

1. Czy prefiks identyfikatora pakietu jest czymś powszechnym, który nie powinien należeć do żadnego indywidualnego właściciela lub organizacji?

1. Czy *nie* zarezerwowanie prefiksu identyfikatora pakietu spowodować niejednoznaczności i zamieszanie dla społeczności?

1. Czy właściwości identyfikujące pakiety, które pasują do prefiksu identyfikatora pakietu, są jasne i spójne (zwłaszcza autor pakietu)?

1. Czy pakiety mają licencję (przy użyciu elementu metadanych [licencji](../reference/nuspec.md#license) i NIE licenseUrl, który jest przestarzały)?

1. Jeśli pakiety mają ikonę (przy użyciu elementu metadanych iconUrl), czy są one również przy użyciu elementu metadanych [ikony](../reference/nuspec.md#icon) (nie jest wymagane, aby usunąć iconUrl)?

## <a name="third-party-feed-provider-scenarios"></a>Scenariusze dostawców usług informacyjnych innych firm

Jeśli dostawca kanału informacyjnego innej firmy jest zainteresowany implementowaniem własnej usługi w celu zapewnienia rezerwacji prefiksów, może to zrobić, modyfikując usługę wyszukiwania w dostawcach kanałów informacyjnych NuGet V3. Zmiana w usłudze wyszukiwania danych `verified` jest dodanie właściwości. Klient NuGet nie będzie obsługiwać dodanej właściwości w źródle danych V2.

Aby uzyskać więcej informacji, zobacz [dokumentację dotyczącą usługi wyszukiwania interfejsu API](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Zasady rozstrzygania sporów o zastrzeżenie prefiksów prefiksów o identyfikatorze pakietu
Jeśli uważasz, że [właścicielowi NuGet.org](https://www.nuget.org) przypisano rezerwację prefiksu identyfikatora pakietu, która jest sprzeczna z wyżej [support@nuget.org](mailto:support@nuget.org) wymienionymi kryteriami lub narusza jakiekolwiek znaki towarowe lub prawa autorskie, wyślij wiadomość e-mail z danym prefiksem do identyfikatora, właścicielem prefiksu do iod i powodem zakwestionowania przypisanej rezerwacji prefiksu.

