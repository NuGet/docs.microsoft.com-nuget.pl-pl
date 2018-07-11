---
title: Jak opublikować pakiet NuGet
description: Szczegółowe instrukcje dotyczące sposobu opublikowania pakietu NuGet nuget.org lub źródła danych prywatnych i zarządzanie własność pakietu w witrynie nuget.org.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: eb45ac1574efc79873d2d372f122a3d756e90ee5
ms.sourcegitcommit: 6cffa6ef59b922df2d87aa9c24034d00542983cd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/10/2018
ms.locfileid: "37963119"
---
# <a name="publishing-packages"></a><span data-ttu-id="331ec-103">Publikowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="331ec-103">Publishing packages</span></span>

<span data-ttu-id="331ec-104">Gdy utworzono pakiet i mają swoje `.nupkg` plików w kasie, jest to prosty proces, aby udostępnić go innym deweloperom publiczną lub prywatną:</span><span class="sxs-lookup"><span data-stu-id="331ec-104">Once you have created a package and have your `.nupkg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="331ec-105">Publicznych pakietów są udostępniane wszystkim deweloperom globalnie za pomocą [nuget.org](https://www.nuget.org/packages/manage/upload) zgodnie z opisem w tym artykule (wymaga NuGet 4.1.0+).</span><span class="sxs-lookup"><span data-stu-id="331ec-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="331ec-106">Prywatne pakiety są dostępne dla zespołu lub organizacji, udostępniając je albo udziału plików, prywatny serwer NuGet, [programu Visual Studio Team Services pakietu Management](https://www.visualstudio.com/docs/package/nuget/publish), lub repozytorium innych firm, takich jak myget, ProGet, Nexus Repozytorium i Artifactory.</span><span class="sxs-lookup"><span data-stu-id="331ec-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="331ec-107">Aby uzyskać więcej informacji, zobacz [hostingu — Omówienie pakietów](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="331ec-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="331ec-108">W tym artykule opisano publikowania w witrynie nuget.org; do publikowania w Visual Studio Team Services, zobacz [zarządzania pakietami](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="331ec-108">This article covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="331ec-109">Publikowanie w witrynie nuget.org</span><span class="sxs-lookup"><span data-stu-id="331ec-109">Publish to nuget.org</span></span>

<span data-ttu-id="331ec-110">Nuget.org musisz zalogować się przy użyciu konta Microsoft, z którym użytkownik zostanie zapytany zarejestrować konto z repozytorium nuget.org. Możesz też zarejestrować się przy użyciu konta nuget.org, utworzony za pomocą starszej wersji portalu.</span><span class="sxs-lookup"><span data-stu-id="331ec-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![Znak NuGet w lokalizacji](media/publish_NuGetSignIn.png)

<span data-ttu-id="331ec-112">Następnie można albo przekaż pakiet za pośrednictwem portalu sieci web w witrynie nuget.org, Wypchnij do repozytorium nuget.org z wiersza polecenia (wymaga `nuget.exe` 4.1.0+), lub Opublikuj jako część procesu ciągłej integracji/ciągłego wdrażania za pomocą programu Visual Studio Team Services, zgodnie z opisem w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="331ec-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="331ec-113">Portal sieci Web: Użyj karty przekazywania pakietu w witrynie nuget.org</span><span class="sxs-lookup"><span data-stu-id="331ec-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="331ec-114">Wybierz **przekazywanie** w menu u góry nuget.org i przejdź do lokalizacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="331ec-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![Przekaż pakiet w witrynie nuget.org](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="331ec-116">nuget.org informuje, czy nazwa pakietu jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="331ec-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="331ec-117">Zmiana nie jest identyfikator pakietu w projekcie, ponownie skompilować, a następnie ponów próbę przekazania.</span><span class="sxs-lookup"><span data-stu-id="331ec-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="331ec-118">Jeśli nazwa pakietu jest dostępny, zostanie otwarty nuget.org **Sprawdź** sekcji, w którym można przejrzeć metadane z manifestu pakietu.</span><span class="sxs-lookup"><span data-stu-id="331ec-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="331ec-119">Aby zmienić dowolne z metadanych, należy edytować projektu (plik projektu lub `.nuspec` pliku), ponownie skompilować, ponowne utworzenie pakietu, a następnie przekaż ponownie.</span><span class="sxs-lookup"><span data-stu-id="331ec-119">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="331ec-120">W obszarze **dokumentacji importu** możesz wkleić języka znaczników Markdown, wskaż swoje dokumenty z adresem URL lub Przekaż plik dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="331ec-120">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="331ec-121">Gdy wszystkie informacje są gotowe, wybierz pozycję **przesyłania** przycisku</span><span class="sxs-lookup"><span data-stu-id="331ec-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="331ec-122">Wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="331ec-122">Command line</span></span>

<span data-ttu-id="331ec-123">Do wypychania pakietów nuget.org, należy użyć [nuget.exe verze 4.1.0 lub nowszej](https://www.nuget.org/downloads), który implementuje wymagane [protokołów NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="331ec-123">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="331ec-124">Musisz mieć również klucz interfejsu API, który jest tworzony w witrynie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="331ec-124">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="331ec-125">Tworzenie kluczy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="331ec-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="331ec-126">Publikowanie za pomocą polecenia dotnet nuget wypychania</span><span class="sxs-lookup"><span data-stu-id="331ec-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="331ec-127">Publikowanie za pomocą wypychania nuget</span><span class="sxs-lookup"><span data-stu-id="331ec-127">Publish with nuget push</span></span>

1. <span data-ttu-id="331ec-128">W wierszu polecenia Uruchom następujące polecenie, zastępując `<your_API_key>` przy użyciu klucza uzyskane z repozytorium nuget.org:</span><span class="sxs-lookup"><span data-stu-id="331ec-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="331ec-129">To polecenie przechowuje klucz interfejsu API w konfiguracji NuGet, dzięki czemu należy powtórzyć ten krok ponownie na tym samym komputerze.</span><span class="sxs-lookup"><span data-stu-id="331ec-129">This command stores your API key in your NuGet configuration so that you need repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="331ec-130">Wypchnij pakietu do galerii pakietów NuGet, używając następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="331ec-130">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a><span data-ttu-id="331ec-131">Publikowanie podpisanych pakietów</span><span class="sxs-lookup"><span data-stu-id="331ec-131">Publish signed packages</span></span>

<span data-ttu-id="331ec-132">Aby przesłać podpisanych pakietów, musisz najpierw [zarejestrować certyfikat](../reference/Signed-Packages-Reference.md#register-certificate-on-nugetorg) używany do podpisywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="331ec-132">To submit signed packages, you must first [register the certificate](../reference/Signed-Packages-Reference.md#register-certificate-on-nugetorg) used for signing the packages.</span></span> 

> [!Warning]
> <span data-ttu-id="331ec-133">nuget.org odrzuci pakiety, które nie spełniają [podpisany wymagań dotyczących pakietu](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="331ec-133">nuget.org rejects packages that don't satisfy the [signed package requirements](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span></span>

### <a name="package-validation-and-indexing"></a><span data-ttu-id="331ec-134">Sprawdzanie poprawności pakietu i indeksowania</span><span class="sxs-lookup"><span data-stu-id="331ec-134">Package validation and indexing</span></span>

<span data-ttu-id="331ec-135">Pakiety wypchnięty do repozytorium nuget.org uczestniczenia w kilku operacji sprawdzania poprawności, takich jak sprawdzanie przed wirusami.</span><span class="sxs-lookup"><span data-stu-id="331ec-135">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="331ec-136">(Wszystkie pakiety w witrynie nuget.org są okresowo skanowane.)</span><span class="sxs-lookup"><span data-stu-id="331ec-136">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="331ec-137">.</span><span class="sxs-lookup"><span data-stu-id="331ec-137">.</span></span> <span data-ttu-id="331ec-138">Gdy pakiet został przekazany wszystkie testy sprawdzania poprawności, może potrwać chwilę, aby mogła być indeksowane i wyświetlane w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="331ec-138">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="331ec-139">Po zakończeniu indeksowania, otrzymasz wiadomość e-mail, potwierdzenia, że pakiet został pomyślnie opublikowany.</span><span class="sxs-lookup"><span data-stu-id="331ec-139">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="331ec-140">Jeśli pakiet nie powiodło się sprawdzenie poprawności, na stronie szczegółów pakietu zostanie zaktualizowana, aby wyświetlić skojarzony błąd i otrzymasz wiadomość e-mail z powiadomieniem o nim.</span><span class="sxs-lookup"><span data-stu-id="331ec-140">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="331ec-141">Sprawdzanie poprawności pakietu i indeksowanie zwykle trwa mniej niż 15 minut.</span><span class="sxs-lookup"><span data-stu-id="331ec-141">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="331ec-142">Publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź stronę [status.nuget.org](https://status.nuget.org/) do sprawdzenia, jeśli nuget.org występuje przerw.</span><span class="sxs-lookup"><span data-stu-id="331ec-142">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="331ec-143">Jeśli pakiet nie został pomyślnie opublikowany w ciągu godziny są wszystkie systemy operacyjne, zaloguj się na stronie nuget.org i skontaktuj się z nami przy użyciu linku skontaktuj się z działem pomocy technicznej na stronie pakiet.</span><span class="sxs-lookup"><span data-stu-id="331ec-143">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="331ec-144">Aby wyświetlić stan pakietu, wybierz **Zarządzanie pakietami** pod nazwą Twojego konta w witrynie nuget.org. Otrzymasz wiadomość e-mail z potwierdzeniem, gdy sprawdzanie poprawności zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="331ec-144">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="331ec-145">Należy zwrócić uwagę na to, że może upłynąć trochę czasu pakiet indeksowane i wyświetlane w wynikach wyszukiwania, gdzie inne osoby mogą ją znaleźć, w tym czasie zostanie wyświetlony następujący komunikat na stronie pakiet:</span><span class="sxs-lookup"><span data-stu-id="331ec-145">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Komunikat wskazujący, że pakiet nie został jeszcze opublikowany.](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="331ec-147">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="331ec-147">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="331ec-148">Jeśli pakiety są wypychane na stronie nuget.org, jako część procesu ciągłej integracji/ciągłego wdrażania za pomocą programu Visual Studio Team Services, należy użyć `nuget.exe` 4.1 lub nowszym w zadaniach NuGet.</span><span class="sxs-lookup"><span data-stu-id="331ec-148">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="331ec-149">Szczegółowe informacje można znaleźć na [przy użyciu najnowszego rozwiązania NuGet w kompilacji](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (blog Microsoft DevOps).</span><span class="sxs-lookup"><span data-stu-id="331ec-149">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="331ec-150">Zarządzanie właścicielami pakietu w witrynie nuget.org</span><span class="sxs-lookup"><span data-stu-id="331ec-150">Managing package owners on nuget.org</span></span>

<span data-ttu-id="331ec-151">Mimo że każdy pakiet NuGet `.nuspec` plik definiuje autorom pakietów, galerii nuget.org nie używa tych metadanych do definiowania własności.</span><span class="sxs-lookup"><span data-stu-id="331ec-151">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="331ec-152">Zamiast tego nuget.org przypisuje początkowej prawa własności do osoby, która publikuje pakiet.</span><span class="sxs-lookup"><span data-stu-id="331ec-152">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="331ec-153">Jest to zalogowanego użytkownika, który pakiet za pośrednictwem interfejsu użytkownika w witrynie nuget.org, lub użytkowników, których klucz interfejsu API została użyta z `nuget SetApiKey` lub `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="331ec-153">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="331ec-154">Wszyscy właściciele pakietu mają pełne uprawnienia do pakietu, w tym dodawanie i usuwanie innych właścicieli i publikowanie aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="331ec-154">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="331ec-155">Aby zmienić własność pakietu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="331ec-155">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="331ec-156">Zaloguj się w witrynie nuget.org, przy użyciu konta, który jest bieżącym właścicielem pakietu.</span><span class="sxs-lookup"><span data-stu-id="331ec-156">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="331ec-157">Wybierz nazwę swojego konta, wybierz pozycję **Zarządzanie pakietami**i rozwiń **opublikowane pakiety**.</span><span class="sxs-lookup"><span data-stu-id="331ec-157">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="331ec-158">Wybierz pakiet, którym chcesz zarządzać, a następnie po prawej stronie wybierz **zarządzenie właścicielami**.</span><span class="sxs-lookup"><span data-stu-id="331ec-158">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="331ec-159">W tym miejscu masz kilka opcji:</span><span class="sxs-lookup"><span data-stu-id="331ec-159">From here you have several options:</span></span>

1. <span data-ttu-id="331ec-160">Usuń wszelkie właściciela na liście **bieżącego właścicieli**.</span><span class="sxs-lookup"><span data-stu-id="331ec-160">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="331ec-161">Dodaj właściciela w obszarze **dodać właściciela** , wprowadzając odpowiednią nazwę użytkownika, komunikat i wybierając **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="331ec-161">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="331ec-162">Ta akcja spowoduje wysłanie wiadomości e-mail do tego nowego właściciela współpracujących z linkiem umożliwiającym potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="331ec-162">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="331ec-163">Po potwierdzeniu, osoba ta ma pełne uprawnienia do dodawania i usuwania właścicieli.</span><span class="sxs-lookup"><span data-stu-id="331ec-163">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="331ec-164">(Do czasu potwierdzenia, **bieżącego właścicieli** sekcji wskazuje na zatwierdzenie dla tej osoby.)</span><span class="sxs-lookup"><span data-stu-id="331ec-164">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="331ec-165">Aby przenieść własność (jako podczas zmiany prawa własności lub pakietu została opublikowana na koncie problem), Dodaj nowego właściciela, a po ich zostało potwierdzone własność one należy usunąć z listy.</span><span class="sxs-lookup"><span data-stu-id="331ec-165">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="331ec-166">Aby przypisać własność firmy lub grupy, Utwórz konto nuget.org, za pomocą aliasu adresu e-mail, który jest przekazywany do członków zespołu odpowiednie.</span><span class="sxs-lookup"><span data-stu-id="331ec-166">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="331ec-167">Na przykład różne pakiety Microsoft ASP.NET wspólnie są własnością [microsoft](http://nuget.org/profiles/microsoft) i [aspnet](http://nuget.org/profiles/aspnet) konta, które po prostu takie aliasy.</span><span class="sxs-lookup"><span data-stu-id="331ec-167">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="331ec-168">Odzyskiwanie własność pakietu</span><span class="sxs-lookup"><span data-stu-id="331ec-168">Recovering package ownership</span></span>

<span data-ttu-id="331ec-169">Od czasu do czasu pakietu nie może mieć aktywne właściciela.</span><span class="sxs-lookup"><span data-stu-id="331ec-169">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="331ec-170">Na przykład pierwotnego właściciela mogą być przechowywane w firmie, która tworzy pakiet, nuget.org poświadczenia zostaną utracone lub wcześniejsze błędy w galerii left ownerless pakietu.</span><span class="sxs-lookup"><span data-stu-id="331ec-170">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="331ec-171">Jeśli są prawowitego właściciela pakietu i trzeba odzyskać własności, użyj [formularz kontaktowy](https://www.nuget.org/policies/Contact) w witrynie nuget.org, aby wyjaśnić sytuacji zespołowi NuGet.</span><span class="sxs-lookup"><span data-stu-id="331ec-171">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="331ec-172">Firma Microsoft następnie postępuj zgodnie z procesem na zweryfikowanie Twojej własności pakietu, w tym próbuje zlokalizować istniejący właściciel za pośrednictwem adresu URL projektu pakietu, Twitter, wiadomości e-mail lub w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="331ec-172">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="331ec-173">Ale jeśli wszystko inne nie powiedzie się, możemy wysłać nowe zaproszenie, aby stać się właścicielem.</span><span class="sxs-lookup"><span data-stu-id="331ec-173">But if all else fails, we can send you a new invite to become an owner.</span></span>
