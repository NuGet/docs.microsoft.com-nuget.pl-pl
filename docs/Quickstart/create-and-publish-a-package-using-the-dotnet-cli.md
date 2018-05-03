---
title: Tworzenie i publikowanie pakietu NuGet dotnet interfejsu wiersza polecenia
description: Samouczek wskazówki na temat tworzenia i publikowania za pomocą .NET Core CLI, platformy dotnet pakietu NuGet.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/24/2018
ms.topic: quickstart
ms.openlocfilehash: e47eb5f9b3cd7e915db82f043ebb6190b656fb28
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="dccb8-103">Szybki Start: Tworzenie i publikowanie pakietu (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="dccb8-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="dccb8-104">Jest to prosty proces tworzenia pakietów NuGet z biblioteki klas .NET i opublikować go za pomocą nuget.org `dotnet` interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="dccb8-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dccb8-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dccb8-105">Prerequisites</span></span>

1. <span data-ttu-id="dccb8-106">Zainstaluj [.NET Core SDK](https://www.microsoft.com/net/download/), która obejmuje `dotnet` interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="dccb8-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span>

1. <span data-ttu-id="dccb8-107">[Zarejestruj bezpłatne konto na nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Jeśli nie masz już.</span><span class="sxs-lookup"><span data-stu-id="dccb8-107">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="dccb8-108">Tworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="dccb8-108">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="dccb8-109">Aby przekazać pakiet, musisz potwierdzić konto.</span><span class="sxs-lookup"><span data-stu-id="dccb8-109">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="dccb8-110">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="dccb8-110">Create a class library project</span></span>

<span data-ttu-id="dccb8-111">Można użyć istniejącego projektu biblioteki klas .NET dla kodu, który ma być pakietu lub Utwórz proste w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="dccb8-111">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="dccb8-112">Utwórz folder o nazwie `AppLogger` i zmiany do niego.</span><span class="sxs-lookup"><span data-stu-id="dccb8-112">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="dccb8-113">Utwórz projekt za pomocą `dotnet new classlib`, która używa nazwy folderu bieżącego projektu.</span><span class="sxs-lookup"><span data-stu-id="dccb8-113">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="dccb8-114">Dodaj metadane pakietów do pliku projektu</span><span class="sxs-lookup"><span data-stu-id="dccb8-114">Add package metadata to the project file</span></span>

<span data-ttu-id="dccb8-115">Każdy pakiet NuGet musi manifestu, który opisuje zawartość pakietu i zależności.</span><span class="sxs-lookup"><span data-stu-id="dccb8-115">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="dccb8-116">W ostatnim pakiecie plik manifestu to `.nuspec` pliku, który jest generowany na podstawie właściwości metadanych NuGet, które obejmują w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="dccb8-116">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="dccb8-117">Otwórz plik projektu (`.csproj`) i dodaj następujące minimalne właściwości wewnątrz Kończenie `<PropertyGroup>` tag, zmiana wartości zależnie od potrzeb:</span><span class="sxs-lookup"><span data-stu-id="dccb8-117">Open your project file (`.csproj`) and add the following minimal properties inside the exiting `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="dccb8-118">Nadaj pakietu używany unikatowy identyfikator w nuget.org lub niezależnie od hosta można.</span><span class="sxs-lookup"><span data-stu-id="dccb8-118">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="dccb8-119">W ramach tego przewodnika, zaleca się tym "Sample" lub "Test" w nazwie, ponieważ kolejnych kroków publikowania pakietu widocznego publicznie (chociaż jest mało prawdopodobne, każda osoba, która zostanie rzeczywiście używane).</span><span class="sxs-lookup"><span data-stu-id="dccb8-119">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="dccb8-120">Dodać opcjonalne właściwości opisu w [właściwości metadanych NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="dccb8-120">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="dccb8-121">W przypadku pakietów skompilowany dla publicznych zużycia zwrócić szczególną uwagę na **PackageTags** właściwości, jak tagi ułatwiała innym pakietu odnaleźć i zrozumieć, jakie operacje.</span><span class="sxs-lookup"><span data-stu-id="dccb8-121">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="dccb8-122">Uruchom polecenie pakietu</span><span class="sxs-lookup"><span data-stu-id="dccb8-122">Run the pack command</span></span>

<span data-ttu-id="dccb8-123">Aby utworzyć pakiet NuGet ( `.nupkg` pliku) w projekcie, uruchom `dotnet pack` polecenia, które również automatycznie tworzy projekt:</span><span class="sxs-lookup"><span data-stu-id="dccb8-123">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="dccb8-124">Dane wyjściowe zawierają ścieżki do `.nupkg` pliku:</span><span class="sxs-lookup"><span data-stu-id="dccb8-124">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="dccb8-125">Automatyczne generowanie pakietu podczas kompilacji</span><span class="sxs-lookup"><span data-stu-id="dccb8-125">Automatically generate package on build</span></span>

<span data-ttu-id="dccb8-126">Aby automatycznie uruchomić `dotnet pack` po uruchomieniu `dotnet build`, Dodaj następujący wiersz w pliku projektu w `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="dccb8-126">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="dccb8-127">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="dccb8-127">Publish the package</span></span>

<span data-ttu-id="dccb8-128">Po utworzeniu `.nupkg` pliku opublikowaniu go przy użyciu nuget.org `dotnet nuget push` polecenia wraz z kluczem interfejsu API z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="dccb8-128">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="dccb8-129">Uzyskanie klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="dccb8-129">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="dccb8-130">Publikowanie za pomocą wypychania nuget dotnet</span><span class="sxs-lookup"><span data-stu-id="dccb8-130">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="dccb8-131">Publikowanie błędów</span><span class="sxs-lookup"><span data-stu-id="dccb8-131">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="dccb8-132">Zarządzanie opublikowanego pakietu</span><span class="sxs-lookup"><span data-stu-id="dccb8-132">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="dccb8-133">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="dccb8-133">Related topics</span></span>

- [<span data-ttu-id="dccb8-134">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="dccb8-134">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="dccb8-135">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="dccb8-135">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="dccb8-136">Pakiety wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="dccb8-136">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="dccb8-137">Obsługuje wiele platform docelowych</span><span class="sxs-lookup"><span data-stu-id="dccb8-137">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="dccb8-138">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="dccb8-138">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="dccb8-139">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="dccb8-139">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="dccb8-140">Podpisywanie pakietów</span><span class="sxs-lookup"><span data-stu-id="dccb8-140">Signing packages</span></span>](../create-packages/Sign-a-package.md)
