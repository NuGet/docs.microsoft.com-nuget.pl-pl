---
title: Przewodnik wprowadzający do tworzenia i publikowania pakietu NuGet .NET Framework za pomocą programu Visual Studio
description: Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet programu .NET Framework za pomocą programu Visual Studio 2017 r.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/13/2018
ms.topic: quickstart
ms.openlocfilehash: 01760034a121b1ff6f227e006415779898c4cf6d
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework"></a><span data-ttu-id="8c139-103">Szybki Start: Tworzenie i publikowanie pakietu programu Visual Studio (.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="8c139-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework)</span></span>

<span data-ttu-id="8c139-104">Tworzenie pakietu NuGet w bibliotece klas programu .NET Framework obejmuje tworzenie biblioteki DLL w programie Visual Studio, a następnie tworzyć i publikować pakietu przy użyciu narzędzia wiersza polecenia nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="8c139-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio, then using the nuget.exe command line tool to create and publish the package.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c139-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8c139-105">Prerequisites</span></span>

1. <span data-ttu-id="8c139-106">Zainstalowania dowolnej wersji programu Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) ze wszystkimi. Obciążenia związane z sieci.</span><span class="sxs-lookup"><span data-stu-id="8c139-106">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="8c139-107">Visual Studio 2017 automatycznie uwzględnia możliwości NuGet obciążenia .NET jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="8c139-107">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="8c139-108">Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisywanie, który `.exe` pliku do odpowiedniego folderu, a następnie dodanie tego folderu do Twojej zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="8c139-108">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="8c139-109">[Zarejestruj bezpłatne konto na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz już.</span><span class="sxs-lookup"><span data-stu-id="8c139-109">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="8c139-110">Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="8c139-110">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="8c139-111">Aby przekazać pakiet, musisz potwierdzić konto.</span><span class="sxs-lookup"><span data-stu-id="8c139-111">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="8c139-112">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="8c139-112">Create a class library project</span></span>

<span data-ttu-id="8c139-113">Można użyć istniejącego projektu biblioteki klas programu .NET Framework dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="8c139-113">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="8c139-114">W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, wybierz pozycję **Visual C#** węzła, wybierz szablon "Biblioteki klas (.NET Framework)", nazwa projektu AppLogger i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8c139-114">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="8c139-115">Kliknij prawym przyciskiem myszy na wynikowy plik projektu i wybierz **kompilacji** się upewnić, że projekt został utworzony prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="8c139-115">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="8c139-116">Biblioteki DLL znajduje się w folderze debugowania (lub wersji, jeśli zamiast tego kompilacji tej konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="8c139-116">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="8c139-117">W rzeczywistym pakiecie NuGet oczywiście zaimplementowaniem wielu przydatnych funkcji, które inne osoby mogą tworzyć aplikacje.</span><span class="sxs-lookup"><span data-stu-id="8c139-117">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="8c139-118">Można również ustawić docelowych platform w dowolny sposób.</span><span class="sxs-lookup"><span data-stu-id="8c139-118">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="8c139-119">Na przykład, zobacz wskazówki dotyczące [UWP](../guides/create-uwp-packages.md) i [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="8c139-119">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="8c139-120">W ramach tego przewodnika jednak nie będzie pisania jakiegokolwiek dodatkowego kodu ponieważ biblioteki klas z szablonu jest wystarczające, aby utworzyć pakiet.</span><span class="sxs-lookup"><span data-stu-id="8c139-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="8c139-121">Nadal Jeśli chcesz funkcjonalności kodu dla pakietu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="8c139-121">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="8c139-122">Chyba że masz powód, w przeciwnym razie wybierz .NET Standard preferowanych celem jest pakietów NuGet, ponieważ zapewnia zgodność z szeroką gamą korzystanie z projektów.</span><span class="sxs-lookup"><span data-stu-id="8c139-122">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="8c139-123">Zobacz [tworzenie i publikowanie pakietu programu Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="8c139-123">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="8c139-124">Skonfiguruj właściwości projektu dla pakietu</span><span class="sxs-lookup"><span data-stu-id="8c139-124">Configure project properties for the package</span></span>

<span data-ttu-id="8c139-125">Pakiet NuGet zawiera manifest ( `.nuspec` pliku), który zawiera odpowiednie metadane, takie jak identyfikator pakietu, numer wersji, opis i.</span><span class="sxs-lookup"><span data-stu-id="8c139-125">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="8c139-126">Niektóre z nich może być pobierana właściwości projektu, który pozwala uniknąć konieczności zaktualizowania ich osobno w manifeście i projektu.</span><span class="sxs-lookup"><span data-stu-id="8c139-126">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="8c139-127">Ta sekcja zawiera wskazówki dotyczące Ustaw odpowiednie właściwości.</span><span class="sxs-lookup"><span data-stu-id="8c139-127">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="8c139-128">Wybierz **projektu > właściwości** menu polecenie, a następnie wybierz **aplikacji** kartę.</span><span class="sxs-lookup"><span data-stu-id="8c139-128">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="8c139-129">W **nazwy zestawu** pola, nadaj Unikatowy identyfikator pakietu.</span><span class="sxs-lookup"><span data-stu-id="8c139-129">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="8c139-130">Podaj pakiet używany unikatowy identyfikator w nuget.org lub niezależnie od hosta można.</span><span class="sxs-lookup"><span data-stu-id="8c139-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="8c139-131">W ramach tego przewodnika, zaleca się tym "Sample" lub "Test" w nazwie, ponieważ kolejnych kroków publikowania pakietu widocznego publicznie (chociaż jest mało prawdopodobne, każda osoba, która zostanie rzeczywiście używane).</span><span class="sxs-lookup"><span data-stu-id="8c139-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="8c139-132">Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="8c139-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="8c139-133">Wybierz **informacji o zestawie...**  przycisku, który wywołuje okno dialogowe, w którym należy wprowadzić w manifeście innych właściwości, które obsługują (zobacz [odwołania do pliku .nuspec — zastępczy tokenów](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="8c139-133">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="8c139-134">Najczęściej używane pola są **tytuł**, **opis**, **firmy**, **Copyright**, i **wersja zestawu**.</span><span class="sxs-lookup"><span data-stu-id="8c139-134">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="8c139-135">Dlatego te właściwości są wyświetlane ostatecznie w pakiecie na hoście, takich jak nuget.org, upewnij się, że są one w pełni opisowy.</span><span class="sxs-lookup"><span data-stu-id="8c139-135">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Informacje o zestawie w projekcie programu .NET Framework w programie Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="8c139-137">Opcjonalnie: Aby wyświetlić i edytować właściwości bezpośrednio, otwórz `Properties/AssemblyInfo.cs` pliku w projekcie.</span><span class="sxs-lookup"><span data-stu-id="8c139-137">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="8c139-138">Właściwości ustawione, ustaw dla konfiguracji projektu **wersji** i skompiluj ponownie projekt, aby wygenerować zaktualizowanej biblioteki DLL.</span><span class="sxs-lookup"><span data-stu-id="8c139-138">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="8c139-139">Generuj manifest początkowej</span><span class="sxs-lookup"><span data-stu-id="8c139-139">Generate the initial manifest</span></span>

<span data-ttu-id="8c139-140">Z biblioteki DLL w zestawie właściwości strony, a projekt, można teraz używać `nuget spec` polecenie, aby wygenerować początkowego `.nuspec` plik z projektu.</span><span class="sxs-lookup"><span data-stu-id="8c139-140">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="8c139-141">Ten krok obejmuje tokeny zastępczy odpowiednie do rysowania informacji z pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="8c139-141">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="8c139-142">Uruchomienie `nuget spec` tylko jeden raz, aby wygenerować manifest początkowej.</span><span class="sxs-lookup"><span data-stu-id="8c139-142">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="8c139-143">Podczas aktualizowania pakietu, można zmienić wartości w projekcie albo bezpośredniego edytowania manifestu.</span><span class="sxs-lookup"><span data-stu-id="8c139-143">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="8c139-144">Otwórz wiersz polecenia i przejdź do folderu projektu zawierającego `AppLogger.csproj` pliku.</span><span class="sxs-lookup"><span data-stu-id="8c139-144">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="8c139-145">Uruchom następujące polecenie: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="8c139-145">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="8c139-146">Określając projektu NuGet tworzy manifestu, który pasuje do nazwy projektu, w tym przypadku `AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="8c139-146">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="8c139-147">Również obejmować tokeny zastąpienia w manifeście.</span><span class="sxs-lookup"><span data-stu-id="8c139-147">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="8c139-148">Otwórz `AppLogger.nuspec` w edytorze tekstów, aby zbadać jego zawartość, która powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="8c139-148">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

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

## <a name="edit-the-manifest"></a><span data-ttu-id="8c139-149">Edytuj manifest</span><span class="sxs-lookup"><span data-stu-id="8c139-149">Edit the manifest</span></span>

1. <span data-ttu-id="8c139-150">NuGet powoduje błąd przy próbie utworzenia pakietu z wartościami domyślnymi w Twojej `.nuspec` plików, dlatego należy zmodyfikować następujące pola przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="8c139-150">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="8c139-151">Zobacz [odwołania do pliku .nuspec — pojedyncze elementy](../reference/nuspec.md#single-elements) opis jak są one używane.</span><span class="sxs-lookup"><span data-stu-id="8c139-151">See [.nuspec file reference - single elements](../reference/nuspec.md#single-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="8c139-152">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="8c139-152">licenseUrl</span></span>
    - <span data-ttu-id="8c139-153">projectUrl</span><span class="sxs-lookup"><span data-stu-id="8c139-153">projectUrl</span></span>
    - <span data-ttu-id="8c139-154">iconUrl</span><span class="sxs-lookup"><span data-stu-id="8c139-154">iconUrl</span></span>
    - <span data-ttu-id="8c139-155">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="8c139-155">releaseNotes</span></span>
    - <span data-ttu-id="8c139-156">tagi</span><span class="sxs-lookup"><span data-stu-id="8c139-156">tags</span></span>

1. <span data-ttu-id="8c139-157">Skompilowany dla publicznych zużycia pakietów, należy zwrócić szczególną uwagę na **tagi** właściwości, jak tagi ułatwiała innym pakietu na źródeł, takich jak nuget.org odnaleźć i zrozumieć, jakie operacje.</span><span class="sxs-lookup"><span data-stu-id="8c139-157">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="8c139-158">Możesz także dodać inne elementy do manifestu w tej chwili zgodnie z opisem na [odwołania do pliku .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="8c139-158">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="8c139-159">Zapisz plik przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="8c139-159">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="8c139-160">Uruchom polecenie pakietu</span><span class="sxs-lookup"><span data-stu-id="8c139-160">Run the pack command</span></span>

1. <span data-ttu-id="8c139-161">Z wiersza polecenia w folder zawierający Twoje `.nuspec` plików, uruchom polecenie `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="8c139-161">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="8c139-162">Generuje NuGet `.nupkg` pliku w postaci *version.nupkg identyfikator*, które znajdują się w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="8c139-162">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="8c139-163">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="8c139-163">Publish the package</span></span>

<span data-ttu-id="8c139-164">Po utworzeniu `.nupkg` pliku opublikowaniu go przy użyciu nuget.org `nuget.exe` przy użyciu klucza interfejsu API uzyskane z nuget.org. W przypadku nuget.org należy użyć `nuget.exe` 4.1.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="8c139-164">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="8c139-165">Uzyskanie klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="8c139-165">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="8c139-166">Publikowanie za pomocą wypychania nuget</span><span class="sxs-lookup"><span data-stu-id="8c139-166">Publish with nuget push</span></span>

1. <span data-ttu-id="8c139-167">Zmień folder zawierający `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="8c139-167">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="8c139-168">Uruchom następujące polecenie, określając nazwę pakietu i zamianę klucza wartość klucza interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="8c139-168">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="8c139-169">nuget.exe wyświetla wyniki procesu publikowania:</span><span class="sxs-lookup"><span data-stu-id="8c139-169">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="8c139-170">Zobacz [wypychania nuget](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="8c139-170">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="8c139-171">Publikowanie błędów</span><span class="sxs-lookup"><span data-stu-id="8c139-171">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="8c139-172">Zarządzanie opublikowanego pakietu</span><span class="sxs-lookup"><span data-stu-id="8c139-172">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="8c139-173">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="8c139-173">Related topics</span></span>

- [<span data-ttu-id="8c139-174">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="8c139-174">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="8c139-175">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="8c139-175">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="8c139-176">Pakiety wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="8c139-176">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="8c139-177">Obsługuje wiele platform docelowych</span><span class="sxs-lookup"><span data-stu-id="8c139-177">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="8c139-178">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="8c139-178">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="8c139-179">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="8c139-179">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
