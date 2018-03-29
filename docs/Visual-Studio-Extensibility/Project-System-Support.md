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
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Obsługa NuGet system projektu programu Visual Studio

Do obsługi typów innych firm projektu w programie Visual Studio, obsługuje NuGet 3.x+ [wspólnej projektu System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), i NuGet 3.2 + obsługuje również systemy z systemem innym niż CPS projektu.

Aby zintegrować z NuGet, system projektu musi anonsują własną obsługę możliwości projektu opisanych w tym temacie.

> [!Note]
> Nie należy deklarować możliwości, które projektu nie ma faktycznego ze względu na włączenie pakietów do zainstalowania w projekcie. Wiele funkcji programu Visual Studio i inne rozszerzenia są zależne od możliwości projektu oprócz klienta NuGet. Fałszywie anonsowanie możliwości projektu może prowadzić te składniki mogą działać nieprawidłowo i doświadczenia użytkowników zmniejszenie.

## <a name="advertise-project-capabilities"></a>Anonsowanie możliwości projektu

Klienta NuGet Określa, które pakiety są zgodne z danego typu projektu na podstawie [możliwości projektu](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), zgodnie z opisem w poniższej tabeli.

| Możliwość | Opis |
| --- | --- |
| Właściwości AssemblyReferences | Oznacza, że projekt obsługuje odwołań do zestawu (w odróżnieniu od WinRTReferences). |
| DeclaredSourceItems | Wskazuje, że projekt jest typowy projektu MSBuild (nie DNX), w tym deklaruje elementów źródła w samym projekcie. |
| UserSourceItems|Wskazuje, czy użytkownik może dodać dowolne pliki do ich projektu. |

Dla systemów opartych na CPS projektu szczegóły implementacji dla projektu możliwości opisane w dalszej części tej sekcji zostały wykonane dla Ciebie. Zobacz [deklarowania możliwości projektu w projektach CPS](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>Implementowanie VsProjectCapabilitiesPresenceChecker

`VsProjectCapabilitiesPresenceChecker` Musi implementować klasę `IVsBooleanSymbolPresenceChecker` interfejs, który jest zdefiniowany w następujący sposób:

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

Przykładowe zastosowanie tego interfejsu przestaną być:

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

Pamiętaj, aby usunąć możliwości z `ActualProjectCapabilities` zestaw oparty na co projekt system faktycznie obsługuje. Zobacz [projektu dokumentacji możliwości](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) pełny opis.

## <a name="responding-to-queries"></a>Odpowiada na zapytania

Projekt deklaruje tej możliwości dzięki obsłudze `VSHPROPID_ProjectCapabilitiesChecker` właściwości za pośrednictwem `IVsHierarchy::GetProperty`. Powinien on zwrócić wystąpienia `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, która jest zdefiniowana w `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` zestawu. Odwołanie tego zestawu, instalując [pakietu NuGet](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).

Na przykład można dodać następujące `case` instrukcji do Twojej `IVsHierarchy::GetProperty` metody `switch` instrukcji:

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>Obsługa DTE

NuGet dyski system projektu, aby dodać odwołania, elementy zawartości i MSBuild importuje przez wywołanie [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), która jest najwyższego poziomu interfejs automatyzacji programu Visual Studio. DTE to zestaw interfejsów modelu COM, które mogą już implementację.

Jeśli danego typu projektu jest oparty na CPS, DTE jest implementowane za Ciebie.
