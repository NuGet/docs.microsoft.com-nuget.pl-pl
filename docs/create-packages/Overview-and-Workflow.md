---
title: Omówienie i przepływ pracy tworzenia pakietów NuGet
description: Omówienie procesu tworzenia i publikowania pakietu NuGet, wraz z łączami do innych określonych części procesu.
author: karann-msft
ms.author: karann
ms.date: 07/26/2017
ms.topic: conceptual
ms.openlocfilehash: 6b41b23df115c45e830404afcf9defa23615bd7c
ms.sourcegitcommit: ce97dded7715f217ec44f6c8368ab0df19c38342
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/29/2018
ms.locfileid: "52615759"
---
# <a name="package-creation-workflow"></a>Przepływ pracy tworzenia pakietu

Tworzenie pakietu rozpoczyna się od skompilowanego kodu (zazwyczaj zestawów platformy .NET), którą chcesz pakietów i udostępnianie innym osobom za pośrednictwem galerii publicznej nuget.org lub prywatną galerię w Twojej organizacji. Ten pakiet może również zawierać dodatkowe pliki, takie jak plik readme, który jest wyświetlany, gdy pakiet jest zainstalowany i może zawierać przekształceń do niektórych plików projektu.

Pakiet może również służyć do tylko ściągania w dowolnej liczbie innych zależności bez zawierające swój własny kod. Taki pakiet to wygodny sposób dostarczania zestaw SDK, który składa się z wielu pakietów niezależnych. W innych przypadkach pakiet może zawierać tylko symbol (`.pdb`) plików, aby ułatwić debugowanie.

> [!Note]
> Podczas tworzenia pakietu do użytku przez innych programistów, ważne jest zrozumienie ich tworzenia zależności na pracy. Jako takie tworzenie i publikowanie pakietu oznacza również zobowiązania do naprawiania błędów i wprowadzania innych aktualizacji lub w bardzo najmniej wprowadzania pakietu, które są dostępne jako Otwórz źródło, aby inni pomogli do jego utrzymania.

Niezależnie od przypadku, tworzenie pakietu rozpoczyna się od przy wyborze rozwiązania, które zespoły i inne pliki do pakietu. Następnie utwórz plik manifestu, określonych jako `.nuspec` pliku, aby opisać zawartość pakietu wraz z jego identyfikatora, numer wersji, informacje o prawach autorskich, właściwości programu MSBuild i obiektów docelowych i wiele innych.

Gdy przygotowanej wszystkie niezbędne pliki w odpowiednie foldery i utworzono odpowiednie `.nuspec` pliku, możesz następnie użyć `nuget pack` polecenia (lub [MSBuild pakiet docelowy](../reference/msbuild-targets.md)) zostać umieszczona wszystko ze sobą `.nupkg` pliku. Następnie możesz przystąpić do wdrażania pakietu do dowolnego hosta umożliwia dostęp do niego innym deweloperom.

> [!Tip]
> Pakiet NuGet za pomocą `.nupkg` rozszerzenie jest po prostu plikiem ZIP. Aby łatwiej zbadać zawartość dowolnego pakietu, należy zmienić rozszerzenie `.zip` i rozwiń jego zawartość w zwykły sposób. Po prostu upewnij się zmienić rozszerzenie do `.nupkg` przed podjęciem próby przekazania jej do hosta.

Aby dowiedzieć się i zrozumieć proces tworzenia, zacznij od [Tworzenie pakietu](../create-packages/creating-a-package.md) który przeprowadzi Cię przez typowe procesy podstawowe do wszystkich pakietów.

Z tego miejsca można wziąć pod uwagę wiele różnych opcji dla pakietu:

- [Obsługa wielu platform docelowych](../create-packages/supporting-multiple-target-frameworks.md) opisano, jak utworzyć pakiet z wieloma wariantami dla różnych platform .NET.
- [Tworzenie zlokalizowanych pakietów](../create-packages/creating-localized-packages.md) opisuje struktury pakietów przy użyciu wielu zasobów języka oraz korzystanie z oddzielnych satelitarnej zlokalizowanych pakietów.
- [Wersja wstępna pakietów](../create-packages/prerelease-packages.md) pokazuje, jak zwolnić alpha, beta i rc pakiety do klientów, którzy są zainteresowani.
- [Źródło i przekształcenia pliku Config](../create-packages/source-and-config-file-transformations.md) w tym artykule opisano, jak zarówno jednokierunkowe zamiany tokenów w plikach, które są dodawane do projektu i zmodyfikować `web.config` i `app.config` przy użyciu ustawień, które są także wspierana się, gdy pakiet został odinstalowany .
- [Pakiety symboli](../create-packages/symbol-packages-snupkg.md) zawiera wskazówki dotyczące dostarczenie symboli w bibliotece, które pozwala użytkownikom można wkroczyć do kodu podczas debugowania.
- [Przechowywanie wersji pakietów](../reference/package-versioning.md) omówiono sposób zidentyfikować dokładną wersję, które umożliwiają zależności (inne pakiety, które zostaną zużyte na podstawie danego pakietu).
- [Pakiety natywne](../create-packages/native-packages.md) w tym artykule opisano proces tworzenia pakietu dla konsumentów C++.
- [Podpisywanie pakietów](../create-packages/sign-a-package.md) w tym artykule opisano proces dodawania podpisu cyfrowego do pakietu.

Gdy następnie wszystko gotowe do opublikowania pakietu na stronie nuget.org, postępuj zgodnie z prosty proces w [publikowanie pakietu](../create-packages/publish-a-package.md).

Jeśli chcesz używać prywatnych źródła danych zamiast nuget.org, zobacz [hostingu — Omówienie pakietów](../hosting-packages/overview.md)
