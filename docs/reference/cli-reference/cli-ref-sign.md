---
title: Polecenie podpisywania interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia nuget.exe Sign
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 84386f1752b98688f1fd34e453f5b72ae8afdd92
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622775"
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="2a9c0-103">Sign — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="2a9c0-103">sign command (NuGet CLI)</span></span>

<span data-ttu-id="2a9c0-104">**Dotyczy:** &bullet; **obsługiwane wersje:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="2a9c0-104">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="2a9c0-105">Podpisuje wszystkie pakiety pasujące do pierwszego argumentu z certyfikatem.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-105">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="2a9c0-106">Certyfikat z kluczem prywatnym można uzyskać z pliku lub z certyfikatu zainstalowanego w magazynie certyfikatów przez podanie nazwy podmiotu lub odcisku palca.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-106">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

> [!Note]
> <span data-ttu-id="2a9c0-107">Podpisywanie pakietów nie jest jeszcze obsługiwane w programie .NET Core, w obszarze mono lub na platformach innych niż Windows.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-107">Package signing is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="2a9c0-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="2a9c0-108">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="2a9c0-109">gdzie `<package(s)>` jest co najmniej jeden `.nupkg` plik.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-109">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="2a9c0-110">Opcje</span><span class="sxs-lookup"><span data-stu-id="2a9c0-110">Options</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="2a9c0-111">Określa odcisk palca SHA-1 certyfikatu używanego do wyszukiwania certyfikatu w lokalnym magazynie certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-111">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span>

- **`-CertificatePassword`**

  <span data-ttu-id="2a9c0-112">Określa hasło certyfikatu, w razie konieczności.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-112">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="2a9c0-113">Jeśli certyfikat jest chroniony hasłem, ale nie podano hasła, polecenie wyświetli monit o podanie hasła w czasie wykonywania, chyba że `-NonInteractive` opcja zostanie przekazana.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-113">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the `-NonInteractive` option is passed.</span></span>

- **`-CertificatePath`**

  <span data-ttu-id="2a9c0-114">Określa ścieżkę pliku do certyfikatu, który ma być używany podczas podpisywania pakietu.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-114">Specifies the file path to the certificate to be used in signing the package.</span></span>

- **`-CertificateStoreLocation`**

  <span data-ttu-id="2a9c0-115">Określa nazwę magazynu certyfikatów X. 509 używanego do wyszukiwania certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-115">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="2a9c0-116">Wartość domyślna to "CurrentUser", magazyn certyfikatów X. 509 używany przez bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-116">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="2a9c0-117">Ta opcja powinna być używana podczas określania certyfikatu za pośrednictwem `-CertificateSubjectName` `-CertificateFingerprint` opcji lub.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-117">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateStoreName`**

  <span data-ttu-id="2a9c0-118">Określa nazwę magazynu certyfikatów X. 509 do użycia w celu wyszukania certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-118">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="2a9c0-119">Wartość domyślna to "my", czyli magazyn certyfikatów X. 509 dla certyfikatów osobistych.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-119">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="2a9c0-120">Ta opcja powinna być używana podczas określania certyfikatu za pośrednictwem `-CertificateSubjectName` `-CertificateFingerprint` opcji lub.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-120">This option should be used when specifying the certificate via `-CertificateSubjectName` or `-CertificateFingerprint` options.</span></span>

- **`-CertificateSubjectName`**

  <span data-ttu-id="2a9c0-121">Określa nazwę podmiotu certyfikatu używanego do wyszukiwania certyfikatu w lokalnym magazynie certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-121">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="2a9c0-122">Wyszukiwanie to porównanie ciągów bez uwzględniania wielkości liter przy użyciu podanej wartości, która będzie znajdować wszystkie certyfikaty z nazwą podmiotu zawierającą ten ciąg, niezależnie od innych wartości podmiotu.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-122">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="2a9c0-123">Magazyn certyfikatów można określić za pomocą `-CertificateStoreName` opcji i `-CertificateStoreLocation` .</span><span class="sxs-lookup"><span data-stu-id="2a9c0-123">The certificate store can be specified by `-CertificateStoreName` and `-CertificateStoreLocation` options.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="2a9c0-124">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2a9c0-125">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="2a9c0-126">Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-126">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-HashAlgorithm`**

  <span data-ttu-id="2a9c0-127">Algorytm wyznaczania wartości skrótu, który ma być używany do podpisywania pakietu.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-127">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="2a9c0-128">Wartość domyślna to SHA256.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-128">Defaults to SHA256.</span></span> <span data-ttu-id="2a9c0-129">Możliwe wartości to SHA256, SHA384 i SHA512.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-129">Possible values are SHA256, SHA384, and SHA512.</span></span>

- **`-?|-help`**

  <span data-ttu-id="2a9c0-130">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-130">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="2a9c0-131">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-131">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="2a9c0-132">Określa katalog, w którym ma zostać zapisany podpisany pakiet.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-132">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="2a9c0-133">Domyślnie oryginalny pakiet jest zastępowany przez podpisany pakiet.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-133">By default the original package is overwritten by the signed package.</span></span>

- **`-Overwrite`**

  <span data-ttu-id="2a9c0-134">Przełącz, aby wskazać, czy bieżący podpis powinien zostać nadpisany.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-134">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="2a9c0-135">Domyślnie polecenie zakończy się niepowodzeniem, jeśli pakiet ma już podpis.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-135">By default the command will fail if the package already has a signature.</span></span>

- **`-Timestamper`**

  <span data-ttu-id="2a9c0-136">Adres URL do serwera znacznika czasu RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-136">URL to an RFC 3161 timestamping server.</span></span>

- **`-TimestampHashAlgorithm`**

  <span data-ttu-id="2a9c0-137">Algorytm wyznaczania wartości skrótu, który ma być używany przez serwer znacznika czasu RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-137">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="2a9c0-138">Wartość domyślna to SHA256.</span><span class="sxs-lookup"><span data-stu-id="2a9c0-138">Defaults to SHA256.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="2a9c0-139">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="2a9c0-139">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="2a9c0-140">Przykłady</span><span class="sxs-lookup"><span data-stu-id="2a9c0-140">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -CertificatePath .\..\certificate.pfx -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -CertificateStoreLocation CurrentUser -CertificateStoreName My -CertificateSubjectName 'subject name' -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```
