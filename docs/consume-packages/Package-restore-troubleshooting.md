---
title: Rozwiązywanie problemów z przywracania pakietów NuGet w programie Visual Studio
description: Opis typowych NuGet przywrócić błędów w Visual Studio oraz ze sposobem rozwiązać ten problem.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 11acb90b45af73137faac1ec6bc403b109e6e808
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549603"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="4f102-103">Rozwiązywanie problemów z błędami Przywracanie pakietu</span><span class="sxs-lookup"><span data-stu-id="4f102-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="4f102-104">Ten artykuł koncentruje się na typowych błędów podczas przywracania pakietów i kroki, aby je rozwiązać.</span><span class="sxs-lookup"><span data-stu-id="4f102-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="4f102-105">Aby uzyskać szczegółowe informacje dotyczące przywracania pakietów, zobacz [Przywracanie pakietu](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="4f102-105">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="4f102-106">Jeśli podanych tutaj instrukcji nie działają, [Zgłoś problem w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak, aby firma Microsoft bardziej dokładnie sprawdź danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="4f102-106">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="4f102-107">Nie używaj "czy ta strona jest pomocna?"</span><span class="sxs-lookup"><span data-stu-id="4f102-107">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="4f102-108">Kontrolka, która może pojawić się na tej stronie, ponieważ jej nie umożliwiają nam się z Tobą, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="4f102-108">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="4f102-109">Szybkie rozwiązanie dla użytkowników programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4f102-109">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="4f102-110">Jeśli używasz programu Visual Studio, najpierw włączyć przywracania pakietów w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="4f102-110">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="4f102-111">W przeciwnym razie przejdź do kolejnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="4f102-111">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="4f102-112">Wybierz **Narzędzia > Menedżer pakietów NuGet > Ustawienia Menedżera pakietów** polecenia menu.</span><span class="sxs-lookup"><span data-stu-id="4f102-112">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="4f102-113">Ustaw obie opcje, w obszarze **Przywracanie pakietów**.</span><span class="sxs-lookup"><span data-stu-id="4f102-113">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="4f102-114">Wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f102-114">Select **OK**.</span></span>
1. <span data-ttu-id="4f102-115">Ponownie skompiluj projekt.</span><span class="sxs-lookup"><span data-stu-id="4f102-115">Build your project again.</span></span>

![Włączanie przywracania pakietów NuGet w narzędzia/Opcje](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="4f102-117">Te ustawienia można zmienić w swojej `NuGet.config` pliku; zobacz [zgody](#consent) sekcji.</span><span class="sxs-lookup"><span data-stu-id="4f102-117">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="4f102-118">Ten projekt przywołuje pakiety NuGet, których brakuje na tym komputerze</span><span class="sxs-lookup"><span data-stu-id="4f102-118">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="4f102-119">Komunikat o błędzie ukończone:</span><span class="sxs-lookup"><span data-stu-id="4f102-119">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="4f102-120">Ten błąd występuje, próba skompilowania projektu, który zawiera odwołania do co najmniej jednego pakietu NuGet, ale te pakiety nie są obecnie zainstalowane na komputerze lub w projekcie.</span><span class="sxs-lookup"><span data-stu-id="4f102-120">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="4f102-121">Korzystając z formatu zarządzania PackageReference, ten błąd oznacza, że pakiet nie jest zainstalowana w *globalnymi pakietami* folderu zgodnie z opisem na zgodnie z opisem na [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="4f102-121">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="4f102-122">Korzystając z `packages.config`, ten błąd oznacza, że pakiet nie jest zainstalowany w `packages` folder w katalogu głównym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="4f102-122">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="4f102-123">Ta sytuacja występuje często, gdy uzyskać kod źródłowy projektu z kontroli źródła lub innego pobierania.</span><span class="sxs-lookup"><span data-stu-id="4f102-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="4f102-124">Pakiety zazwyczaj zostały pominięte w kontroli źródła lub pliki do pobrania, ponieważ pliki mogą zostać przywrócone z pakietu pakietami, takie jak nuget.org (zobacz [pakiety i kontrola źródła](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="4f102-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="4f102-125">Uwzględniając je w przeciwnym razie będzie wybrzuszanie repozytorium lub utworzyć pliki zip niepotrzebnie.</span><span class="sxs-lookup"><span data-stu-id="4f102-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="4f102-126">Ten błąd może też być plik projektu zawiera ścieżki bezwzględnej do lokalizacji pakietu, a następnie przenieść projektu.</span><span class="sxs-lookup"><span data-stu-id="4f102-126">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="4f102-127">Do przywrócenia pakietów, użyj jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="4f102-127">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="4f102-128">Jeśli po przeniesieniu pliku projektu, należy edytować plik bezpośrednio, aby zaktualizować odwołania do pakietu.</span><span class="sxs-lookup"><span data-stu-id="4f102-128">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="4f102-129">W programie Visual Studio, należy włączyć Przywracanie pakietu, wybierając **Narzędzia > Menedżer pakietów NuGet > Ustawienia Menedżera pakietów** polecenia menu, ustawianie obu opcji w obszarze **Przywracanie pakietów**i wybierając polecenie  **OK**.</span><span class="sxs-lookup"><span data-stu-id="4f102-129">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="4f102-130">Następnie ponownie skompiluj rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="4f102-130">Then build the solution again.</span></span>
- <span data-ttu-id="4f102-131">Dla projektów .NET Core, uruchom `dotnet restore` lub `dotnet build` (który automatycznie uruchamia przywracania).</span><span class="sxs-lookup"><span data-stu-id="4f102-131">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="4f102-132">W wierszu polecenia Uruchom `nuget restore` (z wyjątkiem projekty utworzone za pomocą `dotnet`, w którym to przypadku użycia `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="4f102-132">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="4f102-133">W wierszu polecenia z projektami przy użyciu formatu PackageReference Uruchom `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="4f102-133">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="4f102-134">Po pomyślnie przeprowadzić przywrócenie, muszą znajdować się w pakiecie *globalnymi pakietami* folderu.</span><span class="sxs-lookup"><span data-stu-id="4f102-134">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="4f102-135">W przypadku projektów przy użyciu funkcji PackageReference przywracania należy ponownie utworzyć `obj/project.assets.json` pliku; dla projektów przy użyciu `packages.config`, pakiet powinien pojawić się w projekcie `packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="4f102-135">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="4f102-136">Projekt teraz powinien być kompilowany pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="4f102-136">The project should now build successfully.</span></span> <span data-ttu-id="4f102-137">W przeciwnym razie [pliku wystąpił problem w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , dzięki czemu możemy wykonać kolejne czynności z Tobą.</span><span class="sxs-lookup"><span data-stu-id="4f102-137">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="4f102-138">Zasoby plików nie można odnaleźć project.assets.json</span><span class="sxs-lookup"><span data-stu-id="4f102-138">Assets file project.assets.json not found</span></span>

<span data-ttu-id="4f102-139">Komunikat o błędzie ukończone:</span><span class="sxs-lookup"><span data-stu-id="4f102-139">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="4f102-140">`project.assets.json` Pliku przechowuje wykres zależności projektu, gdy w formacie PackageReference zarządzania, który jest używany, aby upewnić się, że wszystkie niezbędne pakiety są instalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="4f102-140">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="4f102-141">Ponieważ ten plik jest generowany dynamicznie za pośrednictwem Przywracanie pakietu, nie został zazwyczaj dodany do kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="4f102-141">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="4f102-142">W wyniku ten błąd występuje podczas kompilowania projektu za pomocą narzędzia, takie jak `msbuild` , nie automatycznie przywraca pakietów.</span><span class="sxs-lookup"><span data-stu-id="4f102-142">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="4f102-143">W takim przypadku uruchom `msbuild /t:restore` następuje `msbuild`, lub użyj `dotnet build` (przywraca pakietów automatycznie).</span><span class="sxs-lookup"><span data-stu-id="4f102-143">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="4f102-144">Można również użyć dowolnej z metod przywracania pakietów w [poprzedniej sekcji](#missing).</span><span class="sxs-lookup"><span data-stu-id="4f102-144">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="4f102-145">Co najmniej jednego pakietu NuGet, muszą zostać przywrócone, ale nie może być, ponieważ nie udzielono zgody</span><span class="sxs-lookup"><span data-stu-id="4f102-145">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="4f102-146">Komunikat o błędzie ukończone:</span><span class="sxs-lookup"><span data-stu-id="4f102-146">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="4f102-147">Ten błąd oznacza, że Przywracanie pakietu jest wyłączone w konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="4f102-147">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="4f102-148">Można zmienić ustawienia mające zastosowanie w programie Visual Studio, zgodnie z wcześniejszym opisem w obszarze [szybkie rozwiązanie dla użytkowników programu Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="4f102-148">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="4f102-149">Można również edytować te ustawienia bezpośrednio w odpowiednią `nuget.config` pliku (zazwyczaj `%AppData%\NuGet\NuGet.Config` na Windows i `~/.nuget/NuGet/NuGet.Config` w systemie Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="4f102-149">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="4f102-150">Upewnij się, że `enabled` i `automatic` klucze w ramach `packageRestore` są ustawione na wartość True:</span><span class="sxs-lookup"><span data-stu-id="4f102-150">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> <span data-ttu-id="4f102-151">Jeśli edytujesz `packageRestore` ustawienia bezpośrednio w `nuget.config`, uruchom ponownie program Visual Studio, okno dialogowe Opcje Pokazuje bieżące wartości.</span><span class="sxs-lookup"><span data-stu-id="4f102-151">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="4f102-152">Inne warunki potencjalnych</span><span class="sxs-lookup"><span data-stu-id="4f102-152">Other potential conditions</span></span>

- <span data-ttu-id="4f102-153">Komunikat informujący o tym, pobierz je za pomocą Przywracanie pakietów NuGet, mogą wystąpić błędy kompilacji z powodu brakujących plików.</span><span class="sxs-lookup"><span data-stu-id="4f102-153">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="4f102-154">Jednak Uruchamianie przywracania może powiedzieć "wszystkie pakiety są już zainstalowane i nie ma nic do przywrócenia".</span><span class="sxs-lookup"><span data-stu-id="4f102-154">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="4f102-155">W takim przypadku usuń `packages` folder (przy użyciu `packages.config`) lub `obj/project.assets.json` pliku (w przypadku używania funkcji PackageReference) i uruchom ponownie przywracania.</span><span class="sxs-lookup"><span data-stu-id="4f102-155">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="4f102-156">Jeśli ten błąd będzie nadal występował, należy użyć `nuget locals all -clear` lub `dotnet locals all --clear` z poziomu wiersza polecenia, aby wyczyścić *globalnymi pakietami* i foldery pamięci podręcznej, zgodnie z opisem na [Zarządzanie globalnymi pakietami i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="4f102-156">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="4f102-157">Podczas uzyskiwania projektu z kontroli źródła, folderów projektu może być ustawiona na tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="4f102-157">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="4f102-158">Zmień uprawnienia do folderu i spróbuj ponownie przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="4f102-158">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="4f102-159">Używasz starszej wersji pakietu nuget.</span><span class="sxs-lookup"><span data-stu-id="4f102-159">You may be using an old version of NuGet.</span></span> <span data-ttu-id="4f102-160">Sprawdź [nuget.org/downloads](https://www.nuget.org/downloads) najnowsze zalecanych wersji.</span><span class="sxs-lookup"><span data-stu-id="4f102-160">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="4f102-161">Dla programu Visual Studio 2015 firma Microsoft zaleca 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="4f102-161">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="4f102-162">Jeśli wystąpią problemy z innymi [pliku wystąpił problem w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) Aby uzyskać więcej szczegółowych informacji ze strony użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4f102-162">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>