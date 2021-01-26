---
title: Informacje o wersji narzędzia NuGet 2.7.2
description: Informacje o wersji programu NuGet 2.7.2, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776780"
---
# <a name="nuget-272-release-notes"></a>Informacje o wersji narzędzia NuGet 2.7.2

Informacje o wersji narzędzia [NuGet 2.7.1](../release-notes/nuget-2.7.1.md)  |  [Informacje o wersji narzędzia NuGet 2,8](../release-notes/nuget-2.8.md)

Pakiet NuGet 2.7.2 został opublikowany od 11 listopada 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Warta poprawka i funkcje błędów

### <a name="license-text"></a>Tekst licencji
Przez jakiś czas firma Microsoft dołączyła pakiety NuGet dla kilku popularnych bibliotek typu open source w ramach domyślnych szablonów dla projektów aplikacji sieci Web w programie Visual Studio. jQuery jest prawdopodobnie najbardziej dobrze znanym przykładem tego typu biblioteki. Ze względu na umowę dotyczącą pomocy technicznej skojarzoną ze składnikami dostarczanymi wraz z produktem plik skryptu pakietu zawiera inny tekst licencji niż plik skryptu znaleziony w tym samym pakiecie w publicznej galerii nuget.org. Różnica w tekście może uniemożliwić aktualizowanie pakietów w wyniku różnych bloków tekstowych licencji, co sprawia, że pliki skryptów mają różne wartości skrótu zawartości (i dlatego są traktowane jako zmodyfikowane w projekcie).

Aby wyeliminować ten problem, program NuGet 2.7.2 umożliwia autorowi skryptu dołączenie bloku tekstu licencji w specjalnie oznaczonej sekcji, która wygląda następująco.

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

W przypadku aktualizowania pakietów z plikami zawartości zawierającymi ten blok NuGet nie jest składnikiem zawartości bloku w porównaniu z wersją w galerii NuGet i dlatego można ją usunąć i zaktualizować, tak jakby była zgodna z oryginalną kopią.

Ten blok jest identyfikowany przez tekst "NUGET: BEGIN LICENSE TEXT" i "NUGET: END LICENSE TEXT" w dowolnym miejscu w wierszu początku i końca.  Nie istnieją inne wymagania dotyczące formatowania, dzięki czemu ta funkcja może być używana w dowolnym typie pliku tekstowego niezależnie od języka.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Dodawanie przekierowań powiązań dla zestawów niezwiązanych z platformą
W przypadku zestawów, które są częścią .NET Framework, pakiet NuGet pomija Dodawanie przekierowań powiązań do pliku konfiguracyjnego aplikacji podczas aktualizacji pakietu. Ta poprawka dotyczy regresji w programie NuGet 2,7, w której przekierowania powiązań nie są dodawane dla niektórych zestawów, nawet jeśli te zestawy nie są uważane za część .NET Framework. Pakiet NuGet 2.7.2 przywraca poprzednie zachowanie NuGet 2,5 i 2,6 i dodaje przekierowania powiązań.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Instalowanie bibliotek przenośnych przy użyciu zainstalowanych narzędzi Xamarin
Gdy narzędzia programistyczne platformy Xamarin są zainstalowane na komputerze, modyfikują obsługiwane dane konfiguracji środowisk w celu określenia zgodności między istniejącymi kombinacjami platformy docelowej i platformami Xamarin. W wersji 2.7.2 pakiet NuGet jest teraz świadomy tych niejawnych reguł zgodności i dlatego ułatwia deweloperom kierowanie platform Xamarin do instalowania przenośnych bibliotek, które są zgodne z interfejsem Xamarin, ale nie są wyraźnie oznaczone jako takie w metadanych pakietu.

### <a name="machine-wide-configuration-settings-honored"></a>Zahonorowane ustawienia konfiguracji maszyny
W przypadku używania hierarchicznych plików Nuget.Config klucz repositoryPath nie jest uznawany za Nuget.Config plików znajdujących się najbliżej katalogu głównego rozwiązania. W Visual Studio 2013 pakiet NuGet instaluje niestandardowy plik Nuget.Config w lokalizacji% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config w celu dodania źródła pakietu "Microsoft i .NET". Z tego powodu obejście tego problemu przy użyciu niestandardowych repositoryPath w rozwiązaniu polega na usunięciu Nuget.Config na poziomie komputera, co oznacza również usunięcie źródła pakietu "Microsoft i .NET". Pakiet NuGet 2.7.2 jest teraz uznawany za reguły pierwszeństwa dla repositoryPath przy użyciu hierarchicznych plików Nuget.Config.

## <a name="all-changes"></a>Wszystkie zmiany
Aby zapoznać się z pełną listą elementów roboczych rozwiązanych w 2.7.2 NuGet, zobacz [Śledzenie problemów NuGet dla tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
