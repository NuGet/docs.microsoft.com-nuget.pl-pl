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
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Obsługa NuGet dla systemu projektu programu Visual Studio

Aby można było obsługiwać typy projektów innych firm w programie Visual Studio, pakiet NuGet 3. x + obsługuje program [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)i NuGet 3.2 + obsługuje również systemy projektów innych niż CPS.

Aby przeprowadzić integrację z pakietem NuGet, system projektu musi zaanonsować własną obsługę wszystkich możliwości projektu opisanych w tym temacie.

> [!Note]
> Nie deklaruj możliwości, które projekt nie ma w rzeczywistości, aby można było włączyć pakiety do zainstalowania w projekcie. Wiele funkcji programu Visual Studio i innych rozszerzeń zależy od możliwości projektu poza klientem NuGet. Fałszywie reklamowe możliwości projektu mogą prowadzić do nieprawidłowego działania tych składników i obniżyć komfort pracy użytkowników.

## <a name="advertise-project-capabilities"></a>Anonsuj możliwości projektu

Klient NuGet określa, które pakiety są zgodne z typem projektu na podstawie [możliwości projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), zgodnie z opisem w poniższej tabeli.

| Możliwość | Opis |
| --- | --- |
| AssemblyReferences | Wskazuje, że projekt obsługuje odwołania do zestawów (różne od WinRTReferences). |
| DeclaredSourceItems | Wskazuje, że projekt jest typowym projektem programu MSBuild (nie środowiska DNX) w tym, że deklaruje elementy źródłowe w samym projekcie. |
| UserSourceItems|Wskazuje, że użytkownik może dodawać do projektu dowolne pliki. |

W przypadku systemów projektów opartych na serwerze CPS szczegóły implementacji dotyczące możliwości projektu opisanych w dalszej części tej sekcji zostały wykonane. Zobacz [deklarowanie możliwości projektu w projektach CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>Implementowanie VsProjectCapabilitiesPresenceChecker

`VsProjectCapabilitiesPresenceChecker`Klasa musi implementować `IVsBooleanSymbolPresenceChecker` interfejs, który jest zdefiniowany w następujący sposób:

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

Przykładowa implementacja tego interfejsu będzie:

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

Należy pamiętać o możliwości dodania/usunięcia z `ActualProjectCapabilities` zestawu na podstawie tego, co system projektu rzeczywiście obsługuje. Zobacz [dokumentację możliwości projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) , aby zapoznać się z pełnymi opisami.

## <a name="responding-to-queries"></a>Reagowanie na zapytania

Projekt deklaruje tę możliwość, obsługując  `VSHPROPID_ProjectCapabilitiesChecker` Właściwość za pomocą `IVsHierarchy::GetProperty` . Powinien zwrócić wystąpienie `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` , które jest zdefiniowane w `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` zestawie. Odwołuje się do tego zestawu, instalując [jego pakiet NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Na przykład można dodać następującą `case` instrukcję do `IVsHierarchy::GetProperty` `switch` instrukcji metody:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Obsługa DTE

Pakiet NuGet umożliwia dodanie odwołań, elementów zawartości i importów MSBuild przez wywołanie do [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), który jest interfejsem automatyzacji programu Visual Studio najwyższego poziomu. DTE jest zestawem interfejsów COM, które mogą już być wdrożone.

Jeśli typ projektu jest oparty na CPS, dla Ciebie zaimplementowano DTE.
