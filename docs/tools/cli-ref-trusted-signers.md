---
title: Polecenie zaufane osoby podpisujące interfejs wiersza polecenia NuGet
description: Dokumentacja dotycząca poleceń zaufane osoby podpisujące nuget.exe
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: ee4ffaa7e250cdbf313476fd794a8d87c80b69f9
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324711"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="45867-103">polecenie zaufane osoby podpisujące (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="45867-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="45867-104">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="45867-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="45867-105">Pobiera lub ustawia zaufane osoby podpisujące konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="45867-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="45867-106">Aby uzyskać dodatkowe użycie, zobacz [Konfigurowanie zachowania pakietu NuGet](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="45867-106">For additional usage, see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="45867-107">Aby uzyskać szczegółowe informacje na temat sposobu schematu pliku nuget.config wygląda na to, zapoznaj się [odwołanie do pliku config NuGet](../reference/nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="45867-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../reference/nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="45867-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="45867-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="45867-109">Jeśli żadna z `list|add|remove|sync` jest określony, domyślnie zostanie polecenie `list`.</span><span class="sxs-lookup"><span data-stu-id="45867-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="45867-110">Lista zaufanych które podpisały nuget</span><span class="sxs-lookup"><span data-stu-id="45867-110">nuget trusted-signers list</span></span>

<span data-ttu-id="45867-111">Wyświetla listę wszystkich zaufanych które podpisały w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="45867-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="45867-112">Ta opcja będzie obejmować wszystkie certyfikaty (przy użyciu linii papilarnych i Algorytm odcisku palca) została każda osoby podpisującej.</span><span class="sxs-lookup"><span data-stu-id="45867-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="45867-113">Jeśli certyfikat ma poprzedzających `[U]`, oznacza to, że wpis certyfikat ma `allowUntrustedRoot` ustawiony jako `true`.</span><span class="sxs-lookup"><span data-stu-id="45867-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="45867-114">Poniżej przedstawiono przykładowe dane wyjściowe tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="45867-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="45867-115">nuget zaufanych — które podpisały Dodaj [opcje]</span><span class="sxs-lookup"><span data-stu-id="45867-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="45867-116">Dodaje zaufane osoby podpisującej o podanej nazwie do konfiguracji. Ta opcja ma różne gestów, można dodać zaufany autora lub repozytorium.</span><span class="sxs-lookup"><span data-stu-id="45867-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="45867-117">Opcje oparte na pakiecie Dodaj</span><span class="sxs-lookup"><span data-stu-id="45867-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="45867-118">gdzie `<package(s)>` ma jeden lub więcej `.nupkg` plików.</span><span class="sxs-lookup"><span data-stu-id="45867-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

| <span data-ttu-id="45867-119">Opcja</span><span class="sxs-lookup"><span data-stu-id="45867-119">Option</span></span> | <span data-ttu-id="45867-120">Opis</span><span class="sxs-lookup"><span data-stu-id="45867-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="45867-121">Autor</span><span class="sxs-lookup"><span data-stu-id="45867-121">Author</span></span> | <span data-ttu-id="45867-122">Określa podpis Autor pakietów należy ufać.</span><span class="sxs-lookup"><span data-stu-id="45867-122">Specifies that the author signature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="45867-123">Repozytorium</span><span class="sxs-lookup"><span data-stu-id="45867-123">Repository</span></span> | <span data-ttu-id="45867-124">Określa, że podpis repozytorium lub dokonanym pakiety mają być zaufane.</span><span class="sxs-lookup"><span data-stu-id="45867-124">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span> |
| <span data-ttu-id="45867-125">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="45867-125">AllowUntrustedRoot</span></span> | <span data-ttu-id="45867-126">Określa, jeśli certyfikat dla zaufanych osoby podpisującej powinien być dozwolony do tworzenia łańcucha niezaufany certyfikat główny.</span><span class="sxs-lookup"><span data-stu-id="45867-126">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="45867-127">Właściciele</span><span class="sxs-lookup"><span data-stu-id="45867-127">Owners</span></span> | <span data-ttu-id="45867-128">Rozdzielana średnikami lista zaufanych właścicieli, aby bardziej ograniczyć zaufanie do repozytorium.</span><span class="sxs-lookup"><span data-stu-id="45867-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="45867-129">Prawidłowa tylko w przypadku korzystania z `-Repository` opcji.</span><span class="sxs-lookup"><span data-stu-id="45867-129">Only valid when using the `-Repository` option.</span></span> |

<span data-ttu-id="45867-130">Podanie zarówno `-Author` i `-Repository` nie jest obsługiwany w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="45867-130">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="45867-131">Opcje przeznaczony do dodania, w oparciu o indeks usług</span><span class="sxs-lookup"><span data-stu-id="45867-131">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="45867-132">_Uwaga_: Ta opcja doda tylko zaufane repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="45867-132">_Note_: This option will only add trusted repositories.</span></span> 

| <span data-ttu-id="45867-133">Opcja</span><span class="sxs-lookup"><span data-stu-id="45867-133">Option</span></span> | <span data-ttu-id="45867-134">Opis</span><span class="sxs-lookup"><span data-stu-id="45867-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="45867-135">ServiceIndex</span><span class="sxs-lookup"><span data-stu-id="45867-135">ServiceIndex</span></span> | <span data-ttu-id="45867-136">Określa indeks usługi V3 repozytorium jako zaufane.</span><span class="sxs-lookup"><span data-stu-id="45867-136">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="45867-137">To repozytorium musi obsługiwać zasób podpisów repozytorium.</span><span class="sxs-lookup"><span data-stu-id="45867-137">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="45867-138">Jeśli nie zostanie podana, polecenie będzie szukać źródło pakietu z takimi samymi `-Name` i uzyskać indeks usług, w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="45867-138">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span> |
| <span data-ttu-id="45867-139">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="45867-139">AllowUntrustedRoot</span></span> | <span data-ttu-id="45867-140">Określa, jeśli certyfikat dla zaufanych osoby podpisującej powinien być dozwolony do tworzenia łańcucha niezaufany certyfikat główny.</span><span class="sxs-lookup"><span data-stu-id="45867-140">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |
| <span data-ttu-id="45867-141">Właściciele</span><span class="sxs-lookup"><span data-stu-id="45867-141">Owners</span></span> | <span data-ttu-id="45867-142">Rozdzielana średnikami lista zaufanych właścicieli, aby bardziej ograniczyć zaufanie do repozytorium.</span><span class="sxs-lookup"><span data-stu-id="45867-142">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> |

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="45867-143">Opcje przeznaczony do dodania, w oparciu o informacje o certyfikacie</span><span class="sxs-lookup"><span data-stu-id="45867-143">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="45867-144">_Uwaga_: Jeśli zaufane osoby podpisującej o podanej nazwie już istnieje, elementu certyfikatu zostanie dodany do tej osoby podpisującej.</span><span class="sxs-lookup"><span data-stu-id="45867-144">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="45867-145">W przeciwnym razie zostanie utworzony zaufanych autor elementu certyfikatu z podanych informacji o certyfikacie.</span><span class="sxs-lookup"><span data-stu-id="45867-145">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>

| <span data-ttu-id="45867-146">Opcja</span><span class="sxs-lookup"><span data-stu-id="45867-146">Option</span></span> | <span data-ttu-id="45867-147">Opis</span><span class="sxs-lookup"><span data-stu-id="45867-147">Description</span></span> |
| --- | --- |
| <span data-ttu-id="45867-148">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="45867-148">CertificateFingerprint</span></span> | <span data-ttu-id="45867-149">Określa certyfikat, który musi być podpisany odciski palców certyfikatu, który podpisał pakietów.</span><span class="sxs-lookup"><span data-stu-id="45867-149">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="45867-150">Odcisk palca certyfikatu jest skrót certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="45867-150">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="45867-151">Określa algorytm wyznaczania wartości skrótu służące do obliczania, ten skrót powinien być `FingerprintAlgorithm` opcji.</span><span class="sxs-lookup"><span data-stu-id="45867-151">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span> |
| <span data-ttu-id="45867-152">FingerprintAlgorithm</span><span class="sxs-lookup"><span data-stu-id="45867-152">FingerprintAlgorithm</span></span> | <span data-ttu-id="45867-153">Określa algorytm wyznaczania wartości skrótu, używane do obliczania odcisk palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="45867-153">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="45867-154">Wartość domyślna to `SHA256`.</span><span class="sxs-lookup"><span data-stu-id="45867-154">Defaults to `SHA256`.</span></span> <span data-ttu-id="45867-155">Obsługiwane wartości `SHA256`, `SHA384` i `SHA512`</span><span class="sxs-lookup"><span data-stu-id="45867-155">Values supported are `SHA256`, `SHA384` and `SHA512`</span></span> |
| <span data-ttu-id="45867-156">AllowUntrustedRoot</span><span class="sxs-lookup"><span data-stu-id="45867-156">AllowUntrustedRoot</span></span> | <span data-ttu-id="45867-157">Określa, jeśli certyfikat dla zaufanych osoby podpisującej powinien być dozwolony do tworzenia łańcucha niezaufany certyfikat główny.</span><span class="sxs-lookup"><span data-stu-id="45867-157">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span> |

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="45867-158">Usuń nuget zaufanych — które podpisały — nazwa <name></span><span class="sxs-lookup"><span data-stu-id="45867-158">nuget trusted-signers remove -Name <name></span></span>

<span data-ttu-id="45867-159">Usuwa zaufane osoby podpisujące, zgodnych z podaną nazwą.</span><span class="sxs-lookup"><span data-stu-id="45867-159">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="45867-160">Synchronizowanie nuget zaufanych — które podpisały — nazwa <name></span><span class="sxs-lookup"><span data-stu-id="45867-160">nuget trusted-signers sync -Name <name></span></span>

<span data-ttu-id="45867-161">Żąda najnowszą listę certyfikatów używanych w zaufana repozytorium, aby zaktualizować istniejące listy certyfikatów w zaufane osoby podpisującej.</span><span class="sxs-lookup"><span data-stu-id="45867-161">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="45867-162">_Uwaga_: Ten gest będzie usunąć bieżącą listę certyfikatów i zastąp je aktualną listę z repozytorium.</span><span class="sxs-lookup"><span data-stu-id="45867-162">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="45867-163">Opcje</span><span class="sxs-lookup"><span data-stu-id="45867-163">Options</span></span>

| <span data-ttu-id="45867-164">Opcja</span><span class="sxs-lookup"><span data-stu-id="45867-164">Option</span></span> | <span data-ttu-id="45867-165">Opis</span><span class="sxs-lookup"><span data-stu-id="45867-165">Description</span></span> |
| --- | --- |
| <span data-ttu-id="45867-166">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="45867-166">ConfigFile</span></span> | <span data-ttu-id="45867-167">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="45867-167">The NuGet configuration file to apply.</span></span> <span data-ttu-id="45867-168">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="45867-168">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="45867-169">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="45867-169">ForceEnglishOutput</span></span> | <span data-ttu-id="45867-170">Wymusza nuget.exe do uruchamiania przy użyciu kultury niezmiennej, oparte na język angielski.</span><span class="sxs-lookup"><span data-stu-id="45867-170">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="45867-171">Pomoc</span><span class="sxs-lookup"><span data-stu-id="45867-171">Help</span></span> | <span data-ttu-id="45867-172">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="45867-172">Displays help information for the command.</span></span> |
| <span data-ttu-id="45867-173">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="45867-173">Verbosity</span></span> | <span data-ttu-id="45867-174">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="45867-174">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="45867-175">Przykłady</span><span class="sxs-lookup"><span data-stu-id="45867-175">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
