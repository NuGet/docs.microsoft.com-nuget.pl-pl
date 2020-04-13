---
title: Tworzenie i publikowanie pakietu NuGet programu .NET Framework przy użyciu programu Visual Studio w systemie Windows
description: Samouczek instruktażowy dotyczący tworzenia i publikowania pakietu NuGet programu .NET Framework przy użyciu programu Visual Studio w systemie Windows.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: e00aac83a710e2f745d5e4bb9aec741ee686e595
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380642"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="7f572-103">Szybki start: tworzenie i publikowanie pakietu przy użyciu programu Visual Studio (.NET Framework, Windows)</span><span class="sxs-lookup"><span data-stu-id="7f572-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="7f572-104">Tworzenie pakietu NuGet z biblioteki klas .NET Framework polega na utworzeniu biblioteki DLL w programie Visual Studio w systemie Windows, a następnie przy użyciu narzędzia wiersza polecenia nuget.exe do tworzenia i publikowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="7f572-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="7f572-105">Ten przewodnik Szybki start dotyczy programu Visual Studio 2017 i nowszych wersji tylko dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="7f572-105">This Quickstart applies to Visual Studio 2017 and higher versions for Windows only.</span></span> <span data-ttu-id="7f572-106">Visual Studio dla komputerów Mac nie zawiera możliwości opisanych w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="7f572-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="7f572-107">Zamiast tego użyj [narzędzi dotnet CLI.](create-and-publish-a-package-using-the-dotnet-cli.md)</span><span class="sxs-lookup"><span data-stu-id="7f572-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f572-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7f572-108">Prerequisites</span></span>

1. <span data-ttu-id="7f572-109">Zainstaluj dowolną wersję programu Visual Studio 2017 lub nowszą z [visualstudio.com](https://www.visualstudio.com/) z dowolnym . Obciążenie związane z siecią.</span><span class="sxs-lookup"><span data-stu-id="7f572-109">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="7f572-110">Visual Studio 2017 automatycznie zawiera funkcje NuGet po zainstalowaniu obciążenia platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="7f572-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="7f572-111">Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go `.exe` z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisując ten plik do odpowiedniego folderu i dodając ten folder do zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="7f572-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="7f572-112">[Zarejestruj się na darmowe konto w nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) jeśli jeszcze go nie masz.</span><span class="sxs-lookup"><span data-stu-id="7f572-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="7f572-113">Utworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="7f572-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="7f572-114">Musisz potwierdzić konto, zanim będzie można przesłać pakiet.</span><span class="sxs-lookup"><span data-stu-id="7f572-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="7f572-115">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="7f572-115">Create a class library project</span></span>

<span data-ttu-id="7f572-116">Można użyć istniejącego projektu biblioteki klas programu .NET Framework dla kodu, który chcesz spakować, lub utworzyć prosty w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="7f572-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="7f572-117">W programie Visual Studio wybierz polecenie **Plik > Nowy projekt >**, wybierz węzeł Visual **C#,** wybierz szablon "Biblioteka klas (.NET Framework)" , nazwij projekt AppLogger i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f572-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="7f572-118">Kliknij prawym przyciskiem myszy wynikowy plik projektu i wybierz **polecenie Build,** aby upewnić się, że projekt został prawidłowo utworzony.</span><span class="sxs-lookup"><span data-stu-id="7f572-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="7f572-119">Biblioteka DLL znajduje się w folderze debugowania (lub Release, jeśli zamiast tego skompilujesz tę konfigurację).</span><span class="sxs-lookup"><span data-stu-id="7f572-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="7f572-120">W ramach prawdziwego pakietu NuGet, oczywiście, można zaimplementować wiele przydatnych funkcji, za pomocą których inni mogą tworzyć aplikacje.</span><span class="sxs-lookup"><span data-stu-id="7f572-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="7f572-121">Można również ustawić struktury docelowe, jak chcesz.</span><span class="sxs-lookup"><span data-stu-id="7f572-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="7f572-122">Na przykład zobacz linie pomocnicze dotyczące [platformy uniwersalnej](../guides/create-uwp-packages.md) systemu i [platformy Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="7f572-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="7f572-123">W tym instruktażu jednak nie będzie pisać żadnego dodatkowego kodu, ponieważ biblioteka klas z szablonu jest wystarczająca do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="7f572-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="7f572-124">Mimo to, jeśli chcesz jakiś kod funkcjonalny dla pakietu, użyj następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="7f572-124">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="7f572-125">Jeśli nie masz powodu, aby wybrać inaczej, .NET Standard jest preferowanym obiektem docelowym dla pakietów NuGet, ponieważ zapewnia zgodność z najszerszym zakresem projektów zużywających.</span><span class="sxs-lookup"><span data-stu-id="7f572-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="7f572-126">Zobacz [Tworzenie i publikowanie pakietu przy użyciu programu Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="7f572-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="7f572-127">Konfigurowanie właściwości projektu dla pakietu</span><span class="sxs-lookup"><span data-stu-id="7f572-127">Configure project properties for the package</span></span>

<span data-ttu-id="7f572-128">Pakiet NuGet zawiera manifest `.nuspec` (plik), który zawiera odpowiednie metadane, takie jak identyfikator pakietu, numer wersji, opis i inne.</span><span class="sxs-lookup"><span data-stu-id="7f572-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="7f572-129">Niektóre z nich można wyciągnąć bezpośrednio z właściwości projektu, co pozwala uniknąć konieczności oddzielnej aktualizacji ich zarówno w projekcie, jak i w manifeście.</span><span class="sxs-lookup"><span data-stu-id="7f572-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="7f572-130">W tej sekcji opisano, gdzie można ustawić odpowiednie właściwości.</span><span class="sxs-lookup"><span data-stu-id="7f572-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="7f572-131">Wybierz polecenie menu **Właściwości projektu >,** a następnie wybierz kartę **Aplikacja.**</span><span class="sxs-lookup"><span data-stu-id="7f572-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="7f572-132">W polu **Nazwa zestawu** nadaj pakietowi unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="7f572-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="7f572-133">Należy nadać pakietowi identyfikator, który jest unikatowy w nuget.org lub niezależnie od hosta, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="7f572-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="7f572-134">W tym instruktażu zalecamy dołączenie "Przykład" lub "Test" w nazwie, ponieważ późniejszy krok publikowania powoduje, że pakiet jest publicznie widoczny (choć jest mało prawdopodobne, aby ktoś go faktycznie używał).</span><span class="sxs-lookup"><span data-stu-id="7f572-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="7f572-135">Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="7f572-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="7f572-136">Wybierz przycisk **Informacje o złożeniu...** z wyświetlonym okszeniem dialogowym, w którym można wprowadzić inne właściwości, które przenoszą do manifestu (patrz [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="7f572-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="7f572-137">Najczęściej używane pola to **Tytuł**, **Opis**, **Firma**, **Prawa autorskie**i Wersja **zestawu**.</span><span class="sxs-lookup"><span data-stu-id="7f572-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="7f572-138">Te właściwości ostatecznie pojawiają się z pakietem na hoście, takim jak nuget.org, więc upewnij się, że są w pełni opisowe.</span><span class="sxs-lookup"><span data-stu-id="7f572-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Informacje o zestawie w projekcie programu .NET Framework w programie Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="7f572-140">Opcjonalnie: aby wyświetlić i edytować `Properties/AssemblyInfo.cs` właściwości bezpośrednio, otwórz plik w projekcie.</span><span class="sxs-lookup"><span data-stu-id="7f572-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="7f572-141">Po ustawieniu właściwości ustaw konfigurację projektu na **Zwolnij** i odbuduj projekt, aby wygenerować zaktualizowaną bibliotekę DLL.</span><span class="sxs-lookup"><span data-stu-id="7f572-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="7f572-142">Generowanie manifestu początkowego</span><span class="sxs-lookup"><span data-stu-id="7f572-142">Generate the initial manifest</span></span>

<span data-ttu-id="7f572-143">Z DLL w ręku i właściwości projektu `nuget spec` zestaw, można `.nuspec` teraz użyć polecenia do wygenerowania pliku początkowego z projektu.</span><span class="sxs-lookup"><span data-stu-id="7f572-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="7f572-144">Ten krok zawiera odpowiednie tokeny zastępcze do rysowania informacji z pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="7f572-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="7f572-145">Uruchom `nuget spec` tylko raz, aby wygenerować manifest początkowy.</span><span class="sxs-lookup"><span data-stu-id="7f572-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="7f572-146">Podczas aktualizowania pakietu, można zmienić wartości w projekcie lub edytować manifest bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="7f572-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="7f572-147">Otwórz wiersz polecenia i przejdź do `AppLogger.csproj` folderu projektu zawierającego plik.</span><span class="sxs-lookup"><span data-stu-id="7f572-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="7f572-148">Uruchom następujące polecenie: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="7f572-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="7f572-149">Określając projekt, NuGet tworzy manifest, który pasuje do nazwy projektu, w tym przypadku. `AppLogger.nuspec`</span><span class="sxs-lookup"><span data-stu-id="7f572-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="7f572-150">Zawiera również tokeny zastępowania w manifeście.</span><span class="sxs-lookup"><span data-stu-id="7f572-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="7f572-151">Otwórz `AppLogger.nuspec` w edytorze tekstu, aby sprawdzić jego zawartość, która powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="7f572-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

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

## <a name="edit-the-manifest"></a><span data-ttu-id="7f572-152">Edytowanie manifestu</span><span class="sxs-lookup"><span data-stu-id="7f572-152">Edit the manifest</span></span>

1. <span data-ttu-id="7f572-153">NuGet generuje błąd, jeśli spróbujesz utworzyć pakiet `.nuspec` z wartościami domyślnymi w pliku, więc należy edytować następujące pola przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="7f572-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="7f572-154">Zobacz [.nuspec odwołanie do pliku — opcjonalne elementy metadanych,](../reference/nuspec.md#optional-metadata-elements) aby uzyskać opis sposobu ich użycia.</span><span class="sxs-lookup"><span data-stu-id="7f572-154">See [.nuspec file reference - optional metadata elements](../reference/nuspec.md#optional-metadata-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="7f572-155">licencjaUrl</span><span class="sxs-lookup"><span data-stu-id="7f572-155">licenseUrl</span></span>
    - <span data-ttu-id="7f572-156">projektUrl</span><span class="sxs-lookup"><span data-stu-id="7f572-156">projectUrl</span></span>
    - <span data-ttu-id="7f572-157">ikonaUrl</span><span class="sxs-lookup"><span data-stu-id="7f572-157">iconUrl</span></span>
    - <span data-ttu-id="7f572-158">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="7f572-158">releaseNotes</span></span>
    - <span data-ttu-id="7f572-159">tags</span><span class="sxs-lookup"><span data-stu-id="7f572-159">tags</span></span>

1. <span data-ttu-id="7f572-160">W przypadku pakietów przeznaczonych do użytku publicznego należy zwrócić szczególną uwagę na właściwość **Tagi,** ponieważ tagi pomagają innym znaleźć pakiet w źródłach takich jak nuget.org i zrozumieć, co robi.</span><span class="sxs-lookup"><span data-stu-id="7f572-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="7f572-161">W tej chwili można również dodać dowolne inne elementy do manifestu, zgodnie z opisem w [pliku .nuspec.](../reference/nuspec.md)</span><span class="sxs-lookup"><span data-stu-id="7f572-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="7f572-162">Zapisz plik przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="7f572-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="7f572-163">Uruchamianie polecenia pack</span><span class="sxs-lookup"><span data-stu-id="7f572-163">Run the pack command</span></span>

1. <span data-ttu-id="7f572-164">W wierszu polecenia w folderze zawierającym `.nuspec` `nuget pack`plik uruchom polecenie .</span><span class="sxs-lookup"><span data-stu-id="7f572-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="7f572-165">NuGet generuje `.nupkg` plik w postaci *identyfikatora-version.nupkg*, który znajdziesz w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="7f572-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="7f572-166">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="7f572-166">Publish the package</span></span>

<span data-ttu-id="7f572-167">Po opublikowaniu `.nupkg` pliku można go opublikować w `nuget.exe` celu nuget.org przy użyciu klucza interfejsu API uzyskanego z nuget.org. W przypadku nuget.org należy `nuget.exe` używać 4.1.0 lub nowszego.</span><span class="sxs-lookup"><span data-stu-id="7f572-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="7f572-168">Uzyskaj klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="7f572-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="7f572-169">Publikuj z nuget push</span><span class="sxs-lookup"><span data-stu-id="7f572-169">Publish with nuget push</span></span>

1. <span data-ttu-id="7f572-170">Otwórz wiersz polecenia i zmień folder `.nupkg` zawierający plik.</span><span class="sxs-lookup"><span data-stu-id="7f572-170">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="7f572-171">Uruchom następujące polecenie, określając nazwę pakietu i zastępując wartość klucza kluczem interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="7f572-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="7f572-172">nuget.exe wyświetla wyniki procesu publikowania:</span><span class="sxs-lookup"><span data-stu-id="7f572-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="7f572-173">Zobacz [nuget push](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="7f572-173">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="7f572-174">Błędy publikowania</span><span class="sxs-lookup"><span data-stu-id="7f572-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="7f572-175">Zarządzanie opublikowanym pakietem</span><span class="sxs-lookup"><span data-stu-id="7f572-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="7f572-176">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7f572-176">Next steps</span></span>

<span data-ttu-id="7f572-177">Gratulujemy stworzenia pierwszego pakietu NuGet!</span><span class="sxs-lookup"><span data-stu-id="7f572-177">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f572-178">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="7f572-178">Create a Package</span></span>](../create-packages/creating-a-package.md)

<span data-ttu-id="7f572-179">Aby dowiedzieć się więcej, że NuGet ma do zaoferowania, wybierz poniższe łącza.</span><span class="sxs-lookup"><span data-stu-id="7f572-179">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="7f572-180">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="7f572-180">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="7f572-181">Pakiety w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="7f572-181">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="7f572-182">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="7f572-182">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="7f572-183">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="7f572-183">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="7f572-184">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="7f572-184">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
