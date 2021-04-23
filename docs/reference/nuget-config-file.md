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
# <a name="nugetconfig-reference"></a>`nuget.config` Odwołanie

Zachowanie programu NuGet jest kontrolowane przez ustawienia w różnych `NuGet.Config` plikach lub `nuget.config` zgodnie z opisem w tece Common [NuGet configurations (Typowe konfiguracje nuGet).](../consume-packages/configuring-nuget-behavior.md)

`nuget.config` to plik XML zawierający węzeł najwyższego `<configuration>` poziomu, który następnie zawiera elementy sekcji opisane w tym temacie. Każda sekcja zawiera zero lub więcej elementów. Zobacz [przykładowy plik konfiguracji](#example-config-file). W nazwach ustawień nie jest uwzględniania litera, a wartości mogą używać [zmiennych środowiskowych](#using-environment-variables).

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>sekcja konfiguracji

Zawiera różne ustawienia konfiguracji, które można ustawić za pomocą [ `nuget config` polecenia](../reference/cli-reference/cli-ref-config.md).

`dependencyVersion` i `repositoryPath` dotyczą tylko projektów korzystających z programu `packages.config` . `globalPackagesFolder` Dotyczy tylko projektów korzystających z formatu PackageReference.

| Klucz | Wartość |
| --- | --- |
| dependencyVersion `packages.config` (tylko) | Wartość `DependencyVersion` domyślna dla instalowania, przywracania i aktualizowania pakietu, gdy `-DependencyVersion` przełącznik nie jest określony bezpośrednio. Ta wartość jest również używana przez interfejs użytkownika Menedżer pakietów NuGet. Wartości to `Lowest` , `HighestPatch` , , `HighestMinor` `Highest` . |
| globalPackagesFolder (projekty korzystające tylko z packageReference) | Lokalizacja domyślnego folderu pakietów globalnych. Wartość domyślna to `%userprofile%\.nuget\packages` (Windows) lub `~/.nuget/packages` (Mac/Linux). Ścieżka względna może być używana w plikach specyficznych dla `nuget.config` projektu. To ustawienie jest zastępowany przez `NUGET_PACKAGES` zmienną środowiskową, która ma pierwszeństwo. |
| repositoryPath `packages.config` (tylko) | Lokalizacja, w której mają być zainstalowane pakiety NuGet zamiast folderu `$(Solutiondir)/packages` domyślnego. Ścieżka względna może być używana w plikach specyficznych dla `nuget.config` projektu. To ustawienie jest zastępowany przez `NUGET_PACKAGES` zmienną środowiskową, która ma pierwszeństwo. |
| defaultPushSource | Identyfikuje adres URL lub ścieżkę źródła pakietu, która powinna być używana jako domyślna, jeśli dla operacji nie zostaną znalezione żadne inne źródła pakietów. |
| http_proxy http_proxy.user http_proxy.password no_proxy | Ustawienia serwera proxy do użycia podczas nawiązywania połączenia ze źródłami pakietów; `http_proxy` powinna mieć format `http://<username>:<password>@<domain>` . Hasła są szyfrowane i nie można ich dodawać ręcznie. W przypadku wartości wartość jest rozdzielaną przecinkami `no_proxy` listą domen, która pomija serwer proxy. Alternatywnie można użyć http_proxy i no_proxy zmiennych środowiskowych dla tych wartości. Aby uzyskać więcej informacji, zobacz [Ustawienia serwera proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Określa tryb weryfikacji używany do weryfikowania podpisów pakietów dla instalowania i przywracania pakietu. Wartości to `accept` , `require` . Wartość domyślna to `accept` .

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

## <a name="bindingredirects-section"></a>sekcja bindingRedirects

Określa, czy pakiet NuGet automatycznie przekierowuje powiązania po zainstalowaniu pakietu.

| Klucz | Wartość |
| --- | --- |
| Pomiń | Wartość logiczna wskazująca, czy pominąć automatyczne przekierowania powiązań. Wartością domyślną jest false. |

**Przykład:**

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>sekcja packageRestore

Steruje przywracaniem pakietów podczas kompilacji.

| Klucz | Wartość |
| --- | --- |
| enabled | Wartość logiczna wskazująca, czy nuGet może wykonać automatyczne przywracanie. Możesz również ustawić `EnableNuGetPackageRestore` zmienną środowiskową z wartością zamiast ustawiać ten `True` klucz w pliku konfiguracji. |
| automatyczne | Wartość logiczna wskazująca, czy pakiet NuGet powinien sprawdzać brakujące pakiety podczas kompilacji. |

**Przykład:**

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>sekcja rozwiązania

Określa, `packages` czy folder rozwiązania jest uwzględniony w kontroli źródła. Ta sekcja działa tylko `nuget.config` w plikach w folderze rozwiązania.

| Klucz | Wartość |
| --- | --- |
| disableSourceControlIntegration | Wartość logiczna wskazująca, czy zignorować folder packages podczas pracy z kontrolą źródła. Wartość domyślna to false. |

**Przykład:**

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Sekcje źródłowe pakietu

Wszystkie , , , i współpracują ze sobą, aby skonfigurować sposób działania pakietu NuGet z repozytoriami pakietów podczas operacji `packageSources` `packageSourceCredentials` `apikeys` `activePackageSource` `disabledPackageSources` `trustedSigners` instalowania, przywracania i aktualizowania.

Polecenie [ `nuget sources` jest](../reference/cli-reference/cli-ref-sources.md) zwykle używane do zarządzania tymi ustawieniami, z wyjątkiem tego, który jest zarządzany przy użyciu polecenia , i który jest `apikeys` zarządzany za pomocą [ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md) `trustedSigners` [ `nuget trusted-signers` polecenia](../reference/cli-reference/cli-ref-trusted-signers.md).

Zwróć uwagę, że źródłowy adres URL nuget.org to `https://api.nuget.org/v3/index.json` .

### <a name="packagesources"></a>packageSources

Wyświetla listę wszystkich znanych źródeł pakietów. Kolejność jest ignorowana podczas operacji przywracania i w dowolnym projekcie w formacie PackageReference. Program NuGet respektuje kolejność źródeł dla operacji instalacji i aktualizacji w projektach korzystających z programu `packages.config` .

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
> Gdy `<clear />` jest obecny dla danego węzła, nuGet ignoruje wcześniej zdefiniowane wartości konfiguracji dla tego węzła. [Dowiedz się więcej na temat sposobu stosowania ustawień](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Przechowuje nazwy użytkowników i hasła dla źródeł, zwykle określone za pomocą `-username` przełączników `-password` i . `nuget sources` Hasła są domyślnie szyfrowane, chyba że `-storepasswordincleartext` jest również używana opcja .
Opcjonalnie za pomocą przełącznika można określić prawidłowe typy `-validauthenticationtypes` uwierzytelniania.

| Klucz | Wartość |
| --- | --- |
| nazwa użytkownika | Nazwa użytkownika źródła w postaci zwykłego tekstu. |
| hasło | Zaszyfrowane hasło dla źródła. Zaszyfrowane hasła są obsługiwane tylko w systemie Windows i można je odszyfrować tylko wtedy, gdy są używane na tym samym komputerze i za pośrednictwem tego samego użytkownika co oryginalne szyfrowanie. |
| cleartextpassword | Niezaszyfrowane hasło źródła. Uwaga: zmienne środowiskowe mogą być używane w celu poprawy zabezpieczeń. |
| validauthenticationtypes | Rozdzielana przecinkami lista prawidłowych typów uwierzytelniania dla tego źródła. Ustaw tę wartość na wartość , jeśli serwer anonsuje NTLM lub Negotiate, a poświadczenia muszą zostać wysłane przy użyciu mechanizmu podstawowego, na przykład w przypadku używania pata dostępu do lokalnego `basic` Azure DevOps Server. Inne prawidłowe wartości to `negotiate` , , i , ale te wartości prawdopodobnie nie będą `kerberos` `ntlm` `digest` przydatne. |

**Przykład:**

W pliku konfiguracji element zawiera węzły podrzędne dla każdej nazwy odpowiedniego źródła (spacje w nazwie `<packageSourceCredentials>` są zastępowane przez `_x0020_` ). Oznacza to, że w przypadku źródeł o nazwach "Contoso" i "Test Source" plik konfiguracji zawiera następujące informacje w przypadku korzystania z zaszyfrowanych haseł:

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

W przypadku korzystania z haseł niezaszyfrowanych:

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

Ponadto można dostarczyć prawidłowe metody uwierzytelniania:

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

Przechowuje klucze dla źródeł, które używają uwierzytelniania za pomocą klucza interfejsu API, zgodnie z ustawieniem za pomocą [ `nuget setapikey` polecenia](../reference/cli-reference/cli-ref-setapikey.md).

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

Identyfikowane obecnie wyłączone źródła. Może być pusta.

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

*(tylko 2.x; przestarzałe w wersji 3.x+)*

Identyfikuje aktualnie aktywne źródło lub wskazuje agregację wszystkich źródeł.

| Klucz | Wartość |
| --- | --- |
| (nazwa źródła) lub `All` | Jeśli klucz jest nazwą źródła, wartość jest ścieżką źródłową lub adresem URL. W `All` przypadku wartości wartość powinna być `(Aggregate source)` taka, aby połączyć wszystkie źródła pakietów, które nie są w przeciwnym razie wyłączone. |

**Przykład:**

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a>sekcja trustedSigners

Przechowuje zaufanych podpisujących używanych do zezwalania na pakiet podczas instalowania lub przywracania. Ta lista nie może być pusta, gdy użytkownik ustawia `signatureValidationMode` na `require` . 

Tę sekcję można zaktualizować za pomocą [ `nuget trusted-signers` polecenia](../reference/cli-reference/cli-ref-trusted-signers.md).

**Schemat**:

Zaufany podpisator ma kolekcję elementów, które zarejestrować wszystkie `certificate` certyfikaty, które identyfikują danego podpiszącego. Zaufanym podpisem może być lub `Author` `Repository` .

Zaufane  repozytorium określa również identyfikator dla repozytorium (który musi być prawidłowym identyfikatorem `serviceIndex` URI) i opcjonalnie może określić listę rozdzieloną średnikami , aby jeszcze bardziej ograniczyć zaufanie do tego konkretnego `https` `owners` repozytorium.

Obsługiwane algorytmy wyznaczania wartości skrótu używane dla odcisku palca certyfikatu to `SHA256` , `SHA384` i `SHA512` .

Jeśli element określa, że dany certyfikat może być łańcuchem do niezaufanego katalogu głównego podczas tworzenia łańcucha certyfikatów `certificate` `allowUntrustedRoot` w ramach `true` weryfikacji podpisu.

**Przykład:**

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

## <a name="fallbackpackagefolders-section"></a>fallbackPackageFolders, sekcja

*(3,5+)* Umożliwia preinstalowanie pakietów, dzięki czemu nie trzeba nic robić, jeśli pakiet zostanie znaleziony w folderach rezerwowych. Foldery pakietów rezerwowych mają dokładnie taką samą strukturę folderów i plików jak globalny folder pakietów: jest obecny plik *.nupkg,* a wszystkie pliki są wyodrębnione.

Logika wyszukiwania dla tej konfiguracji jest:

- Poszukaj w globalnym folderze pakietów, aby sprawdzić, czy pakiet/wersja została już pobrana.

- Poszukaj dopasowania pakietu/wersji w folderach rezerwowych.

Jeśli którekolwiek z tych wyszukiwania powiedzie się, pobieranie nie będzie konieczne.

Jeśli dopasowanie nie zostanie znalezione, program NuGet sprawdzi źródła plików, a następnie źródła http, a następnie pobierze pakiety.

| Klucz | Wartość |
| --- | --- |
| (nazwa folderu rezerwowego) | Ścieżka do folderu rezerwowego. |

**Przykład:**

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>sekcja packageManagement

Ustawia domyślny format zarządzania pakietami, *packages.config* PackageReference. Projekty w stylu zestawu SDK zawsze używają funkcji PackageReference.

| Klucz | Wartość |
| --- | --- |
| format | Wartość logiczna wskazująca domyślny format zarządzania pakietami. Jeśli `1` , format to PackageReference. Jeśli `0` , format jest *packages.config*. |
| wyłączone | Wartość logiczna wskazująca, czy podczas pierwszej instalacji pakietu ma być wyświetlany monit o wybranie domyślnego formatu pakietu. `False` Ukrywa monit. |

**Przykład:**

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a>Korzystanie ze zmiennych środowiskowych

Możesz użyć zmiennych środowiskowych w `nuget.config` wartościach (NuGet 3.4+), aby zastosować ustawienia w czasie uruchamiania.

Jeśli na przykład zmienna środowiskowa w systemie Windows jest ustawiona na wartość , wartość w pliku konfiguracji jest `HOME` `c:\users\username` `%HOME%\NuGetRepository` rozpoznana jako `c:\users\username\NuGetRepository` .

Należy pamiętać, że należy używać zmiennych środowiskowych w stylu systemu Windows (rozpoczyna się i kończy na %) nawet w systemie Mac/Linux. Nie `$HOME/NuGetRepository` można rozwiązać problemu z plikiem konfiguracji. W systemie Mac/Linux wartość będzie `%HOME%/NuGetRepository` rozpoznawiona jako `/home/myStuff/NuGetRepository` .

Jeśli zmienna środowiskowa nie zostanie znaleziona, program NuGet użyje wartości literału z pliku konfiguracji. Na przykład `%MY_UNDEFINED_VAR%/NuGetRepository` zostanie rozpoznany jako `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`

W poniższej tabeli przedstawiono składnię zmiennych środowiska i obsługę separatora ścieżek NuGet.Config plików.

### <a name="nugetconfig-environment-variable-support"></a>`NuGet.Config` obsługa zmiennych środowiskowych

| Składnia | Separator Dir | Windows nuget.exe | Windows dotnet.exe | Mac nuget.exe (w mono) | Mac dotnet.exe |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | Tak | Tak | Tak | Tak |
| `%MY_VAR%` | `\`  | Tak | Tak | Nie | Nie |
| `$MY_VAR` | `/`  | Nie | Nie | Nie | Nie |
| `$MY_VAR` | `\`  | Nie | Nie | Nie | Nie |


## <a name="example-config-file"></a>Przykładowy plik konfiguracji

Poniżej znajduje się `nuget.config` przykładowy plik, który ilustruje wiele ustawień, w tym opcjonalne:

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
