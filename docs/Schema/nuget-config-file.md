---
title: "Odwołanie do pliku NuGet.Config. | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: fbf31530-3bf4-478c-b26c-c2b24dd3406d
description: "Odwołanie do pliku NuGet.Config łącznie z sekcji konfiguracji, bindingRedirects packageRestore, rozwiązanie i packageSource."
keywords: "Pliku NuGet.Config, NuGet konfiguracji odwołania, opcje konfiguracji NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 830c622f622b894a228b18dfdb3a790bccfde8a3
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/10/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="7a3b5-104">Odwołanie do pliku NuGet.Config.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-104">NuGet.Config reference</span></span>

<span data-ttu-id="7a3b5-105">Zachowanie NuGet jest kontrolowane przez ustawienia w różnych `NuGet.Config` plików zgodnie z opisem w [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="7a3b5-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="7a3b5-106">`NuGet.Config`jest to plik XML zawierający najwyższego poziomu `<configuration>` węzła, który następnie zawiera elementy sekcji opisane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="7a3b5-107">Każda sekcja zawiera zero lub więcej `<add>` elementy o `key` i `value` atrybutów.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="7a3b5-108">Zobacz [pliku konfiguracji przykłady](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="7a3b5-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="7a3b5-109">Ustawienie nazwy jest rozróżniana wielkość liter, a wartości można użyć [zmiennych środowiskowych](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="7a3b5-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="7a3b5-110">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="7a3b5-110">In this topic:</span></span>

- [<span data-ttu-id="7a3b5-111">Sekcja konfiguracyjna</span><span class="sxs-lookup"><span data-stu-id="7a3b5-111">config section</span></span>](#config-section)
- [<span data-ttu-id="7a3b5-112">sekcja bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="7a3b5-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="7a3b5-113">sekcja packageRestore</span><span class="sxs-lookup"><span data-stu-id="7a3b5-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="7a3b5-114">sekcji rozwiązania</span><span class="sxs-lookup"><span data-stu-id="7a3b5-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="7a3b5-115">[Pakiet sekcje źródła](#package-source-sections): - [packageSources](#packagesources)</span><span class="sxs-lookup"><span data-stu-id="7a3b5-115">[Package source sections](#package-source-sections): -[packageSources](#packagesources)</span></span>
  - [<span data-ttu-id="7a3b5-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="7a3b5-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="7a3b5-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="7a3b5-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="7a3b5-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="7a3b5-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="7a3b5-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="7a3b5-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="7a3b5-120">Korzystanie ze zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="7a3b5-120">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="7a3b5-121">Przykładowy plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="7a3b5-121">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="7a3b5-122">Sekcja konfiguracyjna</span><span class="sxs-lookup"><span data-stu-id="7a3b5-122">config section</span></span>

<span data-ttu-id="7a3b5-123">Zawiera ustawienia dodatkowych konfiguracji, które można ustawić za pomocą [ `nuget config` polecenia](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="7a3b5-123">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="7a3b5-124">Uwaga: `dependencyVersion` i `repositoryPath` stosowania tylko dla projektów przy użyciu `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-124">Note: `dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="7a3b5-125">`globalPackagesFolder`dotyczy tylko projektów przy użyciu `project.json` i PackageReference formatach.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-125">`globalPackagesFolder` applies only to projects using `project.json` and PackageReference formats.</span></span>

| <span data-ttu-id="7a3b5-126">Key</span><span class="sxs-lookup"><span data-stu-id="7a3b5-126">Key</span></span> | <span data-ttu-id="7a3b5-127">Wartość</span><span class="sxs-lookup"><span data-stu-id="7a3b5-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7a3b5-128">dependencyVersion (`packages.config` tylko)</span><span class="sxs-lookup"><span data-stu-id="7a3b5-128">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="7a3b5-129">Wartość domyślna `DependencyVersion` wartość instalacji pakietu, przywracania i aktualizacji, gdy `-DependencyVersion` przełącznik nie jest określony bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-129">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="7a3b5-130">Ta wartość jest także używana przez interfejs użytkownika Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-130">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="7a3b5-131">Wartości są `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-131">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="7a3b5-132">wartość globalPackagesFolder (projektów nie używa `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="7a3b5-132">globalPackagesFolder (projects not using `packages.config`)</span></span> | <span data-ttu-id="7a3b5-133">Lokalizacja domyślny folder globalne pakietów.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-133">The location of the default global packages folder.</span></span> <span data-ttu-id="7a3b5-134">Wartość domyślna to `%USERPROFILE%\.nuget\packages` (system Windows) lub `~/.nuget/packages` (system Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="7a3b5-134">The default is `%USERPROFILE%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="7a3b5-135">Ścieżka względna mogą być używane w specyficznego dla projektu `Nuget.Config` plików.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-135">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="7a3b5-136">repositoryPath (`packages.config` tylko)</span><span class="sxs-lookup"><span data-stu-id="7a3b5-136">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="7a3b5-137">Lokalizacja, w którym można zainstalować pakietów NuGet, zamiast domyślnej `$(Solutiondir)/packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-137">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="7a3b5-138">Ścieżka względna mogą być używane w specyficznego dla projektu `Nuget.Config` plików.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-138">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="7a3b5-139">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="7a3b5-139">defaultPushSource</span></span> | <span data-ttu-id="7a3b5-140">Określa adres URL lub ścieżkę źródła pakietu, które mają być używane jako domyślne, jeśli inne źródła pakietu nie znaleziono dla operacji.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-140">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="7a3b5-141">że http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="7a3b5-141">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="7a3b5-142">Ustawienia serwera proxy do użycia podczas połączenia ze źródła pakietów; `http_proxy` powinien być w formacie `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-142">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="7a3b5-143">Hasła są szyfrowane i nie można dodać ręcznie.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-143">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="7a3b5-144">Aby uzyskać `no_proxy`, wartość jest rozdzielaną przecinkami listę domen obejścia serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-144">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="7a3b5-145">Można również używać zmiennych środowiskowych że i no_proxy, dla tych wartości.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-145">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="7a3b5-146">Aby uzyskać więcej informacji, zobacz [ustawienia serwera proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="7a3b5-146">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="7a3b5-147">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="7a3b5-147">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="7a3b5-148">sekcja bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="7a3b5-148">bindingRedirects section</span></span>

<span data-ttu-id="7a3b5-149">Określa, czy NuGet nie przekierowania powiązania automatyczne, gdy jest zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-149">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="7a3b5-150">Key</span><span class="sxs-lookup"><span data-stu-id="7a3b5-150">Key</span></span> | <span data-ttu-id="7a3b5-151">Wartość</span><span class="sxs-lookup"><span data-stu-id="7a3b5-151">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7a3b5-152">Pomiń</span><span class="sxs-lookup"><span data-stu-id="7a3b5-152">skip</span></span> | <span data-ttu-id="7a3b5-153">Wartość logiczna wskazująca, czy pominąć przekierowania powiązania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-153">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="7a3b5-154">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-154">The default is false.</span></span> |

<span data-ttu-id="7a3b5-155">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="7a3b5-155">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="7a3b5-156">sekcja packageRestore</span><span class="sxs-lookup"><span data-stu-id="7a3b5-156">packageRestore section</span></span>

<span data-ttu-id="7a3b5-157">*Ignorowane w 2.7 +*</span><span class="sxs-lookup"><span data-stu-id="7a3b5-157">*Ignored in 2.7+*</span></span>

<span data-ttu-id="7a3b5-158">Formanty Przywracanie pakietów podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-158">Controls package restore during builds.</span></span>

| <span data-ttu-id="7a3b5-159">Key</span><span class="sxs-lookup"><span data-stu-id="7a3b5-159">Key</span></span> | <span data-ttu-id="7a3b5-160">Wartość</span><span class="sxs-lookup"><span data-stu-id="7a3b5-160">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7a3b5-161">włączone</span><span class="sxs-lookup"><span data-stu-id="7a3b5-161">enabled</span></span> | <span data-ttu-id="7a3b5-162">Wartość logiczna wskazująca, czy NuGet można wykonać przywracania automatycznie.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-162">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="7a3b5-163">Można również ustawić `EnableNuGetPackageRestore` zmienną środowiskową o wartości `True` zamiast ustawienie tego klucza w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-163">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="7a3b5-164">automatyczne</span><span class="sxs-lookup"><span data-stu-id="7a3b5-164">automatic</span></span> | <span data-ttu-id="7a3b5-165">Wartość logiczna wskazująca, czy NuGet należy sprawdzić, czy brakujących pakietów podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-165">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="7a3b5-166">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="7a3b5-166">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="7a3b5-167">sekcji rozwiązania</span><span class="sxs-lookup"><span data-stu-id="7a3b5-167">solution section</span></span>

<span data-ttu-id="7a3b5-168">Formanty czy `packages` folderu rozwiązania jest uwzględniona w kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-168">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="7a3b5-169">W tej sekcji działa tylko w `Nuget.Config` pliki w folderze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-169">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="7a3b5-170">Key</span><span class="sxs-lookup"><span data-stu-id="7a3b5-170">Key</span></span> | <span data-ttu-id="7a3b5-171">Wartość</span><span class="sxs-lookup"><span data-stu-id="7a3b5-171">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7a3b5-172">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="7a3b5-172">disableSourceControlIntegration</span></span> | <span data-ttu-id="7a3b5-173">Wartość logiczna wskazująca, czy Ignoruj folderu pakietów podczas pracy z kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-173">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="7a3b5-174">Wartość domyślna to false.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-174">The default value is false.</span></span> |

<span data-ttu-id="7a3b5-175">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="7a3b5-175">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="7a3b5-176">Sekcje źródła pakietu</span><span class="sxs-lookup"><span data-stu-id="7a3b5-176">Package source sections</span></span>

<span data-ttu-id="7a3b5-177">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, I `disabledPackageSources` wszystkie działają razem, konfigurowanie, jak NuGet współpracuje z repozytoriów pakietu podczas instalacji, przywracania i operacje aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-177">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="7a3b5-178">[ `nuget sources` Polecenia](../tools/cli-ref-sources.md) jest zazwyczaj używany do zarządzania te ustawienia, z wyjątkiem `apikeys` której odbywa się przy użyciu [ `nuget setapikey` polecenia](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="7a3b5-178">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="7a3b5-179">Należy zauważyć, że adres URL źródła dla nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-179">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="7a3b5-180">packageSources</span><span class="sxs-lookup"><span data-stu-id="7a3b5-180">packageSources</span></span>

<span data-ttu-id="7a3b5-181">Wyświetla wszystkie źródła pakietów znane.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-181">Lists all known package sources.</span></span>

| <span data-ttu-id="7a3b5-182">Key</span><span class="sxs-lookup"><span data-stu-id="7a3b5-182">Key</span></span> | <span data-ttu-id="7a3b5-183">Wartość</span><span class="sxs-lookup"><span data-stu-id="7a3b5-183">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7a3b5-184">(nazwa można przypisać do źródła pakietu)</span><span class="sxs-lookup"><span data-stu-id="7a3b5-184">(name to assign to the package source)</span></span> | <span data-ttu-id="7a3b5-185">Ścieżka lub adres URL źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-185">The path or URL of the package source.</span></span> |

<span data-ttu-id="7a3b5-186">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="7a3b5-186">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="7a3b5-187">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="7a3b5-187">packageSourceCredentials</span></span>

<span data-ttu-id="7a3b5-188">Przechowywane nazwy użytkowników i hasła dla źródeł, zazwyczaj określana z `-username` i `-password` zmienia z `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-188">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="7a3b5-189">Hasła są szyfrowane domyślnie, chyba że `-storepasswordincleartext` również używana jest opcja.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-189">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="7a3b5-190">Key</span><span class="sxs-lookup"><span data-stu-id="7a3b5-190">Key</span></span> | <span data-ttu-id="7a3b5-191">Wartość</span><span class="sxs-lookup"><span data-stu-id="7a3b5-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7a3b5-192">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="7a3b5-192">username</span></span> | <span data-ttu-id="7a3b5-193">Nazwa użytkownika dla źródła w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-193">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="7a3b5-194">Hasło</span><span class="sxs-lookup"><span data-stu-id="7a3b5-194">password</span></span> | <span data-ttu-id="7a3b5-195">Zaszyfrowane hasło dla tego źródła.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-195">The encrypted password for the source.</span></span> |
| <span data-ttu-id="7a3b5-196">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="7a3b5-196">cleartextpassword</span></span> | <span data-ttu-id="7a3b5-197">Hasło nieszyfrowane źródła.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-197">The unencrypted password for the source.</span></span> |

<span data-ttu-id="7a3b5-198">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="7a3b5-198">**Example:**</span></span>

<span data-ttu-id="7a3b5-199">W pliku konfiguracyjnym `<packageSourceCredentials>` element zawiera węzły podrzędne dla każdej nazwy odpowiednich źródła (spacje w nazwie są zastępowane `_x0020+`).</span><span class="sxs-lookup"><span data-stu-id="7a3b5-199">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020+`).</span></span> <span data-ttu-id="7a3b5-200">Oznacza to, że dla źródeł o nazwie "Contoso" i "Źródła testów", plik konfiguracji zawiera następujące przy użyciu hasła szyfrowane:</span><span class="sxs-lookup"><span data-stu-id="7a3b5-200">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="7a3b5-201">Podczas używania niezaszyfrowane hasła:</span><span class="sxs-lookup"><span data-stu-id="7a3b5-201">When using unencrypted passwords:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="7a3b5-202">apikeys</span><span class="sxs-lookup"><span data-stu-id="7a3b5-202">apikeys</span></span>

<span data-ttu-id="7a3b5-203">Przechowuje klucze źródeł, które korzystają z uwierzytelniania klucza interfejsu API, zgodnie z [ `nuget setapikey` polecenia](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="7a3b5-203">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="7a3b5-204">Key</span><span class="sxs-lookup"><span data-stu-id="7a3b5-204">Key</span></span> | <span data-ttu-id="7a3b5-205">Wartość</span><span class="sxs-lookup"><span data-stu-id="7a3b5-205">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7a3b5-206">(adres URL źródła)</span><span class="sxs-lookup"><span data-stu-id="7a3b5-206">(source URL)</span></span> | <span data-ttu-id="7a3b5-207">Zaszyfrowany klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-207">The encrypted API key.</span></span> |

<span data-ttu-id="7a3b5-208">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="7a3b5-208">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="7a3b5-209">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="7a3b5-209">disabledPackageSources</span></span>

<span data-ttu-id="7a3b5-210">Rozpoznane źródła aktualnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-210">Identified currently disabled sources.</span></span> <span data-ttu-id="7a3b5-211">Może być pusta.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-211">May be empty.</span></span>

| <span data-ttu-id="7a3b5-212">Key</span><span class="sxs-lookup"><span data-stu-id="7a3b5-212">Key</span></span> | <span data-ttu-id="7a3b5-213">Wartość</span><span class="sxs-lookup"><span data-stu-id="7a3b5-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7a3b5-214">(nazwa źródła)</span><span class="sxs-lookup"><span data-stu-id="7a3b5-214">(name of source)</span></span> | <span data-ttu-id="7a3b5-215">Wartość logiczna wskazująca, czy źródło jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-215">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="7a3b5-216">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="7a3b5-216">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="7a3b5-217">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="7a3b5-217">activePackageSource</span></span>

<span data-ttu-id="7a3b5-218">*(tylko 2.x; 3.x+ przestarzałe w)*</span><span class="sxs-lookup"><span data-stu-id="7a3b5-218">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="7a3b5-219">Identyfikuje do aktywnego źródła lub wskazuje agregacji wszystkich źródeł.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-219">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="7a3b5-220">Key</span><span class="sxs-lookup"><span data-stu-id="7a3b5-220">Key</span></span> | <span data-ttu-id="7a3b5-221">Wartość</span><span class="sxs-lookup"><span data-stu-id="7a3b5-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="7a3b5-222">(nazwa źródła) lub`All`</span><span class="sxs-lookup"><span data-stu-id="7a3b5-222">(name of source) or `All`</span></span> | <span data-ttu-id="7a3b5-223">Jeśli klucz jest nazwę źródła, wartość jest ścieżka źródłowa lub adres URL.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-223">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="7a3b5-224">Jeśli `All`, wartość powinna być `(Aggregate source)` połączyć wszystkie źródła pakietów, które nie zostały wyłączone w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-224">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="7a3b5-225">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="7a3b5-225">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="7a3b5-226">Korzystanie ze zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="7a3b5-226">Using environment variables</span></span>

<span data-ttu-id="7a3b5-227">Można używać zmiennych środowiskowych w `NuGet.Config` wartości (NuGet 3.4 +) w celu zastosowania ustawień w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-227">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="7a3b5-228">Na przykład jeśli `HOME` ustawiono zmiennej środowiskowej w systemie Windows `c:\users\username`, wartość `%HOME%\NuGetRepository` w konfiguracji pliku jest rozpoznawana jako `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-228">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="7a3b5-229">Podobnie jeśli `HOME` na system Mac/Linux jest ustawiona na `/home/myStuff`, następnie `$HOME/NuGetRepository` w konfiguracji pliku jest rozpoznawana jako `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-229">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="7a3b5-230">Jeśli zmienna środowiskowa nie zostanie znaleziony, NuGet korzysta z wartości literału z pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7a3b5-230">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="7a3b5-231">Przykładowy plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="7a3b5-231">Example config file</span></span>

<span data-ttu-id="7a3b5-232">Poniżej znajduje się przykład `NuGet.Config` pliku, który przedstawia liczbę ustawień:</span><span class="sxs-lookup"><span data-stu-id="7a3b5-232">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>
</configuration>
```
