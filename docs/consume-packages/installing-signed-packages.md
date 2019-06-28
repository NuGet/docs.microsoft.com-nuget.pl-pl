---
title: Zarządzanie granicami zaufania pakietu
description: W tym artykule opisano proces instalowania NuGet podpisanych pakietów i konfigurowanie podpisu pakietu zaufania ustawienia.
author: karann-msft
ms.author: karann
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 8da57dc295ea78f2eb183226fc9b2f4a37e3f5db
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426636"
---
# <a name="manage-package-trust-boundaries"></a><span data-ttu-id="f5711-103">Zarządzanie granicami zaufania pakietu</span><span class="sxs-lookup"><span data-stu-id="f5711-103">Manage package trust boundaries</span></span>

<span data-ttu-id="f5711-104">Podpisanych pakietów nie wymagają żadnych określone działanie prowadzące do zainstalowania; Jeśli jednak zawartość została zmodyfikowana po podpisaniu, instalacja jest zablokowana z powodu błędu [NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="f5711-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="f5711-105">Pakiety podpisany przy użyciu niezaufane certyfikaty są traktowane jako jako bez znaku i są instalowane bez żadnych ostrzeżeń ani błędów, takich jak każdy inny pakiet bez znaku.</span><span class="sxs-lookup"><span data-stu-id="f5711-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="f5711-106">Skonfiguruj wymagania dotyczące podpisu pakietu</span><span class="sxs-lookup"><span data-stu-id="f5711-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="f5711-107">Wymaga NuGet 4.9.0+ i Visual Studio w wersji 15.9, a później Windows</span><span class="sxs-lookup"><span data-stu-id="f5711-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="f5711-108">Można skonfigurować, jak klienci programu NuGet zweryfikowania podpisów pakietów przez ustawienie `signatureValidationMode` do `require` w [nuget.config](../reference/nuget-config-file.md) plików przy użyciu [ `nuget config` ](../tools/cli-ref-config.md) polecenia.</span><span class="sxs-lookup"><span data-stu-id="f5711-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file.md) file using the [`nuget config`](../tools/cli-ref-config.md) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="f5711-109">W tym trybie sprawdzi, czy wszystkie pakiety są podpisane przez certyfikaty zaufanych w `nuget.config` pliku.</span><span class="sxs-lookup"><span data-stu-id="f5711-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="f5711-110">Ten plik pozwala określić które autorzy i/lub repozytoria są zaufane w oparciu o odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="f5711-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="f5711-111">Zaufanie autora pakietu</span><span class="sxs-lookup"><span data-stu-id="f5711-111">Trust package author</span></span>

<span data-ttu-id="f5711-112">Zaufania oparta na wykorzystaniu podpisu autor pakietów [ `trusted-signers` ](../tools/cli-ref-trusted-signers.md) polecenie, aby ustawić `author` właściwość w pliku nuget.config.</span><span class="sxs-lookup"><span data-stu-id="f5711-112">To trust packages based on the author signature use the [`trusted-signers`](../tools/cli-ref-trusted-signers.md) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="f5711-113">Użyj `nuget.exe` [sprawdzić polecenie](../tools/cli-ref-verify.md) można pobrać `SHA256` wartość odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="f5711-113">Use the `nuget.exe` [verify command](../tools/cli-ref-verify.md) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="f5711-114">Zaufanie wszystkie pakiety z repozytorium</span><span class="sxs-lookup"><span data-stu-id="f5711-114">Trust all packages from a repository</span></span>

<span data-ttu-id="f5711-115">Zaufania oparta na wykorzystaniu podpisu repozytorium pakietów `repository` elementu:</span><span class="sxs-lookup"><span data-stu-id="f5711-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="f5711-116">Zaufanie właścicieli pakietu</span><span class="sxs-lookup"><span data-stu-id="f5711-116">Trust Package Owners</span></span>

<span data-ttu-id="f5711-117">Podpisy repozytorium obejmują dodatkowe metadane, aby określić właścicieli pakietu w momencie przesłania.</span><span class="sxs-lookup"><span data-stu-id="f5711-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="f5711-118">Można ograniczyć pakietów z repozytorium, na podstawie listy właścicieli:</span><span class="sxs-lookup"><span data-stu-id="f5711-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="f5711-119">Jeśli pakiet ma wiele właścicieli, a jeden z tych właścicieli jest na liście zaufanych, instalacja pakietu zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="f5711-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="f5711-120">Niezaufane certyfikaty główne</span><span class="sxs-lookup"><span data-stu-id="f5711-120">Untrusted Root certificates</span></span>

<span data-ttu-id="f5711-121">W niektórych sytuacjach można włączyć weryfikację przy użyciu certyfikatów, które nie są powiązane zaufany główny urząd certyfikacji na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="f5711-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="f5711-122">Możesz użyć `allowUntrustedRoot` atrybutu, aby dostosować to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="f5711-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="f5711-123">Synchronizacja repozytorium certyfikatów</span><span class="sxs-lookup"><span data-stu-id="f5711-123">Sync repository certificates</span></span>

<span data-ttu-id="f5711-124">Repozytoriów pakietów powinno poinformować o certyfikaty używają w swoich [indeks usług](../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="f5711-124">Package repositories should announce the certificates they use in their [service index](../api/service-index.md).</span></span> <span data-ttu-id="f5711-125">Po pewnym czasie repozytorium spowoduje zaktualizowanie te certyfikaty, np. po wygaśnięciu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="f5711-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="f5711-126">Jeśli tak się stanie, klientów przy użyciu określonych zasad będzie wymagać aktualizacji konfiguracji do uwzględnienia nowo dodano certyfikat.</span><span class="sxs-lookup"><span data-stu-id="f5711-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="f5711-127">Możesz łatwo przeprowadzić uaktualnienie zaufane osoby podpisujące skojarzony z repozytorium przy użyciu `nuget.exe` [zaufane osoby podpisujące synchronizacji polecenia](../tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span><span class="sxs-lookup"><span data-stu-id="f5711-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](../tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="f5711-128">Odwołanie do schematu</span><span class="sxs-lookup"><span data-stu-id="f5711-128">Schema reference</span></span>

<span data-ttu-id="f5711-129">Odwołanie do schematu pełną zasady klienta można znaleźć w [odwołanie do pliku nuget.config](../reference/nuget-config-file.md#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="f5711-129">The complete schema reference for the client policies can be found in the [nuget.config reference](../reference/nuget-config-file.md#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="f5711-130">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="f5711-130">Related articles</span></span>

- [<span data-ttu-id="f5711-131">Podpisywanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="f5711-131">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="f5711-132">Dokumentacja podpisanych pakietów</span><span class="sxs-lookup"><span data-stu-id="f5711-132">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
