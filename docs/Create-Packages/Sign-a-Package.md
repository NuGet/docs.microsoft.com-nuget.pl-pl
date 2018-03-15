---
title: "Podpisywanie pakietów NuGet | Dokumentacja firmy Microsoft"
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Wyjaśniono, jak podpisanych pakietów można włączyć weryfikację zawartości integralności."
keywords: "Pakiet NuGet podpisywania zabezpieczeń NuGet, tworzenie pakietów podpisem"
ms.reviewer:
- karann-msft
- anangaur
ms.openlocfilehash: aaf6ab7d7a9e66d4d9519d8aa79f0d0fac646d3a
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="b4fa5-104">Podpisywanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="b4fa5-104">Signing NuGet Packages</span></span>

<span data-ttu-id="b4fa5-105">Podpisywanie pakietu jest procesem, który sprawia, że pakiet nie został zmodyfikowany od czasu jego utworzenia.</span><span class="sxs-lookup"><span data-stu-id="b4fa5-105">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4fa5-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b4fa5-106">Prerequisites</span></span>

1. <span data-ttu-id="b4fa5-107">Pakiet ( `.nupkg` pliku) do podpisywania.</span><span class="sxs-lookup"><span data-stu-id="b4fa5-107">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="b4fa5-108">Zobacz [utworzenie pakietu](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="b4fa5-108">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="b4fa5-109">nuget.exe 4.6.0 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="b4fa5-109">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="b4fa5-110">Zobacz temat jak [zainstaluj interfejs wiersza polecenia NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="b4fa5-110">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="b4fa5-111">[Certyfikat podpisywania kodu](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="b4fa5-111">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

> [!Warning]
> <span data-ttu-id="b4fa5-112">nuget.org nie akceptuje obecnie podpisanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="b4fa5-112">nuget.org does not currently accept signed packages.</span></span> <span data-ttu-id="b4fa5-113">Możesz zarejestrować pakietów do publikowania do niestandardowych źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="b4fa5-113">You can sign packages for publishing to custom feeds.</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="b4fa5-114">Podpisywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="b4fa5-114">Sign a package</span></span>

<span data-ttu-id="b4fa5-115">Aby zarejestrować pakiet, należy użyć [znak nuget](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="b4fa5-115">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="b4fa5-116">Zgodnie z opisem w dokumentacji poleceń, można użyć dostępny certyfikat w magazynie certyfikatów lub używania certyfikatu z pliku.</span><span class="sxs-lookup"><span data-stu-id="b4fa5-116">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="b4fa5-117">Typowe problemy podczas podpisywania pakietu</span><span class="sxs-lookup"><span data-stu-id="b4fa5-117">Common problems when signing a package</span></span>

- <span data-ttu-id="b4fa5-118">Certyfikat nie jest prawidłowy do podpisywania kodu.</span><span class="sxs-lookup"><span data-stu-id="b4fa5-118">The certificate is not valid for code signing.</span></span> <span data-ttu-id="b4fa5-119">Należy się upewnić się, że określony certyfikat ma odpowiednie rozszerzone użycie klucza (EKU 1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="b4fa5-119">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="b4fa5-120">Certyfikat nie spełnia podstawowe wymagania, np. RSA, SHA-256 algorytm podpisu lub publicznego klucza 2048 bitów lub większej.</span><span class="sxs-lookup"><span data-stu-id="b4fa5-120">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="b4fa5-121">Certyfikat wygasł lub został odwołany.</span><span class="sxs-lookup"><span data-stu-id="b4fa5-121">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="b4fa5-122">Serwer znaczników czasu nie spełnia wymagań dotyczących certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="b4fa5-122">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="b4fa5-123">Pakiety podpisem powinna zawierać sygnaturę czasową, aby upewnić się, że podpis pozostaje ważny po wygaśnięciu certyfikatu podpisywania.</span><span class="sxs-lookup"><span data-stu-id="b4fa5-123">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="b4fa5-124">Tworzy operacji logowania [ostrzeżenie NU3002](../reference/Errors-and-Warnings.md#nu3002) przy logowaniu się bez sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="b4fa5-124">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="b4fa5-125">Sprawdź podpisanego pakietu</span><span class="sxs-lookup"><span data-stu-id="b4fa5-125">Verify a signed package</span></span>

<span data-ttu-id="b4fa5-126">Użyj [nuget Sprawdź](../tools/cli-ref-verify.md) Aby wyświetlić szczegóły sygnatury danego pakietu:</span><span class="sxs-lookup"><span data-stu-id="b4fa5-126">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="b4fa5-127">Zainstaluj pakiet podpisem</span><span class="sxs-lookup"><span data-stu-id="b4fa5-127">Install a signed package</span></span>

<span data-ttu-id="b4fa5-128">Podpisanych pakietów nie wymagają żadnych określonych czynności w celu zainstalowania; Jednak jeśli zawartość została zmodyfikowana po podpisaniu, podczas instalacji będzie zablokowane i tworzy [błąd NU3008](../reference/Errors-and-Warnings.md#nu3008).</span><span class="sxs-lookup"><span data-stu-id="b4fa5-128">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="b4fa5-129">Uwzględniane są podpisane za pomocą certyfikatów niezaufanych pakiety jako bez znaku i są instalowane bez żadnych ostrzeżeń ani błędów, takich jak niepodpisanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="b4fa5-129">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="b4fa5-130">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="b4fa5-130">See also</span></span>

[<span data-ttu-id="b4fa5-131">Podpisana pakietów odniesienia</span><span class="sxs-lookup"><span data-stu-id="b4fa5-131">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
