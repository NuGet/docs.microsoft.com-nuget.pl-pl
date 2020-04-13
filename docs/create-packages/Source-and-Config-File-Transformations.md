---
title: Transformacje plików źródłowych i konfiguracyjnych dla pakietów NuGet
description: Szczegółowe informacje na temat możliwości pakietów NuGet do przekształcania plików kodu źródłowego i konfiguracji (XML) po zainstalowaniu.
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 2fefd9cff4d151111023521c31d58878743775bf
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231178"
---
# <a name="transforming-source-code-and-configuration-files"></a>Przekształcanie kodu źródłowego i plików konfiguracyjnych

**Transformacja kodu źródłowego** stosuje jednokierunkowe zastępowanie tokenów `contentFiles` do`content` plików `packages.config` w `contentFiles` `PackageReference`pakiecie `content` lub folderze (dla klientów korzystających i dla) po zainstalowaniu pakietu, gdzie tokeny odnoszą się do [właściwości projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)programu Visual Studio. Dzięki temu można wstawić plik do obszaru nazw projektu lub dostosować kod, `global.asax` który zazwyczaj wchodzi w ASP.NET projektu.

**Transformacja pliku konfiguracyjnego** umożliwia modyfikowanie plików, które `web.config` już `app.config`istnieją w projekcie docelowym, takich jak i . Na przykład pakiet może być konieczne dodanie `modules` elementu do sekcji w pliku konfiguracyjnym. Transformacja ta odbywa się poprzez dołączenie specjalnych plików w pakiecie, które opisują sekcje, aby dodać do plików konfiguracyjnych. Po odinstalowaniu pakietu te same zmiany są następnie odwracane, co czyni to transformacją dwukierunkową.

## <a name="specifying-source-code-transformations"></a>Określanie przekształceń kodu źródłowego

1. Pliki, które chcesz wstawić z pakietu do projektu, muszą `content` `contentFiles` znajdować się w folderach i folderach pakietu. Na przykład jeśli chcesz, `ContosoData.cs` aby plik wywoływany, który ma być zainstalowany w folderze `Models` projektu docelowego, musi znajdować się wewnątrz `content\Models` folderów i `contentFiles\{lang}\{tfm}\Models` w pakiecie.

1. Aby poinstruować NuGet, aby zastosować zastąpienie `.pp` tokenu w czasie instalacji, dołącz do nazwy pliku kodu źródłowego. Po instalacji plik nie `.pp` będzie miał rozszerzenia.

    Na przykład, aby dokonać `ContosoData.cs`przekształceń w `ContosoData.cs.pp`programie , nazwij plik w pakiecie . Po instalacji pojawi `ContosoData.cs`się jako .

1. W pliku kodu źródłowego użyj tokenów bez uwzględniania `$token$` wielkości liter formularza, aby wskazać wartości, które NuGet powinien zastąpić właściwościami projektu:

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

    Po instalacji NuGet `$rootnamespace$` `Fabrikam` zastępuje przy założeniu, że projekt `Fabrikam`docelowy, którego głównym obszarem nazw jest .

Token `$rootnamespace$` jest najczęściej używaną właściwością projektu; wszystkie pozostałe są wymienione we [właściwościach projektu](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Należy pamiętać, oczywiście, że niektóre właściwości mogą być specyficzne dla typu projektu.

## <a name="specifying-config-file-transformations"></a>Określanie przekształceń plików konfiguracyjnych

Zgodnie z opisem w kolejnych sekcjach przekształcenia plików konfiguracyjnych można wykonać na dwa sposoby:

- Dołącz `app.config.transform` `web.config.transform` i pliki w `content` folderze pakietu, gdzie `.transform` rozszerzenie mówi NuGet, że te pliki zawierają XML do scalenia z istniejącymi plikami konfiguracyjnymi po zainstalowaniu pakietu. Po odinstalowaniu pakietu ten sam kod XML jest usuwany.
- Dołącz `app.config.install.xdt` `web.config.install.xdt` i pliki w `content` folderze pakietu, używając [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx) do opisania żądanych zmian. Za pomocą tej opcji `.uninstall.xdt` można również dołączyć plik do odwrócenia zmian, gdy pakiet jest usuwany z projektu.

> [!Note]
> Przekształcenia nie są `.config` stosowane do plików, do których odwołuje się jako łącze w programie Visual Studio.

Zaletą korzystania z XDT jest to, że zamiast po prostu scalanie dwóch plików statycznych, zapewnia składnię do manipulowania strukturą XML DOM przy użyciu elementu i atrybutu dopasowania przy użyciu pełnej obsługi XPath. XDT można następnie dodać, zaktualizować lub usunąć elementy, umieścić nowe elementy w określonej lokalizacji lub zastąpić/usunąć elementy (w tym węzłów podrzędnych). To sprawia, że łatwo utworzyć odinstalować przekształca, że kopii zapasowej wszystkich przekształceń wykonanych podczas instalacji pakietu.

### <a name="xml-transforms"></a>Transformacje XML

I `app.config.transform` `web.config.transform` w `content` folderze pakietu zawierają tylko te elementy do scalenia w istniejących `app.config` i `web.config` plików projektu.

Na przykład załóżmy, że projekt `web.config`początkowo zawiera następującą zawartość w:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Aby dodać `MyNuModule` element `modules` do sekcji podczas instalowania `web.config.transform` `content` pakietu, utwórz plik w folderze pakietu, który wygląda następująco:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Po zainstalowaniu pakietu przez `web.config` NuGet pojawi się w następujący sposób:

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

Należy zauważyć, że NuGet `modules` nie zastąpił sekcji, po prostu scalone nowego wpisu do niego, dodając tylko nowe elementy i atrybuty. NuGet nie zmieni żadnych istniejących elementów lub atrybutów.

Po odinstalowaniu pakietu NuGet ponownie `.transform` zbada pliki i usunie `.config` elementy, które zawiera z odpowiednich plików. Należy zauważyć, że ten proces `.config` nie wpłynie na żadne wiersze w pliku, które można zmodyfikować po instalacji pakietu.

Jako bardziej obszerny przykład pakiet [Moduły rejestrowania błędów i programy obsługi ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) dodaje wiele wpisów do `web.config`programu , które są ponownie usuwane po odinstalowaniu pakietu.

Aby sprawdzić `web.config.transform` jego plik, pobierz pakiet ELMAH z powyższego `.nupkg` `.zip`łącza, zmień `content\web.config.transform` rozszerzenie pakietu z , a następnie otwórz w tym pliku ZIP.

Aby zobaczyć efekt instalacji i odinstalowywania pakietu, utwórz nowy projekt ASP.NET w programie Visual Studio (szablon znajduje się w obszarze **Visual C# > Web** w oknie dialogowym Nowy projekt) i wybierz pustą aplikację ASP.NET. Otwórz, `web.config` aby zobaczyć jego stan początkowy. Następnie kliknij prawym przyciskiem myszy projekt, wybierz pozycję **Zarządzaj pakietami NuGet**, wyszukaj elmah na nuget.org i zainstaluj najnowszą wersję. Zwróć uwagę na `web.config`wszystkie zmiany na . Teraz odinstaluj `web.config` pakiet i zobaczysz powrót do poprzedniego stanu.

### <a name="xdt-transforms"></a>Transformacje XDT

> [!Note]
> Jak wspomniano w [sekcji problemy ze zgodnością pakietu dokumentów `packages.config` do `PackageReference`migracji z do ](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), XDT przekształcenia, jak opisano poniżej są obsługiwane tylko przez `packages.config`. Jeśli dodasz poniższe pliki do pakietu, konsumenci `PackageReference` korzystający z pakietu z nie będą mieli zastosowanych przekształceń (patrz [ten przykład,](https://github.com/NuGet/Samples/tree/master/XDTransformExample) aby transformacje XDT działały).`PackageReference`

Pliki konfiguracyjne można modyfikować przy użyciu [składni XDT](https://msdn.microsoft.com/library/dd465326.aspx). Można również nuget zastąpić tokeny z [właściwości projektu,](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) `$` dołączając nazwę właściwości w ogranicznika (bez uwzględniania wielkości liter).

Na przykład następujący `app.config.install.xdt` plik wstawi `app.config` element `FullPath`zawierający `FileName` `appSettings` `ActiveConfigurationSettings` , i wartości z projektu:

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

Na inny przykład załóżmy, że `web.config`projekt początkowo zawiera następującą zawartość w:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Aby dodać `MyNuModule` element `modules` do sekcji podczas instalowania `web.config.install.xdt` pakietu, pakiet będzie zawierać następujące elementy:

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

Po zainstalowaniu `web.config` pakietu, będzie wyglądać następująco:

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

Aby usunąć `MyNuModule` tylko element podczas `web.config.uninstall.xdt` odinstalowywania pakietu, plik powinien zawierać następujące elementy:

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
