---
title: Zarządzanie granicami zaufania pakietów
description: Opisuje proces instalowania podpisanych pakietów NuGet i konfigurowania ustawień zaufania sygnatury pakietu.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 034b9dd9699af529e4d82d6ee5b1c42214673341
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237630"
---
# <a name="manage-package-trust-boundaries"></a>Zarządzanie granicami zaufania pakietów

Podpisane pakiety nie wymagają żadnej konkretnej akcji, która ma zostać zainstalowana; Jeśli jednak zawartość została zmodyfikowana od czasu podpisania, instalacja jest zablokowana z powodu błędu [NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Pakiety podpisane przy użyciu certyfikatów niezaufanych są uznawane za niepodpisane i instalowane bez żadnych ostrzeżeń lub błędów, takich jak każdy inny niepodpisany pakiet.

## <a name="configure-package-signature-requirements"></a>Skonfiguruj wymagania dotyczące podpisu pakietu

> [!Note]
> Wymaga NuGet 4.9.0 + i Visual Studio w wersji 15,9 lub nowszej w systemie Windows

Można skonfigurować sposób weryfikowania podpisów pakietów przez klientów NuGet przez ustawienie `signatureValidationMode` do `require` w pliku [nuget.config](../reference/nuget-config-file.md) przy użyciu [`nuget config`](../reference/cli-reference/cli-ref-config.md) polecenia.

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

Ten tryb pozwala sprawdzić, czy wszystkie pakiety są podpisane przez dowolny z certyfikatów zaufanych w `nuget.config` pliku. Ten plik umożliwia określenie, którzy autorzy i/lub repozytoria są zaufani na podstawie odcisku palca certyfikatu.

### <a name="trust-package-author"></a>Autor pakietu zaufania

Aby ufać pakietom opartym na podpisie autora, użyj [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) polecenia, aby ustawić `author` właściwość w nuget.config.

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
>Użyj `nuget.exe` [polecenia Weryfikuj](../reference/cli-reference/cli-ref-verify.md) , aby pobrać `SHA256` wartość odcisku palca certyfikatu.


### <a name="trust-all-packages-from-a-repository"></a>Ufaj wszystkim pakietom z repozytorium

Aby ufać pakietom opartym na podpisie repozytorium, użyj `repository` elementu:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>Właściciele zaufanych pakietów

Sygnatury repozytorium zawierają dodatkowe metadane w celu ustalenia właścicieli pakietu w momencie przesłania. Można ograniczyć pakiety z repozytorium na podstawie listy właścicieli:

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

Jeśli pakiet ma wielu właścicieli, a jeden z nich znajduje się na liście zaufanych, instalacja pakietu zakończy się pomyślnie.

### <a name="untrusted-root-certificates"></a>Niezaufane certyfikaty główne

W niektórych sytuacjach może być konieczne włączenie weryfikacji przy użyciu certyfikatów, które nie są powiązane z zaufanym certyfikatem głównym na komputerze lokalnym. Możesz użyć atrybutu, `allowUntrustedRoot` Aby dostosować to zachowanie.

### <a name="sync-repository-certificates"></a>Synchronizuj certyfikaty repozytorium

Repozytoria pakietów powinni ogłaszać certyfikaty używane w ich [indeksie usług](../api/service-index.md). Ostatecznie repozytorium zaktualizuje te certyfikaty, np. po wygaśnięciu certyfikatu. W takim przypadku klienci z określonymi zasadami będą musieli zaktualizować konfigurację w celu uwzględnienia nowo dodanego certyfikatu. Można łatwo uaktualnić zaufane osoby podpisujące skojarzone z repozytorium za pomocą `nuget.exe` [polecenia synchronizacji zaufanych nadawców](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).

### <a name="schema-reference"></a>Odwołanie do schematu

Pełne odwołanie do schematu dotyczące zasad klienta można znaleźć w temacie [nuget.config Reference](../reference/nuget-config-file.md#trustedsigners-section)

## <a name="related-articles"></a>Pokrewne artykuły:

- [Podpisywanie pakietów NuGet](../create-packages/Sign-a-Package.md)
- [Odwołanie do podpisanych pakietów](../reference/Signed-Packages-Reference.md)
