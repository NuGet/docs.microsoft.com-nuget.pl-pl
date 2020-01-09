---
title: Informacje o wersji narzędzia NuGet 2,0
description: Informacje o wersji programu NuGet 2,0, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 01fdbfafcaea009cf119dfa880b2b16539c9b088
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383070"
---
# <a name="nuget-20-release-notes"></a>Informacje o wersji narzędzia NuGet 2,0

[Informacje o wersji pakietu nuget 1,8](../release-notes/nuget-1.8.md) | [Informacje o wersji narzędzia NuGet 2,1](../release-notes/nuget-2.1.md)

Pakiet NuGet 2,0 został wydaną 19 czerwca 2012.

## <a name="known-installation-issue"></a>Znany problem z instalacją
W przypadku korzystania z programu VS 2010 z dodatkiem SP1 można napotkać błąd instalacji podczas próby uaktualnienia narzędzia NuGet, jeśli jest zainstalowana starsza wersja.

Obejście polega na prostu odinstalować pakiet NuGet, a następnie zainstalować go z galerii rozszerzeń programu VS.  Aby uzyskać więcej informacji, zobacz <https://support.microsoft.com/kb/2581019> lub [Przejdź bezpośrednio do poprawki programu vs](http://bit.ly/vsixcertfix).

Uwaga: Jeśli program Visual Studio nie zezwoli na odinstalowanie rozszerzenia (przycisk Odinstaluj jest wyłączony), prawdopodobnie trzeba będzie ponownie uruchomić program Visual Studio za pomocą polecenia "Uruchom jako administrator".

## <a name="package-restore-consent-is-now-active"></a>Wyrażanie zgody na przywracanie pakietu jest teraz aktywne

Zgodnie z opisem w tym [wpisie dotyczącym przywracania pakietów pakiet](http://blog.nuget.org/20120518/package-restore-and-consent.html)NuGet 2,0 będzie teraz wymagał zgody, aby umożliwić przywracanie pakietów w trybie online i pobrać pakiety. Upewnij się, że podano zgodę za pośrednictwem okna dialogowego konfiguracji Menedżera pakietów lub zmiennej środowiskowej EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Grupuj zależności według platform docelowych

Począwszy od wersji 2,0, zależności pakietów mogą się różnić w zależności od profilu struktury projektu docelowego. Jest to realizowane przy użyciu zaktualizowanego schematu `.nuspec`. Element `<dependencies>` może teraz zawierać zestaw `<group>` elementów. Każda grupa zawiera zero lub więcej elementów `<dependency>` i atrybut `targetFramework`. Wszystkie zależności wewnątrz grupy są instalowane razem, jeśli struktura docelowa jest zgodna z docelowym profilem platformy projektu. Na przykład:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

Należy zauważyć, że grupa może zawierać **zero** zależności. W powyższym przykładzie, jeśli pakiet jest zainstalowany w projekcie, który jest przeznaczony dla programu Silverlight 3,0 lub nowszego, nie zostaną zainstalowane żadne zależności. Jeśli pakiet jest zainstalowany w projekcie przeznaczonym dla programu .NET 4,0 lub nowszego, zostaną zainstalowane dwie zależności, jQuery i webaktywator.  Jeśli pakiet jest instalowany w projekcie, który jest przeznaczony dla wczesnej wersji tych 2 platform lub innych platform, RouteMagic 1.1.0 zostanie zainstalowana. Nie ma żadnego dziedziczenia między grupami. Jeśli platforma docelowa projektu jest zgodna z atrybutem `targetFramework` grupy, zostaną zainstalowane tylko zależności w ramach tej grupy.

Pakiet może określać zależności pakietu w dowolnym z dwóch formatów: starym formacie płaskiej listy elementów `<dependency>` lub grup. Jeśli jest używany format `<group>`, nie można zainstalować pakietu w wersjach programu NuGet wcześniejszych niż 2,0.

Należy zauważyć, że mieszanie dwóch formatów jest niedozwolone. Na przykład poniższy fragment kodu jest **nieprawidłowy** i zostanie odrzucony przez pakiet NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Grupowanie plików zawartości i skryptów programu PowerShell według platformy docelowej

Oprócz odwołań do zestawów, pliki zawartości i skrypty programu PowerShell mogą być również pogrupowane według platformy docelowej. Ta sama struktura folderów znaleziona w folderze `lib` do określania platformy docelowej można teraz zastosować w taki sam sposób, jak foldery `content` i `tools`. Na przykład:

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

**Uwaga**: ponieważ `init.ps1` jest wykonywany na poziomie rozwiązania i nie zależy od żadnego pojedynczego projektu, musi być umieszczony bezpośrednio pod folderem `tools`. Jeśli zostanie umieszczony w folderze specyficznym dla platformy, zostanie zignorowany.

Ponadto nową funkcją w programie NuGet 2,0 jest to, że folder struktury może być *pusty*, w takim przypadku pakiet NuGet nie dodaje odwołań do zestawów, nie dodaje plików zawartości ani nie uruchamia skryptów programu PowerShell dla konkretnej wersji platformy. W powyższym przykładzie folder `content\net40` jest pusty.

## <a name="improved-tab-completion-performance"></a>Ulepszona wydajność kończenia karty
Funkcja uzupełniania tabulatorów w konsoli Menedżera pakietów NuGet została zaktualizowana w celu znacznego zwiększenia wydajności. Nastąpi znacznie mniej opóźnienia od momentu naciśnięcia klawisza Tab do momentu wyświetlenia listy rozwijanej sugestii.

## <a name="bug-fixes"></a>Poprawki błędów
Pakiet NuGet 2,0 zawiera wiele poprawek błędów z naciskiem na zgodę i wydajność przywracania pakietu.
Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 2,0, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
