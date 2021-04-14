---
title: Rozwiązywanie problemów z zainstalowanymi pakietami
description: Jak znaleźć źródło pakietu, które zostało użyte dla poszczególnych pakietów
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387572"
---
# <a name="troubleshooting-installed-packages"></a><span data-ttu-id="2c525-103">Rozwiązywanie problemów z zainstalowanymi pakietami</span><span class="sxs-lookup"><span data-stu-id="2c525-103">Troubleshooting Installed Packages</span></span>

<span data-ttu-id="2c525-104">Czasami może być konieczne zweryfikowanie źródła, z którego został zainstalowany określony pakiet.</span><span class="sxs-lookup"><span data-stu-id="2c525-104">Sometimes you might want to validate which source a specific package was installed from.</span></span> <span data-ttu-id="2c525-105">Oto kilka sposobów, które można sprawdzić.</span><span class="sxs-lookup"><span data-stu-id="2c525-105">Here are some ways you can check.</span></span>

> [!Note]
> <span data-ttu-id="2c525-106">Niektóre źródła pakietów obsługują koncepcję znaną jako źródła nadrzędne.</span><span class="sxs-lookup"><span data-stu-id="2c525-106">Some package sources support a concept known as upstream sources.</span></span> <span data-ttu-id="2c525-107">Na przykład [Azure Artifacts nadrzędne źródła](/azure/devops/artifacts/concepts/upstream-sources).</span><span class="sxs-lookup"><span data-stu-id="2c525-107">For example, [Azure Artifacts upstream sources](/azure/devops/artifacts/concepts/upstream-sources).</span></span> <span data-ttu-id="2c525-108">Klienci NuGet nie wiedzą, czy pakiet pochodzi ze źródła nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="2c525-108">NuGet clients do not know whether a package came from an upstream source.</span></span> <span data-ttu-id="2c525-109">W związku z tym każde rejestrowanie źródła pakietu spowoduje, że zostanie wyświetlona lista skonfigurowanego źródła, a nie nadrzędnego źródła.</span><span class="sxs-lookup"><span data-stu-id="2c525-109">Therefore, any logging of the package source will list the configured source, not the upstream source.</span></span>

## <a name="nupkgmetadata-file-in-global-packages-folder"></a><span data-ttu-id="2c525-110">`.nupkg.metadata` plik w folderze pakietów globalnych</span><span class="sxs-lookup"><span data-stu-id="2c525-110">`.nupkg.metadata` file in global packages folder</span></span>

<span data-ttu-id="2c525-111">Gdy pakiet jest wyodrębniony do *folderu global-packages,* jest `.nupkg.metadata` zapisywany plik.</span><span class="sxs-lookup"><span data-stu-id="2c525-111">When a package is extracted into the *global-packages* folder, a file `.nupkg.metadata` is written.</span></span> <span data-ttu-id="2c525-112">Począwszy od pakietu NuGet 5.9.0, pakiet NuGet doda źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="2c525-112">Starting from NuGet 5.9.0, NuGet will add the package source.</span></span> <span data-ttu-id="2c525-113">Zobacz poniżej, aby zamapować wersje nuGet na Visual Studio zestawu SDK platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="2c525-113">See below to map NuGet versions to Visual Studio or .NET SDK versions.</span></span> <span data-ttu-id="2c525-114">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2c525-114">For example:</span></span>

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> <span data-ttu-id="2c525-115">Jeśli folder *global-packages* zawiera pakiety wyodrębnione przed uaktualnieniem do nowszej wersji narzędzi z pakietem NuGet 5.9.0, plik będzie w wersji 1 i nie będzie zawierać źródła `.nupkg.metadata` pakietu.</span><span class="sxs-lookup"><span data-stu-id="2c525-115">If your *global-packages* folder has packages extracted before you upgraded to a newer version of tools that has NuGet 5.9.0, the `.nupkg.metadata` file will be version 1 and will not contain the package source.</span></span> <span data-ttu-id="2c525-116">Możesz [wyczyścić folder *global-packages,*](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) aby upewnić się, że wszystkie pakiety będą zawierać źródło pakietu.</span><span class="sxs-lookup"><span data-stu-id="2c525-116">You can [clear your *global-packages* folder](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) to ensure all packages will contain the package source.</span></span>

> [!Tip]
> <span data-ttu-id="2c525-117">Program NuGet zapisuje `.nupkg.metadata` plik tylko w *folderze global-packages.*</span><span class="sxs-lookup"><span data-stu-id="2c525-117">NuGet writes the `.nupkg.metadata` file to the *global-packages* folder only.</span></span> <span data-ttu-id="2c525-118">Projekty `packages.config` używające programu używają folderu pakietów rozwiązań, który nie tworzy `.nupkg.metadata` pliku.</span><span class="sxs-lookup"><span data-stu-id="2c525-118">Projects using `packages.config` use a solution packages folder, which does not create a `.nupkg.metadata` file.</span></span>

## <a name="installed-package-log-message"></a><span data-ttu-id="2c525-119">Komunikat dziennika zainstalowanego pakietu</span><span class="sxs-lookup"><span data-stu-id="2c525-119">Installed package log message</span></span>

<span data-ttu-id="2c525-120">Począwszy od pakietu NuGet 5.9.0, pakiet NuGet wyprowadza źródło pakietu w komunikacie przywracania informujący o zainstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="2c525-120">Starting from NuGet 5.9.0, NuGet outputs the package source in the restore message informing that a package was installed.</span></span> <span data-ttu-id="2c525-121">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2c525-121">For example:</span></span>

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> <span data-ttu-id="2c525-122">Ten komunikat jest wyjściowy z normalnym/informacyjnym poziomem szczegółowości.</span><span class="sxs-lookup"><span data-stu-id="2c525-122">This message is output at normal/informational verbosity.</span></span> <span data-ttu-id="2c525-123">Visual Studio i interfejsie wiersza polecenia mają domyślnie minimalną szczegółowość, więc ten `dotnet` komunikat nie będzie widoczny domyślnie.</span><span class="sxs-lookup"><span data-stu-id="2c525-123">Visual Studio and the `dotnet` CLI default to minimal verbosity, so this message will not be visible by default.</span></span> <span data-ttu-id="2c525-124">Narzędzia interfejsu wiersza polecenia i `msbuild` domyślnie mają normalną szczegółowość, więc ten `nuget` komunikat będzie domyślnie widoczny.</span><span class="sxs-lookup"><span data-stu-id="2c525-124">The `msbuild` and `nuget` CLI tools default to normal verbosity, so this message will be visible by default.</span></span>

## <a name="http-log-message"></a><span data-ttu-id="2c525-125">Komunikat dziennika HTTP</span><span class="sxs-lookup"><span data-stu-id="2c525-125">HTTP log message</span></span>

<span data-ttu-id="2c525-126">Jeśli pakiet nie jest dostępny lokalnie, w folderze *pakietów* globalnych, folderze rezerwowym lub lokalnym źródle plików nuGet pobierze go z dowolnego skonfigurowanego źródła pakietu za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c525-126">When a package is not available locally, either in the *global-packages* folder, a fallback folder, or a local file source, NuGet will download it from any configured package source over HTTP.</span></span> <span data-ttu-id="2c525-127">Żądania HTTP i odpowiedzi są rejestrowane na normalnym poziomie szczegółowości i powinno być widać tylko jedno żądanie i odpowiedź na wersję pakietu.</span><span class="sxs-lookup"><span data-stu-id="2c525-127">HTTP requests and responses are logged at the normal verbosity level, and you should see only a single request and response per package version.</span></span> <span data-ttu-id="2c525-128">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2c525-128">For example:</span></span>

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

<span data-ttu-id="2c525-129">Jeśli pliki zostały ostatnio pobrane, mogą zostać pobrane z pamięci podręcznej *http-cache programu* NuGet</span><span class="sxs-lookup"><span data-stu-id="2c525-129">If the files were recently downloaded, they might be retrieved from NuGet's *http-cache*</span></span>

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

<span data-ttu-id="2c525-130">Format adresu URL może się różnić w przypadku różnych implementacji serwera HTTP NuGet oraz tego, czy implementuje on protokół HTTP NuGet v2, czy V3.</span><span class="sxs-lookup"><span data-stu-id="2c525-130">The URL format may be different for different NuGet HTTP server implementations, and whether it's implementing NuGet V2 or V3 HTTP protocol.</span></span>

<span data-ttu-id="2c525-131">Jeśli masz zdefiniowanych wiele źródeł HTTP, zobaczysz wiele żądań do pliku każdego `nuget.config` `index.json` pakietu, po jednym dla każdego źródła.</span><span class="sxs-lookup"><span data-stu-id="2c525-131">If your `nuget.config` has multiple HTTP sources defined, you will see multiple requests to each package's `index.json` file, one for each source.</span></span> <span data-ttu-id="2c525-132">Jednak dla każdej wersji pakietu będzie dostępne tylko jedno `nupkg` pobranie.</span><span class="sxs-lookup"><span data-stu-id="2c525-132">But there will be only a single `nupkg` download for each version of the package.</span></span>

## <a name="package-signature-log-message"></a><span data-ttu-id="2c525-133">Komunikat dziennika sygnatury pakietu</span><span class="sxs-lookup"><span data-stu-id="2c525-133">Package signature log message</span></span>

<span data-ttu-id="2c525-134">Jeśli pobierany pakiet jest podpisany, pakiet NuGet zweryfikuje podpis i zweryfikuje następujący komunikat ze szczegółowymi informacjami:</span><span class="sxs-lookup"><span data-stu-id="2c525-134">If the package being downloaded is signed, NuGet will validate the signature and will log the following message at detailed verbosity:</span></span>

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

<span data-ttu-id="2c525-135">Ten komunikat będzie zgłaszany, czy pakiet został pobrany ze źródła pakietu HTTP, czy skopiowany ze źródła pakietu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="2c525-135">This message will be reported whether the package was downloaded from an HTTP package source, or copied from a local package source.</span></span> <span data-ttu-id="2c525-136">Nie będzie to dane wyjściowe, jeśli pakiet jest już dostępny w folderze *global-packages* lub folderze rezerwowym.</span><span class="sxs-lookup"><span data-stu-id="2c525-136">It will not be output if the package is already available in the *global-packages* folder or a fallback folder.</span></span>

> [!Important]
> <span data-ttu-id="2c525-137">Ze względu na usunięcie zaufania narzędzia NuGet urzędu certyfikacji [VeriSign](https://github.com/dotnet/announcements/issues/180) wyłączono weryfikację podpisanych pakietów na niektórych platformach, w niektórych wersjach pakietu NuGet i zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="2c525-137">Due to [removal of trust of VeriSign CA](https://github.com/dotnet/announcements/issues/180) NuGet has disabled signed package verification on certain platforms, in certain versions of NuGet and the .NET SDK.</span></span> <span data-ttu-id="2c525-138">W związku z tym te same pakiety mogą zawierać dzienniki lub mogą brakować tych dzienników w zależności od platformy, na której jest uruchomione przywracanie, oraz wersji platformy .NET lub `PackageSignatureVerificationLog` nuGet, której używasz.</span><span class="sxs-lookup"><span data-stu-id="2c525-138">Therefore, the same packages may have `PackageSignatureVerificationLog` logs, or those logs may be missing, depending on what platform you're running restore on, and which version of .NET or NuGet you're using.</span></span>

## <a name="nuget-version-map"></a><span data-ttu-id="2c525-139">Mapa wersji programu NuGet</span><span class="sxs-lookup"><span data-stu-id="2c525-139">NuGet Version Map</span></span>

<span data-ttu-id="2c525-140">Następujące wersje pakietu NuGet mają istotne zmiany dotyczące rejestrowania źródła pakietu:</span><span class="sxs-lookup"><span data-stu-id="2c525-140">The following versions of NuGet have important changes regarding package source logging:</span></span>

|<span data-ttu-id="2c525-141">Wersja nuGet</span><span class="sxs-lookup"><span data-stu-id="2c525-141">NuGet Version</span></span>|<span data-ttu-id="2c525-142">Visual Studio wersji</span><span class="sxs-lookup"><span data-stu-id="2c525-142">Visual Studio Version</span></span>|<span data-ttu-id="2c525-143">Wersja zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2c525-143">.NET SDK Version</span></span>|
|---|---|---|
|<span data-ttu-id="2c525-144">NuGet 5.9.0</span><span class="sxs-lookup"><span data-stu-id="2c525-144">NuGet 5.9.0</span></span>|<span data-ttu-id="2c525-145">Visual Studio 2019 r. 16.9.0</span><span class="sxs-lookup"><span data-stu-id="2c525-145">Visual Studio 2019 16.9.0</span></span>|<span data-ttu-id="2c525-146">.NET 5 SDK 5.0.200</span><span class="sxs-lookup"><span data-stu-id="2c525-146">.NET 5 SDK 5.0.200</span></span>|
