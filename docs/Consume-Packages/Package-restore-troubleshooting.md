---
title: "Rozwiązywanie problemów z pakietu NuGet przywracania w programie Visual Studio | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Opis wspólnej NuGet Przywracanie błędy w Visual Studio i sposoby ich rozwiązywania."
keywords: "Przywracanie pakietu NuGet, przywracanie pakietów, rozwiązywania problemów, rozwiązywanie problemów"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="9e834-104">Rozwiązywanie problemów z błędami przywracania pakietu</span><span class="sxs-lookup"><span data-stu-id="9e834-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="9e834-105">Ten artykuł dotyczy typowe błędy podczas przywracania pakietów i sposobów ich rozwiązywania.</span><span class="sxs-lookup"><span data-stu-id="9e834-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="9e834-106">Aby uzyskać szczegółowe informacje dotyczące przywracania pakietów, zobacz [Przywracanie pakietu](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="9e834-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="9e834-107">Jeśli poniższe instrukcje nie działają, [Zgłoś problem w usłudze GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) tak, aby firma Microsoft bada danego scenariusza bardziej dokładnie.</span><span class="sxs-lookup"><span data-stu-id="9e834-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="9e834-108">Nie używaj "warto tę stronę?"</span><span class="sxs-lookup"><span data-stu-id="9e834-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="9e834-109">formant, który może występować na tej stronie, ponieważ go nie dają nam możliwość się z Tobą, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="9e834-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="9e834-110">Szybkie rozwiązanie dla użytkowników programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e834-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="9e834-111">Jeśli używasz programu Visual Studio, najpierw włączyć Przywracanie pakietu w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="9e834-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="9e834-112">W przeciwnym razie nadal w kolejnych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="9e834-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="9e834-113">Wybierz **Narzędzia > Menedżera pakietów NuGet > Ustawienia Menedżera pakietów** polecenia menu.</span><span class="sxs-lookup"><span data-stu-id="9e834-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="9e834-114">Ustaw obie opcje w obszarze **przywracania pakietów**.</span><span class="sxs-lookup"><span data-stu-id="9e834-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="9e834-115">Wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e834-115">Select **OK**.</span></span>
1. <span data-ttu-id="9e834-116">Skompiluj projekt ponownie.</span><span class="sxs-lookup"><span data-stu-id="9e834-116">Build your project again.</span></span>

![Włącz Przywracanie pakietu NuGet w narzędzia/Opcje](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="9e834-118">Te ustawienia można zmienić w Twojej `NuGet.config` pliku; zobacz [zgody](#consent) sekcji.</span><span class="sxs-lookup"><span data-stu-id="9e834-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="9e834-119">Ten projekt zawiera odwołania do pakietów NuGet Brak na tym komputerze</span><span class="sxs-lookup"><span data-stu-id="9e834-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="9e834-120">Pełny komunikat:</span><span class="sxs-lookup"><span data-stu-id="9e834-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="9e834-121">Ten błąd występuje przystąpieniem do tworzenia projektu, który zawiera odwołania do co najmniej jednego pakietu NuGet, ale pakiety nie są obecnie buforowane w projekcie.</span><span class="sxs-lookup"><span data-stu-id="9e834-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently cached in the project.</span></span> <span data-ttu-id="9e834-122">(Pakiety są buforowane w `packages` folder w katalogu głównym rozwiązanie, jeśli projekt używa `packages.config`, lub `obj/project.assets.json` plik, jeśli projekt używa formatu PackageReference.)</span><span class="sxs-lookup"><span data-stu-id="9e834-122">(Packages are cached in a `packages` folder at the solution root if the project uses `packages.config`, or in the `obj/project.assets.json` file if the project uses the PackageReference format.)</span></span>

<span data-ttu-id="9e834-123">Taka sytuacja często występuje, gdy uzyskać kod źródłowy projektu z kontroli źródła lub innego pobierania.</span><span class="sxs-lookup"><span data-stu-id="9e834-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="9e834-124">Pakiety są zwykle pominięto z kontroli źródła lub pliki do pobrania, ponieważ pliki mogą zostać przywrócone z pakietu źródeł danych, takich jak nuget.org (zobacz [pakietów i kontroli źródła](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="9e834-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="9e834-125">Włączenie ich w przeciwnym razie będzie wybrzuszanie repozytorium lub Utwórz plików zip niepotrzebnie.</span><span class="sxs-lookup"><span data-stu-id="9e834-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="9e834-126">Użyj jednej z następujących metod w celu przywrócenia pakietów:</span><span class="sxs-lookup"><span data-stu-id="9e834-126">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="9e834-127">W programie Visual Studio, Włącz Przywracanie pakietu po wybraniu **Narzędzia > Menedżera pakietów NuGet > Ustawienia Menedżera pakietów** polecenia menu, ustawianie obu opcji w obszarze **przywracania pakietów**i wybierając  **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e834-127">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="9e834-128">Następnie ponownie skompiluj rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="9e834-128">Then build the solution again.</span></span>
- <span data-ttu-id="9e834-129">Projekty platformy .NET Core, uruchom `dotnet restore` lub `dotnet build` (automatycznie uruchamia przywracania).</span><span class="sxs-lookup"><span data-stu-id="9e834-129">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="9e834-130">W wierszu polecenia Uruchom `nuget restore` (z wyjątkiem projektów utworzonych za pomocą `dotnet`, w którym to przypadku użycia `dotnet restore`).</span><span class="sxs-lookup"><span data-stu-id="9e834-130">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="9e834-131">W wierszu polecenia z projektami przy użyciu formatu PackageReference Uruchom `msbuild /t:restore`.</span><span class="sxs-lookup"><span data-stu-id="9e834-131">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="9e834-132">Po pomyślnym przywracania, powinna zostać wyświetlona albo `packages` folder (przy użyciu `packages.config`) lub `obj/project.assets.json` plików (w przypadku używania PackageReference).</span><span class="sxs-lookup"><span data-stu-id="9e834-132">After a successful restore, you should see either a `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference).</span></span> <span data-ttu-id="9e834-133">Projekt powinien teraz kompilacji pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="9e834-133">The project should now build successfully.</span></span> <span data-ttu-id="9e834-134">Jeśli nie, [pliku problemu w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , firma Microsoft możesz skomunikować się z Tobą.</span><span class="sxs-lookup"><span data-stu-id="9e834-134">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="9e834-135">Nie można odnaleźć project.assets.json pliku zasobów</span><span class="sxs-lookup"><span data-stu-id="9e834-135">Assets file project.assets.json not found</span></span>

<span data-ttu-id="9e834-136">Pełny komunikat:</span><span class="sxs-lookup"><span data-stu-id="9e834-136">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="9e834-137">Ten błąd występuje z powodów zgodnie z objaśnieniem w [poprzedniej sekcji](#missing), i ma takie same środki zaradcze.</span><span class="sxs-lookup"><span data-stu-id="9e834-137">This error occurs for the same reasons as explained in the [previous section](#missing), and has the same remedies.</span></span> <span data-ttu-id="9e834-138">Na przykład uruchomiona `msbuild` na .NET Core projektu został uzyskany z kontroli źródła nie będzie automatycznie przywrócić pakiety.</span><span class="sxs-lookup"><span data-stu-id="9e834-138">For example, running `msbuild` on a .NET Core project that's been obtained from source control won't automatically restore packages.</span></span> <span data-ttu-id="9e834-139">W takim przypadku uruchom `msbuild /t:restore` następuje `msbuild`, lub użyj `dotnet build` (co spowoduje przywrócenie pakietów automatycznie).</span><span class="sxs-lookup"><span data-stu-id="9e834-139">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="9e834-140">Konieczne jest przywrócenie co najmniej jednego pakietu NuGet, ale nie może być, ponieważ nie udzielono zgody</span><span class="sxs-lookup"><span data-stu-id="9e834-140">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="9e834-141">Pełny komunikat:</span><span class="sxs-lookup"><span data-stu-id="9e834-141">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="9e834-142">Ten błąd wskazuje, że to, że Przywracanie pakietu jest wyłączone w konfiguracji programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="9e834-142">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="9e834-143">Można zmienić odpowiednich ustawień w programie Visual Studio, jak opisano wcześniej w [szybkie rozwiązanie dla użytkowników programu Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="9e834-143">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="9e834-144">Można również edytować tych ustawień bezpośrednio w odpowiednich `nuget.config` pliku (zazwyczaj `%AppData%\NuGet\NuGet.Config` w systemie Windows i `~/.nuget/NuGet/NuGet.Config` na system Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="9e834-144">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="9e834-145">Upewnij się, że `enabled` i `automatic` kluczy w obszarze `packageRestore` są ustawione na wartość True:</span><span class="sxs-lookup"><span data-stu-id="9e834-145">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="9e834-146">Należy pamiętać, że po zmodyfikowaniu `packageRestore` ustawienia bezpośrednio w `nuget.config`, uruchom ponownie program Visual Studio, opcje — Okno dialogowe zawiera bieżące wartości.</span><span class="sxs-lookup"><span data-stu-id="9e834-146">Note that if you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="9e834-147">Inne potencjalne warunki</span><span class="sxs-lookup"><span data-stu-id="9e834-147">Other potential conditions</span></span>

- <span data-ttu-id="9e834-148">Mogą wystąpić błędy kompilacji z powodu braku plików z komunikat z informacją, użyj polecenia NuGet restore, aby je pobrać.</span><span class="sxs-lookup"><span data-stu-id="9e834-148">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="9e834-149">Jednak Uruchamianie przywracania może powiedzieć "wszystkie pakiety są już zainstalowane i nie ma niczego do przywrócenia."</span><span class="sxs-lookup"><span data-stu-id="9e834-149">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="9e834-150">W takim przypadku usuń `packages` folder (przy użyciu `packages.config`) lub `obj/project.assets.json` plików (w przypadku używania PackageReference) i uruchom ponownie przywracania.</span><span class="sxs-lookup"><span data-stu-id="9e834-150">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span>

- <span data-ttu-id="9e834-151">Podczas uzyskiwania projektu z kontroli źródła, folderów projektu może być równa tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="9e834-151">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="9e834-152">Zmień uprawnienia do folderu i spróbuj ponownie przywrócić pakiety.</span><span class="sxs-lookup"><span data-stu-id="9e834-152">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="9e834-153">Korzystasz z starsza wersja programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="9e834-153">You may be using an old version of NuGet.</span></span> <span data-ttu-id="9e834-154">Sprawdź [nuget.org/downloads](https://www.nuget.org/downloads) najnowsze zalecane wersji.</span><span class="sxs-lookup"><span data-stu-id="9e834-154">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="9e834-155">Dla programu Visual Studio 2015 zaleca się 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="9e834-155">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="9e834-156">Jeśli występują inne problemy [pliku problemu w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , możemy więcej informacji można uzyskać od użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9e834-156">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>