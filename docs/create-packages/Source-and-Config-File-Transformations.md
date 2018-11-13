---
title: Przekształcenia pliku źródłowego i konfiguracji dla pakietów NuGet
description: Szczegółowe informacje na możliwość pakiety NuGet umożliwiające przekształcanie kodu źródłowego i konfiguracji plików (XML), podczas instalacji.
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 830714269ac422a4784c15b000e374195f02332f
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580288"
---
# <a name="transforming-source-code-and-configuration-files"></a>Przekształcanie plików źródłowych kodu i konfiguracji

Dla projektów przy użyciu `packages.config`NuGet obsługuje możliwość przekształcenia do kodu źródłowego i plików konfiguracji w pakiecie instalowania i odinstalowywania razy. Tylko przekształceń kodu źródłowego są stosowane, gdy pakiet jest zainstalowany w projekcie za pomocą [PackageReference](../consume-packages/package-references-in-project-files.md).

A **źródła kodu transformacji** jednokierunkowe zastępowania tokenu jest stosowana do plików w pakiecie `content` lub `contentFiles` folder (`content` dla klientów korzystających z `packages.config` i `contentFiles` dla `PackageReference`) po zainstalowaniu pakietu, gdy tokeny odnoszą się do programu Visual Studio [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Dzięki temu można wstawić plik do projektu przestrzeni nazw lub dostosować program code, zwykle będą przekazywane do `global.asax` w projektach programu ASP.NET.

A **transformacji pliku config** umożliwia modyfikowanie plików, które już istnieją w docelowej projektu, taki jak `web.config` i `app.config`. Na przykład pakiet może być konieczne dodanie elementu do `modules` sekcji w pliku konfiguracji. Ta transformacja odbywa się przy tym specjalnych plików w pakiecie, który opisano w sekcjach, aby dodać do plików konfiguracji. Gdy pakiet zostanie odinstalowany, te same zmiany są następnie wycofać, zastosowania dwukierunkowe transformacji.

## <a name="specifying-source-code-transformations"></a>Określanie przekształceń kodu źródłowego

1. Pliki, które ma zostać wstawiony z pakietu do projektu muszą znajdować się w ramach pakietu `content` i `contentFiles` folderów. Na przykład, jeśli chcesz, aby plik o nazwie `ContosoData.cs` ma być zainstalowany w `Models` folder docelowy projekt, należy go wewnątrz `content\Models` i `contentFiles\{lang}\{tfm}\Models` folderów w pakiecie.

1. Aby nakazać pakietu NuGet, aby zastosować zastępowania tokenu w czasie instalacji, należy dołączyć `.pp` do nazwy pliku kodu źródłowego. Po zakończeniu instalacji, plik nie będzie miał `.pp` rozszerzenia.

    Na przykład, aby wprowadzić przekształcenia w `ContosoData.cs`, nazwę pliku w pakiecie `ContosoData.cs.pp`. Po zakończeniu instalacji zostanie wyświetlony jako `ContosoData.cs`.

1. W pliku kodu źródłowego, należy użyć tokenów bez uwzględniania wielkości liter w postaci `$token$` do wskazywania wartości tego NuGet należy zastąpić właściwości projektu:

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    Po instalacji, zastępuje NuGet `$rootnamespace$` z `Fabrikam` zakładając, że projekt docelowy użytkownika, którego główna przestrzeń nazw jest `Fabrikam`.

`$rootnamespace$` Token jest właściwość projektu najczęściej używanych; wszystkie inne są wymienione w [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Można je na uwadze, oczywiście, że niektóre właściwości mogą być specyficzne dla typu projektu.

## <a name="specifying-config-file-transformations"></a>Określanie przekształcenia pliku konfiguracji

Zgodnie z opisem w kolejnych sekcjach, przekształcenia pliku konfiguracji można zrobić na dwa sposoby:

- Obejmują `app.config.transform` i `web.config.transform` pliki do pakietu `content` folderu, gdzie `.transform` rozszerzenie informuje NuGet, że te pliki zawierają kod XML w celu scalenia z istniejącymi plikami konfiguracji, gdy pakiet jest zainstalowany. Po odinstalowaniu pakietu tego samego XML jest usuwany.
- Obejmują `app.config.install.xdt` i `web.config.install.xdt` pliki do pakietu `content` folderze przy użyciu [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx) do opisania żądane zmiany. Po wybraniu tej opcji możesz również uwzględnić `.uninstall.xdt` plik, aby cofnąć zmiany, gdy pakiet zostanie usunięty z projektu.

> [!Note]
> Przekształcenia nie są stosowane do `.config` pliki określany jako link w programie Visual Studio.

Zaletą używania XDT jest zamiast po prostu scalanie dwa pliki statyczne, składni do manipulowania strukturę modelu DOM języka XML przy użyciu element i atrybut dopasowania, dzięki pełnej obsłudze XPath. XDT można następnie dodać, zaktualizować, lub usuń elementy, umieszczać nowe elementy w określonej lokalizacji lub Zamień lub usuń elementy (łącznie z węzłów podrzędnych). Dzięki temu prosta do utworzenia Odinstaluj przekształceń, które wycofać wszystkie przekształcenia zrobić podczas instalacji pakietu aktualizacji.

### <a name="xml-transforms"></a>Transformacje XML

`app.config.transform` i `web.config.transform` w pakiecie `content` folder zawierają tylko te elementy, aby scalić istniejący projekt `app.config` i `web.config` plików.

Na przykład załóżmy, że projekt zawiera początkowo następującą zawartość w `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Aby dodać `MyNuModule` elementu `modules` sekcji podczas instalowania pakietu, należy utworzyć `web.config.transform` pliku do pakietu `content` folder, który wygląda w następujący sposób:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Po NuGet instaluje pakiet `web.config` pojawi się w następujący sposób:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Należy zauważyć, że nie zastąpić NuGet `modules` sekcji ją po prostu połączone nowy wpis do niego przez dodanie tylko nowych elementów i atrybutów. NuGet nie ulegnie zmianie, wszystkie istniejące elementy lub atrybuty.

Po odinstalowaniu pakietu NuGet zbada `.transform` pliki ponownie i usuwania elementów zawiera odpowiednie `.config` plików. Należy pamiętać, że ten proces nie wpłynie na wszystkie wiersze w `.config` pliku, który modyfikujesz po zakończeniu instalacji pakietu.

Przykład bardziej rozległe [moduły rejestrowania błędów i obsługi platformy ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) pakiet dodaje wiele wpisów w `web.config`, które ponownie zostały usunięte po odinstalowaniu pakietu.

Zbadanie jego `web.config.transform` plik, Pobierz pakiet ELMAH spod linku powyżej, zmień rozszerzenie pakietu z `.nupkg` do `.zip`, a następnie otwórz `content\web.config.transform` w tym pliku ZIP.

Aby zobaczyć efekt Instalowanie i odinstalowywanie pakietu, Utwórz nowy projekt ASP.NET w programie Visual Studio (szablon znajduje się w **Visual C# > sieci Web** w oknie dialogowym Nowy projekt) i wybierz pozycję pusta aplikacja platformy ASP.NET. Otwórz `web.config` Aby wyświetlić jego stan początkowy. Kliknij prawym przyciskiem myszy projekt, wybierz **Zarządzaj pakietami NuGet**, Przeglądaj w poszukiwaniu biblioteki ELMAH w witrynie nuget.org i zainstaluj najnowszą wersję. Zwróć uwagę, wszystkie zmiany do `web.config`. Teraz odinstalować pakiet i zostanie wyświetlony `web.config` powrócić do poprzedniego stanu.

### <a name="xdt-transforms"></a>Przekształca XDT

Można zmodyfikować plików konfiguracji przy użyciu [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx). Mogą też istnieć NuGet zamienić tokeny przy użyciu [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) , łącznie z nazwą właściwości w ramach `$` ograniczniki (bez uwzględniania wielkości liter).

Na przykład następująca `app.config.install.xdt` pliku zostanie wstawiona `appSettings` elementu do `app.config` zawierający `FullPath`, `FileName`, i `ActiveConfigurationSettings` wartości z projektu:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

Inny przykład, załóżmy, że projekt zawiera początkowo następującą zawartość w `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Aby dodać `MyNuModule` elementu `modules` sekcji podczas pakietu instalacji pakietu `web.config.install.xdt` będzie zawierał następujące:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

Po zainstalowaniu pakietu, `web.config` będzie wyglądać następująco:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Aby usunąć tylko `MyNuModule` elementu podczas odinstalowywania pakietu `web.config.uninstall.xdt` plik powinien zawierać następujące czynności:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
