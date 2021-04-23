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
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Obsługa nuGet dla Visual Studio projektu

Aby obsługiwać typy projektów innych firm w programie Visual Studio, nuGet 3.x+ obsługuje system [Common Project System (CPS),](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)a nuGet 3.2+ obsługuje również systemy projektów inne niż CPS.

Aby zintegrować program z programem NuGet, system projektu musi anonsować własną obsługę wszystkich możliwości projektu opisanych w tym temacie.

> [!Note]
> Nie deklaruj możliwości, których w rzeczywistości nie ma w projekcie ze względu na umożliwienie instalowania pakietów w projekcie. Wiele funkcji Visual Studio i innych rozszerzeń zależy od możliwości projektu oprócz klienta NuGet. Fałszywe reklamowanie możliwości projektu może doprowadzić do awarii tych składników i pogorszenia jakości obsługi użytkowników.

## <a name="advertise-project-capabilities"></a>Anonsowanie możliwości projektu

Klient NuGet określa, które pakiety są zgodne z typem projektu, na podstawie możliwości projektu [,](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)zgodnie z opisem w poniższej tabeli.

| Możliwość | Opis |
| --- | --- |
| AssemblyReferences | Wskazuje, że projekt obsługuje odwołania do zestawu (inne niż WinRTReferences). |
| DeclaredSourceItems | Wskazuje, że projekt jest typowym projektem MSBuild (nie DNX), ponieważ deklaruje elementy źródłowe w samym projekcie. |
| UserSourceItems|Wskazuje, że użytkownik może dodawać dowolne pliki do swojego projektu. |

W przypadku systemów projektów opartych na systemie CPS szczegóły implementacji możliwości projektu opisanych w pozostałej części tej sekcji zostały wykonane za Ciebie. Zobacz [deklarowanie możliwości projektu w projektach CPS.](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project)

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>Implementowanie vsProjectCapabilitiesPresenceChecker

Klasa `VsProjectCapabilitiesPresenceChecker` musi implementować `IVsBooleanSymbolPresenceChecker` interfejs , który jest zdefiniowany w następujący sposób:

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

Przykładową implementacją tego interfejsu będzie:

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

Pamiętaj, aby dodawać/usuwać możliwości z `ActualProjectCapabilities` zestawu na podstawie tego, co faktycznie obsługuje system projektu. Pełne [opisy można znaleźć w dokumentacji](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) dotyczącej możliwości projektu.

## <a name="responding-to-queries"></a>Odpowiadanie na zapytania

Projekt deklaruje tę możliwość, obsługując  `VSHPROPID_ProjectCapabilitiesChecker` właściwość za pośrednictwem obiektu `IVsHierarchy::GetProperty` . Powinna zwrócić wystąpienie `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` klasy , które jest zdefiniowane w `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` zestawie. Odwołaj się do tego zestawu, [instalując jego pakiet NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Na przykład możesz dodać następującą `case` instrukcje do `IVsHierarchy::GetProperty` instrukcji metody `switch` :

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Obsługa dte

NuGet kieruje systemem projektu do dodawania odwołań, elementów zawartości i importów MSBuild przez wywołanie [dte](/dotnet/api/envdte.dte), który jest interfejsem automatyzacji Visual Studio najwyższego poziomu. DTE to zestaw interfejsów COM, które być może już zaimplementowano.

Jeśli typ projektu jest oparty na systemie CPS, zostanie zaimplementowany kod DTE.
