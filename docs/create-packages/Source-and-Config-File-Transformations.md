---
title: Przekształcenia plików źródłowych i konfiguracji dla pakietów NuGet
description: Szczegółowe informacje o możliwości pakietów NuGet do przekształcania plików kodu źródłowego i konfiguracji (XML) po zainstalowaniu programu.
author: JonDouglas
ms.author: jodou
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 5bd0e409f527fb668008204fb16ad002f4784c46
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774580"
---
# <a name="transforming-source-code-and-configuration-files"></a>Przekształcanie kodu źródłowego i plików konfiguracji

**Przekształcenie kodu źródłowego** stosuje jednokierunkowe zastępowanie tokenów do plików w pakiecie `content` lub `contentFiles` folderze ( `content` dla klientów korzystających z programu `packages.config` i `contentFiles` dla programu `PackageReference` ) podczas instalowania pakietu, gdzie tokeny odwołują się do [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)programu Visual Studio. Dzięki temu można wstawić plik do przestrzeni nazw projektu lub dostosować kod, który zwykle `global.asax` znajduje się w projekcie ASP.NET.

**Przekształcanie plików konfiguracji** umożliwia modyfikowanie plików, które już istnieją w projekcie docelowym, takich jak `web.config` i `app.config` . Na przykład pakiet może wymagać dodania elementu do `modules` sekcji w pliku konfiguracji. Ta transformacja jest wykonywana przez dodanie plików specjalnych w pakiecie, które opisują sekcje dodawane do plików konfiguracji. Po odinstalowaniu pakietu te same zmiany są odwracane, co sprawia, że jest to dwukierunkowa transformacja.

## <a name="specifying-source-code-transformations"></a>Określanie przekształceń kodu źródłowego

1. Pliki, które mają zostać wstawione z pakietu do projektu, muszą znajdować się w obrębie pakietu `content` i `contentFiles` folderów. Na przykład jeśli plik ma `ContosoData.cs` być zainstalowany w `Models` folderze docelowego projektu, musi znajdować się wewnątrz `content\Models` `contentFiles\{lang}\{tfm}\Models` folderów i w pakiecie.

1. Aby polecić pakietowi NuGet zastosowanie zastąpienia tokenu podczas instalacji, Dołącz `.pp` do nazwy pliku kodu źródłowego. Po instalacji plik nie będzie miał `.pp` rozszerzenia.

    Na przykład aby wykonać przekształcenia w `ContosoData.cs` , Nazwij plik w pakiecie `ContosoData.cs.pp` . Po zakończeniu instalacji zostanie wyświetlona jako `ContosoData.cs` .

1. W pliku kodu źródłowego Użyj tokenów bez uwzględniania wielkości liter w formularzu, `$token$` Aby wskazać wartości, które NuGet powinny zastąpić właściwości projektu:

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

    Podczas instalacji pakiet NuGet zastępuje `$rootnamespace$` przy `Fabrikam` założeniu, że docelowy obszar nazw jest docelowym projektem `Fabrikam` .

`$rootnamespace$`Token jest najczęściej używaną właściwością projektu; wszystkie inne są wyświetlane we [właściwościach projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Oczywiście należy mieć na uwadze, że niektóre właściwości mogą być specyficzne dla typu projektu.

## <a name="specifying-config-file-transformations"></a>Określanie przekształceń pliku konfiguracji

Zgodnie z opisem w poniższych sekcjach przekształcenia plików konfiguracji można wykonać na dwa sposoby:

- Dołącz `app.config.transform` do `web.config.transform` folderu pakietu i plików `content` , w którym `.transform` rozszerzenie informuje program NuGet, że te pliki zawierają kod XML do scalenia z istniejącymi plikami konfiguracji podczas instalowania pakietu. Po odinstalowaniu pakietu ten sam plik XML jest usuwany.
- Dołącz `app.config.install.xdt` `web.config.install.xdt` do folderu pakietu i pliki `content` , używając [składni XDT](/previous-versions/aspnet/dd465326(v=vs.110)) do opisania żądanych zmian. Za pomocą tej opcji można również dołączyć `.uninstall.xdt` plik do odwrócenia zmian, gdy pakiet zostanie usunięty z projektu.

> [!Note]
> Przekształcenia nie są stosowane do `.config` plików, do których odwołuje się jako link w programie Visual Studio.

Zaletą korzystania z XDT jest to, że zamiast bezpośredniego scalania dwóch plików statycznych, zapewnia ona składnię do manipulowania strukturą kodu XML, przy użyciu elementów i atrybutów dopasowywania za pomocą pełnej obsługi XPath. XDT może następnie dodawać, aktualizować lub usuwać elementy, umieszczać nowe elementy w określonej lokalizacji lub zastępować/usuwać elementy (w tym węzłów podrzędnych). Pozwala to na bezpośrednie utworzenie transformacji, które wycofa wszystkie przekształcenia wykonywane podczas instalacji pakietu.

### <a name="xml-transforms"></a>Przekształcenia XML

`app.config.transform`I `web.config.transform` w `content` folderze pakietu zawierają tylko te elementy, które mają być scalane do istniejących `app.config` i plików projektu `web.config` .

Załóżmy na przykład, że projekt początkowo zawiera następującą zawartość w `web.config` :

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Aby dodać `MyNuModule` element do `modules` sekcji podczas instalacji pakietu, Utwórz `web.config.transform` plik w folderze pakietu, `content` który wygląda następująco:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Po zainstalowaniu pakietu NuGet program `web.config` będzie wyglądać w następujący sposób:

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

Zwróć uwagę, że program NuGet nie zamienił `modules` sekcji, po prostu scalał do niego nowy wpis poprzez dodanie tylko nowych elementów i atrybutów. Pakiet NuGet nie zmieni żadnych istniejących elementów ani atrybutów.

Po odinstalowaniu pakietu NuGet `.transform` ponownie sprawdzi pliki i usunie zawarte w nim elementy z odpowiednich `.config` plików. Należy zauważyć, że ten proces nie wpłynie na żadne wiersze w `.config` pliku modyfikowanym po zainstalowaniu pakietu.

W szerszym przykładzie [moduły rejestrowania błędów modułów i programów obsługi dla pakietu ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) dodają wiele wpisów do `web.config` , które są ponownie usuwane po odinstalowaniu pakietu.

Aby przejrzeć swój `web.config.transform` plik, Pobierz pakiet ELMAH z powyższego linku, Zmień rozszerzenie pakietu z `.nupkg` na `.zip` , a następnie otwórz `content\web.config.transform` w tym pliku zip.

Aby zobaczyć efekt instalacji i dezinstalacji pakietu, Utwórz nowy projekt ASP.NET w programie Visual Studio (szablon jest w obszarze **Visual C# > Web** w oknie dialogowym Nowy projekt) i wybierz Pustą aplikację ASP.NET. Otwórz `web.config` , aby zobaczyć jego stan początkowy. Następnie kliknij prawym przyciskiem myszy projekt, wybierz pozycję **Zarządzaj pakietami NuGet**, Wyszukaj pozycję ELMAH w witrynie NuGet.org i zainstaluj najnowszą wersję. Zwróć uwagę na wszystkie zmiany `web.config` . Teraz Odinstaluj pakiet i zobaczysz `web.config` Powrót do poprzedniego stanu.

### <a name="xdt-transforms"></a>Przekształcenia XDT

> [!Note]
> Jak wspomniano w [sekcji problemy ze zgodnością pakietu w dokumentacji dotyczącej migracji z `packages.config` programu do `PackageReference` ](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), przekształceń XDT zgodnie z poniższym opisem są obsługiwane tylko przez program `packages.config` . Jeśli dodasz poniższe pliki do pakietu, użytkownicy korzystający z pakietu `PackageReference` nie będą mieć zastosowanych transformacji (zobacz [ten przykład](https://github.com/NuGet/Samples/tree/master/XDTransformExample) , aby XDT transformacje z programem `PackageReference` ).

Pliki konfiguracji można modyfikować przy użyciu [składni XDT](/previous-versions/aspnet/dd465326(v=vs.110)). Możesz również mieć tokeny zamieniania NuGet na [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) , dołączając nazwę właściwości w `$` ogranicznikach (bez uwzględniania wielkości liter).

Na przykład następujący `app.config.install.xdt` plik spowoduje wstawienie `appSettings` elementu do `app.config` zawierającego `FullPath` `FileName` wartości,, i `ActiveConfigurationSettings` z projektu:

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

W innym przykładzie Załóżmy, że projekt początkowo zawiera następującą zawartość w `web.config` :

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Aby dodać `MyNuModule` element do `modules` sekcji podczas instalacji pakietu, pakiet `web.config.install.xdt` powinien zawierać następujące elementy:

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

Po zainstalowaniu pakietu program `web.config` będzie wyglądać następująco:

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

Aby usunąć tylko `MyNuModule` element podczas odinstalowywania pakietu, `web.config.uninstall.xdt` plik powinien zawierać następujące elementy:

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