---
title: Tworzenie pakietów NuGet dla platformy Xamarin (dla systemów iOS, Android i Windows) przy użyciu programu Visual Studio 2017 lub 2019
description: Kompleksowy przewodnik tworzenia pakietów NuGet dla platformy Xamarin, które używają natywnych interfejsów API w systemach iOS, Android i Windows.
author: JonDouglas
ms.author: jodou
ms.date: 11/05/2019
ms.topic: tutorial
ms.openlocfilehash: fdabeeac57ca12716f6ed2614d036f1623407b20
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774225"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2017-or-2019"></a><span data-ttu-id="4c50b-103">Tworzenie pakietów dla platformy Xamarin za pomocą programu Visual Studio 2017 lub 2019</span><span class="sxs-lookup"><span data-stu-id="4c50b-103">Create packages for Xamarin with Visual Studio 2017 or 2019</span></span>

<span data-ttu-id="4c50b-104">Pakiet dla platformy Xamarin zawiera kod, który używa natywnych interfejsów API w systemach iOS, Android i Windows, w zależności od systemu operacyjnego w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="4c50b-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="4c50b-105">Chociaż jest to proste, zaleca się, aby deweloperzy zużywali pakiet z bibliotek PCL lub .NET Standard za pośrednictwem wspólnego obszaru powierzchni interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="4c50b-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="4c50b-106">W tym instruktażu użyjesz programu Visual Studio 2017 lub 2019, aby utworzyć pakiet NuGet dla wielu platform, który może być używany w projektach mobilnych w systemach iOS, Android i Windows.</span><span class="sxs-lookup"><span data-stu-id="4c50b-106">In this walkthrough you use Visual Studio 2017 or 2019 to create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="4c50b-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4c50b-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="4c50b-108">Tworzenie struktury projektu i kodu abstrakcji</span><span class="sxs-lookup"><span data-stu-id="4c50b-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="4c50b-109">Napisz kod specyficzny dla platformy</span><span class="sxs-lookup"><span data-stu-id="4c50b-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="4c50b-110">Utwórz i zaktualizuj plik. nuspec</span><span class="sxs-lookup"><span data-stu-id="4c50b-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="4c50b-111">Pakowanie składnika</span><span class="sxs-lookup"><span data-stu-id="4c50b-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="4c50b-112">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="4c50b-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="4c50b-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4c50b-113">Prerequisites</span></span>

1. <span data-ttu-id="4c50b-114">Program Visual Studio 2017 lub 2019 z platforma uniwersalna systemu Windows (platformy UWP) i Xamarin.</span><span class="sxs-lookup"><span data-stu-id="4c50b-114">Visual Studio 2017 or 2019 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="4c50b-115">Zainstaluj bezpłatnie wersję Community z [VisualStudio.com](https://www.visualstudio.com/); Możesz również korzystać z wersji Professional i Enterprise.</span><span class="sxs-lookup"><span data-stu-id="4c50b-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="4c50b-116">Aby dołączyć narzędzia platformy UWP i Xamarin Tools, wybierz instalację niestandardową i Sprawdź odpowiednie opcje.</span><span class="sxs-lookup"><span data-stu-id="4c50b-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="4c50b-117">Interfejs wiersza polecenia NuGet.</span><span class="sxs-lookup"><span data-stu-id="4c50b-117">NuGet CLI.</span></span> <span data-ttu-id="4c50b-118">Pobierz najnowszą wersję nuget.exe z [NuGet.org/downloads](https://nuget.org/downloads), zapisując ją w wybranej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="4c50b-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="4c50b-119">Następnie Dodaj tę lokalizację do zmiennej środowiskowej PATH, jeśli nie została jeszcze.</span><span class="sxs-lookup"><span data-stu-id="4c50b-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="4c50b-120">nuget.exe to narzędzie interfejsu wiersza polecenia, a nie Instalator, dlatego pamiętaj o zapisaniu pobranego pliku w przeglądarce zamiast uruchamiania go.</span><span class="sxs-lookup"><span data-stu-id="4c50b-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="4c50b-121">Tworzenie struktury projektu i kodu abstrakcji</span><span class="sxs-lookup"><span data-stu-id="4c50b-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="4c50b-122">Pobierz i uruchom [Międzyplatformowe rozszerzenie .NET Standard szablony wtyczek](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c50b-122">Download and run the [Cross-Platform .NET Standard Plugin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="4c50b-123">Te szablony ułatwiają tworzenie niezbędnej struktury projektu dla tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="4c50b-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="4c50b-124">W programie Visual Studio 2017 **plik > nowy > projektu**, Wyszukaj `Plugin` , wybierz **Międzyplatformowy szablon wtyczki biblioteki .NET Standard** , Zmień nazwę na LoggingLibrary, a następnie kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="4c50b-124">In Visual Studio 2017, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Nowa pusta aplikacja (Xamarin. Forms Portable) w programie VS 2017](media/CrossPlatform-NewProject.png)

    <span data-ttu-id="4c50b-126">W programie Visual Studio 2019 **plik > nowy > projektu**, Wyszukaj `Plugin` , wybierz **Międzyplatformowy szablon wtyczki biblioteki .NET Standard** , a następnie kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="4c50b-126">In Visual Studio 2019, **File > New > Project**, search for `Plugin`, select the **Cross-Platform .NET Standard Library Plugin** template, and click Next.</span></span>

    ![Nowa pusta aplikacja (Xamarin. Forms Portable) w programie VS 2019](media/CrossPlatform-NewProject19-Part1.png)

    <span data-ttu-id="4c50b-128">Zmień nazwę na LoggingLibrary, a następnie kliknij przycisk Utwórz.</span><span class="sxs-lookup"><span data-stu-id="4c50b-128">Change the name to LoggingLibrary, and click Create.</span></span>

    ![Konfiguracja nowej pustej aplikacji (Xamarin. Forms Portable) w programie VS 2019](media/CrossPlatform-NewProject19-Part2.png)

<span data-ttu-id="4c50b-130">Otrzymane rozwiązanie zawiera dwa projekty udostępnione wraz z różnymi projektami specyficznymi dla platformy:</span><span class="sxs-lookup"><span data-stu-id="4c50b-130">The resulting solution contains two Shared projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="4c50b-131">`ILoggingLibrary`Projekt, który jest zawarty w `ILoggingLibrary.shared.cs` pliku, definiuje publiczny interfejs (obszar powierzchniowy interfejsu API) składnika.</span><span class="sxs-lookup"><span data-stu-id="4c50b-131">The `ILoggingLibrary` project, which is contained in the `ILoggingLibrary.shared.cs` file, defines the public interface (the API surface area) of the component.</span></span> <span data-ttu-id="4c50b-132">Jest to miejsce, w którym można zdefiniować interfejs biblioteki.</span><span class="sxs-lookup"><span data-stu-id="4c50b-132">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="4c50b-133">Inny udostępniony projekt zawiera kod `CrossLoggingLibrary.shared.cs` , który będzie odszukać implementację interfejsu abstrakcyjnego dla danej platformy w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="4c50b-133">The other Shared project contains code in `CrossLoggingLibrary.shared.cs` that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="4c50b-134">Zazwyczaj nie trzeba modyfikować tego pliku.</span><span class="sxs-lookup"><span data-stu-id="4c50b-134">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="4c50b-135">Projekty specyficzne dla platformy, takie jak `LoggingLibrary.android.cs` , zawierają natywną implementację interfejsu w odpowiednich `LoggingLibraryImplementation.cs` plikach (vs 2017) lub `LoggingLibrary.<PLATFORM>.cs` (vs 2019).</span><span class="sxs-lookup"><span data-stu-id="4c50b-135">The platform-specific projects, such as `LoggingLibrary.android.cs`, each contain a native implementation of the interface in their respective `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) files.</span></span> <span data-ttu-id="4c50b-136">Jest to miejsce, w którym można utworzyć kod biblioteki.</span><span class="sxs-lookup"><span data-stu-id="4c50b-136">This is where you build out your library's code.</span></span>

<span data-ttu-id="4c50b-137">Domyślnie plik ILoggingLibrary.shared.cs `ILoggingLibrary` projektu zawiera definicję interfejsu, ale nie ma żadnych metod.</span><span class="sxs-lookup"><span data-stu-id="4c50b-137">By default, the ILoggingLibrary.shared.cs file of the `ILoggingLibrary` project contains an interface definition, but no methods.</span></span> <span data-ttu-id="4c50b-138">Na potrzeby tego instruktażu Dodaj `Log` metodę w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4c50b-138">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="4c50b-139">Napisz kod specyficzny dla platformy</span><span class="sxs-lookup"><span data-stu-id="4c50b-139">Write your platform-specific code</span></span>

<span data-ttu-id="4c50b-140">Aby zaimplementować implementację `ILoggingLibrary` interfejsu i jego metody specyficzne dla platformy, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="4c50b-140">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="4c50b-141">Otwórz `LoggingLibraryImplementation.cs` plik (vs 2017) lub `LoggingLibrary.<PLATFORM>.cs` (vs 2019) dla każdego projektu platformy i Dodaj wymagany kod.</span><span class="sxs-lookup"><span data-stu-id="4c50b-141">Open the `LoggingLibraryImplementation.cs` (VS 2017) or `LoggingLibrary.<PLATFORM>.cs` (VS 2019) file of each platform project and add the necessary code.</span></span> <span data-ttu-id="4c50b-142">Na przykład (przy użyciu `Android` projektu platformy):</span><span class="sxs-lookup"><span data-stu-id="4c50b-142">For example (using the `Android` platform project):</span></span>

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

1. <span data-ttu-id="4c50b-143">Powtórz tę implementację w projektach dla każdej platformy, która ma być obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="4c50b-143">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="4c50b-144">Kliknij prawym przyciskiem myszy rozwiązanie, a następnie wybierz pozycję **Kompiluj rozwiązanie** , aby sprawdzić swoją służbę i utworzyć artefakty, które zostały umieszczone w dalszej kolejności.</span><span class="sxs-lookup"><span data-stu-id="4c50b-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="4c50b-145">Jeśli pojawią się błędy dotyczące brakujących odwołań, kliknij prawym przyciskiem myszy rozwiązanie, wybierz polecenie **Przywróć pakiety NuGet** , aby zainstalować zależności i ponownie skompilować.</span><span class="sxs-lookup"><span data-stu-id="4c50b-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="4c50b-146">Jeśli używasz programu Visual Studio 2019, przed wybraniem opcji **Przywróć pakiety NuGet** i próbą odbudowy należy zmienić wersję programu `MSBuild.Sdk.Extras` na `2.0.54` w programie `LoggingLibrary.csproj` .</span><span class="sxs-lookup"><span data-stu-id="4c50b-146">If you are using Visual Studio 2019, before selecting **Restore NuGet Packages** and trying to rebuild, you need to change the version of `MSBuild.Sdk.Extras` to `2.0.54` in `LoggingLibrary.csproj`.</span></span> <span data-ttu-id="4c50b-147">Dostęp do tego pliku można uzyskać tylko przez kliknięcie prawym przyciskiem myszy projektu (poniżej rozwiązania) i wybranie `Unload Project` , po kliknięciu prawym przyciskiem myszy zwolnionego projektu i wybranie opcji `Edit LoggingLibrary.csproj` .</span><span class="sxs-lookup"><span data-stu-id="4c50b-147">This file can only be accessed by first right-clicking the project (below the solution) and selecting `Unload Project`, after which you right-click on the unloaded project and select `Edit LoggingLibrary.csproj`.</span></span>

> [!Note]
> <span data-ttu-id="4c50b-148">Aby można było skompilować system iOS, potrzebny jest komputer Mac podłączony do programu Visual Studio, zgodnie z opisem w artykule [wprowadzenie do platformy Xamarin. iOS dla programu Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span><span class="sxs-lookup"><span data-stu-id="4c50b-148">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="4c50b-149">Jeśli nie masz dostępnego komputera Mac, wyczyść projekt systemu iOS w programie Configuration Manager (krok 3 powyżej).</span><span class="sxs-lookup"><span data-stu-id="4c50b-149">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="4c50b-150">Utwórz i zaktualizuj plik. nuspec</span><span class="sxs-lookup"><span data-stu-id="4c50b-150">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="4c50b-151">Otwórz wiersz polecenia, przejdź do folderu, `LoggingLibrary` który znajduje się poniżej, gdzie znajduje się `.sln` plik, i uruchom polecenie NuGet, `spec` Aby utworzyć `Package.nuspec` plik początkowy:</span><span class="sxs-lookup"><span data-stu-id="4c50b-151">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="4c50b-152">Zmień nazwę tego pliku na `LoggingLibrary.nuspec` i otwórz go w edytorze.</span><span class="sxs-lookup"><span data-stu-id="4c50b-152">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="4c50b-153">Zaktualizuj plik w taki sposób, aby pasował do następującej wartości YOUR_NAME.</span><span class="sxs-lookup"><span data-stu-id="4c50b-153">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="4c50b-154">`<id>`Wartość, szczególnie, musi być unikatowa w obrębie NuGet.org (zobacz Konwencje nazewnictwa opisane w artykule [Tworzenie pakietu](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span><span class="sxs-lookup"><span data-stu-id="4c50b-154">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="4c50b-155">Należy również pamiętać, że należy również zaktualizować Tagi autor i opis lub podczas kroku pakowania wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="4c50b-155">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
> <span data-ttu-id="4c50b-156">Możesz określić sufiks wersji pakietu przy użyciu `-alpha` `-beta` lub `-rc` Aby oznaczyć pakiet jako wersję wstępną, sprawdź [wersje wstępne](../create-packages/prerelease-packages.md) , aby uzyskać więcej informacji o wersjach wstępnych.</span><span class="sxs-lookup"><span data-stu-id="4c50b-156">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="4c50b-157">Dodaj zestawy referencyjne</span><span class="sxs-lookup"><span data-stu-id="4c50b-157">Add reference assemblies</span></span>

<span data-ttu-id="4c50b-158">Aby uwzględnić zestawy referencyjne specyficzne dla platformy, Dodaj następujące elementy do elementu, który jest `<files>` `LoggingLibrary.nuspec` odpowiedni dla obsługiwanych platform:</span><span class="sxs-lookup"><span data-stu-id="4c50b-158">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="4c50b-159">Aby skrócić nazwy plików DLL i XML, kliknij prawym przyciskiem myszy dowolny dany projekt, wybierz kartę **Biblioteka** i Zmień nazwy zestawów.</span><span class="sxs-lookup"><span data-stu-id="4c50b-159">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="4c50b-160">Dodaj zależności</span><span class="sxs-lookup"><span data-stu-id="4c50b-160">Add dependencies</span></span>

<span data-ttu-id="4c50b-161">Jeśli masz określone zależności dla implementacji natywnych, użyj `<dependencies>` elementu z `<group>` elementami, aby je określić, na przykład:</span><span class="sxs-lookup"><span data-stu-id="4c50b-161">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="4c50b-162">Na przykład następujące polecenie ustawi iTextSharp jako zależność dla elementu docelowego UAP:</span><span class="sxs-lookup"><span data-stu-id="4c50b-162">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="4c50b-163">Final. nuspec</span><span class="sxs-lookup"><span data-stu-id="4c50b-163">Final .nuspec</span></span>

<span data-ttu-id="4c50b-164">Ostatni `.nuspec` plik powinien teraz wyglądać podobnie do poniższego, gdzie ponownie YOUR_NAME powinien zostać zastąpiony odpowiednią wartością:</span><span class="sxs-lookup"><span data-stu-id="4c50b-164">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="4c50b-165">Pakowanie składnika</span><span class="sxs-lookup"><span data-stu-id="4c50b-165">Package the component</span></span>

<span data-ttu-id="4c50b-166">Po zakończeniu `.nuspec` odwoływania się do wszystkich plików, które należy uwzględnić w pakiecie, możesz uruchomić `pack` polecenie:</span><span class="sxs-lookup"><span data-stu-id="4c50b-166">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="4c50b-167">Spowoduje to wygenerowanie `LoggingLibrary.YOUR_NAME.1.0.0.nupkg` .</span><span class="sxs-lookup"><span data-stu-id="4c50b-167">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="4c50b-168">Otwierając ten plik w narzędziu, takim jak [Eksplorator pakietów NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzając wszystkie węzły, zobaczysz następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="4c50b-168">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![Eksplorator pakietów NuGet przedstawiający pakiet LoggingLibrary](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="4c50b-170">`.nupkg`Plik jest po prostu plikiem ZIP z innym rozszerzeniem.</span><span class="sxs-lookup"><span data-stu-id="4c50b-170">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="4c50b-171">Możesz również przeanalizować zawartość pakietu, a następnie zmienić `.nupkg` ją na `.zip` , ale pamiętaj, aby przywrócić rozszerzenie przed przekazaniem pakietu do NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="4c50b-171">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="4c50b-172">Aby udostępnić pakiet innym deweloperom, postępuj zgodnie z instrukcjami dotyczącymi [publikowania pakietu](../nuget-org/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4c50b-172">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="4c50b-173">Powiązane tematy</span><span class="sxs-lookup"><span data-stu-id="4c50b-173">Related topics</span></span>

- [<span data-ttu-id="4c50b-174">Odwołanie nuspec</span><span class="sxs-lookup"><span data-stu-id="4c50b-174">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="4c50b-175">Pakiety symboli</span><span class="sxs-lookup"><span data-stu-id="4c50b-175">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="4c50b-176">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="4c50b-176">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="4c50b-177">Obsługa wielu wersji .NET Framework</span><span class="sxs-lookup"><span data-stu-id="4c50b-177">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="4c50b-178">Uwzględnij w pakiecie narzędzia i elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="4c50b-178">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="4c50b-179">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="4c50b-179">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
