---
title: Obsługa nuGet dla Visual Studio Project System
description: Integracja programu NuGet z Visual Studio projektu dla typów projektów innych firm.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 9f1ddfd20835cc3a0f9af40a8b4e712c218b31bc
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901411"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="eb1a7-103">Obsługa nuGet dla Visual Studio projektu</span><span class="sxs-lookup"><span data-stu-id="eb1a7-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="eb1a7-104">Aby obsługiwać typy projektów innych firm w programie Visual Studio, nuGet 3.x+ obsługuje system [Common Project System (CPS),](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)a nuGet 3.2+ obsługuje również systemy projektów inne niż CPS.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="eb1a7-105">Aby zintegrować program z programem NuGet, system projektu musi anonsować własną obsługę wszystkich możliwości projektu opisanych w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="eb1a7-106">Nie deklaruj możliwości, których w rzeczywistości nie ma w projekcie ze względu na umożliwienie instalowania pakietów w projekcie.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="eb1a7-107">Wiele funkcji Visual Studio i innych rozszerzeń zależy od możliwości projektu oprócz klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="eb1a7-108">Fałszywe reklamowanie możliwości projektu może doprowadzić do awarii tych składników i pogorszenia jakości obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="eb1a7-109">Anonsowanie możliwości projektu</span><span class="sxs-lookup"><span data-stu-id="eb1a7-109">Advertise project capabilities</span></span>

<span data-ttu-id="eb1a7-110">Klient NuGet określa, które pakiety są zgodne z typem projektu, na podstawie możliwości projektu [,](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)zgodnie z opisem w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="eb1a7-111">Możliwość</span><span class="sxs-lookup"><span data-stu-id="eb1a7-111">Capability</span></span> | <span data-ttu-id="eb1a7-112">Opis</span><span class="sxs-lookup"><span data-stu-id="eb1a7-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eb1a7-113">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="eb1a7-113">AssemblyReferences</span></span> | <span data-ttu-id="eb1a7-114">Wskazuje, że projekt obsługuje odwołania do zestawu (inne niż WinRTReferences).</span><span class="sxs-lookup"><span data-stu-id="eb1a7-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="eb1a7-115">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="eb1a7-115">DeclaredSourceItems</span></span> | <span data-ttu-id="eb1a7-116">Wskazuje, że projekt jest typowym projektem MSBuild (nie DNX), ponieważ deklaruje elementy źródłowe w samym projekcie.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="eb1a7-117">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="eb1a7-117">UserSourceItems</span></span>|<span data-ttu-id="eb1a7-118">Wskazuje, że użytkownik może dodawać dowolne pliki do swojego projektu.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="eb1a7-119">W przypadku systemów projektów opartych na systemie CPS szczegóły implementacji możliwości projektu opisanych w pozostałej części tej sekcji zostały wykonane za Ciebie.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="eb1a7-120">Zobacz [deklarowanie możliwości projektu w projektach CPS.](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project)</span><span class="sxs-lookup"><span data-stu-id="eb1a7-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="eb1a7-121">Implementowanie vsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="eb1a7-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="eb1a7-122">Klasa `VsProjectCapabilitiesPresenceChecker` musi implementować `IVsBooleanSymbolPresenceChecker` interfejs , który jest zdefiniowany w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="eb1a7-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

```cs
public interface IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// Checks whether the symbols defined may have changed since the last time
    /// this method was called.
    /// </summary>
    /// <param name="versionObject">
    /// The response version object assigned at the last call.
    /// May be null to get the initial version.
    /// At the conclusion of this method call, the reference may be changed so that on a subsequent call
    /// we know what version was last observed. The caller should treat this value as an opaque object,
    /// and should not assume any significance from whether the pointer changed or not.
    /// </param>
    /// <returns>
    /// <c>true</c> if the symbols defined may have changed since the last call to this method
    /// or if <paramref name="versionObject"/> was <c>null</c> upon entering this method.
    /// <c>false</c> if the responses would all be the same.
    /// </returns>
    bool HasChangedSince(ref object versionObject);

    /// <summary>
    /// Checks for the presence of a given symbol.
    /// </summary>
    /// <param name="symbol">The symbol to check for.</param>
    /// <returns><c>true</c> if the symbol is present; <c>false</c> otherwise.</returns>
    bool IsSymbolPresent(string symbol);
}
```

<span data-ttu-id="eb1a7-123">Przykładową implementacją tego interfejsu będzie:</span><span class="sxs-lookup"><span data-stu-id="eb1a7-123">A sample implementation of this interface would then be:</span></span>

```cs
class VsProjectCapabilitiesPresenceChecker : IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// The set of capabilities this project system actually has.
    /// This should be kept current, and honestly reflect what the project can do.
    /// </summary>
    private static readonly HashSet<string> ActualProjectCapabilities = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "AssemblyReferences",
            "DeclaredSourceItems",
            "UserSourceItems",
        };

    public bool HasChangedSince(ref object versionObject)
    {
        // If your project capabilities do not change over time while the project is open,
        // you may simply `return false;` from your `HasChangedSince` method.
        return false;
    }

    public bool IsSymbolPresent(string symbol)
    {
        return ActualProjectCapabilities.Contains(symbol);
    }
}
```

<span data-ttu-id="eb1a7-124">Pamiętaj, aby dodawać/usuwać możliwości z `ActualProjectCapabilities` zestawu na podstawie tego, co faktycznie obsługuje system projektu.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="eb1a7-125">Pełne [opisy można znaleźć w dokumentacji](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) dotyczącej możliwości projektu.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="eb1a7-126">Odpowiadanie na zapytania</span><span class="sxs-lookup"><span data-stu-id="eb1a7-126">Responding to queries</span></span>

<span data-ttu-id="eb1a7-127">Projekt deklaruje tę możliwość, obsługując  `VSHPROPID_ProjectCapabilitiesChecker` właściwość za pośrednictwem obiektu `IVsHierarchy::GetProperty` .</span><span class="sxs-lookup"><span data-stu-id="eb1a7-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="eb1a7-128">Powinna zwrócić wystąpienie `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` klasy , które jest zdefiniowane w `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` zestawie.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="eb1a7-129">Odwołaj się do tego zestawu, [instalując jego pakiet NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="eb1a7-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="eb1a7-130">Na przykład możesz dodać następującą `case` instrukcje do `IVsHierarchy::GetProperty` instrukcji metody `switch` :</span><span class="sxs-lookup"><span data-stu-id="eb1a7-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="eb1a7-131">Obsługa dte</span><span class="sxs-lookup"><span data-stu-id="eb1a7-131">DTE Support</span></span>

<span data-ttu-id="eb1a7-132">NuGet kieruje systemem projektu do dodawania odwołań, elementów zawartości i importów MSBuild przez wywołanie [dte](/dotnet/api/envdte.dte), który jest interfejsem automatyzacji Visual Studio najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="eb1a7-133">DTE to zestaw interfejsów COM, które być może już zaimplementowano.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="eb1a7-134">Jeśli typ projektu jest oparty na systemie CPS, zostanie zaimplementowany kod DTE.</span><span class="sxs-lookup"><span data-stu-id="eb1a7-134">If your project type is based on CPS, DTE is implemented for you.</span></span>
