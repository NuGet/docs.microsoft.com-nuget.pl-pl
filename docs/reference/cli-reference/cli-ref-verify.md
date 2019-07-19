---
title: Polecenie weryfikacji interfejsu wiersza polecenia NuGet
description: Odwołanie do polecenia VERIFY. exe programu NuGet
author: dtivel
ms.author: dtivel
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: rmpablos
ms.openlocfilehash: 9510f7323fe0cb860e0dbde51c1eda761846ee27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328253"
---
# <a name="verify-command-nuget-cli"></a><span data-ttu-id="1c685-103">verify command, polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="1c685-103">verify command (NuGet CLI)</span></span>

<span data-ttu-id="1c685-104">**Dotyczy:** **obsługiwane wersje** pakietów &bullet; : 4.6 +</span><span class="sxs-lookup"><span data-stu-id="1c685-104">**Applies to:** package consumption &bullet; **Supported versions:** 4.6+</span></span>

<span data-ttu-id="1c685-105">Weryfikuje pakiet.</span><span class="sxs-lookup"><span data-stu-id="1c685-105">Verifies a package.</span></span>

<span data-ttu-id="1c685-106">Weryfikacja podpisanych pakietów nie jest jeszcze obsługiwana w programie .NET Core, w obszarze mono lub na platformach innych niż Windows.</span><span class="sxs-lookup"><span data-stu-id="1c685-106">Verification of signed packages is not yet supported in .NET Core, under Mono, or on non-Windows platforms.</span></span>

## <a name="usage"></a><span data-ttu-id="1c685-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="1c685-107">Usage</span></span>

```cli
nuget verify <-All|-Signatures> <package(s)> [options]
```

<span data-ttu-id="1c685-108">gdzie `<package(s)>` jest co najmniej jeden `.nupkg` plik.</span><span class="sxs-lookup"><span data-stu-id="1c685-108">where `<package(s)>` is one or more `.nupkg` files.</span></span>

## <a name="nuget-verify--all"></a><span data-ttu-id="1c685-109">Weryfikacja NuGet — wszystkie</span><span class="sxs-lookup"><span data-stu-id="1c685-109">nuget verify -All</span></span>

<span data-ttu-id="1c685-110">Określa, że wszystkie możliwe weryfikacje powinny być wykonywane na pakietach.</span><span class="sxs-lookup"><span data-stu-id="1c685-110">Specifies that all verifications possible should be performed on the package(s).</span></span>

## <a name="nuget-verify--signatures"></a><span data-ttu-id="1c685-111">Weryfikacja przez pakiet NuGet — sygnatury</span><span class="sxs-lookup"><span data-stu-id="1c685-111">nuget verify -Signatures</span></span>

<span data-ttu-id="1c685-112">Określa, że należy przeprowadzić weryfikację podpisu pakietu.</span><span class="sxs-lookup"><span data-stu-id="1c685-112">Specifies that package signature verification should be performed.</span></span>

## <a name="options-for-verify--signatures"></a><span data-ttu-id="1c685-113">Opcje "Weryfikuj sygnaturę"</span><span class="sxs-lookup"><span data-stu-id="1c685-113">Options for "verify -Signatures"</span></span>

| <span data-ttu-id="1c685-114">Opcja</span><span class="sxs-lookup"><span data-stu-id="1c685-114">Option</span></span> | <span data-ttu-id="1c685-115">Opis</span><span class="sxs-lookup"><span data-stu-id="1c685-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1c685-116">CertificateFingerprint</span><span class="sxs-lookup"><span data-stu-id="1c685-116">CertificateFingerprint</span></span> | <span data-ttu-id="1c685-117">Określa co najmniej jeden odcisk palca certyfikatu SHA-256 certyfikatów, które podpisane pakiety muszą być podpisane.</span><span class="sxs-lookup"><span data-stu-id="1c685-117">Specifies one or more SHA-256 certificate fingerprints of certificates(s) which signed packages must be signed with.</span></span> <span data-ttu-id="1c685-118">Odcisk palca SHA-256 certyfikatu jest skrótem SHA-256 certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="1c685-118">A certificate SHA-256 fingerprint is a SHA-256 hash of the certificate.</span></span> <span data-ttu-id="1c685-119">Wielokrotne dane wejściowe powinny być rozdzielone średnikami.</span><span class="sxs-lookup"><span data-stu-id="1c685-119">Multiple inputs should be semicolon separated.</span></span> |

## <a name="options"></a><span data-ttu-id="1c685-120">Opcje</span><span class="sxs-lookup"><span data-stu-id="1c685-120">Options</span></span>

| <span data-ttu-id="1c685-121">Opcja</span><span class="sxs-lookup"><span data-stu-id="1c685-121">Option</span></span> | <span data-ttu-id="1c685-122">Opis</span><span class="sxs-lookup"><span data-stu-id="1c685-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1c685-123">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1c685-123">ConfigFile</span></span> | <span data-ttu-id="1c685-124">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="1c685-124">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1c685-125">Jeśli nie zostanie określony `%AppData%\NuGet\NuGet.Config` , używany jest system `~/.nuget/NuGet/NuGet.Config` (Windows) lub (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="1c685-125">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1c685-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1c685-126">ForceEnglishOutput</span></span> | <span data-ttu-id="1c685-127">Wymusza uruchomienie NuGet. exe przy użyciu niezmiennej, opartej na języku angielskim kultury.</span><span class="sxs-lookup"><span data-stu-id="1c685-127">Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1c685-128">Help</span><span class="sxs-lookup"><span data-stu-id="1c685-128">Help</span></span> | <span data-ttu-id="1c685-129">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="1c685-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="1c685-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="1c685-130">Verbosity</span></span> | <span data-ttu-id="1c685-131">Określa ilość szczegółów wyświetlanych w danych wyjściowych: *normalne*, *ciche*, *szczegółowe*.</span><span class="sxs-lookup"><span data-stu-id="1c685-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

## <a name="examples"></a><span data-ttu-id="1c685-132">Przykłady</span><span class="sxs-lookup"><span data-stu-id="1c685-132">Examples</span></span>

```cli
nuget verify -Signatures .\..\MyPackage.nupkg -CertificateFingerprint "CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039;5F874AAF47BCB268A19357364E7FBB09D6BF9E8A93E1229909AC5CAC865802E2" -Verbosity detailed

nuget verify -Signatures c:\packages\MyPackage.nupkg -CertificateFingerprint CE40881FF5F0AD3E58965DA20A9F571EF1651A56933748E1BF1C99E537C4E039

nuget verify -Signatures MyPackage.nupkg -Verbosity quiet

nuget verify -Signatures .\*.nupkg

nuget verify -All .\*.nupkg

```