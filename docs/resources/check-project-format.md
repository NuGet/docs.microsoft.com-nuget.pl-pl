---
title: Identyfikowanie formatu projektu
description: W tym artykule opisano, jak tożsamość projektu formatowania
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 3d8745ea30115a2d7f3954d171d92b75a434a55b
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843519"
---
# <a name="identify-the-project-format"></a><span data-ttu-id="aa73b-103">Identyfikowanie formatu projektu</span><span class="sxs-lookup"><span data-stu-id="aa73b-103">Identify the project format</span></span>

<span data-ttu-id="aa73b-104">NuGet współpracuje ze wszystkich projektów .NET.</span><span class="sxs-lookup"><span data-stu-id="aa73b-104">NuGet works with all .NET projects.</span></span> <span data-ttu-id="aa73b-105">Jednak formatu projektu (SDK stylu lub stylu bez zestawu SDK) określa niektóre z narzędzi i metod, które należy użyć w celu umożliwienia użycia i tworzenie pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="aa73b-105">However, the project format (SDK-style or non-SDK-style) determines some of the tools and methods that you need to use to consume and create NuGet packages.</span></span> <span data-ttu-id="aa73b-106">Użyj zestawu SDK stylu projektów [atrybutu zestawu SDK](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="aa73b-106">SDK-style projects use the [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span> <span data-ttu-id="aa73b-107">Należy zidentyfikować typu projektu, ponieważ metody i narzędzia, których używanie i tworzenie pakietów NuGet są zależne od formatu projektu.</span><span class="sxs-lookup"><span data-stu-id="aa73b-107">It is important to identify your project type because the methods and tools you use to consume and create NuGet packages are dependent on the project format.</span></span> <span data-ttu-id="aa73b-108">Dla projektów w stylu bez zestawu SDK, metody i narzędzia są również zależy od tego, czy zostały przeniesione do projektu `PackageReference` formatu.</span><span class="sxs-lookup"><span data-stu-id="aa73b-108">For non-SDK-style projects, the methods and tools are also dependent on whether or not the project has been migrated to `PackageReference` format.</span></span>

<span data-ttu-id="aa73b-109">Czy projekt jest zestaw SDK stylu lub nie zależy od metody używanej do tworzenia projektu.</span><span class="sxs-lookup"><span data-stu-id="aa73b-109">Whether your project is SDK-style or not depends on the method used to create the project.</span></span> <span data-ttu-id="aa73b-110">W poniższej tabeli przedstawiono domyślny format projektu oraz skojarzone narzędzie interfejsu wiersza polecenia dla projektu podczas tworzenia go za pomocą programu Visual Studio 2017 i nowsze wersje.</span><span class="sxs-lookup"><span data-stu-id="aa73b-110">The following table shows the default project format and the associated CLI tool for your project when you create it using Visual Studio 2017 and later versions.</span></span>

| <span data-ttu-id="aa73b-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="aa73b-111">Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="aa73b-112">Domyślny format projektu</span><span class="sxs-lookup"><span data-stu-id="aa73b-112">Default project format</span></span> | <span data-ttu-id="aa73b-113">Narzędzie interfejsu wiersza polecenia&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="aa73b-113">CLI tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="aa73b-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="aa73b-114">Notes</span></span> |
|:------------- |:-------------|:-----|:-----|
| <span data-ttu-id="aa73b-115">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="aa73b-115">.NET Standard</span></span> | <span data-ttu-id="aa73b-116">SDK-style</span><span class="sxs-lookup"><span data-stu-id="aa73b-116">SDK-style</span></span> | [<span data-ttu-id="aa73b-117">Interfejs wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="aa73b-117">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="aa73b-118">Projekty utworzone przed Visual Studio 2017 są inne niż stylu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="aa73b-118">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="aa73b-119">Użyj `nuget.exe` interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="aa73b-119">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="aa73b-120">.NET Core</span><span class="sxs-lookup"><span data-stu-id="aa73b-120">.NET Core</span></span> | <span data-ttu-id="aa73b-121">SDK-style</span><span class="sxs-lookup"><span data-stu-id="aa73b-121">SDK-style</span></span> | [<span data-ttu-id="aa73b-122">Interfejs wiersza polecenia dotnet</span><span class="sxs-lookup"><span data-stu-id="aa73b-122">dotnet CLI</span></span>](../install-nuget-client-tools.md#dotnetexe-cli) | <span data-ttu-id="aa73b-123">Projekty utworzone przed Visual Studio 2017 są inne niż stylu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="aa73b-123">Projects created prior to Visual Studio 2017 are non-SDK-style.</span></span> <span data-ttu-id="aa73b-124">Użyj `nuget.exe` interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="aa73b-124">Use `nuget.exe` CLI.</span></span> |
| <span data-ttu-id="aa73b-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="aa73b-125">.NET Framework</span></span> | <span data-ttu-id="aa73b-126">Non-SDK-style</span><span class="sxs-lookup"><span data-stu-id="aa73b-126">Non-SDK-style</span></span> | [<span data-ttu-id="aa73b-127">Interfejs wiersza polecenia nuget.exe</span><span class="sxs-lookup"><span data-stu-id="aa73b-127">nuget.exe CLI</span></span>](../install-nuget-client-tools.md#nugetexe-cli) | <span data-ttu-id="aa73b-128">Projektów programu .NET framework utworzone przy użyciu innych metod, może być projektów w stylu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="aa73b-128">.NET Framework projects created using other methods may be SDK-style projects.</span></span> <span data-ttu-id="aa73b-129">W tym przypadku użyj [wiersz polecenia dotnet](../install-nuget-client-tools.md#dotnetexe-cli) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="aa73b-129">For these, use [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli) instead.</span></span> |
| <span data-ttu-id="aa73b-130">[Zmigrowane](../reference/migrate-packages-config-to-package-reference.md) projektu .NET</span><span class="sxs-lookup"><span data-stu-id="aa73b-130">[Migrated](../reference/migrate-packages-config-to-package-reference.md) .NET project</span></span> | <span data-ttu-id="aa73b-131">Non-SDK-style</span><span class="sxs-lookup"><span data-stu-id="aa73b-131">Non-SDK-style</span></span>| <span data-ttu-id="aa73b-132">Aby utworzyć pakiety, użyj [msbuild - t: pakiet](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) do tworzenia pakietów.</span><span class="sxs-lookup"><span data-stu-id="aa73b-132">To create packages, use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) to create packages.</span></span> | <span data-ttu-id="aa73b-133">Aby utworzyć pakiety, `msbuild -t:pack` jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="aa73b-133">To create packages, `msbuild -t:pack` is recommended.</span></span> <span data-ttu-id="aa73b-134">W przeciwnym razie użyj [wiersz polecenia dotnet](../install-nuget-client-tools.md#dotnetexe-cli).</span><span class="sxs-lookup"><span data-stu-id="aa73b-134">Otherwise, use the [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli).</span></span> <span data-ttu-id="aa73b-135">Zmigrowane projekty nie są projektów w stylu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="aa73b-135">Migrated projects are not SDK-style projects.</span></span> |

## <a name="check-the-project-format"></a><span data-ttu-id="aa73b-136">Sprawdź format projektu</span><span class="sxs-lookup"><span data-stu-id="aa73b-136">Check the project format</span></span>

<span data-ttu-id="aa73b-137">Jeśli wiesz, czy projekt jest format stylu zestawu SDK, czy nie, poszukaj atrybutu zestawu SDK w `<Project>` elementu w pliku projektu (dla C#, jest to plik \*.csproj).</span><span class="sxs-lookup"><span data-stu-id="aa73b-137">If you're unsure whether the project is SDK-style format or not, look for the SDK attribute in the `<Project>` element in the project file (For C#, this is the \*.csproj file).</span></span> <span data-ttu-id="aa73b-138">Jeśli jest obecny, projektu to projekt zestawu SDK stylu.</span><span class="sxs-lookup"><span data-stu-id="aa73b-138">If it is present, the project is an SDK-style project.</span></span>

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

## <a name="check-the-project-format-in-visual-studio"></a><span data-ttu-id="aa73b-139">Sprawdź format projektu w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aa73b-139">Check the project format in Visual Studio</span></span>

<span data-ttu-id="aa73b-140">Jeśli pracujesz w programie Visual Studio, można szybko sprawdzić formatu projektu przy użyciu jednej z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="aa73b-140">If you are working in Visual Studio, you can quickly check the project format using one of the following methods:</span></span>

- <span data-ttu-id="aa73b-141">Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz **Edytuj myprojectname.csproj**.</span><span class="sxs-lookup"><span data-stu-id="aa73b-141">Right-click the project in Solution Explorer and select **Edit myprojectname.csproj**.</span></span>

   <span data-ttu-id="aa73b-142">Ta opcja jest dostępna tylko dla projektów korzystających z atrybutu zestawu SDK stylu począwszy od programu Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="aa73b-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="aa73b-143">W przeciwnym razie użyj innej metody.</span><span class="sxs-lookup"><span data-stu-id="aa73b-143">Otherwise, use the other method.</span></span>

   ![Edytuj plik projektu](media/edit-project-file.png)

   <span data-ttu-id="aa73b-145">Projekt w stylu zestawu SDK zawiera [atrybutu zestawu SDK](/dotnet/core/tools/csproj#additions) w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="aa73b-145">An SDK-style project shows the [SDK attribute](/dotnet/core/tools/csproj#additions) in the project file.</span></span>
   
- <span data-ttu-id="aa73b-146">Z **projektu** menu, wybierz **Zwolnij projekt** (lub kliknij prawym przyciskiem myszy projekt i wybierz pozycję **Zwolnij projekt**).</span><span class="sxs-lookup"><span data-stu-id="aa73b-146">From the **Project** menu, choose **Unload Project** (or right-click the project and choose **Unload Project**).</span></span>

   <span data-ttu-id="aa73b-147">Ten projekt nie będzie zawierać atrybut zestawu SDK w pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="aa73b-147">This project will not include the SDK attribute in the project file.</span></span> <span data-ttu-id="aa73b-148">Nie jest to projekt zestawu SDK stylu.</span><span class="sxs-lookup"><span data-stu-id="aa73b-148">It is not an SDK-style project.</span></span>

   ![Zwolnij projekt](media/unload-project.png)

   <span data-ttu-id="aa73b-150">Następnie kliknij prawym przyciskiem myszy zwolnionego projektu i wybierz **Edytuj myprojectname.csproj**.</span><span class="sxs-lookup"><span data-stu-id="aa73b-150">Then, right-click the unloaded project and choose **Edit myprojectname.csproj**.</span></span>

## <a name="see-also"></a><span data-ttu-id="aa73b-151">Zobacz także</span><span class="sxs-lookup"><span data-stu-id="aa73b-151">See also</span></span>

- [<span data-ttu-id="aa73b-152">Tworzenie pakietów standardowych .NET przy użyciu interfejsu wiersza polecenia platformy dotnet</span><span class="sxs-lookup"><span data-stu-id="aa73b-152">Create .NET Standard Packages with dotnet CLI</span></span>](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [<span data-ttu-id="aa73b-153">Tworzenie pakietów standardowych .NET za pomocą programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aa73b-153">Create .NET Standard Packages with Visual Studio</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [<span data-ttu-id="aa73b-154">Tworzenie i publikowanie pakietu .NET Framework (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="aa73b-154">Create and publish a .NET Framework package (Visual Studio)</span></span>](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [<span data-ttu-id="aa73b-155">Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild</span><span class="sxs-lookup"><span data-stu-id="aa73b-155">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
