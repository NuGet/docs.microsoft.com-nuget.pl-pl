---
title: "Przy użyciu NuGet.Server do hostowania NuGet źródeł | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Jak tworzyć i obsługiwać pakietu NuGet źródła danych na każdym serwerze z programem IIS za pomocą NuGet.Server, udostępniając pakiety za pośrednictwem protokołu HTTP i OData."
keywords: "NuGet źródła danych, Galeria NuGet pakietu zdalnego źródła danych, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cb3f04954fac1b4a39284be187776ab4a19b364
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server jest pakietem podał Foundation .NET, która tworzy aplikację ASP.NET, która może hostować pakiet źródła danych na dowolnym serwerze z uruchomionymi usługami IIS. Prostu, NuGet.Server udostępnia folderu na serwerze za pośrednictwem protokołu HTTP (S) (w szczególności OData). Jest łatwy w konfiguracji i najlepiej w scenariuszach proste.

1. Utwórz pustą aplikację sieci Web ASP.NET w programie Visual Studio i Dodaj pakiet NuGet.Server do niej.
1. Skonfiguruj `Packages` folderu w aplikacji i dodawanie pakietów.
1. Wdrażanie aplikacji do odpowiedniego serwera.

Poniższe sekcje przeprowadzenie tego procesu szczegółowo przy użyciu języka C#.

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Tworzenie i wdrażanie aplikacji sieci Web platformy ASP.NET z NuGet.Server

1. W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, ustaw docelową platformę dla programu .NET Framework 4.6 (patrz poniżej), wyszukaj "ASP.NET" i wybierz **aplikacji sieci Web platformy ASP.NET (.NET Framework)** szablon języka C#.

    ![Ustawienie docelowej .NET Framework 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Nadaj nazwę odpowiedniej aplikacji *innych* niż NuGet.Server, wybierz OK, a w następnym oknie dialogowym wybierz **pusty** szablon i wybierz OK.

1. Kliknij prawym przyciskiem myszy projekt, wybierz **Zarządzaj pakietami NuGet**, w Interfejsie użytkownika Menedżera pakietów Wyszukaj i zainstaluj najnowszą wersję pakietu NuGet.Server, jeśli aplikacja jest przeznaczona dla platformy .NET Framework 4.6. (Można go także zainstalować z konsoli Menedżera pakietów z `Install-Package NuGet.Server`.)

    ![Instalowanie pakietu NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > Jeśli aplikacja sieci web jest przeznaczony dla platformy .NET Framework 4.5.2, należy zainstalować serwer NuGet **2.10.3** zamiast tego.

1. Instalowanie NuGet.Server konwertuje pustą aplikację sieci Web do źródła pakietu. Tworzy `Packages` folderu w aplikacji i zastępuje `web.config` uwzględnienie dodatkowych ustawień (zobacz komentarze w tym pliku, aby uzyskać szczegółowe informacje).

1. Aby udostępnić pakiety w źródle danych podczas publikowania aplikacji na serwerze, należy dodać ich `.nupkg` plików do `Packages` folderu w programie Visual Studio, a następnie ustaw ich **Akcja kompilacji** do **zawartości**i **Kopiuj do katalogu wyjściowego** do **skopiuj zawsze**:

    ![Kopiowanie pakietów do folderu pakietów w projekcie](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Uruchom witrynę lokalnie w programie Visual Studio (bez debugowania, czyli Ctrl + F5). Strona główna zawiera pakiet podawania adresów URL:

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

`packagesPath`może być ścieżką bezwzględną ani wirtualne.

Gdy `packagesPath` jest pominięty lub pole pozostanie puste, folder pakietów jest domyślnym `~/Packages`.

## <a name="adding-packages-to-the-feed-externally"></a>Dodawanie pakietów do źródła strumieniowego zewnętrznie

Po uruchomieniu lokacji NuGet.Server można dodać lub usunąć pakiety przy użyciu nuget.exe, pod warunkiem, że ustawiona wartość klucza interfejsu API `web.config`.

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

Jeśli serwer jest już zabezpieczone lub nie w przeciwnym razie jest wymagany klucz interfejsu API (na przykład używając prywatnego serwera w sieci lokalnej zespołu), można ustawić `requireApiKey` do `false`. Wszyscy użytkownicy z dostępem do serwera można następnie push lub usuwanie pakietów.