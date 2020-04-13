---
title: Omówienie i przepływ pracy tworzenia pakietów NuGet
description: Omówienie procesu tworzenia i publikowania pakietu NuGet z łączami do innych określonych części procesu.
author: karann-msft
ms.author: karann
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: e4b9f6dae3a4be69e523888cc9bd2f212b45829c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488846"
---
# <a name="package-creation-workflow"></a>Przepływ pracy tworzenia pakietów

Tworzenie pakietu rozpoczyna się od skompilowanego kodu (zazwyczaj zestawów .NET), który chcesz spakować i udostępnić innym osobom za pośrednictwem galerii nuget.org publicznych lub galerii prywatnej w organizacji. Pakiet może również zawierać dodatkowe pliki, takie jak readme, który jest wyświetlany po zainstalowaniu pakietu i może zawierać przekształcenia do niektórych plików projektu.

Pakiet może również służyć tylko ściągać w dowolnej liczbie innych zależności, bez konieczności zawierania kodu własnego. Taki pakiet jest wygodnym sposobem dostarczania zestawu SDK, który składa się z wielu niezależnych pakietów. W innych przypadkach pakiet może zawierać`.pdb`tylko pliki symbolu ( ) ułatwiające debugowanie.

> [!Note]
> Podczas tworzenia pakietu do użytku przez innych deweloperów, ważne jest, aby zrozumieć, że biorą zależności od pracy. W związku z tym utworzenie i opublikowanie pakietu oznacza również zobowiązanie do naprawiania błędów i wprowadzania innych aktualizacji lub przynajmniej udostępniania pakietu jako open source, aby inni mogli pomóc w jego utrzymaniu.

Niezależnie od przypadku, tworzenie pakietu rozpoczyna się od podjęcia decyzji o jego identyfikatorze, numerze wersji, licencji, informacjach o prawach autorskich i wszelkich innych niezbędnych treściach. Po zakończeniu możesz użyć polecenia "pack", aby umieścić `.nupkg` wszystko razem w pliku. Ten plik można opublikować w kanale NuGet, takim jak nuget.org.

> [!Tip]
> Pakiet NuGet z `.nupkg` rozszerzeniem jest po prostu plikiem ZIP. Aby łatwo sprawdzić zawartość dowolnego pakietu, `.zip` zmień rozszerzenie na i rozwiń jego zawartość w zwykły sposób. Pamiętaj tylko, aby zmienić `.nupkg` rozszerzenie z powrotem na przed podjęciem próby przesłania go do hosta.

Aby dowiedzieć się i zrozumieć proces tworzenia, należy rozpocząć od [tworzenia pakietu,](../create-packages/creating-a-package.md) który prowadzi użytkownika przez podstawowe procesy wspólne dla wszystkich pakietów.

W tym miejscu możesz rozważyć kilka innych opcji dla pakietu:

- [Obsługa wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md) opisano sposób tworzenia pakietu z wieloma wariantami dla różnych platform .NET Frameworks.
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md) opisuje sposób struktury pakietu z wielu zasobów językowych i jak używać oddzielnych zlokalizowanych pakietów satelitarnych.
- [Pakiety w wersji wstępnej](../create-packages/prerelease-packages.md) pokazuje, jak zwolnić pakiety alfa, beta i rc do tych klientów, którzy są zainteresowani.
- [Transformacje plików źródłowych i konfiguracyjnych](../create-packages/source-and-config-file-transformations.md) opisano, jak można wykonać zarówno jednokierunkowe zastępowanie tokenów w plikach dodawanych do projektu, jak i modyfikować `web.config` i `app.config` z ustawieniami, które są również wycofywane po odinstalowaniu pakietu.
- [Pakiety symboli](../create-packages/symbol-packages-snupkg.md) oferuje wskazówki dotyczące dostarczania symboli dla biblioteki, które umożliwiają konsumentom krok do kodu podczas debugowania.
- [Przechowywanie wersji pakietu](../concepts/package-versioning.md) w tym artykule omówiono sposób identyfikowania dokładnych wersji, które zezwalają na zależności (inne pakiety, które można wykorzystać z pakietu).
- [Pakiety natywne](../guides/native-packages.md) opisuje proces tworzenia pakietu dla konsumentów języka C++.
- [Podpisywanie pakietów](../create-packages/sign-a-package.md) opisuje proces dodawania podpisu cyfrowego do pakietu.

Gdy będziesz gotowy do opublikowania pakietu do nuget.org, postępuj zgodnie z prostym procesem w [publikuj pakiet](../nuget-org/publish-a-package.md).

Jeśli chcesz użyć prywatnego kanału informacyjnego zamiast nuget.org, zobacz [Omówienie pakietów hostingowych](../hosting-packages/overview.md)
