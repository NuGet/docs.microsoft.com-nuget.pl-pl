---
title: Informacje o programie PowerShell Find-Package NuGet
description: Informacje dotyczące Find-Package programu PowerShell w konsoli Menedżer pakietów NuGet w programie Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901762"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="313d4-103">Find-Package (konsola Menedżer pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="313d4-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="313d4-104">*Wersja 3.0 lub nowsza; W tym temacie opisano polecenie w konsoli [Menedżer pakietów w](../../consume-packages/install-use-packages-powershell.md) Visual Studio w systemie Windows. Aby uzyskać ogólne polecenie Find-Package Programu PowerShell, zobacz informacje dotyczące polecenia [PackageManagement programu PowerShell.](/powershell/module/packagemanagement)*</span><span class="sxs-lookup"><span data-stu-id="313d4-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="313d4-105">Pobiera zestaw pakietów zdalnych z określonym identyfikatorem lub słowami kluczowymi ze źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="313d4-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="313d4-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="313d4-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="313d4-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="313d4-107">Parameters</span></span>

| <span data-ttu-id="313d4-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="313d4-108">Parameter</span></span> | <span data-ttu-id="313d4-109">Opis</span><span class="sxs-lookup"><span data-stu-id="313d4-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="313d4-110">Słowa kluczowe &lt; identyfikatora&gt;</span><span class="sxs-lookup"><span data-stu-id="313d4-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="313d4-111">(Wymagane) Słowa kluczowe do użycia podczas wyszukiwania źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="313d4-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="313d4-112">Użyj -ExactMatch, aby zwrócić tylko te pakiety, których identyfikator pakietu jest taki sam jak słowa kluczowe.</span><span class="sxs-lookup"><span data-stu-id="313d4-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="313d4-113">Jeśli nie podano żadnych słów kluczowych, program zwraca listę 20 pierwszych pakietów według plików do pobrania lub liczbę `Find-Package` określoną przez wartość -First.</span><span class="sxs-lookup"><span data-stu-id="313d4-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="313d4-114">Pamiętaj, że parametr -Id jest opcjonalny i nie jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="313d4-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="313d4-115">Element źródłowy</span><span class="sxs-lookup"><span data-stu-id="313d4-115">Source</span></span> | <span data-ttu-id="313d4-116">Adres URL lub ścieżka folderu dla źródła pakietu do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="313d4-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="313d4-117">Ścieżki folderów lokalnych mogą być bezwzględne lub względne względem bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="313d4-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="313d4-118">W przypadku pominięcia `Find-Package` program wyszukuje aktualnie wybrane źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="313d4-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="313d4-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="313d4-119">AllVersions</span></span> | <span data-ttu-id="313d4-120">Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="313d4-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="313d4-121">Pierwsze</span><span class="sxs-lookup"><span data-stu-id="313d4-121">First</span></span> | <span data-ttu-id="313d4-122">Liczba pakietów, które mają być zwracane od początku listy; Wartość domyślna to 20.</span><span class="sxs-lookup"><span data-stu-id="313d4-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="313d4-123">Pomiń</span><span class="sxs-lookup"><span data-stu-id="313d4-123">Skip</span></span> | <span data-ttu-id="313d4-124">Pomija pierwsze pakiety &lt; int &gt; z wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="313d4-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="313d4-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="313d4-125">IncludePrerelease</span></span> | <span data-ttu-id="313d4-126">Zawiera pakiety wytłaczania wstępnego w wynikach.</span><span class="sxs-lookup"><span data-stu-id="313d4-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="313d4-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="313d4-127">ExactMatch</span></span> | <span data-ttu-id="313d4-128">Określana w celu &lt; &gt; używania słów kluczowych jako identyfikatora pakietu zróżnicowego wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="313d4-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="313d4-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="313d4-129">StartWith</span></span> | <span data-ttu-id="313d4-130">Zwraca pakiety, których identyfikator pakietu zaczyna się od &lt; słów kluczowych &gt; .</span><span class="sxs-lookup"><span data-stu-id="313d4-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="313d4-131">Żaden z tych parametrów nie akceptuje znaków wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="313d4-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="313d4-132">Typowe parametry</span><span class="sxs-lookup"><span data-stu-id="313d4-132">Common Parameters</span></span>

<span data-ttu-id="313d4-133">`Find-Package` obsługuje następujące typowe [parametry programu PowerShell:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="313d4-133">`Find-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="313d4-134">Przykłady</span><span class="sxs-lookup"><span data-stu-id="313d4-134">Examples</span></span>

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