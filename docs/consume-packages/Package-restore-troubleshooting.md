---
title: Rozwiązywanie problemów z przywracaniem pakietu NuGet w programie Visual Studio
description: Opis typowych błędów przywracania NuGet w programie Visual Studio i jak je rozwiązać.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: a1f9f1d03e9a6e58466fa92426bd655d5e8ed83d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860623"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="d4b7e-103">Rozwiązywanie problemów z błędami przywracania pakietu</span><span class="sxs-lookup"><span data-stu-id="d4b7e-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="d4b7e-104">W tym artykule koncentruje się na typowych błędów podczas przywracania pakietów i kroki, aby je rozwiązać.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="d4b7e-105">Narzędzie Package Restore próbuje zainstalować wszystkie zależności pakietów do prawidłowego stanu odpowiadającego odwołaniom do pakietu w pliku projektu (*.csproj*) lub pliku *packages.config.*</span><span class="sxs-lookup"><span data-stu-id="d4b7e-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="d4b7e-106">(W programie Visual Studio odwołania są wyświetlane w Eksploratorze rozwiązań w obszarze **zależności \ NuGet** lub węźle **Odwołania).** Aby wykonać wymagane kroki w celu przywrócenia pakietów, zobacz [Przywracanie pakietów](../consume-packages/package-restore.md#restore-packages).</span><span class="sxs-lookup"><span data-stu-id="d4b7e-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="d4b7e-107">Jeśli odwołania do pakietu w pliku projektu *(csproj)* lub pliku *packages.config* są niepoprawne (nie pasują do żądanego stanu po przywróceniu pakietu), należy zainstalować lub zaktualizować pakiety zamiast przywracania pakietu.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="d4b7e-108">Jeśli instrukcje w tym miejscu nie działają dla Ciebie, [zgłoś problem na GitHub,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) abyśmy mogli dokładniej zbadać twój scenariusz.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="d4b7e-109">Nie używaj "Czy ta strona jest pomocna?"</span><span class="sxs-lookup"><span data-stu-id="d4b7e-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="d4b7e-110">kontroli, która może pojawić się na tej stronie, ponieważ nie daje nam możliwości skontaktowania się z Tobą w celu uzyskania więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="d4b7e-111">Szybkie rozwiązanie dla użytkowników programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4b7e-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="d4b7e-112">Jeśli używasz programu Visual Studio, najpierw włącz przywracanie pakietu w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="d4b7e-113">W przeciwnym razie przejdź do sekcji, które następują.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="d4b7e-114">Wybierz polecenie menu **Narzędzia > Menedżera pakietów NuGet > Ustawienia Menedżera pakietów.**</span><span class="sxs-lookup"><span data-stu-id="d4b7e-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="d4b7e-115">Ustaw obie opcje w obszarze **Przywracanie pakietu**.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="d4b7e-116">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-116">Select **OK**.</span></span>
1. <span data-ttu-id="d4b7e-117">Zbuduj swój projekt ponownie.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-117">Build your project again.</span></span>

![Włącz przywracanie pakietu NuGet w narzędziu/opcjach](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="d4b7e-119">Te ustawienia można również `NuGet.config` zmienić w pliku; patrz sekcja [zgody.](#consent)</span><span class="sxs-lookup"><span data-stu-id="d4b7e-119">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="d4b7e-120">Jeśli projekt jest starszy projekt, który używa msbuild zintegrowane przywracanie pakietu, może być konieczne [migracji](package-restore.md#migrate-to-automatic-package-restore-visual-studio) do automatycznego przywracania pakietu.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="d4b7e-121">Ten projekt odwołuje się do pakietów NuGet, których brakuje na tym komputerze</span><span class="sxs-lookup"><span data-stu-id="d4b7e-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="d4b7e-122">Pełny komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="d4b7e-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="d4b7e-123">Ten błąd występuje podczas próby utworzenia projektu, który zawiera odwołania do jednego lub więcej pakietów NuGet, ale te pakiety nie są obecnie zainstalowane na komputerze lub w projekcie.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="d4b7e-124">Podczas korzystania z formatu zarządzania [PackageReference](package-references-in-project-files.md) błąd oznacza, że pakiet nie jest zainstalowany w folderze *pakietów globalnych,* zgodnie z opisem w [sprawie Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="d4b7e-124">When using the [PackageReference](package-references-in-project-files.md) management format, the error means that the package is not installed in the *global-packages* folder as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="d4b7e-125">Podczas korzystania z [packages.config,](../reference/packages-config.md)błąd oznacza, że `packages` pakiet nie jest zainstalowany w folderze w katalogu głównym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="d4b7e-126">Ta sytuacja często występuje po uzyskaniu kodu źródłowego projektu z kontroli źródła lub innego pobrania.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="d4b7e-127">Pakiety są zazwyczaj pomijane w kontroli źródła lub pobiera, ponieważ można je przywrócić z kanałów pakietowych, takich jak nuget.org (patrz [Pakiety i kontrola źródła).](Packages-and-Source-Control.md)</span><span class="sxs-lookup"><span data-stu-id="d4b7e-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="d4b7e-128">Włączenie ich w przeciwnym razie nadęłoby repozytorium lub stworzyłoby niepotrzebnie duże pliki .zip.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="d4b7e-129">Błąd może również się zdarzyć, jeśli plik projektu zawiera ścieżki bezwzględne do lokalizacji pakietów i przenieść projekt.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="d4b7e-130">Aby przywrócić pakiety, użyj jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="d4b7e-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="d4b7e-131">Jeśli plik projektu został przeniesiony, edytuj plik bezpośrednio, aby zaktualizować odwołania do pakietu.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="d4b7e-132">[Visual Studio](package-restore.md#restore-using-visual-studio) [(automatyczne przywracanie](package-restore.md#restore-packages-automatically-using-visual-studio) lub [ręczne przywracanie)](package-restore.md#restore-packages-manually-using-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="d4b7e-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="d4b7e-133">Interfejs wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="d4b7e-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="d4b7e-134">Interfejs wiersza polecenia nuget.exe</span><span class="sxs-lookup"><span data-stu-id="d4b7e-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="d4b7e-135">MSBuild</span><span class="sxs-lookup"><span data-stu-id="d4b7e-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="d4b7e-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="d4b7e-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="d4b7e-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="d4b7e-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="d4b7e-138">Po pomyślnym przywróceniu pakiet powinien znajdować się w folderze *pakietów globalnych.*</span><span class="sxs-lookup"><span data-stu-id="d4b7e-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="d4b7e-139">W przypadku projektów przy użyciu PackageReference `obj/project.assets.json` przywracanie należy ponownie utworzyć plik; w przypadku `packages.config`projektów korzystających z pakietu `packages` powinien pojawić się w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="d4b7e-140">Projekt powinien teraz pomyślnie zbudować.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-140">The project should now build successfully.</span></span> <span data-ttu-id="d4b7e-141">Jeśli nie, [zgłaś problem na GitHub,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) abyśmy mogli z Tobą śledzić.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="d4b7e-142">Nie znaleziono pliku zasobów project.assets.json</span><span class="sxs-lookup"><span data-stu-id="d4b7e-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="d4b7e-143">Pełny komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="d4b7e-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="d4b7e-144">Plik `project.assets.json` przechowuje wykres zależności projektu podczas korzystania z formatu zarządzania PackageReference, który jest używany, aby upewnić się, że wszystkie niezbędne pakiety są zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="d4b7e-145">Ponieważ ten plik jest generowany dynamicznie za pomocą przywracania pakietu, zazwyczaj nie jest dodawany do kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="d4b7e-146">W rezultacie ten błąd występuje podczas tworzenia projektu `msbuild` za pomocą narzędzia, takiego jak to nie automatycznie przywraca pakiety.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="d4b7e-147">W takim przypadku `msbuild -t:restore` uruchom, a następnie `msbuild`, lub użyj `dotnet build` (który automatycznie przywraca pakiety).</span><span class="sxs-lookup"><span data-stu-id="d4b7e-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="d4b7e-148">Można również użyć dowolnej z metod przywracania pakietu w [poprzedniej sekcji](#missing).</span><span class="sxs-lookup"><span data-stu-id="d4b7e-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="d4b7e-149">Jeden lub więcej pakietów NuGet musi zostać przywrócony, ale nie może być, ponieważ zgoda nie została udzielona</span><span class="sxs-lookup"><span data-stu-id="d4b7e-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="d4b7e-150">Pełny komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="d4b7e-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="d4b7e-151">Ten błąd wskazuje, że przywracanie pakietu jest wyłączone w konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="d4b7e-152">Odpowiednie ustawienia w programie Visual Studio można zmienić w sposób opisany wcześniej w obszarze [Szybkie rozwiązanie dla użytkowników programu Visual Studio.](#quick-solution-for-visual-studio-users)</span><span class="sxs-lookup"><span data-stu-id="d4b7e-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="d4b7e-153">Można również edytować te ustawienia `nuget.config` bezpośrednio w `%AppData%\NuGet\NuGet.Config` odpowiednim pliku `~/.nuget/NuGet/NuGet.Config` (zazwyczaj w systemie Windows i mac/linux).</span><span class="sxs-lookup"><span data-stu-id="d4b7e-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="d4b7e-154">Upewnij `enabled` się, `automatic` że `packageRestore` klawisze i w obszarze są ustawione na True:</span><span class="sxs-lookup"><span data-stu-id="d4b7e-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="d4b7e-155">Jeśli `packageRestore` ustawienia są edytowane `nuget.config`bezpośrednio w programie , uruchom ponownie program Visual Studio, aby okno dialogowe opcji wyświetlał bieżące wartości.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="d4b7e-156">Inne potencjalne warunki</span><span class="sxs-lookup"><span data-stu-id="d4b7e-156">Other potential conditions</span></span>

- <span data-ttu-id="d4b7e-157">Mogą wystąpić błędy kompilacji z powodu brakujących plików, z komunikatem informującym o użyciu przywracania NuGet, aby je pobrać.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="d4b7e-158">Jednak uruchomienie przywracania może powiedzieć: "Wszystkie pakiety są już zainstalowane i nie ma nic do przywrócenia."</span><span class="sxs-lookup"><span data-stu-id="d4b7e-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="d4b7e-159">W takim przypadku `packages` usuń folder `packages.config`(podczas `obj/project.assets.json` korzystania) lub plik (podczas korzystania z PackageReference) i uruchom przywracanie ponownie.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="d4b7e-160">Jeśli błąd nadal występuje, `nuget locals all -clear` `dotnet locals all --clear` użyj lub z wiersza polecenia, aby wyczyścić *globalne pakiety* i foldery pamięci podręcznej, zgodnie z opisem w [temacie Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="d4b7e-160">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="d4b7e-161">Podczas uzyskiwania projektu z kontroli źródła, foldery projektu mogą być ustawione na tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="d4b7e-162">Zmień uprawnienia do folderu i spróbuj przywrócić pakiety ponownie.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="d4b7e-163">Być może używasz starej wersji NuGet.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="d4b7e-164">Sprawdź [nuget.org/downloads,](https://www.nuget.org/downloads) czy dostępne są najnowsze zalecane wersje.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="d4b7e-165">Dla programu Visual Studio 2015 zaleca się 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="d4b7e-166">Jeśli napotkasz inne problemy, [zgładź problem do GitHub,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) abyśmy mogli uzyskać więcej szczegółów od Ciebie.</span><span class="sxs-lookup"><span data-stu-id="d4b7e-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
