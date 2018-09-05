---
title: Dokumentacja programu PowerShell Znajdź — pakiet NuGet
description: Odniesienie do polecenia PowerShell Znajdź pakiet w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: c6797e3778c7095a9abfc6cd87e2337313988c20
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550981"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="d0cae-103">Find-Package (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d0cae-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d0cae-104">*W wersji 3.0 +; w tym temacie opisano polecenia w ramach [Konsola Menedżera pakietów NuGet](package-manager-console.md) w programie Visual Studio na Windows. Ogólne polecenia programu PowerShell Znajdź-Package, zobacz [dokumentacja programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="d0cae-104">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="d0cae-105">Pobiera zbiór pakiety zdalne przy użyciu określonego Identyfikatora lub słowa kluczowe ze źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="d0cae-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="d0cae-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="d0cae-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="d0cae-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="d0cae-107">Parameters</span></span>

| <span data-ttu-id="d0cae-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="d0cae-108">Parameter</span></span> | <span data-ttu-id="d0cae-109">Opis</span><span class="sxs-lookup"><span data-stu-id="d0cae-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d0cae-110">Identyfikator &lt;słów kluczowych&gt;</span><span class="sxs-lookup"><span data-stu-id="d0cae-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="d0cae-111">(Wymagane) Słowa kluczowe do użycia podczas wyszukiwania źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="d0cae-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="d0cae-112">Użyj - ExactMatch, aby zwrócić tylko pakiety o identyfikatorze pakietu dopasowuje słowa kluczowe.</span><span class="sxs-lookup"><span data-stu-id="d0cae-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="d0cae-113">Jeśli zostanie podany żadnych słów kluczowych, `Find-Package` zwraca listę pakietów 20 najpopularniejszych przez pliki do pobrania lub liczba określone przez — najpierw.</span><span class="sxs-lookup"><span data-stu-id="d0cae-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="d0cae-114">Należy pamiętać, że - Id jest opcjonalna i pusta.</span><span class="sxs-lookup"><span data-stu-id="d0cae-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="d0cae-115">Źródło</span><span class="sxs-lookup"><span data-stu-id="d0cae-115">Source</span></span> | <span data-ttu-id="d0cae-116">Adres URL lub folder ścieżka do źródła pakietu do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="d0cae-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="d0cae-117">Ścieżki folderu lokalnego, może być ścieżką bezwzględną, lub względną do bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="d0cae-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="d0cae-118">W przypadku pominięcia `Find-Package` przeszukuje źródło obecnie wybranego pakietu.</span><span class="sxs-lookup"><span data-stu-id="d0cae-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="d0cae-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="d0cae-119">AllVersions</span></span> | <span data-ttu-id="d0cae-120">Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="d0cae-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="d0cae-121">pierwszy</span><span class="sxs-lookup"><span data-stu-id="d0cae-121">First</span></span> | <span data-ttu-id="d0cae-122">Liczba pakietów do zwrócenia z początku listy; Wartość domyślna to 20.</span><span class="sxs-lookup"><span data-stu-id="d0cae-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="d0cae-123">Skip</span><span class="sxs-lookup"><span data-stu-id="d0cae-123">Skip</span></span> | <span data-ttu-id="d0cae-124">Pomija pierwszy &lt;int&gt; pakiety z wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="d0cae-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="d0cae-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="d0cae-125">IncludePrerelease</span></span> | <span data-ttu-id="d0cae-126">Obejmuje pakiety w wersjach wstępnych, w wynikach.</span><span class="sxs-lookup"><span data-stu-id="d0cae-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="d0cae-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="d0cae-127">ExactMatch</span></span> | <span data-ttu-id="d0cae-128">Określony do użycia &lt;słowa kluczowe&gt; jako identyfikator pakietu jest wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d0cae-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="d0cae-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="d0cae-129">StartWith</span></span> | <span data-ttu-id="d0cae-130">Zwraca pakiety pakiet, którego identyfikator rozpoczyna się od &lt;słowa kluczowe&gt;.</span><span class="sxs-lookup"><span data-stu-id="d0cae-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="d0cae-131">Żaden z tych parametrów akceptuje znaków potoku danych wejściowych lub symbol wieloznaczny.</span><span class="sxs-lookup"><span data-stu-id="d0cae-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d0cae-132">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="d0cae-132">Common Parameters</span></span>

<span data-ttu-id="d0cae-133">`Find-Package` obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja w przypadku błędu, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d0cae-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d0cae-134">Przykłady</span><span class="sxs-lookup"><span data-stu-id="d0cae-134">Examples</span></span>

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
