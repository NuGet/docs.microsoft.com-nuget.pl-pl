---
title: Jak utworzyć zlokalizowany pakiet NuGet
description: Szczegółowe informacje na temat dwóch sposobów tworzenia zlokalizowanych pakietów NuGet przy użyciu wszystkich zestawów w pojedynczym pakiecie lub publikowania oddzielnych zestawów.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: cb3f8a9df66f259b130996822f102c27636d5d2c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774748"
---
# <a name="creating-localized-nuget-packages"></a>Tworzenie zlokalizowanych pakietów NuGet

Istnieją dwa sposoby tworzenia zlokalizowanych wersji biblioteki:

1. Uwzględnij wszystkie zestawy zlokalizowanych zasobów w pojedynczym pakiecie.
1. Utwórz oddzielne, zlokalizowane pakiety satelickie, wykonując rygorystyczne zestawy Konwencji.

Obie metody mają swoje zalety i wady, zgodnie z opisem w poniższych sekcjach.

## <a name="localized-resource-assemblies-in-a-single-package"></a>Zlokalizowane zestawy zasobów w pojedynczym pakiecie

Uwzględnianie zlokalizowanych zestawów zasobów w pojedynczym pakiecie jest zazwyczaj najprostszym podejściem. W tym celu należy utworzyć foldery w programie `lib` dla obsługiwanego języka innego niż domyślny pakiet (założono, że jest to en-US). W tych folderach można umieścić zestawy zasobów i zlokalizowane pliki XML IntelliSense.

Na przykład następująca struktura folderów obsługuje, niemiecki (Niemcy), włoski (IT), japoński (ja), rosyjski (ru), chiński (uproszczony) (zh-Hans) i chiński (tradycyjny) (zh-Hant):

```
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
```

Można zobaczyć, że wszystkie języki są wymienione poniżej `net40` folderu platformy docelowej. Jeśli [obsługujesz wiele platform](../create-packages/supporting-multiple-target-frameworks.md), masz folder w obszarze `lib` dla każdego wariantu.

Po wprowadzeniu tych folderów odwołujesz się do wszystkich plików w `.nuspec` :

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

Jednym z przykładowych pakietów korzystających z tej metody jest [Microsoft. Data. OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a>Zalety i wady (zlokalizowane zestawy zasobów)

Zgrupowanie wszystkich języków w jednym pakiecie ma kilka wad:

1. **Udostępnione metadane**: ponieważ pakiet NuGet może zawierać tylko jeden `.nuspec` plik, można dostarczyć metadane tylko dla jednego języka. Oznacza to, że NuGet nie obsługuje zlokalizowanych metadanych.
1. **Rozmiar pakietu**: w zależności od liczby obsługiwanych języków biblioteka może stać się znacznie duża, co powoduje spowolnienie instalowania i przywracania pakietu.
1. **Równoczesne wersje**: umieszczenie zlokalizowanych plików w jednym pakiecie wymaga jednoczesnego zwolnienia wszystkich zasobów w tym pakiecie, a nie w celu wypróbowania poszczególnych lokalizacji oddzielnie. Ponadto każda aktualizacja w jednej lokalizacji wymaga nowej wersji całego pakietu.

Jednak ma ona również kilka korzyści:

1. **Prostota**: konsumenci pakietu uzyskują wszystkie obsługiwane języki w jednej instalacji, a nie muszą osobno instalować każdego języka. Jeden pakiet jest również łatwiejszy do znalezienia w witrynie nuget.org.
1. Powiązane **wersje**: ze względu na to, że wszystkie zestawy zasobów znajdują się w tym samym pakiecie co zestaw podstawowy, współużytkują one ten sam numer wersji i nie uruchamiają ryzyka błędnego oddzielenia.

## <a name="localized-satellite-packages"></a>Zlokalizowane pakiety satelickie

Podobnie jak .NET Framework obsługuje zestawy satelickie, ta metoda oddziela zlokalizowane zasoby i pliki XML IntelliSense do pakietów satelitarnych.

W tym celu pakiet podstawowy używa konwencji nazewnictwa `{identifier}.{version}.nupkg` i zawiera zestaw dla języka domyślnego (na przykład en-US). Na przykład `ContosoUtilities.1.0.0.nupkg` będzie zawierać następującą strukturę:

```
lib
└───net40
        ContosoUtilities.dll
        ContosoUtilities.xml
```

Zestaw satelity używa konwencji nazewnictwa `{identifier}.{language}.{version}.nupkg` , takiej jak `ContosoUtilities.de.1.0.0.nupkg` . Identyfikator **musi** być dokładnie zgodny z pakietem podstawowym.

Ponieważ jest to oddzielny pakiet, ma własny `.nuspec` plik, który zawiera zlokalizowane metadane. Należy mieć na uwadze, że język w `.nuspec` **musi** być zgodny z użytym w nazwie pliku.

Zestaw satelicki **musi** również deklarować dokładną wersję pakietu podstawowego jako zależność przy użyciu notacji wersji [] (zobacz [wersja pakietu](../concepts/package-versioning.md)). Na przykład, `ContosoUtilities.de.1.0.0.nupkg` należy zadeklarować zależność `ContosoUtilities.1.0.0.nupkg` przy użyciu `[1.0.0]` notacji. Pakiet satelitarny może mieć inny numer wersji niż pakiet podstawowy.

Struktura pakietu satelitarnego musi zawierać zestaw zasobów i plik IntelliSense XML w podfolderze, który pasuje do `{language}` nazwy pliku pakietu:

```
lib
└───net40
    └───de
            ContosoUtilities.resources.dll
            ContosoUtilities.xml
```

**Uwaga**: Jeśli określone podkultury, takie jak `ja-JP` są niezbędne, zawsze używają identyfikatora języka wyższego poziomu, takiego jak `ja` .

W zestawie satelity program NuGet rozpozna **tylko** te pliki w folderze, które pasują do `{language}` nazwy pliku. Wszystkie pozostałe są ignorowane.

Gdy zostaną spełnione wszystkie z tych konwencji, pakiet NuGet rozpoznaje go jako pakiet satelitarny i zainstaluje zlokalizowane pliki w folderze pakietu podstawowego `lib` , tak jakby były pierwotnie powiązane. Odinstalowanie pakietu satelickiego spowoduje usunięcie jego plików z tego samego folderu.

W ten sam sposób można utworzyć dodatkowe zestawy satelickie dla każdego obsługiwanego języka. Aby zapoznać się z przykładem, należy zapoznać się z zestawem pakietów ASP.NET MVC:

- [Microsoft. ASPNET. MVC](https://nuget.org/packages/Microsoft.AspNet.Mvc) (podstawowa wersja angielskojęzyczna)
- [Microsoft.ASPNET.MVC.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (niemiecki)
- [Microsoft. ASPNET. MVC. ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (japoński)
- [Microsoft. ASPNET. MVC. zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (chiński (uproszczony))
- [Microsoft. ASPNET. MVC. zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (chiński (tradycyjny))

### <a name="summary-of-required-conventions"></a>Podsumowanie wymaganych Konwencji

- Pakiet podstawowy musi mieć nazwę `{identifier}.{version}.nupkg`
- Pakiet satelitarny musi mieć nazwę `{identifier}.{language}.{version}.nupkg`
- Pakiet satelitarny `.nuspec` musi określać swój język, aby odpowiadał nazwie pliku.
- Pakiet satelitarny musi deklarować zależność dla dokładnej wersji elementu głównego przy użyciu notacji [] w `.nuspec` pliku. Zakresy nie są obsługiwane.
- Pakiet satelitarny musi umieścić pliki w `lib\[{framework}\]{language}` folderze, który dokładnie pasuje do `{language}` nazwy pliku.

### <a name="advantages-and-disadvantages-satellite-packages"></a>Zalety i wady (pakiety satelitarne)

Używanie pakietów satelitarnych ma kilka zalet:

1. **Rozmiar pakietu**: ogólny wpływ pakietu podstawowego jest zminimalizowany, a konsumenci ponoszą koszty każdego języka, którego chcą używać.
1. **Oddziel metadane**: każdy pakiet satelitarny ma własny `.nuspec` plik i dlatego jego własne zlokalizowane metadane. Może to ułatwić klientom łatwiejsze znajdowanie pakietów przez wyszukiwanie nuget.org przy użyciu zlokalizowanych warunków.
1. Rozdzielone **wersje**: zestawy satelickie mogą być uwalniane z upływem czasu, a nie tylko na raz, co pozwala rozłożyć działania dotyczące lokalizacji.

Jednak pakiety satelickie mają swój własny zestaw wad:

1. **Bałaganie**: zamiast pojedynczego pakietu masz wiele pakietów, które mogą prowadzić do nieczytelnych wyników wyszukiwania na NuGet.org i długiej listy odwołań w projekcie programu Visual Studio.
1. **Ścisłe konwencje**. Pakiety satelickie muszą być zgodne z konwencjami dokładnie lub zlokalizowane wersje nie będą prawidłowo pobierane.
1. **Przechowywanie wersji**: każdy pakiet satelitarny musi mieć dokładną zależność wersji w pakiecie podstawowym. Oznacza to, że aktualizacja pakietu podstawowego może wymagać aktualizacji wszystkich pakietów satelitarnych, nawet jeśli zasoby nie uległy zmianie.
