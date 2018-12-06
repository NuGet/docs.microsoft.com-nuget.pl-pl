---
title: Instalowanie pakietu NuGet podpisem
description: W tym artykule opisano proces instalowania NuGet podpisanych pakietów i konfigurowanie podpisu pakietu zaufania ustawienia.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 11ffaee96b6f6a9260f38c534328b6631cd96abf
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977851"
---
# <a name="install-a-signed-package"></a>Zainstaluj pakiet podpisem

Podpisanych pakietów nie wymagają żadnych określone działanie prowadzące do zainstalowania; Jeśli jednak zawartość została zmodyfikowana po podpisaniu, instalacja jest zablokowana z powodu błędu [NU3008](../reference/errors-and-warnings/NU3008.md).

> [!Warning]
> Pakiety podpisany przy użyciu niezaufane certyfikaty są traktowane jako jako bez znaku i są instalowane bez żadnych ostrzeżeń ani błędów, takich jak każdy inny pakiet bez znaku.

## <a name="configure-package-signature-requirements"></a>Skonfiguruj wymagania dotyczące podpisu pakietu

> [!Note]
> Wymaga NuGet 4.9.0+ i Visual Studio w wersji 15.9, a później Windows

Można skonfigurować, jak klienci programu NuGet zweryfikowania podpisów pakietów przez ustawienie `signatureValidationMode` do `require` w [nuget.config](../reference/nuget-config-file) plików przy użyciu [ `nuget config` ](../tools/cli-ref-config) polecenia.

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

W tym trybie sprawdzi, czy wszystkie pakiety są podpisane przez certyfikaty zaufanych w `nuget.config` pliku. Ten plik pozwala określić które autorzy i/lub repozytoria są zaufane w oparciu o odcisku palca certyfikatu.

### <a name="trust-package-author"></a>Zaufanie autora pakietu

Zaufania oparta na wykorzystaniu podpisu autor pakietów [ `trusted-signers` ](..tools/cli-ref-trusted-signers) polecenie, aby ustawić `author` właściwość w pliku nuget.config.

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
>Użyj `nuget.exe` [sprawdzić polecenie](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) można pobrać `SHA256` wartość odcisku palca certyfikatu.


### <a name="trust-all-packages-from-a-repository"></a>Zaufanie wszystkie pakiety z repozytorium

Zaufania oparta na wykorzystaniu podpisu repozytorium pakietów `repository` elementu:

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a>Zaufanie właścicieli pakietu

Podpisy repozytorium obejmują dodatkowe metadane, aby określić właścicieli pakietu w momencie przesłania. Można ograniczyć pakietów z repozytorium, na podstawie listy właścicieli:

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

Jeśli pakiet ma wiele właścicieli, a jeden z tych właścicieli jest na liście zaufanych, instalacja pakietu zakończy się pomyślnie.

### <a name="untrusted-root-certificates"></a>Niezaufane certyfikaty główne

W niektórych sytuacjach można włączyć weryfikację przy użyciu certyfikatów, które nie są powiązane zaufany główny urząd certyfikacji na komputerze lokalnym. Możesz użyć `allowUntrustedRoot` atrybutu, aby dostosować to zachowanie.

### <a name="sync-repository-certificates"></a>Synchronizacja repozytorium certyfikatów

Repozytoriów pakietów powinno poinformować o certyfikaty używają w swoich [indeks usług](https://docs.microsoft.com/en-us/nuget/api/service-index). Po pewnym czasie repozytorium spowoduje zaktualizowanie te certyfikaty, np. po wygaśnięciu certyfikatu. Jeśli tak się stanie, klientów przy użyciu określonych zasad będzie wymagać aktualizacji konfiguracji do uwzględnienia nowo dodano certyfikat. Możesz łatwo przeprowadzić uaktualnienie zaufane osoby podpisujące skojarzony z repozytorium przy użyciu `nuget.exe` [zaufane osoby podpisujące synchronizacji polecenia](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).

### <a name="schema-reference"></a>Odwołanie do schematu

Odwołanie do schematu pełną zasady klienta można znaleźć w [odwołanie do pliku nuget.config](/nuget/reference/nuget-config-file#trustedsigners-section)

## <a name="related-articles"></a>Powiązane artykuły

- [Różne sposoby, aby zainstalować pakiet NuGet](ways-to-install-a-package.md)
- [Podpisywanie pakietów NuGet](../create-packages/Sign-a-Package.md)
- [Dokumentacja podpisanych pakietów](../reference/Signed-Packages-Reference.md)
