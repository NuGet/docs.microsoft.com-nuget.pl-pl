---
title: Informacje o wersji NuGet 2.0 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji dotyczące tym znanych problemów, poprawki, dodatkowe funkcje i dcr NuGet w wersji 2.0."
keywords: NuGet 2.0 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: eaa3c8db1cce72ff93671a1df63698748cdfab70
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-20-release-notes"></a>Informacje o wersji 2.0 NuGet

[Informacje o wersji NuGet 1.8](../release-notes/nuget-1.8.md) | [NuGet 2.1 informacje o wersji](../release-notes/nuget-2.1.md)

19 czerwca 2012 został wydany NuGet 2.0.

## <a name="known-installation-issue"></a>Znane problem
Jeśli korzystasz z VS 2010 z dodatkiem SP1, możesz napotkać błąd instalacji podczas próby uaktualnienia NuGet, jeśli masz starszą wersję zainstalowane.

Obejście jest po prostu odinstalować NuGet, a następnie zainstaluj go z galerii rozszerzeń programu VS.  Zobacz [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) uzyskać więcej informacji, lub [przejdź bezpośrednio do poprawki VS](http://bit.ly/vsixcertfix).

Uwaga: Jeśli program Visual Studio nie pozwalają na odinstalować rozszerzenia (przycisk Odinstaluj jest wyłączony), następnie prawdopodobnie konieczne ponowne uruchomienie programu Visual Studio za pomocą polecenia "Uruchom jako Administrator".

## <a name="package-restore-consent-is-now-active"></a>Jest teraz aktywny zgody przywracania pakietu

Zgodnie z opisem w tym [post na zgody przywracania pakietu](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 będzie teraz wymagać o wyrażenie zgody umożliwiające przywracanie pakietów przejść do trybu online i pobrać pakietów. Upewnij się, że podanych zgody za pomocą okna dialogowego konfiguracji Menedżera pakietów lub zmiennej środowiskowej EnableNuGetPackageRestore.

## <a name="group-dependencies-by-target-frameworks"></a>Zależności grupy według platform docelowych

Począwszy od wersji 2.0, pakiet, który może różnić się zależności oparte na profil platformy docelowej projektu. Odbywa się przy użyciu zaktualizowanych `.nuspec` schematu. `<dependencies>` Element teraz może zawierać zestaw `<group>` elementów. Każda grupa zawiera zero lub więcej `<dependency>` elementów i `targetFramework` atrybutu. Wszystkie zależności w grupie są zainstalowane jednocześnie, jeśli platforma docelowa jest zgodna z profil platformy docelowej projektu. Na przykład:

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

Należy pamiętać, że grupa może zawierać **zero** zależności. W powyższym przykładzie Jeśli pakiet jest zainstalowany w projekcie, którego celem Silverlight 3.0 lub nowszej, zależności nie zostanie zainstalowana. Jeśli pakiet jest zainstalowany w projekcie, przeznaczonego dla programu .NET 4.0 lub nowszy, dwie zależności, jQuery i WebActivator, zostanie zainstalowana.  Po zainstalowaniu pakietu do projektu przeznaczonego dla tych platform 2 lub innych framework wcześniejszą wersję RouteMagic 1.1.0 zostanie zainstalowana. Nie istnieje żadne dziedziczenia między grupami. Jeśli platforma docelowa projektu odpowiada `targetFramework` atrybutu grupy, tylko zależności w ramach tej grupy zostaną zainstalowane.

Pakiet można określić zależności pakietów w jednym z dwóch formatów: starym formacie płaska lista `<dependency>` elementy lub grup. Jeśli `<group>` format jest używany, nie można zainstalować pakietu, w wersjach starszych niż 2.0 programu NuGet.

Należy pamiętać, że mieszanie dwa formaty jest niedozwolone. Na przykład poniższy fragment kodu jest **nieprawidłowy** i zostanie odrzucony przez narzędzie NuGet.

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

Oprócz odwołania do zestawów pliki zawartości i skryptów programu PowerShell również można przedstawić w rozbiciu platformy docelowej. Znaleziono taką samą strukturę folderów w `lib` folder służący do określania platformy docelowej teraz mogą być stosowane w taki sam sposób, aby `content` i `tools` folderów. Na przykład:

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

**Uwaga**: ponieważ `init.ps1` jest wykonywane na poziomie rozwiązania i jest niezależne od dowolnego pojedynczego projektu, musi on być umieszczony bezpośrednio pod `tools` folderu. Umieszczony w folderze określonej struktury, będą ignorowane.

Nową funkcją w NuGet 2.0 jest również można folderze struktury *pusty*, w którym to przypadku NuGet zostanie nie dodać odwołania do zestawów, dodać pliki zawartości lub uruchamiać skrypty programu PowerShell dla konkretnego framework w wersji. W przykładzie powyżej folderu `content\net40` jest pusta.

## <a name="improved-tab-completion-performance"></a>Ulepszone kartę ukończenia wydajności
Karta funkcję uzupełniania w konsoli Menedżera pakietów NuGet została zaktualizowana do znacznie poprawić wydajność. Będzie znacznie mniej opóźnienia od momentu, gdy zostanie naciśnięty klawisz tab, aż pojawi się lista rozwijana uwag.

## <a name="bug-fixes"></a>Poprawki błędów
NuGet 2.0 zawiera wiele poprawek usterek, ze szczególnym uwzględnieniem zgody przywracania pakietu i wydajność.
Pełną listę prac elementów usunięto w wersji NuGet 2.0, sprawdź widok [NuGet Tracker problem w tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
