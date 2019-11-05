---
title: Używanie narzędzia NuGet. Server do hostowania źródeł danych NuGet
description: Jak utworzyć i hostować źródło pakietów NuGet na dowolnym serwerze, na którym są uruchomione usługi IIS, przy użyciu NuGet. Server, dzięki czemu pakiety są dostępne za pośrednictwem protokołów HTTP i OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 82b353450ff1da23a17e5b1c6a825ad32782bf75
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610592"
---
# <a name="nugetserver"></a><span data-ttu-id="83584-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="83584-103">NuGet.Server</span></span>

<span data-ttu-id="83584-104">NuGet. Server jest pakietem dostarczanym przez platformę .NET Foundation, który tworzy aplikację ASP.NET, która umożliwia hostowanie kanału informacyjnego pakietu na dowolnym serwerze, na którym są uruchomione usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="83584-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="83584-105">Po prostu program NuGet. Server udostępnia folder na serwerze za pośrednictwem protokołu HTTP (w przypadku usługi OData).</span><span class="sxs-lookup"><span data-stu-id="83584-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="83584-106">Jest ona łatwa do skonfigurowania i jest Najlepsza w przypadku prostych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="83584-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="83584-107">Utwórz pustą aplikację sieci Web ASP.NET w programie Visual Studio i Dodaj do niej pakiet NuGet. Server.</span><span class="sxs-lookup"><span data-stu-id="83584-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="83584-108">Skonfiguruj folder `Packages` w aplikacji i Dodaj pakiety.</span><span class="sxs-lookup"><span data-stu-id="83584-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="83584-109">Wdróż aplikację na odpowiednim serwerze.</span><span class="sxs-lookup"><span data-stu-id="83584-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="83584-110">W poniższych sekcjach szczegółowo omówiono ten proces, korzystając C#z programu.</span><span class="sxs-lookup"><span data-stu-id="83584-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="83584-111">Jeśli masz więcej pytań na temat NuGet. Server, Utwórz problem na [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="83584-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="83584-112">Tworzenie i wdrażanie aplikacji sieci Web ASP.NET za pomocą narzędzia NuGet. Server</span><span class="sxs-lookup"><span data-stu-id="83584-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="83584-113">W programie Visual Studio wybierz pozycję **plik > nowy > projekt**, wyszukaj ciąg "ASP.NET", wybierz szablon **aplikacja sieci Web ASP.NET (.NET Framework)** dla C#systemu, a następnie ustaw opcję ".NET Framework 4,6":</span><span class="sxs-lookup"><span data-stu-id="83584-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Ustawianie platformy docelowej dla nowego projektu](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="83584-115">Nadaj aplikacji odpowiednią nazwę *inną* niż NuGet. Server, wybierz pozycję OK, a następnie w następnym oknie dialogowym wybierz **pusty** szablon, a następnie wybierz **przycisk OK**.</span><span class="sxs-lookup"><span data-stu-id="83584-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="83584-116">Kliknij prawym przyciskiem myszy projekt, a następnie wybierz pozycję **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="83584-116">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="83584-117">W interfejsie użytkownika Menedżera pakietów wybierz kartę **przeglądanie** , a następnie wyszukaj i zainstaluj najnowszą wersję pakietu NuGet. Server, jeśli jesteś celem .NET Framework 4,6.</span><span class="sxs-lookup"><span data-stu-id="83584-117">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="83584-118">(Można go także zainstalować z konsoli Menedżera pakietów z `Install-Package NuGet.Server`.) Zaakceptuj postanowienia licencyjne, jeśli zostanie wyświetlony monit.</span><span class="sxs-lookup"><span data-stu-id="83584-118">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Instalowanie pakietu NuGet. Server](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="83584-120">Instalowanie NuGet. serwer konwertuje pustą aplikację sieci Web na źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="83584-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="83584-121">Instaluje różne inne pakiety, tworzy `Packages` folder w aplikacji i modyfikuje `web.config` w celu uwzględnienia dodatkowych ustawień (Zobacz komentarze w tym pliku, aby uzyskać szczegółowe informacje).</span><span class="sxs-lookup"><span data-stu-id="83584-121">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="83584-122">Uważnie Zbadaj `web.config` po zakończeniu przez pakiet NuGet. Server zmian w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="83584-122">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="83584-123">NuGet. Server nie może zastąpić istniejących elementów, ale zamiast tego utworzyć zduplikowane elementy.</span><span class="sxs-lookup"><span data-stu-id="83584-123">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="83584-124">Te duplikaty spowodują "wewnętrzny błąd serwera" podczas późniejszej próby uruchomienia projektu.</span><span class="sxs-lookup"><span data-stu-id="83584-124">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="83584-125">Na przykład jeśli `web.config` zawiera `<compilation debug="true" targetFramework="4.5.2" />` przed zainstalowaniem programu NuGet. Server, pakiet nie zastępuje go, ale wstawia drugi `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="83584-125">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="83584-126">W takim przypadku Usuń element ze starszą wersją struktury.</span><span class="sxs-lookup"><span data-stu-id="83584-126">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="83584-127">Aby udostępnić pakiety w kanale informacyjnym po opublikowaniu aplikacji na serwerze programu, Dodaj wszystkie `.nupkg` pliki do folderu `Packages` w programie Visual Studio, a następnie ustaw dla każdej z nich **akcję kompilacji** na **zawartość** i **Skopiuj ją do katalogu wyjściowego** w celu **skopiowania zawsze**:</span><span class="sxs-lookup"><span data-stu-id="83584-127">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Kopiowanie pakietów do folderu Packages w projekcie](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="83584-129">Uruchom lokację lokalnie w programie Visual Studio (przy użyciu **debugowania > Uruchom bez debugowania** lub CTRL + F5).</span><span class="sxs-lookup"><span data-stu-id="83584-129">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="83584-130">Strona główna zawiera adresy URL kanału informacyjnego pakietu, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="83584-130">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="83584-131">Jeśli widzisz błędy, uważnie Przeprowadź inspekcję `web.config` pod kątem zduplikowanych elementów w kroku 5.</span><span class="sxs-lookup"><span data-stu-id="83584-131">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![Domyślna strona główna aplikacji z pakietem NuGet. Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="83584-133">Kliknij **tutaj** w obszarze przedstawionym powyżej, aby zobaczyć źródło danych OData pakietów.</span><span class="sxs-lookup"><span data-stu-id="83584-133">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="83584-134">Przy pierwszym uruchomieniu aplikacji NuGet. serwer ponownie tworzy strukturę folderu `Packages`, aby zawierał folder dla każdego pakietu.</span><span class="sxs-lookup"><span data-stu-id="83584-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="83584-135">Jest to zgodne z [lokalnym układem magazynu](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) wprowadzonym z pakietem NuGet 3,3 w celu zwiększenia wydajności.</span><span class="sxs-lookup"><span data-stu-id="83584-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="83584-136">W przypadku dodawania kolejnych pakietów Kontynuuj korzystanie z tej struktury.</span><span class="sxs-lookup"><span data-stu-id="83584-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="83584-137">Po przetestowaniu lokalnego wdrożenia należy wdrożyć aplikację w dowolnej innej lokacji wewnętrznej lub zewnętrznej, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="83584-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="83584-138">Po wdrożeniu do `http://<domain>`adres URL używany dla źródła pakietu zostanie `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="83584-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="83584-139">Konfigurowanie folderu Packages</span><span class="sxs-lookup"><span data-stu-id="83584-139">Configuring the Packages folder</span></span>

<span data-ttu-id="83584-140">W przypadku `NuGet.Server` 1,5 i nowszych można dokładniej skonfigurować folder pakietu przy użyciu wartości `appSetting/packagesPath` w `web.config`:</span><span class="sxs-lookup"><span data-stu-id="83584-140">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="83584-141">`packagesPath` może być ścieżką bezwzględną lub wirtualną.</span><span class="sxs-lookup"><span data-stu-id="83584-141">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="83584-142">Po pominięciu `packagesPath` lub pozostawieniu pustego pola folder Packages jest domyślnym `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="83584-142">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="83584-143">Zewnętrzne dodawanie pakietów do źródła danych</span><span class="sxs-lookup"><span data-stu-id="83584-143">Adding packages to the feed externally</span></span>

<span data-ttu-id="83584-144">Po uruchomieniu lokacji NuGet. Server można dodać pakiety przy użyciu [wypychania NuGet](../reference/cli-reference/cli-ref-push.md) , pod warunkiem, że wartość klucza interfejsu API jest ustawiona w `web.config`.</span><span class="sxs-lookup"><span data-stu-id="83584-144">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="83584-145">Po zainstalowaniu pakietu NuGet. Server `web.config` zawiera pustą wartość `appSetting/apiKey`:</span><span class="sxs-lookup"><span data-stu-id="83584-145">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="83584-146">W przypadku pominięcia `apiKey` lub pustego, wypchnięcie pakietów do źródła danych jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="83584-146">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="83584-147">Aby włączyć tę funkcję, należy ustawić `apiKey` na wartość (idealnie silne hasło) i dodać klucz o nazwie `appSettings/requireApiKey` z wartością `true`:</span><span class="sxs-lookup"><span data-stu-id="83584-147">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="83584-148">Jeśli serwer jest już zabezpieczony lub nie jest wymagany klucz interfejsu API (na przykład w przypadku korzystania z serwera prywatnego w lokalnej sieci zespołowej), można ustawić `requireApiKey` na `false`.</span><span class="sxs-lookup"><span data-stu-id="83584-148">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="83584-149">Wszyscy użytkownicy z dostępem do serwera mogą następnie wysyłać pakiety.</span><span class="sxs-lookup"><span data-stu-id="83584-149">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="83584-150">Usuwanie pakietów ze źródła danych</span><span class="sxs-lookup"><span data-stu-id="83584-150">Removing packages from the feed</span></span>

<span data-ttu-id="83584-151">W pakiecie NuGet. Server polecenie [NuGet Delete](../reference/cli-reference/cli-ref-delete.md) usuwa pakiet z repozytorium, pod warunkiem, że dołączysz klucz interfejsu API z komentarzem.</span><span class="sxs-lookup"><span data-stu-id="83584-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="83584-152">Jeśli chcesz zmienić zachowanie w celu wyłączania pakietu zamiast niego (pozostawiając dostęp do przywracania pakietu), Zmień klucz `enableDelisting` w `web.config` na true.</span><span class="sxs-lookup"><span data-stu-id="83584-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="83584-153">NuGet. Server — obsługa</span><span class="sxs-lookup"><span data-stu-id="83584-153">NuGet.Server support</span></span>

<span data-ttu-id="83584-154">Aby uzyskać dodatkową pomoc dotyczącą korzystania z programu NuGet. Server, Utwórz problem na [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="83584-154">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>