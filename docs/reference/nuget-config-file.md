---
title: Odwołanie do pliku nuget.config
description: NuGet.Config odwołanie do pliku, w tym sekcje config, bindingRedirects, packageRestore, Solution i packageSource.
author: JonDouglas
ms.author: jodou
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 9b15550d0e6e8aec4d526391d77c654a756f343e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777661"
---
# <a name="nugetconfig-reference"></a>Informacje nuget.config

Zachowanie NuGet jest kontrolowane przez ustawienia w różnych `NuGet.Config` lub `nuget.config` plikach, zgodnie z opisem w temacie [typowe konfiguracje programu NuGet](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` jest plikiem XML zawierającym węzeł najwyższego poziomu `<configuration>` , który zawiera elementy sekcji opisane w tym temacie. Każda sekcja zawiera zero lub więcej elementów. Zobacz [przykład pliku konfiguracji](#example-config-file). W nazwach ustawień jest rozróżniana wielkość liter, a wartości mogą używać [zmiennych środowiskowych](#using-environment-variables).

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>sekcja konfiguracji

Zawiera różne ustawienia konfiguracji, które można ustawić za pomocą [ `nuget config` polecenia](../reference/cli-reference/cli-ref-config.md).

`dependencyVersion` i `repositoryPath` mają zastosowanie tylko do projektów korzystających z programu `packages.config` . `globalPackagesFolder` dotyczy tylko projektów przy użyciu formatu PackageReference.

| Klucz | Wartość |
| --- | --- |
| dependencyVersion ( `packages.config` tylko) | Wartość domyślna `DependencyVersion` instalacji, przywracania i aktualizacji pakietu, gdy `-DependencyVersion` przełącznik nie jest określony bezpośrednio. Ta wartość jest również używana przez interfejs użytkownika Menedżera pakietów NuGet. Wartości to `Lowest` , `HighestPatch` , `HighestMinor` , `Highest` . |
| globalPackagesFolder (projekty korzystające tylko z PackageReference) | Lokalizacja domyślnego folderu pakiety globalne. Wartość domyślna to `%userprofile%\.nuget\packages` (Windows) lub `~/.nuget/packages` (Mac/Linux). Ścieżka względna może być używana w plikach specyficznych dla projektu `nuget.config` . To ustawienie jest zastępowane przez zmienną środowiskową NUGET_PACKAGES, która ma pierwszeństwo. |
| repositoryPath ( `packages.config` tylko) | Lokalizacja, w której mają zostać zainstalowane pakiety NuGet zamiast folderu domyślnego `$(Solutiondir)/packages` . Ścieżka względna może być używana w plikach specyficznych dla projektu `nuget.config` . To ustawienie jest zastępowane przez zmienną środowiskową NUGET_PACKAGES, która ma pierwszeństwo. |
| defaultPushSource | Określa adres URL lub ścieżkę źródła pakietu, które ma być używane jako wartość domyślna, jeśli nie znaleziono żadnych innych źródeł pakietów dla operacji. |
| http_proxy http_proxy. User http_proxy. Password no_proxy | Ustawienia serwera proxy do użycia podczas nawiązywania połączenia ze źródłami pakietów; `http_proxy` powinien mieć format `http://<username>:<password>@<domain>` . Hasła są szyfrowane i nie można ich dodać ręcznie. W przypadku `no_proxy` , wartość jest rozdzielaną przecinkami listą domen, które pomijają serwer proxy. Dla tych wartości można użyć zmiennych środowiskowych http_proxy i no_proxy. Aby uzyskać więcej informacji, zobacz [Ustawienia serwera proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Określa tryb weryfikacji używany do weryfikowania podpisów pakietów na potrzeby instalacji pakietu i przywracania. Wartości to `accept` , `require` . Wartość domyślna to `accept` .

**Przykład:**

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

| Klucz | Wartość |
| --- | --- |
| Pomiń | Wartość logiczna wskazująca, czy pomijać Automatyczne przekierowania powiązań. Wartością domyślną jest false. |

**Przykład:**

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>Sekcja packageRestore

Kontroluje przywracanie pakietu podczas kompilacji.

| Klucz | Wartość |
| --- | --- |
| enabled | Wartość logiczna wskazująca, czy pakiet NuGet może wykonywać automatyczne przywracanie. Można również ustawić dla `EnableNuGetPackageRestore` zmiennej środowiskowej wartość `True` zamiast ustawienia tego klucza w pliku konfiguracji. |
| automatyczne | Wartość logiczna wskazująca, czy NuGet ma sprawdzać brakujące pakiety podczas kompilacji. |

**Przykład:**

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>Sekcja rozwiązania

Określa, czy `packages` folder rozwiązania ma być uwzględniony w kontroli źródła. Ta sekcja działa tylko w `nuget.config` plikach w folderze rozwiązania.

| Klucz | Wartość |
| --- | --- |
| disableSourceControlIntegration | Wartość logiczna wskazująca, czy ignorować folder Packages podczas pracy z kontrolą źródła. Wartość domyślna to false. |

**Przykład:**

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Sekcje źródłowe pakietu

`packageSources`,, `packageSourceCredentials` `apikeys` , `activePackageSource` `disabledPackageSources` I `trustedSigners` wszystkie współpracują ze sobą, aby skonfigurować sposób działania programu NuGet z repozytoriami pakietów podczas operacji instalowania, przywracania i aktualizowania.

[ `nuget sources` Polecenie](../reference/cli-reference/cli-ref-sources.md) jest zwykle używane do zarządzania tymi ustawieniami, z wyjątkiem tego, `apikeys` które jest zarządzane za pomocą [ `nuget setapikey` polecenia](../reference/cli-reference/cli-ref-setapikey.md), i `trustedSigners` które jest zarządzane za pomocą [ `nuget trusted-signers` polecenia](../reference/cli-reference/cli-ref-trusted-signers.md).

Należy pamiętać, że źródłowy adres URL dla nuget.org to `https://api.nuget.org/v3/index.json` .

### <a name="packagesources"></a>packageSources

Wyświetla wszystkie znane źródła pakietów. Kolejność jest ignorowana podczas operacji przywracania i dowolnego projektu przy użyciu formatu PackageReference. Pakiet NuGet szanuje kolejność źródeł dla operacji instalacji i aktualizacji z projektami przy użyciu programu `packages.config` .

| Klucz | Wartość |
| --- | --- |
| (nazwa do przypisania do źródła pakietu) | Ścieżka lub adres URL źródła pakietu. |

**Przykład:**

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

> [!Tip]
> Gdy `<clear />` jest obecny dla danego węzła, pakiet NuGet ignoruje wcześniej zdefiniowane wartości konfiguracji dla tego węzła. [Przeczytaj więcej na temat sposobu stosowania ustawień](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Przechowuje nazwy użytkowników i hasła dla źródeł, zwykle określone przy użyciu `-username` `-password` przełączników i `nuget sources` . Hasła są szyfrowane domyślnie, chyba że `-storepasswordincleartext` jest również używana opcja.
Opcjonalnie można określić prawidłowe typy uwierzytelniania za pomocą `-validauthenticationtypes` przełącznika.

| Klucz | Wartość |
| --- | --- |
| nazwa użytkownika | Nazwa użytkownika dla źródła w postaci zwykłego tekstu. |
| hasło | Hasło zaszyfrowane dla źródła. Hasła szyfrowane są obsługiwane tylko w systemie Windows i mogą być odszyfrowywane tylko wtedy, gdy są używane na tym samym komputerze i za pośrednictwem tego samego użytkownika co oryginalne szyfrowanie. |
| cleartextpassword | Niezaszyfrowane hasło dla źródła. Uwaga: zmienne środowiskowe mogą być używane w celu zwiększenia bezpieczeństwa. |
| validauthenticationtypes | Rozdzielana przecinkami lista prawidłowych typów uwierzytelniania dla tego źródła. Ustaw tę opcję na `basic` , jeśli serwer anonsuje protokół NTLM lub Negocjuj, a Twoje poświadczenia muszą być wysyłane przy użyciu podstawowego mechanizmu, na przykład w przypadku korzystania z elementu "% Azure DevOps Server". Inne prawidłowe wartości to `negotiate` , `kerberos` , `ntlm` , i `digest` , ale te wartości są prawdopodobnie przydatne. |

**Przykład:**

W pliku konfiguracji `<packageSourceCredentials>` element zawiera węzły podrzędne dla każdej stosownej nazwy źródłowej (spacje w nazwie są zastępowane `_x0020_` ). Oznacza to, że w przypadku źródeł o nazwach "contoso" i "Źródło testowe" plik konfiguracyjny zawiera następujące dane w przypadku korzystania z szyfrowanych haseł:

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

W przypadku korzystania z niezaszyfrowanych haseł przechowywanych w zmiennej środowiskowej:

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

Ponadto można podać prawidłowe metody uwierzytelniania:

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

### <a name="apikeys"></a>apikeys

Przechowuje klucze dla źródeł korzystających z uwierzytelniania za pomocą klucza interfejsu API, jak określono za pomocą [ `nuget setapikey` polecenia](../reference/cli-reference/cli-ref-setapikey.md).

| Klucz | Wartość |
| --- | --- |
| (źródłowy adres URL) | Zaszyfrowany klucz interfejsu API. |

**Przykład:**

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

Zidentyfikowano aktualnie wyłączone źródła. Może być pusty.

| Klucz | Wartość |
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

| Klucz | Wartość |
| --- | --- |
| (nazwa źródła) lub `All` | Jeśli klucz jest nazwą źródła, wartość jest ścieżką źródłową lub adresem URL. Jeśli `All` wartość powinna być `(Aggregate source)` połączona ze wszystkimi źródłami pakietów, które nie są wyłączone. |

**Przykład:**

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a>Sekcja trustedSigners

Przechowuje zaufane osoby podpisujące używane do zezwalania na pakiet podczas instalowania lub przywracania. Ta lista nie może być pusta, jeśli użytkownik `signatureValidationMode` ustawi `require` . 

Tę sekcję można zaktualizować za pomocą [ `nuget trusted-signers` polecenia](../reference/cli-reference/cli-ref-trusted-signers.md).

**Schemat**:

Zaufany podpiser zawiera kolekcję `certificate` elementów, które identyfikują wszystkie certyfikaty identyfikujące daną rejestrację. Zaufaną rejestracją może być albo `Author` lub `Repository` .

Zaufane *repozytorium* określa również `serviceIndex` dla repozytorium (które musi być prawidłowym `https` identyfikatorem URI) i opcjonalnie określać listę rozdzielaną średnikami, aby ograniczyć liczbę elementów, które `owners` są zaufane z tego konkretnego repozytorium.

Obsługiwane algorytmy wyznaczania wartości skrótu używane dla odcisku palca certyfikatu to `SHA256` , `SHA384` i `SHA512` .

Jeśli `certificate` określono `allowUntrustedRoot` , że `true` dany certyfikat jest dozwolony do łączenia się z niezaufanym katalogiem głównym, podczas budowania łańcucha certyfikatów w ramach weryfikacji podpisu.

**Przykład:**

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a>Sekcja fallbackPackageFolders

*(3.5 +)* Zapewnia możliwość preinstalacji pakietów, dzięki czemu nie trzeba wykonywać żadnych zadań, jeśli pakiet znajduje się w folderach rezerwowych. Foldery pakietu rezerwowego mają dokładnie ten sam folder i strukturę plików, co folder pakietu globalnego: *. nupkg* jest obecny i wszystkie pliki są wyodrębniane.

Logika wyszukiwania dla tej konfiguracji to:

- Spójrz na folder pakietu globalnego, aby sprawdzić, czy pakiet/wersja została już pobrana.

- Sprawdź, czy w folderach rezerwowych znajduje się zgodność z pakietem/wersją.

Jeśli wyszukiwanie zakończyło się pomyślnie, pobieranie nie jest konieczne.

Jeśli dopasowanie nie zostanie znalezione, pakiet NuGet sprawdza źródła plików, a następnie źródła http, a następnie pobiera pakiety.

| Klucz | Wartość |
| --- | --- |
| (nazwa folderu rezerwowego) | Ścieżka do folderu rezerwowego. |

**Przykład:**

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>Sekcja packageManagement

Ustawia domyślny format zarządzania pakietami, *packages.config* lub PackageReference. Projekty w stylu zestawu SDK zawsze używają PackageReference.

| Klucz | Wartość |
| --- | --- |
| format | Wartość logiczna wskazująca domyślny format zarządzania pakietami. Jeśli `1` , format jest PackageReference. Jeśli `0` Format jest *packages.config*. |
| wyłączone | Wartość logiczna wskazująca, czy wyświetlać monit o wybranie domyślnego formatu pakietu przy pierwszej instalacji pakietu. `False` ukrywa monit. |

**Przykład:**

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a>Korzystanie ze zmiennych środowiskowych

Możesz użyć zmiennych środowiskowych w `nuget.config` wartościach (NuGet 3.4 +), aby zastosować ustawienia w czasie wykonywania.

Na przykład jeśli `HOME` zmienna środowiskowa w systemie Windows jest ustawiona na `c:\users\username` , wartość `%HOME%\NuGetRepository` w pliku konfiguracji jest rozpoznawana jako `c:\users\username\NuGetRepository` .

Należy pamiętać, że należy używać zmiennych środowiskowych w stylu systemu Windows (rozpoczyna się i kończą z%) nawet w systemie Mac/Linux. Posiadanie `$HOME/NuGetRepository` w pliku konfiguracji nie zostanie rozwiązane. W systemie Mac/Linux wartość `%HOME%/NuGetRepository` zostanie rozwiązany `/home/myStuff/NuGetRepository` .

Jeśli zmienna środowiskowa nie zostanie znaleziona, NuGet używa wartości literału z pliku konfiguracyjnego. Na przykład `%MY_UNDEFINED_VAR%/NuGetRepository` zostanie rozpoznany jako `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`

W poniższej tabeli przedstawiono obsługę składni wirtualnym zmiennych i separator ścieżki dla plików NuGet.Config.

### <a name="nugetconfig-environment-variable-support"></a>Obsługa zmiennej środowiskowej NuGet.Config

| Składnia | Separator dir | nuget.exe systemu Windows | dotnet.exe systemu Windows | Mac nuget.exe (w mono) | dotnet.exe Mac |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | Tak | Tak | Tak | Tak |
| `%MY_VAR%` | `\`  | Tak | Tak | Nie | Nie |
| `$MY_VAR` | `/`  | Nie | Nie | Nie | Nie |
| `$MY_VAR` | `\`  | Nie | Nie | Nie | Nie |


## <a name="example-config-file"></a>Przykładowy plik konfiguracji

Poniżej znajduje się przykładowy `nuget.config` plik, który ilustruje wiele ustawień, w tym opcjonalne:

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
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
