---
title: Odwołanie do pliku nuget.config
description: Łącznie z sekcji konfiguracji, bindingRedirects, packageRestore, rozwiązania i packageSource odwołanie pliku NuGet.Config.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: c294e4c188db2e90e6bcb62b60f71ed5529977fe
ms.sourcegitcommit: a1846edf70ddb2505d58e536e08e952d870931b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303522"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="d32b0-103">Odwołanie do pliku nuget.config</span><span class="sxs-lookup"><span data-stu-id="d32b0-103">nuget.config reference</span></span>

<span data-ttu-id="d32b0-104">Zachowania programu NuGet jest kontrolowany przez ustawienia w różnych `NuGet.Config` plików zgodnie z opisem w [Konfigurowanie zachowania pakietu NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="d32b0-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="d32b0-105">`nuget.config` jest to plik XML zawierający najwyższego poziomu `<configuration>` węzła, który następnie zawiera elementy sekcji opisane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="d32b0-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="d32b0-106">Każda sekcja zawiera zero lub więcej elementów.</span><span class="sxs-lookup"><span data-stu-id="d32b0-106">Each section contains zero or more items.</span></span> <span data-ttu-id="d32b0-107">Zobacz [pliku konfiguracyjnego przykłady](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="d32b0-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="d32b0-108">Nazwy ustawień jest rozróżniana wielkość liter, a wartości można użyć [zmienne środowiskowe](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="d32b0-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="d32b0-109">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="d32b0-109">In this topic:</span></span>

- [<span data-ttu-id="d32b0-110">Sekcja konfiguracyjna</span><span class="sxs-lookup"><span data-stu-id="d32b0-110">config section</span></span>](#config-section)
- [<span data-ttu-id="d32b0-111">sekcja bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="d32b0-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="d32b0-112">sekcja packageRestore</span><span class="sxs-lookup"><span data-stu-id="d32b0-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="d32b0-113">sekcja rozwiązania</span><span class="sxs-lookup"><span data-stu-id="d32b0-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="d32b0-114">[Pakiet sekcje źródła](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="d32b0-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="d32b0-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="d32b0-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="d32b0-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="d32b0-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="d32b0-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="d32b0-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="d32b0-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="d32b0-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="d32b0-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="d32b0-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="d32b0-120">sekcja trustedSigners</span><span class="sxs-lookup"><span data-stu-id="d32b0-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="d32b0-121">Korzystanie ze zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="d32b0-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="d32b0-122">Przykładowy plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d32b0-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="d32b0-123">Sekcja konfiguracyjna</span><span class="sxs-lookup"><span data-stu-id="d32b0-123">config section</span></span>

<span data-ttu-id="d32b0-124">Zawiera ustawienia konfiguracji dodatkowych, które można ustawić za pomocą [ `nuget config` polecenia](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="d32b0-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="d32b0-125">`dependencyVersion` i `repositoryPath` mają zastosowanie tylko do projektów przy użyciu `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="d32b0-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="d32b0-126">`globalPackagesFolder` dotyczy tylko projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d32b0-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="d32b0-127">Key</span><span class="sxs-lookup"><span data-stu-id="d32b0-127">Key</span></span> | <span data-ttu-id="d32b0-128">Wartość</span><span class="sxs-lookup"><span data-stu-id="d32b0-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d32b0-129">dependencyVersion (`packages.config` tylko)</span><span class="sxs-lookup"><span data-stu-id="d32b0-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="d32b0-130">Wartość domyślna `DependencyVersion` wartość instalacja pakietu, przywracania i aktualizacji, gdy `-DependencyVersion` nie określono przełącznika bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="d32b0-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="d32b0-131">Ta wartość jest również używana przez interfejs użytkownika Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="d32b0-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="d32b0-132">Wartości są `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="d32b0-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="d32b0-133">globalPackagesFolder (projekty tylko przy użyciu funkcji PackageReference)</span><span class="sxs-lookup"><span data-stu-id="d32b0-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="d32b0-134">Lokalizacja folderu globalnymi pakietami domyślnego.</span><span class="sxs-lookup"><span data-stu-id="d32b0-134">The location of the default global packages folder.</span></span> <span data-ttu-id="d32b0-135">Wartość domyślna to `%userprofile%\.nuget\packages` (Windows) lub `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="d32b0-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="d32b0-136">Ścieżka względna mogą być używane w specyficznych dla projektu `nuget.config` plików.</span><span class="sxs-lookup"><span data-stu-id="d32b0-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="d32b0-137">To ustawienie zostanie zastąpione przez zmienną środowiskową NUGET_PACKAGES ma pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="d32b0-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="d32b0-138">repositoryPath (`packages.config` tylko)</span><span class="sxs-lookup"><span data-stu-id="d32b0-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="d32b0-139">Lokalizacja, w którym chcesz zainstalować pakiety NuGet, zamiast domyślnego `$(Solutiondir)/packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="d32b0-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="d32b0-140">Ścieżka względna mogą być używane w specyficznych dla projektu `nuget.config` plików.</span><span class="sxs-lookup"><span data-stu-id="d32b0-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="d32b0-141">To ustawienie zostanie zastąpione przez zmienną środowiskową NUGET_PACKAGES ma pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="d32b0-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="d32b0-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="d32b0-142">defaultPushSource</span></span> | <span data-ttu-id="d32b0-143">Określa adres URL lub ścieżki źródłowej pakietu, który powinien być używany jako domyślny, jeśli nie zostaną znalezione żadne inne źródła pakietu dla operacji.</span><span class="sxs-lookup"><span data-stu-id="d32b0-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="d32b0-144">no_proxy http_proxy.password http_proxy.user że</span><span class="sxs-lookup"><span data-stu-id="d32b0-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="d32b0-145">Ustawienia serwera proxy do użycia podczas łączenia ze źródłami pakietów; `http_proxy` powinien być w formacie `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="d32b0-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="d32b0-146">Hasła są szyfrowane i nie można dodać ręcznie.</span><span class="sxs-lookup"><span data-stu-id="d32b0-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="d32b0-147">Aby uzyskać `no_proxy`, wartość jest rozdzielana przecinkami lista domen obejścia serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="d32b0-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="d32b0-148">Można też używać zmiennych środowiskowych że i no_proxy, w przypadku tych wartości.</span><span class="sxs-lookup"><span data-stu-id="d32b0-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="d32b0-149">Aby uzyskać więcej informacji, zobacz [ustawienia serwera proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="d32b0-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="d32b0-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="d32b0-150">signatureValidationMode</span></span> | <span data-ttu-id="d32b0-151">Określa tryb weryfikacji używanej do weryfikowania podpisów pakietów do zainstalowania pakietu i przywracania.</span><span class="sxs-lookup"><span data-stu-id="d32b0-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="d32b0-152">Wartości są `accept`, `require`.</span><span class="sxs-lookup"><span data-stu-id="d32b0-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="d32b0-153">Wartość domyślna to `accept`.</span><span class="sxs-lookup"><span data-stu-id="d32b0-153">Defaults to `accept`.</span></span>

<span data-ttu-id="d32b0-154">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="d32b0-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="d32b0-155">sekcja bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="d32b0-155">bindingRedirects section</span></span>

<span data-ttu-id="d32b0-156">Określa, czy NuGet nie automatyczne przekierowania powiązań, gdy pakiet jest zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="d32b0-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="d32b0-157">Key</span><span class="sxs-lookup"><span data-stu-id="d32b0-157">Key</span></span> | <span data-ttu-id="d32b0-158">Wartość</span><span class="sxs-lookup"><span data-stu-id="d32b0-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d32b0-159">Pomiń</span><span class="sxs-lookup"><span data-stu-id="d32b0-159">skip</span></span> | <span data-ttu-id="d32b0-160">Wartość logiczna wskazująca, czy pominąć automatyczne przekierowania powiązań.</span><span class="sxs-lookup"><span data-stu-id="d32b0-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="d32b0-161">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="d32b0-161">The default is false.</span></span> |

<span data-ttu-id="d32b0-162">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="d32b0-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="d32b0-163">sekcja packageRestore</span><span class="sxs-lookup"><span data-stu-id="d32b0-163">packageRestore section</span></span>

<span data-ttu-id="d32b0-164">Formanty przywracania pakietów podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d32b0-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="d32b0-165">Key</span><span class="sxs-lookup"><span data-stu-id="d32b0-165">Key</span></span> | <span data-ttu-id="d32b0-166">Wartość</span><span class="sxs-lookup"><span data-stu-id="d32b0-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d32b0-167">Włączone</span><span class="sxs-lookup"><span data-stu-id="d32b0-167">enabled</span></span> | <span data-ttu-id="d32b0-168">Wartość logiczna wskazująca, czy NuGet przeprowadzić automatycznego przywracania.</span><span class="sxs-lookup"><span data-stu-id="d32b0-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="d32b0-169">Można również ustawić `EnableNuGetPackageRestore` zmienną środowiskową o wartości `True` zamiast ustawiać ten klucz w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d32b0-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="d32b0-170">automatyczne</span><span class="sxs-lookup"><span data-stu-id="d32b0-170">automatic</span></span> | <span data-ttu-id="d32b0-171">Wartość logiczna wskazująca, czy NuGet powinna sprawdzać, czy brakujących pakietów podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="d32b0-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="d32b0-172">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="d32b0-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="d32b0-173">sekcja rozwiązania</span><span class="sxs-lookup"><span data-stu-id="d32b0-173">solution section</span></span>

<span data-ttu-id="d32b0-174">Formanty czy `packages` folder rozwiązania znajduje się w kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="d32b0-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="d32b0-175">W tej sekcji działa tylko w `nuget.config` pliki w folderze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d32b0-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="d32b0-176">Key</span><span class="sxs-lookup"><span data-stu-id="d32b0-176">Key</span></span> | <span data-ttu-id="d32b0-177">Wartość</span><span class="sxs-lookup"><span data-stu-id="d32b0-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d32b0-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="d32b0-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="d32b0-179">Wartość logiczna wskazująca, czy ignorować packages folder podczas pracy z kontrolą źródła.</span><span class="sxs-lookup"><span data-stu-id="d32b0-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="d32b0-180">Wartość domyślna to false.</span><span class="sxs-lookup"><span data-stu-id="d32b0-180">The default value is false.</span></span> |

<span data-ttu-id="d32b0-181">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="d32b0-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="d32b0-182">Sekcje źródła pakietu</span><span class="sxs-lookup"><span data-stu-id="d32b0-182">Package source sections</span></span>

<span data-ttu-id="d32b0-183">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` i `trustedSigners` współdziałają ze sobą, aby skonfigurować, jak NuGet współpracuje z repozytoriów pakietów podczas instalacji, przywracania i operacje aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="d32b0-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="d32b0-184">[ `nuget sources` Polecenia](../tools/cli-ref-sources.md) zwykle jest używana do zarządzania tych ustawień, z wyjątkiem `apikeys` która jest zarządzana przy użyciu [ `nuget setapikey` polecenia](../tools/cli-ref-setapikey.md), i `trustedSigners` która będzie zarządzana za pomocą [ `nuget trusted-signers` polecenia](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="d32b0-184">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="d32b0-185">Należy zauważyć, że adres URL źródła nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="d32b0-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="d32b0-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="d32b0-186">packageSources</span></span>

<span data-ttu-id="d32b0-187">Wyświetla listę wszystkich źródeł pakietów znane.</span><span class="sxs-lookup"><span data-stu-id="d32b0-187">Lists all known package sources.</span></span> <span data-ttu-id="d32b0-188">Kolejność jest ignorowany podczas operacji przywracania i z jakimkolwiek projektem, przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="d32b0-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="d32b0-189">NuGet szanuje kolejność źródeł do instalacji i operacje aktualizacji z projektami za pomocą `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="d32b0-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="d32b0-190">Key</span><span class="sxs-lookup"><span data-stu-id="d32b0-190">Key</span></span> | <span data-ttu-id="d32b0-191">Wartość</span><span class="sxs-lookup"><span data-stu-id="d32b0-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d32b0-192">(Nazwa do przypisania do źródła pakietu)</span><span class="sxs-lookup"><span data-stu-id="d32b0-192">(name to assign to the package source)</span></span> | <span data-ttu-id="d32b0-193">Ścieżka lub adres URL źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="d32b0-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="d32b0-194">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="d32b0-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="d32b0-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="d32b0-195">packageSourceCredentials</span></span>

<span data-ttu-id="d32b0-196">Przechowywane nazwy użytkowników i hasła dla źródeł, zazwyczaj są określane za pomocą `-username` i `-password` zmienia się przy użyciu `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="d32b0-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="d32b0-197">Hasła są szyfrowane domyślnie, chyba że `-storepasswordincleartext` jest również używana opcja.</span><span class="sxs-lookup"><span data-stu-id="d32b0-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="d32b0-198">Key</span><span class="sxs-lookup"><span data-stu-id="d32b0-198">Key</span></span> | <span data-ttu-id="d32b0-199">Wartość</span><span class="sxs-lookup"><span data-stu-id="d32b0-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d32b0-200">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d32b0-200">username</span></span> | <span data-ttu-id="d32b0-201">Nazwa użytkownika źródła w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="d32b0-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="d32b0-202">Hasło</span><span class="sxs-lookup"><span data-stu-id="d32b0-202">password</span></span> | <span data-ttu-id="d32b0-203">Zaszyfrowane hasło dla źródła.</span><span class="sxs-lookup"><span data-stu-id="d32b0-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="d32b0-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="d32b0-204">cleartextpassword</span></span> | <span data-ttu-id="d32b0-205">Hasło nieszyfrowane źródła.</span><span class="sxs-lookup"><span data-stu-id="d32b0-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="d32b0-206">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="d32b0-206">**Example:**</span></span>

<span data-ttu-id="d32b0-207">W pliku konfiguracyjnym `<packageSourceCredentials>` element zawiera węzły podrzędne dla każdej nazwy źródła dotyczy (spacje w nazwie są zamieniane `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="d32b0-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="d32b0-208">Oznacza to w przypadku źródeł o nazwie "Contoso" i "Źródła testów" plik konfiguracji, który zawiera następujące korzystając z hasła szyfrowane:</span><span class="sxs-lookup"><span data-stu-id="d32b0-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="d32b0-209">W przypadku używania niezaszyfrowane hasła:</span><span class="sxs-lookup"><span data-stu-id="d32b0-209">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="d32b0-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="d32b0-210">apikeys</span></span>

<span data-ttu-id="d32b0-211">Przechowuje klucze dla źródeł, które używają uwierzytelniania kluczem interfejsu API, według stawki ustalonej z [ `nuget setapikey` polecenia](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="d32b0-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="d32b0-212">Key</span><span class="sxs-lookup"><span data-stu-id="d32b0-212">Key</span></span> | <span data-ttu-id="d32b0-213">Wartość</span><span class="sxs-lookup"><span data-stu-id="d32b0-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d32b0-214">(źródłowy adres URL)</span><span class="sxs-lookup"><span data-stu-id="d32b0-214">(source URL)</span></span> | <span data-ttu-id="d32b0-215">Zaszyfrowany klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d32b0-215">The encrypted API key.</span></span> |

<span data-ttu-id="d32b0-216">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="d32b0-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="d32b0-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="d32b0-217">disabledPackageSources</span></span>

<span data-ttu-id="d32b0-218">Zidentyfikować obecnie wyłączone źródła.</span><span class="sxs-lookup"><span data-stu-id="d32b0-218">Identified currently disabled sources.</span></span> <span data-ttu-id="d32b0-219">Może być pusta.</span><span class="sxs-lookup"><span data-stu-id="d32b0-219">May be empty.</span></span>

| <span data-ttu-id="d32b0-220">Key</span><span class="sxs-lookup"><span data-stu-id="d32b0-220">Key</span></span> | <span data-ttu-id="d32b0-221">Wartość</span><span class="sxs-lookup"><span data-stu-id="d32b0-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d32b0-222">(nazwa źródła)</span><span class="sxs-lookup"><span data-stu-id="d32b0-222">(name of source)</span></span> | <span data-ttu-id="d32b0-223">Wartość logiczna wskazująca, czy źródło jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="d32b0-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="d32b0-224">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="d32b0-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="d32b0-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="d32b0-225">activePackageSource</span></span>

<span data-ttu-id="d32b0-226">*(tylko 2.x; 3.x+ przestarzałe w)*</span><span class="sxs-lookup"><span data-stu-id="d32b0-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="d32b0-227">Identyfikuje do aktualnie aktywnego źródła lub wskazuje agregacji wszystkich źródeł.</span><span class="sxs-lookup"><span data-stu-id="d32b0-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="d32b0-228">Key</span><span class="sxs-lookup"><span data-stu-id="d32b0-228">Key</span></span> | <span data-ttu-id="d32b0-229">Wartość</span><span class="sxs-lookup"><span data-stu-id="d32b0-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="d32b0-230">(nazwa źródła) lub `All`</span><span class="sxs-lookup"><span data-stu-id="d32b0-230">(name of source) or `All`</span></span> | <span data-ttu-id="d32b0-231">Jeśli nazwa źródła jest klucz, wartość jest ścieżka źródłowa lub adres URL.</span><span class="sxs-lookup"><span data-stu-id="d32b0-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="d32b0-232">Jeśli `All`, ta wartość powinna być `(Aggregate source)` łączenie wszystkich źródeł pakietów, które w przeciwnym razie nie zostały wyłączone.</span><span class="sxs-lookup"><span data-stu-id="d32b0-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="d32b0-233">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="d32b0-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="d32b0-234">sekcja trustedSigners</span><span class="sxs-lookup"><span data-stu-id="d32b0-234">trustedSigners section</span></span>

<span data-ttu-id="d32b0-235">Magazyny zaufane osoby podpisujące używany w celu umożliwienia pakietu podczas instalowania lub przywracania.</span><span class="sxs-lookup"><span data-stu-id="d32b0-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="d32b0-236">Ta lista nie może być pusta, gdy użytkownik ustawi `signatureValidationMode` do `require`.</span><span class="sxs-lookup"><span data-stu-id="d32b0-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="d32b0-237">W tej sekcji mogą być aktualizowane przy użyciu [ `nuget trusted-signers` polecenia](../tools/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="d32b0-237">This section can be updated with the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="d32b0-238">**Schemat**:</span><span class="sxs-lookup"><span data-stu-id="d32b0-238">**Schema**:</span></span>

<span data-ttu-id="d32b0-239">Zaufane osoby podpisującej zawiera zbiór `certificate` elementy, które zarejestrować wszystkie certyfikaty, które identyfikują danego osoby podpisującej.</span><span class="sxs-lookup"><span data-stu-id="d32b0-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="d32b0-240">Może być zaufane osoby podpisującej `Author` lub `Repository`.</span><span class="sxs-lookup"><span data-stu-id="d32b0-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="d32b0-241">Zaufanego *repozytorium* określa również `serviceIndex` repozytorium (która musi być prawidłowym `https` identyfikatora uri) i opcjonalnie można określić Rozdzielana średnikami lista `owners` można ograniczyć jeszcze bardziej który jest zaufany z tego określonego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="d32b0-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="d32b0-242">To algorytmów wyznaczania wartości skrótu obsługiwanych odcisk palca certyfikatu `SHA256`, `SHA384` i `SHA512`.</span><span class="sxs-lookup"><span data-stu-id="d32b0-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="d32b0-243">Jeśli `certificate` Określa `allowUntrustedRoot` jako `true` podany certyfikat jest dozwolone do tworzenia łańcucha niezaufany certyfikat główny podczas tworzenia łańcucha certyfikatów, jako część weryfikacji podpisu.</span><span class="sxs-lookup"><span data-stu-id="d32b0-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="d32b0-244">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="d32b0-244">**Example**:</span></span>

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

## <a name="using-environment-variables"></a><span data-ttu-id="d32b0-245">Korzystanie ze zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="d32b0-245">Using environment variables</span></span>

<span data-ttu-id="d32b0-246">Można użyć zmiennych środowiskowych w `nuget.config` wartości (NuGet 3.4 +) do zastosowania ustawień w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d32b0-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="d32b0-247">Na przykład jeśli `HOME` ustawiono zmiennej środowiskowej na Windows `c:\users\username`, następnie wartość `%HOME%\NuGetRepository` w konfiguracji pliku jest rozpoznawana jako `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="d32b0-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="d32b0-248">Podobnie jeśli `HOME` w systemie Mac/Linux jest równa `/home/myStuff`, następnie `%HOME%/NuGetRepository` w konfiguracji pliku jest rozpoznawana jako `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="d32b0-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="d32b0-249">Jeśli zmienna środowiskowa nie zostanie znaleziony, NuGet używa wartości literału w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d32b0-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="d32b0-250">Przykładowy plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d32b0-250">Example config file</span></span>

<span data-ttu-id="d32b0-251">Poniżej znajduje się przykład `nuget.config` pliku, który przedstawia liczbę ustawień:</span><span class="sxs-lookup"><span data-stu-id="d32b0-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
