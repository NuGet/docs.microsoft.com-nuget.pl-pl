---
title: "Rozwiązywanie sporów nazwa pakietu NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Proces rozwiązywanie sporów między związane z znakowania, znaków towarowych i innych konfliktów wydawcy pakietu NuGet."
keywords: "Sporów pakietu NuGet, rozwiązywanie sporów NuGet, proces rozpoznawania sporów"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 589fe4e7d2b05f3d589dcc70e78e7199d7e717c8
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Rozwiązywanie sporów nazwy pakietu NuGet

W tym artykule przedstawiono proces zalecane rozwiązanie członkom społeczności, rozwiązywanie sporów z innych wydawców NuGet.

Na przykład załóżmy, że Northwind Traders sprawia, że systemu CRM, dla którego zapewniają sterowników klienta jako MSI do pobrania z witryny sieci Web. Irena, niezależnie od dewelopera wymaga ułatwić korzystanie z biblioteki klienta firmy Northwind i konwertuje go na pakietu NuGet o nazwie `NorthwindTraders.Client`. Później Northwind chce utworzyć oficjalnego pakietu NuGet w swoich własnych ich biblioteki klienta i w związku z tym chcesz rozstrzygania własność firmy Irena nazwę pakietu.

W tym scenariuszu Irena nie wydaje się być działające z zamiarów zły, ale raczej obsługuje narzędzia i klientów firmy Northwind, podając własne czasu i kod. W tym samym czasie Northwind jest uzasadnione właścicielem nazwy Northwind.

Wykonując z procesem opisanym niżej Northwind i Irena mogą współdziałać ze sobą odpowiedniego rozwiązania, ponieważ zarówno zainteresowani obsługująca społeczności deweloperów. Zwykle nie jest niezbędna dla zespołu NuGet do angażowania; Współpraca zwykle działa się najlepiej. W rzeczywistości co sporów zespołu NuGet uwagi do daty została działał bez zespołu konieczności przekazać ocenie.

## <a name="process"></a>Proces

1. Skontaktuj się z właściciele pakietu masz sporów przy użyciu **właścicieli skontaktuj się z** łącze na stronie Szczegóły pakietu. Opis problemu w rodzaju i w sposób bezpośredni.
1. Wyślij kopię wiadomości [ support@nuget.org ](mailto:support@nuget.org) tak, aby NuGet i .NET Foundation wiedzą z sporów.
1. Poczekaj maksymalnie 30 dni rozwiązanie problemu, a następnie powiadom [ support@nuget.org ](mailto:support@nuget.org) ponownie. Nuget.org zespołem pomocy technicznej będzie angażowanie i spróbuj pracy za pośrednictwem sporów z obu stron.
