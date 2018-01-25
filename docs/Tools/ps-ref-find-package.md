---
title: "Znajdź pakiet NuGet w programie PowerShell | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Odwołanie do polecenia programu PowerShell Znajdź pakiet w konsoli Menedżera pakietów NuGet w programie Visual Studio."
keywords: "NuGet konsoli Menedżera pakietów, poleceń programu NuGet Powershell NuGet w programie PowerShell, Znajdź pakiet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 47b8420cc49d0a76709cf3268af69fcff310d165
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="842b0-104">Znajdź pakiet (Konsola Menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="842b0-104">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="842b0-105">*W wersji 3.0 +; w tym temacie opisano polecenia w [Konsola Menedżera pakietów NuGet](Package-Manager-Console.md) w programie Visual Studio w systemie Windows. Ogólny polecenia pakiet Znajdź PowerShell, zobacz [odwołania programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="842b0-105">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="842b0-106">Pobiera zestaw pakietów zdalnych z określonym Identyfikatorem lub słowa kluczowe w źródle pakietów.</span><span class="sxs-lookup"><span data-stu-id="842b0-106">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="842b0-107">Składnia</span><span class="sxs-lookup"><span data-stu-id="842b0-107">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="842b0-108">Parametry</span><span class="sxs-lookup"><span data-stu-id="842b0-108">Parameters</span></span>

| <span data-ttu-id="842b0-109">Parametr</span><span class="sxs-lookup"><span data-stu-id="842b0-109">Parameter</span></span> | <span data-ttu-id="842b0-110">Opis</span><span class="sxs-lookup"><span data-stu-id="842b0-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="842b0-111">Identyfikator &lt;słowa kluczowe&gt;</span><span class="sxs-lookup"><span data-stu-id="842b0-111">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="842b0-112">(Wymagane) Słowa kluczowe używane podczas wyszukiwania w źródle pakietów.</span><span class="sxs-lookup"><span data-stu-id="842b0-112">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="842b0-113">Użyj - ExactMatch mają być zwracane tylko pakiety o identyfikatorze pakietu pasuje słów kluczowych.</span><span class="sxs-lookup"><span data-stu-id="842b0-113">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="842b0-114">Jeśli podano słów kluczowych, `Find-Package` zwraca listę pakietów pierwsza 20. wg pliki do pobrania lub numer określony przez — jako pierwszy.</span><span class="sxs-lookup"><span data-stu-id="842b0-114">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="842b0-115">Należy pamiętać, że - Id jest opcjonalna i zerowa.</span><span class="sxs-lookup"><span data-stu-id="842b0-115">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="842b0-116">Źródło</span><span class="sxs-lookup"><span data-stu-id="842b0-116">Source</span></span> | <span data-ttu-id="842b0-117">Adres URL lub folder ścieżka do źródła pakietu do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="842b0-117">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="842b0-118">Ścieżki folderu lokalnego może być bezwzględny, lub względem bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="842b0-118">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="842b0-119">Pominięcie `Find-Package` wyszukiwania w obecnie wybranym źródle pakietów.</span><span class="sxs-lookup"><span data-stu-id="842b0-119">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="842b0-120">AllVersions</span><span class="sxs-lookup"><span data-stu-id="842b0-120">AllVersions</span></span> | <span data-ttu-id="842b0-121">Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="842b0-121">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="842b0-122">pierwszy</span><span class="sxs-lookup"><span data-stu-id="842b0-122">First</span></span> | <span data-ttu-id="842b0-123">Liczba pakietów do zwrócenia z początku listy; Wartość domyślna to 20.</span><span class="sxs-lookup"><span data-stu-id="842b0-123">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="842b0-124">Skip</span><span class="sxs-lookup"><span data-stu-id="842b0-124">Skip</span></span> | <span data-ttu-id="842b0-125">Pominięto pierwszy &lt;int&gt; pakiety z wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="842b0-125">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="842b0-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="842b0-126">IncludePrerelease</span></span> | <span data-ttu-id="842b0-127">Zawiera pakiety wersji wstępnej w wynikach.</span><span class="sxs-lookup"><span data-stu-id="842b0-127">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="842b0-128">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="842b0-128">ExactMatch</span></span> | <span data-ttu-id="842b0-129">Określona do użycia &lt;słowa kluczowe&gt; jako identyfikatora pakietu z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="842b0-129">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="842b0-130">StartWith</span><span class="sxs-lookup"><span data-stu-id="842b0-130">StartWith</span></span> | <span data-ttu-id="842b0-131">Zwraca pakiety pakiet, którego rozpoczyna się od Identyfikatora &lt;słowa kluczowe&gt;.</span><span class="sxs-lookup"><span data-stu-id="842b0-131">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="842b0-132">Żaden z tych parametrów przyjąć potoku dane wejściowe lub symbolu wieloznacznego znaków.</span><span class="sxs-lookup"><span data-stu-id="842b0-132">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="842b0-133">Wspólne parametry</span><span class="sxs-lookup"><span data-stu-id="842b0-133">Common Parameters</span></span>

<span data-ttu-id="842b0-134">`Find-Package`obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): debugowania, akcja błędu ErrorVariable, OutBuffer, OutVariable, PipelineVariable, pełne, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="842b0-134">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="842b0-135">Przykłady</span><span class="sxs-lookup"><span data-stu-id="842b0-135">Examples</span></span>

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
