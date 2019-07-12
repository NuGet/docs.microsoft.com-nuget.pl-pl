---
title: Tworzenie .NET Standard i pakiety NuGet programu .NET Framework przy użyciu programu Visual Studio 2015
description: End-to-end Przewodnik tworzenia pakietów .NET Standard i NuGet programu .NET Framework za pomocą narzędzia NuGet 3.x, a program Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 1198a781543e581f55740cc0ae5a212d3f8a8b61
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842443"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="424e3-103">Tworzenie pakietów .NET Standard i .NET Framework w programie Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="424e3-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="424e3-104">**Uwaga:** Program Visual Studio 2017, zaleca się do tworzenia biblioteki .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="424e3-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="424e3-105">Program Visual Studio 2015 można pracować, ale zestaw narzędzi .NET Core została udostępniona tylko do stanu (wersja zapoznawcza).</span><span class="sxs-lookup"><span data-stu-id="424e3-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="424e3-106">Zobacz [tworzenie i publikowanie pakietu programu Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) do pracy z NuGet 4.x+ i programu Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="424e3-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="424e3-107">[Biblioteka .NET Standard](/dotnet/articles/standard/library) jest formalną specyfikację interfejsów API platformy .NET, które mają być dostępne na wszystkie środowiska uruchomieniowe platformy .NET, dlatego ustanawiania większej jednolitości należący do ekosystemu platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="424e3-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="424e3-108">Biblioteka .NET Standard definiuje zbiór jednolitych BCL (Biblioteka klasy podstawowej) interfejsów API dla wszystkich platform .NET zaimplementować, niezależnie od obciążenia.</span><span class="sxs-lookup"><span data-stu-id="424e3-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="424e3-109">Umożliwia ona deweloperom tworzenia kodu, które są wykorzystywane przez wszystkie środowiska uruchomieniowe platformy .NET i zmniejsza, jeśli nie eliminuje dyrektywy kompilacji warunkowej specyficzne dla platformy w udostępnionego kodu.</span><span class="sxs-lookup"><span data-stu-id="424e3-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="424e3-110">Ten przewodnik przeprowadzi Cię przez tworzenie pakietu NuGet określanie wartości docelowej platformy .NET Standard 1.4 biblioteki lub pakietu przeznaczonych dla platformy .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="424e3-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="424e3-111">Biblioteki .NET Standard 1.4 działa w .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core i platformy Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="424e3-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="424e3-112">Aby uzyskać więcej informacji, zobacz [.NET Standard tabeli mapowania](/dotnet/standard/net-standard#net-implementation-support) (dokumentacja platformy .NET).</span><span class="sxs-lookup"><span data-stu-id="424e3-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="424e3-113">Druga wersja biblioteka .NET Standard można wybrać, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="424e3-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="424e3-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="424e3-114">Prerequisites</span></span>

1. <span data-ttu-id="424e3-115">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="424e3-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="424e3-116">(Tylko .NET standard) [Platformy .NET core SDK](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="424e3-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="424e3-117">Interfejs wiersza polecenia NuGet.</span><span class="sxs-lookup"><span data-stu-id="424e3-117">NuGet CLI.</span></span> <span data-ttu-id="424e3-118">Pobierz najnowszą wersję programu nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), zapisanie go do wybranej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="424e3-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="424e3-119">Następnie dodaj tej lokalizacji do zmiennej środowiskowej PATH, jeśli jeszcze tego nie zrobiono.</span><span class="sxs-lookup"><span data-stu-id="424e3-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="424e3-120">nuget.exe to narzędzie interfejsu wiersza polecenia, nie Instalatora, więc Pamiętaj zapisać pobrany plik z przeglądarki, zamiast uruchamiać go.</span><span class="sxs-lookup"><span data-stu-id="424e3-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="424e3-121">Utwórz projekt biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="424e3-121">Create the class library project</span></span>

1. <span data-ttu-id="424e3-122">W programie Visual Studio **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C# > Windows** węzła, wybierz opcję **Biblioteka klas (przenośna)** , Zmień nazwę na AppLogger i wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="424e3-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Utwórz nowy projekt biblioteki klas](media/NetStandard-NewProject.png)

1. <span data-ttu-id="424e3-124">W **Dodaj Portable Class Library** wyświetlonym oknie dialogowym Wybierz opcje dla `.NET Framework 4.6` i `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="424e3-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="424e3-125">(Jeśli przeznaczony dla .NET Framework, możesz wybrać jednego z tych opcji są odpowiednie.)</span><span class="sxs-lookup"><span data-stu-id="424e3-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="424e3-126">Przeznaczonych dla platformy .NET Standard, kliknij prawym przyciskiem myszy `AppLogger (Portable)` w Eksploratorze rozwiązań wybierz **właściwości**, wybierz opcję **biblioteki** kartę, a następnie wybierz **docelowej platformy .NET Standard** w **Ustawianie elementów docelowych** sekcji.</span><span class="sxs-lookup"><span data-stu-id="424e3-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="424e3-127">Ta akcja monituje o potwierdzenie, po którym można wybrać `.NET Standard 1.4` (lub inna wersja dostępna) z listy rozwijanej:</span><span class="sxs-lookup"><span data-stu-id="424e3-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Ustawienia obiektu docelowego .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="424e3-129">Kliknij pozycję **kompilacji** kartę, zmień **konfiguracji** do `Release`i pole wyboru dla **pliku dokumentacji XML**.</span><span class="sxs-lookup"><span data-stu-id="424e3-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="424e3-130">Dodaj kod do składnika, na przykład:</span><span class="sxs-lookup"><span data-stu-id="424e3-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="424e3-131">Ustaw konfigurację do wersji, skompiluj projekt i sprawdź, czy biblioteka DLL, pliki XML są tworzone w ramach `bin\Release` folderu.</span><span class="sxs-lookup"><span data-stu-id="424e3-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="424e3-132">Tworzenie i aktualizowanie pliku .nuspec</span><span class="sxs-lookup"><span data-stu-id="424e3-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="424e3-133">Otwórz wiersz polecenia, przejdź do folderu zawierającego `AppLogger.csproj` folder (jeden poziom poniżej miejsca `.sln` plik jest), i Uruchom rozszerzenie NuGet `spec` polecenie, aby utworzyć początkowy `AppLogger.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="424e3-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="424e3-134">Otwórz `AppLogger.nuspec` w edytorze i zaktualizuj go zgodnie z poniższym, zamieniając twoja_nazwa odpowiednią wartość.</span><span class="sxs-lookup"><span data-stu-id="424e3-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="424e3-135">`<id>` Wartość, w szczególności musi być unikatowa w witrynie nuget.org (konwencje nazewnictwa, opisane w temacie [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="424e3-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="424e3-136">Należy również zauważyć, że należy również zaktualizować autor i opis znaczników lub wystąpi błąd podczas wykonywania kroku pakowania.</span><span class="sxs-lookup"><span data-stu-id="424e3-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="424e3-137">Dodaj zestawy referencyjne do `.nuspec` pliku, a mianowicie biblioteki DLL i pliku IntelliSense XML:</span><span class="sxs-lookup"><span data-stu-id="424e3-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="424e3-138">Jeśli przeznaczonych dla platformy .NET Standard, wpisy zostaną wyświetlone podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="424e3-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="424e3-139">Jeśli przeznaczony dla .NET Framework, wpisy zostaną wyświetlone podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="424e3-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="424e3-140">Kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz pozycję **Kompiluj rozwiązanie** wygenerować pliki pakietu.</span><span class="sxs-lookup"><span data-stu-id="424e3-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="424e3-141">Deklarowanie zależności</span><span class="sxs-lookup"><span data-stu-id="424e3-141">Declaring dependencies</span></span>

<span data-ttu-id="424e3-142">Jeśli masz jakieś zależności, w innych pakietach NuGet listy w manifeście `<dependencies>` element z `<group>` elementów.</span><span class="sxs-lookup"><span data-stu-id="424e3-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="424e3-143">Na przykład, aby zadeklarować zależność w NewtonSoft.Json 8.0.3 lub nowszej, Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="424e3-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="424e3-144">Składnia *wersji* atrybut wskazuje, w tym miejscu tę wersję 8.0.3 lub powyżej jest dopuszczalna.</span><span class="sxs-lookup"><span data-stu-id="424e3-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="424e3-145">Aby określić zakresy innej wersji, zapoznaj się [przechowywanie wersji pakietów](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="424e3-145">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="424e3-146">Dodawanie pliku readme</span><span class="sxs-lookup"><span data-stu-id="424e3-146">Adding a readme</span></span>

<span data-ttu-id="424e3-147">Utwórz swoje `readme.txt` pliku, umieść go w folderze głównym projektu i odwoływać się do niego w `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="424e3-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="424e3-148">Visual Studio wyświetlanie `readme.txt` po zainstalowaniu pakietu do projektu.</span><span class="sxs-lookup"><span data-stu-id="424e3-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="424e3-149">Plik nie jest wyświetlany, gdy zainstalowane w projektach .NET Core lub pakietów, które są zainstalowane jako zależność.</span><span class="sxs-lookup"><span data-stu-id="424e3-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="424e3-150">Pakiet składnika</span><span class="sxs-lookup"><span data-stu-id="424e3-150">Package the component</span></span>

<span data-ttu-id="424e3-151">Za pomocą ukończoną `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:</span><span class="sxs-lookup"><span data-stu-id="424e3-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="424e3-152">Spowoduje to wygenerowanie `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="424e3-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="424e3-153">Otwarcie tego pliku w narzędzia, takiego jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzając wszystkie węzły, zobacz następującą zawartość (wyświetlana dla platformy .NET Standard):</span><span class="sxs-lookup"><span data-stu-id="424e3-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![Wyświetlanie pakietu AppLogger Eksplorator pakietów NuGet](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="424e3-155">A `.nupkg` plik jest po prostu plikiem ZIP z innym rozszerzeniem.</span><span class="sxs-lookup"><span data-stu-id="424e3-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="424e3-156">Można także sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale należy pamiętać przywrócić rozszerzenia przed przekazaniem pakietu na stronie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="424e3-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="424e3-157">Aby udostępnić pakietu innym deweloperom, postępuj zgodnie z instrukcjami [publikowanie pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="424e3-157">To make your package available to other developers, follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="424e3-158">Należy pamiętać, że `pack` wymaga platformy Mono 4.4.2 w systemie Mac OS X, a nie działa w systemach Linux.</span><span class="sxs-lookup"><span data-stu-id="424e3-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="424e3-159">Na komputerze Mac, należy także przekonwertować nazwy Windows ścieżek w `.nuspec` plik do ścieżki stylu systemu Unix.</span><span class="sxs-lookup"><span data-stu-id="424e3-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="424e3-160">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="424e3-160">Related topics</span></span>

- [<span data-ttu-id="424e3-161">odwołanie .nuspec</span><span class="sxs-lookup"><span data-stu-id="424e3-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="424e3-162">Obsługiwanie wielu wersji programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="424e3-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="424e3-163">Zawiera właściwości programu MSBuild i obiektów docelowych w pakiecie</span><span class="sxs-lookup"><span data-stu-id="424e3-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="424e3-164">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="424e3-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="424e3-165">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="424e3-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="424e3-166">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="424e3-166">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="424e3-167">Dokumentacja .NET biblioteki standardowej</span><span class="sxs-lookup"><span data-stu-id="424e3-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="424e3-168">Eksportowanie do programu .NET Core z .NET Framework</span><span class="sxs-lookup"><span data-stu-id="424e3-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
