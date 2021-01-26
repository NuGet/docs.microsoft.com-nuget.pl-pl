---
title: Omówienie i przepływ pracy tworzenia pakietów NuGet
description: Przegląd procesu tworzenia i publikowania pakietu NuGet wraz z łączami do innych określonych części procesu.
author: JonDouglas
ms.author: jodou
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: d34f8e73dce64a58393433637067651fced08173
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774672"
---
# <a name="package-creation-workflow"></a>Przepływ pracy tworzenia pakietu

Tworzenie pakietu rozpoczyna się od skompilowanego kodu (zazwyczaj zestawy .NET), które mają być spakowane i udostępniane innym osobom przy użyciu publicznej galerii nuget.org lub prywatnej galerii w organizacji. Pakiet może również zawierać dodatkowe pliki, takie jak plik Readme, który jest wyświetlany podczas instalowania pakietu, i może zawierać przekształcenia do niektórych plików projektu.

Pakiet może również umożliwiać ściąganie tylko w dowolnej liczbie innych zależności bez konieczności popełnienia kodu. Taki pakiet jest wygodnym sposobem na dostarczenie zestawu SDK składającego się z wielu niezależnych pakietów. W innych przypadkach pakiet może zawierać tylko pliki symboli ( `.pdb` ), aby pomóc w debugowaniu.

> [!Note]
> W przypadku tworzenia pakietu do użytku przez innych deweloperów ważne jest, aby zrozumieć, że zajmują one zależność od pracy. W związku z tym tworzenie i publikowanie pakietu wiąże się również z zobowiązaniem do naprawienia usterek i wprowadzania innych aktualizacji lub w przypadku, gdy pakiet jest dostępny jako Open Source, dzięki czemu inne osoby mogą pomóc w utrzymaniu tego pakietu.

Bez względu na to, że tworzenie pakietu rozpoczyna się od podejmowania decyzji o jego identyfikatorze, numerze wersji, licencji, informacji o prawach autorskich i innej wymaganej zawartości. Po wykonaniu tych czynności możesz użyć polecenia "Pack", aby umieścić wszystkie dane w `.nupkg` pliku. Ten plik można opublikować w źródle danych NuGet, takim jak nuget.org.

> [!Tip]
> Pakiet NuGet z `.nupkg` rozszerzeniem jest po prostu plikiem zip. Aby łatwo przeanalizować zawartość dowolnego pakietu, Zmień rozszerzenie na `.zip` i rozwiń jego zawartość w zwykły sposób. Pamiętaj, aby `.nupkg` przed podjęciem próby przekazania do hosta zmienić rozszerzenie.

Aby poznać i zrozumieć proces tworzenia, Zacznij od [utworzenia pakietu](../create-packages/creating-a-package.md) , który przeprowadzi Cię przez podstawowe procesy wspólne dla wszystkich pakietów.

Z tego miejsca można wziąć pod uwagę wiele innych opcji pakietu:

- [Obsługa wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md) zawiera opis sposobu tworzenia pakietu z wieloma wariantami dla różnych środowisk .NET Framework.
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md) zawiera opis sposobu tworzenia struktury pakietu z wieloma zasobami językowymi i używania oddzielnych zlokalizowanych pakietów satelickich.
- [Pakiety wersji wstępnej](../create-packages/prerelease-packages.md) pokazują, jak wystawić pakiety alfa, beta i RC dla klientów, którzy są zainteresowani.
- [Przekształcenia plików źródłowych i konfiguracji](../create-packages/source-and-config-file-transformations.md) opisują sposób, w jaki można wykonać zarówno jednokierunkowe zamiany tokenów w plikach, które są dodawane do projektu, i modyfikować `web.config` i `app.config` z ustawieniami, które również są tworzone podczas odinstalowywania pakietu.
- [Pakiety symboli](../create-packages/symbol-packages-snupkg.md) udostępniają wskazówki dotyczące dostarczania symboli dla biblioteki, które umożliwiają klientom wkroczenie się do kodu podczas debugowania.
- Informacje o [wersji pakietu](../concepts/package-versioning.md) omawiają, jak zidentyfikować dokładne wersje, które są dozwolone dla zależności (inne pakiety, które są używane z pakietu).
- [Pakiety natywne](../guides/native-packages.md) opisują proces tworzenia pakietu dla użytkowników języka C++.
- [Pakiety podpisywania](../create-packages/sign-a-package.md) opisują proces dodawania podpisu cyfrowego do pakietu.

Gdy wszystko będzie gotowe do opublikowania pakietu w programie nuget.org, postępuj zgodnie z prostym procesem w [publikacji pakietu](../nuget-org/publish-a-package.md).

Jeśli chcesz użyć prywatnego kanału informacyjnego zamiast nuget.org, zobacz [Omówienie pakietów hostingu](../hosting-packages/overview.md)
