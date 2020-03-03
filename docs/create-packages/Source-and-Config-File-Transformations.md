---
title: Przekształcenia plików źródłowych i konfiguracji dla pakietów NuGet
description: Szczegółowe informacje o możliwości pakietów NuGet do przekształcania plików kodu źródłowego i konfiguracji (XML) po zainstalowaniu programu.
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 2fefd9cff4d151111023521c31d58878743775bf
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231178"
---
# <a name="transforming-source-code-and-configuration-files"></a>Przekształcanie kodu źródłowego i plików konfiguracji

**Przekształcenie kodu źródłowego** stosuje jednokierunkową wymianę tokenów w plikach w `content` lub `contentFiles` folderu (`content` dla klientów korzystających z `packages.config` i `contentFiles` dla `PackageReference`) podczas instalowania pakietu, gdzie tokeny odwołują się do [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)programu Visual Studio. Dzięki temu można wstawić plik do przestrzeni nazw projektu lub dostosować kod, który zwykle przejdzie do `global.asax` w projekcie ASP.NET.

**Przekształcenie pliku konfiguracji** pozwala modyfikować pliki, które już istnieją w projekcie docelowym, takie jak `web.config` i `app.config`. Na przykład może być konieczne dodanie elementu do sekcji `modules` w pliku konfiguracyjnym. Ta transformacja jest wykonywana przez dodanie plików specjalnych w pakiecie, które opisują sekcje dodawane do plików konfiguracji. Po odinstalowaniu pakietu te same zmiany są odwracane, co sprawia, że jest to dwukierunkowa transformacja.

## <a name="specifying-source-code-transformations"></a>Określanie przekształceń kodu źródłowego

1. Pliki, które mają zostać wstawione z pakietu do projektu, muszą znajdować się w folderach `content` i `contentFiles` pakietu. Na przykład, jeśli plik o nazwie `ContosoData.cs` ma być zainstalowany w folderze `Models` projektu docelowego, musi znajdować się wewnątrz folderów `content\Models` i `contentFiles\{lang}\{tfm}\Models` w pakiecie.

1. Aby polecić pakietowi NuGet zastosowanie zastąpienia tokenu podczas instalacji, należy dołączyć `.pp` do nazwy pliku kodu źródłowego. Po instalacji plik nie będzie miał rozszerzenia `.pp`.

    Na przykład aby wykonać przekształcenia w `ContosoData.cs`, Nazwij plik w `ContosoData.cs.pp`pakietu. Po zakończeniu instalacji zostanie wyświetlona jako `ContosoData.cs`.

1. W pliku kodu źródłowego Użyj tokenów bez uwzględniania wielkości liter w formularzu `$token$`, aby wskazać wartości, które NuGet powinny zastąpić właściwości projektu:

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

    Podczas instalacji pakiet NuGet zastępuje `$rootnamespace$` z `Fabrikam` przy założeniu, że docelowy obszar nazw jest `Fabrikam`.

Token `$rootnamespace$` jest najczęściej używaną właściwością projektu; wszystkie inne są wyświetlane we [właściwościach projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Oczywiście należy mieć na uwadze, że niektóre właściwości mogą być specyficzne dla typu projektu.

## <a name="specifying-config-file-transformations"></a>Określanie przekształceń pliku konfiguracji

Zgodnie z opisem w poniższych sekcjach przekształcenia plików konfiguracji można wykonać na dwa sposoby:

- Dołącz pliki `app.config.transform` i `web.config.transform` do folderu `content` pakietu, gdzie rozszerzenie `.transform` informuje program NuGet, że te pliki zawierają kod XML do scalenia z istniejącymi plikami konfiguracji podczas instalowania pakietu. Po odinstalowaniu pakietu ten sam plik XML jest usuwany.
- Uwzględnij pliki `app.config.install.xdt` i `web.config.install.xdt` w folderze `content` pakietu, używając [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx) do opisania żądanych zmian. Za pomocą tej opcji można również dołączyć plik `.uninstall.xdt`, aby cofnąć zmiany po usunięciu pakietu z projektu.

> [!Note]
> Przekształcenia nie są stosowane do `.config` plików, do których odwołuje się łącze w programie Visual Studio.

Zaletą korzystania z XDT jest to, że zamiast bezpośredniego scalania dwóch plików statycznych, zapewnia ona składnię do manipulowania strukturą kodu XML, przy użyciu elementów i atrybutów dopasowywania za pomocą pełnej obsługi XPath. XDT może następnie dodawać, aktualizować lub usuwać elementy, umieszczać nowe elementy w określonej lokalizacji lub zastępować/usuwać elementy (w tym węzłów podrzędnych). Pozwala to na bezpośrednie utworzenie transformacji, które wycofa wszystkie przekształcenia wykonywane podczas instalacji pakietu.

### <a name="xml-transforms"></a>Przekształcenia XML

`app.config.transform` i `web.config.transform` w folderze `content` pakietu zawierają tylko te elementy, które mają być scalane do istniejących plików `app.config` i `web.config` projektu.

Załóżmy na przykład, że projekt początkowo zawiera następującą zawartość w `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Aby dodać `MyNuModule` element do sekcji `modules` podczas instalowania pakietu, Utwórz plik `web.config.transform` w folderze `content` pakietu, który wygląda następująco:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Po zainstalowaniu pakietu NuGet pakiet `web.config` będzie wyglądać w następujący sposób:

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

Zwróć uwagę, że plik NuGet nie zastąpił sekcji `modules`, po prostu scalał do niego nowy wpis poprzez dodanie tylko nowych elementów i atrybutów. Pakiet NuGet nie zmieni żadnych istniejących elementów ani atrybutów.

Po odinstalowaniu pakietu NuGet ponownie sprawdzi `.transform` pliki i usunie zawarte w nim elementy z odpowiednich `.config` plików. Należy zauważyć, że ten proces nie wpłynie na żadne wiersze w `.config` pliku modyfikowanym po zainstalowaniu pakietu.

W szerszym przykładzie [moduły rejestrowania błędów modułów i programów obsługi dla pakietu ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) dodają wiele wpisów do `web.config`, które są ponownie usuwane po odinstalowaniu pakietu.

Aby przejrzeć plik `web.config.transform`, Pobierz pakiet ELMAH z powyższego linku, Zmień rozszerzenie pakietu z `.nupkg` na `.zip`, a następnie otwórz `content\web.config.transform` w tym pliku ZIP.

Aby zobaczyć efekt instalacji i dezinstalacji pakietu, Utwórz nowy projekt ASP.NET w programie Visual Studio (szablon jest w obszarze  **C# Visual > Web** w oknie dialogowym Nowy projekt) i wybierz Pustą aplikację ASP.NET. Otwórz `web.config`, aby zobaczyć jego stan początkowy. Następnie kliknij prawym przyciskiem myszy projekt, wybierz pozycję **Zarządzaj pakietami NuGet**, Wyszukaj pozycję ELMAH w witrynie NuGet.org i zainstaluj najnowszą wersję. Zwróć uwagę na wszystkie zmiany `web.config`. Teraz Odinstaluj pakiet i zobaczysz, że `web.config` powrócić do poprzedniego stanu.

### <a name="xdt-transforms"></a>Przekształcenia XDT

> [!Note]
> Jak wspomniano w [sekcji problemy ze zgodnością pakietu w dokumentacji dotyczącej migrowania z `packages.config` do `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), przekształcenia XDT zgodnie z poniższym opisem są obsługiwane tylko przez `packages.config`. Jeśli dodasz poniższe pliki do pakietu, użytkownicy korzystający z pakietu z `PackageReference` nie będą mieć zastosowanych przekształceń (zobacz [ten przykład](https://github.com/NuGet/Samples/tree/master/XDTransformExample) , aby XDT transformacje pracy z`PackageReference`).

Pliki konfiguracji można modyfikować przy użyciu [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx). Możesz również mieć tokeny zamieniania NuGet na [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) , dołączając nazwę właściwości w ramach ograniczników `$` (bez uwzględniania wielkości liter).

Na przykład następujący plik `app.config.install.xdt` spowoduje wstawienie elementu `appSettings` do `app.config` zawierającego wartości `FullPath`, `FileName`i `ActiveConfigurationSettings` z projektu:

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

W innym przykładzie Załóżmy, że projekt początkowo zawiera następującą zawartość w `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Aby dodać `MyNuModule` element do sekcji `modules` podczas instalowania pakietu, `web.config.install.xdt` pakietu będzie zawierać następujące elementy:

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

Po zainstalowaniu pakietu `web.config` będzie wyglądać następująco:

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

Aby usunąć tylko `MyNuModule` element podczas odinstalowywania pakietu, plik `web.config.uninstall.xdt` powinien zawierać następujące elementy:

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
