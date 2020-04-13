---
title: Jak opublikować pakiet NuGet
description: Szczegółowe instrukcje dotyczące publikowania pakietu NuGet do nuget.org lub prywatnych kanałów informacyjnych oraz zarządzania własnością pakietu w nuget.org.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 02c6c8f3018bfd063c2d16a10381f88b54cac840
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429025"
---
# <a name="publishing-packages"></a><span data-ttu-id="ed4fc-103">Publikowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="ed4fc-103">Publishing packages</span></span>

<span data-ttu-id="ed4fc-104">Po utworzeniu pakietu i `.nupkg` udostępnieniu pliku w ręku jest to prosty proces, aby udostępnić go innym deweloperom, publicznie lub prywatnie:</span><span class="sxs-lookup"><span data-stu-id="ed4fc-104">Once you have created a package and have your `.nupkg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="ed4fc-105">Pakiety publiczne są udostępniane wszystkim deweloperom na całym świecie za pośrednictwem [nuget.org](https://www.nuget.org/packages/manage/upload) zgodnie z opisem w tym artykule (wymaga NuGet 4.1.0+).</span><span class="sxs-lookup"><span data-stu-id="ed4fc-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="ed4fc-106">Pakiety prywatne są dostępne tylko dla zespołu lub organizacji, hostując je albo udział plików, prywatny serwer NuGet, [artefakty platformy Azure](https://www.visualstudio.com/docs/package/nuget/publish), lub repozytorium innych firm, takich jak myget, ProGet, Repozytorium Nexus i Artifactory.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="ed4fc-107">Aby uzyskać dodatkowe informacje, zobacz [Omówienie pakietów hostingowych](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed4fc-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="ed4fc-108">Ten artykuł obejmuje publikowanie do nuget.org; aby opublikować w witrynie Azure Artifacts, zobacz [Zarządzanie pakietami](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="ed4fc-108">This article covers publishing to nuget.org; for publishing to Azure Artifacts, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="ed4fc-109">Publikowanie w nuget.org</span><span class="sxs-lookup"><span data-stu-id="ed4fc-109">Publish to nuget.org</span></span>

<span data-ttu-id="ed4fc-110">Aby nuget.org, musisz zalogować się za pomocą konta Microsoft, za pomocą którego zostaniesz poproszony o zarejestrowanie konta w nuget.org. Możesz również zalogować się przy użyciu konta nuget.org utworzonego przy użyciu starszych wersji portalu.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![Lokalizacja logowania NuGet](media/publish_NuGetSignIn.png)

<span data-ttu-id="ed4fc-112">Następnie można przekazać pakiet za pośrednictwem nuget.org portalu sieci web, wypchnąć do nuget.org z `nuget.exe` wiersza polecenia (wymaga 4.1.0+) lub opublikować jako część procesu ciągłej integracji/ciągłego wdrażania za pośrednictwem usługi Azure DevOps, zgodnie z opisem w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Azure DevOps Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="ed4fc-113">Portal sieci Web: użyj karty Przekaż pakiet na nuget.org</span><span class="sxs-lookup"><span data-stu-id="ed4fc-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="ed4fc-114">Wybierz **pozycję Przekaż** w górnym menu nuget.org i przejdź do lokalizacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![Prześlij paczkę na nuget.org](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="ed4fc-116">nuget.org informuje, czy nazwa pakietu jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="ed4fc-117">Jeśli tak nie jest, zmień identyfikator pakietu w projekcie, odbuduj i spróbuj przekazać ponownie.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="ed4fc-118">Jeśli nazwa pakietu jest dostępna, nuget.org otwiera sekcję **Sprawdź,** w której można przejrzeć metadane z manifestu pakietu.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="ed4fc-119">Aby zmienić dowolny z metadanych, edytuj `.nuspec` projekt (plik projektu lub plik), odbuduj, ponownie stwórz pakiet i przekaż go ponownie.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-119">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="ed4fc-120">W obszarze **Dokumentacja importu** możesz wkleić markdown, wskazać dokumenty za pomocą adresu URL lub przekazać plik dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-120">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="ed4fc-121">Gdy wszystkie informacje będą gotowe, wybierz przycisk **Prześlij**</span><span class="sxs-lookup"><span data-stu-id="ed4fc-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="ed4fc-122">Wiersz polecenia</span><span class="sxs-lookup"><span data-stu-id="ed4fc-122">Command line</span></span>

<span data-ttu-id="ed4fc-123">Aby wypchnąć pakiety do nuget.org należy użyć [nuget.exe v4.1.0 lub wyższej](https://www.nuget.org/downloads), która implementuje wymagane [protokoły NuGet](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="ed4fc-123">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="ed4fc-124">Potrzebny jest również klucz interfejsu API, który jest tworzony na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-124">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="ed4fc-125">Tworzenie kluczy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="ed4fc-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="ed4fc-126">Publikuj z dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="ed4fc-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="ed4fc-127">Publikuj z nuget push</span><span class="sxs-lookup"><span data-stu-id="ed4fc-127">Publish with nuget push</span></span>

1. <span data-ttu-id="ed4fc-128">W wierszu polecenia uruchom następujące `<your_API_key>` polecenie, zastępując kluczem uzyskanym z nuget.org:</span><span class="sxs-lookup"><span data-stu-id="ed4fc-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="ed4fc-129">To polecenie przechowuje klucz interfejsu API w konfiguracji NuGet, dzięki czemu nie trzeba powtarzać tego kroku ponownie na tym samym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-129">This command stores your API key in your NuGet configuration so that you don't need to repeat this step again on the same computer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ed4fc-130">Klucz interfejsu API nie jest używany do uwierzytelniania za pomocą prywatnego kanału informacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-130">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="ed4fc-131">Zapoznaj się z [ `nuget sources` poleceniem,](../reference/cli-reference/cli-ref-sources.md) aby zarządzać poświadczeniami do uwierzytelniania ze źródłem.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-131">Refer to [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
    > <span data-ttu-id="ed4fc-132">Klucze interfejsu API można uzyskać z poszczególnych serwerów NuGet.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-132">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="ed4fc-133">Aby utworzyć i manange APIKeys dla nuget.org odnoszą się do [publish-api-key](../quickstart/includes/publish-api-key.md)</span><span class="sxs-lookup"><span data-stu-id="ed4fc-133">To create and manange APIKeys for nuget.org refer to [publish-api-key](../quickstart/includes/publish-api-key.md)</span></span>

1. <span data-ttu-id="ed4fc-134">Wypchnij pakiet do Galerii NuGet za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ed4fc-134">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a><span data-ttu-id="ed4fc-135">Publikowanie podpisanych pakietów</span><span class="sxs-lookup"><span data-stu-id="ed4fc-135">Publish signed packages</span></span>

<span data-ttu-id="ed4fc-136">Aby przesłać podpisane pakiety, należy najpierw [zarejestrować certyfikat](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) używany do podpisywania pakietów.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-136">To submit signed packages, you must first [register the certificate](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) used for signing the packages.</span></span> 

> [!Warning]
> <span data-ttu-id="ed4fc-137">nuget.org odrzuca pakiety, które nie spełniają [wymagań podpisanego pakietu.](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)</span><span class="sxs-lookup"><span data-stu-id="ed4fc-137">nuget.org rejects packages that don't satisfy the [signed package requirements](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span></span>

### <a name="package-validation-and-indexing"></a><span data-ttu-id="ed4fc-138">Sprawdzanie poprawności i indeksowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="ed4fc-138">Package validation and indexing</span></span>

<span data-ttu-id="ed4fc-139">Pakiety wypchnięte do nuget.org poddawane kilku weryfikacji, takich jak kontrole wirusów.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-139">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="ed4fc-140">(Wszystkie pakiety na nuget.org są okresowo skanowane).</span><span class="sxs-lookup"><span data-stu-id="ed4fc-140">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="ed4fc-141">Gdy pakiet przeszedł wszystkie sprawdzanie poprawności, może upłynąć trochę czasu, aby być indeksowane i pojawiają się w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-141">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="ed4fc-142">Po zakończeniu indeksowania otrzymasz wiadomość e-mail z potwierdzeniem pomyślnego opublikowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-142">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="ed4fc-143">Jeśli pakiet nie zostanie sprawdzony, strona szczegółów pakietu zostanie zaktualizowana, aby wyświetlić skojarzony błąd, a także otrzymasz wiadomość e-mail z powiadomieniem o tym.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-143">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="ed4fc-144">Sprawdzanie poprawności i indeksowanie pakietów zwykle trwa mniej niż 15 minut.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-144">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="ed4fc-145">Jeśli publikowanie pakietu trwa dłużej niż oczekiwano, odwiedź [status.nuget.org,](https://status.nuget.org/) aby sprawdzić, czy nuget.org występują przerwy.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-145">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="ed4fc-146">Jeśli wszystkie systemy działają, a pakiet nie został pomyślnie opublikowany w ciągu godziny, zaloguj się do nuget.org i skontaktuj się z nami za pomocą łącza Skontaktuj się z pomocą techniczną na stronie pakietu.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-146">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="ed4fc-147">Aby wyświetlić stan pakietu, wybierz pozycję **Zarządzaj pakietami** pod nazwą konta w nuget.org. Po zakończeniu sprawdzania poprawności otrzymasz wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-147">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="ed4fc-148">Należy pamiętać, że może upłynąć trochę czasu, aby pakiet został zindeksowany i pojawił się w wynikach wyszukiwania, gdzie inni mogą go znaleźć, w tym czasie na stronie pakietu może pojawić się następujący komunikat:</span><span class="sxs-lookup"><span data-stu-id="ed4fc-148">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Komunikat informujący, że pakiet nie został jeszcze opublikowany](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a><span data-ttu-id="ed4fc-150">Usługi DevOps platformy Azure (ci/cd)</span><span class="sxs-lookup"><span data-stu-id="ed4fc-150">Azure DevOps Services (CI/CD)</span></span>

<span data-ttu-id="ed4fc-151">Jeśli wypychasz pakiety do nuget.org przy użyciu usług Azure DevOps w `nuget.exe` ramach procesu ciągłej integracji/wdrażania, należy użyć 4.1 lub powyżej w zadaniach NuGet.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-151">If you push packages to nuget.org using Azure DevOps Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="ed4fc-152">Szczegóły można znaleźć na [korzystanie z najnowszego NuGet w kompilacji](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blogu).</span><span class="sxs-lookup"><span data-stu-id="ed4fc-152">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="ed4fc-153">Zarządzanie właścicielami pakietów na nuget.org</span><span class="sxs-lookup"><span data-stu-id="ed4fc-153">Managing package owners on nuget.org</span></span>

<span data-ttu-id="ed4fc-154">Mimo że `.nuspec` każdy plik pakietu NuGet definiuje autorów pakietu, nuget.org galeria nie używa tych metadanych do definiowania własności.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-154">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="ed4fc-155">Zamiast tego nuget.org przypisuje początkową własność osobie, która publikuje pakiet.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-155">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="ed4fc-156">Jest to zalogowany użytkownik, który przesłał pakiet za pośrednictwem nuget.org interfejsu użytkownika, lub użytkownicy, których klucz interfejsu API był używany z `nuget SetApiKey` lub `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-156">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="ed4fc-157">Wszyscy właściciele pakietów mają pełne uprawnienia do pakietu, w tym dodawanie i usuwanie innych właścicieli oraz publikowanie aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-157">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="ed4fc-158">Aby zmienić własność pakietu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ed4fc-158">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="ed4fc-159">Zaloguj się, aby nuget.org przy tym za pomocą konta, które jest bieżącym właścicielem pakietu.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-159">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="ed4fc-160">Wybierz nazwę swojego konta, wybierz pozycję **Zarządzaj pakietami**i rozwiń pozycję **Opublikowane pakiety**.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-160">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="ed4fc-161">Wybierz na opakowaniu, który chcesz zarządzać, a następnie po prawej stronie wybierz pozycję **Zarządzaj właścicielami**.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-161">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="ed4fc-162">W tym miejscu masz kilka opcji:</span><span class="sxs-lookup"><span data-stu-id="ed4fc-162">From here you have several options:</span></span>

1. <span data-ttu-id="ed4fc-163">Usuń dowolnego właściciela wymienionego w obszarze **Bieżąci właściciele**.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-163">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="ed4fc-164">Dodaj właściciela w obszarze **Dodaj właściciela,** wprowadzając jego nazwę użytkownika, wiadomość i wybierając **pozycję Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-164">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="ed4fc-165">Ta akcja wysyła wiadomość e-mail do tego nowego współwłaściciela z linkiem potwierdzającym.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-165">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="ed4fc-166">Po potwierdzeniu ta osoba ma pełne uprawnienia do dodawania i usuwania właścicieli.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-166">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="ed4fc-167">(Dopóki nie potwierdzono, sekcja **Obecni właściciele** wskazuje oczekujące zatwierdzenie dla tej osoby).</span><span class="sxs-lookup"><span data-stu-id="ed4fc-167">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="ed4fc-168">Aby przenieść własność (jak w przypadku zmiany własności lub pakiet został opublikowany na niewłaściwym koncie), dodaj nowego właściciela, a po potwierdzeniu własności mogą usunąć Cię z listy.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-168">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="ed4fc-169">Aby przypisać własność do firmy lub grupy, utwórz konto nuget.org przy użyciu aliasu e-mail, który jest przekazywał do odpowiednich członków zespołu.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-169">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="ed4fc-170">Na przykład różne pakiety Microsoft ASP.NET są współwłasnością kont [Microsoft](https://nuget.org/profiles/microsoft) i [Aspnet,](https://nuget.org/profiles/aspnet) które po prostu takie aliasy.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-170">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](https://nuget.org/profiles/microsoft) and [aspnet](https://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="ed4fc-171">Odzyskiwanie własności pakietu</span><span class="sxs-lookup"><span data-stu-id="ed4fc-171">Recovering package ownership</span></span>

<span data-ttu-id="ed4fc-172">Czasami pakiet może nie mieć aktywnego właściciela.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-172">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="ed4fc-173">Na przykład oryginalny właściciel może opuścić firmę, która produkuje pakiet, nuget.org poświadczenia są tracone lub wcześniejsze błędy w galerii pozostawił pakiet bez właściciela.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-173">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="ed4fc-174">Jeśli jesteś prawowitym właścicielem pakietu i trzeba odzyskać własność, użyj [formularza kontaktowego](https://www.nuget.org/policies/Contact) na nuget.org, aby wyjaśnić swoją sytuację do zespołu NuGet.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-174">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="ed4fc-175">Następnie śledzimy proces weryfikacji własności pakietu, w tym próbuje zlokalizować istniejącego właściciela za pośrednictwem adresu URL projektu pakietu, Twitter, e-mail lub w inny sposób.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-175">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="ed4fc-176">Ale jeśli wszystko inne zawiedzie, możemy wysłać ci nowe zaproszenie, aby stać się właścicielem.</span><span class="sxs-lookup"><span data-stu-id="ed4fc-176">But if all else fails, we can send you a new invite to become an owner.</span></span>
