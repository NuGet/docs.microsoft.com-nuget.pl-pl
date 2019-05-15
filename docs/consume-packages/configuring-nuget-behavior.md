---
title: Konfigurowanie zachowania pakietu nuget
description: Pliki w pliku NuGet.Config Sterowanie zachowaniem NuGet, globalnie i na poszczególnych projektów, a są modyfikowane za pomocą polecenia konfiguracji nuget.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: db968189e892723c8fd080cb01a7222696c9d3f3
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610569"
---
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="9d9db-103">Konfigurowanie zachowania pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="9d9db-103">Configuring NuGet behavior</span></span>

<span data-ttu-id="9d9db-104">Zachowanie NuGet jest wymuszany przez ustawienia zebranych w jednej lub więcej `NuGet.Config` plików (XML), które może istnieć na poziomie projektu-, user- i całego komputera.</span><span class="sxs-lookup"><span data-stu-id="9d9db-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="9d9db-105">Globalna `NuGetDefaults.Config` plik konfiguruje również specjalnie źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="9d9db-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="9d9db-106">Ustawienia stosowane do wszystkich poleceń, które pojawiły się w interfejsu wiersza polecenia, konsola Menedżera pakietów i interfejs użytkownika Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="9d9db-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="9d9db-107">Lokalizacje plików konfiguracji i używa</span><span class="sxs-lookup"><span data-stu-id="9d9db-107">Config file locations and uses</span></span>

| <span data-ttu-id="9d9db-108">Scope</span><span class="sxs-lookup"><span data-stu-id="9d9db-108">Scope</span></span> | <span data-ttu-id="9d9db-109">Lokalizacja pliku NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="9d9db-109">NuGet.Config file location</span></span> | <span data-ttu-id="9d9db-110">Opis</span><span class="sxs-lookup"><span data-stu-id="9d9db-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9d9db-111">Projekt</span><span class="sxs-lookup"><span data-stu-id="9d9db-111">Project</span></span> | <span data-ttu-id="9d9db-112">Bieżący folder (zwane również folder projektu) lub dowolnego folderu do katalogu głównego dysku.</span><span class="sxs-lookup"><span data-stu-id="9d9db-112">Current folder (aka Project folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="9d9db-113">W folderze projektu ustawienia mają zastosowanie tylko do tego projektu.</span><span class="sxs-lookup"><span data-stu-id="9d9db-113">In a project folder, settings apply only to that project.</span></span> <span data-ttu-id="9d9db-114">W folderów nadrzędnych zawierających wiele projektów podfolderów ustawienia stosowane do wszystkich projektów w tych podfolderów.</span><span class="sxs-lookup"><span data-stu-id="9d9db-114">In parent folders that contain multiple projects subfolders, settings apply to all projects in those subfolders.</span></span> |
| <span data-ttu-id="9d9db-115">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="9d9db-115">User</span></span> | <span data-ttu-id="9d9db-116">Windows: `%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="9d9db-116">Windows: `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="9d9db-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` lub `~/.nuget/NuGet/NuGet.Config` (zależnie od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="9d9db-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> | <span data-ttu-id="9d9db-118">Ustawienia stosowane do wszystkich operacji, ale są zastępowane przez wszystkie ustawienia na poziomie projektu.</span><span class="sxs-lookup"><span data-stu-id="9d9db-118">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="9d9db-119">Komputer</span><span class="sxs-lookup"><span data-stu-id="9d9db-119">Computer</span></span> | <span data-ttu-id="9d9db-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="9d9db-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="9d9db-121">Mac/Linux: `$XDG_DATA_HOME`.</span><span class="sxs-lookup"><span data-stu-id="9d9db-121">Mac/Linux: `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="9d9db-122">Jeśli `$XDG_DATA_HOME` ma wartość null lub jest pusta, `~/.local/share` lub `/usr/local/share` będzie używany (zależnie od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="9d9db-122">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="9d9db-123">Ustawienia stosowane do wszystkich operacji wykonywanych na komputerze, ale są zastępowane przez ustawienia na poziomie użytkownika lub projektu.</span><span class="sxs-lookup"><span data-stu-id="9d9db-123">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="9d9db-124">Uwagi dla wcześniejszych wersji programu NuGet:</span><span class="sxs-lookup"><span data-stu-id="9d9db-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="9d9db-125">NuGet 3.3 i wcześniej używany `.nuget` folder ustawienia dla całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9d9db-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="9d9db-126">Ten plik nie jest używany w programie NuGet 3.4 +.</span><span class="sxs-lookup"><span data-stu-id="9d9db-126">This file is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="9d9db-127">Dla 2.6 NuGet do 3.x, pliku konfiguracji na poziomie komputera, na Windows znajdują się w lokalizacji % ProgramData%\NuGet\Config [\\{IDE} [\\{Version} [\\{SKU}]]]\NuGet.Config, gdzie *{IDE}* może być  *Visual Studio*, *{Version}* został wersji programu Visual Studio, takie jak *14.0*, i *{jednostki SKU}* jest *społeczności*, *Pro*, lub *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="9d9db-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="9d9db-128">Aby przeprowadzić migrację ustawień do narzędzia NuGet 4.0 +, po prostu skopiować pliku konfiguracji do % ProgramFiles(x86) % \NuGet\Config. W systemie Linux ta lokalizacja poprzedniej została /etc/opt, a na komputerze Mac, Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="9d9db-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="9d9db-129">Zmienianie ustawień konfiguracji</span><span class="sxs-lookup"><span data-stu-id="9d9db-129">Changing config settings</span></span>

<span data-ttu-id="9d9db-130">A `NuGet.Config` plik jest prosty plik tekstowy XML zawierający pary klucz/wartość, zgodnie z opisem w [ustawienia konfiguracji NuGet](../reference/nuget-config-file.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="9d9db-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="9d9db-131">Ustawienia są zarządzane przy użyciu interfejsu wiersza polecenia NuGet [polecenia config](../tools/cli-ref-config.md):</span><span class="sxs-lookup"><span data-stu-id="9d9db-131">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="9d9db-132">Domyślnie zmiany są wprowadzane do pliku konfiguracji na poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9d9db-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="9d9db-133">Aby zmienić ustawienia w innym pliku, należy użyć `-configFile` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="9d9db-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="9d9db-134">W tym przypadku plików można użyć dowolnej nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="9d9db-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="9d9db-135">Klucze są zawsze z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="9d9db-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="9d9db-136">Podniesienie uprawnień jest wymagane do zmiany ustawień w pliku ustawień na poziomie komputera.</span><span class="sxs-lookup"><span data-stu-id="9d9db-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="9d9db-137">Mimo że można zmodyfikować plik w dowolnym edytorze tekstów NuGet (v3.4.3 i nowszych) dyskretnie ignoruje plik całą konfigurację, jeśli zawiera on nieprawidłowo sformułowany kod XML (niedopasowane tagi, nieprawidłowe znaki cudzysłowu, itp.).</span><span class="sxs-lookup"><span data-stu-id="9d9db-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="9d9db-138">Dlatego zaleca się zarządzanie ustawienie przy użyciu `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="9d9db-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="9d9db-139">Ustawienie wartości</span><span class="sxs-lookup"><span data-stu-id="9d9db-139">Setting a value</span></span>

<span data-ttu-id="9d9db-140">W systemie Windows:</span><span class="sxs-lookup"><span data-stu-id="9d9db-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="9d9db-141">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="9d9db-141">Mac/Linux:</span></span>

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
> <span data-ttu-id="9d9db-142">W programie NuGet 3.4 i nowszych można użyć zmiennych środowiskowych w dowolne wartości, podobnie jak w `repositoryPath=%PACKAGEHOME%` (Windows) i `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="9d9db-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="9d9db-143">Usuwanie wartości</span><span class="sxs-lookup"><span data-stu-id="9d9db-143">Removing a value</span></span>

<span data-ttu-id="9d9db-144">Aby usunąć wartość, należy określić klucz o wartości pustej.</span><span class="sxs-lookup"><span data-stu-id="9d9db-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="9d9db-145">Tworzenie nowego pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="9d9db-145">Creating a new config file</span></span>

<span data-ttu-id="9d9db-146">Skopiuj szablon poniżej do nowego pliku, a następnie użyj `nuget config -configFile <filename>` do ustawiania wartości:</span><span class="sxs-lookup"><span data-stu-id="9d9db-146">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="9d9db-147">Jak są stosowane ustawienia</span><span class="sxs-lookup"><span data-stu-id="9d9db-147">How settings are applied</span></span>

<span data-ttu-id="9d9db-148">Wiele `NuGet.Config` pliki umożliwiają przechowywanie ustawień w różnych lokalizacjach, tak aby odnoszą się do pojedynczego projektu, grupy projektów lub wszystkich projektów.</span><span class="sxs-lookup"><span data-stu-id="9d9db-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="9d9db-149">Zbiorczo te ustawienia mają zastosowanie do dowolnej operacji NuGet wywoływane z poziomu wiersza polecenia lub z programu Visual Studio przy użyciu ustawień, które istnieją "najbliższy" do projektu lub w bieżącym folderze, biorąc, pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="9d9db-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="9d9db-150">W szczególności NuGet ładuje ustawienia z plików konfiguracji różnych w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="9d9db-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="9d9db-151">[Pliku NuGetDefaults.Config](#nuget-defaults-file), który zawiera ustawienia dotyczące tylko źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="9d9db-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="9d9db-152">Plik poziomie komputera.</span><span class="sxs-lookup"><span data-stu-id="9d9db-152">The computer-level file.</span></span>
1. <span data-ttu-id="9d9db-153">Plik poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9d9db-153">The user-level file.</span></span>
1. <span data-ttu-id="9d9db-154">Pliku określonego przez `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="9d9db-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="9d9db-155">Pliki znajdujące się w każdy folder w ścieżce w katalogu głównym dysku do bieżącego folderu (przywołane nuget.exe lub folder zawierający projekt programu Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="9d9db-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="9d9db-156">Na przykład, jeśli polecenie zostanie wywołana w c:\A\B\C, NuGet wyszukuje i ładuje pliki konfiguracji w c:\, następnie c:\A, a następnie c:\A\B, a na końcu c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="9d9db-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="9d9db-157">Jak NuGet umożliwia znalezienie ustawień w tych plikach, są one stosowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9d9db-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="9d9db-158">Dla elementów pojedynczą pozycją NuGet zastąpić dowolną z wcześniej znaleźć wartość dla tego samego klucza.</span><span class="sxs-lookup"><span data-stu-id="9d9db-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="9d9db-159">Oznacza to, ustawienia, które są "najbliżej" bieżącego folderu lub projektu zastępują wszystkie inne pola znaleziono wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9d9db-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="9d9db-160">Na przykład `defaultPushSource` ustawienie w `NuGetDefaults.Config` jest zastępowany, jeśli istnieje w innym pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9d9db-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="9d9db-161">Kolekcja elementów (takich jak `<packageSources>`), NuGet łączy wartości z wszystkich plików konfiguracji w jednej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="9d9db-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="9d9db-162">Gdy `<clear />` jest obecny dla danego węzła NuGet ignoruje wcześniej określonych wartości konfiguracji dla tego węzła.</span><span class="sxs-lookup"><span data-stu-id="9d9db-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="9d9db-163">Przewodnik ustawienia</span><span class="sxs-lookup"><span data-stu-id="9d9db-163">Settings walkthrough</span></span>

<span data-ttu-id="9d9db-164">Załóżmy, że mają następującą strukturę folderów na dwa oddzielne dyski:</span><span class="sxs-lookup"><span data-stu-id="9d9db-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="9d9db-165">Następnie możesz wybrać cztery `NuGet.Config` pliki w następujących lokalizacjach za pomocą danej zawartości.</span><span class="sxs-lookup"><span data-stu-id="9d9db-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="9d9db-166">(Plik poziomie komputera nie jest uwzględniony w tym przykładzie, ale czy działają w podobny sposób do pliku poziom użytkownika).</span><span class="sxs-lookup"><span data-stu-id="9d9db-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="9d9db-167">Poziom użytkownika A. plik (`%appdata%\NuGet\NuGet.Config` na Windows, `~/.config/NuGet/NuGet.Config` w systemie Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="9d9db-167">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="9d9db-168">File B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="9d9db-168">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="9d9db-169">File C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="9d9db-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="9d9db-170">File D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="9d9db-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="9d9db-171">NuGet, a następnie ładuje i stosuje ustawienia w następujący sposób, w zależności od tego, gdzie jest wywoływana:</span><span class="sxs-lookup"><span data-stu-id="9d9db-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="9d9db-172">**Wywoływane z disk_drive_1/użytkowników**: Jest używana tylko w repozytorium domyślne, które są wymienione w pliku konfiguracji na poziomie użytkownika (A), ponieważ jest to jedyny plik w disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="9d9db-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="9d9db-173">**Wywoływane z disk_drive_2 / lub disk_drive_/tmp**: Plik poziom użytkownika (A) jest załadowany po raz pierwszy, a następnie NuGet prowadzi do katalogu głównego disk_drive_2 i znajduje się plik (B).</span><span class="sxs-lookup"><span data-stu-id="9d9db-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="9d9db-174">NuGet także szuka pliku konfiguracji w folderze/TMP, ale nie znaleźć partnera.</span><span class="sxs-lookup"><span data-stu-id="9d9db-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="9d9db-175">W rezultacie jest używany domyślny repozytorium w witrynie nuget.org, przywracania pakietów jest włączone i pakietów, Pobierz rozwinięty w disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="9d9db-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="9d9db-176">**Wywołane z disk_drive_2/projektu Project1 lub disk_drive_2/projektu Project1/źródło**: Poziom użytkownika (A) jest on ładowany najpierw, a następnie NuGet ładowania pliku (B) z katalogu głównego disk_drive_2, następuje plików (C).</span><span class="sxs-lookup"><span data-stu-id="9d9db-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="9d9db-177">Ustawienia w (C) zastępują (B) i (A), więc `repositoryPath` gdzie zainstalowania pakietów jest disk_drive_2/projektu Project1/zewnętrzne/pakietów zamiast *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="9d9db-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="9d9db-178">Ponadto ponieważ (C) Czyści `<packageSources>`, nuget.org nie jest już dostępna jako źródło, pozostawiając tylko `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="9d9db-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="9d9db-179">**Wywołane z disk_drive_2/Project2 lub disk_drive_2/Project2/źródło**: Plik poziom użytkownika (A) jest ładowany, najpierw następuje plik (B) i plik (D).</span><span class="sxs-lookup"><span data-stu-id="9d9db-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="9d9db-180">Ponieważ `packageSources` nie jest czyszczony, zarówno `nuget.org` i `https://MyPrivateRepo/DQ/nuget` są dostępne jako źródła.</span><span class="sxs-lookup"><span data-stu-id="9d9db-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="9d9db-181">Pakiety pobrać rozwinięty w disk_drive_2/tmp, jak to określono w (B).</span><span class="sxs-lookup"><span data-stu-id="9d9db-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="9d9db-182">Plik ustawień domyślnych NuGet</span><span class="sxs-lookup"><span data-stu-id="9d9db-182">NuGet defaults file</span></span>

<span data-ttu-id="9d9db-183">`NuGetDefaults.Config` Plik istnieje, aby określić źródła pakietów, z których pakietów są zainstalowane i aktualizowane oraz do sterowania to domyślny cel dla publikowania pakietów z `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="9d9db-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="9d9db-184">Ponieważ administratorzy, mogą wygodnie (na przykład przy użyciu zasad grupy) wdrożyć spójne `NuGetDefaults.Config` plików dla deweloperów i kompilacji do zapewnienia czy wszyscy użytkownicy w organizacji korzystają źródeł poprawny pakiet, a nie adres nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9d9db-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="9d9db-185">`NuGetDefaults.Config` Plik nigdy nie powoduje źródło pakietu, które można usunąć z konfiguracji NuGet dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="9d9db-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="9d9db-186">Oznacza to, że jeśli deweloper, który już użył NuGet i dlatego ma źródło pakietów nuget.org zarejestrowany, go nie zostaną usunięte po utworzeniu `NuGetDefaults.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="9d9db-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="9d9db-187">Ponadto, żaden `NuGetDefaults.Config` ani jakiegokolwiek innego mechanizmu nuget może uniemożliwić dostęp do źródła pakietu, np. nuget.org. Jeśli organizacja chce zablokować takiego dostępu, on używać innych metod, takich jak zapory, aby to zrobić.</span><span class="sxs-lookup"><span data-stu-id="9d9db-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="9d9db-188">NuGetDefaults.Config location</span><span class="sxs-lookup"><span data-stu-id="9d9db-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="9d9db-189">W poniższej tabeli opisano gdzie `NuGetDefaults.Config` ma być przechowywany plik zależnie od docelowego systemu operacyjnego:</span><span class="sxs-lookup"><span data-stu-id="9d9db-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="9d9db-190">Platforma systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="9d9db-190">OS Platform</span></span>  | <span data-ttu-id="9d9db-191">NuGetDefaults.Config Location</span><span class="sxs-lookup"><span data-stu-id="9d9db-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="9d9db-192">Windows</span><span class="sxs-lookup"><span data-stu-id="9d9db-192">Windows</span></span>      | <span data-ttu-id="9d9db-193">**Visual Studio 2017 lub NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="9d9db-193">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="9d9db-194">**Visual Studio 2015 i starsze lub NuGet 3.x i starszych wersji:** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="9d9db-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="9d9db-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="9d9db-195">Mac/Linux</span></span>    | <span data-ttu-id="9d9db-196">`$XDG_DATA_HOME` (zazwyczaj `~/.local/share` lub `/usr/local/share`, w zależności od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="9d9db-196">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="9d9db-197">Ustawienia NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="9d9db-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="9d9db-198">`packageSources`: Ta kolekcja ma takie samo znaczenie jak `packageSources` w zwykłych konfiguracji, pliki i określa źródeł domyślne.</span><span class="sxs-lookup"><span data-stu-id="9d9db-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="9d9db-199">NuGet używa źródła w kolejności podczas instalowania lub aktualizowania pakietów w projektach przy użyciu `packages.config` format zarządzania.</span><span class="sxs-lookup"><span data-stu-id="9d9db-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="9d9db-200">W przypadku projektów przy użyciu formatu PackageReference NuGet najpierw używa lokalnego źródła, a następnie źródeł na udziały sieciowe, a następnie źródła HTTP, niezależnie od kolejności, w plikach konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9d9db-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="9d9db-201">NuGet są zawsze ignorowane kolejność źródeł za pomocą operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="9d9db-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="9d9db-202">`disabledPackageSources`: Ta kolekcja również ma takie samo znaczenie jak w `NuGet.Config` plików, w którym każdego dotyczy źródła znajduje się przez nazwę i wartość PRAWDA/FAŁSZ wskazującą czy jest ono wyłączone.</span><span class="sxs-lookup"><span data-stu-id="9d9db-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="9d9db-203">Dzięki temu nazwa źródła i adres URL, aby pozostać w `packageSources` bez konieczności ona domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="9d9db-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="9d9db-204">Każdy deweloper następnie można ponownie włączyć źródła, ustawiając wartość źródła na wartość false w innych `NuGet.Config` plików bez konieczności jego ponowne znalezienie prawidłowego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="9d9db-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="9d9db-205">Jest to również przydatne do dostarczania deweloperom pełną listę wewnętrzny źródłowy adres URL dla organizacji, pozwalając tylko poszczególne zespoły źródło domyślnie.</span><span class="sxs-lookup"><span data-stu-id="9d9db-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="9d9db-206">`defaultPushSource`: Określa to domyślny cel dla `nuget push` operacji, zastąpienie wbudowanej domyślnej nuget.org. Administratorzy mogą wdrażać to ustawienie, aby uniknąć publikowania wewnętrznego pakietów nuget.org publicznych przypadkowo, jak deweloperzy w szczególności należy użyć `nuget push -Source` do publikowania w witrynie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9d9db-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="9d9db-207">Przykład NuGetDefaults.Config i aplikacji</span><span class="sxs-lookup"><span data-stu-id="9d9db-207">Example NuGetDefaults.Config and application</span></span>

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
