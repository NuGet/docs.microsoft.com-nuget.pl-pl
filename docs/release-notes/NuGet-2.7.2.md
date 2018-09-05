---
title: Informacje o wersji NuGet 2.7.2
description: Informacje o wersji NuGet 2.7.2, w tym — znane problemy, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3e63944a05f66d5dadf17c5d4b91d3bc4478bb33
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550073"
---
# <a name="nuget-272-release-notes"></a>Informacje o wersji NuGet 2.7.2

[Informacje o wersji NuGet 2.7.1](../release-notes/nuget-2.7.1.md) | [informacjach o wersji NuGet 2.8](../release-notes/nuget-2.8.md)

NuGet 2.7.2 została wydana 11 listopada 2013 r.

## <a name="noteworthy-bug-fixes-and-features"></a>Warte zauważenia poprawki i funkcje

### <a name="license-text"></a>Tekst licencji
Przez jakiś czas firma Microsoft dołączyła pakietów NuGet dla kilku popularnych bibliotek typu open source w ramach domyślnych szablonów projektów aplikacji sieci Web w programie Visual Studio. jQuery prawdopodobnie jest dobrze znanych przykład tego typu biblioteki. Ze względu na umowy dotyczącej pomocy technicznej, skojarzone ze składnikami, które są dostarczane wraz z produktem pliku skryptu pakietu zawiera tekst innej licencji, niż w pliku skryptu znaleziono w tym samym pakiecie galerii publicznej witrynie nuget.org. Ta różnica w tekście można zapobiec aktualizacjami pakietów z kontynuowaniem wyniku bloki tekstu innej licencji, powodując pliki skryptów, które mogą mieć różne wartości skrótów zawartości wartości (i dlatego powinien być traktowany jako zmodyfikowane w projekcie).

Aby rozwiązać ten problem, NuGet 2.7.2 umożliwia Autor skryptu dołączyć blok tekstu licencji w ramach sekcji specjalnie oznaczony, który wygląda w następujący sposób.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Podczas aktualizowania pakietów zawartości pliki zawierające ten blok NuGet nie uwzględnić zawartość bloku porównanie z wersją w galerii NuGet i można w związku z tym usuwanie i aktualizowanie zawartości pliku tak, jakby on zgodny oryginał.

Ten blok jest identyfikowany przez tekst "NUGET: Rozpocznij licencji TEXT" i "NUGET: koniec licencji TEXT" występujących w dowolnym miejscu na początku i końcowych wierszy.  Brak innych wymagań formatowania istnieje, dzięki czemu tej funkcji, które zostaną użyte w dowolnego typu pliku tekstowego, niezależnie od języka.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Dodaj powiązanie przekierowuje zestawy bez struktury
Dla zestawów, które są częścią programu .NET Framework NuGet pomija dodanie przekierowań powiązań do pliku konfiguracji aplikacji, podczas aktualizowania pakietu. Ta poprawka eliminuje Regresja w wersji 2.7 NuGet, według której przekierowania powiązań nie utrudniał dla niektórych zestawów, nawet jeśli te zestawy nie są uważana za część .NET Framework. NuGet 2.7.2 przywrócenie poprzedniej wersji NuGet 2.5 i 2.6 zachowanie i dodanie przekierowań powiązań.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Instalowanie bibliotek przenośnych z zainstalowanymi narzędziami platformy Xamarin
Po zainstalowaniu narzędzi programistycznych platformy Xamarin na komputerze mogą modyfikować dane konfiguracji obsługiwanych platform, aby określić zgodność między istniejących target framework kombinacji i platformy Xamarin. Za pomocą wersji 2.7.2 NuGet jest teraz pamiętać o tych reguł niejawnych zgodności i w związku z tym można łatwo dla deweloperów platformy Xamarin do zainstalowania bibliotek przenośnych, które są zgodne z platformy Xamarin, ale nie zostały jawnie oznaczone jako takie w pakiecie metadane sam.

### <a name="machine-wide-configuration-settings-honored"></a>Ustawienia konfiguracji komputera, honorowane
Korzystając z hierarchicznej plików w pliku Nuget.Config, klucz repositoryPath został nie już brane pod uwagę najbliżej katalog główny rozwiązania w pliku Nuget.Config plików. W programie Visual Studio 2013 NuGet instaluje niestandardowy plik Nuget.Config w %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config, aby można było dodać źródła pakietu "Firmy Microsoft i platformy .NET". W wyniku obejście dotyczące korzystania z niestandardowych repositoryPath w rozwiązaniu było usunąć maszyn na poziomie pliku Nuget.Config — co oznaczało, usuwając źródła pakietu "Firmy Microsoft i platformy .NET". NuGet 2.7.2 teraz honoruje reguły pierwszeństwa repositoryPath, korzystając z hierarchicznej plików w pliku Nuget.Config.

## <a name="all-changes"></a>Wszystkie zmiany
Pełną listę prac elementy rozwiązane w NuGet 2.7.2, sprawdź widok [NuGet narzędzie do śledzenia problemów w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
