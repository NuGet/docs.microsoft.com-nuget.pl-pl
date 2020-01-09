---
title: Dokumentacja programu NuGet Find-Package PowerShell
description: Dokumentacja polecenia Znajdź pakiet programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4118b5a38f80a2300b3945738315d56bda096f9a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384636"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="65d67-103">Find-Package (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="65d67-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="65d67-104">*Wersja 3.0 +; w tym temacie opisano polecenie w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows. Aby zapoznać się z ogólnym poleceniem Znajdź pakiet programu PowerShell, zobacz [informacje dotyczące programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="65d67-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="65d67-105">Pobiera zestaw pakietów zdalnych o określonym IDENTYFIKATORze lub słowach kluczowych ze źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="65d67-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="65d67-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="65d67-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="65d67-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="65d67-107">Parameters</span></span>

| <span data-ttu-id="65d67-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="65d67-108">Parameter</span></span> | <span data-ttu-id="65d67-109">Opis</span><span class="sxs-lookup"><span data-stu-id="65d67-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="65d67-110">&gt; &lt;identyfikatorów słów kluczowych</span><span class="sxs-lookup"><span data-stu-id="65d67-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="65d67-111">Potrzeb Słowa kluczowe, które mają być używane podczas wyszukiwania źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="65d67-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="65d67-112">Użyj-ExactMatch, aby zwrócić tylko te pakiety, których identyfikator pakietu pasuje do słów kluczowych.</span><span class="sxs-lookup"><span data-stu-id="65d67-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="65d67-113">Jeśli nie podano słów kluczowych, `Find-Package` zwraca listę 20 najważniejszych pakietów przez pobieranie lub numer określony przez-First.</span><span class="sxs-lookup"><span data-stu-id="65d67-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="65d67-114">Należy pamiętać, że-ID jest opcjonalne i No-op.</span><span class="sxs-lookup"><span data-stu-id="65d67-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="65d67-115">Obiekt źródłowy</span><span class="sxs-lookup"><span data-stu-id="65d67-115">Source</span></span> | <span data-ttu-id="65d67-116">Ścieżka adresu URL lub folderu dla źródła pakietu do przeszukania.</span><span class="sxs-lookup"><span data-stu-id="65d67-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="65d67-117">Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="65d67-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="65d67-118">W przypadku pominięcia `Find-Package` przeszukuje aktualnie wybrane źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="65d67-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="65d67-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="65d67-119">AllVersions</span></span> | <span data-ttu-id="65d67-120">Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="65d67-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="65d67-121">Pierwsze</span><span class="sxs-lookup"><span data-stu-id="65d67-121">First</span></span> | <span data-ttu-id="65d67-122">Liczba pakietów do zwrócenia od początku listy; wartość domyślna to 20.</span><span class="sxs-lookup"><span data-stu-id="65d67-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="65d67-123">Skip</span><span class="sxs-lookup"><span data-stu-id="65d67-123">Skip</span></span> | <span data-ttu-id="65d67-124">Pomija pierwsze &lt;pakietów&gt; int z wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="65d67-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="65d67-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="65d67-125">IncludePrerelease</span></span> | <span data-ttu-id="65d67-126">Zawiera pakiety wersji wstępnej w wynikach.</span><span class="sxs-lookup"><span data-stu-id="65d67-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="65d67-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="65d67-127">ExactMatch</span></span> | <span data-ttu-id="65d67-128">Określono używanie &lt;słów&gt; kluczowych jako identyfikatora pakietu z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="65d67-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="65d67-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="65d67-129">StartWith</span></span> | <span data-ttu-id="65d67-130">Zwraca pakiety, których identyfikator pakietu rozpoczyna się od &lt;słów kluczowych&gt;.</span><span class="sxs-lookup"><span data-stu-id="65d67-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="65d67-131">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="65d67-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="65d67-132">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="65d67-132">Common Parameters</span></span>

<span data-ttu-id="65d67-133">`Find-Package` obsługuje następujące [typowe parametry programu PowerShell](https://go.microsoft.com/fwlink/?LinkID=113216): debugowanie, Akcja błędu, ErrorVariable, buforowanie, subvariable, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="65d67-133">`Find-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="65d67-134">Przykłady</span><span class="sxs-lookup"><span data-stu-id="65d67-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
