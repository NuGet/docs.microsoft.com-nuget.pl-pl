---
title: Prefiks Identyfikatora rezerwacji odwołania
description: Przewodnik dotyczący autor i opis funkcji rezerwacji prefiks Identyfikatora pakietu.
author: diverdan92
ms.author: diverdan92
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 32f83bede42f7643a9a4fed593643eefea0453c1
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981005"
---
# <a name="package-id-prefix-reservation"></a>Rezerwowanie prefiksów identyfikatorów pakietu

Właściciele pakietu zarezerwować i chronić swoją tożsamość, rezerwując prefiksy identyfikator. Użytkownicy pakietu są dostarczane z dodatkowymi informacjami korzystanie z pakietów, która pakiet, w którym są one używania nie są oszukańczym w ich identyfikujące właściwości. 

[nuget.org](https://www.nuget.org/) i Visual Studio 2017 w wersji 15.4 lub nowszej Pokaż wizualny wskaźnik informujący dla pakietów, które są przesyłane przez właścicieli z prefiksem Identyfikatora pakietu zarezerwowane, tak długo, jak pakietu jest zgodny z Identyfikatorem zastrzeżony prefiks wzorca nazewnictwa. Poniżej odniesienia wyjaśnia, co rezerwowanie prefiksów identyfikatorów pociąga za sobą i jak poprosić właściciela o prefiks Identyfikatora.

## <a name="id-prefix-reservation-details"></a>Szczegóły rezerwacji prefiks Identyfikatora

Gdy jest zastrzeżony prefiks Identyfikatora pakietu, kilka działań wykonanych na [nuget.org](https://www.nuget.org/) galerii, jak również tak jak w programie Visual Studio. Ponadto są zaawansowane scenariusze, które są obsługiwane przez zastrzeżenia prefiks Identyfikatora, takie jak ustawianie prefiksu jako "public" delegowanie podzestawy prefiks wielu właścicielom.

### <a name="id-prefix-reservation-on-nugetorg"></a>Rezerwowanie prefiksów identyfikatorów w witrynie nuget.org

Gdy prefiks, który jest zarezerwowana na [nuget.org](https://www.nuget.org/), będą wykonywane następujące czynności:

1. Rezerwowanie prefiksów identyfikatorów jest skojarzony z właścicielem lub zestawu właścicieli na [nuget.org](https://www.nuget.org/).

1. Zawsze, gdy pakiet jest przesyłany do usługi [nuget.org](https://www.nuget.org/) z Identyfikatorem, który odpowiada zastrzeżony prefiks Identyfikatora, pakiet zostanie odrzucony, o ile nie pochodzi z jego właściciela, która zarezerwowana prefiks Identyfikatora.

1. Dowolny pakiet, który odpowiada zastrzeżony prefiks Identyfikatora i pochodzi z jego właściciela, która zarezerwowana prefiks Identyfikatora odniesie wizualny wskaźnik informujący w programie Visual Studio 2017 w wersji 15.4 lub nowszej, a na [nuget.org](https://www.nuget.org/) wskazująca, że pakiet jest w obszarze zastrzeżony prefiks Identyfikatora. Dotyczy to zarówno nowe przesłanych pakietów, jak i istniejące pakiety w ramach jego właściciela. **Uwaga:** wskaźnika w programie Visual Studio pojawia się tylko wtedy, gdy pojedynczy kanał informacyjny został wybrany jako źródło pakietów.

1. Wszystkie uprzednio istniejące pakiety, które odpowiadają zastrzeżony prefiks Identyfikatora, ale są one *nie* należące do właściciela zarezerwowanego prefiks pozostanie niezmieniona (nie będzie nieznajdujące się na liście, ale mogą także mieć wizualny wskaźnik informujący). Ponadto właścicieli tych pakietów nadal będzie można przesłać nowe wersje pakietu.

Zmiany te zależą od następujących warunków i nakłada kilku dodatkowe ograniczenia:

- Tylko jeden właściciel pakietu musi mieć zastrzeżony prefiks dla wizualny wskaźnik informujący (dla pakietów z właścicielami wielu).

- Jeśli istnieje więcej niż jeden właściciel pakietu, gdy co najmniej jednego właściciela ma zastrzeżony prefiks i co najmniej jednego właściciela ma zastrzeżony prefiks, tylko właściciele z zastrzeżonym prefiksem można usunąć inne właściciele z zastrzeżonym prefiksem. Właścicieli, którzy nie mają prefiksu zastrzeżone nie można usunąć właścicieli z prefiksem zastrzeżone. Mogą nadal usuwać innych właścicieli, którzy nie mają też zastrzeżony prefiks.

- Gdy pakiet ma wizualny wskaźnik informujący, należy *zawsze* mają wizualny wskaźnik informujący (zagwarantowanie, że co najmniej jednego właściciela z zastrzeżonym prefiksem zawsze będzie pozostawać właściciela)

### <a name="advanced-prefix-reservation-scenarios"></a>Scenariusze rezerwacji prefiks zaawansowane

Istnieje kilka bardziej zaawansowanych scenariuszy rezerwacji prefiks opisane poniżej, w tym delegowanie subprefix i prefiksy oznaczanie jako publiczne. Poniżej przedstawiono bardziej zaawansowanych rezerwacje prefiksu, które mogą być wykonane. 

- Podczas rezerwowanie prefiksów identyfikatorów Właściciel może żądanie delegowania podzestawy prefiksu (lub prefiks) innych właścicieli. Na przykład jeśli "[Microsoft](https://www.nuget.org/profiles/microsoft)" właścicielem "firmy Microsoft.\*", ale "[aspnet](https://www.nuget.org/profiles/aspnet)" chce, aby zarezerwować "Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)" może możliwość delegowania "Microsoft.AspNet. \*"Aby [aspnet](https://www.nuget.org/profiles/aspnet) konta.

- Podczas rezerwowanie prefiksów identyfikatorów właściciela można upublicznić prefiksu. Nadal zapewni to ich wizualny wskaźnik informujący, pokazujący, że pakiet pochodzi z zastrzeżonego prefiksu, ale będzie **nie** block zgłoszenia przyszłych pakietu na prefiksie dla dowolnego właściciela. Jest to przydatne w przypadku projektów typu open source wielu uczestników — współautorzy top lub core może mieć prefiksu zarezerwowane, ale nadal może być otwarty, aby wszyscy współautorzy. 

### <a name="prefix-reservation-visual-indicator"></a>Prefiks wizualny wskaźnik informujący rezerwacji

Jeśli pakiet pochodzi z zastrzeżonym prefiksem, zobacz poniżej visual wskaźników [nuget.org](https://www.nuget.org/) galerii w programie Visual Studio 2017 w wersji 15.4 lub nowszej:

**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Proces aplikacji rezerwacji prefiks Identyfikatora

1. Przejrzyj akceptacji [kryteria prefiks Identyfikatora rezerwacji](#id-prefix-reservation-criteria).

2. Określić prefiksy, które mają zostać zarezerwowane dodatek do wszelkich [zaawansowanych scenariuszy rezerwacji prefiks](#advanced-prefix-reservation-scenarios) może wymagać.

3. Wyślij wiadomość e-mail do [ account@nuget.org ](mailto:account@nuget.org) z właścicielem nazwy wyświetlanej na [nuget.org](https://www.nuget.org/), a także wszelkie zastrzeżone prefiksy zażądano. Jeśli są delegowania podzestawy prefiks wielu właścicielom, upewnij się, wspomnieć o wszystkich nazw wyświetlanych właściciela i prefiksu podzbiory.

Po przesłaniu wniosku otrzymasz powiadomienie o zaakceptowaniu lub odrzuceniu (przy użyciu kryteriów, które spowodowały odrzucenie). Firma Microsoft może być konieczne zadać pytania identyfikujące potwierdzenie tożsamości właściciela.

### <a name="id-prefix-reservation-criteria"></a>Kryterium rezerwacji prefiks Identyfikatora

Podczas przeglądania wniosek o rezerwowanie prefiksów identyfikatorów [nuget.org](https://www.nuget.org/) zespołu będą oceniać aplikację przed poniższe kryteria. Nie wszystkie kryteria musi być spełnione dla prefiksu mają zostać zarezerwowane, ale aplikacja jest niedozwolony, jeśli nie jest dowód kryteria są spełniane (wraz z wyjaśnieniem, biorąc pod uwagę):

1. Prefiks Identyfikatora pakietu prawidłowo i jednoznacznie identyfikuje właściciel pakietu?

1. Czy znaczna liczba pakietów, które już zostały przesłane przez właściciela, w obszarze prefiks Identyfikatora pakietu?

1. Prefiks Identyfikatora pakietu jest wspólne coś, co nie powinny należeć do dowolnej poszczególnych właściciel lub organizacja?

1. Czy *nie* zarezerwowanie prefiks Identyfikatora pakietu powodować niejednoznaczności i niejasności dla społeczności?

1. Czy właściwości identyfikujących pakiety, które odpowiadają pakietu prefiks Identyfikatora czytelne i spójne (szczególnie Autor pakietu)?

## <a name="third-party-feed-provider-scenarios"></a>Innych firm, źródła danych dostawcy scenariuszy

Jeśli innych firm, dostawca strumieniowych źródeł jest zainteresowana implementowania usługi zapewnienie rezerwacje prefiksu, możesz to zrobić, modyfikując źródła danych usługi search w wersji 3 NuGet dostawców. Dodatek do usługi wyszukiwania kanału informacyjnego jest dodanie *zweryfikować* właściwości wraz z przykładami dla źródeł danych w wersji 3 poniżej. Klienta programu NuGet nie będzie obsługiwać dodanej właściwości w wersji 2, źródła danych.

Aby uzyskać więcej informacji, zobacz [dokumentacji interfejsu API usługi wyszukiwania](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Pakiet prefiks Identyfikatora rezerwacji sporu zasad
Jeśli uważasz, że właściciel na [NuGet.org](https://www.nuget.org) przypisano pakietu rezerwowanie prefiksów identyfikatorów, według kryteriów wymienionych powyżej, czy też narusza na dowolnym znakami towarowymi lub praw autorskich, poczty e-mail [ support@nuget.org ](mailto:support@nuget.org)z danego prefiks Identyfikatora, właściciel prefiks Identyfikatora i przyczynę sporu rezerwacji przypisane prefiks.

