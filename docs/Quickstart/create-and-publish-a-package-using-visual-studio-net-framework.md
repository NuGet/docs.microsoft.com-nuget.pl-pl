---
title: "Przewodnik wprowadzający do tworzenia i publikowania pakietu NuGet .NET Framework za pomocą programu Visual Studio | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet programu .NET Framework za pomocą programu Visual Studio 2017 r."
keywords: "Pakiet NuGet tworzenie, publikowanie pakietu NuGet, samouczek NuGet programu Visual Studio Utwórz pakiet NuGet, pakiet programu msbuild"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 613cb6e8cf5762f354d69aa271c1e2f0d4851c97
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
---
# <a name="create-and-publish-a-package-using-visual-studio-net-framework"></a><span data-ttu-id="9ca1d-104">Tworzenie i publikowanie pakietu programu Visual Studio (.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="9ca1d-104">Create and publish a package using Visual Studio (.NET Framework)</span></span>

<span data-ttu-id="9ca1d-105">Tworzenie pakietu NuGet w bibliotece klas programu .NET Framework obejmuje tworzenie biblioteki DLL w programie Visual Studio, a następnie tworzyć i publikować pakietu przy użyciu narzędzia wiersza polecenia nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-105">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio, then using the nuget.exe command line tool to create and publish the package.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ca1d-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9ca1d-106">Prerequisites</span></span>

1. <span data-ttu-id="9ca1d-107">Zainstalowania dowolnej wersji programu Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/) ze wszystkimi. Obciążenia związane z sieci.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="9ca1d-108">Visual Studio 2017 automatycznie uwzględnia możliwości NuGet obciążenia .NET jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-108">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="9ca1d-109">Zainstaluj `nuget.exe` interfejsu wiersza polecenia, pobierając go z [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), zapisywanie, który `.exe` pliku do odpowiedniego folderu, a następnie dodanie tego folderu do Twojej zmiennej środowiskowej PATH.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-109">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="9ca1d-110">[Zarejestruj bezpłatne konto na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz już.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-110">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="9ca1d-111">Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-111">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="9ca1d-112">Aby przekazać pakiet, musisz potwierdzić konto.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-112">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="9ca1d-113">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="9ca1d-113">Create a class library project</span></span>

<span data-ttu-id="9ca1d-114">Można użyć istniejącego projektu biblioteki klas programu .NET Framework dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9ca1d-114">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="9ca1d-115">W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, wybierz pozycję **Visual C#** węzła, wybierz szablon "Biblioteki klas (.NET Framework)", nazwa projektu AppLogger i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-115">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="9ca1d-116">Kliknij prawym przyciskiem myszy na wynikowy plik projektu i wybierz **kompilacji** się upewnić, że projekt został utworzony prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-116">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="9ca1d-117">Biblioteki DLL znajduje się w folderze debugowania (lub wersji, jeśli zamiast tego kompilacji tej konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="9ca1d-117">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="9ca1d-118">W rzeczywistym pakiecie NuGet oczywiście zaimplementowaniem wielu przydatnych funkcji, które inne osoby mogą tworzyć aplikacje.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-118">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="9ca1d-119">Można również ustawić docelowych platform w dowolny sposób.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-119">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="9ca1d-120">Na przykład, zobacz wskazówki dotyczące [UWP](../guides/create-uwp-packages.md) i [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="9ca1d-120">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="9ca1d-121">W ramach tego przewodnika jednak nie będzie pisania jakiegokolwiek dodatkowego kodu ponieważ biblioteki klas z szablonu jest wystarczające, aby utworzyć pakiet.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-121">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="9ca1d-122">Nadal Jeśli chcesz funkcjonalności kodu dla pakietu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9ca1d-122">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="9ca1d-123">Chyba że masz powód, w przeciwnym razie wybierz .NET Standard preferowanych celem jest pakietów NuGet, ponieważ zapewnia zgodność z szeroką gamą korzystanie z projektów.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-123">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="9ca1d-124">Zobacz [tworzenie i publikowanie pakietu programu Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="9ca1d-124">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="9ca1d-125">Skonfiguruj właściwości projektu dla pakietu</span><span class="sxs-lookup"><span data-stu-id="9ca1d-125">Configure project properties for the package</span></span>

<span data-ttu-id="9ca1d-126">Pakiet NuGet zawiera manifest ( `.nuspec` pliku), który zawiera odpowiednie metadane, takie jak identyfikator pakietu, numer wersji, opis i.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-126">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="9ca1d-127">Niektóre z nich może być pobierana właściwości projektu, który pozwala uniknąć konieczności zaktualizowania ich osobno w manifeście i projektu.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-127">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="9ca1d-128">Ta sekcja zawiera wskazówki dotyczące Ustaw odpowiednie właściwości.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-128">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="9ca1d-129">Wybierz **projektu > właściwości** menu polecenie, a następnie wybierz **aplikacji** kartę.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-129">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="9ca1d-130">W **nazwy zestawu** pola, nadaj Unikatowy identyfikator pakietu.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-130">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="9ca1d-131">Podaj pakiet używany unikatowy identyfikator w nuget.org lub niezależnie od hosta można.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-131">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="9ca1d-132">W ramach tego przewodnika, zaleca się tym "Sample" lub "Test" w nazwie, ponieważ kolejnych kroków publikowania pakietu widocznego publicznie (chociaż jest mało prawdopodobne, każda osoba, która zostanie rzeczywiście używane).</span><span class="sxs-lookup"><span data-stu-id="9ca1d-132">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="9ca1d-133">Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-133">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="9ca1d-134">Wybierz **informacji o zestawie...**  przycisku, który wywołuje okno dialogowe, w którym należy wprowadzić w manifeście innych właściwości, które obsługują (zobacz [odwołania do pliku .nuspec — zastępczy tokenów](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="9ca1d-134">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="9ca1d-135">Najczęściej używane pola są **tytuł**, **opis**, **firmy**, **Copyright**, i **wersja zestawu**.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-135">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="9ca1d-136">Dlatego te właściwości są wyświetlane ostatecznie w pakiecie na hoście, takich jak nuget.org, upewnij się, że są one w pełni opisowy.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-136">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Informacje o zestawie w projekcie programu .NET Framework w programie Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="9ca1d-138">Opcjonalnie: Aby wyświetlić i edytować właściwości bezpośrednio, otwórz `Properties/AssemblyInfo.cs` pliku w projekcie.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-138">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="9ca1d-139">Właściwości ustawione, ustaw dla konfiguracji projektu **wersji** i skompiluj ponownie projekt, aby wygenerować zaktualizowanej biblioteki DLL.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-139">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="9ca1d-140">Generuj manifest początkowej</span><span class="sxs-lookup"><span data-stu-id="9ca1d-140">Generate the initial manifest</span></span>

<span data-ttu-id="9ca1d-141">Z biblioteki DLL w zestawie właściwości strony, a projekt, można teraz używać `nuget spec` polecenie, aby wygenerować początkowego `.nuspec` plik z projektu.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-141">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="9ca1d-142">Ten krok obejmuje tokeny zastępczy odpowiednie do rysowania informacji z pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-142">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="9ca1d-143">Uruchomienie `nuget spec` tylko jeden raz, aby wygenerować manifest początkowej.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-143">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="9ca1d-144">Podczas aktualizowania pakietu, można zmienić wartości w projekcie albo bezpośredniego edytowania manifestu.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-144">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="9ca1d-145">Otwórz wiersz polecenia i przejdź do folderu projektu zawierającego `AppLogger.csproj` pliku.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-145">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="9ca1d-146">Uruchom następujące polecenie: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-146">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="9ca1d-147">Określając projektu NuGet tworzy manifestu, który pasuje do nazwy projektu, w tym przypadku `AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-147">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="9ca1d-148">Również obejmować tokeny zastąpienia w manifeście.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-148">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="9ca1d-149">Otwórz `AppLogger.nuspec` w edytorze tekstów, aby zbadać jego zawartość, która powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="9ca1d-149">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

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

## <a name="edit-the-manifest"></a><span data-ttu-id="9ca1d-150">Edytuj manifest</span><span class="sxs-lookup"><span data-stu-id="9ca1d-150">Edit the manifest</span></span>

1. <span data-ttu-id="9ca1d-151">NuGet powoduje błąd przy próbie utworzenia pakietu z wartościami domyślnymi w Twojej `.nuspec` plików, dlatego należy zmodyfikować następujące pola przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-151">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="9ca1d-152">Zobacz [odwołania do pliku .nuspec — pojedyncze elementy](../reference/nuspec.md#single-elements) opis jak są one używane.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-152">See [.nuspec file reference - single elements](../reference/nuspec.md#single-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="9ca1d-153">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="9ca1d-153">licenseUrl</span></span>
    - <span data-ttu-id="9ca1d-154">projectUrl</span><span class="sxs-lookup"><span data-stu-id="9ca1d-154">projectUrl</span></span>
    - <span data-ttu-id="9ca1d-155">iconUrl</span><span class="sxs-lookup"><span data-stu-id="9ca1d-155">iconUrl</span></span>
    - <span data-ttu-id="9ca1d-156">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="9ca1d-156">releaseNotes</span></span>
    - <span data-ttu-id="9ca1d-157">tagi</span><span class="sxs-lookup"><span data-stu-id="9ca1d-157">tags</span></span>

1. <span data-ttu-id="9ca1d-158">Skompilowany dla publicznych zużycia pakietów, należy zwrócić szczególną uwagę na **tagi** właściwości, jak tagi ułatwiała innym pakietu na źródeł, takich jak nuget.org odnaleźć i zrozumieć, jakie operacje.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-158">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="9ca1d-159">Możesz także dodać inne elementy do manifestu w tej chwili zgodnie z opisem na [odwołania do pliku .nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="9ca1d-159">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="9ca1d-160">Zapisz plik przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-160">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="9ca1d-161">Uruchom polecenie pakietu</span><span class="sxs-lookup"><span data-stu-id="9ca1d-161">Run the pack command</span></span>

1. <span data-ttu-id="9ca1d-162">Z wiersza polecenia w folder zawierający Twoje `.nuspec` plików, uruchom polecenie `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-162">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="9ca1d-163">Generuje NuGet `.nupkg` pliku w postaci *version.nupkg identyfikator*, które znajdują się w bieżącym folderze.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-163">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="9ca1d-164">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="9ca1d-164">Publish the package</span></span>

<span data-ttu-id="9ca1d-165">Po utworzeniu `.nupkg` pliku opublikowaniu go przy użyciu nuget.org `nuget.exe` przy użyciu klucza interfejsu API uzyskane z nuget.org. W przypadku nuget.org należy użyć `nuget.exe` 4.1.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-165">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="9ca1d-166">Uzyskanie klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="9ca1d-166">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="9ca1d-167">Publikowanie za pomocą wypychania nuget</span><span class="sxs-lookup"><span data-stu-id="9ca1d-167">Publish with nuget push</span></span>

1. <span data-ttu-id="9ca1d-168">Zmień folder zawierający `.nupkg` pliku.</span><span class="sxs-lookup"><span data-stu-id="9ca1d-168">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="9ca1d-169">Uruchom następujące polecenie, określając nazwę pakietu i zamianę klucza wartość klucza interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="9ca1d-169">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="9ca1d-170">nuget.exe wyświetla wyniki procesu publikowania:</span><span class="sxs-lookup"><span data-stu-id="9ca1d-170">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="9ca1d-171">Zobacz [wypychania nuget](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="9ca1d-171">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="9ca1d-172">Publikowanie błędów</span><span class="sxs-lookup"><span data-stu-id="9ca1d-172">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="9ca1d-173">Zarządzanie opublikowanego pakietu</span><span class="sxs-lookup"><span data-stu-id="9ca1d-173">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="9ca1d-174">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="9ca1d-174">Related topics</span></span>

- [<span data-ttu-id="9ca1d-175">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="9ca1d-175">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="9ca1d-176">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="9ca1d-176">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="9ca1d-177">Obsługuje wiele platform docelowych</span><span class="sxs-lookup"><span data-stu-id="9ca1d-177">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="9ca1d-178">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="9ca1d-178">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="9ca1d-179">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="9ca1d-179">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
