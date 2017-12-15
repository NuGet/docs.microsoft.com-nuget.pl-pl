---
title: "Odwołanie do pliku NuGet.Config. | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: fbf31530-3bf4-478c-b26c-c2b24dd3406d
description: "Odwołanie do pliku NuGet.Config łącznie z sekcji konfiguracji, bindingRedirects packageRestore, rozwiązanie i packageSource."
keywords: "Pliku NuGet.Config, NuGet konfiguracji odwołania, opcje konfiguracji NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fa471e1ad419c6a4cab99e271375d9be94c29a50
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nugetconfig-reference"></a>Odwołanie do pliku NuGet.Config.

Zachowanie NuGet jest kontrolowane przez ustawienia w różnych `NuGet.Config` plików zgodnie z opisem w [Konfigurowanie zachowania NuGet](../consume-packages/configuring-nuget-behavior.md).

`NuGet.Config`jest to plik XML zawierający najwyższego poziomu `<configuration>` węzła, który następnie zawiera elementy sekcji opisane w tym temacie. Każda sekcja zawiera zero lub więcej `<add>` elementy o `key` i `value` atrybutów. Zobacz [pliku konfiguracji przykłady](#example-config-file). Ustawienie nazwy jest rozróżniana wielkość liter, a wartości można użyć [zmiennych środowiskowych](#using-environment-variables).

W tym temacie:

- [Sekcja konfiguracyjna](#config-section)
- [sekcja bindingRedirects](#bindingredirects-section)
- [sekcja packageRestore](#packagerestore-section)
- [sekcji rozwiązania](#solution-section)
- [Pakiet sekcje źródła](#package-source-sections):
    - [packageSources](#packagesources)
    - [packageSourceCredentials](#packagesourcecredentials)
    - [apikeys](#apikeys)
    - [disabledPackageSources](#disabledpackagesources)
    - [activePackageSource](#activepackagesource)
- [Korzystanie ze zmiennych środowiskowych](#using-environment-variables)
- [Przykładowy plik konfiguracji](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>Sekcja konfiguracyjna

Zawiera ustawienia dodatkowych konfiguracji, które można ustawić za pomocą [ `nuget config` polecenia](../tools/cli-ref-config.md).

Uwaga: `dependencyVersion` i `repositoryPath` stosowania tylko dla projektów przy użyciu `packages.config`. `globalPackagesFolder`dotyczy tylko projektów przy użyciu `project.json` i PackageReference formatach.

| Key | Wartość |
| --- | --- |
| dependencyVersion (`packages.config` tylko) | Wartość domyślna `DependencyVersion` wartość instalacji pakietu, przywracania i aktualizacji, gdy `-DependencyVersion` przełącznik nie jest określony bezpośrednio. Ta wartość jest także używana przez interfejs użytkownika Menedżera pakietów NuGet. Wartości są `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`. |
| wartość globalPackagesFolder (projektów nie używa `packages.config`) | Lokalizacja domyślny folder globalne pakietów. Wartość domyślna to `%USERPROFILE%\.nuget\packages` (system Windows) lub `~/.nuget/packages` (system Mac/Linux). Ścieżka względna mogą być używane w specyficznego dla projektu `Nuget.Config` plików. |
| repositoryPath (`packages.config` tylko) | Lokalizacja, w którym można zainstalować pakietów NuGet, zamiast domyślnej `$(Solutiondir)/packages` folderu. Ścieżka względna mogą być używane w specyficznego dla projektu `Nuget.Config` plików. |
| defaultPushSource | Określa adres URL lub ścieżkę źródła pakietu, które mają być używane jako domyślne, jeśli inne źródła pakietu nie znaleziono dla operacji. |
| że http_proxy.user http_proxy.password no_proxy | Ustawienia serwera proxy do użycia podczas połączenia ze źródła pakietów; `http_proxy` powinien być w formacie `http://<username>:<password>@<domain>`. Hasła są szyfrowane i nie można dodać ręcznie. Aby uzyskać `no_proxy`, wartość jest rozdzielaną przecinkami listę domen obejścia serwera proxy. Można również używać zmiennych środowiskowych że i no_proxy, dla tych wartości. Aby uzyskać więcej informacji, zobacz [ustawienia serwera proxy NuGet](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com). |


**Przykład**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```


## <a name="bindingredirects-section"></a>sekcja bindingRedirects

Określa, czy NuGet nie przekierowania powiązania automatyczne, gdy jest zainstalowany pakiet.

| Key | Wartość |
| --- | --- |
| Pomiń | Wartość logiczna wskazująca, czy pominąć przekierowania powiązania automatycznego. Wartością domyślną jest false. |

**Przykład**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>sekcja packageRestore

*Ignorowane w 2.7 +*

Formanty Przywracanie pakietów podczas kompilacji.

| Key | Wartość |
| --- | --- |
| włączone | Wartość logiczna wskazująca, czy NuGet można wykonać przywracania automatycznie. Można również ustawić `EnableNuGetPackageRestore` zmienną środowiskową o wartości `True` zamiast ustawienie tego klucza w pliku konfiguracji. |
| automatyczne | Wartość logiczna wskazująca, czy NuGet należy sprawdzić, czy brakujących pakietów podczas kompilacji. |

**Przykład**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>sekcji rozwiązania

Formanty czy `packages` folderu rozwiązania jest uwzględniona w kontroli źródła. W tej sekcji działa tylko w `Nuget.Config` pliki w folderze rozwiązania.

| Key | Wartość |
| --- | --- |
| disableSourceControlIntegration | Wartość logiczna wskazująca, czy Ignoruj folderu pakietów podczas pracy z kontroli źródła. Wartość domyślna to false. |


**Przykład**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```


## <a name="package-source-sections"></a>Sekcje źródła pakietu

`packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, I `disabledPackageSources` wszystkie działają razem, konfigurowanie, jak NuGet współpracuje z repozytoriów pakietu podczas instalacji, przywracania i operacje aktualizacji.

[ `nuget sources` Polecenia](../tools/cli-ref-sources.md) jest zazwyczaj używany do zarządzania te ustawienia, z wyjątkiem `apikeys` której odbywa się przy użyciu [ `nuget setapikey` polecenia](../tools/cli-ref-setapikey.md).


### <a name="packagesources"></a>packageSources

Wyświetla wszystkie źródła pakietów znane.

| Key | Wartość |
| --- | --- |
| (nazwa można przypisać do źródła pakietu) | Ścieżka lub adres URL źródła pakietu. |

**Przykład**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```


### <a name="packagesourcecredentials"></a>packageSourceCredentials

Przechowywane nazwy użytkowników i hasła dla źródeł, zazwyczaj określana z `-username` i `-password` zmienia z `nuget sources`. Hasła są szyfrowane domyślnie, chyba że `-storepasswordincleartext` również używana jest opcja.

| Key | Wartość |
| --- | --- |
| Nazwa użytkownika | Nazwa użytkownika dla źródła w postaci zwykłego tekstu. |
| Hasło | Zaszyfrowane hasło dla tego źródła. |
| cleartextpassword | Hasło nieszyfrowane źródła. |

**Przykład:**

W pliku konfiguracyjnym `<packageSourceCredentials>` element zawiera węzły podrzędne dla każdej nazwy odpowiednich źródła (spacje w nazwie są zastępowane `_x0020+`). Oznacza to, że dla źródeł o nazwie "Contoso" i "Źródła testów", plik konfiguracji zawiera następujące przy użyciu hasła szyfrowane:

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

Podczas używania niezaszyfrowane hasła:

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

Przechowuje klucze źródeł, które korzystają z uwierzytelniania klucza interfejsu API, zgodnie z [ `nuget setapikey` polecenia](../tools/cli-ref-setapikey.md).

| Key | Wartość |
| --- | --- |
| (adres URL źródła) | Zaszyfrowany klucz interfejsu API. |

**Przykład**:

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```


### <a name="disabledpackagesources"></a>disabledPackageSources

Rozpoznane źródła aktualnie wyłączone. Może być pusta.

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

*(tylko 2.x; 3.x+ przestarzałe w)*

Identyfikuje do aktywnego źródła lub wskazuje agregacji wszystkich źródeł.

| Key | Wartość |
| --- | --- |
| (nazwa źródła) lub`All` | Jeśli klucz jest nazwę źródła, wartość jest ścieżka źródłowa lub adres URL. Jeśli `All`, wartość powinna być `(Aggregate source)` połączyć wszystkie źródła pakietów, które nie zostały wyłączone w przeciwnym razie wartość. |

**Przykład**:

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a>Korzystanie ze zmiennych środowiskowych

Można używać zmiennych środowiskowych w `NuGet.Config` wartości (NuGet 3.4 +) w celu zastosowania ustawień w czasie wykonywania.

Na przykład jeśli `HOME` ustawiono zmiennej środowiskowej w systemie Windows `c:\users\username`, wartość `%HOME%\NuGetRepository` w konfiguracji pliku jest rozpoznawana jako `c:\users\username\NuGetRepository`.

Podobnie jeśli `HOME` na system Mac/Linux jest ustawiona na `/home/myStuff`, następnie `$HOME/NuGetRepository` w konfiguracji pliku jest rozpoznawana jako `/home/myStuff/NuGetRepository`.

Jeśli zmienna środowiskowa nie zostanie znaleziony, NuGet korzysta z wartości literału z pliku konfiguracji.


## <a name="example-config-file"></a>Przykładowy plik konfiguracji

Poniżej znajduje się przykład `NuGet.Config` pliku, który przedstawia liczbę ustawień:

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
