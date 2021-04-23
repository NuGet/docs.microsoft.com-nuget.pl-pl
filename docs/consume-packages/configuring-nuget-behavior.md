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
# <a name="common-nuget-configurations"></a><span data-ttu-id="20778-103">Typowe konfiguracje narzędzia NuGet</span><span class="sxs-lookup"><span data-stu-id="20778-103">Common NuGet configurations</span></span>

<span data-ttu-id="20778-104">Zachowanie programu NuGet jest oparte na skumulowanych ustawieniach w co najmniej jednym pliku (XML), które mogą istnieć na poziomie całego projektu, użytkownika `NuGet.Config` i komputera.</span><span class="sxs-lookup"><span data-stu-id="20778-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="20778-105">Plik globalny `NuGetDefaults.Config` również specjalnie konfiguruje źródła pakietów.</span><span class="sxs-lookup"><span data-stu-id="20778-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="20778-106">Ustawienia dotyczą wszystkich poleceń wydanych w interfejsie wiersza polecenia, Menedżer pakietów i interfejsie Menedżer pakietów użytkownika.</span><span class="sxs-lookup"><span data-stu-id="20778-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="20778-107">Lokalizacje i zastosowania pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="20778-107">Config file locations and uses</span></span>

| <span data-ttu-id="20778-108">Zakres</span><span class="sxs-lookup"><span data-stu-id="20778-108">Scope</span></span> | <span data-ttu-id="20778-109">`NuGet.Config` lokalizacja pliku</span><span class="sxs-lookup"><span data-stu-id="20778-109">`NuGet.Config` file location</span></span> | <span data-ttu-id="20778-110">Opis</span><span class="sxs-lookup"><span data-stu-id="20778-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="20778-111">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="20778-111">Solution</span></span> | <span data-ttu-id="20778-112">Bieżący folder (folder rozwiązania) lub dowolny folder aż do katalogu głównego dysku.</span><span class="sxs-lookup"><span data-stu-id="20778-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="20778-113">W folderze rozwiązania ustawienia są stosowane do wszystkich projektów w podfolderach.</span><span class="sxs-lookup"><span data-stu-id="20778-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="20778-114">Należy pamiętać, że jeśli plik konfiguracji zostanie umieszczony w folderze projektu, nie ma to wpływu na ten projekt.</span><span class="sxs-lookup"><span data-stu-id="20778-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="20778-115">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="20778-115">User</span></span> | <span data-ttu-id="20778-116">**Windows:**`%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="20778-116">**Windows:** `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="20778-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` lub `~/.nuget/NuGet/NuGet.Config` (zależy od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="20778-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> <br/><span data-ttu-id="20778-118">Dodatkowe konfiguracje są obsługiwane na wszystkich platformach.</span><span class="sxs-lookup"><span data-stu-id="20778-118">Additional configs are supported on all platforms.</span></span> <span data-ttu-id="20778-119">Tych konfiguracji nie można edytować za pomocą narzędzi.</span><span class="sxs-lookup"><span data-stu-id="20778-119">These configs cannot be edited by the tooling.</span></span> </br> <span data-ttu-id="20778-120">**Windows:**`%appdata%\NuGet\config\*.Config`</span><span class="sxs-lookup"><span data-stu-id="20778-120">**Windows:** `%appdata%\NuGet\config\*.Config`</span></span> <br/><span data-ttu-id="20778-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` Lub `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="20778-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> | <span data-ttu-id="20778-122">Ustawienia mają zastosowanie do wszystkich operacji, ale są zastępowany przez dowolne ustawienia na poziomie projektu.</span><span class="sxs-lookup"><span data-stu-id="20778-122">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="20778-123">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="20778-123">Computer</span></span> | <span data-ttu-id="20778-124">**Windows:**`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="20778-124">**Windows:** `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="20778-125">**Mac/Linux:** `$XDG_DATA_HOME` .</span><span class="sxs-lookup"><span data-stu-id="20778-125">**Mac/Linux:** `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="20778-126">Wartość `$XDG_DATA_HOME` null lub pusta albo wartość będzie używana `~/.local/share` `/usr/local/share` (różni się w zależności od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="20778-126">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="20778-127">Ustawienia mają zastosowanie do wszystkich operacji na komputerze, ale są zastępowany przez dowolne ustawienia na poziomie użytkownika lub projektu.</span><span class="sxs-lookup"><span data-stu-id="20778-127">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="20778-128">Uwagi dotyczące wcześniejszych wersji programu NuGet:</span><span class="sxs-lookup"><span data-stu-id="20778-128">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="20778-129">Program NuGet w wersji 3.3 i starszych używa `.nuget` folderu dla ustawień całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="20778-129">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="20778-130">Ten folder nie jest używany w programie NuGet 3.4+.</span><span class="sxs-lookup"><span data-stu-id="20778-130">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="20778-131">W przypadku pakietu NuGet w wersji 2.6 do 3.x plik konfiguracji na poziomie komputera w systemie Windows znajdował się w pliku , gdzie może to być , Visual Studio wersja, taka jak , i to , `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]\NuGet.Config` `{IDE}` lub `VisualStudio` `{Version}` `14.0` `{SKU}` `Community` `Pro` `Enterprise` .</span><span class="sxs-lookup"><span data-stu-id="20778-131">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]\NuGet.Config`, where `{IDE}` can be `VisualStudio`, `{Version}` was the Visual Studio version such as `14.0`, and `{SKU}` is either `Community`, `Pro`, or `Enterprise`.</span></span> <span data-ttu-id="20778-132">Aby przeprowadzić migrację ustawień do programu NuGet 4.0+, po prostu skopiuj plik konfiguracji do pliku `%ProgramFiles(x86)%\NuGet\Config` .</span><span class="sxs-lookup"><span data-stu-id="20778-132">To migrate settings to NuGet 4.0+, simply copy the config file to `%ProgramFiles(x86)%\NuGet\Config`.</span></span> <span data-ttu-id="20778-133">W systemie Linux ta poprzednia lokalizacja to `/etc/opt` , a na komputerze Mac — `/Library/Application Support` .</span><span class="sxs-lookup"><span data-stu-id="20778-133">On Linux, this previous location was `/etc/opt`, and on Mac, `/Library/Application Support`.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="20778-134">Zmienianie ustawień konfiguracji</span><span class="sxs-lookup"><span data-stu-id="20778-134">Changing config settings</span></span>

<span data-ttu-id="20778-135">Plik `NuGet.Config` to prosty plik tekstowy XML zawierający pary klucz/wartość zgodnie z opisem w temacie Ustawienia konfiguracji [nuGet.](../reference/nuget-config-file.md)</span><span class="sxs-lookup"><span data-stu-id="20778-135">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="20778-136">Ustawieniami zarządza się za pomocą polecenia [konfiguracji interfejsu](../reference/cli-reference/cli-ref-config.md)wiersza polecenia nuGet:</span><span class="sxs-lookup"><span data-stu-id="20778-136">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="20778-137">Domyślnie zmiany są dokonywane w pliku konfiguracji na poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="20778-137">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="20778-138">Aby zmienić ustawienia w innym pliku, użyj `-configFile` przełącznika .</span><span class="sxs-lookup"><span data-stu-id="20778-138">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="20778-139">W takim przypadku pliki mogą używać dowolnej nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="20778-139">In this case files can use any filename.</span></span>
- <span data-ttu-id="20778-140">W kluczach jest zawsze wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="20778-140">Keys are always case sensitive.</span></span>
- <span data-ttu-id="20778-141">Podniesienie uprawnień jest wymagane do zmiany ustawień w pliku ustawień na poziomie komputera.</span><span class="sxs-lookup"><span data-stu-id="20778-141">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="20778-142">Chociaż plik można zmodyfikować w dowolnym edytorze tekstów, nuGet (wersja 3.4.3 i nowsze) dyskretnie ignoruje cały plik konfiguracji, jeśli zawiera źle sformułowany kod XML (niezgodne tagi, nieprawidłowe cudzysłowy itp.).</span><span class="sxs-lookup"><span data-stu-id="20778-142">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="20778-143">Dlatego lepiej jest zarządzać ustawieniem przy użyciu programu `nuget config` .</span><span class="sxs-lookup"><span data-stu-id="20778-143">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="20778-144">Ustawianie wartości</span><span class="sxs-lookup"><span data-stu-id="20778-144">Setting a value</span></span>

<span data-ttu-id="20778-145">W systemie Windows:</span><span class="sxs-lookup"><span data-stu-id="20778-145">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="20778-146">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="20778-146">Mac/Linux:</span></span>

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
> <span data-ttu-id="20778-147">W programie NuGet 3.4 lub nowszym można używać zmiennych środowiskowych w dowolnej wartości, tak jak w `repositoryPath=%PACKAGEHOME%` systemach (Windows) i `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="20778-147">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="20778-148">Usuwanie wartości</span><span class="sxs-lookup"><span data-stu-id="20778-148">Removing a value</span></span>

<span data-ttu-id="20778-149">Aby usunąć wartość, określ klucz z pustą wartością.</span><span class="sxs-lookup"><span data-stu-id="20778-149">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="20778-150">Tworzenie nowego pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="20778-150">Creating a new config file</span></span>

<span data-ttu-id="20778-151">Skopiuj poniższy szablon do nowego pliku, a następnie użyj funkcji `nuget config -configFile <filename>` , aby ustawić wartości:</span><span class="sxs-lookup"><span data-stu-id="20778-151">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="20778-152">Jak są stosowane ustawienia</span><span class="sxs-lookup"><span data-stu-id="20778-152">How settings are applied</span></span>

<span data-ttu-id="20778-153">Wiele plików umożliwia przechowywanie ustawień w różnych lokalizacjach, tak aby dotyczyły pojedynczego projektu, grupy `NuGet.Config` projektów lub wszystkich projektów.</span><span class="sxs-lookup"><span data-stu-id="20778-153">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="20778-154">Te ustawienia mają zbiorczo zastosowanie do każdej operacji NuGet wywoływanej z wiersza polecenia lub z programu Visual Studio, z ustawieniami, które istnieją "najbliżej" projektu lub bieżącego folderu, które mają pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="20778-154">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="20778-155">W szczególności program NuGet ładuje ustawienia z różnych plików konfiguracji w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="20778-155">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="20778-156">Plik [ `NuGetDefaults.Config` ,](#nuget-defaults-file)który zawiera ustawienia związane tylko ze źródłami pakietów.</span><span class="sxs-lookup"><span data-stu-id="20778-156">The [`NuGetDefaults.Config` file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="20778-157">Plik na poziomie komputera.</span><span class="sxs-lookup"><span data-stu-id="20778-157">The computer-level file.</span></span>
1. <span data-ttu-id="20778-158">Plik na poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="20778-158">The user-level file.</span></span>
1. <span data-ttu-id="20778-159">Plik określony za `-configFile` pomocą .</span><span class="sxs-lookup"><span data-stu-id="20778-159">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="20778-160">Pliki znalezione w każdym folderze w ścieżce od katalogu głównego dysku do bieżącego folderu (gdzie jest wywoływany lub folderu zawierającego Visual Studio `nuget.exe` projektu).</span><span class="sxs-lookup"><span data-stu-id="20778-160">Files found in every folder in the path from the drive root to the current folder (where `nuget.exe` is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="20778-161">Jeśli na przykład polecenie jest wywoływane w pliku , program NuGet szuka i ładuje pliki konfiguracji w plikach `c:\A\B\C` , następnie , , i na końcu `c:\` `c:\A` `c:\A\B` `c:\A\B\C` .</span><span class="sxs-lookup"><span data-stu-id="20778-161">For example, if a command is invoked in `c:\A\B\C`, NuGet looks for and loads config files in `c:\`, then `c:\A`, then `c:\A\B`, and finally `c:\A\B\C`.</span></span>

<span data-ttu-id="20778-162">Gdy nuGet znajdzie ustawienia w tych plikach, są one stosowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="20778-162">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="20778-163">W przypadku elementów z jednym elementem program NuGet zastąpił wszystkie wcześniej znalezione wartości dla tego samego klucza.</span><span class="sxs-lookup"><span data-stu-id="20778-163">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="20778-164">Oznacza to, że ustawienia znajdujące się "najbliżej" bieżącego folderu lub projektu przesłaniają wszystkie znalezione wcześniej ustawienia.</span><span class="sxs-lookup"><span data-stu-id="20778-164">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="20778-165">Na przykład ustawienie `defaultPushSource` w pliku `NuGetDefaults.Config` zostanie zastąpione, jeśli istnieje w dowolnym innym pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="20778-165">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>
1. <span data-ttu-id="20778-166">W przypadku elementów kolekcji (takich jak ) program NuGet łączy wartości ze `<packageSources>` wszystkich plików konfiguracji w jedną kolekcję.</span><span class="sxs-lookup"><span data-stu-id="20778-166">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>
1. <span data-ttu-id="20778-167">Gdy `<clear />` jest obecny dla danego węzła, nuGet ignoruje wcześniej zdefiniowane wartości konfiguracji dla tego węzła.</span><span class="sxs-lookup"><span data-stu-id="20778-167">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="20778-168">Przewodnik po ustawieniach</span><span class="sxs-lookup"><span data-stu-id="20778-168">Settings walkthrough</span></span>

<span data-ttu-id="20778-169">Załóżmy, że masz następującą strukturę folderów na dwóch oddzielnych dyskach:</span><span class="sxs-lookup"><span data-stu-id="20778-169">Let's say you have the following folder structure on two separate drives:</span></span>

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

<span data-ttu-id="20778-170">Następnie masz cztery `NuGet.Config` pliki w następujących lokalizacjach z podaną zawartością.</span><span class="sxs-lookup"><span data-stu-id="20778-170">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="20778-171">(Plik na poziomie komputera nie jest uwzględniony w tym przykładzie, ale będzie działać podobnie do pliku na poziomie użytkownika).</span><span class="sxs-lookup"><span data-stu-id="20778-171">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="20778-172">Plik A. Plik na poziomie użytkownika ( `%appdata%\NuGet\NuGet.Config` w systemie Windows w systemie `~/.config/NuGet/NuGet.Config` Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="20778-172">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="20778-173">Plik B. `disk_drive_2/NuGet.Config` :</span><span class="sxs-lookup"><span data-stu-id="20778-173">File B. `disk_drive_2/NuGet.Config`:</span></span>

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

<span data-ttu-id="20778-174">Plik C. `disk_drive_2/Project1/NuGet.Config` :</span><span class="sxs-lookup"><span data-stu-id="20778-174">File C. `disk_drive_2/Project1/NuGet.Config`:</span></span>

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

<span data-ttu-id="20778-175">Plik D. `disk_drive_2/Project2/NuGet.Config` :</span><span class="sxs-lookup"><span data-stu-id="20778-175">File D. `disk_drive_2/Project2/NuGet.Config`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="20778-176">Następnie nuGet ładuje i stosuje ustawienia w następujący sposób, w zależności od tego, gdzie jest wywoływany:</span><span class="sxs-lookup"><span data-stu-id="20778-176">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="20778-177">**Wywoływane `disk_drive_1/users` z**: używane jest tylko domyślne repozytorium wymienione w pliku konfiguracji na poziomie użytkownika (A), ponieważ jest to jedyny plik znaleziony w pliku `disk_drive_1` .</span><span class="sxs-lookup"><span data-stu-id="20778-177">**Invoked from `disk_drive_1/users`**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on `disk_drive_1`.</span></span>

- <span data-ttu-id="20778-178">**Wywoływane z `disk_drive_2/` lub `disk_drive_/tmp`**: najpierw jest ładowany plik na poziomie użytkownika (A), a następnie nuGet przechodzi do katalogu głównego pliku i znajduje plik `disk_drive_2` (B).</span><span class="sxs-lookup"><span data-stu-id="20778-178">**Invoked from `disk_drive_2/` or `disk_drive_/tmp`**: The user-level file (A) is loaded first, then NuGet goes to the root of `disk_drive_2` and finds file (B).</span></span> <span data-ttu-id="20778-179">Program NuGet wyszukuje również plik konfiguracji w pliku `/tmp` , ale nie znajduje go.</span><span class="sxs-lookup"><span data-stu-id="20778-179">NuGet also looks for a configuration file in `/tmp` but does not find one.</span></span> <span data-ttu-id="20778-180">W związku z tym jest używane domyślne repozytorium w repozytorium , przywracanie pakietów jest włączone, a pakiety są `nuget.org` rozszerzane w . `disk_drive_2/tmp`</span><span class="sxs-lookup"><span data-stu-id="20778-180">As a result, the default repository on `nuget.org` is used, package restore is enabled, and packages get expanded in `disk_drive_2/tmp`.</span></span>

- <span data-ttu-id="20778-181">**Wywoływany z `disk_drive_2/Project1` lub `disk_drive_2/Project1/Source`**: najpierw jest ładowany plik na poziomie użytkownika (A), a następnie nuGet ładuje plik (B) z katalogu głównego , a następnie plik `disk_drive_2` (C).</span><span class="sxs-lookup"><span data-stu-id="20778-181">**Invoked from `disk_drive_2/Project1` or `disk_drive_2/Project1/Source`**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of `disk_drive_2`, followed by file (C).</span></span> <span data-ttu-id="20778-182">Ustawienia w programie (C) zastępują ustawienia w systemach (B) i (A), więc miejsce, w którym `repositoryPath` instalowane są pakiety, `disk_drive_2/Project1/External/Packages` to zamiast `disk_drive_2/tmp` .</span><span class="sxs-lookup"><span data-stu-id="20778-182">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is `disk_drive_2/Project1/External/Packages` instead of `disk_drive_2/tmp`.</span></span> <span data-ttu-id="20778-183">Ponadto, ponieważ (C) czyszczy `<packageSources>` , nuget.org nie jest już dostępna jako źródło, pozostawiając tylko `https://MyPrivateRepo/ES/nuget` .</span><span class="sxs-lookup"><span data-stu-id="20778-183">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="20778-184">**Wywoływane z `disk_drive_2/Project2` lub `disk_drive_2/Project2/Source`**: plik na poziomie użytkownika (A) jest ładowany jako pierwszy, po którym następuje plik (B) i plik (D).</span><span class="sxs-lookup"><span data-stu-id="20778-184">**Invoked from `disk_drive_2/Project2` or `disk_drive_2/Project2/Source`**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="20778-185">Ponieważ `packageSources` nie jest wyczyszczyszona, `nuget.org` zarówno , jak i są dostępne jako `https://MyPrivateRepo/DQ/nuget` źródła.</span><span class="sxs-lookup"><span data-stu-id="20778-185">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="20778-186">Pakiety są rozszerzane w `disk_drive_2/tmp` sposób określony w (B).</span><span class="sxs-lookup"><span data-stu-id="20778-186">Packages get expanded in `disk_drive_2/tmp` as specified in (B).</span></span>

## <a name="additional-user-wide-configuration"></a><span data-ttu-id="20778-187">Dodatkowa konfiguracja dla całego użytkownika</span><span class="sxs-lookup"><span data-stu-id="20778-187">Additional user wide configuration</span></span>

<span data-ttu-id="20778-188">Począwszy od programu 5.7, w programie NuGet dodano obsługę dodatkowych plików konfiguracji dla całego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="20778-188">Starting with 5.7, NuGet has added support for additional user wide configuration files.</span></span> <span data-ttu-id="20778-189">Dzięki temu dostawcy innych firm mogą dodawać dodatkowe pliki konfiguracji użytkownika bez podniesienia uprawnień.</span><span class="sxs-lookup"><span data-stu-id="20778-189">This allows third-party vendors to add additional user configuration files without elevation.</span></span>
<span data-ttu-id="20778-190">Te pliki konfiguracji znajdują się w folderze konfiguracji użytkownika standardowego w `config` podfolderze.</span><span class="sxs-lookup"><span data-stu-id="20778-190">These configuration files are found in the standard user wide configuration folder within a `config` subfolder.</span></span>
<span data-ttu-id="20778-191">Wszystkie pliki kończące się `.config` na lub `.Config` zostaną rozważone.</span><span class="sxs-lookup"><span data-stu-id="20778-191">All files ending with `.config` or `.Config` will be considered.</span></span>
<span data-ttu-id="20778-192">Tych plików nie można edytować za pomocą standardowych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="20778-192">These files cannot be edited by the standard tooling.</span></span>

| <span data-ttu-id="20778-193">Platforma systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="20778-193">OS Platform</span></span>  | <span data-ttu-id="20778-194">Dodatkowe konfiguracje</span><span class="sxs-lookup"><span data-stu-id="20778-194">Additional Configurations</span></span> |
| --- | --- |
| <span data-ttu-id="20778-195">Windows</span><span class="sxs-lookup"><span data-stu-id="20778-195">Windows</span></span>      | `%appdata%\NuGet\config\*.Config` |
| <span data-ttu-id="20778-196">System Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="20778-196">Mac/Linux</span></span>    | <span data-ttu-id="20778-197">`~/.config/NuGet/config/*.config` lub `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="20778-197">`~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> |

## <a name="nuget-defaults-file"></a><span data-ttu-id="20778-198">Plik domyślny nuGet</span><span class="sxs-lookup"><span data-stu-id="20778-198">NuGet defaults file</span></span>

<span data-ttu-id="20778-199">Plik istnieje, aby określić źródła pakietów, z których pakiety są instalowane i aktualizowane, oraz kontrolować domyślny element `NuGetDefaults.Config` docelowy publikowania pakietów za pomocą programu `nuget push` .</span><span class="sxs-lookup"><span data-stu-id="20778-199">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="20778-200">Ponieważ administratorzy mogą wygodnie (na przykład przy użyciu usługi zasady grupy) wdrażać spójne pliki na maszynach dewelopera i kompilacji, mogą zapewnić, że wszyscy w organizacji będą używać odpowiednich źródeł pakietów, a nie `NuGetDefaults.Config` nuget.org.</span><span class="sxs-lookup"><span data-stu-id="20778-200">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="20778-201">Plik nigdy nie powoduje usunięcia źródła pakietu z konfiguracji `NuGetDefaults.Config` NuGet dewelopera.</span><span class="sxs-lookup"><span data-stu-id="20778-201">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="20778-202">Oznacza to, że jeśli deweloper już użył narzędzia NuGet i w związku z tym ma zarejestrowane źródło pakietu nuget.org, nie zostanie on usunięty po utworzeniu `NuGetDefaults.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="20778-202">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="20778-203">Ponadto ani żaden inny mechanizm w pakiecie NuGet nie może uniemożliwić dostępu do źródeł pakietów, takich `NuGetDefaults.Config` jak nuget.org. Jeśli organizacja chce zablokować taki dostęp, musi w tym celu użyć innych środków, takich jak zapory.</span><span class="sxs-lookup"><span data-stu-id="20778-203">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="20778-204">`NuGetDefaults.Config` Lokalizacji</span><span class="sxs-lookup"><span data-stu-id="20778-204">`NuGetDefaults.Config` location</span></span>

<span data-ttu-id="20778-205">W poniższej tabeli opisano `NuGetDefaults.Config` miejsce przechowywania pliku w zależności od docelowego systemu operacyjnego:</span><span class="sxs-lookup"><span data-stu-id="20778-205">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="20778-206">Platforma systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="20778-206">OS Platform</span></span>  | <span data-ttu-id="20778-207">`NuGetDefaults.Config` Lokalizacji</span><span class="sxs-lookup"><span data-stu-id="20778-207">`NuGetDefaults.Config` Location</span></span> |
| --- | --- |
| <span data-ttu-id="20778-208">Windows</span><span class="sxs-lookup"><span data-stu-id="20778-208">Windows</span></span>      | <span data-ttu-id="20778-209">**Visual Studio 2017 lub NuGet 4.x+:**`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="20778-209">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="20778-210">**Visual Studio 2015 i starsze lub NuGet 3.x i starsze:**`%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="20778-210">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="20778-211">System Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="20778-211">Mac/Linux</span></span>    | <span data-ttu-id="20778-212">`$XDG_DATA_HOME` (zazwyczaj `~/.local/share` lub `/usr/local/share` , w zależności od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="20778-212">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="20778-213">NuGetDefaults.Config ustawień</span><span class="sxs-lookup"><span data-stu-id="20778-213">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="20778-214">`packageSources`: ta kolekcja ma takie samo znaczenie `packageSources` jak w zwykłych plikach konfiguracji i określa domyślne źródła.</span><span class="sxs-lookup"><span data-stu-id="20778-214">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="20778-215">Program NuGet używa źródeł w kolejności podczas instalowania lub aktualizowania pakietów w projektach przy użyciu `packages.config` formatu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="20778-215">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="20778-216">W przypadku projektów korzystających z formatu PackageReference program NuGet najpierw używa źródeł lokalnych, a następnie źródeł w udziałach sieciowych, a następnie źródeł HTTP, niezależnie od kolejności w plikach konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="20778-216">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="20778-217">Program NuGet zawsze ignoruje kolejność źródeł w operacjach przywracania.</span><span class="sxs-lookup"><span data-stu-id="20778-217">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="20778-218">`disabledPackageSources`: ta kolekcja ma również takie samo znaczenie jak w plikach, gdzie każde źródło, którego dotyczy problem, jest wyświetlane według nazwy i wartości wskazującej, czy `NuGet.Config` `true` / `false` jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="20778-218">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a `true`/`false` value indicating whether it's disabled.</span></span> <span data-ttu-id="20778-219">Dzięki temu nazwa źródła i adres URL mogą pozostać w `packageSources` bez domyślnych włączone.</span><span class="sxs-lookup"><span data-stu-id="20778-219">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="20778-220">Poszczegnieni deweloperzy mogą ponownie włączyć źródło, ustawiając wartość źródła na w innych plikach bez konieczności ponownego znalezienia `false` `NuGet.Config` poprawnego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="20778-220">Individual developers can then re-enable the source by setting the source's value to `false` in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="20778-221">Jest to również przydatne w przypadku dostarczania deweloperom pełnej listy wewnętrznych adresów URL źródeł dla organizacji przy jednoczesnym domyślnym włączeniu tylko źródła poszczególnych reprezentacji zespołu.</span><span class="sxs-lookup"><span data-stu-id="20778-221">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="20778-222">`defaultPushSource`: określa domyślny element docelowy dla `nuget push` operacji, zastępując wbudowane ustawienie domyślne `nuget.org` .</span><span class="sxs-lookup"><span data-stu-id="20778-222">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of `nuget.org`.</span></span> <span data-ttu-id="20778-223">Administratorzy mogą wdrożyć to ustawienie, aby uniknąć publikowania pakietów wewnętrznych publicznie przypadkowo, ponieważ deweloperzy muszą używać programu do `nuget.org` `nuget push -Source` publikowania w programie `nuget.org` .</span><span class="sxs-lookup"><span data-stu-id="20778-223">Administrators can deploy this setting to avoid publishing internal packages to the public `nuget.org` by accident, as developers specifically need to use `nuget push -Source` to publish to `nuget.org`.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="20778-224">Przykładowe NuGetDefaults.Config aplikacji</span><span class="sxs-lookup"><span data-stu-id="20778-224">Example NuGetDefaults.Config and application</span></span>

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
