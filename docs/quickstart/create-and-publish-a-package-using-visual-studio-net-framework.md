---
title: Tworzenie i publikowanie pakietu platformy .NET Framework, za pomocą programu Visual Studio na Windows
description: Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet programu .NET Framework za pomocą programu Visual Studio 2017 na Windows.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: 68593211da1a34649c7050753a5db0f3a03cb41b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549631"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="37b93-103">Szybki Start: Tworzenie i publikowanie pakietu przy użyciu programu Visual Studio (.NET Framework, Windows)</span><span class="sxs-lookup"><span data-stu-id="37b93-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="37b93-104">Tworzenie pakietu NuGet w bibliotece klas programu .NET Framework obejmuje tworzenie biblioteki DLL w programie Visual Studio na Windows, a następnie przy użyciu narzędzia wiersza polecenia nuget.exe umożliwiającego tworzenie i publikowanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="37b93-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="37b93-105">Ten przewodnik Szybki Start ma zastosowanie do programu Visual Studio 2017 for Windows tylko.</span><span class="sxs-lookup"><span data-stu-id="37b93-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="37b93-106">Visual Studio dla komputerów Mac nie ma możliwości opisane w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="37b93-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="37b93-107">Użyj [narzędzi interfejsu wiersza polecenia dotnet](create-and-publish-a-package-using-the-dotnet-cli.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="37b93-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37b93-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="37b93-108">Prerequisites</span></span>

1. <span data-ttu-id="37b93-109">Instalowania dowolnej wersji programu Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) ze wszystkimi. Obciążenie związane z sieci.</span><span class="sxs-lookup"><span data-stu-id="37b93-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="37b93-110">Po zainstalowaniu obciążenia platformy .NET, Visual Studio 2017 zawiera automatycznie możliwości NuGet.</span><span class="sxs-lookup"><span data-stu-id="37b93-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="37b93-111">Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisywania, który `.exe` pliku do odpowiedniego folderu i dodawanie folderu do zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="37b93-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="37b93-112">[Zarejestruj, aby utworzyć bezpłatne konto w witrynie nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz jeszcze takiego.</span><span class="sxs-lookup"><span data-stu-id="37b93-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="37b93-113">Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="37b93-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="37b93-114">Aby można było przekazać pakiet, należy potwierdzić konto.</span><span class="sxs-lookup"><span data-stu-id="37b93-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="37b93-115">Utwórz projekt biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="37b93-115">Create a class library project</span></span>

<span data-ttu-id="37b93-116">Można użyć istniejącego projektu biblioteki klas .NET Framework dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="37b93-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="37b93-117">W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, wybierz opcję **Visual C#** węzła, wybierz szablon "Biblioteka klas (.NET Framework)", nazwij projekt AppLogger i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="37b93-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="37b93-118">Kliknij prawym przyciskiem myszy, wynikowy plik projektu, a następnie wybierz pozycję **kompilacji** się upewnić, że projekt został utworzony prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="37b93-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="37b93-119">Biblioteka DLL znajduje się w folderze debugowania (lub wydania, jeśli tworzysz tę konfigurację zamiast).</span><span class="sxs-lookup"><span data-stu-id="37b93-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="37b93-120">W ciągu rzeczywistą pakietu NuGet oczywiście, możesz zaimplementować wiele przydatnych funkcji, które inne osoby mogą tworzyć aplikacje.</span><span class="sxs-lookup"><span data-stu-id="37b93-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="37b93-121">Można również ustawić platform docelowych w dowolny sposób.</span><span class="sxs-lookup"><span data-stu-id="37b93-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="37b93-122">Na przykład, zapoznaj się z przewodnikami dla [platformy uniwersalnej systemu Windows](../guides/create-uwp-packages.md) i [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="37b93-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="37b93-123">W tym przewodniku jednak nie będzie pisania żadnego dodatkowego kodu ponieważ biblioteki klas na podstawie tego szablonu jest wystarczające, aby utworzyć pakiet.</span><span class="sxs-lookup"><span data-stu-id="37b93-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="37b93-124">Jednak jeśli chcesz funkcjonalności kodu dla pakietu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="37b93-124">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="37b93-125">Chyba że istnieje powód, aby wybrać inny sposób, .NET Standard jest preferowany cel pakiety NuGet, ponieważ zapewnia zgodność z szeroką gamą wykorzystywanie projektów.</span><span class="sxs-lookup"><span data-stu-id="37b93-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="37b93-126">Zobacz [tworzenie i publikowanie pakietu przy użyciu programu Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="37b93-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="37b93-127">Konfigurowanie właściwości projektu pakietu</span><span class="sxs-lookup"><span data-stu-id="37b93-127">Configure project properties for the package</span></span>

<span data-ttu-id="37b93-128">Pakiet NuGet zawiera manifest ( `.nuspec` pliku), który zawiera istotne metadane, takie jak identyfikator pakietu, numer wersji, opis i.</span><span class="sxs-lookup"><span data-stu-id="37b93-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="37b93-129">Niektóre z nich może być pobierana z właściwości projektu bezpośrednio, co pozwala uniknąć konieczności oddzielnie zaktualizować je w manifeście i projektu.</span><span class="sxs-lookup"><span data-stu-id="37b93-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="37b93-130">W tej sekcji opisano, gdzie można ustawić odpowiednich właściwości.</span><span class="sxs-lookup"><span data-stu-id="37b93-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="37b93-131">Wybierz **projektu > właściwości** menu polecenia, a następnie wybierz **aplikacji** kartę.</span><span class="sxs-lookup"><span data-stu-id="37b93-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="37b93-132">W **nazwy zestawu** pola, nadaj Unikatowy identyfikator pakietu.</span><span class="sxs-lookup"><span data-stu-id="37b93-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="37b93-133">Musisz nadać pakietu, identyfikator, który jest unikatowa w obrębie nuget.org, lub niezależnie od rodzaju hoście jest używany.</span><span class="sxs-lookup"><span data-stu-id="37b93-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="37b93-134">W ramach tego przewodnika firma Microsoft zaleca, tym "Próbny" lub "Test" w nazwie późniejszym etapie publikowania uwidocznić pakietu publicznie (choć jest mało prawdopodobne, każda osoba będzie faktycznie używać).</span><span class="sxs-lookup"><span data-stu-id="37b93-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="37b93-135">Jeśli spróbujesz opublikować pakietu o nazwie, która już istnieje, zostanie wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="37b93-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="37b93-136">Wybierz **informacje o zestawie...**  przycisk, który wywołuje okno dialogowe, w którym należy wprowadzić inne właściwości, które zawierają do manifestu (zobacz [odwołanie do pliku .nuspec - zastąpienia tokenów](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="37b93-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="37b93-137">Najczęściej używanych pól są **tytuł**, **opis**, **firmy**, **Copyright**, i **wersji zestawu**.</span><span class="sxs-lookup"><span data-stu-id="37b93-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="37b93-138">Te właściwości są wyświetlane ostatecznie z pakietem na hoście, np. nuget.org, dlatego upewnij się, że są one w pełni opisowe.</span><span class="sxs-lookup"><span data-stu-id="37b93-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Informacje o zestawie w projekcie programu .NET Framework w programie Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="37b93-140">Opcjonalnie: Aby wyświetlić i edytować właściwości bezpośrednio, otwórz `Properties/AssemblyInfo.cs` pliku w projekcie.</span><span class="sxs-lookup"><span data-stu-id="37b93-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="37b93-141">Po ustawieniu właściwości jest równa konfiguracji projektu **wersji** i ponownie skompiluj projekt, aby wygenerować zaktualizowanego pliku DLL.</span><span class="sxs-lookup"><span data-stu-id="37b93-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="37b93-142">Generuj manifest początkowej</span><span class="sxs-lookup"><span data-stu-id="37b93-142">Generate the initial manifest</span></span>

<span data-ttu-id="37b93-143">Z biblioteki DLL w zestawie właściwości strony, a projekt, możesz teraz używać `nuget spec` polecenie, aby wygenerować początkową `.nuspec` pliku z projektem.</span><span class="sxs-lookup"><span data-stu-id="37b93-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="37b93-144">Ten krok obejmuje odpowiednie zastąpienia tokenów pobierające informacje z pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="37b93-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="37b93-145">Możesz uruchomić `nuget spec` tylko raz, aby wygenerować manifest początkowej.</span><span class="sxs-lookup"><span data-stu-id="37b93-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="37b93-146">Podczas aktualizowania pakietu, można zmienić wartości w projekcie albo bezpośrednio edytować manifestu.</span><span class="sxs-lookup"><span data-stu-id="37b93-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="37b93-147">Otwórz wiersz polecenia i przejdź do folderu projektu zawierającego `AppLogger.csproj` pliku.</span><span class="sxs-lookup"><span data-stu-id="37b93-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="37b93-148">Uruchom następujące polecenie: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="37b93-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="37b93-149">Określając projektu, NuGet tworzy manifest, który jest zgodna z nazwą projektu, w tym przypadku `AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="37b93-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="37b93-150">To również obejmować zastąpienia tokenów w manifeście.</span><span class="sxs-lookup"><span data-stu-id="37b93-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="37b93-151">Otwórz `AppLogger.nuspec` w edytorze tekstów, aby zbadać jego zawartość, która powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="37b93-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a><span data-ttu-id="37b93-152">Edytuj manifest</span><span class="sxs-lookup"><span data-stu-id="37b93-152">Edit the manifest</span></span>

1. <span data-ttu-id="37b93-153">NuGet generuje błąd, Jeśli spróbujesz utworzyć pakiet z wartościami domyślnymi w swojej `.nuspec` plików, dlatego należy zmodyfikować następujące pola, przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="37b93-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="37b93-154">Zobacz [odwołanie do pliku .nuspec — elementy opcjonalne metadane](../reference/nuspec.md#optional-metadata-elements) opis jak są one używane.</span><span class="sxs-lookup"><span data-stu-id="37b93-154">See [.nuspec file reference - optional metadata elements](../reference/nuspec.md#optional-metadata-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="37b93-155">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="37b93-155">licenseUrl</span></span>
    - <span data-ttu-id="37b93-156">projectUrl</span><span class="sxs-lookup"><span data-stu-id="37b93-156">projectUrl</span></span>
    - <span data-ttu-id="37b93-157">IconUrl</span><span class="sxs-lookup"><span data-stu-id="37b93-157">iconUrl</span></span>
    - <span data-ttu-id="37b93-158">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="37b93-158">releaseNotes</span></span>
    - <span data-ttu-id="37b93-159">tagi</span><span class="sxs-lookup"><span data-stu-id="37b93-159">tags</span></span>

1. <span data-ttu-id="37b93-160">Pakiety utworzone do użytku publicznego, należy zwrócić szczególną uwagę na **tagi** właściwości, jak tagi pomóc innym odnaleźć pakietu na źródeł, takich jak nuget.org i zrozumieć, co robi.</span><span class="sxs-lookup"><span data-stu-id="37b93-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="37b93-161">Można również dodać inne elementy do manifestu w tej chwili zgodnie z opisem na [odwołanie do pliku .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="37b93-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="37b93-162">Zapisz plik przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="37b93-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="37b93-163">Uruchom polecenie pakietu</span><span class="sxs-lookup"><span data-stu-id="37b93-163">Run the pack command</span></span>

1. <span data-ttu-id="37b93-164">Z poziomu wiersza polecenia w folderze zawierającym swoje `.nuspec` pliku, uruchom polecenie `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="37b93-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="37b93-165">Generuje NuGet `.nupkg` pliku w postaci *version.nupkg identyfikator*, które znajdują się w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="37b93-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="37b93-166">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="37b93-166">Publish the package</span></span>

<span data-ttu-id="37b93-167">Po utworzeniu `.nupkg` pliku opublikujesz go w witrynie nuget.org przy użyciu `nuget.exe` przy użyciu klucza interfejsu API uzyskanych z repozytorium nuget.org. Nuget.org należy używać `nuget.exe` 4.1.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="37b93-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="37b93-168">Uzyskiwanie klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="37b93-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="37b93-169">Publikowanie za pomocą wypychania nuget</span><span class="sxs-lookup"><span data-stu-id="37b93-169">Publish with nuget push</span></span>

1. <span data-ttu-id="37b93-170">Zmień folder zawierający `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="37b93-170">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="37b93-171">Uruchom następujące polecenie, określając nazwę pakietu i zastępując wartość klucza swój klucz interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="37b93-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="37b93-172">nuget.exe wyświetla wyniki proces publikowania:</span><span class="sxs-lookup"><span data-stu-id="37b93-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="37b93-173">Zobacz [wypychania nuget](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="37b93-173">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="37b93-174">Publikowanie błędy</span><span class="sxs-lookup"><span data-stu-id="37b93-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="37b93-175">Zarządzanie opublikowany pakiet</span><span class="sxs-lookup"><span data-stu-id="37b93-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="37b93-176">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="37b93-176">Related topics</span></span>

- [<span data-ttu-id="37b93-177">Utwórz pakiet</span><span class="sxs-lookup"><span data-stu-id="37b93-177">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="37b93-178">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="37b93-178">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="37b93-179">Pakiety w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="37b93-179">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="37b93-180">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="37b93-180">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="37b93-181">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="37b93-181">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="37b93-182">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="37b93-182">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
