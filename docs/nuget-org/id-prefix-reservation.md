---
title: Rezerwacja prefiksów identyfikatorów
description: Identyfikator pakietu — opis funkcji rezerwacji i Podręcznik autora.
author: karann-msft
ms.author: karann
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: da464cc44d8c874e13c0cdfab871f31e643b577f
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610489"
---
# <a name="package-id-prefix-reservation"></a>Rezerwacja prefiksu identyfikatora pakietu

Właściciele pakietu mogą zarezerwować i chronić swoją tożsamość przez zarezerwowanie prefiksów identyfikatorów. Odbiorcy pakietu są dostarczani z dodatkowymi informacjami w przypadku, gdy pakiety, których zajmują, nie wprowadzają żadnych zwodniczych właściwości identyfikacyjnych. 

[NuGet.org](https://www.nuget.org/) i Visual Studio 2017 w wersji 15,4 lub nowszej pokazują Wskaźnik wizualny dla pakietów przesyłanych przez właścicieli z prefiksem identyfikatora pakietu zastrzeżonego, o ile pakiet pasuje do wzorca nazewnictwa prefiksu zastrzeżonego identyfikatora. W poniższym odwołaniu wyjaśniono, czym jest rezerwacja prefiksu identyfikatora i jak właściciel może zastosować do prefiksu identyfikatora.

## <a name="id-prefix-reservation-details"></a>Szczegóły rezerwacji prefiksu identyfikatora

Gdy prefiks identyfikatora pakietu jest zarezerwowany, kilka rzeczy odbywa się w galerii [NuGet.org](https://www.nuget.org/) , a także w programie Visual Studio. Ponadto istnieją zaawansowane scenariusze, które są obsługiwane przez rezerwacje prefiksów identyfikatorów, takie jak ustawienie prefiksu jako "Public" i delegowanie podzestawów prefiksu do wielu właścicieli.

### <a name="id-prefix-reservation-on-nugetorg"></a>Rezerwacja prefiksu identyfikatora w nuget.org

Gdy prefiks jest zarezerwowany w [NuGet.org](https://www.nuget.org/), zostaną wykonane następujące:

1. Rezerwacja prefiksu jest skojarzona z właścicielem lub zestawem właścicieli w [NuGet.org](https://www.nuget.org/).

1. Za każdym razem, gdy pakiet jest przesyłany do [NuGet.org](https://www.nuget.org/) z identyfikatorem, który pasuje do zastrzeżonego prefiksu identyfikatora, pakiet zostanie odrzucony, chyba że pochodzi od właściciela, który zarezerwował prefiks identyfikatora.

1. Każdy pakiet, który jest zgodny z zarezerwowanym prefiksem ID i pochodzi od właściciela, który zarezerwował prefiks identyfikatora, będzie miał wskaźnik wizualizacji w programie Visual Studio 2017 w wersji 15,4 lub nowszej, a na [NuGet.org](https://www.nuget.org/) wskazujący, że pakiet znajduje się w zastrzeżonym prefiksie identyfikatora. Dotyczy to zarówno nowych przesłanych pakietów, jak i istniejących pakietów w ramach właścicieli. **Uwaga:** Wskaźnik w programie Visual Studio pojawia się tylko wtedy, gdy jako źródło pakietu jest wybrane pojedyncze źródło danych.

1. Wszystkie poprzednio istniejące pakiety, które pasują do zastrzeżonego prefiksu identyfikatora, ale *nie* należą do właściciela zastrzeżonego prefiksu pozostaną niezmienione (nie zostaną usunięte z listy, ale również nie będą miały wskaźnika wizualizacji). Ponadto właściciele tych pakietów nadal będą mogli przesyłać nowe wersje do pakietu.

Te zmiany są zależne od następujących warunków i nakładają kilka dodatkowych ograniczeń:

- Tylko jeden właściciel pakietu musi mieć zarezerwowany prefiks dla wskaźnika wizualizacji, który ma być wyświetlany (dla pakietów z wieloma właścicielami).

- Jeśli istnieje więcej niż jeden właściciel pakietu, w którym co najmniej jeden właściciel ma zarezerwowany prefiks, a co najmniej jeden właściciel nie ma zastrzeżonego prefiksu, tylko właściciele z zastrzeżonym prefiksem mogą usunąć innych właścicieli z zastrzeżonym prefiksem. Właściciele, którzy nie mają zastrzeżonego prefiksu, nie mogą usuwać właścicieli z zastrzeżonym prefiksem. Nadal mogą usunąć innych właścicieli, którzy również nie mają zastrzeżonego prefiksu.

- Gdy pakiet ma wskaźnik wizualizacji, powinien *zawsze* mieć wskaźnik wizualizacji (gwarantujący, że co najmniej jeden właściciel z zastrzeżonym prefiksem zawsze pozostaje właścicielem)

### <a name="advanced-prefix-reservation-scenarios"></a>Zaawansowane scenariusze rezerwacji prefiksów

Poniżej opisano kilka bardziej zaawansowanych scenariuszy rezerwacji prefiksów, w tym delegowanie podprefiksów i oznaczanie prefiksów jako publiczne. Poniżej znajdują się bardziej zaawansowane rezerwacje prefiksów, które można wprowadzić. 

- Podczas rezerwacji prefiksu właściciel może żądać delegowania podzestawów prefiksów (lub prefiksu) do innych właścicieli. Na przykład jeśli "Microsoft[" jest właścicielem "Microsoft.](https://www.nuget.org/profiles/microsoft)\*", ale"[ASPNET](https://www.nuget.org/profiles/aspnet)"chce zarezerwować element" Microsoft. ASPNET.\*","[Microsoft](https://www.nuget.org/profiles/microsoft)"może wybrać delegata" Microsoft. ASPNET.\*' na konto [ASPNET](https://www.nuget.org/profiles/aspnet) .

- Podczas rezerwacji prefiksu właściciel może określić, że prefiks ma być publiczny. Nadal będzie to dać im Wskaźnik wizualny pokazujący, że pakiet pochodzi z zastrzeżonego prefiksu, ale **nie** będzie blokować przyszłych przesłanych pakietów na prefiksie dla każdego właściciela. Jest to przydatne w przypadku projektów open source z wieloma współautorami — w górnym lub podstawowym współautorze może być zarezerwowany prefiks, ale nadal można go otworzyć dla wszystkich współautorów. 

### <a name="prefix-reservation-visual-indicator"></a>Wskaźnik wizualizacji rezerwacji prefiksu

Gdy pakiet pochodzi z zastrzeżonego prefiksu, zobaczysz poniższe wskaźniki wizualizacji w galerii [NuGet.org](https://www.nuget.org/) i w programie visual Studio 2017 w wersji 15,4 lub nowszej:

**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Proces aplikacji rezerwacji prefiksu identyfikatora

1. Zapoznaj się z [kryteriami akceptacji rezerwacji identyfikatorów prefiksów](#id-prefix-reservation-criteria).

2. Określ prefiksy, które mają być rezerwowane, oprócz wszelkich [zaawansowanych scenariuszy rezerwacji prefiksów](#advanced-prefix-reservation-scenarios) , które mogą być wymagane.

3. Wyślij wiadomość e-mail do [account@nuget.org](mailto:account@nuget.org) z nazwą wyświetlaną właściciela w [NuGet.org](https://www.nuget.org/), a także wszelkimi zarezerwowanymi prefiksami. W przypadku delegowania podzestawów prefiksu do wielu właścicieli upewnij się, że podajesz wszystkie nazwy wyświetlanych właściciela i podzestawy prefiksów.

Po przesłaniu aplikacji otrzymasz powiadomienie o przyjęciu lub odrzuceniu (z kryteriami, które spowodowały odrzucenie). Może być konieczne podanie dodatkowych pytań, aby potwierdzić tożsamość właściciela.

### <a name="id-prefix-reservation-criteria"></a>Kryteria rezerwacji prefiksów identyfikatorów

Podczas przeglądania dowolnych aplikacji dla rezerwacji prefiksów identyfikatorów zespół [NuGet.org](https://www.nuget.org/) ocenia aplikację pod kątem poniższych kryteriów. Nie wszystkie kryteria muszą zostać spełnione dla prefiksu, który ma być zarezerwowany, ale aplikacja może zostać odrzucona, jeśli nie ma istotnego dowodu spełnienia kryteriów (z podaną wyjaśnieniem):

1. Czy identyfikator pakietu jest poprawny i jasno identyfikuje właściciela pakietu?

1. Czy właściciel pakietu jest [włączony funkcji 2FA dla swojego konta NuGet.org](individual-accounts.md#enable-two-factor-authentication-2fa)?

1. Czy jest to znaczna liczba pakietów, które zostały już przesłane przez właściciela w ramach prefiksu identyfikatora pakietu?

1. Czy identyfikator pakietu jest często stosowany, który nie powinien należeć do poszczególnych właścicieli lub organizacji?

1. *Nie* zapełnianie prefiksu identyfikatora pakietu powoduje niejednoznaczność i nieporozumień dla społeczności?

1. Czy właściwości identyfikacyjne pakietów, które pasują do prefiksu identyfikatora pakietu, są wyraźne i spójne (zwłaszcza autor pakietu)?

1. Czy pakiety mają licencję (przy użyciu elementu metadanych [licencji](../reference/nuspec.md#license) , a nie licenseUrl, który jest przestarzały)?

1. Jeśli pakiety mają ikonę (przy użyciu elementu metadanych iconUrl), czy również używają elementu metadanych [ikony](../reference/nuspec.md#icon) (nie jest to wymagane do usunięcia iconUrl)?

## <a name="third-party-feed-provider-scenarios"></a>Scenariusze dostawcy kanałów informacyjnych innych firm

Jeśli dostawca kanału informacyjnego innej firmy interesuje implementację własnej usługi w celu zapewnienia rezerwacji prefiksów, można to zrobić, modyfikując usługę wyszukiwania w dostawcach kanału informacyjnego programu NuGet v3. Zmiana w usłudze wyszukiwania strumieniowego polega na dodaniu właściwości `verified`. Klient NuGet nie będzie obsługiwał właściwości dodanej w kanale informacyjnym v2.

Aby uzyskać więcej informacji, zobacz [dokumentację dotyczącą usługi wyszukiwania interfejsu API](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Prefiks identyfikatora pakietu zasad sporu rezerwacji
Jeśli uważasz, że właściciel na [NuGet.org](https://www.nuget.org) przypisał rezerwację prefiksu identyfikatora pakietu, która przechodzi do powyższych kryteriów wymienionych na liście lub narusza wszelkie znaki towarowe lub prawa autorskie, należy [support@nuget.org](mailto:support@nuget.org) e-mail z podanym prefiksem identyfikatora, właścicielem prefiksu ID i przyczynie sporu do przypisanej rezerwacji prefiksu.

