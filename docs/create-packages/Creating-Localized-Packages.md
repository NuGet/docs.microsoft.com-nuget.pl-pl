---
title: Jak utworzyć zlokalizowany pakiet NuGet
description: Szczegółowe informacje na temat dwóch sposobów tworzenia zlokalizowanych pakietów NuGet, przez włączenie wszystkich zestawów w jednym pakiecie lub publikowania oddzielnych zestawów.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 83414a824676844f9e44eab874e5eac788d50583
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610941"
---
# <a name="creating-localized-nuget-packages"></a>Tworzenie zlokalizowanych pakietów NuGet

Istnieją dwa sposoby tworzenia zlokalizowanych wersji biblioteki:

1. Uwzględnij wszystkie zlokalizowane zestawy zasobów w jednym pakiecie.
1. Tworzenie oddzielnych zlokalizowanych pakietów satelitarnych, postępuje zgodnie ze ścisłym zestawem konwencji.

Obie metody mają swoje zalety i wady, jak opisano w poniższych sekcjach.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Zlokalizowane zestawy zasobów w jednym pakiecie

Włączenie zlokalizowanych zestawów zasobów w jednym pakiecie jest zazwyczaj najprostszym podejściem. Aby to zrobić, należy `lib` utworzyć foldery w dla obsługiwanego języka innego niż domyślny pakiet (zakłada się, że en-us). W tych folderach można umieszczać zestawy zasobów i zlokalizowane pliki IntelliSense XML.

Na przykład: obsługa struktury folderów: niemiecki (de), włoski (it), japoński (ja), rosyjski (ru), chiński (uproszczony) (zh-Hans) i chiński (tradycyjny) (zh-Hant):

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

Widać, że wszystkie języki są wymienione `net40` poniżej folderu struktury docelowej. Jeśli [obsługujesz wiele struktur,](../create-packages/supporting-multiple-target-frameworks.md)masz folder w `lib` obszarze dla każdego wariantu.

Z tych folderów w miejscu, następnie odwołać się do wszystkich plików w : `.nuspec`

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

Jednym z przykładowych pakietów, który używa tego podejścia jest [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Zalety i wady (zlokalizowane zestawy zasobów)

Łączenie wszystkich języków w jednym pakiecie ma kilka wad:

1. **Udostępnione metadane:** Ponieważ pakiet NuGet `.nuspec` może zawierać tylko jeden plik, można podać metadane tylko dla jednego języka. Oznacza to, że NuGet nie przedstawia obsługi zlokalizowanych metadanych.
1. **Rozmiar pakietu:** W zależności od liczby obsługiwanych języków biblioteka może stać się znacznie duża, co spowalnia instalowanie i przywracanie pakietu.
1. **Jednoczesne wydania:** Łączenie zlokalizowanych plików w jeden pakiet wymaga jednoczesnego zwolnienia wszystkich zasobów w tym pakiecie, a nie możliwości osobnego wydania każdej lokalizacji. Ponadto każda aktualizacja dowolnej lokalizacji wymaga nowej wersji całego pakietu.

Jednak, ma również kilka korzyści:

1. **Prostota:** Konsumenci pakietu otrzymują wszystkie obsługiwane języki w jednej instalacji, zamiast instalować każdy język oddzielnie. Pojedynczy pakiet jest również łatwiej znaleźć na nuget.org.
1. **Wersje sprzężone:** Ponieważ wszystkie zestawy zasobów znajdują się w tym samym pakiecie co zestaw podstawowy, wszystkie mają ten sam numer wersji i nie są narażone na błędne oddzielenie.

## <a name="localized-satellite-packages"></a>Zlokalizowane pakiety satelitarne

Podobnie jak program .NET Framework obsługuje zestawy satelityczne, ta metoda oddziela zlokalizowane zasoby i pliki IntelliSense XML do pakietów satelitarnych.

W tym celu pakiet podstawowy używa konwencji `{identifier}.{version}.nupkg` nazewnictwa i zawiera zestaw dla języka domyślnego (na przykład en-US). Na przykład `ContosoUtilities.1.0.0.nupkg` może zawierać następującą strukturę:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Następnie zestaw satelitów używa `{identifier}.{language}.{version}.nupkg`konwencji `ContosoUtilities.de.1.0.0.nupkg`nazewnictwa, takiej jak . Identyfikator musi dokładnie **odpowiadać** identyfikatorowi pakietu podstawowego.

Ponieważ jest to oddzielny pakiet, `.nuspec` ma swój własny plik, który zawiera zlokalizowane metadane. Należy pamiętać, że `.nuspec` język w **musi odpowiadać** język używany w nazwa pliku.

Zestaw satelickiego musi również **zadeklarować** dokładną wersję pakietu podstawowego jako zależność, używając notacji [] wersji (zobacz [Przechowywanie wersji pakietu).](../concepts/package-versioning.md) Na przykład `ContosoUtilities.de.1.0.0.nupkg` musi zadeklarować `ContosoUtilities.1.0.0.nupkg` zależność `[1.0.0]` przy użyciu notacji. Pakiet satelitarny może oczywiście mieć inny numer wersji niż pakiet podstawowy.

Struktura pakietu satelitarnego musi następnie zawierać zestaw zasobów i plik XML IntelliSense w podfolderze, który pasuje `{language}` do nazwy pliku pakietu:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Uwaga:** o ile określone subkultury, takie jak `ja-JP` są konieczne, `ja`zawsze należy używać identyfikatora języka wyższego poziomu, takiego jak .

W zestawie satelicie NuGet rozpozna **tylko** te pliki `{language}` w folderze, który pasuje do nazwy pliku w. Wszystkie inne są ignorowane.

Po spełnieniu wszystkich tych konwencji, NuGet rozpozna pakiet jako pakiet satelitarny i zainstaluje `lib` zlokalizowane pliki w folderze pakietu podstawowego, tak jakby zostały pierwotnie dołączone. Odinstalowanie pakietu satelitarnego spowoduje usunięcie jego plików z tego samego folderu.

Należy utworzyć dodatkowe zestawy satelickie w taki sam sposób dla każdego obsługiwanego języka. Na przykład sprawdź zestaw ASP.NET pakietów MVC:

- [Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (angielski podstawowy)
- [Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (niemiecki)
- [Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japoński)
- [Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (chiński (uproszczony))
- [Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (chiński (tradycyjny))

### <a name="summary-of-required-conventions"></a>Podsumowanie wymaganych konwencji

- Pakiet podstawowy musi mieć nazwę`{identifier}.{version}.nupkg`
- Pakiet satelitarny musi być nazwany`{identifier}.{language}.{version}.nupkg`
- Pakiet satelitarny `.nuspec` musi określać jego język, aby dopasować nazwę pliku.
- Pakiet satelitarny musi zadeklarować zależność od dokładnej wersji podstawowej `.nuspec` przy użyciu notacji [] w jego pliku. Zakresy nie są obsługiwane.
- Pakiet satelitarny musi umieszczać pliki w folderze, `lib\[{framework}\]{language}` który dokładnie pasuje `{language}` do nazwy pliku.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Zalety i wady (pakiety satelitarne)

Korzystanie z pakietów satelitarnych ma kilka zalet:

1. **Rozmiar pakietu:** Ogólny rozmiar pakietu podstawowego jest zminimalizowany, a konsumenci ponoszą tylko koszty każdego języka, którego chcą użyć.
1. **Oddzielne metadane:** Każdy pakiet `.nuspec` satelitarny ma swój własny plik, a tym samym własne zlokalizowane metadane, ponieważ. Dzięki temu niektórzy konsumenci mogą łatwiej znaleźć pakiety, wyszukując nuget.org z zlokalizowanych terminów.
1. **Wydania odłączone:** Zestawy satelitarne mogą być zwalniane w czasie, a nie wszystkie naraz, co pozwala na rozłożenie wysiłków związanych z lokalizacją.

Jednak pakiety satelitarne mają swój własny zestaw wad:

1. **Mało istotne:** Zamiast pojedynczego pakietu, masz wiele pakietów, które mogą prowadzić do zaśmieconych wyników wyszukiwania na nuget.org i długą listę odwołań w projekcie programu Visual Studio.
1. **Ścisłe konwencje**. Pakiety satelitarne muszą dokładnie przestrzegać konwencji lub zlokalizowane wersje nie zostaną prawidłowo odebrane.
1. **Przechowywanie wersji:** Każdy pakiet satelitarny musi mieć dokładną zależność wersji od pakietu podstawowego. Oznacza to, że aktualizacja pakietu podstawowego może wymagać aktualizacji wszystkich pakietów satelitarnych, nawet jeśli zasoby nie zostały zmienić.
