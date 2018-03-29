---
title: Odwołanie do pliku NuGet.Config. | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Odwołanie do pliku NuGet.Config łącznie z sekcji konfiguracji, bindingRedirects packageRestore, rozwiązanie i packageSource.
keywords: Pliku NuGet.Config, NuGet konfiguracji odwołania, opcje konfiguracji NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e2a9d4f10ac6af4e5bc7386d4f78e18c2a5752c4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="70902-104">Odwołanie do pliku NuGet.Config.</span><span class="sxs-lookup"><span data-stu-id="70902-104">NuGet.Config reference</span></span>

<span data-ttu-id="70902-105">Zachowanie NuGet jest kontrolowane przez ustawienia w różnych `NuGet.Config` plików zgodnie z opisem w [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="70902-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="70902-106">`NuGet.Config` jest to plik XML zawierający najwyższego poziomu `<configuration>` węzła, który następnie zawiera elementy sekcji opisane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="70902-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="70902-107">Każda sekcja zawiera zero lub więcej `<add>` elementy o `key` i `value` atrybutów.</span><span class="sxs-lookup"><span data-stu-id="70902-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="70902-108">Zobacz [pliku konfiguracji przykłady](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="70902-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="70902-109">Ustawienie nazwy jest rozróżniana wielkość liter, a wartości można użyć [zmiennych środowiskowych](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="70902-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="70902-110">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="70902-110">In this topic:</span></span>

- [<span data-ttu-id="70902-111">Sekcja konfiguracyjna</span><span class="sxs-lookup"><span data-stu-id="70902-111">config section</span></span>](#config-section)
- [<span data-ttu-id="70902-112">sekcja bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="70902-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="70902-113">sekcja packageRestore</span><span class="sxs-lookup"><span data-stu-id="70902-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="70902-114">sekcji rozwiązania</span><span class="sxs-lookup"><span data-stu-id="70902-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="70902-115">[Pakiet sekcje źródła](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="70902-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="70902-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="70902-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="70902-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="70902-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="70902-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="70902-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="70902-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="70902-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="70902-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="70902-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="70902-121">Korzystanie ze zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="70902-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="70902-122">Przykładowy plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="70902-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="70902-123">Sekcja konfiguracyjna</span><span class="sxs-lookup"><span data-stu-id="70902-123">config section</span></span>

<span data-ttu-id="70902-124">Zawiera ustawienia dodatkowych konfiguracji, które można ustawić za pomocą [ `nuget config` polecenia](../tools/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="70902-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="70902-125">`dependencyVersion` i `repositoryPath` stosowania tylko dla projektów przy użyciu `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="70902-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="70902-126">`globalPackagesFolder` dotyczy tylko projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="70902-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="70902-127">Key</span><span class="sxs-lookup"><span data-stu-id="70902-127">Key</span></span> | <span data-ttu-id="70902-128">Wartość</span><span class="sxs-lookup"><span data-stu-id="70902-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="70902-129">dependencyVersion (`packages.config` tylko)</span><span class="sxs-lookup"><span data-stu-id="70902-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="70902-130">Wartość domyślna `DependencyVersion` wartość instalacji pakietu, przywracania i aktualizacji, gdy `-DependencyVersion` przełącznik nie jest określony bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="70902-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="70902-131">Ta wartość jest także używana przez interfejs użytkownika Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="70902-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="70902-132">Wartości są `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span><span class="sxs-lookup"><span data-stu-id="70902-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="70902-133">wartość globalPackagesFolder (przy użyciu PackageReference tylko projekty)</span><span class="sxs-lookup"><span data-stu-id="70902-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="70902-134">Lokalizacja domyślny folder globalne pakietów.</span><span class="sxs-lookup"><span data-stu-id="70902-134">The location of the default global packages folder.</span></span> <span data-ttu-id="70902-135">Wartość domyślna to `%userprofile%\.nuget\packages` (system Windows) lub `~/.nuget/packages` (system Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="70902-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="70902-136">Ścieżka względna mogą być używane w specyficznego dla projektu `Nuget.Config` plików.</span><span class="sxs-lookup"><span data-stu-id="70902-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="70902-137">To ustawienie jest zastępowany przez zmienną środowiskową NUGET_PACKAGES pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="70902-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="70902-138">repositoryPath (`packages.config` tylko)</span><span class="sxs-lookup"><span data-stu-id="70902-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="70902-139">Lokalizacja, w którym można zainstalować pakietów NuGet, zamiast domyślnej `$(Solutiondir)/packages` folderu.</span><span class="sxs-lookup"><span data-stu-id="70902-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="70902-140">Ścieżka względna mogą być używane w specyficznego dla projektu `Nuget.Config` plików.</span><span class="sxs-lookup"><span data-stu-id="70902-140">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="70902-141">To ustawienie jest zastępowany przez zmienną środowiskową NUGET_PACKAGES pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="70902-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="70902-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="70902-142">defaultPushSource</span></span> | <span data-ttu-id="70902-143">Określa adres URL lub ścieżkę źródła pakietu, które mają być używane jako domyślne, jeśli inne źródła pakietu nie znaleziono dla operacji.</span><span class="sxs-lookup"><span data-stu-id="70902-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="70902-144">że http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="70902-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="70902-145">Ustawienia serwera proxy do użycia podczas połączenia ze źródła pakietów; `http_proxy` powinien być w formacie `http://<username>:<password>@<domain>`.</span><span class="sxs-lookup"><span data-stu-id="70902-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="70902-146">Hasła są szyfrowane i nie można dodać ręcznie.</span><span class="sxs-lookup"><span data-stu-id="70902-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="70902-147">Aby uzyskać `no_proxy`, wartość jest rozdzielaną przecinkami listę domen obejścia serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="70902-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="70902-148">Można również używać zmiennych środowiskowych że i no_proxy, dla tych wartości.</span><span class="sxs-lookup"><span data-stu-id="70902-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="70902-149">Aby uzyskać więcej informacji, zobacz [ustawienia serwera proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="70902-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="70902-150">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="70902-150">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="70902-151">sekcja bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="70902-151">bindingRedirects section</span></span>

<span data-ttu-id="70902-152">Określa, czy NuGet nie przekierowania powiązania automatyczne, gdy jest zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="70902-152">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="70902-153">Key</span><span class="sxs-lookup"><span data-stu-id="70902-153">Key</span></span> | <span data-ttu-id="70902-154">Wartość</span><span class="sxs-lookup"><span data-stu-id="70902-154">Value</span></span> |
| --- | --- |
| <span data-ttu-id="70902-155">Pomiń</span><span class="sxs-lookup"><span data-stu-id="70902-155">skip</span></span> | <span data-ttu-id="70902-156">Wartość logiczna wskazująca, czy pominąć przekierowania powiązania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="70902-156">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="70902-157">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="70902-157">The default is false.</span></span> |

<span data-ttu-id="70902-158">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="70902-158">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="70902-159">sekcja packageRestore</span><span class="sxs-lookup"><span data-stu-id="70902-159">packageRestore section</span></span>

<span data-ttu-id="70902-160">Formanty Przywracanie pakietów podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="70902-160">Controls package restore during builds.</span></span>

| <span data-ttu-id="70902-161">Key</span><span class="sxs-lookup"><span data-stu-id="70902-161">Key</span></span> | <span data-ttu-id="70902-162">Wartość</span><span class="sxs-lookup"><span data-stu-id="70902-162">Value</span></span> |
| --- | --- |
| <span data-ttu-id="70902-163">włączone</span><span class="sxs-lookup"><span data-stu-id="70902-163">enabled</span></span> | <span data-ttu-id="70902-164">Wartość logiczna wskazująca, czy NuGet można wykonać przywracania automatycznie.</span><span class="sxs-lookup"><span data-stu-id="70902-164">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="70902-165">Można również ustawić `EnableNuGetPackageRestore` zmienną środowiskową o wartości `True` zamiast ustawienie tego klucza w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="70902-165">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="70902-166">automatyczne</span><span class="sxs-lookup"><span data-stu-id="70902-166">automatic</span></span> | <span data-ttu-id="70902-167">Wartość logiczna wskazująca, czy NuGet należy sprawdzić, czy brakujących pakietów podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="70902-167">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="70902-168">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="70902-168">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="70902-169">sekcji rozwiązania</span><span class="sxs-lookup"><span data-stu-id="70902-169">solution section</span></span>

<span data-ttu-id="70902-170">Formanty czy `packages` folderu rozwiązania jest uwzględniona w kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="70902-170">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="70902-171">W tej sekcji działa tylko w `Nuget.Config` pliki w folderze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="70902-171">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="70902-172">Key</span><span class="sxs-lookup"><span data-stu-id="70902-172">Key</span></span> | <span data-ttu-id="70902-173">Wartość</span><span class="sxs-lookup"><span data-stu-id="70902-173">Value</span></span> |
| --- | --- |
| <span data-ttu-id="70902-174">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="70902-174">disableSourceControlIntegration</span></span> | <span data-ttu-id="70902-175">Wartość logiczna wskazująca, czy Ignoruj folderu pakietów podczas pracy z kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="70902-175">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="70902-176">Wartość domyślna to false.</span><span class="sxs-lookup"><span data-stu-id="70902-176">The default value is false.</span></span> |

<span data-ttu-id="70902-177">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="70902-177">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="70902-178">Sekcje źródła pakietu</span><span class="sxs-lookup"><span data-stu-id="70902-178">Package source sections</span></span>

<span data-ttu-id="70902-179">`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, I `disabledPackageSources` wszystkie działają razem, konfigurowanie, jak NuGet współpracuje z repozytoriów pakietu podczas instalacji, przywracania i operacje aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="70902-179">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="70902-180">[ `nuget sources` Polecenia](../tools/cli-ref-sources.md) jest zazwyczaj używany do zarządzania te ustawienia, z wyjątkiem `apikeys` której odbywa się przy użyciu [ `nuget setapikey` polecenia](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="70902-180">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="70902-181">Należy zauważyć, że adres URL źródła dla nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="70902-181">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="70902-182">packageSources</span><span class="sxs-lookup"><span data-stu-id="70902-182">packageSources</span></span>

<span data-ttu-id="70902-183">Wyświetla wszystkie źródła pakietów znane.</span><span class="sxs-lookup"><span data-stu-id="70902-183">Lists all known package sources.</span></span> <span data-ttu-id="70902-184">Kolejność jest ignorowany podczas operacji przywracania, a w przypadku projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="70902-184">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="70902-185">Kolejność źródeł instalacji szanuje NuGet i operacje aktualizacji z projektami za pomocą `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="70902-185">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="70902-186">Key</span><span class="sxs-lookup"><span data-stu-id="70902-186">Key</span></span> | <span data-ttu-id="70902-187">Wartość</span><span class="sxs-lookup"><span data-stu-id="70902-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="70902-188">(nazwa można przypisać do źródła pakietu)</span><span class="sxs-lookup"><span data-stu-id="70902-188">(name to assign to the package source)</span></span> | <span data-ttu-id="70902-189">Ścieżka lub adres URL źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="70902-189">The path or URL of the package source.</span></span> |

<span data-ttu-id="70902-190">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="70902-190">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="70902-191">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="70902-191">packageSourceCredentials</span></span>

<span data-ttu-id="70902-192">Przechowywane nazwy użytkowników i hasła dla źródeł, zazwyczaj określana z `-username` i `-password` zmienia z `nuget sources`.</span><span class="sxs-lookup"><span data-stu-id="70902-192">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="70902-193">Hasła są szyfrowane domyślnie, chyba że `-storepasswordincleartext` również używana jest opcja.</span><span class="sxs-lookup"><span data-stu-id="70902-193">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="70902-194">Key</span><span class="sxs-lookup"><span data-stu-id="70902-194">Key</span></span> | <span data-ttu-id="70902-195">Wartość</span><span class="sxs-lookup"><span data-stu-id="70902-195">Value</span></span> |
| --- | --- |
| <span data-ttu-id="70902-196">username</span><span class="sxs-lookup"><span data-stu-id="70902-196">username</span></span> | <span data-ttu-id="70902-197">Nazwa użytkownika dla źródła w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="70902-197">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="70902-198">Hasło</span><span class="sxs-lookup"><span data-stu-id="70902-198">password</span></span> | <span data-ttu-id="70902-199">Zaszyfrowane hasło dla tego źródła.</span><span class="sxs-lookup"><span data-stu-id="70902-199">The encrypted password for the source.</span></span> |
| <span data-ttu-id="70902-200">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="70902-200">cleartextpassword</span></span> | <span data-ttu-id="70902-201">Hasło nieszyfrowane źródła.</span><span class="sxs-lookup"><span data-stu-id="70902-201">The unencrypted password for the source.</span></span> |

<span data-ttu-id="70902-202">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="70902-202">**Example:**</span></span>

<span data-ttu-id="70902-203">W pliku konfiguracyjnym `<packageSourceCredentials>` element zawiera węzły podrzędne dla każdej nazwy odpowiednich źródła (spacje w nazwie są zastępowane `_x0020_`).</span><span class="sxs-lookup"><span data-stu-id="70902-203">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="70902-204">Oznacza to, że dla źródeł o nazwie "Contoso" i "Źródła testów", plik konfiguracji zawiera następujące przy użyciu hasła szyfrowane:</span><span class="sxs-lookup"><span data-stu-id="70902-204">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="70902-205">Podczas używania niezaszyfrowane hasła:</span><span class="sxs-lookup"><span data-stu-id="70902-205">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="70902-206">apikeys</span><span class="sxs-lookup"><span data-stu-id="70902-206">apikeys</span></span>

<span data-ttu-id="70902-207">Przechowuje klucze źródeł, które korzystają z uwierzytelniania klucza interfejsu API, zgodnie z [ `nuget setapikey` polecenia](../tools/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="70902-207">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="70902-208">Key</span><span class="sxs-lookup"><span data-stu-id="70902-208">Key</span></span> | <span data-ttu-id="70902-209">Wartość</span><span class="sxs-lookup"><span data-stu-id="70902-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="70902-210">(adres URL źródła)</span><span class="sxs-lookup"><span data-stu-id="70902-210">(source URL)</span></span> | <span data-ttu-id="70902-211">Zaszyfrowany klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="70902-211">The encrypted API key.</span></span> |

<span data-ttu-id="70902-212">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="70902-212">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="70902-213">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="70902-213">disabledPackageSources</span></span>

<span data-ttu-id="70902-214">Rozpoznane źródła aktualnie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="70902-214">Identified currently disabled sources.</span></span> <span data-ttu-id="70902-215">Może być pusta.</span><span class="sxs-lookup"><span data-stu-id="70902-215">May be empty.</span></span>

| <span data-ttu-id="70902-216">Key</span><span class="sxs-lookup"><span data-stu-id="70902-216">Key</span></span> | <span data-ttu-id="70902-217">Wartość</span><span class="sxs-lookup"><span data-stu-id="70902-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="70902-218">(nazwa źródła)</span><span class="sxs-lookup"><span data-stu-id="70902-218">(name of source)</span></span> | <span data-ttu-id="70902-219">Wartość logiczna wskazująca, czy źródło jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="70902-219">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="70902-220">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="70902-220">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="70902-221">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="70902-221">activePackageSource</span></span>

<span data-ttu-id="70902-222">*(tylko 2.x; 3.x+ przestarzałe w)*</span><span class="sxs-lookup"><span data-stu-id="70902-222">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="70902-223">Identyfikuje do aktywnego źródła lub wskazuje agregacji wszystkich źródeł.</span><span class="sxs-lookup"><span data-stu-id="70902-223">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="70902-224">Key</span><span class="sxs-lookup"><span data-stu-id="70902-224">Key</span></span> | <span data-ttu-id="70902-225">Wartość</span><span class="sxs-lookup"><span data-stu-id="70902-225">Value</span></span> |
| --- | --- |
| <span data-ttu-id="70902-226">(nazwa źródła) lub `All`</span><span class="sxs-lookup"><span data-stu-id="70902-226">(name of source) or `All`</span></span> | <span data-ttu-id="70902-227">Jeśli klucz jest nazwę źródła, wartość jest ścieżka źródłowa lub adres URL.</span><span class="sxs-lookup"><span data-stu-id="70902-227">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="70902-228">Jeśli `All`, wartość powinna być `(Aggregate source)` połączyć wszystkie źródła pakietów, które nie zostały wyłączone w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="70902-228">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="70902-229">**Przykład**:</span><span class="sxs-lookup"><span data-stu-id="70902-229">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="70902-230">Korzystanie ze zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="70902-230">Using environment variables</span></span>

<span data-ttu-id="70902-231">Można używać zmiennych środowiskowych w `NuGet.Config` wartości (NuGet 3.4 +) w celu zastosowania ustawień w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="70902-231">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="70902-232">Na przykład jeśli `HOME` ustawiono zmiennej środowiskowej w systemie Windows `c:\users\username`, wartość `%HOME%\NuGetRepository` w konfiguracji pliku jest rozpoznawana jako `c:\users\username\NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="70902-232">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="70902-233">Podobnie jeśli `HOME` na system Mac/Linux jest ustawiona na `/home/myStuff`, następnie `$HOME/NuGetRepository` w konfiguracji pliku jest rozpoznawana jako `/home/myStuff/NuGetRepository`.</span><span class="sxs-lookup"><span data-stu-id="70902-233">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="70902-234">Jeśli zmienna środowiskowa nie zostanie znaleziony, NuGet korzysta z wartości literału z pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="70902-234">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="70902-235">Przykładowy plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="70902-235">Example config file</span></span>

<span data-ttu-id="70902-236">Poniżej znajduje się przykład `NuGet.Config` pliku, który przedstawia liczbę ustawień:</span><span class="sxs-lookup"><span data-stu-id="70902-236">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
