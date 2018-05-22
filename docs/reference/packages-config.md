---
title: Odwołanie do pliku packages.config NuGet
description: W niektórych typów projektów packages.config przechowuje listę pakiety NuGet służące do projektu.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: e10bc1625bc4cea7b7befe18caa22d33a876489b
ms.sourcegitcommit: f0b31af805183cf3a98eabb504e16d9b05223cfe
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 05/22/2018
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="b58f9-103">Odwołanie do pliku Packages.config</span><span class="sxs-lookup"><span data-stu-id="b58f9-103">packages.config reference</span></span>

<span data-ttu-id="b58f9-104">`packages.config` Plik jest używany w niektórych typów projektów w celu zachowania listy pakietów odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="b58f9-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="b58f9-105">Dzięki temu NuGet łatwo przywrócić zależności projektu podczas projektu do innej maszynie, na przykład serwer kompilacji bez tych pakietów.</span><span class="sxs-lookup"><span data-stu-id="b58f9-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="b58f9-106">Jeśli używana, `packages.config` zazwyczaj znajduje się w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="b58f9-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="b58f9-107">Została ona utworzona automatycznie, gdy pierwszej operacji NuGet jest uruchamiany, ale można także utworzyć ręcznie przed uruchomieniem poleceń, takich jak `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="b58f9-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="b58f9-108">Projekty używające [PackageReference](../consume-packages/Package-References-in-Project-Files.md) nie używaj `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="b58f9-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="b58f9-109">Schemat</span><span class="sxs-lookup"><span data-stu-id="b58f9-109">Schema</span></span>

<span data-ttu-id="b58f9-110">Schemat jest prosty: następujące standardowy nagłówek XML jest jeden `<packages>` węzła, który zawiera co najmniej jeden `<package>` elementy, dla każdego odwołania.</span><span class="sxs-lookup"><span data-stu-id="b58f9-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="b58f9-111">Każdy `<package>` element może mieć następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="b58f9-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="b58f9-112">Atrybut</span><span class="sxs-lookup"><span data-stu-id="b58f9-112">Attribute</span></span> | <span data-ttu-id="b58f9-113">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b58f9-113">Required</span></span> | <span data-ttu-id="b58f9-114">Opis</span><span class="sxs-lookup"><span data-stu-id="b58f9-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b58f9-115">identyfikator</span><span class="sxs-lookup"><span data-stu-id="b58f9-115">id</span></span> | <span data-ttu-id="b58f9-116">Tak</span><span class="sxs-lookup"><span data-stu-id="b58f9-116">Yes</span></span> | <span data-ttu-id="b58f9-117">Identyfikator pakietu, takich jak Newtonsoft.json lub Microsoft.AspNet.Mvc.</span><span class="sxs-lookup"><span data-stu-id="b58f9-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="b58f9-118">version</span><span class="sxs-lookup"><span data-stu-id="b58f9-118">version</span></span> | <span data-ttu-id="b58f9-119">Tak</span><span class="sxs-lookup"><span data-stu-id="b58f9-119">Yes</span></span> | <span data-ttu-id="b58f9-120">Dokładną wersję pakietu do zainstalowania, takich jak 3.1.1 lub 4.2.5.11-beta.</span><span class="sxs-lookup"><span data-stu-id="b58f9-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="b58f9-121">Ciąg wersji musi mieć co najmniej trzech cyfr; czwarty jest opcjonalne, jak jest sufiksem wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="b58f9-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="b58f9-122">Zakresy są niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="b58f9-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="b58f9-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="b58f9-123">targetFramework</span></span> | <span data-ttu-id="b58f9-124">Nie</span><span class="sxs-lookup"><span data-stu-id="b58f9-124">No</span></span> | <span data-ttu-id="b58f9-125">[Target framework moniker (TFM)](target-frameworks.md) do zastosowania podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="b58f9-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="b58f9-126">To jest ustawiany do projektu docelowego podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="b58f9-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="b58f9-127">Dzięki temu różnych `<package>` elementy mogą mieć różne TFMs.</span><span class="sxs-lookup"><span data-stu-id="b58f9-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="b58f9-128">Na przykład jeśli tworzysz projekt przeznaczony dla platformy .NET w wersji 4.5.2 pakiety zainstalowane w tym momencie użyje TFM z net452.</span><span class="sxs-lookup"><span data-stu-id="b58f9-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="b58f9-129">Jeśli użytkownik; później Przekieruj projektu 4.6 .NET i dodać więcej pakietów użyje tych TFM net46.</span><span class="sxs-lookup"><span data-stu-id="b58f9-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="b58f9-130">Niezgodność między docelowym projektu i `targetFramework` atrybutami spowoduje wygenerowanie ostrzeżenia, w tym przypadku można ponownie zainstalować odpowiednich pakietów.</span><span class="sxs-lookup"><span data-stu-id="b58f9-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="b58f9-131">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="b58f9-131">allowedVersions</span></span> | <span data-ttu-id="b58f9-132">Nie</span><span class="sxs-lookup"><span data-stu-id="b58f9-132">No</span></span> | <span data-ttu-id="b58f9-133">Dla zakresu dozwolonych wersji tego pakietu zastosowane podczas aktualizacji pakietu (zobacz [wersji uaktualnienie Constraining](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="b58f9-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="b58f9-134">Robi *nie* wpływają na jakie pakietu jest instalowana podczas instalacji lub operację przywracania.</span><span class="sxs-lookup"><span data-stu-id="b58f9-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="b58f9-135">Zobacz [wersji pakietu](../reference/package-versioning.md#version-ranges-and-wildcards) składni.</span><span class="sxs-lookup"><span data-stu-id="b58f9-135">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="b58f9-136">Interfejs użytkownika PackageManager dodatkowo wyłącza wszystkie wersje poza dozwolonym zakresem.</span><span class="sxs-lookup"><span data-stu-id="b58f9-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="b58f9-137">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="b58f9-137">developmentDependency</span></span> | <span data-ttu-id="b58f9-138">Nie</span><span class="sxs-lookup"><span data-stu-id="b58f9-138">No</span></span> | <span data-ttu-id="b58f9-139">Jeśli korzystanie z projektu sam tworzy pakietu NuGet, ustawienie to `true` dla zależności uniemożliwia dołączanie po utworzeniu pakietu odbierającą tego pakietu.</span><span class="sxs-lookup"><span data-stu-id="b58f9-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="b58f9-140">Wartość domyślna to `false`.</span><span class="sxs-lookup"><span data-stu-id="b58f9-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="b58f9-141">Przykłady</span><span class="sxs-lookup"><span data-stu-id="b58f9-141">Examples</span></span>

<span data-ttu-id="b58f9-142">Następujące `packages.config` odwołuje się do dwóch zależności:</span><span class="sxs-lookup"><span data-stu-id="b58f9-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="b58f9-143">Następujące `packages.config` odwołuje się do pakietów dziewięć, ale `Microsoft.Net.Compilers` nie zostanie uwzględniony podczas tworzenia pakietu korzystanie z powodu `developmentDependency` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="b58f9-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="b58f9-144">Odwołanie do Newtonsoft.Json ogranicza również aktualizacji do wersji 8.x i 9.x tylko.</span><span class="sxs-lookup"><span data-stu-id="b58f9-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
