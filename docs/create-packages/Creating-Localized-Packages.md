---
title: Tworzenie zlokalizowanego pakietu NuGet
description: Szczegółowe informacje na dwa sposoby tworzenia zlokalizowanych pakietów NuGet, w tym wszystkie zestawy w jednym pakiecie lub publikowania oddzielne zestawy.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: b1c2511c1fbafc7f52029c23521fa55671b0b5c5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546898"
---
# <a name="creating-localized-nuget-packages"></a>Tworzenie zlokalizowanych pakietów NuGet

Istnieją dwa sposoby tworzenia zlokalizowane wersje biblioteki:

1. Obejmują wszystkie zestawy zlokalizowanych zasobów w jednym pakiecie.
1. Tworzenie pakietów oddzielne satelitarnej zlokalizowane postępując zgodnie z ograniczeniami zbiór konwencji.

Obie metody mają swoje zalety i wady, zgodnie z opisem w poniższych sekcjach.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Zestawów zlokalizowanych zasobów w jednym pakiecie

Dołączenie zestawów zlokalizowanych zasobów w jednym pakiecie zwykle jest najprostsza metoda. Aby to zrobić, należy utworzyć foldery znajdujące się w `lib` obsługiwanych języka innego niż domyślny pakiet (założono, że to en-us). W tych folderach można umieścić zestawów zasobów i zlokalizowane pliki XML w technologii IntelliSense.

Na przykład następującą strukturę folderów obsługuje, niemiecki (de), włoski (on), japoński (ja), rosyjski (ru), chiński (uproszczony) (zh-Hans) i chiński (tradycyjny) (zh-Hant):

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

Widać, że języki są wszystkie wymienione poniżej `net40` folder struktury docelowej. Jeśli jesteś [Obsługa wielu platform](../create-packages/supporting-multiple-target-frameworks.md), wówczas masz folder w obszarze `lib` każdego wariantu.

Za pomocą tych folderów w miejscu, następnie odwołać wszystkie pliki w Twojej `.nuspec`:

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

Jeden pakiet przykładowy, który korzysta z tej metody jest [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Zalety i wady (zlokalizowany zasób zestawów)

Tworzenie pakietów we wszystkich językach, w jednym pakiecie ma kilka wady:

1. **Udostępnione metadanych**: ponieważ pakietu NuGet może zawierać tylko jeden `.nuspec` pliku, możesz podać metadanych tylko jeden język. Oznacza to, że w NuGet nie są wyświetlane obsługuje zlokalizowanych metadanych.
1. **Rozmiar pakietu**: w zależności od liczby obsługiwanych języków, biblioteka może stać się znacznie dużych który spowalnia, instalowania i przywracania pakietu.
1. **Wersje równoczesne**: tworzenie pakietów zlokalizowane pliki w jednym pakiecie wymaga wersji wszystkie zasoby w tym pakiecie jednocześnie, a nie jak zdołaliśmy oddzielnie każdej lokalizacji. Ponadto wszelkich aktualizacji żadnych jednej lokalizacji wymaga nowej wersji cały pakiet.

Jednak także ma kilka zalet:

1. **Prostota**: konsumentów pakietu Pobierz wszystkie obsługiwane języki w pojedyncza instalacja, niż musieć go zainstalować osobno każdy język. Pojedynczy pakiet jest również łatwiej znaleźć w witrynie nuget.org.
1. **Powiązane wersje**: ponieważ wszystkie zestawy zasobów znajdują się w tym samym pakiecie jako podstawowego zestawu, wszystkie mają ten sam numer wersji i nie należy uruchamiać ryzyka błędnego wprowadzenie odłączone.

## <a name="localized-satellite-packages"></a>Satelitarne zlokalizowanych pakietów

Podobnie jak program .NET Framework obsługuje zestawów satelickich, ta metoda oddziela zlokalizowanych zasobów i plików IntelliSense XML w pakiety satelity.

Czy do tego, pakiet podstawowego używa konwencji nazewnictwa `{identifier}.{version}.nupkg` i zawiera zestaw dla języka domyślnego (np. en US). Na przykład `ContosoUtilities.1.0.0.nupkg` będzie zawierał następującą strukturę:

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

Następnie zestawu satelickiego używa konwencji nazewnictwa `{identifier}.{language}.{version}.nupkg`, takich jak `ContosoUtilities.de.1.0.0.nupkg`. Identyfikator **musi** dokładnie odpowiadać pakiet główny.

Ponieważ oddzielny pakiet ma swoje własne `.nuspec` pliku, który zawiera zlokalizowane metadanych. Można je na uwadze, język, w `.nuspec` **musi** zgodne z działaniem używanym w nazwie pliku.

Zestawu satelickiego **musi** deklarować dokładnej wersji głównej pakietu także jako zależności, przy użyciu notacji wersji [] \(zobacz [wersji pakietu](../reference/package-versioning.md)). Na przykład `ContosoUtilities.de.1.0.0.nupkg` należy zadeklarować zależność w `ContosoUtilities.1.0.0.nupkg` przy użyciu `[1.0.0]` notacji. Pakiet satelitarnej oczywiście mogą mieć numer wersji innej niż pakiet główny.

Struktura pakietu satelitarnej następnie mogą zawierać zestaw zasobów i plik XML IntelliSense w podfolderze, który odpowiada `{language}` w nazwie pliku pakietu:

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

**Uwaga**: chyba że określone podhodowli, takie jak `ja-JP` są niezbędne, zawsze używaj wyższe identyfikatora języka poziomu, takie jak `ja`.

W zestawie satelickim rozpozna NuGet **tylko** tych plików w folderze, który odpowiada `{language}` w nazwie pliku. Wszystkie pozostałe są ignorowane.

Po spełnieniu wszystkich tych konwencji NuGet rozpozna pakietu jako pakiet satelitarne i instalowanie zlokalizowanych plików w pakiecie głównej `lib` folderze tak, jakby były one pierwotnie powiązane. Odinstalowywanie pakietu satelitarnej spowoduje usunięcie jej pliki z tym samym folderze.

Należy utworzyć dodatkowe zestawy satelickie w taki sam sposób dla każdego z obsługiwanych języków. Na przykład sprawdzić zestaw pakietów platformy ASP.NET MVC:

- [Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (podstawowy w języku angielskim)
- [Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (wersja niemiecka)
- [Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)
- [Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))
- [Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))

### <a name="summary-of-required-conventions"></a>Podsumowanie konwencje wymagane

- Pakiet główny musi mieć nazwę. `{identifier}.{version}.nupkg`
- Pakiet satelitarnej musi mieć nazwę. `{identifier}.{language}.{version}.nupkg`
- Pakiet satelitarnej `.nuspec` należy określić jego język, aby dopasować nazwę pliku.
- Pakiet satelitarnej należy zadeklarować zależność w dokładną wersję podstawową przy użyciu notacji [] w jego `.nuspec` pliku. Zakresy nie są obsługiwane.
- Pakiet satelitarnej należy umieścić pliki w `lib\[{framework}\]{language}` folder, który dokładnie pasuje `{language}` w nazwie pliku.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Zalety i wady (satelitarnej pakietów)

Za pomocą pakietów satelitarnej ma kilka zalet:

1. **Rozmiar pakietu**: całkowitego rozmiaru pakietu podstawowego jest zminimalizowany i konsumentów tylko pociągnąć za sobą koszty każdego języka, które mają być użyte.
1. **Oddzielne metadanych**: każdy pakiet satelitarnej ma swój własny `.nuspec` pliku, a zatem zlokalizowanych metadanych ponieważ. Dzięki temu części użytkowników łatwiej znaleźć pakiety, wyszukując nuget.org zlokalizowane warunki.
1. **Odłączone wersji**: zestawy satelickie może być zwolnione wraz z upływem czasu, a nie w całości, umożliwiając rozłożyć prace lokalizacji.

Jednak pakiety satelitarnej mają własne zestawy wady:

1. **Zaśmiecania**: zamiast jeden pakiet, masz wiele pakietów, które mogą prowadzić do dużej liczby wyników w witrynach nuget.org i długą listę odwołań w projekcie programu Visual Studio.
1. **Konwencje Strict**. Pakiety satelitarnej muszą dokładnie zgodne z konwencjami lub zlokalizowane wersje nie będą pobrane prawidłowo.
1. **Przechowywanie wersji**: każdy pakiet satelitarnej musi mieć zależność dokładnie wersji na pakiet główny. Oznacza to, że aktualizowanie pakietu głównej mogą wymagać aktualizacji wszystkich pakietów satelity, nawet wtedy, gdy zasoby nie został zmieniony.
