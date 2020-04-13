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
# <a name="manage-package-trust-boundaries"></a><span data-ttu-id="b6855-103">Zarządzanie granicami zaufania pakietów</span><span class="sxs-lookup"><span data-stu-id="b6855-103">Manage package trust boundaries</span></span>

<span data-ttu-id="b6855-104">Podpisane pakiety nie wymagają żadnych określonych akcji do zainstalowania; jeśli jednak zawartość została zmodyfikowana od momentu podpisania, instalacja jest blokowana z powodu błędu [NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="b6855-104">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked with error [NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="b6855-105">Pakiety podpisane za pomocą niezaufanych certyfikatów są uważane za niepodpisane i są instalowane bez żadnych ostrzeżeń lub błędów, jak każdy inny niepodpisany pakiet.</span><span class="sxs-lookup"><span data-stu-id="b6855-105">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="configure-package-signature-requirements"></a><span data-ttu-id="b6855-106">Konfigurowanie wymagań dotyczących podpisu pakietu</span><span class="sxs-lookup"><span data-stu-id="b6855-106">Configure package signature requirements</span></span>

> [!Note]
> <span data-ttu-id="b6855-107">Wymaga wersji NuGet 4.9.0+ i programu Visual Studio w wersji 15.9 lub nowszej w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="b6855-107">Requires NuGet 4.9.0+ and Visual Studio version 15.9 and later on Windows</span></span>

<span data-ttu-id="b6855-108">Można skonfigurować sposób sprawdzania poprawności podpisów pakietów `signatureValidationMode` `require` przez klientów NuGet, ustawiając [`nuget config`](../reference/cli-reference/cli-ref-config.md) w pliku [nuget.config w pliku nuget.config](../reference/nuget-config-file.md) za pomocą polecenia.</span><span class="sxs-lookup"><span data-stu-id="b6855-108">You can configure how NuGet clients validate package signatures by setting the `signatureValidationMode` to `require` in the [nuget.config](../reference/nuget-config-file.md) file using the [`nuget config`](../reference/cli-reference/cli-ref-config.md) command.</span></span>

```cmd
nuget.exe config -set signatureValidationMode=require
```

```xml
  <config>
    <add key="signatureValidationMode" value="require" />
  </config>
```

<span data-ttu-id="b6855-109">W tym trybie zostanie zweryfikowany, czy wszystkie `nuget.config` pakiety są podpisane przez dowolny z certyfikatów zaufanych w pliku.</span><span class="sxs-lookup"><span data-stu-id="b6855-109">This mode will verify that all packages are signed by any of the certificates trusted in the `nuget.config` file.</span></span> <span data-ttu-id="b6855-110">Ten plik pozwala określić, którzy autorzy i / lub repozytoria są zaufane na podstawie odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="b6855-110">This file allows you to specify which authors and/or repositories are trusted based on the certificate's fingerprint.</span></span>

### <a name="trust-package-author"></a><span data-ttu-id="b6855-111">Autor pakietu zaufania</span><span class="sxs-lookup"><span data-stu-id="b6855-111">Trust package author</span></span>

<span data-ttu-id="b6855-112">Aby ufać pakietom opartym [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) na podpisie autora, użyj polecenia, aby ustawić `author` właściwość w nuget.config.</span><span class="sxs-lookup"><span data-stu-id="b6855-112">To trust packages based on the author signature use the [`trusted-signers`](../reference/cli-reference/cli-ref-trusted-signers.md) command to set the `author` property in the nuget.config.</span></span>

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
><span data-ttu-id="b6855-113">Użyj `nuget.exe` [polecenia weryfikuj,](../reference/cli-reference/cli-ref-verify.md) `SHA256` aby uzyskać wartość odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="b6855-113">Use the `nuget.exe` [verify command](../reference/cli-reference/cli-ref-verify.md) to get the `SHA256` value of the certificate's fingerprint.</span></span>


### <a name="trust-all-packages-from-a-repository"></a><span data-ttu-id="b6855-114">Ufaj wszystkim pakietom z repozytorium</span><span class="sxs-lookup"><span data-stu-id="b6855-114">Trust all packages from a repository</span></span>

<span data-ttu-id="b6855-115">Aby ufać pakietom opartym na `repository` podpisie repozytorium, użyj elementu:</span><span class="sxs-lookup"><span data-stu-id="b6855-115">To trust packages based on the repository signature use the `repository` element:</span></span>

```xml
<trustedSigners>  
  <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
    <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B4676070...." 
                  hashAlgorithm="SHA256" 
                allowUntrustedRoot="false" />
  </repository>
</trustedSigners>
```

### <a name="trust-package-owners"></a><span data-ttu-id="b6855-116">Właściciele pakietów zaufania</span><span class="sxs-lookup"><span data-stu-id="b6855-116">Trust Package Owners</span></span>

<span data-ttu-id="b6855-117">Podpisy repozytorium zawierają dodatkowe metadane w celu określenia właścicieli pakietu w momencie przesyłania.</span><span class="sxs-lookup"><span data-stu-id="b6855-117">Repository signatures include additional metadata to determine the owners of the package at the time of submission.</span></span> <span data-ttu-id="b6855-118">Pakiety można ograniczyć z repozytorium na podstawie listy właścicieli:</span><span class="sxs-lookup"><span data-stu-id="b6855-118">You can restrict packages from a repository based on a list of owners:</span></span>

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

<span data-ttu-id="b6855-119">Jeśli pakiet ma wielu właścicieli, a jeden z tych właścicieli znajduje się na liście zaufanych, instalacja pakietu zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b6855-119">If a package has multiple owners, and any one of those owners is in the trusted list, the package installation will succeed.</span></span>

### <a name="untrusted-root-certificates"></a><span data-ttu-id="b6855-120">Niezaufane certyfikaty główne</span><span class="sxs-lookup"><span data-stu-id="b6855-120">Untrusted Root certificates</span></span>

<span data-ttu-id="b6855-121">W niektórych sytuacjach można włączyć weryfikację przy użyciu certyfikatów, które nie są połączone z zaufanym katalogiem głównym na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="b6855-121">In some situations you may want to enable verification using certificates that do not chain to a trusted root in the local machine.</span></span> <span data-ttu-id="b6855-122">Można użyć `allowUntrustedRoot` atrybutu, aby dostosować to zachowanie.</span><span class="sxs-lookup"><span data-stu-id="b6855-122">You can use the `allowUntrustedRoot` attribute to customize this behavior.</span></span>

### <a name="sync-repository-certificates"></a><span data-ttu-id="b6855-123">Certyfikaty repozytorium synchronizacji</span><span class="sxs-lookup"><span data-stu-id="b6855-123">Sync repository certificates</span></span>

<span data-ttu-id="b6855-124">Repozytoria pakietów powinny ogłaszać certyfikaty, których używają w [indeksie usług.](../api/service-index.md)</span><span class="sxs-lookup"><span data-stu-id="b6855-124">Package repositories should announce the certificates they use in their [service index](../api/service-index.md).</span></span> <span data-ttu-id="b6855-125">Ostatecznie repozytorium zaktualizuje te certyfikaty, na przykład po wygaśnięciu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="b6855-125">Eventually the repository will update these certificates, e.g. when the certificate expires.</span></span> <span data-ttu-id="b6855-126">W takim przypadku klienci z określonymi zasadami będą wymagać aktualizacji konfiguracji w celu uwzględnienia nowo dodanego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="b6855-126">When that happens, clients with specific policies will require an update to the configuration to include the newly added certificate.</span></span> <span data-ttu-id="b6855-127">Zaufane sygnatariusze skojarzone z repozytorium można łatwo `nuget.exe` uaktualnić za pomocą [polecenia synchronizacji zaufanych sygnatariuszy.](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name)</span><span class="sxs-lookup"><span data-stu-id="b6855-127">You can easily upgrade the trusted signers associated to a repository by using the `nuget.exe` [trusted-signers sync command](../reference/cli-reference/cli-ref-trusted-signers.md#nuget-trusted-signers-sync--name-name).</span></span>

### <a name="schema-reference"></a><span data-ttu-id="b6855-128">Odwołanie do schematu</span><span class="sxs-lookup"><span data-stu-id="b6855-128">Schema reference</span></span>

<span data-ttu-id="b6855-129">Pełne odwołanie do schematu dla zasad klienta można znaleźć w [odwołaniu nuget.config](../reference/nuget-config-file.md#trustedsigners-section)</span><span class="sxs-lookup"><span data-stu-id="b6855-129">The complete schema reference for the client policies can be found in the [nuget.config reference](../reference/nuget-config-file.md#trustedsigners-section)</span></span>

## <a name="related-articles"></a><span data-ttu-id="b6855-130">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="b6855-130">Related articles</span></span>

- [<span data-ttu-id="b6855-131">Podpisywanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="b6855-131">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="b6855-132">Odwołanie do pakietów podpisanych</span><span class="sxs-lookup"><span data-stu-id="b6855-132">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
