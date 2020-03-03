---
title: Używanie pakietów z uwierzytelnionych kanałów informacyjnych
description: Zużywanie pakietów ze źródeł uwierzytelnionych we wszystkich scenariuszach klienta NuGet
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231792"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="a800b-103">Używanie pakietów z uwierzytelnionych kanałów informacyjnych</span><span class="sxs-lookup"><span data-stu-id="a800b-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="a800b-104">Oprócz [publicznego kanału informacyjnego](https://api.nuget.org/v3/index.json)NuGet.org klienci programu NuGet mogą korzystać ze źródeł danych i prywatnych źródeł http.</span><span class="sxs-lookup"><span data-stu-id="a800b-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="a800b-105">Aby uwierzytelnić się za pomocą prywatnych źródeł http, dwa podejścia są następujące:</span><span class="sxs-lookup"><span data-stu-id="a800b-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="a800b-106">Dodaj poświadczenia w [pliku NuGet. config](../reference/nuget-config-file.md#packagesourcecredentials)</span><span class="sxs-lookup"><span data-stu-id="a800b-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="a800b-107">Uwierzytelnianie przy użyciu jednego z wielu modeli rozszerzalności w zależności od używanego klienta programu.</span><span class="sxs-lookup"><span data-stu-id="a800b-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="a800b-108">Rozszerzalność uwierzytelniania klientów NuGet</span><span class="sxs-lookup"><span data-stu-id="a800b-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="a800b-109">W przypadku różnych klientów programu NuGet sam dostawca kanału informacyjnego jest odpowiedzialny za uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="a800b-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="a800b-110">Wszyscy klienci NuGet mają metody rozszerzalności obsługujące ten program.</span><span class="sxs-lookup"><span data-stu-id="a800b-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="a800b-111">Są to rozszerzenia programu Visual Studio lub wtyczka, która może komunikować się z pakietem NuGet w celu pobierania poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="a800b-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="a800b-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a800b-112">Visual Studio</span></span>

<span data-ttu-id="a800b-113">W programie Visual Studio pakiet NuGet udostępnia interfejs, który dostawcy kanału informacyjnego mogą zaimplementować i udostępnić klientom.</span><span class="sxs-lookup"><span data-stu-id="a800b-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="a800b-114">Aby uzyskać więcej informacji, zapoznaj się z dokumentacją dotyczącą [tworzenia dostawcy poświadczeń programu Visual Studio](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span><span class="sxs-lookup"><span data-stu-id="a800b-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="a800b-115">Dostępni dostawcy poświadczeń NuGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a800b-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="a800b-116">Istnieje Dostawca poświadczeń wbudowany w program Visual Studio w celu obsługi usługi Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="a800b-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="a800b-117">Dostępne są następujące dostawcy poświadczeń wtyczek:</span><span class="sxs-lookup"><span data-stu-id="a800b-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="a800b-118">Dostawca poświadczeń MyGet dla programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a800b-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="a800b-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="a800b-119">nuget.exe</span></span>

<span data-ttu-id="a800b-120">Gdy `nuget.exe` wymaga poświadczeń do uwierzytelnienia ze źródłem danych, wygląda w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a800b-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="a800b-121">Wyszukaj poświadczenia w plikach `NuGet.config`.</span><span class="sxs-lookup"><span data-stu-id="a800b-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="a800b-122">Użyj dostawców poświadczeń wtyczek v2</span><span class="sxs-lookup"><span data-stu-id="a800b-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="a800b-123">Użyj dostawców poświadczeń wtyczki w wersji 1</span><span class="sxs-lookup"><span data-stu-id="a800b-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="a800b-124">Następnie pakiet NuGet monituje użytkownika o poświadczenia w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="a800b-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="a800b-125">dostawcy poświadczeń NuGet. exe i v2</span><span class="sxs-lookup"><span data-stu-id="a800b-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="a800b-126">W wersji `4.8` NuGet zdefiniowano nowy mechanizm wtyczek uwierzytelniania, zwany dalej dostawcą poświadczeń w wersji 2.</span><span class="sxs-lookup"><span data-stu-id="a800b-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="a800b-127">Aby przeprowadzić instalację i odnajdywanie tych dostawców, zapoznaj się z [dodatkami międzyplatformowymi NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="a800b-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="a800b-128">dostawcy poświadczeń NuGet. exe i v1</span><span class="sxs-lookup"><span data-stu-id="a800b-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="a800b-129">W wersji `3.3` NuGet wprowadził pierwszą wersję wtyczek uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a800b-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="a800b-130">Na potrzeby instalacji i odnajdywania tych dostawców odwołują się do [dostawców poświadczeń NuGet. exe](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span><span class="sxs-lookup"><span data-stu-id="a800b-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="a800b-131">Dostępni dostawcy poświadczeń dla programu NuGet. exe</span><span class="sxs-lookup"><span data-stu-id="a800b-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="a800b-132">Dostawcy [poświadczeń usługi Azure DevOps v2](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) lub [Dostawca poświadczeń Azure Artifacts](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="a800b-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="a800b-133">W programie Visual Studio 2017 w wersji 15,9 lub nowszej Dostawca poświadczeń usługi Azure DevOps jest powiązany z programem Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a800b-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="a800b-134">Jeśli `nuget.exe` używa programu MSBuild z tego konkretnego zestawu narzędzi programu Visual Studio, Wtyczka zostanie odnaleziona automatycznie.</span><span class="sxs-lookup"><span data-stu-id="a800b-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="a800b-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="a800b-135">dotnet.exe</span></span>

<span data-ttu-id="a800b-136">Gdy `dotnet.exe` wymaga poświadczeń do uwierzytelnienia ze źródłem danych, wygląda w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a800b-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="a800b-137">Wyszukaj poświadczenia w plikach `NuGet.config`.</span><span class="sxs-lookup"><span data-stu-id="a800b-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="a800b-138">Użyj dostawców poświadczeń wtyczek v2</span><span class="sxs-lookup"><span data-stu-id="a800b-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="a800b-139">Domyślnie `dotnet.exe` nie jest interaktywna, więc może być konieczne przekazanie flagi `--interactive` w celu uzyskania narzędzia do zablokowania uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a800b-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="a800b-140">dostawcy poświadczeń dotnet. exe i v2</span><span class="sxs-lookup"><span data-stu-id="a800b-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="a800b-141">W wersji `2.2.100` zestawu SDK pakiet NuGet definiuje mechanizm wtyczki uwierzytelniania, który działa na wszystkich klientach.</span><span class="sxs-lookup"><span data-stu-id="a800b-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="a800b-142">Aby przeprowadzić instalację i odnajdywanie tych dostawców, zapoznaj się z [dodatkami międzyplatformowymi NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="a800b-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="a800b-143">Dostępni dostawcy poświadczeń dla programu dotnet. exe</span><span class="sxs-lookup"><span data-stu-id="a800b-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="a800b-144">Dostawca poświadczeń Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="a800b-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="a800b-145">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="a800b-145">MSBuild.exe</span></span>

<span data-ttu-id="a800b-146">Gdy `MSBuild.exe` wymaga poświadczeń do uwierzytelnienia ze źródłem danych, wygląda w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a800b-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="a800b-147">Wyszukaj poświadczenia w plikach `NuGet.config`</span><span class="sxs-lookup"><span data-stu-id="a800b-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="a800b-148">Użyj dostawców poświadczeń wtyczek v2</span><span class="sxs-lookup"><span data-stu-id="a800b-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="a800b-149">Domyślnie `MSBuild.exe` nie jest interaktywna, więc może być konieczne ustawienie właściwości `/p:NuGetInteractive=true` w celu zablokowania uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a800b-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="a800b-150">Dostawcy poświadczeń MSBuild. exe i v2</span><span class="sxs-lookup"><span data-stu-id="a800b-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="a800b-151">W programie Visual Studio 2019 Update 9 pakiet NuGet definiuje mechanizm wtyczki uwierzytelniania, który działa na wszystkich klientach.</span><span class="sxs-lookup"><span data-stu-id="a800b-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="a800b-152">Aby przeprowadzić instalację i odnajdywanie tych dostawców, zapoznaj się z [dodatkami międzyplatformowymi NuGet](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="a800b-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="a800b-153">Dostępni dostawcy poświadczeń dla programu MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="a800b-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="a800b-154">Dostawca poświadczeń Azure Artifacts</span><span class="sxs-lookup"><span data-stu-id="a800b-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="a800b-155">W programie Visual Studio 2017 Update 9 lub nowszym Dostawca poświadczeń usługi Azure DevOps jest powiązany z programem Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a800b-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="a800b-156">Nie są wymagane żadne dodatkowe czynności.</span><span class="sxs-lookup"><span data-stu-id="a800b-156">No additional steps are required.</span></span>
