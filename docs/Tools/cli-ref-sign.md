---
title: Polecenie logowania interfejsu wiersza polecenia NuGet | Dokumentacja firmy Microsoft
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Informacje dotyczące polecenia znak nuget.exe
keywords: Odwołanie do logowania nuget, polecenie logowania
ms.reviewer:
- karann
- rmpablos
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9c83e5abae0e70cdc62917861c1febfce4f792c7
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="sign-command-nuget-cli"></a><span data-ttu-id="2a9e2-104">znak polecenia (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2a9e2-104">sign command (NuGet CLI)</span></span>

<span data-ttu-id="2a9e2-105">**Dotyczy:** pakietu tworzenia &bullet; **obsługiwane wersje:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="2a9e2-105">**Applies to:** package creation &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="2a9e2-106">Rejestruje wszystkie pakiety dopasowania pierwszy argument przy użyciu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-106">Signs all the packages matching the first argument with a certificate.</span></span> <span data-ttu-id="2a9e2-107">Z plikiem lub zainstalowanego w magazynie certyfikatów, podając nazwę podmiotu i odcisk palca certyfikatu można uzyskać certyfikatu z kluczem prywatnym.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-107">The certificate with the private key can be obtained from a file or from a certificate installed in a certificate store by providing a subject name or a thumbprint.</span></span>

<span data-ttu-id="2a9e2-108">Podpisywanie pakietu nie jest jeszcze obsługiwana w obszarze Mono lub na różnych platformach z systemem innym niż Windows.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-108">Package signing is not yet supported under Mono or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="2a9e2-109">Użycie</span><span class="sxs-lookup"><span data-stu-id="2a9e2-109">Usage</span></span>

```cli
nuget sign <package(s)> [options]
```

<span data-ttu-id="2a9e2-110">gdzie `<package(s)>` jest co najmniej jeden `.nupkg` plików.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-110">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="2a9e2-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="2a9e2-111">Options</span></span>

| <span data-ttu-id="2a9e2-112">Opcja</span><span class="sxs-lookup"><span data-stu-id="2a9e2-112">Option</span></span> | <span data-ttu-id="2a9e2-113">Opis</span><span class="sxs-lookup"><span data-stu-id="2a9e2-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a9e2-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="2a9e2-114">CertificateFingerprint</span></span> | <span data-ttu-id="2a9e2-115">Określa algorytm SHA-1 odcisk palca certyfikatu używanego do wyszukiwania lokalnego magazynu certyfikatów dla certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-115">Specifies the SHA-1 fingerprint of the certificate used to search a local certificate store for the certificate.</span></span> |
| <span data-ttu-id="2a9e2-116">CertificatePassword</span><span class="sxs-lookup"><span data-stu-id="2a9e2-116">CertificatePassword</span></span> | <span data-ttu-id="2a9e2-117">Określa hasło certyfikatu, jeśli to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-117">Specifies the certificate password, if needed.</span></span> <span data-ttu-id="2a9e2-118">Jeśli certyfikat jest chroniony hasłem, ale hasło nie jest dostępne, polecenie będzie monitować o hasło w czasie wykonywania, chyba że opcja nieinterakcyjnego jest przekazywana.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-118">If a certificate is password protected but no password is provided, the command will prompt for a password at run time, unless the -NonInteractive option is passed.</span></span> |
| <span data-ttu-id="2a9e2-119">CertificatePath</span><span class="sxs-lookup"><span data-stu-id="2a9e2-119">CertificatePath</span></span> | <span data-ttu-id="2a9e2-120">Określa ścieżkę do certyfikatu, który ma być używana podczas podpisywania pakietu.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-120">Specifies the file path to the certificate to be used in signing the package.</span></span> |
| <span data-ttu-id="2a9e2-121">CertificateStoreLocation</span><span class="sxs-lookup"><span data-stu-id="2a9e2-121">CertificateStoreLocation</span></span> | <span data-ttu-id="2a9e2-122">Określa nazwę Użyj magazynu certyfikatu X.509 do wyszukiwania certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-122">Specifies the name of the X.509 certificate store use to search for the certificate.</span></span> <span data-ttu-id="2a9e2-123">Wartość domyślna to "CurrentUser" magazynu certyfikatu X.509, używanego przez bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-123">Defaults to "CurrentUser", the X.509 certificate store used by the current user.</span></span> <span data-ttu-id="2a9e2-124">Tej opcji należy używać podczas określania certyfikatu przy użyciu opcji - CertificateSubjectName lub - CertificateFingerprint.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-124">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="2a9e2-125">CertificateStoreName</span><span class="sxs-lookup"><span data-stu-id="2a9e2-125">CertificateStoreName</span></span> | <span data-ttu-id="2a9e2-126">Określa nazwę magazynu certyfikatu X.509 do służy do wyszukiwania certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-126">Specifies the name of the X.509 certificate store to use to search for the certificate.</span></span> <span data-ttu-id="2a9e2-127">Wartość domyślna to "My", X.509 magazynu certyfikatów osobistych.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-127">Defaults to "My", the X.509 certificate store for personal certificates.</span></span> <span data-ttu-id="2a9e2-128">Tej opcji należy używać podczas określania certyfikatu przy użyciu opcji - CertificateSubjectName lub - CertificateFingerprint.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-128">This option should be used when specifying the certificate via -CertificateSubjectName or -CertificateFingerprint options.</span></span> |
| <span data-ttu-id="2a9e2-129">CertificateSubjectName</span><span class="sxs-lookup"><span data-stu-id="2a9e2-129">CertificateSubjectName</span></span> | <span data-ttu-id="2a9e2-130">Określa nazwę podmiotu certyfikatu używanego do wyszukiwania lokalnego magazynu certyfikatów dla certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-130">Specifies the subject name of the certificate used to search a local certificate store for the certificate.</span></span>  <span data-ttu-id="2a9e2-131">Wyszukiwanie jest porównania bez uwzględniania wielkości liter ciągów za pomocą podana wartość, która znajdzie wszystkie certyfikaty z nazwą podmiotu, zawierającą ten ciąg, niezależnie od innych wartości podmiotu.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-131">The search is a case-insensitive string comparison using the supplied value, which will find all certificates with the subject name containing that string, regardless of other subject values.</span></span>  <span data-ttu-id="2a9e2-132">Magazyn certyfikatów można określić opcji - CertificateStoreName i - CertificateStoreLocation.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-132">The certificate store can be specified by -CertificateStoreName and -CertificateStoreLocation options.</span></span> |
| <span data-ttu-id="2a9e2-133">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2a9e2-133">ConfigFile</span></span> | <span data-ttu-id="2a9e2-134">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-134">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2a9e2-135">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-135">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2a9e2-136">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2a9e2-136">ForceEnglishOutput</span></span> | <span data-ttu-id="2a9e2-137">Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-137">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2a9e2-138">HashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="2a9e2-138">HashAlgorithm</span></span> | <span data-ttu-id="2a9e2-139">Algorytm wyznaczania wartości skrótu, który ma być używany do podpisywania pakietu.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-139">Hash algorithm to be used to sign the package.</span></span> <span data-ttu-id="2a9e2-140">Wartość domyślna to SHA256.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-140">Defaults to SHA256.</span></span> |
| <span data-ttu-id="2a9e2-141">Pomoc</span><span class="sxs-lookup"><span data-stu-id="2a9e2-141">Help</span></span> | <span data-ttu-id="2a9e2-142">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-142">Displays help information for the command.</span></span> |
| <span data-ttu-id="2a9e2-143">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="2a9e2-143">NonInteractive</span></span> | <span data-ttu-id="2a9e2-144">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2a9e2-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="2a9e2-145">OutputDirectory</span></span> | <span data-ttu-id="2a9e2-146">Określa katalog, w którym ma zostać zapisany pakiet podpisem.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-146">Specifies the directory where the signed package should be saved.</span></span> <span data-ttu-id="2a9e2-147">Domyślnie oryginalnego pakietu jest zastępowany przez pakiet podpisem.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-147">By default the original package is overwritten by the signed package.</span></span> |
| <span data-ttu-id="2a9e2-148">Zastąp</span><span class="sxs-lookup"><span data-stu-id="2a9e2-148">Overwrite</span></span> | <span data-ttu-id="2a9e2-149">Przełącz, aby wskazać, jeśli można zastąpić bieżący podpisu.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-149">Switch to indicate if the current signature should be overwritten.</span></span> <span data-ttu-id="2a9e2-150">Domyślnie polecenia zakończy się niepowodzeniem, jeśli pakiet zawiera już podpisu.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-150">By default the command will fail if the package already has a signature.</span></span> |
| <span data-ttu-id="2a9e2-151">Timestamper</span><span class="sxs-lookup"><span data-stu-id="2a9e2-151">Timestamper</span></span> | <span data-ttu-id="2a9e2-152">Adres URL serwera sygnatur RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-152">URL to an RFC 3161 timestamping server.</span></span> |
| <span data-ttu-id="2a9e2-153">TimestampHashAlgorithm</span><span class="sxs-lookup"><span data-stu-id="2a9e2-153">TimestampHashAlgorithm</span></span> | <span data-ttu-id="2a9e2-154">Algorytm wyznaczania wartości skrótu używanego przez serwer znaczników czasu RFC 3161.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-154">Hash algorithm to be used by the RFC 3161 timestamp server.</span></span> <span data-ttu-id="2a9e2-155">Wartość domyślna to SHA256.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-155">Defaults to SHA256.</span></span> |
| <span data-ttu-id="2a9e2-156">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="2a9e2-156">Verbosity</span></span> | <span data-ttu-id="2a9e2-157">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="2a9e2-157">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="2a9e2-158">Przykłady</span><span class="sxs-lookup"><span data-stu-id="2a9e2-158">Examples</span></span>

```cli
nuget sign MyPackage.nupkg -Timestamper http://timestamp.test

nuget sign .\..\MyPackage.nupkg -Timestamper http://timestamp.test -OutputDirectory .\..\Signed
```