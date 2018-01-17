---
title: "Tworzenie pakietów NuGet standardowe .NET z programem Visual Studio 2015 | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "Przewodnik end-to-end tworzenia pakietów NuGet programu .NET Standard przy użyciu narzędzia NuGet 3.x i programu Visual Studio 2015."
keywords: "Tworzenie pakietu, .NET Standard pakietów, .NET Standard tabeli mapowania"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e02888bf552997afe25e967f13e021e78e40d48d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="ce81f-104">Utwórz pakiety .NET Standard z programem Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ce81f-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="ce81f-105">*Dotyczy NuGet 3.x. Zobacz [utworzyć .NET Standard pakiety z programu Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) do pracy z NuGet 4.x+.*</span><span class="sxs-lookup"><span data-stu-id="ce81f-105">*Applies to NuGet 3.x. See [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="ce81f-106">[Biblioteki standardowej .NET](/dotnet/articles/standard/library) jest formalną specyfikację interfejsów API architektury .NET mają być dostępne na wszystkich środowisk uruchomieniowych .NET, w związku z tym ustanawianie większej jednolitości w ekosystemie .NET.</span><span class="sxs-lookup"><span data-stu-id="ce81f-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="ce81f-107">Standardowa biblioteka .NET definiuje zestaw uniform BCL (Biblioteka klasy podstawowej) interfejsów API dla wszystkich platform .NET zaimplementować, niezależnie od obciążenia.</span><span class="sxs-lookup"><span data-stu-id="ce81f-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="ce81f-108">Go umożliwia deweloperom tworzenia PCLs, które będą używać dla wszystkich programów .NET, i zmniejsza Jeśli nie eliminuje dyrektywy kompilacja warunkowa specyficzne dla platformy w kodzie udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="ce81f-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="ce81f-109">Ten przewodnik przeprowadzi Cię przez proces tworzenia pakietu nuget przeznaczonych dla platformy .NET Standard biblioteki 1.4.</span><span class="sxs-lookup"><span data-stu-id="ce81f-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="ce81f-110">To będzie działać w .NET Framework 4.6.1, uniwersalnych systemu Windows 10 platformy .NET Core i Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="ce81f-110">This will work across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="ce81f-111">Aby uzyskać więcej informacji, zobacz [.NET Standard tabeli mapowania](#net-standard-mapping-table) dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="ce81f-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

1. [<span data-ttu-id="ce81f-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ce81f-112">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="ce81f-113">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="ce81f-113">Create the class library project</span></span>](#create-the-class-library-project)
1. [<span data-ttu-id="ce81f-114">Tworzenie i aktualizowanie pliku .nuspec</span><span class="sxs-lookup"><span data-stu-id="ce81f-114">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="ce81f-115">Pakiet składnika</span><span class="sxs-lookup"><span data-stu-id="ce81f-115">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="ce81f-116">Dodatkowe opcje</span><span class="sxs-lookup"><span data-stu-id="ce81f-116">Additional options</span></span>](#additional-options)
1. [<span data-ttu-id="ce81f-117">.NET standard tabeli mapowania</span><span class="sxs-lookup"><span data-stu-id="ce81f-117">.NET Standard mapping table</span></span>](#net-standard-mapping-table)
1. [<span data-ttu-id="ce81f-118">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="ce81f-118">Related topics</span></span>](#related-topics)


## <a name="pre-requisites"></a><span data-ttu-id="ce81f-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ce81f-119">Pre-requisites</span></span>

1. <span data-ttu-id="ce81f-120">Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ce81f-120">Visual Studio 2015.</span></span> <span data-ttu-id="ce81f-121">Bezpłatnie zainstalować Community edition z [visualstudio.com](https://www.visualstudio.com/); oczywiście można również wersje Professional i Enterprise.</span><span class="sxs-lookup"><span data-stu-id="ce81f-121">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span>
1. <span data-ttu-id="ce81f-122">.NET core: Zainstaluj oprogramowanie .NET Core wraz z szablonów i innych narzędzi dla programu Visual Studio 2015 z [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span><span class="sxs-lookup"><span data-stu-id="ce81f-122">.NET Core: Install .NET Core along with templates and other tools for Visual Studio 2015 from [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span></span>
1. <span data-ttu-id="ce81f-123">Interfejs wiersza polecenia NuGet.</span><span class="sxs-lookup"><span data-stu-id="ce81f-123">NuGet CLI.</span></span> <span data-ttu-id="ce81f-124">Pobierz najnowszą wersję nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), zapisać go do wybranej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="ce81f-124">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="ce81f-125">Dodać tej lokalizacji do Twojej zmiennej środowiskowej PATH, gdy nie jest jeszcze.</span><span class="sxs-lookup"><span data-stu-id="ce81f-125">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="ce81f-126">nuget.exe to narzędzie interfejsu wiersza polecenia, nie Instalatora, dlatego należy Zapisz pobrany plik z przeglądarki, a jego uruchomieniem.</span><span class="sxs-lookup"><span data-stu-id="ce81f-126">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>



## <a name="create-the-class-library-project"></a><span data-ttu-id="ce81f-127">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="ce81f-127">Create the class library project</span></span>

1. <span data-ttu-id="ce81f-128">W programie Visual Studio **Plik > Nowy > projektu**, rozwiń węzeł **Visual C# > Windows** węzła, wybierz opcję **biblioteki klas (przenośna)**, Zmień nazwę na AppLogger i kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="ce81f-128">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Tworzenie nowego projektu biblioteki klas](media/NetStandard-NewProject.png)

1. <span data-ttu-id="ce81f-130">W **dodać przenośnej biblioteki klas** okno dialogowe zostanie wyświetlone, wybierz `.NET Framework 4.6` i `ASP.NET Core 1.0` opcje.</span><span class="sxs-lookup"><span data-stu-id="ce81f-130">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>
1. <span data-ttu-id="ce81f-131">Kliknij prawym przyciskiem myszy `AppLogger (Portable)` w Eksploratorze rozwiązań wybierz **właściwości**, wybierz pozycję **biblioteki** , a następnie kliknij **docelowej platformy .NET Standard** w **Przeznaczonych dla** sekcji.</span><span class="sxs-lookup"><span data-stu-id="ce81f-131">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="ce81f-132">Ten monit o potwierdzenie, po którym można wybrać `.NET Standard 1.4` z listy rozwijanej:</span><span class="sxs-lookup"><span data-stu-id="ce81f-132">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Ustawienie docelowej platformy .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="ce81f-134">Polecenie **kompilacji** Zmień **konfiguracji** do `Release`i pole wyboru dla **pliku dokumentacji XML**.</span><span class="sxs-lookup"><span data-stu-id="ce81f-134">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>
1. <span data-ttu-id="ce81f-135">Dodaj swój kod do składnika, na przykład:</span><span class="sxs-lookup"><span data-stu-id="ce81f-135">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. <span data-ttu-id="ce81f-136">Skompiluj projekt (przy użyciu konfiguracji Release) i sprawdź, czy biblioteka DLL, pliki XML są tworzone w folderze bin\Release.</span><span class="sxs-lookup"><span data-stu-id="ce81f-136">Build the project (with the Release configuration) and check that DLL and XML files are produced within the bin\Release folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="ce81f-137">Tworzenie i aktualizowanie pliku .nuspec</span><span class="sxs-lookup"><span data-stu-id="ce81f-137">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="ce81f-138">Otwórz wiersz polecenia, przejdź do folderu zawierającego `AppLogg.csproj` folder (jeden poziom w dół where `.sln` pliku), i uruchom NuGet `spec` polecenie, aby utworzyć pierwszy `AppLogger.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="ce81f-138">Open a command prompt, navigate to the folder containing `AppLogg.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="ce81f-139">Otwórz `AppLogger.nuspec` w edytorze i zaktualizować je zgodnie z poniższym, zamieniając twoje_imie odpowiednią wartość.</span><span class="sxs-lookup"><span data-stu-id="ce81f-139">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="ce81f-140">`<id>` Wartość, w szczególności musi być unikatowa w nuget.org (konwencje nazewnictwa opisane w temacie [utworzenie pakietu](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="ce81f-140">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="ce81f-141">Należy również zauważyć, że należy również zaktualizować tagi autora oraz opis lub zostanie wyświetlony błąd podczas wykonywania kroku pakowania.</span><span class="sxs-lookup"><span data-stu-id="ce81f-141">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

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
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. <span data-ttu-id="ce81f-142">Dodaj zestawy odwołań `.nuspec` plików, to znaczy biblioteki DLL i pliku IntelliSense XML:</span><span class="sxs-lookup"><span data-stu-id="ce81f-142">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="ce81f-143">Kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz **Kompiluj rozwiązanie** do wygenerowania wszystkich plików w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="ce81f-143">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="ce81f-144">Pakiet składnika</span><span class="sxs-lookup"><span data-stu-id="ce81f-144">Package the component</span></span>

<span data-ttu-id="ce81f-145">Z ukończonej `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:</span><span class="sxs-lookup"><span data-stu-id="ce81f-145">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack AppLogger.nuspec
```

<span data-ttu-id="ce81f-146">Spowoduje to wygenerowanie `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="ce81f-146">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="ce81f-147">Otwarcie tego pliku w narzędzia, takiego jak [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzanie wszystkich węzłów, zobaczysz następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="ce81f-147">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![Wyświetlanie pakietu AppLogger Explorer pakietu NuGet](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="ce81f-149">A `.nupkg` plik jest tylko plik ZIP zawierający inne rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="ce81f-149">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="ce81f-150">Można również sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale pamiętaj, aby przywrócić rozszerzenia przed przekazaniem do nuget.org pakietu.</span><span class="sxs-lookup"><span data-stu-id="ce81f-150">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="ce81f-151">Aby udostępnić pakietu inni deweloperzy, postępuj zgodnie z instrukcjami [opublikowania pakietu](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ce81f-151">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="ce81f-152">Należy pamiętać, że `pack` wymaga Mono 4.4.2 w systemie Mac OS X i nie działa w systemach Linux.</span><span class="sxs-lookup"><span data-stu-id="ce81f-152">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="ce81f-153">Na komputerze Mac, należy także przekonwertować nazwy ścieżek systemu Windows w `.nuspec` pliku do ścieżki typu Unix.</span><span class="sxs-lookup"><span data-stu-id="ce81f-153">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="additional-options"></a><span data-ttu-id="ce81f-154">Dodatkowe opcje</span><span class="sxs-lookup"><span data-stu-id="ce81f-154">Additional options</span></span>

<span data-ttu-id="ce81f-155">Poniższe sekcje przejdź do dodatkowe opcje tworzenia pakietu NuGet:</span><span class="sxs-lookup"><span data-stu-id="ce81f-155">The following sections go into additional options for NuGet package creation:</span></span>

- [<span data-ttu-id="ce81f-156">Deklarowanie zależności</span><span class="sxs-lookup"><span data-stu-id="ce81f-156">Declaring dependencies</span></span>](#declaring-dependencies)
- [<span data-ttu-id="ce81f-157">Obsługujący wiele platform docelowych</span><span class="sxs-lookup"><span data-stu-id="ce81f-157">Supporting multiple target frameworks</span></span>](#supporting-multiple-target-frameworks)
- [<span data-ttu-id="ce81f-158">Dodawanie elementów docelowych i właściwości dla programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="ce81f-158">Adding targets and props for MSBuild</span></span>](#adding-targets-and-props-for-msbuild)
- [<span data-ttu-id="ce81f-159">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="ce81f-159">Creating localized packages</span></span>](#creating-localized-packages)
- [<span data-ttu-id="ce81f-160">Dodawanie pliku readme</span><span class="sxs-lookup"><span data-stu-id="ce81f-160">Adding a readme</span></span>](#adding-a-readme)

### <a name="declaring-dependencies"></a><span data-ttu-id="ce81f-161">Deklarowanie zależności</span><span class="sxs-lookup"><span data-stu-id="ce81f-161">Declaring dependencies</span></span>

<span data-ttu-id="ce81f-162">Jeśli jest zależne od innych pakietów NuGet, listy w `<dependencies>` element z `<group>` elementów.</span><span class="sxs-lookup"><span data-stu-id="ce81f-162">If you have any dependencies on other NuGet packages, list those in the `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="ce81f-163">Na przykład aby zadeklarować zależność w NewtonSoft.Json 8.0.3 lub nowszym, należy dodać:</span><span class="sxs-lookup"><span data-stu-id="ce81f-163">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="ce81f-164">Składnia *wersji* tutaj wskazuje, czy w wersji 8.0.3 lub nowszy jest dopuszczalne atrybutu.</span><span class="sxs-lookup"><span data-stu-id="ce81f-164">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="ce81f-165">Aby określić inną wersję zakresów, zapoznaj się [wersji pakietu](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="ce81f-165">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="supporting-multiple-target-frameworks"></a><span data-ttu-id="ce81f-166">Obsługujący wiele platform docelowych</span><span class="sxs-lookup"><span data-stu-id="ce81f-166">Supporting multiple target frameworks</span></span>

<span data-ttu-id="ce81f-167">Załóżmy, że chcesz korzystać z interfejsu API w .NET Framework 4.6.2, która nie jest dostępna w .NET Standard 1.4.</span><span class="sxs-lookup"><span data-stu-id="ce81f-167">Suppose you'd like to take advantage of an API in .NET Framework 4.6.2 that is not available in .NET Standard 1.4.</span></span> <span data-ttu-id="ce81f-168">Aby to zrobić, musisz najpierw upewnij się, że biblioteka jest kompilowany dla .NET 4.6.2 przy użyciu kompilacja warunkowa lub udostępnionych projektów.</span><span class="sxs-lookup"><span data-stu-id="ce81f-168">To do this, you'll first need to make sure the library compiles for .NET 4.6.2 by using conditional compilation or shared projects.</span></span> <span data-ttu-id="ce81f-169">(W programie Visual Studio, możesz można utworzyć projekt NetCore, wiele sekcji framework dodać framework wyboru i późniejszego kompilowania.) Następnie można utworzyć pakietu przy użyciu prostego technika katalogu opartych na konwencjach pracy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ce81f-169">(In Visual Studio, you can create a NetCore project, add the framework of choice to the multiple framework section, and then build.) Then you create the package using the simple convention-based working directory technique as follows:</span></span>

1. <span data-ttu-id="ce81f-170">W projekcie głównym folderu zawierającego Twojej `.nuspec` plików, Utwórz folder o nazwie `lib`.</span><span class="sxs-lookup"><span data-stu-id="ce81f-170">In the project's root folder containing your `.nuspec` file, create a folder named `lib`.</span></span>
1. <span data-ttu-id="ce81f-171">Wewnątrz `lib`, tworzenie folderów na różnych platformach, które mają być obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="ce81f-171">Inside `lib`, create folders for each platform you want to support:</span></span>

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. <span data-ttu-id="ce81f-172">W `.nuspec` plików, dodawanie `files` węźle `package` węzła i odwołują się do plików w `lib` przy użyciu symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="ce81f-172">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `lib` using wildcards.</span></span> <span data-ttu-id="ce81f-173">**Uwaga:** Token zamiany nie są obsługiwane z podejścia opartych na konwencjach katalog roboczy, aby je zastąpić wartości literałów:</span><span class="sxs-lookup"><span data-stu-id="ce81f-173">**Note:** Token replacements are not supported with the convention-based working directory approach, so replace them with literal values:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="ce81f-174">Utwórz pakiet ponownie, używając `nuget pack AppLogger.spec`.</span><span class="sxs-lookup"><span data-stu-id="ce81f-174">Create the package again using `nuget pack AppLogger.spec`.</span></span>

<span data-ttu-id="ce81f-175">Aby uzyskać więcej informacji na temat używania tej metody, zobacz [obsługi wielu wersje programu .NET Framework](../create-packages/supporting-multiple-target-frameworks.md)</span><span class="sxs-lookup"><span data-stu-id="ce81f-175">For more details on using this technique, see [Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)</span></span>

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="ce81f-176">Dodawanie elementów docelowych i właściwości dla programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="ce81f-176">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="ce81f-177">W niektórych przypadkach można dodać elementów docelowych niestandardowej kompilacji lub właściwości w projektach używające pakietu, takie jak uruchomienie niestandardowego narzędzia lub procesu podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="ce81f-177">In some cases you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="ce81f-178">Aby to zrobić, dodanie plików w `\build` folderu zgodnie z opisem w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="ce81f-178">You do this by adding files in a `\build` folder as described in the steps below.</span></span> <span data-ttu-id="ce81f-179">Podczas instalowania pakietu z plikami \build NuGet dodaje element programu MSBuild w pliku projektu wskazujące pliki .targets i .props.</span><span class="sxs-lookup"><span data-stu-id="ce81f-179">When NuGet installs a package with \build files, it adds an MSBuild element in the project file pointing to the .targets and .props files.</span></span>

> [!Note]
> <span data-ttu-id="ce81f-180">Korzystając z `project.json`, elementy docelowe nie zostaną dodane do projektu, ale są udostępniane za pośrednictwem `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="ce81f-180">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>


1. <span data-ttu-id="ce81f-181">W projekcie folder zawierający Twoje `.nuspec` plików, Utwórz folder o nazwie `build`.</span><span class="sxs-lookup"><span data-stu-id="ce81f-181">In the project folder containing the your `.nuspec` file, create a folder named `build`.</span></span>
1. <span data-ttu-id="ce81f-182">Wewnątrz `build`, tworzenie folderów dla każdego obsługiwane i umieść w obrębie tych sieci `.targets` i `.props` plików:</span><span class="sxs-lookup"><span data-stu-id="ce81f-182">Inside `build`, create folders for each supported, and within those place your `.targets` and `.props` files:</span></span>

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. <span data-ttu-id="ce81f-183">W `.nuspec` plików, dodawanie `files` węźle `package` węzła i odwołują się do plików w `build` przy użyciu symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="ce81f-183">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `build` using wildcards.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. <span data-ttu-id="ce81f-184">Utwórz pakiet ponownie, używając `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ce81f-184">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>

<span data-ttu-id="ce81f-185">Aby uzyskać więcej informacji, zapoznaj się [właściwości MSBuild obejmują i obiektów docelowych w pakiecie](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="ce81f-185">For additional details, refer to [Include MSBuild props and targets in a package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span></span>


### <a name="creating-localized-packages"></a><span data-ttu-id="ce81f-186">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="ce81f-186">Creating localized packages</span></span>

<span data-ttu-id="ce81f-187">Aby utworzyć zlokalizowane wersje biblioteki, można utworzyć oddzielne pakiety dla innych języków lub zawierają zestawy zlokalizowanych zasobów w jednym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="ce81f-187">To create localized versions of your library, you can either create separate packages for different locales, or include localized resource assemblies within a single package.</span></span> <span data-ttu-id="ce81f-188">Oto jak to zrobić to drugie podejście, niemieckim i hiszpańskim:</span><span class="sxs-lookup"><span data-stu-id="ce81f-188">Here's how to do the latter approach for German and Italian:</span></span>

1. <span data-ttu-id="ce81f-189">W ramach każdej docelowej framework folderze `lib`, tworzyć foldery dla każdego z obsługiwanych języków innych niż domyślne angielskiej wersji językowej.</span><span class="sxs-lookup"><span data-stu-id="ce81f-189">Within each target framework folder under `lib`, create folders for each supported language other than the English default.</span></span> <span data-ttu-id="ce81f-190">W tych folderach można umieścić zestawy zasobów i zlokalizowanych plików IntelliSense XML.</span><span class="sxs-lookup"><span data-stu-id="ce81f-190">In these folders you can place resource assemblies  and localized IntelliSense XML files.</span></span> <span data-ttu-id="ce81f-191">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="ce81f-191">For example:</span></span>

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. <span data-ttu-id="ce81f-192">W `.nuspec` plików, odwołania tych plików w `<files>` węzła:</span><span class="sxs-lookup"><span data-stu-id="ce81f-192">In the `.nuspec` file, reference these files in the `<files>` node:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="ce81f-193">Utwórz pakiet ponownie, używając `nuget pack AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="ce81f-193">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>


### <a name="adding-a-readme"></a><span data-ttu-id="ce81f-194">Dodawanie pliku readme</span><span class="sxs-lookup"><span data-stu-id="ce81f-194">Adding a readme</span></span>

<span data-ttu-id="ce81f-195">Jeśli dołączysz `readme.txt` w katalogu głównym pakietu Visual Studio zostanie wyświetlona po zainstalowaniu pakietu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="ce81f-195">When you include a `readme.txt` file in the root of the package, Visual Studio will display it when the package is installed directly.</span></span>

> [!Note]
> <span data-ttu-id="ce81f-196">Pliki Readme nie są wyświetlane pakiety, które są zainstalowane jako zależność lub .NET Core projektów.</span><span class="sxs-lookup"><span data-stu-id="ce81f-196">Readme files are not shown for packages that are installed as a dependency, or for .NET Core projects.</span></span>


<span data-ttu-id="ce81f-197">W tym celu należy utworzyć użytkownika `readme.txt` pliku, umieść go w folderze głównym projektu i odwołuje się do niego w `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="ce81f-197">To do this, create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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


## <a name="net-standard-mapping-table"></a><span data-ttu-id="ce81f-198">.NET standard tabeli mapowania</span><span class="sxs-lookup"><span data-stu-id="ce81f-198">.NET Standard mapping table</span></span>

|<span data-ttu-id="ce81f-199">Nazwa platformy</span><span class="sxs-lookup"><span data-stu-id="ce81f-199">Platform Name</span></span> |<span data-ttu-id="ce81f-200">Alias</span><span class="sxs-lookup"><span data-stu-id="ce81f-200">Alias</span></span>|
|--------------|-----|
|<span data-ttu-id="ce81f-201">.NET standard</span><span class="sxs-lookup"><span data-stu-id="ce81f-201">.NET Standard</span></span> | <span data-ttu-id="ce81f-202">krótkich nazw netstandard</span><span class="sxs-lookup"><span data-stu-id="ce81f-202">netstandard</span></span>| <span data-ttu-id="ce81f-203">1.0</span><span class="sxs-lookup"><span data-stu-id="ce81f-203">1.0</span></span>| <span data-ttu-id="ce81f-204">1.1</span><span class="sxs-lookup"><span data-stu-id="ce81f-204">1.1</span></span>| <span data-ttu-id="ce81f-205">1.2</span><span class="sxs-lookup"><span data-stu-id="ce81f-205">1.2</span></span>| <span data-ttu-id="ce81f-206">1.3</span><span class="sxs-lookup"><span data-stu-id="ce81f-206">1.3</span></span>| <span data-ttu-id="ce81f-207">1.4</span><span class="sxs-lookup"><span data-stu-id="ce81f-207">1.4</span></span>| <span data-ttu-id="ce81f-208">1.5</span><span class="sxs-lookup"><span data-stu-id="ce81f-208">1.5</span></span>| <span data-ttu-id="ce81f-209">1.6</span><span class="sxs-lookup"><span data-stu-id="ce81f-209">1.6</span></span>|
|<span data-ttu-id="ce81f-210">.NET Core</span><span class="sxs-lookup"><span data-stu-id="ce81f-210">.NET Core</span></span> | <span data-ttu-id="ce81f-211">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="ce81f-211">netcoreapp</span></span>| <span data-ttu-id="ce81f-212">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-212">&#x2192;</span></span>| <span data-ttu-id="ce81f-213">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-213">&#x2192;</span></span>| <span data-ttu-id="ce81f-214">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-214">&#x2192;</span></span>| <span data-ttu-id="ce81f-215">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-215">&#x2192;</span></span>| <span data-ttu-id="ce81f-216">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-216">&#x2192;</span></span>| <span data-ttu-id="ce81f-217">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-217">&#x2192;</span></span>| <span data-ttu-id="ce81f-218">1.0</span><span class="sxs-lookup"><span data-stu-id="ce81f-218">1.0</span></span>|
|<span data-ttu-id="ce81f-219">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="ce81f-219">.NET Framework</span></span>| <span data-ttu-id="ce81f-220">NET</span><span class="sxs-lookup"><span data-stu-id="ce81f-220">net</span></span>| <span data-ttu-id="ce81f-221">4.5</span><span class="sxs-lookup"><span data-stu-id="ce81f-221">4.5</span></span>| <span data-ttu-id="ce81f-222">4.5.1</span><span class="sxs-lookup"><span data-stu-id="ce81f-222">4.5.1</span></span>| <span data-ttu-id="ce81f-223">4.6</span><span class="sxs-lookup"><span data-stu-id="ce81f-223">4.6</span></span>| <span data-ttu-id="ce81f-224">4.6.1</span><span class="sxs-lookup"><span data-stu-id="ce81f-224">4.6.1</span></span>| <span data-ttu-id="ce81f-225">4.6.2</span><span class="sxs-lookup"><span data-stu-id="ce81f-225">4.6.2</span></span>| <span data-ttu-id="ce81f-226">4.6.3</span><span class="sxs-lookup"><span data-stu-id="ce81f-226">4.6.3</span></span>|
|<span data-ttu-id="ce81f-227">Platformy mono/Xamarin</span><span class="sxs-lookup"><span data-stu-id="ce81f-227">Mono/Xamarin Platforms</span></span>| <span data-ttu-id="ce81f-228">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-228">&#x2192;</span></span>| <span data-ttu-id="ce81f-229">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-229">&#x2192;</span></span>| <span data-ttu-id="ce81f-230">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-230">&#x2192;</span></span>| <span data-ttu-id="ce81f-231">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-231">&#x2192;</span></span>| <span data-ttu-id="ce81f-232">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-232">&#x2192;</span></span>| <span data-ttu-id="ce81f-233">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-233">&#x2192;</span></span>|
|<span data-ttu-id="ce81f-234">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="ce81f-234">Universal Windows Platform</span></span>| <span data-ttu-id="ce81f-235">uap</span><span class="sxs-lookup"><span data-stu-id="ce81f-235">uap</span></span>| <span data-ttu-id="ce81f-236">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-236">&#x2192;</span></span>| <span data-ttu-id="ce81f-237">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-237">&#x2192;</span></span>| <span data-ttu-id="ce81f-238">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-238">&#x2192;</span></span>| <span data-ttu-id="ce81f-239">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-239">&#x2192;</span></span>|<span data-ttu-id="ce81f-240">10.0</span><span class="sxs-lookup"><span data-stu-id="ce81f-240">10.0</span></span>|
|<span data-ttu-id="ce81f-241">Windows</span><span class="sxs-lookup"><span data-stu-id="ce81f-241">Windows</span></span>| <span data-ttu-id="ce81f-242">win</span><span class="sxs-lookup"><span data-stu-id="ce81f-242">win</span></span>| <span data-ttu-id="ce81f-243">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-243">&#x2192;</span></span>| <span data-ttu-id="ce81f-244">8.0</span><span class="sxs-lookup"><span data-stu-id="ce81f-244">8.0</span></span>| <span data-ttu-id="ce81f-245">8.1</span><span class="sxs-lookup"><span data-stu-id="ce81f-245">8.1</span></span>|
|<span data-ttu-id="ce81f-246">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="ce81f-246">Windows Phone</span></span>| <span data-ttu-id="ce81f-247">WPA</span><span class="sxs-lookup"><span data-stu-id="ce81f-247">wpa</span></span>| <span data-ttu-id="ce81f-248">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-248">&#x2192;</span></span>| <span data-ttu-id="ce81f-249">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="ce81f-249">&#x2192;</span></span>|<span data-ttu-id="ce81f-250">8.1</span><span class="sxs-lookup"><span data-stu-id="ce81f-250">8.1</span></span>|
|<span data-ttu-id="ce81f-251">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="ce81f-251">Windows Phone Silverlight</span></span>| <span data-ttu-id="ce81f-252">WP</span><span class="sxs-lookup"><span data-stu-id="ce81f-252">wp</span></span>| <span data-ttu-id="ce81f-253">8.0</span><span class="sxs-lookup"><span data-stu-id="ce81f-253">8.0</span></span>|



## <a name="related-topics"></a><span data-ttu-id="ce81f-254">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="ce81f-254">Related topics</span></span>

- [<span data-ttu-id="ce81f-255">Plik Nuspec odwołania</span><span class="sxs-lookup"><span data-stu-id="ce81f-255">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="ce81f-256">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="ce81f-256">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="ce81f-257">Przechowywanie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="ce81f-257">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="ce81f-258">Obsługa wielu wersje programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="ce81f-258">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="ce81f-259">Zawiera właściwości programu MSBuild i obiektów docelowych w pakiecie</span><span class="sxs-lookup"><span data-stu-id="ce81f-259">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="ce81f-260">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="ce81f-260">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="ce81f-261">Dokumentacja biblioteki standardowej .NET</span><span class="sxs-lookup"><span data-stu-id="ce81f-261">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="ce81f-262">Eksportowanie do platformy .NET Core z .NET Framework</span><span class="sxs-lookup"><span data-stu-id="ce81f-262">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
