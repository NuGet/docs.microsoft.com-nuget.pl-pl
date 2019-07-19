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
# <a name="nugetconfig-reference"></a>Dokumentacja NuGet. config

Zachowanie NuGet jest kontrolowane przez ustawienia w różnych `NuGet.Config` plikach, zgodnie z opisem w temacie [typowe konfiguracje programu NuGet](../consume-packages/configuring-nuget-behavior.md).

`nuget.config`jest plikiem XML zawierającym węzeł najwyższego `<configuration>` poziomu, który zawiera elementy sekcji opisane w tym temacie. Każda sekcja zawiera zero lub więcej elementów. Zobacz [przykład pliku konfiguracji](#example-config-file). W nazwach ustawień jest rozróżniana wielkość liter, a wartości mogą używać [zmiennych środowiskowych](#using-environment-variables).

W tym temacie:

- [sekcja konfiguracji](#config-section)
- [Sekcja bindingRedirects](#bindingredirects-section)
- [Sekcja packageRestore](#packagerestore-section)
- [Sekcja rozwiązania](#solution-section)
- [Sekcje źródłowe pakietu](#package-source-sections):
  - [packageSources](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledPackageSources](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [Sekcja trustedSigners](#trustedsigners-section)
- [Korzystanie ze zmiennych środowiskowych](#using-environment-variables)
- [Przykładowy plik konfiguracji](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>sekcja konfiguracji

Zawiera różne ustawienia konfiguracji, które można ustawić za pomocą [ `nuget config` polecenia](../reference/cli-reference/cli-ref-config.md).

`dependencyVersion`i `repositoryPath` mają zastosowanie tylko do projektów `packages.config`korzystających z programu. `globalPackagesFolder`dotyczy tylko projektów przy użyciu formatu PackageReference.

| Key | Wartość |
| --- | --- |
| dependencyVersion (`packages.config` tylko) | Wartość domyślna `DependencyVersion` instalacji, przywracania i aktualizacji pakietu, `-DependencyVersion` gdy przełącznik nie jest określony bezpośrednio. Ta wartość jest również używana przez interfejs użytkownika Menedżera pakietów NuGet. Wartości to `Lowest` `HighestPatch` ,,`Highest`, `HighestMinor`. |
| globalPackagesFolder (projekty korzystające tylko z PackageReference) | Lokalizacja domyślnego folderu pakiety globalne. Wartość domyślna to `%userprofile%\.nuget\packages` (Windows) lub `~/.nuget/packages` (Mac/Linux). Ścieżka względna może być używana w plikach specyficznych `nuget.config` dla projektu. To ustawienie jest zastępowane przez zmienną środowiskową NUGET_PACKAGES, która ma pierwszeństwo. |
| repositoryPath (`packages.config` tylko) | Lokalizacja, w której mają zostać zainstalowane pakiety NuGet zamiast folderu domyślnego `$(Solutiondir)/packages` . Ścieżka względna może być używana w plikach specyficznych `nuget.config` dla projektu. To ustawienie jest zastępowane przez zmienną środowiskową NUGET_PACKAGES, która ma pierwszeństwo. |
| defaultPushSource | Określa adres URL lub ścieżkę źródła pakietu, które ma być używane jako wartość domyślna, jeśli nie znaleziono żadnych innych źródeł pakietów dla operacji. |
| http_proxy http_proxy. User http_proxy. Password no_proxy | Ustawienia serwera proxy do użycia podczas nawiązywania połączenia ze źródłami pakietów; powinien mieć format `http://<username>:<password>@<domain>`. `http_proxy` Hasła są szyfrowane i nie można ich dodać ręcznie. W `no_proxy`przypadku, wartość jest rozdzielaną przecinkami listą domen, które pomijają serwer proxy. Dla tych wartości można użyć zmiennych środowiskowych http_proxy i no_proxy. Aby uzyskać więcej informacji, zobacz [Ustawienia serwera proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Określa tryb weryfikacji używany do weryfikowania podpisów pakietów na potrzeby instalacji pakietu i przywracania. Wartości to `accept`, `require`. Wartość domyślna to `accept`.

**Przykład**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a>Sekcja bindingRedirects

Określa, czy program NuGet ma przekierować automatyczne powiązania po zainstalowaniu pakietu.

| Key | Wartość |
| --- | --- |
| Pomiń | Wartość logiczna wskazująca, czy pomijać Automatyczne przekierowania powiązań. Wartością domyślną jest false. |

**Przykład**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>Sekcja packageRestore

Kontroluje przywracanie pakietu podczas kompilacji.

| Key | Wartość |
| --- | --- |
| Dostępny | Wartość logiczna wskazująca, czy pakiet NuGet może wykonywać automatyczne przywracanie. Można również ustawić `EnableNuGetPackageRestore` dla zmiennej środowiskowej `True` wartość zamiast ustawienia tego klucza w pliku konfiguracji. |
| automatyczne | Wartość logiczna wskazująca, czy NuGet ma sprawdzać brakujące pakiety podczas kompilacji. |

**Przykład**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>Sekcja rozwiązania

Określa, `packages` czy folder rozwiązania ma być uwzględniony w kontroli źródła. Ta sekcja działa tylko w `nuget.config` plikach w folderze rozwiązania.

| Key | Wartość |
| --- | --- |
| disableSourceControlIntegration | Wartość logiczna wskazująca, czy ignorować folder Packages podczas pracy z kontrolą źródła. Wartość domyślna to false. |

**Przykład**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Sekcje źródłowe pakietu

`packageSourceCredentials` ,,`activePackageSource`, I`disabledPackageSources` wszystkie współpracują ze sobą, aby skonfigurować sposób działania programu NuGet z repozytoriami pakietów podczas operacji instalowania, przywracania i aktualizowania. `trustedSigners` `packageSources` `apikeys`

[ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md) `apikeys` `trustedSigners` [ `nuget trusted-signers` ](../reference/cli-reference/cli-ref-trusted-signers.md) [ Polecenie`nuget sources` ](../reference/cli-reference/cli-ref-sources.md) jest zwykle używane do zarządzania tymi ustawieniami, z wyjątkiem tego, które jest zarządzane za pomocą polecenia, i które jest zarządzane za pomocą polecenia.

Należy pamiętać, że źródłowy adres URL dla `https://api.nuget.org/v3/index.json`NuGet.org to.

### <a name="packagesources"></a>packageSources

Wyświetla wszystkie znane źródła pakietów. Kolejność jest ignorowana podczas operacji przywracania i dowolnego projektu przy użyciu formatu PackageReference. Pakiet NuGet szanuje kolejność źródeł dla operacji instalacji i aktualizacji z projektami przy użyciu `packages.config`programu.

| Key | Wartość |
| --- | --- |
| (nazwa do przypisania do źródła pakietu) | Ścieżka lub adres URL źródła pakietu. |

**Przykład**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Przechowuje nazwy użytkowników i hasła dla źródeł, zwykle określone przy użyciu `-username` przełączników `nuget sources`i `-password` . Hasła są szyfrowane domyślnie, chyba że `-storepasswordincleartext` jest również używana opcja.

| Key | Wartość |
| --- | --- |
| username | Nazwa użytkownika dla źródła w postaci zwykłego tekstu. |
| password | Hasło zaszyfrowane dla źródła. |
| cleartextpassword | Niezaszyfrowane hasło dla źródła. |

**Przykład:**

W pliku `<packageSourceCredentials>` konfiguracji element zawiera węzły podrzędne dla każdej stosownej nazwy źródłowej (spacje w nazwie są `_x0020_`zastępowane). Oznacza to, że w przypadku źródeł o nazwach "contoso" i "Źródło testowe" plik konfiguracyjny zawiera następujące dane w przypadku korzystania z szyfrowanych haseł:

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

W przypadku korzystania z nieszyfrowanych haseł:

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

### <a name="apikeys"></a>apikeys

Przechowuje klucze dla źródeł korzystających z uwierzytelniania za pomocą klucza interfejsu API, jak określono za pomocą [ `nuget setapikey` polecenia](../reference/cli-reference/cli-ref-setapikey.md).

| Key | Wartość |
| --- | --- |
| (źródłowy adres URL) | Zaszyfrowany klucz interfejsu API. |

**Przykład**:

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

Zidentyfikowano aktualnie wyłączone źródła. Może być pusty.

| Key | Wartość |
| --- | --- |
| (nazwa źródła) | Wartość logiczna wskazująca, czy źródło jest wyłączone. |

**Przykład:**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(tylko 2. x; przestarzałe w 3. x +)*

Identyfikuje aktualnie aktywne źródło lub wskazuje zagregowane wszystkie źródła.

| Key | Wartość |
| --- | --- |
| (nazwa źródła) lub`All` | Jeśli klucz jest nazwą źródła, wartość jest ścieżką źródłową lub adresem URL. Jeśli `All`wartość powinna być `(Aggregate source)` połączona ze wszystkimi źródłami pakietów, które nie są wyłączone. |

**Przykład**:

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a>Sekcja trustedSigners

Przechowuje zaufane osoby podpisujące używane do zezwalania na pakiet podczas instalowania lub przywracania. Ta lista nie może być pusta, jeśli użytkownik `signatureValidationMode` ustawi `require`. 

Tę sekcję można zaktualizować za pomocą [ `nuget trusted-signers` polecenia](../reference/cli-reference/cli-ref-trusted-signers.md).

**Schemat**:

Zaufany podpiser zawiera kolekcję `certificate` elementów, które identyfikują wszystkie certyfikaty identyfikujące daną rejestrację. Zaufaną rejestracją może być `Author` albo `Repository`lub.

Zaufane *repozytorium* `serviceIndex` określa również dla repozytorium (które musi być prawidłowym `https` identyfikatorem URI) i opcjonalnie określać listę rozdzielaną średnikami, aby ograniczyć liczbę elementów `owners` , które są zaufane z tego konkretnego kopie.

Obsługiwane algorytmy wyznaczania wartości skrótu używane dla `SHA256`odcisku `SHA512`palca certyfikatu to, `SHA384` i.

`certificate` Jeśli określono `allowUntrustedRoot` , żedanycertyfikatjestdozwolonydołączeniasięzniezaufanymkatalogiemgłównym,podczasbudowaniałańcuchacertyfikatówwramachweryfikacjipodpisu.`true`

**Przykład**:

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

## <a name="using-environment-variables"></a>Korzystanie ze zmiennych środowiskowych

Możesz użyć zmiennych środowiskowych w `nuget.config` wartościach (NuGet 3.4 +), aby zastosować ustawienia w czasie wykonywania.

Na przykład jeśli `HOME` zmienna środowiskowa w systemie Windows jest ustawiona na `c:\users\username` `%HOME%\NuGetRepository` , wartość w pliku konfiguracji jest rozpoznawana `c:\users\username\NuGetRepository`jako.

Analogicznie, `HOME` Jeśli w systemie Mac/Linux jest `/home/myStuff`ustawiona na `%HOME%/NuGetRepository` , w pliku konfiguracji jest rozpoznawana `/home/myStuff/NuGetRepository`wartość.

Jeśli zmienna środowiskowa nie zostanie znaleziona, NuGet używa wartości literału z pliku konfiguracyjnego.

## <a name="example-config-file"></a>Przykładowy plik konfiguracji

Poniżej znajduje się przykładowy `nuget.config` plik, który ilustruje wiele ustawień:

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
