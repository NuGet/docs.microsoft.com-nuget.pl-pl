---
title: Często zadawane pytania dotyczące narzędzia NuGet
description: Często zadawane pytania i odpowiedzi dotyczące korzystania z narzędzia NuGet w wierszu polecenia i w programie Visual Studio
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 8cc990e0c9eed07c59c8dffb04d104be47051736
ms.sourcegitcommit: 7c9f157ba02d9be543de34ab06813ab1ec10192a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999940"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="07fb2-103">Często zadawane pytania dotyczące narzędzia NuGet</span><span class="sxs-lookup"><span data-stu-id="07fb2-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="07fb2-104">Często zadawane pytania dotyczące usługi NuGet.org, takie jak NuGet.org accounts, zobacz [często zadawane pytania](../nuget-org/nuget-org-faq.md).</span><span class="sxs-lookup"><span data-stu-id="07fb2-104">For frequently-asked questions pertaining to NuGet.org, such as NuGet.org account questions, see [NuGet.org frequently-asked questions](../nuget-org/nuget-org-faq.md).</span></span>

<span data-ttu-id="07fb2-105">**Co jest wymagane do uruchomienia narzędzia NuGet?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-105">**What is required to run NuGet?**</span></span>

<span data-ttu-id="07fb2-106">Wszystkie informacje o interfejsie użytkownika i narzędziach wiersza polecenia są dostępne w [przewodniku instalacji](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="07fb2-106">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="07fb2-107">**Czy pakiet NuGet obsługuje mono?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-107">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="07fb2-108">Narzędzie `nuget.exe`wiersza polecenia, kompiluje i uruchamia się w programie mono 3.2 + i może tworzyć pakiety w mono.</span><span class="sxs-lookup"><span data-stu-id="07fb2-108">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="07fb2-109">Chociaż `nuget.exe` działa w pełni w systemie Windows, istnieją znane problemy w systemach Linux i OS X. Zobacz problemy z programem [mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) w serwisie GitHub.</span><span class="sxs-lookup"><span data-stu-id="07fb2-109">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="07fb2-110">[Klient graficzny](https://github.com/mrward/monodevelop-nuget-addin) jest dostępny jako dodatek dla narzędzia MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="07fb2-110">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="07fb2-111">**Jak określić, co pakiet zawiera i czy jest stabilny i przydatny dla mojej aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-111">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="07fb2-112">Podstawowym źródłem informacji o pakiecie jest jego strona aukcji w witrynie nuget.org (lub innego prywatnego źródła).</span><span class="sxs-lookup"><span data-stu-id="07fb2-112">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="07fb2-113">Każda Strona pakietu w witrynie nuget.org zawiera opis pakietu, jego historię wersji oraz dane statystyczne użycia.</span><span class="sxs-lookup"><span data-stu-id="07fb2-113">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="07fb2-114">Sekcja **informacje** na stronie pakiet zawiera również link do witryny sieci Web projektu, gdzie zazwyczaj znajdziesz wiele przykładów i innych dokumentów, które ułatwiają zapoznanie się z używanym pakietem.</span><span class="sxs-lookup"><span data-stu-id="07fb2-114">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="07fb2-115">Aby uzyskać więcej informacji, zobacz [Znajdowanie i wybieranie pakietów](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="07fb2-115">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="07fb2-116">Pakiet NuGet w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="07fb2-116">NuGet in Visual Studio</span></span>

<span data-ttu-id="07fb2-117">**Jak program NuGet jest obsługiwany w różnych produktach Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-117">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="07fb2-118">Program Visual Studio w systemie Windows obsługuje [interfejs użytkownika Menedżera pakietów](../consume-packages/install-use-packages-visual-studio.md) i [konsolę Menedżera pakietów](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="07fb2-118">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="07fb2-119">Visual Studio dla komputerów Mac ma wbudowane funkcje NuGet, zgodnie z opisem w temacie [zawierającym pakiet NuGet w projekcie](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="07fb2-119">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="07fb2-120">Visual Studio Code (wszystkie platformy) nie ma żadnej bezpośredniej integracji z pakietem NuGet.</span><span class="sxs-lookup"><span data-stu-id="07fb2-120">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="07fb2-121">Użyj [interfejsu wiersza polecenia NuGet](../reference/nuget-exe-cli-reference.md) lub [interfejsu wiersza polecenia dotnet](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="07fb2-121">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="07fb2-122">Usługa Azure DevOps udostępnia [krok kompilacji służący do przywracania pakietów NuGet](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="07fb2-122">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="07fb2-123">Możesz również [hostować prywatne źródła pakietów NuGet na platformie Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="07fb2-123">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="07fb2-124">**Jak mogę sprawdzić dokładną wersję zainstalowanych narzędzi NuGet?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-124">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="07fb2-125">W programie Visual Studio Użyj **> pomocy dotyczącej Microsoft Visual Studio** polecenia i sprawdź wersję wyświetlaną obok pozycji **Menedżer pakietów NuGet**.</span><span class="sxs-lookup"><span data-stu-id="07fb2-125">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="07fb2-126">Alternatywnie można uruchomić konsolę Menedżera pakietów (**Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów**) i wprowadzić `$host` polecenie, aby wyświetlić informacje o pakiecie NuGet, w tym wersję.</span><span class="sxs-lookup"><span data-stu-id="07fb2-126">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="07fb2-127">**Jakie języki programowania są obsługiwane przez pakiet NuGet?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-127">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="07fb2-128">Pakiet NuGet zazwyczaj działa w przypadku języków .NET i jest przeznaczony do przenoszenia bibliotek .NET do projektu.</span><span class="sxs-lookup"><span data-stu-id="07fb2-128">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="07fb2-129">Ponieważ obsługuje ona również narzędzia MSBuild i automatyzację programu Visual Studio w niektórych typach projektów, obsługuje również inne projekty i Języki w różnych stopniach.</span><span class="sxs-lookup"><span data-stu-id="07fb2-129">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="07fb2-130">Najnowsza wersja NuGet obsługuje C#, Visual Basic, F#, WIX i. C++</span><span class="sxs-lookup"><span data-stu-id="07fb2-130">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="07fb2-131">**Jakie szablony projektów są obsługiwane przez pakiet NuGet?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-131">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="07fb2-132">Pakiet NuGet ma pełną obsługę wielu szablonów projektów, takich jak Windows, Web, Cloud, SharePoint, WIX i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="07fb2-132">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="07fb2-133">**Jak mogę pakiety aktualizacji, które są częścią szablonów programu Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-133">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="07fb2-134">Przejdź do karty **aktualizacje** w interfejsie użytkownika Menedżera pakietów i wybierz pozycję **Aktualizuj wszystko** [ `Update-Package` ](../reference/ps-reference/ps-ref-update-package.md) lub użyj polecenia z konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="07fb2-134">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="07fb2-135">Aby zaktualizować sam szablon, musisz ręcznie zaktualizować repozytorium szablonów.</span><span class="sxs-lookup"><span data-stu-id="07fb2-135">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="07fb2-136">Zapoznaj się z blogiem dotyczącym [Xavier](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) .</span><span class="sxs-lookup"><span data-stu-id="07fb2-136">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="07fb2-137">Należy pamiętać, że jest to wykonywane na własne ryzyko, ponieważ ręczne aktualizacje mogą uszkodzić szablon, jeśli Najnowsza wersja wszystkich zależności nie jest zgodna ze sobą.</span><span class="sxs-lookup"><span data-stu-id="07fb2-137">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="07fb2-138">**Czy mogę używać narzędzia NuGet poza programem Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-138">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="07fb2-139">Tak, pakiet NuGet działa bezpośrednio z wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="07fb2-139">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="07fb2-140">Zobacz [Przewodnik instalacji](../install-nuget-client-tools.md) i [Dokumentacja interfejsu wiersza polecenia](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="07fb2-140">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="07fb2-141">Wiersz polecenia NuGet</span><span class="sxs-lookup"><span data-stu-id="07fb2-141">NuGet command line</span></span>

<span data-ttu-id="07fb2-142">**Jak mogę pobrać najnowszej wersji narzędzia wiersza polecenia NuGet?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-142">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="07fb2-143">Zobacz [Przewodnik instalacji](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="07fb2-143">See the [Install guide](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="07fb2-144">Aby sprawdzić bieżącą zainstalowaną wersję narzędzia, użyj `nuget help`programu.</span><span class="sxs-lookup"><span data-stu-id="07fb2-144">To check the current installed version of the tool, use `nuget help`.</span></span>

<span data-ttu-id="07fb2-145">**Jaka jest licencja dla programu NuGet. exe?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-145">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="07fb2-146">Można ponownie rozesłać plik NuGet. exe zgodnie z warunkami licencji MIT.</span><span class="sxs-lookup"><span data-stu-id="07fb2-146">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="07fb2-147">Użytkownik jest odpowiedzialny za aktualizowanie i obsługę wszelkich kopii programu NuGet. exe, które należy wykonać w celu ponownej dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="07fb2-147">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="07fb2-148">**Czy jest możliwe rozszerzenie narzędzia wiersza polecenia NuGet?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-148">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="07fb2-149">Tak, możliwe jest dodanie poleceń niestandardowych do `nuget.exe`, zgodnie z opisem w wpisie [Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="07fb2-149">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="07fb2-150">Konsola Menedżera pakietów NuGet (Visual Studio w systemie Windows)</span><span class="sxs-lookup"><span data-stu-id="07fb2-150">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="07fb2-151">**Jak mogę uzyskać dostęp do obiektu DTE w konsoli Menedżera pakietów?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-151">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="07fb2-152">Obiekt najwyższego poziomu w modelu obiektów automatyzacji programu Visual Studio jest nazywany obiektem DTE (środowisko narzędzi programistycznych).</span><span class="sxs-lookup"><span data-stu-id="07fb2-152">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="07fb2-153">Konsola zapewnia tę wartość za pomocą zmiennej o `$DTE`nazwie.</span><span class="sxs-lookup"><span data-stu-id="07fb2-153">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="07fb2-154">Aby uzyskać więcej informacji, zobacz [Omówienie modelu automatyzacji](/visualstudio/extensibility/internals/automation-model-overview) w dokumentacji rozszerzalności programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07fb2-154">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="07fb2-155">**Próbujemy rzutować zmienną $DTE na typ DTE2, ale otrzymuję błąd: Nie można przekonwertować wartości "EnvDTE. DTEClass" typu "EnvDTE. DTEClass" na typ "EnvDTE80. DTE2". Co jest nie tak?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-155">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="07fb2-156">Jest to znany problem związany z współdziałaniem programu PowerShell z obiektem COM.</span><span class="sxs-lookup"><span data-stu-id="07fb2-156">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="07fb2-157">Spróbuj wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="07fb2-157">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="07fb2-158">`Get-Interface`jest funkcją pomocnika dodaną przez hosta NuGet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="07fb2-158">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="07fb2-159">Tworzenie i publikowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="07fb2-159">Creating and publishing packages</span></span>

<span data-ttu-id="07fb2-160">**Jak mogę wyświetlić mój pakiet w kanale informacyjnym?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-160">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="07fb2-161">Zobacz [Tworzenie i publikowanie pakietu](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="07fb2-161">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="07fb2-162">**Mam wiele wersji mojej biblioteki, które są przeznaczone dla różnych wersji .NET Framework. Jak mogę utworzyć pojedynczy pakiet, który go obsługuje?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-162">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="07fb2-163">Zobacz [Obsługa wielu .NET Framework wersji i profilów](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="07fb2-163">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="07fb2-164">**Jak mogę skonfigurować własne repozytorium lub źródło danych?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-164">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="07fb2-165">Zobacz [Omówienie pakietów hostingu](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="07fb2-165">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="07fb2-166">**Jak mogę przekazać pakiety do mojego źródła danych NuGet zbiorczo?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-166">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="07fb2-167">Zobacz [zbiorcze publikowanie pakietów NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="07fb2-167">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="07fb2-168">Praca z pakietami</span><span class="sxs-lookup"><span data-stu-id="07fb2-168">Working with packages</span></span>

<span data-ttu-id="07fb2-169">**Jaka jest różnica między pakietem na poziomie projektu a pakietem na poziomie rozwiązania?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-169">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="07fb2-170">Pakiet na poziomie rozwiązania (NuGet 3. x +) jest instalowany tylko raz w rozwiązaniu, a następnie jest dostępny dla wszystkich projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="07fb2-170">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="07fb2-171">Pakiet na poziomie projektu jest instalowany w każdym projekcie, który go używa.</span><span class="sxs-lookup"><span data-stu-id="07fb2-171">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="07fb2-172">Pakiet na poziomie rozwiązania może również instalować nowe polecenia, które można wywołać z poziomu konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="07fb2-172">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="07fb2-173">**Czy jest możliwe zainstalowanie pakietów NuGet bez połączenia z Internetem?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-173">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="07fb2-174">Tak, zobacz wpis w blogu Scott Hanselman, [jak uzyskać dostęp do narzędzia NuGet, gdy NuGet.org nie działa (lub na płaszczyźnie)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (Hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="07fb2-174">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="07fb2-175">**Jak mogę zainstalować pakiety w innej lokalizacji z folderu pakietów domyślnych?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-175">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="07fb2-176">[`repositoryPath`](../reference/nuget-config-file.md#config-section) Ustaw ustawienie`Nuget.Config` przy użyciu `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="07fb2-176">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="07fb2-177">**Jak mogę unikać dodawania folderu pakietów NuGet do kontroli źródła?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-177">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="07fb2-178">Ustaw wartość [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) `Nuget.Config` wna.`true`</span><span class="sxs-lookup"><span data-stu-id="07fb2-178">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="07fb2-179">Ten klucz działa na poziomie rozwiązania i dlatego należy go dodać do `$(Solutiondir)\.nuget\Nuget.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="07fb2-179">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="07fb2-180">Włączenie przywracania pakietów w programie Visual Studio powoduje automatyczne utworzenie tego pliku.</span><span class="sxs-lookup"><span data-stu-id="07fb2-180">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="07fb2-181">**Jak mogę wyłączyć Przywracanie pakietu?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-181">**How do I turn off package restore?**</span></span>

<span data-ttu-id="07fb2-182">Zobacz [Włączanie i wyłączanie przywracania pakietów](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="07fb2-182">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span></span>

<span data-ttu-id="07fb2-183">**Dlaczego otrzymuję "nie można rozpoznać błędu zależności" podczas instalowania pakietu lokalnego z zależnościami zdalnymi?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-183">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="07fb2-184">W przypadku instalowania pakietu lokalnego w projekcie należy wybrać **wszystkie** źródła.</span><span class="sxs-lookup"><span data-stu-id="07fb2-184">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="07fb2-185">Agreguje wszystkie źródła danych zamiast używać tylko jednego.</span><span class="sxs-lookup"><span data-stu-id="07fb2-185">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="07fb2-186">Przyczyną tego błędu jest to, że użytkownicy lokalnego repozytorium często chcą uniknąć przypadkowego zainstalowania pakietu zdalnego ze względu na zasady korporacyjne.</span><span class="sxs-lookup"><span data-stu-id="07fb2-186">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="07fb2-187">**Mam wiele projektów w tym samym folderze, w jaki sposób mogę używać oddzielnych plików Packages. config dla każdego projektu?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-187">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="07fb2-188">W większości projektów, w których oddzielne projekty znajdują się w oddzielnych folderach, nie jest to problem, `packages.config` ponieważ program NuGet identyfikuje pliki w każdym projekcie.</span><span class="sxs-lookup"><span data-stu-id="07fb2-188">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="07fb2-189">W przypadku programu NuGet 3.3 + i wielu projektów w tym samym folderze można wstawić nazwę projektu do `packages.config` nazwy pliku, użyj wzorca `packages.{project-name}.config`, a NuGet używa tego pliku.</span><span class="sxs-lookup"><span data-stu-id="07fb2-189">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="07fb2-190">Nie jest to problem występujący podczas korzystania z programu PackageReference, ponieważ każdy plik projektu zawiera własną listę zależności.</span><span class="sxs-lookup"><span data-stu-id="07fb2-190">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="07fb2-191">**Nie widzę nuget.org na liście repozytoriów, jak to zrobić?**</span><span class="sxs-lookup"><span data-stu-id="07fb2-191">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="07fb2-192">Dodaj `https://api.nuget.org/v3/index.json` do listy źródeł lub</span><span class="sxs-lookup"><span data-stu-id="07fb2-192">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="07fb2-193">Usuń `%appdata%\.nuget\NuGet.Config` system (Windows) `~/.nuget/NuGet/NuGet.Config` lub (Mac/Linux) i pozwól, aby pakiet NuGet został utworzony ponownie.</span><span class="sxs-lookup"><span data-stu-id="07fb2-193">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>
