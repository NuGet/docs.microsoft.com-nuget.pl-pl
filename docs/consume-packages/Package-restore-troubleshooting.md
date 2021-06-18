---
title: Rozwiązywanie problemów z przywracaniem pakietów NuGet w Visual Studio
description: Opis typowych błędów przywracania nuGet w Visual Studio i sposoby ich rozwiązywania.
author: JonDouglas
ms.author: jodou
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 0bd14104695a15d2e4c65a13b271143809c4ba8a
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323625"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="8f6cc-103">Rozwiązywanie problemów z błędami przywracania pakietów</span><span class="sxs-lookup"><span data-stu-id="8f6cc-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="8f6cc-104">Ten artykuł koncentruje się na typowych błędach podczas przywracania pakietów i krokach ich rozwiązywania.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="8f6cc-105">Przywracanie pakietu próbuje zainstalować wszystkie zależności pakietu do prawidłowego stanu zgodnego z odwołaniami do pakietu w pliku projektu *(csproj)* lub w *packages.config* pliku.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="8f6cc-106">(W Visual Studio odwołania są wyświetlane w Eksplorator rozwiązań w obszarze **Zależności \ NuGet** lub w **węźle Odwołania).** Aby wykonać kroki wymagane do przywrócenia pakietów, zobacz [Przywracanie pakietów](../consume-packages/package-restore.md#restore-packages).</span><span class="sxs-lookup"><span data-stu-id="8f6cc-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="8f6cc-107">Jeśli odwołania do pakietu w pliku projektu *(csproj)* lub w pliku *packages.config* są nieprawidłowe (nie są zgodne z żądanym stanem po przywróceniu pakietu), należy zainstalować lub zaktualizować pakiety zamiast korzystać z funkcji przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="8f6cc-108">Jeśli instrukcje w tym miejscu nie działają, prosimy o slicie problemu w usłudze [GitHub,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) abyśmy dokładniej zbadali Twój scenariusz.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="8f6cc-109">Nie używaj strony "Czy ta strona jest pomocna?"</span><span class="sxs-lookup"><span data-stu-id="8f6cc-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="8f6cc-110">możesz kontrolować, która może pojawić się na tej stronie, ponieważ nie daje nam możliwości skontaktowania się z Tobą w celu uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="8f6cc-111">Szybkie rozwiązanie dla Visual Studio użytkowników</span><span class="sxs-lookup"><span data-stu-id="8f6cc-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="8f6cc-112">Jeśli używasz usługi Visual Studio najpierw włącz przywracanie pakietu w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="8f6cc-113">W przeciwnym razie przejdź do kolejnych sekcji.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="8f6cc-114">Wybierz polecenie **menu Narzędzia > NuGet Menedżer pakietów > Menedżer pakietów Ustawienia.**</span><span class="sxs-lookup"><span data-stu-id="8f6cc-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="8f6cc-115">Ustaw obie opcje w obszarze **Przywracanie pakietu.**</span><span class="sxs-lookup"><span data-stu-id="8f6cc-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="8f6cc-116">Wybierz przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-116">Select **OK**.</span></span>
1. <span data-ttu-id="8f6cc-117">Skompilowanie projektu ponownie.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-117">Build your project again.</span></span>

![Włączanie przywracania pakietów NuGet w narzędziu/opcjach](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="8f6cc-119">Te ustawienia można również zmienić w `NuGet.Config` pliku. Zobacz [sekcję wyrażania](#consent) zgody.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-119">These settings can also be changed in your `NuGet.Config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="8f6cc-120">Jeśli projekt jest starszym projektem, który używa przywracania pakietów zintegrowanych z programem MSBuild, może być konieczne przeprowadzenie [migracji](package-restore.md#migrate-to-automatic-package-restore-visual-studio) do automatycznego przywracania pakietu.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="8f6cc-121">Ten projekt odwołuje się do pakietów NuGet, których brakuje na tym komputerze</span><span class="sxs-lookup"><span data-stu-id="8f6cc-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="8f6cc-122">Pełny komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="8f6cc-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="8f6cc-123">Ten błąd występuje podczas próby skompilowania projektu zawierającego odwołania do co najmniej jednego pakietu NuGet, ale te pakiety nie są obecnie zainstalowane na komputerze ani w projekcie.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="8f6cc-124">W przypadku korzystania z formatu [zarządzania PackageReference](package-references-in-project-files.md) ten błąd może być pozostawiony po migracji [](/nuget/resources/nuget-faq#working-with-packages) z packages.config do packageReference i musi zostać ręcznie usunięty z pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-124">When using the [PackageReference](package-references-in-project-files.md) management format, this error might be a leftover from a packages.config to PackageReference migration and needs to be [manually removed](/nuget/resources/nuget-faq#working-with-packages) from the project file.</span></span>
- <span data-ttu-id="8f6cc-125">W przypadku [packages.config](../reference/packages-config.md)błąd oznacza, że pakiet nie jest zainstalowany w `packages` folderze w katalogu głównym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="8f6cc-126">Taka sytuacja często występuje, gdy uzyskujesz kod źródłowy projektu z kontroli źródła lub innego pliku do pobrania.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="8f6cc-127">Pakiety są zwykle pomijane podczas kontroli źródła lub pobierania, ponieważ można je przywrócić ze źródeł danych pakietów, takich jak nuget.org (zobacz [Pakiety i kontrola źródła).](Packages-and-Source-Control.md)</span><span class="sxs-lookup"><span data-stu-id="8f6cc-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="8f6cc-128">W przeciwnym razie ich uwzględnienie wywłaszczyłoby repozytorium lub niepotrzebnie duże pliki .zip plików.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="8f6cc-129">Ten błąd może również wystąpić, jeśli plik projektu zawiera ścieżki bezwzględne do lokalizacji pakietu i przeniesiesz projekt.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="8f6cc-130">Aby przywrócić pakiety, użyj jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="8f6cc-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="8f6cc-131">Jeśli plik projektu został przeniesiony, edytuj go bezpośrednio, aby zaktualizować odwołania do pakietu.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="8f6cc-132">[Visual Studio](package-restore.md#restore-using-visual-studio) [(przywracanie automatyczne lub](package-restore.md#restore-packages-automatically-using-visual-studio) przywracanie [ręczne)](package-restore.md#restore-packages-manually-using-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="8f6cc-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="8f6cc-133">Interfejs wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="8f6cc-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="8f6cc-134">Interfejs wiersza polecenia nuget.exe</span><span class="sxs-lookup"><span data-stu-id="8f6cc-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="8f6cc-135">MSBuild</span><span class="sxs-lookup"><span data-stu-id="8f6cc-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="8f6cc-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="8f6cc-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="8f6cc-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="8f6cc-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="8f6cc-138">Po pomyślnym przywróceniu pakiet powinien być obecny w *folderze global-packages.*</span><span class="sxs-lookup"><span data-stu-id="8f6cc-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="8f6cc-139">W przypadku projektów korzystających z funkcji PackageReference przywracanie powinno ponownie utworzyć plik. W przypadku projektów korzystających z funkcji pakiet powinien pojawić się w `obj/project.assets.json` `packages.config` `packages` folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="8f6cc-140">Projekt powinien teraz zostać pomyślnie skompilowany.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-140">The project should now build successfully.</span></span> <span data-ttu-id="8f6cc-141">Jeśli tak nie [jest, w usłudze GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) należy utworzyć plik problemu, abyśmy z To użytkownikiem nas obserwowali.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="8f6cc-142">Plik zasobów project.assets.jsnie znaleziono</span><span class="sxs-lookup"><span data-stu-id="8f6cc-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="8f6cc-143">Pełny komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="8f6cc-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="8f6cc-144">Plik zachowuje wykres zależności projektu w przypadku korzystania z formatu zarządzania PackageReference, który służy do upewnienia się, że wszystkie niezbędne pakiety są `project.assets.json` zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="8f6cc-145">Ponieważ ten plik jest generowany dynamicznie za pomocą przywracania pakietu, zazwyczaj nie jest dodawany do kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="8f6cc-146">W związku z tym ten błąd występuje podczas budowania projektu za pomocą narzędzia takiego jak , które `msbuild` nie przywraca automatycznie pakietów.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="8f6cc-147">W takim przypadku uruchom , `msbuild -t:restore` a następnie , lub użyj funkcji `msbuild` `dotnet build` (co spowoduje automatyczne przywrócenie pakietów).</span><span class="sxs-lookup"><span data-stu-id="8f6cc-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="8f6cc-148">Możesz również użyć dowolnej metody przywracania pakietów z [poprzedniej sekcji](#missing).</span><span class="sxs-lookup"><span data-stu-id="8f6cc-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="8f6cc-149">Co najmniej jeden pakiet NuGet musi zostać przywrócony, ale nie można go przywrócić, ponieważ nie udzielono zgody</span><span class="sxs-lookup"><span data-stu-id="8f6cc-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="8f6cc-150">Pełny komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="8f6cc-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="8f6cc-151">Ten błąd wskazuje, że przywracanie pakietu jest wyłączone w konfiguracji nuGet.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="8f6cc-152">Odpowiednie ustawienia można zmienić w programie Visual Studio jak opisano wcześniej w obszarze Szybkie [rozwiązanie dla Visual Studio użytkowników.](#quick-solution-for-visual-studio-users)</span><span class="sxs-lookup"><span data-stu-id="8f6cc-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="8f6cc-153">Te ustawienia można również edytować bezpośrednio w odpowiednich plikach (zazwyczaj w systemie `nuget.config` `%AppData%\NuGet\NuGet.Config` Windows i na `~/.nuget/NuGet/NuGet.Config` komputerach Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="8f6cc-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="8f6cc-154">Upewnij się, `enabled` że klucze i w obszarze są ustawione na wartość `automatic` `packageRestore` True:</span><span class="sxs-lookup"><span data-stu-id="8f6cc-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="8f6cc-155">Jeśli edytujesz ustawienia bezpośrednio w programie , uruchom Visual Studio, aby w oknie dialogowym opcji `packageRestore` `nuget.config` wyświetlane są bieżące wartości.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="8f6cc-156">Inne potencjalne warunki</span><span class="sxs-lookup"><span data-stu-id="8f6cc-156">Other potential conditions</span></span>

- <span data-ttu-id="8f6cc-157">Mogą wystąpić błędy kompilacji z powodu braku plików z komunikatem o użyciu przywracania NuGet w celu ich pobrania.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="8f6cc-158">Jednak uruchomienie przywracania może powiedzieć "Wszystkie pakiety są już zainstalowane i nie ma nic do przywrócenia".</span><span class="sxs-lookup"><span data-stu-id="8f6cc-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="8f6cc-159">W takim przypadku usuń folder (w przypadku używania funkcji ) lub pliku (w przypadku korzystania z `packages` `packages.config` `obj/project.assets.json` packageReference) i uruchom przywracanie ponownie.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="8f6cc-160">Jeśli błąd będzie nadal występował, użyj polecenia lub z wiersza polecenia, aby wyczyścić globalne pakiety i foldery pamięci podręcznej zgodnie z opisem w tece Zarządzanie globalnymi pakietami i folderami `nuget locals all -clear` `dotnet nuget locals all --clear` pamięci [podręcznej](managing-the-global-packages-and-cache-folders.md). </span><span class="sxs-lookup"><span data-stu-id="8f6cc-160">If the error still persists, use `nuget locals all -clear` or `dotnet nuget locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="8f6cc-161">Podczas uzyskiwania projektu z kontroli źródła foldery projektu mogą być ustawione na tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="8f6cc-162">Zmień uprawnienia folderu i spróbuj ponownie przywrócić pakiety.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="8f6cc-163">Być może używasz starej wersji pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="8f6cc-164">Sprawdź [nuget.org/downloads](https://www.nuget.org/downloads) najnowsze zalecane wersje.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="8f6cc-165">W Visual Studio 2015 r. zalecamy korzystanie z 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="8f6cc-166">Jeśli napotkasz inne problemy, [zamów problem w usłudze GitHub,](https://github.com/NuGet/docs.microsoft.com-nuget/issues) aby uzyskać więcej szczegółów od Ciebie.</span><span class="sxs-lookup"><span data-stu-id="8f6cc-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
