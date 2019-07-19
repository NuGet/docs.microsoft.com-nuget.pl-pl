---
title: Dokumentacja programu NuGet Find-Package PowerShell
description: Dokumentacja polecenia Znajdź pakiet programu PowerShell w konsoli Menedżera pakietów NuGet w programie Visual Studio.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328220"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="abdcd-103">Find-Package (konsola menedżera pakietów w programie Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="abdcd-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="abdcd-104">*Wersja 3.0 +; w tym temacie opisano polecenie w [konsoli Menedżera pakietów](../../consume-packages/install-use-packages-powershell.md) w programie Visual Studio w systemie Windows. Aby zapoznać się z ogólnym poleceniem Znajdź pakiet programu PowerShell, zobacz [informacje dotyczące programu PowerShell PackageManagement](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="abdcd-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="abdcd-105">Pobiera zestaw pakietów zdalnych o określonym IDENTYFIKATORze lub słowach kluczowych ze źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="abdcd-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="abdcd-106">Składnia</span><span class="sxs-lookup"><span data-stu-id="abdcd-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="abdcd-107">Parametry</span><span class="sxs-lookup"><span data-stu-id="abdcd-107">Parameters</span></span>

| <span data-ttu-id="abdcd-108">Parametr</span><span class="sxs-lookup"><span data-stu-id="abdcd-108">Parameter</span></span> | <span data-ttu-id="abdcd-109">Opis</span><span class="sxs-lookup"><span data-stu-id="abdcd-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="abdcd-110">Słowa &lt;kluczowe identyfikatora&gt;</span><span class="sxs-lookup"><span data-stu-id="abdcd-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="abdcd-111">Potrzeb Słowa kluczowe, które mają być używane podczas wyszukiwania źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="abdcd-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="abdcd-112">Użyj-ExactMatch, aby zwrócić tylko te pakiety, których identyfikator pakietu pasuje do słów kluczowych.</span><span class="sxs-lookup"><span data-stu-id="abdcd-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="abdcd-113">Jeśli nie podano słów kluczowych `Find-Package` , funkcja zwraca listę 20 najważniejszych pakietów przez pobieranie lub numer określony przez-First.</span><span class="sxs-lookup"><span data-stu-id="abdcd-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="abdcd-114">Należy pamiętać, że-ID jest opcjonalne i No-op.</span><span class="sxs-lookup"><span data-stu-id="abdcd-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="abdcd-115">Source</span><span class="sxs-lookup"><span data-stu-id="abdcd-115">Source</span></span> | <span data-ttu-id="abdcd-116">Ścieżka adresu URL lub folderu dla źródła pakietu do przeszukania.</span><span class="sxs-lookup"><span data-stu-id="abdcd-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="abdcd-117">Ścieżki folderu lokalnego mogą być bezwzględne lub względne w stosunku do bieżącego folderu.</span><span class="sxs-lookup"><span data-stu-id="abdcd-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="abdcd-118">W przypadku pominięcia program `Find-Package` przeszukuje aktualnie wybrane źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="abdcd-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="abdcd-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="abdcd-119">AllVersions</span></span> | <span data-ttu-id="abdcd-120">Wyświetla wszystkie dostępne wersje każdego pakietu, a nie tylko najnowszą wersję.</span><span class="sxs-lookup"><span data-stu-id="abdcd-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="abdcd-121">pierwszego</span><span class="sxs-lookup"><span data-stu-id="abdcd-121">First</span></span> | <span data-ttu-id="abdcd-122">Liczba pakietów do zwrócenia od początku listy; wartość domyślna to 20.</span><span class="sxs-lookup"><span data-stu-id="abdcd-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="abdcd-123">Skip</span><span class="sxs-lookup"><span data-stu-id="abdcd-123">Skip</span></span> | <span data-ttu-id="abdcd-124">Pomija pierwsze &lt;pakiety int&gt; z wyświetlonej listy.</span><span class="sxs-lookup"><span data-stu-id="abdcd-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="abdcd-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="abdcd-125">IncludePrerelease</span></span> | <span data-ttu-id="abdcd-126">Zawiera pakiety wersji wstępnej w wynikach.</span><span class="sxs-lookup"><span data-stu-id="abdcd-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="abdcd-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="abdcd-127">ExactMatch</span></span> | <span data-ttu-id="abdcd-128">Określono, aby &lt;używać&gt; słów kluczowych jako identyfikatora pakietu z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="abdcd-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="abdcd-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="abdcd-129">StartWith</span></span> | <span data-ttu-id="abdcd-130">Zwraca pakiety, których identyfikator pakietu rozpoczyna &lt;się&gt;od słów kluczowych.</span><span class="sxs-lookup"><span data-stu-id="abdcd-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="abdcd-131">Żaden z tych parametrów nie akceptuje danych wejściowych potoku ani symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="abdcd-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="abdcd-132">Parametry wspólne</span><span class="sxs-lookup"><span data-stu-id="abdcd-132">Common Parameters</span></span>

<span data-ttu-id="abdcd-133">`Find-Package`Program obsługuje następujące [typowe parametry programu PowerShell](http://go.microsoft.com/fwlink/?LinkID=113216): Debugowanie, Akcja błędu, ErrorVariable, wybuforuj, niezmienna, PipelineVariable, verbose, WarningAction i WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="abdcd-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="abdcd-134">Przykłady</span><span class="sxs-lookup"><span data-stu-id="abdcd-134">Examples</span></span>

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
