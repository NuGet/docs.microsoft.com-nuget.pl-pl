---
title: Open — PackagePage NuGet w programie PowerShell
description: Odwołanie do polecenia programu PowerShell PackagePage Otwórz w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: df4bea390105a7e3fc5d2abd476f2908d92bbcf8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="ea433-103">Open — PackagePage (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="ea433-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ea433-104">*Przestarzałe w 3.0 +; dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="ea433-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ea433-105">Uruchamia domyślnej przeglądarki z projektu, licencji lub adresu URL programu report nadużyć dla określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="ea433-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="ea433-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="ea433-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ea433-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="ea433-107">Parameters</span></span>

| <span data-ttu-id="ea433-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="ea433-108">Parameter</span></span> | <span data-ttu-id="ea433-109">Opis</span><span class="sxs-lookup"><span data-stu-id="ea433-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ea433-110">Id</span><span class="sxs-lookup"><span data-stu-id="ea433-110">Id</span></span> | <span data-ttu-id="ea433-111">Identyfikator pakietu żądanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="ea433-111">The package ID of the desired package.</span></span> <span data-ttu-id="ea433-112">Id przełącznika sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="ea433-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="ea433-113">Wersja</span><span class="sxs-lookup"><span data-stu-id="ea433-113">Version</span></span> | <span data-ttu-id="ea433-114">Wersja pakietu, domyślnie używany do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="ea433-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="ea433-115">Źródło</span><span class="sxs-lookup"><span data-stu-id="ea433-115">Source</span></span> | <span data-ttu-id="ea433-116">Źródło pakietu domyślnie wybrane źródło w lokalizacji źródłowej listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="ea433-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="ea433-117">Licencji</span><span class="sxs-lookup"><span data-stu-id="ea433-117">License</span></span> | <span data-ttu-id="ea433-118">Otwiera przeglądarkę, aby adres URL licencji pakietu.</span><span class="sxs-lookup"><span data-stu-id="ea433-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="ea433-119">Jeśli nie - licencji - ReportAbuse określono ani, w przeglądarce zostanie otwarty adres URL projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="ea433-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="ea433-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="ea433-120">ReportAbuse</span></span> | <span data-ttu-id="ea433-121">Otwiera przeglądarkę do adresu URL nadużycia raport pakietu.</span><span class="sxs-lookup"><span data-stu-id="ea433-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="ea433-122">Jeśli nie - licencji - ReportAbuse określono ani, w przeglądarce zostanie otwarty adres URL projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="ea433-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="ea433-123">Przekazywanie</span><span class="sxs-lookup"><span data-stu-id="ea433-123">PassThru</span></span> | <span data-ttu-id="ea433-124">Wyświetla adres URL; za pomocą - WhatIf do pomijania otwierania przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="ea433-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="ea433-125">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="ea433-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ea433-126">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="ea433-126">Common Parameters</span></span>

<span data-ttu-id="ea433-127">`Open-PackagePage` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="ea433-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ea433-128">Przykłady</span><span class="sxs-lookup"><span data-stu-id="ea433-128">Examples</span></span>

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