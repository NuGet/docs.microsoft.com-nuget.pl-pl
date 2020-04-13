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
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Obsługa nuGet dla systemu projektu programu Visual Studio

Aby obsługiwać typy projektów innych firm w programie Visual Studio, NuGet 3.x+ obsługuje [wspólny system projektu (CPS),](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md)a NuGet 3.2+ obsługuje również systemy projektów innych niż CPS.

Aby zintegrować z NuGet, system projektu musi anonsować własne wsparcie dla wszystkich możliwości projektu opisanych w tym temacie.

> [!Note]
> Nie deklaruj możliwości, których projekt faktycznie nie ma ze względu na włączenie pakietów do zainstalowania w projekcie. Wiele funkcji programu Visual Studio i innych rozszerzeń zależy od możliwości projektu oprócz klienta NuGet. Fałszywie reklamowe możliwości projektu mogą doprowadzić te składniki do nieprawidłowego działania, a środowisko użytkowników do degradacji.

## <a name="advertise-project-capabilities"></a>Reklamowanie możliwości projektu

Klient NuGet określa, które pakiety są zgodne z typem projektu na podstawie [możliwości projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), zgodnie z opisem w poniższej tabeli.

| Możliwości | Opis |
| --- | --- |
| Wnioski o assemblyreferences | Wskazuje, że projekt obsługuje odwołania do zestawu (w odróżnieniu od WinRTReferences). |
| Zadeklarowanezajednak. | Wskazuje, że projekt jest typowym projektem MSBuild (nie DNX), ponieważ deklaruje elementy źródłowe w samym projekcie. |
| Zasoby zasobów użytkownika|Wskazuje, że użytkownik może dodawać dowolne pliki do swojego projektu. |

W przypadku systemów projektowych opartych na cps szczegóły implementacji możliwości projektu opisane w pozostałej części tej sekcji zostały wykonane dla Ciebie. Zobacz [deklarowanie możliwości projektu w projektach CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>Wdrażanie VsProjectCapabilitiesPresenceChecker

Klasa `VsProjectCapabilitiesPresenceChecker` musi implementować `IVsBooleanSymbolPresenceChecker` interfejs, który jest zdefiniowany w następujący sposób:

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

Przykładową implementacją tego interfejsu będzie wówczas:

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

Pamiętaj, aby dodać/usunąć `ActualProjectCapabilities` możliwości z zestawu w oparciu o to, co system projektu faktycznie obsługuje. Pełne [opisy można](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) znaleźć w dokumentacji możliwości projektu.

## <a name="responding-to-queries"></a>Odpowiadanie na zapytania

Projekt deklaruje tę możliwość, wspierając `VSHPROPID_ProjectCapabilitiesChecker` właściwość `IVsHierarchy::GetProperty`za pośrednictwem . Powinien zwrócić wystąpienie `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, który jest `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` zdefiniowany w zestawie. Odwołaj się do tego zestawu, instalując [jego pakiet NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Na przykład można dodać `case` następującą `IVsHierarchy::GetProperty` instrukcję `switch` do instrukcji metody:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Obsługa DTE

NuGet dyski systemu projektu, aby dodać odwołania, elementy zawartości i MSBuild importu przez wywołanie do [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), który jest interfejsem automatyzacji najwyższego poziomu programu Visual Studio. DTE to zestaw interfejsów COM, które można już zaimplementować.

Jeśli typ projektu jest oparty na CPS, DTE jest implementowany dla Ciebie.
