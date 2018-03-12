---
title: "Tworzenie pakietów NuGet standardowe .NET z programem Visual Studio 2015 | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Przewodnik end-to-end tworzenia pakietów NuGet programu .NET Standard przy użyciu narzędzia NuGet 3.x i programu Visual Studio 2015."
keywords: "Tworzenie pakietu, .NET Standard pakietów, .NET Standard tabeli mapowania"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c15ffd709856fc9d5b9a9fb2fe87c0029b82650d
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/08/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="00bc0-104">Utwórz pakiety .NET Standard z programem Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="00bc0-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="00bc0-105">*Dotyczy NuGet 3.x. Zobacz [tworzenie i publikowanie pakietu z programu Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) do pracy z NuGet 4.x+.*</span><span class="sxs-lookup"><span data-stu-id="00bc0-105">*Applies to NuGet 3.x. See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="00bc0-106">[Biblioteki standardowej .NET](/dotnet/articles/standard/library) jest formalną specyfikację interfejsów API architektury .NET mają być dostępne na wszystkich środowisk uruchomieniowych .NET, w związku z tym ustanawianie większej jednolitości w ekosystemie .NET.</span><span class="sxs-lookup"><span data-stu-id="00bc0-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="00bc0-107">Standardowa biblioteka .NET definiuje zestaw uniform BCL (Biblioteka klasy podstawowej) interfejsów API dla wszystkich platform .NET zaimplementować, niezależnie od obciążenia.</span><span class="sxs-lookup"><span data-stu-id="00bc0-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="00bc0-108">Umożliwia ona deweloperom tworzyć kod, który jest można używać we wszystkich programów .NET i zmniejsza Jeśli nie eliminuje dyrektywy kompilacja warunkowa specyficzne dla platformy w kodzie udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="00bc0-108">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="00bc0-109">Ten przewodnik przeprowadzi Cię przez proces tworzenia pakietu NuGet przeznaczonych dla platformy .NET Standard biblioteki 1.4.</span><span class="sxs-lookup"><span data-stu-id="00bc0-109">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="00bc0-110">Takie biblioteki działa za pośrednictwem platformy .NET Framework 4.6.1, uniwersalnych systemu Windows 10 platformy .NET Core i Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="00bc0-110">Such a library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="00bc0-111">Aby uzyskać więcej informacji, zobacz [.NET Standard tabeli mapowania](#net-standard-mapping-table) dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="00bc0-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00bc0-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="00bc0-112">Prerequisites</span></span>

1. <span data-ttu-id="00bc0-113">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="00bc0-113">Visual Studio 2015 Update 3</span></span>
1. [<span data-ttu-id="00bc0-114">Oprogramowanie .NET core SDK</span><span class="sxs-lookup"><span data-stu-id="00bc0-114">.NET Core SDK</span></span>](https://www.microsoft.com/net/download/)
1. <span data-ttu-id="00bc0-115">Interfejs wiersza polecenia NuGet.</span><span class="sxs-lookup"><span data-stu-id="00bc0-115">NuGet CLI.</span></span> <span data-ttu-id="00bc0-116">Pobierz najnowszą wersję nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), zapisać go do wybranej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="00bc0-116">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="00bc0-117">Dodać tej lokalizacji do Twojej zmiennej środowiskowej PATH, gdy nie jest jeszcze.</span><span class="sxs-lookup"><span data-stu-id="00bc0-117">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="00bc0-118">nuget.exe to narzędzie interfejsu wiersza polecenia, nie Instalatora, dlatego należy Zapisz pobrany plik z przeglądarki, a jego uruchomieniem.</span><span class="sxs-lookup"><span data-stu-id="00bc0-118">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="00bc0-119">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="00bc0-119">Create the class library project</span></span>

1. <span data-ttu-id="00bc0-120">W programie Visual Studio **Plik > Nowy > projektu**, rozwiń węzeł **Visual C# > Windows** węzła, wybierz opcję **biblioteki klas (przenośna)**, Zmień nazwę na AppLogger i kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="00bc0-120">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![Tworzenie nowego projektu biblioteki klas](media/NetStandard-NewProject.png)

1. <span data-ttu-id="00bc0-122">W **dodać przenośnej biblioteki klas** okno dialogowe zostanie wyświetlone, wybierz `.NET Framework 4.6` i `ASP.NET Core 1.0` opcje.</span><span class="sxs-lookup"><span data-stu-id="00bc0-122">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>

1. <span data-ttu-id="00bc0-123">Kliknij prawym przyciskiem myszy `AppLogger (Portable)` w Eksploratorze rozwiązań wybierz **właściwości**, wybierz pozycję **biblioteki** , a następnie kliknij **docelowej platformy .NET Standard** w **Przeznaczonych dla** sekcji.</span><span class="sxs-lookup"><span data-stu-id="00bc0-123">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="00bc0-124">Ten monit o potwierdzenie, po którym można wybrać `.NET Standard 1.4` z listy rozwijanej:</span><span class="sxs-lookup"><span data-stu-id="00bc0-124">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![Ustawienie docelowej platformy .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="00bc0-126">Polecenie **kompilacji** Zmień **konfiguracji** do `Release`i pole wyboru dla **pliku dokumentacji XML**.</span><span class="sxs-lookup"><span data-stu-id="00bc0-126">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="00bc0-127">Dodaj swój kod do składnika, na przykład:</span><span class="sxs-lookup"><span data-stu-id="00bc0-127">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="00bc0-128">Ustaw konfigurację do wersji, skompilować projekt i sprawdź, czy biblioteka DLL, pliki XML są tworzone w ramach `bin\Release` folderu.</span><span class="sxs-lookup"><span data-stu-id="00bc0-128">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="00bc0-129">Tworzenie i aktualizowanie pliku .nuspec</span><span class="sxs-lookup"><span data-stu-id="00bc0-129">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="00bc0-130">Otwórz wiersz polecenia, przejdź do folderu zawierającego `AppLogger.csproj` folder (jeden poziom w dół where `.sln` pliku), i uruchom NuGet `spec` polecenie, aby utworzyć pierwszy `AppLogger.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="00bc0-130">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```cli
nuget spec
```

1. <span data-ttu-id="00bc0-131">Otwórz `AppLogger.nuspec` w edytorze i zaktualizować je zgodnie z poniższym, zamieniając twoje_imie odpowiednią wartość.</span><span class="sxs-lookup"><span data-stu-id="00bc0-131">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="00bc0-132">`<id>` Wartość, w szczególności musi być unikatowa w nuget.org (konwencje nazewnictwa opisane w temacie [utworzenie pakietu](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="00bc0-132">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="00bc0-133">Należy również zauważyć, że należy również zaktualizować tagi autora oraz opis lub wystąpi błąd podczas wykonywania kroku pakowania.</span><span class="sxs-lookup"><span data-stu-id="00bc0-133">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="00bc0-134">Dodaj zestawy odwołań `.nuspec` plików, to znaczy biblioteki DLL i pliku IntelliSense XML:</span><span class="sxs-lookup"><span data-stu-id="00bc0-134">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="00bc0-135">Kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz **Kompiluj rozwiązanie** do wygenerowania wszystkich plików w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="00bc0-135">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="00bc0-136">Deklarowanie zależności</span><span class="sxs-lookup"><span data-stu-id="00bc0-136">Declaring dependencies</span></span>

<span data-ttu-id="00bc0-137">Jeśli jest zależne od innych pakietów NuGet, listy w manifeście `<dependencies>` element z `<group>` elementów.</span><span class="sxs-lookup"><span data-stu-id="00bc0-137">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="00bc0-138">Na przykład aby zadeklarować zależność w NewtonSoft.Json 8.0.3 lub nowszym, należy dodać:</span><span class="sxs-lookup"><span data-stu-id="00bc0-138">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="00bc0-139">Składnia *wersji* tutaj wskazuje, czy w wersji 8.0.3 lub nowszy jest dopuszczalne atrybutu.</span><span class="sxs-lookup"><span data-stu-id="00bc0-139">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="00bc0-140">Aby określić inną wersję zakresów, zapoznaj się [wersji pakietu](../reference/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="00bc0-140">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="00bc0-141">Dodawanie pliku readme</span><span class="sxs-lookup"><span data-stu-id="00bc0-141">Adding a readme</span></span>

<span data-ttu-id="00bc0-142">Tworzenie sieci `readme.txt` pliku, umieść go w folderze głównym projektu i odwołuje się do niego w `.nuspec` pliku:</span><span class="sxs-lookup"><span data-stu-id="00bc0-142">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="00bc0-143">Visual Studio wyświetlania `readme.txt` po zainstalowaniu pakietu do projektu.</span><span class="sxs-lookup"><span data-stu-id="00bc0-143">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="00bc0-144">Plik nie jest wyświetlane, gdy zainstalowane w projektach platformy .NET Core lub pakietów, które są zainstalowane jako zależność.</span><span class="sxs-lookup"><span data-stu-id="00bc0-144">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="00bc0-145">Pakiet składnika</span><span class="sxs-lookup"><span data-stu-id="00bc0-145">Package the component</span></span>

<span data-ttu-id="00bc0-146">Z ukończonej `.nuspec` odwołuje się do wszystkich plików, które należy uwzględnić w pakiecie, wszystko jest gotowe do uruchomienia `pack` polecenia:</span><span class="sxs-lookup"><span data-stu-id="00bc0-146">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="00bc0-147">Spowoduje to wygenerowanie `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="00bc0-147">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="00bc0-148">Otwarcie tego pliku w narzędzia, takiego jak [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzanie wszystkich węzłów, zobacz następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="00bc0-148">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Wyświetlanie pakietu AppLogger Explorer pakietu NuGet](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="00bc0-150">A `.nupkg` plik jest tylko plik ZIP zawierający inne rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="00bc0-150">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="00bc0-151">Można również sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale pamiętaj, aby przywrócić rozszerzenia przed przekazaniem do nuget.org pakietu.</span><span class="sxs-lookup"><span data-stu-id="00bc0-151">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="00bc0-152">Aby udostępnić pakietu inni deweloperzy, postępuj zgodnie z instrukcjami [opublikowania pakietu](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="00bc0-152">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="00bc0-153">Należy pamiętać, że `pack` wymaga Mono 4.4.2 w systemie Mac OS X i nie działa w systemach Linux.</span><span class="sxs-lookup"><span data-stu-id="00bc0-153">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="00bc0-154">Na komputerze Mac, należy także przekonwertować nazwy ścieżek systemu Windows w `.nuspec` pliku do ścieżki typu Unix.</span><span class="sxs-lookup"><span data-stu-id="00bc0-154">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="net-standard-mapping-table"></a><span data-ttu-id="00bc0-155">.NET standard tabeli mapowania</span><span class="sxs-lookup"><span data-stu-id="00bc0-155">.NET Standard mapping table</span></span>

| <span data-ttu-id="00bc0-156">Nazwa platformy</span><span class="sxs-lookup"><span data-stu-id="00bc0-156">Platform Name</span></span> | <span data-ttu-id="00bc0-157">Alias</span><span class="sxs-lookup"><span data-stu-id="00bc0-157">Alias</span></span> |
| --- | --- |
| <span data-ttu-id="00bc0-158">.NET standard</span><span class="sxs-lookup"><span data-stu-id="00bc0-158">.NET Standard</span></span> | <span data-ttu-id="00bc0-159">krótkich nazw netstandard</span><span class="sxs-lookup"><span data-stu-id="00bc0-159">netstandard</span></span> | <span data-ttu-id="00bc0-160">1.0</span><span class="sxs-lookup"><span data-stu-id="00bc0-160">1.0</span></span> | <span data-ttu-id="00bc0-161">1.1</span><span class="sxs-lookup"><span data-stu-id="00bc0-161">1.1</span></span> | <span data-ttu-id="00bc0-162">1.2</span><span class="sxs-lookup"><span data-stu-id="00bc0-162">1.2</span></span> | <span data-ttu-id="00bc0-163">1.3</span><span class="sxs-lookup"><span data-stu-id="00bc0-163">1.3</span></span> | <span data-ttu-id="00bc0-164">1.4</span><span class="sxs-lookup"><span data-stu-id="00bc0-164">1.4</span></span> | <span data-ttu-id="00bc0-165">1.5</span><span class="sxs-lookup"><span data-stu-id="00bc0-165">1.5</span></span> | <span data-ttu-id="00bc0-166">1.6</span><span class="sxs-lookup"><span data-stu-id="00bc0-166">1.6</span></span> |
| <span data-ttu-id="00bc0-167">.NET Core</span><span class="sxs-lookup"><span data-stu-id="00bc0-167">.NET Core</span></span> | <span data-ttu-id="00bc0-168">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="00bc0-168">netcoreapp</span></span> | <span data-ttu-id="00bc0-169">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-169">&#x2192;</span></span> | <span data-ttu-id="00bc0-170">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-170">&#x2192;</span></span> | <span data-ttu-id="00bc0-171">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-171">&#x2192;</span></span> | <span data-ttu-id="00bc0-172">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-172">&#x2192;</span></span> | <span data-ttu-id="00bc0-173">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-173">&#x2192;</span></span> | <span data-ttu-id="00bc0-174">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-174">&#x2192;</span></span> | <span data-ttu-id="00bc0-175">1.0</span><span class="sxs-lookup"><span data-stu-id="00bc0-175">1.0</span></span> |
| <span data-ttu-id="00bc0-176">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="00bc0-176">.NET Framework</span></span> | <span data-ttu-id="00bc0-177">NET</span><span class="sxs-lookup"><span data-stu-id="00bc0-177">net</span></span> | <span data-ttu-id="00bc0-178">4.5</span><span class="sxs-lookup"><span data-stu-id="00bc0-178">4.5</span></span> | <span data-ttu-id="00bc0-179">4.5.1</span><span class="sxs-lookup"><span data-stu-id="00bc0-179">4.5.1</span></span> | <span data-ttu-id="00bc0-180">4.6</span><span class="sxs-lookup"><span data-stu-id="00bc0-180">4.6</span></span> | <span data-ttu-id="00bc0-181">4.6.1</span><span class="sxs-lookup"><span data-stu-id="00bc0-181">4.6.1</span></span> | <span data-ttu-id="00bc0-182">4.6.2</span><span class="sxs-lookup"><span data-stu-id="00bc0-182">4.6.2</span></span> | <span data-ttu-id="00bc0-183">4.6.3</span><span class="sxs-lookup"><span data-stu-id="00bc0-183">4.6.3</span></span> |
| <span data-ttu-id="00bc0-184">Platformy mono/Xamarin</span><span class="sxs-lookup"><span data-stu-id="00bc0-184">Mono/Xamarin Platforms</span></span> | <span data-ttu-id="00bc0-185">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-185">&#x2192;</span></span> | <span data-ttu-id="00bc0-186">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-186">&#x2192;</span></span> | <span data-ttu-id="00bc0-187">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-187">&#x2192;</span></span> | <span data-ttu-id="00bc0-188">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-188">&#x2192;</span></span> | <span data-ttu-id="00bc0-189">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-189">&#x2192;</span></span> | <span data-ttu-id="00bc0-190">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-190">&#x2192;</span></span> |
| <span data-ttu-id="00bc0-191">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="00bc0-191">Universal Windows Platform</span></span> | <span data-ttu-id="00bc0-192">uap</span><span class="sxs-lookup"><span data-stu-id="00bc0-192">uap</span></span> | <span data-ttu-id="00bc0-193">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-193">&#x2192;</span></span> | <span data-ttu-id="00bc0-194">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-194">&#x2192;</span></span> | <span data-ttu-id="00bc0-195">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-195">&#x2192;</span></span> | <span data-ttu-id="00bc0-196">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-196">&#x2192;</span></span> |<span data-ttu-id="00bc0-197">10.0</span><span class="sxs-lookup"><span data-stu-id="00bc0-197">10.0</span></span> |
| <span data-ttu-id="00bc0-198">Windows</span><span class="sxs-lookup"><span data-stu-id="00bc0-198">Windows</span></span> | <span data-ttu-id="00bc0-199">win</span><span class="sxs-lookup"><span data-stu-id="00bc0-199">win</span></span>| <span data-ttu-id="00bc0-200">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-200">&#x2192;</span></span> | <span data-ttu-id="00bc0-201">8.0</span><span class="sxs-lookup"><span data-stu-id="00bc0-201">8.0</span></span> | <span data-ttu-id="00bc0-202">8.1</span><span class="sxs-lookup"><span data-stu-id="00bc0-202">8.1</span></span> |
| <span data-ttu-id="00bc0-203">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="00bc0-203">Windows Phone</span></span> | <span data-ttu-id="00bc0-204">WPA</span><span class="sxs-lookup"><span data-stu-id="00bc0-204">wpa</span></span>| <span data-ttu-id="00bc0-205">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-205">&#x2192;</span></span>| <span data-ttu-id="00bc0-206">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="00bc0-206">&#x2192;</span></span> | <span data-ttu-id="00bc0-207">8.1</span><span class="sxs-lookup"><span data-stu-id="00bc0-207">8.1</span></span> |
| <span data-ttu-id="00bc0-208">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="00bc0-208">Windows Phone Silverlight</span></span> | <span data-ttu-id="00bc0-209">WP</span><span class="sxs-lookup"><span data-stu-id="00bc0-209">wp</span></span> | <span data-ttu-id="00bc0-210">8.0</span><span class="sxs-lookup"><span data-stu-id="00bc0-210">8.0</span></span> |

## <a name="related-topics"></a><span data-ttu-id="00bc0-211">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="00bc0-211">Related topics</span></span>

- [<span data-ttu-id="00bc0-212">odwołanie .nuspec</span><span class="sxs-lookup"><span data-stu-id="00bc0-212">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="00bc0-213">Obsługa wielu wersje programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="00bc0-213">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="00bc0-214">Zawiera właściwości programu MSBuild i obiektów docelowych w pakiecie</span><span class="sxs-lookup"><span data-stu-id="00bc0-214">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="00bc0-215">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="00bc0-215">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="00bc0-216">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="00bc0-216">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="00bc0-217">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="00bc0-217">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="00bc0-218">Dokumentacja biblioteki standardowej .NET</span><span class="sxs-lookup"><span data-stu-id="00bc0-218">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="00bc0-219">Eksportowanie do platformy .NET Core z .NET Framework</span><span class="sxs-lookup"><span data-stu-id="00bc0-219">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
