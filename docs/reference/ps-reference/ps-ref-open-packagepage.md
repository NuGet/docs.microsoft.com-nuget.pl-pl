---
title: Dokumentacja programu NuGet Open-PackagePage PowerShell
description: Informacje dotyczące Open-PackagePage polecenia programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ba90e09c017ec66d73c35a60025474bc77cf65a7
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238065"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="2494b-103">Open-PackagePage (konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="2494b-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="2494b-104">*Przestarzałe w wersji 3.0 +; dostępne tylko w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows.*</span><span class="sxs-lookup"><span data-stu-id="2494b-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="2494b-105">Uruchamia domyślną przeglądarkę z adresem URL nadużycia projektu, licencji lub raportu dla określonego pakietu.</span><span class="sxs-lookup"><span data-stu-id="2494b-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="2494b-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="2494b-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="2494b-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="2494b-107">Parameters</span></span>

| <span data-ttu-id="2494b-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="2494b-108">Parameter</span></span> | <span data-ttu-id="2494b-109">Opis</span><span class="sxs-lookup"><span data-stu-id="2494b-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2494b-110">Id</span><span class="sxs-lookup"><span data-stu-id="2494b-110">Id</span></span> | <span data-ttu-id="2494b-111">Identyfikator pakietu żądanego pakietu.</span><span class="sxs-lookup"><span data-stu-id="2494b-111">The package ID of the desired package.</span></span> <span data-ttu-id="2494b-112">Przełącznik-ID jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="2494b-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="2494b-113">Wersja</span><span class="sxs-lookup"><span data-stu-id="2494b-113">Version</span></span> | <span data-ttu-id="2494b-114">Wersja pakietu, domyślna dla najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="2494b-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="2494b-115">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="2494b-115">Source</span></span> | <span data-ttu-id="2494b-116">Źródło pakietu, które domyślnie jest wybrane źródło w liście rozwijanej Źródło.</span><span class="sxs-lookup"><span data-stu-id="2494b-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="2494b-117">Licencja</span><span class="sxs-lookup"><span data-stu-id="2494b-117">License</span></span> | <span data-ttu-id="2494b-118">Otwiera przeglądarkę w adresie URL licencji pakietu.</span><span class="sxs-lookup"><span data-stu-id="2494b-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="2494b-119">Jeśli nie określono parametru-License ani-ReportAbuse, przeglądarka otworzy adres URL projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="2494b-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="2494b-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="2494b-120">ReportAbuse</span></span> | <span data-ttu-id="2494b-121">Otwiera przeglądarkę w adresie URL nadużycia raportu pakietu.</span><span class="sxs-lookup"><span data-stu-id="2494b-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="2494b-122">Jeśli nie określono parametru-License ani-ReportAbuse, przeglądarka otworzy adres URL projektu pakietu.</span><span class="sxs-lookup"><span data-stu-id="2494b-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="2494b-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="2494b-123">PassThru</span></span> | <span data-ttu-id="2494b-124">Wyświetla adres URL; Użyj with-WhatIf, aby pominąć otwieranie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="2494b-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="2494b-125">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="2494b-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="2494b-126">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="2494b-126">Common Parameters</span></span>

<span data-ttu-id="2494b-127">`Open-PackagePage` obsługuje następujące [typowe parametry programu PowerShell](/powershell/module/microsoft.powershell.core/about/about_commonparameters): debugowanie, Akcja błędu, ErrorVariable, wybuforuj, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="2494b-127">`Open-PackagePage` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="2494b-128">Przykłady</span><span class="sxs-lookup"><span data-stu-id="2494b-128">Examples</span></span>

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