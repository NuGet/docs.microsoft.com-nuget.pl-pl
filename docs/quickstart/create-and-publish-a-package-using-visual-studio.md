---
title: Tworzenie i publikowanie pakietu .NET Standard przy użyciu programu Visual Studio w systemie Windows
description: Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet programu .NET Standard w systemie Windows za pomocą programu Visual Studio 2017 r.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/18/2018
ms.topic: quickstart
ms.openlocfilehash: f4e6473d307f2f71016f6926abbcdb1295abc7b5
ms.sourcegitcommit: f0b31af805183cf3a98eabb504e16d9b05223cfe
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/22/2018
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="59148-103">Szybki Start: Tworzenie i publikowanie pakietu NuGet, za pomocą programu Visual Studio (.NET Standard, tylko system Windows)</span><span class="sxs-lookup"><span data-stu-id="59148-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="59148-104">Jest to prosty proces, aby utworzyć pakiet NuGet z standardowa biblioteka klas programu .NET w programie Visual Studio w systemie Windows, a następnie opublikować nuget.org za pomocą narzędzia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="59148-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="59148-105">Ta opcja szybkiego startu dotyczy programu Visual Studio 2017 r dla systemu Windows tylko.</span><span class="sxs-lookup"><span data-stu-id="59148-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="59148-106">Visual Studio for Mac nie ma możliwości opisane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="59148-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="59148-107">Użyj [narzędzi interfejsu wiersza polecenia platformy dotnet](create-and-publish-a-package-using-the-dotnet-cli.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="59148-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59148-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="59148-108">Prerequisites</span></span>

1. <span data-ttu-id="59148-109">Zainstalowania dowolnej wersji programu Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) ze wszystkimi. Obciążenia związane z sieci.</span><span class="sxs-lookup"><span data-stu-id="59148-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="59148-110">Visual Studio 2017 automatycznie uwzględnia możliwości NuGet obciążenia .NET jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="59148-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="59148-111">Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisywanie, który `.exe` pliku do odpowiedniego folderu, a następnie dodanie tego folderu do Twojej zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="59148-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="59148-112">Alternatywnie Jeśli masz [.NET Core SDK](https://www.microsoft.com/net/download/) zainstalowana, można użyć `dotnet` interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="59148-112">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="59148-113">[Zarejestruj bezpłatne konto na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz już.</span><span class="sxs-lookup"><span data-stu-id="59148-113">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="59148-114">Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="59148-114">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="59148-115">Aby przekazać pakiet, musisz potwierdzić konto.</span><span class="sxs-lookup"><span data-stu-id="59148-115">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="59148-116">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="59148-116">Create a class library project</span></span>

<span data-ttu-id="59148-117">Można użyć istniejącego projektu standardowa biblioteka klas programu .NET dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="59148-117">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="59148-118">W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C# > .NET Standard** węzła, wybierz szablon "Biblioteki klas (.NET Standard)", nazwa projektu AppLogger i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="59148-118">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="59148-119">Kliknij prawym przyciskiem myszy na wynikowy plik projektu i wybierz **kompilacji** się upewnić, że projekt został utworzony prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="59148-119">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="59148-120">Biblioteki DLL znajduje się w folderze debugowania (lub wersji, jeśli zamiast tego kompilacji tej konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="59148-120">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="59148-121">W rzeczywistym pakiecie NuGet oczywiście zaimplementowaniem wielu przydatnych funkcji, które inne osoby mogą tworzyć aplikacje.</span><span class="sxs-lookup"><span data-stu-id="59148-121">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="59148-122">W ramach tego przewodnika jednak nie będzie pisania jakiegokolwiek dodatkowego kodu ponieważ biblioteki klas z szablonu jest wystarczające, aby utworzyć pakiet.</span><span class="sxs-lookup"><span data-stu-id="59148-122">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="59148-123">Nadal Jeśli chcesz funkcjonalności kodu dla pakietu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="59148-123">Still, if you'd like some functional code for the package, use the following:</span></span>

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

> [!Tip]
> <span data-ttu-id="59148-124">Chyba że masz powód, w przeciwnym razie wybierz .NET Standard preferowanych celem jest pakietów NuGet, ponieważ zapewnia zgodność z szeroką gamą korzystanie z projektów.</span><span class="sxs-lookup"><span data-stu-id="59148-124">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="59148-125">Konfigurowanie właściwości pakietu</span><span class="sxs-lookup"><span data-stu-id="59148-125">Configure package properties</span></span>

1. <span data-ttu-id="59148-126">Wybierz **projektu > właściwości** menu polecenie, a następnie wybierz **pakietu** kartę. ( **Pakietu** karta jest wyświetlana tylko dla projektów biblioteki klas .NET Standard; jeśli ma być przeznaczona dla .NET Framework, zobacz [tworzenie i publikowanie pakietu .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="59148-126">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="59148-127">Jeśli nie pojawia się w projekcie .NET Standard, może być konieczne aktualizacji do najnowszej wersji programu Visual Studio 2017 r.)</span><span class="sxs-lookup"><span data-stu-id="59148-127">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Właściwości pakietu NuGet w projekcie programu Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="59148-129">Skompilowany dla publicznych zużycia pakietów, należy zwrócić szczególną uwagę na **tagi** właściwości, jak tagi ułatwiała innym pakietu odnaleźć i zrozumieć, jakie operacje.</span><span class="sxs-lookup"><span data-stu-id="59148-129">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="59148-130">Nadaj Unikatowy identyfikator pakietu i wypełnij wszystkie odpowiednie właściwości.</span><span class="sxs-lookup"><span data-stu-id="59148-130">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="59148-131">Opis różnych właściwości, zobacz [odwołania do pliku .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="59148-131">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="59148-132">Wszystkie właściwości w tym miejscu są przekazywane do `.nuspec` manifest tworzonego projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="59148-132">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="59148-133">Podaj pakiet używany unikatowy identyfikator w nuget.org lub niezależnie od hosta można.</span><span class="sxs-lookup"><span data-stu-id="59148-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="59148-134">W ramach tego przewodnika, zaleca się tym "Sample" lub "Test" w nazwie, ponieważ kolejnych kroków publikowania pakietu widocznego publicznie (chociaż jest mało prawdopodobne, każda osoba, która zostanie rzeczywiście używane).</span><span class="sxs-lookup"><span data-stu-id="59148-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="59148-135">Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="59148-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="59148-136">Opcjonalnie: Aby wyświetlić właściwości bezpośrednio w pliku projektu, kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz **Edytuj AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="59148-136">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="59148-137">Uruchom polecenie pakietu</span><span class="sxs-lookup"><span data-stu-id="59148-137">Run the pack command</span></span>

1. <span data-ttu-id="59148-138">Ustaw dla konfiguracji **wersji**.</span><span class="sxs-lookup"><span data-stu-id="59148-138">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="59148-139">Kliknij prawym przyciskiem myszy projekt w **Eksploratora rozwiązań** i wybierz **pakietu** polecenia:</span><span class="sxs-lookup"><span data-stu-id="59148-139">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Polecenie pakietu NuGet w menu kontekstowym projektu programu Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="59148-141">Program Visual Studio tworzy projekt i tworzy `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="59148-141">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="59148-142">Sprawdź **dane wyjściowe** szczegółowe informacje w oknie (podobnie jak poniżej), który zawiera ścieżkę do pliku pakietu.</span><span class="sxs-lookup"><span data-stu-id="59148-142">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="59148-143">Należy też zauważyć, że skompilowany zestaw znajduje się w `bin\Release\netstandard2.0` befits jako element docelowy .NET 2.0 standardowa.</span><span class="sxs-lookup"><span data-stu-id="59148-143">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="59148-144">Opcja alternatywny: pakiet przy użyciu programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="59148-144">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="59148-145">Przy użyciu dyskietki **pakietu** polecenia menu, NuGet 4.x+ i obsługuje MSBuild 15.1 + `pack` docelowych, jeśli projekt zawiera dane niezbędne pakietu.</span><span class="sxs-lookup"><span data-stu-id="59148-145">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="59148-146">Otwórz wiersz polecenia, przejdź do folderu projektu i uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="59148-146">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="59148-147">(Zazwyczaj ma się rozpocząć "Developer wiersz polecenia dla programu Visual Studio" z Start menu, jak będzie można skonfigurować z wszystkie niezbędne ścieżki programu MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="59148-147">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="59148-148">Następnie można znaleźć pakietu w `bin\Release` folderu.</span><span class="sxs-lookup"><span data-stu-id="59148-148">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="59148-149">Aby uzyskać dodatkowe opcje z `msbuild /t:pack`, zobacz [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="59148-149">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="59148-150">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="59148-150">Publish the package</span></span>

<span data-ttu-id="59148-151">Po utworzeniu `.nupkg` pliku opublikowaniu go za pomocą nuget.org `nuget.exe` interfejsu wiersza polecenia lub `dotnet.exe` CLI wraz z kluczem interfejsu API z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="59148-151">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="59148-152">Uzyskanie klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="59148-152">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="59148-153">Publikowanie za pomocą wypychania nuget</span><span class="sxs-lookup"><span data-stu-id="59148-153">Publish with nuget push</span></span>

<span data-ttu-id="59148-154">Ten krok jest to alternatywa dla użycia `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="59148-154">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="59148-155">Zmień folder zawierający `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="59148-155">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="59148-156">Uruchom następujące polecenie, określając nazwę pakietu i zamianę klucza wartość klucza interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="59148-156">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="59148-157">nuget.exe wyświetla wyniki procesu publikowania:</span><span class="sxs-lookup"><span data-stu-id="59148-157">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="59148-158">Zobacz [wypychania nuget](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="59148-158">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="59148-159">Publikowanie za pomocą wypychania nuget dotnet</span><span class="sxs-lookup"><span data-stu-id="59148-159">Publish with dotnet nuget push</span></span>

<span data-ttu-id="59148-160">Ten krok jest to alternatywa dla użycia `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="59148-160">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="59148-161">Publikowanie błędów</span><span class="sxs-lookup"><span data-stu-id="59148-161">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="59148-162">Zarządzanie opublikowanego pakietu</span><span class="sxs-lookup"><span data-stu-id="59148-162">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="59148-163">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="59148-163">Related topics</span></span>

- [<span data-ttu-id="59148-164">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="59148-164">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="59148-165">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="59148-165">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="59148-166">Pakiety wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="59148-166">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="59148-167">Obsługuje wiele platform docelowych</span><span class="sxs-lookup"><span data-stu-id="59148-167">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="59148-168">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="59148-168">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="59148-169">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="59148-169">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="59148-170">Dokumentacja biblioteki standardowej .NET</span><span class="sxs-lookup"><span data-stu-id="59148-170">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="59148-171">Eksportowanie do platformy .NET Core z .NET Framework</span><span class="sxs-lookup"><span data-stu-id="59148-171">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
