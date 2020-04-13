---
title: Tworzenie pakietów NuGet dla platformy Xamarin (dla systemów iOS, Android i Windows) za pomocą programu Visual Studio 2017 lub 2019
description: End-to-end instruktaż tworzenia pakietów NuGet dla platformy Xamarin, które używają natywnych interfejsów API w systemach iOS, Android i Windows.
author: karann-msft
ms.author: karann
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: 0cb653bad9e853d908039b3f7a94e1dd7eefdde5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230905"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a><span data-ttu-id="7ba23-103">Tworzenie pakietów dla platformy Xamarin za pomocą programu Visual Studio 2017 lub 2019</span><span class="sxs-lookup"><span data-stu-id="7ba23-103">Create packages for Xamarin with Visual Studio 2017 or 2019</span></span>

<span data-ttu-id="7ba23-104">Pakiet dla platformy Xamarin zawiera kod, który używa natywnych interfejsów API w systemach iOS, Android i Windows, w zależności od systemu operacyjnego w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="7ba23-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="7ba23-105">Mimo że jest to proste do zrobienia, lepiej jest pozwolić deweloperom korzystać z pakietu z bibliotek PCL lub .NET Standard za pośrednictwem wspólnego obszaru powierzchni interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="7ba23-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="7ba23-106">W tym instruktażu można użyć programu Visual Studio 2017 lub 2019 do utworzenia wieloplatformowego pakietu NuGet, który może być używany w projektach mobilnych w systemach iOS, Android i Windows.</span><span class="sxs-lookup"><span data-stu-id="7ba23-106">In this walkthrough you use Visual Studio 2017 or 2019 to create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="7ba23-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7ba23-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="7ba23-108">Tworzenie struktury projektu i kodu abstrakcji</span><span class="sxs-lookup"><span data-stu-id="7ba23-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="7ba23-109">Napisz kod specyficzny dla platformy</span><span class="sxs-lookup"><span data-stu-id="7ba23-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="7ba23-110">Tworzenie i aktualizowanie pliku nuspec</span><span class="sxs-lookup"><span data-stu-id="7ba23-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="7ba23-111">Zapakuj składnik</span><span class="sxs-lookup"><span data-stu-id="7ba23-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="7ba23-112">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="7ba23-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="7ba23-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7ba23-113">Prerequisites</span></span>

1. <span data-ttu-id="7ba23-114">Visual Studio 2017 lub 2019 z uniwersalną platformą systemu Windows (UWP) i platformą Xamarin.</span><span class="sxs-lookup"><span data-stu-id="7ba23-114">Visual Studio 2017 or 2019 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="7ba23-115">Zainstaluj wersję wspólnotową bezpłatnie od [visualstudio.com;](https://www.visualstudio.com/) oczywiście można również korzystać z wersji Professional i Enterprise.</span><span class="sxs-lookup"><span data-stu-id="7ba23-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="7ba23-116">Aby uwzględnić narzędzia platformy uniwersalnej systemu Windows i platformy Xamarin, wybierz instalację niestandardową i sprawdź odpowiednie opcje.</span><span class="sxs-lookup"><span data-stu-id="7ba23-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="7ba23-117">Funkcja Interfejsu wiersza polecenia NuGet.</span><span class="sxs-lookup"><span data-stu-id="7ba23-117">NuGet CLI.</span></span> <span data-ttu-id="7ba23-118">Pobierz najnowszą wersję nuget.exe z [nuget.org/downloads](https://nuget.org/downloads), zapisując ją w wybranej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="7ba23-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="7ba23-119">Następnie dodaj tę lokalizację do zmiennej środowiskowej PATH, jeśli jeszcze jej nie ma.</span><span class="sxs-lookup"><span data-stu-id="7ba23-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="7ba23-120">nuget.exe jest samo narzędzie CLI, a nie instalator, więc pamiętaj, aby zapisać pobrany plik z przeglądarki, zamiast go uruchamiać.</span><span class="sxs-lookup"><span data-stu-id="7ba23-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="7ba23-121">Tworzenie struktury projektu i kodu abstrakcji</span><span class="sxs-lookup"><span data-stu-id="7ba23-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="7ba23-122">Pobierz i uruchom [rozszerzenie szablonów standardowych wtyczek platformy .NET](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ba23-122">Download and run the [Cross-Platform .NET Standard Plugin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="7ba23-123">Te szablony ułatwią tworzenie niezbędnej struktury projektu dla tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="7ba23-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="7ba23-124">W programie Visual Studio 2017 **> plik nowego projektu**> `Plugin`, wyszukaj , wybierz szablon **wtyczki biblioteki standardowej .NET na wielu platformach,** zmień nazwę na LoggingLibrary i kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="7ba23-124">In Visual Studio 2017, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Nowy projekt pustej aplikacji (Xamarin.Forms Portable) w programie VS 2017](media/CrossPlatform-NewProject.png)

    <span data-ttu-id="7ba23-126">W programie Visual Studio 2019 **> plik nowego projektu**> `Plugin`, wyszukaj , wybierz szablon **wtyczki biblioteki standardowej platformy .NET** i kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="7ba23-126">In Visual Studio 2019, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, and click Next.</span></span>

    ![Nowy projekt pustej aplikacji (Xamarin.Forms Portable) w programie VS 2019](media/CrossPlatform-NewProject19-Part1.png)

    <span data-ttu-id="7ba23-128">Zmień nazwę na LoggingLibrary i kliknij przycisk Utwórz.</span><span class="sxs-lookup"><span data-stu-id="7ba23-128">Change the name to LoggingLibrary, and click Create.</span></span>

    ![Nowa pusta aplikacja (Xamarin.Forms Portable) w programie VS 2019](media/CrossPlatform-NewProject19-Part2.png)

<span data-ttu-id="7ba23-130">Wynikowe rozwiązanie zawiera dwa projekty współużytkowane, wraz z różnymi projektami specyficznymi dla platformy:</span><span class="sxs-lookup"><span data-stu-id="7ba23-130">The resulting solution contains two Shared projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="7ba23-131">Projekt, `ILoggingLibrary` który znajduje się `ILoggingLibrary.shared.cs` w pliku, definiuje interfejs publiczny (obszar powierzchni INTERFEJSU API) składnika.</span><span class="sxs-lookup"><span data-stu-id="7ba23-131">The `ILoggingLibrary` project, which is contained in the `ILoggingLibrary.shared.cs` file, defines the public interface (the API surface area) of the component.</span></span> <span data-ttu-id="7ba23-132">W tym miejscu można zdefiniować interfejs do biblioteki.</span><span class="sxs-lookup"><span data-stu-id="7ba23-132">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="7ba23-133">Inny udostępniony projekt zawiera `CrossLoggingLibrary.shared.cs` kod, w którym będzie zlokalizować implementacji specyficzne dla platformy abstrakcyjnego interfejsu w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="7ba23-133">The other Shared project contains code in `CrossLoggingLibrary.shared.cs` that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="7ba23-134">Zazwyczaj nie trzeba modyfikować tego pliku.</span><span class="sxs-lookup"><span data-stu-id="7ba23-134">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="7ba23-135">Projekty specyficzne dla platformy, `LoggingLibrary.android.cs`takie jak , każdy zawiera natywną implementację interfejsu w odpowiednich plikach `LoggingLibraryImplementation.cs` (VS 2017) lub `LoggingLibrary.<PLATFORM>.cs` (VS 2019).</span><span class="sxs-lookup"><span data-stu-id="7ba23-135">The platform-specific projects, such as `LoggingLibrary.android.cs`, each contain a native implementation of the interface in their respective `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) files.</span></span> <span data-ttu-id="7ba23-136">W tym miejscu można utworzyć kod biblioteki.</span><span class="sxs-lookup"><span data-stu-id="7ba23-136">This is where you build out your library's code.</span></span>

<span data-ttu-id="7ba23-137">Domyślnie ILoggingLibrary.shared.cs plik `ILoggingLibrary` projektu zawiera definicję interfejsu, ale nie ma metod.</span><span class="sxs-lookup"><span data-stu-id="7ba23-137">By default, the ILoggingLibrary.shared.cs file of the `ILoggingLibrary` project contains an interface definition, but no methods.</span></span> <span data-ttu-id="7ba23-138">Na potrzeby tego przewodnika należy dodać `Log` metodę w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="7ba23-138">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;
using System.Collections.Generic;
using System.Text;

namespace Plugin.LoggingLibrary
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="7ba23-139">Napisz kod specyficzny dla platformy</span><span class="sxs-lookup"><span data-stu-id="7ba23-139">Write your platform-specific code</span></span>

<span data-ttu-id="7ba23-140">Aby zaimplementować implementację `ILoggingLibrary` interfejsu i jego metod specyficznych dla platformy, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7ba23-140">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="7ba23-141">Otwórz `LoggingLibraryImplementation.cs` plik (VS 2017) lub `LoggingLibrary.<PLATFORM>.cs` (VS 2019) każdego projektu platformy i dodaj niezbędny kod.</span><span class="sxs-lookup"><span data-stu-id="7ba23-141">Open the `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) file of each platform project and add the necessary code.</span></span> <span data-ttu-id="7ba23-142">Na przykład (przy użyciu projektu `Android` platformy):</span><span class="sxs-lookup"><span data-stu-id="7ba23-142">For example (using the `Android` platform project):</span></span>

    ```cs
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. <span data-ttu-id="7ba23-143">Powtórz tę implementację w projektach dla każdej platformy, którą chcesz obsługiwać.</span><span class="sxs-lookup"><span data-stu-id="7ba23-143">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="7ba23-144">Kliknij prawym przyciskiem myszy rozwiązanie i wybierz opcję **Buduj rozwiązanie,** aby sprawdzić swoją pracę i utworzyć artefakty, które można spakować w następnej kolejności.</span><span class="sxs-lookup"><span data-stu-id="7ba23-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="7ba23-145">Jeśli pojawia się błędy dotyczące brakujących odwołań, kliknij prawym przyciskiem myszy rozwiązanie, wybierz **pozycję Przywróć pakiety NuGet,** aby zainstalować zależności i odbudować.</span><span class="sxs-lookup"><span data-stu-id="7ba23-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="7ba23-146">Jeśli używasz programu Visual Studio 2019, przed wybraniem **opcji Przywróć pakiety NuGet** i próbą przebudowy należy zmienić wersję `MSBuild.Sdk.Extras` `2.0.54` na w `LoggingLibrary.csproj`programie .</span><span class="sxs-lookup"><span data-stu-id="7ba23-146">If you are using Visual Studio 2019, before selecting **Restore NuGet Packages** and trying to rebuild, you need to change the version of `MSBuild.Sdk.Extras` to `2.0.54` in `LoggingLibrary.csproj`.</span></span> <span data-ttu-id="7ba23-147">Dostęp do tego pliku można uzyskać tylko po kliknięciu prawym przyciskiem `Unload Project`myszy projektu (poniżej rozwiązania) i `Edit LoggingLibrary.csproj`wybraniu , po czym kliknij prawym przyciskiem myszy niezaładowany projekt i wybierz .</span><span class="sxs-lookup"><span data-stu-id="7ba23-147">This file can only be accessed by first right-clicking the project (below the solution) and selecting `Unload Project`, after which you right-click on the unloaded project and select `Edit LoggingLibrary.csproj`.</span></span>

> [!Note]
> <span data-ttu-id="7ba23-148">Do tworzenia dla systemu iOS potrzebny jest komputer Mac połączony z programem Visual Studio zgodnie z opisem w [programie Wprowadzenie do pliku Xamarin.iOS for Visual Studio.](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)</span><span class="sxs-lookup"><span data-stu-id="7ba23-148">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="7ba23-149">Jeśli nie masz dostępnego komputera Mac, wyczyść projekt systemu iOS w menedżerze konfiguracji (krok 3 powyżej).</span><span class="sxs-lookup"><span data-stu-id="7ba23-149">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="7ba23-150">Tworzenie i aktualizowanie pliku nuspec</span><span class="sxs-lookup"><span data-stu-id="7ba23-150">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="7ba23-151">Otwórz wiersz polecenia, przejdź `LoggingLibrary` do folderu znajdującego `.sln` się na jednym poziomie `spec` poniżej miejsca, `Package.nuspec` w którym znajduje się plik, i uruchom polecenie NuGet, aby utworzyć plik początkowy:</span><span class="sxs-lookup"><span data-stu-id="7ba23-151">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="7ba23-152">Zmień nazwę tego `LoggingLibrary.nuspec` pliku i otwórz go w edytorze.</span><span class="sxs-lookup"><span data-stu-id="7ba23-152">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="7ba23-153">Zaktualizuj plik, aby dopasować go do następujących, zastępując YOUR_NAME odpowiednią wartością.</span><span class="sxs-lookup"><span data-stu-id="7ba23-153">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="7ba23-154">Wartość, `<id>` w szczególności, musi być unikatowa w nuget.org (zobacz konwencje nazewnictwa opisane w [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="7ba23-154">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="7ba23-155">Należy również pamiętać, że należy również zaktualizować tagi autora i opisu lub pojawi się błąd podczas kroku pakowania.</span><span class="sxs-lookup"><span data-stu-id="7ba23-155">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="7ba23-156">Możesz sufiks wersji `-alpha`pakietu `-beta` `-rc` z , lub oznaczyć pakiet jako wersji wstępnej, sprawdź [wersje przed wydaniem, aby](../create-packages/prerelease-packages.md) uzyskać więcej informacji na temat wersji przed wydaniem.</span><span class="sxs-lookup"><span data-stu-id="7ba23-156">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="7ba23-157">Dodawanie zestawów referencyjnych</span><span class="sxs-lookup"><span data-stu-id="7ba23-157">Add reference assemblies</span></span>

<span data-ttu-id="7ba23-158">Aby uwzględnić zestawy odwołań specyficzne dla `<files>` platformy, `LoggingLibrary.nuspec` dodaj następujące elementy do elementu odpowiednio dla obsługiwanych platform:</span><span class="sxs-lookup"><span data-stu-id="7ba23-158">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> <span data-ttu-id="7ba23-159">Aby skrócić nazwy plików DLL i XML, kliknij prawym przyciskiem myszy dowolny projekt, wybierz kartę **Biblioteka** i zmień nazwy zestawów.</span><span class="sxs-lookup"><span data-stu-id="7ba23-159">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="7ba23-160">Dodawanie zależności</span><span class="sxs-lookup"><span data-stu-id="7ba23-160">Add dependencies</span></span>

<span data-ttu-id="7ba23-161">Jeśli masz określone zależności dla implementacji `<dependencies>` natywnych, użyj elementu z `<group>` elementami, aby je określić, na przykład:</span><span class="sxs-lookup"><span data-stu-id="7ba23-161">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

<span data-ttu-id="7ba23-162">Na przykład następujące ustawić iTextSharp jako zależność dla obiektu docelowego UAP:</span><span class="sxs-lookup"><span data-stu-id="7ba23-162">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="7ba23-163">Końcowy .nuspec</span><span class="sxs-lookup"><span data-stu-id="7ba23-163">Final .nuspec</span></span>

<span data-ttu-id="7ba23-164">Plik `.nuspec` końcowy powinien teraz wyglądać następująco, gdzie ponownie YOUR_NAME należy zastąpić odpowiednią wartością:</span><span class="sxs-lookup"><span data-stu-id="7ba23-164">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2018</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="7ba23-165">Zapakuj składnik</span><span class="sxs-lookup"><span data-stu-id="7ba23-165">Package the component</span></span>

<span data-ttu-id="7ba23-166">Po zakończeniu `.nuspec` odwoływania się do wszystkich plików, które należy uwzględnić `pack` w pakiecie, możesz uruchomić polecenie:</span><span class="sxs-lookup"><span data-stu-id="7ba23-166">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="7ba23-167">Spowoduje to `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`wygenerowanie .</span><span class="sxs-lookup"><span data-stu-id="7ba23-167">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="7ba23-168">Otwierając ten plik w narzędziu, takim jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozwijając wszystkie węzły, zostanie wyświetleni następująca zawartość:</span><span class="sxs-lookup"><span data-stu-id="7ba23-168">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![NuGet Package Explorer przedstawiający pakiet LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="7ba23-170">Plik `.nupkg` to tylko plik ZIP z innym rozszerzeniem.</span><span class="sxs-lookup"><span data-stu-id="7ba23-170">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="7ba23-171">Możesz również sprawdzić zawartość pakietu, `.nupkg` a `.zip`następnie, zmieniając na , ale pamiętaj, aby przywrócić rozszerzenie przed przesłaniem pakietu do nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7ba23-171">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="7ba23-172">Aby udostępnić pakiet innym deweloperom, postępuj zgodnie z instrukcjami dotyczącymi [publikowania pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="7ba23-172">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="7ba23-173">Powiązane tematy</span><span class="sxs-lookup"><span data-stu-id="7ba23-173">Related topics</span></span>

- [<span data-ttu-id="7ba23-174">Referencje Nuspec</span><span class="sxs-lookup"><span data-stu-id="7ba23-174">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="7ba23-175">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="7ba23-175">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="7ba23-176">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="7ba23-176">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="7ba23-177">Obsługa wielu wersji programu .NET Framework</span><span class="sxs-lookup"><span data-stu-id="7ba23-177">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="7ba23-178">Uwzględnij rekwizyty i obiekty docelowe MSBuild w pakiecie</span><span class="sxs-lookup"><span data-stu-id="7ba23-178">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="7ba23-179">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="7ba23-179">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
