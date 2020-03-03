---
title: Przekształcenia plików źródłowych i konfiguracji dla pakietów NuGet
description: Szczegółowe informacje o możliwości pakietów NuGet do przekształcania plików kodu źródłowego i konfiguracji (XML) po zainstalowaniu programu.
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 2fefd9cff4d151111023521c31d58878743775bf
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231178"
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="d9ace-103">Przekształcanie kodu źródłowego i plików konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d9ace-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="d9ace-104">**Przekształcenie kodu źródłowego** stosuje jednokierunkową wymianę tokenów w plikach w `content` lub `contentFiles` folderu (`content` dla klientów korzystających z `packages.config` i `contentFiles` dla `PackageReference`) podczas instalowania pakietu, gdzie tokeny odwołują się do [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9ace-104">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="d9ace-105">Dzięki temu można wstawić plik do przestrzeni nazw projektu lub dostosować kod, który zwykle przejdzie do `global.asax` w projekcie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d9ace-105">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="d9ace-106">**Przekształcenie pliku konfiguracji** pozwala modyfikować pliki, które już istnieją w projekcie docelowym, takie jak `web.config` i `app.config`.</span><span class="sxs-lookup"><span data-stu-id="d9ace-106">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="d9ace-107">Na przykład może być konieczne dodanie elementu do sekcji `modules` w pliku konfiguracyjnym.</span><span class="sxs-lookup"><span data-stu-id="d9ace-107">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="d9ace-108">Ta transformacja jest wykonywana przez dodanie plików specjalnych w pakiecie, które opisują sekcje dodawane do plików konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d9ace-108">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="d9ace-109">Po odinstalowaniu pakietu te same zmiany są odwracane, co sprawia, że jest to dwukierunkowa transformacja.</span><span class="sxs-lookup"><span data-stu-id="d9ace-109">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="d9ace-110">Określanie przekształceń kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="d9ace-110">Specifying source code transformations</span></span>

1. <span data-ttu-id="d9ace-111">Pliki, które mają zostać wstawione z pakietu do projektu, muszą znajdować się w folderach `content` i `contentFiles` pakietu.</span><span class="sxs-lookup"><span data-stu-id="d9ace-111">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="d9ace-112">Na przykład, jeśli plik o nazwie `ContosoData.cs` ma być zainstalowany w folderze `Models` projektu docelowego, musi znajdować się wewnątrz folderów `content\Models` i `contentFiles\{lang}\{tfm}\Models` w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="d9ace-112">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="d9ace-113">Aby polecić pakietowi NuGet zastosowanie zastąpienia tokenu podczas instalacji, należy dołączyć `.pp` do nazwy pliku kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="d9ace-113">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="d9ace-114">Po instalacji plik nie będzie miał rozszerzenia `.pp`.</span><span class="sxs-lookup"><span data-stu-id="d9ace-114">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="d9ace-115">Na przykład aby wykonać przekształcenia w `ContosoData.cs`, Nazwij plik w `ContosoData.cs.pp`pakietu.</span><span class="sxs-lookup"><span data-stu-id="d9ace-115">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="d9ace-116">Po zakończeniu instalacji zostanie wyświetlona jako `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="d9ace-116">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="d9ace-117">W pliku kodu źródłowego Użyj tokenów bez uwzględniania wielkości liter w formularzu `$token$`, aby wskazać wartości, które NuGet powinny zastąpić właściwości projektu:</span><span class="sxs-lookup"><span data-stu-id="d9ace-117">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="d9ace-118">Podczas instalacji pakiet NuGet zastępuje `$rootnamespace$` z `Fabrikam` przy założeniu, że docelowy obszar nazw jest `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="d9ace-118">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="d9ace-119">Token `$rootnamespace$` jest najczęściej używaną właściwością projektu; wszystkie inne są wyświetlane we [właściwościach projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="d9ace-119">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="d9ace-120">Oczywiście należy mieć na uwadze, że niektóre właściwości mogą być specyficzne dla typu projektu.</span><span class="sxs-lookup"><span data-stu-id="d9ace-120">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="d9ace-121">Określanie przekształceń pliku konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d9ace-121">Specifying config file transformations</span></span>

<span data-ttu-id="d9ace-122">Zgodnie z opisem w poniższych sekcjach przekształcenia plików konfiguracji można wykonać na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="d9ace-122">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="d9ace-123">Dołącz pliki `app.config.transform` i `web.config.transform` do folderu `content` pakietu, gdzie rozszerzenie `.transform` informuje program NuGet, że te pliki zawierają kod XML do scalenia z istniejącymi plikami konfiguracji podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="d9ace-123">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="d9ace-124">Po odinstalowaniu pakietu ten sam plik XML jest usuwany.</span><span class="sxs-lookup"><span data-stu-id="d9ace-124">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="d9ace-125">Uwzględnij pliki `app.config.install.xdt` i `web.config.install.xdt` w folderze `content` pakietu, używając [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx) do opisania żądanych zmian.</span><span class="sxs-lookup"><span data-stu-id="d9ace-125">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="d9ace-126">Za pomocą tej opcji można również dołączyć plik `.uninstall.xdt`, aby cofnąć zmiany po usunięciu pakietu z projektu.</span><span class="sxs-lookup"><span data-stu-id="d9ace-126">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="d9ace-127">Przekształcenia nie są stosowane do `.config` plików, do których odwołuje się łącze w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9ace-127">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="d9ace-128">Zaletą korzystania z XDT jest to, że zamiast bezpośredniego scalania dwóch plików statycznych, zapewnia ona składnię do manipulowania strukturą kodu XML, przy użyciu elementów i atrybutów dopasowywania za pomocą pełnej obsługi XPath.</span><span class="sxs-lookup"><span data-stu-id="d9ace-128">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="d9ace-129">XDT może następnie dodawać, aktualizować lub usuwać elementy, umieszczać nowe elementy w określonej lokalizacji lub zastępować/usuwać elementy (w tym węzłów podrzędnych).</span><span class="sxs-lookup"><span data-stu-id="d9ace-129">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="d9ace-130">Pozwala to na bezpośrednie utworzenie transformacji, które wycofa wszystkie przekształcenia wykonywane podczas instalacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="d9ace-130">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="d9ace-131">Przekształcenia XML</span><span class="sxs-lookup"><span data-stu-id="d9ace-131">XML transforms</span></span>

<span data-ttu-id="d9ace-132">`app.config.transform` i `web.config.transform` w folderze `content` pakietu zawierają tylko te elementy, które mają być scalane do istniejących plików `app.config` i `web.config` projektu.</span><span class="sxs-lookup"><span data-stu-id="d9ace-132">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="d9ace-133">Załóżmy na przykład, że projekt początkowo zawiera następującą zawartość w `web.config`:</span><span class="sxs-lookup"><span data-stu-id="d9ace-133">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="d9ace-134">Aby dodać `MyNuModule` element do sekcji `modules` podczas instalowania pakietu, Utwórz plik `web.config.transform` w folderze `content` pakietu, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="d9ace-134">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="d9ace-135">Po zainstalowaniu pakietu NuGet pakiet `web.config` będzie wyglądać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d9ace-135">After NuGet installs the package, `web.config` will appear as follows:</span></span>

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

<span data-ttu-id="d9ace-136">Zwróć uwagę, że plik NuGet nie zastąpił sekcji `modules`, po prostu scalał do niego nowy wpis poprzez dodanie tylko nowych elementów i atrybutów.</span><span class="sxs-lookup"><span data-stu-id="d9ace-136">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="d9ace-137">Pakiet NuGet nie zmieni żadnych istniejących elementów ani atrybutów.</span><span class="sxs-lookup"><span data-stu-id="d9ace-137">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="d9ace-138">Po odinstalowaniu pakietu NuGet ponownie sprawdzi `.transform` pliki i usunie zawarte w nim elementy z odpowiednich `.config` plików.</span><span class="sxs-lookup"><span data-stu-id="d9ace-138">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="d9ace-139">Należy zauważyć, że ten proces nie wpłynie na żadne wiersze w `.config` pliku modyfikowanym po zainstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="d9ace-139">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="d9ace-140">W szerszym przykładzie [moduły rejestrowania błędów modułów i programów obsługi dla pakietu ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) dodają wiele wpisów do `web.config`, które są ponownie usuwane po odinstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="d9ace-140">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="d9ace-141">Aby przejrzeć plik `web.config.transform`, Pobierz pakiet ELMAH z powyższego linku, Zmień rozszerzenie pakietu z `.nupkg` na `.zip`, a następnie otwórz `content\web.config.transform` w tym pliku ZIP.</span><span class="sxs-lookup"><span data-stu-id="d9ace-141">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="d9ace-142">Aby zobaczyć efekt instalacji i dezinstalacji pakietu, Utwórz nowy projekt ASP.NET w programie Visual Studio (szablon jest w obszarze  **C# Visual > Web** w oknie dialogowym Nowy projekt) i wybierz Pustą aplikację ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d9ace-142">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="d9ace-143">Otwórz `web.config`, aby zobaczyć jego stan początkowy.</span><span class="sxs-lookup"><span data-stu-id="d9ace-143">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="d9ace-144">Następnie kliknij prawym przyciskiem myszy projekt, wybierz pozycję **Zarządzaj pakietami NuGet**, Wyszukaj pozycję ELMAH w witrynie NuGet.org i zainstaluj najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="d9ace-144">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="d9ace-145">Zwróć uwagę na wszystkie zmiany `web.config`.</span><span class="sxs-lookup"><span data-stu-id="d9ace-145">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="d9ace-146">Teraz Odinstaluj pakiet i zobaczysz, że `web.config` powrócić do poprzedniego stanu.</span><span class="sxs-lookup"><span data-stu-id="d9ace-146">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="d9ace-147">Przekształcenia XDT</span><span class="sxs-lookup"><span data-stu-id="d9ace-147">XDT transforms</span></span>

> [!Note]
> <span data-ttu-id="d9ace-148">Jak wspomniano w [sekcji problemy ze zgodnością pakietu w dokumentacji dotyczącej migrowania z `packages.config` do `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), przekształcenia XDT zgodnie z poniższym opisem są obsługiwane tylko przez `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="d9ace-148">As mentioned in the [package compatibility issues section of the docs for migrating from `packages.config` to `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), XDT transformations as described below are only supported by `packages.config`.</span></span> <span data-ttu-id="d9ace-149">Jeśli dodasz poniższe pliki do pakietu, użytkownicy korzystający z pakietu z `PackageReference` nie będą mieć zastosowanych przekształceń (zobacz [ten przykład](https://github.com/NuGet/Samples/tree/master/XDTransformExample) , aby XDT transformacje pracy z`PackageReference`).</span><span class="sxs-lookup"><span data-stu-id="d9ace-149">If you add the below files to your package, consumers using your package with `PackageReference` will not have the transformations applied (refer to [this sample](https://github.com/NuGet/Samples/tree/master/XDTransformExample) to make XDT transforms work with`PackageReference`).</span></span>

<span data-ttu-id="d9ace-150">Pliki konfiguracji można modyfikować przy użyciu [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9ace-150">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="d9ace-151">Możesz również mieć tokeny zamieniania NuGet na [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) , dołączając nazwę właściwości w ramach ograniczników `$` (bez uwzględniania wielkości liter).</span><span class="sxs-lookup"><span data-stu-id="d9ace-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimiters (case-insensitive).</span></span>

<span data-ttu-id="d9ace-152">Na przykład następujący plik `app.config.install.xdt` spowoduje wstawienie elementu `appSettings` do `app.config` zawierającego wartości `FullPath`, `FileName`i `ActiveConfigurationSettings` z projektu:</span><span class="sxs-lookup"><span data-stu-id="d9ace-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="d9ace-153">W innym przykładzie Załóżmy, że projekt początkowo zawiera następującą zawartość w `web.config`:</span><span class="sxs-lookup"><span data-stu-id="d9ace-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="d9ace-154">Aby dodać `MyNuModule` element do sekcji `modules` podczas instalowania pakietu, `web.config.install.xdt` pakietu będzie zawierać następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d9ace-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="d9ace-155">Po zainstalowaniu pakietu `web.config` będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="d9ace-155">After installing the package, `web.config` will look like this:</span></span>

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

<span data-ttu-id="d9ace-156">Aby usunąć tylko `MyNuModule` element podczas odinstalowywania pakietu, plik `web.config.uninstall.xdt` powinien zawierać następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d9ace-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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
