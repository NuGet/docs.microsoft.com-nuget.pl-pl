---
title: Tworzenie i publikowanie standardowego pakietu NuGet platformy .NET — visual studio w systemie Windows
description: Samouczek instruktażowy dotyczący tworzenia i publikowania pakietu NuGet standard .NET przy użyciu programu Visual Studio w systemie Windows.
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 32dcc1d233154463e2950b1ce46554b1cb89956e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429032"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="2187c-103">Szybki start: tworzenie i publikowanie pakietu NuGet przy użyciu programu Visual Studio (.NET Standard, tylko system Windows)</span><span class="sxs-lookup"><span data-stu-id="2187c-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="2187c-104">Jest to prosty proces, aby utworzyć pakiet NuGet z biblioteki klas standardowych platformy .NET w programie Visual Studio w systemie Windows, a następnie opublikować go do nuget.org przy użyciu narzędzia interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2187c-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="2187c-105">Jeśli używasz programu Visual Studio dla komputerów Mac, zapoznaj się z [tymi informacjami](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) dotyczącymi tworzenia pakietu NuGet lub użyj [narzędzi dotnet CLI.](create-and-publish-a-package-using-the-dotnet-cli.md)</span><span class="sxs-lookup"><span data-stu-id="2187c-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2187c-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2187c-106">Prerequisites</span></span>

1. <span data-ttu-id="2187c-107">Zainstaluj dowolną wersję programu Visual Studio 2019 z [visualstudio.com](https://www.visualstudio.com/) z obciążeniem związanym z rdzeniem .NET.</span><span class="sxs-lookup"><span data-stu-id="2187c-107">Install any edition of Visual Studio 2019 from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="2187c-108">Jeśli nie jest jeszcze zainstalowany, `dotnet` zainstaluj cli.</span><span class="sxs-lookup"><span data-stu-id="2187c-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="2187c-109">W `dotnet` przypadku interfejsu wiersza polecenia, począwszy `dotnet` od programu Visual Studio 2017, interfejsu wiersza polecenia jest automatycznie instalowany z dowolnymi obciążeniami powiązanymi z rdzeniem .NET.</span><span class="sxs-lookup"><span data-stu-id="2187c-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="2187c-110">W przeciwnym razie zainstaluj [pakiet SDK rdzenia .NET,](https://www.microsoft.com/net/download/) aby uzyskać `dotnet` plik CLI.</span><span class="sxs-lookup"><span data-stu-id="2187c-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="2187c-111">Cli `dotnet` jest wymagane dla projektów .NET Standard, które używają [formatu SDK stylu](../resources/check-project-format.md) (atrybut SDK).</span><span class="sxs-lookup"><span data-stu-id="2187c-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="2187c-112">Domyślny szablon biblioteki klas .NET Standard w programie Visual Studio 2017 i nowszym, który jest używany w tym artykule, używa atrybutu SDK.</span><span class="sxs-lookup"><span data-stu-id="2187c-112">The default .NET Standard class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="2187c-113">Jeśli pracujesz z projektem w stylu nie-SDK, postępuj zgodnie z procedurami w [Tworzenie i publikowanie pakietu .NET Framework (Visual Studio),](create-and-publish-a-package-using-visual-studio-net-framework.md) aby zamiast tego utworzyć i opublikować pakiet.</span><span class="sxs-lookup"><span data-stu-id="2187c-113">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package instead.</span></span> <span data-ttu-id="2187c-114">W tym artykule zaleca się `dotnet` wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2187c-114">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="2187c-115">Chociaż można opublikować dowolny pakiet `nuget.exe` NuGet przy użyciu interfejsu wiersza polecenia, niektóre kroki w tym artykule są specyficzne dla projektów w stylu zestawu SDK i interfejsu wiersza polecenia dotnet.</span><span class="sxs-lookup"><span data-stu-id="2187c-115">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="2187c-116">Nuget.exe CLI jest używany dla [projektów w stylu innych niż SDK](../resources/check-project-format.md) (zazwyczaj .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="2187c-116">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span>

1. <span data-ttu-id="2187c-117">[Zarejestruj się na darmowe konto w nuget.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) jeśli jeszcze go nie masz.</span><span class="sxs-lookup"><span data-stu-id="2187c-117">[Register for a free account on nuget.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="2187c-118">Utworzenie nowego konta wysyła wiadomość e-mail z potwierdzeniem.</span><span class="sxs-lookup"><span data-stu-id="2187c-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="2187c-119">Musisz potwierdzić konto, zanim będzie można przesłać pakiet.</span><span class="sxs-lookup"><span data-stu-id="2187c-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="2187c-120">Tworzenie projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="2187c-120">Create a class library project</span></span>

<span data-ttu-id="2187c-121">Można użyć istniejącego projektu biblioteki klas standardowych platformy .NET dla kodu, który chcesz spakować, lub utworzyć prosty w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2187c-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="2187c-122">W programie Visual Studio wybierz polecenie **Plik > nowy projekt >**, rozwiń węzeł Visual **C# > .NET Standard,** wybierz szablon "Biblioteka klas (.NET Standard)" , nazwij projekt AppLogger i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2187c-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

   > [!Tip]
   > <span data-ttu-id="2187c-123">Jeśli nie masz powodu, aby wybrać inaczej, .NET Standard jest preferowanym obiektem docelowym dla pakietów NuGet, ponieważ zapewnia zgodność z najszerszym zakresem projektów zużywających.</span><span class="sxs-lookup"><span data-stu-id="2187c-123">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

1. <span data-ttu-id="2187c-124">Kliknij prawym przyciskiem myszy wynikowy plik projektu i wybierz **polecenie Build,** aby upewnić się, że projekt został prawidłowo utworzony.</span><span class="sxs-lookup"><span data-stu-id="2187c-124">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="2187c-125">Biblioteka DLL znajduje się w folderze debugowania (lub Release, jeśli zamiast tego skompilujesz tę konfigurację).</span><span class="sxs-lookup"><span data-stu-id="2187c-125">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="2187c-126">W ramach prawdziwego pakietu NuGet, oczywiście, można zaimplementować wiele przydatnych funkcji, za pomocą których inni mogą tworzyć aplikacje.</span><span class="sxs-lookup"><span data-stu-id="2187c-126">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="2187c-127">W tym instruktażu jednak nie będzie pisać żadnego dodatkowego kodu, ponieważ biblioteka klas z szablonu jest wystarczająca do utworzenia pakietu.</span><span class="sxs-lookup"><span data-stu-id="2187c-127">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="2187c-128">Mimo to, jeśli chcesz jakiś kod funkcjonalny dla pakietu, użyj następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="2187c-128">Still, if you'd like some functional code for the package, use the following:</span></span>

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

## <a name="configure-package-properties"></a><span data-ttu-id="2187c-129">Konfigurowanie właściwości pakietu</span><span class="sxs-lookup"><span data-stu-id="2187c-129">Configure package properties</span></span>

1. <span data-ttu-id="2187c-130">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań, a następnie wybierz polecenie menu **Właściwości,** a następnie wybierz kartę **Pakiet.**</span><span class="sxs-lookup"><span data-stu-id="2187c-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="2187c-131">Karta **Pakiet** jest wyświetlana tylko dla projektów w stylu zestawu SDK w programie Visual Studio, zazwyczaj w projektach biblioteki klas .NET Standard lub .NET Core; jeśli są przeznaczone dla projektu w stylu innego niż SDK (zazwyczaj .NET Framework), albo [migracji projektu](../consume-packages/migrate-packages-config-to-package-reference.md) lub zobacz Tworzenie [i publikowanie pakietu .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) zamiast instrukcji krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="2187c-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Właściwości pakietu NuGet w projekcie programu Visual Studio](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="2187c-133">W przypadku pakietów przeznaczonych do użytku publicznego należy zwrócić szczególną uwagę na właściwość **Tagi,** ponieważ tagi pomagają innym znaleźć pakiet i zrozumieć, co robi.</span><span class="sxs-lookup"><span data-stu-id="2187c-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="2187c-134">Nadaj pakietowi unikatowy identyfikator i wypełnij inne żądane właściwości.</span><span class="sxs-lookup"><span data-stu-id="2187c-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="2187c-135">Aby uzyskać mapowanie właściwości MSBuild (projekt w stylu zestawu SDK) do właściwości w *.nuspec*, zobacz [pack targets](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="2187c-135">For a mapping of MSBuild properties (SDK-style project) to properties in a *.nuspec*, see [pack targets](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="2187c-136">Opisy właściwości można znaleźć w [pliku .nuspec .](../reference/nuspec.md)</span><span class="sxs-lookup"><span data-stu-id="2187c-136">For descriptions of properties, see the [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="2187c-137">Wszystkie właściwości w tym miejscu `.nuspec` przejść do manifestu, który visual studio tworzy dla projektu.</span><span class="sxs-lookup"><span data-stu-id="2187c-137">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="2187c-138">Należy nadać pakietowi identyfikator, który jest unikatowy w nuget.org lub niezależnie od hosta, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="2187c-138">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="2187c-139">W tym instruktażu zalecamy dołączenie "Przykład" lub "Test" w nazwie, ponieważ późniejszy krok publikowania powoduje, że pakiet jest publicznie widoczny (choć jest mało prawdopodobne, aby ktoś go faktycznie używał).</span><span class="sxs-lookup"><span data-stu-id="2187c-139">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="2187c-140">Jeśli spróbujesz opublikować pakiet o nazwie, która już istnieje, zostanie wyświetlony błąd.</span><span class="sxs-lookup"><span data-stu-id="2187c-140">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="2187c-141">(Opcjonalnie) Aby wyświetlić właściwości bezpośrednio w pliku projektu, kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz polecenie **Edytuj plik AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="2187c-141">(Optional) To see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="2187c-142">Ta opcja jest dostępna tylko od programu Visual Studio 2017 dla projektów korzystających z atrybutu w stylu SDK.</span><span class="sxs-lookup"><span data-stu-id="2187c-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="2187c-143">W przeciwnym razie kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zwolnij projekt**.</span><span class="sxs-lookup"><span data-stu-id="2187c-143">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="2187c-144">Następnie kliknij prawym przyciskiem myszy niezaładowany projekt i wybierz polecenie **Edytuj plik AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="2187c-144">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="2187c-145">Uruchamianie polecenia pack</span><span class="sxs-lookup"><span data-stu-id="2187c-145">Run the pack command</span></span>

1. <span data-ttu-id="2187c-146">Ustaw konfigurację na **Zwolnij**.</span><span class="sxs-lookup"><span data-stu-id="2187c-146">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="2187c-147">Kliknij prawym przyciskiem myszy projekt w **Eksploratorze rozwiązań** i wybierz polecenie **Pack:**</span><span class="sxs-lookup"><span data-stu-id="2187c-147">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Polecenie NuGet pack w menu kontekstowym projektu programu Visual Studio](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="2187c-149">Jeśli nie widzisz polecenia **Pack,** projekt prawdopodobnie nie jest projektem w stylu zestawu `nuget.exe` SDK i musisz użyć interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2187c-149">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="2187c-150">Migracji [projektu](../consume-packages/migrate-packages-config-to-package-reference.md) i użyj `dotnet` interfejsu wiersza polecenia lub zobacz Tworzenie i [publikowanie pakietu .NET Framework](create-and-publish-a-package-using-visual-studio-net-framework.md) zamiast instrukcji krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="2187c-150">Either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="2187c-151">Visual Studio tworzy projekt i `.nupkg` tworzy plik.</span><span class="sxs-lookup"><span data-stu-id="2187c-151">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="2187c-152">Sprawdź **dane wyjściowe,** aby uzyskać szczegółowe informacje (podobne do poniższych), który zawiera ścieżkę do pliku pakietu.</span><span class="sxs-lookup"><span data-stu-id="2187c-152">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="2187c-153">Należy również zauważyć, że `bin\Release\netstandard2.0` zestaw zbudowany jest w jak przystało na .NET Standard 2.0 cel.</span><span class="sxs-lookup"><span data-stu-id="2187c-153">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a><span data-ttu-id="2187c-154">(Opcjonalnie) Generowanie pakietu na kompilacji</span><span class="sxs-lookup"><span data-stu-id="2187c-154">(Optional) Generate package on build</span></span>

<span data-ttu-id="2187c-155">Program Visual Studio można skonfigurować do automatycznego generowania pakietu NuGet podczas tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="2187c-155">You can configure Visual Studio to automatically generate the NuGet package when you build the project.</span></span>

1. <span data-ttu-id="2187c-156">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="2187c-156">In Solution Explorer, right-click the project and choose **Properties**.</span></span>

2. <span data-ttu-id="2187c-157">Na karcie **Pakiet** wybierz pozycję **Generuj pakiet NuGet na kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="2187c-157">In the **Package** tab, select **Generate NuGet package on build**.</span></span>

   ![Automatyczne generowanie pakietu na kompilacji](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> <span data-ttu-id="2187c-159">Po automatycznym wygenerowaniu pakietu czas do spakowania zwiększa czas kompilacji dla projektu.</span><span class="sxs-lookup"><span data-stu-id="2187c-159">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="optional-pack-with-msbuild"></a><span data-ttu-id="2187c-160">(Opcjonalnie) opakowanie z MSBuild</span><span class="sxs-lookup"><span data-stu-id="2187c-160">(Optional) pack with MSBuild</span></span>

<span data-ttu-id="2187c-161">Jako alternatywa przy użyciu polecenia menu **Pack,** NuGet 4.x+ i MSBuild `pack` 15.1+ obsługuje miejsce docelowe, gdy projekt zawiera niezbędne dane pakietu.</span><span class="sxs-lookup"><span data-stu-id="2187c-161">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="2187c-162">Otwórz wiersz polecenia, przejdź do folderu projektu i uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="2187c-162">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="2187c-163">(Zazwyczaj chcesz uruchomić "Developer Command Prompt for Visual Studio" z menu Start, ponieważ zostanie skonfigurowany ze wszystkimi niezbędnymi ścieżkami dla msbuild.)</span><span class="sxs-lookup"><span data-stu-id="2187c-163">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

<span data-ttu-id="2187c-164">Aby uzyskać więcej informacji, zobacz [Tworzenie pakietu przy użyciu programu MSBuild](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="2187c-164">For more information, see [Create a package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="2187c-165">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="2187c-165">Publish the package</span></span>

<span data-ttu-id="2187c-166">Po opublikowaniu `.nupkg` pliku można go opublikować w celu `nuget.exe` nuget.org przy `dotnet.exe` użyciu interfejsu wiersza polecenia lub interfejsu wiersza polecenia wraz z kluczem interfejsu API uzyskanym z nuget.org.</span><span class="sxs-lookup"><span data-stu-id="2187c-166">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="2187c-167">Uzyskaj klucz interfejsu API</span><span class="sxs-lookup"><span data-stu-id="2187c-167">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a><span data-ttu-id="2187c-168">Publikowanie za pomocą interfejsu wiersza polecenia dotnet lub nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="2187c-168">Publish with the dotnet CLI or nuget.exe CLI</span></span>

<span data-ttu-id="2187c-169">Wybierz kartę dla narzędzia interfejsu wiersza polecenia, interfejsu **.NET Core CLI** (dotnet CLI) lub **NuGet** (nuget.exe CLI).</span><span class="sxs-lookup"><span data-stu-id="2187c-169">Select the tab for your CLI tool, either **.NET Core CLI** (dotnet CLI) or **NuGet** (nuget.exe CLI).</span></span>

# <a name="net-core-cli"></a>[<span data-ttu-id="2187c-170">Interfejs wiersza polecenia platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="2187c-170">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="2187c-171">Ten krok jest zalecaną `nuget.exe`alternatywą dla używania programu .</span><span class="sxs-lookup"><span data-stu-id="2187c-171">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="2187c-172">Przed opublikowaniem pakietu należy najpierw otworzyć wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="2187c-172">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[<span data-ttu-id="2187c-173">Nuget</span><span class="sxs-lookup"><span data-stu-id="2187c-173">NuGet</span></span>](#tab/nuget)

<span data-ttu-id="2187c-174">Ten krok jest alternatywą dla korzystania z programu `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="2187c-174">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="2187c-175">Otwórz wiersz polecenia i zmień folder `.nupkg` zawierający plik.</span><span class="sxs-lookup"><span data-stu-id="2187c-175">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="2187c-176">Uruchom następujące polecenie, określając nazwę pakietu (unikatowy identyfikator pakietu) i zastępując wartość klucza kluczem interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="2187c-176">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="2187c-177">nuget.exe wyświetla wyniki procesu publikowania:</span><span class="sxs-lookup"><span data-stu-id="2187c-177">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="2187c-178">Zobacz [nuget push](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="2187c-178">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

---

### <a name="publish-errors"></a><span data-ttu-id="2187c-179">Błędy publikowania</span><span class="sxs-lookup"><span data-stu-id="2187c-179">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="2187c-180">Zarządzanie opublikowanym pakietem</span><span class="sxs-lookup"><span data-stu-id="2187c-180">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="2187c-181">Dodawanie pliku readme i innych plików</span><span class="sxs-lookup"><span data-stu-id="2187c-181">Adding a readme and other files</span></span>

<span data-ttu-id="2187c-182">Aby bezpośrednio określić pliki do uwzględnienia w pakiecie, `content` edytuj plik projektu i użyj właściwości:</span><span class="sxs-lookup"><span data-stu-id="2187c-182">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="2187c-183">Będzie to obejmować `readme.txt` plik o nazwie w katalogu głównym pakietu.</span><span class="sxs-lookup"><span data-stu-id="2187c-183">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="2187c-184">Visual Studio wyświetla zawartość tego pliku jako zwykły tekst natychmiast po zainstalowaniu pakietu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="2187c-184">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="2187c-185">(Pliki Readme nie są wyświetlane dla pakietów zainstalowanych jako zależności).</span><span class="sxs-lookup"><span data-stu-id="2187c-185">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="2187c-186">Na przykład, oto jak readme dla pakietu HtmlAgilityPack pojawia się:</span><span class="sxs-lookup"><span data-stu-id="2187c-186">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Wyświetlanie pliku readme dla pakietu NuGet po instalacji](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="2187c-188">Samo dodanie pliku readme.txt w katalogu głównym projektu nie spowoduje, że zostanie on uwzględniony w pakiecie wynikowym.</span><span class="sxs-lookup"><span data-stu-id="2187c-188">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-video"></a><span data-ttu-id="2187c-189">Podobne wideo</span><span class="sxs-lookup"><span data-stu-id="2187c-189">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

<span data-ttu-id="2187c-190">Znajdź więcej filmów NuGet na [Channel 9](https://channel9.msdn.com/Series/NuGet-101) i [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span><span class="sxs-lookup"><span data-stu-id="2187c-190">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="related-topics"></a><span data-ttu-id="2187c-191">Powiązane tematy</span><span class="sxs-lookup"><span data-stu-id="2187c-191">Related topics</span></span>

- [<span data-ttu-id="2187c-192">Tworzenie pakietu</span><span class="sxs-lookup"><span data-stu-id="2187c-192">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)
- [<span data-ttu-id="2187c-193">Publikowanie pakietu</span><span class="sxs-lookup"><span data-stu-id="2187c-193">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="2187c-194">Pakiety w wersji wstępnej</span><span class="sxs-lookup"><span data-stu-id="2187c-194">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="2187c-195">Obsługa wielu platform docelowych</span><span class="sxs-lookup"><span data-stu-id="2187c-195">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="2187c-196">Przechowywanie wersji pakietów</span><span class="sxs-lookup"><span data-stu-id="2187c-196">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="2187c-197">Tworzenie zlokalizowanych pakietów</span><span class="sxs-lookup"><span data-stu-id="2187c-197">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="2187c-198">Dokumentacja biblioteki standardowej platformy .NET</span><span class="sxs-lookup"><span data-stu-id="2187c-198">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="2187c-199">Przenoszenie do rdzenia net z platformy .NET Framework</span><span class="sxs-lookup"><span data-stu-id="2187c-199">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
