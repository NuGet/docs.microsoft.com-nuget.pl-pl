---
title: Używanie narzędzia NuGet. Server do hostowania źródeł danych NuGet
description: Jak utworzyć i hostować źródło pakietów NuGet na dowolnym serwerze, na którym są uruchomione usługi IIS, przy użyciu NuGet. Server, dzięki czemu pakiety są dostępne za pośrednictwem protokołów HTTP i OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 734f0a609f243c7bdb218a53ed664de68c707dd7
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317647"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet. Server jest pakietem dostarczanym przez platformę .NET Foundation, który tworzy aplikację ASP.NET, która umożliwia hostowanie kanału informacyjnego pakietu na dowolnym serwerze, na którym są uruchomione usługi IIS. Po prostu program NuGet. Server udostępnia folder na serwerze za pośrednictwem protokołu HTTP (w przypadku usługi OData). Jest ona łatwa do skonfigurowania i jest Najlepsza w przypadku prostych scenariuszy.

1. Utwórz pustą aplikację sieci Web ASP.NET w programie Visual Studio i Dodaj do niej pakiet NuGet. Server.
1. `Packages` Skonfiguruj folder w aplikacji i Dodaj pakiety.
1. Wdróż aplikację na odpowiednim serwerze.

W poniższych sekcjach szczegółowo omówiono ten proces, korzystając C#z programu.

Jeśli masz więcej pytań na [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)temat NuGet. Server, Utwórz problem.

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Tworzenie i wdrażanie aplikacji sieci Web ASP.NET za pomocą narzędzia NuGet. Server

1. W programie Visual Studio wybierz pozycję **plik > nowy > projekt**, wyszukaj ciąg "ASP.NET", wybierz szablon **aplikacja sieci Web ASP.NET (.NET Framework)** dla C#systemu, a następnie ustaw opcję ".NET Framework 4,6":

    ![Ustawianie platformy docelowej dla nowego projektu](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Nadaj aplikacji odpowiednią nazwę *inną* niż NuGet. Server, wybierz pozycję OK, a następnie w następnym oknie dialogowym wybierz **pusty** szablon, a następnie wybierz **przycisk OK**.

1. Kliknij prawym przyciskiem myszy projekt, a następnie wybierz pozycję **Zarządzaj pakietami NuGet**.

1. W interfejsie użytkownika Menedżera pakietów wybierz kartę **przeglądanie** , a następnie wyszukaj i zainstaluj najnowszą wersję pakietu NuGet. Server, jeśli jesteś celem .NET Framework 4,6. (Można go także zainstalować z konsoli Menedżera pakietów w programie `Install-Package NuGet.Server`). Zaakceptuj postanowienia licencyjne, jeśli zostanie wyświetlony monit.

    ![Instalowanie pakietu NuGet. Server](media/Hosting_02-NuGet.Server-Package.png)

1. Instalowanie NuGet. serwer konwertuje pustą aplikację sieci Web na źródło pakietu. Instaluje różne inne pakiety, tworzy `Packages` folder w aplikacji i modyfikuje `web.config` w celu uwzględnienia dodatkowych ustawień (szczegółowe informacje znajdują się w komentarzach w tym pliku).

    > [!Important]
    > Uważnie Zbadaj `web.config` po wykonaniu przez pakiet NuGet. Server zmian w tym pliku. NuGet. Server nie może zastąpić istniejących elementów, ale zamiast tego utworzyć zduplikowane elementy. Te duplikaty spowodują "wewnętrzny błąd serwera" podczas późniejszej próby uruchomienia projektu. Na przykład jeśli `web.config` zawiera `<compilation debug="true" targetFramework="4.5.2" />` przed zainstalowaniem NuGet. Server, pakiet nie zastępuje go, ale wstawia sekundę `<compilation debug="true" targetFramework="4.6" />`. W takim przypadku Usuń element ze starszą wersją struktury.

1. Aby udostępnić pakiety w kanale informacyjnym po opublikowaniu aplikacji na serwerze, `.nupkg` Dodaj wszystkie pliki `Packages` do folderu w programie Visual Studio, a następnie ustaw dla każdej z nich **akcję kompilacji** na **zawartość** i **Skopiuj ją do katalogu wyjściowego** , aby **Kopiuj zawsze**:

    ![Kopiowanie pakietów do folderu Packages w projekcie](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Uruchom lokację lokalnie w programie Visual Studio (przy użyciu **debugowania > Uruchom bez debugowania** lub CTRL + F5). Strona główna zawiera adresy URL kanału informacyjnego pakietu, jak pokazano poniżej. Jeśli widzisz błędy, uważnie Przeprowadź `web.config` inspekcję pod kątem zduplikowanych elementów, które zostały zanotowane wcześniej z krok 5.

    ![Domyślna strona główna aplikacji z pakietem NuGet. Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. Kliknij **tutaj** w obszarze przedstawionym powyżej, aby zobaczyć źródło danych OData pakietów.

1. Przy pierwszym uruchomieniu aplikacji NuGet. serwer ponownie tworzy strukturę `Packages` folderu tak, aby zawierał folder dla każdego pakietu. Jest to zgodne z [lokalnym układem magazynu](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) wprowadzonym z pakietem NuGet 3,3 w celu zwiększenia wydajności. W przypadku dodawania kolejnych pakietów Kontynuuj korzystanie z tej struktury.

1. Po przetestowaniu lokalnego wdrożenia należy wdrożyć aplikację w dowolnej innej lokacji wewnętrznej lub zewnętrznej, zgodnie z potrzebami.

1. Po wdrożeniu `http://<domain>`w programie adres URL używany dla źródła pakietu będzie miał `http://<domain>/nuget`wartość.

## <a name="configuring-the-packages-folder"></a>Konfigurowanie folderu Packages

W `NuGet.Server` przypadku 1,5 i nowszych można dokładniej skonfigurować folder pakietu `appSetting/packagesPath` przy użyciu wartości w `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath`może być ścieżką bezwzględną lub wirtualną.

Gdy `packagesPath` zostanie pominięte lub pozostawione puste, folder Packages jest wartością `~/Packages`domyślną.

## <a name="adding-packages-to-the-feed-externally"></a>Zewnętrzne dodawanie pakietów do źródła danych

Po uruchomieniu lokacji NuGet. Server można dodać pakiety przy użyciu [wypychania NuGet](../reference/cli-reference/cli-ref-push.md) , pod warunkiem, że wartość klucza interfejsu API jest `web.config`ustawiona w.

Po zainstalowaniu pakietu NuGet. Server program `web.config` zawiera pustą `appSetting/apiKey` wartość:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Gdy `apiKey` zostanie pominięte lub puste, wypychanie pakietów do źródła danych jest wyłączone.

Aby włączyć tę funkcję, należy ustawić `apiKey` na wartość (idealnie silne hasło) i dodać klucz o nazwie `appSettings/requireApiKey` z wartością `true`:

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Jeśli serwer jest już zabezpieczony lub nie jest wymagany klucz interfejsu API (na przykład w przypadku korzystania z serwera prywatnego w lokalnej sieci zespołowej), można ustawić na `requireApiKey` `false`wartość. Wszyscy użytkownicy z dostępem do serwera mogą następnie wysyłać pakiety.

## <a name="removing-packages-from-the-feed"></a>Usuwanie pakietów ze źródła danych

W pakiecie NuGet. Server polecenie [NuGet Delete](../reference/cli-reference/cli-ref-delete.md) usuwa pakiet z repozytorium, pod warunkiem, że dołączysz klucz interfejsu API z komentarzem.

Jeśli chcesz zmienić zachowanie w celu wyłączania pakietu zamiast niego (pozostawiając dostęp do przywracania pakietu), Zmień `enableDelisting` klucz w `web.config` na true.

## <a name="nugetserver-support"></a>NuGet. Server — obsługa

Aby uzyskać dodatkową pomoc dotyczącą korzystania z programu NuGet. Server [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues), Utwórz problem w systemie.