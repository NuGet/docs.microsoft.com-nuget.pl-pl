---
title: Tworzenie pakietów NuGet .NET Standard i .NET Framework za pomocą programu Visual Studio 2015
description: Kompleksowy przewodnik tworzenia pakietów NuGet .NET Standard i .NET Framework przy użyciu programu NuGet 3. x i programu Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 11dce27b93c3d09a2d27dc79f8d4fed86df879ba
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488973"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="41a1d-103">Tworzenie pakietów .NET Standard i .NET Framework za pomocą programu Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="41a1d-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="41a1d-104">**Uwaga:** Program Visual Studio 2017 jest zalecany do tworzenia bibliotek .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="41a1d-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="41a1d-105">Program Visual Studio 2015 może współpracować, ale narzędzia .NET Core zostały przesunięte tylko do stanu wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="41a1d-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="41a1d-106">Zobacz [Tworzenie i publikowanie pakietu przy użyciu programu Visual studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) do pracy z pakietem NuGet 4. x + i Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="41a1d-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="41a1d-107">[Biblioteka .NET Standard](/dotnet/articles/standard/library) jest formalną specyfikacją interfejsów API platformy .NET, które mają być dostępne we wszystkich środowiskach uruchomieniowych platformy .NET, a tym samym ustanowienie większej jednorodności w ekosystemie platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="41a1d-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="41a1d-108">Biblioteka .NET Standard definiuje jednolity zestaw interfejsów API BCL (Biblioteka klas bazowych) dla wszystkich platform .NET do implementacji, niezależnie od obciążenia.</span><span class="sxs-lookup"><span data-stu-id="41a1d-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="41a1d-109">Umożliwia deweloperom tworzenie kodu, który jest użyteczny dla wszystkich środowisk uruchomieniowych platformy .NET, i zmniejsza, czy nie eliminuje specyficznych dla platformy dyrektyw kompilacji warunkowej w kodzie udostępnionym.</span><span class="sxs-lookup"><span data-stu-id="41a1d-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="41a1d-110">Ten przewodnik przeprowadzi Cię przez proces tworzenia pakietu NuGet przeznaczony do .NET Standard biblioteki 1,4 lub pakietu docelowego .NET Framework 4,6.</span><span class="sxs-lookup"><span data-stu-id="41a1d-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="41a1d-111">Biblioteka .NET Standard 1,4 działa w .NET Framework 4.6.1, platforma uniwersalna systemu Windows 10, .NET Core i mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="41a1d-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="41a1d-112">Aby uzyskać szczegółowe informacje, zobacz [tabelę mapowania .NET Standard](/dotnet/standard/net-standard#net-implementation-support) (dokumentacja platformy .NET).</span><span class="sxs-lookup"><span data-stu-id="41a1d-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="41a1d-113">Jeśli chcesz, możesz wybrać inną wersję biblioteki .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="41a1d-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41a1d-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="41a1d-114">Prerequisites</span></span>

1. <span data-ttu-id="41a1d-115">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="41a1d-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="41a1d-116">(Tylko .NET Standard) [Zestaw .NET Core SDK](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="41a1d-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="41a1d-117">Interfejs wiersza polecenia NuGet.</span><span class="sxs-lookup"><span data-stu-id="41a1d-117">NuGet CLI.</span></span> <span data-ttu-id="41a1d-118">Pobierz najnowszą wersję pliku NuGet. exe z [NuGet.org/downloads](https://nuget.org/downloads), zapisując ją w wybranej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="41a1d-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="41a1d-119">Następnie Dodaj tę lokalizację do zmiennej środowiskowej PATH, jeśli nie została jeszcze.</span><span class="sxs-lookup"><span data-stu-id="41a1d-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="41a1d-120">NuGet. exe to narzędzie interfejsu wiersza polecenia, a nie Instalator, dlatego pamiętaj o zapisaniu pobranego pliku w przeglądarce zamiast uruchamiania go.</span><span class="sxs-lookup"><span data-stu-id="41a1d-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="41a1d-121">Utwórz projekt biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="41a1d-121">Create the class library project</span></span>

1. <span data-ttu-id="41a1d-122">W programie Visual Studio, **plik > nowy > projektu**, rozwiń **węzeł C# Visual > Windows** , wybierz pozycję **Biblioteka klas (przenośna)** , Zmień nazwę na AppLogger i wybierz **przycisk OK**.</span><span class="sxs-lookup"><span data-stu-id="41a1d-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Utwórz nowy projekt biblioteki klas](media/NetStandard-NewProject.png)

1. <span data-ttu-id="41a1d-124">W wyświetlonym oknie dialogowym **Dodaj przenośną bibliotekę klas** wybierz opcje dla `.NET Framework 4.6` i `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="41a1d-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="41a1d-125">(Jeśli .NET Framework określania wartości docelowej, możesz wybrać opcje, które są odpowiednie.)</span><span class="sxs-lookup"><span data-stu-id="41a1d-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="41a1d-126">Jeśli element docelowy jest .NET Standard, kliknij prawym `AppLogger (Portable)` przyciskiem myszy w Eksplorator rozwiązań, wybierz pozycję **Właściwości**, wybierz kartę **Biblioteka** , a następnie wybierz pozycję docelowa **platforma .NET Standard** w sekcji **Określanie wartości docelowej** .</span><span class="sxs-lookup"><span data-stu-id="41a1d-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="41a1d-127">Ta akcja monituje o potwierdzenie, a następnie można wybrać `.NET Standard 1.4` (lub inną dostępną wersję) z listy rozwijanej:</span><span class="sxs-lookup"><span data-stu-id="41a1d-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Ustawianie elementu docelowego na .NET Standard 1,4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="41a1d-129">Kliknij kartę **kompilacja** , Zmień **konfigurację** na `Release`, a następnie zaznacz pole wyboru **plik dokumentacji XML**.</span><span class="sxs-lookup"><span data-stu-id="41a1d-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="41a1d-130">Dodaj kod do składnika, na przykład:</span><span class="sxs-lookup"><span data-stu-id="41a1d-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="41a1d-131">Ustaw konfigurację na wydawanie, Skompiluj projekt i sprawdź, czy pliki dll i XML są tworzone w `bin\Release` folderze.</span><span class="sxs-lookup"><span data-stu-id="41a1d-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="41a1d-132">Utwórz i zaktualizuj plik. nuspec</span><span class="sxs-lookup"><span data-stu-id="41a1d-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="41a1d-133">Otwórz wiersz polecenia, przejdź `AppLogger.csproj` do folderu zawierającego folder (jeden poziom poniżej `.sln` lokalizacji pliku) i uruchom polecenie NuGet `spec` , aby utworzyć plik początkowy `AppLogger.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="41a1d-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="41a1d-134">Otwórz `AppLogger.nuspec` w edytorze i zaktualizuj go, aby pasował do następujących wartości, zastępując YOUR_NAME z odpowiednią wartością.</span><span class="sxs-lookup"><span data-stu-id="41a1d-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="41a1d-135">Wartość, szczególnie, musi być unikatowa w obrębie NuGet.org (zobacz Konwencje nazewnictwa opisane w artykule [Tworzenie pakietu.](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) `<id>`</span><span class="sxs-lookup"><span data-stu-id="41a1d-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="41a1d-136">Należy również pamiętać, że należy również zaktualizować Tagi autor i opis lub podczas kroku pakowania wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="41a1d-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="41a1d-137">Dodaj zestawy odwołań do `.nuspec` pliku, a mianowicie biblioteki dll biblioteki i pliku XML IntelliSense:</span><span class="sxs-lookup"><span data-stu-id="41a1d-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="41a1d-138">W przypadku .NET Standard określania wartości docelowej wpisy są podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="41a1d-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="41a1d-139">W przypadku .NET Framework określania wartości docelowej wpisy są podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="41a1d-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="41a1d-140">Kliknij prawym przyciskiem myszy rozwiązanie i wybierz pozycję **Kompiluj rozwiązanie** , aby wygenerować wszystkie pliki pakietu.</span><span class="sxs-lookup"><span data-stu-id="41a1d-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="41a1d-141">Deklarowanie zależności</span><span class="sxs-lookup"><span data-stu-id="41a1d-141">Declaring dependencies</span></span>

<span data-ttu-id="41a1d-142">Jeśli masz jakiekolwiek zależności od innych pakietów NuGet, wystaw je w `<dependencies>` elemencie manifestu z `<group>` elementami.</span><span class="sxs-lookup"><span data-stu-id="41a1d-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="41a1d-143">Na przykład, aby zadeklarować zależność w NewtonSoft. JSON 8.0.3 lub powyżej, Dodaj następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="41a1d-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="41a1d-144">Składnia atrybutu *Version* w tym miejscu wskazuje, że wersja 8.0.3 lub nowsza jest akceptowalna.</span><span class="sxs-lookup"><span data-stu-id="41a1d-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="41a1d-145">Aby określić różne zakresy wersji, zapoznaj się z artykułem [wersja pakietu](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="41a1d-145">To specify different version ranges, refer to [Package versioning](../concepts/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="41a1d-146">Dodawanie pliku Readme</span><span class="sxs-lookup"><span data-stu-id="41a1d-146">Adding a readme</span></span>

<span data-ttu-id="41a1d-147">Utwórz plik, umieść go w folderze głównym projektu i odwołaj się do niego `.nuspec` w pliku: `readme.txt`</span><span class="sxs-lookup"><span data-stu-id="41a1d-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="41a1d-148">Program Visual Studio `readme.txt` jest wyświetlany, gdy pakiet jest instalowany w projekcie.</span><span class="sxs-lookup"><span data-stu-id="41a1d-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="41a1d-149">Plik nie jest wyświetlany, gdy jest zainstalowany w projektach .NET Core lub dla pakietów zainstalowanych jako zależność.</span><span class="sxs-lookup"><span data-stu-id="41a1d-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="41a1d-150">Pakowanie składnika</span><span class="sxs-lookup"><span data-stu-id="41a1d-150">Package the component</span></span>

<span data-ttu-id="41a1d-151">Po zakończeniu `.nuspec` odwoływania się do wszystkich plików, które należy uwzględnić w pakiecie, możesz `pack` uruchomić polecenie:</span><span class="sxs-lookup"><span data-stu-id="41a1d-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="41a1d-152">Spowoduje to `AppLogger.YOUR_NAME.1.0.0.nupkg`wygenerowanie.</span><span class="sxs-lookup"><span data-stu-id="41a1d-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="41a1d-153">Otwieranie tego pliku w narzędziu, takim jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzanie wszystkich węzłów, zostanie wyświetlona następująca zawartość (pokazana dla .NET standard):</span><span class="sxs-lookup"><span data-stu-id="41a1d-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![Eksplorator pakietów NuGet przedstawiający pakiet AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="41a1d-155">`.nupkg` Plik jest po prostu plikiem ZIP z innym rozszerzeniem.</span><span class="sxs-lookup"><span data-stu-id="41a1d-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="41a1d-156">Możesz również przeanalizować zawartość pakietu, a następnie zmienić `.nupkg` ją `.zip`na, ale pamiętaj, aby przywrócić rozszerzenie przed przekazaniem pakietu do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="41a1d-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="41a1d-157">Aby udostępnić pakiet innym deweloperom, postępuj zgodnie z instrukcjami dotyczącymi [publikowania pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="41a1d-157">To make your package available to other developers, follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="41a1d-158">Należy pamiętać `pack` , że wymaga mono 4.4.2 w Mac OS X i nie działa w systemach Linux.</span><span class="sxs-lookup"><span data-stu-id="41a1d-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="41a1d-159">Na komputerze Mac należy również skonwertować nazwy ścieżek systemu Windows w `.nuspec` pliku na ścieżki w stylu systemu UNIX.</span><span class="sxs-lookup"><span data-stu-id="41a1d-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="41a1d-160">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="41a1d-160">Related topics</span></span>

- [<span data-ttu-id="41a1d-161">nuspec — odwołanie</span><span class="sxs-lookup"><span data-stu-id="41a1d-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="41a1d-162">Obsługa wielu wersji programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="41a1d-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="41a1d-163">Uwzględnij w pakiecie narzędzia i elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="41a1d-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="41a1d-164">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="41a1d-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="41a1d-165">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="41a1d-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="41a1d-166">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="41a1d-166">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="41a1d-167">Dokumentacja biblioteki .NET Standard</span><span class="sxs-lookup"><span data-stu-id="41a1d-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="41a1d-168">Przenoszenie do programu .NET Core z .NET Framework</span><span class="sxs-lookup"><span data-stu-id="41a1d-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
