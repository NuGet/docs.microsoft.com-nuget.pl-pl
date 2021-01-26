---
title: nuget.exe dostawców poświadczeń
description: nuget.exe dostawców poświadczeń uwierzytelniają się ze źródłem danych i są zaimplementowane jako pliki wykonywalne wiersza polecenia, które przestrzegają określonych konwencji.
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 285504508fa88c96f5c7a23f15ef14d81ebc21e1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777769"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="697b4-103">Uwierzytelnianie kanałów informacyjnych za pomocą dostawców poświadczeń nuget.exe</span><span class="sxs-lookup"><span data-stu-id="697b4-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="697b4-104">W obszarze `3.3` Obsługa wersji została dodana dla `nuget.exe` określonych dostawców poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="697b4-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="697b4-105">Od tej pory w programie `4.8` Dodano [obsługę dostawców poświadczeń](NuGet-Cross-Platform-Authentication-Plugin.md) , którzy działają we wszystkich scenariuszach wiersza polecenia ( `nuget.exe` , `dotnet.exe` ,, `msbuild.exe` ).</span><span class="sxs-lookup"><span data-stu-id="697b4-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="697b4-106">Aby uzyskać szczegółowe informacje dotyczące wszystkich metod uwierzytelniania dla programu, zobacz artykuł wykorzystywanie [pakietów ze źródeł uwierzytelnionych](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) . `nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="697b4-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="697b4-107">nuget.exe odnajdywania dostawcy poświadczeń</span><span class="sxs-lookup"><span data-stu-id="697b4-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="697b4-108">nuget.exe dostawców poświadczeń można używać na trzy sposoby:</span><span class="sxs-lookup"><span data-stu-id="697b4-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="697b4-109">**Globalnie**: Aby udostępnić dostawcę poświadczeń wszystkim wystąpieniu `nuget.exe` uruchomienia w ramach profilu bieżącego użytkownika, należy dodać go do programu `%LocalAppData%\NuGet\CredentialProviders` .</span><span class="sxs-lookup"><span data-stu-id="697b4-109">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="697b4-110">Może być konieczne utworzenie `CredentialProviders` folderu.</span><span class="sxs-lookup"><span data-stu-id="697b4-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="697b4-111">Dostawców poświadczeń można zainstalować w katalogu głównym `CredentialProviders`  folderu lub w podfolderze.</span><span class="sxs-lookup"><span data-stu-id="697b4-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="697b4-112">Jeśli Dostawca poświadczeń ma wiele plików/zestawów, można użyć podfolderów, aby zachować zorganizowanie dostawców.</span><span class="sxs-lookup"><span data-stu-id="697b4-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="697b4-113">**Ze zmiennej środowiskowej**: dostawcy poświadczeń można przechowywać w dowolnym miejscu i uzyskiwać do nich dostęp `nuget.exe` przez ustawienie `%NUGET_CREDENTIALPROVIDERS_PATH%` zmiennej środowiskowej na lokalizację dostawcy.</span><span class="sxs-lookup"><span data-stu-id="697b4-113">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="697b4-114">Ta zmienna może być rozdzielaną średnikami listą (na przykład `path1;path2` ), jeśli istnieje wiele lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="697b4-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="697b4-115">**Obok nuget.exe**: dostawcy poświadczeń nuget.exe można umieścić w tym samym folderze co `nuget.exe` .</span><span class="sxs-lookup"><span data-stu-id="697b4-115">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="697b4-116">Podczas ładowania dostawców poświadczeń program `nuget.exe` przeszukuje powyższe lokalizacje w podanej kolejności, `credentialprovider*.exe` a następnie ładuje te pliki w kolejności, w jakiej zostały znalezione.</span><span class="sxs-lookup"><span data-stu-id="697b4-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="697b4-117">Jeśli w tym samym folderze istnieje wielu dostawców poświadczeń, są one ładowane w kolejności alfabetycznej.</span><span class="sxs-lookup"><span data-stu-id="697b4-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="697b4-118">Tworzenie dostawcy poświadczeń nuget.exe</span><span class="sxs-lookup"><span data-stu-id="697b4-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="697b4-119">Dostawca poświadczeń to plik wykonywalny wiersza polecenia o nazwie w formularzu `CredentialProvider*.exe` , który zbiera dane wejściowe, uzyskuje poświadczenia zgodnie z potrzebami, a następnie zwraca odpowiedni kod stanu wyjścia i wyjście standardowe.</span><span class="sxs-lookup"><span data-stu-id="697b4-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="697b4-120">Dostawca musi wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="697b4-120">A provider must do the following:</span></span>

- <span data-ttu-id="697b4-121">Przed zainicjowaniem pozyskiwania poświadczeń należy określić, czy może podać poświadczenia dla danego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="697b4-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="697b4-122">Jeśli nie, powinien zwrócić kod stanu 1 bez poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="697b4-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="697b4-123">Nie należy modyfikować `Nuget.Config` (na przykład w przypadku ustawienia poświadczeń).</span><span class="sxs-lookup"><span data-stu-id="697b4-123">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="697b4-124">Obsługa konfiguracji serwera proxy HTTP we własnym zakresie, ponieważ narzędzie NuGet nie udostępnia informacji o serwerze proxy do wtyczki.</span><span class="sxs-lookup"><span data-stu-id="697b4-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="697b4-125">Zwróć poświadczenia lub szczegóły błędu `nuget.exe` , pisząc obiekt odpowiedzi JSON (patrz poniżej) do stdout przy użyciu kodowania UTF-8.</span><span class="sxs-lookup"><span data-stu-id="697b4-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="697b4-126">Opcjonalnie można emitować dodatkowe rejestrowanie śledzenia do STDERR.</span><span class="sxs-lookup"><span data-stu-id="697b4-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="697b4-127">Żadne wpisy tajne nie powinny być nigdy zapisywane w stderr, ponieważ na poziomie szczegółowości "normalny" lub "szczegółowe" takie ślady są wyświetlane przez program NuGet w konsoli programu.</span><span class="sxs-lookup"><span data-stu-id="697b4-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="697b4-128">Nieoczekiwane parametry powinny być ignorowane, co zapewnia zgodność z przyszłymi wersjami NuGet.</span><span class="sxs-lookup"><span data-stu-id="697b4-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="697b4-129">Parametry wejściowe</span><span class="sxs-lookup"><span data-stu-id="697b4-129">Input parameters</span></span>

| <span data-ttu-id="697b4-130">Parametr/przełącznik</span><span class="sxs-lookup"><span data-stu-id="697b4-130">Parameter/Switch</span></span> |<span data-ttu-id="697b4-131">Opis</span><span class="sxs-lookup"><span data-stu-id="697b4-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="697b4-132">Identyfikator URI {Value}</span><span class="sxs-lookup"><span data-stu-id="697b4-132">Uri {value}</span></span> | <span data-ttu-id="697b4-133">Źródłowy identyfikator URI pakietu wymaga poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="697b4-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="697b4-134">Nieinteraktywnych</span><span class="sxs-lookup"><span data-stu-id="697b4-134">NonInteractive</span></span> | <span data-ttu-id="697b4-135">Jeśli jest obecny, dostawca nie wystawia interakcyjnych wierszy.</span><span class="sxs-lookup"><span data-stu-id="697b4-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="697b4-136">Isretry</span><span class="sxs-lookup"><span data-stu-id="697b4-136">IsRetry</span></span> | <span data-ttu-id="697b4-137">Jeśli jest obecny, oznacza to, że próba wykonania poprzedniej nieudanej próby nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="697b4-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="697b4-138">Dostawcy zazwyczaj używają tej flagi, aby upewnić się, że pomijają istniejącą pamięć podręczną i monitują o nowe poświadczenia, jeśli jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="697b4-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="697b4-139">Poziom szczegółowości {Value}</span><span class="sxs-lookup"><span data-stu-id="697b4-139">Verbosity {value}</span></span> | <span data-ttu-id="697b4-140">Jeśli jest obecny, jedna z następujących wartości: "normal", "quiet" lub "Detailed".</span><span class="sxs-lookup"><span data-stu-id="697b4-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="697b4-141">Jeśli nie podano wartości, wartością domyślną jest "normal".</span><span class="sxs-lookup"><span data-stu-id="697b4-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="697b4-142">Dostawcy powinni używać tego jako wskazanie poziomu opcjonalnego rejestrowania do emisji do standardowego strumienia błędów.</span><span class="sxs-lookup"><span data-stu-id="697b4-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="697b4-143">Kody zakończenia</span><span class="sxs-lookup"><span data-stu-id="697b4-143">Exit codes</span></span>

| <span data-ttu-id="697b4-144">Kod</span><span class="sxs-lookup"><span data-stu-id="697b4-144">Code</span></span> |<span data-ttu-id="697b4-145">Wynik</span><span class="sxs-lookup"><span data-stu-id="697b4-145">Result</span></span> | <span data-ttu-id="697b4-146">Opis</span><span class="sxs-lookup"><span data-stu-id="697b4-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="697b4-147">0</span><span class="sxs-lookup"><span data-stu-id="697b4-147">0</span></span> | <span data-ttu-id="697b4-148">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="697b4-148">Success</span></span> | <span data-ttu-id="697b4-149">Pomyślnie pobrano poświadczenia i zapisano je w strumieniu stdout.</span><span class="sxs-lookup"><span data-stu-id="697b4-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="697b4-150">1</span><span class="sxs-lookup"><span data-stu-id="697b4-150">1</span></span> | <span data-ttu-id="697b4-151">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="697b4-151">ProviderNotApplicable</span></span> | <span data-ttu-id="697b4-152">Bieżący dostawca nie dostarcza poświadczeń dla danego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="697b4-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="697b4-153">2</span><span class="sxs-lookup"><span data-stu-id="697b4-153">2</span></span> | <span data-ttu-id="697b4-154">Niepowodzenie</span><span class="sxs-lookup"><span data-stu-id="697b4-154">Failure</span></span> | <span data-ttu-id="697b4-155">Dostawca jest poprawnym dostawcą dla danego identyfikatora URI, ale nie może podawać poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="697b4-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="697b4-156">W takim przypadku nuget.exe nie spróbuje ponownie uwierzytelniania i zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="697b4-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="697b4-157">Typowym przykładem jest to, że użytkownik anuluje Logowanie interakcyjne.</span><span class="sxs-lookup"><span data-stu-id="697b4-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="697b4-158">Wyjście standardowe</span><span class="sxs-lookup"><span data-stu-id="697b4-158">Standard output</span></span>

| <span data-ttu-id="697b4-159">Właściwość</span><span class="sxs-lookup"><span data-stu-id="697b4-159">Property</span></span> |<span data-ttu-id="697b4-160">Uwagi</span><span class="sxs-lookup"><span data-stu-id="697b4-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="697b4-161">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="697b4-161">Username</span></span> | <span data-ttu-id="697b4-162">Nazwa użytkownika dla żądań uwierzytelnionych.</span><span class="sxs-lookup"><span data-stu-id="697b4-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="697b4-163">Hasło</span><span class="sxs-lookup"><span data-stu-id="697b4-163">Password</span></span> | <span data-ttu-id="697b4-164">Hasło dla żądań uwierzytelnionych.</span><span class="sxs-lookup"><span data-stu-id="697b4-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="697b4-165">Komunikat</span><span class="sxs-lookup"><span data-stu-id="697b4-165">Message</span></span> | <span data-ttu-id="697b4-166">Opcjonalne szczegóły dotyczące odpowiedzi używane tylko w celu wyświetlenia dodatkowych szczegółów w przypadku awarii.</span><span class="sxs-lookup"><span data-stu-id="697b4-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="697b4-167">Przykład stdout:</span><span class="sxs-lookup"><span data-stu-id="697b4-167">Example stdout:</span></span>

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="697b4-168">Rozwiązywanie problemów z dostawcą poświadczeń</span><span class="sxs-lookup"><span data-stu-id="697b4-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="697b4-169">W tej chwili NuGet nie zapewnia wielu bezpośrednich obsłudze debugowania niestandardowych dostawców poświadczeń; [problem 4598](https://github.com/NuGet/Home/issues/4598) śledzi tę prace.</span><span class="sxs-lookup"><span data-stu-id="697b4-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="697b4-170">Ponadto można wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="697b4-170">You can also do the following:</span></span>

- <span data-ttu-id="697b4-171">Uruchom nuget.exe z `-verbosity` przełącznikiem, aby sprawdzić szczegółowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="697b4-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="697b4-172">Dodaj komunikaty debugowania do `stdout` w odpowiednich miejscach.</span><span class="sxs-lookup"><span data-stu-id="697b4-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="697b4-173">Upewnij się, że korzystasz z nuget.exe 3,3 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="697b4-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="697b4-174">Dołącz debuger podczas uruchamiania przy użyciu tego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="697b4-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
