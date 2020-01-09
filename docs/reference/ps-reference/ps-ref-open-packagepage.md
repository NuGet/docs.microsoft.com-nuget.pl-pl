---
title: Dokumentacja pakietu NuGet Open-PackagePage programu PowerShell
description: Odwołanie do polecenia programu PowerShell open-PackagePage w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39199ebfc37756ed40158a1c07afca7709067350
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384431"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="b4619-103">Open-PackagePage (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="b4619-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b4619-104">*Przestarzałe w wersji 3.0 +; dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="b4619-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="b4619-105">Uruchamia domyślną przeglądarkę z adresem URL nadużycia projektu, licencji lub raportu dla określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="b4619-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="b4619-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="b4619-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b4619-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="b4619-107">Parameters</span></span>

| <span data-ttu-id="b4619-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="b4619-108">Parameter</span></span> | <span data-ttu-id="b4619-109">Opis</span><span class="sxs-lookup"><span data-stu-id="b4619-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b4619-110">Id</span><span class="sxs-lookup"><span data-stu-id="b4619-110">Id</span></span> | <span data-ttu-id="b4619-111">Identyfikator pakietu żądanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="b4619-111">The package ID of the desired package.</span></span> <span data-ttu-id="b4619-112">Przełącznik-ID jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="b4619-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="b4619-113">Wersja</span><span class="sxs-lookup"><span data-stu-id="b4619-113">Version</span></span> | <span data-ttu-id="b4619-114">Wersja pakietu, domyślna dla najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="b4619-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="b4619-115">Obiekt źródłowy</span><span class="sxs-lookup"><span data-stu-id="b4619-115">Source</span></span> | <span data-ttu-id="b4619-116">Źródło pakietu, które domyślnie jest wybrane źródło w liście rozwijanej Źródło.</span><span class="sxs-lookup"><span data-stu-id="b4619-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="b4619-117">Licencja</span><span class="sxs-lookup"><span data-stu-id="b4619-117">License</span></span> | <span data-ttu-id="b4619-118">Otwiera przeglądarkę w adresie URL licencji pakietu.</span><span class="sxs-lookup"><span data-stu-id="b4619-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="b4619-119">Jeśli nie określono parametru-License ani-ReportAbuse, przeglądarka otworzy adres URL projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="b4619-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="b4619-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="b4619-120">ReportAbuse</span></span> | <span data-ttu-id="b4619-121">Otwiera przeglądarkę w adresie URL nadużycia raportu pakietu.</span><span class="sxs-lookup"><span data-stu-id="b4619-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="b4619-122">Jeśli nie określono parametru-License ani-ReportAbuse, przeglądarka otworzy adres URL projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="b4619-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="b4619-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="b4619-123">PassThru</span></span> | <span data-ttu-id="b4619-124">Wyświetla adres URL; Użyj with-WhatIf, aby pominąć otwieranie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="b4619-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="b4619-125">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="b4619-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b4619-126">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="b4619-126">Common Parameters</span></span>

<span data-ttu-id="b4619-127">`Open-PackagePage` obsługuje następujące [typowe parametry programu PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debugowanie, Akcja błędu, ErrorVariable, buforowanie, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b4619-127">`Open-PackagePage` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b4619-128">Przykłady</span><span class="sxs-lookup"><span data-stu-id="b4619-128">Examples</span></span>

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