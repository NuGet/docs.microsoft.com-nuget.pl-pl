---
title: Jak spakować formanty interfejsu użytkownika za pomocą narzędzia NuGet
description: Jak utworzyć pakiety NuGet, które zawierają kontrolki platformy UWP lub WPF, w tym niezbędne metadane i pliki pomocnicze dla projektantów programów Visual Studio i Blend.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: e1ebf5042597693ee55d986a4f93e797c27ad30a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622710"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>Tworzenie kontrolek interfejsu użytkownika jako pakietów NuGet

Począwszy od programu Visual Studio 2017, możesz skorzystać z dodatkowych możliwości dla formantów platformy UWP i WPF dostarczanych w pakietach NuGet. Ten przewodnik przeprowadzi Cię przez te możliwości w kontekście formantów platformy UWP za pomocą [przykładu ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage). To samo dotyczy formantów WPF, chyba że określono inaczej.

## <a name="prerequisites"></a>Wymagania wstępne

1. Visual Studio 2017
1. Informacje na temat [tworzenia pakietów platformy UWP](create-uwp-packages.md)

## <a name="generate-library-layout"></a>Generuj układ biblioteki

> [!Note]
> Ma to zastosowanie tylko do kontrolek platformy UWP.

Ustawienie `GenerateLibraryLayout` Właściwości zapewnia, że dane wyjściowe kompilacji projektu są generowane w układzie gotowym do spakowania bez potrzeby pojedynczych wpisów plików w nuspec.

Na stronie właściwości projektu przejdź do karty kompilacja i zaznacz pole wyboru "Generuj układ biblioteki". Spowoduje to zmodyfikowanie pliku projektu i ustawienie `GenerateLibraryLayout` flagi na true dla aktualnie wybranej konfiguracji kompilacji i platformy.

Alternatywnie Edytuj plik projektu, aby dodać `<GenerateLibraryLayout>true</GenerateLibraryLayout>` do pierwszej niewarunkowej grupy właściwości. Spowoduje to zastosowanie właściwości niezależnie od konfiguracji kompilacji i platformy.

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>Obsługa okienka Dodawanie zestawu narzędzi/zasobów dla kontrolek XAML

Aby formant XAML pojawił się w przyborniku projektanta XAML w programie Visual Studio i w okienku zasoby programu Blend, Utwórz `VisualStudioToolsManifest.xml` plik w `tools` folderze głównym folderu projektu pakietu. Ten plik nie jest wymagany, Jeśli kontrolka nie jest potrzebna w okienku Przybornik lub składniki.

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

Struktura pliku jest następująca:

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems UIFramework="WPF" VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

gdzie:

- *your_package_file*: nazwa pliku kontrolnego, na przykład `ManagedPackage.winmd` ("ManagedPackage", to arbitralna Nazwa użyta dla tego przykładu i nie ma innego znaczenia).
- *vs_category*: etykieta grupy, w której formant powinien pojawić się w przyborniku projektanta programu Visual Studio. `VSCategory`Jest to konieczne, aby formant pojawił się w przyborniku.
*ui_framework*: Nazwa struktury, taka jak "WPF", należy pamiętać, że ten `UIFramework` atrybut jest wymagany w węzłach ToolboxItems w programie Visual Studio 16,7 Preview 3 lub nowszym, aby formant pojawił się w przyborniku.
- *blend_category*: etykieta grupy, w której formant powinien pojawić się w okienku zasobów projektanta mieszania. `BlendCategory`Jest to konieczne, aby formant pojawił się w elementach zawartości.
- *type_full_name_n*: w pełni kwalifikowana nazwa dla każdej kontrolki, łącznie z przestrzenią nazw, taką jak `ManagedPackage.MyCustomControl` . Należy zauważyć, że format kropki jest używany zarówno dla typów zarządzanych, jak i natywnych.

W bardziej zaawansowanych scenariuszach można także uwzględnić wiele `<File>` elementów w obrębie, `<FileList>` gdy jeden pakiet zawiera wiele zestawów kontrolek. Możesz również mieć wiele `<ToolboxItems>` węzłów w obrębie jednej, `<File>` Jeśli chcesz zorganizować kontrolki w osobnych kategoriach.

W poniższym przykładzie kontrolka zaimplementowana w programie `ManagedPackage.winmd` zostanie wyświetlona w programie Visual Studio i Blend w grupie o nazwie "pakiet zarządzany" i "MyCustomControl" pojawi się w tej grupie. Wszystkie te nazwy są dowolne.

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems UIFramework="WPF" VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Przykładowa kontrolka wyświetlana w programie Visual Studio](media/UWP-control-vs-toolbox.png)

![Przykładowa kontrolka wyświetlana w programie Blend](media/UWP-control-blend-assets.png)

> [!Note]
> Należy jawnie określić każdą kontrolkę, która ma być widoczna w okienku Przybornik/składniki. Upewnij się, że określisz je w formacie `Namespace.ControlName` .

## <a name="add-custom-icons-to-your-controls"></a>Dodawanie niestandardowych ikon do kontrolek

Aby wyświetlić niestandardową ikonę w okienku Przybornik/składniki, Dodaj obraz do projektu lub odpowiedni `design.dll` projekt o nazwie "Namespace. ControlName. Extension" i ustaw akcję Build na "osadzony zasób". Należy również upewnić się, że skojarzona wartość `AssemblyInfo.cs` określa atrybut ProvideMetadata- `[assembly: ProvideMetadata(typeof(RegisterMetadata))]` . Zapoznaj się z tym [przykładem](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).

Obsługiwane formaty to `.png` ,,, `.jpg` `.jpeg` `.gif` i `.bmp` . Zalecany format to BMP24 16 pikseli przez 16 pikseli.

![Ikona pola narzędzia — przykład](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

Różowe tło jest zastępowane w czasie wykonywania. Po zmianie motywu programu Visual Studio ikony są zmieniane, a jego kolor tła jest oczekiwany. Aby uzyskać więcej informacji, zapoznaj się z [obrazami i ikonami dla programu Visual Studio](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).

W poniższym przykładzie projekt zawiera plik obrazu o nazwie "ManagedPackage.MyCustomControl.png".

![Ustawianie niestandardowej ikony w projekcie](media/UWP-control-custom-icon.png)

> [!Note]
> W przypadku kontrolek natywnych należy umieścić ikonę jako zasób w `design.dll` projekcie.

## <a name="support-specific-windows-platform-versions"></a>Obsługa określonych wersji platformy systemu Windows

Pakiety platformy UWP mają TargetPlatformVersion (TPV) i element targetplatformminversion (TPMinV) definiujące górne i dolne granice wersji systemu operacyjnego, w których można zainstalować aplikację. TPV dalsze określa wersję zestawu SDK, dla którego aplikacja została skompilowana. Pamiętaj o tych właściwościach podczas tworzenia pakietu platformy UWP: Używanie interfejsów API poza granicami wersji platformy zdefiniowanych w aplikacji spowoduje, że kompilacja zakończy się niepowodzeniem lub aplikacja zakończy się niepowodzeniem w czasie wykonywania.

Załóżmy na przykład, że ustawiono TPMinV dla pakietu formantów w systemie Windows 10 w wersji rocznicowej (10,0; Kompilacja 14393), aby upewnić się, że pakiet jest używany tylko przez projekty platformy UWP zgodne z tym dolną granicą. Aby zezwolić na korzystanie z pakietu przez projekty platformy UWP, należy spakować kontrolki następującymi nazwami folderów:

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

Pakiet NuGet automatycznie sprawdzi TPMinV pakietu, a instalacja nie powiedzie się, jeśli jest starsza niż Windows 10 rocznic Edition (10,0; Kompilacja 14393)

W przypadku WPF Załóżmy, że chcesz, aby pakiet formantów WPF był używany przez projekty ukierunkowane na .NET Framework v w wersji 4.6.1 lub wyższej. Aby wymusić to, należy spakować kontrolki o następujących nazwach folderów:

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>Dodawanie obsługi czasu projektowania

Aby skonfigurować, gdzie są wyświetlane właściwości kontrolki w Inspektorze właściwości, Dodaj niestandardowe moduły definiowania układu itp., umieść `design.dll` plik wewnątrz `lib\uap10.0.14393\Design` folderu odpowiednio do platformy docelowej. Ponadto, aby upewnić się, że **[Edytuj szablon > edytowanie funkcji kopiowania](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** , należy uwzględnić `Generic.xaml` i wszystkie słowniki zasobów, które Scala w `<your_assembly_name>\Themes` folderze (ponownie przy użyciu rzeczywistej nazwy zestawu). (Ten plik nie ma wpływu na zachowanie w czasie wykonywania kontrolki). Struktura folderów będzie wyglądać następująco:

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


W przypadku platformy WPF kontynuując przykład, w którym chcesz, aby pakiet formantów WPF był używany przez projekty przeznaczone dla .NET Framework v 4.6.1 lub wyższych:

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> Domyślnie właściwości kontrolki będą wyświetlane w kategorii Różne w Inspektorze właściwości.

## <a name="use-strings-and-resources"></a>Korzystanie z ciągów i zasobów

W pakiecie można osadzić zasoby ciągów ( `.resw` ), które mogą być używane przez formant lub projekt zużywający platformy UWP, ustawić właściwość **Akcja kompilacji** `.resw` pliku na **PRIResource**.

Aby zapoznać się z przykładem, zobacz [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) w przykładzie ExtensionSDKasNuGetPackage.

> [!Note]
> Ma to zastosowanie tylko do kontrolek platformy UWP.

## <a name="see-also"></a>Zobacz też

- [Tworzenie pakietów platformy UWP](create-uwp-packages.md)
- [Przykład ExtensionSDKasNuGetPackage](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
