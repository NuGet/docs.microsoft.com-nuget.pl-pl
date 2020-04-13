---
title: Jak zarządzać pakietami globalnymi, pamięcią podręczną, folderami tymczasowymi w NuGet
description: Jak zarządzać globalnym folderem instalacji pakietu, pamięci podręcznej pakietów i folderów tymczasowych, które istnieją na komputerze, które są używane podczas instalowania, przywracania i aktualizowania pakietów.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428969"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="ccc83-103">Zarządzanie pakietami globalnymi, pamięcią podręczną i folderami tymczasowymi</span><span class="sxs-lookup"><span data-stu-id="ccc83-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="ccc83-104">Za każdym razem, gdy instalujesz, aktualizujesz lub przywracasz pakiet, NuGet zarządza pakietami i informacjami o pakiecie w kilku folderach poza strukturą projektu:</span><span class="sxs-lookup"><span data-stu-id="ccc83-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="ccc83-105">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ccc83-105">Name</span></span> | <span data-ttu-id="ccc83-106">Opis i lokalizacja (na użytkownika)</span><span class="sxs-lookup"><span data-stu-id="ccc83-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="ccc83-107">globalne pakiety&#8209;</span><span class="sxs-lookup"><span data-stu-id="ccc83-107">global&#8209;packages</span></span> | <span data-ttu-id="ccc83-108">W folderze *pakietów globalnych* jest miejsce, w którym NuGet instaluje dowolny pobrany pakiet.</span><span class="sxs-lookup"><span data-stu-id="ccc83-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="ccc83-109">Każdy pakiet jest w pełni rozwinięty do podfolderu, który pasuje do identyfikatora pakietu i numeru wersji.</span><span class="sxs-lookup"><span data-stu-id="ccc83-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="ccc83-110">Projekty przy użyciu [formatu PackageReference](package-references-in-project-files.md) zawsze używają pakietów bezpośrednio z tego folderu.</span><span class="sxs-lookup"><span data-stu-id="ccc83-110">Projects using the [PackageReference](package-references-in-project-files.md) format always use packages directly from this folder.</span></span> <span data-ttu-id="ccc83-111">Podczas korzystania z [packages.config,](../reference/packages-config.md)pakiety są instalowane w folderze `packages` *global-packages,* a następnie kopiowane do folderu projektu.</span><span class="sxs-lookup"><span data-stu-id="ccc83-111">When using the [packages.config](../reference/packages-config.md), packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="ccc83-112">Windows:`%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="ccc83-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="ccc83-113">Mac/Linux:`~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="ccc83-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="ccc83-114">Zastąp przy użyciu zmiennej `globalPackagesFolder` środowiskowej NUGET_PACKAGES, ustawień lub `repositoryPath` `packages.config` [konfiguracji](../reference/nuget-config-file.md#config-section) (podczas korzystania z PackageReference i , odpowiednio) lub `RestorePackagesPath` właściwości MSBuild (tylko MSBuild).</span><span class="sxs-lookup"><span data-stu-id="ccc83-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="ccc83-115">Zmienna środowiskowa ma pierwszeństwo przed ustawieniem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ccc83-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="ccc83-116">http&#8209;pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="ccc83-116">http&#8209;cache</span></span> | <span data-ttu-id="ccc83-117">Menedżer pakietów programu Visual Studio (NuGet 3.x+) i `dotnet` kopie pobranych pakietów w tej pamięci podręcznej (zapisane jako `.dat` pliki), zorganizowane w podfoldery dla każdego źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="ccc83-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="ccc83-118">Pakiety nie są rozszerzane, a pamięć podręczna ma czas wygaśnięcia 30 minut.</span><span class="sxs-lookup"><span data-stu-id="ccc83-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="ccc83-119">Windows:`%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="ccc83-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="ccc83-120">Mac/Linux:`~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="ccc83-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="ccc83-121">Zastąp przy użyciu zmiennej środowiskowej NUGET_HTTP_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="ccc83-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="ccc83-122">Najwyższa temp</span><span class="sxs-lookup"><span data-stu-id="ccc83-122">temp</span></span> | <span data-ttu-id="ccc83-123">Folder, w którym NuGet przechowuje pliki tymczasowe podczas różnych operacji.</span><span class="sxs-lookup"><span data-stu-id="ccc83-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="ccc83-124">Windows:`%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="ccc83-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="ccc83-125">Mac/Linux:`/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="ccc83-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="ccc83-126">wtyczki-cache **4.8+**</span><span class="sxs-lookup"><span data-stu-id="ccc83-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="ccc83-127">Folder, w którym NuGet przechowuje wyniki z żądania oświadczeń operacji.</span><span class="sxs-lookup"><span data-stu-id="ccc83-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="ccc83-128">Windows:`%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="ccc83-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="ccc83-129">Mac/Linux:`~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="ccc83-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="ccc83-130">Zastąd wymień przy użyciu zmiennej środowiskowej NUGET_PLUGINS_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="ccc83-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="ccc83-131">NuGet 3.5 i wcześniej używa *pakietów pamięci podręcznej* zamiast *http-cache*, który znajduje się w `%localappdata%\NuGet\Cache`.</span><span class="sxs-lookup"><span data-stu-id="ccc83-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="ccc83-132">Korzystając z pamięci podręcznej i *global-packages* folderów, NuGet zazwyczaj unika pobierania pakietów, które już istnieją na komputerze, zwiększając wydajność operacji instalacji, aktualizacji i przywracania.</span><span class="sxs-lookup"><span data-stu-id="ccc83-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="ccc83-133">Podczas korzystania z PackageReference, *global-packages* folder unika również przechowywania pobranych pakietów wewnątrz folderów projektu, gdzie mogą one zostać przypadkowo dodane do kontroli źródła i zmniejsza ogólny wpływ NuGet na magazyn komputera.</span><span class="sxs-lookup"><span data-stu-id="ccc83-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="ccc83-134">Po zapytaniu o pobranie pakietu, NuGet najpierw szuka w folderze *pakietów globalnych.*</span><span class="sxs-lookup"><span data-stu-id="ccc83-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="ccc83-135">Jeśli dokładna wersja pakietu nie istnieje, następnie NuGet sprawdza wszystkie źródła pakietów innych niż HTTP.</span><span class="sxs-lookup"><span data-stu-id="ccc83-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="ccc83-136">Jeśli pakiet nadal nie został znaleziony, NuGet szuka pakietu w `--no-cache` pamięci `dotnet.exe` *podręcznej http,* chyba że określisz za pomocą poleceń lub `-NoCache` z `nuget.exe` poleceniami.</span><span class="sxs-lookup"><span data-stu-id="ccc83-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="ccc83-137">Jeśli pakiet nie znajduje się w pamięci podręcznej lub pamięć podręczna nie jest używana, NuGet pobiera pakiet za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="ccc83-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="ccc83-138">Aby uzyskać więcej informacji, zobacz [Co się stanie po zainstalowaniu pakietu?](../concepts/package-installation-process.md).</span><span class="sxs-lookup"><span data-stu-id="ccc83-138">For more information, see [What happens when a package is installed?](../concepts/package-installation-process.md).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="ccc83-139">Wyświetlanie lokalizacji folderów</span><span class="sxs-lookup"><span data-stu-id="ccc83-139">Viewing folder locations</span></span>

<span data-ttu-id="ccc83-140">Lokalizacje można wyświetlać za pomocą [polecenia nuget locals:](../reference/cli-reference/cli-ref-locals.md)</span><span class="sxs-lookup"><span data-stu-id="ccc83-140">You can view locations using the [nuget locals command](../reference/cli-reference/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="ccc83-141">Typowe dane wyjściowe (Windows; "user1" to aktualna nazwa użytkownika):</span><span class="sxs-lookup"><span data-stu-id="ccc83-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="ccc83-142">(`package-cache` jest używany w NuGet 2.x i pojawia się z NuGet 3.5 i wcześniej.)</span><span class="sxs-lookup"><span data-stu-id="ccc83-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="ccc83-143">Lokalizacje folderów można również wyświetlać za pomocą [polecenia dotnet nuget locals:](/dotnet/core/tools/dotnet-nuget-locals)</span><span class="sxs-lookup"><span data-stu-id="ccc83-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```dotnetcli
dotnet nuget locals all --list
```

<span data-ttu-id="ccc83-144">Typowe wyjście (Mac/Linux; "user1" to aktualna nazwa użytkownika):</span><span class="sxs-lookup"><span data-stu-id="ccc83-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="ccc83-145">Aby wyświetlić lokalizację pojedynczego `http-cache`folderu, `plugins-cache` użyj , `all` `global-packages`, `temp`lub zamiast .</span><span class="sxs-lookup"><span data-stu-id="ccc83-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="ccc83-146">Czyszczenie folderów lokalnych</span><span class="sxs-lookup"><span data-stu-id="ccc83-146">Clearing local folders</span></span>

<span data-ttu-id="ccc83-147">Jeśli wystąpią problemy z instalacją pakietu lub w inny sposób chcesz `locals --clear` upewnić się, że instalujesz pakiety ze zdalnej galerii, użyj opcji (dotnet.exe) lub `locals -clear` (nuget.exe), określając folder do wyczyszczenie lub `all` wyczyść wszystkie foldery:</span><span class="sxs-lookup"><span data-stu-id="ccc83-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="ccc83-148">Wszystkie pakiety używane przez projekty, które są obecnie otwarte w programie Visual Studio nie są czyszczone z folderu *pakietów globalnych.*</span><span class="sxs-lookup"><span data-stu-id="ccc83-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="ccc83-149">Począwszy od programu Visual Studio 2017, użyj polecenia menu **Narzędzia > Menedżer pakietów NuGet > Ustawienia Menedżera pakietów,** a następnie wybierz pozycję **Wyczyść wszystkie pamięci podręczne NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ccc83-149">Starting in Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="ccc83-150">Zarządzanie pamięcią podręczną nie jest obecnie dostępne za pośrednictwem konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="ccc83-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="ccc83-151">W programie Visual Studio 2015 należy użyć polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="ccc83-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![Polecenie opcji NuGet do usuwania pamięci podręcznych](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="ccc83-153">Rozwiązywanie problemów z błędami</span><span class="sxs-lookup"><span data-stu-id="ccc83-153">Troubleshooting errors</span></span>

<span data-ttu-id="ccc83-154">Podczas korzystania `nuget locals` lub: `dotnet nuget locals`</span><span class="sxs-lookup"><span data-stu-id="ccc83-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="ccc83-155">*Błąd: proces nie może <package> uzyskać dostępu do pliku, ponieważ jest on używany przez inny proces* lub czyszczenie zasobów lokalnych nie *powiodło się: Nie można usunąć jednego lub więcej plików*</span><span class="sxs-lookup"><span data-stu-id="ccc83-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="ccc83-156">Jeden lub więcej plików w folderze są używane przez inny proces; na przykład projekt programu Visual Studio jest otwarty, który odwołuje się do pakietów w folderze *pakietów globalnych.*</span><span class="sxs-lookup"><span data-stu-id="ccc83-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="ccc83-157">Zamknij te procesy i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="ccc83-157">Close those processes and try again.</span></span>

- <span data-ttu-id="ccc83-158">*Błąd: odmowa <path> dostępu do ścieżki* lub *katalog nie jest pusty*</span><span class="sxs-lookup"><span data-stu-id="ccc83-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="ccc83-159">Nie masz uprawnień do usuwania plików w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="ccc83-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="ccc83-160">Jeśli to możliwe, zmień uprawnienia do folderu i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="ccc83-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="ccc83-161">W przeciwnym razie skontaktuj się z administratorem systemu.</span><span class="sxs-lookup"><span data-stu-id="ccc83-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="ccc83-162">*Błąd: określona ścieżka, nazwa pliku lub oba są zbyt długie. W pełni kwalifikowana nazwa pliku musi być mniejsza niż 260 znaków, a nazwa katalogu musi być mniejsza niż 248 znaków.*</span><span class="sxs-lookup"><span data-stu-id="ccc83-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="ccc83-163">Skróć nazwy folderów i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="ccc83-163">Shorten the folder names and try again.</span></span>
