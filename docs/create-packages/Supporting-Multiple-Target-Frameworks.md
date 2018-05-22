---
title: Wielowersyjność kodu dla pakietów NuGet
description: Opis różnych metod pod kątem wiele wersji .NET Framework z w ramach jednego pakietu NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: 9bdcff8210c192a695a5645f28ef88087469ec52
ms.sourcegitcommit: f0b31af805183cf3a98eabb504e16d9b05223cfe
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/22/2018
---
# <a name="supporting-multiple-net-framework-versions"></a>Obsługa wielu wersje programu .NET framework

*Dla platformy .NET Core projektów przy użyciu narzędzia NuGet 4.0 +, zobacz [NuGet pakietu i ich przywracania docelowych elementów MSBuild](../reference/msbuild-targets.md) szczegółowe informacje dotyczące różnych elementów docelowych.*

Wiele bibliotek docelowe określonej wersji programu .NET Framework. Na przykład może być jedną wersję biblioteki, które są specyficzne dla platformy uniwersalnej systemu Windows i inną wersję, która korzysta z funkcji .NET Framework 4.6.

Aby zmieścił się w tym celu NuGet obsługuje wprowadzanie wielu wersji tego samego biblioteki w jednym pakiecie przy korzystaniu z opartych na konwencjach pracy katalogu metody opisane w [utworzenie pakietu](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).

## <a name="framework-version-folder-structure"></a>Struktura folderów wersji Framework

Podczas tworzenia pakietu, który zawiera tylko jedną wersję biblioteki lub docelowej wielu struktur, zawsze utworzyć podfoldery `lib` przy użyciu różnych framework z uwzględnieniem wielkości liter nazwy z następującą konwencją:

    lib\{framework name}[{version}]

Aby uzyskać pełną listę obsługiwanych nazw, zobacz [odwołania docelowych platform](../reference/target-frameworks.md#supported-frameworks).

Nigdy nie powinien mieć wersji biblioteki, który nie jest specyficzne dla struktury i umieszczony bezpośrednio w folderze głównym `lib` folderu. (Ta funkcja jest obsługiwana tylko w przypadku `packages.config`). W ten sposób może zapewnić zgodność z platformy docelowej biblioteki i umożliwić mu można zainstalować w dowolnym miejscu, prawdopodobnie powodujące błędy podczas wykonywania nieoczekiwany. Dodawanie zestawów w folderze głównym (takich jak `lib\abc.dll`) lub podfolderów (takie jak `lib\abc\abc.dll`) jest przestarzała i jest ignorowane w przypadku przy użyciu formatu PackagesReference.

Na przykład następujące struktury folderów obsługuje cztery wersji zestawu, które są specyficzne dla framework:

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Aby łatwo obejmują wszystkie te pliki, podczas tworzenia pakietu, należy użyć cyklicznej `**` symbolu wieloznacznego w `<files>` części Twojego `.nuspec`:

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Foldery architektury

Jeśli masz zestawy architektury, oznacza to, oddzielne zestawy przeznaczonych dla ARM, x 86 i x64, trzeba je umieścić w folderze o nazwie `runtimes` w podfoldery o nazwie `{platform}-{architecture}\lib\{framework}` lub `{platform}-{architecture}\native`. Na przykład następujące struktury folderów może pomieścić natywnych i zarządzanych biblioteki dll przeznaczonych dla systemu Windows 10 i `uap10.0` framework:

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

Zobacz [tworzenie pakietów platformy uniwersalnej systemu Windows](../guides/create-uwp-packages.md) przykład odwołujące się do tych plików w `.nuspec` manifestu.

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Zgodnych wersji zestawu i platforma docelowa projektu

Podczas instalowania pakietu, który ma wiele wersji zestawu NuGet próbuje zgodna z nazwą framework zestawu z platformy docelowej projektu.

Jeśli nie, NuGet kopiuje zestawu dla najwyższa wersja, która jest mniejsza lub równa platformy docelowej projektu, jeśli jest dostępna. Jeśli nie zgodny zestaw zostanie znaleziony, NuGet zwraca odpowiedni komunikat o błędzie.

Na przykład wziąć pod uwagę następujące struktury folderów w pakiecie:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

Podczas instalowania tego pakietu w projekcie, przeznaczonego dla programu .NET Framework 4.6, NuGet instaluje zestaw w `net45` folderu, ponieważ jest to najwyższa wersja dostępne, która jest mniejsza niż 4.6.

Jeśli projekt jest przeznaczony dla platformy .NET Framework 4.6.1, z drugiej strony, NuGet instaluje zestaw w `net461` folderu.

Jeśli projekt jest przeznaczony dla środowiska .NET framework 4.0 lub starszym, NuGet zgłasza odpowiedni komunikat o błędzie dla nie wyszukuje zgodny zestaw.

## <a name="grouping-assemblies-by-framework-version"></a>Zestawy grupowania przez framework w wersji

NuGet kopiuje zestawy z tylko jedna biblioteka folderu w pakiecie. Na przykład załóżmy, że pakiet ma następującą strukturę folderów:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

Podczas instalowania pakietu w projekcie, przeznaczonego dla programu .NET Framework 4.5, `MyAssembly.dll` (w wersji 2.0) to zestaw tylko zainstalowany. `MyAssembly.Core.dll` (1.0) nie jest zainstalowany, ponieważ nie znajduje się w `net45` folderu. NuGet działa w ten sposób, ponieważ `MyAssembly.Core.dll` może mieć scalonego w wersji 2.0 `MyAssembly.dll`.

Jeśli chcesz `MyAssembly.Core.dll` zainstalowania programu .NET Framework 4.5, Umieść kopię w `net45` folderu.

## <a name="grouping-assemblies-by-framework-profile"></a>Zestawy grupowania w ramach profilu

NuGet obsługuje również przeznaczonych dla określonej platformy profil przez dołączenie kreska i nazwa profilu w celu folderu.

    lib\{framework name}-{profile}

Profile obsługiwane są następujące:

- `client`: Profil klienta
- `full`: Full Profile
- `wp`: Windows Phone
- `cf`: Compact Framework

## <a name="determining-which-nuget-target-to-use"></a>Określanie, która docelowa NuGet do użycia

Podczas tworzenia pakietów bibliotek przeznaczonych przenośnej biblioteki klas może być trudnych do określenia docelowej NuGet, których należy używać w nazwach folderów i `.nuspec` plik, zwłaszcza, jeśli celem tylko podzestaw PCL. Następujące zasoby zewnętrzne mogą pomóc w tym:

- [Profile Framework w .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)
- [Profile biblioteki klas przenośnych](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tabela wyliczanie profilów PCL i ich równoważne celów NuGet
- [Przenośnej biblioteki klas profile narzędzie](https://github.com/StephenCleary/PortableLibraryProfiles) (witryną github.com): narzędzie wiersza polecenia, określając PCL profile dostępna w systemie

## <a name="content-files-and-powershell-scripts"></a>Pliki zawartości i skryptów programu PowerShell

> [!Warning]
> Modyfikowalne pliki zawartości i wykonywanie skryptu są dostępne z `packages.config` tylko format; zostały uznane za przestarzałe w innych formatach i nie powinna być używana dla dowolnego nowego pakietu.

Z `packages.config`, zawartości plików i skryptów programu PowerShell można przedstawić w rozbiciu platformy docelowej przy użyciu tej samej Konwencji folder wewnątrz `content` i `tools` folderów. Na przykład:

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

Jeśli w folderze struktury jest puste, NuGet nie dodać odwołania do zestawów ani plików zawartości i uruchamiać skrypty programu PowerShell dla tej struktury.

> [!Note]
> Ponieważ `init.ps1` jest wykonywany rozwiązania poziomu i nie jest zależna od projektu, należy umieścić bezpośrednio pod `tools` folderu. Jest ona ignorowana, jeśli umieszczony w folderze struktury.
