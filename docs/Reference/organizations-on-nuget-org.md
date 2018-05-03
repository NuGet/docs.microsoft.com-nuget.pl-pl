---
title: Organizacje na nuget.org
description: Organizacje na nuget.org pomaga w zakresie zarządzania pakietami opublikowane przez grupę lub w zespole, środowisko firmy.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 0e836f5f39620f0b83212c9510735481119ddda2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="e2b0b-103">Organizacji na nuget.org</span><span class="sxs-lookup"><span data-stu-id="e2b0b-103">Organization on nuget.org</span></span>

<span data-ttu-id="e2b0b-104">Organizacje włączyć w firmach i open source projekty, współpracować nad pakiety przy użyciu tożsamości jednym nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="e2b0b-105">Konsument pakietu konta organizacji wyświetlany jest taki sam jak istniejącego konta użytkownika na nuget.org.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="e2b0b-106">Konta użytkowników, a konta organizacji</span><span class="sxs-lookup"><span data-stu-id="e2b0b-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="e2b0b-107">Twoje konto użytkownika jest Twoją tożsamość na nuget.org i może być członkiem dowolnej liczby organizacji.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="e2b0b-108">Pakiet może należeć do konta organizacji, jak mogą należeć do konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="e2b0b-109">Pakiet nie widzieli różnicę między konta użytkownika lub konta organizacji: znajdować się w pakiecie `owners`.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="e2b0b-110">Konta organizacji ma co najmniej jednego konta użytkowników jako elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="e2b0b-111">Elementy te można zarządzać zestaw pakietów przy zachowaniu jednej tożsamości dla prawa własności.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="e2b0b-112">Dodawanie nowej organizacji</span><span class="sxs-lookup"><span data-stu-id="e2b0b-112">Adding a new organization</span></span>

<span data-ttu-id="e2b0b-113">Aby dodać nową organizację, wybierz konto na nuget.org, a następnie wybierz **zarządzanie organizacji...**  polecenie:</span><span class="sxs-lookup"><span data-stu-id="e2b0b-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Opcja menu na nuget.org dla organizacji Manager](media/org-manage-option.png)

<span data-ttu-id="e2b0b-115">Na następnej stronie wybierz **Dodaj nową organizację** przycisk:</span><span class="sxs-lookup"><span data-stu-id="e2b0b-115">On the next page, select the **Add new organization** button:</span></span>

![Przycisk, aby utworzyć nową organizację na nuget.org](media/org-add-new-option.png)

<span data-ttu-id="e2b0b-117">Na następnej stronie Podaj adres nazwę i adres e-mail organizacji.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="e2b0b-118">Ponieważ konta organizacji używają tego samego obszaru nazw jako konta użytkownika, nazwę organizacji musi się różnić od innych istniejącą organizację lub kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="e2b0b-119">Adres e-mail musi być unikatowa również we wszystkich kont.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-119">The email address must also be unique across all accounts.</span></span>

![Dodaj nową stronę organizacji na nuget.org](media/org-add-new-page.png)

<span data-ttu-id="e2b0b-121">Po utworzeniu konta organizacji jest administratorem i można przesłać pakiety do organizacji i dodać członków organizacji.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="e2b0b-122">Przekształcanie istniejącego konta organizacji</span><span class="sxs-lookup"><span data-stu-id="e2b0b-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="e2b0b-123">Konwersja konta jest nieodwracalne: nie można przekształcić organizacji do konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="e2b0b-124">Jeśli w przypadku zarządzania pakietami w zespole za pomocą jednego konta użytkownika, a chcesz konwertować tego konta organizacji, użyj **Przekształcenie konta organizacji** opcja **zarządzanie organizacji** strony:</span><span class="sxs-lookup"><span data-stu-id="e2b0b-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Opcja na nuget.org do przekształcania istniejącego konta organizacji](media/org-transform-option.png)

<span data-ttu-id="e2b0b-126">Na następnej stronie podaj inne konto użytkownika do przypisania jako administrator w organizacji, a następnie wybierz **przekształcenie**.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Wprowadzanie informacji do przekształcania konto użytkownika w organizacji](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="e2b0b-128">Zarządzanie członków organizacji</span><span class="sxs-lookup"><span data-stu-id="e2b0b-128">Managing organization members</span></span>

<span data-ttu-id="e2b0b-129">Jako administrator w organizacji, możesz dodawać członków, zapewniając nuget.org każdy element członkowski *nazwę konta użytkownika*; nie można używać adresów e-mail.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="e2b0b-130">Następnie oznaczenie każdy element członkowski jako współautor lub administrator z następującymi uprawnieniami:</span><span class="sxs-lookup"><span data-stu-id="e2b0b-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="e2b0b-131">Uprawnienie</span><span class="sxs-lookup"><span data-stu-id="e2b0b-131">Permission</span></span> | <span data-ttu-id="e2b0b-132">Współautor</span><span class="sxs-lookup"><span data-stu-id="e2b0b-132">Collaborator</span></span> | <span data-ttu-id="e2b0b-133">Administrator</span><span class="sxs-lookup"><span data-stu-id="e2b0b-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2b0b-134">Zarządzaj pakietami organizacji</span><span class="sxs-lookup"><span data-stu-id="e2b0b-134">Manage the organization's packages</span></span><br/><span data-ttu-id="e2b0b-135">(przesyłanie nowych pakietów, aktualizacji lub unlist istniejące pakiety)</span><span class="sxs-lookup"><span data-stu-id="e2b0b-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="e2b0b-136">Tak</span><span class="sxs-lookup"><span data-stu-id="e2b0b-136">Yes</span></span> | <span data-ttu-id="e2b0b-137">Tak</span><span class="sxs-lookup"><span data-stu-id="e2b0b-137">Yes</span></span> |
| <span data-ttu-id="e2b0b-138">Zmiana metadanych organizacji</span><span class="sxs-lookup"><span data-stu-id="e2b0b-138">Change organization metadata</span></span><br/><span data-ttu-id="e2b0b-139">(adres e-mail, ustawienia powiadomień)</span><span class="sxs-lookup"><span data-stu-id="e2b0b-139">(email address, notification settings)</span></span> | <span data-ttu-id="e2b0b-140">Nie</span><span class="sxs-lookup"><span data-stu-id="e2b0b-140">No</span></span> | <span data-ttu-id="e2b0b-141">Tak</span><span class="sxs-lookup"><span data-stu-id="e2b0b-141">Yes</span></span> |
| <span data-ttu-id="e2b0b-142">Zarządzanie członków organizacji</span><span class="sxs-lookup"><span data-stu-id="e2b0b-142">Manage organization members</span></span> | <span data-ttu-id="e2b0b-143">Nie</span><span class="sxs-lookup"><span data-stu-id="e2b0b-143">No</span></span> | <span data-ttu-id="e2b0b-144">Tak</span><span class="sxs-lookup"><span data-stu-id="e2b0b-144">Yes</span></span> |
| <span data-ttu-id="e2b0b-145">Żądanie lub działać w odpowiedzi na żądania co-ownership pakietów organizacji</span><span class="sxs-lookup"><span data-stu-id="e2b0b-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="e2b0b-146">Nie</span><span class="sxs-lookup"><span data-stu-id="e2b0b-146">No</span></span> | <span data-ttu-id="e2b0b-147">Tak</span><span class="sxs-lookup"><span data-stu-id="e2b0b-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="e2b0b-148">Zarządzanie pakietami</span><span class="sxs-lookup"><span data-stu-id="e2b0b-148">Managing packages</span></span>

<span data-ttu-id="e2b0b-149">Wszystkie pakiety można wyświetlić na Twoje konto i wszystkich organizacji, w których jesteś członkiem na [Zarządzaj pakietami](https://www.nuget.org/account/Packages) strony.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="e2b0b-150">Aby wyświetlić specyficzne dla swojego konta lub dowolnego organizację określonych pakietów, użyj filtru konta u góry po prawej części strony.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Zarządzanie pakietami z filtrem konta](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="e2b0b-152">Transferu pakietów do organizacji</span><span class="sxs-lookup"><span data-stu-id="e2b0b-152">Transferring packages to an organization</span></span>
<span data-ttu-id="e2b0b-153">Jeśli chcesz przenieść niektórych pakietów do nowo utworzonej organizacji, możesz to zrobić przez żądania konta organizacji, aby wspólnie właścicielem pakietu i usuwanie siebie jako właściciela.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="e2b0b-154">Jeśli jesteś administratorem organizacji nie ma żadnych potwierdzenie, należy zaakceptować własności.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="e2b0b-155">Jednak w przypadku współpracownika dodawania organizacji jako właściciela wymaga jednego z administratorami w celu akceptowania własności.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="e2b0b-156">Publikowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="e2b0b-156">Publishing packages</span></span>

<span data-ttu-id="e2b0b-157">Publikuj pakiety w organizacji, takich jak opublikować pakietów z kontem użytkownika: przekazując bezpośrednio pakietu do nuget.org lub przesyłając pakietu za pomocą `nuget push` lub `dotnet nuget push` polecenia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="e2b0b-158">Przekazywanie pakietów</span><span class="sxs-lookup"><span data-stu-id="e2b0b-158">Uploading packages</span></span>

<span data-ttu-id="e2b0b-159">Jeśli możesz bezpośrednio przekazać nowy pakiet na [nuget.org przekazywania](https://www.nuget.org/packages/manage/upload) strony, możesz przypisać właściciela pakietu na konto użytkownika lub organizację:</span><span class="sxs-lookup"><span data-stu-id="e2b0b-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Przekaż pakiet z opcją konta](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="e2b0b-161">Przy użyciu kluczy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="e2b0b-161">Using API keys</span></span>

<span data-ttu-id="e2b0b-162">Do dystrybuowania pakietu za pomocą `nuget push` lub `dotnet nuget push` polecenia interfejsu wiersza polecenia, należy uzyskać klucz interfejsu API wymagane przez tych poleceń.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="e2b0b-163">Aby uzyskać więcej informacji, zobacz [opublikowania pakietu](https://docs.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-visual-studio#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="e2b0b-163">For details, see [Publish a package](https://docs.microsoft.com/en-us/nuget/quickstart/create-and-publish-a-package-using-visual-studio#publish-the-package).</span></span>

<span data-ttu-id="e2b0b-164">Podczas tworzenia nowego klucza interfejsu API, wybierz odpowiednie organizacji w **właściciela pakietu** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="e2b0b-165">Klucz interfejsu API, wszystkie utworzone ma zastosowanie tylko do wybranych organizacji:</span><span class="sxs-lookup"><span data-stu-id="e2b0b-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Klucz interfejsu API z opcji konta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="e2b0b-167">Usuwanie organizacji</span><span class="sxs-lookup"><span data-stu-id="e2b0b-167">Removing an organization</span></span>

<span data-ttu-id="e2b0b-168">Jako użytkownik, możesz usunąć siebie z organizacji, wybierając `X` przycisk wyświetlane przez członkostwo w danej organizacji:</span><span class="sxs-lookup"><span data-stu-id="e2b0b-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![Usuwanie konta użytkownika z organizacji](media/org-remove-self-option.png)

<span data-ttu-id="e2b0b-170">Administratorzy mogą usunąć członków z organizacji, w tym innych administratorów.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="e2b0b-171">Jeśli jesteś jedynym administratorem dla organizacji, nie możesz usunąć siebie, chyba że dodasz innego elementu członkowskiego jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="e2b0b-172">Usunięcie konta organizacji</span><span class="sxs-lookup"><span data-stu-id="e2b0b-172">Deleting an organization account</span></span>

<span data-ttu-id="e2b0b-173">Ta funkcja będzie dostępna wkrótce.</span><span class="sxs-lookup"><span data-stu-id="e2b0b-173">This feature is coming soon.</span></span>
