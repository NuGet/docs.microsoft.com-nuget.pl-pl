---
title: Zarządzanie granicami zaufania pakietów
description: Opisuje proces instalowania podpisanych pakietów NuGet i konfigurowania ustawień zaufania podpisu pakietu.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 034b9dd9699af529e4d82d6ee5b1c42214673341
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428983"
---
# <a name="manage-package-trust-boundaries"></a>Zarządzanie granicami zaufania pakietów

Podpisane pakiety nie wymagają żadnych określonych akcji do zainstalowania; jeśli jednak zawartość została zmodyfikowana od momentu podpisania, instalacja jest blokowana z powodu błędu [NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Pakiety podpisane za pomocą niezaufanych certyfikatów są uważane za niepodpisane i są instalowane bez żadnych ostrzeżeń lub błędów, jak każdy inny niepodpisany pakiet.

## <a name="configure-package-signature-requirements"></a>Konfigurowanie wymagań dotyczących podpisu pakietu

> [!Note]
> Wymaga wersji NuGet 4.9.0+ i programu Visual Studio w wersji 15.9 lub nowszej w systemie Windows

Można skonfigurować sposób sprawdzania poprawności podpisów pakietów `signatureValidationMode` `require` przez klientów NuGet, ustawiając [`nuget config`](../reference/cli-reference/cli-ref-config.md) w pliku [nuget.config w pliku nuget.config](../reference/nuget-config-file.md) za pomocą polecenia.

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

W tym trybie zostanie zweryfikowany, czy wszystkie `nuget.config` pakiety są podpisane przez dowolny z certyfikatów zaufanych w pliku. Ten plik pozwala określić, którzy autorzy i / lub repozytoria są zaufane na podstawie odcisku palca certyfikatu.

### <a name="trust-package-author"></a>Autor pakietu zaufania

Aby ufać pakietom opartym [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) na podpisie autora, użyj polecenia, aby ustawić `author` właściwość w nuget.config.

```cmd
nuget.exe  trusted-signers Add -Name MyCompanyCert -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256
```

```xml
<trustedSigners>
  <author name="MyCompanyCert">
    <certificate fingerprint="CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
  </author>
</trustedSigners>
```

>[!TIP]
>Użyj `nuget.exe` [polecenia weryfikuj,](../reference/cli-reference/cli-ref-verify.md) `SHA256` aby uzyskać wartość odcisku palca certyfikatu.


### <a name="trust-all-packages-from-a-repository"></a>Ufaj wszystkim pakietom z repozytorium

Aby ufać pakietom opartym na `repository` podpisie repozytorium, użyj elementu:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>Właściciele pakietów zaufania

Podpisy repozytorium zawierają dodatkowe metadane w celu określenia właścicieli pakietu w momencie przesyłania. Pakiety można ograniczyć z repozytorium na podstawie listy właścicieli:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
      <owners>microsoft;nuget</owners>
  </repository>
</trustedSigners>
```

Jeśli pakiet ma wielu właścicieli, a jeden z tych właścicieli znajduje się na liście zaufanych, instalacja pakietu zakończy się pomyślnie.

### <a name="untrusted-root-certificates"></a>Niezaufane certyfikaty główne

W niektórych sytuacjach można włączyć weryfikację przy użyciu certyfikatów, które nie są połączone z zaufanym katalogiem głównym na komputerze lokalnym. Można użyć `allowUntrustedRoot` atrybutu, aby dostosować to zachowanie.

### <a name="sync-repository-certificates"></a>Certyfikaty repozytorium synchronizacji

Repozytoria pakietów powinny ogłaszać certyfikaty, których używają w [indeksie usług.](../api/service-index.md) Ostatecznie repozytorium zaktualizuje te certyfikaty, na przykład po wygaśnięciu certyfikatu. W takim przypadku klienci z określonymi zasadami będą wymagać aktualizacji konfiguracji w celu uwzględnienia nowo dodanego certyfikatu. Zaufane sygnatariusze skojarzone z repozytorium można łatwo `nuget.exe` uaktualnić za pomocą [polecenia synchronizacji zaufanych sygnatariuszy.](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name)

### <a name="schema-reference"></a>Odwołanie do schematu

Pełne odwołanie do schematu dla zasad klienta można znaleźć w [odwołaniu nuget.config](../reference/nuget-config-file.md#trustedsigners-section)

## <a name="related-articles"></a>Pokrewne artykuły:

- [Podpisywanie pakietów NuGet](../create-packages/Sign-a-Package.md)
- [Odwołanie do pakietów podpisanych](../reference/Signed-Packages-Reference.md)
