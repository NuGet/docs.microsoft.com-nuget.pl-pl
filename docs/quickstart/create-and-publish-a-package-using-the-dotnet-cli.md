---
title: Tworzenie i publikowanie pakietu NuGet za pomocą interfejsu wiersza polecenia platformy dotnet
description: Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet za pomocą platformy .NET Core interfejsu wiersza polecenia dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 4e96d9969c8b4570ee69501d6529986f891ea4dc
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842606"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="51cd0-103">Szybki start: Tworzenie i publikowanie pakietu (wiersz polecenia dotnet wim)</span><span class="sxs-lookup"><span data-stu-id="51cd0-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="51cd0-104">Jest to prosty proces, aby utworzyć pakiet NuGet z biblioteki klas .NET i opublikuj go w witrynie nuget.org przy użyciu `dotnet` interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="51cd0-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51cd0-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="51cd0-105">Prerequisites</span></span>

1. <span data-ttu-id="51cd0-106">Zainstaluj [zestawu .NET Core SDK](https://www.microsoft.com/net/download/), która obejmuje `dotnet` interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="51cd0-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="51cd0-107">Począwszy od programu Visual Studio 2017, dotnet, których interfejs wiersza polecenia jest automatycznie instalowany z dowolnej platformy .NET Core powiązanych obciążeń.</span><span class="sxs-lookup"><span data-stu-id="51cd0-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="51cd0-108">[Zarejestruj, aby utworzyć bezpłatne konto w witrynie nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz jeszcze takiego.</span><span class="sxs-lookup"><span data-stu-id="51cd0-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="51cd0-109">Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="51cd0-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="51cd0-110">Aby można było przekazać pakiet, należy potwierdzić konto.</span><span class="sxs-lookup"><span data-stu-id="51cd0-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="51cd0-111">Utwórz projekt biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="51cd0-111">Create a class library project</span></span>

<span data-ttu-id="51cd0-112">Można użyć istniejącego projektu biblioteki klas platformy .NET dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="51cd0-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="51cd0-113">Utwórz folder o nazwie `AppLogger` i zmienić tę sytuację.</span><span class="sxs-lookup"><span data-stu-id="51cd0-113">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="51cd0-114">Utwórz projekt za pomocą `dotnet new classlib`, który używa nazwy bieżącego folderu projektu.</span><span class="sxs-lookup"><span data-stu-id="51cd0-114">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="51cd0-115">Dodaj metadane pakietu do pliku projektu</span><span class="sxs-lookup"><span data-stu-id="51cd0-115">Add package metadata to the project file</span></span>

<span data-ttu-id="51cd0-116">Każdy pakiet NuGet musi manifestu, który opisuje zawartość pakietu i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="51cd0-116">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="51cd0-117">W ostatnim pakiecie manifestu to `.nuspec` pliku, który jest generowany na podstawie właściwości metadanych NuGet, które zawierają w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="51cd0-117">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="51cd0-118">Otwórz plik projektu (`.csproj`) i dodaj następujące minimalne właściwości wewnątrz istniejącego `<PropertyGroup>` tagu, zmieniając wartości zgodnie z potrzebami:</span><span class="sxs-lookup"><span data-stu-id="51cd0-118">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="51cd0-119">Przekazać pakiet identyfikator, który jest unikatowa w obrębie nuget.org, lub niezależnie od rodzaju hoście jest używany.</span><span class="sxs-lookup"><span data-stu-id="51cd0-119">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="51cd0-120">W ramach tego przewodnika firma Microsoft zaleca, tym "Próbny" lub "Test" w nazwie późniejszym etapie publikowania uwidocznić pakietu publicznie (choć jest mało prawdopodobne, każda osoba będzie faktycznie używać).</span><span class="sxs-lookup"><span data-stu-id="51cd0-120">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="51cd0-121">Dodaj wszelkie opcjonalne właściwości opisanych na [właściwości metadanych NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="51cd0-121">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="51cd0-122">Pakiety utworzone do użytku publicznego, należy zwrócić szczególną uwagę na **PackageTags** właściwości, jak tagi pomóc innym odnaleźć pakietu i zrozumieć, co robi.</span><span class="sxs-lookup"><span data-stu-id="51cd0-122">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="51cd0-123">Uruchom polecenie pakietu</span><span class="sxs-lookup"><span data-stu-id="51cd0-123">Run the pack command</span></span>

<span data-ttu-id="51cd0-124">Tworzenie pakietu NuGet ( `.nupkg` plik) z projektu, uruchom `dotnet pack` polecenia, które sprzyja wytwarzaniu się odpowiednich projektu automatycznie:</span><span class="sxs-lookup"><span data-stu-id="51cd0-124">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="51cd0-125">Dane wyjściowe zawierają ścieżkę do `.nupkg` pliku:</span><span class="sxs-lookup"><span data-stu-id="51cd0-125">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="51cd0-126">Automatyczne generowanie pakietu w kompilacji</span><span class="sxs-lookup"><span data-stu-id="51cd0-126">Automatically generate package on build</span></span>

<span data-ttu-id="51cd0-127">Aby automatycznie uruchomić `dotnet pack` po uruchomieniu `dotnet build`, Dodaj następujący wiersz do pliku projektu w ramach `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="51cd0-127">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="51cd0-128">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="51cd0-128">Publish the package</span></span>

<span data-ttu-id="51cd0-129">Po utworzeniu `.nupkg` pliku opublikujesz go w witrynie nuget.org przy użyciu `dotnet nuget push` polecenia wraz z kluczem API uzyskanych z repozytorium nuget.org.</span><span class="sxs-lookup"><span data-stu-id="51cd0-129">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="51cd0-130">Uzyskiwanie klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="51cd0-130">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="51cd0-131">Publikowanie za pomocą polecenia dotnet nuget wypychania</span><span class="sxs-lookup"><span data-stu-id="51cd0-131">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="51cd0-132">Publikowanie błędy</span><span class="sxs-lookup"><span data-stu-id="51cd0-132">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="51cd0-133">Zarządzanie opublikowany pakiet</span><span class="sxs-lookup"><span data-stu-id="51cd0-133">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="51cd0-134">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="51cd0-134">Related topics</span></span>

- [<span data-ttu-id="51cd0-135">Utwórz pakiet</span><span class="sxs-lookup"><span data-stu-id="51cd0-135">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="51cd0-136">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="51cd0-136">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="51cd0-137">Pakiety w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="51cd0-137">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="51cd0-138">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="51cd0-138">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="51cd0-139">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="51cd0-139">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="51cd0-140">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="51cd0-140">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="51cd0-141">Tworzenie pakietów symboli</span><span class="sxs-lookup"><span data-stu-id="51cd0-141">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="51cd0-142">Podpisywanie pakietów</span><span class="sxs-lookup"><span data-stu-id="51cd0-142">Signing packages</span></span>](../create-packages/Sign-a-package.md)
