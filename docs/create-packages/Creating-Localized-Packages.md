---
title: Tworzenie zlokalizowanego pakietu NuGet
description: Szczegółowe informacje na dwa sposoby tworzenia zlokalizowanych pakietów NuGet, w tym wszystkie zestawy w jednym pakiecie lub publikowania oddzielne zestawy.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: b1c2511c1fbafc7f52029c23521fa55671b0b5c5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546898"
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="a0ce7-103">Tworzenie zlokalizowanych pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="a0ce7-103">Creating localized NuGet packages</span></span>

<span data-ttu-id="a0ce7-104">Istnieją dwa sposoby tworzenia zlokalizowane wersje biblioteki:</span><span class="sxs-lookup"><span data-stu-id="a0ce7-104">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="a0ce7-105">Obejmują wszystkie zestawy zlokalizowanych zasobów w jednym pakiecie.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-105">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="a0ce7-106">Tworzenie pakietów oddzielne satelitarnej zlokalizowane postępując zgodnie z ograniczeniami zbiór konwencji.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-106">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="a0ce7-107">Obie metody mają swoje zalety i wady, zgodnie z opisem w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-107">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="a0ce7-108">Zestawów zlokalizowanych zasobów w jednym pakiecie</span><span class="sxs-lookup"><span data-stu-id="a0ce7-108">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="a0ce7-109">Dołączenie zestawów zlokalizowanych zasobów w jednym pakiecie zwykle jest najprostsza metoda.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-109">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="a0ce7-110">Aby to zrobić, należy utworzyć foldery znajdujące się w `lib` obsługiwanych języka innego niż domyślny pakiet (założono, że to en-us).</span><span class="sxs-lookup"><span data-stu-id="a0ce7-110">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="a0ce7-111">W tych folderach można umieścić zestawów zasobów i zlokalizowane pliki XML w technologii IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-111">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="a0ce7-112">Na przykład następującą strukturę folderów obsługuje, niemiecki (de), włoski (on), japoński (ja), rosyjski (ru), chiński (uproszczony) (zh-Hans) i chiński (tradycyjny) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="a0ce7-112">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

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

<span data-ttu-id="a0ce7-113">Widać, że języki są wszystkie wymienione poniżej `net40` folder struktury docelowej.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-113">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="a0ce7-114">Jeśli jesteś [Obsługa wielu platform](../create-packages/supporting-multiple-target-frameworks.md), wówczas masz folder w obszarze `lib` każdego wariantu.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-114">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="a0ce7-115">Za pomocą tych folderów w miejscu, następnie odwołać wszystkie pliki w Twojej `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="a0ce7-115">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

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

<span data-ttu-id="a0ce7-116">Jeden pakiet przykładowy, który korzysta z tej metody jest [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="a0ce7-116">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="a0ce7-117">Zalety i wady (zlokalizowany zasób zestawów)</span><span class="sxs-lookup"><span data-stu-id="a0ce7-117">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="a0ce7-118">Tworzenie pakietów we wszystkich językach, w jednym pakiecie ma kilka wady:</span><span class="sxs-lookup"><span data-stu-id="a0ce7-118">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="a0ce7-119">**Udostępnione metadanych**: ponieważ pakietu NuGet może zawierać tylko jeden `.nuspec` pliku, możesz podać metadanych tylko jeden język.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-119">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="a0ce7-120">Oznacza to, że w NuGet nie są wyświetlane obsługuje zlokalizowanych metadanych.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-120">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="a0ce7-121">**Rozmiar pakietu**: w zależności od liczby obsługiwanych języków, biblioteka może stać się znacznie dużych który spowalnia, instalowania i przywracania pakietu.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-121">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="a0ce7-122">**Wersje równoczesne**: tworzenie pakietów zlokalizowane pliki w jednym pakiecie wymaga wersji wszystkie zasoby w tym pakiecie jednocześnie, a nie jak zdołaliśmy oddzielnie każdej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-122">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="a0ce7-123">Ponadto wszelkich aktualizacji żadnych jednej lokalizacji wymaga nowej wersji cały pakiet.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-123">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="a0ce7-124">Jednak także ma kilka zalet:</span><span class="sxs-lookup"><span data-stu-id="a0ce7-124">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="a0ce7-125">**Prostota**: konsumentów pakietu Pobierz wszystkie obsługiwane języki w pojedyncza instalacja, niż musieć go zainstalować osobno każdy język.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-125">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="a0ce7-126">Pojedynczy pakiet jest również łatwiej znaleźć w witrynie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-126">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="a0ce7-127">**Powiązane wersje**: ponieważ wszystkie zestawy zasobów znajdują się w tym samym pakiecie jako podstawowego zestawu, wszystkie mają ten sam numer wersji i nie należy uruchamiać ryzyka błędnego wprowadzenie odłączone.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-127">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="a0ce7-128">Satelitarne zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="a0ce7-128">Localized satellite packages</span></span>

<span data-ttu-id="a0ce7-129">Podobnie jak program .NET Framework obsługuje zestawów satelickich, ta metoda oddziela zlokalizowanych zasobów i plików IntelliSense XML w pakiety satelity.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-129">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="a0ce7-130">Czy do tego, pakiet podstawowego używa konwencji nazewnictwa `{identifier}.{version}.nupkg` i zawiera zestaw dla języka domyślnego (np. en US).</span><span class="sxs-lookup"><span data-stu-id="a0ce7-130">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="a0ce7-131">Na przykład `ContosoUtilities.1.0.0.nupkg` będzie zawierał następującą strukturę:</span><span class="sxs-lookup"><span data-stu-id="a0ce7-131">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="a0ce7-132">Następnie zestawu satelickiego używa konwencji nazewnictwa `{identifier}.{language}.{version}.nupkg`, takich jak `ContosoUtilities.de.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-132">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="a0ce7-133">Identyfikator **musi** dokładnie odpowiadać pakiet główny.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-133">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="a0ce7-134">Ponieważ oddzielny pakiet ma swoje własne `.nuspec` pliku, który zawiera zlokalizowane metadanych.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-134">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="a0ce7-135">Można je na uwadze, język, w `.nuspec` **musi** zgodne z działaniem używanym w nazwie pliku.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-135">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="a0ce7-136">Zestawu satelickiego **musi** deklarować dokładnej wersji głównej pakietu także jako zależności, przy użyciu notacji wersji [] \(zobacz [wersji pakietu](../reference/package-versioning.md)).</span><span class="sxs-lookup"><span data-stu-id="a0ce7-136">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../reference/package-versioning.md)).</span></span> <span data-ttu-id="a0ce7-137">Na przykład `ContosoUtilities.de.1.0.0.nupkg` należy zadeklarować zależność w `ContosoUtilities.1.0.0.nupkg` przy użyciu `[1.0.0]` notacji.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-137">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="a0ce7-138">Pakiet satelitarnej oczywiście mogą mieć numer wersji innej niż pakiet główny.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-138">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="a0ce7-139">Struktura pakietu satelitarnej następnie mogą zawierać zestaw zasobów i plik XML IntelliSense w podfolderze, który odpowiada `{language}` w nazwie pliku pakietu:</span><span class="sxs-lookup"><span data-stu-id="a0ce7-139">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="a0ce7-140">**Uwaga**: chyba że określone podhodowli, takie jak `ja-JP` są niezbędne, zawsze używaj wyższe identyfikatora języka poziomu, takie jak `ja`.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-140">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="a0ce7-141">W zestawie satelickim rozpozna NuGet **tylko** tych plików w folderze, który odpowiada `{language}` w nazwie pliku.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-141">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="a0ce7-142">Wszystkie pozostałe są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-142">All others are ignored.</span></span>

<span data-ttu-id="a0ce7-143">Po spełnieniu wszystkich tych konwencji NuGet rozpozna pakietu jako pakiet satelitarne i instalowanie zlokalizowanych plików w pakiecie głównej `lib` folderze tak, jakby były one pierwotnie powiązane.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-143">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="a0ce7-144">Odinstalowywanie pakietu satelitarnej spowoduje usunięcie jej pliki z tym samym folderze.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-144">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="a0ce7-145">Należy utworzyć dodatkowe zestawy satelickie w taki sam sposób dla każdego z obsługiwanych języków.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-145">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="a0ce7-146">Na przykład sprawdzić zestaw pakietów platformy ASP.NET MVC:</span><span class="sxs-lookup"><span data-stu-id="a0ce7-146">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="a0ce7-147">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (podstawowy w języku angielskim)</span><span class="sxs-lookup"><span data-stu-id="a0ce7-147">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="a0ce7-148">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (wersja niemiecka)</span><span class="sxs-lookup"><span data-stu-id="a0ce7-148">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="a0ce7-149">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span><span class="sxs-lookup"><span data-stu-id="a0ce7-149">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="a0ce7-150">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span><span class="sxs-lookup"><span data-stu-id="a0ce7-150">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="a0ce7-151">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span><span class="sxs-lookup"><span data-stu-id="a0ce7-151">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="a0ce7-152">Podsumowanie konwencje wymagane</span><span class="sxs-lookup"><span data-stu-id="a0ce7-152">Summary of required conventions</span></span>

- <span data-ttu-id="a0ce7-153">Pakiet główny musi mieć nazwę. `{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="a0ce7-153">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="a0ce7-154">Pakiet satelitarnej musi mieć nazwę. `{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="a0ce7-154">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="a0ce7-155">Pakiet satelitarnej `.nuspec` należy określić jego język, aby dopasować nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-155">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="a0ce7-156">Pakiet satelitarnej należy zadeklarować zależność w dokładną wersję podstawową przy użyciu notacji [] w jego `.nuspec` pliku.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-156">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="a0ce7-157">Zakresy nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-157">Ranges are not supported.</span></span>
- <span data-ttu-id="a0ce7-158">Pakiet satelitarnej należy umieścić pliki w `lib\[{framework}\]{language}` folder, który dokładnie pasuje `{language}` w nazwie pliku.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-158">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="a0ce7-159">Zalety i wady (satelitarnej pakietów)</span><span class="sxs-lookup"><span data-stu-id="a0ce7-159">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="a0ce7-160">Za pomocą pakietów satelitarnej ma kilka zalet:</span><span class="sxs-lookup"><span data-stu-id="a0ce7-160">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="a0ce7-161">**Rozmiar pakietu**: całkowitego rozmiaru pakietu podstawowego jest zminimalizowany i konsumentów tylko pociągnąć za sobą koszty każdego języka, które mają być użyte.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-161">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="a0ce7-162">**Oddzielne metadanych**: każdy pakiet satelitarnej ma swój własny `.nuspec` pliku, a zatem zlokalizowanych metadanych ponieważ.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-162">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="a0ce7-163">Dzięki temu części użytkowników łatwiej znaleźć pakiety, wyszukując nuget.org zlokalizowane warunki.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-163">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="a0ce7-164">**Odłączone wersji**: zestawy satelickie może być zwolnione wraz z upływem czasu, a nie w całości, umożliwiając rozłożyć prace lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-164">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="a0ce7-165">Jednak pakiety satelitarnej mają własne zestawy wady:</span><span class="sxs-lookup"><span data-stu-id="a0ce7-165">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="a0ce7-166">**Zaśmiecania**: zamiast jeden pakiet, masz wiele pakietów, które mogą prowadzić do dużej liczby wyników w witrynach nuget.org i długą listę odwołań w projekcie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-166">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="a0ce7-167">**Konwencje Strict**.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-167">**Strict conventions**.</span></span> <span data-ttu-id="a0ce7-168">Pakiety satelitarnej muszą dokładnie zgodne z konwencjami lub zlokalizowane wersje nie będą pobrane prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-168">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="a0ce7-169">**Przechowywanie wersji**: każdy pakiet satelitarnej musi mieć zależność dokładnie wersji na pakiet główny.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-169">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="a0ce7-170">Oznacza to, że aktualizowanie pakietu głównej mogą wymagać aktualizacji wszystkich pakietów satelity, nawet wtedy, gdy zasoby nie został zmieniony.</span><span class="sxs-lookup"><span data-stu-id="a0ce7-170">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
