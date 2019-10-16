---
title: Wtyczki Międzyplatformowe NuGet
description: Dodatki Międzyplatformowe NuGet dla NuGet. exe, dotnet. exe, MSBuild. exe i Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380499"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="816fd-103">Wtyczki Międzyplatformowe NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="816fd-104">W NuGet 4.8 + Obsługa wtyczek międzyplatformowych została dodana.</span><span class="sxs-lookup"><span data-stu-id="816fd-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="816fd-105">Osiągnięto to przez utworzenie nowego modelu rozszerzalności wtyczki, który musi być zgodny z rygorystycznym zestawem reguł operacji.</span><span class="sxs-lookup"><span data-stu-id="816fd-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="816fd-106">Wtyczki to samodzielne pliki wykonywalne (runnables w środowisku .NET Core), które klienci NuGet uruchamiają w osobnym procesie.</span><span class="sxs-lookup"><span data-stu-id="816fd-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="816fd-107">Jest to jednokrotne zapis, uruchom wszędzie.</span><span class="sxs-lookup"><span data-stu-id="816fd-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="816fd-108">Będzie on działał ze wszystkimi narzędziami klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="816fd-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="816fd-109">Wtyczki mogą być albo .NET Framework (NuGet. exe, MSBuild. exe i Visual Studio) lub .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="816fd-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="816fd-110">Jest zdefiniowany protokół komunikacji z wersjami między klientem NuGet a wtyczką.</span><span class="sxs-lookup"><span data-stu-id="816fd-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="816fd-111">Podczas uzgadniania uruchamiania, 2 procesy negocjują wersję protokołu.</span><span class="sxs-lookup"><span data-stu-id="816fd-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="816fd-112">Aby uwzględnić wszystkie scenariusze narzędzi klienta NuGet, trzeba mieć zarówno .NET Framework, jak i wtyczkę .NET Core.</span><span class="sxs-lookup"><span data-stu-id="816fd-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="816fd-113">Poniżej opisano kombinacje klienta/struktury wtyczek.</span><span class="sxs-lookup"><span data-stu-id="816fd-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="816fd-114">Narzędzie klienta</span><span class="sxs-lookup"><span data-stu-id="816fd-114">Client tool</span></span>  | <span data-ttu-id="816fd-115">Framework</span><span class="sxs-lookup"><span data-stu-id="816fd-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="816fd-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="816fd-116">Visual Studio</span></span> | <span data-ttu-id="816fd-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="816fd-117">.NET Framework</span></span> |
| <span data-ttu-id="816fd-118">dotnet. exe</span><span class="sxs-lookup"><span data-stu-id="816fd-118">dotnet.exe</span></span> | <span data-ttu-id="816fd-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="816fd-119">.NET Core</span></span> |
| <span data-ttu-id="816fd-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="816fd-120">NuGet.exe</span></span> | <span data-ttu-id="816fd-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="816fd-121">.NET Framework</span></span> |
| <span data-ttu-id="816fd-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="816fd-122">MSBuild.exe</span></span> | <span data-ttu-id="816fd-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="816fd-123">.NET Framework</span></span> |
| <span data-ttu-id="816fd-124">NuGet. exe na mono</span><span class="sxs-lookup"><span data-stu-id="816fd-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="816fd-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="816fd-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="816fd-126">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="816fd-126">How does it work</span></span>

<span data-ttu-id="816fd-127">Przepływ pracy wysokiego poziomu można opisać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="816fd-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="816fd-128">Pakiet NuGet odnajduje dostępne wtyczki.</span><span class="sxs-lookup"><span data-stu-id="816fd-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="816fd-129">Jeśli ma to zastosowanie, pakiet NuGet przejdzie iterację na wtyczkach w kolejności priorytetu i uruchomi je po jednym.</span><span class="sxs-lookup"><span data-stu-id="816fd-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="816fd-130">Pakiet NuGet użyje pierwszej wtyczki, która może obsłużyć żądanie.</span><span class="sxs-lookup"><span data-stu-id="816fd-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="816fd-131">Wtyczki zostaną wyłączone, gdy nie będą już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="816fd-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="816fd-132">Ogólne wymagania wtyczki</span><span class="sxs-lookup"><span data-stu-id="816fd-132">General plugin requirements</span></span>

<span data-ttu-id="816fd-133">Bieżąca wersja protokołu to *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="816fd-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="816fd-134">W tej wersji wymagania są następujące:</span><span class="sxs-lookup"><span data-stu-id="816fd-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="816fd-135">Mają prawidłowy zestaw zaufanych podpisów Authenticode, które będą uruchamiane w systemie Windows i mono.</span><span class="sxs-lookup"><span data-stu-id="816fd-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="816fd-136">Nie ma jeszcze specjalnych wymagań zaufania dla zestawów uruchomionych w systemach Linux i Mac.</span><span class="sxs-lookup"><span data-stu-id="816fd-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="816fd-137">Istotny problem</span><span class="sxs-lookup"><span data-stu-id="816fd-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="816fd-138">Obsługa bezstanowego uruchamiania w ramach bieżącego kontekstu zabezpieczeń narzędzi klienckich programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="816fd-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="816fd-139">Na przykład narzędzia klienta NuGet nie będą wykonywały podniesienia uprawnień ani dodatkowego inicjowania poza protokołem wtyczki opisanym w dalszej części.</span><span class="sxs-lookup"><span data-stu-id="816fd-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="816fd-140">Nie jest interaktywny, chyba że zostanie jawnie określony.</span><span class="sxs-lookup"><span data-stu-id="816fd-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="816fd-141">Zgodność z wynegocjowaną wersją protokołu wtyczki.</span><span class="sxs-lookup"><span data-stu-id="816fd-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="816fd-142">Odpowiadanie na wszystkie żądania w rozsądnym czasie.</span><span class="sxs-lookup"><span data-stu-id="816fd-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="816fd-143">Honorować żądania anulowania dla każdej operacji w toku.</span><span class="sxs-lookup"><span data-stu-id="816fd-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="816fd-144">Specyfikacja techniczna została szczegółowo opisana w następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="816fd-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="816fd-145">Wtyczka pobierania pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="816fd-146">Wtyczka do uwierzytelniania między płytkami NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="816fd-147">Interakcja klienta — wtyczka</span><span class="sxs-lookup"><span data-stu-id="816fd-147">Client - Plugin interaction</span></span>

<span data-ttu-id="816fd-148">Narzędzia klienta i wtyczki programu NuGet komunikują się z notacją JSON przez strumienie standardowe (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="816fd-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="816fd-149">Wszystkie dane muszą być kodowane w formacie UTF-8.</span><span class="sxs-lookup"><span data-stu-id="816fd-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="816fd-150">Wtyczki są uruchamiane z argumentem "-plugin".</span><span class="sxs-lookup"><span data-stu-id="816fd-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="816fd-151">W przypadku, gdy użytkownik bezpośrednio uruchamia plik wykonywalny wtyczki bez tego argumentu, wtyczka może dać komunikat informacyjny, a nie oczekuje na uzgadnianie protokołu.</span><span class="sxs-lookup"><span data-stu-id="816fd-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="816fd-152">Limit czasu uzgadniania protokołu wynosi 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="816fd-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="816fd-153">Wtyczka powinna zakończyć instalację tak jak najkrótszej ilości, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="816fd-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="816fd-154">Narzędzia klienta NuGet będą badać obsługiwane operacje wtyczki, przekazując indeks usługi dla źródła NuGet.</span><span class="sxs-lookup"><span data-stu-id="816fd-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="816fd-155">Wtyczka może użyć indeksu usługi, aby sprawdzić obecność obsługiwanych typów usług.</span><span class="sxs-lookup"><span data-stu-id="816fd-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="816fd-156">Komunikacja między narzędziami klienta NuGet a wtyczką jest dwukierunkowa.</span><span class="sxs-lookup"><span data-stu-id="816fd-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="816fd-157">Każde żądanie ma limit czasu wynoszący 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="816fd-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="816fd-158">Jeśli operacje mają trwać dłużej, proces powinien wysłać komunikat o postępie, aby zapobiec przekroczeniu limitu czasu żądania. Po 1 minucie braku aktywności wtyczka jest uważana za bezczynną i jest zamykana.</span><span class="sxs-lookup"><span data-stu-id="816fd-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="816fd-159">Instalowanie i odnajdywanie wtyczki</span><span class="sxs-lookup"><span data-stu-id="816fd-159">Plugin installation and discovery</span></span>

<span data-ttu-id="816fd-160">Wtyczki zostaną odnalezione za pośrednictwem struktury katalogów na podstawie Konwencji.</span><span class="sxs-lookup"><span data-stu-id="816fd-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="816fd-161">Scenariusze ciągłej integracji/ciągłego wdrażania i Użytkownicy zaawansowani mogą używać zmiennych środowiskowych, aby przesłonić zachowanie.</span><span class="sxs-lookup"><span data-stu-id="816fd-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="816fd-162">W przypadku używania zmiennych środowiskowych dozwolone są tylko ścieżki bezwzględne.</span><span class="sxs-lookup"><span data-stu-id="816fd-162">When using environment variables, only absolute paths are allowed.</span></span> <span data-ttu-id="816fd-163">Należy pamiętać, że `NUGET_NETFX_PLUGIN_PATHS` i `NUGET_NETCORE_PLUGIN_PATHS` są dostępne tylko w przypadku używania 5.3 + wersji narzędzi NuGet i nowszych.</span><span class="sxs-lookup"><span data-stu-id="816fd-163">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="816fd-164">`NUGET_NETFX_PLUGIN_PATHS` — definiuje wtyczki, które będą używane przez narzędzia oparte na .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="816fd-164">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="816fd-165">Ma pierwszeństwo przed `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="816fd-165">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="816fd-166">(Tylko wersja 5.3 programu NuGet)</span><span class="sxs-lookup"><span data-stu-id="816fd-166">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="816fd-167">`NUGET_NETCORE_PLUGIN_PATHS` — definiuje wtyczki, które będą używane przez narzędzia oparte na oprogramowaniu .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="816fd-167">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="816fd-168">Ma pierwszeństwo przed `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="816fd-168">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="816fd-169">(Tylko wersja 5.3 programu NuGet)</span><span class="sxs-lookup"><span data-stu-id="816fd-169">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="816fd-170">`NUGET_PLUGIN_PATHS` — definiuje wtyczki, które będą używane dla tego procesu NuGet, a priorytet zachowano.</span><span class="sxs-lookup"><span data-stu-id="816fd-170">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority preserved.</span></span> <span data-ttu-id="816fd-171">Jeśli ta zmienna środowiskowa jest ustawiona, zastępuje ona metodę odnajdywania opartą na Konwencji.</span><span class="sxs-lookup"><span data-stu-id="816fd-171">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="816fd-172">Ignorowany, jeśli określono jedną z zmiennych określonych dla struktury.</span><span class="sxs-lookup"><span data-stu-id="816fd-172">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="816fd-173">Lokalizacja użytkownika, lokalizacja główna narzędzia NuGet w `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="816fd-173">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="816fd-174">Ta lokalizacja nie może być przesłonięta.</span><span class="sxs-lookup"><span data-stu-id="816fd-174">This location cannot be overriden.</span></span> <span data-ttu-id="816fd-175">Dla wtyczek platformy .NET Core i .NET Framework zostanie użyty inny katalog główny.</span><span class="sxs-lookup"><span data-stu-id="816fd-175">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="816fd-176">Framework</span><span class="sxs-lookup"><span data-stu-id="816fd-176">Framework</span></span> | <span data-ttu-id="816fd-177">Główna lokalizacja odnajdowania</span><span class="sxs-lookup"><span data-stu-id="816fd-177">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="816fd-178">.NET Core</span><span class="sxs-lookup"><span data-stu-id="816fd-178">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="816fd-179">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="816fd-179">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="816fd-180">Każda wtyczka powinna być zainstalowana we własnym folderze.</span><span class="sxs-lookup"><span data-stu-id="816fd-180">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="816fd-181">Punkt wejścia wtyczki będzie nazwą zainstalowanego folderu z rozszerzeniami dll dla programu .NET Core i rozszerzeniem exe dla .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="816fd-181">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="816fd-182">Obecnie nie ma żadnego scenariusza użytkownika dla instalacji wtyczek.</span><span class="sxs-lookup"><span data-stu-id="816fd-182">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="816fd-183">Jest to proste przeniesienie wymaganych plików do wstępnie wskazanej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="816fd-183">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="816fd-184">Obsługiwane operacje</span><span class="sxs-lookup"><span data-stu-id="816fd-184">Supported operations</span></span>

<span data-ttu-id="816fd-185">W ramach nowego protokołu wtyczki są obsługiwane dwie operacje.</span><span class="sxs-lookup"><span data-stu-id="816fd-185">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="816fd-186">Nazwa operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-186">Operation name</span></span> | <span data-ttu-id="816fd-187">Minimalna wersja protokołu</span><span class="sxs-lookup"><span data-stu-id="816fd-187">Minimum protocol version</span></span> | <span data-ttu-id="816fd-188">Minimalna wersja klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-188">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="816fd-189">Pobierz pakiet</span><span class="sxs-lookup"><span data-stu-id="816fd-189">Download Package</span></span> | <span data-ttu-id="816fd-190">1.0.0</span><span class="sxs-lookup"><span data-stu-id="816fd-190">1.0.0</span></span> | <span data-ttu-id="816fd-191">4.3.0</span><span class="sxs-lookup"><span data-stu-id="816fd-191">4.3.0</span></span> |
| [<span data-ttu-id="816fd-192">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="816fd-192">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="816fd-193">2.0.0</span><span class="sxs-lookup"><span data-stu-id="816fd-193">2.0.0</span></span> | <span data-ttu-id="816fd-194">4.8.0</span><span class="sxs-lookup"><span data-stu-id="816fd-194">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="816fd-195">Uruchamianie wtyczek w prawidłowym środowisku uruchomieniowym</span><span class="sxs-lookup"><span data-stu-id="816fd-195">Running plugins under the correct runtime</span></span>

<span data-ttu-id="816fd-196">W przypadku pakietu NuGet w scenariuszach programu dotnet. exe wtyczki muszą być w stanie wykonać w tym konkretnym czasie wykonywania programu dotnet. exe.</span><span class="sxs-lookup"><span data-stu-id="816fd-196">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="816fd-197">Jest on dostawcą wtyczki i konsumentem, aby upewnić się, że jest używana kombinacja dotnet. exe/wtyczka.</span><span class="sxs-lookup"><span data-stu-id="816fd-197">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="816fd-198">Potencjalny problem może wystąpić w przypadku wtyczek do lokalizacji użytkownika, gdy na przykład program dotnet. exe w środowisku uruchomieniowym 2,0 próbuje użyć wtyczki zarejestrowanej dla środowiska uruchomieniowego 2,1.</span><span class="sxs-lookup"><span data-stu-id="816fd-198">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="816fd-199">Buforowanie możliwości</span><span class="sxs-lookup"><span data-stu-id="816fd-199">Capabilities caching</span></span>

<span data-ttu-id="816fd-200">Weryfikacja zabezpieczeń i Tworzenie wystąpień wtyczek jest kosztowne.</span><span class="sxs-lookup"><span data-stu-id="816fd-200">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="816fd-201">Operacja pobierania odbywa się częściej niż operacja uwierzytelniania, jednak średni użytkownik programu NuGet może mieć tylko wtyczkę uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="816fd-201">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="816fd-202">Aby ulepszyć środowisko, pakiet NuGet będzie buforować oświadczenia operacji dla danego żądania.</span><span class="sxs-lookup"><span data-stu-id="816fd-202">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="816fd-203">Ta pamięć podręczna jest na wtyczkę z kluczem wtyczki w ścieżce wtyczki, a okres ważności tej pamięci podręcznej to 30 dni.</span><span class="sxs-lookup"><span data-stu-id="816fd-203">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="816fd-204">Pamięć podręczna znajduje się w `%LocalAppData%/NuGet/plugins-cache` i przesłonięta ze zmienną środowiskową `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="816fd-204">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="816fd-205">Aby wyczyścić tę [pamięć podręczną](../../consume-packages/managing-the-global-packages-and-cache-folders.md), jeden może uruchomić polecenie Locals z opcją `plugins-cache`.</span><span class="sxs-lookup"><span data-stu-id="816fd-205">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="816fd-206">Opcja wartości lokalnych `all` spowoduje teraz również usunięcie pamięci podręcznej dodatków.</span><span class="sxs-lookup"><span data-stu-id="816fd-206">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="816fd-207">Indeks komunikatów protokołu</span><span class="sxs-lookup"><span data-stu-id="816fd-207">Protocol messages index</span></span>

<span data-ttu-id="816fd-208">Komunikaty o wersji protokołu *1.0.0* :</span><span class="sxs-lookup"><span data-stu-id="816fd-208">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="816fd-209">Zamknięcie</span><span class="sxs-lookup"><span data-stu-id="816fd-209">Close</span></span>
    * <span data-ttu-id="816fd-210">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-210">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="816fd-211">Żądanie nie będzie zawierać ładunku</span><span class="sxs-lookup"><span data-stu-id="816fd-211">The request will contain no payload</span></span>
    * <span data-ttu-id="816fd-212">Nie oczekiwano odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="816fd-212">No response is expected.</span></span>  <span data-ttu-id="816fd-213">Właściwa odpowiedź dotyczy procesu wtyczki, aby zakończyć pracę.</span><span class="sxs-lookup"><span data-stu-id="816fd-213">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="816fd-214">Kopiuj pliki w pakiecie</span><span class="sxs-lookup"><span data-stu-id="816fd-214">Copy files in package</span></span>
    * <span data-ttu-id="816fd-215">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-215">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="816fd-216">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-216">The request will contain:</span></span>
        * <span data-ttu-id="816fd-217">Identyfikator i wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-217">the package ID and version</span></span>
        * <span data-ttu-id="816fd-218">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-218">the package source repository location</span></span>
        * <span data-ttu-id="816fd-219">ścieżka katalogu docelowego</span><span class="sxs-lookup"><span data-stu-id="816fd-219">destination directory path</span></span>
        * <span data-ttu-id="816fd-220">wyliczalne pliki w pakiecie do skopiowania do ścieżki katalogu docelowego</span><span class="sxs-lookup"><span data-stu-id="816fd-220">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="816fd-221">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-221">A response will contain:</span></span>
        * <span data-ttu-id="816fd-222">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-222">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="816fd-223">wyliczalne pełne ścieżki dla skopiowanych plików w katalogu docelowym, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="816fd-223">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="816fd-224">Kopiuj plik pakietu (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="816fd-224">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="816fd-225">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-225">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="816fd-226">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-226">The request will contain:</span></span>
        * <span data-ttu-id="816fd-227">Identyfikator i wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-227">the package ID and version</span></span>
        * <span data-ttu-id="816fd-228">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-228">the package source repository location</span></span>
        * <span data-ttu-id="816fd-229">ścieżka pliku docelowego</span><span class="sxs-lookup"><span data-stu-id="816fd-229">the destination file path</span></span>
    * <span data-ttu-id="816fd-230">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-230">A response will contain:</span></span>
        * <span data-ttu-id="816fd-231">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-231">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="816fd-232">Pobierz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="816fd-232">Get credentials</span></span>
    * <span data-ttu-id="816fd-233">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-233">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="816fd-234">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-234">The request will contain:</span></span>
        * <span data-ttu-id="816fd-235">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-235">the package source repository location</span></span>
        * <span data-ttu-id="816fd-236">kod stanu HTTP uzyskany z repozytorium źródłowego pakietu przy użyciu bieżących poświadczeń</span><span class="sxs-lookup"><span data-stu-id="816fd-236">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="816fd-237">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-237">A response will contain:</span></span>
        * <span data-ttu-id="816fd-238">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="816fd-239">Nazwa użytkownika, jeśli jest dostępna</span><span class="sxs-lookup"><span data-stu-id="816fd-239">a username, if available</span></span>
        * <span data-ttu-id="816fd-240">hasło, jeśli jest dostępne</span><span class="sxs-lookup"><span data-stu-id="816fd-240">a password, if available</span></span>

5.  <span data-ttu-id="816fd-241">Pobierz pliki w pakiecie</span><span class="sxs-lookup"><span data-stu-id="816fd-241">Get files in package</span></span>
    * <span data-ttu-id="816fd-242">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-242">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="816fd-243">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-243">The request will contain:</span></span>
        * <span data-ttu-id="816fd-244">Identyfikator i wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-244">the package ID and version</span></span>
        * <span data-ttu-id="816fd-245">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-245">the package source repository location</span></span>
    * <span data-ttu-id="816fd-246">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-246">A response will contain:</span></span>
        * <span data-ttu-id="816fd-247">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-247">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="816fd-248">wyliczalne ścieżki plików w pakiecie, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="816fd-248">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="816fd-249">Pobierz oświadczenia operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-249">Get operation claims</span></span> 
    * <span data-ttu-id="816fd-250">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-250">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="816fd-251">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-251">The request will contain:</span></span>
        * <span data-ttu-id="816fd-252">Usługa index. JSON dla źródła pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-252">the service index.json for a package source</span></span>
        * <span data-ttu-id="816fd-253">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-253">the package source repository location</span></span>
    * <span data-ttu-id="816fd-254">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-254">A response will contain:</span></span>
        * <span data-ttu-id="816fd-255">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-255">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="816fd-256">wyliczalne obsługiwane operacje (np.: Pobieranie pakietu), jeśli operacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="816fd-256">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="816fd-257">Jeśli wtyczka nie obsługuje źródła pakietu, wtyczka musi zwrócić pusty zestaw obsługiwanych operacji.</span><span class="sxs-lookup"><span data-stu-id="816fd-257">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="816fd-258">Ten komunikat został zaktualizowany w wersji *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="816fd-258">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="816fd-259">Klient zachowuje zgodność z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="816fd-259">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="816fd-260">Pobierz skrót pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-260">Get package hash</span></span>
    * <span data-ttu-id="816fd-261">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="816fd-262">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-262">The request will contain:</span></span>
        * <span data-ttu-id="816fd-263">Identyfikator i wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-263">the package ID and version</span></span>
        * <span data-ttu-id="816fd-264">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-264">the package source repository location</span></span>
        * <span data-ttu-id="816fd-265">algorytm wyznaczania wartości skrótu</span><span class="sxs-lookup"><span data-stu-id="816fd-265">the hash algorithm</span></span>
    * <span data-ttu-id="816fd-266">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-266">A response will contain:</span></span>
        * <span data-ttu-id="816fd-267">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-267">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="816fd-268">skrót pliku pakietu przy użyciu żądanego algorytmu wyznaczania wartości skrótu, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="816fd-268">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="816fd-269">Pobierz wersje pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-269">Get package versions</span></span>
    * <span data-ttu-id="816fd-270">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-270">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="816fd-271">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-271">The request will contain:</span></span>
        * <span data-ttu-id="816fd-272">Identyfikator pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-272">the package ID</span></span>
        * <span data-ttu-id="816fd-273">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-273">the package source repository location</span></span>
    * <span data-ttu-id="816fd-274">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-274">A response will contain:</span></span>
        * <span data-ttu-id="816fd-275">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-275">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="816fd-276">wyliczalne wersje pakietów, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="816fd-276">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="816fd-277">Pobierz indeks usługi</span><span class="sxs-lookup"><span data-stu-id="816fd-277">Get service index</span></span>
    * <span data-ttu-id="816fd-278">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-278">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="816fd-279">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-279">The request will contain:</span></span>
        * <span data-ttu-id="816fd-280">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-280">the package source repository location</span></span>
    * <span data-ttu-id="816fd-281">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-281">A response will contain:</span></span>
        * <span data-ttu-id="816fd-282">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-282">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="816fd-283">indeks usługi, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="816fd-283">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="816fd-284">Uzgadniania</span><span class="sxs-lookup"><span data-stu-id="816fd-284">Handshake</span></span>
     * <span data-ttu-id="816fd-285">Kierunek żądania: < NuGet — wtyczka ></span><span class="sxs-lookup"><span data-stu-id="816fd-285">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="816fd-286">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-286">The request will contain:</span></span>
         * <span data-ttu-id="816fd-287">Bieżąca wersja protokołu wtyczki</span><span class="sxs-lookup"><span data-stu-id="816fd-287">the current plugin protocol version</span></span>
         * <span data-ttu-id="816fd-288">Minimalna obsługiwana wersja protokołu wtyczki</span><span class="sxs-lookup"><span data-stu-id="816fd-288">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="816fd-289">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-289">A response will contain:</span></span>
         * <span data-ttu-id="816fd-290">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-290">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="816fd-291">wynegocjowana wersja protokołu, jeśli operacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="816fd-291">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="816fd-292">Niepowodzenie spowoduje zakończenie wtyczki.</span><span class="sxs-lookup"><span data-stu-id="816fd-292">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="816fd-293">Initialize</span><span class="sxs-lookup"><span data-stu-id="816fd-293">Initialize</span></span>
     * <span data-ttu-id="816fd-294">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-294">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="816fd-295">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-295">The request will contain:</span></span>
         * <span data-ttu-id="816fd-296">wersja narzędzia klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-296">the NuGet client tool version</span></span>
         * <span data-ttu-id="816fd-297">efektywny język narzędzia klienckiego NuGet.</span><span class="sxs-lookup"><span data-stu-id="816fd-297">the NuGet client tool effective language.</span></span>  <span data-ttu-id="816fd-298">Uwzględnia to ustawienie ForceEnglishOutput, jeśli jest używane.</span><span class="sxs-lookup"><span data-stu-id="816fd-298">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="816fd-299">domyślny limit czasu żądania, który zastępuje domyślny protokół.</span><span class="sxs-lookup"><span data-stu-id="816fd-299">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="816fd-300">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-300">A response will contain:</span></span>
         * <span data-ttu-id="816fd-301">kod odpowiedzi wskazujący wynik operacji.</span><span class="sxs-lookup"><span data-stu-id="816fd-301">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="816fd-302">Niepowodzenie spowoduje zakończenie wtyczki.</span><span class="sxs-lookup"><span data-stu-id="816fd-302">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="816fd-303">rejestrowane</span><span class="sxs-lookup"><span data-stu-id="816fd-303">Log</span></span>
     * <span data-ttu-id="816fd-304">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-304">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="816fd-305">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-305">The request will contain:</span></span>
         * <span data-ttu-id="816fd-306">poziom rejestrowania żądania</span><span class="sxs-lookup"><span data-stu-id="816fd-306">the log level for the request</span></span>
         * <span data-ttu-id="816fd-307">komunikat do zarejestrowania</span><span class="sxs-lookup"><span data-stu-id="816fd-307">a message to log</span></span>
     * <span data-ttu-id="816fd-308">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-308">A response will contain:</span></span>
         * <span data-ttu-id="816fd-309">kod odpowiedzi wskazujący wynik operacji.</span><span class="sxs-lookup"><span data-stu-id="816fd-309">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="816fd-310">Wyjdź z monitorowania procesu NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-310">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="816fd-311">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-311">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="816fd-312">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-312">The request will contain:</span></span>
         * <span data-ttu-id="816fd-313">Identyfikator procesu NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-313">the NuGet process ID</span></span>
     * <span data-ttu-id="816fd-314">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-314">A response will contain:</span></span>
         * <span data-ttu-id="816fd-315">kod odpowiedzi wskazujący wynik operacji.</span><span class="sxs-lookup"><span data-stu-id="816fd-315">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="816fd-316">Pakiet pobierania z wyprzedzeniem</span><span class="sxs-lookup"><span data-stu-id="816fd-316">Prefetch package</span></span>
     * <span data-ttu-id="816fd-317">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-317">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="816fd-318">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-318">The request will contain:</span></span>
         * <span data-ttu-id="816fd-319">Identyfikator i wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-319">the package ID and version</span></span>
         * <span data-ttu-id="816fd-320">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-320">the package source repository location</span></span>
     * <span data-ttu-id="816fd-321">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-321">A response will contain:</span></span>
         * <span data-ttu-id="816fd-322">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-322">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="816fd-323">Ustaw poświadczenia</span><span class="sxs-lookup"><span data-stu-id="816fd-323">Set credentials</span></span>
     * <span data-ttu-id="816fd-324">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-324">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="816fd-325">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-325">The request will contain:</span></span>
         * <span data-ttu-id="816fd-326">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-326">the package source repository location</span></span>
         * <span data-ttu-id="816fd-327">Ostatnia znana nazwa użytkownika źródła pakietu, jeśli jest dostępna</span><span class="sxs-lookup"><span data-stu-id="816fd-327">the last known package source username, if available</span></span>
         * <span data-ttu-id="816fd-328">ostatnie znane hasło źródłowe pakietu, jeśli jest dostępne</span><span class="sxs-lookup"><span data-stu-id="816fd-328">the last known package source password, if available</span></span>
         * <span data-ttu-id="816fd-329">Ostatnia znana nazwa użytkownika serwera proxy, jeśli jest dostępna</span><span class="sxs-lookup"><span data-stu-id="816fd-329">the last known proxy username, if available</span></span>
         * <span data-ttu-id="816fd-330">ostatnie znane hasło serwera proxy, jeśli jest dostępne</span><span class="sxs-lookup"><span data-stu-id="816fd-330">the last known proxy password, if available</span></span>
     * <span data-ttu-id="816fd-331">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-331">A response will contain:</span></span>
         * <span data-ttu-id="816fd-332">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-332">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="816fd-333">Ustawianie poziomu dziennika</span><span class="sxs-lookup"><span data-stu-id="816fd-333">Set log level</span></span>
     * <span data-ttu-id="816fd-334">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-334">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="816fd-335">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-335">The request will contain:</span></span>
         * <span data-ttu-id="816fd-336">domyślny poziom dziennika</span><span class="sxs-lookup"><span data-stu-id="816fd-336">the default log level</span></span>
     * <span data-ttu-id="816fd-337">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-337">A response will contain:</span></span>
         * <span data-ttu-id="816fd-338">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-338">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="816fd-339">Komunikaty *2.0.0* w wersji protokołu</span><span class="sxs-lookup"><span data-stu-id="816fd-339">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="816fd-340">Pobierz oświadczenia operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-340">Get Operation Claims</span></span>

* <span data-ttu-id="816fd-341">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-341">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="816fd-342">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-342">The request will contain:</span></span>
        * <span data-ttu-id="816fd-343">Usługa index. JSON dla źródła pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-343">the service index.json for a package source</span></span>
        * <span data-ttu-id="816fd-344">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="816fd-344">the package source repository location</span></span>
    * <span data-ttu-id="816fd-345">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-345">A response will contain:</span></span>
        * <span data-ttu-id="816fd-346">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="816fd-346">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="816fd-347">wyliczalne obsługiwane operacje, jeśli operacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="816fd-347">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="816fd-348">Jeśli wtyczka nie obsługuje źródła pakietu, wtyczka musi zwrócić pusty zestaw obsługiwanych operacji.</span><span class="sxs-lookup"><span data-stu-id="816fd-348">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="816fd-349">Jeśli indeks usługi i źródło pakietu mają wartość null, wtyczka może odpowiedzieć na uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="816fd-349">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="816fd-350">Uzyskiwanie poświadczeń uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="816fd-350">Get Authentication Credentials</span></span>

* <span data-ttu-id="816fd-351">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="816fd-351">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="816fd-352">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="816fd-352">The request will contain:</span></span>
    * <span data-ttu-id="816fd-353">adresu</span><span class="sxs-lookup"><span data-stu-id="816fd-353">Uri</span></span>
    * <span data-ttu-id="816fd-354">isretry</span><span class="sxs-lookup"><span data-stu-id="816fd-354">isRetry</span></span>
    * <span data-ttu-id="816fd-355">Nieinteraktywnych</span><span class="sxs-lookup"><span data-stu-id="816fd-355">NonInteractive</span></span>
    * <span data-ttu-id="816fd-356">Zashowdialog</span><span class="sxs-lookup"><span data-stu-id="816fd-356">CanShowDialog</span></span>
* <span data-ttu-id="816fd-357">Odpowiedź będzie zawierać</span><span class="sxs-lookup"><span data-stu-id="816fd-357">A response will contain</span></span>
    * <span data-ttu-id="816fd-358">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="816fd-358">Username</span></span>
    * <span data-ttu-id="816fd-359">Hasło</span><span class="sxs-lookup"><span data-stu-id="816fd-359">Password</span></span>
    * <span data-ttu-id="816fd-360">Komunikat</span><span class="sxs-lookup"><span data-stu-id="816fd-360">Message</span></span>
    * <span data-ttu-id="816fd-361">Lista typów uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="816fd-361">List of Auth Types</span></span>
    * <span data-ttu-id="816fd-362">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="816fd-362">MessageResponseCode</span></span>
