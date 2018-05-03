---
title: Przy użyciu NuGet.Server do hostowania NuGet źródeł danych
description: Jak tworzyć i obsługiwać pakietu NuGet źródła danych na każdym serwerze z programem IIS za pomocą NuGet.Server, udostępniając pakiety za pośrednictwem protokołu HTTP i OData.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 55501eedf6c5fdf054a602536ee8c03e7048d5d5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server jest pakietem podał Foundation .NET, która tworzy aplikację ASP.NET, która może hostować pakiet źródła danych na dowolnym serwerze z uruchomionymi usługami IIS. Prostu, NuGet.Server udostępnia folderu na serwerze za pośrednictwem protokołu HTTP (S) (w szczególności OData). Jest łatwy w konfiguracji i najlepiej w scenariuszach proste.

1. Utwórz pustą aplikację sieci Web ASP.NET w programie Visual Studio i Dodaj pakiet NuGet.Server do niej.
1. Skonfiguruj `Packages` folderu w aplikacji i dodawanie pakietów.
1. Wdrażanie aplikacji do odpowiedniego serwera.

Poniższe sekcje przeprowadzenie tego procesu szczegółowo przy użyciu języka C#.

Jeśli masz dodatkowe pytania dotyczące NuGet.Server, Utwórz problem w [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Tworzenie i wdrażanie aplikacji sieci Web platformy ASP.NET z NuGet.Server

1. W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, wyszukaj "ASP.NET", wybierz **aplikacji sieci Web platformy ASP.NET (.NET Framework)** szablon języka C# i zestaw **Framework** ".NET Framework 4.6":

    ![Ustawienie platformę docelową dla nowego projektu](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Nadaj nazwę odpowiedniej aplikacji *innych* niż NuGet.Server, wybierz OK, a w następnym oknie dialogowym wybierz **pusty** szablonu, następnie wybierz **OK**.

1. Kliknij prawym przyciskiem myszy projekt, wybierz **Zarządzaj pakietami NuGet**.

1. W Interfejsie użytkownika Menedżera pakietów, wybierz **Przeglądaj** karcie, a następnie wyszukaj i zainstaluj najnowszą wersję pakietu NuGet.Server, jeśli aplikacja jest przeznaczona dla platformy .NET Framework 4.6. (Można go także zainstalować z konsoli Menedżera pakietów z `Install-Package NuGet.Server`.) Jeśli zostanie wyświetlony monit, należy zaakceptować postanowienia licencyjne.

    ![Instalowanie pakietu NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

1. Instalowanie NuGet.Server konwertuje pustą aplikację sieci Web do źródła pakietu. Instaluje różnych innych pakietów, tworzy `Packages` folderu w aplikacji i modyfikuje `web.config` uwzględnienie dodatkowych ustawień (zobacz komentarze w tym pliku, aby uzyskać szczegółowe informacje).

    > [!Important]
    > Należy dokładnie sprawdzić `web.config` po zakończeniu pakietu NuGet.Server jego modyfikacje tego pliku. NuGet.Server może nie zastąpić istniejące elementy, ale zamiast tego utworzyć zduplikowane elementy. Podczas próby uruchomienia projektu później one spowoduje, że "wewnętrzny błąd serwera". Na przykład jeśli Twoje `web.config` zawiera `<compilation debug="true" targetFramework="4.5.2" />` przed zainstalowaniem NuGet.Server, pakiet nie go zastąpić, ale wstawia drugiej `<compilation debug="true" targetFramework="4.6" />`. W takim przypadku Usuń element ze starszą wersją framework.

1. Aby udostępnić pakiety w źródle danych podczas publikowania aplikacji na serwerze, Dodaj każdy `.nupkg` plików do `Packages` folderu w programie Visual Studio, następnie ustaw każdą z nich w **Akcja kompilacji** do **zawartości**i **Kopiuj do katalogu wyjściowego** do **skopiuj zawsze**:

    ![Kopiowanie pakietów do folderu pakietów w projekcie](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Uruchom witrynę lokalnie w programie Visual Studio (przy użyciu **debugowania > Uruchom bez debugowania** lub Ctrl + F5). Strona główna zawiera pakiet podawania adresów URL, jak pokazano poniżej. Jeśli występuje błąd, należy dokładnie sprawdzić Twoje `web.config` dla zduplikowane elementy są wymienione wcześniej w kroku 5.

    ![Domyślną stronę główną dla aplikacji z NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. Polecenie **tutaj** w obszarze opisanych powyżej, aby wyświetlić źródła strumieniowego OData pakietów.

1. Przy pierwszym uruchomieniu aplikacji, restrukturyzuje NuGet.Server `Packages` folder zawiera folder dla każdego pakietu. Odpowiada [układu magazynu lokalnego](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) wprowadzone w systemie 3.3 NuGet w celu zwiększenia wydajności. Podczas dodawania kolejnych pakietów, nadal postępuj zgodnie z tej struktury.

1. Po przetestowaniu wdrożenia lokalnego wdrożenia aplikacji do innych lokacji wewnętrzne lub zewnętrzne, zgodnie z potrzebami.

1. Po wdrożeniu do `http://<domain>`, adres URL, służące do źródła pakietu będzie `http://<domain>/nuget`.

## <a name="configuring-the-packages-folder"></a>Konfigurowanie folderu pakietów

Z `NuGet.Server` 1,5 i nowsze, w szczególności skonfigurowaniem przy użyciu folderu pakietu `appSetting/packagesPath` wartość w `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` może być ścieżką bezwzględną ani wirtualne.

Gdy `packagesPath` jest pominięty lub pole pozostanie puste, folder pakietów jest domyślnym `~/Packages`.

## <a name="adding-packages-to-the-feed-externally"></a>Dodawanie pakietów do źródła strumieniowego zewnętrznie

Po uruchomieniu lokacji NuGet.Server, można dodać pakiety przy użyciu [wypychania nuget](../tools/cli-ref-push.md) pod warunkiem, że ustawiona wartość klucza interfejsu API `web.config`.

Po zainstalowaniu pakietu NuGet.Server `web.config` zawiera pustą `appSetting/apiKey` wartość:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Gdy `apiKey` zostanie pominięty lub puste, wypychanie pakietów do źródła danych jest wyłączona.

Aby włączyć tę możliwość, ustaw `apiKey` wartości (najlepiej silnego hasła) i Dodaj klucz o nazwie `appSettings/requireApiKey` z wartością `true`:

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Jeśli serwer jest już zabezpieczone lub nie w przeciwnym razie jest wymagany klucz interfejsu API (na przykład używając prywatnego serwera w sieci lokalnej zespołu), można ustawić `requireApiKey` do `false`. Następnie wszystkich użytkowników mających dostęp do serwera może bezzwłocznie przekazywać pakiety.

## <a name="removing-packages-from-the-feed"></a>Usuwanie ze źródła pakietów

Z NuGet.Server [nuget usunąć](../tools/cli-ref-delete.md) polecenia powoduje usunięcie pakietu z repozytorium pod warunkiem, że obejmują klucz interfejsu API z komentarzem.

Jeśli chcesz zmienić to zachowanie odmownej zamiast tego pakietu (pozostawieniu ich umożliwiające przywracanie pakietu), zmienić `enableDelisting` klucza w `web.config` na wartość true.

## <a name="nugetserver-support"></a>Obsługa NuGet.Server

Aby uzyskać dodatkową pomoc przy użyciu NuGet.Server, tworzenia problemu na [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).