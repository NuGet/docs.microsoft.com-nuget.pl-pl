---
title: NuGet — często zadawane pytania
description: Typowe pytania i odpowiedzi dla za pomocą narzędzia NuGet w wierszu polecenia i w programie Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 20a55c6ba89478e70d8e6837aaebc1b7b7754a93
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842436"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="019eb-103">NuGet — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="019eb-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="019eb-104">**Co to jest wymagane do uruchamiania NuGet?**</span><span class="sxs-lookup"><span data-stu-id="019eb-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="019eb-105">Wszystkie informacje dotyczące narzędzia wiersza polecenia i interfejsu użytkownika jest dostępna w [Przewodnik instalacji](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="019eb-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="019eb-106">**NuGet obsługuje platformy Mono?**</span><span class="sxs-lookup"><span data-stu-id="019eb-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="019eb-107">Narzędzie wiersza polecenia `nuget.exe`, kompilacji i uruchamiana Mono 3.2 + i mogą tworzyć pakiety w rozwiązaniu Mono.</span><span class="sxs-lookup"><span data-stu-id="019eb-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="019eb-108">Mimo że `nuget.exe` działa całkowicie w Windows, występują znane problemy w systemie Linux i OS X. zobacz [wystawia Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="019eb-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="019eb-109">A [graficzny klient](https://github.com/mrward/monodevelop-nuget-addin) jest dostępna jako dodatek do programu MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="019eb-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="019eb-110">**Jak sprawdzić, co zawiera pakiet i czy jest stabilna i użyteczna dla mojej aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="019eb-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="019eb-111">Podstawowym źródłem szkoleniowe dotyczące pakietu jest jego strony w witrynie nuget.org (lub innej prywatnej źródła danych).</span><span class="sxs-lookup"><span data-stu-id="019eb-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="019eb-112">Każda strona pakietu w witrynie nuget.org zawiera opis pakietu, jego Historia wersji i statystyki użycia.</span><span class="sxs-lookup"><span data-stu-id="019eb-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="019eb-113">**Informacje** sekcji na stronie pakiet zawiera również link do witryny sieci web projektu, w którym można zwykle znaleźć wiele przykładów i inne dokumenty, aby ułatwić Ci poznanie sposobu używania pakietu.</span><span class="sxs-lookup"><span data-stu-id="019eb-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="019eb-114">Aby uzyskać więcej informacji, zobacz [Znajdowanie i Wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="019eb-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="019eb-115">NuGet w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="019eb-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="019eb-116">**Jak NuGet jest obsługiwane w różnych produktów Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="019eb-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="019eb-117">Program Visual Studio w Windows obsługuje [interfejs użytkownika Menedżera pakietów](../tools/package-manager-ui.md) i [Konsola Menedżera pakietów](../tools/package-manager-console.md).</span><span class="sxs-lookup"><span data-stu-id="019eb-117">Visual Studio on Windows supports the [Package Manager UI](../tools/package-manager-ui.md) and the [Package Manager Console](../tools/package-manager-console.md).</span></span>
- <span data-ttu-id="019eb-118">Program Visual Studio dla komputerów Mac ma wbudowanych funkcji NuGet, zgodnie z opisem na [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="019eb-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="019eb-119">Visual Studio Code (wszystkie platformy) nie ma żadnych bezpośrednią integrację z NuGet.</span><span class="sxs-lookup"><span data-stu-id="019eb-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="019eb-120">Użyj [interfejs wiersza polecenia NuGet](../tools/nuget-exe-cli-reference.md) lub [wiersz polecenia dotnet](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="019eb-120">Use the [NuGet CLI](../tools/nuget-exe-cli-reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="019eb-121">Azure DevOps zapewnia [krok kompilacji, aby przywrócić pakiety NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="019eb-121">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="019eb-122">Możesz również [hosta prywatnego pakietu NuGet kanałów informacyjnych w DevOps platformy Azure](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="019eb-122">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="019eb-123">**Jak sprawdzić wersję narzędzia NuGet, które są zainstalowane?**</span><span class="sxs-lookup"><span data-stu-id="019eb-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="019eb-124">W programie Visual Studio, należy użyć **Pomoc > Microsoft Visual Studio** polecenia i przyjrzyj się wersja wyświetlany obok pozycji **Menedżera pakietów NuGet**.</span><span class="sxs-lookup"><span data-stu-id="019eb-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="019eb-125">Alternatywnie Uruchom konsolę Menedżera pakietów (**Narzędzia > Menedżer pakietów NuGet > Konsola Menedżera pakietów**) i wprowadź `$host` Aby wyświetlić informacje o tym w wersji NuGet.</span><span class="sxs-lookup"><span data-stu-id="019eb-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="019eb-126">**Jakich języków programowania są obsługiwane przez NuGet?**</span><span class="sxs-lookup"><span data-stu-id="019eb-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="019eb-127">NuGet zwykle działa w przypadku języków .NET i jest przeznaczona do bibliotek .NET do projektu.</span><span class="sxs-lookup"><span data-stu-id="019eb-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="019eb-128">Ponieważ w niektórych typach projektów są również obsługuje automatyzacji programu MSBuild i Visual Studio, obsługuje ona również innych projektów i języki różnym stopniu.</span><span class="sxs-lookup"><span data-stu-id="019eb-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="019eb-129">Obsługuje najnowszej wersji pakietu NuGet C#, Visual Basic F#, WiX i C++.</span><span class="sxs-lookup"><span data-stu-id="019eb-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="019eb-130">**Szablony projektów, które są obsługiwane przez NuGet?**</span><span class="sxs-lookup"><span data-stu-id="019eb-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="019eb-131">NuGet ma pełną pomoc techniczną dla różnych szablonów projektu, takich jak Windows, sieci Web, chmury, SharePoint, Wix i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="019eb-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="019eb-132">**Jak zaktualizować pakiety, które są częścią szablony programu Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="019eb-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="019eb-133">Przejdź do **aktualizacje** w Interfejsie użytkownika Menedżera pakietów, a wybierz pozycję **Aktualizuj wszystkie**, lub użyj [ `Update-Package` polecenia](../tools/ps-ref-update-package.md) z konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="019eb-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="019eb-134">Aby zaktualizować samego szablonu, musisz ręcznie zaktualizować repozytorium szablonów.</span><span class="sxs-lookup"><span data-stu-id="019eb-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="019eb-135">Zobacz [blog Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) na ten temat.</span><span class="sxs-lookup"><span data-stu-id="019eb-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="019eb-136">Należy to zrobić na własne ryzyko, należy pamiętać, ponieważ ręczne aktualizacje może spowodować uszkodzenie szablonu, jeśli najnowszą wersję wszystkich zależności nie są ze sobą zgodne.</span><span class="sxs-lookup"><span data-stu-id="019eb-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="019eb-137">**Można użyć NuGet poza programem Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="019eb-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="019eb-138">Tak, NuGet współpracuje bezpośrednio z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="019eb-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="019eb-139">Zobacz [Przewodnik instalacji](../install-nuget-client-tools.md) i [dokumentacja interfejsu wiersza polecenia](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="019eb-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="019eb-140">Wiersz polecenia NuGet</span><span class="sxs-lookup"><span data-stu-id="019eb-140">NuGet command line</span></span>

<span data-ttu-id="019eb-141">**Jak uzyskać najnowszą wersję narzędzia wiersza polecenia NuGet?**</span><span class="sxs-lookup"><span data-stu-id="019eb-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="019eb-142">Zobacz [Przewodnik instalacji](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="019eb-142">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="019eb-143">**Co to jest licencja na nuget.exe?**</span><span class="sxs-lookup"><span data-stu-id="019eb-143">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="019eb-144">Możesz wykonać ponowną dystrybucję nuget.exe zgodnie z warunkami licencji MIT.</span><span class="sxs-lookup"><span data-stu-id="019eb-144">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="019eb-145">Odpowiedzialność za aktualizacji i obsługi wszystkich kopii nuget.exe, który chcesz ponownie rozesłać.</span><span class="sxs-lookup"><span data-stu-id="019eb-145">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="019eb-146">**Czy jest możliwe rozszerzenie narzędzia wiersza polecenia NuGet?**</span><span class="sxs-lookup"><span data-stu-id="019eb-146">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="019eb-147">Tak, istnieje możliwość dodawania niestandardowych poleceń do `nuget.exe`, zgodnie z opisem w [wpis Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="019eb-147">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="019eb-148">Konsola Menedżera pakietów NuGet (Visual Studio Windows)</span><span class="sxs-lookup"><span data-stu-id="019eb-148">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="019eb-149">**Jak uzyskać dostęp do obiektu DTE w konsoli Menedżera pakietów?**</span><span class="sxs-lookup"><span data-stu-id="019eb-149">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="019eb-150">Obiekt najwyższego poziomu w modelu obiektu automatyzacji programu Visual Studio nosi nazwę obiektu DTE (środowisko programistyczne narzędzia).</span><span class="sxs-lookup"><span data-stu-id="019eb-150">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="019eb-151">Konsolę te elementy są dostępne za pośrednictwem zmiennej o nazwie `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="019eb-151">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="019eb-152">Aby uzyskać więcej informacji, zobacz [omówienie modelu automatyzacji](/visualstudio/extensibility/internals/automation-model-overview) w dokumentacji rozszerzeń programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="019eb-152">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="019eb-153">**Próbie rzutowania $DTE zmienną typu DTE2, ale pojawia się błąd: Nie można przekonwertować wartości "EnvDTE.DTEClass" typu "EnvDTE.DTEClass" na typ "EnvDTE80.DTE2". Co jest nie tak?**</span><span class="sxs-lookup"><span data-stu-id="019eb-153">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="019eb-154">Jest to znany problem dotyczący współdziałania programu PowerShell za pomocą obiektu COM.</span><span class="sxs-lookup"><span data-stu-id="019eb-154">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="019eb-155">Spróbuj wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="019eb-155">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="019eb-156">`Get-Interface` czy funkcji pomocnika, która jest dodawany przez hosta NuGet w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="019eb-156">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="019eb-157">Tworzenie i publikowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="019eb-157">Creating and publishing packages</span></span>

<span data-ttu-id="019eb-158">**Jak wyświetlić listę Mój pakiet w źródle danych?**</span><span class="sxs-lookup"><span data-stu-id="019eb-158">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="019eb-159">Zobacz [tworzenie i publikowanie pakietu](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="019eb-159">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="019eb-160">**Mam wiele wersji biblioteki, przeznaczonych dla różnych wersji programu .NET Framework. Jak utworzyć jeden pakiet, który obsługuje tę funkcję?**</span><span class="sxs-lookup"><span data-stu-id="019eb-160">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="019eb-161">Zobacz [obsługujące wiele wersje programu .NET Framework i profile](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="019eb-161">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="019eb-162">**Jak skonfigurować własnego repozytorium lub źródło danych?**</span><span class="sxs-lookup"><span data-stu-id="019eb-162">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="019eb-163">Zobacz [hostingu — Omówienie pakietów](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="019eb-163">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="019eb-164">**Jak przesłać pakiety do mojego NuGet źródła danych w trybie zbiorczym**</span><span class="sxs-lookup"><span data-stu-id="019eb-164">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="019eb-165">Zobacz [zbiorczo publikowania pakietów NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="019eb-165">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="019eb-166">Praca z pakietami</span><span class="sxs-lookup"><span data-stu-id="019eb-166">Working with packages</span></span>

<span data-ttu-id="019eb-167">**Jaka jest różnica między pakietem na poziomie projektu i pakietu poziomie rozwiązania?**</span><span class="sxs-lookup"><span data-stu-id="019eb-167">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="019eb-168">Pakiet poziomie rozwiązania (NuGet 3.x+) zostanie zainstalowana tylko raz w rozwiązaniu i jest dostępna dla wszystkich projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="019eb-168">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="019eb-169">Pakiet na poziomie projektu jest zainstalowany w każdym projekcie, który korzysta z niego.</span><span class="sxs-lookup"><span data-stu-id="019eb-169">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="019eb-170">Pakiet poziomie rozwiązania może również zainstalować nowe polecenia, które mogą być wywoływane z poziomu konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="019eb-170">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="019eb-171">**Czy istnieje możliwość zainstalowania pakietów NuGet bez łączności z Internetem?**</span><span class="sxs-lookup"><span data-stu-id="019eb-171">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="019eb-172">Tak, zobacz wpis w blogu Scotta Hanselmana [jak uzyskać dostęp do NuGet, kiedy nuget.org znajduje się w dół (lub jesteś na płaszczyźnie)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="019eb-172">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="019eb-173">**Jak zainstalować pakiety w innym miejscu niż domyślny folder pakietów?**</span><span class="sxs-lookup"><span data-stu-id="019eb-173">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="019eb-174">Ustaw [ `repositoryPath` ](../reference/nuget-config-file.md#config-section) w `Nuget.Config` przy użyciu `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="019eb-174">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="019eb-175">**Jak uniknąć Dodawanie folderu pakiety NuGet do kontroli źródła**</span><span class="sxs-lookup"><span data-stu-id="019eb-175">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="019eb-176">Ustaw [ `disableSourceControlIntegration` ](../reference/nuget-config-file.md#solution-section) w `Nuget.Config` do `true`.</span><span class="sxs-lookup"><span data-stu-id="019eb-176">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="019eb-177">Ta działa klucza w rozwiązaniu poziomie i w związku z tym konieczne będzie dodanie do `$(Solutiondir)\.nuget\Nuget.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="019eb-177">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="019eb-178">Włączanie przywracania pakietów w programie Visual Studio automatycznie tworzy ten plik.</span><span class="sxs-lookup"><span data-stu-id="019eb-178">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="019eb-179">**Jak wyłączyć Przywracanie pakietu**</span><span class="sxs-lookup"><span data-stu-id="019eb-179">**How do I turn off package restore?**</span></span>

<span data-ttu-id="019eb-180">Zobacz [Włączanie i wyłączanie Przywracanie pakietu](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="019eb-180">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).</span></span>

<span data-ttu-id="019eb-181">**Dlaczego otrzymuję "Nie można rozwiązać błąd zależności" podczas instalowania pakietu lokalnego przy użyciu zależności zdalnych?**</span><span class="sxs-lookup"><span data-stu-id="019eb-181">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="019eb-182">Musisz wybrać **wszystkie** źródła podczas instalowania pakietu lokalnego do projektu.</span><span class="sxs-lookup"><span data-stu-id="019eb-182">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="019eb-183">To agreguje wszystkie źródła danych zamiast przy użyciu tylko jednego.</span><span class="sxs-lookup"><span data-stu-id="019eb-183">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="019eb-184">Przyczyna tego błędu pojawia się jest, czy użytkownicy lokalnego repozytorium często chcą uniknąć przypadkowego instalowania zdalnego pakietu ze względu na firmowe zasady.</span><span class="sxs-lookup"><span data-stu-id="019eb-184">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="019eb-185">**Mam wiele projektów w tym samym folderze, jak korzystać z pliku packages.config oddzielnych plików dla każdego projektu?**</span><span class="sxs-lookup"><span data-stu-id="019eb-185">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="019eb-186">W większości projektów, w którym oddzielnych projektów znajdować się w oddzielnych folderów, nie jest to problem jak NuGet identyfikuje `packages.config` plików w każdym projekcie.</span><span class="sxs-lookup"><span data-stu-id="019eb-186">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="019eb-187">Nuget 3.3 + i jest wiele projektów w tym samym folderze, można wstawiać Nazwa projektu do `packages.config` nazw plików, użyj wzorca `packages.{project-name}.config`, i NuGet korzysta z tego pliku.</span><span class="sxs-lookup"><span data-stu-id="019eb-187">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="019eb-188">To nie jest wystąpił problem podczas korzystania z funkcji PackageReference, ponieważ każdy plik projektu zawiera swój własny listę zależności.</span><span class="sxs-lookup"><span data-stu-id="019eb-188">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="019eb-189">**Nuget.org nie jest widoczny w listy moich repozytoriów, jak uzyskać go ponownie?**</span><span class="sxs-lookup"><span data-stu-id="019eb-189">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="019eb-190">Dodaj `https://api.nuget.org/v3/index.json` do listy źródeł, lub</span><span class="sxs-lookup"><span data-stu-id="019eb-190">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="019eb-191">Usuń `%appdata%\.nuget\NuGet.Config` (Windows) lub `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) i pozwolić NuGet, utwórz go ponownie.</span><span class="sxs-lookup"><span data-stu-id="019eb-191">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>
