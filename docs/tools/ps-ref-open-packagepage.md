---
title: Dokumentacja programu PowerShell NuGet Open-PackagePage
description: Dokumentacja polecenia PowerShell PackagePage otwarcie w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fd738f15b461051c4e9413b3035456c687979b97
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842263"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="fd7a3-103">Open-PackagePage (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="fd7a3-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="fd7a3-104">*Przestarzałe w 3.0 +; dostępne tylko w obrębie [Konsola Menedżera pakietów](package-manager-console.md) w programie Visual Studio na Windows.*</span><span class="sxs-lookup"><span data-stu-id="fd7a3-104">*Deprecated in 3.0+; available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="fd7a3-105">Uruchamia domyślną przeglądarkę z projektem, licencji lub adres URL do raportu nadużyć dla określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="fd7a3-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="fd7a3-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="fd7a3-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="fd7a3-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="fd7a3-107">Parameters</span></span>

| <span data-ttu-id="fd7a3-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="fd7a3-108">Parameter</span></span> | <span data-ttu-id="fd7a3-109">Opis</span><span class="sxs-lookup"><span data-stu-id="fd7a3-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fd7a3-110">Id</span><span class="sxs-lookup"><span data-stu-id="fd7a3-110">Id</span></span> | <span data-ttu-id="fd7a3-111">Identyfikator pakietu żądanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="fd7a3-111">The package ID of the desired package.</span></span> <span data-ttu-id="fd7a3-112">— Identyfikator samym przełączniku jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="fd7a3-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="fd7a3-113">Wersja</span><span class="sxs-lookup"><span data-stu-id="fd7a3-113">Version</span></span> | <span data-ttu-id="fd7a3-114">Wersja pakietu, ustawiając domyślnie do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="fd7a3-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="fd7a3-115">Source</span><span class="sxs-lookup"><span data-stu-id="fd7a3-115">Source</span></span> | <span data-ttu-id="fd7a3-116">Źródło pakietu przyjęty wybranego źródła w źródle listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="fd7a3-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="fd7a3-117">Licencja</span><span class="sxs-lookup"><span data-stu-id="fd7a3-117">License</span></span> | <span data-ttu-id="fd7a3-118">Zostanie otwarta w przeglądarce adres URL licencji pakietu.</span><span class="sxs-lookup"><span data-stu-id="fd7a3-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="fd7a3-119">Jeśli określono - licencji ani - ReportAbuse przeglądarki otwiera adres URL projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="fd7a3-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="fd7a3-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="fd7a3-120">ReportAbuse</span></span> | <span data-ttu-id="fd7a3-121">Zostanie otwarta w przeglądarce adres URL nadużyć raport pakietu.</span><span class="sxs-lookup"><span data-stu-id="fd7a3-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="fd7a3-122">Jeśli określono - licencji ani - ReportAbuse przeglądarki otwiera adres URL projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="fd7a3-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="fd7a3-123">Przekazywanie</span><span class="sxs-lookup"><span data-stu-id="fd7a3-123">PassThru</span></span> | <span data-ttu-id="fd7a3-124">Wyświetla adres URL; za pomocą - WhatIf do pomijania otwierania przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="fd7a3-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="fd7a3-125">Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.</span><span class="sxs-lookup"><span data-stu-id="fd7a3-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="fd7a3-126">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="fd7a3-126">Common Parameters</span></span>

<span data-ttu-id="fd7a3-127">`Open-PackagePage` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="fd7a3-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="fd7a3-128">Przykłady</span><span class="sxs-lookup"><span data-stu-id="fd7a3-128">Examples</span></span>

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