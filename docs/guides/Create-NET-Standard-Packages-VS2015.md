---
title: Tworzenie pakietów NuGet standard i platformy .NET Framework za pomocą programu Visual Studio 2015
description: End-to-end instruktaż tworzenia pakietów NuGet .NET Standard i .NET Framework przy użyciu nuget 3.x i Visual Studio 2015.
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: b16bf422e2627be3b8516a875d749639734064a9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380725"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="16422-103">Tworzenie pakietów programu .NET Standard i .NET Framework za pomocą programu Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="16422-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="16422-104">**Uwaga:** Visual Studio 2017 jest zalecane do tworzenia bibliotek .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="16422-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="16422-105">Visual Studio 2015 może działać, ale narzędzia .NET Core został przeniesiony tylko do stanu wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="16422-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="16422-106">Zobacz [Tworzenie i publikowanie pakietu z programem Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) do pracy z NuGet 4.x+ i Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="16422-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="16422-107">[Biblioteka standardowa platformy .NET](/dotnet/articles/standard/library) jest formalną specyfikacją interfejsów API platformy .NET, które mają być dostępne we wszystkich środowiskach uruchomieniowych platformy .NET, co zapewnia większą jednorodność w ekosystemie platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="16422-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="16422-108">Biblioteka standardowa platformy .NET definiuje jednolity zestaw interfejsów API BCL (Biblioteka klas podstawowych) dla wszystkich platform .NET do zaimplementowania, niezależnie od obciążenia.</span><span class="sxs-lookup"><span data-stu-id="16422-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="16422-109">Umożliwia deweloperom do tworzenia kodu, który jest użyteczny we wszystkich środowiskach uruchomieniowych .NET i zmniejsza, jeśli nie eliminuje dyrektywy kompilacji warunkowej specyficzne dla platformy w kodzie udostępnionym.</span><span class="sxs-lookup"><span data-stu-id="16422-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="16422-110">W tym przewodniku znajdziesz informacje o utworzeniu pakietu NuGet kierowanego na pakiet .NET Standard Library 1.4 lub pakietu docelowego .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="16422-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="16422-111">Biblioteka .NET Standard 1.4 działa w programie .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core i Mono/Xamarin.</span><span class="sxs-lookup"><span data-stu-id="16422-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="16422-112">Aby uzyskać szczegółowe informacje, zobacz [tabelę mapowania .NET Standard](/dotnet/standard/net-standard#net-implementation-support) (dokumentacja.NET).</span><span class="sxs-lookup"><span data-stu-id="16422-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="16422-113">W razie potrzeby można wybrać inną wersję biblioteki standardowej platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="16422-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16422-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16422-114">Prerequisites</span></span>

1. <span data-ttu-id="16422-115">Visual Studio 2015 Update 3</span><span class="sxs-lookup"><span data-stu-id="16422-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="16422-116">(tylko standard NET) [Podstawowy SDK .NET](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="16422-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="16422-117">Funkcja Interfejsu wiersza polecenia NuGet.</span><span class="sxs-lookup"><span data-stu-id="16422-117">NuGet CLI.</span></span> <span data-ttu-id="16422-118">Pobierz najnowszą wersję nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), zapisując ją w wybranej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="16422-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="16422-119">Następnie dodaj tę lokalizację do zmiennej środowiskowej PATH, jeśli jeszcze jej nie ma.</span><span class="sxs-lookup"><span data-stu-id="16422-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="16422-120">nuget.exe jest samo narzędzie CLI, a nie instalator, więc pamiętaj, aby zapisać pobrany plik z przeglądarki, zamiast go uruchamiać.</span><span class="sxs-lookup"><span data-stu-id="16422-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="16422-121">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="16422-121">Create the class library project</span></span>

1. <span data-ttu-id="16422-122">W programie Visual Studio **> programem File > Project**rozwiń węzeł > systemu Windows w programie Visual **C#,** wybierz **pozycję Biblioteka klas (przenośna)**, zmień nazwę na AppLogger i wybierz **przycisk OK**.</span><span class="sxs-lookup"><span data-stu-id="16422-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![Tworzenie nowego projektu biblioteki klas](media/NetStandard-NewProject.png)

1. <span data-ttu-id="16422-124">W wyświetlonym oknie dialogowym **Dodawanie biblioteki klas przenośnych** wybierz opcje dla `.NET Framework 4.6` i `ASP.NET Core 1.0`.</span><span class="sxs-lookup"><span data-stu-id="16422-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="16422-125">(Jeśli kierowanie .NET Framework, można wybrać, które opcje są odpowiednie.)</span><span class="sxs-lookup"><span data-stu-id="16422-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="16422-126">Jeśli kierowanie .NET Standard, `AppLogger (Portable)` kliknij prawym przyciskiem myszy w Eksploratorze **rozwiązań,** wybierz polecenie Właściwości , wybierz kartę **Biblioteka,** a następnie wybierz pozycję **Target .NET Platform Standard** w sekcji **Kierowanie.**</span><span class="sxs-lookup"><span data-stu-id="16422-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="16422-127">Ta akcja monituje o potwierdzenie, `.NET Standard 1.4` po czym można wybrać (lub inną dostępną wersję) z listy rozwijanej:</span><span class="sxs-lookup"><span data-stu-id="16422-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![Ustawianie obiektu docelowego na .NET Standard 1.4](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="16422-129">Kliknij kartę **Kompilacja,** zmień `Release` **konfigurację** na , a następnie zaznacz pole wyboru pliku dokumentacji **XML**.</span><span class="sxs-lookup"><span data-stu-id="16422-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="16422-130">Dodaj kod do składnika, na przykład:</span><span class="sxs-lookup"><span data-stu-id="16422-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="16422-131">Ustaw konfigurację na Zwolnij, skompiluj projekt i sprawdź, `bin\Release` czy pliki DLL i XML są tworzone w folderze.</span><span class="sxs-lookup"><span data-stu-id="16422-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="16422-132">Tworzenie i aktualizowanie pliku nuspec</span><span class="sxs-lookup"><span data-stu-id="16422-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="16422-133">Otwórz wiersz polecenia, przejdź do `AppLogger.csproj` folderu zawierającego folder `.sln` (jeden poziom poniżej, gdzie znajduje się plik) i uruchom polecenie NuGet, `spec` aby utworzyć plik początkowy: `AppLogger.nuspec`</span><span class="sxs-lookup"><span data-stu-id="16422-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="16422-134">Otwórz `AppLogger.nuspec` w edytorze i zaktualizuj go, aby dopasować go do następujących, zastępując YOUR_NAME odpowiednią wartością.</span><span class="sxs-lookup"><span data-stu-id="16422-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="16422-135">Wartość, `<id>` w szczególności, musi być unikatowa w nuget.org (zobacz konwencje nazewnictwa opisane w [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="16422-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="16422-136">Należy również pamiętać, że należy również zaktualizować tagi autora i opisu lub pojawi się błąd podczas kroku pakowania.</span><span class="sxs-lookup"><span data-stu-id="16422-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="16422-137">Dodaj zestawy odwołań `.nuspec` do pliku, a mianowicie biblioteki DLL i pliku IntelliSense XML:</span><span class="sxs-lookup"><span data-stu-id="16422-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="16422-138">W przypadku kierowania na standard .NET wpisy są podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="16422-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="16422-139">Jeśli kierowanie .NET Framework, wpisy są podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="16422-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="16422-140">Kliknij prawym przyciskiem myszy rozwiązanie i wybierz pozycję **Build Solution,** aby wygenerować wszystkie pliki dla pakietu.</span><span class="sxs-lookup"><span data-stu-id="16422-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="16422-141">Deklarowanie zależności</span><span class="sxs-lookup"><span data-stu-id="16422-141">Declaring dependencies</span></span>

<span data-ttu-id="16422-142">Jeśli masz żadnych zależności od innych pakietów NuGet, `<dependencies>` lista `<group>` tych w manifeście elementu z elementami.</span><span class="sxs-lookup"><span data-stu-id="16422-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="16422-143">Na przykład, aby zadeklarować zależność od NewtonSoft.Json 8.0.3 lub wyższej, dodaj następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="16422-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="16422-144">Składnia atrybutu *wersji* w tym miejscu wskazuje, że wersja 8.0.3 lub powyżej jest dopuszczalna.</span><span class="sxs-lookup"><span data-stu-id="16422-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="16422-145">Aby określić różne zakresy wersji, zobacz [Przechowywanie wersji pakietu](../concepts/package-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="16422-145">To specify different version ranges, refer to [Package versioning](../concepts/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="16422-146">Dodawanie readme</span><span class="sxs-lookup"><span data-stu-id="16422-146">Adding a readme</span></span>

<span data-ttu-id="16422-147">Utwórz `readme.txt` plik, umieść go w folderze głównym projektu `.nuspec` i odnieś się do niego w pliku:</span><span class="sxs-lookup"><span data-stu-id="16422-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="16422-148">Visual Studio `readme.txt` wyświetla, gdy pakiet jest zainstalowany w projekcie.</span><span class="sxs-lookup"><span data-stu-id="16422-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="16422-149">Plik nie jest wyświetlany po zainstalowaniu w projektach .NET Core lub dla pakietów, które są instalowane jako zależność.</span><span class="sxs-lookup"><span data-stu-id="16422-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="16422-150">Zapakuj składnik</span><span class="sxs-lookup"><span data-stu-id="16422-150">Package the component</span></span>

<span data-ttu-id="16422-151">Po zakończeniu `.nuspec` odwoływania się do wszystkich plików, które należy uwzględnić `pack` w pakiecie, możesz uruchomić polecenie:</span><span class="sxs-lookup"><span data-stu-id="16422-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="16422-152">To generuje `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="16422-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="16422-153">Otwierając ten plik w narzędziu, takim jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozwijając wszystkie węzły, zostanie wyświetlona następująca zawartość (pokazana dla platformy .NET Standard):</span><span class="sxs-lookup"><span data-stu-id="16422-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![Eksplorator pakietów NuGet z pakietem AppLogger](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="16422-155">Plik `.nupkg` to tylko plik ZIP z innym rozszerzeniem.</span><span class="sxs-lookup"><span data-stu-id="16422-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="16422-156">Możesz również sprawdzić zawartość pakietu, `.nupkg` a `.zip`następnie, zmieniając na , ale pamiętaj, aby przywrócić rozszerzenie przed przesłaniem pakietu do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="16422-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="16422-157">Aby udostępnić pakiet innym deweloperom, postępuj zgodnie z instrukcjami dotyczącymi [publikowania pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="16422-157">To make your package available to other developers, follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="16422-158">Należy `pack` pamiętać, że wymaga Mono 4.4.2 na Mac OS X i nie działa na systemach Linux.</span><span class="sxs-lookup"><span data-stu-id="16422-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="16422-159">Na komputerze Mac należy również przekonwertować `.nuspec` nazwy ścieżek systemu Windows w pliku na ścieżki w stylu Uniksa.</span><span class="sxs-lookup"><span data-stu-id="16422-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="16422-160">Powiązane tematy</span><span class="sxs-lookup"><span data-stu-id="16422-160">Related topics</span></span>

- [<span data-ttu-id="16422-161">Odwołanie .nuspec</span><span class="sxs-lookup"><span data-stu-id="16422-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="16422-162">Obsługa wielu wersji programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="16422-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="16422-163">Uwzględnij rekwizyty i obiekty docelowe MSBuild w pakiecie</span><span class="sxs-lookup"><span data-stu-id="16422-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="16422-164">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="16422-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="16422-165">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="16422-165">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="16422-166">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="16422-166">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="16422-167">Dokumentacja biblioteki standardowej platformy .NET</span><span class="sxs-lookup"><span data-stu-id="16422-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="16422-168">Przenoszenie do rdzenia net z platformy .NET Framework</span><span class="sxs-lookup"><span data-stu-id="16422-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
