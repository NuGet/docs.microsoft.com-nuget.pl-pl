---
title: Tworzenie i publikowanie pakietu NuGet przy użyciu programu Visual Studio w systemie Windows
description: Samouczek instruktażowy dotyczący tworzenia i publikowania pakietu .NET Standard NuGet przy użyciu programu Visual Studio w systemie Windows.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 949c49d77ef088f802bdbd9c681f7df41d9a4c67
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342553"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="f7cc2-103">Szybki start: Tworzenie i publikowanie pakietu NuGet przy użyciu programu Visual Studio (.NET Standard, tylko w systemie Windows)</span><span class="sxs-lookup"><span data-stu-id="f7cc2-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="f7cc2-104">Jest to prosty proces tworzenia pakietu NuGet z biblioteki klas .NET Standard w programie Visual Studio w systemie Windows, a następnie opublikowania jej w celu nuget.org za pomocą narzędzia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="f7cc2-105">Jeśli używasz Visual Studio dla komputerów Mac, zapoznaj się z [informacjami](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) na temat tworzenia pakietu NuGet lub Użyj [narzędzi interfejsu wiersza polecenia dotnet](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f7cc2-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7cc2-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f7cc2-106">Prerequisites</span></span>

1. <span data-ttu-id="f7cc2-107">Zainstaluj dowolną wersję programu Visual Studio 2017 lub nowszą z [VisualStudio.com](https://www.visualstudio.com/) . Obciążenie związane z usługą SIECIową.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-107">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="f7cc2-108">Program Visual Studio 2017 lub nowszy automatycznie uwzględnia funkcje NuGet podczas instalacji obciążenia .NET.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-108">Visual Studio 2017 and higher automatically include NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="f7cc2-109">`dotnet` Zainstaluj interfejs wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-109">Install the `dotnet` CLI.</span></span>

   <span data-ttu-id="f7cc2-110">W przypadku `dotnet` interfejsu wiersza polecenia, rozpoczynając od programu Visual Studio 2017, interfejs wiersza polecenia jest automatycznie instalowany z dowolnymi obciążeniami związanymi z platformą .NET Core. `dotnet`</span><span class="sxs-lookup"><span data-stu-id="f7cc2-110">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="f7cc2-111">W przeciwnym razie zainstaluj [zestaw .NET Core SDK](https://www.microsoft.com/net/download/) , aby uzyskać `dotnet` interfejs wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-111">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="f7cc2-112">Interfejs wiersza polecenia jest wymagany dla projektów .NET Standard, które używają [formatu stylu zestawu SDK](../resources/check-project-format.md) (atrybut zestawu SDK). `dotnet`</span><span class="sxs-lookup"><span data-stu-id="f7cc2-112">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="f7cc2-113">Domyślny szablon biblioteki klas w programie Visual Studio 2017 lub nowszym, który jest używany w tym artykule, używa atrybutu SDK.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-113">The default class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="f7cc2-114">W tym artykule `dotnet` zaleca się używanie interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-114">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="f7cc2-115">Chociaż można opublikować dowolny pakiet NuGet przy użyciu `nuget.exe` interfejsu wiersza polecenia, niektóre kroki opisane w tym artykule są specyficzne dla projektów w stylu zestawu SDK i interfejsu wiersza polecenia dotnet.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-115">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="f7cc2-116">Interfejs wiersza polecenia NuGet. exe jest używany dla [projektów typu non-SDK](../resources/check-project-format.md) (zwykle .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="f7cc2-116">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span> <span data-ttu-id="f7cc2-117">Jeśli pracujesz z projektem w stylu innym niż zestaw SDK, postępuj zgodnie z procedurami w temacie [Tworzenie i publikowanie pakietu .NET Framework (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) , aby utworzyć i opublikować pakiet.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-117">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package.</span></span>

1. <span data-ttu-id="f7cc2-118">[Zarejestruj się, aby korzystać z bezpłatnego konta w usłudze NuGet.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) , jeśli jeszcze go nie masz.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-118">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="f7cc2-119">Utworzenie nowego konta spowoduje wysłanie wiadomości e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-119">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="f7cc2-120">Musisz potwierdzić konto, aby można było przekazać pakiet.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-120">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="f7cc2-121">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="f7cc2-121">Create a class library project</span></span>

<span data-ttu-id="f7cc2-122">Można użyć istniejącego projektu biblioteki klas .NET Standard dla kodu, który ma zostać spakowany, lub utworzyć prosty jeden w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f7cc2-122">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="f7cc2-123">W programie Visual Studio wybierz pozycję **plik > nowy > projekt**, rozwiń **węzeł C# .NET standard > wizualizacji** , wybierz szablon "Biblioteka klas (.NET standard)", nazwij projekt AppLogger i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-123">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="f7cc2-124">Kliknij prawym przyciskiem myszy plik projektu powstały i wybierz pozycję **kompilacja** , aby upewnić się, że projekt został utworzony prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-124">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="f7cc2-125">Biblioteka DLL znajduje się w folderze debugowania (lub zwolnij, jeśli zostanie utworzona ta konfiguracja).</span><span class="sxs-lookup"><span data-stu-id="f7cc2-125">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="f7cc2-126">Oczywiście w rzeczywistym pakiecie NuGet zaimplementowano wiele przydatnych funkcji, z którymi inne mogą tworzyć aplikacje.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-126">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="f7cc2-127">W tym instruktażu nie można jednak napisać żadnego dodatkowego kodu, ponieważ biblioteka klas z szablonu jest wystarczająca do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-127">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="f7cc2-128">Nadal, jeśli chcesz, aby w pakiecie był jakiś kod funkcjonalny, użyj następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="f7cc2-128">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> <span data-ttu-id="f7cc2-129">O ile nie istnieje powód, aby wybrać inny sposób, .NET Standard jest preferowanym celem dla pakietów NuGet, ponieważ zapewnia zgodność z najszerszym zakresem zużywanych projektów.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-129">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="f7cc2-130">Konfigurowanie właściwości pakietu</span><span class="sxs-lookup"><span data-stu-id="f7cc2-130">Configure package properties</span></span>

1. <span data-ttu-id="f7cc2-131">Kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań i wybierz polecenie **Właściwości** menu, a następnie wybierz kartę **pakiet** .</span><span class="sxs-lookup"><span data-stu-id="f7cc2-131">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="f7cc2-132">Karta **pakiet** jest wyświetlana tylko dla projektów w stylu zestawu SDK w programie Visual Studio, zwykle .NET Standard lub projektów biblioteki klas platformy .NET Core; Jeśli obiektem docelowym jest projekt o stylu innym niż zestaw SDK (zwykle .NET Framework), należy [przeprowadzić migrację projektu](../reference/migrate-packages-config-to-package-reference.md) i użyć `dotnet` interfejsu wiersza polecenia lub zobaczyć [Tworzenie i publikowanie pakietu .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) lub zobaczyć [, jak utworzyć i opublikować pakiet .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) Zamiast tego instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-132">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Właściwości pakietu NuGet w projekcie programu Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="f7cc2-134">W przypadku pakietów przeznaczonych do użycia publicznego należy zwrócić szczególną uwagę na właściwości **Tagi** , ponieważ Tagi ułatwiają innym znalezienie pakietu i zrozumienie jego działania.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-134">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="f7cc2-135">Nadaj pakietowi unikatowy identyfikator i Wypełnij wszystkie inne żądane właściwości.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-135">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="f7cc2-136">Opis różnych właściwości można znaleźć w [dokumentacji pliku. nuspec](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="f7cc2-136">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="f7cc2-137">Wszystkie właściwości w tym miejscu należy `.nuspec` do manifestu, który program Visual Studio tworzy dla projektu.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-137">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="f7cc2-138">Należy nadać pakietowi identyfikator, który jest unikatowy w obrębie nuget.org lub dowolnego hosta, który jest używany.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-138">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="f7cc2-139">W tym instruktażu Zalecamy uwzględnienie "przykładowego" lub "testowego" w nazwie, jak w późniejszym kroku publikowania sprawia, że pakiet jest widoczny publicznie (chociaż prawdopodobnie nikt się nie używa).</span><span class="sxs-lookup"><span data-stu-id="f7cc2-139">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="f7cc2-140">Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-140">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="f7cc2-141">Opcjonalne: Aby wyświetlić właściwości bezpośrednio w pliku projektu, kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań i wybierz polecenie **Edytuj AppLogger. csproj**.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-141">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="f7cc2-142">Ta opcja jest dostępna tylko w programie Visual Studio 2017 dla projektów, które używają atrybutu stylu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="f7cc2-143">W przeciwnym razie kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zwolnij projekt**.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-143">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="f7cc2-144">Następnie kliknij prawym przyciskiem myszy niezaładowanego projektu i wybierz polecenie **Edytuj AppLogger. csproj**.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-144">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="f7cc2-145">Uruchom pakiet polecenie</span><span class="sxs-lookup"><span data-stu-id="f7cc2-145">Run the pack command</span></span>

1. <span data-ttu-id="f7cc2-146">Skonfiguruj konfigurację do **wydania**.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-146">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="f7cc2-147">Kliknij prawym przyciskiem myszy projekt w **Eksplorator rozwiązań** i wybierz polecenie **pakiet** :</span><span class="sxs-lookup"><span data-stu-id="f7cc2-147">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Polecenie pakietu NuGet w menu kontekstowym projektu programu Visual Studio](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="f7cc2-149">Jeśli nie widzisz polecenia **Pack** , projekt prawdopodobnie nie jest projektem w `nuget.exe` stylu zestawu SDK i musisz użyć interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-149">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="f7cc2-150">Aby uzyskać instrukcje krok po kroku `dotnet` , należy [przeprowadzić migrację projektu](../reference/migrate-packages-config-to-package-reference.md) i użyć interfejsu wiersza polecenia lub zobaczyć, [jak utworzyć i opublikować pakiet .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) .</span><span class="sxs-lookup"><span data-stu-id="f7cc2-150">Either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="f7cc2-151">Program Visual Studio kompiluje projekt i tworzy `.nupkg` plik.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-151">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="f7cc2-152">Przejrzyj okno **dane wyjściowe** , aby uzyskać szczegółowe informacje (podobne do następujących), które zawiera ścieżkę do pliku pakietu.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-152">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="f7cc2-153">Należy również pamiętać, że skompilowany zestaw jest `bin\Release\netstandard2.0` w befits .NET Standard 2,0.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-153">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="f7cc2-154">Opcja alternatywna: pakiet z programem MSBuild</span><span class="sxs-lookup"><span data-stu-id="f7cc2-154">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="f7cc2-155">Jako alternatywa dla użycia polecenia menu **pakiet** NuGet 4. x + i MSBuild 15.1 + obsługuje `pack` obiekt docelowy, gdy projekt zawiera niezbędne dane pakietu.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-155">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="f7cc2-156">Otwórz wiersz polecenia, przejdź do folderu projektu i uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-156">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="f7cc2-157">(Zazwyczaj chcesz uruchomić "wiersz polecenia dla deweloperów dla programu Visual Studio" z menu Start, ponieważ zostanie on skonfigurowany ze wszystkimi niezbędnymi ścieżkami dla programu MSBuild).</span><span class="sxs-lookup"><span data-stu-id="f7cc2-157">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="f7cc2-158">Pakiet można następnie znaleźć w `bin\Release` folderze.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-158">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="f7cc2-159">Aby uzyskać dodatkowe opcje `msbuild -t:pack`w programie, zobacz [pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="f7cc2-159">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="f7cc2-160">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="f7cc2-160">Publish the package</span></span>

<span data-ttu-id="f7cc2-161">`nuget.exe` `dotnet.exe` Po utworzeniu `.nupkg` pliku opublikuj go w usłudze NuGet.org przy użyciu interfejsu wiersza polecenia lub interfejsu wiersza polecenia oraz klucza API uzyskanego z NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-161">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="f7cc2-162">Pozyskiwanie klucza interfejsu API</span><span class="sxs-lookup"><span data-stu-id="f7cc2-162">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="f7cc2-163">Publikowanie przy użyciu wypychania NuGet programu dotnet (interfejs wiersza polecenia dotnet)</span><span class="sxs-lookup"><span data-stu-id="f7cc2-163">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="f7cc2-164">Ten krok jest zalecaną alternatywą dla `nuget.exe`korzystania z programu.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-164">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="f7cc2-165">Przed opublikowaniem pakietu należy najpierw otworzyć wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-165">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="f7cc2-166">Publikowanie przy użyciu wypychania NuGet (interfejs wiersza polecenia NuGet. exe)</span><span class="sxs-lookup"><span data-stu-id="f7cc2-166">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="f7cc2-167">Ten krok jest alternatywą dla korzystania `dotnet.exe`z programu.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-167">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="f7cc2-168">Otwórz wiersz polecenia i przejdź do folderu zawierającego `.nupkg` plik.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-168">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="f7cc2-169">Uruchom następujące polecenie, określając nazwę pakietu (unikatowy identyfikator pakietu) i zastępując kluczową wartość kluczem interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="f7cc2-169">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="f7cc2-170">NuGet. exe wyświetla wyniki procesu publikowania:</span><span class="sxs-lookup"><span data-stu-id="f7cc2-170">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="f7cc2-171">Zobacz [wypychanie NuGet](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="f7cc2-171">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="f7cc2-172">Błędy publikowania</span><span class="sxs-lookup"><span data-stu-id="f7cc2-172">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="f7cc2-173">Zarządzanie opublikowanym pakietem</span><span class="sxs-lookup"><span data-stu-id="f7cc2-173">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="f7cc2-174">Dodawanie pliku Readme i innych plików</span><span class="sxs-lookup"><span data-stu-id="f7cc2-174">Adding a readme and other files</span></span>

<span data-ttu-id="f7cc2-175">Aby bezpośrednio określić pliki do dołączenia do pakietu, należy edytować plik projektu i użyć `content` właściwości:</span><span class="sxs-lookup"><span data-stu-id="f7cc2-175">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="f7cc2-176">Będzie to zawierać plik o nazwie `readme.txt` w katalogu głównym pakietu.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-176">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="f7cc2-177">Program Visual Studio Wyświetla zawartość tego pliku jako zwykły tekst bezpośrednio po zainstalowaniu pakietu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-177">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="f7cc2-178">(Pliki Readme nie są wyświetlane dla pakietów zainstalowanych jako zależności).</span><span class="sxs-lookup"><span data-stu-id="f7cc2-178">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="f7cc2-179">Na przykład poniżej przedstawiono sposób wyświetlania pliku Readme dla pakietu HtmlAgilityPack:</span><span class="sxs-lookup"><span data-stu-id="f7cc2-179">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Wyświetlanie pliku Readme dla pakietu NuGet podczas instalacji](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="f7cc2-181">Jedynie dodanie pliku Readme. txt w katalogu głównym projektu nie spowoduje uwzględnienia go w pakiecie wynikowym.</span><span class="sxs-lookup"><span data-stu-id="f7cc2-181">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="f7cc2-182">Tematy pokrewne</span><span class="sxs-lookup"><span data-stu-id="f7cc2-182">Related topics</span></span>

- [<span data-ttu-id="f7cc2-183">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="f7cc2-183">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="f7cc2-184">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="f7cc2-184">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="f7cc2-185">Pakiety wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="f7cc2-185">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="f7cc2-186">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="f7cc2-186">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="f7cc2-187">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="f7cc2-187">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="f7cc2-188">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="f7cc2-188">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="f7cc2-189">Dokumentacja biblioteki .NET Standard</span><span class="sxs-lookup"><span data-stu-id="f7cc2-189">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="f7cc2-190">Przenoszenie do programu .NET Core z .NET Framework</span><span class="sxs-lookup"><span data-stu-id="f7cc2-190">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
