---
title: Usunięcie pakietów NuGet z nuget.org
description: Zasady unlisting pakietów z nuget.org; trwałe usuwanie nie jest obsługiwany z wyjątkiem na pakiety narusza inne zasady.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: bea4f1589f184d38da27e5d82c3ce17a183fbdd1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="deleting-packages"></a>Usunięcie pakietów

nuget.org nie obsługuje trwałe usuwanie pakietów. W ten sposób spowoduje przerwanie każdy projekt w zależności od dostępności pakietu, szczególnie w przypadku przepływów pracy kompilacji, które obejmują Przywracanie pakietu.

obsługuje jest nuget.org *unlisting* pakietu, można to zrobić na stronie pakiet zarządzania w witrynie sieci web. Nieznajdujące się na liście pakietów nie są wyświetlane na nuget.org lub w interfejsie użytkownika programu Visual Studio i nie są wyświetlane w wynikach wyszukiwania. Nieznajdujące się na liście pakietów, jednak nadal można pobrać i zainstalować przy użyciu numeru dokładnej wersji, która obsługuje Przywracanie pakietu. Ponadto nieznajdujące się na liście pakietów nadal są wykrywane w następujących scenariuszach określonych:

- Przywracanie przestawne wersji pakietów (na przykład `1.0.0-*`), jeśli jest to najnowsza wersja pakietu dostępne dopasowania ograniczenia wersji lub zależności to pakiet nieznajdujące się na liście.
- Replikacja pakietów za pomocą wykazu (zgodnie z katalogu zawiera również nieznajdujące się na liście pakietów).

## <a name="exceptions"></a>Wyjątki

W sytuacjach wyjątkowych, takich jak praw autorskich i potencjalnie niebezpieczną zawartość pakiety mogą zostać usunięte ręcznie przez zespół NuGet. Prześlij żądanie pomocy technicznej za pośrednictwem [galerii NuGet](http://www.nuget.org) do rozpoczęcia procesu.

## <a name="prohibited-use"></a>Zabronione użycie

Pakiety, które jest spełnienie któregoś z następujących kryteriów nie są dozwolone w publicznej galerii NuGet i zostaną natychmiast usunięte bez dyskusji. Jednak pakiet zostanie właścicieli, otrzymywać powiadomienia o usunięciu.

- Zawiera złośliwego oprogramowania, programów z reklamami lub dowolnego rodzaju programów szpiegujących.
- Mają na celu negatywnie wpłynąć na stacji roboczej dewelopera lub organizacji.
- Narusza prawa autorskie lub narusza licencji.
- Zawartość niedozwolona.
- Są używane do squat na identyfikatorach pakietu, w tym pakietów, które ma zerowy produktywności zawartości. Pakiety musi zawierać kod lub właściciele należy przyznać identyfikator do osoby, która faktycznie zawiera produktu do wysłania.
- Próba utworzenia czymś, które nie są jawnie zostało zaprojektowane do galerii.

Jeśli pakiet, który narusza te elementy, kliknij przycisk **zgłaszania nadużyć** łącze na stronie szczegółów pakietu i przesłać raportu.

Należy pamiętać, że zespół NuGet i .NET Foundation zastrzega sobie prawo w dowolnym momencie zmienić te kryteria.
