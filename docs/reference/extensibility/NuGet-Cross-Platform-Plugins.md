---
title: Wtyczki Międzyplatformowe NuGet
description: Dodatki Międzyplatformowe NuGet dla NuGet. exe, dotnet. exe, MSBuild. exe i Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 74b80b1791dcb403c90bb3032c009717c11ffe57
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815304"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="82f5e-103">Wtyczki Międzyplatformowe NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="82f5e-104">W NuGet 4.8 + Obsługa wtyczek międzyplatformowych została dodana.</span><span class="sxs-lookup"><span data-stu-id="82f5e-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="82f5e-105">Osiągnięto to przez utworzenie nowego modelu rozszerzalności wtyczki, który musi być zgodny z rygorystycznym zestawem reguł operacji.</span><span class="sxs-lookup"><span data-stu-id="82f5e-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="82f5e-106">Wtyczki to samodzielne pliki wykonywalne (runnables w środowisku .NET Core), które klienci NuGet uruchamiają w osobnym procesie.</span><span class="sxs-lookup"><span data-stu-id="82f5e-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="82f5e-107">Jest to jednokrotne zapis, uruchom wszędzie.</span><span class="sxs-lookup"><span data-stu-id="82f5e-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="82f5e-108">Będzie on działał ze wszystkimi narzędziami klienta NuGet.</span><span class="sxs-lookup"><span data-stu-id="82f5e-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="82f5e-109">Wtyczki mogą być albo .NET Framework (NuGet. exe, MSBuild. exe i Visual Studio) lub .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="82f5e-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="82f5e-110">Jest zdefiniowany protokół komunikacji z wersjami między klientem NuGet a wtyczką.</span><span class="sxs-lookup"><span data-stu-id="82f5e-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="82f5e-111">Podczas uzgadniania uruchamiania, 2 procesy negocjują wersję protokołu.</span><span class="sxs-lookup"><span data-stu-id="82f5e-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="82f5e-112">Aby uwzględnić wszystkie scenariusze narzędzi klienta NuGet, trzeba mieć zarówno .NET Framework, jak i wtyczkę .NET Core.</span><span class="sxs-lookup"><span data-stu-id="82f5e-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="82f5e-113">Poniżej opisano kombinacje klienta/struktury wtyczek.</span><span class="sxs-lookup"><span data-stu-id="82f5e-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="82f5e-114">Narzędzie klienta</span><span class="sxs-lookup"><span data-stu-id="82f5e-114">Client tool</span></span>  | <span data-ttu-id="82f5e-115">Framework</span><span class="sxs-lookup"><span data-stu-id="82f5e-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="82f5e-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="82f5e-116">Visual Studio</span></span> | <span data-ttu-id="82f5e-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="82f5e-117">.NET Framework</span></span> |
| <span data-ttu-id="82f5e-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="82f5e-118">dotnet.exe</span></span> | <span data-ttu-id="82f5e-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="82f5e-119">.NET Core</span></span> |
| <span data-ttu-id="82f5e-120">NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="82f5e-120">NuGet.exe</span></span> | <span data-ttu-id="82f5e-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="82f5e-121">.NET Framework</span></span> |
| <span data-ttu-id="82f5e-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="82f5e-122">MSBuild.exe</span></span> | <span data-ttu-id="82f5e-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="82f5e-123">.NET Framework</span></span> |
| <span data-ttu-id="82f5e-124">NuGet. exe na mono</span><span class="sxs-lookup"><span data-stu-id="82f5e-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="82f5e-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="82f5e-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="82f5e-126">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="82f5e-126">How does it work</span></span>

<span data-ttu-id="82f5e-127">Przepływ pracy wysokiego poziomu można opisać w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="82f5e-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="82f5e-128">Pakiet NuGet odnajduje dostępne wtyczki.</span><span class="sxs-lookup"><span data-stu-id="82f5e-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="82f5e-129">Jeśli ma to zastosowanie, pakiet NuGet przejdzie iterację na wtyczkach w kolejności priorytetu i uruchomi je po jednym.</span><span class="sxs-lookup"><span data-stu-id="82f5e-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="82f5e-130">Pakiet NuGet użyje pierwszej wtyczki, która może obsłużyć żądanie.</span><span class="sxs-lookup"><span data-stu-id="82f5e-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="82f5e-131">Wtyczki zostaną wyłączone, gdy nie będą już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="82f5e-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="82f5e-132">Ogólne wymagania wtyczki</span><span class="sxs-lookup"><span data-stu-id="82f5e-132">General plugin requirements</span></span>

<span data-ttu-id="82f5e-133">Bieżąca wersja protokołu to *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="82f5e-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="82f5e-134">W tej wersji wymagania są następujące:</span><span class="sxs-lookup"><span data-stu-id="82f5e-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="82f5e-135">Mają prawidłowy zestaw zaufanych podpisów Authenticode, które będą uruchamiane w systemie Windows i mono.</span><span class="sxs-lookup"><span data-stu-id="82f5e-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="82f5e-136">Nie ma jeszcze specjalnych wymagań zaufania dla zestawów uruchomionych w systemach Linux i Mac.</span><span class="sxs-lookup"><span data-stu-id="82f5e-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="82f5e-137">Istotny problem</span><span class="sxs-lookup"><span data-stu-id="82f5e-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="82f5e-138">Obsługa bezstanowego uruchamiania w ramach bieżącego kontekstu zabezpieczeń narzędzi klienckich programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="82f5e-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="82f5e-139">Na przykład narzędzia klienta NuGet nie będą wykonywały podniesienia uprawnień ani dodatkowego inicjowania poza protokołem wtyczki opisanym w dalszej części.</span><span class="sxs-lookup"><span data-stu-id="82f5e-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="82f5e-140">Nie jest interaktywny, chyba że zostanie jawnie określony.</span><span class="sxs-lookup"><span data-stu-id="82f5e-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="82f5e-141">Zgodność z wynegocjowaną wersją protokołu wtyczki.</span><span class="sxs-lookup"><span data-stu-id="82f5e-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="82f5e-142">Odpowiadanie na wszystkie żądania w rozsądnym czasie.</span><span class="sxs-lookup"><span data-stu-id="82f5e-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="82f5e-143">Honorować żądania anulowania dla każdej operacji w toku.</span><span class="sxs-lookup"><span data-stu-id="82f5e-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="82f5e-144">Specyfikacja techniczna została szczegółowo opisana w następujących kwestiach:</span><span class="sxs-lookup"><span data-stu-id="82f5e-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="82f5e-145">Wtyczka pobierania pakietu NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="82f5e-146">Wtyczka do uwierzytelniania między płytkami NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="82f5e-147">Interakcja klienta — wtyczka</span><span class="sxs-lookup"><span data-stu-id="82f5e-147">Client - Plugin interaction</span></span>

<span data-ttu-id="82f5e-148">Narzędzia klienta i wtyczki programu NuGet komunikują się z notacją JSON przez strumienie standardowe (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="82f5e-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="82f5e-149">Wszystkie dane muszą być kodowane w formacie UTF-8.</span><span class="sxs-lookup"><span data-stu-id="82f5e-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="82f5e-150">Wtyczki są uruchamiane z argumentem "-plugin".</span><span class="sxs-lookup"><span data-stu-id="82f5e-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="82f5e-151">W przypadku, gdy użytkownik bezpośrednio uruchamia plik wykonywalny wtyczki bez tego argumentu, wtyczka może dać komunikat informacyjny, a nie oczekuje na uzgadnianie protokołu.</span><span class="sxs-lookup"><span data-stu-id="82f5e-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="82f5e-152">Limit czasu uzgadniania protokołu wynosi 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="82f5e-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="82f5e-153">Wtyczka powinna zakończyć instalację tak jak najkrótszej ilości, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="82f5e-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="82f5e-154">Narzędzia klienta NuGet będą badać obsługiwane operacje wtyczki, przekazując indeks usługi dla źródła NuGet.</span><span class="sxs-lookup"><span data-stu-id="82f5e-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="82f5e-155">Wtyczka może użyć indeksu usługi, aby sprawdzić obecność obsługiwanych typów usług.</span><span class="sxs-lookup"><span data-stu-id="82f5e-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="82f5e-156">Komunikacja między narzędziami klienta NuGet a wtyczką jest dwukierunkowa.</span><span class="sxs-lookup"><span data-stu-id="82f5e-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="82f5e-157">Każde żądanie ma limit czasu wynoszący 5 sekund.</span><span class="sxs-lookup"><span data-stu-id="82f5e-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="82f5e-158">Jeśli operacje mają trwać dłużej, proces powinien wysłać komunikat o postępie, aby zapobiec przekroczeniu limitu czasu żądania. Po 1 minucie braku aktywności wtyczka jest uważana za bezczynną i jest zamykana.</span><span class="sxs-lookup"><span data-stu-id="82f5e-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="82f5e-159">Instalowanie i odnajdywanie wtyczki</span><span class="sxs-lookup"><span data-stu-id="82f5e-159">Plugin installation and discovery</span></span>

<span data-ttu-id="82f5e-160">Wtyczki zostaną odnalezione za pośrednictwem struktury katalogów na podstawie Konwencji.</span><span class="sxs-lookup"><span data-stu-id="82f5e-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="82f5e-161">Scenariusze ciągłej integracji/ciągłego wdrażania i Użytkownicy zaawansowani mogą używać zmiennych środowiskowych, aby przesłonić zachowanie.</span><span class="sxs-lookup"><span data-stu-id="82f5e-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="82f5e-162">Należy pamiętać `NUGET_NETFX_PLUGIN_PATHS` , `NUGET_NETCORE_PLUGIN_PATHS` że i są dostępne tylko w przypadku używania 5.3 + wersji narzędzi NuGet i nowszych.</span><span class="sxs-lookup"><span data-stu-id="82f5e-162">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="82f5e-163">`NUGET_NETFX_PLUGIN_PATHS`-definiuje wtyczki, które będą używane przez narzędzia oparte na .NET Framework (NuGet. exe/MSBuild. exe/Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="82f5e-163">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="82f5e-164">Ma pierwszeństwo `NUGET_PLUGIN_PATHS`przed.</span><span class="sxs-lookup"><span data-stu-id="82f5e-164">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="82f5e-165">(Tylko wersja 5.3 programu NuGet)</span><span class="sxs-lookup"><span data-stu-id="82f5e-165">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="82f5e-166">`NUGET_NETCORE_PLUGIN_PATHS`-definiuje wtyczki, które będą używane przez narzędzia oparte na oprogramowaniu .NET Core (dotnet. exe).</span><span class="sxs-lookup"><span data-stu-id="82f5e-166">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="82f5e-167">Ma pierwszeństwo `NUGET_PLUGIN_PATHS`przed.</span><span class="sxs-lookup"><span data-stu-id="82f5e-167">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="82f5e-168">(Tylko wersja 5.3 programu NuGet)</span><span class="sxs-lookup"><span data-stu-id="82f5e-168">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="82f5e-169">`NUGET_PLUGIN_PATHS`-definiuje wtyczki, które będą używane dla tego procesu NuGet, czyli priorytet zarezerwowane.</span><span class="sxs-lookup"><span data-stu-id="82f5e-169">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="82f5e-170">Jeśli ta zmienna środowiskowa jest ustawiona, zastępuje ona metodę odnajdywania opartą na Konwencji.</span><span class="sxs-lookup"><span data-stu-id="82f5e-170">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="82f5e-171">Ignorowany, jeśli określono jedną z zmiennych określonych dla struktury.</span><span class="sxs-lookup"><span data-stu-id="82f5e-171">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="82f5e-172">Lokalizacja użytkownika, lokalizacja główna narzędzia NuGet w programie `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="82f5e-172">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="82f5e-173">Ta lokalizacja nie może być przesłonięta.</span><span class="sxs-lookup"><span data-stu-id="82f5e-173">This location cannot be overriden.</span></span> <span data-ttu-id="82f5e-174">Dla wtyczek platformy .NET Core i .NET Framework zostanie użyty inny katalog główny.</span><span class="sxs-lookup"><span data-stu-id="82f5e-174">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="82f5e-175">Framework</span><span class="sxs-lookup"><span data-stu-id="82f5e-175">Framework</span></span> | <span data-ttu-id="82f5e-176">Główna lokalizacja odnajdowania</span><span class="sxs-lookup"><span data-stu-id="82f5e-176">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="82f5e-177">.NET Core</span><span class="sxs-lookup"><span data-stu-id="82f5e-177">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="82f5e-178">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="82f5e-178">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="82f5e-179">Każda wtyczka powinna być zainstalowana we własnym folderze.</span><span class="sxs-lookup"><span data-stu-id="82f5e-179">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="82f5e-180">Punkt wejścia wtyczki będzie nazwą zainstalowanego folderu z rozszerzeniami dll dla programu .NET Core i rozszerzeniem exe dla .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="82f5e-180">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="82f5e-181">Obecnie nie ma żadnego scenariusza użytkownika dla instalacji wtyczek.</span><span class="sxs-lookup"><span data-stu-id="82f5e-181">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="82f5e-182">Jest to proste przeniesienie wymaganych plików do wstępnie wskazanej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="82f5e-182">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="82f5e-183">Obsługiwane operacje</span><span class="sxs-lookup"><span data-stu-id="82f5e-183">Supported operations</span></span>

<span data-ttu-id="82f5e-184">W ramach nowego protokołu wtyczki są obsługiwane dwie operacje.</span><span class="sxs-lookup"><span data-stu-id="82f5e-184">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="82f5e-185">Nazwa operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-185">Operation name</span></span> | <span data-ttu-id="82f5e-186">Minimalna wersja protokołu</span><span class="sxs-lookup"><span data-stu-id="82f5e-186">Minimum protocol version</span></span> | <span data-ttu-id="82f5e-187">Minimalna wersja klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-187">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="82f5e-188">Pobierz pakiet</span><span class="sxs-lookup"><span data-stu-id="82f5e-188">Download Package</span></span> | <span data-ttu-id="82f5e-189">1.0.0</span><span class="sxs-lookup"><span data-stu-id="82f5e-189">1.0.0</span></span> | <span data-ttu-id="82f5e-190">4.3.0</span><span class="sxs-lookup"><span data-stu-id="82f5e-190">4.3.0</span></span> |
| [<span data-ttu-id="82f5e-191">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="82f5e-191">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="82f5e-192">2.0.0</span><span class="sxs-lookup"><span data-stu-id="82f5e-192">2.0.0</span></span> | <span data-ttu-id="82f5e-193">4.8.0</span><span class="sxs-lookup"><span data-stu-id="82f5e-193">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="82f5e-194">Uruchamianie wtyczek w prawidłowym środowisku uruchomieniowym</span><span class="sxs-lookup"><span data-stu-id="82f5e-194">Running plugins under the correct runtime</span></span>

<span data-ttu-id="82f5e-195">W przypadku pakietu NuGet w scenariuszach programu dotnet. exe wtyczki muszą być w stanie wykonać w tym konkretnym czasie wykonywania programu dotnet. exe.</span><span class="sxs-lookup"><span data-stu-id="82f5e-195">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="82f5e-196">Jest on dostawcą wtyczki i konsumentem, aby upewnić się, że jest używana kombinacja dotnet. exe/wtyczka.</span><span class="sxs-lookup"><span data-stu-id="82f5e-196">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="82f5e-197">Potencjalny problem może wystąpić w przypadku wtyczek do lokalizacji użytkownika, gdy na przykład program dotnet. exe w środowisku uruchomieniowym 2,0 próbuje użyć wtyczki zarejestrowanej dla środowiska uruchomieniowego 2,1.</span><span class="sxs-lookup"><span data-stu-id="82f5e-197">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="82f5e-198">Buforowanie możliwości</span><span class="sxs-lookup"><span data-stu-id="82f5e-198">Capabilities caching</span></span>

<span data-ttu-id="82f5e-199">Weryfikacja zabezpieczeń i Tworzenie wystąpień wtyczek jest kosztowne.</span><span class="sxs-lookup"><span data-stu-id="82f5e-199">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="82f5e-200">Operacja pobierania odbywa się częściej niż operacja uwierzytelniania, jednak średni użytkownik programu NuGet może mieć tylko wtyczkę uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="82f5e-200">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="82f5e-201">Aby ulepszyć środowisko, pakiet NuGet będzie buforować oświadczenia operacji dla danego żądania.</span><span class="sxs-lookup"><span data-stu-id="82f5e-201">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="82f5e-202">Ta pamięć podręczna jest na wtyczkę z kluczem wtyczki w ścieżce wtyczki, a okres ważności tej pamięci podręcznej to 30 dni.</span><span class="sxs-lookup"><span data-stu-id="82f5e-202">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="82f5e-203">Pamięć podręczna znajduje się `%LocalAppData%/NuGet/plugins-cache` w i przesłonięta ze zmienną `NUGET_PLUGINS_CACHE_PATH`środowiskową.</span><span class="sxs-lookup"><span data-stu-id="82f5e-203">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="82f5e-204">Aby wyczyścić tę [pamięć podręczną](../../consume-packages/managing-the-global-packages-and-cache-folders.md), jeden może uruchomić polecenie Locals z `plugins-cache` opcją.</span><span class="sxs-lookup"><span data-stu-id="82f5e-204">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="82f5e-205">Opcja `all` ustawienia lokalne spowoduje teraz również usunięcie pamięci podręcznej dodatków.</span><span class="sxs-lookup"><span data-stu-id="82f5e-205">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="82f5e-206">Indeks komunikatów protokołu</span><span class="sxs-lookup"><span data-stu-id="82f5e-206">Protocol messages index</span></span>

<span data-ttu-id="82f5e-207">Komunikaty o wersji protokołu *1.0.0* :</span><span class="sxs-lookup"><span data-stu-id="82f5e-207">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="82f5e-208">Zamknięcie</span><span class="sxs-lookup"><span data-stu-id="82f5e-208">Close</span></span>
    * <span data-ttu-id="82f5e-209">Kierunek żądania:  Wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-209">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="82f5e-210">Żądanie nie będzie zawierać ładunku</span><span class="sxs-lookup"><span data-stu-id="82f5e-210">The request will contain no payload</span></span>
    * <span data-ttu-id="82f5e-211">Nie oczekiwano odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="82f5e-211">No response is expected.</span></span>  <span data-ttu-id="82f5e-212">Właściwa odpowiedź dotyczy procesu wtyczki, aby zakończyć pracę.</span><span class="sxs-lookup"><span data-stu-id="82f5e-212">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="82f5e-213">Kopiuj pliki w pakiecie</span><span class="sxs-lookup"><span data-stu-id="82f5e-213">Copy files in package</span></span>
    * <span data-ttu-id="82f5e-214">Kierunek żądania:  Wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-214">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="82f5e-215">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-215">The request will contain:</span></span>
        * <span data-ttu-id="82f5e-216">Identyfikator i wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-216">the package ID and version</span></span>
        * <span data-ttu-id="82f5e-217">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-217">the package source repository location</span></span>
        * <span data-ttu-id="82f5e-218">ścieżka katalogu docelowego</span><span class="sxs-lookup"><span data-stu-id="82f5e-218">destination directory path</span></span>
        * <span data-ttu-id="82f5e-219">wyliczalne pliki w pakiecie do skopiowania do ścieżki katalogu docelowego</span><span class="sxs-lookup"><span data-stu-id="82f5e-219">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="82f5e-220">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-220">A response will contain:</span></span>
        * <span data-ttu-id="82f5e-221">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-221">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="82f5e-222">wyliczalne pełne ścieżki dla skopiowanych plików w katalogu docelowym, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="82f5e-222">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="82f5e-223">Kopiuj plik pakietu (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="82f5e-223">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="82f5e-224">Kierunek żądania:  Wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-224">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="82f5e-225">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-225">The request will contain:</span></span>
        * <span data-ttu-id="82f5e-226">Identyfikator i wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-226">the package ID and version</span></span>
        * <span data-ttu-id="82f5e-227">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-227">the package source repository location</span></span>
        * <span data-ttu-id="82f5e-228">ścieżka pliku docelowego</span><span class="sxs-lookup"><span data-stu-id="82f5e-228">the destination file path</span></span>
    * <span data-ttu-id="82f5e-229">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-229">A response will contain:</span></span>
        * <span data-ttu-id="82f5e-230">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-230">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="82f5e-231">Pobierz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="82f5e-231">Get credentials</span></span>
    * <span data-ttu-id="82f5e-232">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-232">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="82f5e-233">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-233">The request will contain:</span></span>
        * <span data-ttu-id="82f5e-234">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-234">the package source repository location</span></span>
        * <span data-ttu-id="82f5e-235">kod stanu HTTP uzyskany z repozytorium źródłowego pakietu przy użyciu bieżących poświadczeń</span><span class="sxs-lookup"><span data-stu-id="82f5e-235">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="82f5e-236">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-236">A response will contain:</span></span>
        * <span data-ttu-id="82f5e-237">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-237">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="82f5e-238">Nazwa użytkownika, jeśli jest dostępna</span><span class="sxs-lookup"><span data-stu-id="82f5e-238">a username, if available</span></span>
        * <span data-ttu-id="82f5e-239">hasło, jeśli jest dostępne</span><span class="sxs-lookup"><span data-stu-id="82f5e-239">a password, if available</span></span>

5.  <span data-ttu-id="82f5e-240">Pobierz pliki w pakiecie</span><span class="sxs-lookup"><span data-stu-id="82f5e-240">Get files in package</span></span>
    * <span data-ttu-id="82f5e-241">Kierunek żądania:  Wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="82f5e-242">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-242">The request will contain:</span></span>
        * <span data-ttu-id="82f5e-243">Identyfikator i wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-243">the package ID and version</span></span>
        * <span data-ttu-id="82f5e-244">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-244">the package source repository location</span></span>
    * <span data-ttu-id="82f5e-245">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-245">A response will contain:</span></span>
        * <span data-ttu-id="82f5e-246">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="82f5e-247">wyliczalne ścieżki plików w pakiecie, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="82f5e-247">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="82f5e-248">Pobierz oświadczenia operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-248">Get operation claims</span></span> 
    * <span data-ttu-id="82f5e-249">Kierunek żądania:  Wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-249">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="82f5e-250">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-250">The request will contain:</span></span>
        * <span data-ttu-id="82f5e-251">Usługa index. JSON dla źródła pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-251">the service index.json for a package source</span></span>
        * <span data-ttu-id="82f5e-252">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-252">the package source repository location</span></span>
    * <span data-ttu-id="82f5e-253">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-253">A response will contain:</span></span>
        * <span data-ttu-id="82f5e-254">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-254">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="82f5e-255">wyliczalne obsługiwane operacje (np.: Pobieranie pakietu), jeśli operacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="82f5e-255">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="82f5e-256">Jeśli wtyczka nie obsługuje źródła pakietu, wtyczka musi zwrócić pusty zestaw obsługiwanych operacji.</span><span class="sxs-lookup"><span data-stu-id="82f5e-256">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="82f5e-257">Ten komunikat został zaktualizowany w wersji *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="82f5e-257">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="82f5e-258">Klient zachowuje zgodność z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="82f5e-258">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="82f5e-259">Pobierz skrót pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-259">Get package hash</span></span>
    * <span data-ttu-id="82f5e-260">Kierunek żądania:  Wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-260">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="82f5e-261">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-261">The request will contain:</span></span>
        * <span data-ttu-id="82f5e-262">Identyfikator i wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-262">the package ID and version</span></span>
        * <span data-ttu-id="82f5e-263">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-263">the package source repository location</span></span>
        * <span data-ttu-id="82f5e-264">algorytm wyznaczania wartości skrótu</span><span class="sxs-lookup"><span data-stu-id="82f5e-264">the hash algorithm</span></span>
    * <span data-ttu-id="82f5e-265">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-265">A response will contain:</span></span>
        * <span data-ttu-id="82f5e-266">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="82f5e-267">skrót pliku pakietu przy użyciu żądanego algorytmu wyznaczania wartości skrótu, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="82f5e-267">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="82f5e-268">Pobierz wersje pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-268">Get package versions</span></span>
    * <span data-ttu-id="82f5e-269">Kierunek żądania:  Wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-269">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="82f5e-270">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-270">The request will contain:</span></span>
        * <span data-ttu-id="82f5e-271">Identyfikator pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-271">the package ID</span></span>
        * <span data-ttu-id="82f5e-272">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-272">the package source repository location</span></span>
    * <span data-ttu-id="82f5e-273">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-273">A response will contain:</span></span>
        * <span data-ttu-id="82f5e-274">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-274">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="82f5e-275">wyliczalne wersje pakietów, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="82f5e-275">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="82f5e-276">Pobierz indeks usługi</span><span class="sxs-lookup"><span data-stu-id="82f5e-276">Get service index</span></span>
    * <span data-ttu-id="82f5e-277">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-277">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="82f5e-278">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-278">The request will contain:</span></span>
        * <span data-ttu-id="82f5e-279">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-279">the package source repository location</span></span>
    * <span data-ttu-id="82f5e-280">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-280">A response will contain:</span></span>
        * <span data-ttu-id="82f5e-281">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-281">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="82f5e-282">indeks usługi, jeśli operacja zakończyła się pomyślnie</span><span class="sxs-lookup"><span data-stu-id="82f5e-282">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="82f5e-283">Uzgadniania</span><span class="sxs-lookup"><span data-stu-id="82f5e-283">Handshake</span></span>
     * <span data-ttu-id="82f5e-284">Kierunek żądania:  < NuGet — wtyczka ></span><span class="sxs-lookup"><span data-stu-id="82f5e-284">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="82f5e-285">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-285">The request will contain:</span></span>
         * <span data-ttu-id="82f5e-286">Bieżąca wersja protokołu wtyczki</span><span class="sxs-lookup"><span data-stu-id="82f5e-286">the current plugin protocol version</span></span>
         * <span data-ttu-id="82f5e-287">Minimalna obsługiwana wersja protokołu wtyczki</span><span class="sxs-lookup"><span data-stu-id="82f5e-287">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="82f5e-288">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-288">A response will contain:</span></span>
         * <span data-ttu-id="82f5e-289">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-289">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="82f5e-290">wynegocjowana wersja protokołu, jeśli operacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="82f5e-290">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="82f5e-291">Niepowodzenie spowoduje zakończenie wtyczki.</span><span class="sxs-lookup"><span data-stu-id="82f5e-291">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="82f5e-292">Initialize</span><span class="sxs-lookup"><span data-stu-id="82f5e-292">Initialize</span></span>
     * <span data-ttu-id="82f5e-293">Kierunek żądania:  Wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-293">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="82f5e-294">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-294">The request will contain:</span></span>
         * <span data-ttu-id="82f5e-295">wersja narzędzia klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-295">the NuGet client tool version</span></span>
         * <span data-ttu-id="82f5e-296">efektywny język narzędzia klienckiego NuGet.</span><span class="sxs-lookup"><span data-stu-id="82f5e-296">the NuGet client tool effective language.</span></span>  <span data-ttu-id="82f5e-297">Uwzględnia to ustawienie ForceEnglishOutput, jeśli jest używane.</span><span class="sxs-lookup"><span data-stu-id="82f5e-297">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="82f5e-298">domyślny limit czasu żądania, który zastępuje domyślny protokół.</span><span class="sxs-lookup"><span data-stu-id="82f5e-298">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="82f5e-299">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-299">A response will contain:</span></span>
         * <span data-ttu-id="82f5e-300">kod odpowiedzi wskazujący wynik operacji.</span><span class="sxs-lookup"><span data-stu-id="82f5e-300">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="82f5e-301">Niepowodzenie spowoduje zakończenie wtyczki.</span><span class="sxs-lookup"><span data-stu-id="82f5e-301">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="82f5e-302">Log</span><span class="sxs-lookup"><span data-stu-id="82f5e-302">Log</span></span>
     * <span data-ttu-id="82f5e-303">Kierunek żądania: wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-303">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="82f5e-304">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-304">The request will contain:</span></span>
         * <span data-ttu-id="82f5e-305">poziom rejestrowania żądania</span><span class="sxs-lookup"><span data-stu-id="82f5e-305">the log level for the request</span></span>
         * <span data-ttu-id="82f5e-306">komunikat do zarejestrowania</span><span class="sxs-lookup"><span data-stu-id="82f5e-306">a message to log</span></span>
     * <span data-ttu-id="82f5e-307">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-307">A response will contain:</span></span>
         * <span data-ttu-id="82f5e-308">kod odpowiedzi wskazujący wynik operacji.</span><span class="sxs-lookup"><span data-stu-id="82f5e-308">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="82f5e-309">Wyjdź z monitorowania procesu NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-309">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="82f5e-310">Kierunek żądania:  Wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-310">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="82f5e-311">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-311">The request will contain:</span></span>
         * <span data-ttu-id="82f5e-312">Identyfikator procesu NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-312">the NuGet process ID</span></span>
     * <span data-ttu-id="82f5e-313">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-313">A response will contain:</span></span>
         * <span data-ttu-id="82f5e-314">kod odpowiedzi wskazujący wynik operacji.</span><span class="sxs-lookup"><span data-stu-id="82f5e-314">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="82f5e-315">Pakiet pobierania z wyprzedzeniem</span><span class="sxs-lookup"><span data-stu-id="82f5e-315">Prefetch package</span></span>
     * <span data-ttu-id="82f5e-316">Kierunek żądania:  Wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-316">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="82f5e-317">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-317">The request will contain:</span></span>
         * <span data-ttu-id="82f5e-318">Identyfikator i wersja pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-318">the package ID and version</span></span>
         * <span data-ttu-id="82f5e-319">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-319">the package source repository location</span></span>
     * <span data-ttu-id="82f5e-320">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-320">A response will contain:</span></span>
         * <span data-ttu-id="82f5e-321">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-321">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="82f5e-322">Ustaw poświadczenia</span><span class="sxs-lookup"><span data-stu-id="82f5e-322">Set credentials</span></span>
     * <span data-ttu-id="82f5e-323">Kierunek żądania:  Wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-323">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="82f5e-324">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-324">The request will contain:</span></span>
         * <span data-ttu-id="82f5e-325">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-325">the package source repository location</span></span>
         * <span data-ttu-id="82f5e-326">Ostatnia znana nazwa użytkownika źródła pakietu, jeśli jest dostępna</span><span class="sxs-lookup"><span data-stu-id="82f5e-326">the last known package source username, if available</span></span>
         * <span data-ttu-id="82f5e-327">ostatnie znane hasło źródłowe pakietu, jeśli jest dostępne</span><span class="sxs-lookup"><span data-stu-id="82f5e-327">the last known package source password, if available</span></span>
         * <span data-ttu-id="82f5e-328">Ostatnia znana nazwa użytkownika serwera proxy, jeśli jest dostępna</span><span class="sxs-lookup"><span data-stu-id="82f5e-328">the last known proxy username, if available</span></span>
         * <span data-ttu-id="82f5e-329">ostatnie znane hasło serwera proxy, jeśli jest dostępne</span><span class="sxs-lookup"><span data-stu-id="82f5e-329">the last known proxy password, if available</span></span>
     * <span data-ttu-id="82f5e-330">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-330">A response will contain:</span></span>
         * <span data-ttu-id="82f5e-331">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-331">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="82f5e-332">Ustawianie poziomu dziennika</span><span class="sxs-lookup"><span data-stu-id="82f5e-332">Set log level</span></span>
     * <span data-ttu-id="82f5e-333">Kierunek żądania:  Wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-333">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="82f5e-334">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-334">The request will contain:</span></span>
         * <span data-ttu-id="82f5e-335">domyślny poziom dziennika</span><span class="sxs-lookup"><span data-stu-id="82f5e-335">the default log level</span></span>
     * <span data-ttu-id="82f5e-336">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-336">A response will contain:</span></span>
         * <span data-ttu-id="82f5e-337">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-337">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="82f5e-338">Komunikaty *2.0.0* w wersji protokołu</span><span class="sxs-lookup"><span data-stu-id="82f5e-338">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="82f5e-339">Pobierz oświadczenia operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-339">Get Operation Claims</span></span>

* <span data-ttu-id="82f5e-340">Kierunek żądania:  Wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-340">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="82f5e-341">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-341">The request will contain:</span></span>
        * <span data-ttu-id="82f5e-342">Usługa index. JSON dla źródła pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-342">the service index.json for a package source</span></span>
        * <span data-ttu-id="82f5e-343">Lokalizacja repozytorium źródłowego pakietu</span><span class="sxs-lookup"><span data-stu-id="82f5e-343">the package source repository location</span></span>
    * <span data-ttu-id="82f5e-344">Odpowiedź będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-344">A response will contain:</span></span>
        * <span data-ttu-id="82f5e-345">kod odpowiedzi wskazujący wynik operacji</span><span class="sxs-lookup"><span data-stu-id="82f5e-345">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="82f5e-346">wyliczalne obsługiwane operacje, jeśli operacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="82f5e-346">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="82f5e-347">Jeśli wtyczka nie obsługuje źródła pakietu, wtyczka musi zwrócić pusty zestaw obsługiwanych operacji.</span><span class="sxs-lookup"><span data-stu-id="82f5e-347">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="82f5e-348">Jeśli indeks usługi i źródło pakietu mają wartość null, wtyczka może odpowiedzieć na uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="82f5e-348">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="82f5e-349">Uzyskiwanie poświadczeń uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="82f5e-349">Get Authentication Credentials</span></span>

* <span data-ttu-id="82f5e-350">Kierunek żądania: Wtyczka > NuGet</span><span class="sxs-lookup"><span data-stu-id="82f5e-350">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="82f5e-351">Żądanie będzie zawierać:</span><span class="sxs-lookup"><span data-stu-id="82f5e-351">The request will contain:</span></span>
    * <span data-ttu-id="82f5e-352">Adresu</span><span class="sxs-lookup"><span data-stu-id="82f5e-352">Uri</span></span>
    * <span data-ttu-id="82f5e-353">isretry</span><span class="sxs-lookup"><span data-stu-id="82f5e-353">isRetry</span></span>
    * <span data-ttu-id="82f5e-354">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="82f5e-354">NonInteractive</span></span>
    * <span data-ttu-id="82f5e-355">Zashowdialog</span><span class="sxs-lookup"><span data-stu-id="82f5e-355">CanShowDialog</span></span>
* <span data-ttu-id="82f5e-356">Odpowiedź będzie zawierać</span><span class="sxs-lookup"><span data-stu-id="82f5e-356">A response will contain</span></span>
    * <span data-ttu-id="82f5e-357">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="82f5e-357">Username</span></span>
    * <span data-ttu-id="82f5e-358">Hasło</span><span class="sxs-lookup"><span data-stu-id="82f5e-358">Password</span></span>
    * <span data-ttu-id="82f5e-359">Message</span><span class="sxs-lookup"><span data-stu-id="82f5e-359">Message</span></span>
    * <span data-ttu-id="82f5e-360">Lista typów uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="82f5e-360">List of Auth Types</span></span>
    * <span data-ttu-id="82f5e-361">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="82f5e-361">MessageResponseCode</span></span>
