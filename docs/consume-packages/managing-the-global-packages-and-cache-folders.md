---
title: Jak zarządzać pakietami globalnymi, pamięcią podręczną, folderami tymczasowymi w NuGet
description: Jak zarządzać globalnym folderem instalacji pakietu, pamięci podręcznej pakietów i folderów tymczasowych, które istnieją na komputerze, które są używane podczas instalowania, przywracania i aktualizowania pakietów.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428969"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Zarządzanie pakietami globalnymi, pamięcią podręczną i folderami tymczasowymi

Za każdym razem, gdy instalujesz, aktualizujesz lub przywracasz pakiet, NuGet zarządza pakietami i informacjami o pakiecie w kilku folderach poza strukturą projektu:

| Nazwa | Opis i lokalizacja (na użytkownika)|
| --- | --- |
| globalne pakiety&#8209; | W folderze *pakietów globalnych* jest miejsce, w którym NuGet instaluje dowolny pobrany pakiet. Każdy pakiet jest w pełni rozwinięty do podfolderu, który pasuje do identyfikatora pakietu i numeru wersji. Projekty przy użyciu [formatu PackageReference](package-references-in-project-files.md) zawsze używają pakietów bezpośrednio z tego folderu. Podczas korzystania z [packages.config,](../reference/packages-config.md)pakiety są instalowane w folderze `packages` *global-packages,* a następnie kopiowane do folderu projektu.<br/><ul><li>Windows:`%userprofile%\.nuget\packages`</li><li>Mac/Linux:`~/.nuget/packages`</li><li>Zastąp przy użyciu zmiennej `globalPackagesFolder` środowiskowej NUGET_PACKAGES, ustawień lub `repositoryPath` `packages.config` [konfiguracji](../reference/nuget-config-file.md#config-section) (podczas korzystania z PackageReference i , odpowiednio) lub `RestorePackagesPath` właściwości MSBuild (tylko MSBuild). Zmienna środowiskowa ma pierwszeństwo przed ustawieniem konfiguracji.</li></ul> |
| http&#8209;pamięci podręcznej | Menedżer pakietów programu Visual Studio (NuGet 3.x+) i `dotnet` kopie pobranych pakietów w tej pamięci podręcznej (zapisane jako `.dat` pliki), zorganizowane w podfoldery dla każdego źródła pakietu. Pakiety nie są rozszerzane, a pamięć podręczna ma czas wygaśnięcia 30 minut.<br/><ul><li>Windows:`%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux:`~/.local/share/NuGet/v3-cache`</li><li>Zastąp przy użyciu zmiennej środowiskowej NUGET_HTTP_CACHE_PATH.</li></ul> |
| Najwyższa temp | Folder, w którym NuGet przechowuje pliki tymczasowe podczas różnych operacji.<br/><li>Windows:`%temp%\NuGetScratch`</li><li>Mac/Linux:`/tmp/NuGetScratch`</li></ul> |
| wtyczki-cache **4.8+** | Folder, w którym NuGet przechowuje wyniki z żądania oświadczeń operacji.<br/><ul><li>Windows:`%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux:`~/.local/share/NuGet/plugins-cache`</li><li>Zastąd wymień przy użyciu zmiennej środowiskowej NUGET_PLUGINS_CACHE_PATH.</li></ul> |

> [!Note]
> NuGet 3.5 i wcześniej używa *pakietów pamięci podręcznej* zamiast *http-cache*, który znajduje się w `%localappdata%\NuGet\Cache`.

Korzystając z pamięci podręcznej i *global-packages* folderów, NuGet zazwyczaj unika pobierania pakietów, które już istnieją na komputerze, zwiększając wydajność operacji instalacji, aktualizacji i przywracania. Podczas korzystania z PackageReference, *global-packages* folder unika również przechowywania pobranych pakietów wewnątrz folderów projektu, gdzie mogą one zostać przypadkowo dodane do kontroli źródła i zmniejsza ogólny wpływ NuGet na magazyn komputera.

Po zapytaniu o pobranie pakietu, NuGet najpierw szuka w folderze *pakietów globalnych.* Jeśli dokładna wersja pakietu nie istnieje, następnie NuGet sprawdza wszystkie źródła pakietów innych niż HTTP. Jeśli pakiet nadal nie został znaleziony, NuGet szuka pakietu w `--no-cache` pamięci `dotnet.exe` *podręcznej http,* chyba że określisz za pomocą poleceń lub `-NoCache` z `nuget.exe` poleceniami. Jeśli pakiet nie znajduje się w pamięci podręcznej lub pamięć podręczna nie jest używana, NuGet pobiera pakiet za pośrednictwem protokołu HTTP.

Aby uzyskać więcej informacji, zobacz [Co się stanie po zainstalowaniu pakietu?](../concepts/package-installation-process.md).

## <a name="viewing-folder-locations"></a>Wyświetlanie lokalizacji folderów

Lokalizacje można wyświetlać za pomocą [polecenia nuget locals:](../reference/cli-reference/cli-ref-locals.md)

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

Typowe dane wyjściowe (Windows; "user1" to aktualna nazwa użytkownika):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

(`package-cache` jest używany w NuGet 2.x i pojawia się z NuGet 3.5 i wcześniej.)

Lokalizacje folderów można również wyświetlać za pomocą [polecenia dotnet nuget locals:](/dotnet/core/tools/dotnet-nuget-locals)

```dotnetcli
dotnet nuget locals all --list
```

Typowe wyjście (Mac/Linux; "user1" to aktualna nazwa użytkownika):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

Aby wyświetlić lokalizację pojedynczego `http-cache`folderu, `plugins-cache` użyj , `all` `global-packages`, `temp`lub zamiast .

## <a name="clearing-local-folders"></a>Czyszczenie folderów lokalnych

Jeśli wystąpią problemy z instalacją pakietu lub w inny sposób chcesz `locals --clear` upewnić się, że instalujesz pakiety ze zdalnej galerii, użyj opcji (dotnet.exe) lub `locals -clear` (nuget.exe), określając folder do wyczyszczenie lub `all` wyczyść wszystkie foldery:

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

Wszystkie pakiety używane przez projekty, które są obecnie otwarte w programie Visual Studio nie są czyszczone z folderu *pakietów globalnych.*

Począwszy od programu Visual Studio 2017, użyj polecenia menu **Narzędzia > Menedżer pakietów NuGet > Ustawienia Menedżera pakietów,** a następnie wybierz pozycję **Wyczyść wszystkie pamięci podręczne NuGet**. Zarządzanie pamięcią podręczną nie jest obecnie dostępne za pośrednictwem konsoli Menedżera pakietów. W programie Visual Studio 2015 należy użyć polecenia interfejsu wiersza polecenia.

![Polecenie opcji NuGet do usuwania pamięci podręcznych](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Rozwiązywanie problemów z błędami

Podczas korzystania `nuget locals` lub: `dotnet nuget locals`

- *Błąd: proces nie może <package> uzyskać dostępu do pliku, ponieważ jest on używany przez inny proces* lub czyszczenie zasobów lokalnych nie *powiodło się: Nie można usunąć jednego lub więcej plików*

    Jeden lub więcej plików w folderze są używane przez inny proces; na przykład projekt programu Visual Studio jest otwarty, który odwołuje się do pakietów w folderze *pakietów globalnych.* Zamknij te procesy i spróbuj ponownie.

- *Błąd: odmowa <path> dostępu do ścieżki* lub *katalog nie jest pusty*

    Nie masz uprawnień do usuwania plików w pamięci podręcznej. Jeśli to możliwe, zmień uprawnienia do folderu i spróbuj ponownie. W przeciwnym razie skontaktuj się z administratorem systemu.

- *Błąd: określona ścieżka, nazwa pliku lub oba są zbyt długie. W pełni kwalifikowana nazwa pliku musi być mniejsza niż 260 znaków, a nazwa katalogu musi być mniejsza niż 248 znaków.*

    Skróć nazwy folderów i spróbuj ponownie.
