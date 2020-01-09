---
title: Informacje o wersji narzędzia NuGet 2,6
description: Informacje o wersji programu NuGetobject dla programu WebMatrix, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5e80965aad4caa69130be31a37b7f5f5ffb12ea6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384127"
---
# <a name="nuget-26-release-notes"></a>Informacje o wersji narzędzia NuGet 2,6

[Informacje o wersji programu nuget 2,5](../release-notes/nuget-2.5.md) | [nugetobject dla informacji o wersji programu WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

Pakiet NuGet 2,6 został wydaną 26 czerwca 2013.

## <a name="notable-features-in-the-release"></a>Istotne funkcje w wersji

### <a name="support-for-visual-studio-2013"></a>Obsługa Visual Studio 2013

NuGet 2,6 to pierwsza wersja, która zapewnia obsługę Visual Studio 2013. Podobnie jak w przypadku programu Visual Studio 2012, rozszerzenie Menedżera pakietów NuGet jest dołączone do każdej wersji programu Visual Studio.

Aby zapewnić najlepszą możliwą pomoc techniczną dla Visual Studio 2013 przy jednoczesnym obsłudze zarówno programu Visual Studio 2010, jak i Visual Studio 2012 i zachować rozmiary rozszerzeń jako małe, firma Microsoft tworzy osobne rozszerzenie dla Visual Studio 2013 podczas gdy oryginalne rozszerzenie nadal dotyczy zarówno programu Visual Studio 2010, jak i 2012.

Począwszy od programu NuGet 2,6, zostaną opublikowane dwa rozszerzenia w następujący sposób:

1. [Menedżer pakietów NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (dotyczy programu Visual Studio 2010 i 2012)
1. [NuGet Package Manager for Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Dzięki temu podziale przycisk "Zainstaluj pakiet NuGet" strony głównej [NuGet.org](https://nuget.org) umożliwia przejście do strony [Instalowanie narzędzia NuGet](../install-nuget-client-tools.md) , na której można znaleźć więcej informacji na temat instalowania różnych klientów programu NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Obsługa transformacji w pliku Web. config XDT

Jedną z najważniejszych funkcji klienta NuGet jest obsługa bardziej zaawansowanych transformacji XML przy użyciu aparatu transformacji XDT, który jest używany w transformacjach konfiguracji kompilacji programu Visual Studio.

W kwietniu 2013 wprowadziliśmy dwa duże anonse dotyczące obsługi NuGet dla XDT. Początkowo była to, że sama sama Biblioteka XDT jest [wydawana jako pakiet NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) , i [Open Sourced in CodePlex](http://xdt.codeplex.com/). W tym kroku aparat XDT ma być używany bezpłatnie przez inne oprogramowanie "open source", w tym klienta NuGet. Drugi anons był planem do obsługi transformacji w kliencie NuGet przy użyciu aparatu XDT. Pakiet NuGet 2,6 obejmuje tę integrację.

#### <a name="how-it-works"></a>Jak to działa

Aby skorzystać z pomocy technicznej XDT narzędzia NuGet, Mechanics wyglądać podobnie jak w przypadku [bieżącej funkcji przekształcania konfiguracji](../create-packages/source-and-config-file-transformations.md).
Pliki transformacji są dodawane do folderu zawartości pakietu. Jednak podczas transformacji konfiguracji używany jest jeden plik do instalacji i dezinstalacji, przekształcenia XDT umożliwiają szczegółową kontrolę nad obydwoma procesami przy użyciu następujących plików:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Ponadto program NuGet używa sufiksu pliku do określenia, który aparat ma być uruchamiany dla transformacji, więc pakiety korzystające z istniejącej pliku Web. config. transformacje będą nadal działać. Przekształcenia XDT można także zastosować do dowolnego pliku XML (nie tylko Web. config), więc można go użyć do innych aplikacji w projekcie.

#### <a name="what-you-can-do-with-xdt"></a>Co możesz zrobić z XDT

Jedną z XDT największych jest [prosta, ale Zaawansowana składnia](https://docs.microsoft.com/previous-versions/aspnet/dd465326(v=vs.110)) służąca do manipulowania strukturą kodu XML dom. Zamiast po prostu nałożenie pojedynczej struktury dokumentu na inną strukturę, XDT zapewnia kontrolki do dopasowywania elementów na różne sposoby, od prostego dopasowania nazw atrybutów do pełnej obsługi XPath. Po znalezieniu pasującego elementu lub zestawu elementów XDT oferuje bogaty zestaw funkcji do manipulowania elementami, niezależnie od tego, czy oznacza to dodawanie, aktualizowanie i usuwanie atrybutów, umieszczanie nowego elementu w określonej lokalizacji lub zastępowanie lub usuwanie całego element i jego elementy podrzędne.

### <a name="machine-wide-configuration"></a>Konfiguracja całego komputera

Jedną z zalet NuGet jest uszkodzenie w inny sposób dużego pliku wykonywalnego lub biblioteki do zestawu składników modularnych, które mogą być zintegrowane, a które są w sposób niezależny obsługiwane. Jednym z efektów ubocznych jest jednak to, że konwencjonalne pomysły dotyczące produktu lub rodziny produktów staną się potencjalnie bardziej pofragmentowane.
Funkcja niestandardowe źródło pakietów narzędzia NuGet zapewnia jeden sposób organizowania pakietów. Niemniej jednak niestandardowe źródła pakietów nie są odnajdywane samodzielnie.

Pakiet NuGet 2,6 rozszerza logikę konfigurowania NuGet, przeszukując hierarchię folderów pod ścieżką% ProgramData%/NuGet/Config. Instalatorzy produktów mogą dodawać niestandardowe pliki konfiguracji NuGet w tym folderze w celu zarejestrowania niestandardowego źródła pakietów dla swoich produktów. Ponadto struktura folderów obsługuje semantykę produktu, wersji, a nawet jednostkę SKU IDE. Ustawienia z tych katalogów są stosowane w następującej kolejności przy użyciu strategii pierwszeństwa "Ostatnia w usłudze WINS".

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

Na tej liście symbol zastępczy {IDE} jest specyficzny dla środowiska IDE, w którym działa pakiet NuGet, więc w przypadku programu Visual Studio będzie to "VisualStudio". Symbole zastępcze {Version} i {SKU} są udostępniane przez IDE (np. "11,0" i "WDExpress", "VWDExpress" i "Pro"). Folder może zawierać wiele różnych plików *. config.
W związku z tym, firma ACME Component może w ramach swojego instalatora produktu dodać niestandardowe źródło pakietu, które będzie widoczne tylko w wersjach Professional i Ultimate programu Visual Studio 2012 przez utworzenie następującej ścieżki pliku:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Mimo że struktura folderów jest prosta dla programów, takich jak instalatorzy oprogramowania, aby dodać źródła pakietów dla całej maszyny do konfiguracji programu NuGet, okno dialogowe konfiguracji NuGet zostało także zaktualizowane, aby umożliwić rejestrację źródeł pakietów jako specyficznych dla użytkownika (np. zarejestrowanych w folderze% AppData%/NuGet/NuGet.Config) lub całej maszyny.

Ta funkcja jest używana przez Visual Studio 2013, w której plik jest instalowany w:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

W tym pliku jest skonfigurowane nowe źródło pakietu o nazwie ".NET Framework pakiety".

![Ustawienia całej maszyny pliku konfiguracji NuGet](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Wyszukiwanie Contextualizing

Ponieważ liczba pakietów obsłużonych przez galerię NuGet w dalszym ciągu rośnie w wykładniczym tempie, lepsze wyszukiwanie pozostanie kiedykolwiek w górnej części listy priorytetów NuGet. Jedną z zaplanowanych funkcji NuGet jest wyszukiwanie kontekstowe, co oznacza, że program NuGet będzie używać informacji o wersji i jednostce SKU programu Visual Studio, której używasz, oraz typu projektu, który tworzysz jako kryterium do określania znaczenia potencjalnego wyszukiwania uzyskane.

Począwszy od programu NuGet 2,6, za każdym razem, gdy pakiet jest zainstalowany, kontekst instalacji jest rejestrowany w ramach danych operacji instalacji.  Wyszukiwania również wysyłają te same informacje kontekstu, co umożliwi Galerii pakietów NuGet zwiększenie wyników wyszukiwania przez trendy instalacji kontekstowej.  Przyszła aktualizacja galerii NuGet umożliwi podwyższenie poziomu tego kontekstu.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Śledzenie instalacji bezpośrednich i instalacji zależności

Autorzy pakietów korzystają z dodatkowych i więcej informacji na temat [statystyk pakietów](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) dostępnych w galerii NuGet.  Jeden znaczący brakujący punkt danych, z którym poprosił autorzy, to rozróżnienie między bezpośrednimi instalacjami pakietów i instalacjami zależności.  Do tej pory klient NuGet nie wysłał żadnego kontekstu wokół operacji instalacji, niezależnie od tego, czy deweloper bezpośrednio zainstalował pakiet, czy został zainstalowany w celu spełnienia zależności.
Począwszy od programu NuGet 2,6, dane te będą teraz wysyłane do operacji instalacji.  Statystyki pakietów w galerii NuGet będą uwidaczniać te dane jako osobne operacje instalacji z sufiksem "zależność".

* Instalacja programu
* Zależność instalacji
* Aktualizowanie
* Zależność aktualizacji
* Ponowna instalacja
* Ponowna instalacja — zależność

Oprócz innej nazwy operacji identyfikator pakietu zależnego jest również rejestrowany do instalacji.  W przyszłej aktualizacji galerii NuGet zostaną ujawnione dane w raportach, dzięki czemu autorzy pakietu mogą w pełni zrozumieć, jak deweloperzy instalują swoje pakiety.

## <a name="bug-fixes"></a>Poprawki błędów

Pakiet NuGet 2,6 zawiera również kilka poprawek błędów. Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 2,6, zobacz [Śledzenie problemów NuGet dla tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).