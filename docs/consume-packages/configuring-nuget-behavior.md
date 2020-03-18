---
title: Typowe konfiguracje NuGet
description: Pliki NuGet. config kontrolują zachowanie programu NuGet zarówno globalnie, jak i dla każdego projektu i są modyfikowane za pomocą polecenia konfiguracji NuGet.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 89127203df0aa1eb24f36b8ec64c5bb4a4d59319
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428913"
---
# <a name="common-nuget-configurations"></a><span data-ttu-id="fece3-103">Typowe konfiguracje NuGet</span><span class="sxs-lookup"><span data-stu-id="fece3-103">Common NuGet configurations</span></span>

<span data-ttu-id="fece3-104">Zachowanie narzędzia NuGet jest zależne od ustawień skumulowanych w jednym lub wielu plikach `NuGet.Config` (XML), które mogą istnieć na poziomach na poziomie projektu, użytkownika i komputera.</span><span class="sxs-lookup"><span data-stu-id="fece3-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="fece3-105">Globalny plik `NuGetDefaults.Config` również służy do konfigurowania źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="fece3-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="fece3-106">Ustawienia dotyczą wszystkich poleceń wydawanych w interfejsie wiersza polecenia, konsoli Menedżera pakietów i interfejsu użytkownika Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="fece3-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="fece3-107">Lokalizacje i użycia plików konfiguracji</span><span class="sxs-lookup"><span data-stu-id="fece3-107">Config file locations and uses</span></span>

| <span data-ttu-id="fece3-108">Zakres</span><span class="sxs-lookup"><span data-stu-id="fece3-108">Scope</span></span> | <span data-ttu-id="fece3-109">Lokalizacja pliku NuGet. config</span><span class="sxs-lookup"><span data-stu-id="fece3-109">NuGet.Config file location</span></span> | <span data-ttu-id="fece3-110">Opis</span><span class="sxs-lookup"><span data-stu-id="fece3-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fece3-111">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="fece3-111">Solution</span></span> | <span data-ttu-id="fece3-112">Bieżący folder (folder rozwiązania) lub dowolny folder w katalogu głównym dysku.</span><span class="sxs-lookup"><span data-stu-id="fece3-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="fece3-113">W folderze rozwiązania ustawienia są stosowane do wszystkich projektów w podfolderach.</span><span class="sxs-lookup"><span data-stu-id="fece3-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="fece3-114">Należy pamiętać, że jeśli plik konfiguracyjny znajduje się w folderze projektu, nie ma wpływu na ten projekt.</span><span class="sxs-lookup"><span data-stu-id="fece3-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="fece3-115">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="fece3-115">User</span></span> | <span data-ttu-id="fece3-116">Windows: `%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="fece3-116">Windows: `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="fece3-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` lub `~/.nuget/NuGet/NuGet.Config` (w zależności od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="fece3-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> | <span data-ttu-id="fece3-118">Ustawienia dotyczą wszystkich operacji, ale są zastępowane przez dowolne ustawienia na poziomie projektu.</span><span class="sxs-lookup"><span data-stu-id="fece3-118">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="fece3-119">Computer</span><span class="sxs-lookup"><span data-stu-id="fece3-119">Computer</span></span> | <span data-ttu-id="fece3-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="fece3-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="fece3-121">Mac/Linux: `$XDG_DATA_HOME`.</span><span class="sxs-lookup"><span data-stu-id="fece3-121">Mac/Linux: `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="fece3-122">Jeśli `$XDG_DATA_HOME` ma wartość null lub jest pusty, będą używane `~/.local/share` lub `/usr/local/share` (różne w zależności od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="fece3-122">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="fece3-123">Ustawienia dotyczą wszystkich operacji na komputerze, ale są zastępowane przez dowolne ustawienia użytkownika lub poziomu projektu.</span><span class="sxs-lookup"><span data-stu-id="fece3-123">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="fece3-124">Uwagi dotyczące wcześniejszych wersji programu NuGet:</span><span class="sxs-lookup"><span data-stu-id="fece3-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="fece3-125">Pakiet NuGet 3,3 i wcześniejsze użycie folderu `.nuget` dla ustawień całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="fece3-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="fece3-126">Ten folder nie jest używany w programie NuGet 3.4 +.</span><span class="sxs-lookup"><span data-stu-id="fece3-126">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="fece3-127">W przypadku programu NuGet 2,6 do 3. x plik konfiguracyjny na poziomie komputera w systemie Windows został zlokalizowany w%ProgramData%\NuGet\Config [\\{IDE} [\\{Version} [\\{SKU}]]] \NuGet.Config, gdzie *{IDE}* może być *VisualStudio*, *{Version}* była wersją programu Visual Studio, taką jak *14,0*, i *{SKU}* to *społeczność*, *Pro*lub *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="fece3-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="fece3-128">Aby przeprowadzić migrację ustawień do programu NuGet 4.0 +, po prostu skopiuj plik konfiguracyjny do% ProgramFiles (x86)% \ NuGet\Config. W systemie Linux ta poprzednia lokalizacja została/etc/opt oraz na komputerach Mac,/Library/Application Support support.</span><span class="sxs-lookup"><span data-stu-id="fece3-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="fece3-129">Zmienianie ustawień konfiguracji</span><span class="sxs-lookup"><span data-stu-id="fece3-129">Changing config settings</span></span>

<span data-ttu-id="fece3-130">Plik `NuGet.Config` jest prostym plikiem tekstowym XML zawierającym pary klucz/wartość, zgodnie z opisem w temacie [Ustawienia konfiguracji programu NuGet](../reference/nuget-config-file.md) .</span><span class="sxs-lookup"><span data-stu-id="fece3-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="fece3-131">Ustawienia są zarządzane przy użyciu interfejsu wiersza [polecenia NuGet konfiguracji](../reference/cli-reference/cli-ref-config.md):</span><span class="sxs-lookup"><span data-stu-id="fece3-131">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="fece3-132">Domyślnie zmiany są wprowadzane w pliku konfiguracji na poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fece3-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="fece3-133">Aby zmienić ustawienia w innym pliku, użyj przełącznika `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="fece3-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="fece3-134">W tym przypadku pliki mogą używać dowolnych nazw plików.</span><span class="sxs-lookup"><span data-stu-id="fece3-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="fece3-135">Klucze zawsze uwzględniają wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="fece3-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="fece3-136">Aby zmienić ustawienia w pliku ustawień na poziomie komputera, wymagana jest podniesienie uprawnień.</span><span class="sxs-lookup"><span data-stu-id="fece3-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="fece3-137">Chociaż można modyfikować plik w dowolnym edytorze tekstu, pakiet NuGet (v 3.4.3 i nowsze) w trybie cichym ignoruje cały plik konfiguracyjny, jeśli zawiera źle sformułowany kod XML (niezgodne Tagi, nieprawidłowe znaki cudzysłowu itp.).</span><span class="sxs-lookup"><span data-stu-id="fece3-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="fece3-138">Dlatego zaleca się zarządzanie ustawieniami przy użyciu `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="fece3-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="fece3-139">Ustawianie wartości</span><span class="sxs-lookup"><span data-stu-id="fece3-139">Setting a value</span></span>

<span data-ttu-id="fece3-140">W systemie Windows:</span><span class="sxs-lookup"><span data-stu-id="fece3-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="fece3-141">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="fece3-141">Mac/Linux:</span></span>

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
> <span data-ttu-id="fece3-142">W programie NuGet 3,4 i nowszych można używać zmiennych środowiskowych w dowolnej wartości, jak w `repositoryPath=%PACKAGEHOME%` (Windows) i `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="fece3-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="fece3-143">Usuwanie wartości</span><span class="sxs-lookup"><span data-stu-id="fece3-143">Removing a value</span></span>

<span data-ttu-id="fece3-144">Aby usunąć wartość, określ klucz z pustą wartością.</span><span class="sxs-lookup"><span data-stu-id="fece3-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="fece3-145">Tworzenie nowego pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="fece3-145">Creating a new config file</span></span>

<span data-ttu-id="fece3-146">Skopiuj szablon poniżej do nowego pliku, a następnie użyj `nuget config -configFile <filename>`, aby ustawić wartości:</span><span class="sxs-lookup"><span data-stu-id="fece3-146">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="fece3-147">Jak są stosowane ustawienia</span><span class="sxs-lookup"><span data-stu-id="fece3-147">How settings are applied</span></span>

<span data-ttu-id="fece3-148">Wiele plików `NuGet.Config` umożliwia przechowywanie ustawień w różnych lokalizacjach, tak aby dotyczyły one jednego projektu, grupy projektów lub wszystkich projektów.</span><span class="sxs-lookup"><span data-stu-id="fece3-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="fece3-149">Te ustawienia są stosowane zbiorczo do każdej operacji NuGet wywołanej z wiersza polecenia lub z programu Visual Studio z ustawieniami, które istnieją "najbliżej" w projekcie lub bieżącym folderze, który ma pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="fece3-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="fece3-150">W programie NuGet są ładowane ustawienia z różnych plików konfiguracji w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="fece3-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="fece3-151">[Plik NuGetDefaults. config](#nuget-defaults-file), który zawiera ustawienia dotyczące tylko źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="fece3-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="fece3-152">Plik na poziomie komputera.</span><span class="sxs-lookup"><span data-stu-id="fece3-152">The computer-level file.</span></span>
1. <span data-ttu-id="fece3-153">Plik na poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="fece3-153">The user-level file.</span></span>
1. <span data-ttu-id="fece3-154">Plik określony przy użyciu `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="fece3-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="fece3-155">Pliki znajdujące się w każdym folderze w ścieżce z katalogu głównego dysku do bieżącego folderu (gdzie NuGet. exe jest wywoływany lub folder zawierający projekt programu Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="fece3-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="fece3-156">Na przykład jeśli polecenie jest wywoływane w c:\A\B\C, NuGet szuka i ładuje pliki konfiguracji w c:\, następnie c:\A, c:\A\B i finally c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="fece3-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="fece3-157">Ponieważ program NuGet odnajdzie ustawienia w tych plikach, są one stosowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fece3-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="fece3-158">W przypadku elementów jednego elementu NuGet zastępuje wszystkie poprzednio znalezione wartości dla tego samego klucza.</span><span class="sxs-lookup"><span data-stu-id="fece3-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="fece3-159">Oznacza to, że ustawienia, które są "najbliżej" w bieżącym folderze lub projekcie zastępują inne znalezione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="fece3-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="fece3-160">Na przykład ustawienie `defaultPushSource` w `NuGetDefaults.Config` jest zastępowane, jeśli istnieje w innym pliku konfiguracyjnym.</span><span class="sxs-lookup"><span data-stu-id="fece3-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="fece3-161">W przypadku elementów kolekcji (takich jak `<packageSources>`) pakiet NuGet łączy wartości ze wszystkich plików konfiguracji do jednej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="fece3-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="fece3-162">Gdy `<clear />` jest obecny dla danego węzła, pakiet NuGet ignoruje wcześniej zdefiniowane wartości konfiguracji dla tego węzła.</span><span class="sxs-lookup"><span data-stu-id="fece3-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="fece3-163">Przewodnik po ustawieniach</span><span class="sxs-lookup"><span data-stu-id="fece3-163">Settings walkthrough</span></span>

<span data-ttu-id="fece3-164">Załóżmy, że masz następującą strukturę folderów na dwóch oddzielnych dyskach:</span><span class="sxs-lookup"><span data-stu-id="fece3-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="fece3-165">Następnie masz cztery `NuGet.Config` pliki w następujących lokalizacjach o podanych zawartości.</span><span class="sxs-lookup"><span data-stu-id="fece3-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="fece3-166">(Plik na poziomie komputera nie jest uwzględniony w tym przykładzie, ale zachowuje się podobnie do pliku na poziomie użytkownika).</span><span class="sxs-lookup"><span data-stu-id="fece3-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="fece3-167">Plik A. plik na poziomie użytkownika (`%appdata%\NuGet\NuGet.Config` w systemie Windows `~/.config/NuGet/NuGet.Config` na komputerze Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="fece3-167">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="fece3-168">File B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="fece3-168">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="fece3-169">File C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="fece3-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="fece3-170">File D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="fece3-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="fece3-171">Następnie program NuGet ładuje i stosuje ustawienia w następujący sposób, w zależności od tego, gdzie jest wywoływany:</span><span class="sxs-lookup"><span data-stu-id="fece3-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="fece3-172">**Wywołane z disk_drive_1/users**: używany jest tylko repozytorium domyślne wymienione w pliku konfiguracji na poziomie użytkownika (A), ponieważ jest to jedyny plik znaleziony w disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="fece3-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="fece3-173">**Wywołane z disk_drive_2/lub disk_drive_/tmp**: najpierw załadowano plik poziomu użytkownika (A), a następnie pakiet NuGet przechodzi do katalogu głównego disk_drive_2 i odnajdzie plik (B).</span><span class="sxs-lookup"><span data-stu-id="fece3-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="fece3-174">Pakiet NuGet szuka również pliku konfiguracji w programie/tmp, ale go nie znaleziono.</span><span class="sxs-lookup"><span data-stu-id="fece3-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="fece3-175">W związku z tym używane jest domyślne repozytorium w nuget.org, przywracanie pakietu jest włączone, a pakiety zostaną rozwinięte w disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="fece3-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="fece3-176">**Wywołane z disk_drive_2/Project1 lub disk_drive_2/Project1/Source**: najpierw załadowano plik na poziomie użytkownika (A), a następnie program NuGet ładuje plik (B) z katalogu głównego disk_drive_2, a następnie plik (C).</span><span class="sxs-lookup"><span data-stu-id="fece3-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="fece3-177">Ustawienia w (C) przesłaniają te w (B) i (A), tak aby `repositoryPath`, w których instalowane są pakiety, są disk_drive_2/Project1/External/Packages zamiast *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="fece3-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="fece3-178">Ponadto, ponieważ (C) czyści `<packageSources>`, nuget.org nie jest już dostępne jako źródło opuszczające `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="fece3-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="fece3-179">**Wywołane z disk_drive_2/Project2 lub disk_drive_2/Project2/Source**: plik na poziomie użytkownika (A) jest ładowany po raz pierwszy, po którym następuje plik (B) i plik (D).</span><span class="sxs-lookup"><span data-stu-id="fece3-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="fece3-180">Ponieważ `packageSources` nie jest czyszczony, oba `nuget.org` i `https://MyPrivateRepo/DQ/nuget` są dostępne jako źródła.</span><span class="sxs-lookup"><span data-stu-id="fece3-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="fece3-181">Pakiety zostaną rozwinięte w disk_drive_2/tmp zgodnie z opisem w (B).</span><span class="sxs-lookup"><span data-stu-id="fece3-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="fece3-182">Plik domyślny NuGet</span><span class="sxs-lookup"><span data-stu-id="fece3-182">NuGet defaults file</span></span>

<span data-ttu-id="fece3-183">Plik `NuGetDefaults.Config` istnieje, aby określić źródła pakietów, z których pakiety są instalowane i aktualizowane, i kontrolować domyślny element docelowy dla pakietów publikowanych z `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="fece3-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="fece3-184">Ze względu na to, że administratorzy mogą wygodnie (na przykład za pomocą zasady grupy) wdrażać spójne `NuGetDefaults.Config` plików na maszynach deweloperskich i kompilacji, mogą oni upewnić się, że wszyscy w organizacji korzystają z odpowiednich źródeł pakietów, a nie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="fece3-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="fece3-185">Plik `NuGetDefaults.Config` nigdy nie powoduje usunięcia źródła pakietu z konfiguracji NuGet dewelopera.</span><span class="sxs-lookup"><span data-stu-id="fece3-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="fece3-186">Oznacza to, że deweloper już użył NuGet i w związku z tym ma zarejestrowane źródło pakietów nuget.org, nie zostanie usunięte po utworzeniu pliku `NuGetDefaults.Config`.</span><span class="sxs-lookup"><span data-stu-id="fece3-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="fece3-187">Ponadto żaden `NuGetDefaults.Config` ani inny mechanizm w pakiecie NuGet nie może uniemożliwiać dostępu do źródeł pakietów, takich jak nuget.org. Jeśli organizacja chce zablokować taki dostęp, musi użyć innych środków, takich jak zapory, aby to zrobić.</span><span class="sxs-lookup"><span data-stu-id="fece3-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="fece3-188">NuGetDefaults.Config location</span><span class="sxs-lookup"><span data-stu-id="fece3-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="fece3-189">W poniższej tabeli opisano, gdzie należy przechowywać plik `NuGetDefaults.Config`, w zależności od docelowego systemu operacyjnego:</span><span class="sxs-lookup"><span data-stu-id="fece3-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="fece3-190">Platforma systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="fece3-190">OS Platform</span></span>  | <span data-ttu-id="fece3-191">NuGetDefaults.Config Location</span><span class="sxs-lookup"><span data-stu-id="fece3-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="fece3-192">System Windows</span><span class="sxs-lookup"><span data-stu-id="fece3-192">Windows</span></span>      | <span data-ttu-id="fece3-193">**Visual Studio 2017 lub NuGet 4. x +:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="fece3-193">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="fece3-194">**Visual Studio 2015 i starsze lub NuGet 3. x i wcześniejsze:** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="fece3-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="fece3-195">System Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="fece3-195">Mac/Linux</span></span>    | <span data-ttu-id="fece3-196">`$XDG_DATA_HOME` (zazwyczaj `~/.local/share` lub `/usr/local/share`, w zależności od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="fece3-196">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="fece3-197">NuGetDefaults. config — ustawienia</span><span class="sxs-lookup"><span data-stu-id="fece3-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="fece3-198">`packageSources`: Ta kolekcja ma takie samo znaczenie jak `packageSources` w zwykłych plikach konfiguracji i określa źródła domyślne.</span><span class="sxs-lookup"><span data-stu-id="fece3-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="fece3-199">Program NuGet używa źródeł w celu instalowania lub aktualizowania pakietów w projektach przy użyciu `packages.config`ego formatu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="fece3-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="fece3-200">W przypadku projektów korzystających z formatu PackageReference, pakiet NuGet najpierw używa lokalnych źródeł, a następnie źródeł w udziałach sieciowych, a następnie źródeł HTTP, niezależnie od kolejności w plikach konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fece3-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="fece3-201">NuGet zawsze ignoruje kolejność źródeł przy użyciu operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="fece3-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="fece3-202">`disabledPackageSources`: Ta kolekcja ma także takie samo znaczenie jak w plikach `NuGet.Config`, gdzie każde z nich ma nazwę, a wartość true/false wskazuje, czy jest ona wyłączona.</span><span class="sxs-lookup"><span data-stu-id="fece3-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="fece3-203">Dzięki temu nazwa i adres URL źródła mogą pozostać w `packageSources` bez domyślnego włączenia.</span><span class="sxs-lookup"><span data-stu-id="fece3-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="fece3-204">Poszczególni deweloperzy mogą następnie ponownie włączyć źródło, ustawiając wartość źródła na false w innych plikach `NuGet.Config` bez konieczności ponownego znalezienia poprawnego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="fece3-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="fece3-205">Jest to również przydatne w przypadku deweloperów, którzy mają pełną listę wewnętrznych źródłowych adresów URL dla organizacji, jednocześnie domyślnie włączając tylko źródło poszczególnych zespołów.</span><span class="sxs-lookup"><span data-stu-id="fece3-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="fece3-206">`defaultPushSource`: określa domyślny element docelowy dla operacji `nuget push`, zastępując wbudowane domyślne wartości nuget.org. Administratorzy mogą wdrożyć to ustawienie, aby uniknąć przypadkowego publikowania wewnętrznych nuget.org przez deweloperów, ponieważ deweloperzy muszą używać `nuget push -Source` do publikowania w nuget.org.</span><span class="sxs-lookup"><span data-stu-id="fece3-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="fece3-207">Przykład NuGetDefaults. config i aplikacja</span><span class="sxs-lookup"><span data-stu-id="fece3-207">Example NuGetDefaults.Config and application</span></span>

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
