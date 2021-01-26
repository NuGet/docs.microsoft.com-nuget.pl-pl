---
title: Tworzenie i publikowanie pakietu .NET Framework NuGet przy użyciu programu Visual Studio w systemie Windows
description: Samouczek instruktażowy dotyczący tworzenia i publikowania pakietu .NET Framework NuGet przy użyciu programu Visual Studio w systemie Windows.
author: JonDouglas
ms.author: jodou
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: 7c030db769973e3b3c41da6523d57ab2cd769a9d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775751"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="665f9-103">Szybki Start: Tworzenie i publikowanie pakietu przy użyciu programu Visual Studio (.NET Framework, Windows)</span><span class="sxs-lookup"><span data-stu-id="665f9-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="665f9-104">Tworzenie pakietu NuGet z biblioteki klas .NET Framework obejmuje tworzenie bibliotek DLL w programie Visual Studio w systemie Windows, a następnie za pomocą narzędzia wiersza polecenia nuget.exe do tworzenia i publikowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="665f9-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="665f9-105">Ten przewodnik Szybki Start dotyczy tylko programu Visual Studio 2017 i nowszych wersji dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="665f9-105">This Quickstart applies to Visual Studio 2017 and higher versions for Windows only.</span></span> <span data-ttu-id="665f9-106">Visual Studio dla komputerów Mac nie obejmuje funkcji opisanych w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="665f9-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="665f9-107">Zamiast tego użyj [narzędzi interfejsu wiersza polecenia dotnet](create-and-publish-a-package-using-the-dotnet-cli.md) .</span><span class="sxs-lookup"><span data-stu-id="665f9-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="665f9-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="665f9-108">Prerequisites</span></span>

1. <span data-ttu-id="665f9-109">Zainstaluj dowolną wersję programu Visual Studio 2017 lub nowszą z [VisualStudio.com](https://www.visualstudio.com/) . Obciążenie związane z usługą SIECIową.</span><span class="sxs-lookup"><span data-stu-id="665f9-109">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="665f9-110">Program Visual Studio 2017 automatycznie zawiera funkcje NuGet podczas instalacji obciążenia .NET.</span><span class="sxs-lookup"><span data-stu-id="665f9-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="665f9-111">Zainstaluj `nuget.exe` interfejs wiersza polecenia, pobierając go z [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisując ten `.exe` plik w odpowiednim folderze i dodając go do zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="665f9-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="665f9-112">[Zarejestruj się, aby korzystać z bezpłatnego konta w usłudze NuGet.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) , jeśli jeszcze go nie masz.</span><span class="sxs-lookup"><span data-stu-id="665f9-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="665f9-113">Utworzenie nowego konta spowoduje wysłanie wiadomości e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="665f9-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="665f9-114">Musisz potwierdzić konto, aby można było przekazać pakiet.</span><span class="sxs-lookup"><span data-stu-id="665f9-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="665f9-115">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="665f9-115">Create a class library project</span></span>

<span data-ttu-id="665f9-116">Można użyć istniejącego projektu biblioteki klas .NET Framework dla kodu, który ma zostać spakowany, lub utworzyć prosty jeden w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="665f9-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="665f9-117">W programie Visual Studio wybierz pozycję **plik > nowy > projekt**, wybierz węzeł **Visual C#** , wybierz szablon "Biblioteka klas (.NET Framework)", nazwij projekt AppLogger i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="665f9-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="665f9-118">Kliknij prawym przyciskiem myszy plik projektu powstały i wybierz pozycję **kompilacja** , aby upewnić się, że projekt został utworzony prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="665f9-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="665f9-119">Biblioteka DLL znajduje się w folderze debugowania (lub zwolnij, jeśli zostanie utworzona ta konfiguracja).</span><span class="sxs-lookup"><span data-stu-id="665f9-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="665f9-120">Oczywiście w rzeczywistym pakiecie NuGet zaimplementowano wiele przydatnych funkcji, z którymi inne mogą tworzyć aplikacje.</span><span class="sxs-lookup"><span data-stu-id="665f9-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="665f9-121">Możesz również ustawić Platformy docelowe.</span><span class="sxs-lookup"><span data-stu-id="665f9-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="665f9-122">Na przykład zapoznaj się z przewodnikami dla [platformy UWP](../guides/create-uwp-packages.md) i [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="665f9-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="665f9-123">W tym instruktażu nie można jednak napisać żadnego dodatkowego kodu, ponieważ biblioteka klas z szablonu jest wystarczająca do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="665f9-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="665f9-124">Nadal, jeśli chcesz, aby w pakiecie był jakiś kod funkcjonalny, użyj następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="665f9-124">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
using System;

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
> <span data-ttu-id="665f9-125">O ile nie istnieje powód, aby wybrać inny sposób, .NET Standard jest preferowanym celem dla pakietów NuGet, ponieważ zapewnia zgodność z najszerszym zakresem zużywanych projektów.</span><span class="sxs-lookup"><span data-stu-id="665f9-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="665f9-126">Zobacz [Tworzenie i publikowanie pakietu przy użyciu programu Visual Studio (.NET standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="665f9-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="665f9-127">Konfigurowanie właściwości projektu dla pakietu</span><span class="sxs-lookup"><span data-stu-id="665f9-127">Configure project properties for the package</span></span>

<span data-ttu-id="665f9-128">Pakiet NuGet zawiera manifest ( `.nuspec` plik), który zawiera odpowiednie metadane, takie jak identyfikator pakietu, numer wersji, opis i inne.</span><span class="sxs-lookup"><span data-stu-id="665f9-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="665f9-129">Niektóre z nich mogą być narysowane bezpośrednio we właściwościach projektu, co pozwala uniknąć konieczności osobnego aktualizowania ich zarówno w projekcie, jak i w manifeście.</span><span class="sxs-lookup"><span data-stu-id="665f9-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="665f9-130">W tej sekcji opisano, gdzie ustawić odpowiednie właściwości.</span><span class="sxs-lookup"><span data-stu-id="665f9-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="665f9-131">Wybierz polecenie menu **> właściwości projektu** , a następnie wybierz kartę **aplikacja** .</span><span class="sxs-lookup"><span data-stu-id="665f9-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="665f9-132">W polu **Nazwa zestawu** nadaj pakietowi unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="665f9-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="665f9-133">Należy nadać pakietowi identyfikator, który jest unikatowy w obrębie nuget.org lub dowolnego hosta, który jest używany.</span><span class="sxs-lookup"><span data-stu-id="665f9-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="665f9-134">W tym instruktażu Zalecamy uwzględnienie "przykładowego" lub "testowego" w nazwie, jak w późniejszym kroku publikowania sprawia, że pakiet jest widoczny publicznie (chociaż prawdopodobnie nikt się nie używa).</span><span class="sxs-lookup"><span data-stu-id="665f9-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="665f9-135">Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="665f9-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="665f9-136">Wybierz przycisk **Informacje o zestawie** , który umożliwia wyświetlenie okna dialogowego, w którym można wprowadzić inne właściwości, które są umieszczane w manifeście (zobacz [. nuspec plik — tokeny zastępcze](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="665f9-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="665f9-137">Najczęściej używane pola to **tytuł**, **Opis**, **firma**, **prawa autorskie** i **wersja zestawu**.</span><span class="sxs-lookup"><span data-stu-id="665f9-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="665f9-138">Te właściwości ostatecznie pojawiają się wraz z pakietem na hoście, takim jak nuget.org, więc upewnij się, że są one w pełni opisowe.</span><span class="sxs-lookup"><span data-stu-id="665f9-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Informacje o zestawie w projekcie .NET Framework w programie Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="665f9-140">Opcjonalne: Aby wyświetlić i edytować właściwości bezpośrednio, Otwórz `Properties/AssemblyInfo.cs` plik w projekcie.</span><span class="sxs-lookup"><span data-stu-id="665f9-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="665f9-141">Po ustawieniu właściwości ustaw konfigurację projektu na **Zwolnij** i Skompiluj ponownie projekt w celu wygenerowania zaktualizowanej biblioteki DLL.</span><span class="sxs-lookup"><span data-stu-id="665f9-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="665f9-142">Generuj początkowy manifest</span><span class="sxs-lookup"><span data-stu-id="665f9-142">Generate the initial manifest</span></span>

<span data-ttu-id="665f9-143">Z biblioteką DLL w oddziałach i ustawionych właściwościach projektu można teraz użyć `nuget spec` polecenia, aby wygenerować początkowy `.nuspec` plik z projektu.</span><span class="sxs-lookup"><span data-stu-id="665f9-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="665f9-144">Ten krok obejmuje odpowiednie tokeny zastępcze do rysowania informacji z pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="665f9-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="665f9-145">Uruchamia `nuget spec` się tylko raz, aby wygenerować początkowy manifest.</span><span class="sxs-lookup"><span data-stu-id="665f9-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="665f9-146">Podczas aktualizowania pakietu należy zmienić wartości w projekcie lub bezpośrednio edytować manifest.</span><span class="sxs-lookup"><span data-stu-id="665f9-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="665f9-147">Otwórz wiersz polecenia i przejdź do folderu projektu zawierającego `AppLogger.csproj` plik.</span><span class="sxs-lookup"><span data-stu-id="665f9-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="665f9-148">Uruchom następujące polecenie: `nuget spec AppLogger.csproj` .</span><span class="sxs-lookup"><span data-stu-id="665f9-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="665f9-149">Określając projekt, pakiet NuGet tworzy manifest, który jest zgodny z nazwą projektu, w tym przypadku `AppLogger.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="665f9-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="665f9-150">Zawiera również tokeny zastępcze w manifeście.</span><span class="sxs-lookup"><span data-stu-id="665f9-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="665f9-151">Otwórz `AppLogger.nuspec` w edytorze tekstów, aby przejrzeć jego zawartość, która powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="665f9-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>Package</id>
        <version>1.0.0</version>
        <authors>YourUsername</authors>
        <owners>YourUsername</owners>
        <license type="expression">MIT</license>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Package description</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2019</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a><span data-ttu-id="665f9-152">Edytuj manifest</span><span class="sxs-lookup"><span data-stu-id="665f9-152">Edit the manifest</span></span>

1. <span data-ttu-id="665f9-153">Pakiet NuGet generuje błąd w przypadku próby utworzenia pakietu z wartościami domyślnymi w `.nuspec` pliku, dlatego przed kontynuowaniem należy edytować następujące pola.</span><span class="sxs-lookup"><span data-stu-id="665f9-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="665f9-154">Zobacz [. nuspec — odwołanie do pliku — opcjonalne elementy metadanych](../reference/nuspec.md#optional-metadata-elements) opisujące sposób ich użycia.</span><span class="sxs-lookup"><span data-stu-id="665f9-154">See [.nuspec file reference - optional metadata elements](../reference/nuspec.md#optional-metadata-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="665f9-155">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="665f9-155">licenseUrl</span></span>
    - <span data-ttu-id="665f9-156">projectUrl</span><span class="sxs-lookup"><span data-stu-id="665f9-156">projectUrl</span></span>
    - <span data-ttu-id="665f9-157">iconUrl</span><span class="sxs-lookup"><span data-stu-id="665f9-157">iconUrl</span></span>
    - <span data-ttu-id="665f9-158">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="665f9-158">releaseNotes</span></span>
    - <span data-ttu-id="665f9-159">tags</span><span class="sxs-lookup"><span data-stu-id="665f9-159">tags</span></span>

1. <span data-ttu-id="665f9-160">W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na właściwości **Tagi** , ponieważ Tagi ułatwiają innym znalezienie pakietu na źródłach, takich jak NuGet.org, i zrozumienie jego działania.</span><span class="sxs-lookup"><span data-stu-id="665f9-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="665f9-161">W tym momencie można również dodać wszystkie inne elementy do manifestu, zgodnie z opisem w [dokumentacji pliku. nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="665f9-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="665f9-162">Zapisz plik przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="665f9-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="665f9-163">Uruchom pakiet polecenie</span><span class="sxs-lookup"><span data-stu-id="665f9-163">Run the pack command</span></span>

1. <span data-ttu-id="665f9-164">W wierszu polecenia w folderze zawierającym `.nuspec` plik Uruchom polecenie `nuget pack` .</span><span class="sxs-lookup"><span data-stu-id="665f9-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="665f9-165">Pakiet NuGet generuje `.nupkg` plik w postaci *identyfikatora-Version. nupkg*, który znajduje się w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="665f9-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="665f9-166">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="665f9-166">Publish the package</span></span>

<span data-ttu-id="665f9-167">Po utworzeniu `.nupkg` pliku opublikuj go w celu NuGet.org przy użyciu `nuget.exe` klucza interfejsu API uzyskanego z NuGet.org. W przypadku nuget.org należy użyć `nuget.exe` 4.1.0 lub wyższej.</span><span class="sxs-lookup"><span data-stu-id="665f9-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="665f9-168">Pozyskiwanie klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="665f9-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="665f9-169">Publikowanie przy użyciu wypychania NuGet</span><span class="sxs-lookup"><span data-stu-id="665f9-169">Publish with nuget push</span></span>

1. <span data-ttu-id="665f9-170">Otwórz wiersz polecenia i przejdź do folderu zawierającego `.nupkg` plik.</span><span class="sxs-lookup"><span data-stu-id="665f9-170">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="665f9-171">Uruchom następujące polecenie, określając nazwę pakietu i zastępując wartość klucza kluczem interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="665f9-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="665f9-172">nuget.exe wyświetla wyniki procesu publikowania:</span><span class="sxs-lookup"><span data-stu-id="665f9-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="665f9-173">Zobacz [wypychanie NuGet](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="665f9-173">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="665f9-174">Błędy publikowania</span><span class="sxs-lookup"><span data-stu-id="665f9-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="665f9-175">Zarządzanie opublikowanym pakietem</span><span class="sxs-lookup"><span data-stu-id="665f9-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="665f9-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="665f9-176">Next steps</span></span>

<span data-ttu-id="665f9-177">Gratulujemy utworzenia pierwszego pakietu NuGet!</span><span class="sxs-lookup"><span data-stu-id="665f9-177">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="665f9-178">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="665f9-178">Create a Package</span></span>](../create-packages/creating-a-package.md)

<span data-ttu-id="665f9-179">Aby poznać więcej informacji o tym, że pakiet NuGet jest oferowany, wybierz poniższe linki.</span><span class="sxs-lookup"><span data-stu-id="665f9-179">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="665f9-180">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="665f9-180">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="665f9-181">Pakiety wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="665f9-181">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="665f9-182">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="665f9-182">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="665f9-183">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="665f9-183">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="665f9-184">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="665f9-184">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
