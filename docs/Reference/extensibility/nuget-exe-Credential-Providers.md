---
title: Dostawcy poświadczeń nuget.exe
description: nuget.exe dostawcy poświadczeń uwierzytelniania za pomocą źródło danych i są zaimplementowane jako zgodne z konwencjami określone elementy wykonywalne wiersza polecenia.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 494ea83007895e973585395e0cfe05b7226c4c3e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="2a316-103">Źródła danych za pomocą nuget.exe dostawcy poświadczeń uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="2a316-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="2a316-104">*NuGet 3.3+*</span><span class="sxs-lookup"><span data-stu-id="2a316-104">*NuGet 3.3+*</span></span>

<span data-ttu-id="2a316-105">Gdy `nuget.exe` potrzebuje poświadczeń do uwierzytelniania źródło szuka je w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2a316-105">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="2a316-106">NuGet najpierw szuka poświadczeń w `Nuget.Config` plików.</span><span class="sxs-lookup"><span data-stu-id="2a316-106">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="2a316-107">Następnie NuGet używa dostawcy poświadczeń wtyczki, mogą ulec kolejności podanej poniżej.</span><span class="sxs-lookup"><span data-stu-id="2a316-107">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="2a316-108">(I przykład [programu Visual Studio Team Services Dostawca poświadczeń](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="2a316-108">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="2a316-109">NuGet następnie monituje użytkownika o poświadczenia w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="2a316-109">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="2a316-110">Należy pamiętać, że dostawcy poświadczeń opisanych tutaj działa tylko w `nuget.exe` , a nie w "dotnet restore" lub Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2a316-110">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="2a316-111">Dla dostawcy poświadczeń z programem Visual Studio, zobacz [nuget.exe dostawcy poświadczeń dla programu Visual Studio](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="2a316-111">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="2a316-112">dostawcy poświadczeń nuget.exe mogą być używane na 3 sposoby:</span><span class="sxs-lookup"><span data-stu-id="2a316-112">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="2a316-113">**Globalny**: Aby dostawca poświadczeń dostępne dla wszystkich wystąpień `nuget.exe` uruchamiana profilu bieżącego użytkownika, dodaj go do `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="2a316-113">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="2a316-114">Może być konieczne utworzenie `CredentialProviders` folderu.</span><span class="sxs-lookup"><span data-stu-id="2a316-114">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="2a316-115">Dostawcy poświadczeń można zainstalować w katalogu głównym `CredentialProviders` folder lub podfolder.</span><span class="sxs-lookup"><span data-stu-id="2a316-115">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="2a316-116">Jeśli dostawca poświadczeń ma wiele plików/zestawów, można użyć podfoldery do zachowania dostawców organizowane.</span><span class="sxs-lookup"><span data-stu-id="2a316-116">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="2a316-117">**Ze zmiennej środowiskowej**: może być przechowywany w dowolnym miejscu i dostępny dla dostawcy poświadczeń `nuget.exe` przez ustawienie `%NUGET_CREDENTIALPROVIDERS_PATH%` zmiennej środowiskowej do lokalizacji dostawcy.</span><span class="sxs-lookup"><span data-stu-id="2a316-117">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="2a316-118">Ta zmienna może być rozdzielana średnikami lista (na przykład `path1;path2`) Jeśli masz wiele lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="2a316-118">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="2a316-119">**Obok nuget.exe**: nuget.exe dostawcy poświadczeń można umieścić w tym samym folderze co `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="2a316-119">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="2a316-120">Podczas ładowania dostawcy poświadczeń `nuget.exe` wyszukuje powyższych lokalizacjach, w kolejności, dowolne pliki o nazwie `credentialprovider*.exe`, następnie ładuje tych plików w kolejności, w przypadku można odnaleźć.</span><span class="sxs-lookup"><span data-stu-id="2a316-120">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="2a316-121">Jeśli istnieje wielu dostawców poświadczeń w tym samym folderze, są one ładowane w kolejności alfabetycznej.</span><span class="sxs-lookup"><span data-stu-id="2a316-121">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="2a316-122">Tworzenie dostawcy poświadczeń nuget.exe</span><span class="sxs-lookup"><span data-stu-id="2a316-122">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="2a316-123">Dostawca poświadczeń jest pliku wykonywalnego wiersza polecenia o nazwie w postaci `CredentialProvider*.exe`, która gromadzi dane wejściowe, uzyskuje poświadczenia zależnie od potrzeb, a następnie zwraca kod stanu zakończenia odpowiednie i wyjścia standardowego.</span><span class="sxs-lookup"><span data-stu-id="2a316-123">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="2a316-124">Dostawca, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2a316-124">A provider must do the following:</span></span>

- <span data-ttu-id="2a316-125">Ustal, czy jego Podaj poświadczenia dla docelowego identyfikatora URI przed zainicjowaniem przejęcie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="2a316-125">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="2a316-126">Jeśli nie, powinien zostać zwrócony kod stanu 1 bez poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="2a316-126">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="2a316-127">Nie modyfikować `Nuget.Config` (na przykład istnieje ustawienie poświadczeń).</span><span class="sxs-lookup"><span data-stu-id="2a316-127">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="2a316-128">Konfiguracja serwera proxy obsługi HTTP na jego własnej jako NuGet nie zawiera informacje o serwerze proxy do wtyczki.</span><span class="sxs-lookup"><span data-stu-id="2a316-128">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="2a316-129">Zwraca poświadczeń lub szczegółów błędów do `nuget.exe` pisząc obiekt odpowiedzi JSON (patrz poniżej) do stdout, przy użyciu kodowania UTF-8.</span><span class="sxs-lookup"><span data-stu-id="2a316-129">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="2a316-130">Opcjonalnie Emituj rejestrowanie śledzenia dodatkowe stderr.</span><span class="sxs-lookup"><span data-stu-id="2a316-130">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="2a316-131">Nie kluczy tajnych kiedykolwiek powinna być zapisana stderr, ponieważ na poziomie szczegółowości "normal" lub "szczegółowe" takie śladów powtarzana przez narzędzie NuGet w konsoli.</span><span class="sxs-lookup"><span data-stu-id="2a316-131">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="2a316-132">Nieoczekiwany parametrów powinny być ignorowane, zapewniając zgodność z nowszymi wersjami w przyszłych wersjach programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="2a316-132">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="2a316-133">Parametry wejściowe</span><span class="sxs-lookup"><span data-stu-id="2a316-133">Input parameters</span></span>

| <span data-ttu-id="2a316-134">Parametr/przełącznika</span><span class="sxs-lookup"><span data-stu-id="2a316-134">Parameter/Switch</span></span> |<span data-ttu-id="2a316-135">Opis</span><span class="sxs-lookup"><span data-stu-id="2a316-135">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="2a316-136">Identyfikator URI {value}</span><span class="sxs-lookup"><span data-stu-id="2a316-136">Uri {value}</span></span> | <span data-ttu-id="2a316-137">Pakiet źródłowe poświadczenia wymagające identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="2a316-137">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="2a316-138">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="2a316-138">NonInteractive</span></span> | <span data-ttu-id="2a316-139">Jeśli jest obecny, dostawcy nie wystawiać interaktywne monity.</span><span class="sxs-lookup"><span data-stu-id="2a316-139">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="2a316-140">IsRetry</span><span class="sxs-lookup"><span data-stu-id="2a316-140">IsRetry</span></span> | <span data-ttu-id="2a316-141">Jeśli jest obecny, wskazuje ta próba ponowienia wcześniej nieudanej próby.</span><span class="sxs-lookup"><span data-stu-id="2a316-141">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="2a316-142">Zazwyczaj dostawcy używają tej flagi Aby pominąć wszystkie istniejące pamięci podręcznej i monit o podanie poświadczeń nowe, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="2a316-142">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="2a316-143">Poziom szczegółowości {value}</span><span class="sxs-lookup"><span data-stu-id="2a316-143">Verbosity {value}</span></span> | <span data-ttu-id="2a316-144">Jeśli nie istnieje jeden z następujących wartości: "normal", "quiet" lub "szczegóły".</span><span class="sxs-lookup"><span data-stu-id="2a316-144">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="2a316-145">Jeśli nie dostarczono żadnej wartości, domyślnie "normal".</span><span class="sxs-lookup"><span data-stu-id="2a316-145">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="2a316-146">Dostawców należy użyć tego wskaźnik poziomu rejestrowania opcjonalne do wysyłania do Standardowy strumień błędów.</span><span class="sxs-lookup"><span data-stu-id="2a316-146">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="2a316-147">Kody zakończenia</span><span class="sxs-lookup"><span data-stu-id="2a316-147">Exit codes</span></span>

| <span data-ttu-id="2a316-148">Kod</span><span class="sxs-lookup"><span data-stu-id="2a316-148">Code</span></span> |<span data-ttu-id="2a316-149">Wynik</span><span class="sxs-lookup"><span data-stu-id="2a316-149">Result</span></span> | <span data-ttu-id="2a316-150">Opis</span><span class="sxs-lookup"><span data-stu-id="2a316-150">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="2a316-151">0</span><span class="sxs-lookup"><span data-stu-id="2a316-151">0</span></span> | <span data-ttu-id="2a316-152">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="2a316-152">Success</span></span> | <span data-ttu-id="2a316-153">Poświadczenia zostały pomyślnie uzyskano i zapisano do stdout.</span><span class="sxs-lookup"><span data-stu-id="2a316-153">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="2a316-154">1</span><span class="sxs-lookup"><span data-stu-id="2a316-154">1</span></span> | <span data-ttu-id="2a316-155">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="2a316-155">ProviderNotApplicable</span></span> | <span data-ttu-id="2a316-156">Bieżący dostawca nie Podaj poświadczenia dla danego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="2a316-156">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="2a316-157">2</span><span class="sxs-lookup"><span data-stu-id="2a316-157">2</span></span> | <span data-ttu-id="2a316-158">Błąd</span><span class="sxs-lookup"><span data-stu-id="2a316-158">Failure</span></span> | <span data-ttu-id="2a316-159">Dostawca jest poprawna dostawca dla danego identyfikatora URI, ale nie można udostępnić poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="2a316-159">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="2a316-160">W takim przypadku nuget.exe nie podejmie kolejnej próby uwierzytelniania i zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="2a316-160">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="2a316-161">Typowym przykładem jest, gdy użytkownik anuluje interakcyjnego logowania.</span><span class="sxs-lookup"><span data-stu-id="2a316-161">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="2a316-162">Standardowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="2a316-162">Standard output</span></span>

| <span data-ttu-id="2a316-163">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2a316-163">Property</span></span> |<span data-ttu-id="2a316-164">Uwagi</span><span class="sxs-lookup"><span data-stu-id="2a316-164">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="2a316-165">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="2a316-165">Username</span></span> | <span data-ttu-id="2a316-166">Nazwa użytkownika dla żądań uwierzytelnionych.</span><span class="sxs-lookup"><span data-stu-id="2a316-166">Username for authenticated requests.</span></span>|
| <span data-ttu-id="2a316-167">Hasło</span><span class="sxs-lookup"><span data-stu-id="2a316-167">Password</span></span> | <span data-ttu-id="2a316-168">Hasło dla żądań uwierzytelnionych.</span><span class="sxs-lookup"><span data-stu-id="2a316-168">Password for authenticated requests.</span></span>|
| <span data-ttu-id="2a316-169">Komunikat</span><span class="sxs-lookup"><span data-stu-id="2a316-169">Message</span></span> | <span data-ttu-id="2a316-170">Opcjonalne szczegóły dotyczące odpowiedzi służą wyłącznie do zawierają dodatkowe szczegółowe informacje w przypadku awarii.</span><span class="sxs-lookup"><span data-stu-id="2a316-170">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="2a316-171">Przykład stdout:</span><span class="sxs-lookup"><span data-stu-id="2a316-171">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="2a316-172">Rozwiązywanie problemów z dostawcy poświadczeń</span><span class="sxs-lookup"><span data-stu-id="2a316-172">Troubleshooting a credential provider</span></span>

<span data-ttu-id="2a316-173">Obecnie NuGet nie obsługują wiele bezpośredniego debugowanie dostawców niestandardowych poświadczeń; [wystawiać 4598](https://github.com/NuGet/Home/issues/4598) służy do śledzenia tę pracę.</span><span class="sxs-lookup"><span data-stu-id="2a316-173">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="2a316-174">Można również wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="2a316-174">You can also do the following:</span></span>

- <span data-ttu-id="2a316-175">Uruchom nuget.exe z `-verbosity` przełącznik, aby sprawdzić szczegółowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="2a316-175">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="2a316-176">Komunikaty debugowania, aby dodać `stdout` w odpowiednich miejscach.</span><span class="sxs-lookup"><span data-stu-id="2a316-176">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="2a316-177">Pamiętaj, że używasz nuget.exe 3.3 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="2a316-177">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="2a316-178">Dołącz debugera przy uruchamianiu z następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="2a316-178">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="2a316-179">Aby uzyskać dalszą pomoc [przesłać żądanie obsługi nuget.org](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="2a316-179">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
