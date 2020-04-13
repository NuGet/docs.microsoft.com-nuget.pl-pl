---
title: Jak utworzyć zlokalizowany pakiet NuGet
description: Szczegółowe informacje na temat dwóch sposobów tworzenia zlokalizowanych pakietów NuGet, przez włączenie wszystkich zestawów w jednym pakiecie lub publikowania oddzielnych zestawów.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 83414a824676844f9e44eab874e5eac788d50583
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610941"
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="e158e-103">Tworzenie zlokalizowanych pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="e158e-103">Creating localized NuGet packages</span></span>

<span data-ttu-id="e158e-104">Istnieją dwa sposoby tworzenia zlokalizowanych wersji biblioteki:</span><span class="sxs-lookup"><span data-stu-id="e158e-104">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="e158e-105">Uwzględnij wszystkie zlokalizowane zestawy zasobów w jednym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="e158e-105">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="e158e-106">Tworzenie oddzielnych zlokalizowanych pakietów satelitarnych, postępuje zgodnie ze ścisłym zestawem konwencji.</span><span class="sxs-lookup"><span data-stu-id="e158e-106">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="e158e-107">Obie metody mają swoje zalety i wady, jak opisano w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="e158e-107">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="e158e-108">Zlokalizowane zestawy zasobów w jednym pakiecie</span><span class="sxs-lookup"><span data-stu-id="e158e-108">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="e158e-109">Włączenie zlokalizowanych zestawów zasobów w jednym pakiecie jest zazwyczaj najprostszym podejściem.</span><span class="sxs-lookup"><span data-stu-id="e158e-109">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="e158e-110">Aby to zrobić, należy `lib` utworzyć foldery w dla obsługiwanego języka innego niż domyślny pakiet (zakłada się, że en-us).</span><span class="sxs-lookup"><span data-stu-id="e158e-110">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="e158e-111">W tych folderach można umieszczać zestawy zasobów i zlokalizowane pliki IntelliSense XML.</span><span class="sxs-lookup"><span data-stu-id="e158e-111">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="e158e-112">Na przykład: obsługa struktury folderów: niemiecki (de), włoski (it), japoński (ja), rosyjski (ru), chiński (uproszczony) (zh-Hans) i chiński (tradycyjny) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="e158e-112">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

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

<span data-ttu-id="e158e-113">Widać, że wszystkie języki są wymienione `net40` poniżej folderu struktury docelowej.</span><span class="sxs-lookup"><span data-stu-id="e158e-113">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="e158e-114">Jeśli [obsługujesz wiele struktur,](../create-packages/supporting-multiple-target-frameworks.md)masz folder w `lib` obszarze dla każdego wariantu.</span><span class="sxs-lookup"><span data-stu-id="e158e-114">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="e158e-115">Z tych folderów w miejscu, następnie odwołać się do wszystkich plików w : `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="e158e-115">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

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

<span data-ttu-id="e158e-116">Jednym z przykładowych pakietów, który używa tego podejścia jest [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="e158e-116">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="e158e-117">Zalety i wady (zlokalizowane zestawy zasobów)</span><span class="sxs-lookup"><span data-stu-id="e158e-117">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="e158e-118">Łączenie wszystkich języków w jednym pakiecie ma kilka wad:</span><span class="sxs-lookup"><span data-stu-id="e158e-118">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="e158e-119">**Udostępnione metadane:** Ponieważ pakiet NuGet `.nuspec` może zawierać tylko jeden plik, można podać metadane tylko dla jednego języka.</span><span class="sxs-lookup"><span data-stu-id="e158e-119">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="e158e-120">Oznacza to, że NuGet nie przedstawia obsługi zlokalizowanych metadanych.</span><span class="sxs-lookup"><span data-stu-id="e158e-120">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="e158e-121">**Rozmiar pakietu:** W zależności od liczby obsługiwanych języków biblioteka może stać się znacznie duża, co spowalnia instalowanie i przywracanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="e158e-121">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="e158e-122">**Jednoczesne wydania:** Łączenie zlokalizowanych plików w jeden pakiet wymaga jednoczesnego zwolnienia wszystkich zasobów w tym pakiecie, a nie możliwości osobnego wydania każdej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="e158e-122">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="e158e-123">Ponadto każda aktualizacja dowolnej lokalizacji wymaga nowej wersji całego pakietu.</span><span class="sxs-lookup"><span data-stu-id="e158e-123">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="e158e-124">Jednak, ma również kilka korzyści:</span><span class="sxs-lookup"><span data-stu-id="e158e-124">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="e158e-125">**Prostota:** Konsumenci pakietu otrzymują wszystkie obsługiwane języki w jednej instalacji, zamiast instalować każdy język oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="e158e-125">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="e158e-126">Pojedynczy pakiet jest również łatwiej znaleźć na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e158e-126">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="e158e-127">**Wersje sprzężone:** Ponieważ wszystkie zestawy zasobów znajdują się w tym samym pakiecie co zestaw podstawowy, wszystkie mają ten sam numer wersji i nie są narażone na błędne oddzielenie.</span><span class="sxs-lookup"><span data-stu-id="e158e-127">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="e158e-128">Zlokalizowane pakiety satelitarne</span><span class="sxs-lookup"><span data-stu-id="e158e-128">Localized satellite packages</span></span>

<span data-ttu-id="e158e-129">Podobnie jak program .NET Framework obsługuje zestawy satelityczne, ta metoda oddziela zlokalizowane zasoby i pliki IntelliSense XML do pakietów satelitarnych.</span><span class="sxs-lookup"><span data-stu-id="e158e-129">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="e158e-130">W tym celu pakiet podstawowy używa konwencji `{identifier}.{version}.nupkg` nazewnictwa i zawiera zestaw dla języka domyślnego (na przykład en-US).</span><span class="sxs-lookup"><span data-stu-id="e158e-130">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="e158e-131">Na przykład `ContosoUtilities.1.0.0.nupkg` może zawierać następującą strukturę:</span><span class="sxs-lookup"><span data-stu-id="e158e-131">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="e158e-132">Następnie zestaw satelitów używa `{identifier}.{language}.{version}.nupkg`konwencji `ContosoUtilities.de.1.0.0.nupkg`nazewnictwa, takiej jak .</span><span class="sxs-lookup"><span data-stu-id="e158e-132">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="e158e-133">Identyfikator musi dokładnie **odpowiadać** identyfikatorowi pakietu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="e158e-133">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="e158e-134">Ponieważ jest to oddzielny pakiet, `.nuspec` ma swój własny plik, który zawiera zlokalizowane metadane.</span><span class="sxs-lookup"><span data-stu-id="e158e-134">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="e158e-135">Należy pamiętać, że `.nuspec` język w **musi odpowiadać** język używany w nazwa pliku.</span><span class="sxs-lookup"><span data-stu-id="e158e-135">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="e158e-136">Zestaw satelickiego musi również **zadeklarować** dokładną wersję pakietu podstawowego jako zależność, używając notacji [] wersji (zobacz [Przechowywanie wersji pakietu).](../concepts/package-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="e158e-136">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../concepts/package-versioning.md)).</span></span> <span data-ttu-id="e158e-137">Na przykład `ContosoUtilities.de.1.0.0.nupkg` musi zadeklarować `ContosoUtilities.1.0.0.nupkg` zależność `[1.0.0]` przy użyciu notacji.</span><span class="sxs-lookup"><span data-stu-id="e158e-137">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="e158e-138">Pakiet satelitarny może oczywiście mieć inny numer wersji niż pakiet podstawowy.</span><span class="sxs-lookup"><span data-stu-id="e158e-138">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="e158e-139">Struktura pakietu satelitarnego musi następnie zawierać zestaw zasobów i plik XML IntelliSense w podfolderze, który pasuje `{language}` do nazwy pliku pakietu:</span><span class="sxs-lookup"><span data-stu-id="e158e-139">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="e158e-140">**Uwaga:** o ile określone subkultury, takie jak `ja-JP` są konieczne, `ja`zawsze należy używać identyfikatora języka wyższego poziomu, takiego jak .</span><span class="sxs-lookup"><span data-stu-id="e158e-140">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="e158e-141">W zestawie satelicie NuGet rozpozna **tylko** te pliki `{language}` w folderze, który pasuje do nazwy pliku w.</span><span class="sxs-lookup"><span data-stu-id="e158e-141">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="e158e-142">Wszystkie inne są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="e158e-142">All others are ignored.</span></span>

<span data-ttu-id="e158e-143">Po spełnieniu wszystkich tych konwencji, NuGet rozpozna pakiet jako pakiet satelitarny i zainstaluje `lib` zlokalizowane pliki w folderze pakietu podstawowego, tak jakby zostały pierwotnie dołączone.</span><span class="sxs-lookup"><span data-stu-id="e158e-143">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="e158e-144">Odinstalowanie pakietu satelitarnego spowoduje usunięcie jego plików z tego samego folderu.</span><span class="sxs-lookup"><span data-stu-id="e158e-144">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="e158e-145">Należy utworzyć dodatkowe zestawy satelickie w taki sam sposób dla każdego obsługiwanego języka.</span><span class="sxs-lookup"><span data-stu-id="e158e-145">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="e158e-146">Na przykład sprawdź zestaw ASP.NET pakietów MVC:</span><span class="sxs-lookup"><span data-stu-id="e158e-146">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="e158e-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (angielski podstawowy)</span><span class="sxs-lookup"><span data-stu-id="e158e-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="e158e-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (niemiecki)</span><span class="sxs-lookup"><span data-stu-id="e158e-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="e158e-149">[Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japoński)</span><span class="sxs-lookup"><span data-stu-id="e158e-149">[Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="e158e-150">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (chiński (uproszczony))</span><span class="sxs-lookup"><span data-stu-id="e158e-150">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="e158e-151">[Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (chiński (tradycyjny))</span><span class="sxs-lookup"><span data-stu-id="e158e-151">[Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="e158e-152">Podsumowanie wymaganych konwencji</span><span class="sxs-lookup"><span data-stu-id="e158e-152">Summary of required conventions</span></span>

- <span data-ttu-id="e158e-153">Pakiet podstawowy musi mieć nazwę`{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="e158e-153">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="e158e-154">Pakiet satelitarny musi być nazwany`{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="e158e-154">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="e158e-155">Pakiet satelitarny `.nuspec` musi określać jego język, aby dopasować nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="e158e-155">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="e158e-156">Pakiet satelitarny musi zadeklarować zależność od dokładnej wersji podstawowej `.nuspec` przy użyciu notacji [] w jego pliku.</span><span class="sxs-lookup"><span data-stu-id="e158e-156">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="e158e-157">Zakresy nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e158e-157">Ranges are not supported.</span></span>
- <span data-ttu-id="e158e-158">Pakiet satelitarny musi umieszczać pliki w folderze, `lib\[{framework}\]{language}` który dokładnie pasuje `{language}` do nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="e158e-158">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="e158e-159">Zalety i wady (pakiety satelitarne)</span><span class="sxs-lookup"><span data-stu-id="e158e-159">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="e158e-160">Korzystanie z pakietów satelitarnych ma kilka zalet:</span><span class="sxs-lookup"><span data-stu-id="e158e-160">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="e158e-161">**Rozmiar pakietu:** Ogólny rozmiar pakietu podstawowego jest zminimalizowany, a konsumenci ponoszą tylko koszty każdego języka, którego chcą użyć.</span><span class="sxs-lookup"><span data-stu-id="e158e-161">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="e158e-162">**Oddzielne metadane:** Każdy pakiet `.nuspec` satelitarny ma swój własny plik, a tym samym własne zlokalizowane metadane, ponieważ.</span><span class="sxs-lookup"><span data-stu-id="e158e-162">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="e158e-163">Dzięki temu niektórzy konsumenci mogą łatwiej znaleźć pakiety, wyszukując nuget.org z zlokalizowanych terminów.</span><span class="sxs-lookup"><span data-stu-id="e158e-163">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="e158e-164">**Wydania odłączone:** Zestawy satelitarne mogą być zwalniane w czasie, a nie wszystkie naraz, co pozwala na rozłożenie wysiłków związanych z lokalizacją.</span><span class="sxs-lookup"><span data-stu-id="e158e-164">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="e158e-165">Jednak pakiety satelitarne mają swój własny zestaw wad:</span><span class="sxs-lookup"><span data-stu-id="e158e-165">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="e158e-166">**Mało istotne:** Zamiast pojedynczego pakietu, masz wiele pakietów, które mogą prowadzić do zaśmieconych wyników wyszukiwania na nuget.org i długą listę odwołań w projekcie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e158e-166">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="e158e-167">**Ścisłe konwencje**.</span><span class="sxs-lookup"><span data-stu-id="e158e-167">**Strict conventions**.</span></span> <span data-ttu-id="e158e-168">Pakiety satelitarne muszą dokładnie przestrzegać konwencji lub zlokalizowane wersje nie zostaną prawidłowo odebrane.</span><span class="sxs-lookup"><span data-stu-id="e158e-168">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="e158e-169">**Przechowywanie wersji:** Każdy pakiet satelitarny musi mieć dokładną zależność wersji od pakietu podstawowego.</span><span class="sxs-lookup"><span data-stu-id="e158e-169">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="e158e-170">Oznacza to, że aktualizacja pakietu podstawowego może wymagać aktualizacji wszystkich pakietów satelitarnych, nawet jeśli zasoby nie zostały zmienić.</span><span class="sxs-lookup"><span data-stu-id="e158e-170">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
