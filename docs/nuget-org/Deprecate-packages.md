---
title: Przestarzałe pakiety w nuget.org
description: Szczegółowy opis procesu wycofywania pakietów i sposobu wyświetlania tych informacji przez klientów
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096884"
---
# <a name="deprecating-packages"></a><span data-ttu-id="f31ac-103">Przestarzałe pakiety</span><span class="sxs-lookup"><span data-stu-id="f31ac-103">Deprecating packages</span></span>

<span data-ttu-id="f31ac-104">Możesz zastąpić pakiet, jeśli już nie przechowujesz pakietu lub chcesz zachęcić odbiorców pakietu do przejścia do innego pakietu.</span><span class="sxs-lookup"><span data-stu-id="f31ac-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="f31ac-105">Wycofanie pakietu jest inne niż Wycofaj **listę** pakietów, jak wyjaśniono poniżej:</span><span class="sxs-lookup"><span data-stu-id="f31ac-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="f31ac-106">**Nielistowanie** pakietu uniemożliwia jego odnajdywanie, ponieważ jest on ukryty w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="f31ac-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="f31ac-107">**Wycofanie** pakietu pozwala istniejącym konsumentom pakietu sprawdzić, czy są one zainstalowane lub używane w projektach.</span><span class="sxs-lookup"><span data-stu-id="f31ac-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="f31ac-108">Pozwala również znać przyczynę wycofania i inny zalecany pakiet określony przez użytkownika (Wydawca pakietu).</span><span class="sxs-lookup"><span data-stu-id="f31ac-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="f31ac-109">Wycofanie pakietu nie powoduje odlistowania pakietu.</span><span class="sxs-lookup"><span data-stu-id="f31ac-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="f31ac-110">Jako wydawca możesz wybrać zarówno opcję unlist, jak i przestarzałe pakiety.</span><span class="sxs-lookup"><span data-stu-id="f31ac-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="f31ac-111">Przepływ pracy wycofania</span><span class="sxs-lookup"><span data-stu-id="f31ac-111">Deprecation workflow</span></span>
1. <span data-ttu-id="f31ac-112">Aby zastąpić pakiet, przejdź do obszaru **Zarządzanie pakietami** i wybierz pozycję **przestarzałe**:</span><span class="sxs-lookup"><span data-stu-id="f31ac-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Przejdź do opcji przestarzały pakiet](media/deprecation-select-option.png)

2. <span data-ttu-id="f31ac-114">Wybierz wersję, którą chcesz wycofać.</span><span class="sxs-lookup"><span data-stu-id="f31ac-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="f31ac-115">Jeśli chcesz zrezygnować z całej wersji, wybierz opcję **Wybierz wszystkie wersje** .</span><span class="sxs-lookup"><span data-stu-id="f31ac-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Wybierz wersje pakietu do wycofania](media/deprecation-select-version.png)

3. <span data-ttu-id="f31ac-117">Wybierz przyczynę wycofania.</span><span class="sxs-lookup"><span data-stu-id="f31ac-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="f31ac-118">Jeśli pakiet nie jest już obsługiwany, wybierz opcję **Starsza wersja** .</span><span class="sxs-lookup"><span data-stu-id="f31ac-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="f31ac-119">Jeśli określona wersja ma krytyczny błąd, wybierz opcję **ma błędy krytyczne** .</span><span class="sxs-lookup"><span data-stu-id="f31ac-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="f31ac-120">Z dowolnego powodu wybierz pozycję **inne**.</span><span class="sxs-lookup"><span data-stu-id="f31ac-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="f31ac-121">Zawsze możesz określić alternatywny, zalecany pakiet (i wersja) oraz niestandardowy komunikat do właścicieli.</span><span class="sxs-lookup"><span data-stu-id="f31ac-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Wybieranie z przyczyn alternatywnego zalecenia pakietu i komunikatu niestandardowego](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="f31ac-123">Komunikat niestandardowy jest wyświetlany tylko w witrynie nuget.org, ale nie z poziomu klientów.</span><span class="sxs-lookup"><span data-stu-id="f31ac-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="f31ac-124">Obecnie klienci tacy jak `dotnet.exe` i Menedżer pakietów NuGet nie wyświetlają komunikatu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="f31ac-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="f31ac-125">Środowisko klienta dla przestarzałych pakietów</span><span class="sxs-lookup"><span data-stu-id="f31ac-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="f31ac-126">Gdy pakiet jest przestarzały, jego konsumenci są powiadamiani o nich w następujący sposób (w zależności od używanego klienta).</span><span class="sxs-lookup"><span data-stu-id="f31ac-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="f31ac-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f31ac-127">Visual Studio</span></span> 
<span data-ttu-id="f31ac-128">*Dostępne począwszy od programu Visual Studio 2019 w wersji 16,3*</span><span class="sxs-lookup"><span data-stu-id="f31ac-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="f31ac-129">Program Visual Studio ostrzega o użyciu przestarzałego pakietu na karcie `Installed`. Spowoduje to wyświetlenie ostrzeżenia dotyczącego pakietu i jego informacji o zaniechaniu (w tym przyczyny jego wycofania oraz alternatywnego pakietu do użycia zamiast tego, jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="f31ac-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Przestarzałe pakiety na karcie zainstalowanej w programie Visual Studio Menedżer pakietów](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="f31ac-131">dotnet. exe</span><span class="sxs-lookup"><span data-stu-id="f31ac-131">dotnet.exe</span></span>
<span data-ttu-id="f31ac-132">*Dostępne począwszy od zestawu .NET SDK 3,0*</span><span class="sxs-lookup"><span data-stu-id="f31ac-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="f31ac-133">Jeśli używasz programu dotnet. exe, możesz uruchomić polecenie `dotnet list package --deprecated` w folderze rozwiązania lub projektu, aby uzyskać listę przestarzałych pakietów wraz z informacjami o zaniechaniu:</span><span class="sxs-lookup"><span data-stu-id="f31ac-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
