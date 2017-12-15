---
title: Informacje o wersji NuGet 2.7.2 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c775d1d7-de26-476c-bf9e-0cf95986a22f
description: "Informacje o wersji programu NuGet 2.7.2 tym — znane problemy, poprawki, dodatkowe funkcje i dcr."
keywords: NuGet 2.7.2 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5bb1eb346666c5d5ee790fcdcd7d844bfd37b22e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-272-release-notes"></a>Informacje o wersji NuGet 2.7.2

[Informacje o wersji NuGet 2.7.1](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 informacje o wersji](../release-notes/nuget-2.8.md)

NuGet 2.7.2 została wydana 11 listopad 2013.

## <a name="noteworthy-bug-fixes-and-features"></a>Warte wymienienia poprawki i funkcje

### <a name="license-text"></a>Tekst licencji
Przez jakiś czas Microsoft uwzględniła pakietów NuGet dla kilku popularnych bibliotek open source jako część domyślnych szablonów dla projektów aplikacji sieci Web w programie Visual Studio. dobrze znane przykładem tego typu biblioteki jest prawdopodobnie jQuery. Z powodu umowy pomocy technicznej, skojarzone ze składnikami, które są dostarczane wraz z produktem plik skryptu pakietu zawiera tekst innej licencji niż plik skryptu znalezione w pakiecie w galerii nuget.org publicznych. Ta różnica w tekście można zapobiec aktualizacji pakietu z kontynuowaniem wyniku bloki tekstu innej licencji powoduje plików skryptów przeznaczonych do wartości skrótu zawartości innego (i dlatego powinien być traktowany jako zmodyfikowane w projekcie).

Aby uniknąć tego problemu, NuGet 2.7.2 umożliwia autorowi skryptu obejmują bloku tekstu licencji w ramach sekcji specjalnie oznaczony, która wygląda w następujący sposób.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Podczas aktualizacji pakietów z zawartością pliki zawierające ten blok NuGet nie uwzględnić zawartość bloku podczas porównywania wersji w galerii NuGet i w związku z tym usunąć i zaktualizować zawartości pliku tak, jakby było zgodne z oryginalną kopię.

Ten blok jest identyfikowane przez tekstem "NUGET: Rozpocznij licencji" i "NUGET: koniec licencji TEXT" występujących w dowolnym miejscu na początku i końcowych wierszy.  Inne formatowania nie istnieją żadne wymagania, dzięki czemu ta funkcja umożliwia dowolny typ pliku tekstowego, niezależnie od języka.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Dodaj przekierowania powiązania dla zestawów bez struktury
Dla zestawów, które są częścią programu .NET Framework NuGet pomija Dodawanie przekierowania powiązania do pliku konfiguracji aplikacji, podczas aktualizowania pakietu. Ta poprawka eliminuje Regresja w 2.7 NuGet zgodnie z którymi przekierowania powiązania nie są dodano w programie niektóre zestawy, nawet jeśli te zestawy nie są uznawane za częścią programu .NET Framework. NuGet 2.7.2 przywraca poprzedniej 2.5 NuGet i zachowanie 2.6 i dodaje przekierowania wiązań.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Instalowanie przenośnych bibliotek z zainstalowanymi narzędziami Xamarin
Po zainstalowaniu na komputerze narzędzia do programowania dla platformy Xamarin modyfikują dane konfiguracji obsługiwanych platform, aby określić zgodność istniejących kombinacji framework docelowych i platform Xamarin. Wersją 2.7.2 NuGet zna teraz tych zasad zgodności niejawne i w związku z tym ułatwia dla deweloperów korzystających platformy Xamarin zainstalować przenośnych bibliotek, które są zgodne z Xamarin, ale nie zostało oznaczone jako takie w pakiecie metadane samej siebie.

### <a name="machine-wide-configuration-settings-honored"></a>Ustawienia konfiguracji komputera honorowane
Używając hierarchiczna pliki Nuget.Config, klucz repositoryPath nie został jest honorowane plików Nuget.Config najbardziej zbliżony do katalogu głównego rozwiązania. W programie Visual Studio 2013 NuGet instaluje niestandardowego pliku Nuget.Config na %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config aby można było dodać źródła pakietu "Microsoft i .NET". W związku z tym obejścia dla przy użyciu niestandardowych repositoryPath w rozwiązaniu było usunąć plik Nuget.Config poziom maszyny — co oznaczało, również usunięcie źródła pakietu "Microsoft i .NET". NuGet 2.7.2 teraz honoruje reguły pierwszeństwo repositoryPath korzystania z plików Nuget.Config hierarchicznej.

## <a name="all-changes"></a>Wszystkie zmiany
Pełną listę prac elementów usunięto w wersji NuGet 2.7.2, sprawdź widok [NuGet Tracker problem w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
