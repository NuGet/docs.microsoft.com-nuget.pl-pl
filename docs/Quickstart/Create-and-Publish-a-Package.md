---
title: "Przewodnik wprowadzający do tworzenia i pakietu NuGet publikowania | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/03/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet przy użyciu interfejsu wiersza polecenia nuget.exe i Visual Studio."
keywords: Tworzenie pakietu NuGet, pakietu NuGet publikowania, samouczek NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53d29283c9e786fc27e9a608d7d251d8d0b5b0b2
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="94ad0-104">Tworzenie i publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="94ad0-104">Create and publish a package</span></span>

<span data-ttu-id="94ad0-105">Jest to prosty proces tworzenia pakietu NuGet z biblioteki klas .NET i opublikowania go w usłudze nuget.org. Ten artykuł przeprowadzi Cię przez proces, korzystając z NuGet interfejsu wiersza polecenia (CLI) i Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="94ad0-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. This article walks you through the process using the NuGet command-line interface (CLI) and Visual Studio.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="94ad0-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="94ad0-106">Pre-requisites</span></span>

1. <span data-ttu-id="94ad0-107">Zainstalowania dowolnej wersji programu Visual Studio 2017 z [visualstudio.com](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="94ad0-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="94ad0-108">Zainstaluj narzędzie interfejsu wiersza polecenia NuGet `nuget.exe`, pobierając najnowszą wersję `nuget.exe` z [nuget.org/downloads](https://nuget.org/downloads)i zapisywanie `.exe` do lokalizacji w ŚCIEŻCE.</span><span class="sxs-lookup"><span data-stu-id="94ad0-108">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="94ad0-109">Należy pamiętać, że pobieranie *jest* samo narzędzie, nie Instalatora.</span><span class="sxs-lookup"><span data-stu-id="94ad0-109">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="94ad0-110">Utworzenie odpowiedniego projektu Biblioteka klas programu .NET dla kodu, który ma być pakietu.</span><span class="sxs-lookup"><span data-stu-id="94ad0-110">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="94ad0-111">Jeśli nie masz już projekt, można utworzyć tylko jedna w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="94ad0-111">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="94ad0-112">W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, rozwiń węzeł **Visual C# > Windows** węzła, wybierz szablon "Biblioteki klas", nazwa projektu AppLogger i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="94ad0-112">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="94ad0-113">Kliknij prawym przyciskiem myszy na wynikowy plik projektu i wybierz **kompilacji** się upewnić, że projekt został utworzony prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="94ad0-113">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="94ad0-114">Biblioteki DLL znajduje się w folderze debugowania (lub wersji, jeśli zamiast tego kompilacji tej konfiguracji).</span><span class="sxs-lookup"><span data-stu-id="94ad0-114">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="94ad0-115">Oczywiście w rzeczywistym pakiecie NuGet, będzie wdrożenie wielu przydatnych funkcji, na których inne osoby mogą tworzyć aplikacje.</span><span class="sxs-lookup"><span data-stu-id="94ad0-115">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="94ad0-116">W ramach tego przewodnika jednak nie będzie pisania jakiegokolwiek dodatkowego kodu ponieważ biblioteki klas z szablonu jest wystarczające, aby utworzyć pakiet.</span><span class="sxs-lookup"><span data-stu-id="94ad0-116">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="94ad0-117">Utwórz plik manifestu pakietu .nuspec</span><span class="sxs-lookup"><span data-stu-id="94ad0-117">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="94ad0-118">Każdy pakiet NuGet musi manifestu&mdash; `.nuspec` pliku&mdash;do opisywania zawartością i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="94ad0-118">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="94ad0-119">`nuget spec` Polecenie tworzy plik dla Ciebie, którą można następnie dostosować.</span><span class="sxs-lookup"><span data-stu-id="94ad0-119">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="94ad0-120">W tym przykładzie utworzysz `.nuspec` z pliku projektu; można też utworzyć manifestu w inny sposób zgodnie z opisem na [Utwórz pakiet](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="94ad0-120">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="94ad0-121">Otwórz wiersz polecenia i przejdź do folderu zawierającego plik projektu (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="94ad0-121">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="94ad0-122">Uruchamianie interfejsu wiersza polecenia NuGet `spec` polecenie, aby wygenerować manifest, nosi nazwę po projektu, takie jak `AppLogger.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="94ad0-122">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="94ad0-123">Otwórz plik w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="94ad0-123">Open the file in a text editor.</span></span> <span data-ttu-id="94ad0-124">Manifest wygląda kod poniżej, gdzie tokenów w postaci `<token>` (takie jak `$id$`) są zastępowane podczas procesu tworzenia pakietów z wartościami z pliku Properties/AssemblyInfo.cs projektu.</span><span class="sxs-lookup"><span data-stu-id="94ad0-124">The manifest looks something like the code below, where tokens in the form `<token>` (such as `$id$`) are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="94ad0-125">Aby uzyskać więcej szczegółów na tokeny, zobacz [Tworzenie pliku .nuspec](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="94ad0-125">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
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
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="94ad0-126">Wybierz identyfikator pakietu, który jest unikatowy w całej nuget.org. Firma Microsoft zaleca używanie konwencji nazewnictwa opisanego w [utworzenie pakietu](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="94ad0-126">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="94ad0-127">Należy zaktualizować tagi autora oraz opis lub błąd pojawia się w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="94ad0-127">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="94ad0-128">Oto zaktualizowaną `.nuspec` pliku, na przykład:</span><span class="sxs-lookup"><span data-stu-id="94ad0-128">Here's an updated `.nuspec` file as an example:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="94ad0-129">Skompilowany dla publicznych zużycia pakietów, należy zwrócić szczególną uwagę na `<tags>` element, jak te znaczniki ułatwiała innym pakietu odnaleźć i zrozumieć, jakie operacje.</span><span class="sxs-lookup"><span data-stu-id="94ad0-129">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="94ad0-130">Uruchom polecenie pakietu</span><span class="sxs-lookup"><span data-stu-id="94ad0-130">Run the pack command</span></span>

<span data-ttu-id="94ad0-131">Aby utworzyć pakiet NuGet ( `.nupkg` plik) z projektem, uruchom `pack` polecenia:</span><span class="sxs-lookup"><span data-stu-id="94ad0-131">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```cli
nuget pack AppLogger.csproj
```

<span data-ttu-id="94ad0-132">To polecenie tworzy `AppLogger.1.0.0.0.nupkg` za pomocą numeru nazwę i wersję pakietu z `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="94ad0-132">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="94ad0-133">Polecenie wystawia ostrzeżenia, jeśli nie zostały zaktualizowane różnych pól w `.nuspec` pliku z wartościami domyślnymi.</span><span class="sxs-lookup"><span data-stu-id="94ad0-133">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="94ad0-134">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="94ad0-134">Publish the package</span></span>

<span data-ttu-id="94ad0-135">Po utworzeniu `.nupkg` pliku opublikowaniu go przy użyciu nuget.org `push` polecenia.</span><span class="sxs-lookup"><span data-stu-id="94ad0-135">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="94ad0-136">(Alternatywnie można użyć [nuget.org publikowania przepływu pracy](../create-packages/publish-a-package.md#publish-to-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="94ad0-136">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="94ad0-137">Pakiety, które publikowania nuget.org są publicznie widoczne dla innych deweloperów.</span><span class="sxs-lookup"><span data-stu-id="94ad0-137">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="94ad0-138">Do hostowania pakietów prywatnie, zobacz [Hosting pakiety](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="94ad0-138">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>

1. <span data-ttu-id="94ad0-139">Utwórz bezpłatne konto na [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), lub jeśli już istnieje.</span><span class="sxs-lookup"><span data-stu-id="94ad0-139">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="94ad0-140">Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="94ad0-140">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="94ad0-141">Aby przekazać pakiet, musisz potwierdzić konto.</span><span class="sxs-lookup"><span data-stu-id="94ad0-141">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="94ad0-142">Po zalogowaniu, wybierz nazwę użytkownika (w prawym górnym rogu), a następnie wybierz **klucze interfejsu API**.</span><span class="sxs-lookup"><span data-stu-id="94ad0-142">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="94ad0-143">Wybierz **Utwórz**, podaj nazwę klucza, wybierz **wybierz zakresy > Push** w obszarze **klucz interfejsu API**, wprowadź \* dla **wzorzec Glob**, następnie Wybierz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="94ad0-143">Select **Create**, provide a name for your key, select **Select Scopes > Push** under **API Key**, enter \* for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="94ad0-144">Po klucz zostanie utworzony, wybierz **kopiowania** można pobrać dostępu do klucza będziesz potrzebować na platformie interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="94ad0-144">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![Kopiowanie do Schowka klucz interfejsu API](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="94ad0-146">Zapisz klucz w bezpiecznej lokalizacji, a nie ujawniaj go.</span><span class="sxs-lookup"><span data-stu-id="94ad0-146">Save your key in a secure location and keep it secret.</span></span> <span data-ttu-id="94ad0-147">Jeśli klucz zostanie przypadkowo ujawniony, można go odtworzyć w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="94ad0-147">If your key is accidentally revealed, you can regenerate it at any time.</span></span> <span data-ttu-id="94ad0-148">Można również usunąć klucz interfejsu API, jeśli nie chcesz push pakietów za pomocą interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="94ad0-148">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="94ad0-149">W wierszu polecenia, uruchom następujące polecenie określając nazwę pakietu i zastępowanie klucza o wartości skopiowany w kroku 4:</span><span class="sxs-lookup"><span data-stu-id="94ad0-149">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="94ad0-150">nuget.exe wyświetla wyniki procesu publikowania:</span><span class="sxs-lookup"><span data-stu-id="94ad0-150">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="94ad0-151">Z profilu nuget.org, wybierz **Zarządzaj pakietami** można znaleźć w jednym opublikowana.</span><span class="sxs-lookup"><span data-stu-id="94ad0-151">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="94ad0-152">Otrzymasz również wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="94ad0-152">You also receive a confirmation email.</span></span> <span data-ttu-id="94ad0-153">Należy pamiętać, że może upłynąć trochę czasu pakietu indeksowane i wyświetlana w wynikach wyszukiwania, gdzie innym go znaleźć.</span><span class="sxs-lookup"><span data-stu-id="94ad0-153">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="94ad0-154">W tym czasie stronę pakietu zawiera następujący komunikat:</span><span class="sxs-lookup"><span data-stu-id="94ad0-154">During that time your package page shows the message below:</span></span>

    ![Ten pakiet nie ma jeszcze indeksowania.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="94ad0-157">**Skanowania antywirusowego**: wszystkie pakiety przekazane do nuget.org są skanowane pod kątem wirusów i odrzucone w przypadku znalezienia wirusy.</span><span class="sxs-lookup"><span data-stu-id="94ad0-157">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="94ad0-158">Wszystkie pakiety wymienione na nuget.org również są skanowane okresowo.</span><span class="sxs-lookup"><span data-stu-id="94ad0-158">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="94ad0-159">I to już wszystko!</span><span class="sxs-lookup"><span data-stu-id="94ad0-159">And that's it!</span></span> <span data-ttu-id="94ad0-160">Został właśnie opublikowany pakiet NuGet pierwszy [nuget.org](https://www.nuget.org/), który innych deweloperzy mogą używać w ich własnych projektów.</span><span class="sxs-lookup"><span data-stu-id="94ad0-160">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="94ad0-161">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="94ad0-161">Related topics</span></span>

- [<span data-ttu-id="94ad0-162">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="94ad0-162">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="94ad0-163">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="94ad0-163">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="94ad0-164">Obsługuje wiele platform docelowych</span><span class="sxs-lookup"><span data-stu-id="94ad0-164">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="94ad0-165">Przechowywanie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="94ad0-165">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="94ad0-166">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="94ad0-166">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
