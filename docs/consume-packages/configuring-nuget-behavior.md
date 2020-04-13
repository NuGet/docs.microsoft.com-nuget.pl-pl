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
# <a name="common-nuget-configurations"></a><span data-ttu-id="11f03-103">Typowe konfiguracje narzędzia NuGet</span><span class="sxs-lookup"><span data-stu-id="11f03-103">Common NuGet configurations</span></span>

<span data-ttu-id="11f03-104">Zachowanie NuGet jest napędzany przez skumulowane ustawienia `NuGet.Config` w jednym lub więcej plików (XML), które mogą istnieć na poziomie projektu, użytkownika i komputera.</span><span class="sxs-lookup"><span data-stu-id="11f03-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="11f03-105">Plik `NuGetDefaults.Config` globalny również specjalnie konfiguruje źródła pakietów.</span><span class="sxs-lookup"><span data-stu-id="11f03-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="11f03-106">Ustawienia dotyczą wszystkich poleceń wydanych w interfejsie wiersza polecenia, konsoli Menedżera pakietów i interfejsie użytkownika Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="11f03-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="11f03-107">Lokalizacje i zastosowania plików konfiguracyjne</span><span class="sxs-lookup"><span data-stu-id="11f03-107">Config file locations and uses</span></span>

| <span data-ttu-id="11f03-108">Zakres</span><span class="sxs-lookup"><span data-stu-id="11f03-108">Scope</span></span> | <span data-ttu-id="11f03-109">Lokalizacja pliku NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="11f03-109">NuGet.Config file location</span></span> | <span data-ttu-id="11f03-110">Opis</span><span class="sxs-lookup"><span data-stu-id="11f03-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="11f03-111">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="11f03-111">Solution</span></span> | <span data-ttu-id="11f03-112">Bieżący folder (aka folder Rozwiązanie) lub dowolny folder do katalogu głównego dysku.</span><span class="sxs-lookup"><span data-stu-id="11f03-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="11f03-113">W folderze rozwiązania ustawienia dotyczą wszystkich projektów w podfolderach.</span><span class="sxs-lookup"><span data-stu-id="11f03-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="11f03-114">Należy zauważyć, że jeśli plik konfiguracyjny jest umieszczony w folderze projektu, nie ma to wpływu na ten projekt.</span><span class="sxs-lookup"><span data-stu-id="11f03-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="11f03-115">Użytkownik</span><span class="sxs-lookup"><span data-stu-id="11f03-115">User</span></span> | <span data-ttu-id="11f03-116">Windows:`%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="11f03-116">Windows: `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="11f03-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` `~/.nuget/NuGet/NuGet.Config` lub (w zależności od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="11f03-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> | <span data-ttu-id="11f03-118">Ustawienia dotyczą wszystkich operacji, ale są zastępowane przez wszystkie ustawienia na poziomie projektu.</span><span class="sxs-lookup"><span data-stu-id="11f03-118">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="11f03-119">Computer (Komputer)</span><span class="sxs-lookup"><span data-stu-id="11f03-119">Computer</span></span> | <span data-ttu-id="11f03-120">Windows:`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="11f03-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="11f03-121">Mac/Linux: `$XDG_DATA_HOME`.</span><span class="sxs-lookup"><span data-stu-id="11f03-121">Mac/Linux: `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="11f03-122">Jeśli `$XDG_DATA_HOME` jest null `~/.local/share` lub `/usr/local/share` puste, lub będą używane (zależy od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="11f03-122">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="11f03-123">Ustawienia dotyczą wszystkich operacji na komputerze, ale są zastępowane przez ustawienia na poziomie użytkownika lub projektu.</span><span class="sxs-lookup"><span data-stu-id="11f03-123">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="11f03-124">Uwagi dotyczące wcześniejszych wersji programu NuGet:</span><span class="sxs-lookup"><span data-stu-id="11f03-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="11f03-125">NuGet 3.3 i `.nuget` wcześniej używane folder dla ustawień dla całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="11f03-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="11f03-126">Ten folder nie jest używany w nuget 3.4+.</span><span class="sxs-lookup"><span data-stu-id="11f03-126">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="11f03-127">W przypadku nugeta 2.6 do 3.x plik konfiguracyjny na poziomie komputera w systemie\\Windows znajdował\\się w\\%ProgramData%\NuGet\Config[ {IDE}[ {Version}[ {SKU}]]]\NuGet.Config, gdzie *{IDE}* może być *VisualStudio*, *{Version}* była wersją programu Visual Studio, taką jak *14.0,* a *{SKU}* jest *wspólnotą*, *Pro*lub *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="11f03-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="11f03-128">Aby przeprowadzić migrację ustawień do wersji NuGet 4.0+, wystarczy skopiować plik konfiguracyjny do pliku %ProgramFiles(x86)%\NuGet\Config. W systemie Linux ta poprzednia lokalizacja była /etc/opt, a na macu , /Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="11f03-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="11f03-129">Zmiana ustawień konfiguracji</span><span class="sxs-lookup"><span data-stu-id="11f03-129">Changing config settings</span></span>

<span data-ttu-id="11f03-130">Plik `NuGet.Config` jest prostym plikiem tekstowym XML zawierającym pary klucz/wartość, zgodnie z opisem w temacie [Ustawienia konfiguracji NuGet.](../reference/nuget-config-file.md)</span><span class="sxs-lookup"><span data-stu-id="11f03-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="11f03-131">Ustawieniami zarządzają za pomocą [polecenia konfiguracyjnego](../reference/cli-reference/cli-ref-config.md)NuGet CLI:</span><span class="sxs-lookup"><span data-stu-id="11f03-131">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="11f03-132">Domyślnie zmiany są wprowadzane do pliku konfiguracyjnego na poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="11f03-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="11f03-133">Aby zmienić ustawienia w innym `-configFile` pliku, użyj przełącznika.</span><span class="sxs-lookup"><span data-stu-id="11f03-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="11f03-134">W tym przypadku pliki mogą używać dowolnej nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="11f03-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="11f03-135">W klawiszach zawsze rozróżniana jest wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="11f03-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="11f03-136">Podniesienie uprawnień jest wymagane do zmiany ustawień w pliku ustawień na poziomie komputera.</span><span class="sxs-lookup"><span data-stu-id="11f03-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="11f03-137">Chociaż można zmodyfikować plik w dowolnym edytorze tekstu, NuGet (w wersji 3.4.3 lub nowszej) dyskretnie ignoruje cały plik konfiguracyjny, jeśli zawiera zniekształcony kod XML (niezgodne tagi, nieprawidłowe cudzysłowy itp.).</span><span class="sxs-lookup"><span data-stu-id="11f03-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="11f03-138">Dlatego lepiej jest zarządzać ustawieniem za `nuget config`pomocą .</span><span class="sxs-lookup"><span data-stu-id="11f03-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="11f03-139">Ustawianie wartości</span><span class="sxs-lookup"><span data-stu-id="11f03-139">Setting a value</span></span>

<span data-ttu-id="11f03-140">W systemie Windows:</span><span class="sxs-lookup"><span data-stu-id="11f03-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="11f03-141">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="11f03-141">Mac/Linux:</span></span>

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
> <span data-ttu-id="11f03-142">W NuGet 3.4 i nowszych można używać zmiennych środowiskowych w dowolnej wartości, jak w `repositoryPath=%PACKAGEHOME%` (Windows) i `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="11f03-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="11f03-143">Usuwanie wartości</span><span class="sxs-lookup"><span data-stu-id="11f03-143">Removing a value</span></span>

<span data-ttu-id="11f03-144">Aby usunąć wartość, należy określić klucz o pustej wartości.</span><span class="sxs-lookup"><span data-stu-id="11f03-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="11f03-145">Tworzenie nowego pliku konfiguracyjnego</span><span class="sxs-lookup"><span data-stu-id="11f03-145">Creating a new config file</span></span>

<span data-ttu-id="11f03-146">Skopiuj poniższy szablon `nuget config -configFile <filename>` do nowego pliku, a następnie użyj do ustawiania wartości:</span><span class="sxs-lookup"><span data-stu-id="11f03-146">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="11f03-147">Jak są stosowane ustawienia</span><span class="sxs-lookup"><span data-stu-id="11f03-147">How settings are applied</span></span>

<span data-ttu-id="11f03-148">Wiele `NuGet.Config` plików umożliwia przechowywanie ustawień w różnych lokalizacjach, dzięki czemu mają zastosowanie do jednego projektu, grupy projektów lub wszystkich projektów.</span><span class="sxs-lookup"><span data-stu-id="11f03-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="11f03-149">Te ustawienia zbiorczo dotyczą dowolnej operacji NuGet wywołanej z wiersza polecenia lub programu Visual Studio, z ustawieniami, które istnieją "najbliżej" projektu lub bieżącego folderu mającego pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="11f03-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="11f03-150">W szczególności NuGet ładuje ustawienia z różnych plików konfiguracyjnych w następującej kolejności:</span><span class="sxs-lookup"><span data-stu-id="11f03-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="11f03-151">[Plik NuGetDefaults.Config](#nuget-defaults-file), który zawiera ustawienia związane tylko ze źródłami pakietów.</span><span class="sxs-lookup"><span data-stu-id="11f03-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="11f03-152">Plik na poziomie komputera.</span><span class="sxs-lookup"><span data-stu-id="11f03-152">The computer-level file.</span></span>
1. <span data-ttu-id="11f03-153">Plik na poziomie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="11f03-153">The user-level file.</span></span>
1. <span data-ttu-id="11f03-154">Plik określony `-configFile`za pomocą pliku .</span><span class="sxs-lookup"><span data-stu-id="11f03-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="11f03-155">Pliki znalezione w każdym folderze w ścieżce z katalogu głównego dysku do bieżącego folderu (gdzie wywoływany jest plik nuget.exe lub folder zawierający projekt programu Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="11f03-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="11f03-156">Na przykład, jeśli polecenie jest wywoływane w c:\A\B\C, NuGet wyszukuje i ładuje pliki konfiguracyjne w c:\, następnie c:\A, następnie c:\A\B i na koniec c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="11f03-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="11f03-157">Jak NuGet znajdzie ustawienia w tych plikach, są one stosowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="11f03-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="11f03-158">W przypadku elementów jednoeliskowych NuGet zastąpił dowolną wcześniej znalezioną wartość dla tego samego klucza.</span><span class="sxs-lookup"><span data-stu-id="11f03-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="11f03-159">Oznacza to, że ustawienia, które są "najbliżej" do bieżącego folderu lub projektu zastąpić wszystkie inne znalezione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="11f03-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="11f03-160">Na przykład `defaultPushSource` ustawienie `NuGetDefaults.Config` w jest zastępowane, jeśli istnieje w innym pliku konfiguracyjnym.</span><span class="sxs-lookup"><span data-stu-id="11f03-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="11f03-161">Dla elementów kolekcji (takich jak `<packageSources>`), NuGet łączy wartości ze wszystkich plików konfiguracyjnych w jednej kolekcji.</span><span class="sxs-lookup"><span data-stu-id="11f03-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="11f03-162">Gdy `<clear />` jest obecny dla danego węzła, NuGet ignoruje wcześniej zdefiniowane wartości konfiguracji dla tego węzła.</span><span class="sxs-lookup"><span data-stu-id="11f03-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="11f03-163">Przewodnik po ustawieniach</span><span class="sxs-lookup"><span data-stu-id="11f03-163">Settings walkthrough</span></span>

<span data-ttu-id="11f03-164">Załóżmy, że masz następującą strukturę folderów na dwóch oddzielnych dyskach:</span><span class="sxs-lookup"><span data-stu-id="11f03-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="11f03-165">Następnie masz `NuGet.Config` cztery pliki w następujących lokalizacjach z danej zawartości.</span><span class="sxs-lookup"><span data-stu-id="11f03-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="11f03-166">(Plik na poziomie komputera nie jest uwzględniony w tym przykładzie, ale będzie zachowywać się podobnie do pliku na poziomie użytkownika).</span><span class="sxs-lookup"><span data-stu-id="11f03-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="11f03-167">Plik A. Plik na`%appdata%\NuGet\NuGet.Config` poziomie użytkownika `~/.config/NuGet/NuGet.Config` ( w systemie Windows, na Mac/Linux):</span><span class="sxs-lookup"><span data-stu-id="11f03-167">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="11f03-168">Plik B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="11f03-168">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="11f03-169">Plik C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="11f03-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="11f03-170">Plik D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="11f03-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="11f03-171">NuGet następnie ładuje i stosuje ustawienia w następujący sposób, w zależności od tego, gdzie jest wywoływany:</span><span class="sxs-lookup"><span data-stu-id="11f03-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="11f03-172">**Wywoływane od disk_drive_1/użytkowników:** Używane jest tylko domyślne repozytorium wymienione w pliku konfiguracyjnym na poziomie użytkownika (A), ponieważ jest to jedyny plik znaleziony na disk_drive_1.</span><span class="sxs-lookup"><span data-stu-id="11f03-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="11f03-173">**Wywoływane z disk_drive_2/ lub disk_drive_/tmp:** Najpierw jest ładowany plik na poziomie użytkownika (A), a następnie NuGet przechodzi do katalogu głównego disk_drive_2 i znajduje plik (B).</span><span class="sxs-lookup"><span data-stu-id="11f03-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="11f03-174">NuGet również wyszukuje plik konfiguracyjny w /tmp, ale nie znajduje.</span><span class="sxs-lookup"><span data-stu-id="11f03-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="11f03-175">W rezultacie używane jest domyślne repozytorium nuget.org, włączone jest przywracanie pakietu, a pakiety są rozszerzane w disk_drive_2/tmp.</span><span class="sxs-lookup"><span data-stu-id="11f03-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="11f03-176">**Wywoływany z disk_drive_2/Project1 lub disk_drive_2/Project1/Source**: Najpierw jest ładowany plik na poziomie użytkownika (A), a następnie plik NuGet loads (B) z katalogu głównego disk_drive_2, a następnie plik (C).</span><span class="sxs-lookup"><span data-stu-id="11f03-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="11f03-177">Ustawienia w (C) zastępują te w (B) `repositoryPath` i (A), więc miejsce, w którym pakiety są instalowane, jest disk_drive_2/Project1/External/Packages zamiast *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="11f03-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="11f03-178">Ponadto, ponieważ (C) `<packageSources>`czyści , nuget.org nie jest już `https://MyPrivateRepo/ES/nuget`dostępna jako źródło pozostawiając tylko .</span><span class="sxs-lookup"><span data-stu-id="11f03-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="11f03-179">**Wywoływany z disk_drive_2/Project2 lub disk_drive_2/Project2/Source**: Plik na poziomie użytkownika (A) jest ładowany najpierw po pliku (B) i pliku (D).</span><span class="sxs-lookup"><span data-stu-id="11f03-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="11f03-180">Ponieważ `packageSources` nie jest wyczyszczone, zarówno `nuget.org` i `https://MyPrivateRepo/DQ/nuget` są dostępne jako źródła.</span><span class="sxs-lookup"><span data-stu-id="11f03-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="11f03-181">Pakiety są rozszerzane w disk_drive_2/tmp, jak określono w (B).</span><span class="sxs-lookup"><span data-stu-id="11f03-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="11f03-182">Plik domyślny NuGet</span><span class="sxs-lookup"><span data-stu-id="11f03-182">NuGet defaults file</span></span>

<span data-ttu-id="11f03-183">Istnieje `NuGetDefaults.Config` plik, aby określić źródła pakietów, z których pakiety są instalowane i aktualizowane, oraz kontrolować domyślny cel publikowania pakietów za pomocą pliku `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="11f03-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="11f03-184">Ponieważ administratorzy mogą wygodnie (na przykład przy `NuGetDefaults.Config` użyciu zasad grupy) wdrażać spójne pliki na komputerach deweloperskich i kompilacji, mogą zapewnić, że wszyscy w organizacji używają odpowiednich źródeł pakietów, a nie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="11f03-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="11f03-185">Plik `NuGetDefaults.Config` nigdy nie powoduje, że źródło pakietu do usunięcia z konfiguracji NuGet dewelopera.</span><span class="sxs-lookup"><span data-stu-id="11f03-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="11f03-186">Oznacza to, że jeśli deweloper już używane NuGet i dlatego ma nuget.org źródło pakietu zarejestrowane, `NuGetDefaults.Config` nie zostanie usunięty po utworzeniu pliku.</span><span class="sxs-lookup"><span data-stu-id="11f03-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="11f03-187">Ponadto ani `NuGetDefaults.Config` żaden inny mechanizm w NuGet może uniemożliwić dostęp do źródeł pakietów, takich jak nuget.org. Jeśli organizacja chce zablokować taki dostęp, musi użyć innych środków, takich jak zapory, aby to zrobić.</span><span class="sxs-lookup"><span data-stu-id="11f03-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="11f03-188">Lokalizacja Pliku NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="11f03-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="11f03-189">W poniższej tabeli opisano, gdzie `NuGetDefaults.Config` plik powinien być przechowywany, w zależności od docelowego systemu operacyjnego:</span><span class="sxs-lookup"><span data-stu-id="11f03-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="11f03-190">Platforma systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="11f03-190">OS Platform</span></span>  | <span data-ttu-id="11f03-191">Lokalizacja pliku NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="11f03-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="11f03-192">Windows</span><span class="sxs-lookup"><span data-stu-id="11f03-192">Windows</span></span>      | <span data-ttu-id="11f03-193">**Visual Studio 2017 lub NuGet 4.x+:**`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="11f03-193">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="11f03-194">**Visual Studio 2015 i starsze lub NuGet 3.x i wcześniej:**`%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="11f03-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="11f03-195">System Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="11f03-195">Mac/Linux</span></span>    | <span data-ttu-id="11f03-196">`$XDG_DATA_HOME`(zazwyczaj `~/.local/share` lub `/usr/local/share`, w zależności od dystrybucji systemu operacyjnego)</span><span class="sxs-lookup"><span data-stu-id="11f03-196">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="11f03-197">Ustawienia pliku NuGetDefaults.Config</span><span class="sxs-lookup"><span data-stu-id="11f03-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="11f03-198">`packageSources`: ta kolekcja ma `packageSources` takie samo znaczenie jak w zwykłych plikach konfiguracyjnych i określa źródła domyślne.</span><span class="sxs-lookup"><span data-stu-id="11f03-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="11f03-199">NuGet używa źródeł w kolejności podczas instalowania lub aktualizowania pakietów w projektach przy użyciu formatu `packages.config` zarządzania.</span><span class="sxs-lookup"><span data-stu-id="11f03-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="11f03-200">W przypadku projektów przy użyciu formatu PackageReference, NuGet używa najpierw źródeł lokalnych, a następnie źródeł na udziałach sieciowych, a następnie źródeł HTTP, niezależnie od kolejności w plikach konfiguracyjnych.</span><span class="sxs-lookup"><span data-stu-id="11f03-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="11f03-201">NuGet zawsze ignoruje kolejność źródeł z operacjami przywracania.</span><span class="sxs-lookup"><span data-stu-id="11f03-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="11f03-202">`disabledPackageSources`: ta kolekcja ma również `NuGet.Config` takie samo znaczenie jak w plikach, gdzie każde źródło, którego dotyczy problem, jest wymienione według jego nazwy i wartości true/false wskazującej, czy jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="11f03-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="11f03-203">Dzięki temu nazwa źródła i `packageSources` adres URL pozostają w bez konieczności jego domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="11f03-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="11f03-204">Poszczególni deweloperzy mogą następnie ponownie włączyć źródło, `NuGet.Config` ustawiając wartość źródła na false w innych plikach bez konieczności ponownego znajdowania poprawnego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="11f03-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="11f03-205">Jest to również przydatne do dostarczania deweloperom pełną listę wewnętrznych źródłowych adresów URL dla organizacji, jednocześnie włączając domyślnie tylko źródło pojedynczego zespołu.</span><span class="sxs-lookup"><span data-stu-id="11f03-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="11f03-206">`defaultPushSource`: określa domyślny `nuget push` cel dla operacji, zastępując wbudowany domyślny nuget.org. Administratorzy mogą wdrożyć to ustawienie, aby uniknąć publikowania pakietów wewnętrznych w nuget.org `nuget push -Source` publicznych przez przypadek, ponieważ deweloperzy muszą używać do publikowania w celu nuget.org.</span><span class="sxs-lookup"><span data-stu-id="11f03-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="11f03-207">Przykład NuGetDefaults.Config i aplikacji</span><span class="sxs-lookup"><span data-stu-id="11f03-207">Example NuGetDefaults.Config and application</span></span>

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
