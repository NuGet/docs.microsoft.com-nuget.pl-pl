---
title: Tworzenie i publikowanie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet
description: Samouczek instruktażowy dotyczący tworzenia i publikowania pakietu NuGet przy użyciu interfejs wiersza polecenia platformy .NET Core, dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 55f9c760ae05f060b748e6fbb82d8e9bd77c4e37
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825318"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="2e62a-103">Szybki Start: Tworzenie i publikowanie pakietu (interfejs wiersza polecenia dotnet)</span><span class="sxs-lookup"><span data-stu-id="2e62a-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="2e62a-104">Jest to prosty proces tworzenia pakietu NuGet z biblioteki klas .NET i publikowania go do nuget.org przy użyciu interfejsu wiersza polecenia `dotnet` (CLI).</span><span class="sxs-lookup"><span data-stu-id="2e62a-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e62a-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2e62a-105">Prerequisites</span></span>

1. <span data-ttu-id="2e62a-106">Zainstaluj [zestaw .NET Core SDK](https://www.microsoft.com/net/download/), który zawiera `dotnet` interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2e62a-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="2e62a-107">Począwszy od programu Visual Studio 2017, interfejs wiersza polecenia dotnet jest automatycznie instalowany z dowolnymi obciążeniami związanymi z platformą .NET Core.</span><span class="sxs-lookup"><span data-stu-id="2e62a-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="2e62a-108">[Zarejestruj się, aby korzystać z bezpłatnego konta w usłudze NuGet.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) , jeśli jeszcze go nie masz.</span><span class="sxs-lookup"><span data-stu-id="2e62a-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="2e62a-109">Utworzenie nowego konta spowoduje wysłanie wiadomości e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="2e62a-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="2e62a-110">Musisz potwierdzić konto, aby można było przekazać pakiet.</span><span class="sxs-lookup"><span data-stu-id="2e62a-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="2e62a-111">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="2e62a-111">Create a class library project</span></span>

<span data-ttu-id="2e62a-112">Można użyć istniejącego projektu biblioteki klas .NET dla kodu, który ma zostać spakowany, lub utworzyć prosty jeden w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2e62a-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="2e62a-113">Utwórz folder o nazwie `AppLogger`.</span><span class="sxs-lookup"><span data-stu-id="2e62a-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="2e62a-114">Otwórz wiersz polecenia i przejdź do folderu `AppLogger`.</span><span class="sxs-lookup"><span data-stu-id="2e62a-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="2e62a-115">Wpisz `dotnet new classlib`, który używa nazwy bieżącego folderu dla projektu.</span><span class="sxs-lookup"><span data-stu-id="2e62a-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="2e62a-116">Spowoduje to utworzenie nowego projektu.</span><span class="sxs-lookup"><span data-stu-id="2e62a-116">This creates the new project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="2e62a-117">Dodawanie metadanych pakietu do pliku projektu</span><span class="sxs-lookup"><span data-stu-id="2e62a-117">Add package metadata to the project file</span></span>

<span data-ttu-id="2e62a-118">Każdy pakiet NuGet wymaga manifestu opisującego zawartość pakietu i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="2e62a-118">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="2e62a-119">W pakiecie końcowym manifest jest plikiem `.nuspec`, który jest generowany na podstawie właściwości metadanych NuGet, które są zawarte w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="2e62a-119">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="2e62a-120">Otwórz plik projektu (`.csproj`) i Dodaj następujące minimalne właściwości w istniejącym tagu `<PropertyGroup>`, zmieniając wartości zgodnie z potrzebami:</span><span class="sxs-lookup"><span data-stu-id="2e62a-120">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="2e62a-121">Nadaj pakietowi identyfikator, który jest unikatowy w obrębie nuget.org lub dowolnego hosta, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="2e62a-121">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="2e62a-122">W tym instruktażu Zalecamy uwzględnienie "przykładowego" lub "testowego" w nazwie, jak w późniejszym kroku publikowania sprawia, że pakiet jest widoczny publicznie (chociaż prawdopodobnie nikt się nie używa).</span><span class="sxs-lookup"><span data-stu-id="2e62a-122">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="2e62a-123">Dodaj wszystkie opcjonalne właściwości opisane we [właściwościach metadanych NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="2e62a-123">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="2e62a-124">W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na Właściwość **PackageTags** , ponieważ Tagi ułatwiają innym znalezienie pakietu i zrozumienie jego działania.</span><span class="sxs-lookup"><span data-stu-id="2e62a-124">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="2e62a-125">Uruchom pakiet polecenie</span><span class="sxs-lookup"><span data-stu-id="2e62a-125">Run the pack command</span></span>

<span data-ttu-id="2e62a-126">Aby skompilować pakiet NuGet (plik `.nupkg`) z projektu, uruchom polecenie `dotnet pack`, które również automatycznie kompiluje projekt:</span><span class="sxs-lookup"><span data-stu-id="2e62a-126">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="2e62a-127">Dane wyjściowe przedstawiają ścieżkę do pliku `.nupkg`:</span><span class="sxs-lookup"><span data-stu-id="2e62a-127">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="2e62a-128">Automatycznie Generuj pakiet podczas kompilacji</span><span class="sxs-lookup"><span data-stu-id="2e62a-128">Automatically generate package on build</span></span>

<span data-ttu-id="2e62a-129">Aby automatycznie uruchomić `dotnet pack` podczas uruchamiania `dotnet build`, Dodaj następujący wiersz do pliku projektu w `<PropertyGroup>`:</span><span class="sxs-lookup"><span data-stu-id="2e62a-129">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="2e62a-130">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="2e62a-130">Publish the package</span></span>

<span data-ttu-id="2e62a-131">Gdy masz plik `.nupkg`, opublikujesz go w usłudze nuget.org przy użyciu polecenia `dotnet nuget push` wraz z kluczem interfejsu API uzyskanym z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2e62a-131">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="2e62a-132">Pozyskiwanie klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="2e62a-132">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="2e62a-133">Publikowanie przy użyciu wypychania NuGet programu dotnet</span><span class="sxs-lookup"><span data-stu-id="2e62a-133">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="2e62a-134">Błędy publikowania</span><span class="sxs-lookup"><span data-stu-id="2e62a-134">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="2e62a-135">Zarządzanie opublikowanym pakietem</span><span class="sxs-lookup"><span data-stu-id="2e62a-135">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="2e62a-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2e62a-136">Next steps</span></span>

<span data-ttu-id="2e62a-137">Gratulujemy utworzenia pierwszego pakietu NuGet!</span><span class="sxs-lookup"><span data-stu-id="2e62a-137">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2e62a-138">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="2e62a-138">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="2e62a-139">Aby poznać więcej informacji o tym, że pakiet NuGet jest oferowany, wybierz poniższe linki.</span><span class="sxs-lookup"><span data-stu-id="2e62a-139">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="2e62a-140">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="2e62a-140">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="2e62a-141">Pakiety wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="2e62a-141">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="2e62a-142">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="2e62a-142">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="2e62a-143">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="2e62a-143">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="2e62a-144">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="2e62a-144">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="2e62a-145">Tworzenie pakietów symboli</span><span class="sxs-lookup"><span data-stu-id="2e62a-145">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="2e62a-146">Podpisywanie pakietów</span><span class="sxs-lookup"><span data-stu-id="2e62a-146">Signing packages</span></span>](../create-packages/Sign-a-package.md)
