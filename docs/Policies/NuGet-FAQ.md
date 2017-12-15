---
title: "NuGet często zadawane pytania | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 199a915d-9595-4ae2-a1fb-b15da6d7735a
description: "Typowe pytania i odpowiedzi przy użyciu narzędzia NuGet w wierszu polecenia, a w programie Visual Studio i pracy z galerii NuGet."
keywords: "Wersje pakietu NuGet pytań i odpowiedzi, pytania i odpowiedzi, typowe problemy, wersje NuGet"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 105fa6e1cad3d163b673376c74ce9c835a0b5059
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="62884-104">NuGet często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="62884-104">NuGet frequently-asked questions</span></span>

<span data-ttu-id="62884-105">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="62884-105">In this topic:</span></span>

- [<span data-ttu-id="62884-106">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="62884-106">Getting started</span></span>](#getting-started)
- [<span data-ttu-id="62884-107">NuGet w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="62884-107">NuGet in Visual Studio</span></span>](#nuget-in-visual-studio)
- [<span data-ttu-id="62884-108">Wiersz polecenia NuGet</span><span class="sxs-lookup"><span data-stu-id="62884-108">NuGet command line</span></span>](#nuget-command-line)
- [<span data-ttu-id="62884-109">Konsola Menedżera pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="62884-109">NuGet Package Manager Console</span></span>](#nuget-package-manager-console)
- [<span data-ttu-id="62884-110">Tworzenie i publikowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="62884-110">Creating and publishing packages</span></span>](#creating-and-publishing-packages)
- [<span data-ttu-id="62884-111">Praca z pakietami</span><span class="sxs-lookup"><span data-stu-id="62884-111">Working with packages</span></span>](#working-with-packages)
- [<span data-ttu-id="62884-112">Zarządzanie pakietami na nuget.org</span><span class="sxs-lookup"><span data-stu-id="62884-112">Managing packages on nuget.org</span></span>](#managing-packages-on-nugetorg)
- [<span data-ttu-id="62884-113">nuget.org niedostępny</span><span class="sxs-lookup"><span data-stu-id="62884-113">nuget.org not accessible</span></span>](#nugetorg-not-accessible)

## <a name="getting-started"></a><span data-ttu-id="62884-114">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="62884-114">Getting started</span></span>

<span data-ttu-id="62884-115">**Co to jest wymagany do uruchamiania NuGet?**</span><span class="sxs-lookup"><span data-stu-id="62884-115">**What is required to run NuGet?**</span></span>

<span data-ttu-id="62884-116">Wszystkie informacje dotyczące narzędzia wiersza polecenia i interfejsu użytkownika są dostępne w [Przewodnik instalacji](../guides/install-nuget.md).</span><span class="sxs-lookup"><span data-stu-id="62884-116">All the information around both UI and command-line tools is available in the [Install guide](../guides/install-nuget.md).</span></span>

<span data-ttu-id="62884-117">**NuGet obsługuje Mono?**</span><span class="sxs-lookup"><span data-stu-id="62884-117">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="62884-118">Narzędzie wiersza polecenia `nuget.exe`, tworzy i uruchamiana Mono 3.2 + oraz pakiety można tworzyć w Mono.</span><span class="sxs-lookup"><span data-stu-id="62884-118">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="62884-119">Mimo że `nuget.exe` działa w pełni w systemie Windows, istnieją znane problemy w systemie Linux i OS X. znajduje się w [wystawia Mono](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="62884-119">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="62884-120">A [graficznego klienta](https://github.com/mrward/monodevelop-nuget-addin) jest dostępna jako dodatek do MonoDevelop.</span><span class="sxs-lookup"><span data-stu-id="62884-120">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="62884-121">**Jak można określić pakiet zawiera i czy jest ona stabilna i przydatne w przypadku mojej aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="62884-121">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="62884-122">Podstawowym źródłem szkoleniowe dotyczące pakietu jest stroną listy na nuget.org (lub innej prywatnej źródła danych).</span><span class="sxs-lookup"><span data-stu-id="62884-122">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="62884-123">Każda strona pakietu na nuget.org zawiera opis pakietu, jego Historia wersji i statystyki użycia.</span><span class="sxs-lookup"><span data-stu-id="62884-123">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="62884-124">**Informacji** sekcja na stronie pakiet zawiera również link do witryny sieci web projektu, w którym zwykle znaleźć wiele przykłady i inne dokumentacji, aby uzyskać więcej informacji, sposobu używania pakietu.</span><span class="sxs-lookup"><span data-stu-id="62884-124">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="62884-125">Aby uzyskać więcej informacji, zobacz [wyszukiwanie i Wybieranie pakietów](../Consume-Packages/Finding-and-Choosing-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="62884-125">For more information, see [Finding and choosing packages](../Consume-Packages/Finding-and-Choosing-Packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="62884-126">NuGet w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="62884-126">NuGet in Visual Studio</span></span>

<span data-ttu-id="62884-127">**Jak NuGet jest obsługiwane w różnych produktów Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="62884-127">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="62884-128">Program Visual Studio w systemie Windows obsługuje [interfejsu użytkownika Menedżera pakietów](../tools/Package-Manager-UI.md) i [Konsola Menedżera pakietów](../tools/Package-Manager-Console.md).</span><span class="sxs-lookup"><span data-stu-id="62884-128">Visual Studio on Windows supports the [Package Manager UI](../tools/Package-Manager-UI.md) and the [Package Manager Console](../tools/Package-Manager-Console.md).</span></span>
- <span data-ttu-id="62884-129">Visual Studio for Mac ma wbudowane funkcje NuGet, zgodnie z opisem na [pakietu w tym NuGet w projekcie](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="62884-129">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="62884-130">Visual Studio Code (wszystkie platformy) nie ma żadnych bezpośrednich integracji z programem NuGet.</span><span class="sxs-lookup"><span data-stu-id="62884-130">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="62884-131">Użyj [interfejsu wiersza polecenia NuGet](../tools/nuget-exe-CLI-Reference.md) lub [dotnet interfejsu wiersza polecenia](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="62884-131">Use the [NuGet CLI](../tools/nuget-exe-CLI-Reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="62884-132">Visual Studio Team Services zapewnia [kroku kompilacji pod kątem przywracania pakietów NuGet](https://docs.microsoft.com/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="62884-132">Visual Studio Team Services provides [a build step to restore NuGet packages](https://docs.microsoft.com/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="62884-133">Możesz również [pakietu NuGet prywatnych hosta źródła na Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="62884-133">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="62884-134">**Jak sprawdzić dokładnej wersji narzędzia NuGet, które są zainstalowane**</span><span class="sxs-lookup"><span data-stu-id="62884-134">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="62884-135">W programie Visual Studio, użyj **Pomoc > Microsoft Visual Studio** polecenia i przyjrzyj się wersja wyświetlana obok **Menedżera pakietów NuGet**.</span><span class="sxs-lookup"><span data-stu-id="62884-135">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="62884-136">Można również uruchomić konsoli Menedżera pakietów (**Narzędzia > Menedżera pakietów NuGet > konsoli Menedżera pakietów**), a następnie wprowadź `$host` Aby wyświetlić informacje o tym wersję NuGet.</span><span class="sxs-lookup"><span data-stu-id="62884-136">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="62884-137">**Jakich języków programowania są obsługiwane przez narzędzie NuGet?**</span><span class="sxs-lookup"><span data-stu-id="62884-137">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="62884-138">NuGet zwykle działa w przypadku języków .NET i jest przeznaczony do bibliotek .NET do projektu.</span><span class="sxs-lookup"><span data-stu-id="62884-138">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="62884-139">Ponieważ obsługuje ona również automatyzacji MSBuild i Visual Studio w niektórych typów projektów, obsługuje ona również inne projekty i języki do różnych stopni.</span><span class="sxs-lookup"><span data-stu-id="62884-139">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="62884-140">Najnowszą wersję programu NuGet obsługuje C#, Visual Basic, F #, WiX i C++.</span><span class="sxs-lookup"><span data-stu-id="62884-140">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="62884-141">**Szablony projektów, które są obsługiwane przez narzędzie NuGet?**</span><span class="sxs-lookup"><span data-stu-id="62884-141">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="62884-142">NuGet zawiera pełną obsługę różnych szablonów projektu, takie jak Windows, sieci Web, chmur, SharePoint, Wix i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="62884-142">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="62884-143">**Jak zaktualizować pakiety, które są częścią szablony programu Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="62884-143">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="62884-144">Przejdź do **aktualizacje** w Interfejsie użytkownika Menedżera pakietów i zaznacz **Aktualizuj wszystkie**, lub użyj [ `Update-Package` polecenia](../Tools/ps-ref-update-package.md) w konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="62884-144">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../Tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="62884-145">Aby zaktualizować samego szablonu, należy ręcznie zaktualizować repozytorium szablonu.</span><span class="sxs-lookup"><span data-stu-id="62884-145">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="62884-146">Zobacz [blog Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) na ten temat.</span><span class="sxs-lookup"><span data-stu-id="62884-146">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="62884-147">Uwaga to zrobić na własne ryzyko, ponieważ ręcznej aktualizacji może spowodować uszkodzenie szablonu, jeśli najnowszą wersję wszystkich zależności nie są zgodne ze sobą.</span><span class="sxs-lookup"><span data-stu-id="62884-147">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="62884-148">**Można użyć NuGet poza programu Visual Studio?**</span><span class="sxs-lookup"><span data-stu-id="62884-148">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="62884-149">Tak, NuGet działa bezpośrednio z poziomu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="62884-149">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="62884-150">Zobacz [Przewodnik instalacji](../guides/install-nuget.md) i [odwołania interfejsu wiersza polecenia](../tools/nuget-exe-CLI-Reference.md).</span><span class="sxs-lookup"><span data-stu-id="62884-150">See the [Install guide](../guides/install-nuget.md) and the [CLI reference](../tools/nuget-exe-CLI-Reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="62884-151">Wiersz polecenia NuGet</span><span class="sxs-lookup"><span data-stu-id="62884-151">NuGet command line</span></span>

<span data-ttu-id="62884-152">**Jak uzyskać najnowszą wersję narzędzia wiersza polecenia NuGet?**</span><span class="sxs-lookup"><span data-stu-id="62884-152">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="62884-153">Zobacz [Przewodnik instalacji](../guides/install-nuget.md).</span><span class="sxs-lookup"><span data-stu-id="62884-153">See the [Install guide](../guides/install-nuget.md).</span></span>

<span data-ttu-id="62884-154">**Czy jest możliwe rozszerzenie NuGet narzędzia wiersza polecenia**</span><span class="sxs-lookup"><span data-stu-id="62884-154">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="62884-155">Tak, istnieje możliwość dodawania niestandardowych poleceń do `nuget.exe`, zgodnie z opisem w [post Tomasz Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="62884-155">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="62884-156">Konsola Menedżera pakietów NuGet (Visual Studio w systemie Windows)</span><span class="sxs-lookup"><span data-stu-id="62884-156">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="62884-157">**Jak uzyskać dostęp do obiektu DTE w konsoli Menedżera pakietów?**</span><span class="sxs-lookup"><span data-stu-id="62884-157">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="62884-158">Obiekt najwyższego poziomu w modelu obiektu automatyzacji programu Visual Studio jest wywołać obiekt DTE (Development Tools Environment).</span><span class="sxs-lookup"><span data-stu-id="62884-158">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="62884-159">Zapewnia to za pośrednictwem zmiennej o nazwie konsoli `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="62884-159">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="62884-160">Aby uzyskać więcej informacji, zobacz [omówienie modelu automatyzacji](https://docs.microsoft.com/visualstudio/extensibility/internals/automation-model-overview) w dokumentacji programu Visual Studio Extensibility.</span><span class="sxs-lookup"><span data-stu-id="62884-160">For more information, see [Automation Model Overview](https://docs.microsoft.com/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="62884-161">**Próbie rzutowania $DTE zmienną typu DTE2, ale występuje błąd: nie można przekonwertować wartości "EnvDTE.DTEClass" typu "EnvDTE.DTEClass" na typ "EnvDTE80.DTE2". Co jest nie tak?**</span><span class="sxs-lookup"><span data-stu-id="62884-161">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="62884-162">Jest to znany problem dotyczący współdziałania programu PowerShell z obiektu COM.</span><span class="sxs-lookup"><span data-stu-id="62884-162">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="62884-163">Spróbuj wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="62884-163">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="62884-164">`Get-Interface`Funkcja pomocnika jest dodawany przez hosta programu NuGet PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62884-164">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="62884-165">Tworzenie i publikowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="62884-165">Creating and publishing packages</span></span>

<span data-ttu-id="62884-166">**Jak wyświetlić listę Mój pakiet w źródło danych?**</span><span class="sxs-lookup"><span data-stu-id="62884-166">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="62884-167">Zobacz [tworzenie i publikowania pakietu](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="62884-167">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="62884-168">**Mam wiele wersji biblioteki, które odnoszą się do różnych wersji programu .NET Framework. Jak zbudować pojedynczy pakiet, który obsługuje tę funkcję?**</span><span class="sxs-lookup"><span data-stu-id="62884-168">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="62884-169">Zobacz [obsługi wielu wersje programu .NET Framework i profile](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="62884-169">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="62884-170">**Jak skonfigurować własną repozytorium lub źródła danych?**</span><span class="sxs-lookup"><span data-stu-id="62884-170">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="62884-171">Zobacz [hostingu — Omówienie pakietów](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="62884-171">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="62884-172">**Jak przesłać pakiety do mojego NuGet źródła danych zbiorczych**</span><span class="sxs-lookup"><span data-stu-id="62884-172">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="62884-173">Zobacz [zbiorcze publikowania pakietów NuGet](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="62884-173">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="62884-174">Praca z pakietami</span><span class="sxs-lookup"><span data-stu-id="62884-174">Working with packages</span></span>

<span data-ttu-id="62884-175">**Jaka jest różnica między pakietem poziom projektu i pakietu poziomu rozwiązania?**</span><span class="sxs-lookup"><span data-stu-id="62884-175">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="62884-176">Pakiet rozwiązanie na poziomie (NuGet 3.x+) jest zainstalowana tylko raz w rozwiązaniu i jest dostępna dla wszystkich projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="62884-176">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="62884-177">Pakiet poziom projektu jest zainstalowany w każdym projekcie, który korzysta z niego.</span><span class="sxs-lookup"><span data-stu-id="62884-177">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="62884-178">Pakiet poziomu rozwiązania może również zainstalować nowych poleceń, które mogą być wywoływane z poziomu konsoli Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="62884-178">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="62884-179">**Czy jest możliwe, można zainstalować pakietów NuGet bez łączności z Internetem?**</span><span class="sxs-lookup"><span data-stu-id="62884-179">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="62884-180">Tak, zobacz Scott Hanselman blogu [sposobu dostępu NuGet, gdy działa nuget.org (lub jesteś na płaszczyźnie)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="62884-180">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="62884-181">**Jak zainstalować pakiety w innej lokalizacji niż domyślny folder pakiety?**</span><span class="sxs-lookup"><span data-stu-id="62884-181">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="62884-182">Ustaw [ `repositoryPath` ](../Schema/nuget-config-file.md#config-section) w `Nuget.Config` przy użyciu `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="62884-182">Set the [`repositoryPath`](../Schema/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="62884-183">**Jak uniknąć dodawania do folderu pakietów NuGet do kontroli źródła**</span><span class="sxs-lookup"><span data-stu-id="62884-183">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="62884-184">Ustaw [ `disableSourceControlIntegration` ](../Schema/nuget-config-file.md#solution-section) w `Nuget.Config` do `true`.</span><span class="sxs-lookup"><span data-stu-id="62884-184">Set the [`disableSourceControlIntegration`](../Schema/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="62884-185">Ta działa klucza w rozwiązaniu poziomu i dlatego musi zostać dodany do `$(Solutiondir)\.nuget\Nuget.Config` pliku.</span><span class="sxs-lookup"><span data-stu-id="62884-185">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="62884-186">Włączanie Przywracanie pakietu z programu Visual Studio automatycznie tworzy ten plik.</span><span class="sxs-lookup"><span data-stu-id="62884-186">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="62884-187">**Jak wyłączyć przywracania pakietu**</span><span class="sxs-lookup"><span data-stu-id="62884-187">**How do I turn off package restore?**</span></span>

<span data-ttu-id="62884-188">Zobacz [Włączanie i wyłączanie Przywracanie pakietu](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="62884-188">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="62884-189">**Dlaczego otrzymuję błąd "Nie można rozpoznać zależności błąd" podczas instalowania lokalnego pakietu z zależności zdalnych?**</span><span class="sxs-lookup"><span data-stu-id="62884-189">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="62884-190">Musisz wybrać **wszystkie** źródła podczas instalowania lokalnego pakietu w projekcie.</span><span class="sxs-lookup"><span data-stu-id="62884-190">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="62884-191">To agreguje wszystkich źródeł danych zamiast przy użyciu tylko jednego.</span><span class="sxs-lookup"><span data-stu-id="62884-191">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="62884-192">Przyczyna ten błąd pojawia się jest, że użytkownicy lokalnego repozytorium często chcą uniknąć przypadkowego instalowania zdalnego pakietu z powodu firmowe zasady.</span><span class="sxs-lookup"><span data-stu-id="62884-192">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="62884-193">**Mam wiele projektów, w tym samym folderze, do czego służy packages.config oddzielne pliki dla każdego projektu?**</span><span class="sxs-lookup"><span data-stu-id="62884-193">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="62884-194">W większości projektów miejsca zamieszkania osobne projekty w oddzielnych folderach, nie jest to problem jak identyfikuje NuGet `packages.config` plików w każdym projekcie.</span><span class="sxs-lookup"><span data-stu-id="62884-194">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="62884-195">Nuget 3.3 + i jest wiele projektów, w tym samym folderze, można wstawić nazwę projektu w `packages.config` nazw plików, użyj wzorca `packages.{project-name}.config`, i NuGet korzysta z tego pliku.</span><span class="sxs-lookup"><span data-stu-id="62884-195">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="62884-196">To nie jest problem przy użyciu PackageReference, ponieważ każdy plik projektu zawiera własną listę zależności.</span><span class="sxs-lookup"><span data-stu-id="62884-196">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="62884-197">**Nuget.org nie jest wyświetlane na liście repozytoriów, jak pobrać go ponownie?**</span><span class="sxs-lookup"><span data-stu-id="62884-197">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="62884-198">Dodaj `https://api.nuget.org/v3/index.json` do listy źródeł, lub</span><span class="sxs-lookup"><span data-stu-id="62884-198">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="62884-199">Usuń `%appdata%\.nuget\NuGet.Config` i pozwól NuGet, utwórz go ponownie.</span><span class="sxs-lookup"><span data-stu-id="62884-199">Delete the `%appdata%\.nuget\NuGet.Config` and let NuGet re-create it.</span></span>

<span data-ttu-id="62884-200">**Jakie są domyślne licencji warunki Jeśli pakietu nie zawierają informacje o licencji określonego?**</span><span class="sxs-lookup"><span data-stu-id="62884-200">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="62884-201">Każdy pakiet jest objęte postanowienia, które są dołączone do pakietu.</span><span class="sxs-lookup"><span data-stu-id="62884-201">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="62884-202">Należy przejrzeć postanowienia mające zastosowanie przed uzyskiwanie dostępu do, pobierania lub uzyskiwania wszystkie pakiety.</span><span class="sxs-lookup"><span data-stu-id="62884-202">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="62884-203">Na nuget.org, użyj **informacje dotyczące licencji** łącze na stronie pakiet.</span><span class="sxs-lookup"><span data-stu-id="62884-203">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="62884-204">Jeśli pakiet nie określa postanowień licencyjnych, skontaktuj się z właścicielem pakietu bezpośrednio za pomocą **skontaktuj się z właścicieli** łącze na stronie pakiet nuget.org.</span><span class="sxs-lookup"><span data-stu-id="62884-204">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="62884-205">Microsoft nie licencji jakiejkolwiek własności intelektualnej użytkownikowi od innych dostawców pakietu i nie jest odpowiedzialny za informacji dostarczonych przez strony trzecie.</span><span class="sxs-lookup"><span data-stu-id="62884-205">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>


## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="62884-206">Zarządzanie pakietami na nuget.org</span><span class="sxs-lookup"><span data-stu-id="62884-206">Managing packages on nuget.org</span></span>

<span data-ttu-id="62884-207">**Metadane pakietów można edytować po jest przekazane? Dlaczego zalecamy edycji plik nuspec i przekazać nowy pakiet do wprowadzania zmian do pakietu metadanych?**</span><span class="sxs-lookup"><span data-stu-id="62884-207">**Can I edit package metadata after it's been uploaded? Why do you recommend editing the nuspec and uploading a new package for making changes to package metadata?**</span></span>

<span data-ttu-id="62884-208">Będzie można implementacja NuGet podpisywania pakietu.</span><span class="sxs-lookup"><span data-stu-id="62884-208">NuGet will be implementing package signing.</span></span> <span data-ttu-id="62884-209">Zasada projektowania podpisywania pakietu jest, że zawartość podpisanego pakietu musi być niezmienne, która obejmuje plik nuspec.</span><span class="sxs-lookup"><span data-stu-id="62884-209">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="62884-210">Edytowanie metadanych pakietu powoduje zmian w plik nuspec, unieważnienie istniejących podpisów.</span><span class="sxs-lookup"><span data-stu-id="62884-210">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="62884-211">Zaleca się zmodyfikowanie istniejącej przepływy pracy, aby nie wymagają edycji metadanych pakietu po utworzeniu pakietu.</span><span class="sxs-lookup"><span data-stu-id="62884-211">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="62884-212">Należy pamiętać, że zależności dla pakietu są generowane automatycznie z pakietu się i nie można edytować.</span><span class="sxs-lookup"><span data-stu-id="62884-212">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="62884-213">Ponadto przekazywania pakietów do [staging.nuget.org](http://staging.nuget.org) jest doskonałym sposobem testowanie i weryfikowanie pakietu bez udostępniania pakietu w publicznej galerii.</span><span class="sxs-lookup"><span data-stu-id="62884-213">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="62884-214">**Czy jest możliwe do zarezerwowania nazwy pakietów, które zostaną opublikowane w przyszłości?**</span><span class="sxs-lookup"><span data-stu-id="62884-214">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="62884-215">Tak.</span><span class="sxs-lookup"><span data-stu-id="62884-215">Yes.</span></span> <span data-ttu-id="62884-216">Identyfikatory pakietów można zarezerwować na [nuget.org](https://www.nuget.org/) przez zażądanie prefiks Identyfikatora pakietu dla Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="62884-216">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="62884-217">Aby poprosić o prefiks Identyfikatora pakietu, wysyłanie poczty do konta (nuget.org Nazwa wyświetlana pakietu właściciela i prefiks Identyfikatora żądanego pakietu w).</span><span class="sxs-lookup"><span data-stu-id="62884-217">In order to request a package ID prefix, send mail to account (at) nuget.org with the package owner display name, and the requested package ID prefix.</span></span>  

<span data-ttu-id="62884-218">**Jak potwierdzić prawa własności do pakietów?**</span><span class="sxs-lookup"><span data-stu-id="62884-218">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="62884-219">Zobacz [Zarządzanie właścicieli pakietu na nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="62884-219">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="62884-220">**Sposób postępowania z właścicielem pakietu, który narusza Moje licencji na oprogramowanie**</span><span class="sxs-lookup"><span data-stu-id="62884-220">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="62884-221">Firma Microsoft zachęca społeczności NuGet współdziałają ze sobą rozwiązywać wszelkie sporów, które mogą wystąpić podczas między właścicieli pakietu i innego oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="62884-221">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="62884-222">Firma Microsoft ma co [rozstrzygania procesu rozpoznawania](../policies/dispute-resolution.md) do wykonania przed żądaniem administratorom nuget.org intercede.</span><span class="sxs-lookup"><span data-stu-id="62884-222">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="62884-223">**Przekaż moje pakietów testowych do nuget.org jest zalecane?**</span><span class="sxs-lookup"><span data-stu-id="62884-223">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="62884-224">Do celów testowych można użyć [staging.nuget.org](http://staging.nuget.org), lub alternatywne publiczne serwery NuGet, takich jak [myget.org](https://myget.org) lub [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span><span class="sxs-lookup"><span data-stu-id="62884-224">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="62884-225">Należy pamiętać, że pakiety przekazane do staging.nuget.org mogą nie zostać zachowane.</span><span class="sxs-lookup"><span data-stu-id="62884-225">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="62884-226">Zobacz [Podgląd praktyczny brak jakichkolwiek](http://blog.nuget.org/20130419/goodbye-preview.html).</span><span class="sxs-lookup"><span data-stu-id="62884-226">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="62884-227">**Co to jest maksymalny rozmiar pakietów, które można przekazać do nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="62884-227">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="62884-228">nuget.org umożliwia pakietów do 250MB, ale firma Microsoft zaleca się utrzymywanie pakietów w obszarze 1MB, jeśli to możliwe, a następnie połącz pakietów przy użyciu zależności.</span><span class="sxs-lookup"><span data-stu-id="62884-228">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="62884-229">Zasadą zawierać tylko jeden zestaw, aby uniknąć kolizji pakietów.</span><span class="sxs-lookup"><span data-stu-id="62884-229">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="62884-230">NuGet korzysta z protokołu HTTP do pobierania pakietów, więc pakietów większych niż mniejszych wyższe prawdopodobieństwo instaluje nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="62884-230">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="62884-231">Istnieje możliwość udostępniania zależności między kilka pakietów, co mniejszy rozmiar całkowitą pobierania dla konsumentów pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="62884-231">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="62884-232">Zależności są prawie statyczna i nigdy nie zmiany.</span><span class="sxs-lookup"><span data-stu-id="62884-232">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="62884-233">Po usunięciu błędu w kodzie, zależności nie muszą zostać zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="62884-233">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="62884-234">Jeśli pakietu zależności, przechodzili reshipping pakietów większych zawsze.</span><span class="sxs-lookup"><span data-stu-id="62884-234">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="62884-235">Dzieląc pakietów NuGet w zależności powiązane, uaktualnienia są bardziej szczegółowych dla konsumentów do pakietu.</span><span class="sxs-lookup"><span data-stu-id="62884-235">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="62884-236">nuget.org niedostępny</span><span class="sxs-lookup"><span data-stu-id="62884-236">nuget.org not accessible</span></span>

<span data-ttu-id="62884-237">**Dlaczego nie można pobrać pakietów z ani przekazywać pakiety do nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="62884-237">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="62884-238">Najpierw upewnij się, że używasz najnowszej wersji programu NuGet.</span><span class="sxs-lookup"><span data-stu-id="62884-238">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="62884-239">Jeśli w tej wersji zakończy się niepowodzeniem, [się z pomocą techniczną](https://www.nuget.org/policies/Contact) i podaj dodatkowego połączenia Rozwiązywanie problemów z informacje w tym:</span><span class="sxs-lookup"><span data-stu-id="62884-239">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="62884-240">Wersja programu NuGet używasz</span><span class="sxs-lookup"><span data-stu-id="62884-240">The version of NuGet you're using</span></span>
- <span data-ttu-id="62884-241">Używanego źródła pakietu</span><span class="sxs-lookup"><span data-stu-id="62884-241">The package sources you're using</span></span>
- <span data-ttu-id="62884-242">Dziennik przywracania o poziomie szczegółowości szczegółowe</span><span class="sxs-lookup"><span data-stu-id="62884-242">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="62884-243">MTR lub Fiddler dane śledzenia (zobacz poniżej)</span><span class="sxs-lookup"><span data-stu-id="62884-243">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="62884-244">Obszar geograficzny</span><span class="sxs-lookup"><span data-stu-id="62884-244">Your geographical area</span></span>
- <span data-ttu-id="62884-245">Wersji systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="62884-245">Your operating system version</span></span>
- <span data-ttu-id="62884-246">Konfiguracja maszyny (Procesora i sieci, dysk twardy)</span><span class="sxs-lookup"><span data-stu-id="62884-246">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="62884-247">Określa, czy jest komputer serwera proxy lub zapory</span><span class="sxs-lookup"><span data-stu-id="62884-247">Whether is your machine behind a proxy or firewall</span></span>
- <span data-ttu-id="62884-248">Wersje programu .NET, które są zainstalowane na tym komputerze</span><span class="sxs-lookup"><span data-stu-id="62884-248">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="62884-249">Wersje narzędzi i platform, takich jak .NET interfejsu wiersza polecenia lub DNU, którego używasz</span><span class="sxs-lookup"><span data-stu-id="62884-249">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="62884-250">*Aby przechwycić MTR:*</span><span class="sxs-lookup"><span data-stu-id="62884-250">*To capture MTR:*</span></span>

- <span data-ttu-id="62884-251">Pobierz WinMTR z [http://winmtr.net/download/](http://winmtr.net/)</span><span class="sxs-lookup"><span data-stu-id="62884-251">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="62884-252">Wprowadź `api.nuget.org` jako nazwę hosta i kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="62884-252">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="62884-253">Poczekaj na **wysłane** kolumny > = 100.</span><span class="sxs-lookup"><span data-stu-id="62884-253">Wait until the **Sent** column is >= 100.</span></span>

    ![Przechwytywanie MTR](media/mtr.png)

- <span data-ttu-id="62884-255">Skopiować tekst do Schowka.</span><span class="sxs-lookup"><span data-stu-id="62884-255">Copy text to clipboard.</span></span>

<span data-ttu-id="62884-256">*Aby przechwycić Fiddler:*</span><span class="sxs-lookup"><span data-stu-id="62884-256">*To capture Fiddler:*</span></span>

- <span data-ttu-id="62884-257">Zainstaluj najnowszą wersję pakietu [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="62884-257">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="62884-258">Uruchom narzędzie Fiddler i Wyłącz Przechwytywanie ruchu przy użyciu **pliku > przechwytywania ruchu** menu.</span><span class="sxs-lookup"><span data-stu-id="62884-258">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="62884-259">Usuń wszystkie sesje (Wybierz wszystkie elementy na liście, naciśnij klawisz **usunąć** klucza).</span><span class="sxs-lookup"><span data-stu-id="62884-259">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="62884-260">Konfigurowanie narzędzia Fiddler do przechwytywania ruchu HTTPS, sprawdzając **ruchu HTTPS odszyfrować** w **HTTPS** karcie **Narzędzia > Opcje Fiddler...**  menu.</span><span class="sxs-lookup"><span data-stu-id="62884-260">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="62884-261">Zamknij program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="62884-261">Close Visual Studio.</span></span>
- <span data-ttu-id="62884-262">Włącz **pliku > przechwytywania ruchu** menu.</span><span class="sxs-lookup"><span data-stu-id="62884-262">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="62884-263">Uruchom program Visual Studio lub nuget.exe .exe i wykonać akcje, które nie działają.</span><span class="sxs-lookup"><span data-stu-id="62884-263">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="62884-264">Ruch generowany przez te akcje powinny być widoczne w narzędziu Fiddler.</span><span class="sxs-lookup"><span data-stu-id="62884-264">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="62884-265">Po akcje zostało uruchomione, użyj **Plik > Zapisz > wszystkie sesje** do przechowywania przechwyconego sesji.</span><span class="sxs-lookup"><span data-stu-id="62884-265">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="62884-266">Uwaga: może być konieczne można ustawić `HTTP_PROXY` zmienną środowiskową `http://127.0.0.1:8888` dla routingu ruchu NuGet przez Fiddler.</span><span class="sxs-lookup"><span data-stu-id="62884-266">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="62884-267">W przypadku niepowodzenia spróbuj [porady wymienione w tym wpisie StackOverflow](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span><span class="sxs-lookup"><span data-stu-id="62884-267">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="62884-268">**Co to są punkty końcowe interfejsu API dla nuget.org?**</span><span class="sxs-lookup"><span data-stu-id="62884-268">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="62884-269">W wersji 3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (należy pamiętać, że interfejs API w wersji 2 jest przestarzała i nie działa z programem NuGet 4.)</span><span class="sxs-lookup"><span data-stu-id="62884-269">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
