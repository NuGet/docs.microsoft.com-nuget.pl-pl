---
title: Obsługa nuget dla systemu projektu programu Visual Studio
description: Integracja NuGet do systemu projektu Visual Studio dla typów projektów innych firm.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 00a64d95c943e9e5cb3a279358a6495125a1bd87
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495930"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="ab7f3-103">Obsługa nuGet dla systemu projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ab7f3-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="ab7f3-104">Aby obsługiwać typy projektów innych firm w programie Visual Studio, NuGet 3.x+ obsługuje [wspólny system projektu (CPS),](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)a NuGet 3.2+ obsługuje również systemy projektów innych niż CPS.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="ab7f3-105">Aby zintegrować z NuGet, system projektu musi anonsować własne wsparcie dla wszystkich możliwości projektu opisanych w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="ab7f3-106">Nie deklaruj możliwości, których projekt faktycznie nie ma ze względu na włączenie pakietów do zainstalowania w projekcie.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="ab7f3-107">Wiele funkcji programu Visual Studio i innych rozszerzeń zależy od możliwości projektu oprócz klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="ab7f3-108">Fałszywie reklamowe możliwości projektu mogą doprowadzić te składniki do nieprawidłowego działania, a środowisko użytkowników do degradacji.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="ab7f3-109">Reklamowanie możliwości projektu</span><span class="sxs-lookup"><span data-stu-id="ab7f3-109">Advertise project capabilities</span></span>

<span data-ttu-id="ab7f3-110">Klient NuGet określa, które pakiety są zgodne z typem projektu na podstawie [możliwości projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), zgodnie z opisem w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="ab7f3-111">Możliwości</span><span class="sxs-lookup"><span data-stu-id="ab7f3-111">Capability</span></span> | <span data-ttu-id="ab7f3-112">Opis</span><span class="sxs-lookup"><span data-stu-id="ab7f3-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ab7f3-113">Wnioski o assemblyreferences</span><span class="sxs-lookup"><span data-stu-id="ab7f3-113">AssemblyReferences</span></span> | <span data-ttu-id="ab7f3-114">Wskazuje, że projekt obsługuje odwołania do zestawu (w odróżnieniu od WinRTReferences).</span><span class="sxs-lookup"><span data-stu-id="ab7f3-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="ab7f3-115">Zadeklarowanezajednak.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-115">DeclaredSourceItems</span></span> | <span data-ttu-id="ab7f3-116">Wskazuje, że projekt jest typowym projektem MSBuild (nie DNX), ponieważ deklaruje elementy źródłowe w samym projekcie.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="ab7f3-117">Zasoby zasobów użytkownika</span><span class="sxs-lookup"><span data-stu-id="ab7f3-117">UserSourceItems</span></span>|<span data-ttu-id="ab7f3-118">Wskazuje, że użytkownik może dodawać dowolne pliki do swojego projektu.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="ab7f3-119">W przypadku systemów projektowych opartych na cps szczegóły implementacji możliwości projektu opisane w pozostałej części tej sekcji zostały wykonane dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="ab7f3-120">Zobacz [deklarowanie możliwości projektu w projektach CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="ab7f3-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="ab7f3-121">Wdrażanie VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="ab7f3-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="ab7f3-122">Klasa `VsProjectCapabilitiesPresenceChecker` musi implementować `IVsBooleanSymbolPresenceChecker` interfejs, który jest zdefiniowany w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ab7f3-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

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

<span data-ttu-id="ab7f3-123">Przykładową implementacją tego interfejsu będzie wówczas:</span><span class="sxs-lookup"><span data-stu-id="ab7f3-123">A sample implementation of this interface would then be:</span></span>

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

<span data-ttu-id="ab7f3-124">Pamiętaj, aby dodać/usunąć `ActualProjectCapabilities` możliwości z zestawu w oparciu o to, co system projektu faktycznie obsługuje.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="ab7f3-125">Pełne [opisy można](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) znaleźć w dokumentacji możliwości projektu.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="ab7f3-126">Odpowiadanie na zapytania</span><span class="sxs-lookup"><span data-stu-id="ab7f3-126">Responding to queries</span></span>

<span data-ttu-id="ab7f3-127">Projekt deklaruje tę możliwość, wspierając `VSHPROPID_ProjectCapabilitiesChecker` właściwość `IVsHierarchy::GetProperty`za pośrednictwem .</span><span class="sxs-lookup"><span data-stu-id="ab7f3-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="ab7f3-128">Powinien zwrócić wystąpienie `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, który jest `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` zdefiniowany w zestawie.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="ab7f3-129">Odwołaj się do tego zestawu, instalując [jego pakiet NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="ab7f3-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="ab7f3-130">Na przykład można dodać `case` następującą `IVsHierarchy::GetProperty` instrukcję `switch` do instrukcji metody:</span><span class="sxs-lookup"><span data-stu-id="ab7f3-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="ab7f3-131">Obsługa DTE</span><span class="sxs-lookup"><span data-stu-id="ab7f3-131">DTE Support</span></span>

<span data-ttu-id="ab7f3-132">NuGet dyski systemu projektu, aby dodać odwołania, elementy zawartości i MSBuild importu przez wywołanie do [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), który jest interfejsem automatyzacji najwyższego poziomu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="ab7f3-133">DTE to zestaw interfejsów COM, które można już zaimplementować.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="ab7f3-134">Jeśli typ projektu jest oparty na CPS, DTE jest implementowany dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="ab7f3-134">If your project type is based on CPS, DTE is implemented for you.</span></span>
