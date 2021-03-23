---
title: Odwołanie do pliku nuget.config
description: NuGet.Config odwołanie do pliku, w tym sekcje config, bindingRedirects, packageRestore, Solution i packageSource.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: afc06c81bf0344f2086efd19111cc60d24d7f723
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859515"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="269b0-103">Informacje nuget.config</span><span class="sxs-lookup"><span data-stu-id="269b0-103">nuget.config reference</span></span>

<span data-ttu-id="269b0-104">Zachowanie NuGet jest kontrolowane przez ustawienia w różnych `NuGet.Config` lub `nuget.config` plikach, zgodnie z opisem w temacie [typowe konfiguracje programu NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="269b0-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="269b0-105">`nuget.config` jest plikiem XML zawierającym węzeł najwyższego poziomu `<configuration>` , który zawiera elementy sekcji opisane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="269b0-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="269b0-106">Każda sekcja zawiera zero lub więcej elementów.</span><span class="sxs-lookup"><span data-stu-id="269b0-106">Each section contains zero or more items.</span></span> <span data-ttu-id="269b0-107">Zobacz [przykład pliku konfiguracji](#example-config-file).</span><span class="sxs-lookup"><span data-stu-id="269b0-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="269b0-108">W nazwach ustawień jest rozróżniana wielkość liter, a wartości mogą używać [zmiennych środowiskowych](#using-environment-variables).</span><span class="sxs-lookup"><span data-stu-id="269b0-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="269b0-109">sekcja konfiguracji</span><span class="sxs-lookup"><span data-stu-id="269b0-109">config section</span></span>

<span data-ttu-id="269b0-110">Zawiera różne ustawienia konfiguracji, które można ustawić za pomocą [ `nuget config` polecenia](../reference/cli-reference/cli-ref-config.md).</span><span class="sxs-lookup"><span data-stu-id="269b0-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="269b0-111">`dependencyVersion` i `repositoryPath` mają zastosowanie tylko do projektów korzystających z programu `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="269b0-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="269b0-112">`globalPackagesFolder` dotyczy tylko projektów przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="269b0-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="269b0-113">Klucz</span><span class="sxs-lookup"><span data-stu-id="269b0-113">Key</span></span> | <span data-ttu-id="269b0-114">Wartość</span><span class="sxs-lookup"><span data-stu-id="269b0-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="269b0-115">dependencyVersion ( `packages.config` tylko)</span><span class="sxs-lookup"><span data-stu-id="269b0-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="269b0-116">Wartość domyślna `DependencyVersion` instalacji, przywracania i aktualizacji pakietu, gdy `-DependencyVersion` przełącznik nie jest określony bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="269b0-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="269b0-117">Ta wartość jest również używana przez interfejs użytkownika Menedżera pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="269b0-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="269b0-118">Wartości to `Lowest` , `HighestPatch` , `HighestMinor` , `Highest` .</span><span class="sxs-lookup"><span data-stu-id="269b0-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="269b0-119">globalPackagesFolder (projekty korzystające tylko z PackageReference)</span><span class="sxs-lookup"><span data-stu-id="269b0-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="269b0-120">Lokalizacja domyślnego folderu pakiety globalne.</span><span class="sxs-lookup"><span data-stu-id="269b0-120">The location of the default global packages folder.</span></span> <span data-ttu-id="269b0-121">Wartość domyślna to `%userprofile%\.nuget\packages` (Windows) lub `~/.nuget/packages` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="269b0-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="269b0-122">Ścieżka względna może być używana w plikach specyficznych dla projektu `nuget.config` .</span><span class="sxs-lookup"><span data-stu-id="269b0-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="269b0-123">To ustawienie jest zastępowane przez `NUGET_PACKAGES` zmienną środowiskową, która ma pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="269b0-123">This setting is overridden by the `NUGET_PACKAGES` environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="269b0-124">repositoryPath ( `packages.config` tylko)</span><span class="sxs-lookup"><span data-stu-id="269b0-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="269b0-125">Lokalizacja, w której mają zostać zainstalowane pakiety NuGet zamiast folderu domyślnego `$(Solutiondir)/packages` .</span><span class="sxs-lookup"><span data-stu-id="269b0-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="269b0-126">Ścieżka względna może być używana w plikach specyficznych dla projektu `nuget.config` .</span><span class="sxs-lookup"><span data-stu-id="269b0-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="269b0-127">To ustawienie jest zastępowane przez `NUGET_PACKAGES` zmienną środowiskową, która ma pierwszeństwo.</span><span class="sxs-lookup"><span data-stu-id="269b0-127">This setting is overridden by the `NUGET_PACKAGES` environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="269b0-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="269b0-128">defaultPushSource</span></span> | <span data-ttu-id="269b0-129">Określa adres URL lub ścieżkę źródła pakietu, które ma być używane jako wartość domyślna, jeśli nie znaleziono żadnych innych źródeł pakietów dla operacji.</span><span class="sxs-lookup"><span data-stu-id="269b0-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="269b0-130">http_proxy http_proxy. User http_proxy. Password no_proxy</span><span class="sxs-lookup"><span data-stu-id="269b0-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="269b0-131">Ustawienia serwera proxy do użycia podczas nawiązywania połączenia ze źródłami pakietów; `http_proxy` powinien mieć format `http://<username>:<password>@<domain>` .</span><span class="sxs-lookup"><span data-stu-id="269b0-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="269b0-132">Hasła są szyfrowane i nie można ich dodać ręcznie.</span><span class="sxs-lookup"><span data-stu-id="269b0-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="269b0-133">W przypadku `no_proxy` , wartość jest rozdzielaną przecinkami listą domen, które pomijają serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="269b0-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="269b0-134">Dla tych wartości można użyć zmiennych środowiskowych http_proxy i no_proxy.</span><span class="sxs-lookup"><span data-stu-id="269b0-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="269b0-135">Aby uzyskać więcej informacji, zobacz [Ustawienia serwera proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span><span class="sxs-lookup"><span data-stu-id="269b0-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="269b0-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="269b0-136">signatureValidationMode</span></span> | <span data-ttu-id="269b0-137">Określa tryb weryfikacji używany do weryfikowania podpisów pakietów na potrzeby instalacji pakietu i przywracania.</span><span class="sxs-lookup"><span data-stu-id="269b0-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="269b0-138">Wartości to `accept` , `require` .</span><span class="sxs-lookup"><span data-stu-id="269b0-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="269b0-139">Wartość domyślna to `accept` .</span><span class="sxs-lookup"><span data-stu-id="269b0-139">Defaults to `accept`.</span></span>

<span data-ttu-id="269b0-140">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="269b0-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="269b0-141">Sekcja bindingRedirects</span><span class="sxs-lookup"><span data-stu-id="269b0-141">bindingRedirects section</span></span>

<span data-ttu-id="269b0-142">Określa, czy program NuGet ma przekierować automatyczne powiązania po zainstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="269b0-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="269b0-143">Klucz</span><span class="sxs-lookup"><span data-stu-id="269b0-143">Key</span></span> | <span data-ttu-id="269b0-144">Wartość</span><span class="sxs-lookup"><span data-stu-id="269b0-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="269b0-145">Pomiń</span><span class="sxs-lookup"><span data-stu-id="269b0-145">skip</span></span> | <span data-ttu-id="269b0-146">Wartość logiczna wskazująca, czy pomijać Automatyczne przekierowania powiązań.</span><span class="sxs-lookup"><span data-stu-id="269b0-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="269b0-147">Wartością domyślną jest false.</span><span class="sxs-lookup"><span data-stu-id="269b0-147">The default is false.</span></span> |

<span data-ttu-id="269b0-148">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="269b0-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="269b0-149">Sekcja packageRestore</span><span class="sxs-lookup"><span data-stu-id="269b0-149">packageRestore section</span></span>

<span data-ttu-id="269b0-150">Kontroluje przywracanie pakietu podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="269b0-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="269b0-151">Klucz</span><span class="sxs-lookup"><span data-stu-id="269b0-151">Key</span></span> | <span data-ttu-id="269b0-152">Wartość</span><span class="sxs-lookup"><span data-stu-id="269b0-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="269b0-153">enabled</span><span class="sxs-lookup"><span data-stu-id="269b0-153">enabled</span></span> | <span data-ttu-id="269b0-154">Wartość logiczna wskazująca, czy pakiet NuGet może wykonywać automatyczne przywracanie.</span><span class="sxs-lookup"><span data-stu-id="269b0-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="269b0-155">Można również ustawić dla `EnableNuGetPackageRestore` zmiennej środowiskowej wartość `True` zamiast ustawienia tego klucza w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="269b0-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="269b0-156">automatyczne</span><span class="sxs-lookup"><span data-stu-id="269b0-156">automatic</span></span> | <span data-ttu-id="269b0-157">Wartość logiczna wskazująca, czy NuGet ma sprawdzać brakujące pakiety podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="269b0-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="269b0-158">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="269b0-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="269b0-159">Sekcja rozwiązania</span><span class="sxs-lookup"><span data-stu-id="269b0-159">solution section</span></span>

<span data-ttu-id="269b0-160">Określa, czy `packages` folder rozwiązania ma być uwzględniony w kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="269b0-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="269b0-161">Ta sekcja działa tylko w `nuget.config` plikach w folderze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="269b0-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="269b0-162">Klucz</span><span class="sxs-lookup"><span data-stu-id="269b0-162">Key</span></span> | <span data-ttu-id="269b0-163">Wartość</span><span class="sxs-lookup"><span data-stu-id="269b0-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="269b0-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="269b0-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="269b0-165">Wartość logiczna wskazująca, czy ignorować folder Packages podczas pracy z kontrolą źródła.</span><span class="sxs-lookup"><span data-stu-id="269b0-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="269b0-166">Wartość domyślna to false.</span><span class="sxs-lookup"><span data-stu-id="269b0-166">The default value is false.</span></span> |

<span data-ttu-id="269b0-167">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="269b0-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="269b0-168">Sekcje źródłowe pakietu</span><span class="sxs-lookup"><span data-stu-id="269b0-168">Package source sections</span></span>

<span data-ttu-id="269b0-169">`packageSources`,, `packageSourceCredentials` `apikeys` , `activePackageSource` `disabledPackageSources` I `trustedSigners` wszystkie współpracują ze sobą, aby skonfigurować sposób działania programu NuGet z repozytoriami pakietów podczas operacji instalowania, przywracania i aktualizowania.</span><span class="sxs-lookup"><span data-stu-id="269b0-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="269b0-170">[ `nuget sources` Polecenie](../reference/cli-reference/cli-ref-sources.md) jest zwykle używane do zarządzania tymi ustawieniami, z wyjątkiem tego, `apikeys` które jest zarządzane za pomocą [ `nuget setapikey` polecenia](../reference/cli-reference/cli-ref-setapikey.md), i `trustedSigners` które jest zarządzane za pomocą [ `nuget trusted-signers` polecenia](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="269b0-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="269b0-171">Należy pamiętać, że źródłowy adres URL dla nuget.org to `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="269b0-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="269b0-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="269b0-172">packageSources</span></span>

<span data-ttu-id="269b0-173">Wyświetla wszystkie znane źródła pakietów.</span><span class="sxs-lookup"><span data-stu-id="269b0-173">Lists all known package sources.</span></span> <span data-ttu-id="269b0-174">Kolejność jest ignorowana podczas operacji przywracania i dowolnego projektu przy użyciu formatu PackageReference.</span><span class="sxs-lookup"><span data-stu-id="269b0-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="269b0-175">Pakiet NuGet szanuje kolejność źródeł dla operacji instalacji i aktualizacji z projektami przy użyciu programu `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="269b0-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="269b0-176">Klucz</span><span class="sxs-lookup"><span data-stu-id="269b0-176">Key</span></span> | <span data-ttu-id="269b0-177">Wartość</span><span class="sxs-lookup"><span data-stu-id="269b0-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="269b0-178">(nazwa do przypisania do źródła pakietu)</span><span class="sxs-lookup"><span data-stu-id="269b0-178">(name to assign to the package source)</span></span> | <span data-ttu-id="269b0-179">Ścieżka lub adres URL źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="269b0-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="269b0-180">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="269b0-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> <span data-ttu-id="269b0-181">Gdy `<clear />` jest obecny dla danego węzła, pakiet NuGet ignoruje wcześniej zdefiniowane wartości konfiguracji dla tego węzła.</span><span class="sxs-lookup"><span data-stu-id="269b0-181">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span> <span data-ttu-id="269b0-182">[Przeczytaj więcej na temat sposobu stosowania ustawień](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span><span class="sxs-lookup"><span data-stu-id="269b0-182">[Read more about how settings are applied](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

### <a name="packagesourcecredentials"></a><span data-ttu-id="269b0-183">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="269b0-183">packageSourceCredentials</span></span>

<span data-ttu-id="269b0-184">Przechowuje nazwy użytkowników i hasła dla źródeł, zwykle określone przy użyciu `-username` `-password` przełączników i `nuget sources` .</span><span class="sxs-lookup"><span data-stu-id="269b0-184">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="269b0-185">Hasła są szyfrowane domyślnie, chyba że `-storepasswordincleartext` jest również używana opcja.</span><span class="sxs-lookup"><span data-stu-id="269b0-185">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>
<span data-ttu-id="269b0-186">Opcjonalnie można określić prawidłowe typy uwierzytelniania za pomocą `-validauthenticationtypes` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="269b0-186">Optionally, valid authentication types can be specified with the `-validauthenticationtypes` switch.</span></span>

| <span data-ttu-id="269b0-187">Klucz</span><span class="sxs-lookup"><span data-stu-id="269b0-187">Key</span></span> | <span data-ttu-id="269b0-188">Wartość</span><span class="sxs-lookup"><span data-stu-id="269b0-188">Value</span></span> |
| --- | --- |
| <span data-ttu-id="269b0-189">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="269b0-189">username</span></span> | <span data-ttu-id="269b0-190">Nazwa użytkownika dla źródła w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="269b0-190">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="269b0-191">hasło</span><span class="sxs-lookup"><span data-stu-id="269b0-191">password</span></span> | <span data-ttu-id="269b0-192">Hasło zaszyfrowane dla źródła.</span><span class="sxs-lookup"><span data-stu-id="269b0-192">The encrypted password for the source.</span></span> <span data-ttu-id="269b0-193">Hasła szyfrowane są obsługiwane tylko w systemie Windows i mogą być odszyfrowywane tylko wtedy, gdy są używane na tym samym komputerze i za pośrednictwem tego samego użytkownika co oryginalne szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="269b0-193">Encrypted passwords are only supported on Windows, and only can be decrypted when used on the same machine and via the same user as the original encryption.</span></span> |
| <span data-ttu-id="269b0-194">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="269b0-194">cleartextpassword</span></span> | <span data-ttu-id="269b0-195">Niezaszyfrowane hasło dla źródła.</span><span class="sxs-lookup"><span data-stu-id="269b0-195">The unencrypted password for the source.</span></span> <span data-ttu-id="269b0-196">Uwaga: zmienne środowiskowe mogą być używane w celu zwiększenia bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="269b0-196">Note: environment variables can be used for improved security.</span></span> |
| <span data-ttu-id="269b0-197">validauthenticationtypes</span><span class="sxs-lookup"><span data-stu-id="269b0-197">validauthenticationtypes</span></span> | <span data-ttu-id="269b0-198">Rozdzielana przecinkami lista prawidłowych typów uwierzytelniania dla tego źródła.</span><span class="sxs-lookup"><span data-stu-id="269b0-198">Comma-separated list of valid authentication types for this source.</span></span> <span data-ttu-id="269b0-199">Ustaw tę opcję na `basic` , jeśli serwer anonsuje protokół NTLM lub Negocjuj, a Twoje poświadczenia muszą być wysyłane przy użyciu podstawowego mechanizmu, na przykład w przypadku korzystania z elementu "% Azure DevOps Server".</span><span class="sxs-lookup"><span data-stu-id="269b0-199">Set this to `basic` if the server advertises NTLM or Negotiate and your credentials must be sent using the Basic mechanism, for instance when using a PAT with on-premises Azure DevOps Server.</span></span> <span data-ttu-id="269b0-200">Inne prawidłowe wartości to `negotiate` , `kerberos` , `ntlm` , i `digest` , ale te wartości są prawdopodobnie przydatne.</span><span class="sxs-lookup"><span data-stu-id="269b0-200">Other valid values include `negotiate`, `kerberos`, `ntlm`, and `digest`, but these values are unlikely to be useful.</span></span> |

<span data-ttu-id="269b0-201">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="269b0-201">**Example:**</span></span>

<span data-ttu-id="269b0-202">W pliku konfiguracji `<packageSourceCredentials>` element zawiera węzły podrzędne dla każdej stosownej nazwy źródłowej (spacje w nazwie są zastępowane `_x0020_` ).</span><span class="sxs-lookup"><span data-stu-id="269b0-202">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="269b0-203">Oznacza to, że w przypadku źródeł o nazwach "contoso" i "Źródło testowe" plik konfiguracyjny zawiera następujące dane w przypadku korzystania z szyfrowanych haseł:</span><span class="sxs-lookup"><span data-stu-id="269b0-203">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="269b0-204">W przypadku korzystania z niezaszyfrowanych haseł przechowywanych w zmiennej środowiskowej:</span><span class="sxs-lookup"><span data-stu-id="269b0-204">When using unencrypted passwords stored in an environment variable:</span></span>

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

<span data-ttu-id="269b0-205">W przypadku korzystania z nieszyfrowanych haseł:</span><span class="sxs-lookup"><span data-stu-id="269b0-205">When using unencrypted passwords:</span></span>

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

<span data-ttu-id="269b0-206">Ponadto można podać prawidłowe metody uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="269b0-206">Additionally, valid authentication methods can be supplied:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="269b0-207">apikeys</span><span class="sxs-lookup"><span data-stu-id="269b0-207">apikeys</span></span>

<span data-ttu-id="269b0-208">Przechowuje klucze dla źródeł korzystających z uwierzytelniania za pomocą klucza interfejsu API, jak określono za pomocą [ `nuget setapikey` polecenia](../reference/cli-reference/cli-ref-setapikey.md).</span><span class="sxs-lookup"><span data-stu-id="269b0-208">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="269b0-209">Klucz</span><span class="sxs-lookup"><span data-stu-id="269b0-209">Key</span></span> | <span data-ttu-id="269b0-210">Wartość</span><span class="sxs-lookup"><span data-stu-id="269b0-210">Value</span></span> |
| --- | --- |
| <span data-ttu-id="269b0-211">(źródłowy adres URL)</span><span class="sxs-lookup"><span data-stu-id="269b0-211">(source URL)</span></span> | <span data-ttu-id="269b0-212">Zaszyfrowany klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="269b0-212">The encrypted API key.</span></span> |

<span data-ttu-id="269b0-213">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="269b0-213">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="269b0-214">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="269b0-214">disabledPackageSources</span></span>

<span data-ttu-id="269b0-215">Zidentyfikowano aktualnie wyłączone źródła.</span><span class="sxs-lookup"><span data-stu-id="269b0-215">Identified currently disabled sources.</span></span> <span data-ttu-id="269b0-216">Może być pusty.</span><span class="sxs-lookup"><span data-stu-id="269b0-216">May be empty.</span></span>

| <span data-ttu-id="269b0-217">Klucz</span><span class="sxs-lookup"><span data-stu-id="269b0-217">Key</span></span> | <span data-ttu-id="269b0-218">Wartość</span><span class="sxs-lookup"><span data-stu-id="269b0-218">Value</span></span> |
| --- | --- |
| <span data-ttu-id="269b0-219">(nazwa źródła)</span><span class="sxs-lookup"><span data-stu-id="269b0-219">(name of source)</span></span> | <span data-ttu-id="269b0-220">Wartość logiczna wskazująca, czy źródło jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="269b0-220">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="269b0-221">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="269b0-221">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="269b0-222">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="269b0-222">activePackageSource</span></span>

<span data-ttu-id="269b0-223">*(tylko 2. x; przestarzałe w 3. x +)*</span><span class="sxs-lookup"><span data-stu-id="269b0-223">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="269b0-224">Identyfikuje aktualnie aktywne źródło lub wskazuje zagregowane wszystkie źródła.</span><span class="sxs-lookup"><span data-stu-id="269b0-224">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="269b0-225">Klucz</span><span class="sxs-lookup"><span data-stu-id="269b0-225">Key</span></span> | <span data-ttu-id="269b0-226">Wartość</span><span class="sxs-lookup"><span data-stu-id="269b0-226">Value</span></span> |
| --- | --- |
| <span data-ttu-id="269b0-227">(nazwa źródła) lub `All`</span><span class="sxs-lookup"><span data-stu-id="269b0-227">(name of source) or `All`</span></span> | <span data-ttu-id="269b0-228">Jeśli klucz jest nazwą źródła, wartość jest ścieżką źródłową lub adresem URL.</span><span class="sxs-lookup"><span data-stu-id="269b0-228">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="269b0-229">Jeśli `All` wartość powinna być `(Aggregate source)` połączona ze wszystkimi źródłami pakietów, które nie są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="269b0-229">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="269b0-230">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="269b0-230">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="269b0-231">Sekcja trustedSigners</span><span class="sxs-lookup"><span data-stu-id="269b0-231">trustedSigners section</span></span>

<span data-ttu-id="269b0-232">Przechowuje zaufane osoby podpisujące używane do zezwalania na pakiet podczas instalowania lub przywracania.</span><span class="sxs-lookup"><span data-stu-id="269b0-232">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="269b0-233">Ta lista nie może być pusta, jeśli użytkownik `signatureValidationMode` ustawi `require` .</span><span class="sxs-lookup"><span data-stu-id="269b0-233">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="269b0-234">Tę sekcję można zaktualizować za pomocą [ `nuget trusted-signers` polecenia](../reference/cli-reference/cli-ref-trusted-signers.md).</span><span class="sxs-lookup"><span data-stu-id="269b0-234">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="269b0-235">**Schemat**:</span><span class="sxs-lookup"><span data-stu-id="269b0-235">**Schema**:</span></span>

<span data-ttu-id="269b0-236">Zaufany podpiser zawiera kolekcję `certificate` elementów, które identyfikują wszystkie certyfikaty identyfikujące daną rejestrację.</span><span class="sxs-lookup"><span data-stu-id="269b0-236">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="269b0-237">Zaufaną rejestracją może być albo `Author` lub `Repository` .</span><span class="sxs-lookup"><span data-stu-id="269b0-237">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="269b0-238">Zaufane *repozytorium* określa również `serviceIndex` dla repozytorium (które musi być prawidłowym `https` identyfikatorem URI) i opcjonalnie określać listę rozdzielaną średnikami, aby ograniczyć liczbę elementów, które `owners` są zaufane z tego konkretnego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="269b0-238">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="269b0-239">Obsługiwane algorytmy wyznaczania wartości skrótu używane dla odcisku palca certyfikatu to `SHA256` , `SHA384` i `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="269b0-239">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="269b0-240">Jeśli `certificate` określono `allowUntrustedRoot` , że `true` dany certyfikat jest dozwolony do łączenia się z niezaufanym katalogiem głównym, podczas budowania łańcucha certyfikatów w ramach weryfikacji podpisu.</span><span class="sxs-lookup"><span data-stu-id="269b0-240">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="269b0-241">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="269b0-241">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="269b0-242">Sekcja fallbackPackageFolders</span><span class="sxs-lookup"><span data-stu-id="269b0-242">fallbackPackageFolders section</span></span>

<span data-ttu-id="269b0-243">*(3.5 +)* Zapewnia możliwość preinstalacji pakietów, dzięki czemu nie trzeba wykonywać żadnych zadań, jeśli pakiet znajduje się w folderach rezerwowych.</span><span class="sxs-lookup"><span data-stu-id="269b0-243">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="269b0-244">Foldery pakietu rezerwowego mają dokładnie ten sam folder i strukturę plików, co folder pakietu globalnego: *. nupkg* jest obecny i wszystkie pliki są wyodrębniane.</span><span class="sxs-lookup"><span data-stu-id="269b0-244">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="269b0-245">Logika wyszukiwania dla tej konfiguracji to:</span><span class="sxs-lookup"><span data-stu-id="269b0-245">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="269b0-246">Spójrz na folder pakietu globalnego, aby sprawdzić, czy pakiet/wersja została już pobrana.</span><span class="sxs-lookup"><span data-stu-id="269b0-246">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="269b0-247">Sprawdź, czy w folderach rezerwowych znajduje się zgodność z pakietem/wersją.</span><span class="sxs-lookup"><span data-stu-id="269b0-247">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="269b0-248">Jeśli wyszukiwanie zakończyło się pomyślnie, pobieranie nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="269b0-248">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="269b0-249">Jeśli dopasowanie nie zostanie znalezione, pakiet NuGet sprawdza źródła plików, a następnie źródła http, a następnie pobiera pakiety.</span><span class="sxs-lookup"><span data-stu-id="269b0-249">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="269b0-250">Klucz</span><span class="sxs-lookup"><span data-stu-id="269b0-250">Key</span></span> | <span data-ttu-id="269b0-251">Wartość</span><span class="sxs-lookup"><span data-stu-id="269b0-251">Value</span></span> |
| --- | --- |
| <span data-ttu-id="269b0-252">(nazwa folderu rezerwowego)</span><span class="sxs-lookup"><span data-stu-id="269b0-252">(name of fallback folder)</span></span> | <span data-ttu-id="269b0-253">Ścieżka do folderu rezerwowego.</span><span class="sxs-lookup"><span data-stu-id="269b0-253">Path to fallback folder.</span></span> |

<span data-ttu-id="269b0-254">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="269b0-254">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="269b0-255">Sekcja packageManagement</span><span class="sxs-lookup"><span data-stu-id="269b0-255">packageManagement section</span></span>

<span data-ttu-id="269b0-256">Ustawia domyślny format zarządzania pakietami, *packages.config* lub PackageReference.</span><span class="sxs-lookup"><span data-stu-id="269b0-256">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="269b0-257">Projekty w stylu zestawu SDK zawsze używają PackageReference.</span><span class="sxs-lookup"><span data-stu-id="269b0-257">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="269b0-258">Klucz</span><span class="sxs-lookup"><span data-stu-id="269b0-258">Key</span></span> | <span data-ttu-id="269b0-259">Wartość</span><span class="sxs-lookup"><span data-stu-id="269b0-259">Value</span></span> |
| --- | --- |
| <span data-ttu-id="269b0-260">format</span><span class="sxs-lookup"><span data-stu-id="269b0-260">format</span></span> | <span data-ttu-id="269b0-261">Wartość logiczna wskazująca domyślny format zarządzania pakietami.</span><span class="sxs-lookup"><span data-stu-id="269b0-261">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="269b0-262">Jeśli `1` , format jest PackageReference.</span><span class="sxs-lookup"><span data-stu-id="269b0-262">If `1`, format is PackageReference.</span></span> <span data-ttu-id="269b0-263">Jeśli `0` Format jest *packages.config*.</span><span class="sxs-lookup"><span data-stu-id="269b0-263">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="269b0-264">wyłączone</span><span class="sxs-lookup"><span data-stu-id="269b0-264">disabled</span></span> | <span data-ttu-id="269b0-265">Wartość logiczna wskazująca, czy wyświetlać monit o wybranie domyślnego formatu pakietu przy pierwszej instalacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="269b0-265">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="269b0-266">`False` ukrywa monit.</span><span class="sxs-lookup"><span data-stu-id="269b0-266">`False` hides the prompt.</span></span> |

<span data-ttu-id="269b0-267">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="269b0-267">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="269b0-268">Korzystanie ze zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="269b0-268">Using environment variables</span></span>

<span data-ttu-id="269b0-269">Możesz użyć zmiennych środowiskowych w `nuget.config` wartościach (NuGet 3.4 +), aby zastosować ustawienia w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="269b0-269">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="269b0-270">Na przykład jeśli `HOME` zmienna środowiskowa w systemie Windows jest ustawiona na `c:\users\username` , wartość `%HOME%\NuGetRepository` w pliku konfiguracji jest rozpoznawana jako `c:\users\username\NuGetRepository` .</span><span class="sxs-lookup"><span data-stu-id="269b0-270">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="269b0-271">Należy pamiętać, że należy używać zmiennych środowiskowych w stylu systemu Windows (rozpoczyna się i kończą z%) nawet w systemie Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="269b0-271">Note that you have to use Windows-style environment variables (starts and ends with %) even on Mac/Linux.</span></span> <span data-ttu-id="269b0-272">Posiadanie `$HOME/NuGetRepository` w pliku konfiguracji nie zostanie rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="269b0-272">Having `$HOME/NuGetRepository` in a configuration file will not resolve.</span></span> <span data-ttu-id="269b0-273">W systemie Mac/Linux wartość `%HOME%/NuGetRepository` zostanie rozwiązany `/home/myStuff/NuGetRepository` .</span><span class="sxs-lookup"><span data-stu-id="269b0-273">On Mac/Linux the value of `%HOME%/NuGetRepository` will resolve to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="269b0-274">Jeśli zmienna środowiskowa nie zostanie znaleziona, NuGet używa wartości literału z pliku konfiguracyjnego.</span><span class="sxs-lookup"><span data-stu-id="269b0-274">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span> <span data-ttu-id="269b0-275">Na przykład `%MY_UNDEFINED_VAR%/NuGetRepository` zostanie rozpoznany jako `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span><span class="sxs-lookup"><span data-stu-id="269b0-275">For example `%MY_UNDEFINED_VAR%/NuGetRepository` will be resolved as `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`</span></span>

<span data-ttu-id="269b0-276">W poniższej tabeli przedstawiono obsługę składni wirtualnym zmiennych i separator ścieżki dla plików NuGet.Config.</span><span class="sxs-lookup"><span data-stu-id="269b0-276">The table below show environnment variable syntax and path separator support for NuGet.Config files.</span></span>

### <a name="nugetconfig-environment-variable-support"></a><span data-ttu-id="269b0-277">Obsługa zmiennej środowiskowej NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="269b0-277">NuGet.Config environment variable support</span></span>

| <span data-ttu-id="269b0-278">Składnia</span><span class="sxs-lookup"><span data-stu-id="269b0-278">Syntax</span></span> | <span data-ttu-id="269b0-279">Separator dir</span><span class="sxs-lookup"><span data-stu-id="269b0-279">Dir separator</span></span> | <span data-ttu-id="269b0-280">nuget.exe systemu Windows</span><span class="sxs-lookup"><span data-stu-id="269b0-280">Windows nuget.exe</span></span> | <span data-ttu-id="269b0-281">dotnet.exe systemu Windows</span><span class="sxs-lookup"><span data-stu-id="269b0-281">Windows dotnet.exe</span></span> | <span data-ttu-id="269b0-282">Mac nuget.exe (w mono)</span><span class="sxs-lookup"><span data-stu-id="269b0-282">Mac nuget.exe (in Mono)</span></span> | <span data-ttu-id="269b0-283">dotnet.exe Mac</span><span class="sxs-lookup"><span data-stu-id="269b0-283">Mac dotnet.exe</span></span> |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | <span data-ttu-id="269b0-284">Tak</span><span class="sxs-lookup"><span data-stu-id="269b0-284">Yes</span></span> | <span data-ttu-id="269b0-285">Tak</span><span class="sxs-lookup"><span data-stu-id="269b0-285">Yes</span></span> | <span data-ttu-id="269b0-286">Tak</span><span class="sxs-lookup"><span data-stu-id="269b0-286">Yes</span></span> | <span data-ttu-id="269b0-287">Tak</span><span class="sxs-lookup"><span data-stu-id="269b0-287">Yes</span></span> |
| `%MY_VAR%` | `\`  | <span data-ttu-id="269b0-288">Tak</span><span class="sxs-lookup"><span data-stu-id="269b0-288">Yes</span></span> | <span data-ttu-id="269b0-289">Tak</span><span class="sxs-lookup"><span data-stu-id="269b0-289">Yes</span></span> | <span data-ttu-id="269b0-290">Nie</span><span class="sxs-lookup"><span data-stu-id="269b0-290">No</span></span> | <span data-ttu-id="269b0-291">Nie</span><span class="sxs-lookup"><span data-stu-id="269b0-291">No</span></span> |
| `$MY_VAR` | `/`  | <span data-ttu-id="269b0-292">Nie</span><span class="sxs-lookup"><span data-stu-id="269b0-292">No</span></span> | <span data-ttu-id="269b0-293">Nie</span><span class="sxs-lookup"><span data-stu-id="269b0-293">No</span></span> | <span data-ttu-id="269b0-294">Nie</span><span class="sxs-lookup"><span data-stu-id="269b0-294">No</span></span> | <span data-ttu-id="269b0-295">Nie</span><span class="sxs-lookup"><span data-stu-id="269b0-295">No</span></span> |
| `$MY_VAR` | `\`  | <span data-ttu-id="269b0-296">Nie</span><span class="sxs-lookup"><span data-stu-id="269b0-296">No</span></span> | <span data-ttu-id="269b0-297">Nie</span><span class="sxs-lookup"><span data-stu-id="269b0-297">No</span></span> | <span data-ttu-id="269b0-298">Nie</span><span class="sxs-lookup"><span data-stu-id="269b0-298">No</span></span> | <span data-ttu-id="269b0-299">Nie</span><span class="sxs-lookup"><span data-stu-id="269b0-299">No</span></span> |


## <a name="example-config-file"></a><span data-ttu-id="269b0-300">Przykładowy plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="269b0-300">Example config file</span></span>

<span data-ttu-id="269b0-301">Poniżej znajduje się przykładowy `nuget.config` plik, który ilustruje wiele ustawień, w tym opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="269b0-301">Below is an example `nuget.config` file that illustrates a number of settings including optional ones:</span></span>

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
