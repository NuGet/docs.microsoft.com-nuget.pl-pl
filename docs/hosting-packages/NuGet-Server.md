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
# <a name="nugetserver"></a><span data-ttu-id="a9569-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="a9569-103">NuGet.Server</span></span>

<span data-ttu-id="a9569-104">NuGet.Server to pakiet dostarczone przez .NET Foundation, która tworzy aplikację ASP.NET, która może hostować pakiet źródła danych na dowolnym serwerze, na którym działa program IIS.</span><span class="sxs-lookup"><span data-stu-id="a9569-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="a9569-105">Był wyświetlany NuGet.Server sprawia, że folder na serwerze, dostępne za pośrednictwem protokołu HTTP (S) (w szczególności OData).</span><span class="sxs-lookup"><span data-stu-id="a9569-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="a9569-106">Jest łatwy w konfiguracji i sprawdza się najlepiej w przypadku prostych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="a9569-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="a9569-107">Utwórz pustą aplikację sieci Web platformy ASP.NET w programie Visual Studio i Dodaj pakiet NuGet.Server do niego.</span><span class="sxs-lookup"><span data-stu-id="a9569-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="a9569-108">Konfigurowanie `Packages` folderu w aplikacji i dodawanie pakietów.</span><span class="sxs-lookup"><span data-stu-id="a9569-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="a9569-109">Wdróż aplikację do odpowiedniego serwera.</span><span class="sxs-lookup"><span data-stu-id="a9569-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="a9569-110">Poniższe sekcje przeprowadzą przez ten proces szczegółowo, przy użyciu języka C#.</span><span class="sxs-lookup"><span data-stu-id="a9569-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="a9569-111">Jeśli masz więcej pytań dotyczących NuGet.Server, Utwórz problem w [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="a9569-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="a9569-112">Tworzenie i wdrażanie aplikacji sieci Web platformy ASP.NET za pomocą NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="a9569-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="a9569-113">W programie Visual Studio, wybierz **Plik > Nowy > Projekt**, wyszukaj "ASP.NET", wybierz **aplikacji sieci Web platformy ASP.NET (.NET Framework)** szablonu języka C# i zestaw **Framework** ".NET Framework 4.6":</span><span class="sxs-lookup"><span data-stu-id="a9569-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Ustawienie platforma docelowa dla nowego projektu](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="a9569-115">Nadaj aplikacji nazwę odpowiedniego *innych* niż NuGet.Server, wybierz pozycję OK, a w następnym oknie dialogowym wybierz **pusty** szablonu, następnie wybierz pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="a9569-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="a9569-116">Kliknij prawym przyciskiem myszy projekt, wybierz **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a9569-116">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="a9569-117">W Interfejsie użytkownika Menedżera pakietów, wybierz **Przeglądaj** kartę, a następnie wyszukaj i zainstaluj najnowszą wersję pakietu NuGet.Server, jeśli jest przeznaczony dla .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="a9569-117">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="a9569-118">(Można także zainstalować go z poziomu konsoli Menedżera pakietów przy użyciu `Install-Package NuGet.Server`.) Jeśli zostanie wyświetlony monit, należy zaakceptować postanowienia licencyjne.</span><span class="sxs-lookup"><span data-stu-id="a9569-118">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Instalowanie pakietu NuGet.Server](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="a9569-120">Instalowanie NuGet.Server konwertuje pusta aplikacja sieci Web do źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="a9569-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="a9569-121">Instaluje różnych innych pakietów, tworzy `Packages` folderu w aplikacji i modyfikuje `web.config` uwzględnienie dodatkowych ustawień (zobacz komentarze w tym pliku, aby uzyskać szczegółowe informacje).</span><span class="sxs-lookup"><span data-stu-id="a9569-121">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="a9569-122">Należy dokładnie sprawdzić `web.config` po pakietu NuGet.Server zakończeniu jego modyfikacji pliku.</span><span class="sxs-lookup"><span data-stu-id="a9569-122">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="a9569-123">NuGet.Server może nie zastąpić istniejące elementy, ale zamiast tego utworzyć zduplikowane elementy.</span><span class="sxs-lookup"><span data-stu-id="a9569-123">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="a9569-124">Te duplikaty spowoduje, że "wewnętrzny błąd serwera" podczas próby uruchomienia projektu później.</span><span class="sxs-lookup"><span data-stu-id="a9569-124">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="a9569-125">Na przykład jeśli Twoja `web.config` zawiera `<compilation debug="true" targetFramework="4.5.2" />` przed zainstalowaniem NuGet.Server, pakiet nie zastępuje go, ale wstawia sekundy `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="a9569-125">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="a9569-126">W takim przypadku Usuń element ze starszą wersją framework.</span><span class="sxs-lookup"><span data-stu-id="a9569-126">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="a9569-127">Aby udostępnić pakietów w kanale informacyjnym podczas publikowania aplikacji na serwerze, należy dodać każdy `.nupkg` plików `Packages` folderu w programie Visual Studio, następnie ustawić każdy z nich w **Build Action** do **zawartości**i **Kopiuj do katalogu wyjściowego** do **zawsze Kopiuj**:</span><span class="sxs-lookup"><span data-stu-id="a9569-127">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Skopiuj pakiety do folderu pakietów w projekcie](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="a9569-129">Uruchamianie witryny lokalnie w programie Visual Studio (przy użyciu **Debuguj > Uruchom bez debugowania** lub Ctrl + F5).</span><span class="sxs-lookup"><span data-stu-id="a9569-129">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="a9569-130">Strona główna zawiera pakiet kanału informacyjnego adresy URL, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="a9569-130">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="a9569-131">Jeśli widzisz błędy, należy dokładnie sprawdzić swoje `web.config` dla zduplikowane elementy są zanotowanej wcześniej w kroku 5.</span><span class="sxs-lookup"><span data-stu-id="a9569-131">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![Domyślną stronę główną dla aplikacji za pomocą NuGet.Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="a9569-133">Kliknij pozycję **tutaj** w obszarze opisanych powyżej, aby wyświetlić źródło danych OData pakietów.</span><span class="sxs-lookup"><span data-stu-id="a9569-133">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="a9569-134">Przy pierwszym uruchomieniu aplikacji, restrukturyzuje NuGet.Server `Packages` folderu zawierającego folderu dla każdego pakietu.</span><span class="sxs-lookup"><span data-stu-id="a9569-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="a9569-135">Odpowiada to [układu magazynu lokalnego](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) wprowadzone w programie NuGet 3.3 w celu zwiększenia wydajności.</span><span class="sxs-lookup"><span data-stu-id="a9569-135">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="a9569-136">Podczas dodawania dodatkowych pakietów, w dalszym ciągu strukturą.</span><span class="sxs-lookup"><span data-stu-id="a9569-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="a9569-137">Po przetestowaniu wdrożenia lokalnego, należy wdrożyć aplikację na żadnej innej witrynie wewnętrzne lub zewnętrzne, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="a9569-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="a9569-138">Po jej wdrożeniu na `http://<domain>`, adres URL, którego używasz jako źródła pakietu będzie `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="a9569-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="a9569-139">Konfigurowanie folderu pakietów</span><span class="sxs-lookup"><span data-stu-id="a9569-139">Configuring the Packages folder</span></span>

<span data-ttu-id="a9569-140">Za pomocą `NuGet.Server` 1.5 lub nowszej można bardziej szczegółowo skonfigurować przy użyciu folderu pakietu `appSetting/packagesPath` wartość w `web.config`:</span><span class="sxs-lookup"><span data-stu-id="a9569-140">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="a9569-141">`packagesPath` może być ścieżką bezwzględną lub wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="a9569-141">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="a9569-142">Gdy `packagesPath` zostanie pominięty lub pole pozostanie puste, packages folder jest ustawieniem domyślnym `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="a9569-142">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="a9569-143">Trwa dodawanie pakietów w kanale informacyjnym zewnętrznie</span><span class="sxs-lookup"><span data-stu-id="a9569-143">Adding packages to the feed externally</span></span>

<span data-ttu-id="a9569-144">Gdy NuGet.Server lokacji zostanie uruchomiona, można dodać pakietów przy użyciu [wypychania nuget](../tools/cli-ref-push.md) pod warunkiem, że ustawisz wartość klucza interfejsu API w `web.config`.</span><span class="sxs-lookup"><span data-stu-id="a9569-144">Once a NuGet.Server site is running, you can add packages using [nuget push](../tools/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="a9569-145">Po zainstalowaniu pakietu NuGet.Server `web.config` zawiera pustą `appSetting/apiKey` wartość:</span><span class="sxs-lookup"><span data-stu-id="a9569-145">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="a9569-146">Gdy `apiKey` zostanie pominięty lub puste i wypychania pakietów do kanału informacyjnego jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="a9569-146">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="a9569-147">Aby włączenie tej funkcji, należy ustawić `apiKey` wartości (najlepiej silnego hasła) i Dodaj wartość dla kucza zwanego `appSettings/requireApiKey` z wartością `true`:</span><span class="sxs-lookup"><span data-stu-id="a9569-147">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="a9569-148">Jeśli serwer jest już zabezpieczone lub można inaczej nie wymagają klucza interfejsu API (na przykład, jeśli korzystasz z serwera prywatnej sieci lokalnej zespołu), można ustawić `requireApiKey` do `false`.</span><span class="sxs-lookup"><span data-stu-id="a9569-148">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="a9569-149">Wszyscy użytkownicy z dostępem do serwera, następnie można wypchnąć pakietów.</span><span class="sxs-lookup"><span data-stu-id="a9569-149">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="a9569-150">Usuwanie pakietów z kanału informacyjnego</span><span class="sxs-lookup"><span data-stu-id="a9569-150">Removing packages from the feed</span></span>

<span data-ttu-id="a9569-151">Za pomocą NuGet.Server [Usuń nuget](../tools/cli-ref-delete.md) polecenie usuwa pakiet z repozytorium, pod warunkiem, że zawierają klucz interfejsu API z komentarzem.</span><span class="sxs-lookup"><span data-stu-id="a9569-151">With NuGet.Server, the [nuget delete](../tools/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="a9569-152">Jeśli chcesz zmienić zachowanie, aby zamiast tego odmownej pakietu (pozostawiając ona dostępna dla przywracania pakietów), zmień `enableDelisting` w `web.config` na wartość true.</span><span class="sxs-lookup"><span data-stu-id="a9569-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="a9569-153">Obsługa NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="a9569-153">NuGet.Server support</span></span>

<span data-ttu-id="a9569-154">Aby uzyskać dodatkową pomoc przy użyciu NuGet.Server, Utwórz problem w [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="a9569-154">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>