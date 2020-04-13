---
title: Co się stanie, gdy pakiet jest zainstalowany?
description: Szczegółowe informacje o procesie instalacji pakietu
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 1ae030c308b14b8884fb608c1683c8c46000b0bd
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "77036906"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Co się stanie, gdy zainstalowany jest pakiet NuGet?

Po prostu powiedział, różne narzędzia NuGet zazwyczaj utworzyć odwołanie do `packages.config`pakietu w pliku projektu lub , a następnie wykonać przywracanie pakietu, który skutecznie instaluje pakiet. Wyjątkiem jest `nuget install`, który tylko rozszerza `packages` pakiet do folderu i nie modyfikuje żadnych innych plików.

Ogólny proces wygląda następująco:

1. (Wszystkie narzędzia `nuget.exe`z wyjątkiem ) Zapisz identyfikator i wersję pakietu w `packages.config`pliku projektu lub .

   Jeśli narzędziem instalacyjnym jest Visual Studio lub dotnet CLI, narzędzie najpierw próbuje zainstalować pakiet. Jeśli pakiet jest niezgodny, nie jest dodawany `packages.config`do pliku projektu lub .

2. Nabyć pakiet:
   - Sprawdź, czy pakiet (według dokładnego identyfikatora i numeru wersji) jest już zainstalowany w folderze *pakietów globalnych,* zgodnie z opisem w sprawie [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej.](../consume-packages/managing-the-global-packages-and-cache-folders.md)

   - Jeśli pakiet nie znajduje się w folderze *pakietów globalnych,* spróbuj go pobrać ze źródeł wymienionych w [plikach konfiguracyjnych](../consume-packages/Configuring-NuGet-Behavior.md). W przypadku źródeł online spróbuj najpierw pobrać pakiet z `-NoCache` pamięci `nuget.exe` podręcznej `--no-cache` HTTP, `dotnet restore`chyba że jest określony za pomocą poleceń lub jest określony za pomocą pliku . (Visual Studio `dotnet add package` i zawsze używać pamięci podręcznej.) Jeśli pakiet jest używany z pamięci podręcznej, "CACHE" pojawia się w danych wyjściowych. Czas wygaśnięcia pamięci podręcznej ma 30 minut.

   - Jeśli pakiet nie znajduje się w pamięci podręcznej HTTP, spróbuj pobrać go ze źródeł wymienionych w konfiguracji. Jeśli pakiet zostanie pobrany, na wyjściu pojawią się "GET" i "OK". NuGet dzienniki http ruchu na normalnej szczegółowości.

   - Jeśli pakiet nie może zostać pomyślnie nabyty z dowolnego źródła, instalacja nie powiedzie się w tym momencie z błędem, takim jak [NU1103](../reference/errors-and-warnings/NU1103.md). Należy zauważyć, `nuget.exe` że błędy z poleceń pokazują tylko ostatnie źródło sprawdzone, ale oznacza, że pakiet nie był dostępny z dowolnego źródła.

   Podczas uzyskiwania pakietu może mieć zastosowanie kolejność źródeł w konfiguracji NuGet:

   - NuGet sprawdza źródła folderu lokalnego i udziałów sieciowych przed sprawdzeniem źródeł HTTP.

3. Zapisz kopię pakietu i inne informacje w folderze *http-cache,* zgodnie z opisem w [sprawie Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).

4. Jeśli pobrano, zainstaluj pakiet w folderze *pakietów globalnych* dla użytkownika. NuGet tworzy podfolder dla każdego identyfikatora pakietu, a następnie tworzy podfoldery dla każdej zainstalowanej wersji pakietu.

5. NuGet instaluje zależności pakietu zgodnie z wymaganiami. Ten proces może zaktualizować wersje pakietów w procesie, zgodnie z opisem w [rozpoznawaniu zależności](../concepts/dependency-resolution.md).

6. Zaktualizuj inne pliki i foldery projektu:

    - W przypadku projektów korzystających z packagereference należy `obj/project.assets.json`zaktualizować wykres zależności pakietu przechowywany w pliku . Zawartość pakietu nie są kopiowane do żadnego folderu projektu.
    - Aktualizacja `app.config` i/lub `web.config` jeśli pakiet używa [przekształceń plików źródłowych i konfiguracyjnych](../create-packages/source-and-config-file-transformations.md).

7. (Tylko program Visual Studio) Wyświetlanie pliku readme pakietu, jeśli jest dostępny, w oknie programu Visual Studio.

Ciesz się produktywnym kodowaniem dzięki pakietom NuGet!
