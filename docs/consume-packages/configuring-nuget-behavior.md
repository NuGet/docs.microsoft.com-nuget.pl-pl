---
title: Typowe konfiguracje narzędzia NuGet
description: NuGet.Config pliki kontrolują zachowanie narzędzia NuGet zarówno globalnie, jak i dla każdego projektu i są modyfikowane za pomocą polecenia konfiguracji NuGet.
author: JonDouglas
ms.author: jodou
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 35339626b0a20ccfceafa89fef94fb3187013fd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774853"
---
# <a name="common-nuget-configurations"></a><span data-ttu-id="5816f-103">Typowe konfiguracje narzędzia NuGet</span><span class="sxs-lookup"><span data-stu-id="5816f-103">Common NuGet configurations</span></span>

<span data-ttu-id="5816f-104">Zachowanie narzędzia NuGet jest zależne od ustawień skumulowanych w jednym lub kilku `NuGet.Config` plikach (XML), które mogą istnieć na poziomach na poziomie projektu, użytkownika i komputera.</span><span class="sxs-lookup"><span data-stu-id="5816f-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="5816f-105">Plik globalny `NuGetDefaults.Config` również służy do konfigurowania źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="5816f-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="5816f-106">Ustawienia dotyczą wszystkich poleceń wydawanych w interfejsie wiersza polecenia, konsoli Menedżera pakietów i interfejsu użytkownika Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="5816f-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="5816f-107">Lokalizacje i użycia plików konfiguracji</span><span class="sxs-lookup"><span data-stu-id="5816f-107">Config file locations and uses</span></span>

| <span data-ttu-id="5816f-108">Zakres</span><span class="sxs-lookup"><span data-stu-id="5816f-108">Scope</span></span> | <span data-ttu-id="5816f-109">Lokalizacja pliku NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="5816f-109">NuGet.Config file location</span></span> | <span data-ttu-id="5816f-110">Opis</span><span class="sxs-lookup"><span data-stu-id="5816f-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5816f-111">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="5816f-111">Solution</span></span> | <span data-ttu-id="5816f-112">Bieżący folder (folder rozwiązania) lub dowolny folder w katalogu głównym dysku.</span><span class="sxs-lookup"><span data-stu-id="5816f-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="5816f-113">W folderze rozwiązania ustawienia są stosowane do wszystkich projektów w podfolderach.</span><span class="sxs-lookup"><span data-stu-id="5816f-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="5816f-114">Należy pamiętać, że jeśli plik konfiguracyjny znajduje się w folderze projektu, nie ma wpływu na ten projekt.</span><span class="sxs-lookup"><span data-stu-id="5816f-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="5816f-115">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="5816f-115">User</span></span> | <span data-ttu-id="5816f-116">**System Windows:**`%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="5816f-116">**Windows:** `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="5816f-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` lub `~/.nuget/NuGet/NuGet.Config` (w zależności od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="5816f-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> <br/><span data-ttu-id="5816f-118">Dodatkowe konfiguracje są obsługiwane na wszystkich platformach.</span><span class="sxs-lookup"><span data-stu-id="5816f-118">Additional configs are supported on all platforms.</span></span> <span data-ttu-id="5816f-119">Te konfiguracje nie mogą być edytowane przez narzędzia.</span><span class="sxs-lookup"><span data-stu-id="5816f-119">These configs cannot be edited by the tooling.</span></span> </br> <span data-ttu-id="5816f-120">**System Windows:**`%appdata%\NuGet\config\*.Config`</span><span class="sxs-lookup"><span data-stu-id="5816f-120">**Windows:** `%appdata%\NuGet\config\*.Config`</span></span> <br/><span data-ttu-id="5816f-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` oraz `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="5816f-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> | <span data-ttu-id="5816f-122">Ustawienia dotyczą wszystkich operacji, ale są zastępowane przez dowolne ustawienia na poziomie projektu.</span><span class="sxs-lookup"><span data-stu-id="5816f-122">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="5816f-123">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="5816f-123">Computer</span></span> | <span data-ttu-id="5816f-124">**System Windows:**`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="5816f-124">**Windows:** `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="5816f-125">**Mac/Linux:** `$XDG_DATA_HOME` .</span><span class="sxs-lookup"><span data-stu-id="5816f-125">**Mac/Linux:** `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="5816f-126">Jeśli `$XDG_DATA_HOME` ma wartość null lub jest pusty `~/.local/share` lub `/usr/local/share` będzie używany (zależy od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="5816f-126">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="5816f-127">Ustawienia dotyczą wszystkich operacji na komputerze, ale są zastępowane przez dowolne ustawienia użytkownika lub poziomu projektu.</span><span class="sxs-lookup"><span data-stu-id="5816f-127">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="5816f-128">Uwagi dotyczące wcześniejszych wersji programu NuGet:</span><span class="sxs-lookup"><span data-stu-id="5816f-128">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="5816f-129">Pakiet NuGet 3,3 i wcześniejsze użycie `.nuget` folderu dla ustawień całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5816f-129">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="5816f-130">Ten folder nie jest używany w programie NuGet 3.4 +.</span><span class="sxs-lookup"><span data-stu-id="5816f-130">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="5816f-131">W przypadku programu NuGet 2,6 do 3. x plik konfiguracyjny na poziomie komputera w systemie Windows został zlokalizowany w%ProgramData%\NuGet\Config [ \\ {IDE} [ \\ {Version} [ \\ {SKU}]]] \NuGet.Config, gdzie *{IDE}* może być *VisualStudio*, *{Version}* była wersją programu Visual Studio, taką jak *14,0*, i *{SKU}* to *społeczność*, *Pro* lub *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="5816f-131">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="5816f-132">Aby przeprowadzić migrację ustawień do programu NuGet 4.0 +, po prostu skopiuj plik konfiguracyjny do% ProgramFiles (x86)% \ NuGet\Config. W systemie Linux ta poprzednia lokalizacja została/etc/opt oraz na komputerach Mac,/Library/Application Support support.</span><span class="sxs-lookup"><span data-stu-id="5816f-132">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="5816f-133">Zmienianie ustawień konfiguracji</span><span class="sxs-lookup"><span data-stu-id="5816f-133">Changing config settings</span></span>

<span data-ttu-id="5816f-134">`NuGet.Config`Plik to prosty plik tekstowy XML zawierający pary klucz/wartość, zgodnie z opisem w temacie [Ustawienia konfiguracji programu NuGet](../reference/nuget-config-file.md) .</span><span class="sxs-lookup"><span data-stu-id="5816f-134">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="5816f-135">Ustawienia są zarządzane przy użyciu interfejsu wiersza [polecenia NuGet konfiguracji](../reference/cli-reference/cli-ref-config.md):</span><span class="sxs-lookup"><span data-stu-id="5816f-135">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="5816f-136">Domyślnie zmiany są wprowadzane w pliku konfiguracji na poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5816f-136">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="5816f-137">Aby zmienić ustawienia w innym pliku, należy użyć `-configFile` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="5816f-137">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="5816f-138">W tym przypadku pliki mogą używać dowolnych nazw plików.</span><span class="sxs-lookup"><span data-stu-id="5816f-138">In this case files can use any filename.</span></span>
- <span data-ttu-id="5816f-139">Klucze zawsze uwzględniają wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="5816f-139">Keys are always case sensitive.</span></span>
- <span data-ttu-id="5816f-140">Aby zmienić ustawienia w pliku ustawień na poziomie komputera, wymagana jest podniesienie uprawnień.</span><span class="sxs-lookup"><span data-stu-id="5816f-140">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="5816f-141">Chociaż można modyfikować plik w dowolnym edytorze tekstu, pakiet NuGet (v 3.4.3 i nowsze) w trybie cichym ignoruje cały plik konfiguracyjny, jeśli zawiera źle sformułowany kod XML (niezgodne Tagi, nieprawidłowe znaki cudzysłowu itp.).</span><span class="sxs-lookup"><span data-stu-id="5816f-141">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="5816f-142">Dlatego zaleca się zarządzanie ustawieniami przy użyciu `nuget config` .</span><span class="sxs-lookup"><span data-stu-id="5816f-142">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="5816f-143">Ustawianie wartości</span><span class="sxs-lookup"><span data-stu-id="5816f-143">Setting a value</span></span>

<span data-ttu-id="5816f-144">W systemie Windows:</span><span class="sxs-lookup"><span data-stu-id="5816f-144">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="5816f-145">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="5816f-145">Mac/Linux:</span></span>

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
> <span data-ttu-id="5816f-146">W programie NuGet 3,4 i nowszych można używać zmiennych środowiskowych w dowolnej wartości, jak w `repositoryPath=%PACKAGEHOME%` systemach (Windows) i `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="5816f-146">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="5816f-147">Usuwanie wartości</span><span class="sxs-lookup"><span data-stu-id="5816f-147">Removing a value</span></span>

<span data-ttu-id="5816f-148">Aby usunąć wartość, określ klucz z pustą wartością.</span><span class="sxs-lookup"><span data-stu-id="5816f-148">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="5816f-149">Tworzenie nowego pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="5816f-149">Creating a new config file</span></span>

<span data-ttu-id="5816f-150">Skopiuj szablon poniżej do nowego pliku, a następnie użyj, `nuget config -configFile <filename>` Aby ustawić wartości:</span><span class="sxs-lookup"><span data-stu-id="5816f-150">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="5816f-151">Jak są stosowane ustawienia</span><span class="sxs-lookup"><span data-stu-id="5816f-151">How settings are applied</span></span>

<span data-ttu-id="5816f-152">Wiele `NuGet.Config` plików umożliwia przechowywanie ustawień w różnych lokalizacjach, tak aby dotyczyły one jednego projektu, grupy projektów lub wszystkich projektów.</span><span class="sxs-lookup"><span data-stu-id="5816f-152">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="5816f-153">Te ustawienia są stosowane zbiorczo do każdej operacji NuGet wywołanej z wiersza polecenia lub z programu Visual Studio z ustawieniami, które istnieją "najbliżej" w projekcie lub bieżącym folderze, który ma pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="5816f-153">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="5816f-154">W programie NuGet są ładowane ustawienia z różnych plików konfiguracji w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="5816f-154">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="5816f-155">[PlikNuGetDefaults.Config](#nuget-defaults-file), który zawiera ustawienia dotyczące tylko źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="5816f-155">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="5816f-156">Plik na poziomie komputera.</span><span class="sxs-lookup"><span data-stu-id="5816f-156">The computer-level file.</span></span>
1. <span data-ttu-id="5816f-157">Plik na poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5816f-157">The user-level file.</span></span>
1. <span data-ttu-id="5816f-158">Plik określony przy użyciu `-configFile` .</span><span class="sxs-lookup"><span data-stu-id="5816f-158">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="5816f-159">Pliki znajdujące się w każdym folderze w ścieżce z katalogu głównego dysku do bieżącego folderu (gdzie nuget.exe są wywoływane lub folder zawierający projekt programu Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="5816f-159">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="5816f-160">Na przykład jeśli polecenie jest wywoływane w c:\A\B\C, NuGet szuka i ładuje pliki konfiguracji w c: \, then c:\a, c:\A\B i finally c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="5816f-160">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="5816f-161">Ponieważ program NuGet odnajdzie ustawienia w tych plikach, są one stosowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="5816f-161">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="5816f-162">W przypadku elementów jednego elementu NuGet zastępuje wszystkie poprzednio znalezione wartości dla tego samego klucza.</span><span class="sxs-lookup"><span data-stu-id="5816f-162">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="5816f-163">Oznacza to, że ustawienia, które są "najbliżej" w bieżącym folderze lub projekcie zastępują inne znalezione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="5816f-163">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="5816f-164">Na przykład `defaultPushSource` ustawienie w `NuGetDefaults.Config` jest zastępowane, jeśli istnieje w innym pliku konfiguracyjnym.</span><span class="sxs-lookup"><span data-stu-id="5816f-164">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="5816f-165">W przypadku elementów kolekcji (takich jak `<packageSources>` ) pakiet NuGet łączy wartości ze wszystkich plików konfiguracji w jedną kolekcję.</span><span class="sxs-lookup"><span data-stu-id="5816f-165">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="5816f-166">Gdy `<clear />` jest obecny dla danego węzła, pakiet NuGet ignoruje wcześniej zdefiniowane wartości konfiguracji dla tego węzła.</span><span class="sxs-lookup"><span data-stu-id="5816f-166">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="5816f-167">Przewodnik po ustawieniach</span><span class="sxs-lookup"><span data-stu-id="5816f-167">Settings walkthrough</span></span>

<span data-ttu-id="5816f-168">Załóżmy, że masz następującą strukturę folderów na dwóch oddzielnych dyskach:</span><span class="sxs-lookup"><span data-stu-id="5816f-168">Let's say you have the following folder structure on two separate drives:</span></span>

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

<span data-ttu-id="5816f-169">Następnie `NuGet.Config` w poniższych lokalizacjach znajdują się cztery pliki o podaną zawartość.</span><span class="sxs-lookup"><span data-stu-id="5816f-169">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="5816f-170">(Plik na poziomie komputera nie jest uwzględniony w tym przykładzie, ale zachowuje się podobnie do pliku na poziomie użytkownika).</span><span class="sxs-lookup"><span data-stu-id="5816f-170">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="5816f-171">Plik A. plik na poziomie użytkownika ( `%appdata%\NuGet\NuGet.Config` w systemie Windows, `~/.config/NuGet/NuGet.Config` na komputerze Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="5816f-171">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="5816f-172">Plik B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="5816f-172">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="5816f-173">Plik C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="5816f-173">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="5816f-174">Plik D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="5816f-174">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="5816f-175">Następnie program NuGet ładuje i stosuje ustawienia w następujący sposób, w zależności od tego, gdzie jest wywoływany:</span><span class="sxs-lookup"><span data-stu-id="5816f-175">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="5816f-176">**Wywołane z disk_drive_1/users**: używany jest tylko repozytorium domyślne wymienione w pliku konfiguracji na poziomie użytkownika (A), ponieważ jest to jedyny plik znaleziony w disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="5816f-176">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="5816f-177">**Wywołane z disk_drive_2/lub disk_drive_/tmp**: najpierw załadowano plik poziomu użytkownika (A), a następnie pakiet NuGet przechodzi do katalogu głównego disk_drive_2 i odnajdzie plik (B).</span><span class="sxs-lookup"><span data-stu-id="5816f-177">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="5816f-178">Pakiet NuGet szuka również pliku konfiguracji w programie/tmp, ale go nie znaleziono.</span><span class="sxs-lookup"><span data-stu-id="5816f-178">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="5816f-179">W związku z tym używane jest domyślne repozytorium w nuget.org, przywracanie pakietu jest włączone, a pakiety zostaną rozwinięte w disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="5816f-179">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="5816f-180">**Wywołane z disk_drive_2/Project1 lub disk_drive_2/Project1/Source**: najpierw załadowano plik na poziomie użytkownika (A), a następnie program NuGet ładuje plik (B) z katalogu głównego disk_drive_2, a następnie plik (C).</span><span class="sxs-lookup"><span data-stu-id="5816f-180">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="5816f-181">Ustawienia w (C) przesłaniają te w (B) i (A), dzięki czemu `repositoryPath` instalowane pakiety są disk_drive_2/Project1/External/Packages, a nie *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="5816f-181">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="5816f-182">Ponadto, ponieważ (C) czyści `<packageSources>` , NuGet.org nie jest już dostępne tylko jako źródło wychodzące `https://MyPrivateRepo/ES/nuget` .</span><span class="sxs-lookup"><span data-stu-id="5816f-182">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="5816f-183">**Wywołane z disk_drive_2/Project2 lub disk_drive_2/Project2/Source**: plik na poziomie użytkownika (A) jest ładowany po raz pierwszy, po którym następuje plik (B) i plik (D).</span><span class="sxs-lookup"><span data-stu-id="5816f-183">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="5816f-184">Ponieważ `packageSources` nie jest wyczyszczone, oba `nuget.org` i `https://MyPrivateRepo/DQ/nuget` są dostępne jako źródła.</span><span class="sxs-lookup"><span data-stu-id="5816f-184">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="5816f-185">Pakiety zostaną rozwinięte w disk_drive_2/tmp zgodnie z opisem w (B).</span><span class="sxs-lookup"><span data-stu-id="5816f-185">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="additional-user-wide-configuration"></a><span data-ttu-id="5816f-186">Dodatkowa konfiguracja dla wszystkich użytkowników</span><span class="sxs-lookup"><span data-stu-id="5816f-186">Additional user wide configuration</span></span>

<span data-ttu-id="5816f-187">Począwszy od 5,7, pakiet NuGet dodał obsługę dodatkowych plików konfiguracji o wielu użytkownikach.</span><span class="sxs-lookup"><span data-stu-id="5816f-187">Starting with 5.7, NuGet has added support for additional user wide configuration files.</span></span> <span data-ttu-id="5816f-188">Umożliwia to dostawcom innych firm Dodawanie dodatkowych plików konfiguracji użytkownika bez podniesienia uprawnień.</span><span class="sxs-lookup"><span data-stu-id="5816f-188">This allows third-party vendors to add additional user configuration files without elevation.</span></span>
<span data-ttu-id="5816f-189">Te pliki konfiguracyjne znajdują się w folderze Standardowa konfiguracja użytkownika w `config` podfolderze.</span><span class="sxs-lookup"><span data-stu-id="5816f-189">These configuration files are found in the standard user wide configuration folder within a `config` subfolder.</span></span>
<span data-ttu-id="5816f-190">Wszystkie pliki kończące się na `.config` lub `.Config` zostaną uwzględnione.</span><span class="sxs-lookup"><span data-stu-id="5816f-190">All files ending with `.config` or `.Config` will be considered.</span></span>
<span data-ttu-id="5816f-191">Tych plików nie można edytować za pomocą standardowych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="5816f-191">These files cannot be edited by the standard tooling.</span></span>

| <span data-ttu-id="5816f-192">Platforma systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="5816f-192">OS Platform</span></span>  | <span data-ttu-id="5816f-193">Dodatkowe konfiguracje</span><span class="sxs-lookup"><span data-stu-id="5816f-193">Additional Configurations</span></span> |
| --- | --- |
| <span data-ttu-id="5816f-194">Windows</span><span class="sxs-lookup"><span data-stu-id="5816f-194">Windows</span></span>      | `%appdata%\NuGet\config\*.Config` |
| <span data-ttu-id="5816f-195">System Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="5816f-195">Mac/Linux</span></span>    | <span data-ttu-id="5816f-196">`~/.config/NuGet/config/*.config` lub `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="5816f-196">`~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> |

## <a name="nuget-defaults-file"></a><span data-ttu-id="5816f-197">Plik domyślny NuGet</span><span class="sxs-lookup"><span data-stu-id="5816f-197">NuGet defaults file</span></span>

<span data-ttu-id="5816f-198">`NuGetDefaults.Config`Plik istnieje, aby określić źródła pakietów, z których pakiety są instalowane i aktualizowane, i kontrolować domyślny element docelowy dla pakietów publikowanych za pomocą programu `nuget push` .</span><span class="sxs-lookup"><span data-stu-id="5816f-198">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="5816f-199">Ze względu na to, że administratorzy mogą wygodnie (na przykład za pomocą zasady grupy) wdrażać spójne `NuGetDefaults.Config` pliki na maszynach deweloperskich i kompilacji, mogą oni upewnić się, że wszyscy w organizacji używają odpowiednich źródeł pakietów, a nie NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="5816f-199">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="5816f-200">`NuGetDefaults.Config`Plik nigdy nie powoduje usunięcia źródła pakietu z konfiguracji NuGet dewelopera.</span><span class="sxs-lookup"><span data-stu-id="5816f-200">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="5816f-201">Oznacza to, że deweloper już użył NuGet i w związku z tym ma zarejestrowane źródło pakietów nuget.org, nie zostanie usunięte po utworzeniu `NuGetDefaults.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="5816f-201">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="5816f-202">Ponadto żaden `NuGetDefaults.Config` inny mechanizm w pakiecie NuGet nie może uniemożliwiać dostępu do źródeł pakietów, takich jak NuGet.org. Jeśli organizacja chce zablokować taki dostęp, musi użyć innych środków, takich jak zapory, aby to zrobić.</span><span class="sxs-lookup"><span data-stu-id="5816f-202">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="5816f-203">Lokalizacja NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="5816f-203">NuGetDefaults.Config location</span></span>

<span data-ttu-id="5816f-204">W poniższej tabeli opisano, gdzie `NuGetDefaults.Config` należy przechowywać plik, w zależności od docelowego systemu operacyjnego:</span><span class="sxs-lookup"><span data-stu-id="5816f-204">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="5816f-205">Platforma systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="5816f-205">OS Platform</span></span>  | <span data-ttu-id="5816f-206">Lokalizacja NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="5816f-206">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="5816f-207">Windows</span><span class="sxs-lookup"><span data-stu-id="5816f-207">Windows</span></span>      | <span data-ttu-id="5816f-208">**Visual Studio 2017 lub NuGet 4. x +:**`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="5816f-208">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="5816f-209">**Program Visual Studio 2015 i wcześniejsze lub NuGet 3. x i wcześniejsze:**`%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="5816f-209">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="5816f-210">System Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="5816f-210">Mac/Linux</span></span>    | <span data-ttu-id="5816f-211">`$XDG_DATA_HOME` (zwykle `~/.local/share` lub `/usr/local/share` , w zależności od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="5816f-211">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="5816f-212">Ustawienia NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="5816f-212">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="5816f-213">`packageSources`: Ta kolekcja ma takie samo znaczenie jak `packageSources` w zwykłych plikach konfiguracji i określa domyślne źródła.</span><span class="sxs-lookup"><span data-stu-id="5816f-213">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="5816f-214">Przy instalowaniu lub aktualizowaniu pakietów w projektach przy użyciu formatu zarządzania narzędzia NuGet używa źródeł `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="5816f-214">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="5816f-215">W przypadku projektów korzystających z formatu PackageReference, pakiet NuGet najpierw używa lokalnych źródeł, a następnie źródeł w udziałach sieciowych, a następnie źródeł HTTP, niezależnie od kolejności w plikach konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5816f-215">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="5816f-216">NuGet zawsze ignoruje kolejność źródeł przy użyciu operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="5816f-216">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="5816f-217">`disabledPackageSources`: Ta kolekcja ma także takie samo znaczenie jak w `NuGet.Config` przypadku plików, gdzie każde z nich ma swoją nazwę i wartość true/false wskazującą, czy jest ona wyłączona.</span><span class="sxs-lookup"><span data-stu-id="5816f-217">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="5816f-218">Dzięki temu nazwa i adres URL źródła mogą pozostać w programie `packageSources` bez domyślnego włączenia.</span><span class="sxs-lookup"><span data-stu-id="5816f-218">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="5816f-219">Poszczególni deweloperzy mogą następnie ponownie włączyć źródło, ustawiając wartość źródła na false w innych `NuGet.Config` plikach bez konieczności ponownego znalezienia poprawnego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="5816f-219">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="5816f-220">Jest to również przydatne w przypadku deweloperów, którzy mają pełną listę wewnętrznych źródłowych adresów URL dla organizacji, jednocześnie domyślnie włączając tylko źródło poszczególnych zespołów.</span><span class="sxs-lookup"><span data-stu-id="5816f-220">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="5816f-221">`defaultPushSource`: określa domyślny element docelowy dla `nuget push` operacji, zastępując wbudowane domyślne wartości NuGet.org. Administratorzy mogą wdrożyć to ustawienie, aby zapobiec publikowaniu wewnętrznych pakietów nuget.org w sposób niezależny od sytuacji, gdy deweloperzy muszą używać `nuget push -Source` do publikowania w NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="5816f-221">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="5816f-222">Przykład NuGetDefaults.Config i aplikacji</span><span class="sxs-lookup"><span data-stu-id="5816f-222">Example NuGetDefaults.Config and application</span></span>

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
