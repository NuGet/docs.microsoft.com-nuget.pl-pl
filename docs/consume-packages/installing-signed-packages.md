---
title: Zarządzanie granicami zaufania pakietów
description: Opisuje proces instalowania podpisanych pakietów NuGet i konfigurowania ustawień zaufania sygnatury pakietu.
author: JonDouglas
ms.author: jodou
ms.date: 11/29/2018
ms.topic: conceptual
ms.openlocfilehash: 596ce330e434253e6fb200aa59ae4e14d47779ed
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774807"
---
# <a name="manage-package-trust-boundaries"></a><span data-ttu-id="0baa4-103">Zarządzanie granicami zaufania pakietów</span><span class="sxs-lookup"><span data-stu-id="0baa4-103">Manage package trust boundaries</span></span>

<span data-ttu-id="0baa4-104">Podpisane pakiety nie wymagają żadnej konkretnej akcji, która ma zostać zainstalowana; Jeśli jednak zawartość została zmodyfikowana od czasu podpisania, instalacja jest zablokowana z powodu błędu [NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="0baa4-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="0baa4-105">Pakiety podpisane przy użyciu certyfikatów niezaufanych są uznawane za niepodpisane i instalowane bez żadnych ostrzeżeń lub błędów, takich jak każdy inny niepodpisany pakiet.</span><span class="sxs-lookup"><span data-stu-id="0baa4-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="0baa4-106">Skonfiguruj wymagania dotyczące podpisu pakietu</span><span class="sxs-lookup"><span data-stu-id="0baa4-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="0baa4-107">Wymaga NuGet 4.9.0 + i Visual Studio w wersji 15,9 lub nowszej w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="0baa4-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="0baa4-108">Można skonfigurować sposób weryfikowania podpisów pakietów przez klientów NuGet przez ustawienie `signatureValidationMode` do `require` w pliku [nuget.config](../reference/nuget-config-file.md) przy użyciu [`nuget config`](../reference/cli-reference/cli-ref-config.md) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0baa4-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file.md) file using the [`nuget config`](../reference/cli-reference/cli-ref-config.md) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="0baa4-109">Ten tryb pozwala sprawdzić, czy wszystkie pakiety są podpisane przez dowolny z certyfikatów zaufanych w `nuget.config` pliku.</span><span class="sxs-lookup"><span data-stu-id="0baa4-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="0baa4-110">Ten plik umożliwia określenie, którzy autorzy i/lub repozytoria są zaufani na podstawie odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0baa4-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="0baa4-111">Autor pakietu zaufania</span><span class="sxs-lookup"><span data-stu-id="0baa4-111">Trust package author</span></span>

<span data-ttu-id="0baa4-112">Aby ufać pakietom opartym na podpisie autora, użyj [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) polecenia, aby ustawić `author` właściwość w nuget.config.</span><span class="sxs-lookup"><span data-stu-id="0baa4-112">To trust packages based on the author signature use the [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="0baa4-113">Użyj `nuget.exe` [polecenia Weryfikuj](../reference/cli-reference/cli-ref-verify.md) , aby pobrać `SHA256` wartość odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0baa4-113">Use the `nuget.exe` [verify command](../reference/cli-reference/cli-ref-verify.md) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="0baa4-114">Ufaj wszystkim pakietom z repozytorium</span><span class="sxs-lookup"><span data-stu-id="0baa4-114">Trust all packages from a repository</span></span>

<span data-ttu-id="0baa4-115">Aby ufać pakietom opartym na podpisie repozytorium, użyj `repository` elementu:</span><span class="sxs-lookup"><span data-stu-id="0baa4-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="0baa4-116">Właściciele zaufanych pakietów</span><span class="sxs-lookup"><span data-stu-id="0baa4-116">Trust Package Owners</span></span>

<span data-ttu-id="0baa4-117">Sygnatury repozytorium zawierają dodatkowe metadane w celu ustalenia właścicieli pakietu w momencie przesłania.</span><span class="sxs-lookup"><span data-stu-id="0baa4-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="0baa4-118">Można ograniczyć pakiety z repozytorium na podstawie listy właścicieli:</span><span class="sxs-lookup"><span data-stu-id="0baa4-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="0baa4-119">Jeśli pakiet ma wielu właścicieli, a jeden z nich znajduje się na liście zaufanych, instalacja pakietu zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="0baa4-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="0baa4-120">Niezaufane certyfikaty główne</span><span class="sxs-lookup"><span data-stu-id="0baa4-120">Untrusted Root certificates</span></span>

<span data-ttu-id="0baa4-121">W niektórych sytuacjach może być konieczne włączenie weryfikacji przy użyciu certyfikatów, które nie są powiązane z zaufanym certyfikatem głównym na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="0baa4-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="0baa4-122">Możesz użyć atrybutu, `allowUntrustedRoot` Aby dostosować to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="0baa4-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="0baa4-123">Synchronizuj certyfikaty repozytorium</span><span class="sxs-lookup"><span data-stu-id="0baa4-123">Sync repository certificates</span></span>

<span data-ttu-id="0baa4-124">Repozytoria pakietów powinni ogłaszać certyfikaty używane w ich [indeksie usług](../api/service-index.md).</span><span class="sxs-lookup"><span data-stu-id="0baa4-124">Package repositories should announce the certificates they use in their [service index](../api/service-index.md).</span></span> <span data-ttu-id="0baa4-125">Ostatecznie repozytorium zaktualizuje te certyfikaty, np. po wygaśnięciu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0baa4-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="0baa4-126">W takim przypadku klienci z określonymi zasadami będą musieli zaktualizować konfigurację w celu uwzględnienia nowo dodanego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0baa4-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="0baa4-127">Można łatwo uaktualnić zaufane osoby podpisujące skojarzone z repozytorium za pomocą `nuget.exe` [polecenia synchronizacji zaufanych nadawców](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).</span><span class="sxs-lookup"><span data-stu-id="0baa4-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="0baa4-128">Odwołanie do schematu</span><span class="sxs-lookup"><span data-stu-id="0baa4-128">Schema reference</span></span>

<span data-ttu-id="0baa4-129">Pełne odwołanie do schematu dotyczące zasad klienta można znaleźć w temacie [nuget.config Reference](../reference/nuget-config-file.md#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="0baa4-129">The complete schema reference for the client policies can be found in the [nuget.config reference](../reference/nuget-config-file.md#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="0baa4-130">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="0baa4-130">Related articles</span></span>

- [<span data-ttu-id="0baa4-131">Podpisywanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="0baa4-131">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="0baa4-132">Odwołanie do podpisanych pakietów</span><span class="sxs-lookup"><span data-stu-id="0baa4-132">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
