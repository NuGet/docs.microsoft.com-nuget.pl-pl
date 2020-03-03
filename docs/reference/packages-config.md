---
title: Dokumentacja pliku Packages. config pakietów NuGet
description: W niektórych typach projektów Packages. config obsługuje listę pakietów NuGet używanych w projekcie.
author: karann-msft
ms.author: karann
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 3665989d35d7362b30a106cf6b4ed0210619efee
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230582"
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="e113e-103">Dokumentacja Packages. config</span><span class="sxs-lookup"><span data-stu-id="e113e-103">packages.config reference</span></span>

<span data-ttu-id="e113e-104">Plik `packages.config` jest używany w niektórych typach projektów do obsługi listy pakietów, do których odwołuje się projekt.</span><span class="sxs-lookup"><span data-stu-id="e113e-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="e113e-105">Dzięki temu NuGet może łatwo przywrócić zależności projektu, gdy projekt ma być transportowany do innego komputera, na przykład na serwerze kompilacji, bez wszystkich pakietów.</span><span class="sxs-lookup"><span data-stu-id="e113e-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="e113e-106">Jeśli jest używany, `packages.config` zwykle znajduje się w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="e113e-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="e113e-107">Jest ona tworzona automatycznie podczas uruchamiania pierwszej operacji NuGet, ale można ją również utworzyć ręcznie przed uruchomieniem jakichkolwiek poleceń, takich jak `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="e113e-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="e113e-108">Projekty używające [PackageReference](../consume-packages/Package-References-in-Project-Files.md) nie używają `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="e113e-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="e113e-109">Schemat</span><span class="sxs-lookup"><span data-stu-id="e113e-109">Schema</span></span>

<span data-ttu-id="e113e-110">Schemat jest prosty: poniżej standardowego nagłówka XML jest pojedynczy węzeł `<packages>`, który zawiera co najmniej jeden element `<package>`, jeden dla każdego odwołania.</span><span class="sxs-lookup"><span data-stu-id="e113e-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="e113e-111">Każdy element `<package>` może mieć następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="e113e-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="e113e-112">Atrybut</span><span class="sxs-lookup"><span data-stu-id="e113e-112">Attribute</span></span> | <span data-ttu-id="e113e-113">Wymagany</span><span class="sxs-lookup"><span data-stu-id="e113e-113">Required</span></span> | <span data-ttu-id="e113e-114">Opis</span><span class="sxs-lookup"><span data-stu-id="e113e-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e113e-115">id</span><span class="sxs-lookup"><span data-stu-id="e113e-115">id</span></span> | <span data-ttu-id="e113e-116">Yes</span><span class="sxs-lookup"><span data-stu-id="e113e-116">Yes</span></span> | <span data-ttu-id="e113e-117">Identyfikator pakietu, taki jak Newtonsoft. JSON lub Microsoft. AspNet. MVC.</span><span class="sxs-lookup"><span data-stu-id="e113e-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="e113e-118">version</span><span class="sxs-lookup"><span data-stu-id="e113e-118">version</span></span> | <span data-ttu-id="e113e-119">Yes</span><span class="sxs-lookup"><span data-stu-id="e113e-119">Yes</span></span> | <span data-ttu-id="e113e-120">Dokładna wersja pakietu do zainstalowania, taka jak 3.1.1 lub 4.2.5.11-beta.</span><span class="sxs-lookup"><span data-stu-id="e113e-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="e113e-121">Ciąg wersji musi zawierać co najmniej trzy cyfry; czwarta jest opcjonalna, ponieważ jest sufiksem w wersji wstępnej.</span><span class="sxs-lookup"><span data-stu-id="e113e-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="e113e-122">Zakresy są niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="e113e-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="e113e-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="e113e-123">targetFramework</span></span> | <span data-ttu-id="e113e-124">Nie</span><span class="sxs-lookup"><span data-stu-id="e113e-124">No</span></span> | <span data-ttu-id="e113e-125">[Moniker platformy docelowej (TFM)](target-frameworks.md) , który ma zostać zastosowany podczas instalowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="e113e-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="e113e-126">Jest to początkowo ustawione na obiekt docelowy projektu po zainstalowaniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="e113e-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="e113e-127">W efekcie różne elementy `<package>` mogą mieć różne TFMs.</span><span class="sxs-lookup"><span data-stu-id="e113e-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="e113e-128">Na przykład jeśli tworzysz projekt przeznaczony dla platformy .NET 4.5.2, pakiety zainstalowane w tym punkcie będą korzystały z TFM net452.</span><span class="sxs-lookup"><span data-stu-id="e113e-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="e113e-129">Jeśli użytkownik; później przekieruje projekt do programu .NET 4,6 i doda więcej pakietów, będzie używać TFM z net46.</span><span class="sxs-lookup"><span data-stu-id="e113e-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="e113e-130">Niezgodność między atrybutami docelowymi projektu a `targetFramework` będzie generować ostrzeżenia, w takim przypadku można ponownie zainstalować pakiety, których to dotyczy.</span><span class="sxs-lookup"><span data-stu-id="e113e-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="e113e-131">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="e113e-131">allowedVersions</span></span> | <span data-ttu-id="e113e-132">Nie</span><span class="sxs-lookup"><span data-stu-id="e113e-132">No</span></span> | <span data-ttu-id="e113e-133">Zakres dozwolonych wersji tego pakietu stosowany podczas aktualizacji pakietu (zobacz ograniczenia dotyczące [wersji uaktualnienia](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="e113e-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="e113e-134">*Nie ma to wpływu na* pakiet instalowany podczas operacji instalowania lub przywracania.</span><span class="sxs-lookup"><span data-stu-id="e113e-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="e113e-135">Aby poznać składnię, zobacz [wersja pakietu](../concepts/package-versioning.md#version-ranges) .</span><span class="sxs-lookup"><span data-stu-id="e113e-135">See [Package versioning](../concepts/package-versioning.md#version-ranges) for syntax.</span></span> <span data-ttu-id="e113e-136">Interfejs użytkownika pakietu Packagemanager wyłącza również wszystkie wersje poza dozwolonym zakresem.</span><span class="sxs-lookup"><span data-stu-id="e113e-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="e113e-137">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="e113e-137">developmentDependency</span></span> | <span data-ttu-id="e113e-138">Nie</span><span class="sxs-lookup"><span data-stu-id="e113e-138">No</span></span> | <span data-ttu-id="e113e-139">Jeśli sam projekt będzie tworzył pakiet NuGet, ustawienie tej opcji na `true` dla zależności uniemożliwia uwzględnienie tego pakietu podczas tworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="e113e-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="e113e-140">Wartość domyślna to `false`.</span><span class="sxs-lookup"><span data-stu-id="e113e-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="e113e-141">Przykłady</span><span class="sxs-lookup"><span data-stu-id="e113e-141">Examples</span></span>

<span data-ttu-id="e113e-142">Następujące `packages.config` odnoszą się do dwóch zależności:</span><span class="sxs-lookup"><span data-stu-id="e113e-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="e113e-143">Następujące `packages.config` odnoszą się do dziewięciu pakietów, ale `Microsoft.Net.Compilers` nie będzie uwzględniane podczas kompilowania pakietu zużywanego z powodu atrybutu `developmentDependency`.</span><span class="sxs-lookup"><span data-stu-id="e113e-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="e113e-144">Odwołanie do Newtonsoft. JSON również ogranicza aktualizacje tylko do wersji 8. x i 9. x.</span><span class="sxs-lookup"><span data-stu-id="e113e-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
