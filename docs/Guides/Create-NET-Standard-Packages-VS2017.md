---
title: "Tworzenie pakietów NuGet 2.0 standardowe .NET z programu Visual Studio 2017 | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 05/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Przewodnik end-to-end tworzenia pakietów NuGet programu .NET Standard 2.0 przy użyciu narzędzia NuGet 4.x i Visual Studio 2017 r."
keywords: "Utwórz pakiet, .NET Standard pakietów platformy .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: aae38dd141c688a6eccc18cabea9e8245dbc36c5
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a><span data-ttu-id="caab8-104">Utwórz pakiety .NET 2.0 standardowe z programu Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="caab8-104">Create .NET Standard 2.0 packages with Visual Studio 2017</span></span>

<span data-ttu-id="caab8-105">*Dotyczy NuGet 4.x+ i MSBuild 15 ustęp 3 + zgodnie z programu Visual Studio 2017 aktualizacji 3 lub nowszym. W przypadku wcześniejszych wersji programu Visual Studio 2017 te instrukcje dotyczą 1.4 standardowe .NET do wersji 1.6, zmieniając \<TargetFramework\> właściwości. Zobacz też [utworzyć .NET Standard pakiety z programem Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) do pracy z NuGet 3.x+.*</span><span class="sxs-lookup"><span data-stu-id="caab8-105">*Applies to NuGet 4.x+ and MSBuild 15.3+ as provided with Visual Studio 2017 Update 3 and later. For earlier versions of Visual Studio 2017, these instructions apply to .NET Standard 1.4 to 1.6 by changing the \<TargetFramework\> property. Also see [Create .NET Standard Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) for working with NuGet 3.x+.*</span></span>

<span data-ttu-id="caab8-106">[Biblioteki standardowej .NET](/dotnet/articles/standard/library) jest formalną specyfikację interfejsów API architektury .NET mają być dostępne na wszystkich środowisk uruchomieniowych .NET, w związku z tym ustanawianie większej jednolitości w ekosystemie .NET.</span><span class="sxs-lookup"><span data-stu-id="caab8-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="caab8-107">Standardowa biblioteka .NET definiuje zestaw uniform BCL (Biblioteka klasy podstawowej) interfejsów API dla wszystkich platform .NET zaimplementować, niezależnie od obciążenia.</span><span class="sxs-lookup"><span data-stu-id="caab8-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="caab8-108">Go umożliwia deweloperom tworzenia PCLs, które będą używać dla wszystkich programów .NET, i zmniejsza Jeśli nie eliminuje dyrektywy kompilacja warunkowa specyficzne dla platformy w kodzie udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="caab8-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="caab8-109">Ten przewodnik przeprowadzi Cię przez proces tworzenia pakietu nuget przeznaczonych dla platformy .NET Standard biblioteki 2.0 z programu Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="caab8-109">This guide walks you through creating a nuget package targeting .NET Standard Library 2.0 with Visual Studio 2017.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="caab8-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="caab8-110">Pre-requisites</span></span>

<span data-ttu-id="caab8-111">W tym przewodniku wymaga programu Visual Studio 2017 Update 3 z **aplikacji dla wielu platform .NET Core** obciążenia.</span><span class="sxs-lookup"><span data-stu-id="caab8-111">This walkthrough requires Visual Studio 2017 Update 3 with the **.NET Core cross-platform development** workload.</span></span> <span data-ttu-id="caab8-112">Można zainstalować Community edition bezpłatnie z [visualstudio.com](https://www.visualstudio.com/), lub użyj wersje Professional i Enterprise.</span><span class="sxs-lookup"><span data-stu-id="caab8-112">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/), or use the Professional and Enterprise editions.</span></span>

<span data-ttu-id="caab8-113">Wymagaj obciążenia wygląda następująco w Instalatorze programu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="caab8-113">The require workload appears as follows in the Visual Studio installer:</span></span>

![Obciążenie wiele platform .NET core w Instalatorze programu Visual Studio](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a><span data-ttu-id="caab8-115">Utwórz .NET Standard projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="caab8-115">Create the .NET Standard class library project</span></span>

1. <span data-ttu-id="caab8-116">W programie Visual Studio **Plik > Nowy > projektu**, rozwiń węzeł **Visual C# > .NET Standard** węzła, wybierz opcję **biblioteki klas (Net Standard)**, Zmień nazwę na AppLogger, i Kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="caab8-116">In Visual Studio, **File > New > Project**, expand the **Visual C# > .NET Standard** node, select **Class Library (Net Standard)**, change the name to AppLogger, and click OK.</span></span>

    ![Tworzenie nowego projektu biblioteki klas](media/NuGet4-02-NewProject.png)

1. <span data-ttu-id="caab8-118">Zmień konfigurację kompilacji, aby **wersji**.</span><span class="sxs-lookup"><span data-stu-id="caab8-118">Change the build configuration to **Release**.</span></span>
1. <span data-ttu-id="caab8-119">Kliknij prawym przyciskiem myszy `AppLogger` projekt w Eksploratorze rozwiązań wybierz **właściwości**, wybierz pozycję **kompilacji** karcie, pole wyboru dla **pliku dokumentacji XML**i ustaw Nazwa pliku, aby dokładnie `AppLogger.xml`.</span><span class="sxs-lookup"><span data-stu-id="caab8-119">Right-click the `AppLogger` project in Solution Explorer, select **Properties**, select the **Build** tab, check the box for **XML documentation file**, and set the filename to just `AppLogger.xml`.</span></span> <span data-ttu-id="caab8-120">Następnie zapisz projekt.</span><span class="sxs-lookup"><span data-stu-id="caab8-120">Then save the project.</span></span>

1. <span data-ttu-id="caab8-121">Dodaj swój kod do składnika, takich jak (która wyraźnie tylko wysyła komunikaty do konsoli):</span><span class="sxs-lookup"><span data-stu-id="caab8-121">Add your code to the component, such as the following (which clearly just outputs messages to the console):</span></span>

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

1. <span data-ttu-id="caab8-122">Skompiluj projekt (przy użyciu konfiguracji Release) i sprawdź, czy biblioteka DLL, pliki XML są tworzone w ramach `bin\Release\netstandard2.0` folderu.</span><span class="sxs-lookup"><span data-stu-id="caab8-122">Build the project (with the Release configuration) and check that DLL and XML files are produced within the `bin\Release\netstandard2.0` folder.</span></span>

## <a name="edit-metadata-in-the-csproj-file"></a><span data-ttu-id="caab8-123">Edytuj metadane w pliku .csproj</span><span class="sxs-lookup"><span data-stu-id="caab8-123">Edit metadata in the .csproj file</span></span>

<span data-ttu-id="caab8-124">Z projektów NuGet 4.0 i .NET Core, metadane pakietów znajduje się bezpośrednio w `.csproj` plików zamiast plików zewnętrznych, takich jak `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="caab8-124">With NuGet 4.0 and .NET Core projects, package metadata is contained directly in the `.csproj` file instead of external files such as a `.nuspec`.</span></span> <span data-ttu-id="caab8-125">Pełny opis tych metadanych znajduje się w [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="caab8-125">A full description of that metadata is found in [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

1. <span data-ttu-id="caab8-126">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań wybierz **Edytuj AppLogger.csproj**, a następnie edytuj pierwszy grupę właściwości, aby uwzględnić informacje o pakiecie podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="caab8-126">Right-click the project in Solution Explorer, select **Edit AppLogger.csproj**, and then edit the first property group to include package information such as the following:</span></span>

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. <span data-ttu-id="caab8-127">Zapisz projekt, a następnie kliknij rozwiązanie prawym przyciskiem myszy i wybierz **Kompiluj rozwiązanie** można ponownie wygenerować wszystkich plików w pakiecie, tym razem z prawidłowych metadanych.</span><span class="sxs-lookup"><span data-stu-id="caab8-127">Save the project, then right-click the solution and select **Build Solution** to again generate all the files for the package, this time with the correct metadata.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="caab8-128">Pakiet składnika</span><span class="sxs-lookup"><span data-stu-id="caab8-128">Package the component</span></span>

<span data-ttu-id="caab8-129">NuGet 4.0 obsługuje obiektu docelowego pakietu przy użyciu programu MSBuild w wersji 15.1 + (łącznie z 15 MSBuild ustęp 3 jako część programu Visual Studio 2017 Update 3) Jeśli projekt zawiera metadanych potrzebny pakiet został dodany w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="caab8-129">NuGet 4.0 supports a pack target using MSBuild version 15.1+ (including MSBuild 15.3 as part of Visual Studio 2017 Update 3) when the project contains the necessary package metadata, as was added in the previous section.</span></span> <span data-ttu-id="caab8-130">Aby wywołać program MSBuild w ten sposób, po prostu Określ cel pakietu w wierszu polecenia, w tym samym folderze co `.csproj` pliku:</span><span class="sxs-lookup"><span data-stu-id="caab8-130">To invoke MSBuild in this way, simply specify the pack target on the command line in the same folder as the `.csproj` file:</span></span>

    msbuild /t:pack /p:Configuration=Release

<span data-ttu-id="caab8-131">Aby uzyskać dodatkowe opcje z `msbuild /t:pack`, takich jak dołączanie plików zawartości, symbole i kod źródłowy, zobacz [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../schema/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="caab8-131">For additional options with `msbuild /t:pack`, such as including content files, symbols, and source code, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

<span data-ttu-id="caab8-132">W każdym przypadku generuje polecenie powyżej `AppLogger.YOUR_NAME.1.0.0.nupkg` w `bin\Release` folder domyślny, ponieważ tworzy tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="caab8-132">In any case, the command above generates `AppLogger.YOUR_NAME.1.0.0.nupkg` in the `bin\Release` folder by default, as it builds that configuration.</span></span> <span data-ttu-id="caab8-133">W przypadku pominięcia `/p` przełącznik, będzie domyślna konfiguracja `Debug`.</span><span class="sxs-lookup"><span data-stu-id="caab8-133">If you omit the `/p` switch, the default configuration will be `Debug`.</span></span> 

<span data-ttu-id="caab8-134">Otwarcie tego pliku w narzędzia, takiego jak [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) i rozszerzanie wszystkich węzłów, zobaczysz następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="caab8-134">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![Wyświetlanie pakietu AppLogger Explorer pakietu NuGet](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="caab8-136">A `.nupkg` plik jest tylko plik ZIP zawierający inne rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="caab8-136">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="caab8-137">Można również sprawdzić zawartość pakietu, następnie zmieniając `.nupkg` do `.zip`, ale pamiętaj, aby przywrócić rozszerzenia przed przekazaniem do nuget.org pakietu.</span><span class="sxs-lookup"><span data-stu-id="caab8-137">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="caab8-138">Aby udostępnić pakietu inni deweloperzy, postępuj zgodnie z instrukcjami [opublikowania pakietu](../create-packages/publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="caab8-138">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="caab8-139">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="caab8-139">Related topics</span></span>

- <span data-ttu-id="caab8-140">[Pakiet odwołań w plikach projektu](../consume-packages/package-references-in-project-files.md) opisano wszystkie szczegóły opisujące pakiet bezpośrednio w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="caab8-140">[Package References in Project Files](../consume-packages/package-references-in-project-files.md) describes all the details of describing your package directly in the project file.</span></span>
- <span data-ttu-id="caab8-141">[NuGet pakietu i ich przywracania docelowych elementów MSBuild](../schema/msbuild-targets.md) opisuje wszystkie opcje przy użyciu `msbuild /t:pack` do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="caab8-141">[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) describes all the options for using `msbuild /t:pack` to create the package.</span></span>
- [<span data-ttu-id="caab8-142">Dokumentacja biblioteki standardowej .NET</span><span class="sxs-lookup"><span data-stu-id="caab8-142">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="caab8-143">Eksportowanie do platformy .NET Core z .NET Framework</span><span class="sxs-lookup"><span data-stu-id="caab8-143">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
