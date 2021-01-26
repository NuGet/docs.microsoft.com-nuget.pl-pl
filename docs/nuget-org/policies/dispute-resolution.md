---
title: Nazwa pakietu NuGet rozstrzyganie sporu
description: Proces rozwiązywania sporów między wydawcami pakietów NuGet związanymi z marką, znakami towarowymi i innymi sytuacjami związanymi z konfliktem.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: d9ed7de95a1f38ea2c288b28958519b1dff0e595
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775661"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Rozwiązywanie sporów dotyczących nazw pakietów NuGet

Ten artykuł zawiera zalecany proces rozwiązywania problemów z członkami społeczności w celu rozwiązywania sporów z innymi wydawcami programu NuGet.

Załóżmy na przykład, że firma Northwind Traders tworzy system CRM, dla którego udostępnia sterowniki klientów jako plik MSI do pobrania z witryny sieci Web. W firmie Nancy niezależny deweloper chce ułatwić korzystanie z biblioteki klienta Northwind i przekształcić ją w pakiet NuGet o nazwie `NorthwindTraders.Client` . Później firma Northwind chce utworzyć urzędowy pakiet NuGet własny dla swojej biblioteki klienckiej, a tym samym zachodzić na spór Nancy na własność nazwy pakietu.

W tym scenariuszu Nancy nie działa z nieprawidłowymi intencjami, ale raczej obsługuje narzędzia i klientów Northwind, tworząc własny czas i kod. W tym samym czasie Northwind jest uprawnionym właścicielem nazwy Northwind.

Postępując zgodnie z poniższym procesem, Northwind i Nancy mogą współdziałać z odpowiednimi rozwiązaniami, ponieważ obie osoby chcą obsługiwać społeczność deweloperów. Zwykle nie jest to konieczne, aby zespół NuGet stał się zainteresowany; Współpraca zwykle działa najlepiej.

## <a name="process"></a>Proces

1. Skontaktuj się z właścicielami pakietu, korzystając z linku **skontaktuj się z właścicielem** na stronie Szczegóły pakietu. Wyjaśnij swój problem w rodzaju i bezpośrednio.
2. Wyślij kopię wiadomości w [support@nuget.org](mailto:support@nuget.org) taki sposób, aby NuGet i .NET Foundation były świadome sporu.
3. Poczekaj maksymalnie 30 dni na rozwiązanie, a następnie Powiadom [support@nuget.org](mailto:support@nuget.org) ponownie. Zespół pomocy technicznej nuget.org będzie uczestniczyć w pracy, a następnie spróbuje przeprowadzić Cię przez spór z obiema stronami.
