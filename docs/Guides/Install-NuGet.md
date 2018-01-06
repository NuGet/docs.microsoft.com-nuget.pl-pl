---
title: "Instalowanie narzędzi klienta NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "Wskazówki na temat instalowania narzędzi klienta, interfejsu wiersza polecenia (CLI) i Menedżer pakietów dla programu Visual Studio."
keywords: "nuget.exe interfejsu wiersza polecenia narzędzia klienta NuGet, Menedżer pakietów NuGet, konsoli Menedżera pakietów NuGet, NuGet dla programu Visual Studio, NuGet w wersji beta kanału"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2f67c298d269149bba9f36ad9e026d5443c39b6a
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="installing-nuget-client-tools"></a><span data-ttu-id="17148-104">Instalowanie narzędzi klienta NuGet</span><span class="sxs-lookup"><span data-stu-id="17148-104">Installing NuGet client tools</span></span>

> [!Tip]
> <span data-ttu-id="17148-105">**Wyszukiwanie, aby zainstalować pakiet? Zobacz [Szybki Start - Użyj pakietu](../Quickstart/Use-a-Package.md).**</span><span class="sxs-lookup"><span data-stu-id="17148-105">**Looking to install a package? See [Quickstart - Use a package](../Quickstart/Use-a-Package.md).**</span></span>

<span data-ttu-id="17148-106">Istnieją dwa podstawowe narzędzia ułatwiających tworzenie, publikowanie i korzystać z pakietów NuGet:</span><span class="sxs-lookup"><span data-stu-id="17148-106">There are two primary tools available to help you build, publish and consume NuGet packages:</span></span>

1. <span data-ttu-id="17148-107">[ **Interfejsu wiersza polecenia NuGet** ](#nuget-cli) to narzędzie wiersza polecenia dla systemu Windows, który zawiera wszystkie funkcje NuGet; może również być uruchomione na systemu Mac OS x i Linux za pomocą Mono lub za pośrednictwem interfejsu wiersza polecenia platformy .NET Core (`dotnet`).</span><span class="sxs-lookup"><span data-stu-id="17148-107">The [**NuGet CLI**](#nuget-cli) is the command-line utility for Windows that provides all NuGet capabilities; it can also be run on Mac OSX and Linux using Mono, or through the .NET Core CLI (`dotnet`).</span></span>
1. <span data-ttu-id="17148-108">[ **Menedżera pakietów NuGet w programie Visual Studio** ](#nuget-package-manager-in-visual-studio) (tylko system Windows) jest narzędziem do graficznego interfejsu użytkownika dla zarządzania pakietów i obejmuje konsolę programu PowerShell, za pomocą których można użyć pewnych poleceń NuGet bezpośrednio z poziomu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17148-108">The [**NuGet Package Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows only) is a GUI tool for managing packages and includes a PowerShell console through which you can use certain NuGet commands directly within Visual Studio.</span></span> <span data-ttu-id="17148-109">Interfejs użytkownika Menedżera pakietów i konsoli są dołączone do programu Visual Studio (w systemie Windows), 2012 lub nowszy i może zostać zainstalowany ręcznie w przypadku wcześniejszych wersji.</span><span class="sxs-lookup"><span data-stu-id="17148-109">The Package Manager UI and Console are both included with Visual Studio (on Windows) 2012 and later and can be installed manually for earlier versions.</span></span>

    <span data-ttu-id="17148-110">Program Visual Studio dla komputerów Mac możliwości NuGet są wbudowane bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="17148-110">With Visual Studio for Mac, NuGet capabilities are built in directly.</span></span> <span data-ttu-id="17148-111">Zobacz [pakietu w tym NuGet w projekcie](/visualstudio/mac/nuget-walkthrough) przewodnik.</span><span class="sxs-lookup"><span data-stu-id="17148-111">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough) for a walkthrough.</span></span>

    <span data-ttu-id="17148-112">Visual Studio Code obecnie nie ma żadnych wbudowana obsługa NuGet.</span><span class="sxs-lookup"><span data-stu-id="17148-112">Visual Studio Code at present does not have any built-in NuGet support.</span></span> <span data-ttu-id="17148-113">Użyj interfejsu wiersza polecenia NuGet lub [dotnet interfejsu wiersza polecenia](../Tools/dotnet-Commands.md).</span><span class="sxs-lookup"><span data-stu-id="17148-113">Use the NuGet CLI or the [dotnet CLI](../Tools/dotnet-Commands.md).</span></span>

<span data-ttu-id="17148-114">Interfejs wiersza polecenia NuGet i Package Manager obsługuje następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="17148-114">The NuGet CLI and Package Manager both support the following operations:</span></span>

- <span data-ttu-id="17148-115">Pakiety wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="17148-115">Search packages</span></span>
- <span data-ttu-id="17148-116">Instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="17148-116">Install packages</span></span>
- <span data-ttu-id="17148-117">Pakiety aktualizacji</span><span class="sxs-lookup"><span data-stu-id="17148-117">Update packages</span></span>
- <span data-ttu-id="17148-118">Odinstalowania pakietów</span><span class="sxs-lookup"><span data-stu-id="17148-118">Uninstall packages</span></span>
- <span data-ttu-id="17148-119">Przywracanie pakietów (tylko w Menedżerze pakietów interfejsu użytkownika)</span><span class="sxs-lookup"><span data-stu-id="17148-119">Restore packages (UI only in the Package Manager)</span></span>
- <span data-ttu-id="17148-120">Zarządzaj źródłami NuGet</span><span class="sxs-lookup"><span data-stu-id="17148-120">Manage NuGet sources</span></span>

<span data-ttu-id="17148-121">Następujące funkcje są obsługiwane tylko w przypadku interfejsu wiersza polecenia NuGet:</span><span class="sxs-lookup"><span data-stu-id="17148-121">The following capabilities are supported only in the NuGet CLI:</span></span>

- <span data-ttu-id="17148-122">Zarządzaj pakietami (nuget.org lub prywatnej źródła danych)</span><span class="sxs-lookup"><span data-stu-id="17148-122">Manage packages (nuget.org or private feed)</span></span>
- <span data-ttu-id="17148-123">Tworzenie pakietów</span><span class="sxs-lookup"><span data-stu-id="17148-123">Create packages</span></span> 
- <span data-ttu-id="17148-124">Publikowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="17148-124">Publish packages</span></span>
- <span data-ttu-id="17148-125">Zarządzanie pliku Nuget.Config.</span><span class="sxs-lookup"><span data-stu-id="17148-125">Manage Nuget.Config</span></span>
- <span data-ttu-id="17148-126">Zarządzanie pamięcią podręczną NuGet</span><span class="sxs-lookup"><span data-stu-id="17148-126">Manage the NuGet cache</span></span>
- <span data-ttu-id="17148-127">Replikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="17148-127">Replicating a package</span></span>

> [!Note]
> <span data-ttu-id="17148-128">Kolejnym narzędziem dobrej jest [Explorer pakietu NuGet](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), open source, autonomiczne narzędzie, aby wizualnie eksplorować, tworzyć i edytować pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="17148-128">Another good tool is the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), an open-source, stand-alone tool to visually explore, create, and edit NuGet packages.</span></span> <span data-ttu-id="17148-129">Bardzo przydatne, jest na przykład zmienić eksperymentalne Struktura pakietu bez konieczności Skompiluj ponownie pakiet zawsze.</span><span class="sxs-lookup"><span data-stu-id="17148-129">It's very helpful, for example, to make experimental changes to a package structure without having to rebuild the package each time.</span></span>
> <span data-ttu-id="17148-130">Obsługujący wiele platform [interfejsu wiersza polecenia platformy .NET Core](/dotnet/articles/core/tools/index#installation) łańcuch narzędzi, używany do tworzenia aplikacji platformy .NET Core obsługuje kilka polecenia NuGet, takich jak usuwanie, zmienne lokalne, wypychania, pakietu i przywracania.</span><span class="sxs-lookup"><span data-stu-id="17148-130">The cross-platform [.NET Core CLI](/dotnet/articles/core/tools/index#installation) toolchain, used for developing .NET Core applications, supports several NuGet commands, such as delete, locals, push, pack, and restore.</span></span> 

## <a name="nuget-cli"></a><span data-ttu-id="17148-131">Interfejs wiersza polecenia NuGet</span><span class="sxs-lookup"><span data-stu-id="17148-131">NuGet CLI</span></span>

<span data-ttu-id="17148-132">Interfejs wiersza polecenia NuGet zapewnia dostęp do wszystkich funkcji NuGet i mogą być uruchamiane w systemach Windows, Mac OS x i Linux, zgodnie z opisem w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="17148-132">The NuGet command-line interface provides access to all NuGet capabilities, and can be run on Windows, Mac OSX, and Linux as described in the following sections.</span></span>

### <a name="windows"></a><span data-ttu-id="17148-133">Windows</span><span class="sxs-lookup"><span data-stu-id="17148-133">Windows</span></span>

<span data-ttu-id="17148-134">**Pobieranie bezpośrednie:**</span><span class="sxs-lookup"><span data-stu-id="17148-134">**Direct download:**</span></span>

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> <span data-ttu-id="17148-135">Nuget 1.4 +, można użyć `nuget update -self` aktualizacji z istniejących nuget.exe do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="17148-135">With NuGet 1.4+, you can use `nuget update -self` to update your existing nuget.exe to the latest version.</span></span>

<span data-ttu-id="17148-136">**Inne metody:**</span><span class="sxs-lookup"><span data-stu-id="17148-136">**Other methods:**</span></span>

- <span data-ttu-id="17148-137">**Chocolatey**: Zainstaluj [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey pakietu przy użyciu [Chocolatey](http://chocolatey.org) klienta.</span><span class="sxs-lookup"><span data-stu-id="17148-137">**Chocolatey**: Install the [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey package using the [Chocolatey](http://chocolatey.org) client.</span></span> 

    ```ps
    choco install nuget.commandline
    ```

- <span data-ttu-id="17148-138">**Visual Studio**: Zainstaluj [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) pakietu w konsoli Menedżera pakietów w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17148-138">**Visual Studio**: Install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the Package Manager Console in Visual Studio.</span></span>

    > [!Note]
    > <span data-ttu-id="17148-139">**Dla użytkowników 2.x NuGet**: ze względu na istotne zmiany wprowadzone w NuGet 3.2 [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) trwania stanu stabilnego punktów do najnowszej wersji 2.x NuGet, aby zapobiec systemów ciągłej integracji z potencjalnie przerywanie.</span><span class="sxs-lookup"><span data-stu-id="17148-139">**For NuGet 2.x users**: Because of breaking changes introduced in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) points to the latest stable NuGet 2.x release to prevent continuous integration systems from potentially breaking.</span></span>

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a><span data-ttu-id="17148-140">Mac OS x i Linux</span><span class="sxs-lookup"><span data-stu-id="17148-140">Mac OSX and Linux</span></span>

<span data-ttu-id="17148-141">W systemie Mac OS x i Linux istnieją dwa sposoby uruchamiania interfejsu wiersza polecenia NuGet:</span><span class="sxs-lookup"><span data-stu-id="17148-141">On Mac OSX and Linux, there are two ways to run the NuGet CLI:</span></span>

- <span data-ttu-id="17148-142">Zainstaluj [.NET Core SDK](https://www.microsoft.com/net/download/core), która obejmuje podstawowych możliwości NuGet.</span><span class="sxs-lookup"><span data-stu-id="17148-142">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core), which includes the core NuGet capabilities.</span></span> <span data-ttu-id="17148-143">Pliki do pobrania znajdują się na [github.com/dotnet/cli](https://github.com/dotnet/cli).</span><span class="sxs-lookup"><span data-stu-id="17148-143">Downloads are also listed on [github.com/dotnet/cli](https://github.com/dotnet/cli).</span></span> <span data-ttu-id="17148-144">Jeśli potrzebujesz możliwości na pełniejsze, następnie użyć opcji drugi poniżej do użycia `nuget.exe` z Mono.</span><span class="sxs-lookup"><span data-stu-id="17148-144">If you need fuller capabilities, then use the second option below to use `nuget.exe` with Mono.</span></span>

- <span data-ttu-id="17148-145">Zainstaluj [Mono](http://www.mono-project.com/docs/getting-started/install/) , a następnie użyj `nuget.exe` pliku wykonywalnego wiersza polecenia dla systemu Windows (w wersji 3.2 i nowszej) z [nuget.org/downloads](https://nuget.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="17148-145">Install [Mono](http://www.mono-project.com/docs/getting-started/install/) and then use the `nuget.exe` command-line executable for Windows (version 3.2 and later) from [nuget.org/downloads](https://nuget.org/downloads).</span></span> <span data-ttu-id="17148-146">Systemem NuGet Mono podlega następującym ograniczeniom:</span><span class="sxs-lookup"><span data-stu-id="17148-146">Running NuGet on Mono is subject to the following limitations:</span></span>

    - <span data-ttu-id="17148-147">Przetestowany pod kątem pracy polecenia:</span><span class="sxs-lookup"><span data-stu-id="17148-147">Commands tested to work:</span></span>
        - <span data-ttu-id="17148-148">Konfiguracji</span><span class="sxs-lookup"><span data-stu-id="17148-148">config</span></span>
        - <span data-ttu-id="17148-149">Usuń</span><span class="sxs-lookup"><span data-stu-id="17148-149">delete</span></span>
        - <span data-ttu-id="17148-150">Pomoc</span><span class="sxs-lookup"><span data-stu-id="17148-150">help</span></span>
        - <span data-ttu-id="17148-151">Zainstaluj</span><span class="sxs-lookup"><span data-stu-id="17148-151">install</span></span>
        - <span data-ttu-id="17148-152">list</span><span class="sxs-lookup"><span data-stu-id="17148-152">list</span></span>
        - <span data-ttu-id="17148-153">Push</span><span class="sxs-lookup"><span data-stu-id="17148-153">push</span></span>
        - <span data-ttu-id="17148-154">setApiKey</span><span class="sxs-lookup"><span data-stu-id="17148-154">setApiKey</span></span>
        - <span data-ttu-id="17148-155">Źródeł</span><span class="sxs-lookup"><span data-stu-id="17148-155">sources</span></span>
        - <span data-ttu-id="17148-156">Specyfikacja</span><span class="sxs-lookup"><span data-stu-id="17148-156">spec</span></span>

    - <span data-ttu-id="17148-157">Częściowo pracy polecenia:</span><span class="sxs-lookup"><span data-stu-id="17148-157">Partially-working commands:</span></span>
        - <span data-ttu-id="17148-158">pakiet: współpracuje z `.nuspec` plików, ale nie pliki projektu.</span><span class="sxs-lookup"><span data-stu-id="17148-158">pack: works with `.nuspec` files but not with project files.</span></span>
        - <span data-ttu-id="17148-159">Przywróć: współpracuje z `packages.config` i `project.json` plików, ale nie z rozwiązania (`.sln`) plików.</span><span class="sxs-lookup"><span data-stu-id="17148-159">restore: works with `packages.config` and `project.json` files but not with solution (`.sln`) files.</span></span>

    - <span data-ttu-id="17148-160">Polecenia, które nie są obsługiwane:</span><span class="sxs-lookup"><span data-stu-id="17148-160">Commands that do not work:</span></span>
        - <span data-ttu-id="17148-161">Aktualizacja</span><span class="sxs-lookup"><span data-stu-id="17148-161">update</span></span>

### <a name="related-topics"></a><span data-ttu-id="17148-162">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="17148-162">Related topics</span></span>

- [<span data-ttu-id="17148-163">Odwołanie do interfejsu wiersza polecenia NuGet</span><span class="sxs-lookup"><span data-stu-id="17148-163">NuGet CLI reference</span></span>](../tools/nuget-exe-cli-reference.md)
- [<span data-ttu-id="17148-164">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="17148-164">Creating a package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="17148-165">Publikowania pakietu</span><span class="sxs-lookup"><span data-stu-id="17148-165">Publishing a Package</span></span>](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a><span data-ttu-id="17148-166">Menedżer pakietów NuGet w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="17148-166">NuGet Package Manager in Visual Studio</span></span>

<span data-ttu-id="17148-167">Menedżer pakietów NuGet jest zawarte we wszystkich wersjach programu Visual Studio w systemie Windows 2012 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="17148-167">The NuGet Package Manager is included in every edition of Visual Studio on Windows, 2012 and later.</span></span> <span data-ttu-id="17148-168">Obejmuje on interfejsu użytkownika Menedżera pakietów ([odwołania](../tools/package-manager-ui.md)), a konsola Menedżera pakietów, za pomocą którego można uzyskać dostępu do narzędzi, które pochodzą z niektórych pakietów ([odwołania](../tools/package-manager-console.md)).</span><span class="sxs-lookup"><span data-stu-id="17148-168">It includes the Package Manager UI ([reference](../tools/package-manager-ui.md)), and the Package Manager Console through which you can access tools that come with certain packages ([reference](../tools/package-manager-console.md)).</span></span>

<span data-ttu-id="17148-169">Instalator programu Visual Studio 2017 obejmuje Menedżera pakietów NuGet z dowolnym obciążeniu używającego .NET.</span><span class="sxs-lookup"><span data-stu-id="17148-169">The Visual Studio 2017 installer includes the NuGet Package Manager with any workload that employs .NET.</span></span> <span data-ttu-id="17148-170">Aby zainstalować oddzielnie lub sprawdź, czy jest zainstalowany Menedżer pakietów, uruchom Instalatora programu Visual Studio 2017 i zaznacz opcję w obszarze **pojedynczych składników > narzędzia Code > Menedżera pakietów NuGet**.</span><span class="sxs-lookup"><span data-stu-id="17148-170">To install separately, or to verify that the Package Manager is installed, run the Visual Studio 2017 installer and check the option under **Individual Components > Code tools > NuGet package manager**.</span></span>

> [!Note]
> <span data-ttu-id="17148-171">Wymaga konsoli [PowerShell 2.0](http://support.microsoft.com/kb/968929), który już będzie zainstalowanego w systemach Windows 7 lub nowszy i Windows Server 2008 R2 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="17148-171">The console requires [PowerShell 2.0](http://support.microsoft.com/kb/968929), which will already be installed on Windows 7 or higher and Windows Server 2008 R2 or higher.</span></span>
>
> <span data-ttu-id="17148-172">Konsola Menedżera pakietów polecenia również działać tylko w programie Visual Studio w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="17148-172">Package Manager Console commands also work only within Visual Studio on Windows.</span></span> <span data-ttu-id="17148-173">Za pomocą interfejsu wiersza polecenia NuGet poza tym środowiskiem, łącznie z programem Visual Studio for Mac i Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="17148-173">Use the NuGet CLI outside of that environment, including with Visual Studio for Mac and Visual Studio Code.</span></span>

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a><span data-ttu-id="17148-174">Instalacja Menedżera pakietów dla programu Visual Studio 2010 i starszych wersji</span><span class="sxs-lookup"><span data-stu-id="17148-174">Package Manager installation for Visual Studio 2010 and earlier</span></span>

<span data-ttu-id="17148-175">*Te kroki nie są niezbędne dla programu Visual Studio 2012 lub nowszym, które już zawierają Menedżera pakietów.*</span><span class="sxs-lookup"><span data-stu-id="17148-175">*These steps are not necessary for Visual Studio 2012 and later, which already include the Package Manager.*</span></span>

1. <span data-ttu-id="17148-176">W programie Visual Studio 2010 i starszych wersji, kliknij przycisk **Narzędzia > rozszerzenia i aktualizacje**.</span><span class="sxs-lookup"><span data-stu-id="17148-176">In Visual Studio 2010 and earlier, click **Tools > Extension and Updates**.</span></span>
1. <span data-ttu-id="17148-177">Przejdź do **Online**, następnie wyszukaj "NuGet pakietu Manager dla programu Visual Studio" i kliknij przycisk **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="17148-177">Navigate to **Online**, then search for "NuGet Package Manager for Visual Studio" and click **Download**.</span></span>
1. <span data-ttu-id="17148-178">W oknie dialogowym Instalatora, kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="17148-178">In the Installer dialog box, click **Install**.</span></span>
1. <span data-ttu-id="17148-179">Po zakończeniu instalacji uruchom ponownie program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17148-179">When installation is complete, restart Visual Studio.</span></span>

> [!Tip]
> <span data-ttu-id="17148-180">Jeśli nie można użyć **rozszerzenia i aktualizacje** okna dialogowego w programie Visual Studio (na przykład zablokowanych przez serwer proxy), możesz pobrać rozszerzeń dla programu Visual Studio 2013 i 2015 bezpośrednio na [https://dist.nuget.org/ index.HTML](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="17148-180">If you're unable to use the **Extensions and Updates** dialog in Visual Studio (for example, its blocked by a proxy), you can download extensions for Visual Studio 2013 and 2015 directly at [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

### <a name="updating-the-package-manager"></a><span data-ttu-id="17148-181">Aktualizowanie Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="17148-181">Updating the Package Manager</span></span>

<span data-ttu-id="17148-182">Dla programu Visual Studio 2015 Update 2 lub nowszego oraz Package Manager zostanie automatycznie zaktualizowany do najnowszej wersji stabilnej.</span><span class="sxs-lookup"><span data-stu-id="17148-182">For Visual Studio 2015 Update 2 and later, the Package Manager is automatically updated to the latest stable release.</span></span>

<span data-ttu-id="17148-183">Dla programu Visual Studio 2015 Update 1 i starszych wersji, wybierz **Narzędzia > rozszerzenia i aktualizacje** polecenia, a następnie kliknij polecenie **aktualizacje** kartę, aby zobaczyć, czy dostępna jest nowa wersja Menedżera pakietów.</span><span class="sxs-lookup"><span data-stu-id="17148-183">For Visual Studio 2015 Update 1 and earlier, select the **Tools > Extensions and Updates** command and click on the **Updates** tab to see if a new version of the Package Manager is available.</span></span>  

### <a name="nuget-previews"></a><span data-ttu-id="17148-184">Podglądy NuGet</span><span class="sxs-lookup"><span data-stu-id="17148-184">NuGet previews</span></span>

<span data-ttu-id="17148-185">Jeśli chcesz nadchodzących funkcji NuGet w wersji zapoznawczej, zainstaluj [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), który działa side-by-side z stabilne wersje programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17148-185">If you'd like to preview upcoming NuGet features, install the [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), which works side-by-side with stable releases of Visual Studio.</span></span>

<span data-ttu-id="17148-186">Należy pamiętać, że kanał poprzedniej wersji Beta NuGet (`https://dotnet.myget.org/F/nuget-beta/vsix/`) dla programu Visual Studio 2015 nie jest już używana.</span><span class="sxs-lookup"><span data-stu-id="17148-186">Note that the previous NuGet Beta Channel (`https://dotnet.myget.org/F/nuget-beta/vsix/`) for Visual Studio 2015 is no longer used.</span></span>

<span data-ttu-id="17148-187">Zgłaszanie problemów z dowolną wersją systemu NuGet lub Podziel się pomysłami, należy otworzyć na problemu [repozytorium NuGet GitHub](https://github.com/Nuget/Home).</span><span class="sxs-lookup"><span data-stu-id="17148-187">To report problems with any release of NuGet or to share ideas, open an issue on the [NuGet GitHub repository](https://github.com/Nuget/Home).</span></span>

### <a name="related-topics"></a><span data-ttu-id="17148-188">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="17148-188">Related topics</span></span>

- [<span data-ttu-id="17148-189">Informacje o interfejsie użytkownika Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="17148-189">Package Manager UI reference</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="17148-190">Odwołanie do konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="17148-190">Package Manager Console reference</span></span>](../tools/package-manager-console.md)
- [<span data-ttu-id="17148-191">Dokumentacja programu PowerShell konsoli Menedżera pakietów</span><span class="sxs-lookup"><span data-stu-id="17148-191">Package Manager Console PowerShell reference</span></span>](../tools/powershell-reference.md)