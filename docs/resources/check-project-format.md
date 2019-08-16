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
# <a name="identify-the-project-format"></a>Określ format projektu

Pakiet NuGet współpracuje ze wszystkimi projektami .NET. Jednak format projektu (zestaw SDK lub styl inny niż zestaw SDK) określa niektóre narzędzia i metody, które są potrzebne do korzystania z pakietów NuGet i ich tworzenia. Projekty w stylu zestawu SDK używają [atrybutu SDK](/dotnet/core/tools/csproj#additions). Ważne jest, aby zidentyfikować typ projektu, ponieważ metody i narzędzia używane do użycia i tworzenia pakietów NuGet są zależne od formatu projektu. W przypadku projektów typu non-SDK metody i narzędzia są również zależne od tego, czy projekt został zmigrowany do `PackageReference` formatu.

Czy projekt jest w stylu zestawu SDK, czy nie zależy od metody użytej do utworzenia projektu. W poniższej tabeli przedstawiono domyślny format projektu i skojarzone narzędzie interfejsu wiersza polecenia dla projektu podczas jego tworzenia przy użyciu programu Visual Studio 2017 i jego nowszych wersji.

| Project&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Domyślny format projektu | Narzędzie interfejsu wiersza polecenia&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Uwagi |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | SDK-style | [Interfejs wiersza polecenia dotnet](../install-nuget-client-tools.md#dotnetexe-cli) | Projekty utworzone przed Visual Studio 2017 są w stylu innym niż zestaw SDK. Użyj `nuget.exe` interfejsu wiersza polecenia. |
| .NET Core | SDK-style | [Interfejs wiersza polecenia dotnet](../install-nuget-client-tools.md#dotnetexe-cli) | Projekty utworzone przed Visual Studio 2017 są w stylu innym niż zestaw SDK. Użyj `nuget.exe` interfejsu wiersza polecenia. |
| .NET Framework | Non-SDK-style | [Interfejs wiersza polecenia nuget.exe](../install-nuget-client-tools.md#nugetexe-cli) | Projekty .NET Framework utworzone przy użyciu innych metod mogą być projektami w stylu zestawu SDK. W tym celu należy użyć [interfejsu wiersza polecenia dotnet](../install-nuget-client-tools.md#dotnetexe-cli) . |
| [Migrowany](../consume-packages/migrate-packages-config-to-package-reference.md) projekt .NET | Non-SDK-style| Aby utworzyć pakiety, użyj programu [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) do tworzenia pakietów. | Zalecane `msbuild -t:pack` jest utworzenie pakietów. W przeciwnym razie użyj [interfejsu wiersza polecenia dotnet](../install-nuget-client-tools.md#dotnetexe-cli). Zmigrowane projekty nie są projektami w stylu zestawu SDK. |

## <a name="check-the-project-format"></a>Sprawdź format projektu

Jeśli nie masz pewności, czy projekt jest w formacie stylu zestawu SDK, poszukaj atrybutu SDK w `<Project>` elemencie w pliku projektu (dla C#, jest to plik *. csproj). Jeśli jest obecny, projekt jest projektem w stylu zestawu SDK.

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

Jeśli pracujesz w programie Visual Studio, możesz szybko sprawdzić format projektu przy użyciu jednej z następujących metod:

- Kliknij prawym przyciskiem myszy projekt w Eksplorator rozwiązań i wybierz polecenie **Edytuj projektname. csproj**.

   Ta opcja jest dostępna tylko w programie Visual Studio 2017 dla projektów, które używają atrybutu stylu zestawu SDK. W przeciwnym razie użyj innej metody.

   ![Edytuj plik projektu](media/edit-project-file.png)

   Projekt w stylu zestawu SDK pokazuje [atrybut zestawu SDK](/dotnet/core/tools/csproj#additions) w pliku projektu.
   
- W menu **projekt** wybierz polecenie **Zwolnij projekt** (lub kliknij prawym przyciskiem myszy projekt i wybierz polecenie **Zwolnij projekt**).

   Ten projekt nie zawiera atrybutu SDK w pliku projektu. Nie jest to projekt w stylu zestawu SDK.

   ![Zwolnij projekt](media/unload-project.png)

   Następnie kliknij prawym przyciskiem myszy niezaładowanego projektu i wybierz polecenie **Edytuj projektname. csproj**.

## <a name="see-also"></a>Zobacz także

- [Tworzenie pakietów .NET Standard za pomocą interfejsu wiersza polecenia dotnet](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Tworzenie pakietów .NET Standard za pomocą programu Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [Tworzenie i publikowanie pakietu .NET Framework (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [Pakiet NuGet i przywracanie jako elementy docelowe programu MSBuild](../reference/msbuild-targets.md)
