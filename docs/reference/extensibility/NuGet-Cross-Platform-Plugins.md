---
title: NuGet cross platform wtyczek
description: NuGet cross platform wtyczek NuGet.exe, dotnet.exe, msbuild.exe i programu Visual Studio
author: nkolev92
ms.author: nikolev
manager: rrelyea
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: cf2c4fb484703b034a8569d053f2417fe58e41ff
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794199"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="3da19-103">NuGet cross platform wtyczek</span><span class="sxs-lookup"><span data-stu-id="3da19-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="3da19-104">W pakiecie NuGet 4.8 + została dodana obsługa wielu platform, wtyczki.</span><span class="sxs-lookup"><span data-stu-id="3da19-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="3da19-105">Osiągnięto to dzięki przez utworzenie nowego modelu rozszerzalności wtyczki, który ma być zgodna z ograniczeniami zestawu reguł działania.</span><span class="sxs-lookup"><span data-stu-id="3da19-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="3da19-106">Wtyczki są niezależne pliki wykonywalne (runnables w środowisku .NET Core), które klienci programu NuGet, uruchom w oddzielnym procesie.</span><span class="sxs-lookup"><span data-stu-id="3da19-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="3da19-107">Jest to wartość true, zapis raz uruchomić wszędzie, gdzie dodatku typu plug-in.</span><span class="sxs-lookup"><span data-stu-id="3da19-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="3da19-108">Będzie ona współdziałać z wszystkich narzędzi klienta programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="3da19-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="3da19-109">Wtyczki można .NET Framework (NuGet.exe, MSBuild.exe i programu Visual Studio) lub .NET Core (dotnet.exe).</span><span class="sxs-lookup"><span data-stu-id="3da19-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="3da19-110">Protokół komunikacyjny numerów wersji między klientem NuGet i wtyczka jest zdefiniowana.</span><span class="sxs-lookup"><span data-stu-id="3da19-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="3da19-111">Podczas uzgadniania uruchamiania 2 procesy negocjowania protokołu wersji.</span><span class="sxs-lookup"><span data-stu-id="3da19-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="3da19-112">Aby uwzględnić wszystkie scenariusze narzędzia klienta NuGet, należałoby jednej wtyczki platformy .NET Core i .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="3da19-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="3da19-113">Poniżej przedstawiono kombinacje klienta/framework wtyczki.</span><span class="sxs-lookup"><span data-stu-id="3da19-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="3da19-114">Narzędzie klienta</span><span class="sxs-lookup"><span data-stu-id="3da19-114">Client tool</span></span>  | <span data-ttu-id="3da19-115">Framework</span><span class="sxs-lookup"><span data-stu-id="3da19-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="3da19-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3da19-116">Visual Studio</span></span> | <span data-ttu-id="3da19-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3da19-117">.NET Framework</span></span> |
| <span data-ttu-id="3da19-118">DotNet.exe</span><span class="sxs-lookup"><span data-stu-id="3da19-118">dotnet.exe</span></span> | <span data-ttu-id="3da19-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3da19-119">.NET Core</span></span> |
| <span data-ttu-id="3da19-120">NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="3da19-120">NuGet.exe</span></span> | <span data-ttu-id="3da19-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3da19-121">.NET Framework</span></span> |
| <span data-ttu-id="3da19-122">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="3da19-122">MSBuild.exe</span></span> | <span data-ttu-id="3da19-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3da19-123">.NET Framework</span></span> |
| <span data-ttu-id="3da19-124">NuGet.exe na platformy Mono</span><span class="sxs-lookup"><span data-stu-id="3da19-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="3da19-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3da19-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="3da19-126">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="3da19-126">How does it work</span></span>

<span data-ttu-id="3da19-127">Przepływ pracy wysokiego poziomu, można przedstawić w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="3da19-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="3da19-128">NuGet odnajduje dostępne dodatki.</span><span class="sxs-lookup"><span data-stu-id="3da19-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="3da19-129">Jeśli ma to zastosowanie, NuGet, będzie ona przechodzić przez wtyczki w kolejności priorytetu i uruchamia je jeden po drugim.</span><span class="sxs-lookup"><span data-stu-id="3da19-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="3da19-130">NuGet użyje pierwszego wtyczkę, która może obsłużyć żądania.</span><span class="sxs-lookup"><span data-stu-id="3da19-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="3da19-131">Wtyczki zostanie zamknięty, gdy nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="3da19-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="3da19-132">Wymagania ogólne wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-132">General plugin requirements</span></span>

<span data-ttu-id="3da19-133">Bieżąca wersja protokołu jest *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="3da19-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="3da19-134">W tej wersji wymagania są następujące:</span><span class="sxs-lookup"><span data-stu-id="3da19-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="3da19-135">Należy mieć prawidłowy i zaufanej Authenticode podpisu zestawów, które będzie działać w Windows i platformy Mono.</span><span class="sxs-lookup"><span data-stu-id="3da19-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="3da19-136">Nie jest wymagane specjalne zaufania dla zestawów w systemie Linux i Mac jeszcze uruchomione.</span><span class="sxs-lookup"><span data-stu-id="3da19-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="3da19-137">Odpowiednie problem</span><span class="sxs-lookup"><span data-stu-id="3da19-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="3da19-138">Obsługa bezstanowych, uruchamiania w kontekście zabezpieczeń bieżącego narzędzia klienta programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="3da19-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="3da19-139">Na przykład narzędzia klienta programu NuGet nie będzie wykonywać podniesienia uprawnień lub dodatkowe inicjowania poza protokołu wtyczki opisanym w dalszej części.</span><span class="sxs-lookup"><span data-stu-id="3da19-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="3da19-140">Być nieinterakcyjny, chyba że jawnie określony.</span><span class="sxs-lookup"><span data-stu-id="3da19-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="3da19-141">Być zgodne z wersji protokołu wynegocjowanym wtyczki.</span><span class="sxs-lookup"><span data-stu-id="3da19-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="3da19-142">Odpowiedz na wszystkie żądania w rozsądnym czasie.</span><span class="sxs-lookup"><span data-stu-id="3da19-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="3da19-143">Honorować anulowania żądania dla każdej operacji w toku.</span><span class="sxs-lookup"><span data-stu-id="3da19-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="3da19-144">Specyfikacja techniczna jest opisany bardziej szczegółowo w specyfikacji następujące:</span><span class="sxs-lookup"><span data-stu-id="3da19-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="3da19-145">Wtyczka pobierania pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="3da19-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="3da19-146">NuGet krzyżowe wtyczki uwierzytelniania plat</span><span class="sxs-lookup"><span data-stu-id="3da19-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="3da19-147">Klient — interakcji wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-147">Client - Plugin interaction</span></span>

<span data-ttu-id="3da19-148">Narzędzia klienta programu NuGet i wtyczki komunikują się z JSON za pośrednictwem standardowych strumieni (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="3da19-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="3da19-149">Wszystkie dane muszą być zakodowane w formacie UTF-8.</span><span class="sxs-lookup"><span data-stu-id="3da19-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="3da19-150">Wtyczki są uruchamiane z argumentem "-wtyczki".</span><span class="sxs-lookup"><span data-stu-id="3da19-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="3da19-151">W przypadku, gdy użytkownik uruchamia bezpośrednio pliku wykonywalnego bez tego argumentu wtyczki, wtyczka może dać komunikat informacyjny, zamiast czekać na uzgadnianie protokołu.</span><span class="sxs-lookup"><span data-stu-id="3da19-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="3da19-152">Upłynął limit czasu protokołu uzgadniania to 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="3da19-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="3da19-153">Wtyczka powinno zająć instalacji w jako ograniczony ilości, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="3da19-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="3da19-154">Narzędzia klienta programu NuGet zapytanie obsługiwane operacje wtyczki, przekazując w indeksie usługi dla źródła pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="3da19-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="3da19-155">Wtyczki mogą używać indeksu usługi pod kątem obecności obsługiwanych typów usług.</span><span class="sxs-lookup"><span data-stu-id="3da19-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="3da19-156">Komunikacja między narzędzia klienta programu NuGet i wtyczka jest dwukierunkowy.</span><span class="sxs-lookup"><span data-stu-id="3da19-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="3da19-157">Każde żądanie ma limit czasu równy 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="3da19-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="3da19-158">Jeśli operacje są powinien trwać dłużej odpowiedniego procesu powinien wysłać komunikat o postępie, aby uniemożliwić żądania z przekroczeniem limitu czasu. Po 1 min braku wtyczkę uznaje się bezczynności i jest wyłączony.</span><span class="sxs-lookup"><span data-stu-id="3da19-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="3da19-159">Instalowanie wtyczki i odnajdywania</span><span class="sxs-lookup"><span data-stu-id="3da19-159">Plugin installation and discovery</span></span>

<span data-ttu-id="3da19-160">Wtyczki zostaną odnalezione za pośrednictwem struktury katalogów oparte na Konwencji.</span><span class="sxs-lookup"><span data-stu-id="3da19-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="3da19-161">Scenariusze ciągłej integracji/ciągłego Dostarczania i użytkownicy zaawansowani, można użyć zmiennej środowiskowej zastąpić zachowanie.</span><span class="sxs-lookup"><span data-stu-id="3da19-161">CI/CD scenarios and power users can use an environment variable to override the behavior.</span></span>

- <span data-ttu-id="3da19-162">`NUGET_PLUGIN_PATHS` -Definiuje wtyczki, który będzie używany dla tego procesu NuGet priorytet zastrzeżone.</span><span class="sxs-lookup"><span data-stu-id="3da19-162">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="3da19-163">Jeśli ustawiono tę zmienną środowiskową, zastępuje ona odnajdywanie oparte na Konwencji.</span><span class="sxs-lookup"><span data-stu-id="3da19-163">If this environment variable is set, it overrides the convention based discovery.</span></span>
-  <span data-ttu-id="3da19-164">Lokalizacja użytkownika, lokalizacji głównej NuGet w `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="3da19-164">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="3da19-165">Ta lokalizacja nie może zostać zastąpiony.</span><span class="sxs-lookup"><span data-stu-id="3da19-165">This location cannot be overriden.</span></span> <span data-ttu-id="3da19-166">Katalog główny różnych będzie używany dla wtyczek platformy .NET Core i .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="3da19-166">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="3da19-167">Framework</span><span class="sxs-lookup"><span data-stu-id="3da19-167">Framework</span></span> | <span data-ttu-id="3da19-168">Lokalizacja odnajdywania główna</span><span class="sxs-lookup"><span data-stu-id="3da19-168">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="3da19-169">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3da19-169">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="3da19-170">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3da19-170">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="3da19-171">Każdy dodatek typu plug-in powinien być zainstalowany w jego własnym folderze.</span><span class="sxs-lookup"><span data-stu-id="3da19-171">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="3da19-172">Punkt wejścia wtyczki będzie Nazwa zainstalowanego folderu, z rozszerzeniem dll dla platformy .NET Core i rozszerzenie .exe na platformie .NET.</span><span class="sxs-lookup"><span data-stu-id="3da19-172">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> <span data-ttu-id="3da19-173">Obecnie jest nie scenariusza użytkownika do zainstalowania wtyczki.</span><span class="sxs-lookup"><span data-stu-id="3da19-173">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="3da19-174">Jest tak proste, jak przenoszenie wymaganych plików do określonej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="3da19-174">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="3da19-175">Obsługiwane operacje</span><span class="sxs-lookup"><span data-stu-id="3da19-175">Supported operations</span></span>

<span data-ttu-id="3da19-176">Dwie operacje są obsługiwane w ramach nowego protokołu wtyczki.</span><span class="sxs-lookup"><span data-stu-id="3da19-176">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="3da19-177">Nazwa operacji</span><span class="sxs-lookup"><span data-stu-id="3da19-177">Operation name</span></span> | <span data-ttu-id="3da19-178">Wersja minimalna protokołu</span><span class="sxs-lookup"><span data-stu-id="3da19-178">Minimum protocol version</span></span> | <span data-ttu-id="3da19-179">Minimalna wersja klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="3da19-179">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="3da19-180">Pobierz pakiet</span><span class="sxs-lookup"><span data-stu-id="3da19-180">Download Package</span></span> | <span data-ttu-id="3da19-181">1.0.0</span><span class="sxs-lookup"><span data-stu-id="3da19-181">1.0.0</span></span> | <span data-ttu-id="3da19-182">4.3.0</span><span class="sxs-lookup"><span data-stu-id="3da19-182">4.3.0</span></span> |
| [<span data-ttu-id="3da19-183">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="3da19-183">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="3da19-184">2.0.0</span><span class="sxs-lookup"><span data-stu-id="3da19-184">2.0.0</span></span> | <span data-ttu-id="3da19-185">4.8.0</span><span class="sxs-lookup"><span data-stu-id="3da19-185">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="3da19-186">Uruchamiania wtyczek w obszarze poprawne środowiska uruchomieniowego</span><span class="sxs-lookup"><span data-stu-id="3da19-186">Running plugins under the correct runtime</span></span>

<span data-ttu-id="3da19-187">Dla pakietu NuGet w scenariuszach dotnet.exe wtyczek muszą być możliwe do wykonania w ramach tego określonego środowiska uruchomieniowego programu dotnet.exe.</span><span class="sxs-lookup"><span data-stu-id="3da19-187">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="3da19-188">Jest ona włączona dostawca wtyczki i konsumentów, upewnij się, że jest używana kombinacja dotnet.exe/plugin zgodny.</span><span class="sxs-lookup"><span data-stu-id="3da19-188">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="3da19-189">Potencjalny problem może wystąpić z wtyczek lokalizacji użytkownika, gdy na przykład, dotnet.exe w obszarze 2.0 środowiska uruchomieniowego próbuje użyć wtyczki, przeznaczony dla środowiska uruchomieniowego 2.1.</span><span class="sxs-lookup"><span data-stu-id="3da19-189">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="3da19-190">Funkcje pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="3da19-190">Capabilities caching</span></span>

<span data-ttu-id="3da19-191">Weryfikacja zabezpieczeń i wystąpienia wtyczki jest kosztowne.</span><span class="sxs-lookup"><span data-stu-id="3da19-191">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="3da19-192">Operacja pobierania odbywa się sposób częściej niż operację uwierzytelniania, jednak średni użytkownik NuGet jest tylko może mieć wtyczki uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="3da19-192">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="3da19-193">Aby ulepszyć środowisko pracy, NuGet będzie buforować oświadczeń operacji dla danego żądania.</span><span class="sxs-lookup"><span data-stu-id="3da19-193">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="3da19-194">Ta pamięć podręczna odbywa się dla wtyczki za pomocą klucza wtyczka jest ścieżka wtyczki, a czas wygaśnięcia pamięci podręcznej tej możliwości wynosi 30 dni.</span><span class="sxs-lookup"><span data-stu-id="3da19-194">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="3da19-195">Pamięć podręczna znajduje się w `%LocalAppData%/NuGet/plugins-cache` i zostać zastąpiona przez zmienną środowiskową `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="3da19-195">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="3da19-196">Aby wyczyścić to [pamięci podręcznej](../../consume-packages/managing-the-global-packages-and-cache-folders.md), jedno uruchomienie, aby zmienne polecenia `plugins-cache` opcji.</span><span class="sxs-lookup"><span data-stu-id="3da19-196">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="3da19-197">`all` Opcja lokalne teraz spowoduje również usunięcie pamięci podręcznej wtyczek.</span><span class="sxs-lookup"><span data-stu-id="3da19-197">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="3da19-198">Indeks komunikaty protokołu</span><span class="sxs-lookup"><span data-stu-id="3da19-198">Protocol messages index</span></span>

<span data-ttu-id="3da19-199">Wersja protokołu *1.0.0* wiadomości:</span><span class="sxs-lookup"><span data-stu-id="3da19-199">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="3da19-200">Zamknięcie</span><span class="sxs-lookup"><span data-stu-id="3da19-200">Close</span></span>
    * <span data-ttu-id="3da19-201">Żądanie kierunek: NuGet -> Wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-201">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3da19-202">Żądanie zawiera ładunek</span><span class="sxs-lookup"><span data-stu-id="3da19-202">The request will contain no payload</span></span>
    * <span data-ttu-id="3da19-203">Brak odpowiedzi jest oczekiwany.</span><span class="sxs-lookup"><span data-stu-id="3da19-203">No response is expected.</span></span>  <span data-ttu-id="3da19-204">Właściwej odpowiedzi jest niezwłocznie zakończyć działanie procesu wtyczki.</span><span class="sxs-lookup"><span data-stu-id="3da19-204">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="3da19-205">Skopiuj pliki w pakiecie</span><span class="sxs-lookup"><span data-stu-id="3da19-205">Copy files in package</span></span>
    * <span data-ttu-id="3da19-206">Żądanie kierunek: NuGet -> Wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-206">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3da19-207">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-207">The request will contain:</span></span>
        * <span data-ttu-id="3da19-208">Identyfikator pakietu i wersję</span><span class="sxs-lookup"><span data-stu-id="3da19-208">the package ID and version</span></span>
        * <span data-ttu-id="3da19-209">repozytorium lokalizacji źródłowej pakietu</span><span class="sxs-lookup"><span data-stu-id="3da19-209">the package source repository location</span></span>
        * <span data-ttu-id="3da19-210">Ścieżka katalogu docelowego</span><span class="sxs-lookup"><span data-stu-id="3da19-210">destination directory path</span></span>
        * <span data-ttu-id="3da19-211">Element wyliczalny z plików w pakiecie, który ma być kopiowana ścieżkę katalogu docelowego</span><span class="sxs-lookup"><span data-stu-id="3da19-211">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="3da19-212">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-212">A response will contain:</span></span>
        * <span data-ttu-id="3da19-213">Kod odpowiedzi, wskazując wynik operacji</span><span class="sxs-lookup"><span data-stu-id="3da19-213">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3da19-214">Element wyliczalny z pełnej ścieżki do kopiowanych plików w katalogu docelowym, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="3da19-214">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="3da19-215">Skopiuj plik pakietu (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="3da19-215">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="3da19-216">Żądanie kierunek: NuGet -> Wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-216">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3da19-217">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-217">The request will contain:</span></span>
        * <span data-ttu-id="3da19-218">Identyfikator pakietu i wersję</span><span class="sxs-lookup"><span data-stu-id="3da19-218">the package ID and version</span></span>
        * <span data-ttu-id="3da19-219">repozytorium lokalizacji źródłowej pakietu</span><span class="sxs-lookup"><span data-stu-id="3da19-219">the package source repository location</span></span>
        * <span data-ttu-id="3da19-220">Ścieżka pliku docelowego</span><span class="sxs-lookup"><span data-stu-id="3da19-220">the destination file path</span></span>
    * <span data-ttu-id="3da19-221">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-221">A response will contain:</span></span>
        * <span data-ttu-id="3da19-222">Kod odpowiedzi, wskazując wynik operacji</span><span class="sxs-lookup"><span data-stu-id="3da19-222">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="3da19-223">Uzyskiwanie poświadczeń</span><span class="sxs-lookup"><span data-stu-id="3da19-223">Get credentials</span></span>
    * <span data-ttu-id="3da19-224">Żądanie kierunek: wtyczka -> NuGet</span><span class="sxs-lookup"><span data-stu-id="3da19-224">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="3da19-225">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-225">The request will contain:</span></span>
        * <span data-ttu-id="3da19-226">repozytorium lokalizacji źródłowej pakietu</span><span class="sxs-lookup"><span data-stu-id="3da19-226">the package source repository location</span></span>
        * <span data-ttu-id="3da19-227">Kod stanu HTTP, które są uzyskiwane z repozytorium źródłowym pakietu przy użyciu bieżących poświadczeń</span><span class="sxs-lookup"><span data-stu-id="3da19-227">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="3da19-228">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-228">A response will contain:</span></span>
        * <span data-ttu-id="3da19-229">Kod odpowiedzi, wskazując wynik operacji</span><span class="sxs-lookup"><span data-stu-id="3da19-229">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3da19-230">Nazwa użytkownika, jeśli jest dostępny</span><span class="sxs-lookup"><span data-stu-id="3da19-230">a username, if available</span></span>
        * <span data-ttu-id="3da19-231">hasło, jeśli jest dostępny</span><span class="sxs-lookup"><span data-stu-id="3da19-231">a password, if available</span></span>

5.  <span data-ttu-id="3da19-232">Pobierz pliki w pakiecie</span><span class="sxs-lookup"><span data-stu-id="3da19-232">Get files in package</span></span>
    * <span data-ttu-id="3da19-233">Żądanie kierunek: NuGet -> Wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-233">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3da19-234">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-234">The request will contain:</span></span>
        * <span data-ttu-id="3da19-235">Identyfikator pakietu i wersję</span><span class="sxs-lookup"><span data-stu-id="3da19-235">the package ID and version</span></span>
        * <span data-ttu-id="3da19-236">repozytorium lokalizacji źródłowej pakietu</span><span class="sxs-lookup"><span data-stu-id="3da19-236">the package source repository location</span></span>
    * <span data-ttu-id="3da19-237">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-237">A response will contain:</span></span>
        * <span data-ttu-id="3da19-238">Kod odpowiedzi, wskazując wynik operacji</span><span class="sxs-lookup"><span data-stu-id="3da19-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3da19-239">Element wyliczalny z ścieżki plików w pakiecie, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="3da19-239">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="3da19-240">Rozpoczynanie operacji oświadczeń</span><span class="sxs-lookup"><span data-stu-id="3da19-240">Get operation claims</span></span> 
    * <span data-ttu-id="3da19-241">Żądanie kierunek: NuGet -> Wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3da19-242">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-242">The request will contain:</span></span>
        * <span data-ttu-id="3da19-243">index.json usługi dla źródła pakietów</span><span class="sxs-lookup"><span data-stu-id="3da19-243">the service index.json for a package source</span></span>
        * <span data-ttu-id="3da19-244">repozytorium lokalizacji źródłowej pakietu</span><span class="sxs-lookup"><span data-stu-id="3da19-244">the package source repository location</span></span>
    * <span data-ttu-id="3da19-245">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-245">A response will contain:</span></span>
        * <span data-ttu-id="3da19-246">Kod odpowiedzi, wskazując wynik operacji</span><span class="sxs-lookup"><span data-stu-id="3da19-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3da19-247">Element wyliczalny z obsługiwanych operacji (np.: Pobieranie pakietu) Jeśli operacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="3da19-247">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="3da19-248">Jeśli wtyczka nie obsługuje źródło pakietów, wtyczka musi zwracać pusty zestaw obsługiwanych operacji.</span><span class="sxs-lookup"><span data-stu-id="3da19-248">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="3da19-249">Ten komunikat został zaktualizowany w wersji *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="3da19-249">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="3da19-250">Jest na komputerze klienckim w celu zachowania zgodności z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="3da19-250">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="3da19-251">Pobierz skrót pakietu</span><span class="sxs-lookup"><span data-stu-id="3da19-251">Get package hash</span></span>
    * <span data-ttu-id="3da19-252">Żądanie kierunek: NuGet -> Wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-252">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3da19-253">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-253">The request will contain:</span></span>
        * <span data-ttu-id="3da19-254">Identyfikator pakietu i wersję</span><span class="sxs-lookup"><span data-stu-id="3da19-254">the package ID and version</span></span>
        * <span data-ttu-id="3da19-255">repozytorium lokalizacji źródłowej pakietu</span><span class="sxs-lookup"><span data-stu-id="3da19-255">the package source repository location</span></span>
        * <span data-ttu-id="3da19-256">Algorytm wyznaczania wartości skrótu</span><span class="sxs-lookup"><span data-stu-id="3da19-256">the hash algorithm</span></span>
    * <span data-ttu-id="3da19-257">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-257">A response will contain:</span></span>
        * <span data-ttu-id="3da19-258">Kod odpowiedzi, wskazując wynik operacji</span><span class="sxs-lookup"><span data-stu-id="3da19-258">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3da19-259">Skrót pliku pakietu, przy użyciu algorytmu mieszania żądanego, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="3da19-259">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="3da19-260">Pobieranie wersji pakietu</span><span class="sxs-lookup"><span data-stu-id="3da19-260">Get package versions</span></span>
    * <span data-ttu-id="3da19-261">Żądanie kierunek: NuGet -> Wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3da19-262">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-262">The request will contain:</span></span>
        * <span data-ttu-id="3da19-263">Identyfikator pakietu</span><span class="sxs-lookup"><span data-stu-id="3da19-263">the package ID</span></span>
        * <span data-ttu-id="3da19-264">repozytorium lokalizacji źródłowej pakietu</span><span class="sxs-lookup"><span data-stu-id="3da19-264">the package source repository location</span></span>
    * <span data-ttu-id="3da19-265">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-265">A response will contain:</span></span>
        * <span data-ttu-id="3da19-266">Kod odpowiedzi, wskazując wynik operacji</span><span class="sxs-lookup"><span data-stu-id="3da19-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3da19-267">Element wyliczalny z wersji pakietu, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="3da19-267">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="3da19-268">Pobierz indeks usług</span><span class="sxs-lookup"><span data-stu-id="3da19-268">Get service index</span></span>
    * <span data-ttu-id="3da19-269">Żądanie kierunek: wtyczka -> NuGet</span><span class="sxs-lookup"><span data-stu-id="3da19-269">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="3da19-270">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-270">The request will contain:</span></span>
        * <span data-ttu-id="3da19-271">repozytorium lokalizacji źródłowej pakietu</span><span class="sxs-lookup"><span data-stu-id="3da19-271">the package source repository location</span></span>
    * <span data-ttu-id="3da19-272">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-272">A response will contain:</span></span>
        * <span data-ttu-id="3da19-273">Kod odpowiedzi, wskazując wynik operacji</span><span class="sxs-lookup"><span data-stu-id="3da19-273">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3da19-274">Indeks usług, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="3da19-274">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="3da19-275">Uzgadnianie</span><span class="sxs-lookup"><span data-stu-id="3da19-275">Handshake</span></span>
     * <span data-ttu-id="3da19-276">Żądanie kierunek: wtyczka NuGet <> —</span><span class="sxs-lookup"><span data-stu-id="3da19-276">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="3da19-277">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-277">The request will contain:</span></span>
         * <span data-ttu-id="3da19-278">Bieżąca wersja protokołu wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-278">the current plugin protocol version</span></span>
         * <span data-ttu-id="3da19-279">Minimalna obsługiwana wersja protokołu wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-279">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="3da19-280">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-280">A response will contain:</span></span>
         * <span data-ttu-id="3da19-281">Kod odpowiedzi, wskazując wynik operacji</span><span class="sxs-lookup"><span data-stu-id="3da19-281">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="3da19-282">Wersja wynegocjowanym protokołem, jeśli operacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="3da19-282">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="3da19-283">Błąd spowoduje zakończenie wtyczki.</span><span class="sxs-lookup"><span data-stu-id="3da19-283">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="3da19-284">Inicjowanie</span><span class="sxs-lookup"><span data-stu-id="3da19-284">Initialize</span></span>
     * <span data-ttu-id="3da19-285">Żądanie kierunek: NuGet -> Wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-285">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3da19-286">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-286">The request will contain:</span></span>
         * <span data-ttu-id="3da19-287">wersja narzędzia NuGet klienta</span><span class="sxs-lookup"><span data-stu-id="3da19-287">the NuGet client tool version</span></span>
         * <span data-ttu-id="3da19-288">NuGet narzędzia skuteczne języku klienta.</span><span class="sxs-lookup"><span data-stu-id="3da19-288">the NuGet client tool effective language.</span></span>  <span data-ttu-id="3da19-289">Trwa to pod uwagę ustawienie ForceEnglishOutput, jeśli używany.</span><span class="sxs-lookup"><span data-stu-id="3da19-289">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="3da19-290">Domyślny limit czasu żądania, która zastępuje domyślną protokołu.</span><span class="sxs-lookup"><span data-stu-id="3da19-290">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="3da19-291">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-291">A response will contain:</span></span>
         * <span data-ttu-id="3da19-292">Kod odpowiedzi, wskazując wynik operacji.</span><span class="sxs-lookup"><span data-stu-id="3da19-292">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="3da19-293">Błąd spowoduje zakończenie wtyczki.</span><span class="sxs-lookup"><span data-stu-id="3da19-293">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="3da19-294">Log</span><span class="sxs-lookup"><span data-stu-id="3da19-294">Log</span></span>
     * <span data-ttu-id="3da19-295">Żądanie kierunek: wtyczka -> NuGet</span><span class="sxs-lookup"><span data-stu-id="3da19-295">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="3da19-296">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-296">The request will contain:</span></span>
         * <span data-ttu-id="3da19-297">poziom rejestrowania dla żądania</span><span class="sxs-lookup"><span data-stu-id="3da19-297">the log level for the request</span></span>
         * <span data-ttu-id="3da19-298">komunikat do zarejestrowania</span><span class="sxs-lookup"><span data-stu-id="3da19-298">a message to log</span></span>
     * <span data-ttu-id="3da19-299">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-299">A response will contain:</span></span>
         * <span data-ttu-id="3da19-300">Kod odpowiedzi, wskazując wynik operacji.</span><span class="sxs-lookup"><span data-stu-id="3da19-300">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="3da19-301">Zakończenie procesu NuGet monitora</span><span class="sxs-lookup"><span data-stu-id="3da19-301">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="3da19-302">Żądanie kierunek: NuGet -> Wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-302">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3da19-303">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-303">The request will contain:</span></span>
         * <span data-ttu-id="3da19-304">Identyfikator procesu NuGet</span><span class="sxs-lookup"><span data-stu-id="3da19-304">the NuGet process ID</span></span>
     * <span data-ttu-id="3da19-305">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-305">A response will contain:</span></span>
         * <span data-ttu-id="3da19-306">Kod odpowiedzi, wskazując wynik operacji.</span><span class="sxs-lookup"><span data-stu-id="3da19-306">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="3da19-307">Pakiet pobierania z wyprzedzeniem</span><span class="sxs-lookup"><span data-stu-id="3da19-307">Prefetch package</span></span>
     * <span data-ttu-id="3da19-308">Żądanie kierunek: NuGet -> Wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-308">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3da19-309">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-309">The request will contain:</span></span>
         * <span data-ttu-id="3da19-310">Identyfikator pakietu i wersję</span><span class="sxs-lookup"><span data-stu-id="3da19-310">the package ID and version</span></span>
         * <span data-ttu-id="3da19-311">repozytorium lokalizacji źródłowej pakietu</span><span class="sxs-lookup"><span data-stu-id="3da19-311">the package source repository location</span></span>
     * <span data-ttu-id="3da19-312">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-312">A response will contain:</span></span>
         * <span data-ttu-id="3da19-313">Kod odpowiedzi, wskazując wynik operacji</span><span class="sxs-lookup"><span data-stu-id="3da19-313">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="3da19-314">Ustaw poświadczenia</span><span class="sxs-lookup"><span data-stu-id="3da19-314">Set credentials</span></span>
     * <span data-ttu-id="3da19-315">Żądanie kierunek: NuGet -> Wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-315">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3da19-316">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-316">The request will contain:</span></span>
         * <span data-ttu-id="3da19-317">repozytorium lokalizacji źródłowej pakietu</span><span class="sxs-lookup"><span data-stu-id="3da19-317">the package source repository location</span></span>
         * <span data-ttu-id="3da19-318">ostatni znany pakiet źródła nazwę użytkownika, jeśli jest dostępny</span><span class="sxs-lookup"><span data-stu-id="3da19-318">the last known package source username, if available</span></span>
         * <span data-ttu-id="3da19-319">ostatnie hasło źródła znanych pakietu, jeśli jest dostępny</span><span class="sxs-lookup"><span data-stu-id="3da19-319">the last known package source password, if available</span></span>
         * <span data-ttu-id="3da19-320">ostatni znany nazwa użytkownika serwera proxy, jeśli jest dostępny</span><span class="sxs-lookup"><span data-stu-id="3da19-320">the last known proxy username, if available</span></span>
         * <span data-ttu-id="3da19-321">ostatnie hasło znanych serwera proxy, jeśli jest dostępny</span><span class="sxs-lookup"><span data-stu-id="3da19-321">the last known proxy password, if available</span></span>
     * <span data-ttu-id="3da19-322">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-322">A response will contain:</span></span>
         * <span data-ttu-id="3da19-323">Kod odpowiedzi, wskazując wynik operacji</span><span class="sxs-lookup"><span data-stu-id="3da19-323">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="3da19-324">Ustaw poziom dziennika</span><span class="sxs-lookup"><span data-stu-id="3da19-324">Set log level</span></span>
     * <span data-ttu-id="3da19-325">Żądanie kierunek: NuGet -> Wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-325">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="3da19-326">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-326">The request will contain:</span></span>
         * <span data-ttu-id="3da19-327">Domyślny poziom rejestrowania</span><span class="sxs-lookup"><span data-stu-id="3da19-327">the default log level</span></span>
     * <span data-ttu-id="3da19-328">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-328">A response will contain:</span></span>
         * <span data-ttu-id="3da19-329">Kod odpowiedzi, wskazując wynik operacji</span><span class="sxs-lookup"><span data-stu-id="3da19-329">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="3da19-330">Wersja protokołu *2.0.0* wiadomości</span><span class="sxs-lookup"><span data-stu-id="3da19-330">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="3da19-331">Rozpoczynanie operacji oświadczeń</span><span class="sxs-lookup"><span data-stu-id="3da19-331">Get Operation Claims</span></span>

* <span data-ttu-id="3da19-332">Żądanie kierunek: NuGet -> Wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-332">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="3da19-333">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-333">The request will contain:</span></span>
        * <span data-ttu-id="3da19-334">index.json usługi dla źródła pakietów</span><span class="sxs-lookup"><span data-stu-id="3da19-334">the service index.json for a package source</span></span>
        * <span data-ttu-id="3da19-335">repozytorium lokalizacji źródłowej pakietu</span><span class="sxs-lookup"><span data-stu-id="3da19-335">the package source repository location</span></span>
    * <span data-ttu-id="3da19-336">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-336">A response will contain:</span></span>
        * <span data-ttu-id="3da19-337">Kod odpowiedzi, wskazując wynik operacji</span><span class="sxs-lookup"><span data-stu-id="3da19-337">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="3da19-338">Element wyliczalny z obsługiwanych operacji, jeśli operacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="3da19-338">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="3da19-339">Jeśli wtyczka nie obsługuje źródło pakietów, wtyczka musi zwracać pusty zestaw obsługiwanych operacji.</span><span class="sxs-lookup"><span data-stu-id="3da19-339">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="3da19-340">Jeśli źródło indeks i pakiet usługi ma wartość null, wtyczka pozwala uzyskać odpowiedzi z uwierzytelnianiem.</span><span class="sxs-lookup"><span data-stu-id="3da19-340">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="3da19-341">Pobierz poświadczenia uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="3da19-341">Get Authentication Credentials</span></span>

* <span data-ttu-id="3da19-342">Żądanie kierunek: NuGet -> Wtyczki</span><span class="sxs-lookup"><span data-stu-id="3da19-342">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="3da19-343">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="3da19-343">The request will contain:</span></span>
    * <span data-ttu-id="3da19-344">Identyfikator URI</span><span class="sxs-lookup"><span data-stu-id="3da19-344">Uri</span></span>
    * <span data-ttu-id="3da19-345">isRetry</span><span class="sxs-lookup"><span data-stu-id="3da19-345">isRetry</span></span>
    * <span data-ttu-id="3da19-346">Nieinterakcyjnym</span><span class="sxs-lookup"><span data-stu-id="3da19-346">NonInteractive</span></span>
    * <span data-ttu-id="3da19-347">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="3da19-347">CanShowDialog</span></span>
* <span data-ttu-id="3da19-348">Odpowiedź będzie zawierać</span><span class="sxs-lookup"><span data-stu-id="3da19-348">A response will contain</span></span>
    * <span data-ttu-id="3da19-349">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="3da19-349">Username</span></span>
    * <span data-ttu-id="3da19-350">Hasło</span><span class="sxs-lookup"><span data-stu-id="3da19-350">Password</span></span>
    * <span data-ttu-id="3da19-351">Komunikat</span><span class="sxs-lookup"><span data-stu-id="3da19-351">Message</span></span>
    * <span data-ttu-id="3da19-352">Lista typów uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="3da19-352">List of Auth Types</span></span>
    * <span data-ttu-id="3da19-353">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="3da19-353">MessageResponseCode</span></span>