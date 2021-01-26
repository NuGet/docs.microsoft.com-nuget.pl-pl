---
title: Usuwanie pakietów NuGet z nuget.org
description: Zasady dla pakietów unlisting z nuget.org; trwałe usuwanie nie jest obsługiwane, z wyjątkiem przypadków, gdy pakiety naruszają inne zasady.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: e5c62177b40162cb8b6b37b0d272fb7a945156c1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775712"
---
# <a name="deleting-packages"></a>Usuwanie pakietów

nuget.org nie obsługuje trwałego usuwania pakietów. Wykonanie tej operacji spowodowałoby przerwanie każdego projektu w zależności od dostępności pakietu, szczególnie w przypadku przepływów pracy kompilacji, które obejmują przywracanie pakietów.

Usługa nuget.org obsługuje [listę pakietów](#unlisting-a-package), które można wykonać na stronie Zarządzanie pakietami w witrynie sieci Web. Nieznajdujące się na liście pakiety nie są wyświetlane w programie nuget.org lub w interfejsie użytkownika programu Visual Studio i nie są wyświetlane w wynikach wyszukiwania. Jednak pakiety nieznajdujące się na liście nadal mogą być pobierane i instalowane przy użyciu dokładnego numeru wersji, który obsługuje przywracanie pakietów. Ponadto pakiety nieznajdujące się na liście mogą być nadal odnajdywane w następujących scenariuszach:

- Przywracanie pakietu przy użyciu wersji zmiennoprzecinkowych (na przykład `1.0.0-*` ), Jeśli najnowszy dostępny pakiet zgodny z ograniczeniami wersji lub zależności jest pakietem nieznajdującym się na liście.
- Replikacja pakietów przez wykaz (ponieważ katalog zawiera również nieznajdujące się na liście pakiety).

## <a name="exceptions"></a>Wyjątki

W wyjątkowych sytuacjach, takich jak naruszenie praw autorskich i potencjalnie szkodliwa zawartość, pakiety mogą być usuwane ręcznie przez zespół NuGet. Możesz zgłosić pakiet za pomocą przycisku "Zgłoś nadużycie" na stronie szczegółów pakietu NuGet.org. Jeśli jesteś właścicielem pakietu, zaloguj się do swojego konta usługi NuGet.org, aby uzyskać pomoc techniczną NuGet przy użyciu przycisku "Skontaktuj się z pomocą techniczną" na stronie szczegółów pakietu NuGet.org.

## <a name="prohibited-use"></a>Zabronione użycie

Pakiety spełniające następujące kryteria są niedozwolone w publicznej galerii NuGet i zostaną natychmiast usunięte bez dyskusji. Właściciele pakietu będą jednak powiadamiani o usunięciu.

- Zawiera złośliwe oprogramowanie, programy reklamujące lub dowolny rodzaj programów szpiegujących.
- Są przeznaczone do szkodliwej stacji roboczej lub organizacji dewelopera.
- Narusza prawa autorskie lub narusza licencje.
- Zawiera niedozwoloną zawartość.
- Są używane do squat w identyfikatorach pakietów, w tym pakietów, które mają zerową zawartość produkcyjną. Pakiety muszą zawierać kod lub właściciele muszą oddzielać identyfikator osobie, która rzeczywiście dysponuje produktem do wysłania.
- Podjęto próbę przeprowadzenia przez galerię niejawnie zaprojektowanej do wykonania.

Jeśli znajdziesz pakiet, który narusza którykolwiek z tych elementów, kliknij link **Zgłoś nadużycie** na stronie Szczegóły pakietu i prześlij raport.

Należy pamiętać, że zespół NuGet i .NET Foundation rezerwują prawo do zmiany tych kryteriów w dowolnym momencie.

## <a name="unlisting-a-package"></a>Wylistowanie pakietu
Wylistowanie wersji pakietu powoduje ukrycie jej w programie Search i na stronie szczegółów pakietu nuget.org. Dzięki temu istniejący użytkownicy pakietu mogą nadal z niego korzystać, ale redukuje nowe wdrożenie, ponieważ pakiet nie jest widoczny w wyszukiwaniu.

Procedura wystawiania pakietu:

1. Wybierz `Your account name` (w prawym górnym rogu) >`Manage packages` > `Published packages`
1. Wybierz ikonę "Zarządzaj pakietem"
1. Rozwiń sekcję "Lista" i wybierz wersję pakietu
1. Usuń zaznaczenie pozycji "Wyświetl w wynikach wyszukiwania" i wybierz pozycję "Zapisz"

Określona wersja pakietu została teraz niewymieniona. Aby to sprawdzić, Wyloguj się z konta i przejdź do strony pakietu (bez części wersji), np.: https://www.nuget.org/packages/YOUR-PACKAGE-NAME/ . Zobaczysz wszystkie wersje tego pakietu, które **nie** zostały niewyświetlone na liście. Jednak właściciel pakietu, po zalogowaniu, może zobaczyć wszystkie wersje i ich stan.

Istnieje również możliwość wycofania wersji pakietu (w przypadku, gdy nie można usunąć wersji pakietu). Aby uzyskać więcej informacji na temat przestarzałych wersji pakietu, zobacz [Przestarzałe pakiety](../deprecate-packages.md).
