---
title: Identyfikowanie formatu projektu
description: W tym artykule opisano sposób identyfikacji formatu projektu
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488480"
---
# <a name="identify-the-project-format"></a>Identyfikowanie formatu projektu

NuGet współpracuje ze wszystkimi projektami platformy .NET. Jednak format projektu (SDK stylu lub non-SDK stylu) określa niektóre narzędzia i metody, które należy użyć do korzystania i tworzenia pakietów NuGet. Projekty w stylu SDK używają [atrybutu SDK](/dotnet/core/tools/csproj#additions). Jest ważne, aby zidentyfikować typ projektu, ponieważ metody i narzędzia używane do korzystania i tworzenia pakietów NuGet są zależne od formatu projektu. W przypadku projektów w stylu innych niż SDK metody i narzędzia są również `PackageReference` zależne od tego, czy projekt został zmigrowany do formatu.

To, czy projekt jest w stylu SDK, czy nie, zależy od metody użytej do utworzenia projektu. W poniższej tabeli przedstawiono domyślny format projektu i skojarzone narzędzie interfejsu wiersza polecenia dla projektu podczas tworzenia go przy użyciu programu Visual Studio 2017 i nowszych wersji.

| Projektu&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Domyślny format projektu | Narzędzie CLI&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Uwagi |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | SDK w stylu | [Interfejs wiersza polecenia dotnet](../install-nuget-client-tools.md#dotnetexe-cli) | Projekty utworzone przed programem Visual Studio 2017 są w stylu nienawiązanych do SDK. Użyj `nuget.exe` interfejsu wiersza polecenia. |
| .NET Core | SDK w stylu | [Interfejs wiersza polecenia dotnet](../install-nuget-client-tools.md#dotnetexe-cli) | Projekty utworzone przed programem Visual Studio 2017 są w stylu nienawiązanych do SDK. Użyj `nuget.exe` interfejsu wiersza polecenia. |
| .NET Framework | W stylu innych niż SDK | [Interfejs wiersza polecenia nuget.exe](../install-nuget-client-tools.md#nugetexe-cli) | .NET Framework projektów utworzonych przy użyciu innych metod mogą być projekty w stylu SDK. W tym celu należy użyć [polecenia polecenia dotnet.](../install-nuget-client-tools.md#dotnetexe-cli) |
| [Zmigrowany](../consume-packages/migrate-packages-config-to-package-reference.md) projekt platformy .NET | W stylu innych niż SDK| Aby utworzyć pakiety, użyj [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) do tworzenia pakietów. | Aby utworzyć `msbuild -t:pack` pakiety, zaleca się. W przeciwnym razie użyj [dotnet CLI](../install-nuget-client-tools.md#dotnetexe-cli). Zmigrowane projekty nie są projektami w stylu SDK. |

## <a name="check-the-project-format"></a>Sprawdź format projektu

Jeśli nie masz pewności, czy projekt jest formatem w stylu SDK, poszukaj atrybutu SDK w `<Project>` elemencie w pliku projektu (dla języka C#jest to plik *.csproj). Jeśli jest obecny, projekt jest projektem w stylu SDK.

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

## <a name="check-the-project-format-in-visual-studio"></a>Sprawdzanie formatu projektu w programie Visual Studio

Jeśli pracujesz w programie Visual Studio, możesz szybko sprawdzić format projektu przy użyciu jednej z następujących metod:

- Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz polecenie **Edytuj plik myprojectname.csproj**.

   Ta opcja jest dostępna tylko od programu Visual Studio 2017 dla projektów korzystających z atrybutu w stylu SDK. W przeciwnym razie użyj innej metody.

   ![Edytowanie pliku projektu](media/edit-project-file.png)

   Projekt w stylu SDK pokazuje [atrybut SDK](/dotnet/core/tools/csproj#additions) w pliku projektu.
   
- W menu **Projekt** wybierz polecenie **Zwolnij projekt** (lub kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zwolnij projekt).**

   Ten projekt nie będzie zawierać atrybutu SDK w pliku projektu. Nie jest to projekt w stylu SDK.

   ![Zwalnianie projektu](media/unload-project.png)

   Następnie kliknij prawym przyciskiem myszy niezaładowany projekt i wybierz polecenie **Edytuj plik myprojectname.csproj**.

## <a name="see-also"></a>Zobacz też

- [Tworzenie standardowych pakietów platformy .NET za pomocą interfejsu wiersza polecenia dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Tworzenie standardowych pakietów platformy .NET za pomocą programu Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [Tworzenie i publikowanie pakietu .NET Framework (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [NuGet pack and restore as MSBuild targets NuGet pack and restore as MSBuild targets NuGet pack and restore as MSBuild targets NuGet](../reference/msbuild-targets.md)
