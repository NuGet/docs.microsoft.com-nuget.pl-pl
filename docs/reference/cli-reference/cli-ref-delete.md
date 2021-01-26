---
title: Polecenie usunięcia interfejsu wiersza polecenia NuGet
description: Odwołanie do nuget.exe usuwania polecenia
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 96c75366ae69b34f5cd1f55feb53087b5d0ea324
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775951"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="99718-103">DELETE — polecenie (interfejs wiersza polecenia NuGet)</span><span class="sxs-lookup"><span data-stu-id="99718-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="99718-104">**Dotyczy:** &bullet; **obsługiwane wersje** publikowania pakietów: wszystkie</span><span class="sxs-lookup"><span data-stu-id="99718-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="99718-105">Usuwa pakiet ze źródła pakietu.</span><span class="sxs-lookup"><span data-stu-id="99718-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="99718-106">W przypadku nuget.org polecenie Delete [wystawia pakiet](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="99718-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="99718-107">Użycie</span><span class="sxs-lookup"><span data-stu-id="99718-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="99718-108">gdzie `<packageID>` i `<packageVersion>` Zidentyfikuj dokładny pakiet do usunięcia lub Wycofaj listy.</span><span class="sxs-lookup"><span data-stu-id="99718-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="99718-109">Dokładne zachowanie zależy od źródła.</span><span class="sxs-lookup"><span data-stu-id="99718-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="99718-110">Na przykład dla folderów lokalnych pakiet jest usuwany; dla nuget.org pakiet nie znajduje się na liście.</span><span class="sxs-lookup"><span data-stu-id="99718-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="99718-111">Opcje</span><span class="sxs-lookup"><span data-stu-id="99718-111">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="99718-112">Klucz interfejsu API repozytorium docelowego.</span><span class="sxs-lookup"><span data-stu-id="99718-112">The API key for the target repository.</span></span> <span data-ttu-id="99718-113">Jeśli nie istnieje, jest używany określony w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="99718-113">If not present, the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="99718-114">Plik konfiguracji NuGet, który ma zostać zastosowany.</span><span class="sxs-lookup"><span data-stu-id="99718-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="99718-115">Jeśli nie zostanie określony, `%AppData%\NuGet\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` lub `~/.config/NuGet/NuGet.Config` (Mac/Linux) jest używany.</span><span class="sxs-lookup"><span data-stu-id="99718-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="99718-116">*(3.5 +)* Wymusza uruchamianie nuget.exe przy użyciu niezmiennej kultury opartej na języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="99718-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="99718-117">Wyświetla informacje pomocy dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="99718-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="99718-118">Pomija monity o dane wejściowe lub potwierdzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="99718-118">Suppresses prompts for user input or confirmations.</span></span>

 - **`-np|-NoPrompt`**

   <span data-ttu-id="99718-119">Nie Monituj podczas usuwania.</span><span class="sxs-lookup"><span data-stu-id="99718-119">Do not prompt when deleting.</span></span>

 - <span data-ttu-id="99718-120">**`-NoServiceEndpoint`** Nie dołącza "API/v2/Packages" do źródłowego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="99718-120">**`-NoServiceEndpoint`** Does not append "api/v2/packages" to the source URL.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="99718-121">Określa adres URL serwera.</span><span class="sxs-lookup"><span data-stu-id="99718-121">Specifies the server URL.</span></span> <span data-ttu-id="99718-122">Adres URL nuget.org ma wartość `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="99718-122">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="99718-123">W przypadku prywatnych kanałów informacyjnych należy zastąpić nazwę hosta, na przykład *% hostname%/API/v3*.</span><span class="sxs-lookup"><span data-stu-id="99718-123">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="99718-124">Określa ilość szczegółów wyświetlanych w danych wyjściowych: `normal` (wartość domyślna), `quiet` lub `detailed` .</span><span class="sxs-lookup"><span data-stu-id="99718-124">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="99718-125">Zobacz również [zmienne środowiskowe](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="99718-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="99718-126">Przykłady</span><span class="sxs-lookup"><span data-stu-id="99718-126">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
