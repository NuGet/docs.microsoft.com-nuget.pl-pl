---
title: Za pomocą NuGet.Server do hostowania NuGet źródła danych
description: Jak tworzyć i hostować pakiet NuGet źródła danych na dowolnym serwerze z uruchomionymi usługami IIS przy użyciu NuGet.Server, udostępnianie pakietów za pośrednictwem protokołu HTTP i OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: e99d42744ec860976ae098be94e747ec4bc9a7c6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551959"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server to pakiet dostarczone przez .NET Foundation, która tworzy aplikację ASP.NET, która może hostować pakiet źródła danych na dowolnym serwerze, na którym działa program IIS. Był wyświetlany NuGet.Server sprawia, że folder na serwerze, dostępne za pośrednictwem protokołu HTTP (S) (w szczególności OData). Jest łatwy w konfiguracji i sprawdza się najlepiej w przypadku prostych scenariuszy.

1. Utwórz pustą aplikację sieci Web platformy ASP.NET w programie Visual Studio i Dodaj pakiet NuGet.Server do niego.
1. Konfigurowanie `Packages` folderu w aplikacji i dodawanie pakietów.
1. Wdróż aplikację do odpowiedniego serwera.

Poniższe sekcje przeprowadzą przez ten proces szczegółowo, przy użyciu języka C#.

Jeśli masz więcej pytań dotyczących NuGet.Server, Utwórz problem w [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Tworzenie i wdrażanie aplikacji sieci Web platformy ASP.NET za pomocą NuGet.Server

1. W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, wyszukaj "ASP.NET", wybierz **aplikacji sieci Web platformy ASP.NET (.NET Framework)** szablonu języka C# i zestaw **Framework** ".NET Framework 4.6":

    ![Ustawienie platforma docelowa dla nowego projektu](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Nadaj aplikacji nazwę odpowiedniego *innych* niż NuGet.Server, wybierz pozycję OK, a w następnym oknie dialogowym wybierz **pusty** szablonu, następnie wybierz pozycję **OK**.

1. Kliknij prawym przyciskiem myszy projekt, wybierz **Zarządzaj pakietami NuGet**.

1. W Interfejsie użytkownika Menedżera pakietów, wybierz **Przeglądaj** kartę, a następnie wyszukaj i zainstaluj najnowszą wersję pakietu NuGet.Server, jeśli jest przeznaczony dla .NET Framework 4.6. (Można także zainstalować go z poziomu konsoli Menedżera pakietów przy użyciu `Install-Package NuGet.Server`.) Jeśli zostanie wyświetlony monit, należy zaakceptować postanowienia licencyjne.

    ![Instalowanie pakietu NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

1. Instalowanie NuGet.Server konwertuje pusta aplikacja sieci Web do źródła pakietu. Instaluje różnych innych pakietów, tworzy `Packages` folderu w aplikacji i modyfikuje `web.config` uwzględnienie dodatkowych ustawień (zobacz komentarze w tym pliku, aby uzyskać szczegółowe informacje).

    > [!Important]
    > Należy dokładnie sprawdzić `web.config` po pakietu NuGet.Server zakończeniu jego modyfikacji pliku. NuGet.Server może nie zastąpić istniejące elementy, ale zamiast tego utworzyć zduplikowane elementy. Te duplikaty spowoduje, że "wewnętrzny błąd serwera" podczas próby uruchomienia projektu później. Na przykład jeśli Twoja `web.config` zawiera `<compilation debug="true" targetFramework="4.5.2" />` przed zainstalowaniem NuGet.Server, pakiet nie zastępuje go, ale wstawia sekundy `<compilation debug="true" targetFramework="4.6" />`. W takim przypadku Usuń element ze starszą wersją framework.

1. Aby udostępnić pakietów w kanale informacyjnym podczas publikowania aplikacji na serwerze, należy dodać każdy `.nupkg` plików `Packages` folderu w programie Visual Studio, następnie ustawić każdy z nich w **Build Action** do **zawartości**i **Kopiuj do katalogu wyjściowego** do **zawsze Kopiuj**:

    ![Skopiuj pakiety do folderu pakietów w projekcie](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Uruchamianie witryny lokalnie w programie Visual Studio (przy użyciu **Debuguj > Uruchom bez debugowania** lub Ctrl + F5). Strona główna zawiera pakiet kanału informacyjnego adresy URL, jak pokazano poniżej. Jeśli widzisz błędy, należy dokładnie sprawdzić swoje `web.config` dla zduplikowane elementy są zanotowanej wcześniej w kroku 5.

    ![Domyślną stronę główną dla aplikacji za pomocą NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. Kliknij pozycję **tutaj** w obszarze opisanych powyżej, aby wyświetlić źródło danych OData pakietów.

1. Przy pierwszym uruchomieniu aplikacji, restrukturyzuje NuGet.Server `Packages` folderu zawierającego folderu dla każdego pakietu. Odpowiada to [układu magazynu lokalnego](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) wprowadzone w programie NuGet 3.3 w celu zwiększenia wydajności. Podczas dodawania dodatkowych pakietów, w dalszym ciągu strukturą.

1. Po przetestowaniu wdrożenia lokalnego, należy wdrożyć aplikację na żadnej innej witrynie wewnętrzne lub zewnętrzne, zgodnie z potrzebami.

1. Po jej wdrożeniu na `http://<domain>`, adres URL, którego używasz jako źródła pakietu będzie `http://<domain>/nuget`.

## <a name="configuring-the-packages-folder"></a>Konfigurowanie folderu pakietów

Za pomocą `NuGet.Server` 1.5 lub nowszej można bardziej szczegółowo skonfigurować przy użyciu folderu pakietu `appSetting/packagesPath` wartość w `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` może być ścieżką bezwzględną lub wirtualnych.

Gdy `packagesPath` zostanie pominięty lub pole pozostanie puste, packages folder jest ustawieniem domyślnym `~/Packages`.

## <a name="adding-packages-to-the-feed-externally"></a>Trwa dodawanie pakietów w kanale informacyjnym zewnętrznie

Gdy NuGet.Server lokacji zostanie uruchomiona, można dodać pakietów przy użyciu [wypychania nuget](../tools/cli-ref-push.md) pod warunkiem, że ustawisz wartość klucza interfejsu API w `web.config`.

Po zainstalowaniu pakietu NuGet.Server `web.config` zawiera pustą `appSetting/apiKey` wartość:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Gdy `apiKey` zostanie pominięty lub puste i wypychania pakietów do kanału informacyjnego jest wyłączona.

Aby włączenie tej funkcji, należy ustawić `apiKey` wartości (najlepiej silnego hasła) i Dodaj wartość dla kucza zwanego `appSettings/requireApiKey` z wartością `true`:

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Jeśli serwer jest już zabezpieczone lub można inaczej nie wymagają klucza interfejsu API (na przykład, jeśli korzystasz z serwera prywatnej sieci lokalnej zespołu), można ustawić `requireApiKey` do `false`. Wszyscy użytkownicy z dostępem do serwera, następnie można wypchnąć pakietów.

## <a name="removing-packages-from-the-feed"></a>Usuwanie pakietów z kanału informacyjnego

Za pomocą NuGet.Server [Usuń nuget](../tools/cli-ref-delete.md) polecenie usuwa pakiet z repozytorium, pod warunkiem, że zawierają klucz interfejsu API z komentarzem.

Jeśli chcesz zmienić zachowanie, aby zamiast tego odmownej pakietu (pozostawiając ona dostępna dla przywracania pakietów), zmień `enableDelisting` w `web.config` na wartość true.

## <a name="nugetserver-support"></a>Obsługa NuGet.Server

Aby uzyskać dodatkową pomoc przy użyciu NuGet.Server, Utwórz problem w [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).