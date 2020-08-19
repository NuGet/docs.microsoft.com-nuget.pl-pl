---
title: Używanie narzędzia NuGet. Server do hostowania źródeł danych NuGet
description: Jak utworzyć i hostować źródło pakietów NuGet na dowolnym serwerze, na którym są uruchomione usługi IIS, przy użyciu NuGet. Server, dzięki czemu pakiety są dostępne za pośrednictwem protokołów HTTP i OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 7a806e6b586c63c701642c9e43865cb077d7999c
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623048"
---
# <a name="nugetserver"></a><span data-ttu-id="39c92-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="39c92-103">NuGet.Server</span></span>

<span data-ttu-id="39c92-104">NuGet. Server jest pakietem dostarczanym przez platformę .NET Foundation, który tworzy aplikację ASP.NET, która umożliwia hostowanie kanału informacyjnego pakietu na dowolnym serwerze, na którym są uruchomione usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="39c92-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="39c92-105">Po prostu program NuGet. Server udostępnia folder na serwerze za pośrednictwem protokołu HTTP (w przypadku usługi OData).</span><span class="sxs-lookup"><span data-stu-id="39c92-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="39c92-106">Jest ona łatwa do skonfigurowania i jest Najlepsza w przypadku prostych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="39c92-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="39c92-107">Utwórz pustą aplikację sieci Web ASP.NET w programie Visual Studio i Dodaj do niej pakiet NuGet. Server.</span><span class="sxs-lookup"><span data-stu-id="39c92-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="39c92-108">Skonfiguruj `Packages` folder w aplikacji i Dodaj pakiety.</span><span class="sxs-lookup"><span data-stu-id="39c92-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="39c92-109">Wdróż aplikację na odpowiednim serwerze.</span><span class="sxs-lookup"><span data-stu-id="39c92-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="39c92-110">W poniższych sekcjach szczegółowo omówiono ten proces przy użyciu języka C#.</span><span class="sxs-lookup"><span data-stu-id="39c92-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="39c92-111">Jeśli masz więcej pytań na temat NuGet. Server, Utwórz problem [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) .</span><span class="sxs-lookup"><span data-stu-id="39c92-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="39c92-112">Tworzenie i wdrażanie aplikacji sieci Web ASP.NET za pomocą narzędzia NuGet. Server</span><span class="sxs-lookup"><span data-stu-id="39c92-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="39c92-113">W programie Visual Studio wybierz pozycję **plik > nowy > projekt**, wyszukaj ciąg "aplikacja sieci Web ASP.NET (.NET Framework)", wybierz odpowiedni szablon dla **języka C#**.</span><span class="sxs-lookup"><span data-stu-id="39c92-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET Web Application (.NET Framework)", select the matching template for **C#**.</span></span>

    ![Wybierz szablon projektu sieci Web .NET Framework](media/Hosting_00-NuGet.Server-ProjectType.png)

1. <span data-ttu-id="39c92-115">Ustaw **strukturę** na ".NET Framework 4,6".</span><span class="sxs-lookup"><span data-stu-id="39c92-115">Set **Framework** to ".NET Framework 4.6".</span></span>

    ![Ustawianie platformy docelowej dla nowego projektu](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="39c92-117">Nadaj aplikacji odpowiednią nazwę *inną* niż NuGet. Server, wybierz pozycję OK, a następnie w następnym oknie dialogowym wybierz **pusty** szablon, a następnie wybierz **przycisk OK**.</span><span class="sxs-lookup"><span data-stu-id="39c92-117">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

    ![Wybierz pusty projekt sieci Web](media/Hosting_02-NuGet.Server-Empty.png)

1. <span data-ttu-id="39c92-119">Kliknij prawym przyciskiem myszy projekt, a następnie wybierz pozycję **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="39c92-119">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="39c92-120">W interfejsie użytkownika Menedżera pakietów wybierz kartę **przeglądanie** , a następnie wyszukaj i zainstaluj najnowszą wersję pakietu NuGet. Server, jeśli jesteś celem .NET Framework 4,6.</span><span class="sxs-lookup"><span data-stu-id="39c92-120">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="39c92-121">(Można go także zainstalować z konsoli Menedżera pakietów w programie `Install-Package NuGet.Server` ). Zaakceptuj postanowienia licencyjne, jeśli zostanie wyświetlony monit.</span><span class="sxs-lookup"><span data-stu-id="39c92-121">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Instalowanie pakietu NuGet. Server](media/Hosting_03-NuGet.Server-Package.png)

1. <span data-ttu-id="39c92-123">Instalowanie NuGet. serwer konwertuje pustą aplikację sieci Web na źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="39c92-123">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="39c92-124">Instaluje różne inne pakiety, tworzy `Packages` folder w aplikacji i modyfikuje `web.config` w celu uwzględnienia dodatkowych ustawień (szczegółowe informacje znajdują się w komentarzach w tym pliku).</span><span class="sxs-lookup"><span data-stu-id="39c92-124">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="39c92-125">Uważnie Zbadaj po wykonaniu przez `web.config` pakiet NuGet. Server zmian w tym pliku.</span><span class="sxs-lookup"><span data-stu-id="39c92-125">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="39c92-126">NuGet. Server nie może zastąpić istniejących elementów, ale zamiast tego utworzyć zduplikowane elementy.</span><span class="sxs-lookup"><span data-stu-id="39c92-126">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="39c92-127">Te duplikaty spowodują "wewnętrzny błąd serwera" podczas późniejszej próby uruchomienia projektu.</span><span class="sxs-lookup"><span data-stu-id="39c92-127">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="39c92-128">Na przykład jeśli `web.config` zawiera `<compilation debug="true" targetFramework="4.5.2" />` przed zainstalowaniem NuGet. Server, pakiet nie zastępuje go, ale wstawia sekundę `<compilation debug="true" targetFramework="4.6" />` .</span><span class="sxs-lookup"><span data-stu-id="39c92-128">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="39c92-129">W takim przypadku Usuń element ze starszą wersją struktury.</span><span class="sxs-lookup"><span data-stu-id="39c92-129">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="39c92-130">Uruchom lokację lokalnie w programie Visual Studio (przy użyciu **debugowania > Uruchom bez debugowania** lub CTRL + F5).</span><span class="sxs-lookup"><span data-stu-id="39c92-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="39c92-131">Strona główna zawiera adresy URL kanału informacyjnego pakietu, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="39c92-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="39c92-132">Jeśli widzisz błędy, uważnie Przeprowadź inspekcję pod `web.config` kątem zduplikowanych elementów zgodnie z wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="39c92-132">If you see errors, carefully inspect your `web.config` for duplicate elements as noted earlier.</span></span>

    ![Domyślna strona główna aplikacji z pakietem NuGet. Server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  <span data-ttu-id="39c92-134">Przy pierwszym uruchomieniu aplikacji NuGet. serwer ponownie tworzy strukturę folderu tak, `Packages` aby zawierał folder dla każdego pakietu.</span><span class="sxs-lookup"><span data-stu-id="39c92-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="39c92-135">Jest to zgodne z [lokalnym układem magazynu](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) wprowadzonym z pakietem NuGet 3,3 w celu zwiększenia wydajności.</span><span class="sxs-lookup"><span data-stu-id="39c92-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="39c92-136">W przypadku dodawania kolejnych pakietów Kontynuuj korzystanie z tej struktury.</span><span class="sxs-lookup"><span data-stu-id="39c92-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="39c92-137">Po przetestowaniu lokalnego wdrożenia należy wdrożyć aplikację w dowolnej innej lokacji wewnętrznej lub zewnętrznej, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="39c92-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="39c92-138">Po wdrożeniu w `http://<domain>` programie adres URL używany dla źródła pakietu będzie miał wartość `http://<domain>/nuget` .</span><span class="sxs-lookup"><span data-stu-id="39c92-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="39c92-139">Zewnętrzne dodawanie pakietów do źródła danych</span><span class="sxs-lookup"><span data-stu-id="39c92-139">Adding packages to the feed externally</span></span>

<span data-ttu-id="39c92-140">Po uruchomieniu lokacji NuGet. Server można dodać pakiety przy użyciu [wypychania NuGet](../reference/cli-reference/cli-ref-push.md) , pod warunkiem, że wartość klucza interfejsu API jest ustawiona w `web.config` .</span><span class="sxs-lookup"><span data-stu-id="39c92-140">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="39c92-141">Po zainstalowaniu pakietu NuGet. Server program `web.config` zawiera pustą `appSetting/apiKey` wartość:</span><span class="sxs-lookup"><span data-stu-id="39c92-141">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="39c92-142">Gdy `apiKey` zostanie pominięte lub puste, wypychanie pakietów do źródła danych jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="39c92-142">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="39c92-143">Aby włączyć tę funkcję, należy ustawić `apiKey` na wartość (idealnie silne hasło) i dodać klucz o nazwie `appSettings/requireApiKey` z wartością `true` :</span><span class="sxs-lookup"><span data-stu-id="39c92-143">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="39c92-144">Jeśli serwer jest już zabezpieczony lub nie jest wymagany klucz interfejsu API (na przykład w przypadku korzystania z serwera prywatnego w lokalnej sieci zespołowej), można ustawić `requireApiKey` na wartość `false` .</span><span class="sxs-lookup"><span data-stu-id="39c92-144">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="39c92-145">Wszyscy użytkownicy z dostępem do serwera mogą następnie wysyłać pakiety.</span><span class="sxs-lookup"><span data-stu-id="39c92-145">All users with access to the server can then push packages.</span></span>

<span data-ttu-id="39c92-146">Począwszy od elementu NuGet. Server 3.0.0, adres URL dla pakietów wypychania został zmieniony na `http://<domain>/nuget` .</span><span class="sxs-lookup"><span data-stu-id="39c92-146">Starting with NuGet.Server 3.0.0, the URL for pushing packages was change to `http://<domain>/nuget`.</span></span> <span data-ttu-id="39c92-147">W wersji starszej niż 3.0.0, adres URL wypychania to `http://<domain>/api/v2/package` .</span><span class="sxs-lookup"><span data-stu-id="39c92-147">Prior to the 3.0.0 release, the push URL was `http://<domain>/api/v2/package`.</span></span>

<span data-ttu-id="39c92-148">W przypadku programu NuGet 3.2.1 i nowszego ten starszy adres URL `/api/v2/package` jest domyślnie włączony przy `/nuget` użyciu `enableLegacyPushRoute: true` opcji w konfiguracji startowej ( `NuGetODataConfig.cs` domyślnie).</span><span class="sxs-lookup"><span data-stu-id="39c92-148">With NuGet 3.2.1 and newer, this legacy URL `/api/v2/package` is enabled in addition to `/nuget` by default via `enableLegacyPushRoute: true` option in your startup config (`NuGetODataConfig.cs` by default).</span></span> <span data-ttu-id="39c92-149">Należy pamiętać, że ta funkcja nie działa, gdy wiele kanałów informacyjnych znajduje się w tym samym projekcie.</span><span class="sxs-lookup"><span data-stu-id="39c92-149">Note that this feature does not work when multiple feeds are hosted in the same project.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="39c92-150">Usuwanie pakietów ze źródła danych</span><span class="sxs-lookup"><span data-stu-id="39c92-150">Removing packages from the feed</span></span>

<span data-ttu-id="39c92-151">W pakiecie NuGet. Server polecenie [NuGet Delete](../reference/cli-reference/cli-ref-delete.md) usuwa pakiet z repozytorium, pod warunkiem, że dołączysz klucz interfejsu API z komentarzem.</span><span class="sxs-lookup"><span data-stu-id="39c92-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="39c92-152">Jeśli chcesz zmienić zachowanie w celu wyłączania pakietu zamiast niego (pozostawiając dostęp do przywracania pakietu), Zmień `enableDelisting` klucz w `web.config` na true.</span><span class="sxs-lookup"><span data-stu-id="39c92-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="39c92-153">Konfigurowanie folderu Packages</span><span class="sxs-lookup"><span data-stu-id="39c92-153">Configuring the Packages folder</span></span>

<span data-ttu-id="39c92-154">W przypadku `NuGet.Server` 1,5 i nowszych można dostosować folder pakietu przy użyciu `appSettings/packagesPath` wartości w `web.config` :</span><span class="sxs-lookup"><span data-stu-id="39c92-154">With `NuGet.Server` 1.5 and later, you can customize the package folder using the `appSettings/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="39c92-155">`packagesPath` może być ścieżką bezwzględną lub wirtualną.</span><span class="sxs-lookup"><span data-stu-id="39c92-155">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="39c92-156">Gdy `packagesPath` zostanie pominięte lub pozostawione puste, folder Packages jest wartością domyślną `~/Packages` .</span><span class="sxs-lookup"><span data-stu-id="39c92-156">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="making-packages-available-when-you-publish-the-web-app"></a><span data-ttu-id="39c92-157">Udostępnianie pakietów przy publikowaniu aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="39c92-157">Making packages available when you publish the web app</span></span>

<span data-ttu-id="39c92-158">Aby udostępnić pakiety w kanale informacyjnym po opublikowaniu aplikacji na serwerze programu, Dodaj wszystkie `.nupkg` pliki do `Packages` folderu w programie Visual Studio, a następnie ustaw dla każdej z nich **akcję kompilacji** na **zawartość** i **Skopiuj ją do katalogu wyjściowego** , aby **skopiować zawsze**:</span><span class="sxs-lookup"><span data-stu-id="39c92-158">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

![Kopiowanie pakietów do folderu Packages w projekcie](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a><span data-ttu-id="39c92-160">Uwagi do wersji</span><span class="sxs-lookup"><span data-stu-id="39c92-160">Release Notes</span></span>

<span data-ttu-id="39c92-161">Informacje o wersji programu NuGet. Server są dostępne na [stronie wydania usługi GitHub](https://github.com/NuGet/NuGet.Server/releases).</span><span class="sxs-lookup"><span data-stu-id="39c92-161">Release notes for NuGet.Server are available on the [GitHub release page](https://github.com/NuGet/NuGet.Server/releases).</span></span>
<span data-ttu-id="39c92-162">Obejmuje to szczegółowe informacje o poprawkach błędów i nowych funkcjach, które są dodawane.</span><span class="sxs-lookup"><span data-stu-id="39c92-162">This includes details about bug fixes and new features that are added.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="39c92-163">NuGet. Server — obsługa</span><span class="sxs-lookup"><span data-stu-id="39c92-163">NuGet.Server support</span></span>

<span data-ttu-id="39c92-164">Aby uzyskać dodatkową pomoc dotyczącą korzystania z programu NuGet. Server, Utwórz problem w systemie [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) .</span><span class="sxs-lookup"><span data-stu-id="39c92-164">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>
