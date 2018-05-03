---
title: Sposoby można zainstalować pakietów NuGet
description: W tym artykule opisano proces instalowania pakietów NuGet do projektu, w tym, co się dzieje na dysku oraz pliki dotyczy projektu.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 02/12/2018
ms.topic: overview
ms.openlocfilehash: 028fb9710e808974348d9cca3c56103c087d5390
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Różne sposoby, można zainstalować pakietu NuGet

Pakiety NuGet zostaną pobrane i zainstalowane przy użyciu dowolnej z metod w poniższej tabeli (zobacz [NuGet zainstalować narzędzia klienta](../install-nuget-client-tools.md) Jeśli nie są już zainstalowane). Pakiet można pobrać z pamięci podręcznej zamiast pobrane.

| Metoda | Opis |
| --- | --- |
| DotNet.exe interfejsu wiersza polecenia<br/>`dotnet add package <package_name>` | (Wszystkie platformy) Pobiera pakiet identyfikowane przez \<nazwa_pakietu\>rozszerza jego zawartość do folderu w bieżącym katalogu i dodaje odwołanie do pliku projektu. Ponadto pobiera i instaluje zależności.<ul><li>[Instalowanie i używanie pakietu (wiersz polecenia dotnet)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[polecenie pakietu dodać DotNet](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| Interfejs użytkownika Menedżera pakietów (Visual Studio) | (System Windows i Mac) Udostępnia interfejs użytkownika za pośrednictwem której można wybrać, wybierz i zainstalować pakietów oraz ich zależności w projekcie ze źródła określonego pakietu. Dodaje odwołania do zainstalowanych pakietów do pliku projektu.<ul><li>[Instalowanie i używanie pakietu (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Informacje o interfejsie użytkownika Menedżera pakietów (system Windows)](../tools/package-manager-ui.md)</li><li>[W tym pakietu NuGet w projekcie (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Konsola Menedżera pakietów (Visual Studio)<br/>`Install-Package <package_name>` | (Tylko system Windows) Pobiera i instaluje pakiet identyfikowane przez \<nazwa_pakietu\> z wybranego źródła do określonego projektu w rozwiązaniu, a następnie dodaje odwołanie do pliku projektu. Ponadto pobiera i instaluje zależności.<ul><li>[Instalowanie i używanie pakietu (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Przewodnik Konsola Menedżera pakietów](../tools/package-manager-console.md)</li></ul> |
| nuget.exe interfejsu wiersza polecenia<br/>`nuget install <package_name>` | (Wszystkie platformy) Pobiera pakiet identyfikowane przez \<nazwa_pakietu\> i rozwija jego zawartość do folderu w bieżącym katalogu; można również pobrać wszystkie pakiety wymienione w `packages.config` pliku. Również pobiera i instaluje zależności, ale nie zmienia pliki projektu lub `packages.config`.<ul><li>[polecenie instalacji](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>Co się dzieje, gdy pakiet jest zainstalowany

Prostu, różnych narzędzi NuGet zwykle utworzyć odwołanie do pakietu w pliku projektu lub `packages.config`, następnie wykonaj operację przywracania pakietu, które skutecznie instaluje pakiet. Wyjątek stanowi `nuget install`, która rozszerza tylko pakietu do `packages` folderu i inne pliki nie modyfikować.

Ogólny proces wygląda następująco:

1. (Wszystkie narzędzia, z wyjątkiem `nuget.exe`) rekord identyfikator pakietu i wersja pliku projektu lub `packages.config`.

2. Pobieranie pakietu:
   - Sprawdź, czy pakiet (przez dokładne identyfikatorem oraz numer wersji) jest już zainstalowany w *globalne pakiety* folderu zgodnie z opisem na [Zarządzanie globalne pakietów i foldery pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).

   - Jeśli pakiet nie znajduje się w *globalne pakiety* folderu, próbują pobrać go ze źródeł wymienionych na liście [pliki konfiguracji](Configuring-NuGet-Behavior.md). Dla źródeł online próbował najpierw pobrać pakiet z pamięci podręcznej, chyba że `-NoCache` zostanie określony z `nuget.exe` polecenia lub `--no-cache` zostanie określony z `dotnet restore`. (Visual Studio i `dotnet add package` zawsze używać pamięci podręcznej.) Jeśli pakiet jest używany z pamięci podręcznej, "Pamięci PODRĘCZNEJ" pojawia się w danych wyjściowych. Pamięć podręczna zawiera czas wygaśnięcia 30 minut.

   - Jeśli pakiet nie jest w pamięci podręcznej, próba go pobrać ze źródła w konfiguracji. Jeśli pakiet zostanie pobrany "GET" i "OK", są wyświetlane w danych wyjściowych.

   - Jeśli pakiet nie może zostać pomyślnie pobrany z żadnymi źródłami, instalacja nie powiedzie się w tym punkcie z powodu błędu takie jak [NU1103](../reference/errors-and-warnings.md#nu1103). Uwaga tego błędów z `nuget.exe` Pokaż polecenia zaznaczone tylko ostatni źródła, ale oznacza, że pakiet nie była dostępna z dowolnego źródła.

   Podczas pobierania pakietu, mogą stosować kolejność źródeł w konfiguracji NuGet:

   - W przypadku projektów przy użyciu formatu PackageReference NuGet sprawdza źródła lokalnego folderu i udziałów sieciowych przed zaewidencjonowaniem źródła HTTP.

   - Dla projektów przy użyciu `packages.config` format zarządzania, NuGet używa kolejność źródeł w konfiguracji. Wyjątek operacje przywracania, w którym to przypadku porządkowania źródła jest ignorowana i NuGet korzysta z pakietu z innego źródła odpowiada w pierwszej kolejności.

   - Ogólnie rzecz biorąc kolejność, w którym NuGet kontroli źródła nie jest szczególnie przydatne, ponieważ wszystkie danego pakietu o określoną liczbę identyfikator i wersja jest dokładnie taka sama niezależnie od źródła został znaleziony.

3. (Wszystkie narzędzia, z wyjątkiem `nuget.exe`) Zapisz kopię pakietu oraz inne informacje w *pamięci podręcznej http* folderu zgodnie z opisem na [Zarządzanie globalne pakietów i foldery pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).

4. Jeśli pobrano, zainstaluj pakiet w poszczególnych użytkowników *globalne pakiety* folderu. NuGet tworzy podfolder dla każdego identyfikatora pakietu, a następnie tworzy oddzielne podfoldery dla każdej zainstalowanej wersji pakietu.

5. Aktualizacja innych projektów plików i folderów:

    - Dla projektów przy użyciu PackageReference, zaktualizuj wykresu zależności pakietu, które są przechowywane w `obj/project.assets.json`. Zawartość pakietu, same nie są kopiowane do folderu projektu.
    - Dla projektów przy użyciu `packages.config`, skopiuj części pakietu rozwinięte zgodne platformy docelowej projektu do projektu `packages` folderu. (Przy użyciu `nuget install`, cały pakiet rozszerzonej jest kopiowana, ponieważ `nuget.exe` nie bada pliki projektu, aby zidentyfikować platformy docelowej.)
    - Aktualizacja `app.config` i/lub `web.config` Jeśli pakiet używa [źródła i konfiguracji pliku przekształcenia](../create-packages/source-and-config-file-transformations.md).

6. Zainstaluj wszelkie zależności niższego poziomu Jeśli nie są jeszcze zainstalowane w projekcie. Ten proces może zaktualizować wersje pakietu w procesie, zgodnie z opisem w [rozpoznawania zależności](../consume-packages/dependency-resolution.md).

7. (Tylko w programie visual Studio) Wyświetl plik readme pakietu, jeśli są dostępne w oknie programu Visual Studio.

## <a name="related-articles"></a>Pokrewne artykuły

- [Omówienie i przepływ pracy zużycia pakietu](../consume-packages/overview-and-workflow.md)
- [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md)
- [Zarządzanie folderami pamięci podręcznej i globalnych pakietów NuGet](managing-the-global-packages-and-cache-folders.md)
- [Konfigurowanie zachowania pakietu NuGet](../consume-packages/configuring-nuget-behavior.md)
