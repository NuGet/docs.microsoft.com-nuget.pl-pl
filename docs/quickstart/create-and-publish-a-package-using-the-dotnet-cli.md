---
title: Tworzenie i publikowanie pakietu NuGet przy użyciu interfejsu wiersza polecenia dotnet
description: Samouczek instruktażowy dotyczący tworzenia i publikowania pakietu NuGet przy użyciu interfejsu wiersza polecenia .NET Core, dotnet.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 8c09d6d5662ed6ff0deffa5d45b823ad0992f399
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231308"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="c6981-103">Szybki start: tworzenie i publikowanie pakietu (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="c6981-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="c6981-104">Jest to prosty proces, aby utworzyć pakiet NuGet z biblioteki klas .NET `dotnet` i opublikować go do nuget.org przy użyciu interfejsu wiersza polecenia (CLI).</span><span class="sxs-lookup"><span data-stu-id="c6981-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6981-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c6981-105">Prerequisites</span></span>

1. <span data-ttu-id="c6981-106">Zainstaluj zestaw [SDK .NET](https://www.microsoft.com/net/download/)Core `dotnet` , który zawiera zestaw wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="c6981-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="c6981-107">Począwszy od programu Visual Studio 2017, dotnet interfejsu wiersza polecenia jest automatycznie instalowany z dowolnego .NET Core obciążeń związanych.</span><span class="sxs-lookup"><span data-stu-id="c6981-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="c6981-108">[Zarejestruj się na darmowe konto w nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) jeśli jeszcze go nie masz.</span><span class="sxs-lookup"><span data-stu-id="c6981-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="c6981-109">Utworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="c6981-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="c6981-110">Musisz potwierdzić konto, zanim będzie można przesłać pakiet.</span><span class="sxs-lookup"><span data-stu-id="c6981-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="c6981-111">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="c6981-111">Create a class library project</span></span>

<span data-ttu-id="c6981-112">Można użyć istniejącego projektu biblioteki klas platformy .NET dla kodu, który chcesz spakować, lub utworzyć prosty w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c6981-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="c6981-113">Tworzenie folderu `AppLogger`o nazwie .</span><span class="sxs-lookup"><span data-stu-id="c6981-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="c6981-114">Otwórz wiersz polecenia i `AppLogger` przełącz się do folderu.</span><span class="sxs-lookup"><span data-stu-id="c6981-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="c6981-115">Typ `dotnet new classlib`, który używa nazwy bieżącego folderu dla projektu.</span><span class="sxs-lookup"><span data-stu-id="c6981-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="c6981-116">Spowoduje to utworzenie nowego projektu.</span><span class="sxs-lookup"><span data-stu-id="c6981-116">This creates the new project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="c6981-117">Dodawanie metadanych pakietu do pliku projektu</span><span class="sxs-lookup"><span data-stu-id="c6981-117">Add package metadata to the project file</span></span>

<span data-ttu-id="c6981-118">Każdy pakiet NuGet potrzebuje manifestu, który opisuje zawartość i zależności pakietu.</span><span class="sxs-lookup"><span data-stu-id="c6981-118">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="c6981-119">W pakiecie końcowym manifest jest `.nuspec` plikiem, który jest generowany z właściwości metadanych NuGet, które można uwzględnić w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="c6981-119">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="c6981-120">Otwórz plik projektu`.csproj`( ) i dodaj następujące `<PropertyGroup>` minimalne właściwości wewnątrz istniejącego tagu, zmieniając odpowiednie wartości:</span><span class="sxs-lookup"><span data-stu-id="c6981-120">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="c6981-121">Nadaj pakietowi identyfikator, który jest unikatowy w nuget.org lub dowolnym hostie, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="c6981-121">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="c6981-122">W tym instruktażu zalecamy dołączenie "Przykład" lub "Test" w nazwie, ponieważ późniejszy krok publikowania powoduje, że pakiet jest publicznie widoczny (choć jest mało prawdopodobne, aby ktoś go faktycznie używał).</span><span class="sxs-lookup"><span data-stu-id="c6981-122">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="c6981-123">Dodaj wszystkie opcjonalne właściwości opisane we [właściwościach metadanych NuGet](/dotnet/core/tools/csproj#nuget-metadata-properties).</span><span class="sxs-lookup"><span data-stu-id="c6981-123">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="c6981-124">W przypadku pakietów przeznaczonych do użytku publicznego należy zwrócić szczególną uwagę na **PackageTags** właściwości, jak tagi pomóc innym znaleźć pakiet i zrozumieć, co robi.</span><span class="sxs-lookup"><span data-stu-id="c6981-124">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="c6981-125">Uruchamianie polecenia pack</span><span class="sxs-lookup"><span data-stu-id="c6981-125">Run the pack command</span></span>

<span data-ttu-id="c6981-126">Aby utworzyć pakiet NuGet `.nupkg` (plik) z projektu, uruchom `dotnet pack` polecenie, które również automatycznie tworzy projekt:</span><span class="sxs-lookup"><span data-stu-id="c6981-126">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="c6981-127">Dane wyjściowe pokazują `.nupkg` ścieżkę do pliku:</span><span class="sxs-lookup"><span data-stu-id="c6981-127">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="c6981-128">Automatyczne generowanie pakietu na kompilacji</span><span class="sxs-lookup"><span data-stu-id="c6981-128">Automatically generate package on build</span></span>

<span data-ttu-id="c6981-129">Aby uruchomić `dotnet pack` je automatycznie `dotnet build`po uruchomieniu, dodaj następujący `<PropertyGroup>`wiersz do pliku projektu w obrębie:</span><span class="sxs-lookup"><span data-stu-id="c6981-129">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="c6981-130">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="c6981-130">Publish the package</span></span>

<span data-ttu-id="c6981-131">Po opublikowaniu `.nupkg` pliku, aby opublikować go do `dotnet nuget push` nuget.org przy użyciu polecenia wraz z kluczem interfejsu API nabyte z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="c6981-131">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="c6981-132">Uzyskaj klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="c6981-132">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="c6981-133">Publikuj z dotnet nuget push</span><span class="sxs-lookup"><span data-stu-id="c6981-133">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="c6981-134">Błędy publikowania</span><span class="sxs-lookup"><span data-stu-id="c6981-134">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="c6981-135">Zarządzanie opublikowanym pakietem</span><span class="sxs-lookup"><span data-stu-id="c6981-135">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-video"></a><span data-ttu-id="c6981-136">Podobne wideo</span><span class="sxs-lookup"><span data-stu-id="c6981-136">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-the-NET-CLI-5-of-5/player]

<span data-ttu-id="c6981-137">Znajdź więcej filmów NuGet na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) i [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="c6981-137">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6981-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6981-138">Next steps</span></span>

<span data-ttu-id="c6981-139">Gratulujemy stworzenia pierwszego pakietu NuGet!</span><span class="sxs-lookup"><span data-stu-id="c6981-139">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c6981-140">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="c6981-140">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="c6981-141">Aby dowiedzieć się więcej, że NuGet ma do zaoferowania, wybierz poniższe łącza.</span><span class="sxs-lookup"><span data-stu-id="c6981-141">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="c6981-142">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="c6981-142">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="c6981-143">Pakiety w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="c6981-143">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="c6981-144">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="c6981-144">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="c6981-145">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="c6981-145">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="c6981-146">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="c6981-146">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="c6981-147">Tworzenie pakietów symboli</span><span class="sxs-lookup"><span data-stu-id="c6981-147">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="c6981-148">Podpisywanie pakietów</span><span class="sxs-lookup"><span data-stu-id="c6981-148">Signing packages</span></span>](../create-packages/Sign-a-package.md)
