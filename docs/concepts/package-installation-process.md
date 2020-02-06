---
title: Co się stanie po zainstalowaniu pakietu?
description: Szczegółowe informacje na temat procesu instalacji pakietu
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 1ae030c308b14b8884fb608c1683c8c46000b0bd
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036906"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Co się stanie po zainstalowaniu pakietu NuGet?

Po prostu różne narzędzia NuGet zwykle tworzą odwołanie do pakietu w pliku projektu lub `packages.config`, a następnie wykonaj przywracanie pakietów, które skutecznie zainstaluje pakiet. Wyjątek jest `nuget install`, który rozszerza tylko pakiet do folderu `packages` i nie modyfikuje innych plików.

Ogólny proces jest następujący:

1. (Wszystkie narzędzia z wyjątkiem `nuget.exe`) Zapisz identyfikator pakietu i wersję w pliku projektu lub `packages.config`.

   Jeśli narzędzie instalacji jest Visual Studio lub interfejs wiersza polecenia dotnet, narzędzie najpierw próbuje zainstalować pakiet. Jeśli jest niezgodny, pakiet nie jest dodawany do pliku projektu ani `packages.config`.

2. Pobierz pakiet:
   - Sprawdź, czy pakiet (według dokładnych identyfikator i numer wersji) jest już zainstalowany w folderze *pakiety globalne* , zgodnie z opisem w temacie [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).

   - Jeśli pakiet nie znajduje się w folderze *pakiety globalne* , spróbuj pobrać go ze źródeł wymienionych w [plikach konfiguracji](../consume-packages/Configuring-NuGet-Behavior.md). W przypadku źródeł online spróbuj najpierw pobrać pakiet z pamięci podręcznej HTTP, chyba że `-NoCache` jest określony za pomocą poleceń `nuget.exe` lub `--no-cache` jest określony za pomocą `dotnet restore`. (Program Visual Studio i `dotnet add package` zawsze używają pamięci podręcznej). Jeśli pakiet jest używany z pamięci podręcznej, w danych wyjściowych zostanie wyświetlona wartość "CACHE". Pamięć podręczna ma czas wygaśnięcia wynoszący 30 minut.

   - Jeśli pakiet nie znajduje się w pamięci podręcznej HTTP, spróbuj pobrać go ze źródeł wymienionych w konfiguracji. Jeśli pakiet zostanie pobrany, w danych wyjściowych pojawi się polecenie "GET" i "OK". Pakiet NuGet rejestruje ruch HTTP w normalnej szczegółowości.

   - Jeśli nie można pomyślnie pobrać pakietu z żadnych źródeł, instalacja nie powiedzie się z powodu błędu, takiego jak [NU1103](../reference/errors-and-warnings/NU1103.md). Należy zauważyć, że błędy z poleceń `nuget.exe` pokazują tylko ostatnie zaznaczone źródło, ale oznacza, że pakiet nie był dostępny z żadnego źródła.

   Podczas uzyskiwania pakietu można zastosować kolejność źródeł w konfiguracji programu NuGet:

   - Pakiet NuGet sprawdza źródłowe foldery lokalne i udziały sieciowe przed sprawdzaniem źródeł HTTP.

3. Zapisz kopię pakietu i inne informacje w folderze *pamięci podręcznej http* zgodnie z opisem w temacie [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).

4. W przypadku pobrania należy zainstalować pakiet w folderze *Global-Packages* dla użytkownika. Pakiet NuGet tworzy podfolder dla każdego identyfikatora pakietu, a następnie tworzy podfoldery dla każdej zainstalowanej wersji pakietu.

5. Pakiet NuGet instaluje zależności pakietów zgodnie z wymaganiami. Ten proces może aktualizować wersje pakietów w procesie, zgodnie z opisem w temacie [rozpoznawanie zależności](../concepts/dependency-resolution.md).

6. Aktualizowanie innych plików i folderów projektu:

    - W przypadku projektów korzystających z programu PackageReference należy zaktualizować wykres zależności pakietu przechowywany w `obj/project.assets.json`. Sama zawartość pakietu nie jest kopiowana do żadnego folderu projektu.
    - Zaktualizuj `app.config` i/lub `web.config`, jeśli pakiet używa [transformacji plików źródłowych i konfiguracyjnych](../create-packages/source-and-config-file-transformations.md).

7. (Tylko Visual Studio) Wyświetl plik Readme pakietu, jeśli jest dostępny, w oknie programu Visual Studio.

Korzystaj z wydajnych kodowania z pakietami NuGet.
