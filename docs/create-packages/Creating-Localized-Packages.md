---
title: Jak utworzyć zlokalizowany pakiet NuGet
description: Szczegółowe informacje na temat dwóch sposobów tworzenia zlokalizowanych pakietów NuGet przy użyciu wszystkich zestawów w pojedynczym pakiecie lub publikowania oddzielnych zestawów.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: dbc3781bd17f815c6b32fc70b275469337148f41
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488835"
---
# <a name="creating-localized-nuget-packages"></a>Tworzenie zlokalizowanych pakietów NuGet

Istnieją dwa sposoby tworzenia zlokalizowanych wersji biblioteki:

1. Uwzględnij wszystkie zestawy zlokalizowanych zasobów w pojedynczym pakiecie.
1. Utwórz oddzielne, zlokalizowane pakiety satelickie, wykonując rygorystyczne zestawy Konwencji.

Obie metody mają swoje zalety i wady, zgodnie z opisem w poniższych sekcjach.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Zlokalizowane zestawy zasobów w pojedynczym pakiecie

Uwzględnianie zlokalizowanych zestawów zasobów w pojedynczym pakiecie jest zazwyczaj najprostszym podejściem. W tym celu należy utworzyć foldery w `lib` programie dla obsługiwanego języka innego niż domyślny pakiet (założono, że jest to en-US). W tych folderach można umieścić zestawy zasobów i zlokalizowane pliki XML IntelliSense.

Na przykład następująca struktura folderów obsługuje, niemiecki (Niemcy), włoski (IT), japoński (ja), rosyjski (ru), chiński (uproszczony) (zh-Hans) i chiński (tradycyjny) (zh-Hant):

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

Można zobaczyć, że wszystkie języki są wymienione poniżej `net40` folderu platformy docelowej. Jeśli obsługujesz [wiele platform](../create-packages/supporting-multiple-target-frameworks.md), masz folder w obszarze `lib` dla każdego wariantu.

Po wprowadzeniu tych folderów odwołujesz się do wszystkich plików w `.nuspec`:

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

Jednym z przykładowych pakietów korzystających z tej metody jest [Microsoft. Data. OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Zalety i wady (zlokalizowane zestawy zasobów)

Zgrupowanie wszystkich języków w jednym pakiecie ma kilka wad:

1. **Udostępnione metadane**: Ponieważ pakiet NuGet może zawierać tylko jeden `.nuspec` plik, można dostarczyć metadane tylko dla jednego języka. Oznacza to, że NuGet nie obsługuje zlokalizowanych metadanych.
1. **Rozmiar pakietu**: W zależności od liczby obsługiwanych języków biblioteka może stać się znacznie duża, co powoduje spowolnienie instalowania i przywracania pakietu.
1. **Równoczesne wersje**: Umieszczenie zlokalizowanych plików w pojedynczym pakiecie wymaga jednoczesnego udostępnienia wszystkich zasobów w tym pakiecie, a nie udostępnienia oddzielnie każdej lokalizacji. Ponadto każda aktualizacja w jednej lokalizacji wymaga nowej wersji całego pakietu.

Jednak ma ona również kilka korzyści:

1. **Prostota**: Odbiorcy pakietu pobierają wszystkie obsługiwane języki w jednej instalacji, a nie muszą oddzielnie instalować każdego języka. Jeden pakiet jest również łatwiejszy do znalezienia w witrynie nuget.org.
1. **Połączone wersje**: Ze względu na to, że wszystkie zestawy zasobów znajdują się w tym samym pakiecie co zestaw podstawowy, każdy z nich ma ten sam numer wersji i nie powoduje ryzyka błędnego oddzielenia.

## <a name="localized-satellite-packages"></a>Zlokalizowane pakiety satelickie

Podobnie jak .NET Framework obsługuje zestawy satelickie, ta metoda oddziela zlokalizowane zasoby i pliki XML IntelliSense do pakietów satelitarnych.

W tym celu pakiet podstawowy używa konwencji `{identifier}.{version}.nupkg` nazewnictwa i zawiera zestaw dla języka domyślnego (na przykład en-US). Na przykład `ContosoUtilities.1.0.0.nupkg` będzie zawierać następującą strukturę:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Zestaw satelity używa konwencji `{identifier}.{language}.{version}.nupkg`nazewnictwa, takiej jak. `ContosoUtilities.de.1.0.0.nupkg` Identyfikator **musi** być dokładnie zgodny z pakietem podstawowym.

Ponieważ jest to oddzielny pakiet, ma własny `.nuspec` plik, który zawiera zlokalizowane metadane. Należy mieć na uwadze, że język `.nuspec` w **musi** być zgodny z użytym w nazwie pliku.

Zestawu satelickiego **musi** deklarować dokładnej wersji głównej pakietu także jako zależności, przy użyciu notacji wersji [] \(zobacz [wersji pakietu](../concepts/package-versioning.md)). Na przykład, `ContosoUtilities.de.1.0.0.nupkg` należy zadeklarować `ContosoUtilities.1.0.0.nupkg` zależność przy użyciu `[1.0.0]` notacji. Pakiet satelitarny może mieć inny numer wersji niż pakiet podstawowy.

Struktura pakietu satelitarnego musi zawierać zestaw zasobów i plik IntelliSense XML w podfolderze, który pasuje `{language}` do nazwy pliku pakietu:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Uwaga**: Jeśli określone podkultury, takie jak `ja-JP` są niezbędne, zawsze używają identyfikatora `ja`języka wyższego poziomu, takiego jak.

W zestawie satelity program NuGet rozpozna **tylko** te pliki w folderze, które pasują `{language}` do nazwy pliku. Wszystkie pozostałe są ignorowane.

Gdy zostaną spełnione wszystkie z tych konwencji, pakiet NuGet rozpoznaje go jako pakiet satelitarny i zainstaluje zlokalizowane pliki w `lib` folderze pakietu podstawowego, tak jakby były pierwotnie powiązane. Odinstalowanie pakietu satelickiego spowoduje usunięcie jego plików z tego samego folderu.

W ten sam sposób można utworzyć dodatkowe zestawy satelickie dla każdego obsługiwanego języka. Aby zapoznać się z przykładem, należy zapoznać się z zestawem pakietów ASP.NET MVC:

- [Microsoft. ASPNET. MVC](http://nuget.org/packages/Microsoft.AspNet.Mvc) (podstawowa wersja angielskojęzyczna)
- [Microsoft.ASPNET.MVC.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (niemiecki)
- [Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)
- [Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))
- [Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))

### <a name="summary-of-required-conventions"></a>Podsumowanie wymaganych Konwencji

- Pakiet podstawowy musi mieć nazwę`{identifier}.{version}.nupkg`
- Pakiet satelitarny musi mieć nazwę`{identifier}.{language}.{version}.nupkg`
- Pakiet satelitarny `.nuspec` musi określać swój język, aby odpowiadał nazwie pliku.
- Pakiet satelitarny musi deklarować zależność dla dokładnej wersji elementu głównego przy użyciu notacji [] w `.nuspec` pliku. Zakresy nie są obsługiwane.
- Pakiet satelitarny musi umieścić pliki w `lib\[{framework}\]{language}` folderze, który dokładnie pasuje `{language}` do nazwy pliku.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Zalety i wady (pakiety satelitarne)

Używanie pakietów satelitarnych ma kilka zalet:

1. **Rozmiar pakietu**: Ogólny wpływ pakietu podstawowego jest zminimalizowany, a konsumenci ponoszą koszty każdego języka, którego chcą używać.
1. **Oddziel metadane**: Każdy pakiet satelitarny ma własny `.nuspec` plik i dlatego jego własne zlokalizowane metadane. Może to ułatwić klientom łatwiejsze znajdowanie pakietów przez wyszukiwanie nuget.org przy użyciu zlokalizowanych warunków.
1. Rozłączone **wersje**: Zestawy satelickie mogą być uwalniane z upływem czasu, a nie tylko na raz, co pozwala na rozłożenie wysiłków związanych z lokalizacją.

Jednak pakiety satelickie mają swój własny zestaw wad:

1. **Bałagan**: Zamiast pojedynczego pakietu, masz wiele pakietów, które mogą prowadzić do nieczytelnych wyników wyszukiwania na nuget.org i długiej listy odwołań w projekcie programu Visual Studio.
1. **Ścisłe konwencje**. Pakiety satelickie muszą być zgodne z konwencjami dokładnie lub zlokalizowane wersje nie będą prawidłowo pobierane.
1. **Przechowywanie wersji**: Każdy pakiet satelitarny musi mieć dokładną zależność wersji w pakiecie podstawowym. Oznacza to, że aktualizacja pakietu podstawowego może wymagać aktualizacji wszystkich pakietów satelitarnych, nawet jeśli zasoby nie uległy zmianie.
