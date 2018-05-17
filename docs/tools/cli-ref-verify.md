---
title: Sprawdź NuGet interfejsu wiersza polecenia, polecenie
description: Dokumentacja dotycząca nuget.exe Sprawdź polecenie
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c2c31b71358bc50a1fb9aab8905c279cd1235b07
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/27/2018
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="50e28-103">verify command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="50e28-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="50e28-104">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="50e28-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="50e28-105">Sprawdza, czy pakiet.</span><span class="sxs-lookup"><span data-stu-id="50e28-105">Verifies a package.</span></span>

<span data-ttu-id="50e28-106">Weryfikacja podpisanych pakietów nie jest jeszcze obsługiwana w .NET Core, w obszarze Mono lub na różnych platformach z systemem innym niż Windows.</span><span class="sxs-lookup"><span data-stu-id="50e28-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="50e28-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="50e28-107">Usage</span></span>

```cli
nuget verify <package(s)> [options]
```

<span data-ttu-id="50e28-108">gdzie `<package(s)>` jest co najmniej jeden `.nupkg` plików.</span><span class="sxs-lookup"><span data-stu-id="50e28-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="options"></a><span data-ttu-id="50e28-109">Opcje</span><span class="sxs-lookup"><span data-stu-id="50e28-109">Options</span></span>

| <span data-ttu-id="50e28-110">Opcja</span><span class="sxs-lookup"><span data-stu-id="50e28-110">Option</span></span> | <span data-ttu-id="50e28-111">Opis</span><span class="sxs-lookup"><span data-stu-id="50e28-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="50e28-112">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="50e28-112">All</span></span> | <span data-ttu-id="50e28-113">Określa, że wszystkie sprawdzenia możliwe powinien być wykonywany na pakietów.</span><span class="sxs-lookup"><span data-stu-id="50e28-113">Specifies that all verifications possible should be performed on the package(s).</span></span> |
| <span data-ttu-id="50e28-114">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="50e28-114">CertificateFingerprint</span></span> | <span data-ttu-id="50e28-115">Określa co najmniej jeden algorytm SHA-256 certyfikatu odciski palców certyfikatów (s), które podpisem pakiety muszą być podpisane przy.</span><span class="sxs-lookup"><span data-stu-id="50e28-115">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="50e28-116">Odcisk palca certyfikatu algorytmu SHA-256 jest Skrót SHA-256 certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="50e28-116">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="50e28-117">Wielu danych wejściowych powinny być oddzielone średnikami.</span><span class="sxs-lookup"><span data-stu-id="50e28-117">Multiple inputs should be semicolon separated.</span></span> |
| <span data-ttu-id="50e28-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="50e28-118">ConfigFile</span></span> | <span data-ttu-id="50e28-119">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="50e28-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="50e28-120">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="50e28-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="50e28-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="50e28-121">ForceEnglishOutput</span></span> | <span data-ttu-id="50e28-122">Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="50e28-122">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="50e28-123">Pomoc</span><span class="sxs-lookup"><span data-stu-id="50e28-123">Help</span></span> | <span data-ttu-id="50e28-124">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="50e28-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="50e28-125">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="50e28-125">NonInteractive</span></span> | <span data-ttu-id="50e28-126">Pomija wyświetla monit o dane wejściowe użytkownika lub potwierdzeń.</span><span class="sxs-lookup"><span data-stu-id="50e28-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="50e28-127">Podpisy</span><span class="sxs-lookup"><span data-stu-id="50e28-127">Signatures</span></span> | <span data-ttu-id="50e28-128">Określa, należy wykonać weryfikacji podpisu pakietu.</span><span class="sxs-lookup"><span data-stu-id="50e28-128">Specifies that package signature verification should be performed.</span></span> |
| <span data-ttu-id="50e28-129">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="50e28-129">Verbosity</span></span> | <span data-ttu-id="50e28-130">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="50e28-130">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="50e28-131">Przykłady</span><span class="sxs-lookup"><span data-stu-id="50e28-131">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg
```