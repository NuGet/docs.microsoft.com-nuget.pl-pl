---
title: Typowe konfiguracje NuGet
description: Pliki w pliku NuGet.Config Sterowanie zachowaniem NuGet, globalnie i na poszczególnych projektów, a są modyfikowane za pomocą polecenia konfiguracji nuget.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 57b7f29b533a8e6d7db2710c7e42a239f50199a1
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426653"
---
# <a name="common-nuget-configurations"></a>Typowe konfiguracje NuGet

Zachowanie NuGet jest wymuszany przez ustawienia zebranych w jednej lub więcej `NuGet.Config` plików (XML), które może istnieć na poziomie projektu-, user- i całego komputera. Globalna `NuGetDefaults.Config` plik konfiguruje również specjalnie źródeł pakietów. Ustawienia stosowane do wszystkich poleceń, które pojawiły się w interfejsu wiersza polecenia, konsola Menedżera pakietów i interfejs użytkownika Menedżera pakietów.

## <a name="config-file-locations-and-uses"></a>Lokalizacje plików konfiguracji i używa

| Scope | Lokalizacja pliku NuGet.Config | Opis |
| --- | --- | --- |
| Rozwiązanie | Bieżący folder (czyli folderu rozwiązania) lub dowolnego folderu do katalogu głównego dysku.| W folderze rozwiązania ustawienia stosowane do wszystkich projektów w podfolderach. Należy pamiętać, że jeśli plik konfiguracji znajduje się w folderze projektu, nie ma ona wpływu na ten projekt. |
| Użytkownik | Windows: `%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux: `~/.config/NuGet/NuGet.Config` lub `~/.nuget/NuGet/NuGet.Config` (zależnie od dystrybucji systemu operacyjnego) | Ustawienia stosowane do wszystkich operacji, ale są zastępowane przez wszystkie ustawienia na poziomie projektu. |
| Komputer | Windows: `%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux: `$XDG_DATA_HOME`. Jeśli `$XDG_DATA_HOME` ma wartość null lub jest pusta, `~/.local/share` lub `/usr/local/share` będzie używany (zależnie od dystrybucji systemu operacyjnego)  | Ustawienia stosowane do wszystkich operacji wykonywanych na komputerze, ale są zastępowane przez ustawienia na poziomie użytkownika lub projektu. |

Uwagi dla wcześniejszych wersji programu NuGet:
- NuGet 3.3 i wcześniej używany `.nuget` folder ustawienia dla całego rozwiązania. Ten plik nie jest używany w programie NuGet 3.4 +.
- Dla 2.6 NuGet do 3.x, pliku konfiguracji na poziomie komputera, na Windows znajdują się w lokalizacji % ProgramData%\NuGet\Config [\\{IDE} [\\{Version} [\\{SKU}]]]\NuGet.Config, gdzie *{IDE}* może być  *Visual Studio*, *{Version}* został wersji programu Visual Studio, takie jak *14.0*, i *{jednostki SKU}* jest *społeczności*, *Pro*, lub *Enterprise*. Aby przeprowadzić migrację ustawień do narzędzia NuGet 4.0 +, po prostu skopiować pliku konfiguracji do % ProgramFiles(x86) % \NuGet\Config. W systemie Linux ta lokalizacja poprzedniej została /etc/opt, a na komputerze Mac, Library/Application Support.

## <a name="changing-config-settings"></a>Zmienianie ustawień konfiguracji

A `NuGet.Config` plik jest prosty plik tekstowy XML zawierający pary klucz/wartość, zgodnie z opisem w [ustawienia konfiguracji NuGet](../reference/nuget-config-file.md) tematu.

Ustawienia są zarządzane przy użyciu interfejsu wiersza polecenia NuGet [polecenia config](../tools/cli-ref-config.md):
- Domyślnie zmiany są wprowadzane do pliku konfiguracji na poziomie użytkownika.
- Aby zmienić ustawienia w innym pliku, należy użyć `-configFile` przełącznika. W tym przypadku plików można użyć dowolnej nazwy pliku.
- Klucze są zawsze z uwzględnieniem wielkości liter.
- Podniesienie uprawnień jest wymagane do zmiany ustawień w pliku ustawień na poziomie komputera.

> [!Warning]
> Mimo że można zmodyfikować plik w dowolnym edytorze tekstów NuGet (v3.4.3 i nowszych) dyskretnie ignoruje plik całą konfigurację, jeśli zawiera on nieprawidłowo sformułowany kod XML (niedopasowane tagi, nieprawidłowe znaki cudzysłowu, itp.). Dlatego zaleca się zarządzanie ustawienie przy użyciu `nuget config`.

### <a name="setting-a-value"></a>Ustawienie wartości

W systemie Windows:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

Mac/Linux:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> W programie NuGet 3.4 i nowszych można użyć zmiennych środowiskowych w dowolne wartości, podobnie jak w `repositoryPath=%PACKAGEHOME%` (Windows) i `repositoryPath=$PACKAGEHOME` (Mac/Linux).

### <a name="removing-a-value"></a>Usuwanie wartości

Aby usunąć wartość, należy określić klucz o wartości pustej.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Tworzenie nowego pliku konfiguracji

Skopiuj szablon poniżej do nowego pliku, a następnie użyj `nuget config -configFile <filename>` do ustawiania wartości:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Jak są stosowane ustawienia

Wiele `NuGet.Config` pliki umożliwiają przechowywanie ustawień w różnych lokalizacjach, tak aby odnoszą się do pojedynczego projektu, grupy projektów lub wszystkich projektów. Zbiorczo te ustawienia mają zastosowanie do dowolnej operacji NuGet wywoływane z poziomu wiersza polecenia lub z programu Visual Studio przy użyciu ustawień, które istnieją "najbliższy" do projektu lub w bieżącym folderze, biorąc, pierwszeństwo.

W szczególności NuGet ładuje ustawienia z plików konfiguracji różnych w następującej kolejności:

1. [Pliku NuGetDefaults.Config](#nuget-defaults-file), który zawiera ustawienia dotyczące tylko źródeł pakietów.
1. Plik poziomie komputera.
1. Plik poziomie użytkownika.
1. Pliku określonego przez `-configFile`.
1. Pliki znajdujące się w każdy folder w ścieżce w katalogu głównym dysku do bieżącego folderu (przywołane nuget.exe lub folder zawierający projekt programu Visual Studio). Na przykład, jeśli polecenie zostanie wywołana w c:\A\B\C, NuGet wyszukuje i ładuje pliki konfiguracji w c:\, następnie c:\A, a następnie c:\A\B, a na końcu c:\A\B\C.

Jak NuGet umożliwia znalezienie ustawień w tych plikach, są one stosowane w następujący sposób:

1. Dla elementów pojedynczą pozycją NuGet zastąpić dowolną z wcześniej znaleźć wartość dla tego samego klucza. Oznacza to, ustawienia, które są "najbliżej" bieżącego folderu lub projektu zastępują wszystkie inne pola znaleziono wcześniej. Na przykład `defaultPushSource` ustawienie w `NuGetDefaults.Config` jest zastępowany, jeśli istnieje w innym pliku konfiguracji.

1. Kolekcja elementów (takich jak `<packageSources>`), NuGet łączy wartości z wszystkich plików konfiguracji w jednej kolekcji.

1. Gdy `<clear />` jest obecny dla danego węzła NuGet ignoruje wcześniej określonych wartości konfiguracji dla tego węzła.

### <a name="settings-walkthrough"></a>Przewodnik ustawienia

Załóżmy, że mają następującą strukturę folderów na dwa oddzielne dyski:

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

Następnie możesz wybrać cztery `NuGet.Config` pliki w następujących lokalizacjach za pomocą danej zawartości. (Plik poziomie komputera nie jest uwzględniony w tym przykładzie, ale czy działają w podobny sposób do pliku poziom użytkownika).

Poziom użytkownika A. plik (`%appdata%\NuGet\NuGet.Config` na Windows, `~/.config/NuGet/NuGet.Config` w systemie Mac/Linux):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

File B. disk_drive_2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="disk_drive_2/tmp" />
    </config>
    <packageRestore>
        <add key="enabled" value="True" />
    </packageRestore>
</configuration>
```

File C. disk_drive_2/Project1/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="External/Packages" />
        <add key="defaultPushSource" value="https://MyPrivateRepo/ES/api/v2/package" />
    </config>
    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="MyPrivateRepo - ES" value="https://MyPrivateRepo/ES/nuget" />
    </packageSources>
</configuration>
```

File D. disk_drive_2/Project2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

NuGet, a następnie ładuje i stosuje ustawienia w następujący sposób, w zależności od tego, gdzie jest wywoływana:

- **Wywoływane z disk_drive_1/użytkowników**: Jest używana tylko w repozytorium domyślne, które są wymienione w pliku konfiguracji na poziomie użytkownika (A), ponieważ jest to jedyny plik w disk_drive_1.

- **Wywoływane z disk_drive_2 / lub disk_drive_/tmp**: Plik poziom użytkownika (A) jest załadowany po raz pierwszy, a następnie NuGet prowadzi do katalogu głównego disk_drive_2 i znajduje się plik (B). NuGet także szuka pliku konfiguracji w folderze/TMP, ale nie znaleźć partnera. W rezultacie jest używany domyślny repozytorium w witrynie nuget.org, przywracania pakietów jest włączone i pakietów, Pobierz rozwinięty w disk_drive_2/tmp.

- **Wywołane z disk_drive_2/projektu Project1 lub disk_drive_2/projektu Project1/źródło**: Poziom użytkownika (A) jest on ładowany najpierw, a następnie NuGet ładowania pliku (B) z katalogu głównego disk_drive_2, następuje plików (C). Ustawienia w (C) zastępują (B) i (A), więc `repositoryPath` gdzie zainstalowania pakietów jest disk_drive_2/projektu Project1/zewnętrzne/pakietów zamiast *disk_drive_2/tmp*. Ponadto ponieważ (C) Czyści `<packageSources>`, nuget.org nie jest już dostępna jako źródło, pozostawiając tylko `https://MyPrivateRepo/ES/nuget`.

- **Wywołane z disk_drive_2/Project2 lub disk_drive_2/Project2/źródło**: Plik poziom użytkownika (A) jest ładowany, najpierw następuje plik (B) i plik (D). Ponieważ `packageSources` nie jest czyszczony, zarówno `nuget.org` i `https://MyPrivateRepo/DQ/nuget` są dostępne jako źródła. Pakiety pobrać rozwinięty w disk_drive_2/tmp, jak to określono w (B).

## <a name="nuget-defaults-file"></a>Plik ustawień domyślnych NuGet

`NuGetDefaults.Config` Plik istnieje, aby określić źródła pakietów, z których pakietów są zainstalowane i aktualizowane oraz do sterowania to domyślny cel dla publikowania pakietów z `nuget push`. Ponieważ administratorzy, mogą wygodnie (na przykład przy użyciu zasad grupy) wdrożyć spójne `NuGetDefaults.Config` plików dla deweloperów i kompilacji do zapewnienia czy wszyscy użytkownicy w organizacji korzystają źródeł poprawny pakiet, a nie adres nuget.org.

> [!Important]
> `NuGetDefaults.Config` Plik nigdy nie powoduje źródło pakietu, które można usunąć z konfiguracji NuGet dla deweloperów. Oznacza to, że jeśli deweloper, który już użył NuGet i dlatego ma źródło pakietów nuget.org zarejestrowany, go nie zostaną usunięte po utworzeniu `NuGetDefaults.Config` pliku.
>
> Ponadto, żaden `NuGetDefaults.Config` ani jakiegokolwiek innego mechanizmu nuget może uniemożliwić dostęp do źródła pakietu, np. nuget.org. Jeśli organizacja chce zablokować takiego dostępu, on używać innych metod, takich jak zapory, aby to zrobić.

### <a name="nugetdefaultsconfig-location"></a>NuGetDefaults.Config location

W poniższej tabeli opisano gdzie `NuGetDefaults.Config` ma być przechowywany plik zależnie od docelowego systemu operacyjnego:

| Platforma systemu operacyjnego  | NuGetDefaults.Config Location |
| --- | --- |
| Windows      | **Visual Studio 2017 lub NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 i starsze lub NuGet 3.x i starszych wersji:** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME` (zazwyczaj `~/.local/share` lub `/usr/local/share`, w zależności od dystrybucji systemu operacyjnego)|

### <a name="nugetdefaultsconfig-settings"></a>Ustawienia NuGetDefaults.Config

- `packageSources`: Ta kolekcja ma takie samo znaczenie jak `packageSources` w zwykłych konfiguracji, pliki i określa źródeł domyślne. NuGet używa źródła w kolejności podczas instalowania lub aktualizowania pakietów w projektach przy użyciu `packages.config` format zarządzania. W przypadku projektów przy użyciu formatu PackageReference NuGet najpierw używa lokalnego źródła, a następnie źródeł na udziały sieciowe, a następnie źródła HTTP, niezależnie od kolejności, w plikach konfiguracji. NuGet są zawsze ignorowane kolejność źródeł za pomocą operacji przywracania.

- `disabledPackageSources`: Ta kolekcja również ma takie samo znaczenie jak w `NuGet.Config` plików, w którym każdego dotyczy źródła znajduje się przez nazwę i wartość PRAWDA/FAŁSZ wskazującą czy jest ono wyłączone. Dzięki temu nazwa źródła i adres URL, aby pozostać w `packageSources` bez konieczności ona domyślnie włączona. Każdy deweloper następnie można ponownie włączyć źródła, ustawiając wartość źródła na wartość false w innych `NuGet.Config` plików bez konieczności jego ponowne znalezienie prawidłowego adresu URL. Jest to również przydatne do dostarczania deweloperom pełną listę wewnętrzny źródłowy adres URL dla organizacji, pozwalając tylko poszczególne zespoły źródło domyślnie.

- `defaultPushSource`: Określa to domyślny cel dla `nuget push` operacji, zastąpienie wbudowanej domyślnej nuget.org. Administratorzy mogą wdrażać to ustawienie, aby uniknąć publikowania wewnętrznego pakietów nuget.org publicznych przypadkowo, jak deweloperzy w szczególności należy użyć `nuget push -Source` do publikowania w witrynie nuget.org.

### <a name="example-nugetdefaultsconfig-and-application"></a>Przykład NuGetDefaults.Config i aplikacji

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- defaultPushSource key works like the 'defaultPushSource' key of NuGet.Config files. -->
    <!-- This can be used by administrators to prevent accidental publishing of packages to nuget.org. -->
    <config>
        <add key="defaultPushSource" value="https://contoso.com/packages/" />
    </config>

    <!-- Default Package Sources; works like the 'packageSources' section of NuGet.Config files. -->
    <!-- This collection cannot be deleted or modified but can be disabled/enabled by users. -->
    <packageSources>
        <add key="Contoso Package Source" value="https://contoso.com/packages/" />
        <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>

    <!-- Default Package Sources that are disabled by default. -->
    <!-- Works like the 'disabledPackageSources' section of NuGet.Config files. -->
    <!-- Sources cannot be modified or deleted either but can be enabled/disabled by users. -->
    <disabledPackageSources>
        <add key="nuget.org" value="true" />
    </disabledPackageSources>
</configuration>
```
