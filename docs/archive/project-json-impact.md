---
title: "Project.JSON wpływ na autora pakietu NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Więcej informacji na temat formatu implementacja project.json w NuGet 3.x wpływa na autora pakietu, takich jak nieobsługiwane funkcje zawartości i pakietu."
keywords: "Pakiet NuGet i project.json, wpływ project.json tworzenia zagadnienia, funkcje project.json"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6104b4dac330869bc5724ffcf15cc0ac9ee26c1f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="6e1bc-104">Wpływ project.json podczas tworzenia pakietów</span><span class="sxs-lookup"><span data-stu-id="6e1bc-104">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="6e1bc-105">Ta zawartość jest przestarzały.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-105">This content is deprecated.</span></span> <span data-ttu-id="6e1bc-106">Projekty powinny używać albo `packages.config` lub PackageReference formatów.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-106">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="6e1bc-107">`project.json` System używany w NuGet 3 + wpływa na autora pakietu na kilka sposobów, zgodnie z opisem w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-107">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="6e1bc-108">Zmiany mające wpływ na istniejące pakiety użycie</span><span class="sxs-lookup"><span data-stu-id="6e1bc-108">Changes affecting existing packages usage</span></span>

<span data-ttu-id="6e1bc-109">Tradycyjne pakiety NuGet obsługuje zestaw funkcji, które nie są przenoszone do przechodnie world.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-109">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="6e1bc-110">Instalowanie i odinstalowywanie skrypty są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-110">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="6e1bc-111">Model przechodnie przywracania, opisanego w [rozpoznawania zależności](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), nie ma pojęcie "Godzina instalacji pakietu".</span><span class="sxs-lookup"><span data-stu-id="6e1bc-111">The transitive restore model, described in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="6e1bc-112">Pakiet jest obecny lub nie jest obecne, ale nie ma żadnych procesów spójne, gdy jest zainstalowany pakiet.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-112">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="6e1bc-113">Ponadto Zainstaluj skrypty są obsługiwane tylko w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-113">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="6e1bc-114">Inne IDEs musiały mock rozszerzalności programu Visual Studio interfejsu API na próbę obsługiwać te skrypty i nie obsługuje był dostępny w typowych edytory i narzędzia wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-114">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="6e1bc-115">Transformacje zawartości nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-115">Content transforms are not supported</span></span>

<span data-ttu-id="6e1bc-116">Podobnie jak instalowanie skryptów, transformacje Uruchom w pakiecie instalacji i nie są zwykle idempotentności.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-116">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="6e1bc-117">Ponieważ nie istnieje już nie czas instalacji, XDT transformacji i podobne funkcje nie są obsługiwane i są ignorowane, jeśli taki pakiet jest używany w scenariuszu przechodnie.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-117">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="6e1bc-118">Zawartość</span><span class="sxs-lookup"><span data-stu-id="6e1bc-118">Content</span></span>

<span data-ttu-id="6e1bc-119">Tradycyjne pakiety NuGet są wysyłania plików zawartości, takich jak kodu źródłowego i pliki konfiguracyjne.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-119">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="6e1bc-120">Są zwykle używane w przypadku dwóch scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="6e1bc-120">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="6e1bc-121">Pliki początkowe upuścić na projektu, więc użytkownik może edytować je w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-121">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="6e1bc-122">Typowym przykładem są pliki konfiguracji domyślnej.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-122">The common example is default configuration files.</span></span>

1. <span data-ttu-id="6e1bc-123">Pliki zawartości są używane jako towarzyszami do zestawów zainstalowanych w projekcie.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-123">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="6e1bc-124">W tym przykładzie będzie używana przez zestaw obraz logo.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-124">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="6e1bc-125">Obsługa zawartości jest obecnie wyłączona podobnych przyczyn dla skryptów i transformacje, ale trwa projektowania obsługę zawartości.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-125">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="6e1bc-126">Zawartość plików może nadal znajdować się wewnątrz pakietów i są ignorowane obecnie, jednak użytkownik końcowy może nadal skopiuj je do odpowiednim miejscem.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-126">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="6e1bc-127">Znajduje się propozycje ponownie Przywracanie plików zawartości i wykonaj jego postępu, w tym miejscu: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span><span class="sxs-lookup"><span data-stu-id="6e1bc-127">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="6e1bc-128">Wpływ dla autorów pakietu</span><span class="sxs-lookup"><span data-stu-id="6e1bc-128">Impact for package authors</span></span>

<span data-ttu-id="6e1bc-129">Pakiety przy użyciu funkcji powyżej musi używać różnych mechanizmów.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-129">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="6e1bc-130">Najczęściej przydatne mechanizm ten będzie MSBuild celów/arkuszy właściwości, które w dalszym ciągu uzyskać w pełni obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-130">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="6e1bc-131">System kompilacji można wybrać do pobrania innych Konwencji w pakiecie.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-131">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="6e1bc-132">Jest to, jak docelowych elementów MSBuild są obsługiwane, jak również analizatory Roslyn.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-132">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="6e1bc-133">Istnieje możliwość tworzenia pakietów, które obsługuje cele i analizatorów dla `packages.config` i `project.json` scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-133">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="6e1bc-134">Pakiety, które próbuje zmodyfikować projektu, aby ułatwić uruchamiania zwykle działają w bardzo ograniczony zestaw scenariusze, a zamiast tego powinien udostępnić plik readme lub wskazówki dotyczące sposobu używania pakietu.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-134">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="6e1bc-135">Większość istniejących pakietów nie jest konieczna Użyj formatu pakietu opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-135">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="6e1bc-136">Format umożliwia natywnego zawartości jako pierwszej klasie scenariusza.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-136">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="6e1bc-137">Oznacza to, że zarządzane zestawy w zależności od bliski implementacje sprzętu na potrzeby wysłania binarne implementacje równolegle z zarządzanych zestawów oparte na platformie docelowej.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-137">This means that managed assemblies depending on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="6e1bc-138">Na przykład pakiet System.IO.Compression jest przy użyciu tej technologii.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-138">For example System.IO.Compression package is utilizing this technology.</span></span> [<span data-ttu-id="6e1bc-139">https://www.nuget.org/packages/System.IO.Compression</span><span class="sxs-lookup"><span data-stu-id="6e1bc-139">https://www.nuget.org/packages/System.IO.Compression</span></span>](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="6e1bc-140">W podsumowaniu Jeśli powyżej funkcji nie jest to konieczne, zalecamy spełni format istniejącego pakietu, format opisany jest obsługiwana tylko przez NuGet 3.x+.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-140">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="6e1bc-141">Będzie można skompilować pakiety w celu pracy dla obu `packages.config` i `project.json` scenariuszy za pośrednictwem shimming, jednak często łatwiej jest po prostu struktury pakiety w tradycyjny sposób, bez przestarzałe funkcje wymienione powyżej.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-141">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="6e1bc-142">format pakietu 3.x</span><span class="sxs-lookup"><span data-stu-id="6e1bc-142">3.x package format</span></span>

<span data-ttu-id="6e1bc-143">Format pakietu 3.x pozwala na kilka dodatkowych funkcji poza NuGet 2.x:</span><span class="sxs-lookup"><span data-stu-id="6e1bc-143">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="6e1bc-144">Definiowanie zestawu odwołania używany dla kompilacji i zestaw używany do środowiska uruchomieniowego na różnych platformach/urządzeń zestawy implementacji.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-144">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="6e1bc-145">Co pozwala korzystać z platformy określonych interfejsów API, zapewniając wspólnej powierzchni przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-145">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="6e1bc-146">W szczególności w ten sposób zapisywania pośredniego bibliotek przenośnych łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-146">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="6e1bc-147">Umożliwia pakietów do tabeli przestawnej — na platformach np. systemy operacyjne i architektury Procesora.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-147">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="6e1bc-148">Umożliwia rozdzielenie implementacji określonych platform do pakietów pomocnika.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-148">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="6e1bc-149">Obsługa natywnego zależności jako pierwszej klasie obywateli.</span><span class="sxs-lookup"><span data-stu-id="6e1bc-149">Support Native dependencies as a first class citizen.</span></span>