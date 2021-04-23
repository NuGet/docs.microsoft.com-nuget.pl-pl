---
title: Korzystanie z pakietów z uwierzytelnionych źródeł danych
description: Korzystanie z pakietów z uwierzytelnionych źródeł danych we wszystkich scenariuszach klienta NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: e76fefaf4d3c86aa15cf279090c0adb8ed779aab
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901515"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="a6780-103">Korzystanie z pakietów z uwierzytelnionych źródeł danych</span><span class="sxs-lookup"><span data-stu-id="a6780-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="a6780-104">Oprócz publicznego źródła [nuget.org,](https://api.nuget.org/v3/index.json)klienci NuGet mogą wchodzić w interakcje z kanałami informacyjnymi plików i prywatnymi kanałami informacyjnymi HTTP.</span><span class="sxs-lookup"><span data-stu-id="a6780-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="a6780-105">Do uwierzytelniania za pomocą prywatnych kanałów informacyjnych HTTP są dostępne 2 podejścia:</span><span class="sxs-lookup"><span data-stu-id="a6780-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="a6780-106">Dodawanie poświadczeń w [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span><span class="sxs-lookup"><span data-stu-id="a6780-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="a6780-107">Uwierzytelnianie przy użyciu jednego z wielu modeli rozszerzalności w zależności od używanego klienta.</span><span class="sxs-lookup"><span data-stu-id="a6780-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="a6780-108">Rozszerzalność uwierzytelniania klientów NuGet</span><span class="sxs-lookup"><span data-stu-id="a6780-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="a6780-109">W przypadku różnych klientów NuGet za uwierzytelnianie odpowiada sam prywatny dostawca kanału informacyjnego.</span><span class="sxs-lookup"><span data-stu-id="a6780-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="a6780-110">Wszyscy klienci NuGet mają metody rozszerzalności, które to obsługują.</span><span class="sxs-lookup"><span data-stu-id="a6780-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="a6780-111">Są to rozszerzenie Visual Studio lub wtyczka, która może komunikować się z nuGet w celu pobrania poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="a6780-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="a6780-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6780-112">Visual Studio</span></span>

<span data-ttu-id="a6780-113">W Visual Studio NuGet uwidacznia interfejs, który dostawcy kanału informacyjnego mogą implementować i dostarczać swoim klientom.</span><span class="sxs-lookup"><span data-stu-id="a6780-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="a6780-114">Aby uzyskać więcej informacji, zapoznaj się z dokumentacją dotyczącą tworzenia dostawcy [Visual Studio poświadczeń.](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)</span><span class="sxs-lookup"><span data-stu-id="a6780-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="a6780-115">Dostępni dostawcy poświadczeń NuGet dla Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6780-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="a6780-116">Dostawca poświadczeń jest wbudowany w Visual Studio do obsługi Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="a6780-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="a6780-117">Do dostępnych dostawców poświadczeń wtyczki należą:</span><span class="sxs-lookup"><span data-stu-id="a6780-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="a6780-118">MyGet Dostawca poświadczeń for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a6780-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="a6780-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="a6780-119">nuget.exe</span></span>

<span data-ttu-id="a6780-120">Gdy `nuget.exe` potrzebuje poświadczeń do uwierzytelnienia za pomocą kanału informacyjnego, szuka ich w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a6780-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="a6780-121">Poszukaj poświadczeń w `NuGet.config` plikach.</span><span class="sxs-lookup"><span data-stu-id="a6780-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="a6780-122">Korzystanie z dostawców poświadczeń wtyczki w wersji 2</span><span class="sxs-lookup"><span data-stu-id="a6780-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="a6780-123">Korzystanie z dostawców poświadczeń wtyczki w wersji 1</span><span class="sxs-lookup"><span data-stu-id="a6780-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="a6780-124">Następnie program NuGet monituje użytkownika o poświadczenia w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="a6780-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="a6780-125">nuget.exe i dostawcy poświadczeń w wersji 2</span><span class="sxs-lookup"><span data-stu-id="a6780-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="a6780-126">W wersji NuGet zdefiniowano nowy mechanizm wtyczki uwierzytelniania, nazywany dostawcami `4.8` poświadczeń w wersji 2.</span><span class="sxs-lookup"><span data-stu-id="a6780-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="a6780-127">Aby uzyskać informacje na temat instalacji i odnajdywania tych dostawców, zapoznaj się z [tematem NuGet cross platform plugins (Wtyczki NuGet dla wielu platform).](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)</span><span class="sxs-lookup"><span data-stu-id="a6780-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="a6780-128">nuget.exe i dostawcy poświadczeń w wersji 1</span><span class="sxs-lookup"><span data-stu-id="a6780-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="a6780-129">W wersji `3.3` NuGet wprowadzono pierwszą wersję wtyczek uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a6780-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="a6780-130">Aby uzyskać informacje na temat instalacji i odnajdywania tych dostawców, [ zobacznuget.exe dostawcy poświadczeń](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="a6780-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="a6780-131">Dostępni dostawcy poświadczeń dla nuget.exe</span><span class="sxs-lookup"><span data-stu-id="a6780-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="a6780-132">[Azure DevOps dostawcy poświadczeń w wersji 2](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) [lub Azure Artifacts Dostawca poświadczeń](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="a6780-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="a6780-133">W Visual Studio 2017 r. w wersji 15.9 lub nowszej dostawca poświadczeń Azure DevOps jest dołączony do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a6780-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="a6780-134">Jeśli `nuget.exe` program korzysta z programu MSBuild z Visual Studio zestawu narzędzi, wtyczka zostanie wykryta automatycznie.</span><span class="sxs-lookup"><span data-stu-id="a6780-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="a6780-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="a6780-135">dotnet.exe</span></span>

<span data-ttu-id="a6780-136">Gdy `dotnet.exe` wymaga poświadczeń do uwierzytelnienia za pomocą kanału informacyjnego, szuka ich w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a6780-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="a6780-137">Poszukaj poświadczeń w `NuGet.config` plikach.</span><span class="sxs-lookup"><span data-stu-id="a6780-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="a6780-138">Korzystanie z dostawców poświadczeń wtyczki w wersji 2</span><span class="sxs-lookup"><span data-stu-id="a6780-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="a6780-139">Domyślnie nie jest interakcyjna, więc może być konieczne podanie flagi w celu zablokowania narzędzia `dotnet.exe` `--interactive` na potrzeby uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a6780-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="a6780-140">dotnet.exe i dostawcy poświadczeń w wersji 2</span><span class="sxs-lookup"><span data-stu-id="a6780-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="a6780-141">W wersji `2.2.100` zestawu SDK program NuGet zdefiniuje mechanizm wtyczki uwierzytelniania, który działa we wszystkich klientach.</span><span class="sxs-lookup"><span data-stu-id="a6780-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="a6780-142">Aby uzyskać informacje na temat instalacji i odnajdywania tych dostawców, zapoznaj się z [tematem NuGet cross platform plugins (Wtyczki NuGet dla wielu platform).](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)</span><span class="sxs-lookup"><span data-stu-id="a6780-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="a6780-143">Dostępni dostawcy poświadczeń dla dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="a6780-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="a6780-144">Azure Artifacts Dostawca poświadczeń</span><span class="sxs-lookup"><span data-stu-id="a6780-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="a6780-145">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="a6780-145">MSBuild.exe</span></span>

<span data-ttu-id="a6780-146">Gdy `MSBuild.exe` potrzebuje poświadczeń do uwierzytelnienia za pomocą kanału informacyjnego, szuka ich w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a6780-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="a6780-147">Poszukaj poświadczeń w `NuGet.config` plikach</span><span class="sxs-lookup"><span data-stu-id="a6780-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="a6780-148">Korzystanie z dostawców poświadczeń wtyczki w wersji 2</span><span class="sxs-lookup"><span data-stu-id="a6780-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="a6780-149">Domyślnie nie jest interakcyjna, więc może być konieczne ustawienie właściwości w celu zablokowania `MSBuild.exe` `/p:NuGetInteractive=true` narzędzia na potrzeby uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a6780-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="a6780-150">MSBuild.exe i dostawcy poświadczeń w wersji 2</span><span class="sxs-lookup"><span data-stu-id="a6780-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="a6780-151">W Visual Studio 2019 Update 9 nuGet zdefiniuje mechanizm wtyczki uwierzytelniania, który działa na wszystkich klientach.</span><span class="sxs-lookup"><span data-stu-id="a6780-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="a6780-152">Aby uzyskać informacje na temat instalacji i odnajdywania tych dostawców, zapoznaj się z [tematem NuGet cross platform plugins (Wtyczki NuGet dla wielu platform).](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)</span><span class="sxs-lookup"><span data-stu-id="a6780-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="a6780-153">Dostępni dostawcy poświadczeń dla MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="a6780-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="a6780-154">Azure Artifacts Dostawca poświadczeń</span><span class="sxs-lookup"><span data-stu-id="a6780-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="a6780-155">W Visual Studio 2017 Update 9 i nowszych dostawca poświadczeń Azure DevOps jest dołączony do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a6780-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="a6780-156">Nie są wymagane żadne dodatkowe kroki.</span><span class="sxs-lookup"><span data-stu-id="a6780-156">No additional steps are required.</span></span>
