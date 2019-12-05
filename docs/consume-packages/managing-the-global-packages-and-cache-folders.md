---
title: Jak zarządzać pakietami globalnymi, pamięcią podręczną, folderami tymczasowymi w pakiecie NuGet
description: Jak zarządzać folderem instalacji pakietów globalnych, pamięci podręcznej pakietów i folderami tymczasowymi, które istnieją na komputerze, które są używane podczas instalowania, przywracania i aktualizowania pakietów.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825210"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="b3af7-103">Zarządzanie pakietami globalnymi, pamięcią podręczną i folderami tymczasowymi</span><span class="sxs-lookup"><span data-stu-id="b3af7-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="b3af7-104">Za każdym razem, gdy instalujesz, aktualizujesz lub przywracasz pakiet, program NuGet zarządza pakietami i informacjami o pakietach w kilku folderach poza strukturą projektu:</span><span class="sxs-lookup"><span data-stu-id="b3af7-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="b3af7-105">Nazwa</span><span class="sxs-lookup"><span data-stu-id="b3af7-105">Name</span></span> | <span data-ttu-id="b3af7-106">Opis i lokalizacja (na użytkownika)</span><span class="sxs-lookup"><span data-stu-id="b3af7-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="b3af7-107">global&#8209;packages</span><span class="sxs-lookup"><span data-stu-id="b3af7-107">global&#8209;packages</span></span> | <span data-ttu-id="b3af7-108">W folderze *globalne pakiety* jest instalowany pobrany pakiet NuGet.</span><span class="sxs-lookup"><span data-stu-id="b3af7-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="b3af7-109">Każdy pakiet jest w pełni rozwinięty do podfolderu, który jest zgodny z identyfikatorem pakietu i numerem wersji.</span><span class="sxs-lookup"><span data-stu-id="b3af7-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="b3af7-110">Projekty korzystające z formatu [PackageReference](package-references-in-project-files.md) zawsze używają pakietów bezpośrednio z tego folderu.</span><span class="sxs-lookup"><span data-stu-id="b3af7-110">Projects using the [PackageReference](package-references-in-project-files.md) format always use packages directly from this folder.</span></span> <span data-ttu-id="b3af7-111">W przypadku korzystania z [pliku Packages. config](../reference/packages-config.md)pakiety są instalowane do folderu *Global-Packages* , a następnie kopiowane do folderu `packages` projektu.</span><span class="sxs-lookup"><span data-stu-id="b3af7-111">When using the [packages.config](../reference/packages-config.md), packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="b3af7-112">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="b3af7-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="b3af7-113">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="b3af7-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="b3af7-114">Zastąpienie przy użyciu zmiennej środowiskowej NUGET_PACKAGES, [ustawień konfiguracji](../reference/nuget-config-file.md#config-section) `globalPackagesFolder` lub `repositoryPath` (w przypadku używania odpowiednio PackageReference i `packages.config`) lub właściwości programu MSBuild `RestorePackagesPath` (tylko MSBuild).</span><span class="sxs-lookup"><span data-stu-id="b3af7-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="b3af7-115">Zmienna środowiskowa ma pierwszeństwo przed ustawieniem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b3af7-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="b3af7-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="b3af7-116">http&#8209;cache</span></span> | <span data-ttu-id="b3af7-117">Menedżer pakietów programu Visual Studio (NuGet 3. x +) i narzędzie `dotnet` przechowują kopie pobranych pakietów w tej pamięci podręcznej (zapisane jako pliki `.dat`), zorganizowane w podfoldery dla każdego źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="b3af7-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="b3af7-118">Pakiety nie są rozwinięte, a pamięć podręczna ma czas wygaśnięcia 30 minut.</span><span class="sxs-lookup"><span data-stu-id="b3af7-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="b3af7-119">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="b3af7-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="b3af7-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="b3af7-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="b3af7-121">Przesłoń przy użyciu zmiennej środowiskowej NUGET_HTTP_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="b3af7-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="b3af7-122">temp</span><span class="sxs-lookup"><span data-stu-id="b3af7-122">temp</span></span> | <span data-ttu-id="b3af7-123">Folder, w którym narzędzia NuGet przechowują pliki tymczasowe podczas wykonywania różnych operacji.</span><span class="sxs-lookup"><span data-stu-id="b3af7-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="b3af7-124">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="b3af7-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="b3af7-125">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="b3af7-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="b3af7-126">plugins-cache **4.8+**</span><span class="sxs-lookup"><span data-stu-id="b3af7-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="b3af7-127">Folder, w którym narzędzia NuGet przechowują wyniki żądania oświadczeń operacji.</span><span class="sxs-lookup"><span data-stu-id="b3af7-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="b3af7-128">Windows: `%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="b3af7-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="b3af7-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="b3af7-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="b3af7-130">Przesłoń przy użyciu zmiennej środowiskowej NUGET_PLUGINS_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="b3af7-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="b3af7-131">Narzędzia NuGet 3,5 i starsze używają *pamięci podręcznej pakietów* zamiast *pamięci podręcznej http*, która znajduje się w `%localappdata%\NuGet\Cache`.</span><span class="sxs-lookup"><span data-stu-id="b3af7-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="b3af7-132">Przy użyciu folderów pamięci podręcznej i *pakietów globalnych pakiet* NuGet zazwyczaj eliminuje pobieranie pakietów, które już istnieją na komputerze, co zwiększa wydajność operacji instalacji, aktualizacji i przywracania.</span><span class="sxs-lookup"><span data-stu-id="b3af7-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="b3af7-133">W przypadku korzystania z programu PackageReference folder *Global-Packages* również pozwala uniknąć utrzymywania pobranych pakietów wewnątrz folderów projektu, gdzie mogą być przypadkowo dodawane do kontroli źródła i zmniejsza ogólny wpływ narzędzia NuGet na magazyn komputerowy.</span><span class="sxs-lookup"><span data-stu-id="b3af7-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="b3af7-134">Po wyświetleniu monitu o pobranie pakietu pakiet NuGet najpierw szuka folderu *Global-Packages* .</span><span class="sxs-lookup"><span data-stu-id="b3af7-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="b3af7-135">Jeśli dokładna wersja pakietu nie istnieje, pakiet NuGet sprawdza wszystkie źródła pakietów spoza protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="b3af7-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="b3af7-136">Jeśli pakiet nadal nie zostanie znaleziony, pakiet NuGet szuka pakietu w *pamięci podręcznej http* , chyba że zostanie określony `--no-cache` z poleceniami `dotnet.exe` lub `-NoCache` z `nuget.exe` poleceniami.</span><span class="sxs-lookup"><span data-stu-id="b3af7-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="b3af7-137">Jeśli pakiet nie znajduje się w pamięci podręcznej, a pamięć podręczna nie jest używana, narzędzie NuGet pobierze pakiet za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="b3af7-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="b3af7-138">Aby uzyskać więcej informacji, zobacz [co się stanie po zainstalowaniu pakietu?](../concepts/package-installation-process.md).</span><span class="sxs-lookup"><span data-stu-id="b3af7-138">For more information, see [What happens when a package is installed?](../concepts/package-installation-process.md).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="b3af7-139">Przeglądanie lokalizacji folderów</span><span class="sxs-lookup"><span data-stu-id="b3af7-139">Viewing folder locations</span></span>

<span data-ttu-id="b3af7-140">Lokalizacje można wyświetlić za pomocą [polecenia locale programu NuGet](../reference/cli-reference/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="b3af7-140">You can view locations using the [nuget locals command](../reference/cli-reference/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="b3af7-141">Typowe dane wyjściowe (Windows; "Użytkownik1" jest bieżącą nazwą użytkownika:</span><span class="sxs-lookup"><span data-stu-id="b3af7-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="b3af7-142">(`package-cache` jest używany w NuGet 2. x i występuje z pakietem NuGet 3,5 i wcześniejszym).</span><span class="sxs-lookup"><span data-stu-id="b3af7-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="b3af7-143">Lokalizacje folderów można także wyświetlić przy użyciu [polecenia locale programu dotnet dla ustawień regionalnych](/dotnet/core/tools/dotnet-nuget-locals):</span><span class="sxs-lookup"><span data-stu-id="b3af7-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```dotnetcli
dotnet nuget locals all --list
```

<span data-ttu-id="b3af7-144">Typowe dane wyjściowe (Mac/Linux; "Użytkownik1" jest bieżącą nazwą użytkownika:</span><span class="sxs-lookup"><span data-stu-id="b3af7-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="b3af7-145">Aby wyświetlić lokalizację pojedynczego folderu, użyj `http-cache`, `global-packages`, `temp`lub `plugins-cache` zamiast `all`.</span><span class="sxs-lookup"><span data-stu-id="b3af7-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="b3af7-146">Czyszczenie folderów lokalnych</span><span class="sxs-lookup"><span data-stu-id="b3af7-146">Clearing local folders</span></span>

<span data-ttu-id="b3af7-147">Jeśli wystąpią problemy z instalacją pakietu lub w przeciwnym razie chcesz upewnić się, że instalujesz pakiety z galerii zdalnej, użyj opcji `locals --clear` (dotnet. exe) lub `locals -clear` (NuGet. exe), określając folder do wyczyszczenia lub `all` wyczyścić wszystkie foldery:</span><span class="sxs-lookup"><span data-stu-id="b3af7-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

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

<span data-ttu-id="b3af7-148">Wszystkie pakiety używane przez projekty, które są aktualnie otwarte w programie Visual Studio, nie są usuwane z folderu *Global-Packages* .</span><span class="sxs-lookup"><span data-stu-id="b3af7-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="b3af7-149">Począwszy od programu Visual Studio 2017, użyj **narzędzia > Menedżer pakietów NuGet > menu Ustawienia Menedżera pakietów** , a następnie wybierz polecenie **Wyczyść wszystkie pamięć podręczna NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b3af7-149">Starting in Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="b3af7-150">Zarządzanie pamięcią podręczną nie jest obecnie dostępne za pomocą konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="b3af7-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="b3af7-151">W programie Visual Studio 2015 zamiast tego Użyj poleceń interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b3af7-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![Polecenie NuGet opcji do czyszczenia pamięci podręcznych](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="b3af7-153">Rozwiązywanie problemów z błędami</span><span class="sxs-lookup"><span data-stu-id="b3af7-153">Troubleshooting errors</span></span>

<span data-ttu-id="b3af7-154">Podczas używania `nuget locals` lub `dotnet nuget locals`mogą wystąpić następujące błędy:</span><span class="sxs-lookup"><span data-stu-id="b3af7-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="b3af7-155">*Błąd: proces nie może uzyskać dostępu do pliku <package>, ponieważ jest on używany przez inny proces* lub *czyszczenie zasobów lokalnych nie powiodło się: nie można usunąć co najmniej jednego pliku*</span><span class="sxs-lookup"><span data-stu-id="b3af7-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="b3af7-156">Co najmniej jeden plik w folderze jest używany przez inny proces; na przykład projekt programu Visual Studio jest otwarty, który odwołuje się do pakietów w folderze *Global-Packages* .</span><span class="sxs-lookup"><span data-stu-id="b3af7-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="b3af7-157">Zamknij te procesy i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="b3af7-157">Close those processes and try again.</span></span>

- <span data-ttu-id="b3af7-158">*Błąd: odmowa dostępu do ścieżki <path>* lub *katalog nie jest pusty*</span><span class="sxs-lookup"><span data-stu-id="b3af7-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="b3af7-159">Nie masz uprawnień do usuwania plików w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="b3af7-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="b3af7-160">Zmień uprawnienia folderu, jeśli to możliwe, i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="b3af7-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="b3af7-161">W przeciwnym razie skontaktuj się z administratorem systemu.</span><span class="sxs-lookup"><span data-stu-id="b3af7-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="b3af7-162">*Błąd: określona ścieżka, nazwa pliku lub obie te wartości są za długie. W pełni kwalifikowana nazwa pliku musi być krótsza niż 260 znaków, a nazwa katalogu musi być krótsza niż 248 znaków.*</span><span class="sxs-lookup"><span data-stu-id="b3af7-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="b3af7-163">Skróć nazwy folderów i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="b3af7-163">Shorten the folder names and try again.</span></span>
