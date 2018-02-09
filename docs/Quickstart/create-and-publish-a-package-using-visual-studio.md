---
title: "Przewodnik wprowadzający do tworzenia i publikowania pakietu NuGet, za pomocą programu Visual Studio | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet przy użyciu programu Visual Studio 2017 r."
keywords: "Pakiet NuGet tworzenie, publikowanie pakietu NuGet, samouczek NuGet programu Visual Studio Utwórz pakiet NuGet, pakiet programu msbuild"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a4d60fdc0f27f9c4080266e212ac1cfe470ba925
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/09/2018
---
# <a name="create-and-publish-a-package-using-visual-studio"></a><span data-ttu-id="b1d40-104">Tworzenie i publikowanie pakietu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b1d40-104">Create and publish a package using Visual Studio</span></span>

<span data-ttu-id="b1d40-105">Jest to prosty proces, aby utworzyć pakiet NuGet z biblioteki klas .NET w programie Visual Studio, a następnie opublikować nuget.org za pomocą narzędzia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b1d40-105">It's a simple process to create a NuGet package from a .NET Class Library in Visual Studio, and then publish it to nuget.org using a CLI tool.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="b1d40-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b1d40-106">Pre-requisites</span></span>

1. <span data-ttu-id="b1d40-107">Zainstalowania dowolnej wersji programu Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) ze wszystkimi. Obciążenia związane z sieci.</span><span class="sxs-lookup"><span data-stu-id="b1d40-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="b1d40-108">Visual Studio 2017 automatycznie uwzględnia możliwości NuGet obciążenia .NET jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="b1d40-108">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="b1d40-109">Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisywanie, który `.exe` pliku do odpowiedniego folderu, a następnie dodanie tego folderu do Twojej zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="b1d40-109">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="b1d40-110">Alternatywnie Jeśli masz [.NET Core SDK](https://www.microsoft.com/net/download/) zainstalowana, można użyć `dotnet` interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b1d40-110">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="b1d40-111">[Zarejestruj bezpłatne konto na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz już.</span><span class="sxs-lookup"><span data-stu-id="b1d40-111">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="b1d40-112">Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="b1d40-112">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="b1d40-113">Aby przekazać pakiet, musisz potwierdzić konto.</span><span class="sxs-lookup"><span data-stu-id="b1d40-113">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="b1d40-114">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="b1d40-114">Create a class library project</span></span>

<span data-ttu-id="b1d40-115">Można użyć istniejącego projektu biblioteki klas .NET dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b1d40-115">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="b1d40-116">W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C# > .NET Standard** węzła, wybierz szablon "Biblioteki klas (.NET Standard)", nazwa projektu AppLogger i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1d40-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="b1d40-117">Kliknij prawym przyciskiem myszy na wynikowy plik projektu i wybierz **kompilacji** się upewnić, że projekt został utworzony prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="b1d40-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="b1d40-118">Biblioteki DLL znajduje się w folderze debugowania (lub wersji, jeśli zamiast tego kompilacji tej konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="b1d40-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="b1d40-119">W rzeczywistym pakiecie NuGet oczywiście zaimplementowaniem wielu przydatnych funkcji, które inne osoby mogą tworzyć aplikacje.</span><span class="sxs-lookup"><span data-stu-id="b1d40-119">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="b1d40-120">W ramach tego przewodnika jednak nie będzie pisania jakiegokolwiek dodatkowego kodu ponieważ biblioteki klas z szablonu jest wystarczające, aby utworzyć pakiet.</span><span class="sxs-lookup"><span data-stu-id="b1d40-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="b1d40-121">Nadal Jeśli chcesz funkcjonalności kodu dla pakietu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="b1d40-121">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="b1d40-122">Chyba że masz powód, w przeciwnym razie wybierz .NET Standard preferowanych celem jest pakietów NuGet, ponieważ zapewnia zgodność z szeroką gamą korzystanie z projektów.</span><span class="sxs-lookup"><span data-stu-id="b1d40-122">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="b1d40-123">Konfigurowanie właściwości pakietu</span><span class="sxs-lookup"><span data-stu-id="b1d40-123">Configure package properties</span></span>

1. <span data-ttu-id="b1d40-124">Wybierz **projektu > właściwości** menu polecenie, a następnie wybierz **pakietu** karty:</span><span class="sxs-lookup"><span data-stu-id="b1d40-124">Select the **Project > Properties** menu command, then select the **Package** tab:</span></span>

    ![Właściwości pakietu NuGet w projekcie programu Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="b1d40-126">Skompilowany dla publicznych zużycia pakietów, należy zwrócić szczególną uwagę na **tagi** właściwości, jak tagi ułatwiała innym pakietu odnaleźć i zrozumieć, jakie operacje.</span><span class="sxs-lookup"><span data-stu-id="b1d40-126">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="b1d40-127">Nadaj Unikatowy identyfikator pakietu i wypełnij wszystkie odpowiednie właściwości.</span><span class="sxs-lookup"><span data-stu-id="b1d40-127">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="b1d40-128">Opis różnych właściwości, zobacz [odwołania do pliku .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="b1d40-128">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="b1d40-129">Wszystkie właściwości w tym miejscu są przekazywane do `.nuspec` manifest tworzonego projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b1d40-129">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="b1d40-130">Podaj pakiet używany unikatowy identyfikator w nuget.org lub niezależnie od hosta można.</span><span class="sxs-lookup"><span data-stu-id="b1d40-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="b1d40-131">W ramach tego przewodnika, zaleca się tym "Sample" lub "Test" w nazwie, ponieważ kolejnych kroków publikowania pakietu widocznego publicznie (chociaż jest mało prawdopodobne, każda osoba, która zostanie rzeczywiście używane).</span><span class="sxs-lookup"><span data-stu-id="b1d40-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="b1d40-132">Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="b1d40-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="b1d40-133">Opcjonalnie: Aby wyświetlić właściwości bezpośrednio w pliku projektu, kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz **Edytuj AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="b1d40-133">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="b1d40-134">Uruchom polecenie pakietu</span><span class="sxs-lookup"><span data-stu-id="b1d40-134">Run the pack command</span></span>

1. <span data-ttu-id="b1d40-135">Ustaw dla konfiguracji **wersji**.</span><span class="sxs-lookup"><span data-stu-id="b1d40-135">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="b1d40-136">Kliknij prawym przyciskiem myszy projekt w **Eksploratora rozwiązań** i wybierz **pakietu** polecenia:</span><span class="sxs-lookup"><span data-stu-id="b1d40-136">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Polecenie pakietu NuGet w menu kontekstowym projektu programu Visual Studio](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="b1d40-138">Program Visual Studio tworzy projekt i tworzy `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="b1d40-138">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="b1d40-139">Sprawdź **dane wyjściowe** szczegółowe informacje w oknie (podobnie jak poniżej), który zawiera ścieżkę do pliku pakietu.</span><span class="sxs-lookup"><span data-stu-id="b1d40-139">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="b1d40-140">Należy też zauważyć, że skompilowany zestaw znajduje się w `bin\Release\netstandard2.0` befits jako element docelowy .NET 2.0 standardowa.</span><span class="sxs-lookup"><span data-stu-id="b1d40-140">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="b1d40-141">Opcja alternatywny: pakiet przy użyciu programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="b1d40-141">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="b1d40-142">Przy użyciu dyskietki **pakietu** polecenia menu, NuGet 4.x+ i obsługuje MSBuild 15.1 + `pack` docelowych, jeśli projekt zawiera dane niezbędne pakietu:</span><span class="sxs-lookup"><span data-stu-id="b1d40-142">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data:</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="b1d40-143">Następnie można znaleźć pakietu w `bin\Release` folderu.</span><span class="sxs-lookup"><span data-stu-id="b1d40-143">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="b1d40-144">Aby uzyskać dodatkowe opcje z `msbuild /t:pack`, zobacz [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="b1d40-144">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="b1d40-145">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="b1d40-145">Publish the package</span></span>

<span data-ttu-id="b1d40-146">Po utworzeniu `.nupkg` pliku opublikowaniu go za pomocą nuget.org `nuget.exe` interfejsu wiersza polecenia lub `dotnet.exe` CLI wraz z kluczem interfejsu API z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="b1d40-146">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="b1d40-147">Uzyskanie klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="b1d40-147">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="b1d40-148">Publikowanie za pomocą wypychania nuget</span><span class="sxs-lookup"><span data-stu-id="b1d40-148">Publish with nuget push</span></span>

<span data-ttu-id="b1d40-149">Ten krok jest to alternatywa dla użycia `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="b1d40-149">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="b1d40-150">Zmień folder zawierający `.nupkg` pliku...</span><span class="sxs-lookup"><span data-stu-id="b1d40-150">Change to the folder containing the `.nupkg` file..</span></span>

1. <span data-ttu-id="b1d40-151">Uruchom następujące polecenie, określając nazwę pakietu i zamianę klucza wartość klucza interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="b1d40-151">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="b1d40-152">nuget.exe wyświetla wyniki procesu publikowania:</span><span class="sxs-lookup"><span data-stu-id="b1d40-152">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="b1d40-153">Zobacz [wypychania nuget](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="b1d40-153">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="b1d40-154">Publikowanie za pomocą wypychania nuget dotnet</span><span class="sxs-lookup"><span data-stu-id="b1d40-154">Publish with dotnet nuget push</span></span>

<span data-ttu-id="b1d40-155">Ten krok jest to alternatywa dla użycia `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="b1d40-155">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="b1d40-156">Publikowanie błędów</span><span class="sxs-lookup"><span data-stu-id="b1d40-156">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="b1d40-157">Zarządzanie opublikowanego pakietu</span><span class="sxs-lookup"><span data-stu-id="b1d40-157">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="b1d40-158">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="b1d40-158">Related topics</span></span>

- [<span data-ttu-id="b1d40-159">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="b1d40-159">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="b1d40-160">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="b1d40-160">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="b1d40-161">Obsługuje wiele platform docelowych</span><span class="sxs-lookup"><span data-stu-id="b1d40-161">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="b1d40-162">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="b1d40-162">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="b1d40-163">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="b1d40-163">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="b1d40-164">Dokumentacja biblioteki standardowej .NET</span><span class="sxs-lookup"><span data-stu-id="b1d40-164">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="b1d40-165">Eksportowanie do platformy .NET Core z .NET Framework</span><span class="sxs-lookup"><span data-stu-id="b1d40-165">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)