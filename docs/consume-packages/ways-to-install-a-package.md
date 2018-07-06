---
title: Sposoby, aby zainstalować pakiety NuGet
description: W tym artykule opisano proces instalowania pakietów NuGet do projektu, w tym, co się stanie, na dysku i pliki projektu dotyczy.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/12/2018
ms.topic: overview
ms.openlocfilehash: 0f59c3b7f1e32ae34889921c13d15074ef5c1260
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843384"
---
# <a name="different-ways-to-install-a-nuget-package"></a>Różne sposoby, aby zainstalować pakiet NuGet

Pakiety NuGet zostaną pobrane i zainstalowane przy użyciu dowolnej z metod w poniższej tabeli (zobacz [narzędzia klienta programu NuGet zainstalować](../install-nuget-client-tools.md) Jeśli nie masz, są już zainstalowane). Pakiet może zostać pobrana z pamięci podręcznej zamiast pobrane.

| Metoda | Opis |
| --- | --- |
| DotNet.exe interfejsu wiersza polecenia<br/>`dotnet add package <package_name>` | (Wszystkie platformy) Pobiera pakiet identyfikowane przez \<nazwa_pakietu\>rozwija jego zawartość do folderu w bieżącym katalogu i dodanie odwołania do pliku projektu. Ponadto umożliwia pobranie i zainstalowanie zależności.<ul><li>[Instalowanie i używanie pakietu (wiersz polecenia dotnet)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[polecenia DotNet Dodaj pakiet — polecenie](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| Interfejs użytkownika Menedżera pakietów (Visual Studio) | (Windows i Mac) Udostępnia interfejs użytkownika, za pomocą którego można przeglądać, wybierz i zainstalować pakiety i ich zależności do projektu ze źródła określonego pakietu. Dodaje odwołania do pakietów zainstalowanych w pliku projektu.<ul><li>[Instalowanie i używanie pakietu (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Odwołanie do interfejsu użytkownika Menedżera pakietów (Windows)](../tools/package-manager-ui.md)</li><li>[Dołączanie pakietu NuGet w projekcie (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Konsola Menedżera pakietów (Visual Studio)<br/>`Install-Package <package_name>` | (Tylko Windows) Pobiera i instaluje pakiet identyfikowane przez \<nazwa_pakietu\> z wybranego źródła do określonego projektu w rozwiązaniu, a następnie dodaje odwołanie do pliku projektu. Ponadto umożliwia pobranie i zainstalowanie zależności.<ul><li>[Instalowanie i używanie pakietu (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Przewodnik Konsola Menedżera pakietów](../tools/package-manager-console.md)</li></ul> |
| Interfejs wiersza polecenia nuget.exe<br/>`nuget install <package_name>` | (Wszystkie platformy) Pobiera pakiet identyfikowane przez \<nazwa_pakietu\> i zwiększa jego zawartość do folderu w bieżącym katalogu; można także pobrać wszystkie pakiety wymienione w `packages.config` pliku. Również umożliwia pobranie i zainstalowanie zależności, ale nie wprowadza żadnych zmian w plikach projektu lub `packages.config`.<ul><li>[polecenie instalacji](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>Co się stanie, gdy pakiet jest zainstalowany

Był wyświetlany różne narzędzia NuGet zazwyczaj utworzyć odwołanie do pakietu w pliku projektu lub `packages.config`, następnie wykonać przywracania pakietów skuteczne pakiet zostanie zainstalowany. Wyjątek stanowi `nuget install`, który rozwija tylko pakiet do `packages` folder i wszystkie inne pliki nie powoduje modyfikacji.

Ogólny proces jest następująca:

1. (Wszystkie narzędzia, z wyjątkiem `nuget.exe`) Zapisz identyfikator pakietu i wersję do pliku projektu lub `packages.config`.

2. Pobieranie pakietu:
   - Sprawdź, czy pakiet (przez dokładny identyfikator oraz numer wersji) jest już zainstalowany w *globalnymi pakietami* folderu zgodnie z opisem na [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).

   - Jeśli pakiet nie znajduje się w *globalnymi pakietami* folderze próbują pobrać go ze źródeł wymienione na liście [pliki konfiguracyjne](Configuring-NuGet-Behavior.md). Dla źródeł online próbował najpierw pobrać pakiet z pamięci podręcznej, chyba że `-NoCache` jest określony za pomocą `nuget.exe` poleceń lub `--no-cache` jest określony za pomocą `dotnet restore`. (Visual Studio i `dotnet add package` zawsze używać pamięci podręcznej.) Jeśli pakiet jest używany z pamięci podręcznej, "Pamięć PODRĘCZNĄ" pojawia się w danych wyjściowych. Pamięć podręczna zawiera 30-minutowy czas wygaśnięcia.

   - Jeśli pakiet nie jest w pamięci podręcznej, próba go pobrać ze źródła wymienione w konfiguracji. Jeśli pakiet został pobrany, "GET" i "OK" są wyświetlane w danych wyjściowych.

   - Jeśli pakiet nie może pomyślnie uzyskana z dowolnymi źródłami, instalacja nie powiedzie się na tym etapie ze względu na błąd taki jak [NU1103](../reference/errors-and-warnings/NU1103.md). Uwaga tego błędy z `nuget.exe` Pokaż polecenia tylko ostatni źródło opcja jest zaznaczona, ale oznacza, że pakiet nie była dostępna z dowolnego źródła.

   Podczas uzyskiwania pakietu, mogą mieć zastosowanie kolejność źródeł w konfiguracji NuGet:

   - W przypadku projektów przy użyciu formatu PackageReference NuGet sprawdza źródła lokalnego folderu i udziałów sieciowych przed sprawdzeniem źródła HTTP.

   - Dla projektów przy użyciu `packages.config` zarządzania formatu NuGet używa kolejności źródeł w konfiguracji. Wyjątek stanowi operacje przywracania, w którym to przypadku porządkowania źródła jest ignorowany i NuGet korzysta z pakietu z dowolnego źródła odpowiada w pierwszej kolejności.

   - Ogólnie rzecz biorąc kolejność, w którym NuGet kontroli źródła nie jest szczególnie istotne, ponieważ dowolnego danego pakietu przy użyciu określonego identyfikatora oraz numer wersji jest dokładnie taka sama, niezależnie od źródła został znaleziony.

3. (Wszystkie narzędzia, z wyjątkiem `nuget.exe`) Zapisz kopię pakietu oraz inne informacje w *pamięci podręcznej http* folderu zgodnie z opisem na [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).

4. Jeśli pobrane, należy zainstalować pakiet w poszczególnych użytkowników *globalnymi pakietami* folderu. NuGet tworzy osobny podfolder dla każdego identyfikatora pakietu, a następnie tworzy oddzielne podfoldery dla każdej zainstalowanej wersji pakietu.

5. Aktualizacja innych projektów, plików i folderów:

    - W przypadku projektów przy użyciu funkcji PackageReference, zaktualizuj wykres zależności pakietu, które są przechowywane w `obj/project.assets.json`. Zawartość pakietu, sami nie są kopiowane do dowolnego folderu projektu.
    - Dla projektów przy użyciu `packages.config`, skopiuj te części pakietu rozwinięty, które odpowiadają platforma docelowa projektu do projektu `packages` folderu. (Korzystając z `nuget install`, cały pakiet rozszerzonej jest kopiowana, ponieważ `nuget.exe` nie analizuje pliki projektu, aby zidentyfikować platformę docelową.)
    - Aktualizacja `app.config` i/lub `web.config` Jeśli korzysta z pakietu [źródła i konfiguracji pliku przekształcenia](../create-packages/source-and-config-file-transformations.md).

6. Jeśli zainstalować wszystkie zależności niskiego poziomu nie już istnieje w projekcie. Ten proces może aktualizować wersje pakietów w procesie, zgodnie z opisem w [rozpoznawania zależności](../consume-packages/dependency-resolution.md).

7. (Tylko visual Studio) Wyświetl plik readme pakietu, jeśli to możliwe, w oknie programu Visual Studio.

## <a name="related-articles"></a>Powiązane artykuły

- [Omówienie i przepływ pracy zużycia pakietu](../consume-packages/overview-and-workflow.md)
- [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md)
- [Zarządzanie folderami pamięci podręcznej i globalnymi pakietami NuGet](managing-the-global-packages-and-cache-folders.md)
- [Konfigurowanie zachowania pakietu NuGet](../consume-packages/configuring-nuget-behavior.md)
