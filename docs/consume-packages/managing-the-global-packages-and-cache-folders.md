---
title: Jak zarządzać globalnymi pakietami, pamięci podręcznej, folderów tymczasowych w programie NuGet
description: Jak zarządzać folderu instalacji pakietu globalnej pamięci podręcznej pakietu i folderów tymczasowych, które istnieją na komputerze, które są używane podczas instalowania, przywracania i aktualizowanie pakietów.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: c547ae1d46079d040d7c3aa4c7678e70cd199dce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548016"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Zarządzanie globalnymi pakietami, pamięci podręcznej i folderów tymczasowych

Zawsze, gdy instalować, aktualizować ani przywrócić pakietu NuGet zarządza pakiety i informacje o pakiecie w kilku folderach poza do struktury projektu:

| Nazwa | Opis i lokalizacji (na użytkownika)|
| --- | --- |
| globalne&#8209;pakietów | *Globalnymi pakietami* folder to, gdzie NuGet instaluje wszelkie pobranego pakietu. Każdy pakiet jest w pełni rozwinięta do podfolderu, który odpowiada identyfikator pakietu i numeru wersji. Projektów przy użyciu funkcji PackageReference zawsze formatu pakietów Użyj bezpośrednio z tego folderu. Korzystając z `packages.config`, pakiety są instalowane na *globalnymi pakietami* folder i następnie kopiowane do projektu `packages` folderu.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>Zastąp przy użyciu zmiennej środowiskowej NUGET_PACKAGES, `globalPackagesFolder` lub `repositoryPath` [ustawienia konfiguracji](../reference/nuget-config-file.md#config-section) (korzystając z funkcji PackageReference i `packages.config`odpowiednio), lub `RestorePackagesPath` MSBuild Właściwość (MSBuild tylko). Zmienna środowiskowa mają pierwszeństwo przed ustawieniem konfiguracji.</li></ul> |
| http&#8209;cache | Menedżera pakietów programu Visual Studio (NuGet 3.x+) i `dotnet` narzędzie przechowują kopie pakietów do pobrania w tej pamięci podręcznej (zapisane jako `.dat` pliki) zorganizowanym w podfoldery dla każdego źródła pakietu. Pakiety nie zostaną rozwinięte i pamięć podręczna zawiera 30-minutowy czas wygaśnięcia.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>Musi zostać zastąpiona, przy użyciu zmiennej środowiskowej NUGET_HTTP_CACHE_PATH.</li></ul> |
| Temp | Folder, w którym NuGet przechowywania plików tymczasowych podczas jego różne operacje.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |
| pamięć podręczna wtyczek **4.8 +** | Folder, w którym NuGet przechowuje wyniki z żądania oświadczeń operacji.<br/><ul><li>Windows: `%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/plugins-cache`</li><li>Musi zostać zastąpiona, przy użyciu zmiennej środowiskowej NUGET_PLUGINS_CACHE_PATH.</li></ul> |

> [!Note]
> NuGet 3.5 i starszych używa *pamięci podręcznej pakietów* zamiast *pamięci podręcznej http*, który znajduje się w `%localappdata%\NuGet\Cache`.

Przy użyciu pamięci podręcznej i *globalnymi pakietami* folderów, NuGet ogólnie pozwala uniknąć pobierania pakietów, które już istnieją na komputerze, poprawę wydajności instalacji, aktualizacji i operacji przywracania. Korzystając z funkcji PackageReference, *globalnymi pakietami* folderu również pozwala uniknąć przechowywania pobrane pakiety w folderach projektu, gdzie one może przypadkowo dodane do kontroli źródła i zmniejsza całkowity wpływ NuGet na komputerze Magazyn.

Po wyświetleniu monitu, aby pobrać pakiet, NuGet najpierw przeszukuje *globalnymi pakietami* folderu. Jeśli dokładna wersja pakietu nie jest dostępne, NuGet umożliwia sprawdzenie wszystkich źródeł pakietów protokołu HTTP. Jeśli nadal nie znaleziono pakietu, NuGet szuka pakietu w *pamięci podręcznej http* chyba że określisz `--no-cache` z `dotnet.exe` poleceń lub `-NoCache` z `nuget.exe` poleceń. Jeśli pakiet nie znajduje się w pamięci podręcznej lub pamięci podręcznej nie jest używany, NuGet następnie pobiera pakiet za pośrednictwem protokołu HTTP.

Aby uzyskać więcej informacji, zobacz [co się dzieje po zainstalowaniu pakietu](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).

## <a name="viewing-folder-locations"></a>Wyświetlanie lokalizacje folderów

Można wyświetlić przy użyciu lokalizacji [polecenie lokalne nuget](../tools/cli-ref-locals.md):

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

Typowe dane wyjściowe (Windows; Bieżąca nazwa użytkownika to "uzytkownik1"):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

(`package-cache` jest używany w pakiecie NuGet 2.x i pojawia się za pomocą NuGet 3.5 i starszych.)

Można także wyświetlać lokalizacje folderów za pomocą [polecenie lokalne nuget dotnet](/dotnet/core/tools/dotnet-nuget-locals):

```cli
dotnet nuget locals all --list
```

Typowe dane wyjściowe (Mac/Linux; Bieżąca nazwa użytkownika to "uzytkownik1"):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

Aby wyświetlić lokalizację pojedynczy folder, należy użyć `http-cache`, `global-packages`, `temp`, lub `plugins-cache` zamiast `all`.

## <a name="clearing-local-folders"></a>Czyszczenie foldery lokalne

Jeśli występują problemy z instalacją pakietu lub chcesz w przeciwnym razie upewnij się, czy instalujesz pakiety ze zdalnego galerii, użyj `locals --clear` opcji (dotnet.exe) lub `locals -clear` (nuget.exe), określając folder, aby wyczyścić, lub `all` do Wyczyść wszystkie foldery:

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

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

Wszystkie pakiety używane w projektach, które są aktualnie otwarte w programie Visual Studio nie są usuwane z *globalnymi pakietami* folderu.

W programie Visual Studio 2017, użyj **Narzędzia > Menedżer pakietów NuGet > Ustawienia Menedżera pakietów** menu polecenia, a następnie wybierz **wyczyść wszystkie Cache(s) NuGet**. Zarządzanie pamięcią podręczną nie jest obecnie dostępna za pośrednictwem konsoli Menedżera pakietów. W programie Visual Studio 2015 zamiast tego użyj poleceń interfejsu wiersza polecenia.

![NuGet — opcja polecenia czyszczenia pamięci podręcznych](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Rozwiązywanie problemów z błędami

Następujące błędy mogą wystąpić, gdy za pomocą `nuget locals` lub `dotnet nuget locals`:

- *Błąd: Proces nie może uzyskać dostępu do pliku <package> , ponieważ jest on używany przez inny proces* lub *wyczyszczenie zasobów lokalnych nie powiodło się: nie można usunąć jeden lub więcej plików*

    Jeden lub więcej plików w folderze są używane przez inny proces; na przykład projektu programu Visual Studio jest otwarty, która odwołuje się do pakietów w *globalnymi pakietami* folderu. Zamknij tych procesów i spróbuj ponownie.

- *Błąd: Dostęp do ścieżki <path> odmowa* lub *katalog nie jest pusty*

    Nie masz uprawnień do usuwania plików w pamięci podręcznej. Zmień uprawnienia do folderu, jeśli to możliwe i spróbuj ponownie. W przeciwnym razie skontaktuj się z administratorem systemu.

- *Błąd: Określona ścieżka i nazwa pliku są za długie. W pełni kwalifikowanej nazwy pliku musi być mniejsza niż 260 znaków, a nazwy katalogu musi być mniejsza niż 248 znaków.*

    Skróć nazwy folderu i spróbuj ponownie.
