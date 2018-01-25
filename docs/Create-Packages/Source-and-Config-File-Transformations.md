---
title: "Źródło i konfiguracji pliku przekształcenia pakietów NuGet | Dokumentacja firmy Microsoft"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Szczegóły możliwości pakietów NuGet do przekształcania kodu źródłowego i konfiguracji plików (XML) podczas instalacji."
keywords: "Instalacja pakietu NuGet, przekształcenia pakietu NuGet, modyfikowanie plików konfiguracyjnych, modyfikowania kodu źródłowego"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 1340e8440c62f8037c931667c6e2f7fc9d1590c4
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/25/2018
---
# <a name="transforming-source-code-and-configuration-files"></a>Przekształcanie plików źródłowych kodem i konfiguracją

Dla projektów przy użyciu `packages.config`NuGet obsługuje możliwość przekształcenia do kodu źródłowego i plików konfiguracji w pakiecie instalowania i odinstalowywania razy. Przekształcenia nie są stosowane, gdy pakiet jest zainstalowany w projekcie przy użyciu [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md).

A **źródła kodu transformacji** jednokierunkowe zastępujący tokenu jest stosowana do plików w pakiecie `content` folderu, gdy pakiet jest zainstalowany, gdy tokeny odnoszą się do programu Visual Studio [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) . Dzięki temu można wstawić plik do projektu przestrzeni nazw lub Dostosuj kod, który zazwyczaj przejdzie do `global.asax` w projekcie programu ASP.NET.

A **transformacji pliku config** umożliwia modyfikowanie plików, które już istnieją w projekcie docelowym, takich jak `web.config` i `app.config`. Na przykład pakiet może być konieczne dodanie elementu `modules` sekcji w pliku konfiguracji. Ta transformacja odbywa się przy tym specjalne pliki w pakiecie, który opisano sekcjach, aby dodać do plików konfiguracji. Po odinstalowaniu pakietu te same zmiany są następnie wycofać, co to dwukierunkowe przekształcania.

## <a name="specifying-source-code-transformations"></a>Określanie przekształcenia kodu źródłowego

1. Pliki, które ma zostać wstawiony z pakietu w projekcie musi znajdować się w pakiecie `content` folderu. Na przykład, jeśli chcesz, aby plik o nazwie `ContosoData.cs` ma być zainstalowany w `Models` folder docelowy projekt, musi znajdować się wewnątrz `content\Models` folderu w pakiecie.

1. Aby nakazać NuGet, aby zastosować zastępujący tokenu w czasie instalacji, należy dołączyć `.pp` nazwy pliku kodu źródłowego. Po zakończeniu instalacji, nie ma pliku `.pp` rozszerzenia.

    Na przykład, aby dokonać przekształcenia w `ContosoData.cs`, nazwa pliku w pakiecie `ContosoData.cs.pp`. Po zakończeniu instalacji zostanie wyświetlony jako `ContosoData.cs`.

1. W pliku kodu źródłowego za pomocą tokenów bez uwzględniania wielkości liter w postaci `$token$` wartości tego NuGet należy zastąpić właściwości projektu:

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

    Podczas instalacji, zastępuje NuGet `$rootnamespace$` z `Fabrikam` przy założeniu projektu docelowego obiektu, którego przestrzeń nazw głównego `Fabrikam`.

`$rootnamespace$` Token jest właściwość projektu najczęściej używane; pozostałe są wymienione w [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Można, mając na uwadze, że niektóre właściwości mogą być specyficzne dla typu projektu.

## <a name="specifying-config-file-transformations"></a>Określenie konfiguracji pliku przekształcenia

Zgodnie z opisem w poniższych sekcjach, przekształcenia pliku konfiguracji można zrobić na dwa sposoby:

- Obejmują `app.config.transform` i `web.config.transform` plików do pakietu `content` folder, gdzie `.transform` rozszerzenie informuje NuGet, że te pliki zawierają XML do scalenia z istniejących plików konfiguracji, gdy pakiet jest zainstalowany. Po odinstalowaniu pakietu tego samego XML zostaną usunięte.
- (NuGet 2.6 lub nowszej) Obejmują `app.config.install.xdt` i `web.config.install.xdt` plików do pakietu `content` folderu, za pomocą [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx) do opisywania żądane zmiany. Po wybraniu tej opcji możesz również uwzględnić `.uninstall.xdt` plik, aby cofnąć zmiany, gdy pakiet zostanie usunięty z projektu.

> [!Note]
> Przekształcenia nie są stosowane do `.config` plików jako łącze w programie Visual Studio.

Zaletą używania XDT to, że zamiast po prostu scalanie dwa pliki statyczne, zawiera składnię do manipulowania struktury XML DOM przy użyciu element i atrybut dopasowania za pomocą pełną obsługę języka XPath. XDT można następnie dodać, zaktualizować, lub usuń elementy, umieść nowe elementy z określonej lokalizacji lub Zamień lub usuń elementy (łącznie z węzłami podrzędnymi). Dzięki temu prostego do utworzenia transformacji Odinstaluj, które Wycofaj wszystkie przekształcenia zrobić podczas instalacji pakietu aktualizacji.

### <a name="xml-transforms"></a>Transformacji XML

`app.config.transform` i `web.config.transform` w pakiecie `content` folder zawiera tylko elementy do scalenia istniejącego projektu `app.config` i `web.config` plików.

Na przykład załóżmy, że projekt zawiera początkowo następującą zawartość w `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

Aby dodać `MyNuModule` elementu `modules` sekcji podczas instalacji, Utwórz `web.config.transform` pliku do pakietu `content` folderu, który wygląda następująco:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

Po zainstalowaniu pakietu NuGet `web.config` będzie wyglądać następująco:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

Należy zauważyć, że nie Zastąp NuGet `modules` sekcji go po prostu połączone nowy wpis do niej przez dodanie tylko nowych elementów i atrybutów. NuGet nie zmieni się żadnych istniejących elementów lub atrybutów.

Po odinstalowaniu pakietu NuGet zbada `.transform` ponownie pliki i usuwanie elementów zawiera odpowiednie `.config` plików. Należy pamiętać, że ten proces nie wpłynie na wszystkie wiersze w `.config` pliku, który można modyfikować po zainstalowaniu pakietu.

Przykład szerszej [moduły rejestrowania błędów i programy obsługi dla platformy ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) pakiet dodaje wiele wpisów w `web.config`, które są ponownie usunięte po odinstalowaniu pakietu.

Do sprawdzenia jego `web.config.transform` plik, Pobierz pakiet ELMAH z powyższego łącza, zmień rozszerzenie pakietu z `.nupkg` do `.zip`, a następnie otwórz `content\web.config.transform` w tym pliku ZIP.

Aby zobaczyć efekt Instalowanie i odinstalowanie pakietu, należy utworzyć nowy projekt ASP.NET w programie Visual Studio (szablon podlega **Visual C# > sieci Web** w oknie dialogowym Nowy projekt) i wybierz opcję Pusta aplikacja platformy ASP.NET. Otwórz `web.config` aby zobaczyć stan początkowy. Kliknij prawym przyciskiem myszy projekt, wybierz **Zarządzaj pakietami NuGet**Przeglądaj w poszukiwaniu ELMAH na nuget.org i zainstaluj najnowszą wersję. Zwróć uwagę, wszystkie zmiany do `web.config`. Teraz odinstalować pakiet i zobaczysz `web.config` powrócić do poprzedniego stanu.

### <a name="xdt-transforms"></a>Przekształca XDT

2.6 NuGet i nowsze, można zmodyfikować plików konfiguracji przy użyciu [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx). Może także zawierać NuGet Zastąp tokeny z [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) przez dołączenie nazwy właściwości w `$` ograniczników (bez uwzględniania wielkości liter).

Na przykład następująca `app.config.install.xdt` pliku zostanie wstawiona `appSettings` element do `app.config` zawierający `FullPath`, `FileName`, i `ActiveConfigurationSettings` wartości z projektu:

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

Innym przykładem Załóżmy, że projekt zawiera początkowo następującą zawartość w `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
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
    <system.webServer>
</configuration>
```

Aby usunąć tylko `MyNuModule` elementu podczas odinstalowywania pakietu `web.config.uninstall.xdt` plik powinien zawierać następujące:

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
