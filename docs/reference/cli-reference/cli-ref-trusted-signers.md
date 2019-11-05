---
title: Polecenie zaufanych-podpisywania interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia Trusted-signers programu NuGet. exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 94c4c6524c1870898893b80be914477af5a14e8b
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610334"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="0af9d-103">Zaufane-podpisujące — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="0af9d-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="0af9d-104">**Dotyczy:** użycie pakietu &bullet; **obsługiwane wersje:** 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="0af9d-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="0af9d-105">Pobiera lub ustawia zaufane osoby podpisujące do konfiguracji programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="0af9d-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="0af9d-106">Aby uzyskać dodatkowe użycie, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="0af9d-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="0af9d-107">Aby uzyskać szczegółowe informacje o tym, jak wygląda schemat NuGet. config, zapoznaj się z tematem [Dokumentacja pliku konfiguracji programu NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="0af9d-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="0af9d-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="0af9d-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="0af9d-109">Jeśli żadna z `list|add|remove|sync` nie zostanie określona, polecenie będzie domyślnie `list`.</span><span class="sxs-lookup"><span data-stu-id="0af9d-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="0af9d-110">Lista zaufanych nadawców NuGet</span><span class="sxs-lookup"><span data-stu-id="0af9d-110">nuget trusted-signers list</span></span>

<span data-ttu-id="0af9d-111">Wyświetla listę wszystkich zaufanych podpisów w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0af9d-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="0af9d-112">Ta opcja spowoduje uwzględnienie wszystkich certyfikatów (z użyciem algorytmu odcisku palca i odcisku palca) każdego osoby podpisującej.</span><span class="sxs-lookup"><span data-stu-id="0af9d-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="0af9d-113">Jeśli certyfikat ma wcześniejszą `[U]`, oznacza to, że wpis certyfikatu ma `allowUntrustedRoot` ustawiony jako `true`.</span><span class="sxs-lookup"><span data-stu-id="0af9d-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="0af9d-114">Poniżej znajduje się przykładowe dane wyjściowe z tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0af9d-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="0af9d-115">zaufane osoby podpisujące NuGet — Dodawanie [opcje]</span><span class="sxs-lookup"><span data-stu-id="0af9d-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="0af9d-116">Dodaje do konfiguracji nazwę zaufanego podpisującego o danej nazwie. Ta opcja ma inne gesty umożliwiające dodanie zaufanego autora lub repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0af9d-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="0af9d-117">Opcje dodawania w oparciu o pakiet</span><span class="sxs-lookup"><span data-stu-id="0af9d-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="0af9d-118">gdzie `<package(s)>` to co najmniej jeden plik `.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="0af9d-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="0af9d-119">Opcja</span><span class="sxs-lookup"><span data-stu-id="0af9d-119">Option</span></span> | <span data-ttu-id="0af9d-120">Opis</span><span class="sxs-lookup"><span data-stu-id="0af9d-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0af9d-121">Tworzone</span><span class="sxs-lookup"><span data-stu-id="0af9d-121">Author</span></span> | <span data-ttu-id="0af9d-122">Określa, że podpis autora pakietów powinien być zaufany.</span><span class="sxs-lookup"><span data-stu-id="0af9d-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="0af9d-123">Kopie</span><span class="sxs-lookup"><span data-stu-id="0af9d-123">Repository</span></span> | <span data-ttu-id="0af9d-124">Określa, że podpis repozytorium lub kontrpodpis pakietów powinien być zaufany.</span><span class="sxs-lookup"><span data-stu-id="0af9d-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="0af9d-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="0af9d-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="0af9d-126">Określa, czy certyfikat zaufanego podpisującego ma być dozwolony w łańcuchu do niezaufanego certyfikatu głównego.</span><span class="sxs-lookup"><span data-stu-id="0af9d-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="0af9d-127">rzecz</span><span class="sxs-lookup"><span data-stu-id="0af9d-127">Owners</span></span> | <span data-ttu-id="0af9d-128">Rozdzielana średnikami lista zaufanych właścicieli, aby bardziej ograniczyć zaufanie do repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0af9d-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="0af9d-129">Prawidłowy tylko przy użyciu opcji `-Repository`.</span><span class="sxs-lookup"><span data-stu-id="0af9d-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="0af9d-130">Udostępnianie jednocześnie `-Author` i `-Repository` nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="0af9d-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="0af9d-131">Opcje dodawania oparte na indeksie usługi</span><span class="sxs-lookup"><span data-stu-id="0af9d-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="0af9d-132">_Uwaga_: Ta opcja spowoduje dodanie tylko zaufanych repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="0af9d-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="0af9d-133">Opcja</span><span class="sxs-lookup"><span data-stu-id="0af9d-133">Option</span></span> | <span data-ttu-id="0af9d-134">Opis</span><span class="sxs-lookup"><span data-stu-id="0af9d-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0af9d-135">Serviceindex</span><span class="sxs-lookup"><span data-stu-id="0af9d-135">ServiceIndex</span></span> | <span data-ttu-id="0af9d-136">Określa indeks usługi v3 repozytorium, który ma być zaufany.</span><span class="sxs-lookup"><span data-stu-id="0af9d-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="0af9d-137">To repozytorium ma obsługiwać zasób sygnatur repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0af9d-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="0af9d-138">Jeśli nie zostanie podany, polecenie będzie szukać źródła pakietu o tej samej `-Name` i pobrać z niego indeks usługi.</span><span class="sxs-lookup"><span data-stu-id="0af9d-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="0af9d-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="0af9d-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="0af9d-140">Określa, czy certyfikat zaufanego podpisującego ma być dozwolony w łańcuchu do niezaufanego certyfikatu głównego.</span><span class="sxs-lookup"><span data-stu-id="0af9d-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="0af9d-141">rzecz</span><span class="sxs-lookup"><span data-stu-id="0af9d-141">Owners</span></span> | <span data-ttu-id="0af9d-142">Rozdzielana średnikami lista zaufanych właścicieli, aby bardziej ograniczyć zaufanie do repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0af9d-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="0af9d-143">Opcje dodawania na podstawie informacji o certyfikacie</span><span class="sxs-lookup"><span data-stu-id="0af9d-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="0af9d-144">_Uwaga_: Jeśli zaufany podpis o podanej nazwie już istnieje, element certyfikatu zostanie dodany do osoby podpisującej.</span><span class="sxs-lookup"><span data-stu-id="0af9d-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="0af9d-145">W przeciwnym razie zaufany autor zostanie utworzony za pomocą elementu certyfikatu z informacji podanych w certyfikacie.</span><span class="sxs-lookup"><span data-stu-id="0af9d-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="0af9d-146">Opcja</span><span class="sxs-lookup"><span data-stu-id="0af9d-146">Option</span></span> | <span data-ttu-id="0af9d-147">Opis</span><span class="sxs-lookup"><span data-stu-id="0af9d-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0af9d-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="0af9d-148">CertificateFingerprint</span></span> | <span data-ttu-id="0af9d-149">Określa odciski palca certyfikatu, z którym podpisane pakiety muszą być podpisane.</span><span class="sxs-lookup"><span data-stu-id="0af9d-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="0af9d-150">Odcisk palca certyfikatu jest skrótem certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0af9d-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="0af9d-151">Algorytm wyznaczania wartości skrótu używany do obliczania tego skrótu powinien być określany w opcji `FingerprintAlgorithm`.</span><span class="sxs-lookup"><span data-stu-id="0af9d-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="0af9d-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="0af9d-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="0af9d-153">Określa algorytm wyznaczania wartości skrótu używany do obliczania odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0af9d-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="0af9d-154">Wartość domyślna to `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="0af9d-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="0af9d-155">Obsługiwane wartości to `SHA256`, `SHA384` i `SHA512`</span><span class="sxs-lookup"><span data-stu-id="0af9d-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="0af9d-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="0af9d-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="0af9d-157">Określa, czy certyfikat zaufanego podpisującego ma być dozwolony w łańcuchu do niezaufanego certyfikatu głównego.</span><span class="sxs-lookup"><span data-stu-id="0af9d-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="0af9d-158">zaufane osoby podpisujące NuGet usuwają nazwę \<nazwy\></span><span class="sxs-lookup"><span data-stu-id="0af9d-158">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="0af9d-159">Usuwa wszystkie zaufane osoby podpisujące zgodne z podaną nazwą.</span><span class="sxs-lookup"><span data-stu-id="0af9d-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="0af9d-160">Synchronizacja zaufanych nadawców NuGet — nazwa \<nazwa\></span><span class="sxs-lookup"><span data-stu-id="0af9d-160">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="0af9d-161">Żąda najnowszej listy certyfikatów używanych w bieżącym repozytorium, aby zaktualizować listę istniejących certyfikatów w zaufanej rejestracji.</span><span class="sxs-lookup"><span data-stu-id="0af9d-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="0af9d-162">_Uwaga_: ten gest spowoduje usunięcie bieżącej listy certyfikatów i zamienienie ich na aktualną listę z repozytorium.</span><span class="sxs-lookup"><span data-stu-id="0af9d-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="0af9d-163">Opcje</span><span class="sxs-lookup"><span data-stu-id="0af9d-163">Options</span></span>

| <span data-ttu-id="0af9d-164">Opcja</span><span class="sxs-lookup"><span data-stu-id="0af9d-164">Option</span></span> | <span data-ttu-id="0af9d-165">Opis</span><span class="sxs-lookup"><span data-stu-id="0af9d-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0af9d-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0af9d-166">ConfigFile</span></span> | <span data-ttu-id="0af9d-167">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="0af9d-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="0af9d-168">Jeśli nie zostanie określony, używany jest `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="0af9d-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="0af9d-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0af9d-169">ForceEnglishOutput</span></span> | <span data-ttu-id="0af9d-170">Wymusza uruchomienie NuGet. exe przy użyciu niezmiennej, opartej na języku angielskim kultury.</span><span class="sxs-lookup"><span data-stu-id="0af9d-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0af9d-171">Pomoc</span><span class="sxs-lookup"><span data-stu-id="0af9d-171">Help</span></span> | <span data-ttu-id="0af9d-172">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="0af9d-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="0af9d-173">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="0af9d-173">Verbosity</span></span> | <span data-ttu-id="0af9d-174">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="0af9d-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="0af9d-175">Przykłady</span><span class="sxs-lookup"><span data-stu-id="0af9d-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
