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
# <a name="identify-the-project-format"></a>Identyfikowanie formatu projektu

NuGet współpracuje ze wszystkich projektów .NET. Jednak formatu projektu (SDK stylu lub stylu bez zestawu SDK) określa niektóre z narzędzi i metod, które należy użyć w celu umożliwienia użycia i tworzenie pakietów NuGet. Użyj zestawu SDK stylu projektów [atrybutu zestawu SDK](/dotnet/core/tools/csproj#additions). Należy zidentyfikować typu projektu, ponieważ metody i narzędzia, których używanie i tworzenie pakietów NuGet są zależne od formatu projektu. Dla projektów w stylu bez zestawu SDK, metody i narzędzia są również zależy od tego, czy zostały przeniesione do projektu `PackageReference` formatu.

Czy projekt jest zestaw SDK stylu lub nie zależy od metody używanej do tworzenia projektu. W poniższej tabeli przedstawiono domyślny format projektu oraz skojarzone narzędzie interfejsu wiersza polecenia dla projektu podczas tworzenia go za pomocą programu Visual Studio 2017 i nowsze wersje.

| Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Domyślny format projektu | Narzędzie interfejsu wiersza polecenia&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Uwagi |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | SDK-style | [Interfejs wiersza polecenia dotnet](../install-nuget-client-tools.md#dotnetexe-cli) | Projekty utworzone przed Visual Studio 2017 są inne niż stylu zestawu SDK. Użyj `nuget.exe` interfejsu wiersza polecenia. |
| .NET Core | SDK-style | [Interfejs wiersza polecenia dotnet](../install-nuget-client-tools.md#dotnetexe-cli) | Projekty utworzone przed Visual Studio 2017 są inne niż stylu zestawu SDK. Użyj `nuget.exe` interfejsu wiersza polecenia. |
| .NET Framework | Non-SDK-style | [Interfejs wiersza polecenia nuget.exe](../install-nuget-client-tools.md#nugetexe-cli) | Projektów programu .NET framework utworzone przy użyciu innych metod, może być projektów w stylu zestawu SDK. W tym przypadku użyj [wiersz polecenia dotnet](../install-nuget-client-tools.md#dotnetexe-cli) zamiast tego. |
| [Zmigrowane](../reference/migrate-packages-config-to-package-reference.md) projektu .NET | Non-SDK-style| Aby utworzyć pakiety, użyj [msbuild - t: pakiet](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) do tworzenia pakietów. | Aby utworzyć pakiety, `msbuild -t:pack` jest zalecane. W przeciwnym razie użyj [wiersz polecenia dotnet](../install-nuget-client-tools.md#dotnetexe-cli). Zmigrowane projekty nie są projektów w stylu zestawu SDK. |

## <a name="check-the-project-format"></a>Sprawdź format projektu

Jeśli wiesz, czy projekt jest format stylu zestawu SDK, czy nie, poszukaj atrybutu zestawu SDK w `<Project>` elementu w pliku projektu (dla C#, jest to plik *.csproj). Jeśli jest obecny, projektu to projekt zestawu SDK stylu.

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

## <a name="check-the-project-format-in-visual-studio"></a>Sprawdź format projektu w programie Visual Studio

Jeśli pracujesz w programie Visual Studio, można szybko sprawdzić formatu projektu przy użyciu jednej z następujących metod:

- Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań i wybierz **Edytuj myprojectname.csproj**.

   Ta opcja jest dostępna tylko dla projektów korzystających z atrybutu zestawu SDK stylu począwszy od programu Visual Studio 2017. W przeciwnym razie użyj innej metody.

   ![Edytuj plik projektu](media/edit-project-file.png)

   Projekt w stylu zestawu SDK zawiera [atrybutu zestawu SDK](/dotnet/core/tools/csproj#additions) w pliku projektu.
   
- Z **projektu** menu, wybierz **Zwolnij projekt** (lub kliknij prawym przyciskiem myszy projekt i wybierz pozycję **Zwolnij projekt**).

   Ten projekt nie będzie zawierać atrybut zestawu SDK w pliku projektu. Nie jest to projekt zestawu SDK stylu.

   ![Zwolnij projekt](media/unload-project.png)

   Następnie kliknij prawym przyciskiem myszy zwolnionego projektu i wybierz **Edytuj myprojectname.csproj**.

## <a name="see-also"></a>Zobacz także

- [Tworzenie pakietów standardowych .NET przy użyciu interfejsu wiersza polecenia platformy dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Tworzenie pakietów standardowych .NET za pomocą programu Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [Tworzenie i publikowanie pakietu .NET Framework (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild](../reference/msbuild-targets.md)
