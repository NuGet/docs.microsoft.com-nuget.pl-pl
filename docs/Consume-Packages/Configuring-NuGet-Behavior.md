---
title: Konfigurowanie zachowania NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c1e34826-d07d-4609-a0fd-123459ae89c5
description: "Pliki NuGet.Config kontrolowania zachowania NuGet, globalnie i na podstawie na projekt i są modyfikowane za pomocą polecenia konfiguracyjnego nuget."
keywords: "Pliki konfiguracji programu NuGet, NuGet ustawienia zachowania NuGet, konfigurowanie ustawień NuGet, Nuget.Config, NuGetDefaults.Config, wartości domyślne"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9269180241a880d3b796b79a13dbcd45627d74d7
ms.sourcegitcommit: 9ac1fa23a4a8ce098692de93328b1db4136fe3d2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/22/2018
---
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="16373-104">Konfigurowanie zachowania NuGet</span><span class="sxs-lookup"><span data-stu-id="16373-104">Configuring NuGet behavior</span></span>

<span data-ttu-id="16373-105">Zachowanie NuGet jest wymuszany przez wszystkich ustawień w co najmniej jednej `NuGet.Config` plików (XML), może istnieć projektu, użytkownika i komputera poziomów.</span><span class="sxs-lookup"><span data-stu-id="16373-105">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="16373-106">Globalny `NuGetDefaults.Config` pliku (2.7 +) konfiguruje również specjalnie źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="16373-106">A global `NuGetDefaults.Config` file (2.7+) also specifically configures package sources.</span></span> <span data-ttu-id="16373-107">Ustawienia stosowane do wszystkich poleceń wykonania interfejsu wiersza polecenia, w konsoli Menedżera pakietów i interfejsu użytkownika Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="16373-107">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

<span data-ttu-id="16373-108">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="16373-108">In this topic:</span></span>

- [<span data-ttu-id="16373-109">Lokalizacje pliku NuGet.Config i używa</span><span class="sxs-lookup"><span data-stu-id="16373-109">NuGet.Config file locations and uses</span></span>](#config-file-locations-and-uses)
- [<span data-ttu-id="16373-110">Zmiana ustawień</span><span class="sxs-lookup"><span data-stu-id="16373-110">Changing settings</span></span>](#changing-config-settings)
- [<span data-ttu-id="16373-111">Jak są stosowane ustawienia</span><span class="sxs-lookup"><span data-stu-id="16373-111">How settings are applied</span></span>](#how-settings-are-applied)
- [<span data-ttu-id="16373-112">NuGetDefaults.Config file</span><span class="sxs-lookup"><span data-stu-id="16373-112">NuGetDefaults.Config file</span></span>](#nuget-defaults-file)

## <a name="nugetconfig-file-locations-and-uses"></a><span data-ttu-id="16373-113">Lokalizacje pliku NuGet.Config i używa</span><span class="sxs-lookup"><span data-stu-id="16373-113">NuGet.Config file locations and uses</span></span>

| <span data-ttu-id="16373-114">Zakres</span><span class="sxs-lookup"><span data-stu-id="16373-114">Scope</span></span> | <span data-ttu-id="16373-115">Lokalizacja pliku NuGet.Config.</span><span class="sxs-lookup"><span data-stu-id="16373-115">NuGet.Config file location</span></span> | <span data-ttu-id="16373-116">Opis</span><span class="sxs-lookup"><span data-stu-id="16373-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16373-117">Projekt</span><span class="sxs-lookup"><span data-stu-id="16373-117">Project</span></span> | <span data-ttu-id="16373-118">Bieżący folder (alias folderu projektu) lub dowolnego folderu do katalogu głównego dysku.</span><span class="sxs-lookup"><span data-stu-id="16373-118">Current folder (aka Project folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="16373-119">W folderze projektu ustawienia mają zastosowanie tylko do tego projektu.</span><span class="sxs-lookup"><span data-stu-id="16373-119">In a project folder, settings apply only to that project.</span></span> <span data-ttu-id="16373-120">W folderów nadrzędnych zawierających wiele projektów podfolderów ustawienia mają zastosowanie do wszystkich projektów w tych podfolderach.</span><span class="sxs-lookup"><span data-stu-id="16373-120">In parent folders that contain multiple projects subfolders, settings apply to all projects in those subfolders.</span></span> |
| <span data-ttu-id="16373-121">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="16373-121">User</span></span> | <span data-ttu-id="16373-122">Windows: %APPDATA%\NuGet\NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="16373-122">Windows: %APPDATA%\NuGet\NuGet.Config</span></span><br/><span data-ttu-id="16373-123">Mac/Linux: ~/.nuget/NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="16373-123">Mac/Linux: ~/.nuget/NuGet.Config</span></span> | <span data-ttu-id="16373-124">Ustawienia stosowane do wszystkich operacji, ale są zastępowane przez wszystkie ustawienia na poziomie projektu.</span><span class="sxs-lookup"><span data-stu-id="16373-124">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="16373-125">Komputer</span><span class="sxs-lookup"><span data-stu-id="16373-125">Computer</span></span> | <span data-ttu-id="16373-126">Windows: %ProgramFiles(x86)%\NuGet\Config</span><span class="sxs-lookup"><span data-stu-id="16373-126">Windows: %ProgramFiles(x86)%\NuGet\Config</span></span><br/><span data-ttu-id="16373-127">System Mac/Linux: XDG_DATA_HOME $ (zazwyczaj ~/.local/share)</span><span class="sxs-lookup"><span data-stu-id="16373-127">Mac/Linux: $XDG_DATA_HOME (typically ~/.local/share)</span></span> | <span data-ttu-id="16373-128">Ustawienia stosowane do wszystkich operacji na komputerze, ale zostały zastąpione przez wszystkie ustawienia na poziomie użytkownika lub projektu.</span><span class="sxs-lookup"><span data-stu-id="16373-128">Settings apply to all operations on the computer, but are overriden by any user- or project-level settings.</span></span> |

<span data-ttu-id="16373-129">Uwagi dotyczące starszych wersji programu NuGet:</span><span class="sxs-lookup"><span data-stu-id="16373-129">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="16373-130">NuGet 3.3 i wcześniej używany `.nuget` folder ustawienia dotyczące całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="16373-130">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="16373-131">Ten plik nie jest używany w NuGet 3.4 +.</span><span class="sxs-lookup"><span data-stu-id="16373-131">This file not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="16373-132">Dla 2.6 NuGet do 3.x, pliku konfiguracji na poziomie komputera w systemie Windows znajduje się w lokalizacji % ProgramData%\NuGet\Config [\\{IDE} [\\{wersja} [\\{SKU}]]]\NuGet.Config, gdzie *{IDE}* może być  *Visual Studio*, *{wersja}* został wersji programu Visual Studio, takich jak *14.0*, i *{SKU}* jest *społeczności*, *Pro*, lub *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="16373-132">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="16373-133">Aby przeprowadzić migrację ustawień do NuGet 4.0 +, po prostu skopiuj plik konfiguracji do % ProgramFiles(x86) % \NuGet\Config. W systemie Linux, to poprzedniej lokalizacji został /etc/opt, a dla komputerów Mac, Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="16373-133">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="16373-134">Zmiana ustawień konfiguracji</span><span class="sxs-lookup"><span data-stu-id="16373-134">Changing config settings</span></span>

<span data-ttu-id="16373-135">A `NuGet.Config` plik jest prosty plik tekstowy XML zawierający pary klucz wartość, zgodnie z opisem w [ustawienia konfiguracji NuGet](../Schema/nuget-config-file.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="16373-135">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../Schema/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="16373-136">Ustawienia są zarządzane przy użyciu interfejsu wiersza polecenia NuGet [polecenia konfiguracyjnego](../tools/cli-ref-config.md):</span><span class="sxs-lookup"><span data-stu-id="16373-136">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="16373-137">Domyślnie zmiany zostały wprowadzone do pliku konfiguracji na poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="16373-137">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="16373-138">Aby zmienić ustawienia w innym pliku, należy użyć `-configFile` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="16373-138">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="16373-139">W takim przypadku pliki można użyć nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="16373-139">In this case files can use any filename.</span></span>
- <span data-ttu-id="16373-140">Klucze są zawsze z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="16373-140">Keys are always case sensitive.</span></span>
- <span data-ttu-id="16373-141">Podniesienie uprawnień jest wymagane do zmiany ustawień w pliku ustawień na poziomie komputera.</span><span class="sxs-lookup"><span data-stu-id="16373-141">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="16373-142">Mimo że można zmodyfikować plik w edytorze tekstu, NuGet (v3.4.3 i nowsze) dyskretnie ignoruje całą konfigurację pliku, jeśli zawiera on nieprawidłowo sformułowany kod XML (niedopasowane tagi, nieprawidłowe znaki cudzysłowu, itp.).</span><span class="sxs-lookup"><span data-stu-id="16373-142">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="16373-143">Dlatego zaleca się zarządzanie ustawienie przy użyciu `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="16373-143">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="16373-144">Ustawienie wartości</span><span class="sxs-lookup"><span data-stu-id="16373-144">Setting a value</span></span>

<span data-ttu-id="16373-145">System Windows:</span><span class="sxs-lookup"><span data-stu-id="16373-145">Windows:</span></span>

```
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
```

<span data-ttu-id="16373-146">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="16373-146">Mac/Linux:</span></span>

```
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> <span data-ttu-id="16373-147">W NuGet 3.4 lub nowszym można używać zmiennych środowiskowych w żadnej wartości, podobnie jak w `repositoryPath=%PACKAGEHOME%` (system Windows) i `repositoryPath=%PACKAGEHOME` (system Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="16373-147">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="16373-148">Usuwanie wartości</span><span class="sxs-lookup"><span data-stu-id="16373-148">Removing a value</span></span>

<span data-ttu-id="16373-149">Aby usunąć wartość, należy określić klucz o wartości pustej.</span><span class="sxs-lookup"><span data-stu-id="16373-149">To remove a value, specify a key with an empty value.</span></span>

```
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="16373-150">Tworzenie nowego pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="16373-150">Creating a new config file</span></span>

<span data-ttu-id="16373-151">Kopiowanie szablonu poniżej do nowego pliku, a następnie użyć `nuget config --configFile <filename>` można ustawić wartości:</span><span class="sxs-lookup"><span data-stu-id="16373-151">Copy the template below into the new file and then use `nuget config --configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

<br/>

## <a name="how-settings-are-applied"></a><span data-ttu-id="16373-152">Jak są stosowane ustawienia</span><span class="sxs-lookup"><span data-stu-id="16373-152">How settings are applied</span></span>

<span data-ttu-id="16373-153">Wiele `NuGet.Config` pliki umożliwiają przechowywanie ustawień w różnych lokalizacjach, tak aby odnoszą się do pojedynczego projektu, grupy projektów lub wszystkich projektów.</span><span class="sxs-lookup"><span data-stu-id="16373-153">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="16373-154">Te ustawienia dotyczą zbiorczo żadnej operacji NuGet wywołany z poziomu wiersza polecenia lub w programie Visual Studio z ustawień, które istnieje "najbliższy" do projektu lub bieżący folder biorąc pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="16373-154">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="16373-155">W szczególności NuGet ładuje ustawienia z plików różnych konfiguracji w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="16373-155">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="16373-156">[NuGetDefaults.Config pliku](#nuget-defaults-file), który zawiera ustawienia dotyczące tylko źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="16373-156">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="16373-157">Plik poziomie komputera.</span><span class="sxs-lookup"><span data-stu-id="16373-157">The computer-level file.</span></span>
1. <span data-ttu-id="16373-158">Plik na poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="16373-158">The user-level file.</span></span>
1. <span data-ttu-id="16373-159">Podany plik z `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="16373-159">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="16373-160">Pliki znajdujące się w folderze, co w ścieżce z katalogu głównego dysku do bieżącego folderu (przywołane nuget.exe lub folder zawierający projekt programu Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="16373-160">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="16373-161">Na przykład, jeśli polecenie jest wywoływana w c:\A\B\C, NuGet wyszukuje i ładuje pliki konfiguracji w c:\, następnie c:\A, a następnie c:\A\B, a na końcu c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="16373-161">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="16373-162">Jak NuGet znajdzie ustawień w tych plikach, są one stosowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="16373-162">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="16373-163">Dla elementów pojedynczego elementu NuGet zamienić wartości poprzednio znaleziono tego samego klucza.</span><span class="sxs-lookup"><span data-stu-id="16373-163">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="16373-164">Oznacza to, ustawienia, które znajdują się w bieżącym folderze lub projektu "najbliżej" zastąpienie innych znalezionych wcześniej.</span><span class="sxs-lookup"><span data-stu-id="16373-164">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="16373-165">Na przykład `defaultPushSource` w `NuGetDefaults.Config` zostanie zastąpione, jeśli istnieje on w innym pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="16373-165">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="16373-166">Kolekcja elementów (takich jak `<packageSources>`), NuGet łączy wartości z wszystkie pliki konfiguracji w jednej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="16373-166">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="16373-167">Gdy `<clear />` występuje w przypadku danego węzła NuGet ignoruje wartości konfiguracji wcześniej zdefiniowanego dla tego węzła.</span><span class="sxs-lookup"><span data-stu-id="16373-167">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="16373-168">Ustawienia wskazówki</span><span class="sxs-lookup"><span data-stu-id="16373-168">Settings walkthrough</span></span>

<span data-ttu-id="16373-169">Załóżmy, że masz następujące struktury folderów na dwóch oddzielnych dyskach:</span><span class="sxs-lookup"><span data-stu-id="16373-169">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="16373-170">Następnie możesz wybrać cztery `NuGet.Config` pliki w następujących lokalizacjach z danej zawartości.</span><span class="sxs-lookup"><span data-stu-id="16373-170">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="16373-171">(Plik poziomie komputera jest niedostępna w tym przykładzie, ale czy zachowują się podobnie do pliku na poziomie użytkownika).</span><span class="sxs-lookup"><span data-stu-id="16373-171">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="16373-172">A. użytkownika na poziomie pliku, (%APPDATA%\NuGet\NuGet.Config w systemie Windows, ~/.nuget/NuGet.Config na system Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="16373-172">File A. User-level file, (%APPDATA%\NuGet\NuGet.Config on Windows, ~/.nuget/NuGet.Config on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="16373-173">File B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="16373-173">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="16373-174">File C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="16373-174">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="16373-175">File D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="16373-175">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="16373-176">NuGet, a następnie ładuje i stosuje ustawienia w następujący sposób, w zależności od tego, gdzie jest wywoływany:</span><span class="sxs-lookup"><span data-stu-id="16373-176">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="16373-177">**Wywoływany z disk_drive_1/użytkownicy**: używane tylko repozytorium domyślne wymienione w pliku konfiguracji na poziomie użytkownika (A), ponieważ jest to jedyny plik znaleziono na disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="16373-177">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="16373-178">**Wywoływany z disk_drive_2 / lub disk_drive_/tmp**: najpierw załadować pliku na poziomie użytkownika (A), a następnie NuGet przechodzi do katalogu głównego disk_drive_2 i wyszukuje plik (B).</span><span class="sxs-lookup"><span data-stu-id="16373-178">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="16373-179">NuGet także szuka pliku konfiguracyjnego /tmp, ale brakuje jednego.</span><span class="sxs-lookup"><span data-stu-id="16373-179">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="16373-180">W związku z tym repozytorium domyślne na nuget.org jest używany, Przywracanie pakietu jest włączona i pakiety pobrać rozwinięty w disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="16373-180">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="16373-181">**Wywoływane z disk_drive_2/Project1 lub disk_drive_2/Project1/źródła**: najpierw załadować pliku na poziomie użytkownika (A), a następnie NuGet obciążeń pliku (B) z folderu głównego disk_drive_2, a następnie pliku (C).</span><span class="sxs-lookup"><span data-stu-id="16373-181">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="16373-182">Ustawienia w (C) zastępują (B) i (A), więc `repositoryPath` gdzie zainstalowane pakiety jest disk_drive_2/Project1/zewnętrznego/pakietów zamiast *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="16373-182">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="16373-183">Ponadto ponieważ czyści (C) `<packageSources>`, nuget.org nie jest już dostępna jako źródła, pozostawiając tylko `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="16373-183">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="16373-184">**Wywoływane z projekcie disk_drive_2/2 lub disk_drive_2/projekcie 2/źródła**: załadowaniu pliku na poziomie użytkownika (A), najpierw następuje pliku (B) i pliku (D).</span><span class="sxs-lookup"><span data-stu-id="16373-184">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="16373-185">Ponieważ `packageSources` jest nie wyczyszczony, zarówno `nuget.org` i `https://MyPrivateRepo/DQ/nuget` są dostępne jako źródła.</span><span class="sxs-lookup"><span data-stu-id="16373-185">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="16373-186">Pakiety pobrać rozwinięty w disk_drive_2/tmp, jak określono w (B).</span><span class="sxs-lookup"><span data-stu-id="16373-186">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="16373-187">Plik ustawień domyślnych NuGet</span><span class="sxs-lookup"><span data-stu-id="16373-187">NuGet defaults file</span></span>

<span data-ttu-id="16373-188">`NuGetDefaults.Config` Plik istnieje, aby określić źródła pakietów, z których są zainstalowane i zaktualizowane pakiety oraz do sterowania domyślnego celu publikowania pakietów z `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="16373-188">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="16373-189">Ponieważ administratorzy mogą łatwo (na przykład przy użyciu zasad grupy) wdrażanie spójne `NuGetDefaults.Config` deweloperów i plików maszyny kompilacji, mogą zapewnienie, że wszyscy użytkownicy w organizacji używa poprawny pakiet źródeł, a nie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="16373-189">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensuring that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="16373-190">`NuGetDefaults.Config` Pliku nigdy nie powoduje źródła pakietów były usuwane z Konfiguracja nuget projektu dewelopera.</span><span class="sxs-lookup"><span data-stu-id="16373-190">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="16373-191">Oznacza to, że jeśli projektanta został już użyty NuGet i w związku z tym ma w źródle pakietów nuget.org zarejestrowany, jego nie zostaną usunięte po utworzeniu `NuGetDefaults.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="16373-191">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="16373-192">Ponadto, ani `NuGetDefaults.Config` ani innych mechanizmu w NuGet może uniemożliwić dostęp do pakietu źródeł, takich jak nuget.org. Jeśli organizacja chce zablokować takiego dostępu, znacznie użyć innych środków, takich jak zapory w tym celu.</span><span class="sxs-lookup"><span data-stu-id="16373-192">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it much use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="16373-193">NuGetDefaults.Config location</span><span class="sxs-lookup"><span data-stu-id="16373-193">NuGetDefaults.Config location</span></span>

<span data-ttu-id="16373-194">System Windows: % ProgramFiles (x86) %\NuGet\Config (2.7 NuGet do NuGet 3.x: % PROGRAMDATA%\NuGet\NuGetDefaults.Config) system Mac/Linux: XDG_DATA_HOME $ (zazwyczaj ~/.local/share)</span><span class="sxs-lookup"><span data-stu-id="16373-194">Windows: %ProgramFiles(x86)%\NuGet\Config (NuGet 2.7 to NuGet 3.x: %PROGRAMDATA%\NuGet\NuGetDefaults.Config) Mac/Linux: $XDG_DATA_HOME (typically ~/.local/share)</span></span> 

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="16373-195">Ustawienia NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="16373-195">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="16373-196">`packageSources`: Ta kolekcja ma takie samo znaczenie jak `packageSources` w regularnych config pliki i określa źródeł domyślnego w ich preferowanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="16373-196">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources in their preferred order.</span></span> <span data-ttu-id="16373-197">Jeśli to ustawienie istnieje w `NuGetDefaults.Config`, a następnie NuGet nuget.org nie są używane jako źródło domyślnego pakietu.</span><span class="sxs-lookup"><span data-stu-id="16373-197">If this setting exists in `NuGetDefaults.Config`, then NuGet doesn't use nuget.org as a default package source.</span></span> <span data-ttu-id="16373-198">Administrator w związku z tym można upewnić się, wszyscy przy użyciu tego pliku jest praca z tych samych źródeł i pozwala uniknąć przy użyciu nuget.org w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="16373-198">An administrator can thus make sure that everyone using this file is working with the same sources and avoids using nuget.org if desired.</span></span>

- <span data-ttu-id="16373-199">`disabledPackageSources`: Ta kolekcja również ma takie samo znaczenie jak w `NuGet.Config` plików, gdy każdego dotyczy źródła znajduje się jego nazwa i wartość PRAWDA/FAŁSZ wskazującą czy jest ona wyłączona.</span><span class="sxs-lookup"><span data-stu-id="16373-199">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="16373-200">Dzięki temu nazwa źródła i adres URL ma pozostawać w `packageSources` bez konieczności ona domyślnie włączona.</span><span class="sxs-lookup"><span data-stu-id="16373-200">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="16373-201">Każdy deweloper może następnie ponownie włącz jej źródło przez ustawienie wartości false w innych wartość źródła `NuGet.Config` plików bez konieczności ponownie znaleźć poprawny adres URL.</span><span class="sxs-lookup"><span data-stu-id="16373-201">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="16373-202">To także dostarczyć deweloperom pełną listę wewnętrzny źródłowy adres URL dla organizacji, podczas włączania tylko źródła indywidualnych zespołu domyślnie.</span><span class="sxs-lookup"><span data-stu-id="16373-202">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="16373-203">`defaultPushSource`: Określa domyślnego celu `nuget push` operacje zastępowania wbudowanej domyślnej nuget.org. Administratorzy mogą wdrożyć to ustawienie, aby uniknąć publikowania pakietów wewnętrzny do publicznego nuget.org przypadkowo, jak deweloperzy w szczególności należy użyć `nuget push -Source` do publikowania nuget.org.</span><span class="sxs-lookup"><span data-stu-id="16373-203">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="16373-204">Przykład NuGetDefaults.Config i aplikacji</span><span class="sxs-lookup"><span data-stu-id="16373-204">Example NuGetDefaults.Config and application</span></span>

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
