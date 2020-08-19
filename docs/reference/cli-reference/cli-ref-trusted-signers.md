---
title: Polecenie zaufanych-podpisywania interfejsu wiersza polecenia NuGet
description: Informacje dotyczące nuget.exe zaufanych-Signer polecenia
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 2753f92601b3d8b43593762cc07cd8384646feea
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622671"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="861d1-103">Zaufane-podpisujące — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="861d1-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="861d1-104">**Dotyczy:** &bullet; **obsługiwane wersje** pakietów: 4.9.1 +</span><span class="sxs-lookup"><span data-stu-id="861d1-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="861d1-105">Pobiera lub ustawia zaufane osoby podpisujące do konfiguracji programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="861d1-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="861d1-106">Aby uzyskać dodatkowe użycie, zobacz [typowe konfiguracje NuGet](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="861d1-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="861d1-107">Aby uzyskać szczegółowe informacje o tym, jak wygląda schemat nuget.config, zapoznaj się z tematem [Dokumentacja pliku konfiguracji programu NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="861d1-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="861d1-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="861d1-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="861d1-109">Jeśli żadna z nie `list|add|remove|sync` jest określona, polecenie będzie domyślnie `list` .</span><span class="sxs-lookup"><span data-stu-id="861d1-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="861d1-110">Lista zaufanych nadawców NuGet</span><span class="sxs-lookup"><span data-stu-id="861d1-110">nuget trusted-signers list</span></span>

<span data-ttu-id="861d1-111">Wyświetla listę wszystkich zaufanych podpisów w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="861d1-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="861d1-112">Ta opcja spowoduje uwzględnienie wszystkich certyfikatów (z użyciem algorytmu odcisku palca i odcisku palca) każdego osoby podpisującej.</span><span class="sxs-lookup"><span data-stu-id="861d1-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="861d1-113">Jeśli certyfikat ma wcześniejszą wartość `[U]` , oznacza to, że wpis certyfikatu ma `allowUntrustedRoot` ustawioną opcję `true` .</span><span class="sxs-lookup"><span data-stu-id="861d1-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="861d1-114">Poniżej znajduje się przykładowe dane wyjściowe z tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="861d1-114">Below is an example output from this command:</span></span>

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

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="861d1-115">zaufane osoby podpisujące NuGet — Dodawanie [opcje]</span><span class="sxs-lookup"><span data-stu-id="861d1-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="861d1-116">Dodaje do konfiguracji nazwę zaufanego podpisującego o danej nazwie. Ta opcja ma inne gesty umożliwiające dodanie zaufanego autora lub repozytorium.</span><span class="sxs-lookup"><span data-stu-id="861d1-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="861d1-117">Opcje dodawania w oparciu o pakiet</span><span class="sxs-lookup"><span data-stu-id="861d1-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package(s)> -Name <name> [options]
```

<span data-ttu-id="861d1-118">gdzie `<package(s)>` jest co najmniej jeden `.nupkg` plik.</span><span class="sxs-lookup"><span data-stu-id="861d1-118">where `<package(s)>` is one or more `.nupkg` files.</span></span>

- **`-Author`**

  <span data-ttu-id="861d1-119">Określa, że podpis autora pakietów powinien być zaufany.</span><span class="sxs-lookup"><span data-stu-id="861d1-119">Specifies that the author signature of the package(s) should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="861d1-120">Określa, czy certyfikat zaufanego podpisującego ma być dozwolony w łańcuchu do niezaufanego certyfikatu głównego.</span><span class="sxs-lookup"><span data-stu-id="861d1-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="861d1-121">Rozdzielana średnikami lista zaufanych właścicieli, aby bardziej ograniczyć zaufanie do repozytorium.</span><span class="sxs-lookup"><span data-stu-id="861d1-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="861d1-122">Prawidłowy tylko w przypadku użycia `-Repository` opcji.</span><span class="sxs-lookup"><span data-stu-id="861d1-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="861d1-123">Określa, że podpis repozytorium lub kontrpodpis pakietów powinien być zaufany.</span><span class="sxs-lookup"><span data-stu-id="861d1-123">Specifies that the repository signature or countersignature of the package(s) should be trusted.</span></span>

<span data-ttu-id="861d1-124">Udostępnianie jednocześnie `-Author` i `-Repository` w tym samym czasie nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="861d1-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="861d1-125">Opcje dodawania oparte na indeksie usługi</span><span class="sxs-lookup"><span data-stu-id="861d1-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="861d1-126">_Uwaga_: Ta opcja spowoduje dodanie tylko zaufanych repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="861d1-126">_Note_: This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="861d1-127">Określa, czy certyfikat zaufanego podpisującego ma być dozwolony w łańcuchu do niezaufanego certyfikatu głównego.</span><span class="sxs-lookup"><span data-stu-id="861d1-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="861d1-128">Rozdzielana średnikami lista zaufanych właścicieli, aby bardziej ograniczyć zaufanie do repozytorium.</span><span class="sxs-lookup"><span data-stu-id="861d1-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="861d1-129">Określa indeks usługi v3 repozytorium, który ma być zaufany.</span><span class="sxs-lookup"><span data-stu-id="861d1-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="861d1-130">To repozytorium ma obsługiwać zasób sygnatur repozytorium.</span><span class="sxs-lookup"><span data-stu-id="861d1-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="861d1-131">Jeśli nie zostanie podany, polecenie będzie szukać źródła pakietu o tej samej `-Name` i pobrać z niego indeks usługi.</span><span class="sxs-lookup"><span data-stu-id="861d1-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="861d1-132">Opcje dodawania na podstawie informacji o certyfikacie</span><span class="sxs-lookup"><span data-stu-id="861d1-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="861d1-133">_Uwaga_: Jeśli zaufany podpis o podanej nazwie już istnieje, element certyfikatu zostanie dodany do osoby podpisującej.</span><span class="sxs-lookup"><span data-stu-id="861d1-133">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="861d1-134">W przeciwnym razie zaufany autor zostanie utworzony za pomocą elementu certyfikatu z informacji podanych w certyfikacie.</span><span class="sxs-lookup"><span data-stu-id="861d1-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="861d1-135">Określa, czy certyfikat zaufanego podpisującego ma być dozwolony w łańcuchu do niezaufanego certyfikatu głównego.</span><span class="sxs-lookup"><span data-stu-id="861d1-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="861d1-136">Określa odciski palca certyfikatu, z którym podpisane pakiety muszą być podpisane.</span><span class="sxs-lookup"><span data-stu-id="861d1-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="861d1-137">Odcisk palca certyfikatu jest skrótem certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="861d1-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="861d1-138">Algorytm wyznaczania wartości skrótu używany do obliczania tego skrótu powinien być określany w `FingerprintAlgorithm` opcji.</span><span class="sxs-lookup"><span data-stu-id="861d1-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="861d1-139">Określa algorytm wyznaczania wartości skrótu używany do obliczania odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="861d1-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="861d1-140">Wartość domyślna to `SHA256` .</span><span class="sxs-lookup"><span data-stu-id="861d1-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="861d1-141">Obsługiwane są wartości `SHA256` , `SHA384` i `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="861d1-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="861d1-142">zaufane osoby podpisujące NuGet — usuwanie nazwy \<name\></span><span class="sxs-lookup"><span data-stu-id="861d1-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="861d1-143">Usuwa wszystkie zaufane osoby podpisujące zgodne z podaną nazwą.</span><span class="sxs-lookup"><span data-stu-id="861d1-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="861d1-144">Synchronizacja zaufanych nadawców NuGet — nazwa \<name\></span><span class="sxs-lookup"><span data-stu-id="861d1-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="861d1-145">Żąda najnowszej listy certyfikatów używanych w bieżącym repozytorium, aby zaktualizować listę istniejących certyfikatów w zaufanej rejestracji.</span><span class="sxs-lookup"><span data-stu-id="861d1-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="861d1-146">_Uwaga_: ten gest spowoduje usunięcie bieżącej listy certyfikatów i zamienienie ich na aktualną listę z repozytorium.</span><span class="sxs-lookup"><span data-stu-id="861d1-146">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="861d1-147">Opcje</span><span class="sxs-lookup"><span data-stu-id="861d1-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="861d1-148">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="861d1-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="861d1-149">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="861d1-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="861d1-150">Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="861d1-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="861d1-151">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="861d1-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="861d1-152">Nazwa zaufanej osoby podpisującej.</span><span class="sxs-lookup"><span data-stu-id="861d1-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="861d1-153">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="861d1-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="861d1-154">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="861d1-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="861d1-155">Przykłady</span><span class="sxs-lookup"><span data-stu-id="861d1-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget-trusted-signers Remove -Name TrustedRepo

nuget-trusted-signers Sync -Name TrustedRepo
```
