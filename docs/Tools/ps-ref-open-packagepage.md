---
title: Open — PackagePage NuGet w programie PowerShell | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Odwołanie do polecenia programu PowerShell PackagePage Otwórz w konsoli Menedżera pakietów NuGet w programie Visual Studio.
keywords: NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, otwórz PackagePage
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5e0955e58daacf381666c676c8fcf22c698e9db6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="68dfb-104">Open — PackagePage (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="68dfb-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="68dfb-105">*Przestarzałe w 3.0 +; dostępne tylko w obrębie [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="68dfb-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="68dfb-106">Uruchamia domyślnej przeglądarki z projektu, licencji lub adresu URL programu report nadużyć dla określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="68dfb-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="68dfb-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="68dfb-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="68dfb-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="68dfb-108">Parameters</span></span>

| <span data-ttu-id="68dfb-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="68dfb-109">Parameter</span></span> | <span data-ttu-id="68dfb-110">Opis</span><span class="sxs-lookup"><span data-stu-id="68dfb-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="68dfb-111">Id</span><span class="sxs-lookup"><span data-stu-id="68dfb-111">Id</span></span> | <span data-ttu-id="68dfb-112">Identyfikator pakietu żądanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="68dfb-112">The package ID of the desired package.</span></span> <span data-ttu-id="68dfb-113">Id przełącznika sam jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="68dfb-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="68dfb-114">Wersja</span><span class="sxs-lookup"><span data-stu-id="68dfb-114">Version</span></span> | <span data-ttu-id="68dfb-115">Wersja pakietu, domyślnie używany do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="68dfb-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="68dfb-116">Źródło</span><span class="sxs-lookup"><span data-stu-id="68dfb-116">Source</span></span> | <span data-ttu-id="68dfb-117">Źródło pakietu domyślnie wybrane źródło w lokalizacji źródłowej listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="68dfb-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="68dfb-118">Licencji</span><span class="sxs-lookup"><span data-stu-id="68dfb-118">License</span></span> | <span data-ttu-id="68dfb-119">Otwiera przeglądarkę, aby adres URL licencji pakietu.</span><span class="sxs-lookup"><span data-stu-id="68dfb-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="68dfb-120">Jeśli nie - licencji - ReportAbuse określono ani, w przeglądarce zostanie otwarty adres URL projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="68dfb-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="68dfb-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="68dfb-121">ReportAbuse</span></span> | <span data-ttu-id="68dfb-122">Otwiera przeglądarkę do adresu URL nadużycia raport pakietu.</span><span class="sxs-lookup"><span data-stu-id="68dfb-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="68dfb-123">Jeśli nie - licencji - ReportAbuse określono ani, w przeglądarce zostanie otwarty adres URL projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="68dfb-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="68dfb-124">PassThru</span><span class="sxs-lookup"><span data-stu-id="68dfb-124">PassThru</span></span> | <span data-ttu-id="68dfb-125">Wyświetla adres URL; za pomocą - WhatIf do pomijania otwierania przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="68dfb-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="68dfb-126">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="68dfb-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="68dfb-127">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="68dfb-127">Common Parameters</span></span>

<span data-ttu-id="68dfb-128">`Open-PackagePage` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="68dfb-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="68dfb-129">Przykłady</span><span class="sxs-lookup"><span data-stu-id="68dfb-129">Examples</span></span>

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