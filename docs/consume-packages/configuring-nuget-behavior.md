---
title: Typowe konfiguracje narzędzia NuGet
description: NuGet.Config pliki kontrolują zachowanie narzędzia NuGet zarówno globalnie, jak i dla każdego projektu i są modyfikowane za pomocą polecenia konfiguracji NuGet.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: e81c380eab3f1a8635e50e62811c7ae463ec3653
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699765"
---
# <a name="common-nuget-configurations"></a>Typowe konfiguracje narzędzia NuGet

Zachowanie narzędzia NuGet jest zależne od ustawień skumulowanych w jednym lub kilku `NuGet.Config` plikach (XML), które mogą istnieć na poziomach na poziomie projektu, użytkownika i komputera. Plik globalny `NuGetDefaults.Config` również służy do konfigurowania źródeł pakietów. Ustawienia dotyczą wszystkich poleceń wydawanych w interfejsie wiersza polecenia, konsoli Menedżera pakietów i interfejsu użytkownika Menedżera pakietów.

## <a name="config-file-locations-and-uses"></a>Lokalizacje i użycia plików konfiguracji

| Zakres | Lokalizacja pliku NuGet.Config | Opis |
| --- | --- | --- |
| Rozwiązanie | Bieżący folder (folder rozwiązania) lub dowolny folder w katalogu głównym dysku.| W folderze rozwiązania ustawienia są stosowane do wszystkich projektów w podfolderach. Należy pamiętać, że jeśli plik konfiguracyjny znajduje się w folderze projektu, nie ma wpływu na ten projekt. |
| Użytkownik | **System Windows:**`%appdata%\NuGet\NuGet.Config`<br/>**Mac/Linux:** `~/.config/NuGet/NuGet.Config` lub `~/.nuget/NuGet/NuGet.Config` (w zależności od dystrybucji systemu operacyjnego) <br/>Dodatkowe konfiguracje są obsługiwane na wszystkich platformach. Te konfiguracje nie mogą być edytowane przez narzędzia. </br> **System Windows:**`%appdata%\NuGet\config\*.Config` <br/>**Mac/Linux:** `~/.config/NuGet/config/*.config` oraz `~/.nuget/config/*.config` | Ustawienia dotyczą wszystkich operacji, ale są zastępowane przez dowolne ustawienia na poziomie projektu. |
| Computer (Komputer) | **System Windows:**`%ProgramFiles(x86)%\NuGet\Config`<br/>**Mac/Linux:** `$XDG_DATA_HOME` . Jeśli `$XDG_DATA_HOME` ma wartość null lub jest pusty `~/.local/share` lub `/usr/local/share` będzie używany (zależy od dystrybucji systemu operacyjnego)  | Ustawienia dotyczą wszystkich operacji na komputerze, ale są zastępowane przez dowolne ustawienia użytkownika lub poziomu projektu. |

Uwagi dotyczące wcześniejszych wersji programu NuGet:
- Pakiet NuGet 3,3 i wcześniejsze użycie `.nuget` folderu dla ustawień całego rozwiązania. Ten folder nie jest używany w programie NuGet 3.4 +.
- W przypadku programu NuGet 2,6 do 3. x plik konfiguracyjny na poziomie komputera w systemie Windows został zlokalizowany w%ProgramData%\NuGet\Config [ \\ {IDE} [ \\ {Version} [ \\ {SKU}]]] \NuGet.Config, gdzie *{IDE}* może być *VisualStudio*, *{Version}* była wersją programu Visual Studio, taką jak *14,0*, i *{SKU}* to *społeczność*, *Pro* lub *Enterprise*. Aby przeprowadzić migrację ustawień do programu NuGet 4.0 +, po prostu skopiuj plik konfiguracyjny do% ProgramFiles (x86)% \ NuGet\Config. W systemie Linux ta poprzednia lokalizacja została/etc/opt oraz na komputerach Mac,/Library/Application Support support.

## <a name="changing-config-settings"></a>Zmienianie ustawień konfiguracji

`NuGet.Config`Plik to prosty plik tekstowy XML zawierający pary klucz/wartość, zgodnie z opisem w temacie [Ustawienia konfiguracji programu NuGet](../reference/nuget-config-file.md) .

Ustawienia są zarządzane przy użyciu interfejsu wiersza [polecenia NuGet konfiguracji](../reference/cli-reference/cli-ref-config.md):
- Domyślnie zmiany są wprowadzane w pliku konfiguracji na poziomie użytkownika.
- Aby zmienić ustawienia w innym pliku, należy użyć `-configFile` przełącznika. W tym przypadku pliki mogą używać dowolnych nazw plików.
- Klucze zawsze uwzględniają wielkość liter.
- Aby zmienić ustawienia w pliku ustawień na poziomie komputera, wymagana jest podniesienie uprawnień.

> [!Warning]
> Chociaż można modyfikować plik w dowolnym edytorze tekstu, pakiet NuGet (v 3.4.3 i nowsze) w trybie cichym ignoruje cały plik konfiguracyjny, jeśli zawiera źle sformułowany kod XML (niezgodne Tagi, nieprawidłowe znaki cudzysłowu itp.). Dlatego zaleca się zarządzanie ustawieniami przy użyciu `nuget config` .

### <a name="setting-a-value"></a>Ustawianie wartości

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
> W programie NuGet 3,4 i nowszych można używać zmiennych środowiskowych w dowolnej wartości, jak w `repositoryPath=%PACKAGEHOME%` systemach (Windows) i `repositoryPath=$PACKAGEHOME` (Mac/Linux).

### <a name="removing-a-value"></a>Usuwanie wartości

Aby usunąć wartość, określ klucz z pustą wartością.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Tworzenie nowego pliku konfiguracji

Skopiuj szablon poniżej do nowego pliku, a następnie użyj, `nuget config -configFile <filename>` Aby ustawić wartości:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Jak są stosowane ustawienia

Wiele `NuGet.Config` plików umożliwia przechowywanie ustawień w różnych lokalizacjach, tak aby dotyczyły one jednego projektu, grupy projektów lub wszystkich projektów. Te ustawienia są stosowane zbiorczo do każdej operacji NuGet wywołanej z wiersza polecenia lub z programu Visual Studio z ustawieniami, które istnieją "najbliżej" w projekcie lub bieżącym folderze, który ma pierwszeństwo.

W programie NuGet są ładowane ustawienia z różnych plików konfiguracji w następującej kolejności:

1. [PlikNuGetDefaults.Config](#nuget-defaults-file), który zawiera ustawienia dotyczące tylko źródeł pakietów.
1. Plik na poziomie komputera.
1. Plik na poziomie użytkownika.
1. Plik określony przy użyciu `-configFile` .
1. Pliki znajdujące się w każdym folderze w ścieżce z katalogu głównego dysku do bieżącego folderu (gdzie nuget.exe są wywoływane lub folder zawierający projekt programu Visual Studio). Na przykład jeśli polecenie jest wywoływane w c:\A\B\C, NuGet szuka i ładuje pliki konfiguracji w c: \, then c:\a, c:\A\B i finally c:\A\B\C.

Ponieważ program NuGet odnajdzie ustawienia w tych plikach, są one stosowane w następujący sposób:

1. W przypadku elementów jednego elementu NuGet zastępuje wszystkie poprzednio znalezione wartości dla tego samego klucza. Oznacza to, że ustawienia, które są "najbliżej" w bieżącym folderze lub projekcie zastępują inne znalezione wcześniej. Na przykład `defaultPushSource` ustawienie w `NuGetDefaults.Config` jest zastępowane, jeśli istnieje w innym pliku konfiguracyjnym.

1. W przypadku elementów kolekcji (takich jak `<packageSources>` ) pakiet NuGet łączy wartości ze wszystkich plików konfiguracji w jedną kolekcję.

1. Gdy `<clear />` jest obecny dla danego węzła, pakiet NuGet ignoruje wcześniej zdefiniowane wartości konfiguracji dla tego węzła.

### <a name="settings-walkthrough"></a>Przewodnik po ustawieniach

Załóżmy, że masz następującą strukturę folderów na dwóch oddzielnych dyskach:

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

Następnie `NuGet.Config` w poniższych lokalizacjach znajdują się cztery pliki o podaną zawartość. (Plik na poziomie komputera nie jest uwzględniony w tym przykładzie, ale zachowuje się podobnie do pliku na poziomie użytkownika).

Plik A. plik na poziomie użytkownika ( `%appdata%\NuGet\NuGet.Config` w systemie Windows, `~/.config/NuGet/NuGet.Config` na komputerze Mac/Linux):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

Plik B. disk_drive_2/NuGet.Config:

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

Plik C. disk_drive_2/Project1/NuGet.Config:

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

Plik D. disk_drive_2/Project2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

Następnie program NuGet ładuje i stosuje ustawienia w następujący sposób, w zależności od tego, gdzie jest wywoływany:

- **Wywołane z disk_drive_1/users**: używany jest tylko repozytorium domyślne wymienione w pliku konfiguracji na poziomie użytkownika (A), ponieważ jest to jedyny plik znaleziony w disk_drive_1.

- **Wywołane z disk_drive_2/lub disk_drive_/tmp**: najpierw załadowano plik poziomu użytkownika (A), a następnie pakiet NuGet przechodzi do katalogu głównego disk_drive_2 i odnajdzie plik (B). Pakiet NuGet szuka również pliku konfiguracji w programie/tmp, ale go nie znaleziono. W związku z tym używane jest domyślne repozytorium w nuget.org, przywracanie pakietu jest włączone, a pakiety zostaną rozwinięte w disk_drive_2/tmp.

- **Wywołane z disk_drive_2/Project1 lub disk_drive_2/Project1/Source**: najpierw załadowano plik na poziomie użytkownika (A), a następnie program NuGet ładuje plik (B) z katalogu głównego disk_drive_2, a następnie plik (C). Ustawienia w (C) przesłaniają te w (B) i (A), dzięki czemu `repositoryPath` instalowane pakiety są disk_drive_2/Project1/External/Packages, a nie *disk_drive_2/tmp*. Ponadto, ponieważ (C) czyści `<packageSources>` , NuGet.org nie jest już dostępne tylko jako źródło wychodzące `https://MyPrivateRepo/ES/nuget` .

- **Wywołane z disk_drive_2/Project2 lub disk_drive_2/Project2/Source**: plik na poziomie użytkownika (A) jest ładowany po raz pierwszy, po którym następuje plik (B) i plik (D). Ponieważ `packageSources` nie jest wyczyszczone, oba `nuget.org` i `https://MyPrivateRepo/DQ/nuget` są dostępne jako źródła. Pakiety zostaną rozwinięte w disk_drive_2/tmp zgodnie z opisem w (B).

## <a name="additional-user-wide-configuration"></a>Dodatkowa konfiguracja dla wszystkich użytkowników

Począwszy od 5,7, pakiet NuGet dodał obsługę dodatkowych plików konfiguracji o wielu użytkownikach. Umożliwia to dostawcom innych firm Dodawanie dodatkowych plików konfiguracji użytkownika bez podniesienia uprawnień.
Te pliki konfiguracyjne znajdują się w folderze Standardowa konfiguracja użytkownika w `config` podfolderze.
Wszystkie pliki kończące się na `.config` lub `.Config` zostaną uwzględnione.
Tych plików nie można edytować za pomocą standardowych narzędzi.

| Platforma systemu operacyjnego  | Dodatkowe konfiguracje |
| --- | --- |
| Windows      | `%appdata%\NuGet\config\*.Config` |
| System Mac/Linux    | `~/.config/NuGet/config/*.config` lub `~/.nuget/config/*.config` |

## <a name="nuget-defaults-file"></a>Plik domyślny NuGet

`NuGetDefaults.Config`Plik istnieje, aby określić źródła pakietów, z których pakiety są instalowane i aktualizowane, i kontrolować domyślny element docelowy dla pakietów publikowanych za pomocą programu `nuget push` . Ze względu na to, że administratorzy mogą wygodnie (na przykład za pomocą zasady grupy) wdrażać spójne `NuGetDefaults.Config` pliki na maszynach deweloperskich i kompilacji, mogą oni upewnić się, że wszyscy w organizacji używają odpowiednich źródeł pakietów, a nie NuGet.org.

> [!Important]
> `NuGetDefaults.Config`Plik nigdy nie powoduje usunięcia źródła pakietu z konfiguracji NuGet dewelopera. Oznacza to, że deweloper już użył NuGet i w związku z tym ma zarejestrowane źródło pakietów nuget.org, nie zostanie usunięte po utworzeniu `NuGetDefaults.Config` pliku.
>
> Ponadto żaden `NuGetDefaults.Config` inny mechanizm w pakiecie NuGet nie może uniemożliwiać dostępu do źródeł pakietów, takich jak NuGet.org. Jeśli organizacja chce zablokować taki dostęp, musi użyć innych środków, takich jak zapory, aby to zrobić.

### <a name="nugetdefaultsconfig-location"></a>Lokalizacja NuGetDefaults.Config

W poniższej tabeli opisano, gdzie `NuGetDefaults.Config` należy przechowywać plik, w zależności od docelowego systemu operacyjnego:

| Platforma systemu operacyjnego  | Lokalizacja NuGetDefaults.Config |
| --- | --- |
| Windows      | **Visual Studio 2017 lub NuGet 4. x +:**`%ProgramFiles(x86)%\NuGet\Config` <br />**Program Visual Studio 2015 i wcześniejsze lub NuGet 3. x i wcześniejsze:**`%PROGRAMDATA%\NuGet` |
| System Mac/Linux    | `$XDG_DATA_HOME` (zwykle `~/.local/share` lub `/usr/local/share` , w zależności od dystrybucji systemu operacyjnego)|

### <a name="nugetdefaultsconfig-settings"></a>Ustawienia NuGetDefaults.Config

- `packageSources`: Ta kolekcja ma takie samo znaczenie jak `packageSources` w zwykłych plikach konfiguracji i określa domyślne źródła. Przy instalowaniu lub aktualizowaniu pakietów w projektach przy użyciu formatu zarządzania narzędzia NuGet używa źródeł `packages.config` . W przypadku projektów korzystających z formatu PackageReference, pakiet NuGet najpierw używa lokalnych źródeł, a następnie źródeł w udziałach sieciowych, a następnie źródeł HTTP, niezależnie od kolejności w plikach konfiguracji. NuGet zawsze ignoruje kolejność źródeł przy użyciu operacji przywracania.

- `disabledPackageSources`: Ta kolekcja ma także takie samo znaczenie jak w `NuGet.Config` przypadku plików, gdzie każde z nich ma swoją nazwę i wartość true/false wskazującą, czy jest ona wyłączona. Dzięki temu nazwa i adres URL źródła mogą pozostać w programie `packageSources` bez domyślnego włączenia. Poszczególni deweloperzy mogą następnie ponownie włączyć źródło, ustawiając wartość źródła na false w innych `NuGet.Config` plikach bez konieczności ponownego znalezienia poprawnego adresu URL. Jest to również przydatne w przypadku deweloperów, którzy mają pełną listę wewnętrznych źródłowych adresów URL dla organizacji, jednocześnie domyślnie włączając tylko źródło poszczególnych zespołów.

- `defaultPushSource`: określa domyślny element docelowy dla `nuget push` operacji, zastępując wbudowane domyślne wartości NuGet.org. Administratorzy mogą wdrożyć to ustawienie, aby zapobiec publikowaniu wewnętrznych pakietów nuget.org w sposób niezależny od sytuacji, gdy deweloperzy muszą używać `nuget push -Source` do publikowania w NuGet.org.

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
