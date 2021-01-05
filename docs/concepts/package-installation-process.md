---
title: Co się stanie po zainstalowaniu pakietu?
description: Szczegółowe informacje na temat procesu instalacji pakietu
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 634c421499b06f6b62d88a95f8703614dec5ace8
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699759"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Co się stanie po zainstalowaniu pakietu NuGet?

Po prostu poszczególne narzędzia NuGet zwykle tworzą odwołanie do pakietu w pliku projektu lub `packages.config` , a następnie wykonują przywracanie pakietów, które skutecznie instalują pakiet. Wyjątek polega na `nuget install` tym, że rozszerza pakiet jedynie do `packages` folderu i nie modyfikuje żadnych innych plików.

Ogólny proces wygląda następująco:

1. (Wszystkie narzędzia z wyjątkiem `nuget.exe` ) Zapisz identyfikator pakietu i wersję w pliku projektu lub `packages.config` .

   Jeśli narzędzie instalacji jest Visual Studio lub interfejs wiersza polecenia dotnet, narzędzie najpierw próbuje zainstalować pakiet. Jeśli jest niezgodny, pakiet nie jest dodawany do pliku projektu ani `packages.config` .

2. Pobierz pakiet:
   - Sprawdź, czy pakiet (według dokładnych identyfikator i numer wersji) jest już zainstalowany w folderze *pakiety globalne* , zgodnie z opisem w temacie [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).

   - Jeśli pakiet nie znajduje się w folderze *pakiety globalne* , spróbuj pobrać go ze źródeł wymienionych w [plikach konfiguracji](../consume-packages/Configuring-NuGet-Behavior.md). W przypadku źródeł online spróbuj najpierw pobrać pakiet z pamięci podręcznej HTTP, chyba że `-NoCache` jest określony za pomocą `nuget.exe` poleceń lub `--no-cache` jest określony za pomocą polecenia `dotnet restore` . (Program Visual Studio i `dotnet add package` zawsze korzysta z pamięci podręcznej). Jeśli pakiet jest używany z pamięci podręcznej, w danych wyjściowych zostanie wyświetlona wartość "CACHE". Pamięć podręczna ma czas wygaśnięcia wynoszący 30 minut.

   - Jeśli pakiet został określony przy użyciu [wersji zmiennoprzecinkowej](../consume-packages/Package-References-in-Project-Files.md#floating-versions)lub bez minimalnej wersji, *program NuGet skontaktuje się ze* wszystkimi źródłami, aby poznać najlepsze dopasowanie.
   Przykład: `1.*` , `(, 2.0.0]` .

   - Jeśli pakiet nie znajduje się w pamięci podręcznej HTTP, spróbuj pobrać go ze źródeł wymienionych w konfiguracji. Jeśli pakiet zostanie pobrany, w danych wyjściowych pojawi się polecenie "GET" i "OK". Pakiet NuGet rejestruje ruch HTTP w normalnej szczegółowości.

   - Jeśli nie można pomyślnie pobrać pakietu z żadnych źródeł, instalacja nie powiedzie się z powodu błędu, takiego jak [NU1103](../reference/errors-and-warnings/NU1103.md). Należy zauważyć, że błędy z `nuget.exe` poleceń pokazują tylko ostatnie zaznaczone źródło, ale oznacza, że pakiet nie był dostępny z żadnego źródła.

   Podczas uzyskiwania pakietu można zastosować kolejność źródeł w konfiguracji programu NuGet:

   - Pakiet NuGet sprawdza źródłowe foldery lokalne i udziały sieciowe przed sprawdzaniem źródeł HTTP.

3. Zapisz kopię pakietu i inne informacje w folderze *pamięci podręcznej http* zgodnie z opisem w temacie [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](../consume-packages/managing-the-global-packages-and-cache-folders.md).

4. W przypadku pobrania należy zainstalować pakiet w folderze *Global-Packages* dla użytkownika. Pakiet NuGet tworzy podfolder dla każdego identyfikatora pakietu, a następnie tworzy podfoldery dla każdej zainstalowanej wersji pakietu.

5. Pakiet NuGet instaluje zależności pakietów zgodnie z wymaganiami. Ten proces może aktualizować wersje pakietów w procesie, zgodnie z opisem w temacie [rozpoznawanie zależności](../concepts/dependency-resolution.md).

6. Aktualizowanie innych plików i folderów projektu:

    - W przypadku projektów korzystających z programu PackageReference należy zaktualizować wykres zależności pakietu przechowywany w temacie `obj/project.assets.json` . Sama zawartość pakietu nie jest kopiowana do żadnego folderu projektu.
    - Aktualizacja `app.config` i/lub `web.config` Jeśli pakiet używa [transformacji plików źródłowych i konfiguracyjnych](../create-packages/source-and-config-file-transformations.md).

7. (Tylko Visual Studio) Wyświetl plik Readme pakietu, jeśli jest dostępny, w oknie programu Visual Studio.

Korzystaj z wydajnych kodowania z pakietami NuGet.
