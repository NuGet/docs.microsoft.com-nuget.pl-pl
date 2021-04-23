---
title: nuget.config pliku
description: NuGet.Config plików, w tym sekcje config, bindingRedirects, packageRestore, solution i packageSource.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 38620058bccde876152328302a6049f011c149db
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901866"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="6d4ac-103">`nuget.config` Odwołanie</span><span class="sxs-lookup"><span data-stu-id="6d4ac-103">`nuget.config` reference</span></span>

<span data-ttu-id="6d4ac-104">Zachowanie programu NuGet jest kontrolowane przez ustawienia w różnych `NuGet.Config` plikach lub `nuget.config` zgodnie z opisem w tece Common [NuGet configurations (Typowe konfiguracje nuGet).](../consume-packages/configuring-nuget-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="6d4ac-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="6d4ac-105">`nuget.config` to plik XML zawierający węzeł najwyższego `<configuration>` poziomu, który następnie zawiera elementy sekcji opisane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="6d4ac-106">Każda sekcja zawiera zero lub więcej elementów.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-106">Each section contains zero or more items.</span></span> <span data-ttu-id="6d4ac-107">Zobacz [przykładowy plik konfiguracji](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="6d4ac-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="6d4ac-108">W nazwach ustawień nie jest uwzględniania litera, a wartości mogą używać [zmiennych środowiskowych](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="6d4ac-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="6d4ac-109">sekcja konfiguracji</span><span class="sxs-lookup"><span data-stu-id="6d4ac-109">config section</span></span>

<span data-ttu-id="6d4ac-110">Zawiera różne ustawienia konfiguracji, które można ustawić za pomocą [ `nuget config` polecenia](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="6d4ac-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="6d4ac-111">`dependencyVersion` i `repositoryPath` dotyczą tylko projektów korzystających z programu `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="6d4ac-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="6d4ac-112">`globalPackagesFolder` Dotyczy tylko projektów korzystających z formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="6d4ac-113">Klucz</span><span class="sxs-lookup"><span data-stu-id="6d4ac-113">Key</span></span> | <span data-ttu-id="6d4ac-114">Wartość</span><span class="sxs-lookup"><span data-stu-id="6d4ac-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6d4ac-115">dependencyVersion `packages.config` (tylko)</span><span class="sxs-lookup"><span data-stu-id="6d4ac-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="6d4ac-116">Wartość `DependencyVersion` domyślna dla instalowania, przywracania i aktualizowania pakietu, gdy `-DependencyVersion` przełącznik nie jest określony bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="6d4ac-117">Ta wartość jest również używana przez interfejs użytkownika Menedżer pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="6d4ac-118">Wartości to `Lowest` , `HighestPatch` , , `HighestMinor` `Highest` .</span><span class="sxs-lookup"><span data-stu-id="6d4ac-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="6d4ac-119">globalPackagesFolder (projekty korzystające tylko z packageReference)</span><span class="sxs-lookup"><span data-stu-id="6d4ac-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="6d4ac-120">Lokalizacja domyślnego folderu pakietów globalnych.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-120">The location of the default global packages folder.</span></span> <span data-ttu-id="6d4ac-121">Wartość domyślna to `%userprofile%\.nuget\packages` (Windows) lub `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="6d4ac-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="6d4ac-122">Ścieżka względna może być używana w plikach specyficznych dla `nuget.config` projektu.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="6d4ac-123">To ustawienie jest zastępowany przez `NUGET_PACKAGES` zmienną środowiskową, która ma pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-123">This setting is overridden by the `NUGET_PACKAGES` environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="6d4ac-124">repositoryPath `packages.config` (tylko)</span><span class="sxs-lookup"><span data-stu-id="6d4ac-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="6d4ac-125">Lokalizacja, w której mają być zainstalowane pakiety NuGet zamiast folderu `$(Solutiondir)/packages` domyślnego.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="6d4ac-126">Ścieżka względna może być używana w plikach specyficznych dla `nuget.config` projektu.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="6d4ac-127">To ustawienie jest zastępowany przez `NUGET_PACKAGES` zmienną środowiskową, która ma pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-127">This setting is overridden by the `NUGET_PACKAGES` environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="6d4ac-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="6d4ac-128">defaultPushSource</span></span> | <span data-ttu-id="6d4ac-129">Identyfikuje adres URL lub ścieżkę źródła pakietu, która powinna być używana jako domyślna, jeśli dla operacji nie zostaną znalezione żadne inne źródła pakietów.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="6d4ac-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="6d4ac-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="6d4ac-131">Ustawienia serwera proxy do użycia podczas nawiązywania połączenia ze źródłami pakietów; `http_proxy` powinna mieć format `http://<username>:<password>@<domain>` .</span><span class="sxs-lookup"><span data-stu-id="6d4ac-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="6d4ac-132">Hasła są szyfrowane i nie można ich dodawać ręcznie.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="6d4ac-133">W przypadku wartości wartość jest rozdzielaną przecinkami `no_proxy` listą domen, która pomija serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="6d4ac-134">Alternatywnie można użyć http_proxy i no_proxy zmiennych środowiskowych dla tych wartości.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="6d4ac-135">Aby uzyskać więcej informacji, zobacz [Ustawienia serwera proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="6d4ac-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="6d4ac-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="6d4ac-136">signatureValidationMode</span></span> | <span data-ttu-id="6d4ac-137">Określa tryb weryfikacji używany do weryfikowania podpisów pakietów dla instalowania i przywracania pakietu.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="6d4ac-138">Wartości to `accept` , `require` .</span><span class="sxs-lookup"><span data-stu-id="6d4ac-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="6d4ac-139">Wartość domyślna to `accept` .</span><span class="sxs-lookup"><span data-stu-id="6d4ac-139">Defaults to `accept`.</span></span>

<span data-ttu-id="6d4ac-140">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="6d4ac-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="6d4ac-141">sekcja bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="6d4ac-141">bindingRedirects section</span></span>

<span data-ttu-id="6d4ac-142">Określa, czy pakiet NuGet automatycznie przekierowuje powiązania po zainstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="6d4ac-143">Klucz</span><span class="sxs-lookup"><span data-stu-id="6d4ac-143">Key</span></span> | <span data-ttu-id="6d4ac-144">Wartość</span><span class="sxs-lookup"><span data-stu-id="6d4ac-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6d4ac-145">Pomiń</span><span class="sxs-lookup"><span data-stu-id="6d4ac-145">skip</span></span> | <span data-ttu-id="6d4ac-146">Wartość logiczna wskazująca, czy pominąć automatyczne przekierowania powiązań.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="6d4ac-147">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-147">The default is false.</span></span> |

<span data-ttu-id="6d4ac-148">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="6d4ac-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="6d4ac-149">sekcja packageRestore</span><span class="sxs-lookup"><span data-stu-id="6d4ac-149">packageRestore section</span></span>

<span data-ttu-id="6d4ac-150">Steruje przywracaniem pakietów podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="6d4ac-151">Klucz</span><span class="sxs-lookup"><span data-stu-id="6d4ac-151">Key</span></span> | <span data-ttu-id="6d4ac-152">Wartość</span><span class="sxs-lookup"><span data-stu-id="6d4ac-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6d4ac-153">enabled</span><span class="sxs-lookup"><span data-stu-id="6d4ac-153">enabled</span></span> | <span data-ttu-id="6d4ac-154">Wartość logiczna wskazująca, czy nuGet może wykonać automatyczne przywracanie.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="6d4ac-155">Możesz również ustawić `EnableNuGetPackageRestore` zmienną środowiskową z wartością zamiast ustawiać ten `True` klucz w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="6d4ac-156">automatyczne</span><span class="sxs-lookup"><span data-stu-id="6d4ac-156">automatic</span></span> | <span data-ttu-id="6d4ac-157">Wartość logiczna wskazująca, czy pakiet NuGet powinien sprawdzać brakujące pakiety podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="6d4ac-158">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="6d4ac-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="6d4ac-159">sekcja rozwiązania</span><span class="sxs-lookup"><span data-stu-id="6d4ac-159">solution section</span></span>

<span data-ttu-id="6d4ac-160">Określa, `packages` czy folder rozwiązania jest uwzględniony w kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="6d4ac-161">Ta sekcja działa tylko `nuget.config` w plikach w folderze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="6d4ac-162">Klucz</span><span class="sxs-lookup"><span data-stu-id="6d4ac-162">Key</span></span> | <span data-ttu-id="6d4ac-163">Wartość</span><span class="sxs-lookup"><span data-stu-id="6d4ac-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6d4ac-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="6d4ac-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="6d4ac-165">Wartość logiczna wskazująca, czy zignorować folder packages podczas pracy z kontrolą źródła.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="6d4ac-166">Wartość domyślna to false.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-166">The default value is false.</span></span> |

<span data-ttu-id="6d4ac-167">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="6d4ac-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="6d4ac-168">Sekcje źródłowe pakietu</span><span class="sxs-lookup"><span data-stu-id="6d4ac-168">Package source sections</span></span>

<span data-ttu-id="6d4ac-169">Wszystkie , , , i współpracują ze sobą, aby skonfigurować sposób działania pakietu NuGet z repozytoriami pakietów podczas operacji `packageSources` `packageSourceCredentials` `apikeys` `activePackageSource` `disabledPackageSources` `trustedSigners` instalowania, przywracania i aktualizowania.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="6d4ac-170">Polecenie [ `nuget sources` jest](../reference/cli-reference/cli-ref-sources.md) zwykle używane do zarządzania tymi ustawieniami, z wyjątkiem tego, który jest zarządzany przy użyciu polecenia , i który jest `apikeys` zarządzany za pomocą [ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md) `trustedSigners` [ `nuget trusted-signers` polecenia](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="6d4ac-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="6d4ac-171">Zwróć uwagę, że źródłowy adres URL nuget.org to `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="6d4ac-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="6d4ac-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="6d4ac-172">packageSources</span></span>

<span data-ttu-id="6d4ac-173">Wyświetla listę wszystkich znanych źródeł pakietów.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-173">Lists all known package sources.</span></span> <span data-ttu-id="6d4ac-174">Kolejność jest ignorowana podczas operacji przywracania i w dowolnym projekcie w formacie PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="6d4ac-175">Program NuGet respektuje kolejność źródeł dla operacji instalacji i aktualizacji w projektach korzystających z programu `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="6d4ac-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="6d4ac-176">Klucz</span><span class="sxs-lookup"><span data-stu-id="6d4ac-176">Key</span></span> | <span data-ttu-id="6d4ac-177">Wartość</span><span class="sxs-lookup"><span data-stu-id="6d4ac-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6d4ac-178">(nazwa do przypisania do źródła pakietu)</span><span class="sxs-lookup"><span data-stu-id="6d4ac-178">(name to assign to the package source)</span></span> | <span data-ttu-id="6d4ac-179">Ścieżka lub adres URL źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="6d4ac-180">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="6d4ac-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="6d4ac-181">Gdy `<clear />` jest obecny dla danego węzła, nuGet ignoruje wcześniej zdefiniowane wartości konfiguracji dla tego węzła.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="6d4ac-182">[Dowiedz się więcej na temat sposobu stosowania ustawień](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="6d4ac-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="6d4ac-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="6d4ac-183">packageSourceCredentials</span></span>

<span data-ttu-id="6d4ac-184">Przechowuje nazwy użytkowników i hasła dla źródeł, zwykle określone za pomocą `-username` przełączników `-password` i . `nuget sources`</span><span class="sxs-lookup"><span data-stu-id="6d4ac-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="6d4ac-185">Hasła są domyślnie szyfrowane, chyba że `-storepasswordincleartext` jest również używana opcja .</span><span class="sxs-lookup"><span data-stu-id="6d4ac-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>
<span data-ttu-id="6d4ac-186">Opcjonalnie za pomocą przełącznika można określić prawidłowe typy `-validauthenticationtypes` uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-186">Optionally, valid authentication types can be specified with the `-validauthenticationtypes` switch.</span></span>

| <span data-ttu-id="6d4ac-187">Klucz</span><span class="sxs-lookup"><span data-stu-id="6d4ac-187">Key</span></span> | <span data-ttu-id="6d4ac-188">Wartość</span><span class="sxs-lookup"><span data-stu-id="6d4ac-188">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6d4ac-189">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="6d4ac-189">username</span></span> | <span data-ttu-id="6d4ac-190">Nazwa użytkownika źródła w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-190">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="6d4ac-191">hasło</span><span class="sxs-lookup"><span data-stu-id="6d4ac-191">password</span></span> | <span data-ttu-id="6d4ac-192">Zaszyfrowane hasło dla źródła.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-192">The encrypted password for the source.</span></span> <span data-ttu-id="6d4ac-193">Zaszyfrowane hasła są obsługiwane tylko w systemie Windows i można je odszyfrować tylko wtedy, gdy są używane na tym samym komputerze i za pośrednictwem tego samego użytkownika co oryginalne szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-193">Encrypted passwords are only supported on Windows, and only can be decrypted when used on the same machine and via the same user as the original encryption.</span></span> |
| <span data-ttu-id="6d4ac-194">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="6d4ac-194">cleartextpassword</span></span> | <span data-ttu-id="6d4ac-195">Niezaszyfrowane hasło źródła.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-195">The unencrypted password for the source.</span></span> <span data-ttu-id="6d4ac-196">Uwaga: zmienne środowiskowe mogą być używane w celu poprawy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-196">Note: environment variables can be used for improved security.</span></span> |
| <span data-ttu-id="6d4ac-197">validauthenticationtypes</span><span class="sxs-lookup"><span data-stu-id="6d4ac-197">validauthenticationtypes</span></span> | <span data-ttu-id="6d4ac-198">Rozdzielana przecinkami lista prawidłowych typów uwierzytelniania dla tego źródła.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-198">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="6d4ac-199">Ustaw tę wartość na wartość , jeśli serwer anonsuje NTLM lub Negotiate, a poświadczenia muszą zostać wysłane przy użyciu mechanizmu podstawowego, na przykład w przypadku używania pata dostępu do lokalnego `basic` Azure DevOps Server.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-199">Set this to `basic` if the server advertises NTLM or Negotiate and your credentials must be sent using the Basic mechanism, for instance when using a PAT with on-premises Azure DevOps Server.</span></span> <span data-ttu-id="6d4ac-200">Inne prawidłowe wartości to `negotiate` , , i , ale te wartości prawdopodobnie nie będą `kerberos` `ntlm` `digest` przydatne.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-200">Other valid values include `negotiate`, `kerberos`, `ntlm`, and `digest`, but these values are unlikely to be useful.</span></span> |

<span data-ttu-id="6d4ac-201">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="6d4ac-201">**Example:**</span></span>

<span data-ttu-id="6d4ac-202">W pliku konfiguracji element zawiera węzły podrzędne dla każdej nazwy odpowiedniego źródła (spacje w nazwie `<packageSourceCredentials>` są zastępowane przez `_x0020_` ).</span><span class="sxs-lookup"><span data-stu-id="6d4ac-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="6d4ac-203">Oznacza to, że w przypadku źródeł o nazwach "Contoso" i "Test Source" plik konfiguracji zawiera następujące informacje w przypadku korzystania z zaszyfrowanych haseł:</span><span class="sxs-lookup"><span data-stu-id="6d4ac-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="6d4ac-204">W przypadku korzystania z niezaszyfrowanych haseł przechowywanych w zmiennej środowiskowej:</span><span class="sxs-lookup"><span data-stu-id="6d4ac-204">When using unencrypted passwords stored in an environment variable:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

<span data-ttu-id="6d4ac-205">W przypadku korzystania z haseł niezaszyfrowanych:</span><span class="sxs-lookup"><span data-stu-id="6d4ac-205">When using unencrypted passwords:</span></span>

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

<span data-ttu-id="6d4ac-206">Ponadto można dostarczyć prawidłowe metody uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="6d4ac-206">Additionally, valid authentication methods can be supplied:</span></span>

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a><span data-ttu-id="6d4ac-207">apikeys</span><span class="sxs-lookup"><span data-stu-id="6d4ac-207">apikeys</span></span>

<span data-ttu-id="6d4ac-208">Przechowuje klucze dla źródeł, które używają uwierzytelniania za pomocą klucza interfejsu API, zgodnie z ustawieniem za pomocą [ `nuget setapikey` polecenia](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="6d4ac-208">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="6d4ac-209">Klucz</span><span class="sxs-lookup"><span data-stu-id="6d4ac-209">Key</span></span> | <span data-ttu-id="6d4ac-210">Wartość</span><span class="sxs-lookup"><span data-stu-id="6d4ac-210">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6d4ac-211">(źródłowy adres URL)</span><span class="sxs-lookup"><span data-stu-id="6d4ac-211">(source URL)</span></span> | <span data-ttu-id="6d4ac-212">Zaszyfrowany klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-212">The encrypted API key.</span></span> |

<span data-ttu-id="6d4ac-213">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="6d4ac-213">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="6d4ac-214">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="6d4ac-214">disabledPackageSources</span></span>

<span data-ttu-id="6d4ac-215">Identyfikowane obecnie wyłączone źródła.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-215">Identified currently disabled sources.</span></span> <span data-ttu-id="6d4ac-216">Może być pusta.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-216">May be empty.</span></span>

| <span data-ttu-id="6d4ac-217">Klucz</span><span class="sxs-lookup"><span data-stu-id="6d4ac-217">Key</span></span> | <span data-ttu-id="6d4ac-218">Wartość</span><span class="sxs-lookup"><span data-stu-id="6d4ac-218">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6d4ac-219">(nazwa źródła)</span><span class="sxs-lookup"><span data-stu-id="6d4ac-219">(name of source)</span></span> | <span data-ttu-id="6d4ac-220">Wartość logiczna wskazująca, czy źródło jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-220">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="6d4ac-221">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="6d4ac-221">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="6d4ac-222">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="6d4ac-222">activePackageSource</span></span>

<span data-ttu-id="6d4ac-223">*(tylko 2.x; przestarzałe w wersji 3.x+)*</span><span class="sxs-lookup"><span data-stu-id="6d4ac-223">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="6d4ac-224">Identyfikuje aktualnie aktywne źródło lub wskazuje agregację wszystkich źródeł.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-224">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="6d4ac-225">Klucz</span><span class="sxs-lookup"><span data-stu-id="6d4ac-225">Key</span></span> | <span data-ttu-id="6d4ac-226">Wartość</span><span class="sxs-lookup"><span data-stu-id="6d4ac-226">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6d4ac-227">(nazwa źródła) lub `All`</span><span class="sxs-lookup"><span data-stu-id="6d4ac-227">(name of source) or `All`</span></span> | <span data-ttu-id="6d4ac-228">Jeśli klucz jest nazwą źródła, wartość jest ścieżką źródłową lub adresem URL.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-228">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="6d4ac-229">W `All` przypadku wartości wartość powinna być `(Aggregate source)` taka, aby połączyć wszystkie źródła pakietów, które nie są w przeciwnym razie wyłączone.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-229">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="6d4ac-230">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="6d4ac-230">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="6d4ac-231">sekcja trustedSigners</span><span class="sxs-lookup"><span data-stu-id="6d4ac-231">trustedSigners section</span></span>

<span data-ttu-id="6d4ac-232">Przechowuje zaufanych podpisujących używanych do zezwalania na pakiet podczas instalowania lub przywracania.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-232">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="6d4ac-233">Ta lista nie może być pusta, gdy użytkownik ustawia `signatureValidationMode` na `require` .</span><span class="sxs-lookup"><span data-stu-id="6d4ac-233">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="6d4ac-234">Tę sekcję można zaktualizować za pomocą [ `nuget trusted-signers` polecenia](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="6d4ac-234">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="6d4ac-235">**Schemat**:</span><span class="sxs-lookup"><span data-stu-id="6d4ac-235">**Schema**:</span></span>

<span data-ttu-id="6d4ac-236">Zaufany podpisator ma kolekcję elementów, które zarejestrować wszystkie `certificate` certyfikaty, które identyfikują danego podpiszącego.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-236">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="6d4ac-237">Zaufanym podpisem może być lub `Author` `Repository` .</span><span class="sxs-lookup"><span data-stu-id="6d4ac-237">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="6d4ac-238">Zaufane  repozytorium określa również identyfikator dla repozytorium (który musi być prawidłowym identyfikatorem `serviceIndex` URI) i opcjonalnie może określić listę rozdzieloną średnikami , aby jeszcze bardziej ograniczyć zaufanie do tego konkretnego `https` `owners` repozytorium.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-238">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="6d4ac-239">Obsługiwane algorytmy wyznaczania wartości skrótu używane dla odcisku palca certyfikatu to `SHA256` , `SHA384` i `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="6d4ac-239">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="6d4ac-240">Jeśli element określa, że dany certyfikat może być łańcuchem do niezaufanego katalogu głównego podczas tworzenia łańcucha certyfikatów `certificate` `allowUntrustedRoot` w ramach `true` weryfikacji podpisu.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-240">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="6d4ac-241">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="6d4ac-241">**Example**:</span></span>

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="6d4ac-242">fallbackPackageFolders, sekcja</span><span class="sxs-lookup"><span data-stu-id="6d4ac-242">fallbackPackageFolders section</span></span>

<span data-ttu-id="6d4ac-243">*(3,5+)* Umożliwia preinstalowanie pakietów, dzięki czemu nie trzeba nic robić, jeśli pakiet zostanie znaleziony w folderach rezerwowych.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-243">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="6d4ac-244">Foldery pakietów rezerwowych mają dokładnie taką samą strukturę folderów i plików jak globalny folder pakietów: jest obecny plik *.nupkg,* a wszystkie pliki są wyodrębnione.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-244">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="6d4ac-245">Logika wyszukiwania dla tej konfiguracji jest:</span><span class="sxs-lookup"><span data-stu-id="6d4ac-245">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="6d4ac-246">Poszukaj w globalnym folderze pakietów, aby sprawdzić, czy pakiet/wersja została już pobrana.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-246">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="6d4ac-247">Poszukaj dopasowania pakietu/wersji w folderach rezerwowych.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-247">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="6d4ac-248">Jeśli którekolwiek z tych wyszukiwania powiedzie się, pobieranie nie będzie konieczne.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-248">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="6d4ac-249">Jeśli dopasowanie nie zostanie znalezione, program NuGet sprawdzi źródła plików, a następnie źródła http, a następnie pobierze pakiety.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-249">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="6d4ac-250">Klucz</span><span class="sxs-lookup"><span data-stu-id="6d4ac-250">Key</span></span> | <span data-ttu-id="6d4ac-251">Wartość</span><span class="sxs-lookup"><span data-stu-id="6d4ac-251">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6d4ac-252">(nazwa folderu rezerwowego)</span><span class="sxs-lookup"><span data-stu-id="6d4ac-252">(name of fallback folder)</span></span> | <span data-ttu-id="6d4ac-253">Ścieżka do folderu rezerwowego.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-253">Path to fallback folder.</span></span> |

<span data-ttu-id="6d4ac-254">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="6d4ac-254">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="6d4ac-255">sekcja packageManagement</span><span class="sxs-lookup"><span data-stu-id="6d4ac-255">packageManagement section</span></span>

<span data-ttu-id="6d4ac-256">Ustawia domyślny format zarządzania pakietami, *packages.config* PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-256">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="6d4ac-257">Projekty w stylu zestawu SDK zawsze używają funkcji PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-257">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="6d4ac-258">Klucz</span><span class="sxs-lookup"><span data-stu-id="6d4ac-258">Key</span></span> | <span data-ttu-id="6d4ac-259">Wartość</span><span class="sxs-lookup"><span data-stu-id="6d4ac-259">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6d4ac-260">format</span><span class="sxs-lookup"><span data-stu-id="6d4ac-260">format</span></span> | <span data-ttu-id="6d4ac-261">Wartość logiczna wskazująca domyślny format zarządzania pakietami.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-261">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="6d4ac-262">Jeśli `1` , format to PackageReference.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-262">If `1`, format is PackageReference.</span></span> <span data-ttu-id="6d4ac-263">Jeśli `0` , format jest *packages.config*.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-263">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="6d4ac-264">wyłączone</span><span class="sxs-lookup"><span data-stu-id="6d4ac-264">disabled</span></span> | <span data-ttu-id="6d4ac-265">Wartość logiczna wskazująca, czy podczas pierwszej instalacji pakietu ma być wyświetlany monit o wybranie domyślnego formatu pakietu.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-265">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="6d4ac-266">`False` Ukrywa monit.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-266">`False` hides the prompt.</span></span> |

<span data-ttu-id="6d4ac-267">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="6d4ac-267">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="6d4ac-268">Korzystanie ze zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="6d4ac-268">Using environment variables</span></span>

<span data-ttu-id="6d4ac-269">Możesz użyć zmiennych środowiskowych w `nuget.config` wartościach (NuGet 3.4+), aby zastosować ustawienia w czasie uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-269">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="6d4ac-270">Jeśli na przykład zmienna środowiskowa w systemie Windows jest ustawiona na wartość , wartość w pliku konfiguracji jest `HOME` `c:\users\username` `%HOME%\NuGetRepository` rozpoznana jako `c:\users\username\NuGetRepository` .</span><span class="sxs-lookup"><span data-stu-id="6d4ac-270">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="6d4ac-271">Należy pamiętać, że należy używać zmiennych środowiskowych w stylu systemu Windows (rozpoczyna się i kończy na %) nawet w systemie Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-271">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="6d4ac-272">Nie `$HOME/NuGetRepository` można rozwiązać problemu z plikiem konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-272">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="6d4ac-273">W systemie Mac/Linux wartość będzie `%HOME%/NuGetRepository` rozpoznawiona jako `/home/myStuff/NuGetRepository` .</span><span class="sxs-lookup"><span data-stu-id="6d4ac-273">On Mac/Linux the value of `%HOME%/NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="6d4ac-274">Jeśli zmienna środowiskowa nie zostanie znaleziona, program NuGet użyje wartości literału z pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-274">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span> <span data-ttu-id="6d4ac-275">Na przykład `%MY_UNDEFINED_VAR%/NuGetRepository` zostanie rozpoznany jako `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span><span class="sxs-lookup"><span data-stu-id="6d4ac-275">For example `%MY_UNDEFINED_VAR%/NuGetRepository` will be resolved as `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span></span>

<span data-ttu-id="6d4ac-276">W poniższej tabeli przedstawiono składnię zmiennych środowiska i obsługę separatora ścieżek NuGet.Config plików.</span><span class="sxs-lookup"><span data-stu-id="6d4ac-276">The table below show environnment variable syntax and path separator support for NuGet.Config files.</span></span>

### <a name="nugetconfig-environment-variable-support"></a><span data-ttu-id="6d4ac-277">`NuGet.Config` obsługa zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="6d4ac-277">`NuGet.Config` environment variable support</span></span>

| <span data-ttu-id="6d4ac-278">Składnia</span><span class="sxs-lookup"><span data-stu-id="6d4ac-278">Syntax</span></span> | <span data-ttu-id="6d4ac-279">Separator Dir</span><span class="sxs-lookup"><span data-stu-id="6d4ac-279">Dir separator</span></span> | <span data-ttu-id="6d4ac-280">Windows nuget.exe</span><span class="sxs-lookup"><span data-stu-id="6d4ac-280">Windows nuget.exe</span></span> | <span data-ttu-id="6d4ac-281">Windows dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="6d4ac-281">Windows dotnet.exe</span></span> | <span data-ttu-id="6d4ac-282">Mac nuget.exe (w mono)</span><span class="sxs-lookup"><span data-stu-id="6d4ac-282">Mac nuget.exe (in Mono)</span></span> | <span data-ttu-id="6d4ac-283">Mac dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="6d4ac-283">Mac dotnet.exe</span></span> |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | <span data-ttu-id="6d4ac-284">Tak</span><span class="sxs-lookup"><span data-stu-id="6d4ac-284">Yes</span></span> | <span data-ttu-id="6d4ac-285">Tak</span><span class="sxs-lookup"><span data-stu-id="6d4ac-285">Yes</span></span> | <span data-ttu-id="6d4ac-286">Tak</span><span class="sxs-lookup"><span data-stu-id="6d4ac-286">Yes</span></span> | <span data-ttu-id="6d4ac-287">Tak</span><span class="sxs-lookup"><span data-stu-id="6d4ac-287">Yes</span></span> |
| `%MY_VAR%` | `\`  | <span data-ttu-id="6d4ac-288">Tak</span><span class="sxs-lookup"><span data-stu-id="6d4ac-288">Yes</span></span> | <span data-ttu-id="6d4ac-289">Tak</span><span class="sxs-lookup"><span data-stu-id="6d4ac-289">Yes</span></span> | <span data-ttu-id="6d4ac-290">Nie</span><span class="sxs-lookup"><span data-stu-id="6d4ac-290">No</span></span> | <span data-ttu-id="6d4ac-291">Nie</span><span class="sxs-lookup"><span data-stu-id="6d4ac-291">No</span></span> |
| `$MY_VAR` | `/`  | <span data-ttu-id="6d4ac-292">Nie</span><span class="sxs-lookup"><span data-stu-id="6d4ac-292">No</span></span> | <span data-ttu-id="6d4ac-293">Nie</span><span class="sxs-lookup"><span data-stu-id="6d4ac-293">No</span></span> | <span data-ttu-id="6d4ac-294">Nie</span><span class="sxs-lookup"><span data-stu-id="6d4ac-294">No</span></span> | <span data-ttu-id="6d4ac-295">Nie</span><span class="sxs-lookup"><span data-stu-id="6d4ac-295">No</span></span> |
| `$MY_VAR` | `\`  | <span data-ttu-id="6d4ac-296">Nie</span><span class="sxs-lookup"><span data-stu-id="6d4ac-296">No</span></span> | <span data-ttu-id="6d4ac-297">Nie</span><span class="sxs-lookup"><span data-stu-id="6d4ac-297">No</span></span> | <span data-ttu-id="6d4ac-298">Nie</span><span class="sxs-lookup"><span data-stu-id="6d4ac-298">No</span></span> | <span data-ttu-id="6d4ac-299">Nie</span><span class="sxs-lookup"><span data-stu-id="6d4ac-299">No</span></span> |


## <a name="example-config-file"></a><span data-ttu-id="6d4ac-300">Przykładowy plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="6d4ac-300">Example config file</span></span>

<span data-ttu-id="6d4ac-301">Poniżej znajduje się `nuget.config` przykładowy plik, który ilustruje wiele ustawień, w tym opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="6d4ac-301">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

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
            <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <certificate fingerprint="5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
