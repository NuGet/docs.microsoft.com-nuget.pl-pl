---
title: Podpisywanie pakietów NuGet
description: Wyjaśnia, jak podpisanych pakietów może służyć do włączyć weryfikację zawartości integralności.
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 0679b60179760d6626e7ce42bfdbdfa266677ce6
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793564"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="1f47d-103">Podpisywanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="1f47d-103">Signing NuGet Packages</span></span>

<span data-ttu-id="1f47d-104">Podpisywanie pakietu jest procesem, który sprawia, że pakiet nie został zmodyfikowany od czasu jego utworzenia.</span><span class="sxs-lookup"><span data-stu-id="1f47d-104">Signing a package is a process that makes sure the package has not been modified since its creation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f47d-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1f47d-105">Prerequisites</span></span>

1. <span data-ttu-id="1f47d-106">Pakiet ( `.nupkg` plików) do podpisywania.</span><span class="sxs-lookup"><span data-stu-id="1f47d-106">The package (a `.nupkg` file) to sign.</span></span> <span data-ttu-id="1f47d-107">Zobacz [Tworzenie pakietu](creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="1f47d-107">See [Creating a package](creating-a-package.md).</span></span>

1. <span data-ttu-id="1f47d-108">nuget.exe 4.6.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1f47d-108">nuget.exe 4.6.0 or later.</span></span> <span data-ttu-id="1f47d-109">Zobacz jak [zainstalować interfejs wiersza polecenia NuGet](../install-nuget-client-tools.md#nugetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="1f47d-109">See how to [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span>

1. <span data-ttu-id="1f47d-110">[Certyfikat podpisywania kodu](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span><span class="sxs-lookup"><span data-stu-id="1f47d-110">[A code signing certificate](../reference/signed-packages-reference.md#get-a-code-signing-certificate).</span></span>

## <a name="sign-a-package"></a><span data-ttu-id="1f47d-111">Podpisywanie pakietu</span><span class="sxs-lookup"><span data-stu-id="1f47d-111">Sign a package</span></span>

<span data-ttu-id="1f47d-112">Aby zarejestrować pakiet, należy użyć [logowania nuget](../tools/cli-ref-sign.md):</span><span class="sxs-lookup"><span data-stu-id="1f47d-112">To sign a package, use [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateSubjectName <MyCertSubjectName> -Timestamper <TimestampServiceURL>
```

<span data-ttu-id="1f47d-113">Zgodnie z opisem w dokumentacji poleceń, można użyć certyfikatu jest dostępny w magazynie certyfikatów lub używany certyfikat z pliku.</span><span class="sxs-lookup"><span data-stu-id="1f47d-113">As described in the command reference, you can use a certificate available in the certificate store or use a certificate from a file.</span></span>

### <a name="common-problems-when-signing-a-package"></a><span data-ttu-id="1f47d-114">Typowe problemy podczas podpisywania pakietu</span><span class="sxs-lookup"><span data-stu-id="1f47d-114">Common problems when signing a package</span></span>

- <span data-ttu-id="1f47d-115">Certyfikat nie jest prawidłowy do podpisywania kodu.</span><span class="sxs-lookup"><span data-stu-id="1f47d-115">The certificate is not valid for code signing.</span></span> <span data-ttu-id="1f47d-116">Upewnij się, że określony certyfikat ma odpowiednią rozszerzone użycie klucza (EKU 1.3.6.1.5.5.7.3.3).</span><span class="sxs-lookup"><span data-stu-id="1f47d-116">You must ensure the certificate specified has the appropriate extended key usage (EKU 1.3.6.1.5.5.7.3.3).</span></span>
- <span data-ttu-id="1f47d-117">Certyfikat nie spełnia wymagania podstawowe, takie jak algorytm podpisu RSA, SHA-256 lub publicznej klucza 2048 bitów lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1f47d-117">The certificate does not satisfy the basic requirements such as the RSA SHA-256 signature algorithm or a public key 2048 bits or greater.</span></span>
- <span data-ttu-id="1f47d-118">Certyfikat wygasł lub został odwołany.</span><span class="sxs-lookup"><span data-stu-id="1f47d-118">The certificate has expired or has been revoked.</span></span>
- <span data-ttu-id="1f47d-119">Serwera znacznika czasowego nie spełnia wymagań dotyczących certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="1f47d-119">The timestamp server does not satisfy the certificate requirements.</span></span>

> [!Note]
> <span data-ttu-id="1f47d-120">Podpisanych pakietów powinien zawierać sygnaturę czasową, aby upewnić się, że podpis pozostaje ważny, gdy wygasł certyfikat podpisywania.</span><span class="sxs-lookup"><span data-stu-id="1f47d-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="1f47d-121">Generuje operacji logowania [ostrzeżenie NU3002](../reference/errors-and-warnings/NU3002.md) podczas logowania się bez sygnatury czasowej.</span><span class="sxs-lookup"><span data-stu-id="1f47d-121">The sign operation produce a [warning NU3002](../reference/errors-and-warnings/NU3002.md) when signing without a timestamp.</span></span>

## <a name="verify-a-signed-package"></a><span data-ttu-id="1f47d-122">Sprawdź podpisanych pakietów</span><span class="sxs-lookup"><span data-stu-id="1f47d-122">Verify a signed package</span></span>

<span data-ttu-id="1f47d-123">Użyj [Sprawdź nuget](../tools/cli-ref-verify.md) szczegóły podpisu danego pakietu:</span><span class="sxs-lookup"><span data-stu-id="1f47d-123">Use [nuget verify](../tools/cli-ref-verify.md) to see the signature details of a given package:</span></span>

```cli
nuget verify -signature MyPackage.nupkg
```

## <a name="install-a-signed-package"></a><span data-ttu-id="1f47d-124">Zainstaluj pakiet podpisem</span><span class="sxs-lookup"><span data-stu-id="1f47d-124">Install a signed package</span></span>

<span data-ttu-id="1f47d-125">Podpisanych pakietów nie wymagają żadnych określone działanie prowadzące do zainstalowania; Jeśli jednak zawartość została zmodyfikowana po podpisaniu, instalacja jest zablokowana i tworzy [błąd NU3008](../reference/errors-and-warnings/NU3008.md).</span><span class="sxs-lookup"><span data-stu-id="1f47d-125">Signed packages don't require any specific action to be installed; however, if the content has been modified since it was signed, the installation is blocked and produces an [error NU3008](../reference/errors-and-warnings/NU3008.md).</span></span>

> [!Warning]
> <span data-ttu-id="1f47d-126">Pakiety podpisany przy użyciu niezaufane certyfikaty są traktowane jako jako bez znaku i są instalowane bez żadnych ostrzeżeń ani błędów, takich jak każdy inny pakiet bez znaku.</span><span class="sxs-lookup"><span data-stu-id="1f47d-126">Packages signed with untrusted certificates are considered as unsigned and are installed without any warnings or errors like any other unsigned package.</span></span>

## <a name="see-also"></a><span data-ttu-id="1f47d-127">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="1f47d-127">See also</span></span>

[<span data-ttu-id="1f47d-128">Dokumentacja podpisanych pakietów</span><span class="sxs-lookup"><span data-stu-id="1f47d-128">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
