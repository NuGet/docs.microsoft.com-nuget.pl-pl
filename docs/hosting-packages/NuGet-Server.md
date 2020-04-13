---
title: Używanie pliku NuGet.Server do hosta kanałów nuget
description: Jak utworzyć i hostować źródło danych pakietu NuGet na dowolnym serwerze z uruchomionymi usługami IIS przy użyciu serwera NuGet.Server, udostępniając pakiety za pośrednictwem protokołu HTTP i OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79059565"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server to pakiet dostarczony przez fundację .NET, który tworzy aplikację ASP.NET, która może obsługiwać kanał informacyjny pakietu na dowolnym serwerze z uruchomiona usługami IIS. Po prostu powiedział, NuGet.Server sprawia, że folder na serwerze dostępne za pośrednictwem HTTP(S) (w szczególności OData). Jest łatwy w konfiguracji i najlepiej nadaje się do prostych scenariuszy.

1. Utwórz pustą aplikację sieci Web ASP.NET w programie Visual Studio i dodaj do niej pakiet NuGet.Server.
1. Skonfiguruj `Packages` folder w aplikacji i dodaj pakiety.
1. Wdrażanie aplikacji na odpowiednim serwerze.

W poniższych sekcjach opisano szczegółowo ten proces przy użyciu języka C#.

Jeśli masz dalsze pytania dotyczące programu NuGet.Server, utwórz problem w programie [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Tworzenie i wdrażanie ASP.NET aplikacji sieci Web za pomocą pliku NuGet.Server

1. W programie Visual Studio wybierz **pozycję Plik > nowy projekt >**, wyszukaj hasło "ASP.NET aplikacji sieci Web (.NET Framework)", wybierz pasujący szablon dla języka C#.

    ![Wybieranie szablonu projektu sieci Web programu .NET Framework](media/Hosting_00-NuGet.Server-ProjectType.png)

1. Ustaw **framework** na ".NET Framework 4.6".

    ![Ustalanie ram docelowych dla nowego projektu](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Nadaj aplikacji odpowiednią nazwę *inną* niż NuGet.Server, wybierz przycisk OK, a w następnym oknie dialogowym wybierz **pusty** szablon, a następnie wybierz **przycisk OK**.

    ![Wybieranie pustego projektu sieci Web](media/Hosting_02-NuGet.Server-Empty.png)

1. Kliknij prawym przyciskiem myszy projekt, wybierz polecenie **Zarządzaj pakietami NuGet**.

1. W interfejsie użytkownika Menedżera pakietów wybierz kartę **Przeglądaj,** a następnie wyszukaj i zainstaluj najnowszą wersję pakietu NuGet.Server, jeśli kierujesz reklamy na platformę .NET Framework 4.6. (Można go również zainstalować z Konsoli `Install-Package NuGet.Server`Menedżera pakietów za pomocą .) Zaakceptuj postanowienia licencyjne, jeśli zostanie wyświetlony monit.

    ![Instalowanie pakietu NuGet.Server](media/Hosting_03-NuGet.Server-Package.png)

1. Zainstalowanie serwera NuGet.Server konwertuje pustą aplikację sieci Web na źródło pakietu. Instaluje wiele innych pakietów, `Packages` tworzy folder w aplikacji `web.config` i modyfikuje, aby uwzględnić dodatkowe ustawienia (szczegółowe informacje można znaleźć w komentarzach w tym pliku).

    > [!Important]
    > Dokładnie `web.config` sprawdź po nuget.server pakiet zakończył jego modyfikacje tego pliku. NuGet.Server nie może zastąpić istniejące elementy, ale zamiast tego utworzyć zduplikowane elementy. Te duplikaty spowoduje "Wewnętrzny błąd serwera", gdy później spróbujesz uruchomić projekt. Na przykład, `web.config` jeśli `<compilation debug="true" targetFramework="4.5.2" />` zawiera przed zainstalowaniem NuGet.Server, pakiet nie zastępuje go, ale wstawia drugi `<compilation debug="true" targetFramework="4.6" />`. W takim przypadku usuń element ze starszą wersją frameworka.

1. Uruchom witrynę lokalnie w programie Visual Studio (przy użyciu **debugowania > start bez debugowania** lub Ctrl+F5). Strona główna zawiera adresy URL kanału informacyjnego pakietu, jak pokazano poniżej. Jeśli widzisz błędy, należy `web.config` dokładnie sprawdzić, czy nie ma zduplikowanych elementów, jak wspomniano wcześniej.

    ![Domyślna strona główna aplikacji z nuget.server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  Przy pierwszym uruchomieniu aplikacji nuget.server restrukturyzuje folder, `Packages` aby zawierał folder dla każdego pakietu. To pasuje do [układu magazynu lokalnego](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) wprowadzone z NuGet 3.3 w celu zwiększenia wydajności. Podczas dodawania większej liczby pakietów, kontynuuj podążanie za tą strukturą.

1. Po przetestowaniu wdrożenia lokalnego należy wdrożyć aplikację w dowolnej innej lokacji wewnętrznej lub zewnętrznej, zgodnie z potrzebami.

1. Po wdrożeniu do `http://<domain>`, adres URL, `http://<domain>/nuget`który jest używany dla źródła pakietu będzie .

## <a name="adding-packages-to-the-feed-externally"></a>Dodawanie pakietów do kanału zewnętrznego

Po uruchomieniu witryny NuGet.Server można dodać pakiety za pomocą [nuget](../reference/cli-reference/cli-ref-push.md) push `web.config`pod warunkiem ustawienia wartości klucza interfejsu API w pliku .

Po zainstalowaniu pakietu NuGet.Server `web.config` `appSetting/apiKey` zawiera pustą wartość:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Po `apiKey` pominięciu lub pustym wypychanie pakietów do kanału informacyjnego jest wyłączone.

Aby włączyć tę funkcję, `apiKey` ustaw wartość (najlepiej silne hasło) i `appSettings/requireApiKey` dodaj klucz `true`o nazwie o wartości:

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Jeśli serwer jest już zabezpieczony lub w przeciwnym razie nie jest wymagany klucz interfejsu API (na `false`przykład podczas korzystania z serwera prywatnego w lokalnej sieci zespołu), można ustawić opcję `requireApiKey` . Wszyscy użytkownicy z dostępem do serwera mogą następnie wypychać pakiety.

Począwszy od NuGet.Server 3.0.0, adres URL `http://<domain>/nuget`do pchania pakietów został zmieniony na . Przed wydaniem wersji 3.0.0 adres `http://<domain>/api/v2/package`URL wypychania wynosił .

Z NuGet 3.2.1 i nowsze, ten `/api/v2/package` starszy `/nuget` adres `enableLegacyPushRoute: true` URL jest włączona`NuGetODataConfig.cs` oprócz domyślnie za pomocą opcji w konfiguracji uruchamiania (domyślnie). Należy zauważyć, że ta funkcja nie działa, gdy wiele kanałów informacyjnych są hostowane w tym samym projekcie.

## <a name="removing-packages-from-the-feed"></a>Usuwanie opakowań z podajnika

W systemie NuGet.Server polecenie [nuget delete](../reference/cli-reference/cli-ref-delete.md) usuwa pakiet z repozytorium pod warunkiem, że klucz interfejsu API jest dołączany do komentarza.

Jeśli chcesz zmienić zachowanie, aby wykreślić pakiet zamiast (pozostawiając `enableDelisting` go `web.config` dostępny do przywrócenia pakietu), zmień klucz na true.

## <a name="configuring-the-packages-folder"></a>Konfigurowanie folderu Pakiety

W `NuGet.Server` 1.5 lub nowszym folderze można `appSettings/packagesPath` dostosować `web.config`folder pakietu za pomocą wartości w :

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath`może być ścieżką bezwzględną lub wirtualną.

Po `packagesPath` pominięciu lub pozostawieniu pustego folderu pakietów jest domyślny `~/Packages`folder .

## <a name="making-packages-available-when-you-publish-the-web-app"></a>Udostępnianie pakietów podczas publikowania aplikacji internetowej

Aby udostępnić pakiety w kanale informacyjnym podczas publikowania `.nupkg` aplikacji `Packages` na serwerze, należy dodać każdy plik do folderu w programie Visual Studio, a następnie ustawić **akcję kompilacji** każdego z nich na **zawartość** i **skopiuj do katalogu wyjściowego,** aby **zawsze skopiować:**

![Kopiowanie pakietów do folderu Pakiety w projekcie](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a>Informacje o wersji

Informacje o wersji dla serwera NuGet.Server są dostępne na [stronie wydania usługi GitHub](https://github.com/NuGet/NuGet.Server/releases).
Obejmuje to szczegółowe informacje na temat poprawek błędów i nowych funkcji, które są dodawane.

## <a name="nugetserver-support"></a>Pomoc techniczna usługi NuGet.Server

Aby uzyskać dodatkową pomoc dotyczącą korzystania z [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)pliku NuGet.Server, utwórz problem w programie .
