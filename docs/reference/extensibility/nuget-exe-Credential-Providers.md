---
title: nuget.exe dostawcy poświadczeń
description: nuget.exe uwierzytelniają się za pomocą kanału informacyjnego i są implementowane jako pliki wykonywalne wiersza polecenia zgodne z określonymi konwencjami.
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 4f0a5a2355b34c39a435d24691a3f8ea10ee9c00
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323833"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="faa6b-103">Uwierzytelnianie źródeł danych za pomocą nuget.exe poświadczeń</span><span class="sxs-lookup"><span data-stu-id="faa6b-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="faa6b-104">W wersji `3.3` dodano obsługę określonych `nuget.exe` dostawców poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="faa6b-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="faa6b-105">Od tego czasu dodano obsługę wersji `4.8` [dostawców poświadczeń,](NuGet-Cross-Platform-Authentication-Plugin.md) którzy działają we wszystkich scenariuszach wiersza polecenia ( `nuget.exe` , , `dotnet.exe` `msbuild.exe` ).</span><span class="sxs-lookup"><span data-stu-id="faa6b-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="faa6b-106">Zobacz [Korzystanie z pakietów z uwierzytelnionych źródeł danych,](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) aby uzyskać więcej informacji na temat wszystkich metod uwierzytelniania dla `nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="faa6b-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="faa6b-107">nuget.exe odnajdywania dostawcy poświadczeń</span><span class="sxs-lookup"><span data-stu-id="faa6b-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="faa6b-108">nuget.exe poświadczeń można używać na 3 sposoby:</span><span class="sxs-lookup"><span data-stu-id="faa6b-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="faa6b-109">**Globalnie:** aby udostępnić dostawcę poświadczeń dla wszystkich wystąpień uruchamiania w profilu bieżącego `nuget.exe` użytkownika, dodaj go do . `%LocalAppData%\NuGet\CredentialProviders`</span><span class="sxs-lookup"><span data-stu-id="faa6b-109">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="faa6b-110">Może być konieczne utworzenie `CredentialProviders` folderu .</span><span class="sxs-lookup"><span data-stu-id="faa6b-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="faa6b-111">Dostawców poświadczeń można zainstalować w katalogu głównym `CredentialProviders`  folderu lub w podfolderze.</span><span class="sxs-lookup"><span data-stu-id="faa6b-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="faa6b-112">Jeśli dostawca poświadczeń ma wiele plików/zestawów, można użyć podfolderów, aby zachować zorganizowaność dostawców.</span><span class="sxs-lookup"><span data-stu-id="faa6b-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="faa6b-113">**Ze zmiennej środowiskowej**: Dostawcy poświadczeń mogą być przechowywani w dowolnym miejscu i dostępni do nich przez ustawienie zmiennej środowiskowej `nuget.exe` na `%NUGET_CREDENTIALPROVIDERS_PATH%` lokalizację dostawcy.</span><span class="sxs-lookup"><span data-stu-id="faa6b-113">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="faa6b-114">Ta zmienna może być listą rozdzieloną średnikami (na przykład `path1;path2` ), jeśli masz wiele lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="faa6b-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="faa6b-115">**Oprócz nuget.exe:** nuget.exe poświadczeń można umieścić w tym samym folderze, w którym znajduje się folder `nuget.exe` .</span><span class="sxs-lookup"><span data-stu-id="faa6b-115">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="faa6b-116">Podczas ładowania dostawców poświadczeń program wyszukuje w powyższych lokalizacjach dowolny plik o nazwie , a następnie ładuje te pliki w kolejności, w których `nuget.exe` `credentialprovider*.exe` zostały znalezione.</span><span class="sxs-lookup"><span data-stu-id="faa6b-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="faa6b-117">Jeśli w tym samym folderze istnieje wielu dostawców poświadczeń, są one ładowane w kolejności alfabetycznej.</span><span class="sxs-lookup"><span data-stu-id="faa6b-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="faa6b-118">Tworzenie dostawcy nuget.exe poświadczeń</span><span class="sxs-lookup"><span data-stu-id="faa6b-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="faa6b-119">Dostawca poświadczeń to plik wykonywalny wiersza polecenia o nazwie w postaci , który zbiera dane wejściowe, uzyskuje odpowiednie poświadczenia, a następnie zwraca odpowiedni kod stanu zakończenia i standardowe `CredentialProvider*.exe` dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="faa6b-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="faa6b-120">Dostawca musi wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="faa6b-120">A provider must do the following:</span></span>

- <span data-ttu-id="faa6b-121">Określ, czy można podać poświadczenia dla docelowego URI przed zainicjowanie pozyskiwania poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="faa6b-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="faa6b-122">Jeśli nie, powinien zostać zwrócony kod stanu 1 bez poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="faa6b-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="faa6b-123">Nie modyfikuj (na przykład w tym miejscu `NuGet.Config` ustawiaj poświadczenia).</span><span class="sxs-lookup"><span data-stu-id="faa6b-123">Not modify `NuGet.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="faa6b-124">Samodzielnie obsługuj konfigurację serwera proxy HTTP, ponieważ nuGet nie dostarcza informacji o serwerze proxy do wtyczki.</span><span class="sxs-lookup"><span data-stu-id="faa6b-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="faa6b-125">Zwróć poświadczenia lub szczegóły błędu do obiektu , zapisując obiekt odpowiedzi JSON (patrz poniżej) w obiekcie `nuget.exe` stdout przy użyciu kodowania UTF-8.</span><span class="sxs-lookup"><span data-stu-id="faa6b-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="faa6b-126">Opcjonalnie emituj dodatkowe rejestrowanie śledzenia do stderr.</span><span class="sxs-lookup"><span data-stu-id="faa6b-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="faa6b-127">Nie należy kiedykolwiek zapisywać wpisów tajnych w programie stderr, ponieważ na poziomie szczegółowości "normalne" lub "szczegółowe" takie ślady są powtarzane w konsoli przez program NuGet.</span><span class="sxs-lookup"><span data-stu-id="faa6b-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="faa6b-128">Nieoczekiwane parametry powinny być ignorowane, zapewniając zgodność z przyszłymi wersjami pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="faa6b-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="faa6b-129">Parametry wejściowe</span><span class="sxs-lookup"><span data-stu-id="faa6b-129">Input parameters</span></span>

| <span data-ttu-id="faa6b-130">Parametr/przełącznik</span><span class="sxs-lookup"><span data-stu-id="faa6b-130">Parameter/Switch</span></span> |<span data-ttu-id="faa6b-131">Opis</span><span class="sxs-lookup"><span data-stu-id="faa6b-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="faa6b-132">Identyfikator URI {value}</span><span class="sxs-lookup"><span data-stu-id="faa6b-132">Uri {value}</span></span> | <span data-ttu-id="faa6b-133">Źródłowy kod URI pakietu wymagający poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="faa6b-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="faa6b-134">Nieinteraktywnych</span><span class="sxs-lookup"><span data-stu-id="faa6b-134">NonInteractive</span></span> | <span data-ttu-id="faa6b-135">Jeśli jest obecny, dostawca nie wyświetla monitów interakcyjnych.</span><span class="sxs-lookup"><span data-stu-id="faa6b-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="faa6b-136">IsRetry</span><span class="sxs-lookup"><span data-stu-id="faa6b-136">IsRetry</span></span> | <span data-ttu-id="faa6b-137">Jeśli istnieje, wskazuje, że ta próba jest ponowieniem próby, która wcześniej zakończyła się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="faa6b-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="faa6b-138">Dostawcy zwykle używają tej flagi, aby upewnić się, że pomijają istniejącą pamięć podręczną i w miarę możliwości monitują o nowe poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="faa6b-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="faa6b-139">Szczegółowość {value}</span><span class="sxs-lookup"><span data-stu-id="faa6b-139">Verbosity {value}</span></span> | <span data-ttu-id="faa6b-140">Jeśli jest obecna, jedna z następujących wartości: "normal", "quiet" lub "detailed".</span><span class="sxs-lookup"><span data-stu-id="faa6b-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="faa6b-141">Jeśli żadna wartość nie zostanie dostarczona, wartość domyślna to "normal".</span><span class="sxs-lookup"><span data-stu-id="faa6b-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="faa6b-142">Dostawcy powinni używać tego jako wskazania poziomu opcjonalnego rejestrowania do emitowania do standardowego strumienia błędów.</span><span class="sxs-lookup"><span data-stu-id="faa6b-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="faa6b-143">Kody zakończenia</span><span class="sxs-lookup"><span data-stu-id="faa6b-143">Exit codes</span></span>

| <span data-ttu-id="faa6b-144">Kod</span><span class="sxs-lookup"><span data-stu-id="faa6b-144">Code</span></span> |<span data-ttu-id="faa6b-145">Wynik</span><span class="sxs-lookup"><span data-stu-id="faa6b-145">Result</span></span> | <span data-ttu-id="faa6b-146">Opis</span><span class="sxs-lookup"><span data-stu-id="faa6b-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="faa6b-147">0</span><span class="sxs-lookup"><span data-stu-id="faa6b-147">0</span></span> | <span data-ttu-id="faa6b-148">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="faa6b-148">Success</span></span> | <span data-ttu-id="faa6b-149">Poświadczenia zostały pomyślnie uzyskane i zapisane w stdout.</span><span class="sxs-lookup"><span data-stu-id="faa6b-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="faa6b-150">1</span><span class="sxs-lookup"><span data-stu-id="faa6b-150">1</span></span> | <span data-ttu-id="faa6b-151">DostawcaNotApplicable</span><span class="sxs-lookup"><span data-stu-id="faa6b-151">ProviderNotApplicable</span></span> | <span data-ttu-id="faa6b-152">Bieżący dostawca nie podaje poświadczeń dla danego URI.</span><span class="sxs-lookup"><span data-stu-id="faa6b-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="faa6b-153">2</span><span class="sxs-lookup"><span data-stu-id="faa6b-153">2</span></span> | <span data-ttu-id="faa6b-154">Niepowodzenie</span><span class="sxs-lookup"><span data-stu-id="faa6b-154">Failure</span></span> | <span data-ttu-id="faa6b-155">Dostawca jest poprawnym dostawcą dla danego URI, ale nie może podać poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="faa6b-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="faa6b-156">W takim przypadku metoda nuget.exe ponowi próbę uwierzytelnienia i nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="faa6b-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="faa6b-157">Typowym przykładem jest anulowanie logowania interakcyjnego przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="faa6b-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="faa6b-158">Wyjście standardowe</span><span class="sxs-lookup"><span data-stu-id="faa6b-158">Standard output</span></span>

| <span data-ttu-id="faa6b-159">Właściwość</span><span class="sxs-lookup"><span data-stu-id="faa6b-159">Property</span></span> |<span data-ttu-id="faa6b-160">Uwagi</span><span class="sxs-lookup"><span data-stu-id="faa6b-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="faa6b-161">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="faa6b-161">Username</span></span> | <span data-ttu-id="faa6b-162">Nazwa użytkownika dla uwierzytelnionych żądań.</span><span class="sxs-lookup"><span data-stu-id="faa6b-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="faa6b-163">Hasło</span><span class="sxs-lookup"><span data-stu-id="faa6b-163">Password</span></span> | <span data-ttu-id="faa6b-164">Hasło dla uwierzytelnionych żądań.</span><span class="sxs-lookup"><span data-stu-id="faa6b-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="faa6b-165">Komunikat</span><span class="sxs-lookup"><span data-stu-id="faa6b-165">Message</span></span> | <span data-ttu-id="faa6b-166">Opcjonalne szczegóły dotyczące odpowiedzi, używane tylko do pokazywania dodatkowych szczegółów w przypadkach awarii.</span><span class="sxs-lookup"><span data-stu-id="faa6b-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="faa6b-167">Przykład stdout:</span><span class="sxs-lookup"><span data-stu-id="faa6b-167">Example stdout:</span></span>

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="faa6b-168">Rozwiązywanie problemów z dostawcą poświadczeń</span><span class="sxs-lookup"><span data-stu-id="faa6b-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="faa6b-169">Obecnie narzędzie NuGet nie zapewnia bezpośredniej obsługi debugowania niestandardowych dostawców poświadczeń. [problem 4598 śledzi](https://github.com/NuGet/Home/issues/4598) tę pracę.</span><span class="sxs-lookup"><span data-stu-id="faa6b-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="faa6b-170">Ponadto można wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="faa6b-170">You can also do the following:</span></span>

- <span data-ttu-id="faa6b-171">Uruchom nuget.exe z `-verbosity` przełącznikiem , aby sprawdzić szczegółowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="faa6b-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="faa6b-172">Dodaj komunikaty debugowania `stdout` do polecenia w odpowiednich miejscach.</span><span class="sxs-lookup"><span data-stu-id="faa6b-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="faa6b-173">Upewnij się, że używasz usługi nuget.exe 3.3 lub wyższej.</span><span class="sxs-lookup"><span data-stu-id="faa6b-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="faa6b-174">Dołącz debuger podczas uruchamiania za pomocą tego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="faa6b-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
