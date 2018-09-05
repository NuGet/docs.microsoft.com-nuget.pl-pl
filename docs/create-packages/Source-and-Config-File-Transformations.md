---
title: Przekształcenia pliku źródłowego i konfiguracji dla pakietów NuGet
description: Szczegółowe informacje na możliwość pakiety NuGet umożliwiające przekształcanie kodu źródłowego i konfiguracji plików (XML), podczas instalacji.
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: c2cd61b692b80cdc45fce399483cda3b57d12e5e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547688"
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="323a7-103">Przekształcanie plików źródłowych kodu i konfiguracji</span><span class="sxs-lookup"><span data-stu-id="323a7-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="323a7-104">Dla projektów przy użyciu `packages.config`NuGet obsługuje możliwość przekształcenia do kodu źródłowego i plików konfiguracji w pakiecie instalowania i odinstalowywania razy.</span><span class="sxs-lookup"><span data-stu-id="323a7-104">For projects using `packages.config`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span> <span data-ttu-id="323a7-105">Tylko przekształceń kodu źródłowego są stosowane, gdy pakiet jest zainstalowany w projekcie za pomocą [PackageReference](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="323a7-105">Only Source code transformations are applied when a package is installed in a project using [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span>

<span data-ttu-id="323a7-106">A **źródła kodu transformacji** jednokierunkowe zastępowania tokenu jest stosowana do plików w pakiecie `content` lub `contentFiles` folder (`content` dla klientów korzystających z `packages.config` i `contentFiles` dla `PackageReference`) po zainstalowaniu pakietu, gdy tokeny odnoszą się do programu Visual Studio [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="323a7-106">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="323a7-107">Dzięki temu można wstawić plik do projektu przestrzeni nazw lub dostosować program code, zwykle będą przekazywane do `global.asax` w projektach programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="323a7-107">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="323a7-108">A **transformacji pliku config** umożliwia modyfikowanie plików, które już istnieją w docelowej projektu, taki jak `web.config` i `app.config`.</span><span class="sxs-lookup"><span data-stu-id="323a7-108">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="323a7-109">Na przykład pakiet może być konieczne dodanie elementu do `modules` sekcji w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="323a7-109">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="323a7-110">Ta transformacja odbywa się przy tym specjalnych plików w pakiecie, który opisano w sekcjach, aby dodać do plików konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="323a7-110">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="323a7-111">Gdy pakiet zostanie odinstalowany, te same zmiany są następnie wycofać, zastosowania dwukierunkowe transformacji.</span><span class="sxs-lookup"><span data-stu-id="323a7-111">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="323a7-112">Określanie przekształceń kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="323a7-112">Specifying source code transformations</span></span>

1. <span data-ttu-id="323a7-113">Pliki, które ma zostać wstawiony z pakietu do projektu muszą znajdować się w ramach pakietu `content` i `contentFiles` folderów.</span><span class="sxs-lookup"><span data-stu-id="323a7-113">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="323a7-114">Na przykład, jeśli chcesz, aby plik o nazwie `ContosoData.cs` ma być zainstalowany w `Models` folder docelowy projekt, należy go wewnątrz `content\Models` i `contentFiles\{lang}\{tfm}\Models` folderów w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="323a7-114">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="323a7-115">Aby nakazać pakietu NuGet, aby zastosować zastępowania tokenu w czasie instalacji, należy dołączyć `.pp` do nazwy pliku kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="323a7-115">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="323a7-116">Po zakończeniu instalacji, plik nie będzie miał `.pp` rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="323a7-116">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="323a7-117">Na przykład, aby wprowadzić przekształcenia w `ContosoData.cs`, nazwę pliku w pakiecie `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="323a7-117">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="323a7-118">Po zakończeniu instalacji zostanie wyświetlony jako `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="323a7-118">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="323a7-119">W pliku kodu źródłowego, należy użyć tokenów bez uwzględniania wielkości liter w postaci `$token$` do wskazywania wartości tego NuGet należy zastąpić właściwości projektu:</span><span class="sxs-lookup"><span data-stu-id="323a7-119">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    <span data-ttu-id="323a7-120">Po instalacji, zastępuje NuGet `$rootnamespace$` z `Fabrikam` zakładając, że projekt docelowy użytkownika, którego główna przestrzeń nazw jest `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="323a7-120">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="323a7-121">`$rootnamespace$` Token jest właściwość projektu najczęściej używanych; wszystkie inne są wymienione w [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="323a7-121">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="323a7-122">Można je na uwadze, oczywiście, że niektóre właściwości mogą być specyficzne dla typu projektu.</span><span class="sxs-lookup"><span data-stu-id="323a7-122">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="323a7-123">Określanie przekształcenia pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="323a7-123">Specifying config file transformations</span></span>

<span data-ttu-id="323a7-124">Zgodnie z opisem w kolejnych sekcjach, przekształcenia pliku konfiguracji można zrobić na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="323a7-124">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="323a7-125">Obejmują `app.config.transform` i `web.config.transform` pliki do pakietu `content` folderu, gdzie `.transform` rozszerzenie informuje NuGet, że te pliki zawierają kod XML w celu scalenia z istniejącymi plikami konfiguracji, gdy pakiet jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="323a7-125">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="323a7-126">Po odinstalowaniu pakietu tego samego XML jest usuwany.</span><span class="sxs-lookup"><span data-stu-id="323a7-126">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="323a7-127">Obejmują `app.config.install.xdt` i `web.config.install.xdt` pliki do pakietu `content` folderze przy użyciu [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx) do opisania żądane zmiany.</span><span class="sxs-lookup"><span data-stu-id="323a7-127">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="323a7-128">Po wybraniu tej opcji możesz również uwzględnić `.uninstall.xdt` plik, aby cofnąć zmiany, gdy pakiet zostanie usunięty z projektu.</span><span class="sxs-lookup"><span data-stu-id="323a7-128">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="323a7-129">Przekształcenia nie są stosowane do `.config` pliki określany jako link w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="323a7-129">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="323a7-130">Zaletą używania XDT jest zamiast po prostu scalanie dwa pliki statyczne, składni do manipulowania strukturę modelu DOM języka XML przy użyciu element i atrybut dopasowania, dzięki pełnej obsłudze XPath.</span><span class="sxs-lookup"><span data-stu-id="323a7-130">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="323a7-131">XDT można następnie dodać, zaktualizować, lub usuń elementy, umieszczać nowe elementy w określonej lokalizacji lub Zamień lub usuń elementy (łącznie z węzłów podrzędnych).</span><span class="sxs-lookup"><span data-stu-id="323a7-131">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="323a7-132">Dzięki temu prosta do utworzenia Odinstaluj przekształceń, które wycofać wszystkie przekształcenia zrobić podczas instalacji pakietu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="323a7-132">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="323a7-133">Transformacje XML</span><span class="sxs-lookup"><span data-stu-id="323a7-133">XML transforms</span></span>

<span data-ttu-id="323a7-134">`app.config.transform` i `web.config.transform` w pakiecie `content` folder zawierają tylko te elementy, aby scalić istniejący projekt `app.config` i `web.config` plików.</span><span class="sxs-lookup"><span data-stu-id="323a7-134">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="323a7-135">Na przykład załóżmy, że projekt zawiera początkowo następującą zawartość w `web.config`:</span><span class="sxs-lookup"><span data-stu-id="323a7-135">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="323a7-136">Aby dodać `MyNuModule` elementu `modules` sekcji podczas instalowania pakietu, należy utworzyć `web.config.transform` pliku do pakietu `content` folder, który wygląda w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="323a7-136">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="323a7-137">Po NuGet instaluje pakiet `web.config` pojawi się w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="323a7-137">After NuGet installs the package, `web.config` will appear as follows:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="323a7-138">Należy zauważyć, że nie zastąpić NuGet `modules` sekcji ją po prostu połączone nowy wpis do niego przez dodanie tylko nowych elementów i atrybutów.</span><span class="sxs-lookup"><span data-stu-id="323a7-138">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="323a7-139">NuGet nie ulegnie zmianie, wszystkie istniejące elementy lub atrybuty.</span><span class="sxs-lookup"><span data-stu-id="323a7-139">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="323a7-140">Po odinstalowaniu pakietu NuGet zbada `.transform` pliki ponownie i usuwania elementów zawiera odpowiednie `.config` plików.</span><span class="sxs-lookup"><span data-stu-id="323a7-140">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="323a7-141">Należy pamiętać, że ten proces nie wpłynie na wszystkie wiersze w `.config` pliku, który modyfikujesz po zakończeniu instalacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="323a7-141">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="323a7-142">Przykład bardziej rozległe [moduły rejestrowania błędów i obsługi platformy ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) pakiet dodaje wiele wpisów w `web.config`, które ponownie zostały usunięte po odinstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="323a7-142">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="323a7-143">Zbadanie jego `web.config.transform` plik, Pobierz pakiet ELMAH spod linku powyżej, zmień rozszerzenie pakietu z `.nupkg` do `.zip`, a następnie otwórz `content\web.config.transform` w tym pliku ZIP.</span><span class="sxs-lookup"><span data-stu-id="323a7-143">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="323a7-144">Aby zobaczyć efekt Instalowanie i odinstalowywanie pakietu, Utwórz nowy projekt ASP.NET w programie Visual Studio (szablon znajduje się w **Visual C# > sieci Web** w oknie dialogowym Nowy projekt) i wybierz pozycję pusta aplikacja platformy ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="323a7-144">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="323a7-145">Otwórz `web.config` Aby wyświetlić jego stan początkowy.</span><span class="sxs-lookup"><span data-stu-id="323a7-145">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="323a7-146">Kliknij prawym przyciskiem myszy projekt, wybierz **Zarządzaj pakietami NuGet**, Przeglądaj w poszukiwaniu biblioteki ELMAH w witrynie nuget.org i zainstaluj najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="323a7-146">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="323a7-147">Zwróć uwagę, wszystkie zmiany do `web.config`.</span><span class="sxs-lookup"><span data-stu-id="323a7-147">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="323a7-148">Teraz odinstalować pakiet i zostanie wyświetlony `web.config` powrócić do poprzedniego stanu.</span><span class="sxs-lookup"><span data-stu-id="323a7-148">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="323a7-149">Przekształca XDT</span><span class="sxs-lookup"><span data-stu-id="323a7-149">XDT transforms</span></span>

<span data-ttu-id="323a7-150">Można zmodyfikować plików konfiguracji przy użyciu [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="323a7-150">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="323a7-151">Mogą też istnieć NuGet zamienić tokeny przy użyciu [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) , łącznie z nazwą właściwości w ramach `$` ograniczników (bez uwzględniania wielkości liter).</span><span class="sxs-lookup"><span data-stu-id="323a7-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimeters (case-insensitive).</span></span>

<span data-ttu-id="323a7-152">Na przykład następująca `app.config.install.xdt` pliku zostanie wstawiona `appSettings` elementu do `app.config` zawierający `FullPath`, `FileName`, i `ActiveConfigurationSettings` wartości z projektu:</span><span class="sxs-lookup"><span data-stu-id="323a7-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

<span data-ttu-id="323a7-153">Inny przykład, załóżmy, że projekt zawiera początkowo następującą zawartość w `web.config`:</span><span class="sxs-lookup"><span data-stu-id="323a7-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="323a7-154">Aby dodać `MyNuModule` elementu `modules` sekcji podczas pakietu instalacji pakietu `web.config.install.xdt` będzie zawierał następujące:</span><span class="sxs-lookup"><span data-stu-id="323a7-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="323a7-155">Po zainstalowaniu pakietu, `web.config` będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="323a7-155">After installing the package, `web.config` will look like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="323a7-156">Aby usunąć tylko `MyNuModule` elementu podczas odinstalowywania pakietu `web.config.uninstall.xdt` plik powinien zawierać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="323a7-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
