---
title: Twoja organizacja na NuGet.org
description: Organizacje na NuGet.org pomaga zarządzać pakietami publikowanych przez grupę lub w środowisku zespołowym, firmowym.
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427540"
---
# <a name="your-organization-on-nugetorg"></a><span data-ttu-id="39f0d-103">Twoja organizacja na NuGet.org</span><span class="sxs-lookup"><span data-stu-id="39f0d-103">Your organization on NuGet.org</span></span>

<span data-ttu-id="39f0d-104">Organizacje umożliwiają firmom i projektom typu open source współpracę nad pakietami przy użyciu jednej NuGet.org tożsamości.</span><span class="sxs-lookup"><span data-stu-id="39f0d-104">Organizations enable businesses and open-source projects to collaborate on packages using a single NuGet.org identity.</span></span> <span data-ttu-id="39f0d-105">W przypadku konsumenta pakietu konto organizacji jest takie samo jak istniejące konto użytkownika w NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="39f0d-105">For a package consumer, an organization account appears same as an existing user account on NuGet.org.</span></span>

## <a name="organization-accounts-vs-individual-accounts"></a><span data-ttu-id="39f0d-106">Konta organizacji a konta indywidualne</span><span class="sxs-lookup"><span data-stu-id="39f0d-106">Organization accounts vs. individual accounts</span></span>

<span data-ttu-id="39f0d-107">Konto organizacji ma co najmniej jedno konto indywidualne (użytkownika) jako jego członków.</span><span class="sxs-lookup"><span data-stu-id="39f0d-107">An organization account has one or more individual (user) accounts as its members.</span></span> <span data-ttu-id="39f0d-108">Te elementy członkowskie mogą zarządzać zestawem pakietów przy zachowaniu jednej tożsamości dla własności.</span><span class="sxs-lookup"><span data-stu-id="39f0d-108">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

<span data-ttu-id="39f0d-109">Twoje indywidualne konto jest Twoją tożsamością w NuGet.org i może być członkiem dowolnej liczby organizacji.</span><span class="sxs-lookup"><span data-stu-id="39f0d-109">Your individual account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="39f0d-110">Pakiet może należeć do konta organizacji, tak jak może należeć do indywidualnego konta.</span><span class="sxs-lookup"><span data-stu-id="39f0d-110">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="39f0d-111">Konsumenci pakietów nie widzą żadnej różnicy między kontem indywidualnym `owners`lub kontem organizacji: oba są wyświetlane jako pakiet.</span><span class="sxs-lookup"><span data-stu-id="39f0d-111">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="39f0d-112">Dodawanie nowej organizacji</span><span class="sxs-lookup"><span data-stu-id="39f0d-112">Adding a new organization</span></span>

<span data-ttu-id="39f0d-113">Aby dodać nową organizację, wybierz swoje konto w NuGet.org, a następnie wybierz polecenie menu **Zarządzaj organizacjami...:**</span><span class="sxs-lookup"><span data-stu-id="39f0d-113">To add a new organization, select your account on NuGet.org, then select the **Manage Organizations...** menu command:</span></span>

![Opcja menu w NuGet.org dla organizacji menedżera](media/org-manage-option.png)

<span data-ttu-id="39f0d-115">Na następnej stronie wybierz przycisk **Dodaj nową organizację:**</span><span class="sxs-lookup"><span data-stu-id="39f0d-115">On the next page, select the **Add new organization** button:</span></span>

![Przycisk, aby utworzyć nową organizację na NuGet.org](media/org-add-new-option.png)

<span data-ttu-id="39f0d-117">Na następnej stronie podaj nazwę organizacji i adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="39f0d-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="39f0d-118">Ponieważ konta organizacji mają ten sam obszar nazw co konta użytkowników, nazwa organizacji musi się różnić od innych istniejących kont organizacji lub użytkowników.</span><span class="sxs-lookup"><span data-stu-id="39f0d-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="39f0d-119">Adres e-mail musi być również unikatowy na wszystkich kontach.</span><span class="sxs-lookup"><span data-stu-id="39f0d-119">The email address must also be unique across all accounts.</span></span>

![Dodawanie nowej strony organizacji w NuGet.org](media/org-add-new-page.png)

<span data-ttu-id="39f0d-121">Po utworzeniu konta instytucji jesteś administratorem i możesz przesyłać pakiety dla instytucji i dodawać członków instytucji.</span><span class="sxs-lookup"><span data-stu-id="39f0d-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="39f0d-122">Przekształcanie istniejącego konta w organizację</span><span class="sxs-lookup"><span data-stu-id="39f0d-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="39f0d-123">Konwersja konta jest nieodwracalna: nie można przekształcić organizacji z powrotem w konto użytkownika.</span><span class="sxs-lookup"><span data-stu-id="39f0d-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="39f0d-124">Jeśli zarządzasz pakietami jako zespół przy użyciu jednego konta użytkownika i chcesz przekonwertować je na organizację, użyj opcji **Przekształć swoje konto** w organizację na stronie **Zarządzanie organizacjami:**</span><span class="sxs-lookup"><span data-stu-id="39f0d-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Opcja NuGet.org, aby przekształcić istniejące konto w organizację](media/org-transform-option.png)

<span data-ttu-id="39f0d-126">Na następnej stronie określ inne konto użytkownika, które ma zostać przypisane jako administrator organizacji, a następnie wybierz pozycję **Przekształć**.</span><span class="sxs-lookup"><span data-stu-id="39f0d-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![Wprowadzanie informacji dotyczących przekształcania konta użytkownika w organizację](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="39f0d-128">Zarządzanie członkami instytucji</span><span class="sxs-lookup"><span data-stu-id="39f0d-128">Managing organization members</span></span>

<span data-ttu-id="39f0d-129">Jako administrator organizacji możesz dodawać członków, podając nazwę *konta użytkownika*NuGet.org każdego członka; nie można używać adresów e-mail.</span><span class="sxs-lookup"><span data-stu-id="39f0d-129">As the organization administrator, you can add members by providing each member's NuGet.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="39f0d-130">Następnie każdy członek oznacza jako współpracownika lub administratora z następującymi uprawnieniami:</span><span class="sxs-lookup"><span data-stu-id="39f0d-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="39f0d-131">Uprawnienie</span><span class="sxs-lookup"><span data-stu-id="39f0d-131">Permission</span></span> | <span data-ttu-id="39f0d-132">Współpracownik</span><span class="sxs-lookup"><span data-stu-id="39f0d-132">Collaborator</span></span> | <span data-ttu-id="39f0d-133">Administrator</span><span class="sxs-lookup"><span data-stu-id="39f0d-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39f0d-134">Zarządzanie pakietami organizacji</span><span class="sxs-lookup"><span data-stu-id="39f0d-134">Manage the organization's packages</span></span><br/><span data-ttu-id="39f0d-135">(przesyłać nowe pakiety, aktualizować lub wystawić istniejące pakiety)</span><span class="sxs-lookup"><span data-stu-id="39f0d-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="39f0d-136">Tak</span><span class="sxs-lookup"><span data-stu-id="39f0d-136">Yes</span></span> | <span data-ttu-id="39f0d-137">Tak</span><span class="sxs-lookup"><span data-stu-id="39f0d-137">Yes</span></span> |
| <span data-ttu-id="39f0d-138">Zmienianie metadanych organizacji</span><span class="sxs-lookup"><span data-stu-id="39f0d-138">Change organization metadata</span></span><br/><span data-ttu-id="39f0d-139">(adres e-mail, ustawienia powiadomień)</span><span class="sxs-lookup"><span data-stu-id="39f0d-139">(email address, notification settings)</span></span> | <span data-ttu-id="39f0d-140">Nie</span><span class="sxs-lookup"><span data-stu-id="39f0d-140">No</span></span> | <span data-ttu-id="39f0d-141">Tak</span><span class="sxs-lookup"><span data-stu-id="39f0d-141">Yes</span></span> |
| <span data-ttu-id="39f0d-142">Zarządzanie członkami instytucji</span><span class="sxs-lookup"><span data-stu-id="39f0d-142">Manage organization members</span></span> | <span data-ttu-id="39f0d-143">Nie</span><span class="sxs-lookup"><span data-stu-id="39f0d-143">No</span></span> | <span data-ttu-id="39f0d-144">Tak</span><span class="sxs-lookup"><span data-stu-id="39f0d-144">Yes</span></span> |
| <span data-ttu-id="39f0d-145">Żądanie lub działanie w sprawie żądań współwłasności dla pakietów organizacji</span><span class="sxs-lookup"><span data-stu-id="39f0d-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="39f0d-146">Nie</span><span class="sxs-lookup"><span data-stu-id="39f0d-146">No</span></span> | <span data-ttu-id="39f0d-147">Tak</span><span class="sxs-lookup"><span data-stu-id="39f0d-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="39f0d-148">Zarządzanie pakietami</span><span class="sxs-lookup"><span data-stu-id="39f0d-148">Managing packages</span></span>

<span data-ttu-id="39f0d-149">Możesz wyświetlić wszystkie pakiety na swoim koncie i we wszystkich organizacjach, których jesteś członkiem, na stronie [Zarządzanie pakietami.](https://www.nuget.org/account/Packages)</span><span class="sxs-lookup"><span data-stu-id="39f0d-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="39f0d-150">Aby wyświetlić pakiety specyficzne dla Twojego konta lub określonej organizacji, użyj filtru kont w prawym górnym rogu strony.</span><span class="sxs-lookup"><span data-stu-id="39f0d-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![Zarządzanie pakietami za pomocą filtru konta](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="39f0d-152">Przenoszenie pakietów do organizacji</span><span class="sxs-lookup"><span data-stu-id="39f0d-152">Transferring packages to an organization</span></span>
<span data-ttu-id="39f0d-153">Jeśli chcesz przenieść niektóre pakiety do nowo utworzonej organizacji, możesz to zrobić, żądając od konta organizacji współwłasnego pakietu, a następnie usuwając siebie jako właściciela.</span><span class="sxs-lookup"><span data-stu-id="39f0d-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="39f0d-154">Jeśli jesteś administratorem organizacji, nie ma potwierdzenia wymaganego do zaakceptowania własności.</span><span class="sxs-lookup"><span data-stu-id="39f0d-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="39f0d-155">Jeśli jednak jesteś współpracownikiem, dodanie organizacji jako właściciela wymaga od jednego z administratorów zaakceptowania własności.</span><span class="sxs-lookup"><span data-stu-id="39f0d-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="39f0d-156">Publikowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="39f0d-156">Publishing packages</span></span>

<span data-ttu-id="39f0d-157">Publikujesz pakiety w organizacji, takiej jak publikowanie pakietów na konto użytkownika: przesyłając bezpośrednio pakiet `nuget push` do `dotnet nuget push` NuGet.org lub wypychając pakiet za pomocą poleceń lub interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="39f0d-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to NuGet.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="39f0d-158">Przesyłanie pakietów</span><span class="sxs-lookup"><span data-stu-id="39f0d-158">Uploading packages</span></span>

<span data-ttu-id="39f0d-159">Podczas bezpośredniego przekazywania nowego pakietu na stronie [przekazywania NuGet.org](https://www.nuget.org/packages/manage/upload) właściciel pakietu jest przypisywany do konta użytkownika lub organizacji:</span><span class="sxs-lookup"><span data-stu-id="39f0d-159">When you directly upload a new package on the [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![Przekaż pakiet z opcją konta](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="39f0d-161">Korzystanie z kluczy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="39f0d-161">Using API keys</span></span>

<span data-ttu-id="39f0d-162">Aby wypchnąć `nuget push` pakiet `dotnet nuget push` za pośrednictwem poleceń lub interfejsu wiersza polecenia, należy uzyskać klucz interfejsu API wymagany przez te polecenia.</span><span class="sxs-lookup"><span data-stu-id="39f0d-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="39f0d-163">Aby uzyskać szczegółowe informacje, zobacz [Publikowanie pakietu](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span><span class="sxs-lookup"><span data-stu-id="39f0d-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="39f0d-164">Podczas tworzenia nowego klucza interfejsu API wybierz odpowiednią organizację w rozwijanej właściciel **pakietu.**</span><span class="sxs-lookup"><span data-stu-id="39f0d-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="39f0d-165">Każdy utworzony klucz interfejsu API ma zastosowanie tylko do wybranej organizacji:</span><span class="sxs-lookup"><span data-stu-id="39f0d-165">Any API key you create is applicable only to the chosen organization:</span></span>

![Klucz interfejsu API z opcją konta](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="39f0d-167">Usuwanie organizacji</span><span class="sxs-lookup"><span data-stu-id="39f0d-167">Removing an organization</span></span>

<span data-ttu-id="39f0d-168">Jako użytkownik możesz usunąć siebie z organizacji, wybierając przycisk **X** wyświetlany przez członkostwo w organizacji:</span><span class="sxs-lookup"><span data-stu-id="39f0d-168">As a user, you can remove yourself from an organization by selecting the **X** button shown by your organization membership:</span></span>

![Usuwanie konta użytkownika z instytucji](media/org-remove-self-option.png)

<span data-ttu-id="39f0d-170">Administratorzy mogą usuwać dowolnego członka instytucji, w tym innych administratorów.</span><span class="sxs-lookup"><span data-stu-id="39f0d-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="39f0d-171">Jeśli jesteś jedynym administratorem organizacji, nie możesz usunąć siebie, chyba że dodasz innego członka jako administratora.</span><span class="sxs-lookup"><span data-stu-id="39f0d-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="39f0d-172">Usuwanie konta instytucji</span><span class="sxs-lookup"><span data-stu-id="39f0d-172">Deleting an organization account</span></span>

<span data-ttu-id="39f0d-173">Konto organizacji można usunąć, klikając przycisk **Usuń** wyświetlany na stronie organizacji.</span><span class="sxs-lookup"><span data-stu-id="39f0d-173">You can delete an organization account by clicking the **Delete** button shown in your organization page.</span></span>

![Usuwanie organizacji](media/org-delete-option.png)

<span data-ttu-id="39f0d-175">Aby usunąć organizatora, należy go potwierdzić, klikając przycisk Usuń potwierdzenie **organizacji.**</span><span class="sxs-lookup"><span data-stu-id="39f0d-175">To delete the organizaiton, you must confirm it by clicking the **Delete organization** confirmation button.</span></span>
