---
title: Przestarzałe pakiety na nuget.org
description: Szczegółowy opis procesu przestarzałości pakietów i sposobu, w jaki klienci pokazują te informacje
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096884"
---
# <a name="deprecating-packages"></a><span data-ttu-id="db178-103">Przestarzałe pakiety</span><span class="sxs-lookup"><span data-stu-id="db178-103">Deprecating packages</span></span>

<span data-ttu-id="db178-104">Możesz przestarzałe pakiet, jeśli nie prowadzisz już pakietu lub jeśli chcesz zachęcić konsumentów pakietu do przejścia do innego pakietu.</span><span class="sxs-lookup"><span data-stu-id="db178-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="db178-105">Wycofanie pakietu różni się od **nienaszacowania** pakietu, jak wyjaśniono poniżej:</span><span class="sxs-lookup"><span data-stu-id="db178-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="db178-106">**Odsuwanie** pakietu z listy uniemożliwia jego odnajdowanie, ponieważ jest on ukryty w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="db178-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="db178-107">**Przestarzałe rozwiązanie** pakietu pozwala istniejącym odbiorcom pakietu dowiedzieć się, czy mają go zainstalowany lub używany w swoich projektach.</span><span class="sxs-lookup"><span data-stu-id="db178-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="db178-108">Pozwala im również znać przyczynę wycofania i alternatywny zalecany pakiet określony przez Ciebie (wydawca pakietu).</span><span class="sxs-lookup"><span data-stu-id="db178-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="db178-109">Przestarzałe pakiet nie powoduje wykreślenia pakietu z listy.</span><span class="sxs-lookup"><span data-stu-id="db178-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="db178-110">Jako wydawca możesz wybrać zarówno niepubliczne, jak i przestarzałe pakiety.</span><span class="sxs-lookup"><span data-stu-id="db178-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="db178-111">Przepływ pracy deprecation</span><span class="sxs-lookup"><span data-stu-id="db178-111">Deprecation workflow</span></span>
1. <span data-ttu-id="db178-112">Aby przestarzałe pakiet, przejdź do **zarządzania pakietami** i wybierz **opcję Zaniechanie:**</span><span class="sxs-lookup"><span data-stu-id="db178-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Przejdź do opcji przestarzałego pakietu](media/deprecation-select-option.png)

2. <span data-ttu-id="db178-114">Wybierz wersję, którą chcesz przestarzałe.</span><span class="sxs-lookup"><span data-stu-id="db178-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="db178-115">Jeśli chcesz przestarzałe wszystkie wersje, wybierz wybierz **wszystkie wersje** opcji.</span><span class="sxs-lookup"><span data-stu-id="db178-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Wybieranie wersji pakietów do przestarzałości](media/deprecation-select-version.png)

3. <span data-ttu-id="db178-117">Wybierz przyczynę wycofania.</span><span class="sxs-lookup"><span data-stu-id="db178-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="db178-118">Jeśli pakiet nie jest już utrzymywany, wybierz opcję **Starsza.**</span><span class="sxs-lookup"><span data-stu-id="db178-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="db178-119">Jeśli określona wersja ma błąd krytyczny, wybierz opcję **ma krytyczne błędy.**</span><span class="sxs-lookup"><span data-stu-id="db178-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="db178-120">Z dowolnego innego powodu wybierz opcję **Inne**.</span><span class="sxs-lookup"><span data-stu-id="db178-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="db178-121">Zawsze można określić alternatywny zalecany pakiet (i wersję) i niestandardowy komunikat do właścicieli.</span><span class="sxs-lookup"><span data-stu-id="db178-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Wybierz powody alternatywnego pakietu rekomendacji i wiadomości niestandardowej](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="db178-123">Wiadomość niestandardowa jest wyświetlana tylko na nuget.org ale nie od klientów.</span><span class="sxs-lookup"><span data-stu-id="db178-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="db178-124">Obecnie klienci, tacy `dotnet.exe` jak i Menedżer pakietów NuGet, nie wyświetlają wiadomości niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="db178-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="db178-125">Obsługa klienta dla przestarzałych pakietów</span><span class="sxs-lookup"><span data-stu-id="db178-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="db178-126">Gdy pakiet został przestarzały, jego konsumenci są powiadamiani o tym w następujący sposób (w zależności od używanego klienta).</span><span class="sxs-lookup"><span data-stu-id="db178-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="db178-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="db178-127">Visual Studio</span></span> 
<span data-ttu-id="db178-128">*Dostępne od wersji Visual Studio 2019 w wersji 16.3*</span><span class="sxs-lookup"><span data-stu-id="db178-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="db178-129">Visual Studio ostrzega o użyciu przestarzałego `Installed` pakietu na karcie. Wyświetli ostrzeżenie dla pakietu i jego informacje o umorzyniu (w tym powód, dla którego został przestarzały i alternatywny pakiet do użycia zamiast tego, jeśli jest obecny).</span><span class="sxs-lookup"><span data-stu-id="db178-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Przestarzałe pakiety w programie Visual Studio zainstalowanej karty Menedżera pakietów](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="db178-131">plik dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="db178-131">dotnet.exe</span></span>
<span data-ttu-id="db178-132">*Dostępne począwszy od .NET SDK 3.0*</span><span class="sxs-lookup"><span data-stu-id="db178-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="db178-133">Jeśli używasz dotnet.exe, można `dotnet list package --deprecated` uruchomić polecenie w folderze rozwiązania lub projektu, aby uzyskać listę przestarzałych pakietów wraz z informacjami o umorzazaniu:</span><span class="sxs-lookup"><span data-stu-id="db178-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
