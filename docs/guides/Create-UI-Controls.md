---
title: Jak spakować kontrolki interfejsu użytkownika za pomocą nuget
description: Jak utworzyć pakiety NuGet, które zawierają formanty platformy uniwersalnej systemu Wizjudy lub WPF, w tym niezbędne metadane i pliki pomocnicze dla projektantów programu Visual Studio i Blend.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: da8c5a05311c790bf6b873bc0f1a077d3ef1db87
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610618"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>Tworzenie kontrolek interfejsu użytkownika jako pakietów NuGet

Począwszy od programu Visual Studio 2017, można skorzystać z dodatkowych funkcji dla formantów platformy uniwersalnej systemu i WPF, które dostarczasz w pakietach NuGet. W tym przewodniku przeprowadzi Cię przez te możliwości w kontekście formantów platformy uniwersalnej systemuśpiłnie przy użyciu [extensionSDKasNuGetPackage próbki](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). To samo dotyczy formantów WPF, chyba że określono inaczej.

## <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2017
1. Dowiesz się, jak [tworzyć pakiety platformy uniwersalnej systemuśpiłnie](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Generowanie układu biblioteki

> [!Note]
> Dotyczy to tylko formantów platformy uniwersalnej systemuśpiłka.

Ustawienie `GenerateLibraryLayout` właściwości zapewnia, że dane wyjściowe kompilacji projektu jest generowany w układzie, który jest gotowy do pakowania bez konieczności poszczególnych wpisów plików w nuspec.

We właściwościach projektu przejdź do karty kompilacji i zaznacz pole wyboru "Generowanie układu biblioteki". Spowoduje to zmodyfikowanie pliku `GenerateLibraryLayout` projektu i ustawienie flagi na true dla aktualnie wybranej konfiguracji kompilacji i platformy.

Alternatywnie edytuj plik projektu, `<GenerateLibraryLayout>true</GenerateLibraryLayout>` aby dodać go do pierwszej bezwarunkowej grupy właściwości. To będzie zastosowanie właściwości niezależnie od konfiguracji kompilacji i platformy.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Dodawanie obsługi okienek przybornika/zasobów dla formantów XAML

Aby kontrolka XAML była wyświetlana w przyborniku projektanta XAML w programie `VisualStudioToolsManifest.xml` Visual Studio i `tools` okienku Zasoby programu Blend, utwórz plik w katalogu głównym folderu projektu pakietu. Ten plik nie jest wymagany, jeśli nie potrzebujesz formantu, aby pojawić się w przyborniku lub okienku Zasoby.

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

- *your_package_file*: nazwa pliku kontrolnego, na `ManagedPackage.winmd` przykład ("ManagedPackage" jest dowolną nazwą używaną w tym przykładzie i nie ma innego znaczenia).
- *vs_category:* Etykieta dla grupy, w której formant powinien pojawić się w przyborniku projektanta programu Visual Studio. A `VSCategory` jest niezbędne, aby formant pojawiał się w przyborniku.
- *blend_category*: Etykieta dla grupy, w której formant powinien być wyświetlany w okienku Zasoby projektanta mieszania. A `BlendCategory` jest niezbędne do formantu do stawienia się w zasoby.
- *type_full_name_n*: W pełni kwalifikowana nazwa dla każdego formantu, łącznie z obszarem nazw, na przykład `ManagedPackage.MyCustomControl`. Należy zauważyć, że format kropki jest używany zarówno dla typów zarządzanych, jak i natywnych.

W bardziej zaawansowanych scenariuszach można `<File>` również `<FileList>` dołączyć wiele elementów w ramach, gdy pojedynczy pakiet zawiera wiele zestawów kontroli. Można również mieć `<ToolboxItems>` wiele węzłów `<File>` w ramach jednego, jeśli chcesz zorganizować formanty w oddzielnych kategoriach.

W poniższym przykładzie formant `ManagedPackage.winmd` zaimplementowany w pojawi się w programie Visual Studio i Blend w grupie o nazwie "Pakiet zarządzany", a w tej grupie pojawi się "MyCustomControl". Wszystkie te nazwy są dowolne.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Przykładowy formant wyświetlany w programie Visual Studio](media/UWP-control-vs-toolbox.png)

![Przykładowy formant wyświetlany w trybie Mieszania](media/UWP-control-blend-assets.png)

> [!Note]
> Należy jawnie określić każdy formant, który chcesz zobaczyć w polu narzędziowym/zasobach okienka. Upewnij się, że `Namespace.ControlName`określisz je w formacie .

## <a name="add-custom-icons-to-your-controls"></a>Dodawanie niestandardowych ikon do kontrolek

Aby wyświetlić niestandardową ikonę w okienku przybornika/zasobu, `design.dll` dodaj obraz do projektu lub odpowiedniego projektu o nazwie "Namespace.ControlName.extension" i ustaw akcję kompilacji na "Osadzony zasób". Należy również upewnić się, że skojarzony `AssemblyInfo.cs` określa `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`atrybut ProvideMetadata - . Zobacz ten [przykład](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).

Obsługiwane formaty `.png`to `.jpg` `.jpeg`, `.gif`, `.bmp`, i . Zalecanym formatem jest BMP24 w 16 pikselach na 16 pikseli.

![Przykład ikony pola narzędzi](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

Różowe tło zostanie zastąpione w czasie wykonywania. Ikony są ponownie kolorowane po zmianie motywu programu Visual Studio i oczekuje się, że kolor tła. Aby uzyskać więcej informacji, zapoznaj się [z obrazami i ikonami programu Visual Studio](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).

W poniższym przykładzie projekt zawiera plik obrazu o nazwie "ManagedPackage.MyCustomControl.png".

![Ustawianie niestandardowej ikony w projekcie](media/UWP-control-custom-icon.png)

> [!Note]
> W przypadku formantów natywnych należy `design.dll` umieścić ikonę jako zasób w projekcie.

## <a name="support-specific-windows-platform-versions"></a>Obsługa określonych wersji platformy systemu Windows

Pakiety platformy uniwersalnej systemu Windows mają targetplatformversion (TPV) i TargetPlatformMinVersion (TPMinV), które definiują górne i dolne granice wersji systemu operacyjnego, w której można zainstalować aplikację. TPV dalej określa wersję SDK, dla którego aplikacja jest zbudowana. Należy pamiętać o tych właściwości podczas tworzenia pakietu platformy uniwersalnej systemu Windows: przy użyciu interfejsów API poza granicami wersji platformy zdefiniowane w aplikacji spowoduje, że kompilacja zakończy się niepowodzeniem lub aplikacji zakończy się niepowodzeniem w czasie wykonywania.

Załóżmy na przykład, że ustawiłeś pakiet TPMinV dla pakietu formanty na Windows 10 Anniversary Edition (10.0; Kompilacja 14393), więc chcesz upewnić się, że pakiet jest zużywany tylko przez projekty platformy uniwersalnej systemu i platformy uniwersalnej systemu i platformy uniwersalnej systemu, które pasują do tej dolnej granicy. Aby zezwolić na korzystanie z pakietu przez projekty platformy uniwersalnej systemu Windows, należy spakować formanty z następującymi nazwami folderów:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet automatycznie sprawdzi TPMinV projektu zużywającego i zakończy się niepowodzeniem instalacji, jeśli jest niższa niż Windows 10 Anniversary Edition (10.0; Kompilacja 14393)

W przypadku WPF, załóżmy, że chcesz, aby pakiet formanty WPF do korzystania przez projekty przeznaczone dla platformy .NET Framework v4.6.1 lub nowszego. Aby to wymusić, należy spakować formanty z następującymi nazwami folderów:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Dodaj obsługę czasu projektowania

Aby skonfigurować, gdzie właściwości formantu są wyświetlane w inspektorze właściwości, dodaj `design.dll` niestandardowe `lib\uap10.0.14393\Design` adorners itp., umieść plik wewnątrz folderu odpowiednio do platformy docelowej. Ponadto, aby upewnić się, że edytuj szablon > Edytuj funkcję `Generic.xaml` **[kopiowania](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** działa, należy dołączyć `<your_assembly_name>\Themes` i wszystkie słowniki zasobów, które scala się w folderze (ponownie, przy użyciu rzeczywistej nazwy zestawu). (Ten plik nie ma wpływu na zachowanie środowiska wykonawczego formantu.) Struktura folderów wydaje się zatem następująca:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


W przypadku WPF, kontynuując przykład, w którym chcesz, aby pakiet formanty WPF był zużywany przez projekty przeznaczone dla platformy .NET Framework w wersji 4.6.1 lub wyższej:

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Domyślnie właściwości formantu będą wyświetlane w kategorii Różne w Inspektorze właściwości.

## <a name="use-strings-and-resources"></a>Używanie ciągów i zasobów

Można osadzić zasoby`.resw`ciągów ( ) w pakiecie, który może być używany przez formant lub `.resw` zużywający projekt platformy uniwersalnej systemu wytwórczego, ustaw właściwość **Kompilacja pliku** na **PRIResource**.

Na przykład należy zapoznać się [z MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) w ExtensionSDKasNuGetPackage próbki.

> [!Note]
> Dotyczy to tylko formantów platformy uniwersalnej systemuśpiłka.

## <a name="see-also"></a>Zobacz też

- [Tworzenie pakietów platformy uniwersalnej systemu i platformy uniwersalnej systemu](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage przykład](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
