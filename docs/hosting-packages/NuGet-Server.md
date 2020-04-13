---
title: Używanie pliku NuGet.Server do hosta kanałów nuget
description: Jak utworzyć i hostować źródło danych pakietu NuGet na dowolnym serwerze z uruchomionymi usługami IIS przy użyciu serwera NuGet.Server, udostępniając pakiety za pośrednictwem protokołu HTTP i OData.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79059565"
---
# <a name="nugetserver"></a><span data-ttu-id="cd13a-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="cd13a-103">NuGet.Server</span></span>

<span data-ttu-id="cd13a-104">NuGet.Server to pakiet dostarczony przez fundację .NET, który tworzy aplikację ASP.NET, która może obsługiwać kanał informacyjny pakietu na dowolnym serwerze z uruchomiona usługami IIS.</span><span class="sxs-lookup"><span data-stu-id="cd13a-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="cd13a-105">Po prostu powiedział, NuGet.Server sprawia, że folder na serwerze dostępne za pośrednictwem HTTP(S) (w szczególności OData).</span><span class="sxs-lookup"><span data-stu-id="cd13a-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="cd13a-106">Jest łatwy w konfiguracji i najlepiej nadaje się do prostych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="cd13a-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="cd13a-107">Utwórz pustą aplikację sieci Web ASP.NET w programie Visual Studio i dodaj do niej pakiet NuGet.Server.</span><span class="sxs-lookup"><span data-stu-id="cd13a-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="cd13a-108">Skonfiguruj `Packages` folder w aplikacji i dodaj pakiety.</span><span class="sxs-lookup"><span data-stu-id="cd13a-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="cd13a-109">Wdrażanie aplikacji na odpowiednim serwerze.</span><span class="sxs-lookup"><span data-stu-id="cd13a-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="cd13a-110">W poniższych sekcjach opisano szczegółowo ten proces przy użyciu języka C#.</span><span class="sxs-lookup"><span data-stu-id="cd13a-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="cd13a-111">Jeśli masz dalsze pytania dotyczące programu NuGet.Server, utwórz problem w programie [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="cd13a-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="cd13a-112">Tworzenie i wdrażanie ASP.NET aplikacji sieci Web za pomocą pliku NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="cd13a-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="cd13a-113">W programie Visual Studio wybierz **pozycję Plik > nowy projekt >**, wyszukaj hasło "ASP.NET aplikacji sieci Web (.NET Framework)", wybierz pasujący szablon dla języka C#.</span><span class="sxs-lookup"><span data-stu-id="cd13a-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET Web Application (.NET Framework)", select the matching template for C#.</span></span>

    ![Wybieranie szablonu projektu sieci Web programu .NET Framework](media/Hosting_00-NuGet.Server-ProjectType.png)

1. <span data-ttu-id="cd13a-115">Ustaw **framework** na ".NET Framework 4.6".</span><span class="sxs-lookup"><span data-stu-id="cd13a-115">Set **Framework** to ".NET Framework 4.6".</span></span>

    ![Ustalanie ram docelowych dla nowego projektu](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="cd13a-117">Nadaj aplikacji odpowiednią nazwę *inną* niż NuGet.Server, wybierz przycisk OK, a w następnym oknie dialogowym wybierz **pusty** szablon, a następnie wybierz **przycisk OK**.</span><span class="sxs-lookup"><span data-stu-id="cd13a-117">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

    ![Wybieranie pustego projektu sieci Web](media/Hosting_02-NuGet.Server-Empty.png)

1. <span data-ttu-id="cd13a-119">Kliknij prawym przyciskiem myszy projekt, wybierz polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cd13a-119">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="cd13a-120">W interfejsie użytkownika Menedżera pakietów wybierz kartę **Przeglądaj,** a następnie wyszukaj i zainstaluj najnowszą wersję pakietu NuGet.Server, jeśli kierujesz reklamy na platformę .NET Framework 4.6.</span><span class="sxs-lookup"><span data-stu-id="cd13a-120">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="cd13a-121">(Można go również zainstalować z Konsoli `Install-Package NuGet.Server`Menedżera pakietów za pomocą .) Zaakceptuj postanowienia licencyjne, jeśli zostanie wyświetlony monit.</span><span class="sxs-lookup"><span data-stu-id="cd13a-121">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![Instalowanie pakietu NuGet.Server](media/Hosting_03-NuGet.Server-Package.png)

1. <span data-ttu-id="cd13a-123">Zainstalowanie serwera NuGet.Server konwertuje pustą aplikację sieci Web na źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="cd13a-123">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="cd13a-124">Instaluje wiele innych pakietów, `Packages` tworzy folder w aplikacji `web.config` i modyfikuje, aby uwzględnić dodatkowe ustawienia (szczegółowe informacje można znaleźć w komentarzach w tym pliku).</span><span class="sxs-lookup"><span data-stu-id="cd13a-124">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="cd13a-125">Dokładnie `web.config` sprawdź po nuget.server pakiet zakończył jego modyfikacje tego pliku.</span><span class="sxs-lookup"><span data-stu-id="cd13a-125">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="cd13a-126">NuGet.Server nie może zastąpić istniejące elementy, ale zamiast tego utworzyć zduplikowane elementy.</span><span class="sxs-lookup"><span data-stu-id="cd13a-126">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="cd13a-127">Te duplikaty spowoduje "Wewnętrzny błąd serwera", gdy później spróbujesz uruchomić projekt.</span><span class="sxs-lookup"><span data-stu-id="cd13a-127">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="cd13a-128">Na przykład, `web.config` jeśli `<compilation debug="true" targetFramework="4.5.2" />` zawiera przed zainstalowaniem NuGet.Server, pakiet nie zastępuje go, ale wstawia drugi `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="cd13a-128">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="cd13a-129">W takim przypadku usuń element ze starszą wersją frameworka.</span><span class="sxs-lookup"><span data-stu-id="cd13a-129">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="cd13a-130">Uruchom witrynę lokalnie w programie Visual Studio (przy użyciu **debugowania > start bez debugowania** lub Ctrl+F5).</span><span class="sxs-lookup"><span data-stu-id="cd13a-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="cd13a-131">Strona główna zawiera adresy URL kanału informacyjnego pakietu, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="cd13a-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="cd13a-132">Jeśli widzisz błędy, należy `web.config` dokładnie sprawdzić, czy nie ma zduplikowanych elementów, jak wspomniano wcześniej.</span><span class="sxs-lookup"><span data-stu-id="cd13a-132">If you see errors, carefully inspect your `web.config` for duplicate elements as noted earlier.</span></span>

    ![Domyślna strona główna aplikacji z nuget.server](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  <span data-ttu-id="cd13a-134">Przy pierwszym uruchomieniu aplikacji nuget.server restrukturyzuje folder, `Packages` aby zawierał folder dla każdego pakietu.</span><span class="sxs-lookup"><span data-stu-id="cd13a-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="cd13a-135">To pasuje do [układu magazynu lokalnego](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) wprowadzone z NuGet 3.3 w celu zwiększenia wydajności.</span><span class="sxs-lookup"><span data-stu-id="cd13a-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="cd13a-136">Podczas dodawania większej liczby pakietów, kontynuuj podążanie za tą strukturą.</span><span class="sxs-lookup"><span data-stu-id="cd13a-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="cd13a-137">Po przetestowaniu wdrożenia lokalnego należy wdrożyć aplikację w dowolnej innej lokacji wewnętrznej lub zewnętrznej, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="cd13a-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="cd13a-138">Po wdrożeniu do `http://<domain>`, adres URL, `http://<domain>/nuget`który jest używany dla źródła pakietu będzie .</span><span class="sxs-lookup"><span data-stu-id="cd13a-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="cd13a-139">Dodawanie pakietów do kanału zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="cd13a-139">Adding packages to the feed externally</span></span>

<span data-ttu-id="cd13a-140">Po uruchomieniu witryny NuGet.Server można dodać pakiety za pomocą [nuget](../reference/cli-reference/cli-ref-push.md) push `web.config`pod warunkiem ustawienia wartości klucza interfejsu API w pliku .</span><span class="sxs-lookup"><span data-stu-id="cd13a-140">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="cd13a-141">Po zainstalowaniu pakietu NuGet.Server `web.config` `appSetting/apiKey` zawiera pustą wartość:</span><span class="sxs-lookup"><span data-stu-id="cd13a-141">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="cd13a-142">Po `apiKey` pominięciu lub pustym wypychanie pakietów do kanału informacyjnego jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="cd13a-142">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="cd13a-143">Aby włączyć tę funkcję, `apiKey` ustaw wartość (najlepiej silne hasło) i `appSettings/requireApiKey` dodaj klucz `true`o nazwie o wartości:</span><span class="sxs-lookup"><span data-stu-id="cd13a-143">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="cd13a-144">Jeśli serwer jest już zabezpieczony lub w przeciwnym razie nie jest wymagany klucz interfejsu API (na `false`przykład podczas korzystania z serwera prywatnego w lokalnej sieci zespołu), można ustawić opcję `requireApiKey` .</span><span class="sxs-lookup"><span data-stu-id="cd13a-144">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="cd13a-145">Wszyscy użytkownicy z dostępem do serwera mogą następnie wypychać pakiety.</span><span class="sxs-lookup"><span data-stu-id="cd13a-145">All users with access to the server can then push packages.</span></span>

<span data-ttu-id="cd13a-146">Począwszy od NuGet.Server 3.0.0, adres URL `http://<domain>/nuget`do pchania pakietów został zmieniony na .</span><span class="sxs-lookup"><span data-stu-id="cd13a-146">Starting with NuGet.Server 3.0.0, the URL for pushing packages was change to `http://<domain>/nuget`.</span></span> <span data-ttu-id="cd13a-147">Przed wydaniem wersji 3.0.0 adres `http://<domain>/api/v2/package`URL wypychania wynosił .</span><span class="sxs-lookup"><span data-stu-id="cd13a-147">Prior to the 3.0.0 release, the push URL was `http://<domain>/api/v2/package`.</span></span>

<span data-ttu-id="cd13a-148">Z NuGet 3.2.1 i nowsze, ten `/api/v2/package` starszy `/nuget` adres `enableLegacyPushRoute: true` URL jest włączona`NuGetODataConfig.cs` oprócz domyślnie za pomocą opcji w konfiguracji uruchamiania (domyślnie).</span><span class="sxs-lookup"><span data-stu-id="cd13a-148">With NuGet 3.2.1 and newer, this legacy URL `/api/v2/package` is enabled in addition to `/nuget` by default via `enableLegacyPushRoute: true` option in your startup config (`NuGetODataConfig.cs` by default).</span></span> <span data-ttu-id="cd13a-149">Należy zauważyć, że ta funkcja nie działa, gdy wiele kanałów informacyjnych są hostowane w tym samym projekcie.</span><span class="sxs-lookup"><span data-stu-id="cd13a-149">Note that this feature does not work when multiple feeds are hosted in the same project.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="cd13a-150">Usuwanie opakowań z podajnika</span><span class="sxs-lookup"><span data-stu-id="cd13a-150">Removing packages from the feed</span></span>

<span data-ttu-id="cd13a-151">W systemie NuGet.Server polecenie [nuget delete](../reference/cli-reference/cli-ref-delete.md) usuwa pakiet z repozytorium pod warunkiem, że klucz interfejsu API jest dołączany do komentarza.</span><span class="sxs-lookup"><span data-stu-id="cd13a-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="cd13a-152">Jeśli chcesz zmienić zachowanie, aby wykreślić pakiet zamiast (pozostawiając `enableDelisting` go `web.config` dostępny do przywrócenia pakietu), zmień klucz na true.</span><span class="sxs-lookup"><span data-stu-id="cd13a-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="cd13a-153">Konfigurowanie folderu Pakiety</span><span class="sxs-lookup"><span data-stu-id="cd13a-153">Configuring the Packages folder</span></span>

<span data-ttu-id="cd13a-154">W `NuGet.Server` 1.5 lub nowszym folderze można `appSettings/packagesPath` dostosować `web.config`folder pakietu za pomocą wartości w :</span><span class="sxs-lookup"><span data-stu-id="cd13a-154">With `NuGet.Server` 1.5 and later, you can customize the package folder using the `appSettings/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="cd13a-155">`packagesPath`może być ścieżką bezwzględną lub wirtualną.</span><span class="sxs-lookup"><span data-stu-id="cd13a-155">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="cd13a-156">Po `packagesPath` pominięciu lub pozostawieniu pustego folderu pakietów jest domyślny `~/Packages`folder .</span><span class="sxs-lookup"><span data-stu-id="cd13a-156">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="making-packages-available-when-you-publish-the-web-app"></a><span data-ttu-id="cd13a-157">Udostępnianie pakietów podczas publikowania aplikacji internetowej</span><span class="sxs-lookup"><span data-stu-id="cd13a-157">Making packages available when you publish the web app</span></span>

<span data-ttu-id="cd13a-158">Aby udostępnić pakiety w kanale informacyjnym podczas publikowania `.nupkg` aplikacji `Packages` na serwerze, należy dodać każdy plik do folderu w programie Visual Studio, a następnie ustawić **akcję kompilacji** każdego z nich na **zawartość** i **skopiuj do katalogu wyjściowego,** aby **zawsze skopiować:**</span><span class="sxs-lookup"><span data-stu-id="cd13a-158">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

![Kopiowanie pakietów do folderu Pakiety w projekcie](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a><span data-ttu-id="cd13a-160">Informacje o wersji</span><span class="sxs-lookup"><span data-stu-id="cd13a-160">Release Notes</span></span>

<span data-ttu-id="cd13a-161">Informacje o wersji dla serwera NuGet.Server są dostępne na [stronie wydania usługi GitHub](https://github.com/NuGet/NuGet.Server/releases).</span><span class="sxs-lookup"><span data-stu-id="cd13a-161">Release notes for NuGet.Server are available on the [GitHub release page](https://github.com/NuGet/NuGet.Server/releases).</span></span>
<span data-ttu-id="cd13a-162">Obejmuje to szczegółowe informacje na temat poprawek błędów i nowych funkcji, które są dodawane.</span><span class="sxs-lookup"><span data-stu-id="cd13a-162">This includes details about bug fixes and new features that are added.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="cd13a-163">Pomoc techniczna usługi NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="cd13a-163">NuGet.Server support</span></span>

<span data-ttu-id="cd13a-164">Aby uzyskać dodatkową pomoc dotyczącą korzystania z [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)pliku NuGet.Server, utwórz problem w programie .</span><span class="sxs-lookup"><span data-stu-id="cd13a-164">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>
