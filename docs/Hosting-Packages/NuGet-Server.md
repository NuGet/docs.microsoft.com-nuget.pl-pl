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
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2018
---
# <a name="nugetserver"></a><span data-ttu-id="166aa-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="166aa-104">NuGet.Server</span></span>

<span data-ttu-id="166aa-105">NuGet.Server jest pakietem podał Foundation .NET, która tworzy aplikację ASP.NET, która może hostować pakiet źródła danych na dowolnym serwerze z uruchomionymi usługami IIS.</span><span class="sxs-lookup"><span data-stu-id="166aa-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="166aa-106">Prostu, NuGet.Server udostępnia folderu na serwerze za pośrednictwem protokołu HTTP (S) (w szczególności OData).</span><span class="sxs-lookup"><span data-stu-id="166aa-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="166aa-107">Jest łatwy w konfiguracji i najlepiej w scenariuszach proste.</span><span class="sxs-lookup"><span data-stu-id="166aa-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="166aa-108">Utwórz pustą aplikację sieci Web ASP.NET w programie Visual Studio i Dodaj pakiet NuGet.Server do niej.</span><span class="sxs-lookup"><span data-stu-id="166aa-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="166aa-109">Skonfiguruj `Packages` folderu w aplikacji i dodawanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="166aa-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="166aa-110">Wdrażanie aplikacji do odpowiedniego serwera.</span><span class="sxs-lookup"><span data-stu-id="166aa-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="166aa-111">Poniższe sekcje przeprowadzenie tego procesu szczegółowo przy użyciu języka C#.</span><span class="sxs-lookup"><span data-stu-id="166aa-111">The following sections walk through this process in detail, using C#.</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="166aa-112">Tworzenie i wdrażanie aplikacji sieci Web platformy ASP.NET z NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="166aa-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="166aa-113">W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, ustaw docelową platformę dla programu .NET Framework 4.6 (patrz poniżej), wyszukaj "ASP.NET" i wybierz **aplikacji sieci Web platformy ASP.NET (.NET Framework)** szablon języka C#.</span><span class="sxs-lookup"><span data-stu-id="166aa-113">In Visual Studio, select **File > New > Project**, set the target framework for .NET Framework 4.6 (see below), search for "ASP.NET", and select the **ASP.NET Web Application (.NET Framework)** template for C#.</span></span>

    ![Ustawienie docelowej .NET Framework 4.6](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="166aa-115">Nadaj nazwę odpowiedniej aplikacji *innych* niż NuGet.Server, wybierz OK, a w następnym oknie dialogowym wybierz **pusty** szablon i wybierz OK.</span><span class="sxs-lookup"><span data-stu-id="166aa-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template and select OK.</span></span>

1. <span data-ttu-id="166aa-116">Kliknij prawym przyciskiem myszy projekt, wybierz **Zarządzaj pakietami NuGet**, w Interfejsie użytkownika Menedżera pakietów Wyszukaj i zainstaluj najnowszą wersję pakietu NuGet.Server, jeśli aplikacja jest przeznaczona dla platformy .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="166aa-116">Right-click the project, select **Manage NuGet Packages**, and in the Package Manager UI search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="166aa-117">(Można go także zainstalować z konsoli Menedżera pakietów z `Install-Package NuGet.Server`.)</span><span class="sxs-lookup"><span data-stu-id="166aa-117">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.)</span></span>

    ![Instalowanie pakietu NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > <span data-ttu-id="166aa-119">Jeśli aplikacja sieci web jest przeznaczony dla platformy .NET Framework 4.5.2, należy zainstalować serwer NuGet **2.10.3** zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="166aa-119">If your web application targets .NET Framework 4.5.2, you must install NuGet Server **2.10.3** instead.</span></span>

1. <span data-ttu-id="166aa-120">Instalowanie NuGet.Server konwertuje pustą aplikację sieci Web do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="166aa-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="166aa-121">Tworzy `Packages` folderu w aplikacji i zastępuje `web.config` uwzględnienie dodatkowych ustawień (zobacz komentarze w tym pliku, aby uzyskać szczegółowe informacje).</span><span class="sxs-lookup"><span data-stu-id="166aa-121">It creates a `Packages` folder in the application and overwrites `web.config` to include additional settings (see the comments in that file for details).</span></span>

1. <span data-ttu-id="166aa-122">Aby udostępnić pakiety w źródle danych podczas publikowania aplikacji na serwerze, należy dodać ich `.nupkg` plików do `Packages` folderu w programie Visual Studio, a następnie ustaw ich **Akcja kompilacji** do **zawartości**i **Kopiuj do katalogu wyjściowego** do **skopiuj zawsze**:</span><span class="sxs-lookup"><span data-stu-id="166aa-122">To make packages available in the feed when you publish the application to a server, add their `.nupkg` files to the `Packages` folder in Visual Studio, then set their **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Kopiowanie pakietów do folderu pakietów w projekcie](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="166aa-124">Uruchom witrynę lokalnie w programie Visual Studio (bez debugowania, czyli Ctrl + F5).</span><span class="sxs-lookup"><span data-stu-id="166aa-124">Run the site locally in Visual Studio (without debugging, that is Ctrl+F5).</span></span> <span data-ttu-id="166aa-125">Strona główna zawiera pakiet podawania adresów URL:</span><span class="sxs-lookup"><span data-stu-id="166aa-125">The home page provides the package feed URLs:</span></span>

    ![Domyślną stronę główną dla aplikacji z NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="166aa-127">Polecenie **tutaj** w obszarze opisanych powyżej, aby wyświetlić źródła strumieniowego OData pakietów.</span><span class="sxs-lookup"><span data-stu-id="166aa-127">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="166aa-128">Przy pierwszym uruchomieniu aplikacji, restrukturyzuje NuGet.Server `Packages` folder zawiera folder dla każdego pakietu.</span><span class="sxs-lookup"><span data-stu-id="166aa-128">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="166aa-129">Odpowiada [układu magazynu lokalnego](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) wprowadzone w systemie 3.3 NuGet w celu zwiększenia wydajności.</span><span class="sxs-lookup"><span data-stu-id="166aa-129">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="166aa-130">Podczas dodawania kolejnych pakietów, nadal postępuj zgodnie z tej struktury.</span><span class="sxs-lookup"><span data-stu-id="166aa-130">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="166aa-131">Po przetestowaniu wdrożenia lokalnego wdrożenia aplikacji do innych lokacji wewnętrzne lub zewnętrzne, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="166aa-131">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>
1. <span data-ttu-id="166aa-132">Po wdrożeniu do `http://<domain>`, adres URL, służące do źródła pakietu będzie `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="166aa-132">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="166aa-133">Konfigurowanie folderu pakietów</span><span class="sxs-lookup"><span data-stu-id="166aa-133">Configuring the Packages folder</span></span>

<span data-ttu-id="166aa-134">Z `NuGet.Server` 1,5 i nowsze, w szczególności skonfigurowaniem przy użyciu folderu pakietu `appSetting/packagesPath` wartość w `web.config`:</span><span class="sxs-lookup"><span data-stu-id="166aa-134">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="166aa-135">`packagesPath`może być ścieżką bezwzględną ani wirtualne.</span><span class="sxs-lookup"><span data-stu-id="166aa-135">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="166aa-136">Gdy `packagesPath` jest pominięty lub pole pozostanie puste, folder pakietów jest domyślnym `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="166aa-136">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="166aa-137">Dodawanie pakietów do źródła strumieniowego zewnętrznie</span><span class="sxs-lookup"><span data-stu-id="166aa-137">Adding packages to the feed externally</span></span>

<span data-ttu-id="166aa-138">Po uruchomieniu lokacji NuGet.Server można dodać lub usunąć pakiety przy użyciu nuget.exe, pod warunkiem, że ustawiona wartość klucza interfejsu API `web.config`.</span><span class="sxs-lookup"><span data-stu-id="166aa-138">Once a NuGet.Server site is running, you can add or delete packages using nuget.exe provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="166aa-139">Po zainstalowaniu pakietu NuGet.Server `web.config` zawiera pustą `appSetting/apiKey` wartość:</span><span class="sxs-lookup"><span data-stu-id="166aa-139">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="166aa-140">Gdy `apiKey` zostanie pominięty lub puste, wypychanie pakietów do źródła danych jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="166aa-140">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="166aa-141">Aby włączyć tę możliwość, ustaw `apiKey` wartości (najlepiej silnego hasła) i Dodaj klucz o nazwie `appSettings/requireApiKey` z wartością `true`:</span><span class="sxs-lookup"><span data-stu-id="166aa-141">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="166aa-142">Jeśli serwer jest już zabezpieczone lub nie w przeciwnym razie jest wymagany klucz interfejsu API (na przykład używając prywatnego serwera w sieci lokalnej zespołu), można ustawić `requireApiKey` do `false`.</span><span class="sxs-lookup"><span data-stu-id="166aa-142">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="166aa-143">Wszyscy użytkownicy z dostępem do serwera można następnie push lub usuwanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="166aa-143">All users with access to the server can then push or delete packages.</span></span>