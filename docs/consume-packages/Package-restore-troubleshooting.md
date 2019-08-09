---
title: Rozwiązywanie problemów z przywracaniem pakietów NuGet w programie Visual Studio
description: Opis typowych błędów przywracania NuGet w programie Visual Studio i sposoby ich rozwiązywania.
author: karann-msft
ms.author: karann
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: a1f9f1d03e9a6e58466fa92426bd655d5e8ed83d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860623"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="72f11-103">Rozwiązywanie problemów z błędami przywracania pakietu</span><span class="sxs-lookup"><span data-stu-id="72f11-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="72f11-104">Ten artykuł koncentruje się na typowych błędach podczas przywracania pakietów i kroków w celu ich rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="72f11-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="72f11-105">Przywracanie pakietu próbuje zainstalować wszystkie zależności pakietów do poprawnego stanu pasującego do odwołania do pakietu w pliku projektu ( *. csproj*) lub pliku *Packages. config* .</span><span class="sxs-lookup"><span data-stu-id="72f11-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="72f11-106">(W programie Visual Studio odwołania pojawiają się w Eksplorator rozwiązań w obszarze **zależności \ NuGet** lub węzeł **odwołania** ). Aby wykonać kroki wymagane do przywrócenia pakietów, zobacz [przywracanie pakietów](../consume-packages/package-restore.md#restore-packages).</span><span class="sxs-lookup"><span data-stu-id="72f11-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="72f11-107">Jeśli odwołania do pakietu w pliku projektu ( *. csproj*) lub pliku *Packages. config* są nieprawidłowe (nie są zgodne z żądanym stanem po przywróceniu pakietu), należy zainstalować lub zaktualizować pakiety zamiast korzystać z pakietu Przywracania.</span><span class="sxs-lookup"><span data-stu-id="72f11-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="72f11-108">Jeśli instrukcje tego nie zadziałały, należy [rozwiązać problem w usłudze GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , aby dokładniej przeanalizować scenariusz.</span><span class="sxs-lookup"><span data-stu-id="72f11-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="72f11-109">Nie używaj "czy ta strona jest pomocna?"</span><span class="sxs-lookup"><span data-stu-id="72f11-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="72f11-110">kontrolka, która może pojawić się na tej stronie, ponieważ nie daje nam możliwości skontaktowania się z Tobą w celu uzyskania dodatkowych informacji.</span><span class="sxs-lookup"><span data-stu-id="72f11-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="72f11-111">Szybkie rozwiązanie dla użytkowników programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="72f11-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="72f11-112">Jeśli używasz programu Visual Studio, najpierw włącz przywracanie pakietu w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="72f11-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="72f11-113">W przeciwnym razie przejdź do kolejnych sekcji.</span><span class="sxs-lookup"><span data-stu-id="72f11-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="72f11-114">Wybierz polecenie **narzędzia > Menedżer pakietów NuGet > menu Ustawienia Menedżera pakietów** .</span><span class="sxs-lookup"><span data-stu-id="72f11-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="72f11-115">Ustaw obie opcje w obszarze **przywracanie pakietu**.</span><span class="sxs-lookup"><span data-stu-id="72f11-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="72f11-116">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="72f11-116">Select **OK**.</span></span>
1. <span data-ttu-id="72f11-117">Ponownie skompiluj projekt.</span><span class="sxs-lookup"><span data-stu-id="72f11-117">Build your project again.</span></span>

![Włącz przywracanie pakietu NuGet w narzędziu/opcjach](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="72f11-119">Te ustawienia można także zmienić w `NuGet.config` pliku; zapoznaj się z sekcją [zgody](#consent) .</span><span class="sxs-lookup"><span data-stu-id="72f11-119">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="72f11-120">Jeśli projekt jest starszym projektem, który używa przywracania pakietu programu MSBuild, może być konieczne przeprowadzenie [migracji](package-restore.md#migrate-to-automatic-package-restore-visual-studio) do automatycznego przywracania pakietów.</span><span class="sxs-lookup"><span data-stu-id="72f11-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="72f11-121">Ten projekt odwołuje się do pakietów NuGet, których brakuje na tym komputerze</span><span class="sxs-lookup"><span data-stu-id="72f11-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="72f11-122">Pełny komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="72f11-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="72f11-123">Ten błąd występuje podczas próby skompilowania projektu, który zawiera odwołania do co najmniej jednego pakietu NuGet, ale te pakiety nie są obecnie zainstalowane na komputerze ani w projekcie.</span><span class="sxs-lookup"><span data-stu-id="72f11-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="72f11-124">W przypadku korzystania z formatu zarządzania [PackageReference](package-references-in-project-files.md) błąd oznacza, że pakiet nie jest zainstalowany w folderze *globalne pakiety* , zgodnie z opisem w temacie [Zarządzanie pakietami globalnymi i folderami pamięci](managing-the-global-packages-and-cache-folders.md)podręcznej.</span><span class="sxs-lookup"><span data-stu-id="72f11-124">When using the [PackageReference](package-references-in-project-files.md) management format, the error means that the package is not installed in the *global-packages* folder as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>
- <span data-ttu-id="72f11-125">W przypadku korzystania z [Packages. config](../reference/packages-config.md)błąd oznacza, że pakiet nie jest zainstalowany w `packages` folderze w katalogu głównym rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="72f11-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="72f11-126">Ta sytuacja często występuje, gdy uzyskujesz kod źródłowy projektu z kontroli źródła lub innego pobierania.</span><span class="sxs-lookup"><span data-stu-id="72f11-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="72f11-127">Pakiety są zwykle pomijane na podstawie kontroli źródła lub pobierania, ponieważ można je przywrócić ze źródeł danych pakietu, takich jak nuget.org (zobacz [pakiety i kontrola źródła](Packages-and-Source-Control.md)).</span><span class="sxs-lookup"><span data-stu-id="72f11-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="72f11-128">Dołączenie ich w inny sposób przeładowanie repozytorium lub tworzenie niepotrzebnych dużych plików. zip.</span><span class="sxs-lookup"><span data-stu-id="72f11-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="72f11-129">Ten błąd może również wystąpić, jeśli plik projektu zawiera bezwzględne ścieżki do lokalizacji pakietów i przeniesiesz projekt.</span><span class="sxs-lookup"><span data-stu-id="72f11-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="72f11-130">Aby przywrócić pakiety, użyj jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="72f11-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="72f11-131">Jeśli plik projektu został przeniesiony, edytuj go bezpośrednio, aby zaktualizować odwołania do pakietu.</span><span class="sxs-lookup"><span data-stu-id="72f11-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="72f11-132">[Program Visual Studio](package-restore.md#restore-using-visual-studio) ([automatyczne przywracanie](package-restore.md#restore-packages-automatically-using-visual-studio) lub [przywracanie ręczne](package-restore.md#restore-packages-manually-using-visual-studio))</span><span class="sxs-lookup"><span data-stu-id="72f11-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="72f11-133">Interfejs wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="72f11-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="72f11-134">Interfejs wiersza polecenia nuget.exe</span><span class="sxs-lookup"><span data-stu-id="72f11-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="72f11-135">MSBuild</span><span class="sxs-lookup"><span data-stu-id="72f11-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="72f11-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="72f11-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="72f11-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="72f11-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="72f11-138">Po pomyślnym przywróceniu pakiet powinien znajdować się w folderze *Global-Packages* .</span><span class="sxs-lookup"><span data-stu-id="72f11-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="72f11-139">W przypadku projektów korzystających z programu PackageReference przywracanie powinno `obj/project.assets.json` odtworzyć plik. w przypadku projektów używających `packages.config`pakiet powinien `packages` pojawić się w folderze projektu.</span><span class="sxs-lookup"><span data-stu-id="72f11-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="72f11-140">Projekt powinien teraz zostać pomyślnie skompilowany.</span><span class="sxs-lookup"><span data-stu-id="72f11-140">The project should now build successfully.</span></span> <span data-ttu-id="72f11-141">Jeśli nie, Zastąp [problem w usłudze GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , dzięki czemu będziemy mogli z nich skorzystać.</span><span class="sxs-lookup"><span data-stu-id="72f11-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="72f11-142">Nie znaleziono pliku zasobów Project. assets. JSON</span><span class="sxs-lookup"><span data-stu-id="72f11-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="72f11-143">Pełny komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="72f11-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="72f11-144">`project.assets.json` Plik utrzymuje wykres zależności projektu przy użyciu formatu zarządzania PackageReference, który jest używany do upewnienia się, że wszystkie wymagane pakiety są zainstalowane na komputerze.</span><span class="sxs-lookup"><span data-stu-id="72f11-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="72f11-145">Ponieważ ten plik jest generowany dynamicznie przez Przywracanie pakietów, zazwyczaj nie jest dodawany do kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="72f11-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="72f11-146">W związku z tym ten błąd występuje podczas kompilowania projektu za pomocą narzędzia, takiego `msbuild` jak nie przywraca automatycznie pakietów.</span><span class="sxs-lookup"><span data-stu-id="72f11-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="72f11-147">W takim przypadku należy uruchomić `msbuild -t:restore` `msbuild`polecenie, a następnie użyć `dotnet build` (które automatycznie przywraca pakiety).</span><span class="sxs-lookup"><span data-stu-id="72f11-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="72f11-148">Można również użyć dowolnej z metod przywracania pakietów w [poprzedniej sekcji](#missing).</span><span class="sxs-lookup"><span data-stu-id="72f11-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="72f11-149">Należy przywrócić co najmniej jeden pakiet NuGet, ale nie można go z powodu braku zgody</span><span class="sxs-lookup"><span data-stu-id="72f11-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="72f11-150">Pełny komunikat o błędzie:</span><span class="sxs-lookup"><span data-stu-id="72f11-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="72f11-151">Ten błąd wskazuje, że przywracanie pakietu jest wyłączone w konfiguracji programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="72f11-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="72f11-152">Można zmienić odpowiednie ustawienia w programie Visual Studio zgodnie z wcześniejszym opisem w sekcji [szybkie rozwiązanie dla użytkowników programu Visual Studio](#quick-solution-for-visual-studio-users).</span><span class="sxs-lookup"><span data-stu-id="72f11-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="72f11-153">Te ustawienia można również edytować bezpośrednio w odpowiednim `nuget.config` pliku (zazwyczaj `%AppData%\NuGet\NuGet.Config` w systemach Windows i `~/.nuget/NuGet/NuGet.Config` Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="72f11-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="72f11-154">Upewnij się, `enabled` że `automatic` klucze i `packageRestore` w obszarze są ustawione na wartość true:</span><span class="sxs-lookup"><span data-stu-id="72f11-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

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
> <span data-ttu-id="72f11-155">Jeśli edytujesz `packageRestore` ustawienia bezpośrednio w programie `nuget.config`, uruchom ponownie program Visual Studio, aby okno dialogowe Opcje pokazywało bieżące wartości.</span><span class="sxs-lookup"><span data-stu-id="72f11-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="72f11-156">Inne potencjalne warunki</span><span class="sxs-lookup"><span data-stu-id="72f11-156">Other potential conditions</span></span>

- <span data-ttu-id="72f11-157">Błędy kompilacji mogą wystąpić z powodu braku plików, a komunikat informujący o konieczności użycia przywracania NuGet do pobrania.</span><span class="sxs-lookup"><span data-stu-id="72f11-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="72f11-158">Jednak uruchomienie przywracania może powiedzieć, "wszystkie pakiety są już zainstalowane i nie ma niczego do przywrócenia".</span><span class="sxs-lookup"><span data-stu-id="72f11-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="72f11-159">W takim przypadku Usuń `packages` folder (w przypadku używania `packages.config`) lub `obj/project.assets.json` plik (w przypadku korzystania z programu PackageReference) i ponownie uruchom przywracanie.</span><span class="sxs-lookup"><span data-stu-id="72f11-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="72f11-160">Jeśli błąd nadal występuje, `nuget locals all -clear` Użyj lub `dotnet locals all --clear` z wiersza polecenia, aby wyczyścić foldery *globalne-Packages* i pamięci podręcznej zgodnie z opisem w temacie [Zarządzanie pakietami globalnymi i folderami pamięci podręcznej](managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="72f11-160">If the error still persists, use `nuget locals all -clear` or `dotnet locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="72f11-161">Podczas uzyskiwania projektu z kontroli źródła foldery projektu mogą być ustawione na tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="72f11-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="72f11-162">Zmień uprawnienia folderu i spróbuj ponownie przywrócić pakiety.</span><span class="sxs-lookup"><span data-stu-id="72f11-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="72f11-163">Być może używasz starej wersji programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="72f11-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="72f11-164">Sprawdź [NuGet.org/downloads](https://www.nuget.org/downloads) z najnowszymi zalecanymi wersjami.</span><span class="sxs-lookup"><span data-stu-id="72f11-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="72f11-165">W przypadku programu Visual Studio 2015 zalecamy 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="72f11-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="72f11-166">Jeśli napotkasz inne problemy, zapoznaj [się z problemem w serwisie GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) , aby uzyskać więcej szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="72f11-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
