---
title: Rozwiązywanie sporów nazwa pakietu NuGet
description: Proces rozstrzygania sporów między wydawcy pakietu NuGet związanych z znakowanie, znaków towarowych i innych sytuacjach konflikt.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: a2f1fed578f1635296892ab925219f0f27883c02
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427498"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Rozwiązywanie sporów nazwy pakietów NuGet

Ten artykuł zawiera zalecane rozwiązanie procesu dla członków społeczności rozstrzygania sporów identyfikatorami różnych wydawców NuGet.

Na przykład załóżmy, że Northwind Traders sprawia, że system CRM, dla którego zapewniają sterowników klienta jako do pobrania plik MSI z ich witryny sieci Web. Nancy, niezależny Deweloper chce ułatwić używanie biblioteki klienckiej firmy Northwind i konwertuje go na pakiet NuGet o nazwie `NorthwindTraders.Client`. Później Northwind chce utworzyć oficjalne pakietu NuGet własne ich biblioteki klienta usługi, a w związku z tym chce rozstrzygania Ireny własności nazwy pakietu.

W tym scenariuszu Nancy wydaje się być działające z zamiarów zły, ale raczej obsługuje narzędzia firmy Northwind i klientów, przekazując własne czasu i kod. W tym samym czasie Northwind jest prawowitym właścicielem nazwy Northwind.

Postępując zgodnie z procesem opisanym niżej, Northwind i Nancy mogą pracować razem odpowiednie rozwiązanie, ponieważ oba są zainteresowani obsługująca społeczności deweloperów. Zazwyczaj nie jest konieczne dla zespołu NuGet do angażowania; współpraca zazwyczaj działa najlepiej. W rzeczywistości sporów, każdy zespół NuGet uwagi do daty wypracowała zostało bez zespołu konieczności przekazywania orzeczenia.

## <a name="process"></a>Proces

1. Skontaktuj się z właścicielami pakietu mają sporu przy użyciu **skontaktuj się z właścicielami** łącze na stronie szczegółów pakietu. Opis problemu w rodzaju i w sposób bezpośredni.
2. Wyślij kopię wiadomości dla [ support@nuget.org ](mailto:support@nuget.org) tak, aby NuGet i .NET Foundation świadomość spór.
3. Poczekaj maksymalnie 30 dni na rozwiązanie problemu, a następnie powiadom [ support@nuget.org ](mailto:support@nuget.org) ponownie. Zespół pomocy technicznej w witrynie nuget.org będzie Dołącz do społeczności, a następnie spróbuj do pracy za pośrednictwem sporu z obu stron.
