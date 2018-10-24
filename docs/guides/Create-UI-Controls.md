---
title: Jak kontrolek interfejsu użytkownika pakietu nuget
description: Jak utworzyć pakiety NuGet, które zawierają platformy uniwersalnej systemu Windows lub programu WPF steruje tym potrzebnych metadanych i plików pomocniczych dla projektantów programu Visual Studio i Blend.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: dd36987e020c2daa02bb875aa9dbd69c85bba4d3
ms.sourcegitcommit: 1bd72dca2f85b4267b9924236f1d23dd7b0ed733
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/23/2018
ms.locfileid: "49951749"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>Tworzenie kontrolek interfejsu użytkownika jako pakietów NuGet

Za pomocą programu Visual Studio 2017 możesz korzystać z zalet dodano funkcje dla platformy uniwersalnej systemu Windows i kontrolek WPF, które dostarczają w pakietach NuGet. Ten przewodnik przeprowadzi Cię przez te możliwości w kontekście kontrolek platformy UWP przy użyciu [przykładowe ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). To samo dotyczy kontrolek WPF, chyba, że wymienione w inny sposób.

## <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2017
1. Opis sposobu [tworzenie pakietów platformy UWP](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Generuj układ biblioteki

> [!Note]
> Dotyczy tylko kontrolek platformy UWP.

Ustawienie `GenerateLibraryLayout` właściwość gwarantuje, że dane wyjściowe kompilacji projektu jest generowany w układzie, który jest gotowy do umieszczenia w pakiecie bez konieczności dla poszczególnych plików zapisów nuspec.

Z właściwości projektu przejdź na kartę kompilacji, a następnie zaznacz pole wyboru "Generuj układ biblioteki". Spowoduje to zmodyfikowania pliku projektu i ustawić `GenerateLibraryLayout` flagi na wartość true dla aktualnie wybrana konfiguracja kompilacji i platformy.

Możesz również edytować plik projektu, aby dodać `<GenerateLibraryLayout>true</GenerateLibraryLayout>` do pierwszej grupy właściwości bezwarunkowy. Ma to zastosowanie właściwości niezależnie od tego, czy konfigurację kompilacji i platformy.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Obsługę przybornika/zasoby okienka kontrolki XAML

Aby kontrolki XAML są wyświetlane w przyborniku projektanta XAML w programie Visual Studio i w okienku zasobów programu Blend, należy utworzyć `VisualStudioToolsManifest.xml` pliku w folderze głównym `tools` folderu projektu pakietu. Ten plik nie jest wymagane, jeśli nie potrzebujesz, aby formant mógł być wyświetlany w przyborniku lub w okienku zasobów.

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

Struktura pliku jest następująca:

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

- *your_package_file*: pliku nazwę kontrolki, takie jak `ManagedPackage.winmd` ("ManagedPackage" jest używany na potrzeby tego przykładu i nie ma innych znaczenia dowolną o nazwie).
- *vs_category*: Etykieta dla grupy, w którym formant powinna zostać wyświetlona w przyborniku projektanta programu Visual Studio. Element `VSCategory` jest konieczny, aby formant mógł być wyświetlany w przyborniku.
- *blend_category*: Etykieta dla grupy, w którym formant powinna zostać wyświetlona w okienku zasobów projektanta programu Blend. Element `BlendCategory` jest konieczny, aby formant mógł być wyświetlany w zasoby.
- *type_full_name_n*: w pełni kwalifikowaną nazwę dla każdej kontrolki, w tym przestrzeń nazw, takich jak `ManagedPackage.MyCustomControl`. Należy pamiętać, że format kropka jest używane dla typów zarządzane i natywne.

W bardziej zaawansowanych scenariuszy może również obejmować wiele `<File>` elementów w obrębie `<FileList>` Jeśli pojedynczy pakiet zawiera wiele zestawów formantu. Mogą też istnieć wiele `<ToolboxItems>` węzłów w ramach pojedynczej `<File>` aby organizować formantów na osobne kategorie.

W poniższym przykładzie kontrolki implementowany w `ManagedPackage.winmd` pojawi się w programie Visual Studio i Blend w grupie o nazwie "Pakiet Managed" i "MyCustomControl" pojawi się w tej grupie. Te nazwy są dowolne.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Kontrolka w postaci przykład postaci, w jakiej są wyświetlane w programie Visual Studio](media/UWP-control-vs-toolbox.png)

![Kontrolka w postaci przykład postaci, w jakiej są wyświetlane w programie Blend](media/UWP-control-blend-assets.png)

> [!Note]
> Należy jawnie określić każdy formant, który chcesz zobaczyć w okienku przybornika/zasobów. Upewnij się, podaj w formacie `Namespace.ControlName`.

## <a name="add-custom-icons-to-your-controls"></a>Dodawanie niestandardowych ikon do formantów

Aby wyświetlić ikonę niestandardową, w okienku przybornika/zasoby, należy dodać obraz do projektu lub odpowiednich `design.dll` projektu o nazwie "Namespace.ControlName.extension" i Ustaw akcję kompilacji "Osadzonego zasobu". Należy również zagwarantować, że skojarzone `AssemblyInfo.cs` Określa atrybut ProvideMetadata - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`. Zobacz ten [przykładowe](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).

Obsługiwane formaty to `.png`, `.jpg`, `.jpeg`, `.gif`, i `.bmp`. Rozmiar obrazu zalecane jest 64 pikseli 64 pikseli.

W poniższym przykładzie projekt zawiera plik o nazwie "ManagedPackage.MyCustomControl.png".

![Ustawienie ikony niestandardowej w projekcie](media/UWP-control-custom-icon.png)

> [!Note]
> W przypadku natywnych kontrolek należy umieścić ikony jako zasób w `design.dll` projektu.

## <a name="support-specific-windows-platform-versions"></a>Obsługa określonych wersji platformy Windows

Pakiety platformy uniwersalnej systemu Windows mają TargetPlatformVersion (TPV) i TargetPlatformMinVersion (TPMinV), które definiują górne i dolne granice wersji systemu operacyjnego zainstalowaną aplikację. Dodatkowo TPV Określa wersję zestawu SDK, względem którego skompilowano aplikację. Można je na uwadze tych właściwości, podczas tworzenia pakietu platformy uniwersalnej systemu Windows: za pomocą interfejsów API poza granicami wersje platformy, zdefiniowane w aplikacji spowoduje, że kompilacja nie powiedzie się lub aplikację, aby zakończyć się niepowodzeniem w czasie wykonywania.

Na przykład załóżmy, że ustawiono TPMinV dla pakietu formanty do systemu Windows 10 Anniversary Edition (10.0; Kompilacja 14393), tak aby mieć pewność, że pakiet jest używane tylko przez platformy uniwersalnej systemu Windows projektów pasujący i obniżyć powiązane z. Aby umożliwić pakietu do użycia w projektach platformy uniwersalnej systemu Windows, należy spakować formantów z następującymi nazwami folderu:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet sprawdzi automatycznie TPMinV konsumencki projektu i zakończona niepowodzeniem instalacji, jeśli jest on niższy niż Windows 10 Anniversary Edition (10.0; Kompilacja 14393)

W przypadku WPF Załóżmy się, że chcesz, aby pakiet kontrolek WPF być wykorzystane przez projekty przeznaczone dla .NET Framework v4.6.1 lub nowszej. Aby wymusić, który, należy spakować formantów z następującymi nazwami folderu:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Dodawanie obsługi w czasie projektowania

Aby skonfigurować, gdzie właściwości kontrolki wyświetlane w panelu Inspektor właściwości, Dodaj niestandardowe moduły definiowania układu itp., umieść usługi `design.dll` pliku wewnątrz `lib\uap10.0.14393\Design` folderów właściwe dla platformy docelowej. Ponadto aby upewnić się, że **[Edytuj szablon > Edytuj kopię](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** działania funkcji musi zawierać `Generic.xaml` i słowników zasobów, które łączy się on w `<your_assembly_name>\Themes` folder (ponownie przy użyciu Twoja nazwa zestawu rzeczywistego). (Ten plik nie ma wpływu na zachowanie środowiska uruchomieniowego kontrolki.) Struktura folderów związku z tym będzie wyglądać następująco:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


Dla WPF kontynuując w przykładzie gdzie chcesz użytkownika WPF kontrolki pakiet, który ma zostać użyte przez projekty przeznaczone dla .NET Framework v4.6.1 lub nowszej:

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Domyślnie właściwości kontrolki będą wyświetlane w różnych kategorii w panelu Inspektor właściwości.

## <a name="use-strings-and-resources"></a>Użyj ciągów i zasobów

Możesz osadzić zasoby w postaci ciągów (`.resw`) do pakietu, które mogą być używane przez formant lub konsumencki projektu platformy uniwersalnej systemu Windows, należy ustawić **Build Action** właściwość `.resw` plik **PRIResource**.

Na przykład dotyczyć [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) w przykładzie ExtensionSDKasNuGetPackage.

> [!Note]
> Dotyczy tylko kontrolek platformy UWP.

## <a name="see-also"></a>Zobacz także

- [Tworzenie pakietów platformy UWP](create-uwp-packages.md)
- [Przykładowe ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
