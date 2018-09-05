---
title: Jak zarządzać globalnymi pakietami, pamięci podręcznej, folderów tymczasowych w programie NuGet
description: Jak zarządzać folderu instalacji pakietu globalnej pamięci podręcznej pakietu i folderów tymczasowych, które istnieją na komputerze, które są używane podczas instalowania, przywracania i aktualizowanie pakietów.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: c547ae1d46079d040d7c3aa4c7678e70cd199dce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548016"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="ed6ca-103">Zarządzanie globalnymi pakietami, pamięci podręcznej i folderów tymczasowych</span><span class="sxs-lookup"><span data-stu-id="ed6ca-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="ed6ca-104">Zawsze, gdy instalować, aktualizować ani przywrócić pakietu NuGet zarządza pakiety i informacje o pakiecie w kilku folderach poza do struktury projektu:</span><span class="sxs-lookup"><span data-stu-id="ed6ca-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="ed6ca-105">Nazwa</span><span class="sxs-lookup"><span data-stu-id="ed6ca-105">Name</span></span> | <span data-ttu-id="ed6ca-106">Opis i lokalizacji (na użytkownika)</span><span class="sxs-lookup"><span data-stu-id="ed6ca-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="ed6ca-107">globalne&#8209;pakietów</span><span class="sxs-lookup"><span data-stu-id="ed6ca-107">global&#8209;packages</span></span> | <span data-ttu-id="ed6ca-108">*Globalnymi pakietami* folder to, gdzie NuGet instaluje wszelkie pobranego pakietu.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="ed6ca-109">Każdy pakiet jest w pełni rozwinięta do podfolderu, który odpowiada identyfikator pakietu i numeru wersji.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="ed6ca-110">Projektów przy użyciu funkcji PackageReference zawsze formatu pakietów Użyj bezpośrednio z tego folderu.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-110">Projects using the PackageReference format always use packages directly from this folder.</span></span> <span data-ttu-id="ed6ca-111">Korzystając z `packages.config`, pakiety są instalowane na *globalnymi pakietami* folder i następnie kopiowane do projektu `packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-111">When using the `packages.config`, packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="ed6ca-112">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="ed6ca-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="ed6ca-113">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="ed6ca-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="ed6ca-114">Zastąp przy użyciu zmiennej środowiskowej NUGET_PACKAGES, `globalPackagesFolder` lub `repositoryPath` [ustawienia konfiguracji](../reference/nuget-config-file.md#config-section) (korzystając z funkcji PackageReference i `packages.config`odpowiednio), lub `RestorePackagesPath` MSBuild Właściwość (MSBuild tylko).</span><span class="sxs-lookup"><span data-stu-id="ed6ca-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="ed6ca-115">Zmienna środowiskowa mają pierwszeństwo przed ustawieniem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="ed6ca-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="ed6ca-116">http&#8209;cache</span></span> | <span data-ttu-id="ed6ca-117">Menedżera pakietów programu Visual Studio (NuGet 3.x+) i `dotnet` narzędzie przechowują kopie pakietów do pobrania w tej pamięci podręcznej (zapisane jako `.dat` pliki) zorganizowanym w podfoldery dla każdego źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="ed6ca-118">Pakiety nie zostaną rozwinięte i pamięć podręczna zawiera 30-minutowy czas wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="ed6ca-119">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="ed6ca-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="ed6ca-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="ed6ca-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="ed6ca-121">Musi zostać zastąpiona, przy użyciu zmiennej środowiskowej NUGET_HTTP_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="ed6ca-122">Temp</span><span class="sxs-lookup"><span data-stu-id="ed6ca-122">temp</span></span> | <span data-ttu-id="ed6ca-123">Folder, w którym NuGet przechowywania plików tymczasowych podczas jego różne operacje.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="ed6ca-124">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="ed6ca-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="ed6ca-125">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="ed6ca-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="ed6ca-126">pamięć podręczna wtyczek **4.8 +**</span><span class="sxs-lookup"><span data-stu-id="ed6ca-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="ed6ca-127">Folder, w którym NuGet przechowuje wyniki z żądania oświadczeń operacji.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="ed6ca-128">Windows: `%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="ed6ca-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="ed6ca-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="ed6ca-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="ed6ca-130">Musi zostać zastąpiona, przy użyciu zmiennej środowiskowej NUGET_PLUGINS_CACHE_PATH.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="ed6ca-131">NuGet 3.5 i starszych używa *pamięci podręcznej pakietów* zamiast *pamięci podręcznej http*, który znajduje się w `%localappdata%\NuGet\Cache`.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="ed6ca-132">Przy użyciu pamięci podręcznej i *globalnymi pakietami* folderów, NuGet ogólnie pozwala uniknąć pobierania pakietów, które już istnieją na komputerze, poprawę wydajności instalacji, aktualizacji i operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="ed6ca-133">Korzystając z funkcji PackageReference, *globalnymi pakietami* folderu również pozwala uniknąć przechowywania pobrane pakiety w folderach projektu, gdzie one może przypadkowo dodane do kontroli źródła i zmniejsza całkowity wpływ NuGet na komputerze Magazyn.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="ed6ca-134">Po wyświetleniu monitu, aby pobrać pakiet, NuGet najpierw przeszukuje *globalnymi pakietami* folderu.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="ed6ca-135">Jeśli dokładna wersja pakietu nie jest dostępne, NuGet umożliwia sprawdzenie wszystkich źródeł pakietów protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="ed6ca-136">Jeśli nadal nie znaleziono pakietu, NuGet szuka pakietu w *pamięci podręcznej http* chyba że określisz `--no-cache` z `dotnet.exe` poleceń lub `-NoCache` z `nuget.exe` poleceń.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="ed6ca-137">Jeśli pakiet nie znajduje się w pamięci podręcznej lub pamięci podręcznej nie jest używany, NuGet następnie pobiera pakiet za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="ed6ca-138">Aby uzyskać więcej informacji, zobacz [co się dzieje po zainstalowaniu pakietu](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span><span class="sxs-lookup"><span data-stu-id="ed6ca-138">For more information, see [What happens when a package is installed](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="ed6ca-139">Wyświetlanie lokalizacje folderów</span><span class="sxs-lookup"><span data-stu-id="ed6ca-139">Viewing folder locations</span></span>

<span data-ttu-id="ed6ca-140">Można wyświetlić przy użyciu lokalizacji [polecenie lokalne nuget](../tools/cli-ref-locals.md):</span><span class="sxs-lookup"><span data-stu-id="ed6ca-140">You can view locations using the [nuget locals command](../tools/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="ed6ca-141">Typowe dane wyjściowe (Windows; Bieżąca nazwa użytkownika to "uzytkownik1"):</span><span class="sxs-lookup"><span data-stu-id="ed6ca-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="ed6ca-142">(`package-cache` jest używany w pakiecie NuGet 2.x i pojawia się za pomocą NuGet 3.5 i starszych.)</span><span class="sxs-lookup"><span data-stu-id="ed6ca-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="ed6ca-143">Można także wyświetlać lokalizacje folderów za pomocą [polecenie lokalne nuget dotnet](/dotnet/core/tools/dotnet-nuget-locals):</span><span class="sxs-lookup"><span data-stu-id="ed6ca-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```cli
dotnet nuget locals all --list
```

<span data-ttu-id="ed6ca-144">Typowe dane wyjściowe (Mac/Linux; Bieżąca nazwa użytkownika to "uzytkownik1"):</span><span class="sxs-lookup"><span data-stu-id="ed6ca-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="ed6ca-145">Aby wyświetlić lokalizację pojedynczy folder, należy użyć `http-cache`, `global-packages`, `temp`, lub `plugins-cache` zamiast `all`.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="ed6ca-146">Czyszczenie foldery lokalne</span><span class="sxs-lookup"><span data-stu-id="ed6ca-146">Clearing local folders</span></span>

<span data-ttu-id="ed6ca-147">Jeśli występują problemy z instalacją pakietu lub chcesz w przeciwnym razie upewnij się, czy instalujesz pakiety ze zdalnego galerii, użyj `locals --clear` opcji (dotnet.exe) lub `locals -clear` (nuget.exe), określając folder, aby wyczyścić, lub `all` do Wyczyść wszystkie foldery:</span><span class="sxs-lookup"><span data-stu-id="ed6ca-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

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

<span data-ttu-id="ed6ca-148">Wszystkie pakiety używane w projektach, które są aktualnie otwarte w programie Visual Studio nie są usuwane z *globalnymi pakietami* folderu.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="ed6ca-149">W programie Visual Studio 2017, użyj **Narzędzia > Menedżer pakietów NuGet > Ustawienia Menedżera pakietów** menu polecenia, a następnie wybierz **wyczyść wszystkie Cache(s) NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-149">In Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="ed6ca-150">Zarządzanie pamięcią podręczną nie jest obecnie dostępna za pośrednictwem konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="ed6ca-151">W programie Visual Studio 2015 zamiast tego użyj poleceń interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![NuGet — opcja polecenia czyszczenia pamięci podręcznych](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="ed6ca-153">Rozwiązywanie problemów z błędami</span><span class="sxs-lookup"><span data-stu-id="ed6ca-153">Troubleshooting errors</span></span>

<span data-ttu-id="ed6ca-154">Następujące błędy mogą wystąpić, gdy za pomocą `nuget locals` lub `dotnet nuget locals`:</span><span class="sxs-lookup"><span data-stu-id="ed6ca-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="ed6ca-155">*Błąd: Proces nie może uzyskać dostępu do pliku <package> , ponieważ jest on używany przez inny proces* lub *wyczyszczenie zasobów lokalnych nie powiodło się: nie można usunąć jeden lub więcej plików*</span><span class="sxs-lookup"><span data-stu-id="ed6ca-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="ed6ca-156">Jeden lub więcej plików w folderze są używane przez inny proces; na przykład projektu programu Visual Studio jest otwarty, która odwołuje się do pakietów w *globalnymi pakietami* folderu.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="ed6ca-157">Zamknij tych procesów i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-157">Close those processes and try again.</span></span>

- <span data-ttu-id="ed6ca-158">*Błąd: Dostęp do ścieżki <path> odmowa* lub *katalog nie jest pusty*</span><span class="sxs-lookup"><span data-stu-id="ed6ca-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="ed6ca-159">Nie masz uprawnień do usuwania plików w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="ed6ca-160">Zmień uprawnienia do folderu, jeśli to możliwe i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="ed6ca-161">W przeciwnym razie skontaktuj się z administratorem systemu.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="ed6ca-162">*Błąd: Określona ścieżka i nazwa pliku są za długie. W pełni kwalifikowanej nazwy pliku musi być mniejsza niż 260 znaków, a nazwy katalogu musi być mniejsza niż 248 znaków.*</span><span class="sxs-lookup"><span data-stu-id="ed6ca-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="ed6ca-163">Skróć nazwy folderu i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="ed6ca-163">Shorten the folder names and try again.</span></span>
