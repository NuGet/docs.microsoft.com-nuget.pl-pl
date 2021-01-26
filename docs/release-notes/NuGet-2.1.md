---
title: Informacje o wersji narzędzia NuGet 2,1
description: Informacje o wersji programu NuGet 2,1, w tym znane problemy, poprawki błędów, dodane funkcje i DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777031"
---
# <a name="nuget-21-release-notes"></a>Informacje o wersji narzędzia NuGet 2,1

Informacje o wersji narzędzia [NuGet 2,0](../release-notes/nuget-2.0.md)  |  [Informacje o wersji narzędzia NuGet 2,2](../release-notes/nuget-2.2.md)

Pakiet NuGet 2,1 został wydaną 4 października 2012.

## <a name="hierarchical-nugetconfig"></a>Nuget.Config hierarchiczne

Pakiet NuGet 2,1 zapewnia większą elastyczność kontrolowania ustawień NuGet w drodze cyklicznego powiększania struktury folderów szukających `NuGet.Config` plików, a następnie tworzenia konfiguracji z zestawu wszystkich odnalezionych plików.  Przykładowo Rozważmy scenariusz, w którym zespół ma wewnętrzne repozytorium pakietów dla kompilacji CI innych zależności wewnętrznych. Struktura folderów dla pojedynczego projektu może wyglądać następująco:

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

Ponadto jeśli dla rozwiązania włączono funkcję przywracania pakietów, istnieje również następujący folder:

```
C:\myteam\solution1\.nuget
```

Aby można było udostępnić wewnętrzne repozytorium pakietów dla wszystkich projektów, na których pracuje zespół, bez udostępniania go dla każdego projektu na komputerze, możemy utworzyć nowy plik Nuget.Config i umieścić go w folderze c:\myteam. Nie istnieje sposób, aby określony folder pakietów dla projektu.

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

Teraz możemy zobaczyć, że źródło zostało dodane przez uruchomienie polecenia "nuget.exe sources" z dowolnego folderu poniżej c:\myteam, jak pokazano poniżej:

![Źródła pakietów z konfiguracji nadrzędnej programu NuGet](./media/releasenotes-21-cfg-hierarchy.png)

`NuGet.Config` pliki są wyszukiwane w następującej kolejności:

1. `.nuget\Nuget.Config`
2. Przechodzenie cykliczne z folderu projektu do katalogu głównego
3. Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )

Konfiguracje są stosowane w *odwrotnej kolejności*, co oznacza, że na podstawie powyższego porządku zostanie najpierw zastosowana globalna Nuget.Config, a następnie odnalezione pliki Nuget.Config z katalogu głównego do folderu projektu, a następnie `.nuget\Nuget.Config` .  Jest to szczególnie ważne, jeśli używasz `<clear/>` elementu do usuwania zestawu elementów z konfiguracji.

## <a name="specify-packages-folder-location"></a>Określ lokalizację folderu "Packages"

W przeszłości program NuGet zarządzał pakietami rozwiązań z znanego folderu "Packages" znajdującego się pod folderem głównym rozwiązania.  W przypadku zespołów programistycznych, które mają wiele różnych rozwiązań z zainstalowanymi pakietami NuGet, może to spowodować zainstalowanie tego samego pakietu w wielu różnych miejscach w systemie plików.

Program NuGet 2,1 zapewnia bardziej szczegółową kontrolę nad lokalizacją folderu Packages za pośrednictwem `repositoryPath` elementu w `NuGet.Config` pliku.  Korzystając z powyższego przykładu wsparcia Nuget.Config hierarchicznego, założono, że wszystkie projekty w obszarze C:\myteam\ korzystają z tego samego folderu Packages.  Aby to osiągnąć, po prostu Dodaj następujący wpis do `c:\myteam\Nuget.Config` .

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

W tym przykładzie udostępniony `Nuget.Config` plik określa folder pakietów udostępnionych dla każdego projektu, który jest tworzony pod C:\myteam, bez względu na głębokość. Należy pamiętać, że jeśli masz folder pakietów znajdujący się pod elementem głównym rozwiązania, musisz go usunąć, zanim pakiet NuGet umieści pakiety w nowej lokalizacji.

## <a name="support-for-portable-libraries"></a>Obsługa bibliotek przenośnych

[Biblioteki przenośne](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) to funkcja, która została wprowadzona najpierw z platformą .NET 4, która umożliwia tworzenie zestawów, które mogą współdziałać bez modyfikacji na różnych platformach firmy Microsoft, od wersji The.NET Framework do Silverlight do Windows Phone i nawet dla konsoli Xbox 360  Rozszerzając [konwencje pakietu](../create-packages/supporting-multiple-target-frameworks.md) dla wersji i profilów struktury, program NuGet 2,1 obsługuje teraz przenośne biblioteki, umożliwiając tworzenie pakietów, które mają foldery programu złożonej struktury i profil docelowy `lib` .

Rozważmy na przykład następujące Platformy docelowe dostępne w bibliotece klas przenośnych.

![Okno dialogowe tworzenia biblioteki przenośnej](./media/releasenotes-21-plib.png)

Po skompilowaniu biblioteki i `nuget.exe pack MyPortableProject.csproj` uruchomieniu polecenia można zobaczyć nową strukturę folderu przenośnego pakietu biblioteki, sprawdzając zawartość wygenerowanego pakietu NuGet.

![Układ pakietu biblioteki przenośnej](./media/releasenotes-21-plib-layout.png)

Jak widać, konwencja nazw folderu biblioteki przenośnej jest zgodna ze wzorcem "Portable-{Framework 1} + {Framework n}", w której identyfikatory struktury są zgodne z istniejącymi [nazwami i konwencjami dotyczącymi wersji platformy](../reference/target-frameworks.md). Jeden wyjątek od konwencji nazw i wersji znajduje się w identyfikatorze platformy używanym do Windows Phone.  Moniker powinien używać nazwy platformy "wp" (WP7, wp71 lub WP8). Na przykład przy użyciu polecenia "Silverlight-WP7" spowoduje to wystąpienie błędu.

Podczas instalowania pakietu, który jest tworzony na podstawie tej struktury folderów, pakiet NuGet może teraz zastosować jego strukturę i reguły profilu do wielu obiektów docelowych, jak określono w nazwie folderu.  Za reguły dopasowywania narzędzia NuGet jest zasada, że "bardziej specyficzne" cel będzie miał pierwszeństwo przed "mniej konkretnymi".  Oznacza to, że monikere ukierunkowane na konkretną platformę zawsze są preferowane w przypadku urządzeń przenośnych, jeśli są one zgodne z projektem.  Ponadto jeśli wiele przenośnych obiektów docelowych jest zgodnych z projektem, pakiet NuGet woli, że zestaw obsługiwanych platform jest "najbliższy" w projekcie odwołującym się do pakietu.

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a>Ukierunkowane projekty systemu Windows 8 i Windows Phone 8

Oprócz dodawania obsługi docelowych projektów bibliotek, program NuGet 2,1 udostępnia nowe monikery struktury dla projektów systemu Windows 8 i Windows Phone 8, a także kilka nowych ogólnych monikerów dla projektów sklepu Windows i Windows Phone, które będą łatwiejsze do zarządzania w przyszłych wersjach odpowiednich platform.

W przypadku aplikacji ze sklepu Windows 8 identyfikatory wyglądają następująco:

| Pakiet NuGet 2,0 i wcześniejsze | NuGet 2.1 |
| ---------------- | ----------- |
| winRT45, . NETCore45 | Windows, Windows8, win, Win8 |

<br/>
W przypadku projektów Windows Phone identyfikatory wyglądają następująco:

| Telefon SYSTEMowy | Pakiet NuGet 2,0 i wcześniejsze | NuGet 2.1 |
| --- | --- | --- |
| Windows Phone 7 | silverlight3-WP | WP, WP7, WindowsPhone, WindowsPhone7 |
| Windows Phone 7,5 (mango) | silverlight4-wp71 | wp71, WindowsPhone71 |
| Windows Phone 8 | (nieobsługiwane) | WP8, WindowsPhone8 |

<br/>
We wszystkich powyższych zmianach nazwy starych struktur będą nadal w pełni obsługiwane przez program NuGet 2,1.  Po przeniesieniu do przodu nowe nazwy powinny być używane, ponieważ będą bardziej stabilne w przyszłych wersjach odpowiednich platform. Nowe nazwy *nie* będą obsługiwane w wersjach programu NuGet wcześniejszych niż 2,1, dlatego należy zaplanować odpowiednie dla momentu przełączenia.

## <a name="improved-search-in-package-manager-dialog"></a>Ulepszone wyszukiwanie w oknie dialogowym Menedżera pakietów

W ciągu ostatnich kilku iteracji wprowadzono zmiany w galerii NuGet, które znacznie poprawiły szybkość i przydatność wyszukiwania pakietów.  Jednak te ulepszenia zostały ograniczone do witryny sieci Web nuget.org.  Pakiet NuGet 2,1 zapewnia udoskonalone środowisko wyszukiwania dostępne za pomocą okna dialogowego Menedżera pakietów NuGet.  Załóżmy na przykład, że chcesz znaleźć pakiet zapoznawczy usługi Windows Azure w wersji zapoznawczej.  Odpowiednie zapytanie wyszukiwania dla tego pakietu może być "Azure cache".  W poprzednich wersjach okna dialogowego Menedżera pakietów żądany pakiet nie będzie nawet wyświetlany na pierwszej stronie wyników.  Jednak w programie NuGet 2,1 żądany pakiet jest teraz wyświetlany w górnej części wyników wyszukiwania.

![Wyszukiwanie okna dialogowego Menedżera pakietów](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a>Wymuś aktualizację pakietu

Przed pakietem NuGet 2,1, pakiet NuGet pominie aktualizację pakietu, gdy nie jest dostępny żaden wysoki numer wersji.  W przypadku niektórych scenariuszy — w szczególności w przypadku scenariuszy kompilacji lub tworzenia, w których zespół nie chce zwiększyć numeru wersji pakietu przy każdej kompilacji.  Odpowiednie zachowanie miało wymusić aktualizację bez względu na to, co.  Pakiet NuGet 2,1 dotyczy tej flagi z flagą "Zainstaluj ponownie".  Na przykład poprzednie wersje programu NuGet spowodują następujące próby zaktualizowania pakietu, który nie miał nowszej wersji pakietu:

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

Przy użyciu flagi reinstall pakiet zostanie zaktualizowany niezależnie od tego, czy jest dostępna nowsza wersja.

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

Innym scenariuszem, w którym flaga ponownej instalacji udowadnia korzystne znaczenie, jest zmiana struktury. W przypadku zmiany platformy docelowej projektu (na przykład z programu .NET 4 do programu .NET 4,5) Update-Package-reinstall można zaktualizować odwołania do odpowiednich zestawów dla wszystkich pakietów NuGet zainstalowanych w projekcie.

## <a name="edit-package-sources-within-visual-studio"></a>Edytowanie źródeł pakietów w programie Visual Studio

W poprzednich wersjach programu NuGet aktualizowanie źródła pakietu z poziomu okna dialogowego Opcje programu Visual Studio wymagało usunięcia i ponownego dodania źródła pakietu.  Pakiet NuGet 2,1 usprawnia ten przepływ pracy, obsługując aktualizację jako pierwszą funkcję klasy interfejsu użytkownika konfiguracji.

![Okno dialogowe konfiguracji Menedżera pakietów](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a>Poprawki błędów

Pakiet NuGet 2,1 zawiera wiele poprawek błędów. Aby zapoznać się z pełną listą elementów roboczych ustalonych w programie NuGet 2,0, zobacz [Śledzenie problemów NuGet dla tej wersji](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
