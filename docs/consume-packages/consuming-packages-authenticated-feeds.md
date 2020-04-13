---
title: Korzystanie z pakietów z uwierzytelnionych kanałów informacyjnych
description: Korzystanie z pakietów z uwierzytelnionych kanałów informacyjnych we wszystkich scenariuszach klienta NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231792"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="77624-103">Korzystanie z pakietów z uwierzytelnionych kanałów informacyjnych</span><span class="sxs-lookup"><span data-stu-id="77624-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="77624-104">Oprócz nuget.org [publicznych kanałów informacyjnych,](https://api.nuget.org/v3/index.json)klienci NuGet mają możliwość interakcji z plikami danych i prywatnymi źródłami http.</span><span class="sxs-lookup"><span data-stu-id="77624-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="77624-105">Aby uwierzytelnić się za pomocą prywatnych kanałów http, 2 podejścia są:</span><span class="sxs-lookup"><span data-stu-id="77624-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="77624-106">Dodawanie poświadczeń w pliku [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span><span class="sxs-lookup"><span data-stu-id="77624-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="77624-107">Uwierzytelnij się przy użyciu jednego z wielu modeli rozszerzalności w zależności od używanego klienta.</span><span class="sxs-lookup"><span data-stu-id="77624-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="77624-108">Rozszerzalność uwierzytelniania klientów NuGet</span><span class="sxs-lookup"><span data-stu-id="77624-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="77624-109">Dla różnych klientów NuGet sam dostawca prywatnego źródła danych jest odpowiedzialny za uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="77624-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="77624-110">Wszystkie klienci NuGet mają metody rozszerzalności do obsługi tego.</span><span class="sxs-lookup"><span data-stu-id="77624-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="77624-111">Są to rozszerzenie programu Visual Studio lub wtyczki, które mogą komunikować się z NuGet do pobierania poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="77624-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="77624-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77624-112">Visual Studio</span></span>

<span data-ttu-id="77624-113">W programie Visual Studio NuGet udostępnia interfejs, który dostawcy kanałów informacyjnych można zaimplementować i dostarczyć do swoich klientów.</span><span class="sxs-lookup"><span data-stu-id="77624-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="77624-114">Aby uzyskać więcej informacji, zapoznaj się z [dokumentacją dotyczącą tworzenia dostawcy poświadczeń programu Visual Studio.](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)</span><span class="sxs-lookup"><span data-stu-id="77624-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="77624-115">Dostępne dostawców poświadczeń NuGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77624-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="77624-116">Istnieje dostawca poświadczeń wbudowany w programie Visual Studio do obsługi usługi Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="77624-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="77624-117">Wśród dostawców poświadczeń dostępnych dodatków dodatku plug-in są:</span><span class="sxs-lookup"><span data-stu-id="77624-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="77624-118">Dostawca poświadczeń MyGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77624-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="77624-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="77624-119">nuget.exe</span></span>

<span data-ttu-id="77624-120">Gdy `nuget.exe` potrzebne poświadczenia do uwierzytelniania za pomocą pliku danych, wyszukuje je w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="77624-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="77624-121">Poszukaj `NuGet.config` poświadczeń w plikach.</span><span class="sxs-lookup"><span data-stu-id="77624-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="77624-122">Korzystanie z dostawców poświadczeń dodatku plug-in w wersji 2</span><span class="sxs-lookup"><span data-stu-id="77624-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="77624-123">Korzystanie z dostawców poświadczeń dodatku plug 1</span><span class="sxs-lookup"><span data-stu-id="77624-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="77624-124">Następnie NuGet monituje użytkownika o poświadczenia w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="77624-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="77624-125">dostawcy poświadczeń nuget.exe i V2</span><span class="sxs-lookup"><span data-stu-id="77624-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="77624-126">W `4.8` wersji NuGet zdefiniowano nowy mechanizm wtyczki uwierzytelniania, dalej określane jako dostawców poświadczeń V2.</span><span class="sxs-lookup"><span data-stu-id="77624-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="77624-127">Aby uzyskać informacje na temat instalacji i wykrywania tych dostawców, zobacz [wtyczki platformy wieloplatformowej NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="77624-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="77624-128">dostawcy poświadczeń nuget.exe i V1</span><span class="sxs-lookup"><span data-stu-id="77624-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="77624-129">W `3.3` wersji NuGet wprowadzono pierwszą wersję wtyczek uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="77624-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="77624-130">W przypadku instalacji i odnajdywania tych dostawców można znaleźć w [u dostawców poświadczeń nuget.exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="77624-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="77624-131">Dostawcy poświadczeń dostępnych dla pliku nuget.exe</span><span class="sxs-lookup"><span data-stu-id="77624-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="77624-132">[Dostawcy poświadczeń usługi Azure DevOps w wersji V2](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) lub [dostawca poświadczeń artefaktów platformy Azure](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="77624-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="77624-133">W programie Visual Studio 2017 w wersji 15.9 lub nowszej dostawca poświadczeń usługi Azure DevOps jest dołączany do programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="77624-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="77624-134">Jeśli `nuget.exe` używa MSBuild z tego konkretnego zestawu narzędzi programu Visual Studio, wtyczka zostanie wykryta automatycznie.</span><span class="sxs-lookup"><span data-stu-id="77624-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="77624-135">plik dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="77624-135">dotnet.exe</span></span>

<span data-ttu-id="77624-136">Gdy `dotnet.exe` potrzebne poświadczenia do uwierzytelniania za pomocą pliku danych, wyszukuje je w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="77624-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="77624-137">Poszukaj `NuGet.config` poświadczeń w plikach.</span><span class="sxs-lookup"><span data-stu-id="77624-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="77624-138">Korzystanie z dostawców poświadczeń dodatku plug-in w wersji 2</span><span class="sxs-lookup"><span data-stu-id="77624-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="77624-139">Domyślnie `dotnet.exe` nie jest interaktywna, więc `--interactive` może być konieczne przekazanie flagi, aby narzędzie do blokowania do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="77624-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="77624-140">Dostawcy poświadczeń dotnet.exe i V2</span><span class="sxs-lookup"><span data-stu-id="77624-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="77624-141">W `2.2.100` wersji SDK NuGet zdefiniowane mechanizm wtyczki uwierzytelniania, który działa we wszystkich klientach.</span><span class="sxs-lookup"><span data-stu-id="77624-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="77624-142">Aby uzyskać informacje na temat instalacji i wykrywania tych dostawców, zobacz [wtyczki platformy wieloplatformowej NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="77624-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="77624-143">Dostawcy poświadczeń dostępnych dla programu dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="77624-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="77624-144">Dostawca poświadczeń artefaktów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="77624-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="77624-145">Msbuild.exe</span><span class="sxs-lookup"><span data-stu-id="77624-145">MSBuild.exe</span></span>

<span data-ttu-id="77624-146">Gdy `MSBuild.exe` potrzebne poświadczenia do uwierzytelniania za pomocą pliku danych, wyszukuje je w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="77624-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="77624-147">Szukaj poświadczeń w `NuGet.config` plikach</span><span class="sxs-lookup"><span data-stu-id="77624-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="77624-148">Korzystanie z dostawców poświadczeń dodatku plug-in w wersji 2</span><span class="sxs-lookup"><span data-stu-id="77624-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="77624-149">Domyślnie `MSBuild.exe` nie jest interaktywna, więc `/p:NuGetInteractive=true` może być konieczne ustawienie właściwości, aby narzędzie do blokowania uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="77624-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="77624-150">Dostawcy poświadczeń MSBuild.exe i V2</span><span class="sxs-lookup"><span data-stu-id="77624-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="77624-151">W programie Visual Studio 2019 Update 9 NuGet zdefiniował mechanizm wtyczki uwierzytelniania, który działa na wszystkich klientach.</span><span class="sxs-lookup"><span data-stu-id="77624-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="77624-152">Aby uzyskać informacje na temat instalacji i wykrywania tych dostawców, zobacz [wtyczki platformy wieloplatformowej NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="77624-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="77624-153">Dostawcy poświadczeń dla programu MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="77624-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="77624-154">Dostawca poświadczeń artefaktów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="77624-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="77624-155">Z visual studio 2017 Update 9 i nowsze, dostawca poświadczeń usługi Azure DevOps jest w pakiecie w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="77624-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="77624-156">Nie są wymagane żadne dodatkowe kroki.</span><span class="sxs-lookup"><span data-stu-id="77624-156">No additional steps are required.</span></span>
