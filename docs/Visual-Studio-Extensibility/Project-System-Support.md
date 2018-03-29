---
title: Obsługa NuGet System projektu programu Visual Studio | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Integracja programu NuGet do systemu projektu programu Visual Studio dla typów projektów innych firm.
keywords: NuGet w Visual Studio, projektu niestandardowe typy projektów Visual Studio
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0ffebfc9e403315482d3781a00a0a6896fd04f0c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="98024-104">Obsługa NuGet system projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="98024-104">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="98024-105">Do obsługi typów innych firm projektu w programie Visual Studio, obsługuje NuGet 3.x+ [wspólnej projektu System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), i NuGet 3.2 + obsługuje również systemy z systemem innym niż CPS projektu.</span><span class="sxs-lookup"><span data-stu-id="98024-105">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="98024-106">Aby zintegrować z NuGet, system projektu musi anonsują własną obsługę możliwości projektu opisanych w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="98024-106">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="98024-107">Nie należy deklarować możliwości, które projektu nie ma faktycznego ze względu na włączenie pakietów do zainstalowania w projekcie.</span><span class="sxs-lookup"><span data-stu-id="98024-107">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="98024-108">Wiele funkcji programu Visual Studio i inne rozszerzenia są zależne od możliwości projektu oprócz klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="98024-108">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="98024-109">Fałszywie anonsowanie możliwości projektu może prowadzić te składniki mogą działać nieprawidłowo i doświadczenia użytkowników zmniejszenie.</span><span class="sxs-lookup"><span data-stu-id="98024-109">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="98024-110">Anonsowanie możliwości projektu</span><span class="sxs-lookup"><span data-stu-id="98024-110">Advertise project capabilities</span></span>

<span data-ttu-id="98024-111">Klienta NuGet Określa, które pakiety są zgodne z danego typu projektu na podstawie [możliwości projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), zgodnie z opisem w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="98024-111">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="98024-112">Możliwość</span><span class="sxs-lookup"><span data-stu-id="98024-112">Capability</span></span> | <span data-ttu-id="98024-113">Opis</span><span class="sxs-lookup"><span data-stu-id="98024-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="98024-114">Właściwości AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="98024-114">AssemblyReferences</span></span> | <span data-ttu-id="98024-115">Oznacza, że projekt obsługuje odwołań do zestawu (w odróżnieniu od WinRTReferences).</span><span class="sxs-lookup"><span data-stu-id="98024-115">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="98024-116">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="98024-116">DeclaredSourceItems</span></span> | <span data-ttu-id="98024-117">Wskazuje, że projekt jest typowy projektu MSBuild (nie DNX), w tym deklaruje elementów źródła w samym projekcie.</span><span class="sxs-lookup"><span data-stu-id="98024-117">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="98024-118">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="98024-118">UserSourceItems</span></span>|<span data-ttu-id="98024-119">Wskazuje, czy użytkownik może dodać dowolne pliki do ich projektu.</span><span class="sxs-lookup"><span data-stu-id="98024-119">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="98024-120">Dla systemów opartych na CPS projektu szczegóły implementacji dla projektu możliwości opisane w dalszej części tej sekcji zostały wykonane dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="98024-120">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="98024-121">Zobacz [deklarowania możliwości projektu w projektach CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span><span class="sxs-lookup"><span data-stu-id="98024-121">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="98024-122">Implementowanie VsProjectCapabilitiesPresenceChecker</span><span class="sxs-lookup"><span data-stu-id="98024-122">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="98024-123">`VsProjectCapabilitiesPresenceChecker` Musi implementować klasę `IVsBooleanSymbolPresenceChecker` interfejs, który jest zdefiniowany w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="98024-123">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

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

<span data-ttu-id="98024-124">Przykładowe zastosowanie tego interfejsu przestaną być:</span><span class="sxs-lookup"><span data-stu-id="98024-124">A sample implementation of this interface would then be:</span></span>

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

<span data-ttu-id="98024-125">Pamiętaj, aby usunąć możliwości z `ActualProjectCapabilities` zestaw oparty na co projekt system faktycznie obsługuje.</span><span class="sxs-lookup"><span data-stu-id="98024-125">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="98024-126">Zobacz [projektu dokumentacji możliwości](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) pełny opis.</span><span class="sxs-lookup"><span data-stu-id="98024-126">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="98024-127">Odpowiada na zapytania</span><span class="sxs-lookup"><span data-stu-id="98024-127">Responding to queries</span></span>

<span data-ttu-id="98024-128">Projekt deklaruje tej możliwości dzięki obsłudze `VSHPROPID_ProjectCapabilitiesChecker` właściwości za pośrednictwem `IVsHierarchy::GetProperty`.</span><span class="sxs-lookup"><span data-stu-id="98024-128">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="98024-129">Powinien on zwrócić wystąpienia `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, która jest zdefiniowana w `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` zestawu.</span><span class="sxs-lookup"><span data-stu-id="98024-129">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="98024-130">Odwołanie tego zestawu, instalując [pakietu NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span><span class="sxs-lookup"><span data-stu-id="98024-130">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="98024-131">Na przykład można dodać następujące `case` instrukcji do Twojej `IVsHierarchy::GetProperty` metody `switch` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="98024-131">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="98024-132">Obsługa DTE</span><span class="sxs-lookup"><span data-stu-id="98024-132">DTE Support</span></span>

<span data-ttu-id="98024-133">NuGet dyski system projektu, aby dodać odwołania, elementy zawartości i MSBuild importuje przez wywołanie [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), która jest najwyższego poziomu interfejs automatyzacji programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="98024-133">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="98024-134">DTE to zestaw interfejsów modelu COM, które mogą już implementację.</span><span class="sxs-lookup"><span data-stu-id="98024-134">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="98024-135">Jeśli danego typu projektu jest oparty na CPS, DTE jest implementowane za Ciebie.</span><span class="sxs-lookup"><span data-stu-id="98024-135">If your project type is based on CPS, DTE is implemented for you.</span></span>
