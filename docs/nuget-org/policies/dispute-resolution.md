---
title: Rozwiązanie sporów o nazwę pakietu NuGet
description: Proces rozwiązywania sporów między wydawcami pakietów NuGet związanych z znakowanie, znaki towarowe i inne sytuacje konfliktu.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: a2f1fed578f1635296892ab925219f0f27883c02
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427498"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Rozwiązywanie sporów dotyczących nazw pakietów NuGet

Ten artykuł zawiera zalecany proces rozwiązywania problemów dla członków społeczności do rozwiązywania sporów z innymi wydawcami NuGet.

Załóżmy na przykład, że Northwind Traders tworzy system CRM, dla którego dostarczają sterowniki klienta jako msi do pobrania ze swojej strony internetowej. Nancy, niezależny deweloper, chce ułatwić korzystanie z biblioteki klienta Northwind i zamienia ją w `NorthwindTraders.Client`pakiet NuGet o nazwie . Później Northwind chce utworzyć oficjalny pakiet NuGet własnych dla biblioteki klienta i w związku z tym chciałby zakwestionować własność Nancy nazwy pakietu.

W tym scenariuszu Nancy nie wydaje się działać ze złymi intencjami, ale jest raczej wspieranie narzędzi Northwind i klientów, przyczyniając się do jej własnego czasu i kodu. W tym samym czasie Northwind jest prawowitym właścicielem nazwy Northwind.

Postępując zgodnie z poniższym procesem, Northwind i Nancy mogą współpracować w celu odpowiedniego rozwiązania, ponieważ obie są zainteresowane obsługą społeczności programistów. Zazwyczaj nie jest konieczne dla zespołu NuGet do zaangażowania; współpraca zwykle działa najlepiej. W rzeczywistości każdy spór zwrócił uwagę zespołu NuGet do tej pory został wypracowany bez zespołu konieczności wydania wyroku.

## <a name="process"></a>Proces

1. Skontaktuj się z właścicielami pakietu, z którymi masz spór, korzystając z linku Skontaktuj się z **właścicielami** na stronie szczegółów pakietu. Wyjaśnij swój problem w sposób miły i bezpośredni.
2. Wyślij kopię wiadomości do [support@nuget.org](mailto:support@nuget.org) tak, aby NuGet i .NET Foundation są świadomi twojego sporu.
3. Poczekaj maksymalnie 30 dni na rozwiązanie, [support@nuget.org](mailto:support@nuget.org) a następnie powiadom ponownie. Zespół wsparcia nuget.org zaangażuje się i spróbuje przepracować spór z obiema stronami.
