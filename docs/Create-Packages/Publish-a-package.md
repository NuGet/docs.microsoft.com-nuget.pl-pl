---
title: Jak opublikować pakietu NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Szczegółowe instrukcje dotyczące sposobu publikowania pakietu NuGet nuget.org lub prywatnej źródeł danych i jak zarządzać własność pakietu na nuget.org.
keywords: Publikowanie pakietu NuGet, publikowania pakietu NuGet, własność pakietu NuGet, publikować nuget.org, prywatnego źródeł danych NuGet
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 68db25276297353fab03258adecd9169149dbe51
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="publishing-packages"></a><span data-ttu-id="f6f90-104">Publikowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="f6f90-104">Publishing packages</span></span>

<span data-ttu-id="f6f90-105">Gdy utworzono pakiet i mieć Twojej `.nukpg` w pliku, jest prosty proces, aby udostępnić ją innym producentom publiczną lub prywatną:</span><span class="sxs-lookup"><span data-stu-id="f6f90-105">Once you have created a package and have your `.nukpg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="f6f90-106">Pakiety publicznego były dostępne dla wszystkich deweloperów globalnie za pomocą [nuget.org](https://www.nuget.org/packages/manage/upload) zgodnie z opisem w tym artykule (wymaga NuGet 4.1.0+).</span><span class="sxs-lookup"><span data-stu-id="f6f90-106">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="f6f90-107">Pakietów prywatnych są dostępne dla tylko zespół lub organizacja, umieszczając je albo udziału plików, serwer prywatnej NuGet [Visual Studio Team Services pakietu zarządzania](https://www.visualstudio.com/docs/package/nuget/publish), lub repozytorium innych firm, takich jak myget, ProGet, węzła Repozytorium i Artifactory.</span><span class="sxs-lookup"><span data-stu-id="f6f90-107">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="f6f90-108">Aby uzyskać więcej informacji, zobacz [Hosting Omówienie pakietów](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="f6f90-108">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="f6f90-109">W tym artykule omówiono publikowanie nuget.org; do publikowania w Visual Studio Team Services, zobacz [zarządzania pakietami](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="f6f90-109">This article covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="f6f90-110">Publikowanie nuget.org</span><span class="sxs-lookup"><span data-stu-id="f6f90-110">Publish to nuget.org</span></span>

<span data-ttu-id="f6f90-111">Dla nuget.org należy zalogować się przy użyciu konta Microsoft, z którym użytkownik zostanie zapytany zarejestrować konto z nuget.org. Możesz też zalogować się na koncie nuget.org utworzone za pomocą starszych wersji portalu.</span><span class="sxs-lookup"><span data-stu-id="f6f90-111">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![Lokalizacja logowania NuGet](media/publish_NuGetSignIn.png)

<span data-ttu-id="f6f90-113">Następnie można albo przekaż pakiet w portalu sieci web nuget.org, wypychać do nuget.org za pomocą wiersza polecenia (wymaga `nuget.exe` 4.1.0+), lub Opublikuj jako część procesu CI/CD za pomocą programu Visual Studio Team Services, zgodnie z opisem w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="f6f90-113">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="f6f90-114">Portal sieci Web: karta przekaż pakiet na nuget.org</span><span class="sxs-lookup"><span data-stu-id="f6f90-114">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="f6f90-115">Wybierz **przekazać** w górnym menu nuget.org i przejdź do lokalizacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="f6f90-115">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![Przekaż pakiet na nuget.org](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="f6f90-117">nuget.org informuje, czy nazwa pakietu jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="f6f90-117">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="f6f90-118">Zmiana nie będzie identyfikator pakietu w projekcie, skompiluj ponownie i spróbuj ponownie przekazywania.</span><span class="sxs-lookup"><span data-stu-id="f6f90-118">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="f6f90-119">Jeśli nazwa pakietu jest dostępny, zostanie otwarty nuget.org **Sprawdź** sekcji, w którym można przejrzeć metadanych z manifestu pakietu.</span><span class="sxs-lookup"><span data-stu-id="f6f90-119">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="f6f90-120">Aby zmienić dowolne z metadanych, należy edytować projektu (plik projektu lub `.nuspec` pliku), skompiluj ponownie ponownie utworzyć pakiet i Prześlij ponownie.</span><span class="sxs-lookup"><span data-stu-id="f6f90-120">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="f6f90-121">W obszarze **dokumentacji importu** możesz wkleić języka znaczników Markdown, wskaż polecenie swoje dokumenty przy użyciu adresu URL lub Przekaż plik dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="f6f90-121">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="f6f90-122">Gdy wszystkie informacje są gotowe, wybierz **przesyłania** przycisku</span><span class="sxs-lookup"><span data-stu-id="f6f90-122">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="f6f90-123">Wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="f6f90-123">Command line</span></span>

<span data-ttu-id="f6f90-124">Pakiety wypychania do nuget.org musi używać [nuget.exe v4.1.0 lub nowszej](https://www.nuget.org/downloads), który implementuje wymaganych [protokołów NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="f6f90-124">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="f6f90-125">Należy również klucz interfejsu API, który jest tworzony na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="f6f90-125">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="f6f90-126">Tworzenie kluczy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="f6f90-126">Create API keys</span></span>

[!INCLUDE[publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="f6f90-127">Publikowanie za pomocą wypychania nuget dotnet</span><span class="sxs-lookup"><span data-stu-id="f6f90-127">Publish with dotnet nuget push</span></span>

[!INCLUDE[publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="f6f90-128">Publikowanie za pomocą wypychania nuget</span><span class="sxs-lookup"><span data-stu-id="f6f90-128">Publish with nuget push</span></span>

1. <span data-ttu-id="f6f90-129">W wierszu polecenia, uruchom następujące polecenie, zastępując `<your_API_key>` z kluczem uzyskane z nuget.org:</span><span class="sxs-lookup"><span data-stu-id="f6f90-129">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="f6f90-130">To polecenie zapisuje klucz interfejsu API w konfiguracji NuGet, aby należy powtórzyć ten krok ponownie na tym samym komputerze.</span><span class="sxs-lookup"><span data-stu-id="f6f90-130">This command stores your API key in your NuGet configuration so that you need repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="f6f90-131">Wypychanie do pakietu do galerii NuGet przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f6f90-131">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

### <a name="package-validation-and-indexing"></a><span data-ttu-id="f6f90-132">Sprawdzanie poprawności pakietu i indeksowania</span><span class="sxs-lookup"><span data-stu-id="f6f90-132">Package validation and indexing</span></span>

<span data-ttu-id="f6f90-133">Pakiety do nuget.org przechodzą kilku operacji sprawdzania poprawności, takich jak sprawdzanie przed wirusami.</span><span class="sxs-lookup"><span data-stu-id="f6f90-133">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="f6f90-134">(Wszystkie pakiety na nuget.org okresowo są skanowane.)</span><span class="sxs-lookup"><span data-stu-id="f6f90-134">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="f6f90-135">.</span><span class="sxs-lookup"><span data-stu-id="f6f90-135">.</span></span> <span data-ttu-id="f6f90-136">Po upływie wszystkie testy sprawdzania poprawności pakietu może upłynąć trochę czasu na jej indeksowane i wyświetlane w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="f6f90-136">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="f6f90-137">Po zakończeniu indeksowania otrzymasz wiadomość e-mail z potwierdzeniem, że pakiet został pomyślnie opublikowany.</span><span class="sxs-lookup"><span data-stu-id="f6f90-137">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="f6f90-138">W przypadku niepowodzenia sprawdzenia poprawności pakietu na stronie Szczegóły pakietu zostanie zaktualizowana, aby wyświetlić skojarzony błąd i otrzymasz wiadomość e-mail powiadomienia użytkownika o nim.</span><span class="sxs-lookup"><span data-stu-id="f6f90-138">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="f6f90-139">Sprawdzanie poprawności pakietu i indeksowania zazwyczaj trwa poniżej 15 minut.</span><span class="sxs-lookup"><span data-stu-id="f6f90-139">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="f6f90-140">Publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź stronę [status.nuget.org](https://status.nuget.org/) do sprawdzenia, czy nuget.org występują żadnych przerw w działaniu.</span><span class="sxs-lookup"><span data-stu-id="f6f90-140">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="f6f90-141">Jeśli pakiet nie został pomyślnie opublikowany w ciągu godziny są wszystkie systemy operacyjne, zaloguj się do nuget.org i skontaktuj się z nami za pomocą łącza Skontaktuj się z pomocą techniczną na stronie pakiet.</span><span class="sxs-lookup"><span data-stu-id="f6f90-141">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="f6f90-142">Aby wyświetlić stan pakietu, wybierz **zarządzania pakietami** pod nazwą konta na nuget.org. Otrzymasz wiadomość e-mail z potwierdzeniem po zakończeniu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="f6f90-142">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="f6f90-143">Należy pamiętać, że może upłynąć trochę czasu pakietu indeksowane i wyświetlane w wynikach wyszukiwania, gdy inne można znaleźć go w tym czasie zostanie wyświetlony następujący komunikat na stronie pakiet:</span><span class="sxs-lookup"><span data-stu-id="f6f90-143">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Komunikat wskazujący, że pakiet nie został jeszcze opublikowany.](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="f6f90-145">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="f6f90-145">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="f6f90-146">Jeśli pakiety są Wypychanie do nuget.org jako część procesu ciągłej integracji/wdrożenia przy użyciu programu Visual Studio Team Services, należy użyć `nuget.exe` 4.1 lub nowszej w zadaniach NuGet.</span><span class="sxs-lookup"><span data-stu-id="f6f90-146">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="f6f90-147">Szczegółowe informacje można znaleźć w [za pomocą najnowszej NuGet w kompilacji](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog DevOps firmy Microsoft).</span><span class="sxs-lookup"><span data-stu-id="f6f90-147">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="f6f90-148">Zarządzanie właścicielami pakietu na nuget.org</span><span class="sxs-lookup"><span data-stu-id="f6f90-148">Managing package owners on nuget.org</span></span>

<span data-ttu-id="f6f90-149">Mimo że każdy pakiet NuGet `.nuspec` pliku definiuje autorów pakietu, Galeria nuget.org nie używa tych metadanych do definiowania własności.</span><span class="sxs-lookup"><span data-stu-id="f6f90-149">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="f6f90-150">Zamiast tego nuget.org przypisuje początkowej prawa własności do osoby, która publikuje pakiet.</span><span class="sxs-lookup"><span data-stu-id="f6f90-150">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="f6f90-151">To jest zalogowany użytkownik, który pakiet za pomocą nuget.org interfejsu użytkownika lub użytkowników, którego klucz interfejsu API została użyta z `nuget SetApiKey` lub `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="f6f90-151">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="f6f90-152">Wszystkie właściciele pakietu mają pełne uprawnienia do pakietu, w tym dodawanie i usuwanie właścicieli innych oraz publikowanie aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="f6f90-152">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="f6f90-153">Aby zmienić własność pakietu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f6f90-153">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="f6f90-154">Zaloguj się do nuget.org przy użyciu konta, który jest bieżącym właścicielem pakietu.</span><span class="sxs-lookup"><span data-stu-id="f6f90-154">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="f6f90-155">Wybierz nazwę konta, wybierz pozycję **zarządzania pakietami**i rozwiń **opublikowane pakiety**.</span><span class="sxs-lookup"><span data-stu-id="f6f90-155">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="f6f90-156">Wybierz w pakiecie, którymi chcesz zarządzać, a następnie po prawej stronie wybierz **Zarządzaj właścicielami**.</span><span class="sxs-lookup"><span data-stu-id="f6f90-156">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="f6f90-157">W tym miejscu masz kilka opcji:</span><span class="sxs-lookup"><span data-stu-id="f6f90-157">From here you have several options:</span></span>

1. <span data-ttu-id="f6f90-158">Usuń wszelkie właściciela kategorii **bieżącego właścicieli**.</span><span class="sxs-lookup"><span data-stu-id="f6f90-158">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="f6f90-159">Dodaj właściciela w obszarze **dodać właściciela** wprowadzania nazwy użytkownika, wiadomości i wybierając **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f6f90-159">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="f6f90-160">Ta akcja wysyła wiadomość e-mail do tej nowej współwłaściciel Link potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="f6f90-160">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="f6f90-161">Po potwierdzeniu, że osoba ma pełne uprawnienia do dodawania i usuwania właścicieli.</span><span class="sxs-lookup"><span data-stu-id="f6f90-161">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="f6f90-162">(Do momentu potwierdzony, **bieżącego właścicieli** sekcji wskazuje oczekują na zatwierdzenie dla tej osoby.)</span><span class="sxs-lookup"><span data-stu-id="f6f90-162">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="f6f90-163">Aby przetransferować własność (jako podczas zmiany własności lub pakiet został opublikowany na koncie niewłaściwy), Dodaj nowy właściciel, a po ich zostały potwierdzone własność one należy usunąć z listy.</span><span class="sxs-lookup"><span data-stu-id="f6f90-163">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="f6f90-164">Aby przypisać własność firmy lub grupy, należy utworzyć konto nuget.org przy użyciu alias poczty e-mail, który jest przekazywany do członków zespołu odpowiednie.</span><span class="sxs-lookup"><span data-stu-id="f6f90-164">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="f6f90-165">Na przykład różnych pakietów Microsoft ASP.NET umieszczone są własnością [microsoft](http://nuget.org/profiles/microsoft) i [aspnet](http://nuget.org/profiles/aspnet) kont, która po prostu takich aliasów.</span><span class="sxs-lookup"><span data-stu-id="f6f90-165">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="f6f90-166">Odzyskiwanie własność pakietu</span><span class="sxs-lookup"><span data-stu-id="f6f90-166">Recovering package ownership</span></span>

<span data-ttu-id="f6f90-167">Czasami pakietu nie mogą mieć aktywne właściciela.</span><span class="sxs-lookup"><span data-stu-id="f6f90-167">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="f6f90-168">Na przykład pierwotny właściciel mogą być przechowywane w firmie, która tworzy pakiet, nuget.org poświadczenia zostaną utracone lub wcześniejszych błędów w galerii pozostałych ownerless pakietu.</span><span class="sxs-lookup"><span data-stu-id="f6f90-168">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="f6f90-169">Jeśli jesteś właścicielem prawowitego pakietu i trzeba odzyskać własność, użyj [skontaktuj się z formularza](https://www.nuget.org/policies/Contact) na nuget.org w celu ułatwienia zrozumienia potrzeb do zespołu NuGet.</span><span class="sxs-lookup"><span data-stu-id="f6f90-169">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="f6f90-170">Firma Microsoft postępuj procesu zweryfikowanie prawa własności pakietu, w tym próby zlokalizowania istniejących właściciela przez adres URL projektu pakietu, Twitter, poczty e-mail lub w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="f6f90-170">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="f6f90-171">Ale jeśli nie wszystkie inne, abyśmy mogli podać nowe zaproszenie do staje się właścicielem.</span><span class="sxs-lookup"><span data-stu-id="f6f90-171">But if all else fails, we can send you a new invite to become an owner.</span></span>
