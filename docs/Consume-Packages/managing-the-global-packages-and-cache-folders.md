---
title: Jak zarządzać globalne pakietów, pamięci podręcznej, folderów tymczasowych w NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Jak zarządzać folderu instalacji globalnej pakietu, pamięć podręczną pakietów i folderów tymczasowych, które istnieją na komputerze, które są używane podczas instalowania, przywracania i aktualizowanie pakietów.
keywords: Globalne dzaj pakietami folderu, pamięć podręczną pakietów NuGet, buforowanie pakietu, folder instalacji pakietu, pamięci podręcznych NuGet, zarządzanie pamięci podręcznych, lokalnej pamięci podręcznej NuGet, globalnej pamięci podręcznej NuGet, NuGet polecenie zmiennych lokalnych, czyszczenie pamięci podręcznej
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e9f4383a3f1700b96e3d6fe9ea4c0a7c24daa45a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Zarządzanie pakietów globalnej pamięci podręcznej i folderów tymczasowych

Zawsze, gdy zainstalować, zaktualizować lub przywracanie pakietu NuGet zarządza pakietów i informacji w kilku folderach poza struktury projektu:

| Nazwa | Opis i lokalizację (dla poszczególnych użytkowników)|
| --- | --- |
| globalne&#8209;pakietów | *Globalne pakiety* jest folder, gdzie NuGet instaluje wszystkie pobranego pakietu. Każdy pakiet jest w pełni rozwinięta do podfolderu zgodny identyfikator pakietu i numer wersji. Projektów przy użyciu PackageReference zawsze formatu Użyj pakietów bezpośrednio z tego folderu. Korzystając z `packages.config`, pakiety są instalowane na *globalne pakiety* folderu, następnie kopiowane do projektu `packages` folderu.<br/><ul><li>System Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>Override, za pomocą zmiennej środowiskowej NUGET_PACKAGES, `globalPackagesFolder` lub `repositoryPath` [ustawienia konfiguracji](../reference/nuget-config-file.md#config-section) (przy użyciu PackageReference i `packages.config`odpowiednio), lub `RestorePackagesPath` MSBuild Właściwość (MSBuild tylko). Zmienna środowiskowa mają pierwszeństwo przed ustawieniem konfiguracji.</li></ul> |
| http&#8209;cache | Menedżer pakietów programu Visual Studio (NuGet 3.x+) i `dotnet` narzędzia przechowują kopie pobrane pakiety w pamięci podręcznej (zapisane jako `.dat` plików), są organizowane w podfolderach dla każdego źródła pakietu. Pakiety nie zostaną rozwinięte, a pamięć podręczna zawiera czas wygaśnięcia 30 minut.<br/><ul><li>System Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>Override, za pomocą zmiennej środowiskowej NUGET_HTTP_CACHE_PATH.</li></ul> |
| Temp | Folder, w którym NuGet przechowuje pliki tymczasowe podczas jego różnych operacji.<br/><li>System Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |

> [!Note]
> NuGet 3.5 i wcześniejszych zastosowań *pamięci podręcznej pakiety* zamiast *pamięci podręcznej http*, który znajduje się w `%localappdata%\NuGet\Cache`.

Przy użyciu pamięci podręcznej i *globalne pakiety* folderów, NuGet zazwyczaj pozwala uniknąć pobierania pakietów, które już istnieją na komputerze, poprawa wydajności instalacji, aktualizacji i operacji przywracania. Korzystając z PackageReference, *globalne pakiety* folderu również pozwala uniknąć porządkowania pobrane pakiety w folderach projektu, w których one mogą przypadkowo dodane do kontroli źródła i zmniejsza NuGet ogólnego wpływu na komputerze Magazyn.

Po otrzymaniu monitu, aby pobrać pakiet, NuGet najpierw wyszukiwana *globalne pakiety* folderu. Jeśli dokładną wersję pakietu nie jest dostępne, NuGet sprawdza wszystkie źródła pakietów w innych niż HTTP. Jeśli nadal nie można znaleźć pakietu, NuGet szuka pakietu w *pamięci podręcznej http* chyba że zostanie `--no-cache` z `dotnet.exe` polecenia lub `-NoCache` z `nuget.exe` poleceń. Jeśli pakiet nie znajduje się w pamięci podręcznej lub pamięci podręcznej nie jest używany, NuGet następnie pobiera pakiet za pośrednictwem protokołu HTTP.

Aby uzyskać więcej informacji, zobacz [co się dzieje, gdy jest zainstalowany pakiet](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).

## <a name="viewing-folder-locations"></a>Wyświetlanie lokalizacje folderów

Można wyświetlić przy użyciu lokalizacji folderu [polecenia zmiennych lokalnych nuget dotnet](/dotnet/core/tools/dotnet-nuget-locals):

```cli
dotnet nuget locals all --list
```

Dane wyjściowe zazwyczaj (system Mac/Linux; Nazwa bieżącego użytkownika jest "uzytkownik1"):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
```

Aby wyświetlić lokalizacji folderu, użyj `http-cache`, `global-packages`, lub `temp` zamiast `all`. 

Możesz również wyświetlić przy użyciu lokalizacji [polecenia nuget zmiennych lokalnych](../tools/cli-ref-locals.md):

```cli
# Display locals for all folders: global-packages, cache, and temp
nuget locals all -list
```

Dane wyjściowe zazwyczaj (z systemem Windows; Nazwa bieżącego użytkownika jest "uzytkownik1"):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
```

(`package-cache` jest używany w NuGet 2.x i pojawi się z NuGet 3.5 lub starszej.)

## <a name="clearing-local-folders"></a>Wyczyszczenie foldery lokalne

Jeśli występują problemy z instalacją pakietu lub w przeciwnym razie chcesz zapewnić instalowany pakiety ze zdalnego galerii, użyj `locals --clear` opcji (dotnet.exe) lub `locals -clear` (nuget.exe), określenia folderu, aby wyczyścić, lub `all` do Usuń zaznaczenie wszystkich folderów:

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

Wszystkie pakiety używane w projektach, które są aktualnie otwarte w programie Visual Studio nie są usuwane z *globalne pakiety* folderu.

W programie Visual Studio, użyj **Narzędzia > Menedżera pakietów NuGet > Ustawienia Menedżera pakietów** menu polecenie, a następnie wybierz **wyczyść wszystkie Cache(s) NuGet**. Zarządzanie pamięcią podręczną nie jest obecnie dostępna za pośrednictwem konsoli Menedżera pakietów.

![Polecenia NuGet opcję czyszczenia pamięci podręcznych](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Rozwiązywanie problemów z błędami

Następujące błędy może wystąpić, gdy za pomocą `nuget locals` lub `dotnet nuget locals`:

- *Błąd: Proces nie może uzyskać dostępu do pliku <package> , ponieważ jest on używany przez inny proces* lub *wyczyszczenie zasobów lokalnych nie powiodło się: nie można usunąć jednego lub więcej plików*

    Jeden lub więcej plików w folderze są używane przez inny proces; na przykład projektu programu Visual Studio jest otwarty, która odwołuje się do pakietów w *globalne pakiety* folderu. Zamknij tych procesów i spróbuj ponownie.

- *Błąd: Dostęp do ścieżki <path> odmowa* lub *katalog nie jest pusty*

    Nie masz uprawnień do usuwania plików w pamięci podręcznej. Zmień uprawnienia do folderu, jeśli to możliwe i spróbuj ponownie. W przeciwnym razie skontaktuj się z administratorem systemu.

- *Błąd: Określona ścieżka i nazwa pliku jest zbyt długa. W pełni kwalifikowanej nazwy pliku musi być mniejsza niż 260 znaków, a nazwa katalogu musi być mniejsza niż 248 znaków.*

    Skróć nazwę folderu i spróbuj ponownie.
