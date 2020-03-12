---
title: Używanie narzędzia NuGet. Server do hostowania źródeł danych NuGet
description: Jak utworzyć i hostować źródło pakietów NuGet na dowolnym serwerze, na którym są uruchomione usługi IIS, przy użyciu NuGet. Server, dzięki czemu pakiety są dostępne za pośrednictwem protokołów HTTP i OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/10/2020
ms.locfileid: "79059565"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet. Server jest pakietem dostarczanym przez platformę .NET Foundation, który tworzy aplikację ASP.NET, która umożliwia hostowanie kanału informacyjnego pakietu na dowolnym serwerze, na którym są uruchomione usługi IIS. Po prostu program NuGet. Server udostępnia folder na serwerze za pośrednictwem protokołu HTTP (w przypadku usługi OData). Jest ona łatwa do skonfigurowania i jest Najlepsza w przypadku prostych scenariuszy.

1. Utwórz pustą aplikację sieci Web ASP.NET w programie Visual Studio i Dodaj do niej pakiet NuGet. Server.
1. Skonfiguruj folder `Packages` w aplikacji i Dodaj pakiety.
1. Wdróż aplikację na odpowiednim serwerze.

W poniższych sekcjach szczegółowo omówiono ten proces, korzystając C#z programu.

Jeśli masz więcej pytań na temat NuGet. Server, Utwórz problem na [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Tworzenie i wdrażanie aplikacji sieci Web ASP.NET za pomocą narzędzia NuGet. Server

1. W programie Visual Studio wybierz pozycję **plik > nowy > projekt**, wyszukaj ciąg "ASP.NET Web Application (.NET Framework)", wybierz odpowiedni szablon dla C#.

    ![Wybierz szablon projektu sieci Web .NET Framework](media/Hosting_00-NuGet.Server-ProjectType.png)

1. Ustaw **strukturę** na ".NET Framework 4,6".

    ![Ustawianie platformy docelowej dla nowego projektu](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Nadaj aplikacji odpowiednią nazwę *inną* niż NuGet. Server, wybierz pozycję OK, a następnie w następnym oknie dialogowym wybierz **pusty** szablon, a następnie wybierz **przycisk OK**.

    ![Wybierz pusty projekt sieci Web](media/Hosting_02-NuGet.Server-Empty.png)

1. Kliknij prawym przyciskiem myszy projekt, a następnie wybierz pozycję **Zarządzaj pakietami NuGet**.

1. W interfejsie użytkownika Menedżera pakietów wybierz kartę **przeglądanie** , a następnie wyszukaj i zainstaluj najnowszą wersję pakietu NuGet. Server, jeśli jesteś celem .NET Framework 4,6. (Można go także zainstalować z konsoli Menedżera pakietów z `Install-Package NuGet.Server`.) Zaakceptuj postanowienia licencyjne, jeśli zostanie wyświetlony monit.

    ![Instalowanie pakietu NuGet. Server](media/Hosting_03-NuGet.Server-Package.png)

1. Instalowanie NuGet. serwer konwertuje pustą aplikację sieci Web na źródło pakietu. Instaluje różne inne pakiety, tworzy `Packages` folder w aplikacji i modyfikuje `web.config` w celu uwzględnienia dodatkowych ustawień (Zobacz komentarze w tym pliku, aby uzyskać szczegółowe informacje).

    > [!Important]
    > Uważnie Zbadaj `web.config` po zakończeniu przez pakiet NuGet. Server zmian w tym pliku. NuGet. Server nie może zastąpić istniejących elementów, ale zamiast tego utworzyć zduplikowane elementy. Te duplikaty spowodują "wewnętrzny błąd serwera" podczas późniejszej próby uruchomienia projektu. Na przykład jeśli `web.config` zawiera `<compilation debug="true" targetFramework="4.5.2" />` przed zainstalowaniem programu NuGet. Server, pakiet nie zastępuje go, ale wstawia drugi `<compilation debug="true" targetFramework="4.6" />`. W takim przypadku Usuń element ze starszą wersją struktury.

1. Uruchom lokację lokalnie w programie Visual Studio (przy użyciu **debugowania > Uruchom bez debugowania** lub CTRL + F5). Strona główna zawiera adresy URL kanału informacyjnego pakietu, jak pokazano poniżej. Jeśli widzisz błędy, uważnie Przeprowadź inspekcję `web.config` pod kątem zduplikowanych elementów zgodnie z wcześniejszym opisem.

    ![Domyślna strona główna aplikacji z pakietem NuGet. Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  Przy pierwszym uruchomieniu aplikacji NuGet. serwer ponownie tworzy strukturę folderu `Packages`, aby zawierał folder dla każdego pakietu. Jest to zgodne z [lokalnym układem magazynu](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) wprowadzonym z pakietem NuGet 3,3 w celu zwiększenia wydajności. W przypadku dodawania kolejnych pakietów Kontynuuj korzystanie z tej struktury.

1. Po przetestowaniu lokalnego wdrożenia należy wdrożyć aplikację w dowolnej innej lokacji wewnętrznej lub zewnętrznej, zgodnie z potrzebami.

1. Po wdrożeniu do `http://<domain>`adres URL używany dla źródła pakietu zostanie `http://<domain>/nuget`.

## <a name="adding-packages-to-the-feed-externally"></a>Zewnętrzne dodawanie pakietów do źródła danych

Po uruchomieniu lokacji NuGet. Server można dodać pakiety przy użyciu [wypychania NuGet](../reference/cli-reference/cli-ref-push.md) , pod warunkiem, że wartość klucza interfejsu API jest ustawiona w `web.config`.

Po zainstalowaniu pakietu NuGet. Server `web.config` zawiera pustą wartość `appSetting/apiKey`:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

W przypadku pominięcia `apiKey` lub pustego, wypchnięcie pakietów do źródła danych jest wyłączone.

Aby włączyć tę funkcję, należy ustawić `apiKey` na wartość (idealnie silne hasło) i dodać klucz o nazwie `appSettings/requireApiKey` z wartością `true`:

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Jeśli serwer jest już zabezpieczony lub nie jest wymagany klucz interfejsu API (na przykład w przypadku korzystania z serwera prywatnego w lokalnej sieci zespołowej), można ustawić `requireApiKey` na `false`. Wszyscy użytkownicy z dostępem do serwera mogą następnie wysyłać pakiety.

Począwszy od elementu NuGet. Server 3.0.0, adres URL dla pakietów wypychania został zmieniony na `http://<domain>/nuget`. Przed wydaniem 3.0.0 adres URL wypychania został `http://<domain>/api/v2/package`.

W przypadku programu NuGet 3.2.1 i nowszego ten starszy adres URL `/api/v2/package` jest domyślnie włączony do `/nuget` domyślnie za pośrednictwem opcji `enableLegacyPushRoute: true` w konfiguracji startowej (domyślnie`NuGetODataConfig.cs`). Należy pamiętać, że ta funkcja nie działa, gdy wiele kanałów informacyjnych znajduje się w tym samym projekcie.

## <a name="removing-packages-from-the-feed"></a>Usuwanie pakietów ze źródła danych

W pakiecie NuGet. Server polecenie [NuGet Delete](../reference/cli-reference/cli-ref-delete.md) usuwa pakiet z repozytorium, pod warunkiem, że dołączysz klucz interfejsu API z komentarzem.

Jeśli chcesz zmienić zachowanie w celu wyłączania pakietu zamiast niego (pozostawiając dostęp do przywracania pakietu), Zmień klucz `enableDelisting` w `web.config` na true.

## <a name="configuring-the-packages-folder"></a>Konfigurowanie folderu Packages

W `NuGet.Server` 1,5 i nowszych można dostosować folder pakietu przy użyciu wartości `appSettings/packagesPath` w `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` może być ścieżką bezwzględną lub wirtualną.

Po pominięciu `packagesPath` lub pozostawieniu pustego pola folder Packages jest domyślnym `~/Packages`.

## <a name="making-packages-available-when-you-publish-the-web-app"></a>Udostępnianie pakietów przy publikowaniu aplikacji sieci Web

Aby udostępnić pakiety w kanale informacyjnym po opublikowaniu aplikacji na serwerze programu, Dodaj każde `.nupkg` pliki do folderu `Packages` w programie Visual Studio, a następnie ustaw dla każdej z nich **akcję kompilacji** na **zawartość** i **Skopiuj ją do katalogu wyjściowego** , aby **skopiować zawsze**:

![Kopiowanie pakietów do folderu Packages w projekcie](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a>Uwagi do wersji

Informacje o wersji programu NuGet. Server są dostępne na [stronie wydania usługi GitHub](https://github.com/NuGet/NuGet.Server/releases).
Obejmuje to szczegółowe informacje o poprawkach błędów i nowych funkcjach, które są dodawane.

## <a name="nugetserver-support"></a>NuGet. Server — obsługa

Aby uzyskać dodatkową pomoc dotyczącą korzystania z programu NuGet. Server, Utwórz problem na [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).
