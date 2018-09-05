---
title: Informacje o wersji 2.6 NuGet
description: Informacje o wersji programu NuGet 2.6.1 dla programu WebMatrix, w tym znanych problemów, poprawki, funkcje dodane i DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f011a8db7ac2067a2ed7db67849d63f7dd40d1ce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551946"
---
# <a name="nuget-26-release-notes"></a>Informacje o wersji 2.6 NuGet

[Informacje o wersji NuGet 2.5](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 dla programu WebMatrix informacje o wersji](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 został wydany 26 czerwca 2013 r.

## <a name="notable-features-in-the-release"></a>Ważne funkcje w wersji

### <a name="support-for-visual-studio-2013"></a>Obsługa programu Visual Studio 2013

NuGet 2.6 to pierwsze wydanie, które zapewnia obsługę programu Visual Studio 2013. A jak Visual Studio 2012, rozszerzenie Menedżera pakietów NuGet jest zawarte w każdej wersji programu Visual Studio.

Aby zapewnić najlepszą możliwą obsługę programu Visual Studio 2013 podczas nadal obsługi programu Visual Studio 2010 i Visual Studio 2012 i utrzymywanie rozmiary rozszerzenie tak małej, jak to możliwe, firma Microsoft produkuje osobne rozszerzenie dla programu Visual Studio 2013 podczas oryginalne rozszerzenie nadal pod kątem programu Visual Studio 2010 i 2012.

Począwszy od wersji 2.6 NuGet, opublikujemy odpowiednie dwa rozszerzenia zgodnie z poniższymi instrukcjami:

1. [Menedżer pakietów NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (dotyczy programu Visual Studio 2010 i 2012)
1. [NuGet Package Manager for Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Z tego podziału [nuget.org](https://nuget.org) przycisk "Zainstaluj NuGet" Strona główna spowoduje przejście do [instalacji NuGet](../install-nuget-client-tools.md) strony, gdzie można znaleźć więcej informacji na temat instalacji różnych klientów NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Obsługa przekształcania XDT Web.config

Jedną z najbardziej wysoce żądanych funkcji dla klienta programu NuGet został do obsługi bardziej zaawansowane transformacje XML przy użyciu aparatu przekształcania XDT, który jest używany w przekształcenia konfiguracji kompilacji programu Visual Studio.

W kwietniu 2013 wprowadziliśmy dwie big ogłoszenia dotyczące Obsługa NuGet dla XDT. Pierwszy został sama biblioteka XDT został on sam [wydane jako pakiet NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) i [open source w witrynie CodePlex](http://xdt.codeplex.com/). W tym kroku włączony aparat XDT być swobodnie używane przez innego oprogramowania typu open source, w tym klienta programu NuGet. Drugim etapem jest planu, który będzie obsługiwał Użycie aparatu XDT przekształcenia w kliencie programu NuGet. NuGet 2.6 zawiera tej integracji.

#### <a name="how-it-works"></a>Jak to działa

Aby móc korzystać z pomocy technicznej XDT NuGet, mechanizmach wyglądać podobnie do osób, [bieżącej funkcji przekształcenia konfiguracji](../create-packages/source-and-config-file-transformations.md).
Pliki transformacji są dodawane do folderu zawartości pakietu. Jednak podczas konfiguracji przekształcenia na użytek pojedynczego pliku instalacji i dezinstalacji, przekształcenia XDT Włącz szczegółową kontrolę nad tym oba procesy przy użyciu następujących plików:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Ponadto NuGet używa sufiks pliku, aby określić, który aparat są uruchamiane dla przekształceń, więc pakiety przy użyciu istniejących web.config.transforms będą nadal działać. Przekształcenia XDT można również będą stosowane do każdego pliku XML (nie tylko web.config), dzięki czemu można korzystać z tego dla innych aplikacji w projekcie.

#### <a name="what-you-can-do-with-xdt"></a>Co można zrobić za pomocą XDT

Jednym z największych sił firmy XDT jest jego [składni prosty, lecz wydajny](http://msdn.microsoft.com/library/dd465326.aspx) do manipulowania strukturę modelu DOM. XML Zamiast po prostu nałożenie jedną strukturę dokumentu stałą na inną strukturę, XDT udostępnia mechanizmy kontroli do dopasowania elementów w na różne sposoby, od prostego atrybutu Dopasowywanie nazw pełnej obsługi XPath. Gdy zostanie znaleziony pasujący element lub zbiór elementów XDT zapewnia bogaty zestaw funkcji, manipulowanie elementami, czy oznacza to, dodawanie, aktualizowanie lub usuwanie atrybutów, umieszczenie nowego elementu w określonej lokalizacji lub zastępowanie lub usuwanie całą element i jego elementów podrzędnych.

### <a name="machine-wide-configuration"></a>Konfiguracja komputera

Jedną z zalet doskonałe NuGet jest przerywa w dół w przeciwnym razie duży plik wykonywalny lub biblioteka do zestawu składników moduły, które mogą być zintegrowane i najważniejsze utrzymywana oraz numerów wersji niezależnie. Jeden efekt uboczny tej, jest jednak, że konwencjonalne koncepcję produktu lub rodziny produktów potencjalnie zwiększaniem się poziomu fragmentacji.
Funkcja źródła niestandardowy pakiet NuGet zawiera jeden sposób organizowania pakietów; niestandardowy pakiet źródeł nie są jednak wykrywalny własnych.

NuGet 2.6 rozszerza logikę Konfigurowanie NuGet, wyszukując hierarchia folderów w ścieżce % ProgramData%/NuGet/Config. Instalatory produktu można dodać niestandardowe pliki konfiguracji NuGet w tym folderze można zarejestrować Źródło niestandardowe pakietu dla swoich produktów. Ponadto struktura folderów obsługuje semantyki dla produktu, wersja i nawet jednostki SKU środowiska IDE. Ustawienia z tych katalogów są stosowane w następującej kolejności ze strategią pierwszeństwo "ostatnie w usłudze wins".

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

Na tej liście symbol zastępczy {IDE} dotyczy środowiska IDE, w którym jest uruchomiona NuGet, tak więc w przypadku programu Visual Studio będzie "Visual Studio". {Version} i {SKU} symbole zastępcze są udostępniane przez środowisko IDE (np. "11.0" i "WDExpress", "VWDExpress" i "Zaawansowany", odpowiednio). Folder następnie może zawierać wiele różnych *.config plików.
W związku z tym firmy składnik xyz w ramach ich Instalatora produktu, dodać źródła niestandardowego pakietu, która będzie widoczna tylko w wersjach Professional i Ultimate Visual Studio 2012, tworząc następującą ścieżkę pliku:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Gdy struktura folderów sprawia, że proste dla programów, takich jak instalatory oprogramowania, aby dodać źródła pakietu komputera do konfiguracji NuGet, w oknie dialogowym konfiguracji NuGet został także zaktualizowany i aby umożliwić rejestrację źródła pakietów jako albo specyficzne dla użytkownika (np. zarejestrowany w lokalizacji % AppData%/NuGet/NuGet.Config) lub dla komputera.

Ta funkcja jest wykorzystywany przez Visual Studio 2013, gdzie plik jest zainstalowany na:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

W tym pliku nowe źródło pakietu o nazwie ".NET Framework Packages" jest skonfigurowany.

![Ustawienia dla całego komputera pliku konfiguracyjnego NuGet](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Wyszukiwanie uczestnika

Jak stale rośnie w tempie wykładniczym, liczba pakietów obsługiwanych przez galerii pakietów NuGet, ulepszanie wyszukiwania nigdy nie pozostaje w górnej części listy Priorytet NuGet. Jednym z planowanych funkcji NuGet jest kontekstowe wyszukiwania, co oznacza, że NuGet będzie używać informacji na temat wersji i jednostka SKU programu Visual Studio, którego używasz i typu projektu, który jest kompilowany jako kryterium ustalania przydatność wyszukiwania potencjalnych wyniki.

Począwszy od wersji 2.6 NuGet, każdym razem, gdy pakiet jest zainstalowany, kontekst instalacji jest rejestrowany jako część danych operacji instalacji.  Wyszukuje również wysyłać te same informacje kontekstu, co umożliwi użytkownikom galerii pakietów NuGet do poprawienia wyników wyszukiwania trendami kontekstowych instalacji.  Przyszłej aktualizacji w galerii NuGet umożliwi to ulepszanie kontekstową istotności.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Śledzenie bezpośredniej instalacji programu vs. Instaluje zależności

Autorzy pakietów korzysta z bardziej [statystyk pakietu](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) udostępniane w galerii NuGet.  Jedna duża ilość danych. Brak wskazują, że autorzy poprosiło o opis jest rozróżnianie bezpośrednie pakiet instaluje i instaluje zależności.  Do tej pory klienta programu NuGet nie wysłał wszystkich kontekstach wokół operacji instalacji, czy deweloper bezpośrednio zainstalowany pakiet lub jeśli została zainstalowana w celu spełnienia zależności.
Począwszy od wersji 2.6 NuGet, że dane zostaną wysłane teraz dla operacji instalacji.  Statystyki pakietu w galerii NuGet udostępni te dane jako oddzielna instalacja operacje, za pomocą "-zależności" sufiks.

* Zainstaluj
* Instalacja zależności
* Aktualizacja
* Zależności aktualizacji
* Zainstaluj ponownie
* Zainstaluj ponownie zależności

Wraz z nazwą innej operacji identyfikator pakietu zależnego jest zarejestrowany dla instalacji.  Przyszła aktualizacja w galerii NuGet udostępni te dane w raportach, umożliwiając autorom pakietów w pełni zrozumieć, jak deweloperzy instalujesz swoich pakietów.

## <a name="bug-fixes"></a>Poprawki błędów

NuGet 2.6 zawiera także kilka poprawek usterek. Pełną listę prac elementy rozwiązane w NuGet 2.6, widok [NuGet narzędzie do śledzenia problemów w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).