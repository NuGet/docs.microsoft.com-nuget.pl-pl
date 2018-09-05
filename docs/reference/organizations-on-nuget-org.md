---
title: Organizacje w witrynie nuget.org
description: Organizacje w witrynie nuget.org ułatwia zarządzanie pakietami publikowane przez grupę lub w zespole, środowisko firmy.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: ea1ca607f169cd31c0a1b59d575d1a743763420c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551231"
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="a6121-103">Organizacji w witrynie nuget.org</span><span class="sxs-lookup"><span data-stu-id="a6121-103">Organization on nuget.org</span></span>

<span data-ttu-id="a6121-104">Organizacje umożliwiają firmom i projektów typu open source do współpracy nad pakietów przy użyciu tożsamości jednym nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a6121-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="a6121-105">Konsument pakietu konto organizacji wyświetlany jest taka sama jak istniejącego konta użytkownika w witrynie nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a6121-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="a6121-106">Konta użytkowników i kont organizacji</span><span class="sxs-lookup"><span data-stu-id="a6121-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="a6121-107">Twoje konto użytkownika jest swoją tożsamość w witrynie nuget.org i może należeć do dowolnej liczby organizacji.</span><span class="sxs-lookup"><span data-stu-id="a6121-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="a6121-108">Pakiet może należeć do organizacji, takich jak mogą należeć do konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a6121-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="a6121-109">Konsumentów pakietu nie jest widoczna różnica między kontem użytkownika lub konta organizacji: oba są wyświetlane jako pakiet `owners`.</span><span class="sxs-lookup"><span data-stu-id="a6121-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="a6121-110">Konto organizacji ma co najmniej jednego konta użytkownika jako elementy członkowskie.</span><span class="sxs-lookup"><span data-stu-id="a6121-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="a6121-111">Członkowie mogą zarządzać zestaw pakietów przy zachowaniu jednej tożsamości dla własności.</span><span class="sxs-lookup"><span data-stu-id="a6121-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="a6121-112">Dodawanie nowej organizacji</span><span class="sxs-lookup"><span data-stu-id="a6121-112">Adding a new organization</span></span>

<span data-ttu-id="a6121-113">Aby dodać nową organizację, wybierz swoje konto w witrynie nuget.org, a następnie wybierz **organizacjom zarządzanie...**  polecenia menu:</span><span class="sxs-lookup"><span data-stu-id="a6121-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Opcja menu w witrynie nuget.org dla organizacji Menedżera](media/org-manage-option.png)

<span data-ttu-id="a6121-115">Na następnej stronie wybierz **Dodaj nową organizację** przycisku:</span><span class="sxs-lookup"><span data-stu-id="a6121-115">On the next page, select the **Add new organization** button:</span></span>

![Przycisk, aby utworzyć nową organizację, w witrynie nuget.org](media/org-add-new-option.png)

<span data-ttu-id="a6121-117">Na następnej stronie Podaj adres nazwę i adres e-mail organizacji.</span><span class="sxs-lookup"><span data-stu-id="a6121-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="a6121-118">Ponieważ konta organizacji używają tej samej przestrzeni nazw jako konta użytkownika, nazwę organizacji musi być różni się od innych istniejących organizacji lub kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a6121-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="a6121-119">Adres e-mail również musi być unikatowa dla wszystkich kont.</span><span class="sxs-lookup"><span data-stu-id="a6121-119">The email address must also be unique across all accounts.</span></span>

![Dodaj nową stronę organizacji w witrynie nuget.org](media/org-add-new-page.png)

<span data-ttu-id="a6121-121">Po utworzeniu konta organizacji, możesz jesteś administratorem i przesłać pakiety do organizacji i dodać członków organizacji.</span><span class="sxs-lookup"><span data-stu-id="a6121-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="a6121-122">Przekształcanie istniejące konto organizacji</span><span class="sxs-lookup"><span data-stu-id="a6121-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="a6121-123">Konwersja konta jest nieodwracalne: nie można przekształcić organizacji do konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a6121-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="a6121-124">Jeśli pakiety zarządzania jako zespół przy użyciu jednego konta użytkownika, a chcesz przekonwertować to konto do organizacji, użyj **Przekształć swoje konto, aby organizacja** opcja **organizacjom zarządzanie** strony:</span><span class="sxs-lookup"><span data-stu-id="a6121-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Opcja w witrynie nuget.org do przekształcania istniejącego konta do organizacji](media/org-transform-option.png)

<span data-ttu-id="a6121-126">Na następnej stronie podaj inne konto użytkownika można przypisać jako administrator w organizacji, a następnie wybierz **Przekształcanie**.</span><span class="sxs-lookup"><span data-stu-id="a6121-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Wprowadzanie informacji do przekształcania konto użytkownika w organizacji](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="a6121-128">Zarządzanie członkami organizacji</span><span class="sxs-lookup"><span data-stu-id="a6121-128">Managing organization members</span></span>

<span data-ttu-id="a6121-129">Jako administrator organizacji, możesz dodawać członków, podając adres nuget.org każdy element członkowski *nazwę konta użytkownika*; nie można używać adresów e-mail.</span><span class="sxs-lookup"><span data-stu-id="a6121-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="a6121-130">Następnie oznacz każdy element członkowski jako współpracownika lub administrator z następującymi uprawnieniami:</span><span class="sxs-lookup"><span data-stu-id="a6121-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="a6121-131">Uprawnienie</span><span class="sxs-lookup"><span data-stu-id="a6121-131">Permission</span></span> | <span data-ttu-id="a6121-132">Współautor</span><span class="sxs-lookup"><span data-stu-id="a6121-132">Collaborator</span></span> | <span data-ttu-id="a6121-133">Administrator</span><span class="sxs-lookup"><span data-stu-id="a6121-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a6121-134">Zarządzanie pakietami w organizacji</span><span class="sxs-lookup"><span data-stu-id="a6121-134">Manage the organization's packages</span></span><br/><span data-ttu-id="a6121-135">(przesyłanie nowych pakietów, aktualizacji lub wyrejestrowanie istniejących pakietów)</span><span class="sxs-lookup"><span data-stu-id="a6121-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="a6121-136">Tak</span><span class="sxs-lookup"><span data-stu-id="a6121-136">Yes</span></span> | <span data-ttu-id="a6121-137">Tak</span><span class="sxs-lookup"><span data-stu-id="a6121-137">Yes</span></span> |
| <span data-ttu-id="a6121-138">Zmiana organizacji metadanych</span><span class="sxs-lookup"><span data-stu-id="a6121-138">Change organization metadata</span></span><br/><span data-ttu-id="a6121-139">(adres e-mail, ustawienia powiadomień)</span><span class="sxs-lookup"><span data-stu-id="a6121-139">(email address, notification settings)</span></span> | <span data-ttu-id="a6121-140">Nie</span><span class="sxs-lookup"><span data-stu-id="a6121-140">No</span></span> | <span data-ttu-id="a6121-141">Tak</span><span class="sxs-lookup"><span data-stu-id="a6121-141">Yes</span></span> |
| <span data-ttu-id="a6121-142">Zarządzanie członkami organizacji</span><span class="sxs-lookup"><span data-stu-id="a6121-142">Manage organization members</span></span> | <span data-ttu-id="a6121-143">Nie</span><span class="sxs-lookup"><span data-stu-id="a6121-143">No</span></span> | <span data-ttu-id="a6121-144">Tak</span><span class="sxs-lookup"><span data-stu-id="a6121-144">Yes</span></span> |
| <span data-ttu-id="a6121-145">Żądania lub reagowanie na żądania co-ownership pakietów organizacji</span><span class="sxs-lookup"><span data-stu-id="a6121-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="a6121-146">Nie</span><span class="sxs-lookup"><span data-stu-id="a6121-146">No</span></span> | <span data-ttu-id="a6121-147">Tak</span><span class="sxs-lookup"><span data-stu-id="a6121-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="a6121-148">Zarządzanie pakietami</span><span class="sxs-lookup"><span data-stu-id="a6121-148">Managing packages</span></span>

<span data-ttu-id="a6121-149">Wszystkie pakiety można wyświetlić na swoje konto i wszystkie organizacje, których jesteś członkiem na [Zarządzanie pakietami](https://www.nuget.org/account/Packages) strony.</span><span class="sxs-lookup"><span data-stu-id="a6121-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="a6121-150">Aby wyświetlić te pakiety, które są specyficzne dla swojego konta lub wszelkich konkretnej organizacji, użyj filtru kont w górnym rogu strony.</span><span class="sxs-lookup"><span data-stu-id="a6121-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Zarządzanie pakietami za pomocą filtru konta](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="a6121-152">Przenoszenie pakietów do organizacji</span><span class="sxs-lookup"><span data-stu-id="a6121-152">Transferring packages to an organization</span></span>
<span data-ttu-id="a6121-153">Jeśli chcesz przenieść niektórych pakietów do nowo utworzonego organizacji, możesz to zrobić, żądania konta organizacji do współwłaścicielami pakietu, a następnie usuwając siebie jako właściciela.</span><span class="sxs-lookup"><span data-stu-id="a6121-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="a6121-154">Jeśli jesteś administratorem w organizacji, jest Brak potwierdzenia zaakceptowanie własność.</span><span class="sxs-lookup"><span data-stu-id="a6121-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="a6121-155">Jeśli jesteś współpracownika, dodawanie organizacji jako właściciel wymaga jednak jeden z administratorów, aby zaakceptować własność.</span><span class="sxs-lookup"><span data-stu-id="a6121-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="a6121-156">Publikowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="a6121-156">Publishing packages</span></span>

<span data-ttu-id="a6121-157">Publikowanie pakietów dla organizacji, takich jak publikowanie pakietów do konta użytkownika: bezpośrednie przekazanie pakietu na stronie nuget.org lub wypychając pakiet za pośrednictwem `nuget push` lub `dotnet nuget push` poleceń interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="a6121-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="a6121-158">Przekazywanie pakietów</span><span class="sxs-lookup"><span data-stu-id="a6121-158">Uploading packages</span></span>

<span data-ttu-id="a6121-159">Gdy możesz bezpośrednio przekazać nowy pakiet na [nuget.org przekazywania](https://www.nuget.org/packages/manage/upload) stronie przypisujesz właściciel pakietu do użytkownika lub konta organizacji:</span><span class="sxs-lookup"><span data-stu-id="a6121-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Przekaż pakiet za pomocą opcji konta](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="a6121-161">Przy użyciu kluczy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="a6121-161">Using API keys</span></span>

<span data-ttu-id="a6121-162">Aby wypchnąć pakiet za pośrednictwem `nuget push` lub `dotnet nuget push` poleceń interfejsu wiersza polecenia, należy uzyskać klucz interfejsu API wymagane przez tych poleceń.</span><span class="sxs-lookup"><span data-stu-id="a6121-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="a6121-163">Aby uzyskać więcej informacji, zobacz [publikowanie pakietu](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="a6121-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="a6121-164">Podczas tworzenia nowego klucza interfejsu API, wybierz odpowiednie organizacji w **właścicielem pakietu** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="a6121-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="a6121-165">Dowolny klucz interfejsu API, które możesz utworzyć ma zastosowanie tylko do wybranych organizacji:</span><span class="sxs-lookup"><span data-stu-id="a6121-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Klucz interfejsu API za pomocą opcji konta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="a6121-167">Usuwanie organizacji</span><span class="sxs-lookup"><span data-stu-id="a6121-167">Removing an organization</span></span>

<span data-ttu-id="a6121-168">Jako użytkownik, możesz usunąć siebie z organizacji, wybierając `X` przycisk wyświetlane przez członkostwo w Twojej organizacji:</span><span class="sxs-lookup"><span data-stu-id="a6121-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![Usuwanie konta użytkownika z organizacji](media/org-remove-self-option.png)

<span data-ttu-id="a6121-170">Administratorzy mogą usuwać dowolnego elementu członkowskiego z organizacji, w tym innych administratorów.</span><span class="sxs-lookup"><span data-stu-id="a6121-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="a6121-171">Jeśli jesteś jedynym administratorem w organizacji, nie możesz usunąć siebie chyba że dodasz inny użytkownik z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="a6121-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="a6121-172">Trwa usuwanie konta organizacji</span><span class="sxs-lookup"><span data-stu-id="a6121-172">Deleting an organization account</span></span>

<span data-ttu-id="a6121-173">Ta funkcja będzie dostępna wkrótce.</span><span class="sxs-lookup"><span data-stu-id="a6121-173">This feature is coming soon.</span></span>
