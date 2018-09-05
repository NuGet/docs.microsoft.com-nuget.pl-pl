---
title: Informacje o wersji 2.0 programu NuGet
description: Informacje o wersji programu NuGet w tym znanych problemów, poprawki, funkcje dodane i DCRs w wersji 2.0.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547578"
---
# <a name="nuget-20-release-notes"></a>Informacje o wersji 2.0 programu NuGet

[Informacje o wersji NuGet 1.8](../release-notes/nuget-1.8.md) | [informacjach o wersji NuGet 2.1](../release-notes/nuget-2.1.md)

NuGet w wersji 2.0 została wydana 19 czerwca 2012 r.

## <a name="known-installation-issue"></a>Problem z instalacją znane
Jeśli używasz programu VS 2010 z dodatkiem SP1, możesz napotkać błąd instalacji podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.

Obejście polega na po prostu Odinstaluj NuGet, a następnie zainstalować go z galerii rozszerzeń programu VS.  Zobacz [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) uzyskać więcej informacji, lub [przejdź bezpośrednio do poprawki programu VS](http://bit.ly/vsixcertfix).

Uwaga: Jeśli program Visual Studio nie pozwalają na odinstalować rozszerzenie (przycisk Odinstaluj jest wyłączony), prawdopodobnie musisz ponownie program Visual Studio za pomocą polecenia "Uruchom jako Administrator".

## <a name="package-restore-consent-is-now-active"></a>Pakiet przywracania zgody jest teraz aktywna

Zgodnie z opisem w tym [publikować zgody przywracania pakietu](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet w wersji 2.0 będzie wymagać teraz od o wyrażenie zgody umożliwiające przywracanie pakietu przejdź do trybu online i pobierania pakietów. Upewnij się, czy podane zgodę za pomocą okna dialogowego konfiguracji dla Menedżera pakietów lub zmiennej środowiskowej EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Grupa zależności według platform docelowych

Począwszy od wersji 2.0, pakietów, które mogą się różnić w zależności oparte na profilu framework projektu docelowego. Jest to realizowane przy użyciu zaktualizowanych `.nuspec` schematu. `<dependencies>` Elementu może teraz zawierać zestaw `<group>` elementów. Każda grupa zawiera zero lub więcej `<dependency>` elementy i `targetFramework` atrybutu. Wszystkie zależności wewnątrz grupy są instalowane razem, gdy platforma docelowa jest zgodny z profil platformy docelowej projektu. Na przykład:

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

Należy zauważyć, że grupa może zawierać **zero** zależności. W powyższym przykładzie Jeśli pakiet jest zainstalowany w projekcie, który jest przeznaczony dla programu Silverlight 3.0 lub nowszej, żadne zależności zostanie zainstalowana. Jeśli pakiet jest zainstalowany w projekcie, który jest przeznaczony dla programu .NET 4.0 lub nowszy, dwie zależności, jQuery i WebActivator, zostanie zainstalowana.  Jeśli pakiet jest zainstalowany w projekcie, który jest przeznaczony dla starszej wersji tych struktur 2 lub innych framework, zostanie zainstalowana RouteMagic 1.1.0. Brak nie dziedziczenia między grupami. Jeśli platforma docelowa projektu odpowiada `targetFramework` atrybut grupy, tylko zależności w ramach tej grupy zostaną zainstalowane.

Pakiet można określić zależności pakietów w jednym z dwóch formatów: stary format płaską listę `<dependency>` elementów lub grup. Jeśli `<group>` jest używany format, nie można zainstalować pakietu do pakietu nuget w wersji wcześniejszej niż w wersji 2.0.

Należy pamiętać, że mieszanie dwa formaty jest niedozwolone. Na przykład poniższy fragment kodu jest **nieprawidłowy** i zostanie odrzucony przez NuGet.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Pliki zawartości i skryptów programu PowerShell są grupowane według platformy docelowej

Oprócz odwołania do zestawów pliki zawartości i skryptów programu PowerShell także można grupować według wartości docelowej. Tę samą strukturę folderów znaleziony w `lib` folderu do określania wartości docelowej można teraz stosować w taki sam sposób, aby `content` i `tools` folderów. Na przykład:

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

**Uwaga**: ponieważ `init.ps1` jest wykonywane na poziomie rozwiązania i jest nie jest ona zależna od dowolnego pojedynczego projektu, musi zostać umieszczony bezpośrednio pod `tools` folderu. Umieszczony w folderze określonej platformy, zostaną zignorowane.

Ponadto jest nowa funkcja NuGet w wersji 2.0, że folder struktury może być *pusty*, w którym to przypadku NuGet zostanie nie Dodawanie odwołania do zestawów, dodać pliki zawartości lub Uruchamiaj skrypty programu PowerShell dla konkretnego framework w wersji. W przykładzie powyżej folderu `content\net40` jest pusty.

## <a name="improved-tab-completion-performance"></a>Wydajność uzupełniania ulepszone karty
Funkcję uzupełniania kartę w konsoli Menedżera pakietów NuGet został zaktualizowany w celu znacznego podniesienia wydajności. Będzie znacznie mniejsze opóźnienie od chwili, gdy naciskania klawisza tab, aż pojawi się lista rozwijana sugestii.

## <a name="bug-fixes"></a>Poprawki błędów
NuGet w wersji 2.0 obejmuje wiele poprawek błędów, z naciskiem na wydajność i zgody przywracania pakietu.
Aby uzyskać pełną listę prac elementy rozwiązane w NuGet w wersji 2.0, widok [NuGet narzędzie do śledzenia problemów w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
