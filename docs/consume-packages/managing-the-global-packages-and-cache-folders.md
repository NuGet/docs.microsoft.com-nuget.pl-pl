---
title: Jak zarządzać pakietami globalnymi, pamięcią podręczną, folderami tymczasowymi w pakiecie NuGet
description: Jak zarządzać folderem instalacji pakietów globalnych, pamięci podręcznej pakietów i folderami tymczasowymi, które istnieją na komputerze, które są używane podczas instalowania, przywracania i aktualizowania pakietów.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: 2a30904c5d26ea2114432dfbef08f53407926a33
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317753"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Zarządzanie pakietami globalnymi, pamięcią podręczną i folderami tymczasowymi

Za każdym razem, gdy instalujesz, aktualizujesz lub przywracasz pakiet, program NuGet zarządza pakietami i informacjami o pakietach w kilku folderach poza strukturą projektu:

| Nazwa | Opis i lokalizacja (na użytkownika)|
| --- | --- |
| global&#8209;packages | W folderze *globalne pakiety* jest instalowany pobrany pakiet NuGet. Każdy pakiet jest w pełni rozwinięty do podfolderu, który jest zgodny z identyfikatorem pakietu i numerem wersji. Projekty korzystające z formatu PackageReference zawsze używają pakietów bezpośrednio z tego folderu. W przypadku korzystania `packages.config`z programu pakiety są instalowane w folderze *globalne pakiety* , a następnie kopiowane `packages` do folderu projektu.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux:`~/.nuget/packages`</li><li>Przesłoń przy użyciu zmiennej środowiskowej NUGET_PACKAGES `globalPackagesFolder` , `repositoryPath` [Ustawienia konfiguracji](../reference/nuget-config-file.md#config-section) (w przypadku używania PackageReference `packages.config`i, odpowiednio) lub właściwości `RestorePackagesPath` programu MSBuild (tylko MSBuild). Zmienna środowiskowa ma pierwszeństwo przed ustawieniem konfiguracji.</li></ul> |
| http&#8209;cache | Menedżer pakietów programu Visual Studio (NuGet 3. x +) i `dotnet` narzędzie przechowuje kopie pobranych pakietów w tej pamięci podręcznej (zapisane jako `.dat` pliki), zorganizowane w podfolderach dla każdego źródła pakietu. Pakiety nie są rozwinięte, a pamięć podręczna ma czas wygaśnięcia 30 minut.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux:`~/.local/share/NuGet/v3-cache`</li><li>Przesłoń przy użyciu zmiennej środowiskowej NUGET_HTTP_CACHE_PATH.</li></ul> |
| temp | Folder, w którym narzędzia NuGet przechowują pliki tymczasowe podczas wykonywania różnych operacji.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux:`/tmp/NuGetScratch`</li></ul> |
| plugins-cache **4.8+** | Folder, w którym narzędzia NuGet przechowują wyniki żądania oświadczeń operacji.<br/><ul><li>Windows: `%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux:`~/.local/share/NuGet/plugins-cache`</li><li>Przesłoń przy użyciu zmiennej środowiskowej NUGET_PLUGINS_CACHE_PATH.</li></ul> |

> [!Note]
> Program NuGet 3,5 i starsze wersje używają *pamięci podręcznej pakietów* zamiast pamięci podręcznej *http*, `%localappdata%\NuGet\Cache`która znajduje się w.

Przy użyciu folderów pamięci podręcznej i *pakietów globalnych pakiet* NuGet zazwyczaj eliminuje pobieranie pakietów, które już istnieją na komputerze, co zwiększa wydajność operacji instalacji, aktualizacji i przywracania. W przypadku korzystania z programu PackageReference folder *Global-Packages* również pozwala uniknąć utrzymywania pobranych pakietów wewnątrz folderów projektu, gdzie mogą być przypadkowo dodawane do kontroli źródła i zmniejsza ogólny wpływ narzędzia NuGet na magazyn komputerowy.

Po wyświetleniu monitu o pobranie pakietu pakiet NuGet najpierw szuka folderu *Global-Packages* . Jeśli dokładna wersja pakietu nie istnieje, pakiet NuGet sprawdza wszystkie źródła pakietów spoza protokołu HTTP. Jeśli pakiet nadal nie zostanie znaleziony, pakiet NuGet szuka pakietu w *pamięci podręcznej http* , chyba że zostanie `--no-cache` określony `dotnet.exe` z poleceniami `nuget.exe` lub `-NoCache` z poleceniami. Jeśli pakiet nie znajduje się w pamięci podręcznej, a pamięć podręczna nie jest używana, narzędzie NuGet pobierze pakiet za pośrednictwem protokołu HTTP.

Aby uzyskać więcej informacji, zobacz [co się stanie po zainstalowaniu pakietu?](../concepts/package-installation-process.md).

## <a name="viewing-folder-locations"></a>Przeglądanie lokalizacji folderów

Lokalizacje można wyświetlić za pomocą [polecenia locale programu NuGet](../reference/cli-reference/cli-ref-locals.md):

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

Typowe dane wyjściowe (Windows; "Użytkownik1" jest bieżącą nazwą użytkownika:

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

(`package-cache` jest używany w NuGet 2. x i występuje z pakietem NuGet 3,5 i wcześniejszym).

Lokalizacje folderów można także wyświetlić przy użyciu [polecenia locale programu dotnet dla ustawień regionalnych](/dotnet/core/tools/dotnet-nuget-locals):

```cli
dotnet nuget locals all --list
```

Typowe dane wyjściowe (Mac/Linux; "Użytkownik1" jest bieżącą nazwą użytkownika:

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

Aby wyświetlić lokalizację pojedynczego folderu, użyj `http-cache`, `global-packages` `temp` `plugins-cache` ,, lub zamiast. `all`

## <a name="clearing-local-folders"></a>Czyszczenie folderów lokalnych

Jeśli wystąpią problemy z instalacją pakietu lub w przeciwnym razie chcesz upewnić się, że instalujesz pakiety z galerii zdalnej `locals --clear` , użyj opcji (dotnet. exe `locals -clear` ) lub (NuGet. exe), określając folder do wyczyszczenia `all` lub Wyczyść wszystkie foldery:

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

Wszystkie pakiety używane przez projekty, które są aktualnie otwarte w programie Visual Studio, nie są usuwane z folderu *Global-Packages* .

Począwszy od programu Visual Studio 2017, użyj **narzędzia > Menedżer pakietów NuGet > menu Ustawienia Menedżera pakietów** , a następnie wybierz polecenie **Wyczyść wszystkie pamięć podręczna NuGet**. Zarządzanie pamięcią podręczną nie jest obecnie dostępne za pomocą konsoli Menedżera pakietów. W programie Visual Studio 2015 zamiast tego Użyj poleceń interfejsu wiersza polecenia.

![Polecenie NuGet opcji do czyszczenia pamięci podręcznych](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Rozwiązywanie problemów z błędami

Następujące błędy mogą wystąpić podczas korzystania `nuget locals` z lub: `dotnet nuget locals`

- *Błąd: Proces nie może uzyskać dostępu do <package> pliku, ponieważ jest on używany przez inny* proces *lub czyszczenie zasobów lokalnych nie powiodło się: Nie można usunąć co najmniej jednego pliku*

    Co najmniej jeden plik w folderze jest używany przez inny proces; na przykład projekt programu Visual Studio jest otwarty, który odwołuje się do pakietów w folderze *Global-Packages* . Zamknij te procesy i spróbuj ponownie.

- *Błąd: <path> Odmówiono* dostępu do ścieżki lub *katalog nie jest pusty*

    Nie masz uprawnień do usuwania plików w pamięci podręcznej. Zmień uprawnienia folderu, jeśli to możliwe, i spróbuj ponownie. W przeciwnym razie skontaktuj się z administratorem systemu.

- *Błąd: Określona ścieżka, nazwa pliku lub obie są zbyt długie. W pełni kwalifikowana nazwa pliku musi być krótsza niż 260 znaków, a nazwa katalogu musi być krótsza niż 248 znaków.*

    Skróć nazwy folderów i spróbuj ponownie.
