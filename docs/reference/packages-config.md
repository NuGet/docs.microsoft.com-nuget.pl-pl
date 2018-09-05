---
title: Odwołanie do pliku packages.config NuGet
description: W niektórych typach projektów packages.config przechowuje listę pakietów NuGet, używany w projekcie.
author: karann-msft
ms.author: karann
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 18566671b611899b28fcc8542cf53935f5ee2dfd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551773"
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="f608c-103">Odwołanie do pliku Packages.config</span><span class="sxs-lookup"><span data-stu-id="f608c-103">packages.config reference</span></span>

<span data-ttu-id="f608c-104">`packages.config` Plik jest używany w niektórych typach projektów do przechowywania listy pakietów przywoływanego przez projekt.</span><span class="sxs-lookup"><span data-stu-id="f608c-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="f608c-105">Dzięki temu NuGet można łatwo przywrócić zależności projektu podczas projektu do innej maszynie, na przykład na serwerze kompilacji, bez tych pakietów.</span><span class="sxs-lookup"><span data-stu-id="f608c-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="f608c-106">Jeśli używane, `packages.config` znajduje się w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="f608c-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="f608c-107">Została ona utworzona automatycznie, gdy pierwszą operacją NuGet jest uruchamiany, ale można również utworzyć ręcznie przed uruchomieniem dowolnych poleceń, takich jak `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="f608c-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="f608c-108">Projekty używające [PackageReference](../consume-packages/Package-References-in-Project-Files.md) nie należy używać `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="f608c-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="f608c-109">Schemat</span><span class="sxs-lookup"><span data-stu-id="f608c-109">Schema</span></span>

<span data-ttu-id="f608c-110">Schemat jest prosty: następujące standardowy nagłówek XML jest pojedynczym `<packages>` węzeł, który zawiera co najmniej jeden `<package>` elementy, po jednym dla każdego odwołania.</span><span class="sxs-lookup"><span data-stu-id="f608c-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="f608c-111">Każdy `<package>` element może mieć następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="f608c-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="f608c-112">Atrybut</span><span class="sxs-lookup"><span data-stu-id="f608c-112">Attribute</span></span> | <span data-ttu-id="f608c-113">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f608c-113">Required</span></span> | <span data-ttu-id="f608c-114">Opis</span><span class="sxs-lookup"><span data-stu-id="f608c-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f608c-115">identyfikator</span><span class="sxs-lookup"><span data-stu-id="f608c-115">id</span></span> | <span data-ttu-id="f608c-116">Tak</span><span class="sxs-lookup"><span data-stu-id="f608c-116">Yes</span></span> | <span data-ttu-id="f608c-117">Identyfikator pakietu, takich jak pakiet Newtonsoft.json lub Microsoft.AspNet.Mvc.</span><span class="sxs-lookup"><span data-stu-id="f608c-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="f608c-118">version</span><span class="sxs-lookup"><span data-stu-id="f608c-118">version</span></span> | <span data-ttu-id="f608c-119">Tak</span><span class="sxs-lookup"><span data-stu-id="f608c-119">Yes</span></span> | <span data-ttu-id="f608c-120">Dokładną wersję pakietu do zainstalowania, takich jak 3.1.1 lub 4.2.5.11-beta.</span><span class="sxs-lookup"><span data-stu-id="f608c-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="f608c-121">Ciąg wersji musi mieć co najmniej trzy cyfry; czwarty jest opcjonalny, ponieważ sufiks wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="f608c-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="f608c-122">Zakresy są niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="f608c-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="f608c-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="f608c-123">targetFramework</span></span> | <span data-ttu-id="f608c-124">Nie</span><span class="sxs-lookup"><span data-stu-id="f608c-124">No</span></span> | <span data-ttu-id="f608c-125">[Docelowe moniker struktury (TFM)](target-frameworks.md) do zastosowania podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="f608c-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="f608c-126">To jest ustawiany na obiekcie docelowym projektu po zainstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="f608c-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="f608c-127">W wyniku innego `<package>` elementy mogą mieć różne krótkich nazw.</span><span class="sxs-lookup"><span data-stu-id="f608c-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="f608c-128">Na przykład jeśli tworzysz projekt przeznaczony dla .NET 4.5.2, pakietów zainstalowanych w tym momencie użyje elementu TFM z net452.</span><span class="sxs-lookup"><span data-stu-id="f608c-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="f608c-129">Jeśli użytkownik; później rzekieruj projekt .NET 4.6 i dodawanie dodatkowych pakietów, użyje tych TFM net46.</span><span class="sxs-lookup"><span data-stu-id="f608c-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="f608c-130">Niezgodność obiektu docelowego projektu i `targetFramework` atrybutami spowoduje wygenerowanie ostrzeżenia, w tym przypadku można ponownie zainstalować pakiety, których to dotyczy.</span><span class="sxs-lookup"><span data-stu-id="f608c-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="f608c-131">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="f608c-131">allowedVersions</span></span> | <span data-ttu-id="f608c-132">Nie</span><span class="sxs-lookup"><span data-stu-id="f608c-132">No</span></span> | <span data-ttu-id="f608c-133">Zakres dozwolonych wersji tego pakietu, stosowane podczas aktualizacji pakietu (zobacz [wersji uaktualnienie Constraining](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="f608c-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="f608c-134">Robi *nie* wpływają na jakie pakiet jest zainstalowany podczas instalacji lub operacji przywracania.</span><span class="sxs-lookup"><span data-stu-id="f608c-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="f608c-135">Zobacz [przechowywanie wersji pakietów](../reference/package-versioning.md#version-ranges-and-wildcards) składni.</span><span class="sxs-lookup"><span data-stu-id="f608c-135">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="f608c-136">Interfejs użytkownika PackageManager wyłącza również wszystkie wersje poza dozwolonym zakresem.</span><span class="sxs-lookup"><span data-stu-id="f608c-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="f608c-137">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="f608c-137">developmentDependency</span></span> | <span data-ttu-id="f608c-138">Nie</span><span class="sxs-lookup"><span data-stu-id="f608c-138">No</span></span> | <span data-ttu-id="f608c-139">W przypadku używania sam projekt tworzy pakiet NuGet, ustawienie tej opcji na `true` dla zależności zapobiega włączaniu po utworzeniu pakietu konsumencki tego pakietu.</span><span class="sxs-lookup"><span data-stu-id="f608c-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="f608c-140">Wartość domyślna to `false`.</span><span class="sxs-lookup"><span data-stu-id="f608c-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="f608c-141">Przykłady</span><span class="sxs-lookup"><span data-stu-id="f608c-141">Examples</span></span>

<span data-ttu-id="f608c-142">Następujące `packages.config` odwołuje się do dwie zależności:</span><span class="sxs-lookup"><span data-stu-id="f608c-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="f608c-143">Następujące `packages.config` odwołuje się do dziewięć pakietów, ale `Microsoft.Net.Compilers` nie zostaną uwzględnione podczas tworzenia pakietu korzystanie z powodu `developmentDependency` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="f608c-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="f608c-144">Odwołanie do pakietu Newtonsoft.Json ogranicza również aktualizacje tylko 8.x i 9.x wersji.</span><span class="sxs-lookup"><span data-stu-id="f608c-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
