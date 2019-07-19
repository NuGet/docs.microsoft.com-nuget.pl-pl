---
title: Dokumentacja pliku NuGet. config
description: Odwołanie do pliku NuGet. config, w tym sekcje config, bindingRedirects, packageRestore, Solution i packageSource.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: b03bb8da0191a679671e5898ac70fff2024d52f2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317219"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="a6a88-103">Dokumentacja NuGet. config</span><span class="sxs-lookup"><span data-stu-id="a6a88-103">nuget.config reference</span></span>

<span data-ttu-id="a6a88-104">Zachowanie NuGet jest kontrolowane przez ustawienia w różnych `NuGet.Config` plikach, zgodnie z opisem w temacie [typowe konfiguracje programu NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="a6a88-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="a6a88-105">`nuget.config`jest plikiem XML zawierającym węzeł najwyższego `<configuration>` poziomu, który zawiera elementy sekcji opisane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="a6a88-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="a6a88-106">Każda sekcja zawiera zero lub więcej elementów.</span><span class="sxs-lookup"><span data-stu-id="a6a88-106">Each section contains zero or more items.</span></span> <span data-ttu-id="a6a88-107">Zobacz [przykład pliku konfiguracji](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="a6a88-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="a6a88-108">W nazwach ustawień jest rozróżniana wielkość liter, a wartości mogą używać [zmiennych środowiskowych](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="a6a88-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="a6a88-109">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="a6a88-109">In this topic:</span></span>

- [<span data-ttu-id="a6a88-110">sekcja konfiguracji</span><span class="sxs-lookup"><span data-stu-id="a6a88-110">config section</span></span>](#config-section)
- [<span data-ttu-id="a6a88-111">Sekcja bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="a6a88-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="a6a88-112">Sekcja packageRestore</span><span class="sxs-lookup"><span data-stu-id="a6a88-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="a6a88-113">Sekcja rozwiązania</span><span class="sxs-lookup"><span data-stu-id="a6a88-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="a6a88-114">[Sekcje źródłowe pakietu](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="a6a88-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="a6a88-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="a6a88-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="a6a88-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="a6a88-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="a6a88-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="a6a88-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="a6a88-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="a6a88-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="a6a88-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="a6a88-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="a6a88-120">Sekcja trustedSigners</span><span class="sxs-lookup"><span data-stu-id="a6a88-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="a6a88-121">Korzystanie ze zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="a6a88-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="a6a88-122">Przykładowy plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="a6a88-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="a6a88-123">sekcja konfiguracji</span><span class="sxs-lookup"><span data-stu-id="a6a88-123">config section</span></span>

<span data-ttu-id="a6a88-124">Zawiera różne ustawienia konfiguracji, które można ustawić za pomocą [ `nuget config` polecenia](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="a6a88-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="a6a88-125">`dependencyVersion`i `repositoryPath` mają zastosowanie tylko do projektów `packages.config`korzystających z programu.</span><span class="sxs-lookup"><span data-stu-id="a6a88-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="a6a88-126">`globalPackagesFolder`dotyczy tylko projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="a6a88-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="a6a88-127">Key</span><span class="sxs-lookup"><span data-stu-id="a6a88-127">Key</span></span> | <span data-ttu-id="a6a88-128">Wartość</span><span class="sxs-lookup"><span data-stu-id="a6a88-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a6a88-129">dependencyVersion (`packages.config` tylko)</span><span class="sxs-lookup"><span data-stu-id="a6a88-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="a6a88-130">Wartość domyślna `DependencyVersion` instalacji, przywracania i aktualizacji pakietu, `-DependencyVersion` gdy przełącznik nie jest określony bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="a6a88-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="a6a88-131">Ta wartość jest również używana przez interfejs użytkownika Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="a6a88-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="a6a88-132">Wartości to `Lowest` `HighestPatch` ,,`Highest`, `HighestMinor`.</span><span class="sxs-lookup"><span data-stu-id="a6a88-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="a6a88-133">globalPackagesFolder (projekty korzystające tylko z PackageReference)</span><span class="sxs-lookup"><span data-stu-id="a6a88-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="a6a88-134">Lokalizacja domyślnego folderu pakiety globalne.</span><span class="sxs-lookup"><span data-stu-id="a6a88-134">The location of the default global packages folder.</span></span> <span data-ttu-id="a6a88-135">Wartość domyślna to `%userprofile%\.nuget\packages` (Windows) lub `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="a6a88-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="a6a88-136">Ścieżka względna może być używana w plikach specyficznych `nuget.config` dla projektu.</span><span class="sxs-lookup"><span data-stu-id="a6a88-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="a6a88-137">To ustawienie jest zastępowane przez zmienną środowiskową NUGET_PACKAGES, która ma pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="a6a88-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="a6a88-138">repositoryPath (`packages.config` tylko)</span><span class="sxs-lookup"><span data-stu-id="a6a88-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="a6a88-139">Lokalizacja, w której mają zostać zainstalowane pakiety NuGet zamiast folderu domyślnego `$(Solutiondir)/packages` .</span><span class="sxs-lookup"><span data-stu-id="a6a88-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="a6a88-140">Ścieżka względna może być używana w plikach specyficznych `nuget.config` dla projektu.</span><span class="sxs-lookup"><span data-stu-id="a6a88-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="a6a88-141">To ustawienie jest zastępowane przez zmienną środowiskową NUGET_PACKAGES, która ma pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="a6a88-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="a6a88-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="a6a88-142">defaultPushSource</span></span> | <span data-ttu-id="a6a88-143">Określa adres URL lub ścieżkę źródła pakietu, które ma być używane jako wartość domyślna, jeśli nie znaleziono żadnych innych źródeł pakietów dla operacji.</span><span class="sxs-lookup"><span data-stu-id="a6a88-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="a6a88-144">http_proxy http_proxy. User http_proxy. Password no_proxy</span><span class="sxs-lookup"><span data-stu-id="a6a88-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="a6a88-145">Ustawienia serwera proxy do użycia podczas nawiązywania połączenia ze źródłami pakietów; powinien mieć format `http://<username>:<password>@<domain>`. `http_proxy`</span><span class="sxs-lookup"><span data-stu-id="a6a88-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="a6a88-146">Hasła są szyfrowane i nie można ich dodać ręcznie.</span><span class="sxs-lookup"><span data-stu-id="a6a88-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="a6a88-147">W `no_proxy`przypadku, wartość jest rozdzielaną przecinkami listą domen, które pomijają serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="a6a88-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="a6a88-148">Dla tych wartości można użyć zmiennych środowiskowych http_proxy i no_proxy.</span><span class="sxs-lookup"><span data-stu-id="a6a88-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="a6a88-149">Aby uzyskać więcej informacji, zobacz [Ustawienia serwera proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="a6a88-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="a6a88-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="a6a88-150">signatureValidationMode</span></span> | <span data-ttu-id="a6a88-151">Określa tryb weryfikacji używany do weryfikowania podpisów pakietów na potrzeby instalacji pakietu i przywracania.</span><span class="sxs-lookup"><span data-stu-id="a6a88-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="a6a88-152">Wartości to `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="a6a88-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="a6a88-153">Wartość domyślna to `accept`.</span><span class="sxs-lookup"><span data-stu-id="a6a88-153">Defaults to `accept`.</span></span>

<span data-ttu-id="a6a88-154">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a6a88-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="a6a88-155">Sekcja bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="a6a88-155">bindingRedirects section</span></span>

<span data-ttu-id="a6a88-156">Określa, czy program NuGet ma przekierować automatyczne powiązania po zainstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="a6a88-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="a6a88-157">Key</span><span class="sxs-lookup"><span data-stu-id="a6a88-157">Key</span></span> | <span data-ttu-id="a6a88-158">Wartość</span><span class="sxs-lookup"><span data-stu-id="a6a88-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a6a88-159">Pomiń</span><span class="sxs-lookup"><span data-stu-id="a6a88-159">skip</span></span> | <span data-ttu-id="a6a88-160">Wartość logiczna wskazująca, czy pomijać Automatyczne przekierowania powiązań.</span><span class="sxs-lookup"><span data-stu-id="a6a88-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="a6a88-161">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="a6a88-161">The default is false.</span></span> |

<span data-ttu-id="a6a88-162">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a6a88-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="a6a88-163">Sekcja packageRestore</span><span class="sxs-lookup"><span data-stu-id="a6a88-163">packageRestore section</span></span>

<span data-ttu-id="a6a88-164">Kontroluje przywracanie pakietu podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a6a88-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="a6a88-165">Key</span><span class="sxs-lookup"><span data-stu-id="a6a88-165">Key</span></span> | <span data-ttu-id="a6a88-166">Wartość</span><span class="sxs-lookup"><span data-stu-id="a6a88-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a6a88-167">Dostępny</span><span class="sxs-lookup"><span data-stu-id="a6a88-167">enabled</span></span> | <span data-ttu-id="a6a88-168">Wartość logiczna wskazująca, czy pakiet NuGet może wykonywać automatyczne przywracanie.</span><span class="sxs-lookup"><span data-stu-id="a6a88-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="a6a88-169">Można również ustawić `EnableNuGetPackageRestore` dla zmiennej środowiskowej `True` wartość zamiast ustawienia tego klucza w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a6a88-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="a6a88-170">automatyczne</span><span class="sxs-lookup"><span data-stu-id="a6a88-170">automatic</span></span> | <span data-ttu-id="a6a88-171">Wartość logiczna wskazująca, czy NuGet ma sprawdzać brakujące pakiety podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="a6a88-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="a6a88-172">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a6a88-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="a6a88-173">Sekcja rozwiązania</span><span class="sxs-lookup"><span data-stu-id="a6a88-173">solution section</span></span>

<span data-ttu-id="a6a88-174">Określa, `packages` czy folder rozwiązania ma być uwzględniony w kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="a6a88-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="a6a88-175">Ta sekcja działa tylko w `nuget.config` plikach w folderze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="a6a88-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="a6a88-176">Key</span><span class="sxs-lookup"><span data-stu-id="a6a88-176">Key</span></span> | <span data-ttu-id="a6a88-177">Wartość</span><span class="sxs-lookup"><span data-stu-id="a6a88-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a6a88-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="a6a88-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="a6a88-179">Wartość logiczna wskazująca, czy ignorować folder Packages podczas pracy z kontrolą źródła.</span><span class="sxs-lookup"><span data-stu-id="a6a88-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="a6a88-180">Wartość domyślna to false.</span><span class="sxs-lookup"><span data-stu-id="a6a88-180">The default value is false.</span></span> |

<span data-ttu-id="a6a88-181">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a6a88-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="a6a88-182">Sekcje źródłowe pakietu</span><span class="sxs-lookup"><span data-stu-id="a6a88-182">Package source sections</span></span>

<span data-ttu-id="a6a88-183">`packageSourceCredentials` ,,`activePackageSource`, I`disabledPackageSources` wszystkie współpracują ze sobą, aby skonfigurować sposób działania programu NuGet z repozytoriami pakietów podczas operacji instalowania, przywracania i aktualizowania. `trustedSigners` `packageSources` `apikeys`</span><span class="sxs-lookup"><span data-stu-id="a6a88-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="a6a88-184">[ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md) `apikeys` `trustedSigners` [ `nuget trusted-signers` ](../reference/cli-reference/cli-ref-trusted-signers.md) [ Polecenie`nuget sources` ](../reference/cli-reference/cli-ref-sources.md) jest zwykle używane do zarządzania tymi ustawieniami, z wyjątkiem tego, które jest zarządzane za pomocą polecenia, i które jest zarządzane za pomocą polecenia.</span><span class="sxs-lookup"><span data-stu-id="a6a88-184">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="a6a88-185">Należy pamiętać, że źródłowy adres URL dla `https://api.nuget.org/v3/index.json`NuGet.org to.</span><span class="sxs-lookup"><span data-stu-id="a6a88-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="a6a88-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="a6a88-186">packageSources</span></span>

<span data-ttu-id="a6a88-187">Wyświetla wszystkie znane źródła pakietów.</span><span class="sxs-lookup"><span data-stu-id="a6a88-187">Lists all known package sources.</span></span> <span data-ttu-id="a6a88-188">Kolejność jest ignorowana podczas operacji przywracania i dowolnego projektu przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="a6a88-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="a6a88-189">Pakiet NuGet szanuje kolejność źródeł dla operacji instalacji i aktualizacji z projektami przy użyciu `packages.config`programu.</span><span class="sxs-lookup"><span data-stu-id="a6a88-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="a6a88-190">Key</span><span class="sxs-lookup"><span data-stu-id="a6a88-190">Key</span></span> | <span data-ttu-id="a6a88-191">Wartość</span><span class="sxs-lookup"><span data-stu-id="a6a88-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a6a88-192">(nazwa do przypisania do źródła pakietu)</span><span class="sxs-lookup"><span data-stu-id="a6a88-192">(name to assign to the package source)</span></span> | <span data-ttu-id="a6a88-193">Ścieżka lub adres URL źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="a6a88-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="a6a88-194">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a6a88-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="a6a88-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="a6a88-195">packageSourceCredentials</span></span>

<span data-ttu-id="a6a88-196">Przechowuje nazwy użytkowników i hasła dla źródeł, zwykle określone przy użyciu `-username` przełączników `nuget sources`i `-password` .</span><span class="sxs-lookup"><span data-stu-id="a6a88-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="a6a88-197">Hasła są szyfrowane domyślnie, chyba że `-storepasswordincleartext` jest również używana opcja.</span><span class="sxs-lookup"><span data-stu-id="a6a88-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="a6a88-198">Key</span><span class="sxs-lookup"><span data-stu-id="a6a88-198">Key</span></span> | <span data-ttu-id="a6a88-199">Wartość</span><span class="sxs-lookup"><span data-stu-id="a6a88-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a6a88-200">username</span><span class="sxs-lookup"><span data-stu-id="a6a88-200">username</span></span> | <span data-ttu-id="a6a88-201">Nazwa użytkownika dla źródła w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="a6a88-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="a6a88-202">password</span><span class="sxs-lookup"><span data-stu-id="a6a88-202">password</span></span> | <span data-ttu-id="a6a88-203">Hasło zaszyfrowane dla źródła.</span><span class="sxs-lookup"><span data-stu-id="a6a88-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="a6a88-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="a6a88-204">cleartextpassword</span></span> | <span data-ttu-id="a6a88-205">Niezaszyfrowane hasło dla źródła.</span><span class="sxs-lookup"><span data-stu-id="a6a88-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="a6a88-206">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="a6a88-206">**Example:**</span></span>

<span data-ttu-id="a6a88-207">W pliku `<packageSourceCredentials>` konfiguracji element zawiera węzły podrzędne dla każdej stosownej nazwy źródłowej (spacje w nazwie są `_x0020_`zastępowane).</span><span class="sxs-lookup"><span data-stu-id="a6a88-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="a6a88-208">Oznacza to, że w przypadku źródeł o nazwach "contoso" i "Źródło testowe" plik konfiguracyjny zawiera następujące dane w przypadku korzystania z szyfrowanych haseł:</span><span class="sxs-lookup"><span data-stu-id="a6a88-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="a6a88-209">W przypadku korzystania z nieszyfrowanych haseł:</span><span class="sxs-lookup"><span data-stu-id="a6a88-209">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="a6a88-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="a6a88-210">apikeys</span></span>

<span data-ttu-id="a6a88-211">Przechowuje klucze dla źródeł korzystających z uwierzytelniania za pomocą klucza interfejsu API, jak określono za pomocą [ `nuget setapikey` polecenia](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="a6a88-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="a6a88-212">Key</span><span class="sxs-lookup"><span data-stu-id="a6a88-212">Key</span></span> | <span data-ttu-id="a6a88-213">Wartość</span><span class="sxs-lookup"><span data-stu-id="a6a88-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a6a88-214">(źródłowy adres URL)</span><span class="sxs-lookup"><span data-stu-id="a6a88-214">(source URL)</span></span> | <span data-ttu-id="a6a88-215">Zaszyfrowany klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="a6a88-215">The encrypted API key.</span></span> |

<span data-ttu-id="a6a88-216">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a6a88-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="a6a88-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="a6a88-217">disabledPackageSources</span></span>

<span data-ttu-id="a6a88-218">Zidentyfikowano aktualnie wyłączone źródła.</span><span class="sxs-lookup"><span data-stu-id="a6a88-218">Identified currently disabled sources.</span></span> <span data-ttu-id="a6a88-219">Może być pusty.</span><span class="sxs-lookup"><span data-stu-id="a6a88-219">May be empty.</span></span>

| <span data-ttu-id="a6a88-220">Key</span><span class="sxs-lookup"><span data-stu-id="a6a88-220">Key</span></span> | <span data-ttu-id="a6a88-221">Wartość</span><span class="sxs-lookup"><span data-stu-id="a6a88-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a6a88-222">(nazwa źródła)</span><span class="sxs-lookup"><span data-stu-id="a6a88-222">(name of source)</span></span> | <span data-ttu-id="a6a88-223">Wartość logiczna wskazująca, czy źródło jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="a6a88-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="a6a88-224">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="a6a88-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="a6a88-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="a6a88-225">activePackageSource</span></span>

<span data-ttu-id="a6a88-226">*(tylko 2. x; przestarzałe w 3. x +)*</span><span class="sxs-lookup"><span data-stu-id="a6a88-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="a6a88-227">Identyfikuje aktualnie aktywne źródło lub wskazuje zagregowane wszystkie źródła.</span><span class="sxs-lookup"><span data-stu-id="a6a88-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="a6a88-228">Key</span><span class="sxs-lookup"><span data-stu-id="a6a88-228">Key</span></span> | <span data-ttu-id="a6a88-229">Wartość</span><span class="sxs-lookup"><span data-stu-id="a6a88-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a6a88-230">(nazwa źródła) lub`All`</span><span class="sxs-lookup"><span data-stu-id="a6a88-230">(name of source) or `All`</span></span> | <span data-ttu-id="a6a88-231">Jeśli klucz jest nazwą źródła, wartość jest ścieżką źródłową lub adresem URL.</span><span class="sxs-lookup"><span data-stu-id="a6a88-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="a6a88-232">Jeśli `All`wartość powinna być `(Aggregate source)` połączona ze wszystkimi źródłami pakietów, które nie są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="a6a88-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="a6a88-233">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a6a88-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="a6a88-234">Sekcja trustedSigners</span><span class="sxs-lookup"><span data-stu-id="a6a88-234">trustedSigners section</span></span>

<span data-ttu-id="a6a88-235">Przechowuje zaufane osoby podpisujące używane do zezwalania na pakiet podczas instalowania lub przywracania.</span><span class="sxs-lookup"><span data-stu-id="a6a88-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="a6a88-236">Ta lista nie może być pusta, jeśli użytkownik `signatureValidationMode` ustawi `require`.</span><span class="sxs-lookup"><span data-stu-id="a6a88-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="a6a88-237">Tę sekcję można zaktualizować za pomocą [ `nuget trusted-signers` polecenia](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="a6a88-237">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="a6a88-238">**Schemat**:</span><span class="sxs-lookup"><span data-stu-id="a6a88-238">**Schema**:</span></span>

<span data-ttu-id="a6a88-239">Zaufany podpiser zawiera kolekcję `certificate` elementów, które identyfikują wszystkie certyfikaty identyfikujące daną rejestrację.</span><span class="sxs-lookup"><span data-stu-id="a6a88-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="a6a88-240">Zaufaną rejestracją może być `Author` albo `Repository`lub.</span><span class="sxs-lookup"><span data-stu-id="a6a88-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="a6a88-241">Zaufane *repozytorium* `serviceIndex` określa również dla repozytorium (które musi być prawidłowym `https` identyfikatorem URI) i opcjonalnie określać listę rozdzielaną średnikami, aby ograniczyć liczbę elementów `owners` , które są zaufane z tego konkretnego kopie.</span><span class="sxs-lookup"><span data-stu-id="a6a88-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="a6a88-242">Obsługiwane algorytmy wyznaczania wartości skrótu używane dla `SHA256`odcisku `SHA512`palca certyfikatu to, `SHA384` i.</span><span class="sxs-lookup"><span data-stu-id="a6a88-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="a6a88-243">`certificate` Jeśli określono `allowUntrustedRoot` , żedanycertyfikatjestdozwolonydołączeniasięzniezaufanymkatalogiemgłównym,podczasbudowaniałańcuchacertyfikatówwramachweryfikacjipodpisu.`true`</span><span class="sxs-lookup"><span data-stu-id="a6a88-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="a6a88-244">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="a6a88-244">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a><span data-ttu-id="a6a88-245">Korzystanie ze zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="a6a88-245">Using environment variables</span></span>

<span data-ttu-id="a6a88-246">Możesz użyć zmiennych środowiskowych w `nuget.config` wartościach (NuGet 3.4 +), aby zastosować ustawienia w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="a6a88-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="a6a88-247">Na przykład jeśli `HOME` zmienna środowiskowa w systemie Windows jest ustawiona na `c:\users\username` `%HOME%\NuGetRepository` , wartość w pliku konfiguracji jest rozpoznawana `c:\users\username\NuGetRepository`jako.</span><span class="sxs-lookup"><span data-stu-id="a6a88-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="a6a88-248">Analogicznie, `HOME` Jeśli w systemie Mac/Linux jest `/home/myStuff`ustawiona na `%HOME%/NuGetRepository` , w pliku konfiguracji jest rozpoznawana `/home/myStuff/NuGetRepository`wartość.</span><span class="sxs-lookup"><span data-stu-id="a6a88-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="a6a88-249">Jeśli zmienna środowiskowa nie zostanie znaleziona, NuGet używa wartości literału z pliku konfiguracyjnego.</span><span class="sxs-lookup"><span data-stu-id="a6a88-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="a6a88-250">Przykładowy plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="a6a88-250">Example config file</span></span>

<span data-ttu-id="a6a88-251">Poniżej znajduje się przykładowy `nuget.config` plik, który ilustruje wiele ustawień:</span><span class="sxs-lookup"><span data-stu-id="a6a88-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
