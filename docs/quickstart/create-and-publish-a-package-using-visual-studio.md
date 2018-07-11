---
title: Tworzenie i publikowanie pakietu platformy .NET Standard, za pomocą programu Visual Studio na Windows
description: Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet programu .NET Standard za pomocą programu Visual Studio 2017 na Windows.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: quickstart
ms.openlocfilehash: e97773d79b22db1f08d868190895a9417b12c924
ms.sourcegitcommit: 6cffa6ef59b922df2d87aa9c24034d00542983cd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2018
ms.locfileid: "37963090"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="e8d1f-103">Szybki Start: Tworzenie i publikowanie pakietu NuGet za pomocą programu Visual Studio (.NET Standard, tylko Windows)</span><span class="sxs-lookup"><span data-stu-id="e8d1f-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="e8d1f-104">Jest to prosty proces, aby utworzyć pakiet NuGet z standardowe biblioteki klas .NET w programie Visual Studio na Windows, a następnie opublikować go w witrynie nuget.org, za pomocą narzędzia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="e8d1f-105">Ten przewodnik Szybki Start ma zastosowanie do programu Visual Studio 2017 for Windows tylko.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="e8d1f-106">Visual Studio dla komputerów Mac nie ma możliwości opisane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="e8d1f-107">Użyj [narzędzi interfejsu wiersza polecenia dotnet](create-and-publish-a-package-using-the-dotnet-cli.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8d1f-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e8d1f-108">Prerequisites</span></span>

1. <span data-ttu-id="e8d1f-109">Instalowania dowolnej wersji programu Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) ze wszystkimi. Obciążenie związane z sieci.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="e8d1f-110">Po zainstalowaniu obciążenia platformy .NET, Visual Studio 2017 zawiera automatycznie możliwości NuGet.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="e8d1f-111">Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisywania, który `.exe` pliku do odpowiedniego folderu i dodawanie folderu do zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="e8d1f-112">Alternatywnie Jeśli masz [zestawu .NET Core SDK](https://www.microsoft.com/net/download/) zainstalowany, możesz użyć `dotnet` interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-112">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="e8d1f-113">[Zarejestruj, aby utworzyć bezpłatne konto w witrynie nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz jeszcze takiego.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-113">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="e8d1f-114">Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-114">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="e8d1f-115">Aby można było przekazać pakiet, należy potwierdzić konto.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-115">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="e8d1f-116">Utwórz projekt biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="e8d1f-116">Create a class library project</span></span>

<span data-ttu-id="e8d1f-117">Można użyć istniejącego projektu Biblioteka klas programu .NET Standard dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e8d1f-117">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="e8d1f-118">W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C# > .NET Standard** węzła, wybierz szablon "Biblioteka klas (.NET Standard)", nazwij projekt AppLogger i kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-118">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="e8d1f-119">Kliknij prawym przyciskiem myszy, wynikowy plik projektu, a następnie wybierz pozycję **kompilacji** się upewnić, że projekt został utworzony prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-119">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="e8d1f-120">Biblioteka DLL znajduje się w folderze debugowania (lub wydania, jeśli tworzysz tę konfigurację zamiast).</span><span class="sxs-lookup"><span data-stu-id="e8d1f-120">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="e8d1f-121">W ciągu rzeczywistą pakietu NuGet oczywiście, możesz zaimplementować wiele przydatnych funkcji, które inne osoby mogą tworzyć aplikacje.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-121">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="e8d1f-122">W tym przewodniku jednak nie będzie pisania żadnego dodatkowego kodu ponieważ biblioteki klas na podstawie tego szablonu jest wystarczające, aby utworzyć pakiet.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-122">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="e8d1f-123">Jednak jeśli chcesz funkcjonalności kodu dla pakietu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="e8d1f-123">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="e8d1f-124">Chyba że istnieje powód, aby wybrać inny sposób, .NET Standard jest preferowany cel pakiety NuGet, ponieważ zapewnia zgodność z szeroką gamą wykorzystywanie projektów.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-124">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="e8d1f-125">Konfigurowanie właściwości pakietu</span><span class="sxs-lookup"><span data-stu-id="e8d1f-125">Configure package properties</span></span>

1. <span data-ttu-id="e8d1f-126">Wybierz **projektu > właściwości** menu polecenia, a następnie wybierz **pakietu** kartę. ( **Pakietu** karta jest wyświetlana tylko dla projektów biblioteki klas .NET Standard; jeśli są przeznaczone dla .NET Framework, zobacz [tworzenie i publikowanie pakietu platformy .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-126">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="e8d1f-127">Jeśli nie pojawia się dla projektu .NET Standard, konieczne może być aktualizacja programu Visual Studio 2017 do najnowszej wersji.)</span><span class="sxs-lookup"><span data-stu-id="e8d1f-127">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Właściwości pakietu NuGet w projekcie programu Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="e8d1f-129">Pakiety utworzone do użytku publicznego, należy zwrócić szczególną uwagę na **tagi** właściwości, jak tagi pomóc innym odnaleźć pakietu i zrozumieć, co robi.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-129">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="e8d1f-130">Nadaj Unikatowy identyfikator pakietu i podaj żądane właściwości.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-130">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="e8d1f-131">Aby uzyskać opis różnych właściwości, zobacz [odwołanie do pliku .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="e8d1f-131">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="e8d1f-132">Wszystkie właściwości, w tym miejscu są przekazywane do `.nuspec` manifest przez program Visual Studio dla projektu.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-132">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="e8d1f-133">Musisz nadać pakietu, identyfikator, który jest unikatowa w obrębie nuget.org, lub niezależnie od rodzaju hoście jest używany.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="e8d1f-134">W ramach tego przewodnika firma Microsoft zaleca, tym "Próbny" lub "Test" w nazwie późniejszym etapie publikowania uwidocznić pakietu publicznie (choć jest mało prawdopodobne, każda osoba będzie faktycznie używać).</span><span class="sxs-lookup"><span data-stu-id="e8d1f-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="e8d1f-135">Jeśli spróbujesz opublikować pakietu o nazwie, która już istnieje, zostanie wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="e8d1f-136">Opcjonalnie: Aby wyświetlić właściwości bezpośrednio w pliku projektu, kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz **Edytuj AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-136">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="e8d1f-137">Uruchom polecenie pakietu</span><span class="sxs-lookup"><span data-stu-id="e8d1f-137">Run the pack command</span></span>

1. <span data-ttu-id="e8d1f-138">Ustaw konfigurację **wersji**.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-138">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="e8d1f-139">Kliknij prawym przyciskiem myszy projekt w **Eksploratora rozwiązań** i wybierz **pakiet** polecenia:</span><span class="sxs-lookup"><span data-stu-id="e8d1f-139">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Polecenie pakietu NuGet w menu kontekstowym projektu programu Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="e8d1f-141">Program Visual Studio tworzy projekt i tworzy `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-141">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="e8d1f-142">Sprawdź **dane wyjściowe** okno Szczegóły (podobne do następujących), który zawiera ścieżkę do pliku pakietu.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-142">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="e8d1f-143">Należy zauważyć, że skompilowany zestaw znajduje się w `bin\Release\netstandard2.0` befits jako obiektu docelowego .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-143">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="e8d1f-144">Alternatywna opcja: pakiet za pomocą narzędzia MSBuild</span><span class="sxs-lookup"><span data-stu-id="e8d1f-144">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="e8d1f-145">Jako alternatywnego za pomocą **pakiet** polecenia menu, NuGet 4.x+ i obsługuje program MSBuild 15.1 + `pack` docelowy, jeśli projekt zawiera dane niezbędne pakietu.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-145">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="e8d1f-146">Otwórz wiersz polecenia, przejdź do folderu projektu i uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-146">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="e8d1f-147">(Zazwyczaj należy start "Developer wiersz polecenia dla programu Visual Studio" z Start menu, co będzie można skonfigurować wszystkie niezbędne ścieżki programu MSBuild.)</span><span class="sxs-lookup"><span data-stu-id="e8d1f-147">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="e8d1f-148">Następnie można znaleźć pakietu w `bin\Release` folderu.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-148">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="e8d1f-149">Aby uzyskać dodatkowe opcje z `msbuild /t:pack`, zobacz [NuGet pakowanie i przywrócić jako elementów docelowych MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="e8d1f-149">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="e8d1f-150">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="e8d1f-150">Publish the package</span></span>

<span data-ttu-id="e8d1f-151">Po utworzeniu `.nupkg` pliku opublikujesz go w witrynie nuget.org, za pomocą `nuget.exe` interfejsu wiersza polecenia lub `dotnet.exe` interfejsu wiersza polecenia oraz klucza interfejsu API uzyskanych z repozytorium nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-151">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="e8d1f-152">Uzyskiwanie klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="e8d1f-152">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="e8d1f-153">Publikowanie za pomocą wypychania nuget</span><span class="sxs-lookup"><span data-stu-id="e8d1f-153">Publish with nuget push</span></span>

<span data-ttu-id="e8d1f-154">Ten krok jest alternatywa dla użycia `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-154">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="e8d1f-155">Zmień folder zawierający `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-155">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="e8d1f-156">Uruchom następujące polecenie, określając nazwę pakietu i zastępując wartość klucza swój klucz interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="e8d1f-156">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="e8d1f-157">nuget.exe wyświetla wyniki proces publikowania:</span><span class="sxs-lookup"><span data-stu-id="e8d1f-157">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="e8d1f-158">Zobacz [wypychania nuget](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="e8d1f-158">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="e8d1f-159">Publikowanie za pomocą polecenia dotnet nuget wypychania</span><span class="sxs-lookup"><span data-stu-id="e8d1f-159">Publish with dotnet nuget push</span></span>

<span data-ttu-id="e8d1f-160">Ten krok jest alternatywa dla użycia `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="e8d1f-160">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="e8d1f-161">Publikowanie błędy</span><span class="sxs-lookup"><span data-stu-id="e8d1f-161">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="e8d1f-162">Zarządzanie opublikowany pakiet</span><span class="sxs-lookup"><span data-stu-id="e8d1f-162">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="e8d1f-163">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="e8d1f-163">Related topics</span></span>

- [<span data-ttu-id="e8d1f-164">Utwórz pakiet</span><span class="sxs-lookup"><span data-stu-id="e8d1f-164">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="e8d1f-165">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="e8d1f-165">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="e8d1f-166">Pakiety w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="e8d1f-166">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="e8d1f-167">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="e8d1f-167">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="e8d1f-168">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="e8d1f-168">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="e8d1f-169">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="e8d1f-169">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="e8d1f-170">Dokumentacja .NET biblioteki standardowej</span><span class="sxs-lookup"><span data-stu-id="e8d1f-170">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="e8d1f-171">Eksportowanie do programu .NET Core z .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e8d1f-171">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
