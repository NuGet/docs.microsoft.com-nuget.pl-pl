---
title: Dokumentacja pakietu NuGet Open-PackagePage programu PowerShell
description: Odwołanie do polecenia programu PowerShell open-PackagePage w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0237c23d81000a1d58264cc0ab48c73d819d0e5a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328217"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="9e103-103">Open-PackagePage (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="9e103-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9e103-104">*Przestarzałe w wersji 3.0 +; dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="9e103-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="9e103-105">Uruchamia domyślną przeglądarkę z adresem URL nadużycia projektu, licencji lub raportu dla określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="9e103-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="9e103-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="9e103-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="9e103-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="9e103-107">Parameters</span></span>

| <span data-ttu-id="9e103-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="9e103-108">Parameter</span></span> | <span data-ttu-id="9e103-109">Opis</span><span class="sxs-lookup"><span data-stu-id="9e103-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9e103-110">Id</span><span class="sxs-lookup"><span data-stu-id="9e103-110">Id</span></span> | <span data-ttu-id="9e103-111">Identyfikator pakietu żądanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="9e103-111">The package ID of the desired package.</span></span> <span data-ttu-id="9e103-112">Przełącznik-ID jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="9e103-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="9e103-113">Wersja</span><span class="sxs-lookup"><span data-stu-id="9e103-113">Version</span></span> | <span data-ttu-id="9e103-114">Wersja pakietu, domyślna dla najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="9e103-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="9e103-115">Source</span><span class="sxs-lookup"><span data-stu-id="9e103-115">Source</span></span> | <span data-ttu-id="9e103-116">Źródło pakietu, które domyślnie jest wybrane źródło w liście rozwijanej Źródło.</span><span class="sxs-lookup"><span data-stu-id="9e103-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="9e103-117">Licencja</span><span class="sxs-lookup"><span data-stu-id="9e103-117">License</span></span> | <span data-ttu-id="9e103-118">Otwiera przeglądarkę w adresie URL licencji pakietu.</span><span class="sxs-lookup"><span data-stu-id="9e103-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="9e103-119">Jeśli nie określono parametru-License ani-ReportAbuse, przeglądarka otworzy adres URL projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="9e103-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="9e103-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="9e103-120">ReportAbuse</span></span> | <span data-ttu-id="9e103-121">Otwiera przeglądarkę w adresie URL nadużycia raportu pakietu.</span><span class="sxs-lookup"><span data-stu-id="9e103-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="9e103-122">Jeśli nie określono parametru-License ani-ReportAbuse, przeglądarka otworzy adres URL projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="9e103-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="9e103-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="9e103-123">PassThru</span></span> | <span data-ttu-id="9e103-124">Wyświetla adres URL; Użyj with-WhatIf, aby pominąć otwieranie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="9e103-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="9e103-125">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="9e103-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="9e103-126">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="9e103-126">Common Parameters</span></span>

<span data-ttu-id="9e103-127">`Open-PackagePage`Program obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, Akcja błędu, ErrorVariable, wybuforuj, niezmienna, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9e103-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="9e103-128">Przykłady</span><span class="sxs-lookup"><span data-stu-id="9e103-128">Examples</span></span>

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