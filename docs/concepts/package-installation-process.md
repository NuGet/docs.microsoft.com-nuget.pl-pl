---
title: Co się stanie, gdy jest zainstalowany pakiet?
description: Szczegółowe informacje na temat procesu instalacji pakietu
author: karann-msft
ms.author: karann
ms.date: 0/20/2019
ms.topic: conceptual
ms.openlocfilehash: 9ea0e6d28fa7af6e4061f762ea9af06c3028c247
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427654"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Co się dzieje po zainstalowaniu pakietu NuGet?

Był wyświetlany różne narzędzia NuGet zazwyczaj utworzyć odwołanie do pakietu w pliku projektu lub `packages.config`, następnie wykonać przywracania pakietów skuteczne pakiet zostanie zainstalowany. Wyjątek stanowi `nuget install`, który rozwija tylko pakiet do `packages` folder i wszystkie inne pliki nie powoduje modyfikacji.

Ogólny proces jest następująca:

1. (Wszystkie narzędzia, z wyjątkiem `nuget.exe`) Zapisz identyfikator pakietu i wersję do pliku projektu lub `packages.config`.

   Jeśli narzędzie instalacji programu Visual Studio lub wiersz polecenia dotnet, narzędzie najpierw próbuje zainstalować pakiet. Jeśli jest niezgodna, pakiet nie jest dodawany do pliku projektu lub `packages.config`.

2. Pobieranie pakietu:
   - Sprawdź, czy pakiet (przez dokładny identyfikator oraz numer wersji) jest już zainstalowany w *globalnymi pakietami* folderu zgodnie z opisem na [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).

   - Jeśli pakiet nie znajduje się w *globalnymi pakietami* folderze próbują pobrać go ze źródeł wymienione na liście [pliki konfiguracyjne](../consume-packages/Configuring-NuGet-Behavior.md). Dla źródeł online próbował najpierw Pobierz pakiet z pamięci podręcznej HTTP, chyba że `-NoCache` jest określony za pomocą `nuget.exe` poleceń lub `--no-cache` jest określony za pomocą `dotnet restore`. (Visual Studio i `dotnet add package` zawsze używać pamięci podręcznej.) Jeśli pakiet jest używany z pamięci podręcznej, "Pamięć PODRĘCZNĄ" pojawia się w danych wyjściowych. Pamięć podręczna zawiera 30-minutowy czas wygaśnięcia.

   - Pakiet nie jest w pamięci podręcznej HTTP, próba go pobrać ze źródła wymienione w konfiguracji. Jeśli pakiet został pobrany, "GET" i "OK" są wyświetlane w danych wyjściowych. NuGet dzienniki ruchu http na normalne poziom szczegółowości.

   - Jeśli pakiet nie może pomyślnie uzyskana z dowolnymi źródłami, instalacja nie powiedzie się na tym etapie ze względu na błąd taki jak [NU1103](../reference/errors-and-warnings/NU1103.md). Uwaga tego błędy z `nuget.exe` Pokaż polecenia tylko ostatni źródło opcja jest zaznaczona, ale oznacza, że pakiet nie była dostępna z dowolnego źródła.

   Podczas uzyskiwania pakietu, mogą mieć zastosowanie kolejność źródeł w konfiguracji NuGet:

   - NuGet sprawdza źródła lokalnego folderu i udziałów sieciowych przed sprawdzeniem źródła HTTP.

3. Zapisz kopię pakietu oraz inne informacje w *pamięci podręcznej http* folderu zgodnie z opisem na [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).

4. Jeśli pobrane, należy zainstalować pakiet w poszczególnych użytkowników *globalnymi pakietami* folderu. NuGet tworzy osobny podfolder dla każdego identyfikatora pakietu, a następnie tworzy oddzielne podfoldery dla każdej zainstalowanej wersji pakietu.

5. NuGet instaluje zależności pakietów, zgodnie z potrzebami. Ten proces może aktualizować wersje pakietów w procesie, zgodnie z opisem w [rozpoznawania zależności](../consume-packages/dependency-resolution.md).

6. Aktualizacja innych projektów, plików i folderów:

    - W przypadku projektów przy użyciu funkcji PackageReference, zaktualizuj wykres zależności pakietu, które są przechowywane w `obj/project.assets.json`. Zawartość pakietu, sami nie są kopiowane do dowolnego folderu projektu.
    - Aktualizacja `app.config` i/lub `web.config` Jeśli korzysta z pakietu [źródła i konfiguracji pliku przekształcenia](../create-packages/source-and-config-file-transformations.md).

7. (Tylko visual Studio) Wyświetl plik readme pakietu, jeśli to możliwe, w oknie programu Visual Studio.

Korzystaj z usługi produktywne kodowanie dzięki pakiety NuGet!
