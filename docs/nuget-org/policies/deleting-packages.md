---
title: Usuwanie pakietów NuGet z repozytorium nuget.org
description: Zasady dotyczące unlisting pakiety z witryny nuget.org; trwałego usunięcia nie jest obsługiwane z wyjątkiem na pakiety naruszyć innych zasad.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 833f4a67bc75c5d650e85180b52ecd8f69218f15
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427510"
---
# <a name="deleting-packages"></a>Usuwanie pakietów

nuget.org nie obsługuje trwałe usuwanie pakietów. To spowoduje przerwanie każdego projektu, w zależności od dostępności pakietu, szczególnie w przypadku przepływów pracy kompilacji, które obejmują Przywracanie pakietu.

nuget.org jest obsługuje *unlisting* pakietu, co można zrobić na stronie pakiet zarządzania, w witrynie sieci web. Nieznajdujące się na liście pakietów nie są wyświetlane w witrynie nuget.org, lub w interfejsie użytkownika programu Visual Studio i nie są wyświetlane w wynikach wyszukiwania. Nieznajdujące się na liście pakietów, jednak nadal można pobrać i zainstalować za pomocą numeru wersji dokładnie, która obsługuje Przywracanie pakietu. Ponadto nieznajdujące się na liście pakietów, może nadal odnalezionych w następujących scenariuszach określonych:

- Pakiet przywracania przy użyciu wersji zmiennoprzecinkowego (na przykład `1.0.0-*`), gdy najnowszy pakiet dopasowania ograniczenia wersji lub zależności jest pakietu nieznajdujące się na liście.
- Replikacja pakietów w wykazie (jak katalog zawiera również nieznajdujące się na liście pakietów).

## <a name="exceptions"></a>Wyjątki

W sytuacjach wyjątkowych, takich jak naruszenie praw autorskich i potencjalnie niebezpieczną zawartość pakietów można je usunąć ręcznie przez zespół programu NuGet. Możesz zgłosić pakietu przy użyciu przycisku "Zgłoś nadużycie" na stronie szczegółów pakietu NuGet.org. Jeśli jesteś właścicielem pakietu i zaloguj się na swoje konto NuGet.org, aby osiągnąć obsługę pakietów NuGet za pomocą przycisku "Się z pomocą techniczną" na stronie szczegółów pakietu NuGet.org.

## <a name="prohibited-use"></a>Zabronione korzystanie

Pakiety, które spełniają dowolne z poniższych kryteriów nie są dozwolone w publicznej galerii pakietów NuGet i zostaną natychmiast usunięte bez dyskusji. Jednak pakietu będą właścicielami, otrzymywać powiadomienia o usunięciu.

- Zawiera złośliwego oprogramowania, oprogramowaniem reklamowym lub dowolnych programów szpiegujących.
- Są przeznaczone do negatywnie wpłynąć na stacji roboczej dewelopera lub jego organizację.
- Narusza prawa autorskie lub narusza licencji.
- Zawartość jest niedozwolone.
- Są używane do squat dotyczące identyfikatorów pakietu, w tym pakietów, które ma zero produktywność zawartości. Pakiety mogą zawierać kod lub właściciele należy przyznać identyfikator do osoby, która faktycznie zawiera produktu do wysłania.
- Spróbuj spowodować galerii, zadania, które nie zostały jawnie ustalono, aby zrobić.

Jeśli znajdziesz pakietu, który narusza dowolnego z tych elementów, kliknij przycisk **Zgłoś nadużycie** łącze na stronie szczegółów pakietu i przesłać raport.

Należy pamiętać, że zespół NuGet i .NET Foundation zastrzega sobie prawo w dowolnym momencie zmienić te kryteria.
