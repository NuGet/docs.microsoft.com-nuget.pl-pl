---
title: Informacje o wersji NuGet 2.6 | Dokumentacja firmy Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Informacje o wersji dla tym znanych problemów, poprawki, dodatkowe funkcje i dcr 2.6 NuGet."
keywords: NuGet 2.6 informacje o wersji, poprawki, znanymi problemami, nowe funkcje, dcr
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2df9721e6941c110948af1a2d4ec4b7aeb476dd
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-26-release-notes"></a>Informacje o wersji version 2.6 NuGet

[Informacje o wersji NuGet 2.5](../release-notes/nuget-2.5.md) | [2.6.1 NuGet, aby uzyskać informacje o wersji programu WebMatrix](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 został wydany 26 czerwca 2013.

## <a name="notable-features-in-the-release"></a>Ważne funkcje w wersji

### <a name="support-for-visual-studio-2013"></a>Obsługa programu Visual Studio 2013

NuGet 2.6 jest pierwszą wersję, która zapewnia obsługę dla programu Visual Studio 2013. I jak Visual Studio 2012, rozszerzenie NuGet Package Manager znajduje się w każdej wersji programu Visual Studio.

Aby zapewnić najlepsze możliwe pomocy technicznej dla programu Visual Studio 2013 obsługi zarówno programu Visual Studio 2010 i Visual Studio 2012, i utrzymywanie możliwie najmniejsze rozmiary rozszerzenia, firma Microsoft tworzenie oddzielnych rozszerzenia dla programu Visual Studio 2013 podczas oryginalne rozszerzenie w dalszym ciągu docelowego zarówno programu Visual Studio 2010 oraz 2012.

Począwszy od wersji 2.6 NuGet, firma Microsoft będzie publikować dwóch rozszerzeń, jak pokazano poniżej:

1. [Menedżer pakietów NuGet](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (dotyczy programu Visual Studio 2010 i 2012)
1. [NuGet Package Manager for Visual Studio 2013](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Z tego podziału [nuget.org](https://nuget.org) przycisk "Instalowania NuGet" Strona główna umożliwia przejście do [instalowania NuGet](../install-nuget-client-tools.md) strony, gdzie można znaleźć więcej informacji na temat instalacji różnych klientów NuGet.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>Obsługa transformacji pliku Web.config XDT

Jedną z najbardziej wysokiej wymagane funkcje klienta NuGet została do obsługi bardziej zaawansowanych transformacji XML przy użyciu aparat przekształcania XDT, który jest używany w transformacji konfiguracji kompilacji programu Visual Studio.

W przypadku kwietnia 2013 wprowadziliśmy dwóch big ogłoszenia dotyczące NuGet obsługę XDT. Pierwszy został samej biblioteki XDT został on sam [wydane jako pakietu NuGet](https://nuget.org/packages/Microsoft.Web.Xdt) i [Otwórz powierzając jej ich konserwację w witrynie CodePlex](http://xdt.codeplex.com/). Ten krok włączony aparat XDT za darmo używanego przez inne oprogramowanie open source, w tym klienta NuGet. Drugi anons został planu, który będzie obsługiwał Użycie aparatu XDT przekształcenia w kliencie programu NuGet. NuGet 2.6 obejmuje tej integracji.

#### <a name="how-it-works"></a>Jak to działa

Aby skorzystać z pomocy technicznej XDT NuGet, sposobu podobne do tych [bieżącej konfiguracji funkcji przekształcenia](../create-packages/source-and-config-file-transformations.md).
Pliki transformacji zostaną dodane do folderu zawartości pakietu. Jednak przekształcenia konfiguracji używanie jednego pliku dla instalacji i dezinstalacji, przekształcenia XDT Włącz precyzyjną kontrolę nad obu tych procesów przy użyciu następujących plików:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Ponadto NuGet używa sufiks pliku w celu określenia, który aparat Uruchom dla przekształceń, aby pakiety przy użyciu istniejących web.config.transforms będą nadal działać. Przekształcenia XDT można również będą stosowane do dowolnego pliku XML (nie tylko plik web.config), więc można wykorzystać to dla innych aplikacji w projekcie.

#### <a name="what-you-can-do-with-xdt"></a>Co można zrobić XDT

Jeden sile największe firmy XDT jest jego [prostego, ale jednocześnie wydajną składnię](http://msdn.microsoft.com/library/dd465326.aspx) do manipulowania strukturę modelu DOM. XML Zamiast po prostu nakładanie jeden strukturę dokumentu stałej na inną strukturę, XDT zawiera formanty pasujących elementów na różne sposoby, od prostego atrybutu nazwy dopasowany do pełnej obsługi języka XPath. Po znalezieniu pasujący element lub zbiór elementów XDT zawiera bogaty zestaw funkcji do manipulowania elementów, czy oznacza to dodawanie, aktualizowanie, lub usuwanie atrybutów, umieszczenie nowego elementu z określonej lokalizacji lub zastępowanie lub usuwanie całą elementu i jego elementów podrzędnych.

### <a name="machine-wide-configuration"></a>Konfiguracja komputera

Jednym z bardzo silnych NuGet jest przerywa w dół w przeciwnym razie dużych plik wykonywalny lub biblioteka na zestaw składników moduły, które mogą zostać zintegrowane i najważniejsze utrzymywana oraz numerów wersji niezależnie. Jeden po stronie, jednak powoduje, że konwencjonalnej pomysł produktu lub rodziny produktów potencjalnie jest bardziej pofragmentowana.
Funkcja źródła niestandardowego pakietu NuGet zapewnia jeden sposób organizowania pakietów; źródeł niestandardowych pakietów nie są jednak wykrywalny samodzielnie.

NuGet 2.6 rozszerza logikę Konfigurowanie NuGet wyszukując hierarchii folder na ścieżce % ProgramData%/NuGet/Config. Instalatorzy produktu można dodać niestandardowe pliki konfiguracji NuGet w tym folderze, aby zarejestrować Źródło niestandardowe pakietu dla swoich produktów. Ponadto struktury folderów obsługuje semantyki produktu, wersję i nawet SKU IDE. Ustawienia z tych katalogów są stosowane w następującej kolejności ze strategią pierwszeństwo "ostatni w usłudze wins".

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{Version}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\*.config

Na tej liście symbol zastępczy {IDE} dotyczy IDE, w którym jest uruchomiona NuGet, tak więc w przypadku programu Visual Studio będzie "VisualStudio". {{Wersja} i {SKU} symbole zastępcze są udostępniane przez IDE (np. "11.0" i "WDExpress", "VWDExpress" i "Zaawansowany", odpowiednio). Folder następnie może zawierać wiele różnych *.config plików.
W związku z tym firmy składnika xyz w ramach ich Instalatora produktu, dodać źródło niestandardowe pakietu, które będą widoczne tylko w wersjach Professional i Ultimate programu Visual Studio 2012, tworząc następująca ścieżka pliku:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Podczas tej struktury folderów sprawia, że proste dla programów, takich jak pliki instalacyjne oprogramowania do dodania źródła pakietów dla komputera do konfiguracji w narzędziu NuGet, okna dialogowego konfiguracji NuGet również została zaktualizowana w celu umożliwienia rejestracji źródła pakietów jako albo specyficzne dla użytkownika (np. zarejestrowany w % AppData%/NuGet/NuGet.Config) lub komputera.

Ta funkcja jest wykorzystywany przez Visual Studio 2013 z zainstalowanym pliku na:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

W tym pliku nowe źródło pakietów o nazwie ".NET Framework Packages" jest skonfigurowana.

![Ustawienia dla całego komputera pliku konfiguracji NuGet](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Kontekstem wyszukiwania

W miarę liczba obsłużonych przez galerii NuGet pakietów rośnie w tempie wykładniczym, ulepszanie wyszukiwania kiedykolwiek pozostaje na początku listy Priorytet NuGet. Planowane funkcji programu NuGet jest wyszukiwanie kontekstowe, co oznacza, że NuGet będzie używać informacji o wersji i wersji programu Visual Studio używanego i typ projektu, który tworzysz jako kryterium określania istotność potencjalnych wyszukiwania wyniki.

Począwszy od wersji 2.6 NuGet, zawsze, gdy pakiet jest zainstalowany, w kontekście instalacji jest rejestrowany jako część danych operacji instalacji.  Wyszukuje również wysyłać te same informacje kontekstu, co pozwoli galerii NuGet w celu zwiększania wyników wyszukiwania przez trendów kontekstowe instalacji.  Przyszłej aktualizacji do galerii NuGet spowoduje włączenie tego zwiększania istotność kontekstowa.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Śledzenie bezpośredniej instalacji programu vs. Instaluje zależności

Autorzy pakietów są bardziej polegania na [statystyk pakietu](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) podanego w galerii NuGet.  Jedna duża ilość danych. Brak punktu, że się w opiniach autorów jest rozróżnianie między instaluje pakiet bezpośredniego i instalowanie zależności.  Do tej pory klienta NuGet nie wysłał żadnego kontekstu wokół operacja instalacji czy dewelopera bezpośrednio zainstalowany pakiet lub jeśli zainstalowano do zaspokojenia zależności.
Począwszy od wersji 2.6 NuGet, że dane zostaną wysłane teraz dla operacji instalacji.  Statystyki pakietu galerii NuGet uwidoczni danych jako osobne instalacji operacji z "-zależności" sufiks.

* Zainstaluj
* Zainstaluj zależności
* Aktualizacja
* Zależności aktualizacji
* Zainstaluj ponownie
* Ponownie zainstaluj zależności

Oprócz nazwy innej operacji identyfikator pakietu zależnego jest zarejestrowany dla instalacji.  Te dane w raportach, umożliwiając autorów pakietu w pełni zrozumieć sposób deweloperzy instalowania ich pakiety powoduje to udostępnienie przyszłej aktualizacji do galerii NuGet.

## <a name="bug-fixes"></a>Poprawki błędów

NuGet 2.6 zawiera również kilka poprawek. Pełną listę prac elementów usunięto w wersji NuGet 2.6, sprawdź widok [NuGet Tracker problem w tej wersji](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).