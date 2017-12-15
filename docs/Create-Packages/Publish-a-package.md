---
title: "Jak opublikować pakietu NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/5/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2342aabd-983e-4db1-9230-57c84fa36969
description: "Szczegółowe instrukcje dotyczące sposobu publikowania pakietu NuGet nuget.org lub prywatnej źródeł danych i jak zarządzać własność pakietu na nuget.org."
keywords: "Publikowanie pakietu NuGet, publikowania pakietu NuGet, własność pakietu NuGet, publikować nuget.org, prywatnego źródeł danych NuGet"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: fab25931165afb65aa3fd09c5bc37492ce814a49
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="publishing-packages"></a><span data-ttu-id="1e456-104">Publikowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="1e456-104">Publishing packages</span></span>

<span data-ttu-id="1e456-105">Po utworzeniu [utworzył pakiet](../create-packages/creating-a-package.md) z `nuget pack`, jest prosty proces, aby udostępnić ją innym producentom publiczną lub prywatną:</span><span class="sxs-lookup"><span data-stu-id="1e456-105">Once you have [created a package](../create-packages/creating-a-package.md) with `nuget pack`, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="1e456-106">Pakiety publicznego były dostępne dla wszystkich deweloperów globalnie za pomocą [nuget.org](https://www.nuget.org/packages/manage/upload) zgodnie z opisem w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="1e456-106">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this topic.</span></span>
- <span data-ttu-id="1e456-107">Pakietów prywatnych są dostępne dla tylko zespół lub organizacja, umieszczając je albo udziału plików, serwer prywatnej NuGet [Visual Studio Team Services pakietu zarządzania](https://www.visualstudio.com/docs/package/nuget/publish), lub repozytorium innych firm, takich jak myget, ProGet, węzła Repozytorium i Artifactory.</span><span class="sxs-lookup"><span data-stu-id="1e456-107">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="1e456-108">Aby uzyskać więcej informacji, zobacz [Hosting Omówienie pakietów](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="1e456-108">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="1e456-109">W tym temacie omówiono publikowanie nuget.org; do publikowania w Visual Studio Team Services, zobacz [zarządzania pakietami](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="1e456-109">This topic covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="1e456-110">Publikowanie nuget.org</span><span class="sxs-lookup"><span data-stu-id="1e456-110">Publish to nuget.org</span></span>

<span data-ttu-id="1e456-111">Dla nuget.org, należy najpierw [zarejestrować bezpłatne konto](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) lub zaloguj się, jeśli jest już zarejestrowany:</span><span class="sxs-lookup"><span data-stu-id="1e456-111">For nuget.org, you must first [register for a free account](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) or sign in if already registered:</span></span>

![Rejestracja NuGet i zalogować się w lokalizacji](media/publish_NuGetSignIn.png)

<span data-ttu-id="1e456-113">Następnie możesz przekazać pakiet w portalu sieci web nuget.org, wypychać do nuget.org za pomocą wiersza polecenia lub opublikować jako część procesu CI/CD za pomocą programu Visual Studio Team Services, zgodnie z opisem w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="1e456-113">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line, or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="1e456-114">Portal sieci Web: karta przekaż pakiet na nuget.org:</span><span class="sxs-lookup"><span data-stu-id="1e456-114">Web portal: use the Upload Package tab on nuget.org:</span></span>

![Przekaż pakiet z Menedżera pakietów NuGet](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a><span data-ttu-id="1e456-116">Wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="1e456-116">Command line:</span></span>
> [!Important]
> <span data-ttu-id="1e456-117">Pakiety wypychania do nuget.org musi używać [nuget.exe v4.1.0 lub nowszej](https://www.nuget.org/downloads), który implementuje wymaganych [protokołów NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="1e456-117">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="1e456-118">Kliknij nazwę użytkownika, aby przejść do ustawień konta.</span><span class="sxs-lookup"><span data-stu-id="1e456-118">Click on your user name to navigate to your account settings.</span></span>
2. <span data-ttu-id="1e456-119">W obszarze **klucz interfejsu API**, kliknij przycisk **Kopiuj do Schowka** można pobrać dostępu do klucza będziesz potrzebować na platformie interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="1e456-119">Under **API Key**, click **copy to clipboard** to retrieve the access key you'll need in the CLI:</span></span>

    ![Kopiowanie klucza interfejsu API z ustawienia konta](media/publish_APIKey.png)

3. <span data-ttu-id="1e456-121">W wierszu polecenia Uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1e456-121">At a command prompt, run the following command:</span></span>

    ```
    nuget setApiKey Your-API-Key
    ```

    <span data-ttu-id="1e456-122">Klucz interfejsu API to przechowuje na komputerze, dzięki czemu nie muszą wykonać ten krok ponownie na tym samym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1e456-122">This stores your API key on the machine so that you need not do this step again on the same machine.</span></span>

4. <span data-ttu-id="1e456-123">Wypychanie do pakietu do galerii NuGet za pomocą polecenia:</span><span class="sxs-lookup"><span data-stu-id="1e456-123">Push your package to NuGet Gallery using the command:</span></span>

    ```
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

5. <span data-ttu-id="1e456-124">Przed upubliczniona są wszystkie pakiety przekazane do nuget.org są skanowany w poszukiwaniu wirusów i odrzucone w przypadku znalezienia wirusów.</span><span class="sxs-lookup"><span data-stu-id="1e456-124">Before being made public, all packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="1e456-125">Wszystkie pakiety wymienione na nuget.org również są skanowane okresowo.</span><span class="sxs-lookup"><span data-stu-id="1e456-125">All packages listed on nuget.org are also scanned periodically.</span></span>

6. <span data-ttu-id="1e456-126">Na koncie nuget.org, kliknij przycisk **Moje pakiety zarządzania** aby zobaczyć ten właśnie opublikowane; otrzymasz również wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="1e456-126">In your account on nuget.org, click **Manage my packages** to see the one that you just published; you'll also receive a confirmation email.</span></span> <span data-ttu-id="1e456-127">Należy pamiętać, że może upłynąć trochę czasu pakietu indeksowane i wyświetlane w wynikach wyszukiwania, gdzie inne osoby mogą znaleźć go w tym czasie na stronie pakiet zostanie wyświetlony następujący komunikat:</span><span class="sxs-lookup"><span data-stu-id="1e456-127">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you'll see the following message on your package page:</span></span>

    ![Komunikat wskazujący, że pakiet nie jest jeszcze indeksowanym.](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a><span data-ttu-id="1e456-129">Sprawdzanie poprawności pakietu i indeksowania</span><span class="sxs-lookup"><span data-stu-id="1e456-129">Package Validation and Indexing</span></span>

<span data-ttu-id="1e456-130">Pakiety do NuGet.org przechodzą kilku operacji sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="1e456-130">Packages pushed to NuGet.org undergo several validations.</span></span> <span data-ttu-id="1e456-131">Po upływie wszystkie testy sprawdzania poprawności pakietu może upłynąć trochę czasu na jej indeksowane i wyświetlane w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="1e456-131">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="1e456-132">Po zakończeniu indeksowania otrzymasz wiadomość e-mail z potwierdzeniem, że pakiet został pomyślnie opublikowany.</span><span class="sxs-lookup"><span data-stu-id="1e456-132">Once indexing is complete, you'll receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="1e456-133">W przypadku niepowodzenia sprawdzenia poprawności pakietu na stronie Szczegóły pakietu zostanie zaktualizowana, aby wyświetlić skojarzony błąd i otrzymasz również wiadomość e-mail powiadomienia użytkownika o nim.</span><span class="sxs-lookup"><span data-stu-id="1e456-133">If the package fails a validation check, the package details page will update to display the associated error and you'll also receive an email notifying you about it.</span></span>

<span data-ttu-id="1e456-134">Sprawdzanie poprawności pakietu i indeksowania zazwyczaj trwa poniżej 15 minut.</span><span class="sxs-lookup"><span data-stu-id="1e456-134">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="1e456-135">Publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź stronę [status.nuget.org](https://status.nuget.org/) do sprawdzenia, czy NuGet.org występują żadnych przerw w działaniu.</span><span class="sxs-lookup"><span data-stu-id="1e456-135">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="1e456-136">Jeśli pakiet nie został pomyślnie opublikowany w ciągu godziny są wszystkie systemy operacyjne, zaloguj się do NuGet.org i skontaktuj się z nami za pomocą łącza Skontaktuj się z pomocą techniczną na stronie pakiet.</span><span class="sxs-lookup"><span data-stu-id="1e456-136">If all systems are operational and the package hasn't been successfully published within an hour, please login to NuGet.org and contact us using the Contact Support link on the package page.</span></span>

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="1e456-137">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="1e456-137">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="1e456-138">Jeśli pakiety są Wypychanie do nuget.org jako część procesu ciągłej integracji/wdrożenia przy użyciu programu Visual Studio Team Services, należy użyć nuget.exe 4.1 lub nowszej w zadaniach NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e456-138">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use nuget.exe 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="1e456-139">Szczegółowe informacje można znaleźć w [za pomocą najnowszej NuGet w kompilacji](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog DevOps firmy Microsoft).</span><span class="sxs-lookup"><span data-stu-id="1e456-139">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="1e456-140">Zarządzanie właścicielami pakietu na nuget.org</span><span class="sxs-lookup"><span data-stu-id="1e456-140">Managing package owners on nuget.org</span></span>

<span data-ttu-id="1e456-141">Mimo że każdy pakiet NuGet `.nuspec` pliku definiuje autorów pakietu, Galeria nuget.org nie używa tych metadanych do definiowania własności.</span><span class="sxs-lookup"><span data-stu-id="1e456-141">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="1e456-142">Zamiast tego nuget.org przypisuje początkowej prawa własności do osoby, która publikuje pakiet.</span><span class="sxs-lookup"><span data-stu-id="1e456-142">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="1e456-143">To jest zalogowany użytkownik, który pakiet za pomocą nuget.org interfejsu użytkownika lub użytkowników, którego klucz interfejsu API została użyta z `nuget SetApiKey` lub `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="1e456-143">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="1e456-144">Wszystkie właściciele pakietu mają pełne uprawnienia do pakietu, w tym dodawanie i usuwanie właścicieli innych oraz publikowanie aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="1e456-144">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="1e456-145">Aby zmienić własność pakietu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1e456-145">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="1e456-146">Zaloguj się do nuget.org przy użyciu konta, który jest bieżącym właścicielem pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e456-146">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="1e456-147">Kliknij swoją nazwę użytkownika, następnie **Moje pakiety zarządzania**, a następnie na pakiet, którym chcesz zarządzać.</span><span class="sxs-lookup"><span data-stu-id="1e456-147">Click on your username, then on **Manage my packages**, then on the package you want to manage.</span></span>
1. <span data-ttu-id="1e456-148">Kliknij przycisk **Zarządzaj właścicielami** link po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="1e456-148">Click the **Manage owners** link on the left side.</span></span>

<span data-ttu-id="1e456-149">W tym miejscu masz kilka opcji:</span><span class="sxs-lookup"><span data-stu-id="1e456-149">From here you have several options:</span></span>

1. <span data-ttu-id="1e456-150">Aby dodać właściciela, wprowadź nazwę konta ich NuGet, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="1e456-150">To add an owner, enter their NuGet account name and click **Add**.</span></span> <span data-ttu-id="1e456-151">To wysyła wiadomość e-mail do tej nowej współwłaściciel Link potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="1e456-151">This sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="1e456-152">Po potwierdzeniu, że osoba ma pełne uprawnienia do dodawania i usuwania właścicieli.</span><span class="sxs-lookup"><span data-stu-id="1e456-152">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="1e456-153">(Do momentu potwierdzony, **Zarządzaj właścicielami** strony wskazuje "oczekuje na zatwierdzenie" dla tej osoby).</span><span class="sxs-lookup"><span data-stu-id="1e456-153">(Until confirmed, the **Manage owners** page indicates "pending approval" for that person).</span></span>
1. <span data-ttu-id="1e456-154">Aby usunąć właściciela, wybierz odpowiednią nazwę na **Zarządzaj właścicielami** i kliknij przycisk **Usuń**.</span><span class="sxs-lookup"><span data-stu-id="1e456-154">To remove an owner, select their name on the **Manage owners** and click **Remove**.</span></span>
1. <span data-ttu-id="1e456-155">Aby przetransferować własność (jako podczas zmiany własności lub pakiet został opublikowany na koncie niewłaściwy), po prostu Dodaj nowy właściciel, a po ich zostały potwierdzone własność one należy usunąć z listy.</span><span class="sxs-lookup"><span data-stu-id="1e456-155">To transfer ownership (as when ownership changes or a package was published under the wrong account), simply add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="1e456-156">Aby przypisać własność firmy lub grupy, należy utworzyć konto nuget.org przy użyciu alias poczty e-mail, który jest przekazywany do członków zespołu odpowiednie.</span><span class="sxs-lookup"><span data-stu-id="1e456-156">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="1e456-157">Na przykład różnych pakietów Microsoft ASP.NET umieszczone są własnością [microsoft](http://nuget.org/profiles/microsoft) i [aspnet](http://nuget.org/profiles/aspnet) kont, która po prostu takich aliasów.</span><span class="sxs-lookup"><span data-stu-id="1e456-157">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="1e456-158">Odzyskiwanie własność pakietu</span><span class="sxs-lookup"><span data-stu-id="1e456-158">Recovering package ownership</span></span>

<span data-ttu-id="1e456-159">Czasami pakietu nie mogą mieć aktywne właściciela.</span><span class="sxs-lookup"><span data-stu-id="1e456-159">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="1e456-160">Na przykład pierwotny właściciel mogą być przechowywane w firmie, która tworzy pakiet, nuget.org poświadczenia zostaną utracone lub wcześniejszych błędów w galerii pozostałych ownerless pakietu.</span><span class="sxs-lookup"><span data-stu-id="1e456-160">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="1e456-161">Jeśli jesteś właścicielem prawowitego pakietu i trzeba odzyskać własność, użyj [skontaktuj się z formularza](https://www.nuget.org/policies/Contact) na nuget.org w celu ułatwienia zrozumienia potrzeb do zespołu NuGet.</span><span class="sxs-lookup"><span data-stu-id="1e456-161">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="1e456-162">Firma Microsoft postępuj procesu zweryfikowanie prawa własności pakietu, w tym próby zlokalizowania istniejących właściciela przez adres URL projektu pakietu, Twitter, poczty e-mail lub w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="1e456-162">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="1e456-163">Ale jeśli nie wszystkie inne, abyśmy mogli podać nowe zaproszenie do staje się właścicielem.</span><span class="sxs-lookup"><span data-stu-id="1e456-163">But if all else fails, we can send you a new invite to become an owner.</span></span>
