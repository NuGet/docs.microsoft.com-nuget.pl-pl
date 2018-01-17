---
title: Tworzenie zlokalizowanego pakietu NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 824c3f45-c6c2-4c82-9d6d-62a19bfdc4a4
description: "Szczegółowe informacje na dwa sposoby tworzenia zlokalizowane pakiety NuGet, w tym wszystkie zestawy w jednym pakiecie lub publikowanie osobnych zestawów."
keywords: "Lokalizacja pakietu NuGet, zestawy satelickie NuGet, tworzenie zlokalizowanych pakietów NuGet konwencje lokalizacji"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: aa48e77bd0e64cf45292687a2d4cada198ff5749
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="4a120-104">Tworzenie zlokalizowanych pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="4a120-104">Creating localized NuGet packages</span></span>

<span data-ttu-id="4a120-105">Istnieją dwa sposoby tworzenia zlokalizowane wersje biblioteki:</span><span class="sxs-lookup"><span data-stu-id="4a120-105">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="4a120-106">Uwzględnij wszystkie zestawy zlokalizowanych zasobów w jednym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="4a120-106">Include all localized resources assemblies in a single package.</span></span>
2. <span data-ttu-id="4a120-107">Utwórz oddzielne satelity zlokalizowanych pakietów (NuGet 1,8 i nowsze), wykonując obowiązek ścisłego przestrzegania Konwencji.</span><span class="sxs-lookup"><span data-stu-id="4a120-107">Create separate localized satellite packages (NuGet 1.8 and later), by following a strict set of conventions.</span></span>

<span data-ttu-id="4a120-108">Obie metody ma swoje zalety i wady, zgodnie z opisem w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="4a120-108">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="4a120-109">Zestawy zlokalizowanych zasobów w jednym pakiecie</span><span class="sxs-lookup"><span data-stu-id="4a120-109">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="4a120-110">W tym zestawy zlokalizowanych zasobów w jednym pakiecie jest zwykle najprostsza metoda.</span><span class="sxs-lookup"><span data-stu-id="4a120-110">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="4a120-111">W tym celu należy utworzyć foldery zawarte w `lib` obsługiwane języka innego niż domyślny pakiet (założono, że to en-us).</span><span class="sxs-lookup"><span data-stu-id="4a120-111">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="4a120-112">W tych folderach można umieścić zestawy zasobów i zlokalizowanych plików IntelliSense XML.</span><span class="sxs-lookup"><span data-stu-id="4a120-112">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="4a120-113">Na przykład następujące struktury folderów obsługuje, niemiecki (de), włoski (go), japoński (ja), rosyjski (ru), chiński (uproszczony) (zh-Hans) i chiński (tradycyjny) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="4a120-113">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

<span data-ttu-id="4a120-114">Widać, że języki są wszystkie wymienione poniżej `net40` folderu docelowego framework.</span><span class="sxs-lookup"><span data-stu-id="4a120-114">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="4a120-115">Jeśli jesteś [obsługujący wiele platform](../create-packages/supporting-multiple-target-frameworks.md), należy folderu `lib` dla każdego wariantu.</span><span class="sxs-lookup"><span data-stu-id="4a120-115">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you'll have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="4a120-116">Z tych folderów w miejscu zostanie następnie odwołać wszystkie pliki w Twojej `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="4a120-116">With these folders in place, you'll then reference all the files in your `.nuspec`:</span></span>

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

<span data-ttu-id="4a120-117">Jeden pakiet przykładzie, który korzysta z tej metody jest [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="4a120-117">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages"></a><span data-ttu-id="4a120-118">Zalety i wady</span><span class="sxs-lookup"><span data-stu-id="4a120-118">Advantages and disadvantages</span></span>

<span data-ttu-id="4a120-119">Tworzenie pakietów wszystkie języki w jednym pakiecie ma kilka wady:</span><span class="sxs-lookup"><span data-stu-id="4a120-119">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="4a120-120">**Udostępnione metadanych**: ponieważ pakietu NuGet może zawierać tylko jeden `.nuspec` plików, można zapewnić metadane tylko jeden język.</span><span class="sxs-lookup"><span data-stu-id="4a120-120">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="4a120-121">Oznacza to, że NuGet nie stanowi obsługuje zlokalizowanych metadanych.</span><span class="sxs-lookup"><span data-stu-id="4a120-121">That is, NuGet does not present support localized metadata.</span></span>
2. <span data-ttu-id="4a120-122">**Rozmiar pakietu**: w zależności od liczby obsługiwanych języków, biblioteki może stać się znacznie duży, który spowalnia Instalowanie i przywracanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="4a120-122">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
3. <span data-ttu-id="4a120-123">**Zwalnia równoczesne**: tworzenie pakietów zlokalizowane pliki w jednym pakiecie wymaga wersji wszystkie zasoby w tym pakiecie jednocześnie, zamiast możliwość oddzielnie wersji każdej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="4a120-123">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="4a120-124">Ponadto żadnych aktualizacji do dowolnej lokalizacji co wymaga nowej wersji cały pakiet.</span><span class="sxs-lookup"><span data-stu-id="4a120-124">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="4a120-125">Jednak także ma kilka korzyści:</span><span class="sxs-lookup"><span data-stu-id="4a120-125">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="4a120-126">**Prostota**: konsumentów pakietu pobrać wszystkich obsługiwanych języków w jednej instalacji, zamiast instalować oddzielnie każdego języka.</span><span class="sxs-lookup"><span data-stu-id="4a120-126">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="4a120-127">Pojedynczy pakiet jest również łatwiej znaleźć na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4a120-127">A single package is also easier to find on nuget.org.</span></span>
2. <span data-ttu-id="4a120-128">**Sprzężona wersji**: ponieważ wszystkie zestawy zasobów znajdują się w tym samym pakiecie jako podstawowy zestaw, wszystkie mają ten sam numer wersji i nie uruchamiaj ryzyko błędnego pobierania całkowicie niezależna.</span><span class="sxs-lookup"><span data-stu-id="4a120-128">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>


## <a name="localized-satellite-packages"></a><span data-ttu-id="4a120-129">Pakiety satelity zlokalizowanych</span><span class="sxs-lookup"><span data-stu-id="4a120-129">Localized satellite packages</span></span>

<span data-ttu-id="4a120-130">Podobnie jak środowisko .NET Framework obsługuje zestawy satelickie, ta metoda oddziela zlokalizowanych zasobów i plików IntelliSense XML w pakiety satelity.</span><span class="sxs-lookup"><span data-stu-id="4a120-130">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="4a120-131">To robić, podstawowy pakiet używa konwencji nazewnictwa `{identifier}.{version}.nupkg` i zawiera zestaw dla języka domyślnego (na przykład "en US).</span><span class="sxs-lookup"><span data-stu-id="4a120-131">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="4a120-132">Na przykład `ContosoUtilities.1.0.0.nupkg` będzie zawierał następującą strukturę:</span><span class="sxs-lookup"><span data-stu-id="4a120-132">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="4a120-133">Następnie zestaw satelicki używa konwencji nazewnictwa `{identifier}.{language}.{version}.nupkg`, takich jak `ContosoUtilities.de.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="4a120-133">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="4a120-134">Identyfikator **musi** dokładnie odpowiadać podstawowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="4a120-134">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="4a120-135">Ponieważ to oddzielny pakiet ma własną `.nuspec` pliku, który zawiera zlokalizowane metadanych.</span><span class="sxs-lookup"><span data-stu-id="4a120-135">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="4a120-136">Zachować ostrożność, który język w `.nuspec` **musi** zgodne z działaniem używanym w nazwie pliku.</span><span class="sxs-lookup"><span data-stu-id="4a120-136">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="4a120-137">Zestawu satelickiego **musi** deklarować dokładnej wersji głównej pakietu także jako zależności, przy użyciu notacji wersji [] \(zobacz [wersji pakietu](../reference/package-versioning.md)).</span><span class="sxs-lookup"><span data-stu-id="4a120-137">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../reference/package-versioning.md)).</span></span> <span data-ttu-id="4a120-138">Na przykład `ContosoUtilities.de.1.0.0.nupkg` należy zadeklarować zależność `ContosoUtilities.1.0.0.nupkg` przy użyciu `[1.0.0]` notacji.</span><span class="sxs-lookup"><span data-stu-id="4a120-138">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="4a120-139">Oczywiście pakietu satelity ma numer wersji innego niż podstawowy pakiet.</span><span class="sxs-lookup"><span data-stu-id="4a120-139">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="4a120-140">Struktura pakietu satelity następnie muszą zawierać zestaw zasobów i plik XML IntelliSense w w podfolderze odpowiadający `{language}` w nazwie pliku pakietu:</span><span class="sxs-lookup"><span data-stu-id="4a120-140">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="4a120-141">**Uwaga**: chyba że określone podhodowli, takich jak `ja-JP` są niezbędne, zawsze używaj wyższy identyfikator języka poziomu, tak samo, jak `ja`.</span><span class="sxs-lookup"><span data-stu-id="4a120-141">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="4a120-142">W zestawie satelickim rozpozna NuGet **tylko** tych plików w folderze, który odpowiada `{language}` w nazwie pliku.</span><span class="sxs-lookup"><span data-stu-id="4a120-142">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="4a120-143">Wszystkie pozostałe są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="4a120-143">All others are ignored.</span></span>

<span data-ttu-id="4a120-144">Gdy są spełnione wszystkie następujące konwencje NuGet rozpozna pakietu jako pakiet satelity i instalowanie zlokalizowanych plików w pakiecie głównej `lib` folderu, tak jakby były one pierwotnie powiązane.</span><span class="sxs-lookup"><span data-stu-id="4a120-144">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="4a120-145">Odinstalowywanie pakietu satelity spowoduje usunięcie jej pliki z tego samego folderu.</span><span class="sxs-lookup"><span data-stu-id="4a120-145">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="4a120-146">Należy utworzyć dodatkowe zestawy satelickie w taki sam sposób dla każdego obsługiwanego języka.</span><span class="sxs-lookup"><span data-stu-id="4a120-146">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="4a120-147">Na przykład sprawdź zestaw pakietów platformy ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="4a120-147">For an example, examine the set of ASP.NET MVC packages:</span></span>

* <span data-ttu-id="4a120-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (podstawowy w języku angielskim)</span><span class="sxs-lookup"><span data-stu-id="4a120-148">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
* <span data-ttu-id="4a120-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (wersja niemiecka)</span><span class="sxs-lookup"><span data-stu-id="4a120-149">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
* <span data-ttu-id="4a120-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (wersja japońska)</span><span class="sxs-lookup"><span data-stu-id="4a120-150">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
* <span data-ttu-id="4a120-151">[Microsoft.AspNet.Mvc.zh Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (chiński (uproszczony))</span><span class="sxs-lookup"><span data-stu-id="4a120-151">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
* <span data-ttu-id="4a120-152">[Microsoft.AspNet.Mvc.zh Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (chiński (tradycyjny))</span><span class="sxs-lookup"><span data-stu-id="4a120-152">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="4a120-153">Podsumowanie konwencje wymagane</span><span class="sxs-lookup"><span data-stu-id="4a120-153">Summary of required conventions</span></span>

- <span data-ttu-id="4a120-154">Pakiet podstawowy musi mieć nazwę.`{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="4a120-154">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="4a120-155">Pakiet satelity musi mieć nazwę.`{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="4a120-155">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="4a120-156">Pakiet satelity `.nuspec` musi określać języka aby dopasować nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="4a120-156">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="4a120-157">Pakiet satelity należy zadeklarować zależność dokładnej wersji głównej przy użyciu notacji [] w jego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="4a120-157">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="4a120-158">Zakresy nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="4a120-158">Ranges are not supported.</span></span>
- <span data-ttu-id="4a120-159">Pakiet satelity należy umieścić pliki w `lib\[{framework}\]{language}` folderu, która dokładnie odpowiada `{language}` w nazwie pliku.</span><span class="sxs-lookup"><span data-stu-id="4a120-159">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages"></a><span data-ttu-id="4a120-160">Zalety i wady</span><span class="sxs-lookup"><span data-stu-id="4a120-160">Advantages and disadvantages</span></span>

<span data-ttu-id="4a120-161">Używanie pakietów satelity ma kilka korzyści:</span><span class="sxs-lookup"><span data-stu-id="4a120-161">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="4a120-162">**Rozmiar pakietu**: jest zminimalizowany ogólną rozmiaru pakiet główny i konsumentów tylko ponoszenia kosztów każdego języka będą wykorzystywane.</span><span class="sxs-lookup"><span data-stu-id="4a120-162">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
2. <span data-ttu-id="4a120-163">**Oddzielne metadanych**: każdy pakiet satelity ma własną `.nuspec` pliku i w związku z tym zlokalizowanych metadanych ponieważ.</span><span class="sxs-lookup"><span data-stu-id="4a120-163">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="4a120-164">Może to umożliwić niektórych konsumentów łatwiej znaleźć pakietów, wyszukując nuget.org z warunkami zlokalizowane.</span><span class="sxs-lookup"><span data-stu-id="4a120-164">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
3. <span data-ttu-id="4a120-165">**Całkowicie niezależna wersjach**: zestawy satelickie może być zwolnione wraz z upływem czasu, a nie w całości, umożliwiając rozłożenia wysiłków lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="4a120-165">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="4a120-166">Jednak pakiety satelity mieć własny zestaw wady:</span><span class="sxs-lookup"><span data-stu-id="4a120-166">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="4a120-167">**Bałaganu**: zamiast pojedynczy pakiet ma wiele pakietów, które mogą prowadzić do dużej liczby wyników nuget.org i długą listę odwołań w projekcie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4a120-167">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
2. <span data-ttu-id="4a120-168">**Konwencje Strict**.</span><span class="sxs-lookup"><span data-stu-id="4a120-168">**Strict conventions**.</span></span> <span data-ttu-id="4a120-169">Pakiety satelity musi dokładnie zgodne z konwencjami lub zlokalizowane wersje nie zostać pobrana prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="4a120-169">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
3. <span data-ttu-id="4a120-170">**Przechowywanie wersji**: każdy pakiet satelity musi mieć zależność dokładnej wersji głównej pakietu.</span><span class="sxs-lookup"><span data-stu-id="4a120-170">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="4a120-171">Oznacza to, że aktualizacji pakietu głównej mogą wymagać aktualizacji wszystkich pakietów satelity również nawet wtedy, gdy nie zmienił się zasoby.</span><span class="sxs-lookup"><span data-stu-id="4a120-171">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
