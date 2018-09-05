---
title: Dokumentacja programu PowerShell NuGet Open-PackagePage
description: Dokumentacja polecenia PowerShell PackagePage otwarcie w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0325aa4ddd718a901dd6a09cdf86cae260e326ab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547171"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="d50e1-103">Open-PackagePage (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d50e1-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d50e1-104">*Przestarzałe w 3.0 +; dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio na Windows.*</span><span class="sxs-lookup"><span data-stu-id="d50e1-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="d50e1-105">Uruchamia domyślną przeglądarkę z projektem, licencji lub adres URL do raportu nadużyć dla określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="d50e1-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="d50e1-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="d50e1-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="d50e1-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="d50e1-107">Parameters</span></span>

| <span data-ttu-id="d50e1-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="d50e1-108">Parameter</span></span> | <span data-ttu-id="d50e1-109">Opis</span><span class="sxs-lookup"><span data-stu-id="d50e1-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d50e1-110">Id</span><span class="sxs-lookup"><span data-stu-id="d50e1-110">Id</span></span> | <span data-ttu-id="d50e1-111">Identyfikator pakietu żądanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="d50e1-111">The package ID of the desired package.</span></span> <span data-ttu-id="d50e1-112">— Identyfikator samym przełączniku jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="d50e1-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="d50e1-113">Wersja</span><span class="sxs-lookup"><span data-stu-id="d50e1-113">Version</span></span> | <span data-ttu-id="d50e1-114">Wersja pakietu, ustawiając domyślnie do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="d50e1-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="d50e1-115">Źródło</span><span class="sxs-lookup"><span data-stu-id="d50e1-115">Source</span></span> | <span data-ttu-id="d50e1-116">Źródło pakietu przyjęty wybranego źródła w źródle listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d50e1-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="d50e1-117">Licencja</span><span class="sxs-lookup"><span data-stu-id="d50e1-117">License</span></span> | <span data-ttu-id="d50e1-118">Zostanie otwarta w przeglądarce adres URL licencji pakietu.</span><span class="sxs-lookup"><span data-stu-id="d50e1-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="d50e1-119">Jeśli określono - licencji ani - ReportAbuse przeglądarki otwiera adres URL projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="d50e1-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="d50e1-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="d50e1-120">ReportAbuse</span></span> | <span data-ttu-id="d50e1-121">Zostanie otwarta w przeglądarce adres URL nadużyć raport pakietu.</span><span class="sxs-lookup"><span data-stu-id="d50e1-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="d50e1-122">Jeśli określono - licencji ani - ReportAbuse przeglądarki otwiera adres URL projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="d50e1-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="d50e1-123">Przekazywanie</span><span class="sxs-lookup"><span data-stu-id="d50e1-123">PassThru</span></span> | <span data-ttu-id="d50e1-124">Wyświetla adres URL; za pomocą - WhatIf do pomijania otwierania przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="d50e1-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="d50e1-125">Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.</span><span class="sxs-lookup"><span data-stu-id="d50e1-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d50e1-126">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="d50e1-126">Common Parameters</span></span>

<span data-ttu-id="d50e1-127">`Open-PackagePage` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d50e1-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d50e1-128">Przykłady</span><span class="sxs-lookup"><span data-stu-id="d50e1-128">Examples</span></span>

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```