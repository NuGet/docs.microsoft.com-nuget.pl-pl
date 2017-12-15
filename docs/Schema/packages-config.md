---
title: "Odwołanie do pliku packages.config NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 207b9547-4558-41dc-9f3f-4bbdfb1d74e3
description: "W niektórych typów projektów packages.config przechowuje listę pakiety NuGet służące do projektu."
keywords: "Pliku packages.config NuGet, odwołania do pakietu NuGet, zależności NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d851a09fad45ca25edc95ecee496bbf399f5e255
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="1ebbe-104">Odwołanie do pliku Packages.config</span><span class="sxs-lookup"><span data-stu-id="1ebbe-104">packages.config reference</span></span>

<span data-ttu-id="1ebbe-105">`packages.config` Plik jest używany w niektórych typów projektów w celu zachowania listy pakietów odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-105">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="1ebbe-106">Dzięki temu NuGet łatwo przywrócić zależności projektu podczas projektu do innej maszynie, na przykład serwer kompilacji bez tych pakietów.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-106">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

## <a name="schema"></a><span data-ttu-id="1ebbe-107">Schemat</span><span class="sxs-lookup"><span data-stu-id="1ebbe-107">Schema</span></span>

<span data-ttu-id="1ebbe-108">Schemat jest prosty: następujące standardowy nagłówek XML jest jeden `<packages>` węzła, który zawiera co najmniej jeden `<package>` elementy, dla każdego odwołania.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-108">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="1ebbe-109">Każdy `<package>` element może mieć następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="1ebbe-109">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="1ebbe-110">Atrybut</span><span class="sxs-lookup"><span data-stu-id="1ebbe-110">Attribute</span></span> | <span data-ttu-id="1ebbe-111">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1ebbe-111">Required</span></span> | <span data-ttu-id="1ebbe-112">Opis</span><span class="sxs-lookup"><span data-stu-id="1ebbe-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1ebbe-113">identyfikator</span><span class="sxs-lookup"><span data-stu-id="1ebbe-113">id</span></span> | <span data-ttu-id="1ebbe-114">Tak</span><span class="sxs-lookup"><span data-stu-id="1ebbe-114">Yes</span></span> | <span data-ttu-id="1ebbe-115">Identyfikator pakietu, takich jak Newtonsoft.json lub Microsoft.AspNet.Mvc.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-115">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="1ebbe-116">version</span><span class="sxs-lookup"><span data-stu-id="1ebbe-116">version</span></span> | <span data-ttu-id="1ebbe-117">Tak</span><span class="sxs-lookup"><span data-stu-id="1ebbe-117">Yes</span></span> | <span data-ttu-id="1ebbe-118">Dokładną wersję pakietu do zainstalowania, takich jak 3.1.1 lub 4.2.5.11-beta.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-118">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="1ebbe-119">Ciąg wersji musi mieć co najmniej trzech cyfr; czwarty jest opcjonalne, jak jest sufiksem wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-119">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="1ebbe-120">Zakresy są niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-120">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="1ebbe-121">targetFramework</span><span class="sxs-lookup"><span data-stu-id="1ebbe-121">targetFramework</span></span> | <span data-ttu-id="1ebbe-122">Nie</span><span class="sxs-lookup"><span data-stu-id="1ebbe-122">No</span></span> | <span data-ttu-id="1ebbe-123">[Target framework moniker (TFM)](Target-Frameworks.md) do zastosowania podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-123">The [target framework moniker (TFM)](Target-Frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="1ebbe-124">To jest ustawiany do projektu docelowego podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-124">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="1ebbe-125">Dzięki temu różnych `<package>` elementy mogą mieć różne TFMs.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-125">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="1ebbe-126">Na przykład jeśli tworzysz projekt przeznaczony dla platformy .NET w wersji 4.5.2 pakiety zainstalowane w tym momencie użyje TFM z net452.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-126">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="1ebbe-127">Jeśli użytkownik; później Przekieruj projektu 4.6 .NET i dodać więcej pakietów użyje tych TFM net46.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-127">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="1ebbe-128">Niezgodność między docelowym projektu i `targetFramework` atrybutami spowoduje wygenerowanie ostrzeżenia, w tym przypadku można ponownie zainstalować odpowiednich pakietów.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-128">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="1ebbe-129">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="1ebbe-129">allowedVersions</span></span> | <span data-ttu-id="1ebbe-130">Nie</span><span class="sxs-lookup"><span data-stu-id="1ebbe-130">No</span></span> | <span data-ttu-id="1ebbe-131">Dla zakresu dozwolonych wersji tego pakietu zastosowane podczas aktualizacji pakietu (zobacz [wersji uaktualnienie Constraining](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="1ebbe-131">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="1ebbe-132">Robi *nie* wpływają na jakie pakietu jest instalowana podczas instalacji lub operację przywracania.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-132">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="1ebbe-133">Zobacz [wersji pakietu](../reference/package-versioning.md#version-ranges-and-wildcards) składni.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-133">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="1ebbe-134">Interfejs użytkownika PackageManager dodatkowo wyłącza wszystkie wersje poza dozwolonym zakresem.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-134">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="1ebbe-135">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="1ebbe-135">developmentDependency</span></span> | <span data-ttu-id="1ebbe-136">Nie</span><span class="sxs-lookup"><span data-stu-id="1ebbe-136">No</span></span> | <span data-ttu-id="1ebbe-137">Jeśli korzystanie z projektu sam tworzy pakietu NuGet, ustawienie to `true` dla zależności uniemożliwia dołączanie po utworzeniu pakietu odbierającą tego pakietu.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-137">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="1ebbe-138">Wartość domyślna to `false`.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-138">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="1ebbe-139">Przykłady</span><span class="sxs-lookup"><span data-stu-id="1ebbe-139">Examples</span></span>

<span data-ttu-id="1ebbe-140">Następujące `packages.config` odwołuje się do dwóch zależności:</span><span class="sxs-lookup"><span data-stu-id="1ebbe-140">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="1ebbe-141">Następujące `packages.config` odwołuje się do pakietów dziewięć, ale `Microsoft.Net.Compilers` nie zostanie uwzględniony podczas tworzenia pakietu korzystanie z powodu `developmentDependency` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-141">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="1ebbe-142">Odwołanie do Newtonsoft.Json ogranicza również aktualizacji do wersji 8.x i 9.x tylko.</span><span class="sxs-lookup"><span data-stu-id="1ebbe-142">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
