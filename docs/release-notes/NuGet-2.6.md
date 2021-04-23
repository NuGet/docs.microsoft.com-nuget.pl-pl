---
title: Informacje o wersji nuGet 2.6
description: Informacje o wersji dla programu NuGet 2.6, w tym znane problemy, poprawki błędów, dodane funkcje i dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6b25b9df062afc88466ad107e718f632878debfc
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901424"
---
# <a name="nuget-26-release-notes"></a>Informacje o wersji nuGet 2.6

[Informacje o wersji nuGet 2.5](../release-notes/nuget-2.5.md)  |  [Informacje o wersji programu NuGet 2.6.1 dla programu WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 został wydany 26 czerwca 2013 r.

## <a name="notable-features-in-the-release"></a>Funkcje, które są dostępne w tej wersji

### <a name="support-for-visual-studio-2013"></a>Obsługa Visual Studio 2013

NuGet 2.6 to pierwsza wersja, która zapewnia obsługę Visual Studio 2013. Podobnie jak Visual Studio 2012, rozszerzenie Menedżer pakietów NuGet jest zawarte w każdej wersji Visual Studio.

Aby zapewnić najlepszą możliwą obsługę programu Visual Studio 2013 przy jednoczesnym zachowaniu obsługi zarówno wersji Visual Studio 2010, jak i Visual Studio 2012 oraz utrzymania możliwie najmniejszych rozmiarów rozszerzeń, produkujemy oddzielne rozszerzenie dla programu Visual Studio 2013, podczas gdy oryginalne rozszerzenie nadal jest ukierunkowane zarówno na program Visual Studio 2010, jak i 2012.

Począwszy od programu NuGet 2.6, opublikujemy dwa rozszerzenia, jak podano poniżej:

1. [NuGet Menedżer pakietów](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (dotyczy Visual Studio 2010 i 2012)
1. [NuGet Menedżer pakietów for Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Po podzielniu przycisk [nuget.org](https://nuget.org) strony głównej "Zainstaluj pakiet NuGet" umożliwia przejść do strony instalowania pakietu [NuGet,](../install-nuget-client-tools.md) na której można znaleźć więcej informacji na temat instalowania różnych klientów NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Obsługa przekształcania Web.config XDT

Jedną z najbardziej żądanych funkcji klienta NuGet było obsługa bardziej zaawansowanych przekształceń XML przy użyciu aparatu transformacji XDT, który jest używany w Visual Studio konfiguracji kompilacji.

W kwietniu 2013 r. ogłoszono dwa duże ogłoszenia dotyczące obsługi narzędzia NuGet dla narzędzia XDT. Pierwszą z nich było to, że sama biblioteka XDT została wydana jako pakiet [NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) i wydana jako [open source w edycie CodePlex.](http://xdt.codeplex.com/) W tym kroku aparat XDT był używany bezpłatnie przez inne oprogramowanie open source, w tym klienta NuGet. Drugim ogłoszeniem był plan obsługi użycia aparatu XDT do przekształceń w kliencie NuGet. Ta integracja obejmuje program NuGet 2.6.

#### <a name="how-it-works"></a>Jak to działa

Aby skorzystać z obsługi XDT narzędzia NuGet, mechanika wygląda podobnie do funkcji przekształcania [bieżącej konfiguracji](../create-packages/source-and-config-file-transformations.md).
Pliki przekształceń są dodawane do folderu zawartości pakietu. Jednak podczas gdy przekształcenia konfiguracji używają jednego pliku zarówno do instalacji, jak i dezinstalacji, przekształcenia XDT umożliwiają łatwa kontrolę nad obu tych procesów przy użyciu następujących plików:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Ponadto program NuGet używa sufiksu pliku do określenia, który aparat ma być uruchamiany dla przekształceń, dzięki czemu pakiety korzystające z istniejącego pliku web.config.transforms będą nadal działać. Przekształcenia XDT można również stosować do dowolnego pliku XML (nie tylko web.config), dzięki czemu można go wykorzystać w przypadku innych aplikacji w projekcie.

#### <a name="what-you-can-do-with-xdt"></a>Co można zrobić za pomocą narzędzia XDT

Jedną z największych zalet narzędzia XDT jest [prosta,](/previous-versions/aspnet/dd465326(v=vs.110)) ale zaawansowana składnia do manipulowania strukturą modelu DOM XML. Zamiast po prostu nakładać jedną stałą strukturę dokumentu na inną strukturę, XDT udostępnia kontrolki do dopasowywania elementów na różne sposoby, od prostego dopasowywania nazwy atrybutu do pełnej obsługi XPath. Po znalezioniu pasującego elementu lub zestawu elementów XDT udostępnia bogaty zestaw funkcji do manipulowania elementami, niezależnie od tego, czy oznacza to dodawanie, aktualizowanie lub usuwanie atrybutów, umieszczanie nowego elementu w określonej lokalizacji, zastępowanie lub usuwanie całego elementu i jego elementów.

### <a name="machine-wide-configuration"></a>Machine-Wide konfiguracji

Jedną z wielkich zalet pakietu NuGet jest to, że dzieli on duży plik wykonywalny lub bibliotekę na zestaw składników modułowych, które można zintegrować, a co najważniejsze jest utrzymywane i wersjonowane niezależnie. Efektem ubocznym tego jest jednak to, że konwencjonalna koncepcja produktu lub rodziny produktów staje się potencjalnie bardziej pofragmentowana.
Funkcja źródła pakietów niestandardowych nuGet zapewnia jeden ze sposobów organizowania pakietów; Jednak niestandardowych źródeł pakietów nie można odnaleźć samodzielnie.

Program NuGet 2.6 rozszerza logikę konfigurowania nuGet, wyszukując hierarchię folderów w ścieżce %ProgramData%/NuGet/Config. Instalatory produktów mogą dodawać niestandardowe pliki konfiguracji NuGet w tym folderze, aby zarejestrować niestandardowe źródło pakietów dla swoich produktów. Ponadto struktura folderów obsługuje semantykę produktu, wersji, a nawet sku środowiska IDE. Ustawienia z tych katalogów są stosowane w następującej kolejności ze strategią pierwszeństwa "ostatni w wins".

1. %ProgramData%\NuGet\Config \* .config
2. %ProgramData%\NuGet\Config \{ IDE} \* .config
3. %ProgramData%\NuGet\Config \{ IDE} \{ version} \* .config
4. %ProgramData%\NuGet\Config \{ IDE} \{ version} \{ SKU} \* .config

Na tej liście symbol zastępczy {IDE} jest specyficzny dla środowiska IDE, w którym jest uruchomiony program NuGet, więc w przypadku Visual Studio będzie to "VisualStudio". Symbole zastępcze {Version} i {SKU} są dostarczane przez środowiska IDE (np. "11.0" i "WDExpress", "VWDExpress" i "Pro"). Następnie folder może zawierać wiele różnych plików *.config.
W związku z tym firma składowa ACME może w ramach instalatora produktu dodać niestandardowe źródło pakietu, które będzie widoczne tylko w wersjach Professional i Ultimate programu Visual Studio 2012, tworząc następującą ścieżkę pliku:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Struktura folderów ułatwia programom, na przykład instalatorom oprogramowania, dodawanie źródeł pakietów dla komputera do konfiguracji nuGet, ale okno dialogowe konfiguracji NuGet zostało również zaktualizowane w celu umożliwienia rejestracji źródeł pakietów jako specyficznych dla użytkownika (np. zarejestrowanych w folderze %AppData%/NuGet/NuGet.Config) lub dla całej maszyny.

Ta funkcja jest wykorzystywana przez Visual Studio 2013, gdzie plik jest instalowany w:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

W tym pliku zostanie skonfigurowane nowe źródło pakietu o nazwie ".NET Framework Packages".

![Ustawienia szerokie maszyny pliku konfiguracji NuGet](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Kontekstowe wyszukiwanie

Ponieważ liczba pakietów obsługiwanych przez galerię NuGet stale rośnie w tempie wykładniczym, ulepszanie wyszukiwania pozostaje na początku listy priorytetów nuGet. Jedną z planowanych funkcji narzędzia NuGet jest wyszukiwanie kontekstowe, co oznacza, że program NuGet będzie używać informacji o wersji i sku programu Visual Studio, który jest przez Ciebie Visual Studio i typie projektu, który jest budowania, jako kryteriów określania istotności potencjalnych wyników wyszukiwania.

Począwszy od programu NuGet 2.6, za każdym razem, gdy pakiet jest instalowany, kontekst instalacji jest rejestrowany jako część danych operacji instalacji.  Wyszukiwania wysyłają również te same informacje kontekstowe, co umożliwi galerii NuGet zwiększenie wyników wyszukiwania dzięki trendom instalacji kontekstowej.  Przyszła aktualizacja galerii NuGet umożliwi zwiększenie istotności kontekstowej.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Śledzenie instalacji bezpośrednich a instalacje zależności

Autorzy pakietów coraz bardziej polegają na statystykach [pakietów podanych](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) w galerii NuGet.  Jednym z istotnych brakujących punktów danych, o które prosili autorzy, jest rozróżnienie między bezpośrednimi instalacjami pakietów a instalacjami zależności.  Do tej pory klient NuGet nie wysyłał żadnego kontekstu wokół operacji instalacji dotyczącej tego, czy deweloper zainstalował pakiet bezpośrednio, czy został zainstalowany w celu spełnienia zależności.
Począwszy od programu NuGet 2.6, te dane będą teraz wysyłane na czas operacji instalacji.  Statystyki pakietów w galerii NuGet uwidocznią te dane jako oddzielne operacje instalacji z sufiksem "-Dependency".

* Instalowanie
* Install-Dependency
* Aktualizacja
* Update-Dependency
* Ponowna instalacja
* Reinstall-Dependency

Oprócz innej nazwy operacji dla instalacji jest również rejestrowany identyfikator pakietu zależnego.  Przyszła aktualizacja galerii NuGet uwidoczni te dane w raportach, umożliwiając autorom pakietów pełne zrozumienie sposobu instalowania pakietów przez deweloperów.

## <a name="bug-fixes"></a>Poprawki błędów

Program NuGet 2.6 zawiera również kilka poprawek błędów. Aby uzyskać pełną listę elementów roboczych rozwiązanych w programie NuGet 2.6, zapoznaj się z artykułem Śledzenie problemów [NuGet dla tej wersji.](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)