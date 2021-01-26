---
title: Obsługa NuGet dla systemu projektu programu Visual Studio
description: Integracja programu NuGet z systemem projektu programu Visual Studio dla typów projektów innych firm.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 7af330f88b47352666933598719d9c8f8cb66a78
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779408"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="334d6-103">Obsługa NuGet dla systemu projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="334d6-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="334d6-104">Aby można było obsługiwać typy projektów innych firm w programie Visual Studio, pakiet NuGet 3. x + obsługuje program [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)i NuGet 3.2 + obsługuje również systemy projektów innych niż CPS.</span><span class="sxs-lookup"><span data-stu-id="334d6-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="334d6-105">Aby przeprowadzić integrację z pakietem NuGet, system projektu musi zaanonsować własną obsługę wszystkich możliwości projektu opisanych w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="334d6-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="334d6-106">Nie deklaruj możliwości, które projekt nie ma w rzeczywistości, aby można było włączyć pakiety do zainstalowania w projekcie.</span><span class="sxs-lookup"><span data-stu-id="334d6-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="334d6-107">Wiele funkcji programu Visual Studio i innych rozszerzeń zależy od możliwości projektu poza klientem NuGet.</span><span class="sxs-lookup"><span data-stu-id="334d6-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="334d6-108">Fałszywie reklamowe możliwości projektu mogą prowadzić do nieprawidłowego działania tych składników i obniżyć komfort pracy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="334d6-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="334d6-109">Anonsuj możliwości projektu</span><span class="sxs-lookup"><span data-stu-id="334d6-109">Advertise project capabilities</span></span>

<span data-ttu-id="334d6-110">Klient NuGet określa, które pakiety są zgodne z typem projektu na podstawie [możliwości projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), zgodnie z opisem w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="334d6-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="334d6-111">Możliwość</span><span class="sxs-lookup"><span data-stu-id="334d6-111">Capability</span></span> | <span data-ttu-id="334d6-112">Opis</span><span class="sxs-lookup"><span data-stu-id="334d6-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="334d6-113">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="334d6-113">AssemblyReferences</span></span> | <span data-ttu-id="334d6-114">Wskazuje, że projekt obsługuje odwołania do zestawów (różne od WinRTReferences).</span><span class="sxs-lookup"><span data-stu-id="334d6-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="334d6-115">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="334d6-115">DeclaredSourceItems</span></span> | <span data-ttu-id="334d6-116">Wskazuje, że projekt jest typowym projektem programu MSBuild (nie środowiska DNX) w tym, że deklaruje elementy źródłowe w samym projekcie.</span><span class="sxs-lookup"><span data-stu-id="334d6-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="334d6-117">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="334d6-117">UserSourceItems</span></span>|<span data-ttu-id="334d6-118">Wskazuje, że użytkownik może dodawać do projektu dowolne pliki.</span><span class="sxs-lookup"><span data-stu-id="334d6-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="334d6-119">W przypadku systemów projektów opartych na serwerze CPS szczegóły implementacji dotyczące możliwości projektu opisanych w dalszej części tej sekcji zostały wykonane.</span><span class="sxs-lookup"><span data-stu-id="334d6-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="334d6-120">Zobacz [deklarowanie możliwości projektu w projektach CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="334d6-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="334d6-121">Implementowanie VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="334d6-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="334d6-122">`VsProjectCapabilitiesPresenceChecker`Klasa musi implementować `IVsBooleanSymbolPresenceChecker` interfejs, który jest zdefiniowany w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="334d6-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

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

<span data-ttu-id="334d6-123">Przykładowa implementacja tego interfejsu będzie:</span><span class="sxs-lookup"><span data-stu-id="334d6-123">A sample implementation of this interface would then be:</span></span>

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

<span data-ttu-id="334d6-124">Należy pamiętać o możliwości dodania/usunięcia z `ActualProjectCapabilities` zestawu na podstawie tego, co system projektu rzeczywiście obsługuje.</span><span class="sxs-lookup"><span data-stu-id="334d6-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="334d6-125">Zobacz [dokumentację możliwości projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) , aby zapoznać się z pełnymi opisami.</span><span class="sxs-lookup"><span data-stu-id="334d6-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="334d6-126">Reagowanie na zapytania</span><span class="sxs-lookup"><span data-stu-id="334d6-126">Responding to queries</span></span>

<span data-ttu-id="334d6-127">Projekt deklaruje tę możliwość, obsługując  `VSHPROPID_ProjectCapabilitiesChecker` Właściwość za pomocą `IVsHierarchy::GetProperty` .</span><span class="sxs-lookup"><span data-stu-id="334d6-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="334d6-128">Powinien zwrócić wystąpienie `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` , które jest zdefiniowane w `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` zestawie.</span><span class="sxs-lookup"><span data-stu-id="334d6-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="334d6-129">Odwołuje się do tego zestawu, instalując [jego pakiet NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="334d6-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="334d6-130">Na przykład można dodać następującą `case` instrukcję do `IVsHierarchy::GetProperty` `switch` instrukcji metody:</span><span class="sxs-lookup"><span data-stu-id="334d6-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="334d6-131">Obsługa DTE</span><span class="sxs-lookup"><span data-stu-id="334d6-131">DTE Support</span></span>

<span data-ttu-id="334d6-132">Pakiet NuGet umożliwia dodanie odwołań, elementów zawartości i importów MSBuild przez wywołanie do [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), który jest interfejsem automatyzacji programu Visual Studio najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="334d6-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="334d6-133">DTE jest zestawem interfejsów COM, które mogą już być wdrożone.</span><span class="sxs-lookup"><span data-stu-id="334d6-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="334d6-134">Jeśli typ projektu jest oparty na CPS, dla Ciebie zaimplementowano DTE.</span><span class="sxs-lookup"><span data-stu-id="334d6-134">If your project type is based on CPS, DTE is implemented for you.</span></span>
