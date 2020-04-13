---
title: Usuwanie pakietów NuGet z nuget.org
description: Zasady dotyczące odsyłania pakietów z nuget.org; trwałe usunięcie nie jest obsługiwane, z wyjątkiem sytuacji, gdy pakiety naruszają inne zasady.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 3abe809d76e75801c2f936aba129d27ba7b64913
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "80581265"
---
# <a name="deleting-packages"></a>Usuwanie pakietów

nuget.org nie obsługuje trwałego usuwania pakietów. W ten sposób można podzielić każdy projekt w zależności od dostępności pakietu, zwłaszcza w przepływach pracy kompilacji, które obejmują przywracanie pakietu.

nuget.org obsługuje [nienotowanie pakietu,](#unlisting-a-package)co można zrobić na stronie zarządzania pakietami na stronie internetowej. Pakiety niepubliczne nie są wyświetlane w nuget.org ani w interfejsie użytkownika programu Visual Studio i nie są wyświetlane w wynikach wyszukiwania. Niepubliczne pakiety nadal można jednak pobrać i zainstalować przy użyciu dokładnego numeru wersji, który obsługuje przywracanie pakietu. Ponadto pakiety nienotowane na liście mogą być nadal odnajdowane w następujących konkretnych scenariuszach:

- Przywracanie pakietu przy użyciu `1.0.0-*`wersji przestawnych (na przykład ), jeśli najnowszy dostępny pakiet pasujący do ograniczeń wersji lub zależności jest pakietem niepublicznym.
- Replikacja pakietów za pośrednictwem katalogu (ponieważ katalog zawiera również pakiety niepubliczne).

## <a name="exceptions"></a>Wyjątki

W wyjątkowych sytuacjach, takich jak naruszenie praw autorskich i potencjalnie szkodliwe treści, pakiety mogą zostać usunięte ręcznie przez zespół NuGet. Pakiet można zgłosić za pomocą przycisku "Zgłoś nadużycie" na stronie szczegółów NuGet.org pakietu. Jeśli jesteś właścicielem pakietu, zaloguj się do swojego konta NuGet.org, aby uzyskać dostęp do pomocy technicznej NuGet za pomocą przycisku "Skontaktuj się z pomocą techniczną" na stronie szczegółów pakietu NuGet.org.

## <a name="prohibited-use"></a>Zabronione używanie

Pakiety, które spełniają którekolwiek z następujących kryteriów nie są dozwolone w publicznej galerii NuGet i zostaną natychmiast usunięte bez dyskusji. Właściciele pakietów zostaną jednak powiadomieni o usunięciu.

- Zawiera złośliwe oprogramowanie, adware lub wszelkiego rodzaju programy szpiegujące.
- Mają na celu uszkodzenie stacji roboczej dewelopera lub ich organizacji.
- Narusza prawa autorskie lub narusza licencje.
- Zawiera nielegalne treści.
- Są używane do kucać na identyfikatory pakietów, w tym pakiety, które mają zero zawartości produkcyjnej. Opakowania muszą zawierać kod lub właściciele muszą przyznać identyfikator osobie, która faktycznie ma produkt do wysyłki.
- Spróbuj zrobić galerii coś, co nie jest jawnie zaprojektowane do zrobienia.

Jeśli znajdziesz pakiet, który narusza którykolwiek z tych elementów, kliknij link **Zgłoś nadużycie** na stronie szczegółów pakietu i prześlij raport.

Należy zauważyć, że zespół NuGet i .NET Foundation zastrzega sobie prawo do zmiany tych kryteriów w dowolnym momencie.

## <a name="unlisting-a-package"></a>Odsłanianie paczki
Odsuwanie wersji pakietu powoduje, że ukrywa ją przed wyszukiwaniem i nuget.org stroną szczegółów pakietu. Dzięki temu istniejących użytkowników pakietu, aby kontynuować korzystanie z niego, ale zmniejsza nowe przyjęcie, ponieważ pakiet nie jest widoczny w wyszukiwaniu.

Kroki, aby odsunąć paczkę z listy:

1. Wybierz `Your account name` (w prawym górnym rogu) >`Manage packages` > `Published packages`
1. Wybierz ikonę "Zarządzaj pakietem"
1. Rozwiń sekcję "Aukcja" i wybierz wersję pakietu
1. Odznacz "Lista w wynikach wyszukiwania" i wybierz "Zapisz"

Wersja określonego pakietu została teraz niepubliczna. Aby to zweryfikować, wyloguj się ze swojego konta i przejdź do https://www.nuget.org/packages/YOUR-PACKAGE-NAME/strony pakietu (bez części wersji) np.: . Zobaczysz wszystkie wersje tego pakietu, które **nie** zostały wystawione na listę. Jednak właściciel pakietu, po zalogowaniu, może zobaczyć wszystkie wersje i ich stan aukcji.

Istnieje również możliwość przestarzałe wersji pakietu (w przypadku, gdy nie można usunąć wersję pakietu). Aby uzyskać więcej informacji na temat przestarzałego podawania wersji [pakietów, zobacz Przestarzałe pakiety](../deprecate-packages.md).
