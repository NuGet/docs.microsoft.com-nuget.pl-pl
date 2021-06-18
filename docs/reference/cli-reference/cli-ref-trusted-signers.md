---
title: Polecenie zaufanych podpisujących interfejs wiersza polecenia nuGet
description: Odwołanie do polecenia nuget.exe zaufanych podpisujących
author: patbel
ms.author: patbel
ms.date: 11/12/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: a5f3564af8b96dfa673d2252aea2e77a79c184a4
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323593"
---
# <a name="trusted-signers-command-nuget-cli"></a><span data-ttu-id="60e28-103">Polecenie trusted-signers (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="60e28-103">trusted-signers command (NuGet CLI)</span></span>

<span data-ttu-id="60e28-104">**Dotyczy: zużycie** pakietu &bullet; **Obsługiwane wersje:** 4.9.1+</span><span class="sxs-lookup"><span data-stu-id="60e28-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.9.1+</span></span>

<span data-ttu-id="60e28-105">Pobiera lub ustawia zaufanych podpisujących do konfiguracji NuGet.</span><span class="sxs-lookup"><span data-stu-id="60e28-105">Gets or sets trusted signers to the NuGet configuration.</span></span> <span data-ttu-id="60e28-106">Aby uzyskać dodatkowe informacje o użyciu, zobacz [Typowe konfiguracje NuGet.](../../consume-packages/configuring-nuget-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="60e28-106">For additional usage, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="60e28-107">Aby uzyskać szczegółowe informacje na temat nuget.config schematu, zapoznaj się z odwołaniem do pliku [konfiguracji NuGet](../nuget-config-file.md).</span><span class="sxs-lookup"><span data-stu-id="60e28-107">For details on how the nuget.config schema looks like, refer to the [NuGet config file reference](../nuget-config-file.md).</span></span>

## <a name="usage"></a><span data-ttu-id="60e28-108">Użycie</span><span class="sxs-lookup"><span data-stu-id="60e28-108">Usage</span></span>

```cli
nuget trusted-signers <list|add|remove|sync> [options]
```

<span data-ttu-id="60e28-109">Jeśli żadna z `list|add|remove|sync` wartości nie zostanie określona, polecenie domyślnie będzie mieć wartość `list` .</span><span class="sxs-lookup"><span data-stu-id="60e28-109">if none of `list|add|remove|sync` is specified, the command will default to `list`.</span></span>

## <a name="nuget-trusted-signers-list"></a><span data-ttu-id="60e28-110">Lista zaufanych podpisujących nuget</span><span class="sxs-lookup"><span data-stu-id="60e28-110">nuget trusted-signers list</span></span>

<span data-ttu-id="60e28-111">Wyświetla listę wszystkich zaufanych osób podpisujących w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="60e28-111">Lists all the trusted signers in the configuration.</span></span> <span data-ttu-id="60e28-112">Ta opcja obejmuje wszystkie certyfikaty (z algorytmem odcisku palca i odcisku palca) posiadane przez każdego podpiszcę.</span><span class="sxs-lookup"><span data-stu-id="60e28-112">This option will include all the certificates (with fingerprint and fingerprint algorithm) each signer has.</span></span> <span data-ttu-id="60e28-113">Jeśli certyfikat ma poprzednią `[U]` wartość , oznacza to, że wpis certyfikatu został `allowUntrustedRoot` ustawiony jako `true` .</span><span class="sxs-lookup"><span data-stu-id="60e28-113">If a certificate has a preceding `[U]`, it means that certificate entry has `allowUntrustedRoot` set as `true`.</span></span>

<span data-ttu-id="60e28-114">Poniżej przedstawiono przykładowe dane wyjściowe tego polecenia:</span><span class="sxs-lookup"><span data-stu-id="60e28-114">Below is an example output from this command:</span></span>

```cli
$ nuget trusted-signers
Registered trusted signers:


 1.   nuget.org [repository]
      Service Index: https://api.nuget.org/v3/index.json
      Certificate fingerprint(s):
        SHA256 - 0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D
        SHA256 - 5A2901D6ADA3D18260B9C6DFE2133C95D74B9EEF6AE0E5DC334C8454D1477DF4

 2.   microsoft [author]
      Certificate fingerprint(s):
        SHA256 - 3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE
        SHA256 - AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27

 3.   myUntrustedAuthorSignature [author]
      Certificate fingerprint(s):
        [U] SHA256 - 518F9CF082C0872025EFB2587B6A6AB198208F63EA58DD54D2B9FF6735CA4434
        
```

## <a name="nuget-trusted-signers-add-options"></a><span data-ttu-id="60e28-115">NuGet — zaufani podpisujący dodają [opcje]</span><span class="sxs-lookup"><span data-stu-id="60e28-115">nuget trusted-signers add [options]</span></span>

<span data-ttu-id="60e28-116">Dodaje zaufanego podpiszącego o podanej nazwie do konfiguracji. Ta opcja ma różne gesty dodawania zaufanego autora lub repozytorium.</span><span class="sxs-lookup"><span data-stu-id="60e28-116">Adds a trusted signer with the given name to the config. This option has different gestures to add a trusted author or repository.</span></span>

## <a name="options-for-add-based-on-a-package"></a><span data-ttu-id="60e28-117">Opcje dodawania na podstawie pakietu</span><span class="sxs-lookup"><span data-stu-id="60e28-117">Options for add based on a package</span></span>

```cli
nuget trusted-signers add <package> -Name <name> [options]
```

<span data-ttu-id="60e28-118">gdzie `<package>` to jeden podpisany `.nupkg` plik.</span><span class="sxs-lookup"><span data-stu-id="60e28-118">where `<package>` is one signed `.nupkg` file.</span></span>

- **`-Author`**

  <span data-ttu-id="60e28-119">Określa, że podpis autora podpisanego pakietu powinien być zaufany.</span><span class="sxs-lookup"><span data-stu-id="60e28-119">Specifies that the author signature of the signed package should be trusted.</span></span>

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="60e28-120">Określa, czy certyfikat zaufanego podpiszącego powinien mieć możliwość podpisania łańcucha do niezaufanego katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="60e28-120">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="60e28-121">Rozdzielana średnikami lista zaufanych właścicieli w celu dalszego ograniczenia zaufania repozytorium.</span><span class="sxs-lookup"><span data-stu-id="60e28-121">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span> <span data-ttu-id="60e28-122">Prawidłowy tylko w przypadku korzystania z `-Repository` opcji .</span><span class="sxs-lookup"><span data-stu-id="60e28-122">Only valid when using the `-Repository` option.</span></span>

- **`-Repository`**

  <span data-ttu-id="60e28-123">Określa, że podpis repozytorium lub countersignature podpisanego pakietu powinny być zaufane.</span><span class="sxs-lookup"><span data-stu-id="60e28-123">Specifies that the repository signature or countersignature of the signed package should be trusted.</span></span>

<span data-ttu-id="60e28-124">Zarówno, `-Author` jak i w tym samym `-Repository` czasie, nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="60e28-124">Providing both `-Author` and `-Repository` at the same time is not supported.</span></span>

## <a name="options-for-add-based-on-a-service-index"></a><span data-ttu-id="60e28-125">Opcje dodawania na podstawie indeksu usługi</span><span class="sxs-lookup"><span data-stu-id="60e28-125">Options for add based on a service index</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="60e28-126">_Uwaga:_ ta opcja spowoduje dodanie tylko zaufanych repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="60e28-126">_Note_: This option will only add trusted repositories.</span></span> 

- **`-AllowUntrustedRoot`**

  <span data-ttu-id="60e28-127">Określa, czy certyfikat zaufanego podpiszącego powinien mieć możliwość podpisania łańcucha do niezaufanego katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="60e28-127">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-Owners`**

  <span data-ttu-id="60e28-128">Rozdzielana średnikami lista zaufanych właścicieli w celu dalszego ograniczenia zaufania repozytorium.</span><span class="sxs-lookup"><span data-stu-id="60e28-128">Semi-colon separated list of trusted owners to further restrict the trust of a repository.</span></span>

- **`-ServiceIndex`**

  <span data-ttu-id="60e28-129">Określa indeks usługi w wersji 3 repozytorium, który ma być zaufany.</span><span class="sxs-lookup"><span data-stu-id="60e28-129">Specifies the V3 service index of the repository to be trusted.</span></span> <span data-ttu-id="60e28-130">To repozytorium musi obsługiwać zasób sygnatur repozytorium.</span><span class="sxs-lookup"><span data-stu-id="60e28-130">This repository has to support the repository signatures resource.</span></span> <span data-ttu-id="60e28-131">Jeśli nie zostanie podany, polecenie będzie szukać źródła pakietu z tym samym i `-Name` pobrać indeks usługi z tego źródła.</span><span class="sxs-lookup"><span data-stu-id="60e28-131">If not provided, the command will look for a package source with the same `-Name` and get the service index from there.</span></span>

## <a name="options-for-add-based-on-the-certificate-information"></a><span data-ttu-id="60e28-132">Opcje dodawania na podstawie informacji o certyfikacie</span><span class="sxs-lookup"><span data-stu-id="60e28-132">Options for add based on the certificate information</span></span>

```cli
nuget trusted-signers add -Name <name> [options]
```

<span data-ttu-id="60e28-133">_Uwaga:_ jeśli zaufany podpiszator o podanej nazwie już istnieje, element certyfikatu zostanie dodany do tego osoby podpiszącego.</span><span class="sxs-lookup"><span data-stu-id="60e28-133">_Note_: If a trusted signer with the given name already exists, the certificate item will be added to that signer.</span></span> <span data-ttu-id="60e28-134">W przeciwnym razie zostanie utworzony zaufany autor z elementem certyfikatu z informacji o certyfikacie.</span><span class="sxs-lookup"><span data-stu-id="60e28-134">Otherwise a trusted author will be created with a certificate item from given certificate information.</span></span>


- **`-AllowUntrustedRoot`**

  <span data-ttu-id="60e28-135">Określa, czy certyfikat zaufanego podpiszącego powinien mieć możliwość podpisania łańcucha do niezaufanego katalogu głównego.</span><span class="sxs-lookup"><span data-stu-id="60e28-135">Specifies if the certificate for the trusted signer should be allowed to chain to an untrusted root.</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="60e28-136">Określa odciski palców certyfikatu, za pomocą którego muszą być podpisane podpisane pakiety.</span><span class="sxs-lookup"><span data-stu-id="60e28-136">Specifies a certificate fingerprints of a certificate which signed packages must be signed with.</span></span> <span data-ttu-id="60e28-137">Odcisk palca certyfikatu jest skrótem certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="60e28-137">A certificate fingerprint is a hash of the certificate.</span></span> <span data-ttu-id="60e28-138">W opcji należy określić algorytm wyznaczania wartości skrótu używany do obliczania tego `FingerprintAlgorithm` skrótu.</span><span class="sxs-lookup"><span data-stu-id="60e28-138">The hash algorithm used for calculating this hash should be specifies in the `FingerprintAlgorithm` option.</span></span>

- **`-FingerprintAlgorithm`**

  <span data-ttu-id="60e28-139">Określa algorytm wyznaczania wartości skrótu używany do obliczania odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="60e28-139">Specifies the hash algorithm used to calculate the certificate fingerprint.</span></span> <span data-ttu-id="60e28-140">Wartość domyślna to `SHA256` .</span><span class="sxs-lookup"><span data-stu-id="60e28-140">Defaults to `SHA256`.</span></span> <span data-ttu-id="60e28-141">Obsługiwane wartości to `SHA256` , `SHA384` i `SHA512` .</span><span class="sxs-lookup"><span data-stu-id="60e28-141">Values supported are `SHA256`, `SHA384` and `SHA512`.</span></span>

## <a name="nuget-trusted-signers-remove--name-name"></a><span data-ttu-id="60e28-142">Zaufani podpisujący nuget usuwają -Name \<name\></span><span class="sxs-lookup"><span data-stu-id="60e28-142">nuget trusted-signers remove -Name \<name\></span></span>

<span data-ttu-id="60e28-143">Usuwa wszystkich zaufanych podpisujących, które pasują do podanej nazwy.</span><span class="sxs-lookup"><span data-stu-id="60e28-143">Removes any trusted signers that match the given name.</span></span>

## <a name="nuget-trusted-signers-sync--name-name"></a><span data-ttu-id="60e28-144">Nuget trusted-signers sync -Name \<name\></span><span class="sxs-lookup"><span data-stu-id="60e28-144">nuget trusted-signers sync -Name \<name\></span></span>

<span data-ttu-id="60e28-145">Żąda najnowszej listy certyfikatów używanych w aktualnie zaufanym repozytorium w celu zaktualizowania istniejącej listy certyfikatów na zaufanym podpisie.</span><span class="sxs-lookup"><span data-stu-id="60e28-145">Requests the latest list of certificates used in a currently trusted repository to update the the existing certificate list in the trusted signer.</span></span>

<span data-ttu-id="60e28-146">_Uwaga:_ ten gest spowoduje usunięcie bieżącej listy certyfikatów i zastąpienie ich aktualną listą z repozytorium.</span><span class="sxs-lookup"><span data-stu-id="60e28-146">_Note_: This gesture will delete the current list of certificates and replace them with an up-to-date list from the repository.</span></span>

## <a name="options"></a><span data-ttu-id="60e28-147">Opcje</span><span class="sxs-lookup"><span data-stu-id="60e28-147">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="60e28-148">Plik konfiguracji NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="60e28-148">The NuGet configuration file to apply.</span></span> <span data-ttu-id="60e28-149">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="60e28-149">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="60e28-150">Wymusza nuget.exe uruchamiania przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="60e28-150">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="60e28-151">Wyświetla informacje pomocy dotyczące polecenia.</span><span class="sxs-lookup"><span data-stu-id="60e28-151">Displays help information for the command.</span></span>

- **`-Name`**

  <span data-ttu-id="60e28-152">Nazwa zaufanego podpisatora.</span><span class="sxs-lookup"><span data-stu-id="60e28-152">Name of the trusted signer.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="60e28-153">Pomija monity o wprowadzenie danych przez użytkownika lub potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="60e28-153">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="60e28-154">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (ustawienie domyślne), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="60e28-154">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>


## <a name="examples"></a><span data-ttu-id="60e28-155">Przykłady</span><span class="sxs-lookup"><span data-stu-id="60e28-155">Examples</span></span>

```cli
nuget trusted-signers list

nuget trusted-signers Add -Name existingSource

nuget trusted-signers Add -Name trustedRepo -ServiceIndex https://trustedRepo.test/v3ServiceIndex

nuget trusted-signers Add -Name author1 -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039 -FingerprintAlgorithm SHA256

nuget trusted-signers Add -Repository .\..\MyRepositorySignedPackage.nupkg -Name TrustedRepo

nuget trusted-signers Remove -Name TrustedRepo

nuget trusted-signers Sync -Name TrustedRepo
```
