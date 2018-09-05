---
title: Obsługa NuGet dla systemu projektu programu Visual Studio
description: Integracja programu NuGet do systemu projektu programu Visual Studio dla typów projektów innych firm.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: 00a64d95c943e9e5cb3a279358a6495125a1bd87
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551373"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Obsługa NuGet dla systemu projektu programu Visual Studio

Aby zapewnić obsługę typów projektów innych firm w programie Visual Studio, obsługuje NuGet 3.x+ [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), i NuGet 3.2 + obsługuje także systemy projektu bez CPS.

Aby zintegrować z NuGet, system projektu muszą anonsować własną obsługę możliwości projektu opisane w tym temacie.

> [!Note]
> Nie należy deklarować możliwości, których projekt nie ma faktycznie ze względu na włączenie pakiety do zainstalowania w projekcie. Wiele funkcji programu Visual Studio i inne rozszerzenia, zależą od możliwości projektu oprócz klienta programu NuGet. Błędnie anonsowanie możliwości projektu może prowadzić te składniki mogą działać poprawnie i środowisko użytkowników, aby zmniejszyć.

## <a name="advertise-project-capabilities"></a>Ogłasza możliwości projektu

Klienta programu NuGet Określa, które pakiety są zgodne z danego typu projektu na podstawie [możliwości projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), zgodnie z opisem w poniższej tabeli.

| Możliwość | Opis |
| --- | --- |
| AssemblyReferences | Wskazuje, że projekt obsługuje odwołania do zestawu (w odróżnieniu od WinRTReferences). |
| DeclaredSourceItems | Wskazuje, że projekt jest typowy projektu MSBuild (nie środowiska DNX), w tym, że relacja ta stwierdza, elementy źródła w samym projekcie. |
| UserSourceItems|Wskazuje, czy użytkownik może dodać dowolne pliki do projektu. |

Dla systemów opartych na systemie CPS projektu szczegóły implementacji projektu funkcji opisanych w dalszej części tej sekcji zostały wykonane dla Ciebie. Zobacz [deklarowania możliwości projektu w projektach systemu CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>Implementowanie VsProjectCapabilitiesPresenceChecker

`VsProjectCapabilitiesPresenceChecker` Klasa musi implementować `IVsBooleanSymbolPresenceChecker` interfejs, który jest zdefiniowany następująco:

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

Następnie będzie przykładową implementację tego interfejsu:

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

Pamiętaj, aby dodawać i usuwać możliwości usługi `ActualProjectCapabilities` zestaw oparty na co systemu projektu faktycznie obsługuje. Zobacz [projektu dokumentacji możliwości](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) pełne opisy.

## <a name="responding-to-queries"></a>Odpowiada na zapytania

Projekt deklaruje tej możliwości dzięki obsłudze `VSHPROPID_ProjectCapabilitiesChecker` właściwości, za pośrednictwem `IVsHierarchy::GetProperty`. Powinien zostać zwrócony wystąpienie `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, który jest zdefiniowany w `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` zestawu. Odwoływać się do tego zestawu, instalując [jego pakiet NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Na przykład można dodać następujące `case` instrukcję, aby Twoje `IVsHierarchy::GetProperty` metody `switch` instrukcji:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Obsługa DTE

NuGet dyski system projektu, aby dodać odwołania, elementy zawartości, a następnie importuje MSBuild, przez wywołanie [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), czyli interfejs automatyzacji najwyższego poziomu programu Visual Studio. DTE to zbiór interfejsów COM, które mogą już implementację.

Jeśli danego typu projektu jest oparty na systemie CPS, DTE został zaimplementowany dla Ciebie.
