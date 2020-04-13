---
title: Transformacje plików źródłowych i konfiguracyjnych dla pakietów NuGet
description: Szczegółowe informacje na temat możliwości pakietów NuGet do przekształcania plików kodu źródłowego i konfiguracji (XML) po zainstalowaniu.
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 2fefd9cff4d151111023521c31d58878743775bf
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231178"
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="6259c-103">Przekształcanie kodu źródłowego i plików konfiguracyjnych</span><span class="sxs-lookup"><span data-stu-id="6259c-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="6259c-104">**Transformacja kodu źródłowego** stosuje jednokierunkowe zastępowanie tokenów `contentFiles` do`content` plików `packages.config` w `contentFiles` `PackageReference`pakiecie `content` lub folderze (dla klientów korzystających i dla) po zainstalowaniu pakietu, gdzie tokeny odnoszą się do [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6259c-104">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="6259c-105">Dzięki temu można wstawić plik do obszaru nazw projektu lub dostosować kod, `global.asax` który zazwyczaj wchodzi w ASP.NET projektu.</span><span class="sxs-lookup"><span data-stu-id="6259c-105">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="6259c-106">**Transformacja pliku konfiguracyjnego** umożliwia modyfikowanie plików, które `web.config` już `app.config`istnieją w projekcie docelowym, takich jak i .</span><span class="sxs-lookup"><span data-stu-id="6259c-106">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="6259c-107">Na przykład pakiet może być konieczne dodanie `modules` elementu do sekcji w pliku konfiguracyjnym.</span><span class="sxs-lookup"><span data-stu-id="6259c-107">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="6259c-108">Transformacja ta odbywa się poprzez dołączenie specjalnych plików w pakiecie, które opisują sekcje, aby dodać do plików konfiguracyjnych.</span><span class="sxs-lookup"><span data-stu-id="6259c-108">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="6259c-109">Po odinstalowaniu pakietu te same zmiany są następnie odwracane, co czyni to transformacją dwukierunkową.</span><span class="sxs-lookup"><span data-stu-id="6259c-109">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="6259c-110">Określanie przekształceń kodu źródłowego</span><span class="sxs-lookup"><span data-stu-id="6259c-110">Specifying source code transformations</span></span>

1. <span data-ttu-id="6259c-111">Pliki, które chcesz wstawić z pakietu do projektu, muszą `content` `contentFiles` znajdować się w folderach i folderach pakietu.</span><span class="sxs-lookup"><span data-stu-id="6259c-111">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="6259c-112">Na przykład jeśli chcesz, `ContosoData.cs` aby plik wywoływany, który ma być zainstalowany w folderze `Models` projektu docelowego, musi znajdować się wewnątrz `content\Models` folderów i `contentFiles\{lang}\{tfm}\Models` w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="6259c-112">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="6259c-113">Aby poinstruować NuGet, aby zastosować zastąpienie `.pp` tokenu w czasie instalacji, dołącz do nazwy pliku kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="6259c-113">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="6259c-114">Po instalacji plik nie `.pp` będzie miał rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="6259c-114">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="6259c-115">Na przykład, aby dokonać `ContosoData.cs`przekształceń w `ContosoData.cs.pp`programie , nazwij plik w pakiecie .</span><span class="sxs-lookup"><span data-stu-id="6259c-115">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="6259c-116">Po instalacji pojawi `ContosoData.cs`się jako .</span><span class="sxs-lookup"><span data-stu-id="6259c-116">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="6259c-117">W pliku kodu źródłowego użyj tokenów bez uwzględniania `$token$` wielkości liter formularza, aby wskazać wartości, które NuGet powinien zastąpić właściwościami projektu:</span><span class="sxs-lookup"><span data-stu-id="6259c-117">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="6259c-118">Po instalacji NuGet `$rootnamespace$` `Fabrikam` zastępuje przy założeniu, że projekt `Fabrikam`docelowy, którego głównym obszarem nazw jest .</span><span class="sxs-lookup"><span data-stu-id="6259c-118">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="6259c-119">Token `$rootnamespace$` jest najczęściej używaną właściwością projektu; wszystkie pozostałe są wymienione we [właściwościach projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="6259c-119">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="6259c-120">Należy pamiętać, oczywiście, że niektóre właściwości mogą być specyficzne dla typu projektu.</span><span class="sxs-lookup"><span data-stu-id="6259c-120">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="6259c-121">Określanie przekształceń plików konfiguracyjnych</span><span class="sxs-lookup"><span data-stu-id="6259c-121">Specifying config file transformations</span></span>

<span data-ttu-id="6259c-122">Zgodnie z opisem w kolejnych sekcjach przekształcenia plików konfiguracyjnych można wykonać na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="6259c-122">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="6259c-123">Dołącz `app.config.transform` `web.config.transform` i pliki w `content` folderze pakietu, gdzie `.transform` rozszerzenie mówi NuGet, że te pliki zawierają XML do scalenia z istniejącymi plikami konfiguracyjnymi po zainstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="6259c-123">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="6259c-124">Po odinstalowaniu pakietu ten sam kod XML jest usuwany.</span><span class="sxs-lookup"><span data-stu-id="6259c-124">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="6259c-125">Dołącz `app.config.install.xdt` `web.config.install.xdt` i pliki w `content` folderze pakietu, używając [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx) do opisania żądanych zmian.</span><span class="sxs-lookup"><span data-stu-id="6259c-125">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="6259c-126">Za pomocą tej opcji `.uninstall.xdt` można również dołączyć plik do odwrócenia zmian, gdy pakiet jest usuwany z projektu.</span><span class="sxs-lookup"><span data-stu-id="6259c-126">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="6259c-127">Przekształcenia nie są `.config` stosowane do plików, do których odwołuje się jako łącze w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6259c-127">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="6259c-128">Zaletą korzystania z XDT jest to, że zamiast po prostu scalanie dwóch plików statycznych, zapewnia składnię do manipulowania strukturą XML DOM przy użyciu elementu i atrybutu dopasowania przy użyciu pełnej obsługi XPath.</span><span class="sxs-lookup"><span data-stu-id="6259c-128">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="6259c-129">XDT można następnie dodać, zaktualizować lub usunąć elementy, umieścić nowe elementy w określonej lokalizacji lub zastąpić/usunąć elementy (w tym węzłów podrzędnych).</span><span class="sxs-lookup"><span data-stu-id="6259c-129">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="6259c-130">To sprawia, że łatwo utworzyć odinstalować przekształca, że kopii zapasowej wszystkich przekształceń wykonanych podczas instalacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="6259c-130">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="6259c-131">Transformacje XML</span><span class="sxs-lookup"><span data-stu-id="6259c-131">XML transforms</span></span>

<span data-ttu-id="6259c-132">I `app.config.transform` `web.config.transform` w `content` folderze pakietu zawierają tylko te elementy do scalenia w istniejących `app.config` i `web.config` plików projektu.</span><span class="sxs-lookup"><span data-stu-id="6259c-132">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="6259c-133">Na przykład załóżmy, że projekt `web.config`początkowo zawiera następującą zawartość w:</span><span class="sxs-lookup"><span data-stu-id="6259c-133">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="6259c-134">Aby dodać `MyNuModule` element `modules` do sekcji podczas instalowania `web.config.transform` `content` pakietu, utwórz plik w folderze pakietu, który wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="6259c-134">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="6259c-135">Po zainstalowaniu pakietu przez `web.config` NuGet pojawi się w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6259c-135">After NuGet installs the package, `web.config` will appear as follows:</span></span>

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

<span data-ttu-id="6259c-136">Należy zauważyć, że NuGet `modules` nie zastąpił sekcji, po prostu scalone nowego wpisu do niego, dodając tylko nowe elementy i atrybuty.</span><span class="sxs-lookup"><span data-stu-id="6259c-136">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="6259c-137">NuGet nie zmieni żadnych istniejących elementów lub atrybutów.</span><span class="sxs-lookup"><span data-stu-id="6259c-137">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="6259c-138">Po odinstalowaniu pakietu NuGet ponownie `.transform` zbada pliki i usunie `.config` elementy, które zawiera z odpowiednich plików.</span><span class="sxs-lookup"><span data-stu-id="6259c-138">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="6259c-139">Należy zauważyć, że ten proces `.config` nie wpłynie na żadne wiersze w pliku, które można zmodyfikować po instalacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="6259c-139">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="6259c-140">Jako bardziej obszerny przykład pakiet [Moduły rejestrowania błędów i programy obsługi ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) dodaje wiele wpisów do `web.config`programu , które są ponownie usuwane po odinstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="6259c-140">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="6259c-141">Aby sprawdzić `web.config.transform` jego plik, pobierz pakiet ELMAH z powyższego `.nupkg` `.zip`łącza, zmień `content\web.config.transform` rozszerzenie pakietu z , a następnie otwórz w tym pliku ZIP.</span><span class="sxs-lookup"><span data-stu-id="6259c-141">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="6259c-142">Aby zobaczyć efekt instalacji i odinstalowywania pakietu, utwórz nowy projekt ASP.NET w programie Visual Studio (szablon znajduje się w obszarze **Visual C# > Web** w oknie dialogowym Nowy projekt) i wybierz pustą aplikację ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6259c-142">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="6259c-143">Otwórz, `web.config` aby zobaczyć jego stan początkowy.</span><span class="sxs-lookup"><span data-stu-id="6259c-143">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="6259c-144">Następnie kliknij prawym przyciskiem myszy projekt, wybierz pozycję **Zarządzaj pakietami NuGet**, wyszukaj elmah na nuget.org i zainstaluj najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="6259c-144">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="6259c-145">Zwróć uwagę na `web.config`wszystkie zmiany na .</span><span class="sxs-lookup"><span data-stu-id="6259c-145">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="6259c-146">Teraz odinstaluj `web.config` pakiet i zobaczysz powrót do poprzedniego stanu.</span><span class="sxs-lookup"><span data-stu-id="6259c-146">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="6259c-147">Transformacje XDT</span><span class="sxs-lookup"><span data-stu-id="6259c-147">XDT transforms</span></span>

> [!Note]
> <span data-ttu-id="6259c-148">Jak wspomniano w [sekcji problemy ze zgodnością pakietu dokumentów `packages.config` do `PackageReference`migracji z do ](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), XDT przekształcenia, jak opisano poniżej są obsługiwane tylko przez `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="6259c-148">As mentioned in the [package compatibility issues section of the docs for migrating from `packages.config` to `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), XDT transformations as described below are only supported by `packages.config`.</span></span> <span data-ttu-id="6259c-149">Jeśli dodasz poniższe pliki do pakietu, konsumenci `PackageReference` korzystający z pakietu z nie będą mieli zastosowanych przekształceń (patrz [ten przykład,](https://github.com/NuGet/Samples/tree/master/XDTransformExample) aby transformacje XDT działały).`PackageReference`</span><span class="sxs-lookup"><span data-stu-id="6259c-149">If you add the below files to your package, consumers using your package with `PackageReference` will not have the transformations applied (refer to [this sample](https://github.com/NuGet/Samples/tree/master/XDTransformExample) to make XDT transforms work with`PackageReference`).</span></span>

<span data-ttu-id="6259c-150">Pliki konfiguracyjne można modyfikować przy użyciu [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="6259c-150">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="6259c-151">Można również nuget zastąpić tokeny z [właściwości projektu,](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) `$` dołączając nazwę właściwości w ogranicznika (bez uwzględniania wielkości liter).</span><span class="sxs-lookup"><span data-stu-id="6259c-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimiters (case-insensitive).</span></span>

<span data-ttu-id="6259c-152">Na przykład następujący `app.config.install.xdt` plik wstawi `app.config` element `FullPath`zawierający `FileName` `appSettings` `ActiveConfigurationSettings` , i wartości z projektu:</span><span class="sxs-lookup"><span data-stu-id="6259c-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="6259c-153">Na inny przykład załóżmy, że `web.config`projekt początkowo zawiera następującą zawartość w:</span><span class="sxs-lookup"><span data-stu-id="6259c-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="6259c-154">Aby dodać `MyNuModule` element `modules` do sekcji podczas instalowania `web.config.install.xdt` pakietu, pakiet będzie zawierać następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6259c-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="6259c-155">Po zainstalowaniu `web.config` pakietu, będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="6259c-155">After installing the package, `web.config` will look like this:</span></span>

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

<span data-ttu-id="6259c-156">Aby usunąć `MyNuModule` tylko element podczas `web.config.uninstall.xdt` odinstalowywania pakietu, plik powinien zawierać następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6259c-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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
