---
title: Obsługa NuGet System projektu programu Visual Studio
description: Integracja programu NuGet do systemu projektu programu Visual Studio dla typów projektów innych firm.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: b0937d5c149d79f25a776efac1946c9f42c161e8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816907"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="d1db3-103">Obsługa NuGet system projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d1db3-103">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="d1db3-104">Do obsługi typów innych firm projektu w programie Visual Studio, obsługuje NuGet 3.x+ [wspólnej projektu System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), i NuGet 3.2 + obsługuje również systemy z systemem innym niż CPS projektu.</span><span class="sxs-lookup"><span data-stu-id="d1db3-104">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="d1db3-105">Aby zintegrować z NuGet, system projektu musi anonsują własną obsługę możliwości projektu opisanych w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="d1db3-105">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="d1db3-106">Nie należy deklarować możliwości, które projektu nie ma faktycznego ze względu na włączenie pakietów do zainstalowania w projekcie.</span><span class="sxs-lookup"><span data-stu-id="d1db3-106">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="d1db3-107">Wiele funkcji programu Visual Studio i inne rozszerzenia są zależne od możliwości projektu oprócz klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="d1db3-107">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="d1db3-108">Fałszywie anonsowanie możliwości projektu może prowadzić te składniki mogą działać nieprawidłowo i doświadczenia użytkowników zmniejszenie.</span><span class="sxs-lookup"><span data-stu-id="d1db3-108">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="d1db3-109">Anonsowanie możliwości projektu</span><span class="sxs-lookup"><span data-stu-id="d1db3-109">Advertise project capabilities</span></span>

<span data-ttu-id="d1db3-110">Klienta NuGet Określa, które pakiety są zgodne z danego typu projektu na podstawie [możliwości projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), zgodnie z opisem w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="d1db3-110">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="d1db3-111">Możliwość</span><span class="sxs-lookup"><span data-stu-id="d1db3-111">Capability</span></span> | <span data-ttu-id="d1db3-112">Opis</span><span class="sxs-lookup"><span data-stu-id="d1db3-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1db3-113">Właściwości AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="d1db3-113">AssemblyReferences</span></span> | <span data-ttu-id="d1db3-114">Oznacza, że projekt obsługuje odwołań do zestawu (w odróżnieniu od WinRTReferences).</span><span class="sxs-lookup"><span data-stu-id="d1db3-114">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="d1db3-115">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="d1db3-115">DeclaredSourceItems</span></span> | <span data-ttu-id="d1db3-116">Wskazuje, że projekt jest typowy projektu MSBuild (nie DNX), w tym deklaruje elementów źródła w samym projekcie.</span><span class="sxs-lookup"><span data-stu-id="d1db3-116">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="d1db3-117">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="d1db3-117">UserSourceItems</span></span>|<span data-ttu-id="d1db3-118">Wskazuje, czy użytkownik może dodać dowolne pliki do ich projektu.</span><span class="sxs-lookup"><span data-stu-id="d1db3-118">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="d1db3-119">Dla systemów opartych na CPS projektu szczegóły implementacji dla projektu możliwości opisane w dalszej części tej sekcji zostały wykonane dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="d1db3-119">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="d1db3-120">Zobacz [deklarowania możliwości projektu w projektach CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="d1db3-120">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="d1db3-121">Implementowanie VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="d1db3-121">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="d1db3-122">`VsProjectCapabilitiesPresenceChecker` Musi implementować klasę `IVsBooleanSymbolPresenceChecker` interfejs, który jest zdefiniowany w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d1db3-122">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

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

<span data-ttu-id="d1db3-123">Przykładowe zastosowanie tego interfejsu przestaną być:</span><span class="sxs-lookup"><span data-stu-id="d1db3-123">A sample implementation of this interface would then be:</span></span>

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

<span data-ttu-id="d1db3-124">Pamiętaj, aby usunąć możliwości z `ActualProjectCapabilities` zestaw oparty na co projekt system faktycznie obsługuje.</span><span class="sxs-lookup"><span data-stu-id="d1db3-124">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="d1db3-125">Zobacz [projektu dokumentacji możliwości](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) pełny opis.</span><span class="sxs-lookup"><span data-stu-id="d1db3-125">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="d1db3-126">Odpowiada na zapytania</span><span class="sxs-lookup"><span data-stu-id="d1db3-126">Responding to queries</span></span>

<span data-ttu-id="d1db3-127">Projekt deklaruje tej możliwości dzięki obsłudze `VSHPROPID_ProjectCapabilitiesChecker` właściwości za pośrednictwem `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="d1db3-127">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="d1db3-128">Powinien on zwrócić wystąpienia `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, która jest zdefiniowana w `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` zestawu.</span><span class="sxs-lookup"><span data-stu-id="d1db3-128">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="d1db3-129">Odwołanie tego zestawu, instalując [pakietu NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="d1db3-129">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="d1db3-130">Na przykład można dodać następujące `case` instrukcji do Twojej `IVsHierarchy::GetProperty` metody `switch` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="d1db3-130">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="d1db3-131">Obsługa DTE</span><span class="sxs-lookup"><span data-stu-id="d1db3-131">DTE Support</span></span>

<span data-ttu-id="d1db3-132">NuGet dyski system projektu, aby dodać odwołania, elementy zawartości i MSBuild importuje przez wywołanie [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), która jest najwyższego poziomu interfejs automatyzacji programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1db3-132">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="d1db3-133">DTE to zestaw interfejsów modelu COM, które mogą już implementację.</span><span class="sxs-lookup"><span data-stu-id="d1db3-133">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="d1db3-134">Jeśli danego typu projektu jest oparty na CPS, DTE jest implementowane za Ciebie.</span><span class="sxs-lookup"><span data-stu-id="d1db3-134">If your project type is based on CPS, DTE is implemented for you.</span></span>
