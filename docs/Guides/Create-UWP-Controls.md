---
title: Formanty porady pakietu platformy uniwersalnej systemu Windows z programem NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 3/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 1f9de20a-f394-4cf2-8e40-ba0f4239cd5e
description: "Tworzenie pakietów NuGet, które zawierają platformy uniwersalnej systemu Windows steruje tym niezbędne metadane i pliki pomocnicze dla programu Visual Studio i Blend projektantów."
keywords: Formanty NuGet platformy uniwersalnej systemu Windows, programu Visual Studio XAML designer, projektanta programu Blend, formanty niestandardowe
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f51dbabd406199752e4f9d612b498f59ffb54021
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="creating-uwp-controls-as-nuget-packages"></a>Tworzenie formantów platformy uniwersalnej systemu Windows w postaci pakietów NuGet

Z programu Visual Studio 2017 r można korzystać z możliwości dodane dla formantów platformy uniwersalnej systemu Windows, które dostarczają w pakietach NuGet. Ten przewodnik przeprowadzi Cię przez te funkcje przy użyciu [próbki ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). 

## <a name="pre-requisites"></a>Wymagania wstępne:

1.  Visual Studio 2017
1.  Opis sposobu [tworzenia pakietów platformy uniwersalnej systemu Windows](create-uwp-packages.md)

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Obsługę przybornika/zasoby okienka kontrolki XAML

Aby wymusić formantowi XAML w przyborniku projektanta XAML w Visual Studio i w okienku zasobów programu Blend, Utwórz `VisualStudioToolsManifest.xml` pliku w folderze głównym `tools` folderu projektu pakietu. Ten plik nie jest wymagane, jeśli nie ma potrzeby wyglądać w przyborniku lub w okienku zasoby.

```
\build
\lib
\tools
    \VisualStudioToolsManifest.xml
```    

Struktura pliku jest następujący:

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

gdzie:

- *your_package_file*: Nazwa formantu plików, takich jak `ManagedPackage.winmd` ("ManagedPackage" jest używany w tym przykładzie dowolnego o nazwie i nie ma innych znaczenia).
- *vs_category*: Etykieta grupy, w którym ma wyglądać formant przybornika projektanta programu Visual Studio. A `VSCategory` jest niezbędna dla formantu pojawią się w przyborniku.
- *blend_category*: Etykieta grupy ma wyglądać formant, w okienku zasoby projektanta mieszania. A `BlendCategory` jest niezbędna dla formantu pojawią się w zasobach.
- *type_full_name_n*: pełni kwalifikowaną nazwą dla każdej kontrolki, w tym przestrzeń nazw, takich jak `ManagedPackage.MyCustomControl`. Należy pamiętać, że format kropka jest używana przez typy zarządzane i natywne.

W bardziej zaawansowanych scenariuszy, mogą również obejmować wiele `<File>` elementów w obrębie `<FileList>` Jeśli pojedynczy pakiet zawiera wiele zestawów formantu. Można również mieć wielu `<ToolboxItems>` węzłów w jednym `<File>` aby organizować formantów na osobne kategorie.

W poniższym przykładzie formantu realizowane w `ManagedPackage.winmd` będą wyświetlane w programie Visual Studio i Blend w grupie o nazwie "Zarządzanego pakietu" i "MyCustomControl" pojawi się w tej grupie. Te nazwy są dowolne.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Formant przykład postaci, w jakiej są wyświetlane w programie Visual Studio](media/UWP-control-vs-toolbox.png)

![Formant przykład postaci, w jakiej są wyświetlane w programie Blend](media/UWP-control-blend-assets.png)

> [!Note]
> Należy jawnie określić każdego formantu, który chcesz wyświetlić w okienku przybornika/zasobów. Upewnij się, określ w formacie `Namespace.ControlName`.

## <a name="add-custom-icons-to-your-controls"></a>Dodawanie ikon niestandardowych do formantów

Aby wyświetlić ikon niestandardowych w okienku przybornika/zasoby, należy dodać obraz do projektu lub odpowiednie `design.dll` projektu o nazwie "Namespace.ControlName.extension" i ustawić akcji kompilacji "Osadzonego zasobu". Obsługiwane formaty to `.png`, `.jpg`, `.jpeg`, `.gif`, i `.bmp`. Rozmiar obrazu zalecane jest x 64 pikseli 64.

W poniższym przykładzie projekt zawiera plik o nazwie "ManagedPackage.MyCustomControl.png".

![Ustawienie ikon niestandardowych w projekcie](media/UWP-control-custom-icon.png)

> [!Note]
> Dla natywnych kontrolek, możesz umieścić ikony jako zasób w `design.dll` projektu.

## <a name="support-specific-windows-platform-versions"></a>Obsługuje określonych wersji platformy systemu Windows

Pakiety platformy uniwersalnej systemu Windows zawierają TargetPlatformVersion (TPV) i TargetPlatformMinVersion (TPMinV), które definiują górne i dolne granice wersji systemu operacyjnego zainstalowaną aplikację. Dalsze TPV Określa wersję zestawu SDK, względem której aplikacja jest wbudowana. Można w trosce o te właściwości, podczas tworzenia pakietu platformy uniwersalnej systemu Windows: poza granicami wersje platformy zdefiniowanych w aplikacji przy użyciu interfejsów API spowoduje niepowodzenie kompilacji lub aplikację, aby zakończyć się niepowodzeniem w czasie wykonywania.

Na przykład załóżmy, że ustawiono TPMinV pakietu formantów systemu Windows 10 Anniversary Edition (10.0; Kompilacja 14393), tak aby mieć pewność, że pakiet jest używany tylko przez platformy uniwersalnej systemu Windows projekcję pasujących obniżyć powiązane z. Aby umożliwić pakietu jest używane przez `project.json` na podstawie projektów uniwersalnych systemu Windows, należy spakować formantów z następującymi nazwami folderu:

```
\lib\uap10.0\*
\ref\uap10.0\*
```

Aby wymusić odpowiednie wyboru TPMinV, Utwórz [plik elementów docelowych MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) i pakietu go w folderze kompilacji (zastępując "your_assembly_name" o nazwie z określonego zestawu):

```
\build
    \uap10.0
        your_assembly_name.targets
\lib
\tools
```

Oto przykład jak powinien wyglądać plik elementów docelowych:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="Build;ReBuild" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a>Dodawanie obsługi w czasie projektowania

Aby skonfigurować, których właściwości wyświetlane w Inspektora właściwości, Dodaj niestandardowego modułu definiowania układu kodu itp., umieść Twojej `design.dll` pliku wewnątrz `lib\<platform>\Design` folderu odpowiednio do platformy docelowej. Ponadto aby upewnić się, że  **[Edytuj szablon > edytowania kopii](https://docs.microsoft.com/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)**  działa funkcja musi zawierać `Generic.xaml` i słowników zasobów, które w scaleń `<AssemblyName>\Themes` folderu. (Ten plik nie ma wpływu na zachowanie środowiska uruchomieniowego formantu.)


```
\build
\lib
    \uap10.0.14393.0
        \Design
            \MyControl.design.dll
        \your_assembly_name
            \Themes     
                Generic.xaml
\tools
```

> [!Note]
> Domyślnie właściwości formantu będą widoczne w różnych kategorii w Inspektora właściwości.


## <a name="use-strings-and-resources"></a>Użyj ciągów i zasobów

Osadzić zasobów ciągu (`.resw`) do pakietu, które mogą być używane przez formant lub odbierającą projektu platformy uniwersalnej systemu Windows, należy ustawić **Akcja kompilacji** właściwość `.resw` pliku **PRIResource**.

Na przykład dotyczą [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) w przykładowym ExtensionSDKasNuGetPackage.

## <a name="package-content-such-as-images"></a>Pakiet zawartości, takich jak obrazy

Do pakietu zawartości, takich jak obrazy, które mogą być używane przez formant lub odbierającą projektu platformy uniwersalnej systemu Windows. Dodaj te pliki `lib\uap10.0.14393.0` folderu w następujący sposób ("your_assembly_name" ponownie powinien odpowiadać określonego formantu):

```
\build
\lib
    \uap10.0.14393.0
        \Design
        \your_assembly_name
\contosoSampleImage.jpg
\tools
```

Mogą również tworzyć[plik elementów docelowych MSBuild](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) zapewnienie element zawartości jest kopiowany do folderu wyjściowego odbierającą projektu:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0.14393.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a>Zobacz także

- [Tworzenie pakietów platformy uniwersalnej systemu Windows](create-uwp-packages.md)
- [Przykładowe ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
