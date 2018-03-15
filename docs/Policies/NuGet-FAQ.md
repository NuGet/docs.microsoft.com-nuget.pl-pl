---
title: "NuGet często zadawane pytania | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/11/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Typowe pytania i odpowiedzi przy użyciu narzędzia NuGet w wierszu polecenia, a w programie Visual Studio i pracy z galerii NuGet."
keywords: "Wersje pakietu NuGet pytań i odpowiedzi, pytania i odpowiedzi, typowe problemy, wersje NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3782fe5dcf8df002d99446aa7548a6eacc62211c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/15/2018
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="5c46d-104">NuGet często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="5c46d-104">NuGet frequently-asked questions</span></span>

<span data-ttu-id="5c46d-105">**Co to jest wymagany do uruchamiania NuGet?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-105">**What is required to run NuGet?**</span></span>

<span data-ttu-id="5c46d-106">Wszystkie informacje dotyczące narzędzia wiersza polecenia i interfejsu użytkownika są dostępne w [Przewodnik instalacji](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="5c46d-106">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="5c46d-107">**NuGet obsługuje Mono?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-107">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="5c46d-108">Narzędzie wiersza polecenia `nuget.exe`, tworzy i uruchamiana Mono 3.2 + oraz pakiety można tworzyć w Mono.</span><span class="sxs-lookup"><span data-stu-id="5c46d-108">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="5c46d-109">Mimo że `nuget.exe` działa w pełni w systemie Windows, istnieją znane problemy w systemie Linux i OS X. znajduje się w [wystawia Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="5c46d-109">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="5c46d-110">A [graficznego klienta](https://github.com/mrward/monodevelop-nuget-addin) jest dostępna jako dodatek do MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="5c46d-110">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="5c46d-111">**Jak można określić pakiet zawiera i czy jest ona stabilna i przydatne w przypadku mojej aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-111">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="5c46d-112">Podstawowym źródłem szkoleniowe dotyczące pakietu jest stroną listy na nuget.org (lub innej prywatnej źródła danych).</span><span class="sxs-lookup"><span data-stu-id="5c46d-112">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="5c46d-113">Każda strona pakietu na nuget.org zawiera opis pakietu, jego Historia wersji i statystyki użycia.</span><span class="sxs-lookup"><span data-stu-id="5c46d-113">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="5c46d-114">**Informacji** sekcja na stronie pakiet zawiera również link do witryny sieci web projektu, w którym zwykle znaleźć wiele przykłady i inne dokumentacji, aby uzyskać więcej informacji, sposobu używania pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c46d-114">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="5c46d-115">Aby uzyskać więcej informacji, zobacz [wyszukiwanie i Wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="5c46d-115">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="5c46d-116">NuGet w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5c46d-116">NuGet in Visual Studio</span></span>

<span data-ttu-id="5c46d-117">**Jak NuGet jest obsługiwane w różnych produktów Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-117">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="5c46d-118">Program Visual Studio w systemie Windows obsługuje [interfejsu użytkownika Menedżera pakietów](../tools/package-manager-ui.md) i [Konsola Menedżera pakietów](../tools/package-manager-console.md).</span><span class="sxs-lookup"><span data-stu-id="5c46d-118">Visual Studio on Windows supports the [Package Manager UI](../tools/package-manager-ui.md) and the [Package Manager Console](../tools/package-manager-console.md).</span></span>
- <span data-ttu-id="5c46d-119">Visual Studio for Mac ma wbudowane funkcje NuGet, zgodnie z opisem na [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="5c46d-119">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="5c46d-120">Visual Studio Code (wszystkie platformy) nie ma żadnych bezpośrednich integracji z programem NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c46d-120">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="5c46d-121">Użyj [interfejsu wiersza polecenia NuGet](../tools/nuget-exe-cli-reference.md) lub [dotnet interfejsu wiersza polecenia](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="5c46d-121">Use the [NuGet CLI](../tools/nuget-exe-cli-reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="5c46d-122">Visual Studio Team Services zapewnia [kroku kompilacji pod kątem przywracania pakietów NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="5c46d-122">Visual Studio Team Services provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="5c46d-123">Możesz również [pakietu NuGet prywatnych hosta źródła na Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="5c46d-123">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="5c46d-124">**Jak sprawdzić dokładnej wersji narzędzia NuGet, które są zainstalowane**</span><span class="sxs-lookup"><span data-stu-id="5c46d-124">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="5c46d-125">W programie Visual Studio, użyj **Pomoc > Microsoft Visual Studio** polecenia i przyjrzyj się wersja wyświetlana obok **Menedżera pakietów NuGet**.</span><span class="sxs-lookup"><span data-stu-id="5c46d-125">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="5c46d-126">Można również uruchomić konsoli Menedżera pakietów (**Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów**), a następnie wprowadź `$host` Aby wyświetlić informacje o tym wersję NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c46d-126">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="5c46d-127">**Jakich języków programowania są obsługiwane przez narzędzie NuGet?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-127">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="5c46d-128">NuGet zwykle działa w przypadku języków .NET i jest przeznaczony do bibliotek .NET do projektu.</span><span class="sxs-lookup"><span data-stu-id="5c46d-128">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="5c46d-129">Ponieważ obsługuje ona również automatyzacji MSBuild i Visual Studio w niektórych typów projektów, obsługuje ona również inne projekty i języki do różnych stopni.</span><span class="sxs-lookup"><span data-stu-id="5c46d-129">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="5c46d-130">Najnowszą wersję programu NuGet obsługuje C#, Visual Basic, F #, WiX i C++.</span><span class="sxs-lookup"><span data-stu-id="5c46d-130">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="5c46d-131">**Szablony projektów, które są obsługiwane przez narzędzie NuGet?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-131">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="5c46d-132">NuGet zawiera pełną obsługę różnych szablonów projektu, takie jak Windows, sieci Web, chmur, SharePoint, Wix i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="5c46d-132">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="5c46d-133">**Jak zaktualizować pakiety, które są częścią szablony programu Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-133">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="5c46d-134">Przejdź do **aktualizacje** w Interfejsie użytkownika Menedżera pakietów i zaznacz **Aktualizuj wszystkie**, lub użyj [ `Update-Package` polecenia](../tools/ps-ref-update-package.md) w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="5c46d-134">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="5c46d-135">Aby zaktualizować samego szablonu, należy ręcznie zaktualizować repozytorium szablonu.</span><span class="sxs-lookup"><span data-stu-id="5c46d-135">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="5c46d-136">Zobacz [blog Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) na ten temat.</span><span class="sxs-lookup"><span data-stu-id="5c46d-136">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="5c46d-137">Uwaga to zrobić na własne ryzyko, ponieważ ręcznej aktualizacji może spowodować uszkodzenie szablonu, jeśli najnowszą wersję wszystkich zależności nie są zgodne ze sobą.</span><span class="sxs-lookup"><span data-stu-id="5c46d-137">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="5c46d-138">**Można użyć NuGet poza programu Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-138">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="5c46d-139">Tak, NuGet działa bezpośrednio z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5c46d-139">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="5c46d-140">Zobacz [Przewodnik instalacji](../install-nuget-client-tools.md) i [odwołania interfejsu wiersza polecenia](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="5c46d-140">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="5c46d-141">Wiersz polecenia NuGet</span><span class="sxs-lookup"><span data-stu-id="5c46d-141">NuGet command line</span></span>

<span data-ttu-id="5c46d-142">**Jak uzyskać najnowszą wersję narzędzia wiersza polecenia NuGet?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-142">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="5c46d-143">Zobacz [Przewodnik instalacji](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="5c46d-143">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="5c46d-144">**Co to jest licencja na nuget.exe?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-144">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="5c46d-145">Możesz wykonać ponowną dystrybucję nuget.exe zgodnie z warunkami licencji MIT.</span><span class="sxs-lookup"><span data-stu-id="5c46d-145">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="5c46d-146">Jest odpowiedzialny za aktualizacji i obsługi kopie nuget.exe, który chcesz ponownie rozesłać.</span><span class="sxs-lookup"><span data-stu-id="5c46d-146">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="5c46d-147">**Czy jest możliwe rozszerzenie NuGet narzędzia wiersza polecenia**</span><span class="sxs-lookup"><span data-stu-id="5c46d-147">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="5c46d-148">Tak, istnieje możliwość dodawania niestandardowych poleceń do `nuget.exe`, zgodnie z opisem w [post Tomasz Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="5c46d-148">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="5c46d-149">Konsola Menedżera pakietów NuGet (Visual Studio w systemie Windows)</span><span class="sxs-lookup"><span data-stu-id="5c46d-149">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="5c46d-150">**Jak uzyskać dostęp do obiektu DTE w konsoli Menedżera pakietów?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-150">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="5c46d-151">Obiekt najwyższego poziomu w modelu obiektu automatyzacji programu Visual Studio jest wywołać obiekt DTE (Development Tools Environment).</span><span class="sxs-lookup"><span data-stu-id="5c46d-151">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="5c46d-152">Zapewnia to za pośrednictwem zmiennej o nazwie konsoli `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="5c46d-152">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="5c46d-153">Aby uzyskać więcej informacji, zobacz [omówienie modelu automatyzacji](/visualstudio/extensibility/internals/automation-model-overview) w dokumentacji programu Visual Studio Extensibility.</span><span class="sxs-lookup"><span data-stu-id="5c46d-153">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="5c46d-154">**Próbie rzutowania $DTE zmienną typu DTE2, ale występuje błąd: nie można przekonwertować wartości "EnvDTE.DTEClass" typu "EnvDTE.DTEClass" na typ "EnvDTE80.DTE2". Co jest nie tak?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-154">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="5c46d-155">Jest to znany problem dotyczący współdziałania programu PowerShell z obiektu COM.</span><span class="sxs-lookup"><span data-stu-id="5c46d-155">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="5c46d-156">Spróbuj wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5c46d-156">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="5c46d-157">`Get-Interface` Funkcja pomocnika jest dodawany przez hosta programu NuGet PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5c46d-157">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="5c46d-158">Tworzenie i publikowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="5c46d-158">Creating and publishing packages</span></span>

<span data-ttu-id="5c46d-159">**Jak wyświetlić listę Mój pakiet w źródło danych?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-159">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="5c46d-160">Zobacz [tworzenie i publikowania pakietu](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="5c46d-160">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="5c46d-161">**Mam wiele wersji biblioteki, które odnoszą się do różnych wersji programu .NET Framework. Jak zbudować pojedynczy pakiet, który obsługuje tę funkcję?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-161">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="5c46d-162">Zobacz [obsługi wielu wersje programu .NET Framework i profile](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="5c46d-162">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="5c46d-163">**Jak skonfigurować własną repozytorium lub źródła danych?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-163">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="5c46d-164">Zobacz [hostingu — Omówienie pakietów](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c46d-164">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="5c46d-165">**Jak przesłać pakiety do mojego NuGet źródła danych zbiorczych**</span><span class="sxs-lookup"><span data-stu-id="5c46d-165">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="5c46d-166">Zobacz [zbiorcze publikowania pakietów NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="5c46d-166">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="5c46d-167">Praca z pakietami</span><span class="sxs-lookup"><span data-stu-id="5c46d-167">Working with packages</span></span>

<span data-ttu-id="5c46d-168">**Jaka jest różnica między pakietem poziom projektu i pakietu poziomu rozwiązania?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-168">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="5c46d-169">Pakiet rozwiązanie na poziomie (NuGet 3.x+) jest zainstalowana tylko raz w rozwiązaniu i jest dostępna dla wszystkich projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="5c46d-169">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="5c46d-170">Pakiet poziom projektu jest zainstalowany w każdym projekcie, który korzysta z niego.</span><span class="sxs-lookup"><span data-stu-id="5c46d-170">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="5c46d-171">Pakiet poziomu rozwiązania może również zainstalować nowych poleceń, które mogą być wywoływane z poziomu konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="5c46d-171">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="5c46d-172">**Czy jest możliwe, można zainstalować pakietów NuGet bez łączności z Internetem?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-172">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="5c46d-173">Tak, zobacz Scott Hanselman blogu [sposobu dostępu NuGet, gdy działa nuget.org (lub jesteś na płaszczyźnie)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="5c46d-173">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="5c46d-174">**Jak zainstalować pakiety w innej lokalizacji niż domyślny folder pakiety?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-174">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="5c46d-175">Ustaw [ `repositoryPath` ](../reference/nuget-config-file.md#config-section) w `Nuget.Config` przy użyciu `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="5c46d-175">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="5c46d-176">**Jak uniknąć dodawania do folderu pakietów NuGet do kontroli źródła**</span><span class="sxs-lookup"><span data-stu-id="5c46d-176">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="5c46d-177">Ustaw [ `disableSourceControlIntegration` ](../reference/nuget-config-file.md#solution-section) w `Nuget.Config` do `true`.</span><span class="sxs-lookup"><span data-stu-id="5c46d-177">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="5c46d-178">Ta działa klucza w rozwiązaniu poziomu i dlatego musi zostać dodany do `$(Solutiondir)\.nuget\Nuget.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="5c46d-178">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="5c46d-179">Włączanie Przywracanie pakietu z programu Visual Studio automatycznie tworzy ten plik.</span><span class="sxs-lookup"><span data-stu-id="5c46d-179">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="5c46d-180">**Jak wyłączyć przywracania pakietu**</span><span class="sxs-lookup"><span data-stu-id="5c46d-180">**How do I turn off package restore?**</span></span>

<span data-ttu-id="5c46d-181">Zobacz [Włączanie i wyłączanie Przywracanie pakietu](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="5c46d-181">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="5c46d-182">**Dlaczego otrzymuję błąd "Nie można rozpoznać zależności błąd" podczas instalowania lokalnego pakietu z zależności zdalnych?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-182">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="5c46d-183">Musisz wybrać **wszystkie** źródła podczas instalowania lokalnego pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="5c46d-183">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="5c46d-184">To agreguje wszystkich źródeł danych zamiast przy użyciu tylko jednego.</span><span class="sxs-lookup"><span data-stu-id="5c46d-184">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="5c46d-185">Przyczyna ten błąd pojawia się jest, że użytkownicy lokalnego repozytorium często chcą uniknąć przypadkowego instalowania zdalnego pakietu z powodu firmowe zasady.</span><span class="sxs-lookup"><span data-stu-id="5c46d-185">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="5c46d-186">**Mam wiele projektów, w tym samym folderze, do czego służy packages.config oddzielne pliki dla każdego projektu?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-186">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="5c46d-187">W większości projektów miejsca zamieszkania osobne projekty w oddzielnych folderach, nie jest to problem jak identyfikuje NuGet `packages.config` plików w każdym projekcie.</span><span class="sxs-lookup"><span data-stu-id="5c46d-187">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="5c46d-188">Nuget 3.3 + i jest wiele projektów, w tym samym folderze, można wstawić nazwę projektu w `packages.config` nazw plików, użyj wzorca `packages.{project-name}.config`, i NuGet korzysta z tego pliku.</span><span class="sxs-lookup"><span data-stu-id="5c46d-188">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="5c46d-189">To nie jest problem przy użyciu PackageReference, ponieważ każdy plik projektu zawiera własną listę zależności.</span><span class="sxs-lookup"><span data-stu-id="5c46d-189">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="5c46d-190">**Nuget.org nie jest wyświetlane na liście repozytoriów, jak pobrać go ponownie?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-190">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="5c46d-191">Dodaj `https://api.nuget.org/v3/index.json` do listy źródeł, lub</span><span class="sxs-lookup"><span data-stu-id="5c46d-191">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="5c46d-192">Usuń `%appdata%\.nuget\NuGet.Config` (system Windows) lub `~/.nuget/NuGet/NuGet.Config` (system Mac/Linux) i pozwól NuGet, utwórz go ponownie.</span><span class="sxs-lookup"><span data-stu-id="5c46d-192">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>

<span data-ttu-id="5c46d-193">**Jakie są domyślne licencji warunki Jeśli pakietu nie zawierają informacje o licencji określonego?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-193">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="5c46d-194">Każdy pakiet jest objęte postanowienia, które są dołączone do pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c46d-194">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="5c46d-195">Należy przejrzeć postanowienia mające zastosowanie przed uzyskiwanie dostępu do, pobierania lub uzyskiwania wszystkie pakiety.</span><span class="sxs-lookup"><span data-stu-id="5c46d-195">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="5c46d-196">Na nuget.org, użyj **informacje dotyczące licencji** łącze na stronie pakiet.</span><span class="sxs-lookup"><span data-stu-id="5c46d-196">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="5c46d-197">Jeśli pakiet nie określa postanowień licencyjnych, skontaktuj się z właścicielem pakietu bezpośrednio za pomocą **skontaktuj się z właścicieli** łącze na stronie pakiet nuget.org.</span><span class="sxs-lookup"><span data-stu-id="5c46d-197">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="5c46d-198">Microsoft nie licencji jakiejkolwiek własności intelektualnej użytkownikowi od innych dostawców pakietu i nie jest odpowiedzialny za informacji dostarczonych przez strony trzecie.</span><span class="sxs-lookup"><span data-stu-id="5c46d-198">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="5c46d-199">Zarządzanie pakietami na nuget.org</span><span class="sxs-lookup"><span data-stu-id="5c46d-199">Managing packages on nuget.org</span></span>

<span data-ttu-id="5c46d-200">**Metadane pakietów można edytować po jest przekazane? Dlaczego wymagają edycji plik nuspec i przekazać nowy pakiet do wprowadzania zmian do pakietu metadanych?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-200">**Can I edit package metadata after it's been uploaded? Why do you require editing the nuspec and uploading a new package for making changes to package metadata?**</span></span>

<span data-ttu-id="5c46d-201">NuGet wymaga wszystkich pakietów, były podpisane.</span><span class="sxs-lookup"><span data-stu-id="5c46d-201">NuGet requires all packages to be signed.</span></span> <span data-ttu-id="5c46d-202">Zasada projektowania podpisywania pakietu jest, że zawartość podpisanego pakietu musi być niezmienne, która obejmuje plik nuspec.</span><span class="sxs-lookup"><span data-stu-id="5c46d-202">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="5c46d-203">Edytowanie metadanych pakietu powoduje zmian w plik nuspec, unieważnienie istniejących podpisów.</span><span class="sxs-lookup"><span data-stu-id="5c46d-203">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="5c46d-204">Zaleca się zmodyfikowanie istniejącej przepływy pracy, aby nie wymagają edycji metadanych pakietu po utworzeniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c46d-204">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="5c46d-205">Należy pamiętać, że zależności dla pakietu są generowane automatycznie z pakietu się i nie można edytować.</span><span class="sxs-lookup"><span data-stu-id="5c46d-205">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="5c46d-206">Ponadto przekazywania pakietów do [staging.nuget.org](http://staging.nuget.org) jest doskonałym sposobem testowanie i weryfikowanie pakietu bez udostępniania pakietu w publicznej galerii.</span><span class="sxs-lookup"><span data-stu-id="5c46d-206">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="5c46d-207">**Czy jest możliwe do zarezerwowania nazwy pakietów, które zostaną opublikowane w przyszłości?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-207">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="5c46d-208">Tak.</span><span class="sxs-lookup"><span data-stu-id="5c46d-208">Yes.</span></span> <span data-ttu-id="5c46d-209">Identyfikatory pakietów można zarezerwować na [nuget.org](https://www.nuget.org/) przez zażądanie prefiks Identyfikatora pakietu dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="5c46d-209">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="5c46d-210">Aby poprosić o prefiks Identyfikatora pakietu, postępuj zgodnie z instrukcjami [dokumentacji](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span><span class="sxs-lookup"><span data-stu-id="5c46d-210">In order to request a package ID prefix, follow the instructions in the [documentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="5c46d-211">**Jak potwierdzić prawa własności do pakietów?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-211">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="5c46d-212">Zobacz [Zarządzanie właścicieli pakietu na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="5c46d-212">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="5c46d-213">**Sposób postępowania z właścicielem pakietu, który narusza Moje licencji na oprogramowanie**</span><span class="sxs-lookup"><span data-stu-id="5c46d-213">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="5c46d-214">Firma Microsoft zachęca społeczności NuGet współdziałają ze sobą rozwiązywać wszelkie sporów, które mogą wystąpić podczas między właścicieli pakietu i innego oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="5c46d-214">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="5c46d-215">Firma Microsoft ma co [rozstrzygania procesu rozpoznawania](../policies/dispute-resolution.md) do wykonania przed żądaniem administratorom nuget.org intercede.</span><span class="sxs-lookup"><span data-stu-id="5c46d-215">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="5c46d-216">**Przekaż moje pakietów testowych do nuget.org jest zalecane?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-216">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="5c46d-217">Do celów testowych można użyć [staging.nuget.org](http://staging.nuget.org), lub alternatywne publiczne serwery NuGet, takich jak [myget.org](https://myget.org) lub [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span><span class="sxs-lookup"><span data-stu-id="5c46d-217">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="5c46d-218">Należy pamiętać, że pakiety przekazane do staging.nuget.org mogą nie zostać zachowane.</span><span class="sxs-lookup"><span data-stu-id="5c46d-218">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="5c46d-219">Zobacz [Podgląd praktyczny brak jakichkolwiek](http://blog.nuget.org/20130419/goodbye-preview.html).</span><span class="sxs-lookup"><span data-stu-id="5c46d-219">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="5c46d-220">**Co to jest maksymalny rozmiar pakietów, które można przekazać do nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-220">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="5c46d-221">nuget.org umożliwia pakietów do 250MB, ale firma Microsoft zaleca się utrzymywanie pakietów w obszarze 1MB, jeśli to możliwe, a następnie połącz pakietów przy użyciu zależności.</span><span class="sxs-lookup"><span data-stu-id="5c46d-221">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="5c46d-222">Zasadą zawierać tylko jeden zestaw, aby uniknąć kolizji pakietów.</span><span class="sxs-lookup"><span data-stu-id="5c46d-222">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="5c46d-223">NuGet korzysta z protokołu HTTP do pobierania pakietów, więc pakietów większych niż mniejszych wyższe prawdopodobieństwo instaluje nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="5c46d-223">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="5c46d-224">Istnieje możliwość udostępniania zależności między kilka pakietów, co mniejszy rozmiar całkowitą pobierania dla konsumentów pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c46d-224">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="5c46d-225">Zależności są prawie statyczna i nigdy nie zmiany.</span><span class="sxs-lookup"><span data-stu-id="5c46d-225">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="5c46d-226">Po usunięciu błędu w kodzie, zależności nie muszą zostać zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="5c46d-226">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="5c46d-227">Jeśli pakietu zależności, przechodzili reshipping pakietów większych zawsze.</span><span class="sxs-lookup"><span data-stu-id="5c46d-227">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="5c46d-228">Dzieląc pakietów NuGet w zależności powiązane, uaktualnienia są bardziej szczegółowych dla konsumentów do pakietu.</span><span class="sxs-lookup"><span data-stu-id="5c46d-228">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="5c46d-229">nuget.org niedostępny</span><span class="sxs-lookup"><span data-stu-id="5c46d-229">nuget.org not accessible</span></span>

<span data-ttu-id="5c46d-230">**Dlaczego nie można pobrać pakietów z ani przekazywać pakiety do nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-230">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="5c46d-231">Najpierw upewnij się, że używasz najnowszej wersji programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="5c46d-231">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="5c46d-232">Jeśli w tej wersji zakończy się niepowodzeniem, [się z pomocą techniczną](https://www.nuget.org/policies/Contact) i podaj dodatkowego połączenia Rozwiązywanie problemów z informacje w tym:</span><span class="sxs-lookup"><span data-stu-id="5c46d-232">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="5c46d-233">Wersja programu NuGet używasz</span><span class="sxs-lookup"><span data-stu-id="5c46d-233">The version of NuGet you're using</span></span>
- <span data-ttu-id="5c46d-234">Używanego źródła pakietu</span><span class="sxs-lookup"><span data-stu-id="5c46d-234">The package sources you're using</span></span>
- <span data-ttu-id="5c46d-235">Dziennik przywracania o poziomie szczegółowości szczegółowe</span><span class="sxs-lookup"><span data-stu-id="5c46d-235">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="5c46d-236">MTR lub Fiddler dane śledzenia (zobacz poniżej)</span><span class="sxs-lookup"><span data-stu-id="5c46d-236">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="5c46d-237">Obszar geograficzny</span><span class="sxs-lookup"><span data-stu-id="5c46d-237">Your geographical area</span></span>
- <span data-ttu-id="5c46d-238">Wersji systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="5c46d-238">Your operating system version</span></span>
- <span data-ttu-id="5c46d-239">Konfiguracja maszyny (Procesora i sieci, dysk twardy)</span><span class="sxs-lookup"><span data-stu-id="5c46d-239">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="5c46d-240">Określa, czy jest komputer serwera proxy lub zapory</span><span class="sxs-lookup"><span data-stu-id="5c46d-240">Whether is your machine behind a proxy or firewall</span></span>
- <span data-ttu-id="5c46d-241">Wersje programu .NET, które są zainstalowane na tym komputerze</span><span class="sxs-lookup"><span data-stu-id="5c46d-241">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="5c46d-242">Wersje narzędzi i platform, takich jak .NET interfejsu wiersza polecenia lub DNU, którego używasz</span><span class="sxs-lookup"><span data-stu-id="5c46d-242">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="5c46d-243">*Aby przechwycić MTR:*</span><span class="sxs-lookup"><span data-stu-id="5c46d-243">*To capture MTR:*</span></span>

- <span data-ttu-id="5c46d-244">Pobierz WinMTR z [http://winmtr.net/download/](http://winmtr.net/)</span><span class="sxs-lookup"><span data-stu-id="5c46d-244">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="5c46d-245">Wprowadź `api.nuget.org` jako nazwę hosta i kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="5c46d-245">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="5c46d-246">Poczekaj na **wysłane** kolumny > = 100.</span><span class="sxs-lookup"><span data-stu-id="5c46d-246">Wait until the **Sent** column is >= 100.</span></span>

    ![Przechwytywanie MTR](media/mtr.png)

- <span data-ttu-id="5c46d-248">Skopiować tekst do Schowka.</span><span class="sxs-lookup"><span data-stu-id="5c46d-248">Copy text to clipboard.</span></span>

<span data-ttu-id="5c46d-249">*Aby przechwycić Fiddler:*</span><span class="sxs-lookup"><span data-stu-id="5c46d-249">*To capture Fiddler:*</span></span>

- <span data-ttu-id="5c46d-250">Zainstaluj najnowszą wersję pakietu [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="5c46d-250">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="5c46d-251">Uruchom narzędzie Fiddler i Wyłącz Przechwytywanie ruchu przy użyciu **pliku > przechwytywania ruchu** menu.</span><span class="sxs-lookup"><span data-stu-id="5c46d-251">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="5c46d-252">Usuń wszystkie sesje (Wybierz wszystkie elementy na liście, naciśnij klawisz **usunąć** klucza).</span><span class="sxs-lookup"><span data-stu-id="5c46d-252">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="5c46d-253">Konfigurowanie narzędzia Fiddler do przechwytywania ruchu HTTPS, sprawdzając **ruchu HTTPS odszyfrować** w **HTTPS** karcie **Narzędzia > Opcje Fiddler...**  menu.</span><span class="sxs-lookup"><span data-stu-id="5c46d-253">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="5c46d-254">Zamknij program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c46d-254">Close Visual Studio.</span></span>
- <span data-ttu-id="5c46d-255">Włącz **pliku > przechwytywania ruchu** menu.</span><span class="sxs-lookup"><span data-stu-id="5c46d-255">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="5c46d-256">Uruchom program Visual Studio lub nuget.exe .exe i wykonać akcje, które nie działają.</span><span class="sxs-lookup"><span data-stu-id="5c46d-256">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="5c46d-257">Ruch generowany przez te akcje powinny być widoczne w narzędziu Fiddler.</span><span class="sxs-lookup"><span data-stu-id="5c46d-257">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="5c46d-258">Po akcje zostało uruchomione, użyj **Plik > Zapisz > wszystkie sesje** do przechowywania przechwyconego sesji.</span><span class="sxs-lookup"><span data-stu-id="5c46d-258">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="5c46d-259">Uwaga: może być konieczne można ustawić `HTTP_PROXY` zmienną środowiskową `http://127.0.0.1:8888` dla routingu ruchu NuGet przez Fiddler.</span><span class="sxs-lookup"><span data-stu-id="5c46d-259">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="5c46d-260">W przypadku niepowodzenia spróbuj [porady wymienione w tym wpisie StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span><span class="sxs-lookup"><span data-stu-id="5c46d-260">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="5c46d-261">**Co to są punkty końcowe interfejsu API dla nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="5c46d-261">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="5c46d-262">W wersji 3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (należy pamiętać, że interfejs API w wersji 2 jest przestarzała i nie działa z programem NuGet 4.)</span><span class="sxs-lookup"><span data-stu-id="5c46d-262">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
