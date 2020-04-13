---
title: Typowe konfiguracje narzędzia NuGet
description: Pliki NuGet.Config kontrolują zachowanie NuGet zarówno globalnie, jak i na podstawie projektu i są modyfikowane za pomocą polecenia nuget config.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 89127203df0aa1eb24f36b8ec64c5bb4a4d59319
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428913"
---
# <a name="common-nuget-configurations"></a>Typowe konfiguracje narzędzia NuGet

Zachowanie NuGet jest napędzany przez skumulowane ustawienia `NuGet.Config` w jednym lub więcej plików (XML), które mogą istnieć na poziomie projektu, użytkownika i komputera. Plik `NuGetDefaults.Config` globalny również specjalnie konfiguruje źródła pakietów. Ustawienia dotyczą wszystkich poleceń wydanych w interfejsie wiersza polecenia, konsoli Menedżera pakietów i interfejsie użytkownika Menedżera pakietów.

## <a name="config-file-locations-and-uses"></a>Lokalizacje i zastosowania plików konfiguracyjne

| Zakres | Lokalizacja pliku NuGet.Config | Opis |
| --- | --- | --- |
| Rozwiązanie | Bieżący folder (aka folder Rozwiązanie) lub dowolny folder do katalogu głównego dysku.| W folderze rozwiązania ustawienia dotyczą wszystkich projektów w podfolderach. Należy zauważyć, że jeśli plik konfiguracyjny jest umieszczony w folderze projektu, nie ma to wpływu na ten projekt. |
| Użytkownik | Windows:`%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux: `~/.config/NuGet/NuGet.Config` `~/.nuget/NuGet/NuGet.Config` lub (w zależności od dystrybucji systemu operacyjnego) | Ustawienia dotyczą wszystkich operacji, ale są zastępowane przez wszystkie ustawienia na poziomie projektu. |
| Computer (Komputer) | Windows:`%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux: `$XDG_DATA_HOME`. Jeśli `$XDG_DATA_HOME` jest null `~/.local/share` lub `/usr/local/share` puste, lub będą używane (zależy od dystrybucji systemu operacyjnego)  | Ustawienia dotyczą wszystkich operacji na komputerze, ale są zastępowane przez ustawienia na poziomie użytkownika lub projektu. |

Uwagi dotyczące wcześniejszych wersji programu NuGet:
- NuGet 3.3 i `.nuget` wcześniej używane folder dla ustawień dla całego rozwiązania. Ten folder nie jest używany w nuget 3.4+.
- W przypadku nugeta 2.6 do 3.x plik konfiguracyjny na poziomie komputera w systemie\\Windows znajdował\\się w\\%ProgramData%\NuGet\Config[ {IDE}[ {Version}[ {SKU}]]]\NuGet.Config, gdzie *{IDE}* może być *VisualStudio*, *{Version}* była wersją programu Visual Studio, taką jak *14.0,* a *{SKU}* jest *wspólnotą*, *Pro*lub *Enterprise*. Aby przeprowadzić migrację ustawień do wersji NuGet 4.0+, wystarczy skopiować plik konfiguracyjny do pliku %ProgramFiles(x86)%\NuGet\Config. W systemie Linux ta poprzednia lokalizacja była /etc/opt, a na macu , /Library/Application Support.

## <a name="changing-config-settings"></a>Zmiana ustawień konfiguracji

Plik `NuGet.Config` jest prostym plikiem tekstowym XML zawierającym pary klucz/wartość, zgodnie z opisem w temacie [Ustawienia konfiguracji NuGet.](../reference/nuget-config-file.md)

Ustawieniami zarządzają za pomocą [polecenia konfiguracyjnego](../reference/cli-reference/cli-ref-config.md)NuGet CLI:
- Domyślnie zmiany są wprowadzane do pliku konfiguracyjnego na poziomie użytkownika.
- Aby zmienić ustawienia w innym `-configFile` pliku, użyj przełącznika. W tym przypadku pliki mogą używać dowolnej nazwy pliku.
- W klawiszach zawsze rozróżniana jest wielkość liter.
- Podniesienie uprawnień jest wymagane do zmiany ustawień w pliku ustawień na poziomie komputera.

> [!Warning]
> Chociaż można zmodyfikować plik w dowolnym edytorze tekstu, NuGet (w wersji 3.4.3 lub nowszej) dyskretnie ignoruje cały plik konfiguracyjny, jeśli zawiera zniekształcony kod XML (niezgodne tagi, nieprawidłowe cudzysłowy itp.). Dlatego lepiej jest zarządzać ustawieniem za `nuget config`pomocą .

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
> W NuGet 3.4 i nowszych można używać zmiennych środowiskowych w dowolnej wartości, jak w `repositoryPath=%PACKAGEHOME%` (Windows) i `repositoryPath=$PACKAGEHOME` (Mac/Linux).

### <a name="removing-a-value"></a>Usuwanie wartości

Aby usunąć wartość, należy określić klucz o pustej wartości.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Tworzenie nowego pliku konfiguracyjnego

Skopiuj poniższy szablon `nuget config -configFile <filename>` do nowego pliku, a następnie użyj do ustawiania wartości:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Jak są stosowane ustawienia

Wiele `NuGet.Config` plików umożliwia przechowywanie ustawień w różnych lokalizacjach, dzięki czemu mają zastosowanie do jednego projektu, grupy projektów lub wszystkich projektów. Te ustawienia zbiorczo dotyczą dowolnej operacji NuGet wywołanej z wiersza polecenia lub programu Visual Studio, z ustawieniami, które istnieją "najbliżej" projektu lub bieżącego folderu mającego pierwszeństwo.

W szczególności NuGet ładuje ustawienia z różnych plików konfiguracyjnych w następującej kolejności:

1. [Plik NuGetDefaults.Config](#nuget-defaults-file), który zawiera ustawienia związane tylko ze źródłami pakietów.
1. Plik na poziomie komputera.
1. Plik na poziomie użytkownika.
1. Plik określony `-configFile`za pomocą pliku .
1. Pliki znalezione w każdym folderze w ścieżce z katalogu głównego dysku do bieżącego folderu (gdzie wywoływany jest plik nuget.exe lub folder zawierający projekt programu Visual Studio). Na przykład, jeśli polecenie jest wywoływane w c:\A\B\C, NuGet wyszukuje i ładuje pliki konfiguracyjne w c:\, następnie c:\A, następnie c:\A\B i na koniec c:\A\B\C.

Jak NuGet znajdzie ustawienia w tych plikach, są one stosowane w następujący sposób:

1. W przypadku elementów jednoeliskowych NuGet zastąpił dowolną wcześniej znalezioną wartość dla tego samego klucza. Oznacza to, że ustawienia, które są "najbliżej" do bieżącego folderu lub projektu zastąpić wszystkie inne znalezione wcześniej. Na przykład `defaultPushSource` ustawienie `NuGetDefaults.Config` w jest zastępowane, jeśli istnieje w innym pliku konfiguracyjnym.

1. Dla elementów kolekcji (takich jak `<packageSources>`), NuGet łączy wartości ze wszystkich plików konfiguracyjnych w jednej kolekcji.

1. Gdy `<clear />` jest obecny dla danego węzła, NuGet ignoruje wcześniej zdefiniowane wartości konfiguracji dla tego węzła.

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

Następnie masz `NuGet.Config` cztery pliki w następujących lokalizacjach z danej zawartości. (Plik na poziomie komputera nie jest uwzględniony w tym przykładzie, ale będzie zachowywać się podobnie do pliku na poziomie użytkownika).

Plik A. Plik na`%appdata%\NuGet\NuGet.Config` poziomie użytkownika `~/.config/NuGet/NuGet.Config` ( w systemie Windows, na Mac/Linux):

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

NuGet następnie ładuje i stosuje ustawienia w następujący sposób, w zależności od tego, gdzie jest wywoływany:

- **Wywoływane od disk_drive_1/użytkowników:** Używane jest tylko domyślne repozytorium wymienione w pliku konfiguracyjnym na poziomie użytkownika (A), ponieważ jest to jedyny plik znaleziony na disk_drive_1.

- **Wywoływane z disk_drive_2/ lub disk_drive_/tmp:** Najpierw jest ładowany plik na poziomie użytkownika (A), a następnie NuGet przechodzi do katalogu głównego disk_drive_2 i znajduje plik (B). NuGet również wyszukuje plik konfiguracyjny w /tmp, ale nie znajduje. W rezultacie używane jest domyślne repozytorium nuget.org, włączone jest przywracanie pakietu, a pakiety są rozszerzane w disk_drive_2/tmp.

- **Wywoływany z disk_drive_2/Project1 lub disk_drive_2/Project1/Source**: Najpierw jest ładowany plik na poziomie użytkownika (A), a następnie plik NuGet loads (B) z katalogu głównego disk_drive_2, a następnie plik (C). Ustawienia w (C) zastępują te w (B) `repositoryPath` i (A), więc miejsce, w którym pakiety są instalowane, jest disk_drive_2/Project1/External/Packages zamiast *disk_drive_2/tmp*. Ponadto, ponieważ (C) `<packageSources>`czyści , nuget.org nie jest już `https://MyPrivateRepo/ES/nuget`dostępna jako źródło pozostawiając tylko .

- **Wywoływany z disk_drive_2/Project2 lub disk_drive_2/Project2/Source**: Plik na poziomie użytkownika (A) jest ładowany najpierw po pliku (B) i pliku (D). Ponieważ `packageSources` nie jest wyczyszczone, zarówno `nuget.org` i `https://MyPrivateRepo/DQ/nuget` są dostępne jako źródła. Pakiety są rozszerzane w disk_drive_2/tmp, jak określono w (B).

## <a name="nuget-defaults-file"></a>Plik domyślny NuGet

Istnieje `NuGetDefaults.Config` plik, aby określić źródła pakietów, z których pakiety są instalowane i aktualizowane, oraz kontrolować domyślny cel publikowania pakietów za pomocą pliku `nuget push`. Ponieważ administratorzy mogą wygodnie (na przykład przy `NuGetDefaults.Config` użyciu zasad grupy) wdrażać spójne pliki na komputerach deweloperskich i kompilacji, mogą zapewnić, że wszyscy w organizacji używają odpowiednich źródeł pakietów, a nie nuget.org.

> [!Important]
> Plik `NuGetDefaults.Config` nigdy nie powoduje, że źródło pakietu do usunięcia z konfiguracji NuGet dewelopera. Oznacza to, że jeśli deweloper już używane NuGet i dlatego ma nuget.org źródło pakietu zarejestrowane, `NuGetDefaults.Config` nie zostanie usunięty po utworzeniu pliku.
>
> Ponadto ani `NuGetDefaults.Config` żaden inny mechanizm w NuGet może uniemożliwić dostęp do źródeł pakietów, takich jak nuget.org. Jeśli organizacja chce zablokować taki dostęp, musi użyć innych środków, takich jak zapory, aby to zrobić.

### <a name="nugetdefaultsconfig-location"></a>Lokalizacja Pliku NuGetDefaults.Config

W poniższej tabeli opisano, gdzie `NuGetDefaults.Config` plik powinien być przechowywany, w zależności od docelowego systemu operacyjnego:

| Platforma systemu operacyjnego  | Lokalizacja pliku NuGetDefaults.Config |
| --- | --- |
| Windows      | **Visual Studio 2017 lub NuGet 4.x+:**`%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 i starsze lub NuGet 3.x i wcześniej:**`%PROGRAMDATA%\NuGet` |
| System Mac/Linux    | `$XDG_DATA_HOME`(zazwyczaj `~/.local/share` lub `/usr/local/share`, w zależności od dystrybucji systemu operacyjnego)|

### <a name="nugetdefaultsconfig-settings"></a>Ustawienia pliku NuGetDefaults.Config

- `packageSources`: ta kolekcja ma `packageSources` takie samo znaczenie jak w zwykłych plikach konfiguracyjnych i określa źródła domyślne. NuGet używa źródeł w kolejności podczas instalowania lub aktualizowania pakietów w projektach przy użyciu formatu `packages.config` zarządzania. W przypadku projektów przy użyciu formatu PackageReference, NuGet używa najpierw źródeł lokalnych, a następnie źródeł na udziałach sieciowych, a następnie źródeł HTTP, niezależnie od kolejności w plikach konfiguracyjnych. NuGet zawsze ignoruje kolejność źródeł z operacjami przywracania.

- `disabledPackageSources`: ta kolekcja ma również `NuGet.Config` takie samo znaczenie jak w plikach, gdzie każde źródło, którego dotyczy problem, jest wymienione według jego nazwy i wartości true/false wskazującej, czy jest wyłączona. Dzięki temu nazwa źródła i `packageSources` adres URL pozostają w bez konieczności jego domyślnie włączone. Poszczególni deweloperzy mogą następnie ponownie włączyć źródło, `NuGet.Config` ustawiając wartość źródła na false w innych plikach bez konieczności ponownego znajdowania poprawnego adresu URL. Jest to również przydatne do dostarczania deweloperom pełną listę wewnętrznych źródłowych adresów URL dla organizacji, jednocześnie włączając domyślnie tylko źródło pojedynczego zespołu.

- `defaultPushSource`: określa domyślny `nuget push` cel dla operacji, zastępując wbudowany domyślny nuget.org. Administratorzy mogą wdrożyć to ustawienie, aby uniknąć publikowania pakietów wewnętrznych w nuget.org `nuget push -Source` publicznych przez przypadek, ponieważ deweloperzy muszą używać do publikowania w celu nuget.org.

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
