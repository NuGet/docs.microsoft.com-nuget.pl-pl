---
title: Określ format projektu
description: Opisuje sposób identyfikacji formatu projektu
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488480"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="4be23-103">Określ format projektu</span><span class="sxs-lookup"><span data-stu-id="4be23-103">Identify the project format</span></span>

<span data-ttu-id="4be23-104">Pakiet NuGet współpracuje ze wszystkimi projektami .NET.</span><span class="sxs-lookup"><span data-stu-id="4be23-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="4be23-105">Jednak format projektu (zestaw SDK lub styl inny niż zestaw SDK) określa niektóre narzędzia i metody, które są potrzebne do korzystania z pakietów NuGet i ich tworzenia.</span><span class="sxs-lookup"><span data-stu-id="4be23-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="4be23-106">Projekty w stylu zestawu SDK używają [atrybutu SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="4be23-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="4be23-107">Ważne jest, aby zidentyfikować typ projektu, ponieważ metody i narzędzia używane do użycia i tworzenia pakietów NuGet są zależne od formatu projektu.</span><span class="sxs-lookup"><span data-stu-id="4be23-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="4be23-108">W przypadku projektów typu non-SDK metody i narzędzia są również zależne od tego, czy projekt został zmigrowany do `PackageReference` formatu.</span><span class="sxs-lookup"><span data-stu-id="4be23-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="4be23-109">Czy projekt jest w stylu zestawu SDK, czy nie zależy od metody użytej do utworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="4be23-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="4be23-110">W poniższej tabeli przedstawiono domyślny format projektu i skojarzone narzędzie interfejsu wiersza polecenia dla projektu podczas jego tworzenia przy użyciu programu Visual Studio 2017 i jego nowszych wersji.</span><span class="sxs-lookup"><span data-stu-id="4be23-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="4be23-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="4be23-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="4be23-112">Domyślny format projektu</span><span class="sxs-lookup"><span data-stu-id="4be23-112">Default project format</span></span> | <span data-ttu-id="4be23-113">Narzędzie interfejsu wiersza polecenia&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="4be23-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="4be23-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4be23-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="4be23-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="4be23-115">.NET Standard</span></span> | <span data-ttu-id="4be23-116">SDK-style</span><span class="sxs-lookup"><span data-stu-id="4be23-116">SDK-style</span></span> | [<span data-ttu-id="4be23-117">Interfejs wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="4be23-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="4be23-118">Projekty utworzone przed Visual Studio 2017 są w stylu innym niż zestaw SDK.</span><span class="sxs-lookup"><span data-stu-id="4be23-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="4be23-119">Użyj `nuget.exe` interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="4be23-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="4be23-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="4be23-120">.NET Core</span></span> | <span data-ttu-id="4be23-121">SDK-style</span><span class="sxs-lookup"><span data-stu-id="4be23-121">SDK-style</span></span> | [<span data-ttu-id="4be23-122">Interfejs wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="4be23-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="4be23-123">Projekty utworzone przed Visual Studio 2017 są w stylu innym niż zestaw SDK.</span><span class="sxs-lookup"><span data-stu-id="4be23-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="4be23-124">Użyj `nuget.exe` interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="4be23-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="4be23-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4be23-125">.NET Framework</span></span> | <span data-ttu-id="4be23-126">Non-SDK-style</span><span class="sxs-lookup"><span data-stu-id="4be23-126">Non-SDK-style</span></span> | [<span data-ttu-id="4be23-127">Interfejs wiersza polecenia nuget.exe</span><span class="sxs-lookup"><span data-stu-id="4be23-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="4be23-128">Projekty .NET Framework utworzone przy użyciu innych metod mogą być projektami w stylu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="4be23-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="4be23-129">W tym celu należy użyć [interfejsu wiersza polecenia dotnet](../install-nuget-client-tools.md#dotnetexe-cli) .</span><span class="sxs-lookup"><span data-stu-id="4be23-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="4be23-130">[Migrowany](../consume-packages/migrate-packages-config-to-package-reference.md) projekt .NET</span><span class="sxs-lookup"><span data-stu-id="4be23-130">[Migrated](../consume-packages/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="4be23-131">Non-SDK-style</span><span class="sxs-lookup"><span data-stu-id="4be23-131">Non-SDK-style</span></span>| <span data-ttu-id="4be23-132">Aby utworzyć pakiety, użyj programu [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) do tworzenia pakietów.</span><span class="sxs-lookup"><span data-stu-id="4be23-132">To create packages, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="4be23-133">Zalecane `msbuild -t:pack` jest utworzenie pakietów.</span><span class="sxs-lookup"><span data-stu-id="4be23-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="4be23-134">W przeciwnym razie użyj [interfejsu wiersza polecenia dotnet](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="4be23-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="4be23-135">Zmigrowane projekty nie są projektami w stylu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="4be23-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="4be23-136">Sprawdź format projektu</span><span class="sxs-lookup"><span data-stu-id="4be23-136">Check the project format</span></span>

<span data-ttu-id="4be23-137">Jeśli nie masz pewności, czy projekt jest w formacie stylu zestawu SDK, poszukaj atrybutu SDK w `<Project>` elemencie w pliku projektu (dla C#, jest to plik \*. csproj).</span><span class="sxs-lookup"><span data-stu-id="4be23-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="4be23-138">Jeśli jest obecny, projekt jest projektem w stylu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="4be23-138">If it is present, the project is an SDK-style project.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="4be23-139">Sprawdź format projektu w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4be23-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="4be23-140">Jeśli pracujesz w programie Visual Studio, możesz szybko sprawdzić format projektu przy użyciu jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="4be23-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="4be23-141">Kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań i wybierz polecenie **Edytuj projektname. csproj**.</span><span class="sxs-lookup"><span data-stu-id="4be23-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="4be23-142">Ta opcja jest dostępna tylko w programie Visual Studio 2017 dla projektów, które używają atrybutu stylu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="4be23-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="4be23-143">W przeciwnym razie użyj innej metody.</span><span class="sxs-lookup"><span data-stu-id="4be23-143">Otherwise, use the other method.</span></span>

   ![Edytuj plik projektu](media/edit-project-file.png)

   <span data-ttu-id="4be23-145">Projekt w stylu zestawu SDK pokazuje [atrybut zestawu SDK](/dotnet/core/tools/csproj#additions) w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="4be23-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="4be23-146">W menu **projekt** wybierz polecenie **Zwolnij projekt** (lub kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zwolnij projekt**).</span><span class="sxs-lookup"><span data-stu-id="4be23-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="4be23-147">Ten projekt nie zawiera atrybutu SDK w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="4be23-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="4be23-148">Nie jest to projekt w stylu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="4be23-148">It is not an SDK-style project.</span></span>

   ![Zwolnij projekt](media/unload-project.png)

   <span data-ttu-id="4be23-150">Następnie kliknij prawym przyciskiem myszy niezaładowanego projektu i wybierz polecenie **Edytuj projektname. csproj**.</span><span class="sxs-lookup"><span data-stu-id="4be23-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="4be23-151">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="4be23-151">See also</span></span>

- [<span data-ttu-id="4be23-152">Tworzenie pakietów .NET Standard za pomocą interfejsu wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="4be23-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="4be23-153">Tworzenie pakietów .NET Standard za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4be23-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="4be23-154">Tworzenie i publikowanie pakietu .NET Framework (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4be23-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="4be23-155">Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="4be23-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
