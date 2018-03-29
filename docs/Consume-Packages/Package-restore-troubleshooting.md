---
title: Rozwiązywanie problemów z pakietu NuGet przywracania w programie Visual Studio | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Opis wspólnej NuGet Przywracanie błędy w Visual Studio i sposoby ich rozwiązywania.
keywords: Przywracanie pakietu NuGet, przywracanie pakietów, rozwiązywania problemów, rozwiązywanie problemów
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 27a43ceaefdf3a7842183a64ea57d05416d6cb02
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="2c473-104">Rozwiązywanie problemów z błędami przywracania pakietu</span><span class="sxs-lookup"><span data-stu-id="2c473-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="2c473-105">Ten artykuł dotyczy typowe błędy podczas przywracania pakietów i sposobów ich rozwiązywania.</span><span class="sxs-lookup"><span data-stu-id="2c473-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="2c473-106">Aby uzyskać szczegółowe informacje dotyczące przywracania pakietów, zobacz [Przywracanie pakietu](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="2c473-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="2c473-107">Jeśli poniższe instrukcje nie działają, [Zgłoś problem w usłudze GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak, aby firma Microsoft bada danego scenariusza bardziej dokładnie.</span><span class="sxs-lookup"><span data-stu-id="2c473-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="2c473-108">Nie używaj "warto tę stronę?"</span><span class="sxs-lookup"><span data-stu-id="2c473-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="2c473-109">formant, który może występować na tej stronie, ponieważ go nie dają nam możliwość się z Tobą, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="2c473-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="2c473-110">Szybkie rozwiązanie dla użytkowników programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2c473-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="2c473-111">Jeśli używasz programu Visual Studio, najpierw włączyć Przywracanie pakietu w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="2c473-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="2c473-112">W przeciwnym razie nadal w kolejnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="2c473-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="2c473-113">Wybierz **Narzędzia > Menedżera pakietów NuGet > Ustawienia Menedżera pakietów** polecenia menu.</span><span class="sxs-lookup"><span data-stu-id="2c473-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="2c473-114">Ustaw obie opcje w obszarze **przywracania pakietów**.</span><span class="sxs-lookup"><span data-stu-id="2c473-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="2c473-115">Wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="2c473-115">Select **OK**.</span></span>
1. <span data-ttu-id="2c473-116">Skompiluj projekt ponownie.</span><span class="sxs-lookup"><span data-stu-id="2c473-116">Build your project again.</span></span>

![Włącz Przywracanie pakietu NuGet w narzędzia/Opcje](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="2c473-118">Te ustawienia można zmienić w Twojej `NuGet.config` pliku; zobacz [zgody](#consent) sekcji.</span><span class="sxs-lookup"><span data-stu-id="2c473-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="2c473-119">Ten projekt zawiera odwołania do pakietów NuGet Brak na tym komputerze</span><span class="sxs-lookup"><span data-stu-id="2c473-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="2c473-120">Pełny komunikat:</span><span class="sxs-lookup"><span data-stu-id="2c473-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="2c473-121">Ten błąd występuje przystąpieniem do tworzenia projektu, który zawiera odwołania do co najmniej jednego pakietu NuGet, ale pakiety nie są obecnie zainstalowane na komputerze lub w projekcie.</span><span class="sxs-lookup"><span data-stu-id="2c473-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="2c473-122">Podczas korzystania z formatu zarządzania PackageReference, błąd oznacza, że pakiet nie jest zainstalowany w *globalne pakiety* folderu zgodnie z opisem na zgodnie z opisem na [Zarządzanie globalne pakietów i pamięci podręcznej folderów](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="2c473-122">When using the PackageReference management format, the error means that the package is not installed in the *global-packages* folder as described on as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="2c473-123">Korzystając z `packages.config`, ten błąd oznacza, że pakiet nie jest zainstalowany w `packages` folder w katalogu głównym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2c473-123">When using `packages.config`, the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="2c473-124">Taka sytuacja często występuje, gdy uzyskać kod źródłowy projektu z kontroli źródła lub innego pobierania.</span><span class="sxs-lookup"><span data-stu-id="2c473-124">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="2c473-125">Pakiety są zwykle pominięto z kontroli źródła lub pliki do pobrania, ponieważ pliki mogą zostać przywrócone z pakietu źródeł danych, takich jak nuget.org (zobacz [pakietów i kontroli źródła](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="2c473-125">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="2c473-126">Włączenie ich w przeciwnym razie będzie wybrzuszanie repozytorium lub Utwórz plików zip niepotrzebnie.</span><span class="sxs-lookup"><span data-stu-id="2c473-126">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="2c473-127">Użyj jednej z następujących metod w celu przywrócenia pakietów:</span><span class="sxs-lookup"><span data-stu-id="2c473-127">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="2c473-128">W programie Visual Studio, Włącz Przywracanie pakietu po wybraniu **Narzędzia > Menedżera pakietów NuGet > Ustawienia Menedżera pakietów** polecenia menu, ustawianie obu opcji w obszarze **przywracania pakietów**i wybierając  **OK**.</span><span class="sxs-lookup"><span data-stu-id="2c473-128">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="2c473-129">Następnie ponownie skompiluj rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="2c473-129">Then build the solution again.</span></span>
- <span data-ttu-id="2c473-130">Projekty platformy .NET Core, uruchom `dotnet restore` lub `dotnet build` (automatycznie uruchamia przywracania).</span><span class="sxs-lookup"><span data-stu-id="2c473-130">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="2c473-131">W wierszu polecenia Uruchom `nuget restore` (z wyjątkiem projektów utworzonych za pomocą `dotnet`, w którym to przypadku użycia `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="2c473-131">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="2c473-132">W wierszu polecenia z projektami przy użyciu formatu PackageReference Uruchom `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="2c473-132">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="2c473-133">Po przywróceniu pomyślnie, powinien znajdować się w pakiecie *globalne pakiety* folderu.</span><span class="sxs-lookup"><span data-stu-id="2c473-133">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="2c473-134">W przypadku projektów przy użyciu PackageReference przywracania należy ponownie utworzyć `obj/project.assets.json` pliku; dla projektów przy użyciu `packages.config`, pakiet powinien zostać wyświetlony w projekcie `packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="2c473-134">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="2c473-135">Projekt powinien teraz kompilacji pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="2c473-135">The project should now build successfully.</span></span> <span data-ttu-id="2c473-136">Jeśli nie, [pliku problemu w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , firma Microsoft możesz skomunikować się z Tobą.</span><span class="sxs-lookup"><span data-stu-id="2c473-136">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="2c473-137">Nie można odnaleźć project.assets.json pliku zasobów</span><span class="sxs-lookup"><span data-stu-id="2c473-137">Assets file project.assets.json not found</span></span>

<span data-ttu-id="2c473-138">Pełny komunikat:</span><span class="sxs-lookup"><span data-stu-id="2c473-138">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="2c473-139">`project.assets.json` Pliku przechowuje wykresu zależności projektu, gdy w formacie PackageReference zarządzania, który jest używany, aby upewnić się, że wszystkie niezbędne pakiety są zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="2c473-139">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="2c473-140">Ponieważ ten plik jest generowany dynamicznie za pośrednictwem Przywracanie pakietu, zwykle nie został dodany do kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="2c473-140">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="2c473-141">W związku z tym, że ten błąd występuje podczas kompilowania projektu za pomocą narzędzia, takie jak `msbuild` który nie automatycznie przywrócić pakiety.</span><span class="sxs-lookup"><span data-stu-id="2c473-141">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="2c473-142">W takim przypadku uruchom `msbuild /t:restore` następuje `msbuild`, lub użyj `dotnet build` (co spowoduje przywrócenie pakietów automatycznie).</span><span class="sxs-lookup"><span data-stu-id="2c473-142">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="2c473-143">Można również użyć dowolnej z metod przywracania pakietu w [poprzedniej sekcji](#missing).</span><span class="sxs-lookup"><span data-stu-id="2c473-143">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="2c473-144">Konieczne jest przywrócenie co najmniej jednego pakietu NuGet, ale nie może być, ponieważ nie udzielono zgody</span><span class="sxs-lookup"><span data-stu-id="2c473-144">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="2c473-145">Pełny komunikat:</span><span class="sxs-lookup"><span data-stu-id="2c473-145">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="2c473-146">Ten błąd wskazuje, że to, że Przywracanie pakietu jest wyłączone w konfiguracji programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="2c473-146">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="2c473-147">Można zmienić odpowiednich ustawień w programie Visual Studio, jak opisano wcześniej w [szybkie rozwiązanie dla użytkowników programu Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="2c473-147">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="2c473-148">Można również edytować tych ustawień bezpośrednio w odpowiednich `nuget.config` pliku (zazwyczaj `%AppData%\NuGet\NuGet.Config` w systemie Windows i `~/.nuget/NuGet/NuGet.Config` na system Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="2c473-148">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="2c473-149">Upewnij się, że `enabled` i `automatic` kluczy w obszarze `packageRestore` są ustawione na wartość True:</span><span class="sxs-lookup"><span data-stu-id="2c473-149">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="2c473-150">Po zmodyfikowaniu `packageRestore` ustawienia bezpośrednio w `nuget.config`, uruchom ponownie program Visual Studio, opcje — Okno dialogowe zawiera bieżące wartości.</span><span class="sxs-lookup"><span data-stu-id="2c473-150">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="2c473-151">Inne potencjalne warunki</span><span class="sxs-lookup"><span data-stu-id="2c473-151">Other potential conditions</span></span>

- <span data-ttu-id="2c473-152">Mogą wystąpić błędy kompilacji z powodu braku plików z komunikat z informacją, użyj polecenia NuGet restore, aby je pobrać.</span><span class="sxs-lookup"><span data-stu-id="2c473-152">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="2c473-153">Jednak Uruchamianie przywracania może powiedzieć "wszystkie pakiety są już zainstalowane i nie ma niczego do przywrócenia."</span><span class="sxs-lookup"><span data-stu-id="2c473-153">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="2c473-154">W takim przypadku usuń `packages` folder (przy użyciu `packages.config`) lub `obj/project.assets.json` plików (w przypadku używania PackageReference) i uruchom ponownie przywracania.</span><span class="sxs-lookup"><span data-stu-id="2c473-154">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="2c473-155">Jeśli błąd będzie nadal występować, użyj `nuget locals all -clear` lub `dotnet locals all --clear` z poziomu wiersza polecenia, aby wyczyścić *globalne pakiety* i pamięci podręcznej folderów, zgodnie z opisem na [Zarządzanie globalne pakietów i pamięci podręcznej folderów](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="2c473-155">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="2c473-156">Podczas uzyskiwania projektu z kontroli źródła, folderów projektu może być równa tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="2c473-156">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="2c473-157">Zmień uprawnienia do folderu i spróbuj ponownie przywrócić pakiety.</span><span class="sxs-lookup"><span data-stu-id="2c473-157">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="2c473-158">Korzystasz z starsza wersja programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="2c473-158">You may be using an old version of NuGet.</span></span> <span data-ttu-id="2c473-159">Sprawdź [nuget.org/downloads](https://www.nuget.org/downloads) najnowsze zalecane wersji.</span><span class="sxs-lookup"><span data-stu-id="2c473-159">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="2c473-160">Dla programu Visual Studio 2015 zaleca się 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="2c473-160">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="2c473-161">Jeśli występują inne problemy [pliku problemu w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , możemy więcej informacji można uzyskać od użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2c473-161">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>