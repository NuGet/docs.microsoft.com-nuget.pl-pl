---
title: Jak formantów interfejsu użytkownika pakietu NuGet
description: Tworzenie pakietów NuGet, które zawierają platformy uniwersalnej systemu Windows lub programu WPF steruje tym niezbędne metadane i pliki pomocnicze dla programu Visual Studio i Blend projektantów.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: ab7499c415f63319fd314f33607f74d400b5f957
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818661"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>Tworzenie formantów interfejsu użytkownika jako pakietów NuGet

Z programu Visual Studio 2017 r można korzystać z możliwości dodane dla platformy uniwersalnej systemu Windows i WPF formantów dostarczających w pakietach NuGet. Ten przewodnik przeprowadzi Cię przez te funkcje w kontekście formantów platformy uniwersalnej systemu Windows za pomocą [próbki ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). To samo dotyczy formantów WPF chyba, że wymienione w inny sposób.

## <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2017
1. Opis sposobu [tworzenia pakietów platformy uniwersalnej systemu Windows](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Generowanie układu biblioteki

> [!Note]
> Ma to zastosowanie tylko do formantów platformy uniwersalnej systemu Windows.

Ustawienie `GenerateLibraryLayout` właściwości zapewnia wygenerowania danych wyjściowych kompilacji projektu w układzie, który jest gotowy do umieszczone bez konieczności poszczególne wpisy w plik nuspec.

We właściwościach projektu, przejdź do karty kompilacji, a następnie zaznacz pole wyboru "Generowanie układu biblioteki". Spowoduje to modyfikowania pliku projektu i ustawić `GenerateLibraryLayout` flagi na wartość true dla aktualnie wybranej kompilacji konfiguracji i platformy.

Alternatywnie Edytuj plik projektu, aby dodać `<GenerateLibraryLayout>true</GenerateLibraryLayout>` do pierwszej grupy właściwości bezwarunkowe. Ma to zastosowanie właściwości niezależnie od konfigurację kompilacji i platformy.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Obsługę przybornika/zasoby okienka kontrolki XAML

Aby wymusić formantowi XAML w przyborniku projektanta XAML w Visual Studio i w okienku zasobów programu Blend, Utwórz `VisualStudioToolsManifest.xml` pliku w folderze głównym `tools` folderu projektu pakietu. Ten plik nie jest wymagane, jeśli nie ma potrzeby wyglądać w przyborniku lub w okienku zasoby.

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

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

Na przykład załóżmy, że ustawiono TPMinV pakietu formantów systemu Windows 10 Anniversary Edition (10.0; Kompilacja 14393), tak aby mieć pewność, że pakiet jest używany tylko przez platformy uniwersalnej systemu Windows projekcję pasujących obniżyć powiązane z. Umożliwia pakietu zużywanych przez projekty platformy uniwersalnej systemu Windows, należy spakować formantów z następującymi nazwami folderu:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet zostanie automatycznie Sprawdź TPMinV odbierającą projektu i niepowodzenie instalacji, jeśli jest mniejszy od systemu Windows 10 Anniversary Edition (10.0; Kompilacja 14393)

W przypadku WPF Załóżmy się, że chcesz pakietu formantów WPF wykorzystanych w projektach przeznaczonych dla platformy .NET Framework v4.6.1 lub nowszej. Aby wymusić, który, należy spakować formantów z następującymi nazwami folderu:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Dodawanie obsługi w czasie projektowania

Aby skonfigurować, których właściwości wyświetlane w Inspektora właściwości, Dodaj niestandardowego modułu definiowania układu kodu itp., umieść Twojej `design.dll` pliku wewnątrz `lib\uap10.0.14393\Design` folderu odpowiednio do platformy docelowej. Ponadto aby upewnić się, że **[Edytuj szablon > edytowania kopii](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** działa funkcja musi zawierać `Generic.xaml` i słowników zasobów, które w scaleń `<your_assembly_name>\Themes` folder (ponownie, używając Nazwa zestawu rzeczywiste). (Ten plik nie ma wpływu na zachowanie środowiska uruchomieniowego formantu.) Struktura folderów w związku z tym będzie wyglądać następująco:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


Dla WPF kontynuowanie w przykładzie miejsce chcesz programu WPF kontrolki pakiecie będą wykorzystane w projektach przeznaczonych dla platformy .NET Framework v4.6.1 lub nowszy:

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Domyślnie właściwości formantu będą widoczne w różnych kategorii w Inspektora właściwości.

## <a name="use-strings-and-resources"></a>Użyj ciągów i zasobów

Osadzić zasobów ciągu (`.resw`) do pakietu, które mogą być używane przez formant lub odbierającą projektu platformy uniwersalnej systemu Windows, należy ustawić **Akcja kompilacji** właściwość `.resw` pliku **PRIResource**.

Na przykład dotyczą [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) w przykładowym ExtensionSDKasNuGetPackage.

> [!Note]
> Ma to zastosowanie tylko do formantów platformy uniwersalnej systemu Windows.

## <a name="see-also"></a>Zobacz także

- [Tworzenie pakietów platformy UWP](create-uwp-packages.md)
- [Przykładowe ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
