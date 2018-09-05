---
title: Sprawdź interfejs wiersza polecenia NuGet, polecenie
description: Dokumentacja dotycząca nuget.exe sprawdź polecenia
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 127f7a549c0a213f319c8820293646b302830436
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545216"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="73c61-103">verify command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="73c61-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="73c61-104">**Dotyczy:** pakietu zużycie &bullet; **obsługiwane wersje:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="73c61-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="73c61-105">Weryfikuje pakietu.</span><span class="sxs-lookup"><span data-stu-id="73c61-105">Verifies a package.</span></span>

<span data-ttu-id="73c61-106">Weryfikacja podpisanych pakietów nie jest jeszcze obsługiwana w platformę .NET Core, w ramach platformy Mono lub na platformach innych niż Windows.</span><span class="sxs-lookup"><span data-stu-id="73c61-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="73c61-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="73c61-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="73c61-108">gdzie `<package(s)>` ma jeden lub więcej `.nupkg` plików.</span><span class="sxs-lookup"><span data-stu-id="73c61-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="73c61-109">Weryfikuj nuget — wszystkie</span><span class="sxs-lookup"><span data-stu-id="73c61-109">nuget verify -All</span></span>

<span data-ttu-id="73c61-110">Określa, że wszystkie sprawdzenia możliwe powinno być przeprowadzane w pakiety.</span><span class="sxs-lookup"><span data-stu-id="73c61-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="73c61-111">Sprawdzanie nuget — podpisów</span><span class="sxs-lookup"><span data-stu-id="73c61-111">nuget verify -Signatures</span></span>

<span data-ttu-id="73c61-112">Określa, że powinno być przeprowadzane Weryfikacja podpisu pakietu.</span><span class="sxs-lookup"><span data-stu-id="73c61-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="73c61-113">Opcje "Weryfikuj - sygnatury"</span><span class="sxs-lookup"><span data-stu-id="73c61-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="73c61-114">Opcja</span><span class="sxs-lookup"><span data-stu-id="73c61-114">Option</span></span> | <span data-ttu-id="73c61-115">Opis</span><span class="sxs-lookup"><span data-stu-id="73c61-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="73c61-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="73c61-116">CertificateFingerprint</span></span> | <span data-ttu-id="73c61-117">Określa co najmniej jeden algorytm SHA-256 certyfikatu odcisków palców certyfikatów (s), które podpisane pakiety muszą być podpisane za pomocą.</span><span class="sxs-lookup"><span data-stu-id="73c61-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="73c61-118">Odcisk palca certyfikatu SHA-256 jest Skrót SHA-256 wymagany certyfikat.</span><span class="sxs-lookup"><span data-stu-id="73c61-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="73c61-119">Wielu danych wejściowych powinien być średnikami.</span><span class="sxs-lookup"><span data-stu-id="73c61-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="73c61-120">Opcje</span><span class="sxs-lookup"><span data-stu-id="73c61-120">Options</span></span>

| <span data-ttu-id="73c61-121">Opcja</span><span class="sxs-lookup"><span data-stu-id="73c61-121">Option</span></span> | <span data-ttu-id="73c61-122">Opis</span><span class="sxs-lookup"><span data-stu-id="73c61-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="73c61-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="73c61-123">ConfigFile</span></span> | <span data-ttu-id="73c61-124">Plik konfiguracyjny NuGet do zastosowania.</span><span class="sxs-lookup"><span data-stu-id="73c61-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="73c61-125">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="73c61-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="73c61-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="73c61-126">ForceEnglishOutput</span></span> | <span data-ttu-id="73c61-127">Wymusza nuget.exe do uruchamiania przy użyciu kultury niezmiennej, oparte na język angielski.</span><span class="sxs-lookup"><span data-stu-id="73c61-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="73c61-128">Pomoc</span><span class="sxs-lookup"><span data-stu-id="73c61-128">Help</span></span> | <span data-ttu-id="73c61-129">Wyświetla Pomoc dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="73c61-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="73c61-130">Szczegółowość</span><span class="sxs-lookup"><span data-stu-id="73c61-130">Verbosity</span></span> | <span data-ttu-id="73c61-131">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *cichy*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="73c61-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="73c61-132">Przykłady</span><span class="sxs-lookup"><span data-stu-id="73c61-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```