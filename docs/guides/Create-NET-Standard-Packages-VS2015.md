---
title: Tworzenie .NET Standard i pakiety NuGet programu .NET Framework przy użyciu programu Visual Studio 2015
description: Przewodnik end-to-end tworzenia pakietów platformy .NET Standard i NuGet programu .NET Framework za pomocą NuGet 3.x i programu Visual Studio 2015.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: c66e782ea5d4e9e2a9585d8301dc2a1b2e8c72b9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818737"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="e99e3-103">Utwórz pakiety .NET Standard i .NET Framework z programem Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e99e3-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="e99e3-104">**Uwaga:** 2017 usługi Visual Studio jest zalecane w przypadku tworzenia bibliotek .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="e99e3-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="e99e3-105">Visual Studio 2015 może działać, ale narzędzi platformy .NET Core został przeniesiony do trybu tylko do podglądu stanu.</span><span class="sxs-lookup"><span data-stu-id="e99e3-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="e99e3-106">Zobacz [tworzenie i publikowanie pakietu z programu Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) do pracy z NuGet 4.x+ i Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="e99e3-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="e99e3-107">[Biblioteki standardowej .NET](/dotnet/articles/standard/library) jest formalną specyfikację interfejsów API architektury .NET mają być dostępne na wszystkich środowisk uruchomieniowych .NET, w związku z tym ustanawianie większej jednolitości w ekosystemie .NET.</span><span class="sxs-lookup"><span data-stu-id="e99e3-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="e99e3-108">Standardowa biblioteka .NET definiuje zestaw uniform BCL (Biblioteka klasy podstawowej) interfejsów API dla wszystkich platform .NET zaimplementować, niezależnie od obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e99e3-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="e99e3-109">Umożliwia ona deweloperom tworzyć kod, który jest można używać we wszystkich programów .NET i zmniejsza Jeśli nie eliminuje dyrektywy kompilacja warunkowa specyficzne dla platformy w kodzie udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="e99e3-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="e99e3-110">Ten przewodnik przeprowadzi Cię przez proces tworzenia pakietu NuGet przeznaczonych dla platformy .NET Standard 1.4 biblioteki lub pakietu przeznaczonych dla platformy .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="e99e3-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="e99e3-111">Biblioteki standardowe 1.4 .NET działa za pośrednictwem platformy .NET Framework 4.6.1, uniwersalnych systemu Windows 10 platformy .NET Core i Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="e99e3-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="e99e3-112">Aby uzyskać więcej informacji, zobacz [.NET Standard tabeli mapowania](/dotnet/standard/net-standard#net-implementation-support) (dokumentacja .NET).</span><span class="sxs-lookup"><span data-stu-id="e99e3-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="e99e3-113">Można wybrać innych wersji biblioteki standardowej .NET, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="e99e3-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e99e3-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e99e3-114">Prerequisites</span></span>

1. <span data-ttu-id="e99e3-115">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="e99e3-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="e99e3-116">(Tylko standardowe .NET) [.NET core SDK](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="e99e3-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="e99e3-117">Interfejs wiersza polecenia NuGet.</span><span class="sxs-lookup"><span data-stu-id="e99e3-117">NuGet CLI.</span></span> <span data-ttu-id="e99e3-118">Pobierz najnowszą wersję nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), zapisać go do wybranej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="e99e3-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="e99e3-119">Dodać tej lokalizacji do Twojej zmiennej środowiskowej PATH, gdy nie jest jeszcze.</span><span class="sxs-lookup"><span data-stu-id="e99e3-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="e99e3-120">nuget.exe to narzędzie interfejsu wiersza polecenia, nie Instalatora, dlatego należy Zapisz pobrany plik z przeglądarki, a jego uruchomieniem.</span><span class="sxs-lookup"><span data-stu-id="e99e3-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="e99e3-121">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="e99e3-121">Create the class library project</span></span>

1. <span data-ttu-id="e99e3-122">W programie Visual Studio **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C# > systemu Windows** węzła, wybierz opcję **biblioteki klas (przenośna)**, Zmień nazwę na AppLogger i wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="e99e3-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Tworzenie nowego projektu biblioteki klas](media/NetStandard-NewProject.png)

1. <span data-ttu-id="e99e3-124">W **dodać przenośnej biblioteki klas** okno dialogowe zostanie wyświetlone, wybierz opcje dla `.NET Framework 4.6` i `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="e99e3-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="e99e3-125">(Jeśli przeznaczonych dla platformy .NET Framework, można wybrać dowolną wskazaną opcje są odpowiednie.)</span><span class="sxs-lookup"><span data-stu-id="e99e3-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="e99e3-126">Jeśli przeznaczonych dla platformy .NET Standard, kliknij prawym przyciskiem myszy `AppLogger (Portable)` w Eksploratorze rozwiązań wybierz **właściwości**, wybierz pozycję **biblioteki** , a następnie wybierz **docelowej platformy .NET Standard** w **docelowych** sekcji.</span><span class="sxs-lookup"><span data-stu-id="e99e3-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="e99e3-127">Ta akcja monituje o potwierdzenie, po którym można wybrać `.NET Standard 1.4` (lub inna wersja dostępna) z listy rozwijanej:</span><span class="sxs-lookup"><span data-stu-id="e99e3-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Ustawienie docelowej platformy .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="e99e3-129">Polecenie **kompilacji** Zmień **konfiguracji** do `Release`i pole wyboru dla **pliku dokumentacji XML**.</span><span class="sxs-lookup"><span data-stu-id="e99e3-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="e99e3-130">Dodaj swój kod do składnika, na przykład:</span><span class="sxs-lookup"><span data-stu-id="e99e3-130">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="e99e3-131">Ustaw konfigurację do wersji, skompilować projekt i sprawdź, czy biblioteka DLL, pliki XML są tworzone w ramach `bin\Release` folderu.</span><span class="sxs-lookup"><span data-stu-id="e99e3-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="e99e3-132">Tworzenie i aktualizowanie pliku .nuspec</span><span class="sxs-lookup"><span data-stu-id="e99e3-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="e99e3-133">Otwórz wiersz polecenia, przejdź do folderu zawierającego `AppLogger.csproj` folder (jeden poziom w dół where `.sln` pliku), i uruchom NuGet `spec` polecenie, aby utworzyć pierwszy `AppLogger.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="e99e3-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="e99e3-134">Otwórz `AppLogger.nuspec` w edytorze i zaktualizować je zgodnie z poniższym, zamieniając twoje_imie odpowiednią wartość.</span><span class="sxs-lookup"><span data-stu-id="e99e3-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="e99e3-135">`<id>` Wartość, w szczególności musi być unikatowa w nuget.org (konwencje nazewnictwa opisane w temacie [utworzenie pakietu](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="e99e3-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="e99e3-136">Należy również zauważyć, że należy również zaktualizować tagi autora oraz opis lub wystąpi błąd podczas wykonywania kroku pakowania.</span><span class="sxs-lookup"><span data-stu-id="e99e3-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="e99e3-137">Dodaj zestawy odwołań `.nuspec` plików, to znaczy biblioteki DLL i pliku IntelliSense XML:</span><span class="sxs-lookup"><span data-stu-id="e99e3-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="e99e3-138">Jeśli przeznaczonych dla platformy .NET Standard, wpisy zostaną wyświetlone podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="e99e3-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="e99e3-139">Jeśli przeznaczonych dla platformy .NET Framework, wpisy zostaną wyświetlone podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="e99e3-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="e99e3-140">Kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz **Kompiluj rozwiązanie** do wygenerowania wszystkich plików w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="e99e3-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="e99e3-141">Deklarowanie zależności</span><span class="sxs-lookup"><span data-stu-id="e99e3-141">Declaring dependencies</span></span>

<span data-ttu-id="e99e3-142">Jeśli jest zależne od innych pakietów NuGet, listy w manifeście `<dependencies>` element z `<group>` elementów.</span><span class="sxs-lookup"><span data-stu-id="e99e3-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="e99e3-143">Na przykład aby zadeklarować zależność w NewtonSoft.Json 8.0.3 lub nowszym, należy dodać:</span><span class="sxs-lookup"><span data-stu-id="e99e3-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="e99e3-144">Składnia *wersji* tutaj wskazuje, czy w wersji 8.0.3 lub nowszy jest dopuszczalne atrybutu.</span><span class="sxs-lookup"><span data-stu-id="e99e3-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="e99e3-145">Aby określić inną wersję zakresów, zapoznaj się [wersji pakietu](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="e99e3-145">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="e99e3-146">Dodawanie pliku readme</span><span class="sxs-lookup"><span data-stu-id="e99e3-146">Adding a readme</span></span>

<span data-ttu-id="e99e3-147">Tworzenie sieci `readme.txt` pliku, umieść go w folderze głównym projektu i odwołuje się do niego w `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="e99e3-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```

<span data-ttu-id="e99e3-148">Visual Studio wyświetlania `readme.txt` po zainstalowaniu pakietu do projektu.</span><span class="sxs-lookup"><span data-stu-id="e99e3-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="e99e3-149">Plik nie jest wyświetlane, gdy zainstalowane w projektach platformy .NET Core lub pakietów, które są zainstalowane jako zależność.</span><span class="sxs-lookup"><span data-stu-id="e99e3-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="e99e3-150">Pakiet składnika</span><span class="sxs-lookup"><span data-stu-id="e99e3-150">Package the component</span></span>

<span data-ttu-id="e99e3-151">Z ukończonej `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:</span><span class="sxs-lookup"><span data-stu-id="e99e3-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="e99e3-152">Spowoduje to wygenerowanie `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="e99e3-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="e99e3-153">Otwarcie tego pliku w narzędzia, takiego jak [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzanie wszystkich węzłów, zobacz następującą zawartość (wyświetlane dla platformy .NET Standard):</span><span class="sxs-lookup"><span data-stu-id="e99e3-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![Wyświetlanie pakietu AppLogger Explorer pakietu NuGet](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="e99e3-155">A `.nupkg` plik jest tylko plik ZIP zawierający inne rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="e99e3-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="e99e3-156">Można również sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale pamiętaj, aby przywrócić rozszerzenia przed przekazaniem do nuget.org pakietu.</span><span class="sxs-lookup"><span data-stu-id="e99e3-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="e99e3-157">Aby udostępnić pakietu inni deweloperzy, postępuj zgodnie z instrukcjami [opublikowania pakietu](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="e99e3-157">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="e99e3-158">Należy pamiętać, że `pack` wymaga Mono 4.4.2 w systemie Mac OS X i nie działa w systemach Linux.</span><span class="sxs-lookup"><span data-stu-id="e99e3-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="e99e3-159">Na komputerze Mac, należy także przekonwertować nazwy ścieżek systemu Windows w `.nuspec` pliku do ścieżki typu Unix.</span><span class="sxs-lookup"><span data-stu-id="e99e3-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="e99e3-160">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="e99e3-160">Related topics</span></span>

- [<span data-ttu-id="e99e3-161">odwołanie .nuspec</span><span class="sxs-lookup"><span data-stu-id="e99e3-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="e99e3-162">Obsługa wielu wersje programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="e99e3-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="e99e3-163">Zawiera właściwości programu MSBuild i obiektów docelowych w pakiecie</span><span class="sxs-lookup"><span data-stu-id="e99e3-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="e99e3-164">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="e99e3-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="e99e3-165">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="e99e3-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="e99e3-166">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="e99e3-166">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="e99e3-167">Dokumentacja biblioteki standardowej .NET</span><span class="sxs-lookup"><span data-stu-id="e99e3-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="e99e3-168">Eksportowanie do platformy .NET Core z .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e99e3-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
