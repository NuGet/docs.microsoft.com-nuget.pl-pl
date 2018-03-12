---
title: "Odwołanie do pliku NuGet.Config. | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Odwołanie do pliku NuGet.Config łącznie z sekcji konfiguracji, bindingRedirects packageRestore, rozwiązanie i packageSource."
keywords: "Pliku NuGet.Config, NuGet konfiguracji odwołania, opcje konfiguracji NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c76ebcb06adc5e5b862647de6b6f4e19bde87b91
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/08/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="dc241-104">Odwołanie do pliku NuGet.Config.</span><span class="sxs-lookup"><span data-stu-id="dc241-104">NuGet.Config reference</span></span>

<span data-ttu-id="dc241-105">Zachowanie NuGet jest kontrolowane przez ustawienia w różnych `NuGet.Config` plików zgodnie z opisem w [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="dc241-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="dc241-106">`NuGet.Config` jest to plik XML zawierający najwyższego poziomu `<configuration>` węzła, który następnie zawiera elementy sekcji opisane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="dc241-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="dc241-107">Każda sekcja zawiera zero lub więcej `<add>` elementy o `key` i `value` atrybutów.</span><span class="sxs-lookup"><span data-stu-id="dc241-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="dc241-108">Zobacz [pliku konfiguracji przykłady](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="dc241-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="dc241-109">Ustawienie nazwy jest rozróżniana wielkość liter, a wartości można użyć [zmiennych środowiskowych](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="dc241-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="dc241-110">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="dc241-110">In this topic:</span></span>

- [<span data-ttu-id="dc241-111">Sekcja konfiguracyjna</span><span class="sxs-lookup"><span data-stu-id="dc241-111">config section</span></span>](#config-section)
- [<span data-ttu-id="dc241-112">sekcja bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="dc241-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="dc241-113">sekcja packageRestore</span><span class="sxs-lookup"><span data-stu-id="dc241-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="dc241-114">sekcji rozwiązania</span><span class="sxs-lookup"><span data-stu-id="dc241-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="dc241-115">[Pakiet sekcje źródła](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="dc241-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="dc241-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="dc241-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="dc241-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="dc241-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="dc241-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="dc241-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="dc241-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="dc241-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="dc241-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="dc241-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="dc241-121">Korzystanie ze zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="dc241-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="dc241-122">Przykładowy plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="dc241-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="dc241-123">Sekcja konfiguracyjna</span><span class="sxs-lookup"><span data-stu-id="dc241-123">config section</span></span>

<span data-ttu-id="dc241-124">Zawiera ustawienia dodatkowych konfiguracji, które można ustawić za pomocą [ `nuget config` polecenia](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="dc241-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="dc241-125">Uwaga: `dependencyVersion` i `repositoryPath` stosowania tylko dla projektów przy użyciu `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="dc241-125">Note: `dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="dc241-126">`globalPackagesFolder` dotyczy tylko projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="dc241-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="dc241-127">Key</span><span class="sxs-lookup"><span data-stu-id="dc241-127">Key</span></span> | <span data-ttu-id="dc241-128">Wartość</span><span class="sxs-lookup"><span data-stu-id="dc241-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="dc241-129">dependencyVersion (`packages.config` tylko)</span><span class="sxs-lookup"><span data-stu-id="dc241-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="dc241-130">Wartość domyślna `DependencyVersion` wartość instalacji pakietu, przywracania i aktualizacji, gdy `-DependencyVersion` przełącznik nie jest określony bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="dc241-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="dc241-131">Ta wartość jest także używana przez interfejs użytkownika Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="dc241-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="dc241-132">Wartości są `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="dc241-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="dc241-133">wartość globalPackagesFolder (projektów nie używa `packages.config`)</span><span class="sxs-lookup"><span data-stu-id="dc241-133">globalPackagesFolder (projects not using `packages.config`)</span></span> | <span data-ttu-id="dc241-134">Lokalizacja domyślny folder globalne pakietów.</span><span class="sxs-lookup"><span data-stu-id="dc241-134">The location of the default global packages folder.</span></span> <span data-ttu-id="dc241-135">Wartość domyślna to `%USERPROFILE%\.nuget\packages` (system Windows) lub `~/.nuget/packages` (system Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="dc241-135">The default is `%USERPROFILE%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="dc241-136">Ścieżka względna mogą być używane w specyficznego dla projektu `Nuget.Config` plików.</span><span class="sxs-lookup"><span data-stu-id="dc241-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="dc241-137">repositoryPath (`packages.config` tylko)</span><span class="sxs-lookup"><span data-stu-id="dc241-137">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="dc241-138">Lokalizacja, w którym można zainstalować pakietów NuGet, zamiast domyślnej `$(Solutiondir)/packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="dc241-138">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="dc241-139">Ścieżka względna mogą być używane w specyficznego dla projektu `Nuget.Config` plików.</span><span class="sxs-lookup"><span data-stu-id="dc241-139">A relative path can be used in project-specific `Nuget.Config` files.</span></span> |
| <span data-ttu-id="dc241-140">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="dc241-140">defaultPushSource</span></span> | <span data-ttu-id="dc241-141">Określa adres URL lub ścieżkę źródła pakietu, które mają być używane jako domyślne, jeśli inne źródła pakietu nie znaleziono dla operacji.</span><span class="sxs-lookup"><span data-stu-id="dc241-141">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="dc241-142">że http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="dc241-142">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="dc241-143">Ustawienia serwera proxy do użycia podczas połączenia ze źródła pakietów; `http_proxy` powinien być w formacie `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="dc241-143">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="dc241-144">Hasła są szyfrowane i nie można dodać ręcznie.</span><span class="sxs-lookup"><span data-stu-id="dc241-144">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="dc241-145">Aby uzyskać `no_proxy`, wartość jest rozdzielaną przecinkami listę domen obejścia serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="dc241-145">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="dc241-146">Można również używać zmiennych środowiskowych że i no_proxy, dla tych wartości.</span><span class="sxs-lookup"><span data-stu-id="dc241-146">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="dc241-147">Aby uzyskać więcej informacji, zobacz [ustawienia serwera proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="dc241-147">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="dc241-148">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="dc241-148">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="dc241-149">sekcja bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="dc241-149">bindingRedirects section</span></span>

<span data-ttu-id="dc241-150">Określa, czy NuGet nie przekierowania powiązania automatyczne, gdy jest zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="dc241-150">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="dc241-151">Key</span><span class="sxs-lookup"><span data-stu-id="dc241-151">Key</span></span> | <span data-ttu-id="dc241-152">Wartość</span><span class="sxs-lookup"><span data-stu-id="dc241-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="dc241-153">Pomiń</span><span class="sxs-lookup"><span data-stu-id="dc241-153">skip</span></span> | <span data-ttu-id="dc241-154">Wartość logiczna wskazująca, czy pominąć przekierowania powiązania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="dc241-154">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="dc241-155">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="dc241-155">The default is false.</span></span> |

<span data-ttu-id="dc241-156">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="dc241-156">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="dc241-157">sekcja packageRestore</span><span class="sxs-lookup"><span data-stu-id="dc241-157">packageRestore section</span></span>

<span data-ttu-id="dc241-158">*Ignorowane wszystkich bieżących wersji (2.7 +)*</span><span class="sxs-lookup"><span data-stu-id="dc241-158">*Ignored in all current versions (2.7+)*</span></span>

<span data-ttu-id="dc241-159">Formanty Przywracanie pakietów podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="dc241-159">Controls package restore during builds.</span></span>

| <span data-ttu-id="dc241-160">Key</span><span class="sxs-lookup"><span data-stu-id="dc241-160">Key</span></span> | <span data-ttu-id="dc241-161">Wartość</span><span class="sxs-lookup"><span data-stu-id="dc241-161">Value</span></span> |
| --- | --- |
| <span data-ttu-id="dc241-162">włączone</span><span class="sxs-lookup"><span data-stu-id="dc241-162">enabled</span></span> | <span data-ttu-id="dc241-163">Wartość logiczna wskazująca, czy NuGet można wykonać przywracania automatycznie.</span><span class="sxs-lookup"><span data-stu-id="dc241-163">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="dc241-164">Można również ustawić `EnableNuGetPackageRestore` zmienną środowiskową o wartości `True` zamiast ustawienie tego klucza w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dc241-164">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="dc241-165">automatyczne</span><span class="sxs-lookup"><span data-stu-id="dc241-165">automatic</span></span> | <span data-ttu-id="dc241-166">Wartość logiczna wskazująca, czy NuGet należy sprawdzić, czy brakujących pakietów podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="dc241-166">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="dc241-167">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="dc241-167">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="dc241-168">sekcji rozwiązania</span><span class="sxs-lookup"><span data-stu-id="dc241-168">solution section</span></span>

<span data-ttu-id="dc241-169">Formanty czy `packages` folderu rozwiązania jest uwzględniona w kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="dc241-169">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="dc241-170">W tej sekcji działa tylko w `Nuget.Config` pliki w folderze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="dc241-170">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="dc241-171">Key</span><span class="sxs-lookup"><span data-stu-id="dc241-171">Key</span></span> | <span data-ttu-id="dc241-172">Wartość</span><span class="sxs-lookup"><span data-stu-id="dc241-172">Value</span></span> |
| --- | --- |
| <span data-ttu-id="dc241-173">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="dc241-173">disableSourceControlIntegration</span></span> | <span data-ttu-id="dc241-174">Wartość logiczna wskazująca, czy Ignoruj folderu pakietów podczas pracy z kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="dc241-174">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="dc241-175">Wartość domyślna to false.</span><span class="sxs-lookup"><span data-stu-id="dc241-175">The default value is false.</span></span> |

<span data-ttu-id="dc241-176">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="dc241-176">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="dc241-177">Sekcje źródła pakietu</span><span class="sxs-lookup"><span data-stu-id="dc241-177">Package source sections</span></span>

<span data-ttu-id="dc241-178">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, I `disabledPackageSources` wszystkie działają razem, konfigurowanie, jak NuGet współpracuje z repozytoriów pakietu podczas instalacji, przywracania i operacje aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="dc241-178">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="dc241-179">[ `nuget sources` Polecenia](../tools/cli-ref-sources.md) jest zazwyczaj używany do zarządzania te ustawienia, z wyjątkiem `apikeys` której odbywa się przy użyciu [ `nuget setapikey` polecenia](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="dc241-179">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="dc241-180">Należy zauważyć, że adres URL źródła dla nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="dc241-180">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="dc241-181">packageSources</span><span class="sxs-lookup"><span data-stu-id="dc241-181">packageSources</span></span>

<span data-ttu-id="dc241-182">Wyświetla wszystkie źródła pakietów znane.</span><span class="sxs-lookup"><span data-stu-id="dc241-182">Lists all known package sources.</span></span> <span data-ttu-id="dc241-183">Kolejność jest ignorowany podczas operacji przywracania, a w przypadku projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="dc241-183">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="dc241-184">Kolejność źródeł instalacji szanuje NuGet i operacje aktualizacji z projektami za pomocą `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="dc241-184">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="dc241-185">Key</span><span class="sxs-lookup"><span data-stu-id="dc241-185">Key</span></span> | <span data-ttu-id="dc241-186">Wartość</span><span class="sxs-lookup"><span data-stu-id="dc241-186">Value</span></span> |
| --- | --- |
| <span data-ttu-id="dc241-187">(nazwa można przypisać do źródła pakietu)</span><span class="sxs-lookup"><span data-stu-id="dc241-187">(name to assign to the package source)</span></span> | <span data-ttu-id="dc241-188">Ścieżka lub adres URL źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="dc241-188">The path or URL of the package source.</span></span> |

<span data-ttu-id="dc241-189">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="dc241-189">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="dc241-190">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="dc241-190">packageSourceCredentials</span></span>

<span data-ttu-id="dc241-191">Przechowywane nazwy użytkowników i hasła dla źródeł, zazwyczaj określana z `-username` i `-password` zmienia z `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="dc241-191">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="dc241-192">Hasła są szyfrowane domyślnie, chyba że `-storepasswordincleartext` również używana jest opcja.</span><span class="sxs-lookup"><span data-stu-id="dc241-192">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="dc241-193">Key</span><span class="sxs-lookup"><span data-stu-id="dc241-193">Key</span></span> | <span data-ttu-id="dc241-194">Wartość</span><span class="sxs-lookup"><span data-stu-id="dc241-194">Value</span></span> |
| --- | --- |
| <span data-ttu-id="dc241-195">username</span><span class="sxs-lookup"><span data-stu-id="dc241-195">username</span></span> | <span data-ttu-id="dc241-196">Nazwa użytkownika dla źródła w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="dc241-196">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="dc241-197">Hasło</span><span class="sxs-lookup"><span data-stu-id="dc241-197">password</span></span> | <span data-ttu-id="dc241-198">Zaszyfrowane hasło dla tego źródła.</span><span class="sxs-lookup"><span data-stu-id="dc241-198">The encrypted password for the source.</span></span> |
| <span data-ttu-id="dc241-199">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="dc241-199">cleartextpassword</span></span> | <span data-ttu-id="dc241-200">Hasło nieszyfrowane źródła.</span><span class="sxs-lookup"><span data-stu-id="dc241-200">The unencrypted password for the source.</span></span> |

<span data-ttu-id="dc241-201">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="dc241-201">**Example:**</span></span>

<span data-ttu-id="dc241-202">W pliku konfiguracyjnym `<packageSourceCredentials>` element zawiera węzły podrzędne dla każdej nazwy odpowiednich źródła (spacje w nazwie są zastępowane `_x0020+`).</span><span class="sxs-lookup"><span data-stu-id="dc241-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020+`).</span></span> <span data-ttu-id="dc241-203">Oznacza to, że dla źródeł o nazwie "Contoso" i "Źródła testów", plik konfiguracji zawiera następujące przy użyciu hasła szyfrowane:</span><span class="sxs-lookup"><span data-stu-id="dc241-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="dc241-204">Podczas używania niezaszyfrowane hasła:</span><span class="sxs-lookup"><span data-stu-id="dc241-204">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="dc241-205">apikeys</span><span class="sxs-lookup"><span data-stu-id="dc241-205">apikeys</span></span>

<span data-ttu-id="dc241-206">Przechowuje klucze źródeł, które korzystają z uwierzytelniania klucza interfejsu API, zgodnie z [ `nuget setapikey` polecenia](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="dc241-206">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="dc241-207">Key</span><span class="sxs-lookup"><span data-stu-id="dc241-207">Key</span></span> | <span data-ttu-id="dc241-208">Wartość</span><span class="sxs-lookup"><span data-stu-id="dc241-208">Value</span></span> |
| --- | --- |
| <span data-ttu-id="dc241-209">(adres URL źródła)</span><span class="sxs-lookup"><span data-stu-id="dc241-209">(source URL)</span></span> | <span data-ttu-id="dc241-210">Zaszyfrowany klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="dc241-210">The encrypted API key.</span></span> |

<span data-ttu-id="dc241-211">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="dc241-211">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="dc241-212">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="dc241-212">disabledPackageSources</span></span>

<span data-ttu-id="dc241-213">Rozpoznane źródła aktualnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="dc241-213">Identified currently disabled sources.</span></span> <span data-ttu-id="dc241-214">Może być pusta.</span><span class="sxs-lookup"><span data-stu-id="dc241-214">May be empty.</span></span>

| <span data-ttu-id="dc241-215">Key</span><span class="sxs-lookup"><span data-stu-id="dc241-215">Key</span></span> | <span data-ttu-id="dc241-216">Wartość</span><span class="sxs-lookup"><span data-stu-id="dc241-216">Value</span></span> |
| --- | --- |
| <span data-ttu-id="dc241-217">(nazwa źródła)</span><span class="sxs-lookup"><span data-stu-id="dc241-217">(name of source)</span></span> | <span data-ttu-id="dc241-218">Wartość logiczna wskazująca, czy źródło jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="dc241-218">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="dc241-219">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="dc241-219">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="dc241-220">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="dc241-220">activePackageSource</span></span>

<span data-ttu-id="dc241-221">*(tylko 2.x; 3.x+ przestarzałe w)*</span><span class="sxs-lookup"><span data-stu-id="dc241-221">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="dc241-222">Identyfikuje do aktywnego źródła lub wskazuje agregacji wszystkich źródeł.</span><span class="sxs-lookup"><span data-stu-id="dc241-222">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="dc241-223">Key</span><span class="sxs-lookup"><span data-stu-id="dc241-223">Key</span></span> | <span data-ttu-id="dc241-224">Wartość</span><span class="sxs-lookup"><span data-stu-id="dc241-224">Value</span></span> |
| --- | --- |
| <span data-ttu-id="dc241-225">(nazwa źródła) lub `All`</span><span class="sxs-lookup"><span data-stu-id="dc241-225">(name of source) or `All`</span></span> | <span data-ttu-id="dc241-226">Jeśli klucz jest nazwę źródła, wartość jest ścieżka źródłowa lub adres URL.</span><span class="sxs-lookup"><span data-stu-id="dc241-226">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="dc241-227">Jeśli `All`, wartość powinna być `(Aggregate source)` połączyć wszystkie źródła pakietów, które nie zostały wyłączone w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="dc241-227">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="dc241-228">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="dc241-228">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="dc241-229">Korzystanie ze zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="dc241-229">Using environment variables</span></span>

<span data-ttu-id="dc241-230">Można używać zmiennych środowiskowych w `NuGet.Config` wartości (NuGet 3.4 +) w celu zastosowania ustawień w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="dc241-230">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="dc241-231">Na przykład jeśli `HOME` ustawiono zmiennej środowiskowej w systemie Windows `c:\users\username`, wartość `%HOME%\NuGetRepository` w konfiguracji pliku jest rozpoznawana jako `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="dc241-231">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="dc241-232">Podobnie jeśli `HOME` na system Mac/Linux jest ustawiona na `/home/myStuff`, następnie `$HOME/NuGetRepository` w konfiguracji pliku jest rozpoznawana jako `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="dc241-232">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="dc241-233">Jeśli zmienna środowiskowa nie zostanie znaleziony, NuGet korzysta z wartości literału z pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="dc241-233">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="dc241-234">Przykładowy plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="dc241-234">Example config file</span></span>

<span data-ttu-id="dc241-235">Poniżej znajduje się przykład `NuGet.Config` pliku, który przedstawia liczbę ustawień:</span><span class="sxs-lookup"><span data-stu-id="dc241-235">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
