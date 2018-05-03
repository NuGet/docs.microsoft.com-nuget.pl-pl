---
title: Podpisywanie pakietów NuGet
description: Wyjaśniono, jak podpisanych pakietów można włączyć weryfikację zawartości integralności.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a469cbdd218a0e9c18950bb0d36faf4dbcb42a01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="3011c-103">Podpisywanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="3011c-103">Signing NuGet Packages</span></span>

<span data-ttu-id="3011c-104">Podpisywanie pakietu jest procesem, który sprawia, że pakiet nie został zmodyfikowany od czasu jego utworzenia.</span><span class="sxs-lookup"><span data-stu-id="3011c-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3011c-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3011c-105">Prerequisites</span></span>

1. <span data-ttu-id="3011c-106">Pakiet ( `.nupkg` pliku) do podpisywania.</span><span class="sxs-lookup"><span data-stu-id="3011c-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="3011c-107">Zobacz [utworzenie pakietu](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="3011c-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="3011c-108">nuget.exe 4.6.0 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="3011c-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="3011c-109">Zobacz temat jak [zainstaluj interfejs wiersza polecenia NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="3011c-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="3011c-110">[Certyfikat podpisywania kodu](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="3011c-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

> [!Warning]
> <span data-ttu-id="3011c-111">nuget.org nie akceptuje obecnie podpisanych pakietów.</span><span class="sxs-lookup"><span data-stu-id="3011c-111">nuget.org does not currently accept signed packages.</span></span> <span data-ttu-id="3011c-112">Możesz zarejestrować pakietów do publikowania do niestandardowych źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="3011c-112">You can sign packages for publishing to custom feeds.</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="3011c-113">Podpisywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="3011c-113">Sign a package</span></span>

<span data-ttu-id="3011c-114">Aby zarejestrować pakiet, należy użyć [znak nuget](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="3011c-114">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="3011c-115">Zgodnie z opisem w dokumentacji poleceń, można użyć dostępny certyfikat w magazynie certyfikatów lub używania certyfikatu z pliku.</span><span class="sxs-lookup"><span data-stu-id="3011c-115">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="3011c-116">Typowe problemy podczas podpisywania pakietu</span><span class="sxs-lookup"><span data-stu-id="3011c-116">Common problems when signing a package</span></span>

- <span data-ttu-id="3011c-117">Certyfikat nie jest prawidłowy do podpisywania kodu.</span><span class="sxs-lookup"><span data-stu-id="3011c-117">The certificate is not valid for code signing.</span></span> <span data-ttu-id="3011c-118">Należy się upewnić się, że określony certyfikat ma odpowiednie rozszerzone użycie klucza (EKU 1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="3011c-118">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="3011c-119">Certyfikat nie spełnia podstawowe wymagania, np. RSA, SHA-256 algorytm podpisu lub publicznego klucza 2048 bitów lub większej.</span><span class="sxs-lookup"><span data-stu-id="3011c-119">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="3011c-120">Certyfikat wygasł lub został odwołany.</span><span class="sxs-lookup"><span data-stu-id="3011c-120">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="3011c-121">Serwer znaczników czasu nie spełnia wymagań dotyczących certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="3011c-121">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="3011c-122">Pakiety podpisem powinna zawierać sygnaturę czasową, aby upewnić się, że podpis pozostaje ważny po wygaśnięciu certyfikatu podpisywania.</span><span class="sxs-lookup"><span data-stu-id="3011c-122">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="3011c-123">Tworzy operacji logowania [ostrzeżenie NU3002](../reference/Errors-and-Warnings.md#nu3002) przy logowaniu się bez sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="3011c-123">The sign operation produce a [warning NU3002](../reference/Errors-and-Warnings.md#nu3002) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="3011c-124">Sprawdź podpisanego pakietu</span><span class="sxs-lookup"><span data-stu-id="3011c-124">Verify a signed package</span></span>

<span data-ttu-id="3011c-125">Użyj [nuget Sprawdź](../tools/cli-ref-verify.md) Aby wyświetlić szczegóły sygnatury danego pakietu:</span><span class="sxs-lookup"><span data-stu-id="3011c-125">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="3011c-126">Zainstaluj pakiet podpisem</span><span class="sxs-lookup"><span data-stu-id="3011c-126">Install a signed package</span></span>

<span data-ttu-id="3011c-127">Podpisanych pakietów nie wymagają żadnych określonych czynności w celu zainstalowania; Jednak jeśli zawartość została zmodyfikowana po podpisaniu, podczas instalacji będzie zablokowane i tworzy [błąd NU3008](../reference/Errors-and-Warnings.md#nu3008).</span><span class="sxs-lookup"><span data-stu-id="3011c-127">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation be blocked and produces a [error NU3008](../reference/Errors-and-Warnings.md#nu3008).</span></span>

> [!Warning]
> <span data-ttu-id="3011c-128">Uwzględniane są podpisane za pomocą certyfikatów niezaufanych pakiety jako bez znaku i są instalowane bez żadnych ostrzeżeń ani błędów, takich jak niepodpisanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="3011c-128">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="3011c-129">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="3011c-129">See also</span></span>

[<span data-ttu-id="3011c-130">Podpisana pakietów odniesienia</span><span class="sxs-lookup"><span data-stu-id="3011c-130">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
