---
title: Tworzenie i publikowanie pakietu NuGet za pomocą interfejsu wiersza polecenia platformy dotnet
description: Samouczek wskazówki na temat tworzenia i publikowania pakietu NuGet za pomocą platformy .NET Core interfejsu wiersza polecenia dotnet.
author: karann-msft
ms.author: karann
ms.date: 01/24/2018
ms.topic: quickstart
ms.openlocfilehash: 02aa7bb9d27352bbecfc718ef5bd6ee33501018d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548432"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="07a39-103">Szybki Start: Tworzenie i publikowanie pakietu (wiersz polecenia dotnet wim)</span><span class="sxs-lookup"><span data-stu-id="07a39-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="07a39-104">Jest to prosty proces, aby utworzyć pakiet NuGet z biblioteki klas .NET i opublikuj go w witrynie nuget.org przy użyciu `dotnet` interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="07a39-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07a39-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="07a39-105">Prerequisites</span></span>

1. <span data-ttu-id="07a39-106">Zainstaluj [zestawu .NET Core SDK](https://www.microsoft.com/net/download/), która obejmuje `dotnet` interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="07a39-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span>

1. <span data-ttu-id="07a39-107">[Zarejestruj, aby utworzyć bezpłatne konto w witrynie nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz jeszcze takiego.</span><span class="sxs-lookup"><span data-stu-id="07a39-107">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="07a39-108">Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="07a39-108">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="07a39-109">Aby można było przekazać pakiet, należy potwierdzić konto.</span><span class="sxs-lookup"><span data-stu-id="07a39-109">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="07a39-110">Utwórz projekt biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="07a39-110">Create a class library project</span></span>

<span data-ttu-id="07a39-111">Można użyć istniejącego projektu biblioteki klas platformy .NET dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="07a39-111">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="07a39-112">Utwórz folder o nazwie `AppLogger` i zmienić tę sytuację.</span><span class="sxs-lookup"><span data-stu-id="07a39-112">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="07a39-113">Utwórz projekt za pomocą `dotnet new classlib`, który używa nazwy bieżącego folderu projektu.</span><span class="sxs-lookup"><span data-stu-id="07a39-113">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="07a39-114">Dodaj metadane pakietu do pliku projektu</span><span class="sxs-lookup"><span data-stu-id="07a39-114">Add package metadata to the project file</span></span>

<span data-ttu-id="07a39-115">Każdy pakiet NuGet musi manifestu, który opisuje zawartość pakietu i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="07a39-115">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="07a39-116">W ostatnim pakiecie manifestu to `.nuspec` pliku, który jest generowany na podstawie właściwości metadanych NuGet, które zawierają w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="07a39-116">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="07a39-117">Otwórz plik projektu (`.csproj`) i dodaj następujące minimalne właściwości wewnątrz istniejącego `<PropertyGroup>` tagu, zmieniając wartości zgodnie z potrzebami:</span><span class="sxs-lookup"><span data-stu-id="07a39-117">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="07a39-118">Przekazać pakiet identyfikator, który jest unikatowa w obrębie nuget.org, lub niezależnie od rodzaju hoście jest używany.</span><span class="sxs-lookup"><span data-stu-id="07a39-118">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="07a39-119">W ramach tego przewodnika firma Microsoft zaleca, tym "Próbny" lub "Test" w nazwie późniejszym etapie publikowania uwidocznić pakietu publicznie (choć jest mało prawdopodobne, każda osoba będzie faktycznie używać).</span><span class="sxs-lookup"><span data-stu-id="07a39-119">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="07a39-120">Dodaj wszelkie opcjonalne właściwości opisanych na [właściwości metadanych NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="07a39-120">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="07a39-121">Pakiety utworzone do użytku publicznego, należy zwrócić szczególną uwagę na **PackageTags** właściwości, jak tagi pomóc innym odnaleźć pakietu i zrozumieć, co robi.</span><span class="sxs-lookup"><span data-stu-id="07a39-121">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="07a39-122">Uruchom polecenie pakietu</span><span class="sxs-lookup"><span data-stu-id="07a39-122">Run the pack command</span></span>

<span data-ttu-id="07a39-123">Tworzenie pakietu NuGet ( `.nupkg` plik) z projektu, uruchom `dotnet pack` polecenia, które sprzyja wytwarzaniu się odpowiednich projektu automatycznie:</span><span class="sxs-lookup"><span data-stu-id="07a39-123">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="07a39-124">Dane wyjściowe zawierają ścieżkę do `.nupkg` pliku:</span><span class="sxs-lookup"><span data-stu-id="07a39-124">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="07a39-125">Automatyczne generowanie pakietu w kompilacji</span><span class="sxs-lookup"><span data-stu-id="07a39-125">Automatically generate package on build</span></span>

<span data-ttu-id="07a39-126">Aby automatycznie uruchomić `dotnet pack` po uruchomieniu `dotnet build`, Dodaj następujący wiersz do pliku projektu w ramach `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="07a39-126">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="07a39-127">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="07a39-127">Publish the package</span></span>

<span data-ttu-id="07a39-128">Po utworzeniu `.nupkg` pliku opublikujesz go w witrynie nuget.org przy użyciu `dotnet nuget push` polecenia wraz z kluczem API uzyskanych z repozytorium nuget.org.</span><span class="sxs-lookup"><span data-stu-id="07a39-128">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="07a39-129">Uzyskiwanie klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="07a39-129">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="07a39-130">Publikowanie za pomocą polecenia dotnet nuget wypychania</span><span class="sxs-lookup"><span data-stu-id="07a39-130">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="07a39-131">Publikowanie błędy</span><span class="sxs-lookup"><span data-stu-id="07a39-131">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="07a39-132">Zarządzanie opublikowany pakiet</span><span class="sxs-lookup"><span data-stu-id="07a39-132">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="07a39-133">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="07a39-133">Related topics</span></span>

- [<span data-ttu-id="07a39-134">Utwórz pakiet</span><span class="sxs-lookup"><span data-stu-id="07a39-134">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="07a39-135">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="07a39-135">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="07a39-136">Pakiety w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="07a39-136">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="07a39-137">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="07a39-137">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="07a39-138">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="07a39-138">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="07a39-139">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="07a39-139">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="07a39-140">Podpisywanie pakietów</span><span class="sxs-lookup"><span data-stu-id="07a39-140">Signing packages</span></span>](../create-packages/Sign-a-package.md)
