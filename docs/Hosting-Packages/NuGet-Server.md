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
# <a name="nugetserver"></a><span data-ttu-id="45d96-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="45d96-103">NuGet.Server</span></span>

<span data-ttu-id="45d96-104">NuGet.Server jest pakietem podał Foundation .NET, która tworzy aplikację ASP.NET, która może hostować pakiet źródła danych na dowolnym serwerze z uruchomionymi usługami IIS.</span><span class="sxs-lookup"><span data-stu-id="45d96-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="45d96-105">Prostu, NuGet.Server udostępnia folderu na serwerze za pośrednictwem protokołu HTTP (S) (w szczególności OData).</span><span class="sxs-lookup"><span data-stu-id="45d96-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="45d96-106">Jest łatwy w konfiguracji i najlepiej w scenariuszach proste.</span><span class="sxs-lookup"><span data-stu-id="45d96-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="45d96-107">Utwórz pustą aplikację sieci Web ASP.NET w programie Visual Studio i Dodaj pakiet NuGet.Server do niej.</span><span class="sxs-lookup"><span data-stu-id="45d96-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="45d96-108">Skonfiguruj `Packages` folderu w aplikacji i dodawanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="45d96-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="45d96-109">Wdrażanie aplikacji do odpowiedniego serwera.</span><span class="sxs-lookup"><span data-stu-id="45d96-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="45d96-110">Poniższe sekcje przeprowadzenie tego procesu szczegółowo przy użyciu języka C#.</span><span class="sxs-lookup"><span data-stu-id="45d96-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="45d96-111">Jeśli masz dodatkowe pytania dotyczące NuGet.Server, Utwórz problem w [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="45d96-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="45d96-112">Tworzenie i wdrażanie aplikacji sieci Web platformy ASP.NET z NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="45d96-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="45d96-113">W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, wyszukaj "ASP.NET", wybierz **aplikacji sieci Web platformy ASP.NET (.NET Framework)** szablon języka C# i zestaw **Framework** ".NET Framework 4.6":</span><span class="sxs-lookup"><span data-stu-id="45d96-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Ustawienie platformę docelową dla nowego projektu](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="45d96-115">Nadaj nazwę odpowiedniej aplikacji *innych* niż NuGet.Server, wybierz OK, a w następnym oknie dialogowym wybierz **pusty** szablonu, następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="45d96-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="45d96-116">Kliknij prawym przyciskiem myszy projekt, wybierz **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="45d96-116">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="45d96-117">W Interfejsie użytkownika Menedżera pakietów, wybierz **Przeglądaj** karcie, a następnie wyszukaj i zainstaluj najnowszą wersję pakietu NuGet.Server, jeśli aplikacja jest przeznaczona dla platformy .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="45d96-117">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="45d96-118">(Można go także zainstalować z konsoli Menedżera pakietów z `Install-Package NuGet.Server`.) Jeśli zostanie wyświetlony monit, należy zaakceptować postanowienia licencyjne.</span><span class="sxs-lookup"><span data-stu-id="45d96-118">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Instalowanie pakietu NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="45d96-120">Instalowanie NuGet.Server konwertuje pustą aplikację sieci Web do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="45d96-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="45d96-121">Instaluje różnych innych pakietów, tworzy `Packages` folderu w aplikacji i modyfikuje `web.config` uwzględnienie dodatkowych ustawień (zobacz komentarze w tym pliku, aby uzyskać szczegółowe informacje).</span><span class="sxs-lookup"><span data-stu-id="45d96-121">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="45d96-122">Należy dokładnie sprawdzić `web.config` po zakończeniu pakietu NuGet.Server jego modyfikacje tego pliku.</span><span class="sxs-lookup"><span data-stu-id="45d96-122">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="45d96-123">NuGet.Server może nie zastąpić istniejące elementy, ale zamiast tego utworzyć zduplikowane elementy.</span><span class="sxs-lookup"><span data-stu-id="45d96-123">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="45d96-124">Podczas próby uruchomienia projektu później one spowoduje, że "wewnętrzny błąd serwera".</span><span class="sxs-lookup"><span data-stu-id="45d96-124">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="45d96-125">Na przykład jeśli Twoje `web.config` zawiera `<compilation debug="true" targetFramework="4.5.2" />` przed zainstalowaniem NuGet.Server, pakiet nie go zastąpić, ale wstawia drugiej `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="45d96-125">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="45d96-126">W takim przypadku Usuń element ze starszą wersją framework.</span><span class="sxs-lookup"><span data-stu-id="45d96-126">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="45d96-127">Aby udostępnić pakiety w źródle danych podczas publikowania aplikacji na serwerze, Dodaj każdy `.nupkg` plików do `Packages` folderu w programie Visual Studio, następnie ustaw każdą z nich w **Akcja kompilacji** do **zawartości**i **Kopiuj do katalogu wyjściowego** do **skopiuj zawsze**:</span><span class="sxs-lookup"><span data-stu-id="45d96-127">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Kopiowanie pakietów do folderu pakietów w projekcie](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="45d96-129">Uruchom witrynę lokalnie w programie Visual Studio (przy użyciu **debugowania > Uruchom bez debugowania** lub Ctrl + F5).</span><span class="sxs-lookup"><span data-stu-id="45d96-129">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="45d96-130">Strona główna zawiera pakiet podawania adresów URL, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="45d96-130">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="45d96-131">Jeśli występuje błąd, należy dokładnie sprawdzić Twoje `web.config` dla zduplikowane elementy są wymienione wcześniej w kroku 5.</span><span class="sxs-lookup"><span data-stu-id="45d96-131">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![Domyślną stronę główną dla aplikacji z NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="45d96-133">Polecenie **tutaj** w obszarze opisanych powyżej, aby wyświetlić źródła strumieniowego OData pakietów.</span><span class="sxs-lookup"><span data-stu-id="45d96-133">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="45d96-134">Przy pierwszym uruchomieniu aplikacji, restrukturyzuje NuGet.Server `Packages` folder zawiera folder dla każdego pakietu.</span><span class="sxs-lookup"><span data-stu-id="45d96-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="45d96-135">Odpowiada [układu magazynu lokalnego](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) wprowadzone w systemie 3.3 NuGet w celu zwiększenia wydajności.</span><span class="sxs-lookup"><span data-stu-id="45d96-135">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="45d96-136">Podczas dodawania kolejnych pakietów, nadal postępuj zgodnie z tej struktury.</span><span class="sxs-lookup"><span data-stu-id="45d96-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="45d96-137">Po przetestowaniu wdrożenia lokalnego wdrożenia aplikacji do innych lokacji wewnętrzne lub zewnętrzne, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="45d96-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="45d96-138">Po wdrożeniu do `http://<domain>`, adres URL, służące do źródła pakietu będzie `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="45d96-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="45d96-139">Konfigurowanie folderu pakietów</span><span class="sxs-lookup"><span data-stu-id="45d96-139">Configuring the Packages folder</span></span>

<span data-ttu-id="45d96-140">Z `NuGet.Server` 1,5 i nowsze, w szczególności skonfigurowaniem przy użyciu folderu pakietu `appSetting/packagesPath` wartość w `web.config`:</span><span class="sxs-lookup"><span data-stu-id="45d96-140">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="45d96-141">`packagesPath` może być ścieżką bezwzględną ani wirtualne.</span><span class="sxs-lookup"><span data-stu-id="45d96-141">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="45d96-142">Gdy `packagesPath` jest pominięty lub pole pozostanie puste, folder pakietów jest domyślnym `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="45d96-142">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="45d96-143">Dodawanie pakietów do źródła strumieniowego zewnętrznie</span><span class="sxs-lookup"><span data-stu-id="45d96-143">Adding packages to the feed externally</span></span>

<span data-ttu-id="45d96-144">Po uruchomieniu lokacji NuGet.Server, można dodać pakiety przy użyciu [wypychania nuget](../tools/cli-ref-push.md) pod warunkiem, że ustawiona wartość klucza interfejsu API `web.config`.</span><span class="sxs-lookup"><span data-stu-id="45d96-144">Once a NuGet.Server site is running, you can add packages using [nuget push](../tools/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="45d96-145">Po zainstalowaniu pakietu NuGet.Server `web.config` zawiera pustą `appSetting/apiKey` wartość:</span><span class="sxs-lookup"><span data-stu-id="45d96-145">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="45d96-146">Gdy `apiKey` zostanie pominięty lub puste, wypychanie pakietów do źródła danych jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="45d96-146">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="45d96-147">Aby włączyć tę możliwość, ustaw `apiKey` wartości (najlepiej silnego hasła) i Dodaj klucz o nazwie `appSettings/requireApiKey` z wartością `true`:</span><span class="sxs-lookup"><span data-stu-id="45d96-147">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="45d96-148">Jeśli serwer jest już zabezpieczone lub nie w przeciwnym razie jest wymagany klucz interfejsu API (na przykład używając prywatnego serwera w sieci lokalnej zespołu), można ustawić `requireApiKey` do `false`.</span><span class="sxs-lookup"><span data-stu-id="45d96-148">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="45d96-149">Następnie wszystkich użytkowników mających dostęp do serwera może bezzwłocznie przekazywać pakiety.</span><span class="sxs-lookup"><span data-stu-id="45d96-149">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="45d96-150">Usuwanie ze źródła pakietów</span><span class="sxs-lookup"><span data-stu-id="45d96-150">Removing packages from the feed</span></span>

<span data-ttu-id="45d96-151">Z NuGet.Server [nuget usunąć](../tools/cli-ref-delete.md) polecenia powoduje usunięcie pakietu z repozytorium pod warunkiem, że obejmują klucz interfejsu API z komentarzem.</span><span class="sxs-lookup"><span data-stu-id="45d96-151">With NuGet.Server, the [nuget delete](../tools/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="45d96-152">Jeśli chcesz zmienić to zachowanie odmownej zamiast tego pakietu (pozostawieniu ich umożliwiające przywracanie pakietu), zmienić `enableDelisting` klucza w `web.config` na wartość true.</span><span class="sxs-lookup"><span data-stu-id="45d96-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="45d96-153">Obsługa NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="45d96-153">NuGet.Server support</span></span>

<span data-ttu-id="45d96-154">Aby uzyskać dodatkową pomoc przy użyciu NuGet.Server, tworzenia problemu na [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="45d96-154">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>