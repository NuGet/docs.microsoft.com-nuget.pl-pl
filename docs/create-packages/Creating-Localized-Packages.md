---
title: Jak utworzyć zlokalizowany pakiet NuGet
description: Szczegółowe informacje na temat dwóch sposobów tworzenia zlokalizowanych pakietów NuGet przy użyciu wszystkich zestawów w pojedynczym pakiecie lub publikowania oddzielnych zestawów.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: cb3f8a9df66f259b130996822f102c27636d5d2c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774748"
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="ff6be-103">Tworzenie zlokalizowanych pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="ff6be-103">Creating localized NuGet packages</span></span>

<span data-ttu-id="ff6be-104">Istnieją dwa sposoby tworzenia zlokalizowanych wersji biblioteki:</span><span class="sxs-lookup"><span data-stu-id="ff6be-104">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="ff6be-105">Uwzględnij wszystkie zestawy zlokalizowanych zasobów w pojedynczym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="ff6be-105">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="ff6be-106">Utwórz oddzielne, zlokalizowane pakiety satelickie, wykonując rygorystyczne zestawy Konwencji.</span><span class="sxs-lookup"><span data-stu-id="ff6be-106">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="ff6be-107">Obie metody mają swoje zalety i wady, zgodnie z opisem w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="ff6be-107">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="ff6be-108">Zlokalizowane zestawy zasobów w pojedynczym pakiecie</span><span class="sxs-lookup"><span data-stu-id="ff6be-108">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="ff6be-109">Uwzględnianie zlokalizowanych zestawów zasobów w pojedynczym pakiecie jest zazwyczaj najprostszym podejściem.</span><span class="sxs-lookup"><span data-stu-id="ff6be-109">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="ff6be-110">W tym celu należy utworzyć foldery w programie `lib` dla obsługiwanego języka innego niż domyślny pakiet (założono, że jest to en-US).</span><span class="sxs-lookup"><span data-stu-id="ff6be-110">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="ff6be-111">W tych folderach można umieścić zestawy zasobów i zlokalizowane pliki XML IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="ff6be-111">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="ff6be-112">Na przykład następująca struktura folderów obsługuje, niemiecki (Niemcy), włoski (IT), japoński (ja), rosyjski (ru), chiński (uproszczony) (zh-Hans) i chiński (tradycyjny) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="ff6be-112">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

```
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
```

<span data-ttu-id="ff6be-113">Można zobaczyć, że wszystkie języki są wymienione poniżej `net40` folderu platformy docelowej.</span><span class="sxs-lookup"><span data-stu-id="ff6be-113">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="ff6be-114">Jeśli [obsługujesz wiele platform](../create-packages/supporting-multiple-target-frameworks.md), masz folder w obszarze `lib` dla każdego wariantu.</span><span class="sxs-lookup"><span data-stu-id="ff6be-114">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="ff6be-115">Po wprowadzeniu tych folderów odwołujesz się do wszystkich plików w `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="ff6be-115">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

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

<span data-ttu-id="ff6be-116">Jednym z przykładowych pakietów korzystających z tej metody jest [Microsoft. Data. OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="ff6be-116">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="ff6be-117">Zalety i wady (zlokalizowane zestawy zasobów)</span><span class="sxs-lookup"><span data-stu-id="ff6be-117">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="ff6be-118">Zgrupowanie wszystkich języków w jednym pakiecie ma kilka wad:</span><span class="sxs-lookup"><span data-stu-id="ff6be-118">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="ff6be-119">**Udostępnione metadane**: ponieważ pakiet NuGet może zawierać tylko jeden `.nuspec` plik, można dostarczyć metadane tylko dla jednego języka.</span><span class="sxs-lookup"><span data-stu-id="ff6be-119">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="ff6be-120">Oznacza to, że NuGet nie obsługuje zlokalizowanych metadanych.</span><span class="sxs-lookup"><span data-stu-id="ff6be-120">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="ff6be-121">**Rozmiar pakietu**: w zależności od liczby obsługiwanych języków biblioteka może stać się znacznie duża, co powoduje spowolnienie instalowania i przywracania pakietu.</span><span class="sxs-lookup"><span data-stu-id="ff6be-121">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="ff6be-122">**Równoczesne wersje**: umieszczenie zlokalizowanych plików w jednym pakiecie wymaga jednoczesnego zwolnienia wszystkich zasobów w tym pakiecie, a nie w celu wypróbowania poszczególnych lokalizacji oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="ff6be-122">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="ff6be-123">Ponadto każda aktualizacja w jednej lokalizacji wymaga nowej wersji całego pakietu.</span><span class="sxs-lookup"><span data-stu-id="ff6be-123">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="ff6be-124">Jednak ma ona również kilka korzyści:</span><span class="sxs-lookup"><span data-stu-id="ff6be-124">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="ff6be-125">**Prostota**: konsumenci pakietu uzyskują wszystkie obsługiwane języki w jednej instalacji, a nie muszą osobno instalować każdego języka.</span><span class="sxs-lookup"><span data-stu-id="ff6be-125">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="ff6be-126">Jeden pakiet jest również łatwiejszy do znalezienia w witrynie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ff6be-126">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="ff6be-127">Powiązane **wersje**: ze względu na to, że wszystkie zestawy zasobów znajdują się w tym samym pakiecie co zestaw podstawowy, współużytkują one ten sam numer wersji i nie uruchamiają ryzyka błędnego oddzielenia.</span><span class="sxs-lookup"><span data-stu-id="ff6be-127">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="ff6be-128">Zlokalizowane pakiety satelickie</span><span class="sxs-lookup"><span data-stu-id="ff6be-128">Localized satellite packages</span></span>

<span data-ttu-id="ff6be-129">Podobnie jak .NET Framework obsługuje zestawy satelickie, ta metoda oddziela zlokalizowane zasoby i pliki XML IntelliSense do pakietów satelitarnych.</span><span class="sxs-lookup"><span data-stu-id="ff6be-129">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="ff6be-130">W tym celu pakiet podstawowy używa konwencji nazewnictwa `{identifier}.{version}.nupkg` i zawiera zestaw dla języka domyślnego (na przykład en-US).</span><span class="sxs-lookup"><span data-stu-id="ff6be-130">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="ff6be-131">Na przykład `ContosoUtilities.1.0.0.nupkg` będzie zawierać następującą strukturę:</span><span class="sxs-lookup"><span data-stu-id="ff6be-131">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

```
lib
└───net40
        ContosoUtilities.dll
        ContosoUtilities.xml
```

<span data-ttu-id="ff6be-132">Zestaw satelity używa konwencji nazewnictwa `{identifier}.{language}.{version}.nupkg` , takiej jak `ContosoUtilities.de.1.0.0.nupkg` .</span><span class="sxs-lookup"><span data-stu-id="ff6be-132">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="ff6be-133">Identyfikator **musi** być dokładnie zgodny z pakietem podstawowym.</span><span class="sxs-lookup"><span data-stu-id="ff6be-133">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="ff6be-134">Ponieważ jest to oddzielny pakiet, ma własny `.nuspec` plik, który zawiera zlokalizowane metadane.</span><span class="sxs-lookup"><span data-stu-id="ff6be-134">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="ff6be-135">Należy mieć na uwadze, że język w `.nuspec` **musi** być zgodny z użytym w nazwie pliku.</span><span class="sxs-lookup"><span data-stu-id="ff6be-135">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="ff6be-136">Zestaw satelicki **musi** również deklarować dokładną wersję pakietu podstawowego jako zależność przy użyciu notacji wersji [] (zobacz [wersja pakietu](../concepts/package-versioning.md)).</span><span class="sxs-lookup"><span data-stu-id="ff6be-136">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../concepts/package-versioning.md)).</span></span> <span data-ttu-id="ff6be-137">Na przykład, `ContosoUtilities.de.1.0.0.nupkg` należy zadeklarować zależność `ContosoUtilities.1.0.0.nupkg` przy użyciu `[1.0.0]` notacji.</span><span class="sxs-lookup"><span data-stu-id="ff6be-137">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="ff6be-138">Pakiet satelitarny może mieć inny numer wersji niż pakiet podstawowy.</span><span class="sxs-lookup"><span data-stu-id="ff6be-138">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="ff6be-139">Struktura pakietu satelitarnego musi zawierać zestaw zasobów i plik IntelliSense XML w podfolderze, który pasuje do `{language}` nazwy pliku pakietu:</span><span class="sxs-lookup"><span data-stu-id="ff6be-139">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

```
lib
└───net40
    └───de
            ContosoUtilities.resources.dll
            ContosoUtilities.xml
```

<span data-ttu-id="ff6be-140">**Uwaga**: Jeśli określone podkultury, takie jak `ja-JP` są niezbędne, zawsze używają identyfikatora języka wyższego poziomu, takiego jak `ja` .</span><span class="sxs-lookup"><span data-stu-id="ff6be-140">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="ff6be-141">W zestawie satelity program NuGet rozpozna **tylko** te pliki w folderze, które pasują do `{language}` nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="ff6be-141">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="ff6be-142">Wszystkie pozostałe są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="ff6be-142">All others are ignored.</span></span>

<span data-ttu-id="ff6be-143">Gdy zostaną spełnione wszystkie z tych konwencji, pakiet NuGet rozpoznaje go jako pakiet satelitarny i zainstaluje zlokalizowane pliki w folderze pakietu podstawowego `lib` , tak jakby były pierwotnie powiązane.</span><span class="sxs-lookup"><span data-stu-id="ff6be-143">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="ff6be-144">Odinstalowanie pakietu satelickiego spowoduje usunięcie jego plików z tego samego folderu.</span><span class="sxs-lookup"><span data-stu-id="ff6be-144">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="ff6be-145">W ten sam sposób można utworzyć dodatkowe zestawy satelickie dla każdego obsługiwanego języka.</span><span class="sxs-lookup"><span data-stu-id="ff6be-145">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="ff6be-146">Aby zapoznać się z przykładem, należy zapoznać się z zestawem pakietów ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="ff6be-146">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="ff6be-147">[Microsoft. ASPNET. MVC](https://nuget.org/packages/Microsoft.AspNet.Mvc) (podstawowa wersja angielskojęzyczna)</span><span class="sxs-lookup"><span data-stu-id="ff6be-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="ff6be-148">[Microsoft.ASPNET.MVC.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (niemiecki)</span><span class="sxs-lookup"><span data-stu-id="ff6be-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="ff6be-149">[Microsoft. ASPNET. MVC. ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japoński)</span><span class="sxs-lookup"><span data-stu-id="ff6be-149">[Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="ff6be-150">[Microsoft. ASPNET. MVC. zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (chiński (uproszczony))</span><span class="sxs-lookup"><span data-stu-id="ff6be-150">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="ff6be-151">[Microsoft. ASPNET. MVC. zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (chiński (tradycyjny))</span><span class="sxs-lookup"><span data-stu-id="ff6be-151">[Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="ff6be-152">Podsumowanie wymaganych Konwencji</span><span class="sxs-lookup"><span data-stu-id="ff6be-152">Summary of required conventions</span></span>

- <span data-ttu-id="ff6be-153">Pakiet podstawowy musi mieć nazwę `{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="ff6be-153">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="ff6be-154">Pakiet satelitarny musi mieć nazwę `{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="ff6be-154">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="ff6be-155">Pakiet satelitarny `.nuspec` musi określać swój język, aby odpowiadał nazwie pliku.</span><span class="sxs-lookup"><span data-stu-id="ff6be-155">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="ff6be-156">Pakiet satelitarny musi deklarować zależność dla dokładnej wersji elementu głównego przy użyciu notacji [] w `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="ff6be-156">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="ff6be-157">Zakresy nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="ff6be-157">Ranges are not supported.</span></span>
- <span data-ttu-id="ff6be-158">Pakiet satelitarny musi umieścić pliki w `lib\[{framework}\]{language}` folderze, który dokładnie pasuje do `{language}` nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="ff6be-158">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="ff6be-159">Zalety i wady (pakiety satelitarne)</span><span class="sxs-lookup"><span data-stu-id="ff6be-159">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="ff6be-160">Używanie pakietów satelitarnych ma kilka zalet:</span><span class="sxs-lookup"><span data-stu-id="ff6be-160">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="ff6be-161">**Rozmiar pakietu**: ogólny wpływ pakietu podstawowego jest zminimalizowany, a konsumenci ponoszą koszty każdego języka, którego chcą używać.</span><span class="sxs-lookup"><span data-stu-id="ff6be-161">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="ff6be-162">**Oddziel metadane**: każdy pakiet satelitarny ma własny `.nuspec` plik i dlatego jego własne zlokalizowane metadane.</span><span class="sxs-lookup"><span data-stu-id="ff6be-162">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="ff6be-163">Może to ułatwić klientom łatwiejsze znajdowanie pakietów przez wyszukiwanie nuget.org przy użyciu zlokalizowanych warunków.</span><span class="sxs-lookup"><span data-stu-id="ff6be-163">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="ff6be-164">Rozdzielone **wersje**: zestawy satelickie mogą być uwalniane z upływem czasu, a nie tylko na raz, co pozwala rozłożyć działania dotyczące lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="ff6be-164">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="ff6be-165">Jednak pakiety satelickie mają swój własny zestaw wad:</span><span class="sxs-lookup"><span data-stu-id="ff6be-165">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="ff6be-166">**Bałaganie**: zamiast pojedynczego pakietu masz wiele pakietów, które mogą prowadzić do nieczytelnych wyników wyszukiwania na NuGet.org i długiej listy odwołań w projekcie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ff6be-166">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="ff6be-167">**Ścisłe konwencje**.</span><span class="sxs-lookup"><span data-stu-id="ff6be-167">**Strict conventions**.</span></span> <span data-ttu-id="ff6be-168">Pakiety satelickie muszą być zgodne z konwencjami dokładnie lub zlokalizowane wersje nie będą prawidłowo pobierane.</span><span class="sxs-lookup"><span data-stu-id="ff6be-168">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="ff6be-169">**Przechowywanie wersji**: każdy pakiet satelitarny musi mieć dokładną zależność wersji w pakiecie podstawowym.</span><span class="sxs-lookup"><span data-stu-id="ff6be-169">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="ff6be-170">Oznacza to, że aktualizacja pakietu podstawowego może wymagać aktualizacji wszystkich pakietów satelitarnych, nawet jeśli zasoby nie uległy zmianie.</span><span class="sxs-lookup"><span data-stu-id="ff6be-170">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
