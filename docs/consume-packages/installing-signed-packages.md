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
# <a name="install-a-signed-package"></a><span data-ttu-id="985d9-103">Zainstaluj pakiet podpisem</span><span class="sxs-lookup"><span data-stu-id="985d9-103">Install a signed package</span></span>

<span data-ttu-id="985d9-104">Podpisanych pakietów nie wymagają żadnych określone działanie prowadzące do zainstalowania; Jeśli jednak zawartość została zmodyfikowana po podpisaniu, instalacja jest zablokowana z powodu błędu [NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="985d9-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="985d9-105">Pakiety podpisany przy użyciu niezaufane certyfikaty są traktowane jako jako bez znaku i są instalowane bez żadnych ostrzeżeń ani błędów, takich jak każdy inny pakiet bez znaku.</span><span class="sxs-lookup"><span data-stu-id="985d9-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="985d9-106">Skonfiguruj wymagania dotyczące podpisu pakietu</span><span class="sxs-lookup"><span data-stu-id="985d9-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="985d9-107">Wymaga NuGet 4.9.0+ i Visual Studio w wersji 15.9, a później Windows</span><span class="sxs-lookup"><span data-stu-id="985d9-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="985d9-108">Można skonfigurować, jak klienci programu NuGet zweryfikowania podpisów pakietów przez ustawienie `signatureValidationMode` do `require` w [nuget.config](../reference/nuget-config-file) plików przy użyciu [ `nuget config` ](../tools/cli-ref-config) polecenia.</span><span class="sxs-lookup"><span data-stu-id="985d9-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file) file using the [`nuget config`](../tools/cli-ref-config) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="985d9-109">W tym trybie sprawdzi, czy wszystkie pakiety są podpisane przez certyfikaty zaufanych w `nuget.config` pliku.</span><span class="sxs-lookup"><span data-stu-id="985d9-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="985d9-110">Ten plik pozwala określić które autorzy i/lub repozytoria są zaufane w oparciu o odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="985d9-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="985d9-111">Zaufanie autora pakietu</span><span class="sxs-lookup"><span data-stu-id="985d9-111">Trust package author</span></span>

<span data-ttu-id="985d9-112">Zaufania oparta na wykorzystaniu podpisu autor pakietów [ `trusted-signers` ](..tools/cli-ref-trusted-signers) polecenie, aby ustawić `author` właściwość w pliku nuget.config.</span><span class="sxs-lookup"><span data-stu-id="985d9-112">To trust packages based on the author signature use the [`trusted-signers`](..tools/cli-ref-trusted-signers) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="985d9-113">Użyj `nuget.exe` [sprawdzić polecenie](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) można pobrać `SHA256` wartość odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="985d9-113">Use the `nuget.exe` [verify command](https://docs.microsoft.com/en-us/nuget/tools/cli-ref-verify) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="985d9-114">Zaufanie wszystkie pakiety z repozytorium</span><span class="sxs-lookup"><span data-stu-id="985d9-114">Trust all packages from a repository</span></span>

<span data-ttu-id="985d9-115">Zaufania oparta na wykorzystaniu podpisu repozytorium pakietów `repository` elementu:</span><span class="sxs-lookup"><span data-stu-id="985d9-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="985d9-116">Zaufanie właścicieli pakietu</span><span class="sxs-lookup"><span data-stu-id="985d9-116">Trust Package Owners</span></span>

<span data-ttu-id="985d9-117">Podpisy repozytorium obejmują dodatkowe metadane, aby określić właścicieli pakietu w momencie przesłania.</span><span class="sxs-lookup"><span data-stu-id="985d9-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="985d9-118">Można ograniczyć pakietów z repozytorium, na podstawie listy właścicieli:</span><span class="sxs-lookup"><span data-stu-id="985d9-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="985d9-119">Jeśli pakiet ma wiele właścicieli, a jeden z tych właścicieli jest na liście zaufanych, instalacja pakietu zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="985d9-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="985d9-120">Niezaufane certyfikaty główne</span><span class="sxs-lookup"><span data-stu-id="985d9-120">Untrusted Root certificates</span></span>

<span data-ttu-id="985d9-121">W niektórych sytuacjach można włączyć weryfikację przy użyciu certyfikatów, które nie są powiązane zaufany główny urząd certyfikacji na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="985d9-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="985d9-122">Możesz użyć `allowUntrustedRoot` atrybutu, aby dostosować to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="985d9-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="985d9-123">Synchronizacja repozytorium certyfikatów</span><span class="sxs-lookup"><span data-stu-id="985d9-123">Sync repository certificates</span></span>

<span data-ttu-id="985d9-124">Repozytoriów pakietów powinno poinformować o certyfikaty używają w swoich [indeks usług](https://docs.microsoft.com/en-us/nuget/api/service-index).</span><span class="sxs-lookup"><span data-stu-id="985d9-124">Package repositories should announce the certificates they use in their [service index](https://docs.microsoft.com/en-us/nuget/api/service-index).</span></span> <span data-ttu-id="985d9-125">Po pewnym czasie repozytorium spowoduje zaktualizowanie te certyfikaty, np. po wygaśnięciu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="985d9-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="985d9-126">Jeśli tak się stanie, klientów przy użyciu określonych zasad będzie wymagać aktualizacji konfiguracji do uwzględnienia nowo dodano certyfikat.</span><span class="sxs-lookup"><span data-stu-id="985d9-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="985d9-127">Możesz łatwo przeprowadzić uaktualnienie zaufane osoby podpisujące skojarzony z repozytorium przy użyciu `nuget.exe` [zaufane osoby podpisujące synchronizacji polecenia](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span><span class="sxs-lookup"><span data-stu-id="985d9-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](/nuget/tools/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="985d9-128">Odwołanie do schematu</span><span class="sxs-lookup"><span data-stu-id="985d9-128">Schema reference</span></span>

<span data-ttu-id="985d9-129">Odwołanie do schematu pełną zasady klienta można znaleźć w [odwołanie do pliku nuget.config](/nuget/reference/nuget-config-file#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="985d9-129">The complete schema reference for the client policies can be found in the [nuget.config reference](/nuget/reference/nuget-config-file#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="985d9-130">Powiązane artykuły</span><span class="sxs-lookup"><span data-stu-id="985d9-130">Related articles</span></span>

- [<span data-ttu-id="985d9-131">Różne sposoby, aby zainstalować pakiet NuGet</span><span class="sxs-lookup"><span data-stu-id="985d9-131">Different ways to install a NuGet Package</span></span>](ways-to-install-a-package.md)
- [<span data-ttu-id="985d9-132">Podpisywanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="985d9-132">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="985d9-133">Dokumentacja podpisanych pakietów</span><span class="sxs-lookup"><span data-stu-id="985d9-133">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
