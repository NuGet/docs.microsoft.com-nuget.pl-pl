---
title: Przekształcenia pliku źródłowego i konfiguracji dla pakietów NuGet
description: Szczegóły możliwości pakietów NuGet do przekształcania kodu źródłowego i konfiguracji plików (XML) podczas instalacji.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 863bf22780313a34690617dd6a1604531272808b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="63fa5-103">Przekształcanie plików źródłowych kodem i konfiguracją</span><span class="sxs-lookup"><span data-stu-id="63fa5-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="63fa5-104">Dla projektów przy użyciu `packages.config`NuGet obsługuje możliwość przekształcenia do kodu źródłowego i plików konfiguracji w pakiecie instalowania i odinstalowywania razy.</span><span class="sxs-lookup"><span data-stu-id="63fa5-104">For projects using `packages.config`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span> <span data-ttu-id="63fa5-105">Tylko źródła kodu przekształceń są stosowane, gdy pakiet jest zainstalowany w projekcie przy użyciu [PackageReference](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="63fa5-105">Only Source code transformations are applied when a package is installed in a project using [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span>

<span data-ttu-id="63fa5-106">A **źródła kodu transformacji** jednokierunkowe zastępujący tokenu jest stosowana do plików w pakiecie `content` lub `contentFiles` folder (`content` dla klientów korzystających z `packages.config` i `contentFiles` dla `PackageReference`) po zainstalowaniu pakietu, gdy tokeny odnoszą się do programu Visual Studio [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="63fa5-106">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="63fa5-107">Dzięki temu można wstawić plik do projektu przestrzeni nazw lub Dostosuj kod, który zazwyczaj przejdzie do `global.asax` w projekcie programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="63fa5-107">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="63fa5-108">A **transformacji pliku config** umożliwia modyfikowanie plików, które już istnieją w projekcie docelowym, takich jak `web.config` i `app.config`.</span><span class="sxs-lookup"><span data-stu-id="63fa5-108">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="63fa5-109">Na przykład pakiet może być konieczne dodanie elementu `modules` sekcji w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="63fa5-109">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="63fa5-110">Ta transformacja odbywa się przy tym specjalne pliki w pakiecie, który opisano sekcjach, aby dodać do plików konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="63fa5-110">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="63fa5-111">Po odinstalowaniu pakietu te same zmiany są następnie wycofać, co to dwukierunkowe przekształcania.</span><span class="sxs-lookup"><span data-stu-id="63fa5-111">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="63fa5-112">Określanie przekształcenia kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="63fa5-112">Specifying source code transformations</span></span>

1. <span data-ttu-id="63fa5-113">Pliki, które ma zostać wstawiony z pakietu w projekcie musi znajdować się w pakiecie `content` i `contentFiles` folderów.</span><span class="sxs-lookup"><span data-stu-id="63fa5-113">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="63fa5-114">Na przykład, jeśli chcesz, aby plik o nazwie `ContosoData.cs` ma być zainstalowany w `Models` folder docelowy projekt, musi znajdować się wewnątrz `content\Models` i `contentFiles\{lang}\{tfm}\Models` folderów w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="63fa5-114">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="63fa5-115">Aby nakazać NuGet, aby zastosować zastępujący tokenu w czasie instalacji, należy dołączyć `.pp` nazwy pliku kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="63fa5-115">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="63fa5-116">Po zakończeniu instalacji, nie ma pliku `.pp` rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="63fa5-116">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="63fa5-117">Na przykład, aby dokonać przekształcenia w `ContosoData.cs`, nazwa pliku w pakiecie `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="63fa5-117">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="63fa5-118">Po zakończeniu instalacji zostanie wyświetlony jako `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="63fa5-118">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="63fa5-119">W pliku kodu źródłowego za pomocą tokenów bez uwzględniania wielkości liter w postaci `$token$` wartości tego NuGet należy zastąpić właściwości projektu:</span><span class="sxs-lookup"><span data-stu-id="63fa5-119">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="63fa5-120">Podczas instalacji, zastępuje NuGet `$rootnamespace$` z `Fabrikam` przy założeniu projektu docelowego obiektu, którego przestrzeń nazw głównego `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="63fa5-120">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="63fa5-121">`$rootnamespace$` Token jest właściwość projektu najczęściej używane; pozostałe są wymienione w [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="63fa5-121">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="63fa5-122">Można, mając na uwadze, że niektóre właściwości mogą być specyficzne dla typu projektu.</span><span class="sxs-lookup"><span data-stu-id="63fa5-122">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="63fa5-123">Określenie konfiguracji pliku przekształcenia</span><span class="sxs-lookup"><span data-stu-id="63fa5-123">Specifying config file transformations</span></span>

<span data-ttu-id="63fa5-124">Zgodnie z opisem w poniższych sekcjach, przekształcenia pliku konfiguracji można zrobić na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="63fa5-124">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="63fa5-125">Obejmują `app.config.transform` i `web.config.transform` plików do pakietu `content` folder, gdzie `.transform` rozszerzenie informuje NuGet, że te pliki zawierają XML do scalenia z istniejących plików konfiguracji, gdy pakiet jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="63fa5-125">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="63fa5-126">Po odinstalowaniu pakietu tego samego XML zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="63fa5-126">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="63fa5-127">Obejmują `app.config.install.xdt` i `web.config.install.xdt` plików do pakietu `content` folderu, za pomocą [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx) do opisywania żądane zmiany.</span><span class="sxs-lookup"><span data-stu-id="63fa5-127">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="63fa5-128">Po wybraniu tej opcji możesz również uwzględnić `.uninstall.xdt` plik, aby cofnąć zmiany, gdy pakiet zostanie usunięty z projektu.</span><span class="sxs-lookup"><span data-stu-id="63fa5-128">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="63fa5-129">Przekształcenia nie są stosowane do `.config` plików jako łącze w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="63fa5-129">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="63fa5-130">Zaletą używania XDT to, że zamiast po prostu scalanie dwa pliki statyczne, zawiera składnię do manipulowania struktury XML DOM przy użyciu element i atrybut dopasowania za pomocą pełną obsługę języka XPath.</span><span class="sxs-lookup"><span data-stu-id="63fa5-130">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="63fa5-131">XDT można następnie dodać, zaktualizować, lub usuń elementy, umieść nowe elementy z określonej lokalizacji lub Zamień lub usuń elementy (łącznie z węzłami podrzędnymi).</span><span class="sxs-lookup"><span data-stu-id="63fa5-131">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="63fa5-132">Dzięki temu prostego do utworzenia transformacji Odinstaluj, które Wycofaj wszystkie przekształcenia zrobić podczas instalacji pakietu aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="63fa5-132">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="63fa5-133">Transformacji XML</span><span class="sxs-lookup"><span data-stu-id="63fa5-133">XML transforms</span></span>

<span data-ttu-id="63fa5-134">`app.config.transform` i `web.config.transform` w pakiecie `content` folder zawiera tylko elementy do scalenia istniejącego projektu `app.config` i `web.config` plików.</span><span class="sxs-lookup"><span data-stu-id="63fa5-134">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="63fa5-135">Na przykład załóżmy, że projekt zawiera początkowo następującą zawartość w `web.config`:</span><span class="sxs-lookup"><span data-stu-id="63fa5-135">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="63fa5-136">Aby dodać `MyNuModule` elementu `modules` sekcji podczas instalacji, Utwórz `web.config.transform` pliku do pakietu `content` folderu, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="63fa5-136">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="63fa5-137">Po zainstalowaniu pakietu NuGet `web.config` będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="63fa5-137">After NuGet installs the package, `web.config` will appear as follows:</span></span>

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

<span data-ttu-id="63fa5-138">Należy zauważyć, że nie Zastąp NuGet `modules` sekcji go po prostu połączone nowy wpis do niej przez dodanie tylko nowych elementów i atrybutów.</span><span class="sxs-lookup"><span data-stu-id="63fa5-138">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="63fa5-139">NuGet nie zmieni się żadnych istniejących elementów lub atrybutów.</span><span class="sxs-lookup"><span data-stu-id="63fa5-139">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="63fa5-140">Po odinstalowaniu pakietu NuGet zbada `.transform` ponownie pliki i usuwanie elementów zawiera odpowiednie `.config` plików.</span><span class="sxs-lookup"><span data-stu-id="63fa5-140">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="63fa5-141">Należy pamiętać, że ten proces nie wpłynie na wszystkie wiersze w `.config` pliku, który można modyfikować po zainstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="63fa5-141">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="63fa5-142">Przykład szerszej [moduły rejestrowania błędów i programy obsługi dla platformy ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) pakiet dodaje wiele wpisów w `web.config`, które są ponownie usunięte po odinstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="63fa5-142">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="63fa5-143">Do sprawdzenia jego `web.config.transform` plik, Pobierz pakiet ELMAH z powyższego łącza, zmień rozszerzenie pakietu z `.nupkg` do `.zip`, a następnie otwórz `content\web.config.transform` w tym pliku ZIP.</span><span class="sxs-lookup"><span data-stu-id="63fa5-143">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="63fa5-144">Aby zobaczyć efekt Instalowanie i odinstalowanie pakietu, należy utworzyć nowy projekt ASP.NET w programie Visual Studio (szablon podlega **Visual C# > sieci Web** w oknie dialogowym Nowy projekt) i wybierz opcję Pusta aplikacja platformy ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="63fa5-144">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="63fa5-145">Otwórz `web.config` aby zobaczyć stan początkowy.</span><span class="sxs-lookup"><span data-stu-id="63fa5-145">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="63fa5-146">Kliknij prawym przyciskiem myszy projekt, wybierz **Zarządzaj pakietami NuGet**Przeglądaj w poszukiwaniu ELMAH na nuget.org i zainstaluj najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="63fa5-146">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="63fa5-147">Zwróć uwagę, wszystkie zmiany do `web.config`.</span><span class="sxs-lookup"><span data-stu-id="63fa5-147">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="63fa5-148">Teraz odinstalować pakiet, aby zobaczyć `web.config` powrócić do poprzedniego stanu.</span><span class="sxs-lookup"><span data-stu-id="63fa5-148">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="63fa5-149">Przekształca XDT</span><span class="sxs-lookup"><span data-stu-id="63fa5-149">XDT transforms</span></span>

<span data-ttu-id="63fa5-150">Można zmodyfikować plików konfiguracji przy użyciu [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="63fa5-150">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="63fa5-151">Może także zawierać NuGet Zastąp tokeny z [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) przez dołączenie nazwy właściwości w `$` ograniczników (bez uwzględniania wielkości liter).</span><span class="sxs-lookup"><span data-stu-id="63fa5-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimeters (case-insensitive).</span></span>

<span data-ttu-id="63fa5-152">Na przykład następująca `app.config.install.xdt` pliku zostanie wstawiona `appSettings` element do `app.config` zawierający `FullPath`, `FileName`, i `ActiveConfigurationSettings` wartości z projektu:</span><span class="sxs-lookup"><span data-stu-id="63fa5-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="63fa5-153">Innym przykładem Załóżmy, że projekt zawiera początkowo następującą zawartość w `web.config`:</span><span class="sxs-lookup"><span data-stu-id="63fa5-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="63fa5-154">Aby dodać `MyNuModule` elementu `modules` sekcji podczas pakietu instalacji pakietu `web.config.install.xdt` będzie zawierał następujące:</span><span class="sxs-lookup"><span data-stu-id="63fa5-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="63fa5-155">Po zainstalowaniu pakietu, `web.config` będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="63fa5-155">After installing the package, `web.config` will look like this:</span></span>

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

<span data-ttu-id="63fa5-156">Aby usunąć tylko `MyNuModule` elementu podczas odinstalowywania pakietu `web.config.uninstall.xdt` plik powinien zawierać następujące:</span><span class="sxs-lookup"><span data-stu-id="63fa5-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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
