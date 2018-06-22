---
title: Sprawdź NuGet interfejsu wiersza polecenia, polecenie
description: Dokumentacja dotycząca nuget.exe Sprawdź polecenie
author: dtivel
ms.author: dtivel
manager: doronm
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: c80334104f7d8b2ccbf16ea2c11dc37b39408eeb
ms.sourcegitcommit: c8485dc61469511485367d2067b97d6f74b49f6e
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/23/2018
ms.locfileid: "34462855"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="f4bac-103">verify command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="f4bac-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="f4bac-104">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="f4bac-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="f4bac-105">Sprawdza, czy pakiet.</span><span class="sxs-lookup"><span data-stu-id="f4bac-105">Verifies a package.</span></span>

<span data-ttu-id="f4bac-106">Weryfikacja podpisanych pakietów nie jest jeszcze obsługiwana w .NET Core, w obszarze Mono lub na różnych platformach z systemem innym niż Windows.</span><span class="sxs-lookup"><span data-stu-id="f4bac-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="f4bac-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="f4bac-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="f4bac-108">gdzie `<package(s)>` jest co najmniej jeden `.nupkg` plików.</span><span class="sxs-lookup"><span data-stu-id="f4bac-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="f4bac-109">Sprawdź nuget — wszystkie</span><span class="sxs-lookup"><span data-stu-id="f4bac-109">nuget verify -All</span></span>

<span data-ttu-id="f4bac-110">Określa, że wszystkie sprawdzenia możliwe powinien być wykonywany na pakietów.</span><span class="sxs-lookup"><span data-stu-id="f4bac-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="f4bac-111">Sprawdź nuget - podpisów</span><span class="sxs-lookup"><span data-stu-id="f4bac-111">nuget verify -Signatures</span></span>

<span data-ttu-id="f4bac-112">Określa, należy wykonać weryfikacji podpisu pakietu.</span><span class="sxs-lookup"><span data-stu-id="f4bac-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="f4bac-113">Opcje "Weryfikuj - podpisów"</span><span class="sxs-lookup"><span data-stu-id="f4bac-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="f4bac-114">Opcja</span><span class="sxs-lookup"><span data-stu-id="f4bac-114">Option</span></span> | <span data-ttu-id="f4bac-115">Opis</span><span class="sxs-lookup"><span data-stu-id="f4bac-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f4bac-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="f4bac-116">CertificateFingerprint</span></span> | <span data-ttu-id="f4bac-117">Określa co najmniej jeden algorytm SHA-256 certyfikatu odciski palców certyfikatów (s), które podpisem pakiety muszą być podpisane przy.</span><span class="sxs-lookup"><span data-stu-id="f4bac-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="f4bac-118">Odcisk palca certyfikatu algorytmu SHA-256 jest Skrót SHA-256 certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="f4bac-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="f4bac-119">Wielu danych wejściowych powinny być oddzielone średnikami.</span><span class="sxs-lookup"><span data-stu-id="f4bac-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="f4bac-120">Opcje</span><span class="sxs-lookup"><span data-stu-id="f4bac-120">Options</span></span>

| <span data-ttu-id="f4bac-121">Opcja</span><span class="sxs-lookup"><span data-stu-id="f4bac-121">Option</span></span> | <span data-ttu-id="f4bac-122">Opis</span><span class="sxs-lookup"><span data-stu-id="f4bac-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f4bac-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f4bac-123">ConfigFile</span></span> | <span data-ttu-id="f4bac-124">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="f4bac-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f4bac-125">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="f4bac-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f4bac-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f4bac-126">ForceEnglishOutput</span></span> | <span data-ttu-id="f4bac-127">Wymusza nuget.exe przy użyciu opartego na język angielski, niezmienna kultura.</span><span class="sxs-lookup"><span data-stu-id="f4bac-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f4bac-128">Pomoc</span><span class="sxs-lookup"><span data-stu-id="f4bac-128">Help</span></span> | <span data-ttu-id="f4bac-129">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="f4bac-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="f4bac-130">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="f4bac-130">Verbosity</span></span> | <span data-ttu-id="f4bac-131">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *quiet*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="f4bac-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="f4bac-132">Przykłady</span><span class="sxs-lookup"><span data-stu-id="f4bac-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```