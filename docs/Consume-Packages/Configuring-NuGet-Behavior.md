---
title: Konfigurowanie zachowania NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Pliki NuGet.Config kontrolowania zachowania NuGet, globalnie i na podstawie na projekt i są modyfikowane za pomocą polecenia konfiguracyjnego nuget.
keywords: Pliki konfiguracji programu NuGet, NuGet ustawienia zachowania NuGet, konfigurowanie ustawień NuGet, Nuget.Config, NuGetDefaults.Config, wartości domyślne
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a575868894d5ca9992b1c9984cf4920bd2858209
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="configuring-nuget-behavior"></a>Konfigurowanie zachowania NuGet

Zachowanie NuGet jest wymuszany przez wszystkich ustawień w co najmniej jednej `NuGet.Config` plików (XML), może istnieć projektu, użytkownika i komputera poziomów. Globalny `NuGetDefaults.Config` pliku konfiguruje również specjalnie źródeł pakietów. Ustawienia stosowane do wszystkich poleceń wykonania interfejsu wiersza polecenia, w konsoli Menedżera pakietów i interfejsu użytkownika Menedżera pakietów.

## <a name="config-file-locations-and-uses"></a>Lokalizacje plików konfiguracji i używa

| Zakres | Lokalizacja pliku NuGet.Config. | Opis |
| --- | --- | --- |
| Projekt | Bieżący folder (alias folderu projektu) lub dowolnego folderu do katalogu głównego dysku.| W folderze projektu ustawienia mają zastosowanie tylko do tego projektu. W folderów nadrzędnych zawierających wiele projektów podfolderów ustawienia mają zastosowanie do wszystkich projektów w tych podfolderach. |
| Użytkownik | System Windows: `%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux: `~/.nuget/NuGet/NuGet.Config` | Ustawienia stosowane do wszystkich operacji, ale są zastępowane przez wszystkie ustawienia na poziomie projektu. |
| Komputer | System Windows: `%ProgramFiles(x86)%\NuGet\Config`<br/>System Mac/Linux: `$XDG_DATA_HOME` (zazwyczaj `~/.local/share`) | Ustawienia stosowane do wszystkich operacji na komputerze, ale zostały zastąpione przez wszystkie ustawienia na poziomie użytkownika lub projektu. |

Uwagi dotyczące starszych wersji programu NuGet:
- NuGet 3.3 i wcześniej używany `.nuget` folder ustawienia dotyczące całego rozwiązania. Ten plik nie jest używany w NuGet 3.4 +.
- Dla 2.6 NuGet do 3.x, pliku konfiguracji na poziomie komputera w systemie Windows znajduje się w lokalizacji % ProgramData%\NuGet\Config [\\{IDE} [\\{wersja} [\\{SKU}]]]\NuGet.Config, gdzie *{IDE}* może być  *Visual Studio*, *{wersja}* został wersji programu Visual Studio, takich jak *14.0*, i *{SKU}* jest *społeczności*, *Pro*, lub *Enterprise*. Aby przeprowadzić migrację ustawień do NuGet 4.0 +, po prostu skopiuj plik konfiguracji do % ProgramFiles(x86) % \NuGet\Config. W systemie Linux, to poprzedniej lokalizacji został /etc/opt, a dla komputerów Mac, Library/Application Support.

## <a name="changing-config-settings"></a>Zmiana ustawień konfiguracji

A `NuGet.Config` plik jest prosty plik tekstowy XML zawierający pary klucz wartość, zgodnie z opisem w [ustawienia konfiguracji NuGet](../reference/nuget-config-file.md) tematu.

Ustawienia są zarządzane przy użyciu interfejsu wiersza polecenia NuGet [polecenia konfiguracyjnego](../tools/cli-ref-config.md):
- Domyślnie zmiany zostały wprowadzone do pliku konfiguracji na poziomie użytkownika.
- Aby zmienić ustawienia w innym pliku, należy użyć `-configFile` przełącznika. W takim przypadku pliki można użyć nazwy pliku.
- Klucze są zawsze z uwzględnieniem wielkości liter.
- Podniesienie uprawnień jest wymagane do zmiany ustawień w pliku ustawień na poziomie komputera.

> [!Warning]
> Mimo że można zmodyfikować plik w edytorze tekstu, NuGet (v3.4.3 i nowsze) dyskretnie ignoruje całą konfigurację pliku, jeśli zawiera on nieprawidłowo sformułowany kod XML (niedopasowane tagi, nieprawidłowe znaki cudzysłowu, itp.). Dlatego zaleca się zarządzanie ustawienie przy użyciu `nuget config`.

### <a name="setting-a-value"></a>Ustawienie wartości

System Windows:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
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
> W NuGet 3.4 lub nowszym można używać zmiennych środowiskowych w żadnej wartości, podobnie jak w `repositoryPath=%PACKAGEHOME%` (system Windows) i `repositoryPath=%PACKAGEHOME` (system Mac/Linux).

### <a name="removing-a-value"></a>Usuwanie wartości

Aby usunąć wartość, należy określić klucz o wartości pustej.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Tworzenie nowego pliku konfiguracji

Kopiowanie szablonu poniżej do nowego pliku, a następnie użyć `nuget config -configFile <filename>` można ustawić wartości:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Jak są stosowane ustawienia

Wiele `NuGet.Config` pliki umożliwiają przechowywanie ustawień w różnych lokalizacjach, tak aby odnoszą się do pojedynczego projektu, grupy projektów lub wszystkich projektów. Te ustawienia dotyczą zbiorczo żadnej operacji NuGet wywołany z poziomu wiersza polecenia lub w programie Visual Studio z ustawień, które istnieje "najbliższy" do projektu lub bieżący folder biorąc pierwszeństwo.

W szczególności NuGet ładuje ustawienia z plików różnych konfiguracji w następującej kolejności:

1. [NuGetDefaults.Config pliku](#nuget-defaults-file), który zawiera ustawienia dotyczące tylko źródeł pakietów.
1. Plik poziomie komputera.
1. Plik na poziomie użytkownika.
1. Podany plik z `-configFile`.
1. Pliki znajdujące się w folderze, co w ścieżce z katalogu głównego dysku do bieżącego folderu (przywołane nuget.exe lub folder zawierający projekt programu Visual Studio). Na przykład, jeśli polecenie jest wywoływana w c:\A\B\C, NuGet wyszukuje i ładuje pliki konfiguracji w c:\, następnie c:\A, a następnie c:\A\B, a na końcu c:\A\B\C.

Jak NuGet znajdzie ustawień w tych plikach, są one stosowane w następujący sposób:

1. Dla elementów pojedynczego elementu NuGet zamienić wartości poprzednio znaleziono tego samego klucza. Oznacza to, ustawienia, które znajdują się w bieżącym folderze lub projektu "najbliżej" zastąpienie innych znalezionych wcześniej. Na przykład `defaultPushSource` w `NuGetDefaults.Config` zostanie zastąpione, jeśli istnieje on w innym pliku konfiguracji.

1. Kolekcja elementów (takich jak `<packageSources>`), NuGet łączy wartości z wszystkie pliki konfiguracji w jednej kolekcji.

1. Gdy `<clear />` występuje w przypadku danego węzła NuGet ignoruje wartości konfiguracji wcześniej zdefiniowanego dla tego węzła.

### <a name="settings-walkthrough"></a>Ustawienia wskazówki

Załóżmy, że masz następujące struktury folderów na dwóch oddzielnych dyskach:

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

Następnie możesz wybrać cztery `NuGet.Config` pliki w następujących lokalizacjach z danej zawartości. (Plik poziomie komputera jest niedostępna w tym przykładzie, ale czy zachowują się podobnie do pliku na poziomie użytkownika).

A. użytkownika na poziomie pliku (`%appdata%\NuGet\NuGet.Config` w systemie Windows, `~/.nuget/NuGet/NuGet.Config` na system Mac/Linux):

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

NuGet, a następnie ładuje i stosuje ustawienia w następujący sposób, w zależności od tego, gdzie jest wywoływany:

- **Wywoływany z disk_drive_1/użytkownicy**: używane tylko repozytorium domyślne wymienione w pliku konfiguracji na poziomie użytkownika (A), ponieważ jest to jedyny plik znaleziono na disk_drive_1.

- **Wywoływany z disk_drive_2 / lub disk_drive_/tmp**: najpierw załadować pliku na poziomie użytkownika (A), a następnie NuGet przechodzi do katalogu głównego disk_drive_2 i wyszukuje plik (B). NuGet także szuka pliku konfiguracyjnego /tmp, ale brakuje jednego. W związku z tym repozytorium domyślne na nuget.org jest używany, Przywracanie pakietu jest włączona i pakiety pobrać rozwinięty w disk_drive_2/tmp.

- **Wywoływane z disk_drive_2/Project1 lub disk_drive_2/Project1/źródła**: najpierw załadować pliku na poziomie użytkownika (A), a następnie NuGet obciążeń pliku (B) z folderu głównego disk_drive_2, a następnie pliku (C). Ustawienia w (C) zastępują (B) i (A), więc `repositoryPath` gdzie zainstalowane pakiety jest disk_drive_2/Project1/zewnętrznego/pakietów zamiast *disk_drive_2/tmp*. Ponadto ponieważ czyści (C) `<packageSources>`, nuget.org nie jest już dostępna jako źródła, pozostawiając tylko `https://MyPrivateRepo/ES/nuget`.

- **Wywoływane z projekcie disk_drive_2/2 lub disk_drive_2/projekcie 2/źródła**: załadowaniu pliku na poziomie użytkownika (A), najpierw następuje pliku (B) i pliku (D). Ponieważ `packageSources` jest nie wyczyszczony, zarówno `nuget.org` i `https://MyPrivateRepo/DQ/nuget` są dostępne jako źródła. Pakiety pobrać rozwinięty w disk_drive_2/tmp, jak określono w (B).

## <a name="nuget-defaults-file"></a>Plik ustawień domyślnych NuGet

`NuGetDefaults.Config` Plik istnieje, aby określić źródła pakietów, z których są zainstalowane i zaktualizowane pakiety oraz do sterowania domyślnego celu publikowania pakietów z `nuget push`. Ponieważ administratorzy mogą łatwo (na przykład przy użyciu zasad grupy) wdrażanie spójne `NuGetDefaults.Config` deweloperów i plików maszyny kompilacji, mogą zapewnienie, że wszyscy użytkownicy w organizacji używa poprawny pakiet źródeł, a nie nuget.org.

> [!Important]
> `NuGetDefaults.Config` Pliku nigdy nie powoduje źródła pakietów były usuwane z Konfiguracja nuget projektu dewelopera. Oznacza to, że jeśli projektanta został już użyty NuGet i w związku z tym ma w źródle pakietów nuget.org zarejestrowany, jego nie zostaną usunięte po utworzeniu `NuGetDefaults.Config` pliku.
>
> Ponadto, ani `NuGetDefaults.Config` ani innych mechanizmu w NuGet może uniemożliwić dostęp do pakietu źródeł, takich jak nuget.org. Jeśli organizacja chce zablokować takiego dostępu, znacznie użyć innych środków, takich jak zapory w tym celu.

### <a name="nugetdefaultsconfig-location"></a>NuGetDefaults.Config location

W poniższej tabeli opisano where `NuGetDefaults.Config` ma być przechowywany plik, w zależności od docelowego systemu operacyjnego:

| Platforma systemu operacyjnego  | NuGetDefaults.Config Location |
| --- | --- |
| Windows      | **Visual Studio 2017 or NuGet 4.x+:** %ProgramFiles(x86)%\NuGet\Config <br />**Visual Studio 2015 lub starszym lub NuGet 3.x i starszych wersji:** %PROGRAMDATA%\NuGet |
| Mac/Linux    | XDG_DATA_HOME $ (zazwyczaj ~/.local/share)|

### <a name="nugetdefaultsconfig-settings"></a>Ustawienia NuGetDefaults.Config

- `packageSources`: Ta kolekcja ma takie samo znaczenie jak `packageSources` w regularnych pliki konfiguracji i umożliwia określenie źródeł domyślne. NuGet korzysta ze źródłami w kolejności podczas instalowania lub aktualizowania pakietów w projektach przy użyciu `packages.config` format zarządzania. Dla projektów w formacie PackageReference NuGet najpierw używa lokalnego źródła, a następnie źródeł w udziałach sieciowych, a następnie źródła HTTP, niezależnie od tego, w kolejności, w plikach konfiguracji. NuGet zawsze ignoruje kolejność źródeł za pomocą operacji przywracania.

- `disabledPackageSources`: Ta kolekcja również ma takie samo znaczenie jak w `NuGet.Config` plików, gdy każdego dotyczy źródła znajduje się jego nazwa i wartość PRAWDA/FAŁSZ wskazującą czy jest ona wyłączona. Dzięki temu nazwa źródła i adres URL ma pozostawać w `packageSources` bez konieczności ona domyślnie włączona. Każdy deweloper może następnie ponownie włącz jej źródło przez ustawienie wartości false w innych wartość źródła `NuGet.Config` plików bez konieczności ponownie znaleźć poprawny adres URL. To także dostarczyć deweloperom pełną listę wewnętrzny źródłowy adres URL dla organizacji, podczas włączania tylko źródła indywidualnych zespołu domyślnie.

- `defaultPushSource`: Określa domyślnego celu `nuget push` operacje zastępowania wbudowanej domyślnej nuget.org. Administratorzy mogą wdrożyć to ustawienie, aby uniknąć publikowania pakietów wewnętrzny do publicznego nuget.org przypadkowo, jak deweloperzy w szczególności należy użyć `nuget push -Source` do publikowania nuget.org.

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
