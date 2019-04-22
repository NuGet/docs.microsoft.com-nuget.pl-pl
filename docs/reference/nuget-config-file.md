---
title: Odwołanie do pliku nuget.config
description: Łącznie z sekcji konfiguracji, bindingRedirects, packageRestore, rozwiązania i packageSource odwołanie pliku NuGet.Config.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: d7c943c1f13edf782dabe4afee9d19a1a42bd42a
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911091"
---
# <a name="nugetconfig-reference"></a>Odwołanie do pliku nuget.config

Zachowania programu NuGet jest kontrolowany przez ustawienia w różnych `NuGet.Config` plików zgodnie z opisem w [Konfigurowanie zachowania pakietu NuGet](../consume-packages/configuring-nuget-behavior.md).

`nuget.config` jest to plik XML zawierający najwyższego poziomu `<configuration>` węzła, który następnie zawiera elementy sekcji opisane w tym temacie. Każda sekcja zawiera zero lub więcej elementów. Zobacz [pliku konfiguracyjnego przykłady](#example-config-file). Nazwy ustawień jest rozróżniana wielkość liter, a wartości można użyć [zmienne środowiskowe](#using-environment-variables).

W tym temacie:

- [Sekcja konfiguracyjna](#config-section)
- [sekcja bindingRedirects](#bindingredirects-section)
- [sekcja packageRestore](#packagerestore-section)
- [sekcja rozwiązania](#solution-section)
- [Pakiet sekcje źródła](#package-source-sections):
  - [packageSources](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledPackageSources](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [sekcja trustedSigners](#trustedsigners-section)
- [Korzystanie ze zmiennych środowiskowych](#using-environment-variables)
- [Przykładowy plik konfiguracji](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>Sekcja konfiguracyjna

Zawiera ustawienia konfiguracji dodatkowych, które można ustawić za pomocą [ `nuget config` polecenia](../tools/cli-ref-config.md).

`dependencyVersion` i `repositoryPath` mają zastosowanie tylko do projektów przy użyciu `packages.config`. `globalPackagesFolder` dotyczy tylko projektów przy użyciu formatu PackageReference.

| Key | Wartość |
| --- | --- |
| dependencyVersion (`packages.config` tylko) | Wartość domyślna `DependencyVersion` wartość instalacja pakietu, przywracania i aktualizacji, gdy `-DependencyVersion` nie określono przełącznika bezpośrednio. Ta wartość jest również używana przez interfejs użytkownika Menedżera pakietów NuGet. Wartości są `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| globalPackagesFolder (projekty tylko przy użyciu funkcji PackageReference) | Lokalizacja folderu globalnymi pakietami domyślnego. Wartość domyślna to `%userprofile%\.nuget\packages` (Windows) lub `~/.nuget/packages` (Mac/Linux). Ścieżka względna mogą być używane w specyficznych dla projektu `nuget.config` plików. To ustawienie zostanie zastąpione przez zmienną środowiskową NUGET_PACKAGES ma pierwszeństwo. |
| repositoryPath (`packages.config` tylko) | Lokalizacja, w którym chcesz zainstalować pakiety NuGet, zamiast domyślnego `$(Solutiondir)/packages` folderu. Ścieżka względna mogą być używane w specyficznych dla projektu `nuget.config` plików. To ustawienie zostanie zastąpione przez zmienną środowiskową NUGET_PACKAGES ma pierwszeństwo. |
| defaultPushSource | Określa adres URL lub ścieżki źródłowej pakietu, który powinien być używany jako domyślny, jeśli nie zostaną znalezione żadne inne źródła pakietu dla operacji. |
| no_proxy http_proxy.password http_proxy.user że | Ustawienia serwera proxy do użycia podczas łączenia ze źródłami pakietów; `http_proxy` powinien być w formacie `http://<username>:<password>@<domain>`. Hasła są szyfrowane i nie można dodać ręcznie. Aby uzyskać `no_proxy`, wartość jest rozdzielana przecinkami lista domen obejścia serwera proxy. Można też używać zmiennych środowiskowych że i no_proxy, w przypadku tych wartości. Aby uzyskać więcej informacji, zobacz [ustawienia serwera proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |
| signatureValidationMode | Określa tryb weryfikacji używanej do weryfikowania podpisów pakietów do zainstalowania pakietu i przywracania. Wartości są `accept`, `require`. Wartość domyślna to `accept`.

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

## <a name="bindingredirects-section"></a>sekcja bindingRedirects

Określa, czy NuGet nie automatyczne przekierowania powiązań, gdy pakiet jest zainstalowany.

| Key | Wartość |
| --- | --- |
| Pomiń | Wartość logiczna wskazująca, czy pominąć automatyczne przekierowania powiązań. Wartością domyślną jest false. |

**Przykład**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>sekcja packageRestore

Formanty przywracania pakietów podczas kompilacji.

| Key | Wartość |
| --- | --- |
| Włączone | Wartość logiczna wskazująca, czy NuGet przeprowadzić automatycznego przywracania. Można również ustawić `EnableNuGetPackageRestore` zmienną środowiskową o wartości `True` zamiast ustawiać ten klucz w pliku konfiguracji. |
| automatyczne | Wartość logiczna wskazująca, czy NuGet powinna sprawdzać, czy brakujących pakietów podczas kompilacji. |

**Przykład**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>sekcja rozwiązania

Formanty czy `packages` folder rozwiązania znajduje się w kontroli źródła. W tej sekcji działa tylko w `nuget.config` pliki w folderze rozwiązania.

| Key | Wartość |
| --- | --- |
| disableSourceControlIntegration | Wartość logiczna wskazująca, czy ignorować packages folder podczas pracy z kontrolą źródła. Wartość domyślna to false. |

**Przykład**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>Sekcje źródła pakietu

`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` i `trustedSigners` współdziałają ze sobą, aby skonfigurować, jak NuGet współpracuje z repozytoriów pakietów podczas instalacji, przywracania i operacje aktualizacji.

[ `nuget sources` Polecenia](../tools/cli-ref-sources.md) zwykle jest używana do zarządzania tych ustawień, z wyjątkiem `apikeys` która jest zarządzana przy użyciu [ `nuget setapikey` polecenia](../tools/cli-ref-setapikey.md), i `trustedSigners` która będzie zarządzana za pomocą [ `nuget trusted-signers` polecenia](../tools/cli-ref-trusted-signers.md).

Należy zauważyć, że adres URL źródła nuget.org `https://api.nuget.org/v3/index.json`.

### <a name="packagesources"></a>packageSources

Wyświetla listę wszystkich źródeł pakietów znane. Kolejność jest ignorowany podczas operacji przywracania i z jakimkolwiek projektem, przy użyciu formatu PackageReference. NuGet szanuje kolejność źródeł do instalacji i operacje aktualizacji z projektami za pomocą `packages.config`.

| Key | Wartość |
| --- | --- |
| (Nazwa do przypisania do źródła pakietu) | Ścieżka lub adres URL źródła pakietu. |

**Przykład**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a>packageSourceCredentials

Przechowywane nazwy użytkowników i hasła dla źródeł, zazwyczaj są określane za pomocą `-username` i `-password` zmienia się przy użyciu `nuget sources`. Hasła są szyfrowane domyślnie, chyba że `-storepasswordincleartext` jest również używana opcja.

| Key | Wartość |
| --- | --- |
| nazwa użytkownika | Nazwa użytkownika źródła w postaci zwykłego tekstu. |
| hasło | Zaszyfrowane hasło dla źródła. |
| cleartextpassword | Hasło nieszyfrowane źródła. |

**Przykład:**

W pliku konfiguracyjnym `<packageSourceCredentials>` element zawiera węzły podrzędne dla każdej nazwy źródła dotyczy (spacje w nazwie są zamieniane `_x0020_`). Oznacza to w przypadku źródeł o nazwie "Contoso" i "Źródła testów" plik konfiguracji, który zawiera następujące korzystając z hasła szyfrowane:

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

W przypadku używania niezaszyfrowane hasła:

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

Przechowuje klucze dla źródeł, które używają uwierzytelniania kluczem interfejsu API, według stawki ustalonej z [ `nuget setapikey` polecenia](../tools/cli-ref-setapikey.md).

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

Zidentyfikować obecnie wyłączone źródła. Może być pusta.

| Key | Wartość |
| --- | --- |
| (nazwa źródła) | Wartość logiczna wskazująca, czy źródło jest wyłączona. |

**Przykład:**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(tylko 2.x; 3.x+ przestarzałe w)*

Identyfikuje do aktualnie aktywnego źródła lub wskazuje agregacji wszystkich źródeł.

| Key | Wartość |
| --- | --- |
| (nazwa źródła) lub `All` | Jeśli nazwa źródła jest klucz, wartość jest ścieżka źródłowa lub adres URL. Jeśli `All`, ta wartość powinna być `(Aggregate source)` łączenie wszystkich źródeł pakietów, które w przeciwnym razie nie zostały wyłączone. |

**Przykład**:

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a>sekcja trustedSigners

Magazyny zaufane osoby podpisujące używany w celu umożliwienia pakietu podczas instalowania lub przywracania. Ta lista nie może być pusta, gdy użytkownik ustawi `signatureValidationMode` do `require`. 

W tej sekcji mogą być aktualizowane przy użyciu [ `nuget trusted-signers` polecenia](../tools/cli-ref-trusted-signers.md).

**Schemat**:

Zaufane osoby podpisującej zawiera zbiór `certificate` elementy, które zarejestrować wszystkie certyfikaty, które identyfikują danego osoby podpisującej. Może być zaufane osoby podpisującej `Author` lub `Repository`.

Zaufanego *repozytorium* określa również `serviceIndex` repozytorium (która musi być prawidłowym `https` identyfikatora uri) i opcjonalnie można określić Rozdzielana średnikami lista `owners` można ograniczyć jeszcze bardziej który jest zaufany z tego określonego repozytorium.

To algorytmów wyznaczania wartości skrótu obsługiwanych odcisk palca certyfikatu `SHA256`, `SHA384` i `SHA512`.

Jeśli `certificate` Określa `allowUntrustedRoot` jako `true` podany certyfikat jest dozwolone do tworzenia łańcucha niezaufany certyfikat główny podczas tworzenia łańcucha certyfikatów, jako część weryfikacji podpisu.

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

Można użyć zmiennych środowiskowych w `nuget.config` wartości (NuGet 3.4 +) do zastosowania ustawień w czasie wykonywania.

Na przykład jeśli `HOME` ustawiono zmiennej środowiskowej na Windows `c:\users\username`, następnie wartość `%HOME%\NuGetRepository` w konfiguracji pliku jest rozpoznawana jako `c:\users\username\NuGetRepository`.

Podobnie jeśli `HOME` w systemie Mac/Linux jest równa `/home/myStuff`, następnie `%HOME%/NuGetRepository` w konfiguracji pliku jest rozpoznawana jako `/home/myStuff/NuGetRepository`.

Jeśli zmienna środowiskowa nie zostanie znaleziony, NuGet używa wartości literału w pliku konfiguracji.

## <a name="example-config-file"></a>Przykładowy plik konfiguracji

Poniżej znajduje się przykład `nuget.config` pliku, który przedstawia liczbę ustawień:

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
