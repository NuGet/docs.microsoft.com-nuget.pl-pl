---
title: "NuGet często zadawane pytania | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/11/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 199a915d-9595-4ae2-a1fb-b15da6d7735a
description: "Typowe pytania i odpowiedzi przy użyciu narzędzia NuGet w wierszu polecenia, a w programie Visual Studio i pracy z galerii NuGet."
keywords: "Wersje pakietu NuGet pytań i odpowiedzi, pytania i odpowiedzi, typowe problemy, wersje NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f029af78edfcc5e542c5df2d4d6db8eeaebc3068
ms.sourcegitcommit: d576d84fb4b6a178eb2ac11f55deb08ac771ba1c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2018
---
# <a name="nuget-frequently-asked-questions"></a>NuGet często zadawane pytania

W tym temacie:

- [Wprowadzenie](#getting-started)
- [NuGet w programie Visual Studio](#nuget-in-visual-studio)
- [Wiersz polecenia NuGet](#nuget-command-line)
- [NuGet Package Manager Console](#nuget-package-manager-console)
- [Tworzenie i publikowanie pakietów](#creating-and-publishing-packages)
- [Praca z pakietami](#working-with-packages)
- [Zarządzanie pakietami na nuget.org](#managing-packages-on-nugetorg)
- [nuget.org niedostępny](#nugetorg-not-accessible)

## <a name="getting-started"></a>Wprowadzenie

**Co to jest wymagany do uruchamiania NuGet?**

Wszystkie informacje dotyczące narzędzia wiersza polecenia i interfejsu użytkownika są dostępne w [Przewodnik instalacji](../guides/install-nuget.md).

**NuGet obsługuje Mono?**

Narzędzie wiersza polecenia `nuget.exe`, tworzy i uruchamiana Mono 3.2 + oraz pakiety można tworzyć w Mono.

Mimo że `nuget.exe` działa w pełni w systemie Windows, istnieją znane problemy w systemie Linux i OS X. znajduje się w [wystawia Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) w witrynie GitHub.

A [graficznego klienta](https://github.com/mrward/monodevelop-nuget-addin) jest dostępna jako dodatek do MonoDevelop.

**Jak można określić pakiet zawiera i czy jest ona stabilna i przydatne w przypadku mojej aplikacji?**

Podstawowym źródłem szkoleniowe dotyczące pakietu jest stroną listy na nuget.org (lub innej prywatnej źródła danych). Każda strona pakietu na nuget.org zawiera opis pakietu, jego Historia wersji i statystyki użycia. **Informacji** sekcja na stronie pakiet zawiera również link do witryny sieci web projektu, w którym zwykle znaleźć wiele przykłady i inne dokumentacji, aby uzyskać więcej informacji, sposobu używania pakietu.

Aby uzyskać więcej informacji, zobacz [wyszukiwanie i Wybieranie pakietów](../Consume-Packages/Finding-and-Choosing-Packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet w programie Visual Studio

**Jak NuGet jest obsługiwane w różnych produktów Visual Studio?**

- Program Visual Studio w systemie Windows obsługuje [interfejsu użytkownika Menedżera pakietów](../tools/Package-Manager-UI.md) i [Konsola Menedżera pakietów](../tools/Package-Manager-Console.md).
- Visual Studio for Mac ma wbudowane funkcje NuGet, zgodnie z opisem na [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (wszystkie platformy) nie ma żadnych bezpośrednich integracji z programem NuGet. Użyj [interfejsu wiersza polecenia NuGet](../tools/nuget-exe-CLI-Reference.md) lub [dotnet interfejsu wiersza polecenia](../tools/dotnet-commands.md).
- Visual Studio Team Services zapewnia [kroku kompilacji pod kątem przywracania pakietów NuGet](/vsts/build-release/tasks/package/nuget). Możesz również [pakietu NuGet prywatnych hosta źródła na Team Services](https://www.visualstudio.com/docs/package/nuget/publish).

**Jak sprawdzić dokładnej wersji narzędzia NuGet, które są zainstalowane**

W programie Visual Studio, użyj **Pomoc > Microsoft Visual Studio** polecenia i przyjrzyj się wersja wyświetlana obok **Menedżera pakietów NuGet**.

Można również uruchomić konsoli Menedżera pakietów (**Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów**), a następnie wprowadź `$host` Aby wyświetlić informacje o tym wersję NuGet.

**Jakich języków programowania są obsługiwane przez narzędzie NuGet?**

NuGet zwykle działa w przypadku języków .NET i jest przeznaczony do bibliotek .NET do projektu. Ponieważ obsługuje ona również automatyzacji MSBuild i Visual Studio w niektórych typów projektów, obsługuje ona również inne projekty i języki do różnych stopni.

Najnowszą wersję programu NuGet obsługuje C#, Visual Basic, F #, WiX i C++.

**Szablony projektów, które są obsługiwane przez narzędzie NuGet?**

NuGet zawiera pełną obsługę różnych szablonów projektu, takie jak Windows, sieci Web, chmur, SharePoint, Wix i tak dalej.

**Jak zaktualizować pakiety, które są częścią szablony programu Visual Studio?**

Przejdź do **aktualizacje** w Interfejsie użytkownika Menedżera pakietów i zaznacz **Aktualizuj wszystkie**, lub użyj [ `Update-Package` polecenia](../Tools/ps-ref-update-package.md) w konsoli Menedżera pakietów.

Aby zaktualizować samego szablonu, należy ręcznie zaktualizować repozytorium szablonu. Zobacz [blog Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) na ten temat. Uwaga to zrobić na własne ryzyko, ponieważ ręcznej aktualizacji może spowodować uszkodzenie szablonu, jeśli najnowszą wersję wszystkich zależności nie są zgodne ze sobą.

**Można użyć NuGet poza programu Visual Studio?**

Tak, NuGet działa bezpośrednio z poziomu wiersza polecenia. Zobacz [Przewodnik instalacji](../guides/install-nuget.md) i [odwołania interfejsu wiersza polecenia](../tools/nuget-exe-CLI-Reference.md).

## <a name="nuget-command-line"></a>Wiersz polecenia NuGet

**Jak uzyskać najnowszą wersję narzędzia wiersza polecenia NuGet?**

Zobacz [Przewodnik instalacji](../guides/install-nuget.md).

**Co to jest licencja na nuget.exe?**

Możesz wykonać ponowną dystrybucję nuget.exe zgodnie z warunkami licencji MIT. Jest odpowiedzialny za aktualizacji i obsługi kopie nuget.exe, który chcesz ponownie rozesłać.

**Czy jest możliwe rozszerzenie NuGet narzędzia wiersza polecenia**

Tak, istnieje możliwość dodawania niestandardowych poleceń do `nuget.exe`, zgodnie z opisem w [post Tomasz Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Konsola Menedżera pakietów NuGet (Visual Studio w systemie Windows)

**Jak uzyskać dostęp do obiektu DTE w konsoli Menedżera pakietów?**

Obiekt najwyższego poziomu w modelu obiektu automatyzacji programu Visual Studio jest wywołać obiekt DTE (Development Tools Environment). Zapewnia to za pośrednictwem zmiennej o nazwie konsoli `$DTE`. Aby uzyskać więcej informacji, zobacz [omówienie modelu automatyzacji](/visualstudio/extensibility/internals/automation-model-overview) w dokumentacji programu Visual Studio Extensibility.

**Próbie rzutowania $DTE zmienną typu DTE2, ale występuje błąd: nie można przekonwertować wartości "EnvDTE.DTEClass" typu "EnvDTE.DTEClass" na typ "EnvDTE80.DTE2". Co jest nie tak?**

Jest to znany problem dotyczący współdziałania programu PowerShell z obiektu COM. Spróbuj wykonać następujące czynności:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface`Funkcja pomocnika jest dodawany przez hosta programu NuGet PowerShell.

## <a name="creating-and-publishing-packages"></a>Tworzenie i publikowanie pakietów

**Jak wyświetlić listę Mój pakiet w źródło danych?**

Zobacz [tworzenie i publikowania pakietu](../quickstart/create-and-publish-a-package.md).

**Mam wiele wersji biblioteki, które odnoszą się do różnych wersji programu .NET Framework. Jak zbudować pojedynczy pakiet, który obsługuje tę funkcję?**

Zobacz [obsługi wielu wersje programu .NET Framework i profile](../create-packages/supporting-multiple-target-frameworks.md).

**Jak skonfigurować własną repozytorium lub źródła danych?**

Zobacz [hostingu — Omówienie pakietów](../hosting-packages/overview.md).

**Jak przesłać pakiety do mojego NuGet źródła danych zbiorczych**

Zobacz [zbiorcze publikowania pakietów NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Praca z pakietami

**Jaka jest różnica między pakietem poziom projektu i pakietu poziomu rozwiązania?**

Pakiet rozwiązanie na poziomie (NuGet 3.x+) jest zainstalowana tylko raz w rozwiązaniu i jest dostępna dla wszystkich projektów w rozwiązaniu. Pakiet poziom projektu jest zainstalowany w każdym projekcie, który korzysta z niego. Pakiet poziomu rozwiązania może również zainstalować nowych poleceń, które mogą być wywoływane z poziomu konsoli Menedżera pakietów.

**Czy jest możliwe, można zainstalować pakietów NuGet bez łączności z Internetem?**

Tak, zobacz Scott Hanselman blogu [sposobu dostępu NuGet, gdy działa nuget.org (lub jesteś na płaszczyźnie)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).

**Jak zainstalować pakiety w innej lokalizacji niż domyślny folder pakiety?**

Ustaw [ `repositoryPath` ](../Schema/nuget-config-file.md#config-section) w `Nuget.Config` przy użyciu `nuget config -set repositoryPath=<path>`.

**Jak uniknąć dodawania do folderu pakietów NuGet do kontroli źródła**

Ustaw [ `disableSourceControlIntegration` ](../Schema/nuget-config-file.md#solution-section) w `Nuget.Config` do `true`. Ta działa klucza w rozwiązaniu poziomu i dlatego musi zostać dodany do `$(Solutiondir)\.nuget\Nuget.Config` pliku. Włączanie Przywracanie pakietu z programu Visual Studio automatycznie tworzy ten plik.

**Jak wyłączyć przywracania pakietu**

Zobacz [Włączanie i wyłączanie Przywracanie pakietu](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

**Dlaczego otrzymuję błąd "Nie można rozpoznać zależności błąd" podczas instalowania lokalnego pakietu z zależności zdalnych?**

Musisz wybrać **wszystkie** źródła podczas instalowania lokalnego pakietu w projekcie. To agreguje wszystkich źródeł danych zamiast przy użyciu tylko jednego. Przyczyna ten błąd pojawia się jest, że użytkownicy lokalnego repozytorium często chcą uniknąć przypadkowego instalowania zdalnego pakietu z powodu firmowe zasady.

**Mam wiele projektów, w tym samym folderze, do czego służy packages.config oddzielne pliki dla każdego projektu?**

W większości projektów miejsca zamieszkania osobne projekty w oddzielnych folderach, nie jest to problem jak identyfikuje NuGet `packages.config` plików w każdym projekcie. Nuget 3.3 + i jest wiele projektów, w tym samym folderze, można wstawić nazwę projektu w `packages.config` nazw plików, użyj wzorca `packages.{project-name}.config`, i NuGet korzysta z tego pliku.

To nie jest problem przy użyciu PackageReference, ponieważ każdy plik projektu zawiera własną listę zależności.

**Nuget.org nie jest wyświetlane na liście repozytoriów, jak pobrać go ponownie?**

- Dodaj `https://api.nuget.org/v3/index.json` do listy źródeł, lub
- Usuń `%appdata%\.nuget\NuGet.Config` i pozwól NuGet, utwórz go ponownie.

**Jakie są domyślne licencji warunki Jeśli pakietu nie zawierają informacje o licencji określonego?**

Każdy pakiet jest objęte postanowienia, które są dołączone do pakietu. Należy przejrzeć postanowienia mające zastosowanie przed uzyskiwanie dostępu do, pobierania lub uzyskiwania wszystkie pakiety. Na nuget.org, użyj **informacje dotyczące licencji** łącze na stronie pakiet.

Jeśli pakiet nie określa postanowień licencyjnych, skontaktuj się z właścicielem pakietu bezpośrednio za pomocą **skontaktuj się z właścicieli** łącze na stronie pakiet nuget.org. Microsoft nie licencji jakiejkolwiek własności intelektualnej użytkownikowi od innych dostawców pakietu i nie jest odpowiedzialny za informacji dostarczonych przez strony trzecie.

## <a name="managing-packages-on-nugetorg"></a>Zarządzanie pakietami na nuget.org

**Metadane pakietów można edytować po jest przekazane? Dlaczego wymagają edycji plik nuspec i przekazać nowy pakiet do wprowadzania zmian do pakietu metadanych?**

NuGet wymaga wszystkich pakietów, były podpisane. Zasada projektowania podpisywania pakietu jest, że zawartość podpisanego pakietu musi być niezmienne, która obejmuje plik nuspec. Edytowanie metadanych pakietu powoduje zmian w plik nuspec, unieważnienie istniejących podpisów. Zaleca się zmodyfikowanie istniejącej przepływy pracy, aby nie wymagają edycji metadanych pakietu po utworzeniu pakietu.

Należy pamiętać, że zależności dla pakietu są generowane automatycznie z pakietu się i nie można edytować.

Ponadto przekazywania pakietów do [staging.nuget.org](http://staging.nuget.org) jest doskonałym sposobem testowanie i weryfikowanie pakietu bez udostępniania pakietu w publicznej galerii.

**Czy jest możliwe do zarezerwowania nazwy pakietów, które zostaną opublikowane w przyszłości?**

Tak. Identyfikatory pakietów można zarezerwować na [nuget.org](https://www.nuget.org/) przez zażądanie prefiks Identyfikatora pakietu dla Twojego konta. Aby poprosić o prefiks Identyfikatora pakietu, wysyłanie poczty do konta (nuget.org Nazwa wyświetlana pakietu właściciela i prefiks Identyfikatora żądanego pakietu w).  

**Jak potwierdzić prawa własności do pakietów?**

Zobacz [Zarządzanie właścicieli pakietu na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**Sposób postępowania z właścicielem pakietu, który narusza Moje licencji na oprogramowanie**

Firma Microsoft zachęca społeczności NuGet współdziałają ze sobą rozwiązywać wszelkie sporów, które mogą wystąpić podczas między właścicieli pakietu i innego oprogramowania. Firma Microsoft ma co [rozstrzygania procesu rozpoznawania](../policies/dispute-resolution.md) do wykonania przed żądaniem administratorom nuget.org intercede.

**Przekaż moje pakietów testowych do nuget.org jest zalecane?**

Do celów testowych można użyć [staging.nuget.org](http://staging.nuget.org), lub alternatywne publiczne serwery NuGet, takich jak [myget.org](https://myget.org) lub [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Należy pamiętać, że pakiety przekazane do staging.nuget.org mogą nie zostać zachowane. Zobacz [Podgląd praktyczny brak jakichkolwiek](http://blog.nuget.org/20130419/goodbye-preview.html).

**Co to jest maksymalny rozmiar pakietów, które można przekazać do nuget.org?**

nuget.org umożliwia pakietów do 250MB, ale firma Microsoft zaleca się utrzymywanie pakietów w obszarze 1MB, jeśli to możliwe, a następnie połącz pakietów przy użyciu zależności. Zasadą zawierać tylko jeden zestaw, aby uniknąć kolizji pakietów.

NuGet korzysta z protokołu HTTP do pobierania pakietów, więc pakietów większych niż mniejszych wyższe prawdopodobieństwo instaluje nie powiodło się.

Istnieje możliwość udostępniania zależności między kilka pakietów, co mniejszy rozmiar całkowitą pobierania dla konsumentów pakietów NuGet.

Zależności są prawie statyczna i nigdy nie zmiany. Po usunięciu błędu w kodzie, zależności nie muszą zostać zaktualizowane. Jeśli pakietu zależności, przechodzili reshipping pakietów większych zawsze. Dzieląc pakietów NuGet w zależności powiązane, uaktualnienia są bardziej szczegółowych dla konsumentów do pakietu.

## <a name="nugetorg-not-accessible"></a>nuget.org niedostępny

**Dlaczego nie można pobrać pakietów z ani przekazywać pakiety do nuget.org?**

Najpierw upewnij się, że używasz najnowszej wersji programu NuGet. Jeśli w tej wersji zakończy się niepowodzeniem, [się z pomocą techniczną](https://www.nuget.org/policies/Contact) i podaj dodatkowego połączenia Rozwiązywanie problemów z informacje w tym:

- Wersja programu NuGet używasz
- Używanego źródła pakietu
- Dziennik przywracania o poziomie szczegółowości szczegółowe
- MTR lub Fiddler dane śledzenia (zobacz poniżej)
- Obszar geograficzny
- Wersji systemu operacyjnego
- Konfiguracja maszyny (Procesora i sieci, dysk twardy)
- Określa, czy jest komputer serwera proxy lub zapory
- Wersje programu .NET, które są zainstalowane na tym komputerze
- Wersje narzędzi i platform, takich jak .NET interfejsu wiersza polecenia lub DNU, którego używasz

*Aby przechwycić MTR:*

- Pobierz WinMTR z [http://winmtr.net/download/](http://winmtr.net/)
- Wprowadź `api.nuget.org` jako nazwę hosta i kliknij przycisk **Start**.
- Poczekaj na **wysłane** kolumny > = 100.

    ![Przechwytywanie MTR](media/mtr.png)

- Skopiować tekst do Schowka.

*Aby przechwycić Fiddler:*

- Zainstaluj najnowszą wersję pakietu [Fiddler](http://www.telerik.com/download/fiddler).
- Uruchom narzędzie Fiddler i Wyłącz Przechwytywanie ruchu przy użyciu **pliku > przechwytywania ruchu** menu.
- Usuń wszystkie sesje (Wybierz wszystkie elementy na liście, naciśnij klawisz **usunąć** klucza).
- Konfigurowanie narzędzia Fiddler do przechwytywania ruchu HTTPS, sprawdzając **ruchu HTTPS odszyfrować** w **HTTPS** karcie **Narzędzia > Opcje Fiddler...**  menu.
- Zamknij program Visual Studio.
- Włącz **pliku > przechwytywania ruchu** menu.
- Uruchom program Visual Studio lub nuget.exe .exe i wykonać akcje, które nie działają. Ruch generowany przez te akcje powinny być widoczne w narzędziu Fiddler.
- Po akcje zostało uruchomione, użyj **Plik > Zapisz > wszystkie sesje** do przechowywania przechwyconego sesji.

Uwaga: może być konieczne można ustawić `HTTP_PROXY` zmienną środowiskową `http://127.0.0.1:8888` dla routingu ruchu NuGet przez Fiddler.

W przypadku niepowodzenia spróbuj [porady wymienione w tym wpisie StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

**Co to są punkty końcowe interfejsu API dla nuget.org?**

W wersji 3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (należy pamiętać, że interfejs API w wersji 2 jest przestarzała i nie działa z programem NuGet 4.)
