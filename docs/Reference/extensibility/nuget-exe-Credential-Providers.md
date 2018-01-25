---
title: "Dostawcy poświadczeń nuget.exe | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "nuget.exe dostawcy poświadczeń uwierzytelniania za pomocą źródło danych i są zaimplementowane jako zgodne z konwencjami określone elementy wykonywalne wiersza polecenia."
keywords: "dostawcy poświadczeń nuget.exe, Dostawca poświadczeń interfejsu API, uwierzytelniania za pomocą kanału informacyjnego, uwierzytelniania za pomocą galerii"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88ce0106ad4e628ba8120f94b7951c7746ab67f3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="1c54f-104">Źródła danych za pomocą nuget.exe dostawcy poświadczeń uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1c54f-104">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="1c54f-105">*NuGet 3.3+*</span><span class="sxs-lookup"><span data-stu-id="1c54f-105">*NuGet 3.3+*</span></span>

<span data-ttu-id="1c54f-106">Gdy `nuget.exe` potrzebuje poświadczeń do uwierzytelniania źródło szuka je w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1c54f-106">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="1c54f-107">NuGet najpierw szuka poświadczeń w `Nuget.Config` plików.</span><span class="sxs-lookup"><span data-stu-id="1c54f-107">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="1c54f-108">Następnie NuGet używa dostawcy poświadczeń wtyczki, mogą ulec kolejności podanej poniżej.</span><span class="sxs-lookup"><span data-stu-id="1c54f-108">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="1c54f-109">(I przykład [programu Visual Studio Team Services Dostawca poświadczeń](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span><span class="sxs-lookup"><span data-stu-id="1c54f-109">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="1c54f-110">NuGet następnie monituje użytkownika o poświadczenia w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="1c54f-110">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="1c54f-111">Należy pamiętać, że dostawcy poświadczeń opisanych tutaj działa tylko w `nuget.exe` , a nie w "dotnet restore" lub Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1c54f-111">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="1c54f-112">Dla dostawcy poświadczeń z programem Visual Studio, zobacz [nuget.exe dostawcy poświadczeń dla programu Visual Studio](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="1c54f-112">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="1c54f-113">dostawcy poświadczeń nuget.exe mogą być używane na 3 sposoby:</span><span class="sxs-lookup"><span data-stu-id="1c54f-113">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="1c54f-114">**Globalny**: Aby dostawca poświadczeń dostępne dla wszystkich wystąpień `nuget.exe` uruchamiana profilu bieżącego użytkownika, dodaj go do `%LocalAppData%\NuGet\CredentialProviders`.</span><span class="sxs-lookup"><span data-stu-id="1c54f-114">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="1c54f-115">Może być konieczne utworzenie `CredentialProviders` folderu.</span><span class="sxs-lookup"><span data-stu-id="1c54f-115">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="1c54f-116">Dostawcy poświadczeń można zainstalować w katalogu głównym `CredentialProviders` folder lub podfolder.</span><span class="sxs-lookup"><span data-stu-id="1c54f-116">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="1c54f-117">Jeśli dostawca poświadczeń ma wiele plików/zestawów, można użyć podfoldery do zachowania dostawców organizowane.</span><span class="sxs-lookup"><span data-stu-id="1c54f-117">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="1c54f-118">**Ze zmiennej środowiskowej**: może być przechowywany w dowolnym miejscu i dostępny dla dostawcy poświadczeń `nuget.exe` przez ustawienie `%NUGET_CREDENTIALPROVIDERS_PATH%` zmiennej środowiskowej do lokalizacji dostawcy.</span><span class="sxs-lookup"><span data-stu-id="1c54f-118">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="1c54f-119">Ta zmienna może być rozdzielana średnikami lista (na przykład `path1;path2`) Jeśli masz wiele lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="1c54f-119">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="1c54f-120">**Obok nuget.exe**: nuget.exe dostawcy poświadczeń można umieścić w tym samym folderze co `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="1c54f-120">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="1c54f-121">Podczas ładowania dostawcy poświadczeń `nuget.exe` wyszukuje powyższych lokalizacjach, w kolejności, dowolne pliki o nazwie `credentialprovider*.exe`, następnie ładuje tych plików w kolejności, w przypadku można odnaleźć.</span><span class="sxs-lookup"><span data-stu-id="1c54f-121">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="1c54f-122">Jeśli istnieje wielu dostawców poświadczeń w tym samym folderze, są one ładowane w kolejności alfabetycznej.</span><span class="sxs-lookup"><span data-stu-id="1c54f-122">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="1c54f-123">Tworzenie dostawcy poświadczeń nuget.exe</span><span class="sxs-lookup"><span data-stu-id="1c54f-123">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="1c54f-124">Dostawca poświadczeń jest pliku wykonywalnego wiersza polecenia o nazwie w postaci `CredentialProvider*.exe`, która gromadzi dane wejściowe, uzyskuje poświadczenia zależnie od potrzeb, a następnie zwraca kod stanu zakończenia odpowiednie i wyjścia standardowego.</span><span class="sxs-lookup"><span data-stu-id="1c54f-124">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="1c54f-125">Dostawca, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1c54f-125">A provider must do the following:</span></span>

- <span data-ttu-id="1c54f-126">Ustal, czy jego Podaj poświadczenia dla docelowego identyfikatora URI przed zainicjowaniem przejęcie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1c54f-126">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="1c54f-127">Jeśli nie, powinien zostać zwrócony kod stanu 1 bez poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1c54f-127">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="1c54f-128">Nie modyfikować `Nuget.Config` (na przykład istnieje ustawienie poświadczeń).</span><span class="sxs-lookup"><span data-stu-id="1c54f-128">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="1c54f-129">Konfiguracja serwera proxy obsługi HTTP na jego własnej jako NuGet nie zawiera informacje o serwerze proxy do wtyczki.</span><span class="sxs-lookup"><span data-stu-id="1c54f-129">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="1c54f-130">Zwraca poświadczeń lub szczegółów błędów do `nuget.exe` pisząc obiekt odpowiedzi JSON (patrz poniżej) do stdout, przy użyciu kodowania UTF-8.</span><span class="sxs-lookup"><span data-stu-id="1c54f-130">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="1c54f-131">Opcjonalnie Emituj rejestrowanie śledzenia dodatkowe stderr.</span><span class="sxs-lookup"><span data-stu-id="1c54f-131">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="1c54f-132">Nie kluczy tajnych kiedykolwiek powinna być zapisana stderr, ponieważ na poziomie szczegółowości "normal" lub "szczegółowe" takie śladów powtarzana przez narzędzie NuGet w konsoli.</span><span class="sxs-lookup"><span data-stu-id="1c54f-132">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="1c54f-133">Nieoczekiwany parametrów powinny być ignorowane, zapewniając zgodność z nowszymi wersjami w przyszłych wersjach programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="1c54f-133">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="1c54f-134">Parametry wejściowe</span><span class="sxs-lookup"><span data-stu-id="1c54f-134">Input parameters</span></span>

| <span data-ttu-id="1c54f-135">Parametr/przełącznika</span><span class="sxs-lookup"><span data-stu-id="1c54f-135">Parameter/Switch</span></span> |<span data-ttu-id="1c54f-136">Opis</span><span class="sxs-lookup"><span data-stu-id="1c54f-136">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="1c54f-137">Identyfikator URI {value}</span><span class="sxs-lookup"><span data-stu-id="1c54f-137">Uri {value}</span></span> | <span data-ttu-id="1c54f-138">Pakiet źródłowe poświadczenia wymagające identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="1c54f-138">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="1c54f-139">Nieinterakcyjne</span><span class="sxs-lookup"><span data-stu-id="1c54f-139">NonInteractive</span></span> | <span data-ttu-id="1c54f-140">Jeśli jest obecny, dostawcy nie wystawiać interaktywne monity.</span><span class="sxs-lookup"><span data-stu-id="1c54f-140">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="1c54f-141">IsRetry</span><span class="sxs-lookup"><span data-stu-id="1c54f-141">IsRetry</span></span> | <span data-ttu-id="1c54f-142">Jeśli jest obecny, wskazuje ta próba ponowienia wcześniej nieudanej próby.</span><span class="sxs-lookup"><span data-stu-id="1c54f-142">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="1c54f-143">Zazwyczaj dostawcy używają tej flagi Aby pominąć wszystkie istniejące pamięci podręcznej i monit o podanie poświadczeń nowe, jeśli to możliwe.</span><span class="sxs-lookup"><span data-stu-id="1c54f-143">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="1c54f-144">Poziom szczegółowości {value}</span><span class="sxs-lookup"><span data-stu-id="1c54f-144">Verbosity {value}</span></span> | <span data-ttu-id="1c54f-145">Jeśli nie istnieje jeden z następujących wartości: "normal", "quiet" lub "szczegóły".</span><span class="sxs-lookup"><span data-stu-id="1c54f-145">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="1c54f-146">Jeśli nie dostarczono żadnej wartości, domyślnie "normal".</span><span class="sxs-lookup"><span data-stu-id="1c54f-146">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="1c54f-147">Dostawców należy użyć tego wskaźnik poziomu rejestrowania opcjonalne do wysyłania do Standardowy strumień błędów.</span><span class="sxs-lookup"><span data-stu-id="1c54f-147">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="1c54f-148">Kody zakończenia</span><span class="sxs-lookup"><span data-stu-id="1c54f-148">Exit codes</span></span>

| <span data-ttu-id="1c54f-149">Kod</span><span class="sxs-lookup"><span data-stu-id="1c54f-149">Code</span></span> |<span data-ttu-id="1c54f-150">Wynik</span><span class="sxs-lookup"><span data-stu-id="1c54f-150">Result</span></span> | <span data-ttu-id="1c54f-151">Opis</span><span class="sxs-lookup"><span data-stu-id="1c54f-151">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="1c54f-152">0</span><span class="sxs-lookup"><span data-stu-id="1c54f-152">0</span></span> | <span data-ttu-id="1c54f-153">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="1c54f-153">Success</span></span> | <span data-ttu-id="1c54f-154">Poświadczenia zostały pomyślnie uzyskano i zapisano do stdout.</span><span class="sxs-lookup"><span data-stu-id="1c54f-154">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="1c54f-155">1</span><span class="sxs-lookup"><span data-stu-id="1c54f-155">1</span></span> | <span data-ttu-id="1c54f-156">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="1c54f-156">ProviderNotApplicable</span></span> | <span data-ttu-id="1c54f-157">Bieżący dostawca nie Podaj poświadczenia dla danego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="1c54f-157">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="1c54f-158">2</span><span class="sxs-lookup"><span data-stu-id="1c54f-158">2</span></span> | <span data-ttu-id="1c54f-159">Błąd</span><span class="sxs-lookup"><span data-stu-id="1c54f-159">Failure</span></span> | <span data-ttu-id="1c54f-160">Dostawca jest poprawna dostawca dla danego identyfikatora URI, ale nie można udostępnić poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1c54f-160">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="1c54f-161">W takim przypadku nuget.exe nie podejmie kolejnej próby uwierzytelniania i zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="1c54f-161">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="1c54f-162">Typowym przykładem jest, gdy użytkownik anuluje interakcyjnego logowania.</span><span class="sxs-lookup"><span data-stu-id="1c54f-162">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="1c54f-163">Standardowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="1c54f-163">Standard output</span></span>

| <span data-ttu-id="1c54f-164">Właściwość</span><span class="sxs-lookup"><span data-stu-id="1c54f-164">Property</span></span> |<span data-ttu-id="1c54f-165">Uwagi</span><span class="sxs-lookup"><span data-stu-id="1c54f-165">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="1c54f-166">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="1c54f-166">Username</span></span> | <span data-ttu-id="1c54f-167">Nazwa użytkownika dla żądań uwierzytelnionych.</span><span class="sxs-lookup"><span data-stu-id="1c54f-167">Username for authenticated requests.</span></span>|
| <span data-ttu-id="1c54f-168">Hasło</span><span class="sxs-lookup"><span data-stu-id="1c54f-168">Password</span></span> | <span data-ttu-id="1c54f-169">Hasło dla żądań uwierzytelnionych.</span><span class="sxs-lookup"><span data-stu-id="1c54f-169">Password for authenticated requests.</span></span>|
| <span data-ttu-id="1c54f-170">Komunikat</span><span class="sxs-lookup"><span data-stu-id="1c54f-170">Message</span></span> | <span data-ttu-id="1c54f-171">Opcjonalne szczegóły dotyczące odpowiedzi służą wyłącznie do zawierają dodatkowe szczegółowe informacje w przypadku awarii.</span><span class="sxs-lookup"><span data-stu-id="1c54f-171">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="1c54f-172">Przykład stdout:</span><span class="sxs-lookup"><span data-stu-id="1c54f-172">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="1c54f-173">Rozwiązywanie problemów z dostawcy poświadczeń</span><span class="sxs-lookup"><span data-stu-id="1c54f-173">Troubleshooting a credential provider</span></span>

<span data-ttu-id="1c54f-174">Obecnie NuGet nie obsługują wiele bezpośredniego debugowanie dostawców niestandardowych poświadczeń; [wystawiać 4598](https://github.com/NuGet/Home/issues/4598) służy do śledzenia tę pracę.</span><span class="sxs-lookup"><span data-stu-id="1c54f-174">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="1c54f-175">Można również wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1c54f-175">You can also do the following:</span></span>

- <span data-ttu-id="1c54f-176">Uruchom nuget.exe z `-verbosity` przełącznik, aby sprawdzić szczegółowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="1c54f-176">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="1c54f-177">Komunikaty debugowania, aby dodać `stdout` w odpowiednich miejscach.</span><span class="sxs-lookup"><span data-stu-id="1c54f-177">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="1c54f-178">Pamiętaj, że używasz nuget.exe 3.3 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1c54f-178">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="1c54f-179">Dołącz debugera przy uruchamianiu z następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="1c54f-179">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="1c54f-180">Aby uzyskać dalszą pomoc [przesłać żądanie obsługi nuget.org](https://www.nuget.org/policies/Contact).</span><span class="sxs-lookup"><span data-stu-id="1c54f-180">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
