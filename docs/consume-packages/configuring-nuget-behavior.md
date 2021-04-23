---
title: Typowe konfiguracje narzędzia NuGet
description: NuGet.Config plików sterują zachowaniem nuGet zarówno globalnie, jak i dla każdego projektu, i są modyfikowane za pomocą polecenia nuget config.
author: JonDouglas
ms.author: jodou
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 18e3af7145495b5753b5900915ffb4b07942b856
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901476"
---
# <a name="common-nuget-configurations"></a>Typowe konfiguracje narzędzia NuGet

Zachowanie programu NuGet jest oparte na skumulowanych ustawieniach w co najmniej jednym pliku (XML), które mogą istnieć na poziomie całego projektu, użytkownika `NuGet.Config` i komputera. Plik globalny `NuGetDefaults.Config` również specjalnie konfiguruje źródła pakietów. Ustawienia dotyczą wszystkich poleceń wydanych w interfejsie wiersza polecenia, Menedżer pakietów i interfejsie Menedżer pakietów użytkownika.

## <a name="config-file-locations-and-uses"></a>Lokalizacje i zastosowania pliku konfiguracji

| Zakres | `NuGet.Config` lokalizacja pliku | Opis |
| --- | --- | --- |
| Rozwiązanie | Bieżący folder (folder rozwiązania) lub dowolny folder aż do katalogu głównego dysku.| W folderze rozwiązania ustawienia są stosowane do wszystkich projektów w podfolderach. Należy pamiętać, że jeśli plik konfiguracji zostanie umieszczony w folderze projektu, nie ma to wpływu na ten projekt. |
| Użytkownik | **Windows:**`%appdata%\NuGet\NuGet.Config`<br/>**Mac/Linux:** `~/.config/NuGet/NuGet.Config` lub `~/.nuget/NuGet/NuGet.Config` (zależy od dystrybucji systemu operacyjnego) <br/>Dodatkowe konfiguracje są obsługiwane na wszystkich platformach. Tych konfiguracji nie można edytować za pomocą narzędzi. </br> **Windows:**`%appdata%\NuGet\config\*.Config` <br/>**Mac/Linux:** `~/.config/NuGet/config/*.config` Lub `~/.nuget/config/*.config` | Ustawienia mają zastosowanie do wszystkich operacji, ale są zastępowany przez dowolne ustawienia na poziomie projektu. |
| Computer (Komputer) | **Windows:**`%ProgramFiles(x86)%\NuGet\Config`<br/>**Mac/Linux:** `$XDG_DATA_HOME` . Wartość `$XDG_DATA_HOME` null lub pusta albo wartość będzie używana `~/.local/share` `/usr/local/share` (różni się w zależności od dystrybucji systemu operacyjnego)  | Ustawienia mają zastosowanie do wszystkich operacji na komputerze, ale są zastępowany przez dowolne ustawienia na poziomie użytkownika lub projektu. |

Uwagi dotyczące wcześniejszych wersji programu NuGet:
- Program NuGet w wersji 3.3 i starszych używa `.nuget` folderu dla ustawień całego rozwiązania. Ten folder nie jest używany w programie NuGet 3.4+.
- W przypadku pakietu NuGet w wersji 2.6 do 3.x plik konfiguracji na poziomie komputera w systemie Windows znajdował się w pliku , gdzie może to być , Visual Studio wersja, taka jak , i to , `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]\NuGet.Config` `{IDE}` lub `VisualStudio` `{Version}` `14.0` `{SKU}` `Community` `Pro` `Enterprise` . Aby przeprowadzić migrację ustawień do programu NuGet 4.0+, po prostu skopiuj plik konfiguracji do pliku `%ProgramFiles(x86)%\NuGet\Config` . W systemie Linux ta poprzednia lokalizacja to `/etc/opt` , a na komputerze Mac — `/Library/Application Support` .

## <a name="changing-config-settings"></a>Zmienianie ustawień konfiguracji

Plik `NuGet.Config` to prosty plik tekstowy XML zawierający pary klucz/wartość zgodnie z opisem w temacie Ustawienia konfiguracji [nuGet.](../reference/nuget-config-file.md)

Ustawieniami zarządza się za pomocą polecenia [konfiguracji interfejsu](../reference/cli-reference/cli-ref-config.md)wiersza polecenia nuGet:
- Domyślnie zmiany są dokonywane w pliku konfiguracji na poziomie użytkownika.
- Aby zmienić ustawienia w innym pliku, użyj `-configFile` przełącznika . W takim przypadku pliki mogą używać dowolnej nazwy pliku.
- W kluczach jest zawsze wielkość liter.
- Podniesienie uprawnień jest wymagane do zmiany ustawień w pliku ustawień na poziomie komputera.

> [!Warning]
> Chociaż plik można zmodyfikować w dowolnym edytorze tekstów, nuGet (wersja 3.4.3 i nowsze) dyskretnie ignoruje cały plik konfiguracji, jeśli zawiera źle sformułowany kod XML (niezgodne tagi, nieprawidłowe cudzysłowy itp.). Dlatego lepiej jest zarządzać ustawieniem przy użyciu programu `nuget config` .

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
> W programie NuGet 3.4 lub nowszym można używać zmiennych środowiskowych w dowolnej wartości, tak jak w `repositoryPath=%PACKAGEHOME%` systemach (Windows) i `repositoryPath=$PACKAGEHOME` (Mac/Linux).

### <a name="removing-a-value"></a>Usuwanie wartości

Aby usunąć wartość, określ klucz z pustą wartością.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Tworzenie nowego pliku konfiguracji

Skopiuj poniższy szablon do nowego pliku, a następnie użyj funkcji `nuget config -configFile <filename>` , aby ustawić wartości:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Jak są stosowane ustawienia

Wiele plików umożliwia przechowywanie ustawień w różnych lokalizacjach, tak aby dotyczyły pojedynczego projektu, grupy `NuGet.Config` projektów lub wszystkich projektów. Te ustawienia mają zbiorczo zastosowanie do każdej operacji NuGet wywoływanej z wiersza polecenia lub z programu Visual Studio, z ustawieniami, które istnieją "najbliżej" projektu lub bieżącego folderu, które mają pierwszeństwo.

W szczególności program NuGet ładuje ustawienia z różnych plików konfiguracji w następującej kolejności:

1. Plik [ `NuGetDefaults.Config` ,](#nuget-defaults-file)który zawiera ustawienia związane tylko ze źródłami pakietów.
1. Plik na poziomie komputera.
1. Plik na poziomie użytkownika.
1. Plik określony za `-configFile` pomocą .
1. Pliki znalezione w każdym folderze w ścieżce od katalogu głównego dysku do bieżącego folderu (gdzie jest wywoływany lub folderu zawierającego Visual Studio `nuget.exe` projektu). Jeśli na przykład polecenie jest wywoływane w pliku , program NuGet szuka i ładuje pliki konfiguracji w plikach `c:\A\B\C` , następnie , , i na końcu `c:\` `c:\A` `c:\A\B` `c:\A\B\C` .

Gdy nuGet znajdzie ustawienia w tych plikach, są one stosowane w następujący sposób:

1. W przypadku elementów z jednym elementem program NuGet zastąpił wszystkie wcześniej znalezione wartości dla tego samego klucza. Oznacza to, że ustawienia znajdujące się "najbliżej" bieżącego folderu lub projektu przesłaniają wszystkie znalezione wcześniej ustawienia. Na przykład ustawienie `defaultPushSource` w pliku `NuGetDefaults.Config` zostanie zastąpione, jeśli istnieje w dowolnym innym pliku konfiguracji.
1. W przypadku elementów kolekcji (takich jak ) program NuGet łączy wartości ze `<packageSources>` wszystkich plików konfiguracji w jedną kolekcję.
1. Gdy `<clear />` jest obecny dla danego węzła, nuGet ignoruje wcześniej zdefiniowane wartości konfiguracji dla tego węzła.

### <a name="settings-walkthrough"></a>Przewodnik po ustawieniach

Załóżmy, że masz następującą strukturę folderów na dwóch oddzielnych dyskach:

```
disk_drive_1
    User
disk_drive_2
    Project1
        Source
    Project2
        Source
    tmp
```

Następnie masz cztery `NuGet.Config` pliki w następujących lokalizacjach z podaną zawartością. (Plik na poziomie komputera nie jest uwzględniony w tym przykładzie, ale będzie działać podobnie do pliku na poziomie użytkownika).

Plik A. Plik na poziomie użytkownika ( `%appdata%\NuGet\NuGet.Config` w systemie Windows w systemie `~/.config/NuGet/NuGet.Config` Mac/Linux):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

Plik B. `disk_drive_2/NuGet.Config` :

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

Plik C. `disk_drive_2/Project1/NuGet.Config` :

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

Plik D. `disk_drive_2/Project2/NuGet.Config` :

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

Następnie nuGet ładuje i stosuje ustawienia w następujący sposób, w zależności od tego, gdzie jest wywoływany:

- **Wywoływane `disk_drive_1/users` z**: używane jest tylko domyślne repozytorium wymienione w pliku konfiguracji na poziomie użytkownika (A), ponieważ jest to jedyny plik znaleziony w pliku `disk_drive_1` .

- **Wywoływane z `disk_drive_2/` lub `disk_drive_/tmp`**: najpierw jest ładowany plik na poziomie użytkownika (A), a następnie nuGet przechodzi do katalogu głównego pliku i znajduje plik `disk_drive_2` (B). Program NuGet wyszukuje również plik konfiguracji w pliku `/tmp` , ale nie znajduje go. W związku z tym jest używane domyślne repozytorium w repozytorium , przywracanie pakietów jest włączone, a pakiety są `nuget.org` rozszerzane w . `disk_drive_2/tmp`

- **Wywoływany z `disk_drive_2/Project1` lub `disk_drive_2/Project1/Source`**: najpierw jest ładowany plik na poziomie użytkownika (A), a następnie nuGet ładuje plik (B) z katalogu głównego , a następnie plik `disk_drive_2` (C). Ustawienia w programie (C) zastępują ustawienia w systemach (B) i (A), więc miejsce, w którym `repositoryPath` instalowane są pakiety, `disk_drive_2/Project1/External/Packages` to zamiast `disk_drive_2/tmp` . Ponadto, ponieważ (C) czyszczy `<packageSources>` , nuget.org nie jest już dostępna jako źródło, pozostawiając tylko `https://MyPrivateRepo/ES/nuget` .

- **Wywoływane z `disk_drive_2/Project2` lub `disk_drive_2/Project2/Source`**: plik na poziomie użytkownika (A) jest ładowany jako pierwszy, po którym następuje plik (B) i plik (D). Ponieważ `packageSources` nie jest wyczyszczyszona, `nuget.org` zarówno , jak i są dostępne jako `https://MyPrivateRepo/DQ/nuget` źródła. Pakiety są rozszerzane w `disk_drive_2/tmp` sposób określony w (B).

## <a name="additional-user-wide-configuration"></a>Dodatkowa konfiguracja dla całego użytkownika

Począwszy od programu 5.7, w programie NuGet dodano obsługę dodatkowych plików konfiguracji dla całego użytkownika. Dzięki temu dostawcy innych firm mogą dodawać dodatkowe pliki konfiguracji użytkownika bez podniesienia uprawnień.
Te pliki konfiguracji znajdują się w folderze konfiguracji użytkownika standardowego w `config` podfolderze.
Wszystkie pliki kończące się `.config` na lub `.Config` zostaną rozważone.
Tych plików nie można edytować za pomocą standardowych narzędzi.

| Platforma systemu operacyjnego  | Dodatkowe konfiguracje |
| --- | --- |
| Windows      | `%appdata%\NuGet\config\*.Config` |
| System Mac/Linux    | `~/.config/NuGet/config/*.config` lub `~/.nuget/config/*.config` |

## <a name="nuget-defaults-file"></a>Plik domyślny nuGet

Plik istnieje, aby określić źródła pakietów, z których pakiety są instalowane i aktualizowane, oraz kontrolować domyślny element `NuGetDefaults.Config` docelowy publikowania pakietów za pomocą programu `nuget push` . Ponieważ administratorzy mogą wygodnie (na przykład przy użyciu usługi zasady grupy) wdrażać spójne pliki na maszynach dewelopera i kompilacji, mogą zapewnić, że wszyscy w organizacji będą używać odpowiednich źródeł pakietów, a nie `NuGetDefaults.Config` nuget.org.

> [!Important]
> Plik nigdy nie powoduje usunięcia źródła pakietu z konfiguracji `NuGetDefaults.Config` NuGet dewelopera. Oznacza to, że jeśli deweloper już użył narzędzia NuGet i w związku z tym ma zarejestrowane źródło pakietu nuget.org, nie zostanie on usunięty po utworzeniu `NuGetDefaults.Config` pliku.
>
> Ponadto ani żaden inny mechanizm w pakiecie NuGet nie może uniemożliwić dostępu do źródeł pakietów, takich `NuGetDefaults.Config` jak nuget.org. Jeśli organizacja chce zablokować taki dostęp, musi w tym celu użyć innych środków, takich jak zapory.

### <a name="nugetdefaultsconfig-location"></a>`NuGetDefaults.Config` Lokalizacji

W poniższej tabeli opisano `NuGetDefaults.Config` miejsce przechowywania pliku w zależności od docelowego systemu operacyjnego:

| Platforma systemu operacyjnego  | `NuGetDefaults.Config` Lokalizacji |
| --- | --- |
| Windows      | **Visual Studio 2017 lub NuGet 4.x+:**`%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 i starsze lub NuGet 3.x i starsze:**`%PROGRAMDATA%\NuGet` |
| System Mac/Linux    | `$XDG_DATA_HOME` (zazwyczaj `~/.local/share` lub `/usr/local/share` , w zależności od dystrybucji systemu operacyjnego)|

### <a name="nugetdefaultsconfig-settings"></a>NuGetDefaults.Config ustawień

- `packageSources`: ta kolekcja ma takie samo znaczenie `packageSources` jak w zwykłych plikach konfiguracji i określa domyślne źródła. Program NuGet używa źródeł w kolejności podczas instalowania lub aktualizowania pakietów w projektach przy użyciu `packages.config` formatu zarządzania. W przypadku projektów korzystających z formatu PackageReference program NuGet najpierw używa źródeł lokalnych, a następnie źródeł w udziałach sieciowych, a następnie źródeł HTTP, niezależnie od kolejności w plikach konfiguracji. Program NuGet zawsze ignoruje kolejność źródeł w operacjach przywracania.

- `disabledPackageSources`: ta kolekcja ma również takie samo znaczenie jak w plikach, gdzie każde źródło, którego dotyczy problem, jest wyświetlane według nazwy i wartości wskazującej, czy `NuGet.Config` `true` / `false` jest wyłączone. Dzięki temu nazwa źródła i adres URL mogą pozostać w `packageSources` bez domyślnych włączone. Poszczegnieni deweloperzy mogą ponownie włączyć źródło, ustawiając wartość źródła na w innych plikach bez konieczności ponownego znalezienia `false` `NuGet.Config` poprawnego adresu URL. Jest to również przydatne w przypadku dostarczania deweloperom pełnej listy wewnętrznych adresów URL źródeł dla organizacji przy jednoczesnym domyślnym włączeniu tylko źródła poszczególnych reprezentacji zespołu.

- `defaultPushSource`: określa domyślny element docelowy dla `nuget push` operacji, zastępując wbudowane ustawienie domyślne `nuget.org` . Administratorzy mogą wdrożyć to ustawienie, aby uniknąć publikowania pakietów wewnętrznych publicznie przypadkowo, ponieważ deweloperzy muszą używać programu do `nuget.org` `nuget push -Source` publikowania w programie `nuget.org` .

### <a name="example-nugetdefaultsconfig-and-application"></a>Przykładowe NuGetDefaults.Config aplikacji

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
