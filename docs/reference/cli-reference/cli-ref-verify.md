---
title: Polecenie weryfikacji interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia nuget.exe verify
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 7ce08f11195437e94bfe69883ff525e9ad3a73f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238143"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="220a7-103">VERIFY — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="220a7-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="220a7-104">**Dotyczy:** &bullet; **obsługiwane wersje pakietów:** 4.6 +</span><span class="sxs-lookup"><span data-stu-id="220a7-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="220a7-105">Weryfikuje pakiet.</span><span class="sxs-lookup"><span data-stu-id="220a7-105">Verifies a package.</span></span>

<span data-ttu-id="220a7-106">Weryfikacja podpisanych pakietów nie jest jeszcze obsługiwana w programie mono.</span><span class="sxs-lookup"><span data-stu-id="220a7-106">Verification of signed packages is not yet supported under Mono.</span></span>

## <a name="usage"></a><span data-ttu-id="220a7-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="220a7-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="220a7-108">gdzie `<package(s)>` jest co najmniej jeden `.nupkg` plik.</span><span class="sxs-lookup"><span data-stu-id="220a7-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="220a7-109">Weryfikacja NuGet — wszystkie</span><span class="sxs-lookup"><span data-stu-id="220a7-109">nuget verify -All</span></span>

<span data-ttu-id="220a7-110">Określa, że wszystkie możliwe weryfikacje powinny być wykonywane na pakietach.</span><span class="sxs-lookup"><span data-stu-id="220a7-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="220a7-111">Weryfikacja przez pakiet NuGet — sygnatury</span><span class="sxs-lookup"><span data-stu-id="220a7-111">nuget verify -Signatures</span></span>

<span data-ttu-id="220a7-112">Określa, że należy przeprowadzić weryfikację podpisu pakietu.</span><span class="sxs-lookup"><span data-stu-id="220a7-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="220a7-113">Opcje "Weryfikuj sygnaturę"</span><span class="sxs-lookup"><span data-stu-id="220a7-113">Options for "verify -Signatures"</span></span>

- **`-CertificateFingerprint`**

  <span data-ttu-id="220a7-114">Określa co najmniej jeden odcisk palca certyfikatu SHA-256 certyfikatów, które podpisane pakiety muszą być podpisane.</span><span class="sxs-lookup"><span data-stu-id="220a7-114">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="220a7-115">Odcisk palca SHA-256 certyfikatu jest skrótem SHA-256 certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="220a7-115">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="220a7-116">Wielokrotne dane wejściowe powinny być rozdzielone średnikami.</span><span class="sxs-lookup"><span data-stu-id="220a7-116">Multiple inputs should be semicolon separated.</span></span>

## <a name="options"></a><span data-ttu-id="220a7-117">Opcje</span><span class="sxs-lookup"><span data-stu-id="220a7-117">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="220a7-118">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="220a7-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="220a7-119">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="220a7-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="220a7-120">Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="220a7-120">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="220a7-121">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="220a7-121">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="220a7-122">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="220a7-122">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="220a7-123">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="220a7-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

## <a name="examples"></a><span data-ttu-id="220a7-124">Przykłady</span><span class="sxs-lookup"><span data-stu-id="220a7-124">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```