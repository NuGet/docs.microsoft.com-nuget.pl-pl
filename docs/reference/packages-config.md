---
title: Odwołanie do pliku packages.config NuGet
description: W niektórych typach projektów packages.config przechowuje listę pakietów NuGet, używany w projekcie.
author: karann-msft
ms.author: karann
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 18566671b611899b28fcc8542cf53935f5ee2dfd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551773"
---
# <a name="packagesconfig-reference"></a>Odwołanie do pliku Packages.config

`packages.config` Plik jest używany w niektórych typach projektów do przechowywania listy pakietów przywoływanego przez projekt. Dzięki temu NuGet można łatwo przywrócić zależności projektu podczas projektu do innej maszynie, na przykład na serwerze kompilacji, bez tych pakietów.

Jeśli używane, `packages.config` znajduje się w katalogu głównym projektu. Została ona utworzona automatycznie, gdy pierwszą operacją NuGet jest uruchamiany, ale można również utworzyć ręcznie przed uruchomieniem dowolnych poleceń, takich jak `nuget restore`.

Projekty używające [PackageReference](../consume-packages/Package-References-in-Project-Files.md) nie należy używać `packages.config`.

## <a name="schema"></a>Schemat

Schemat jest prosty: następujące standardowy nagłówek XML jest pojedynczym `<packages>` węzeł, który zawiera co najmniej jeden `<package>` elementy, po jednym dla każdego odwołania. Każdy `<package>` element może mieć następujące atrybuty:

| Atrybut | Wymagane | Opis |
| --- | --- | --- |
| identyfikator | Tak | Identyfikator pakietu, takich jak pakiet Newtonsoft.json lub Microsoft.AspNet.Mvc. | 
| version | Tak | Dokładną wersję pakietu do zainstalowania, takich jak 3.1.1 lub 4.2.5.11-beta. Ciąg wersji musi mieć co najmniej trzy cyfry; czwarty jest opcjonalny, ponieważ sufiks wersji wstępnej. Zakresy są niedozwolone. | 
| targetFramework | Nie | [Docelowe moniker struktury (TFM)](target-frameworks.md) do zastosowania podczas instalowania pakietu. To jest ustawiany na obiekcie docelowym projektu po zainstalowaniu pakietu. W wyniku innego `<package>` elementy mogą mieć różne krótkich nazw. Na przykład jeśli tworzysz projekt przeznaczony dla .NET 4.5.2, pakietów zainstalowanych w tym momencie użyje elementu TFM z net452. Jeśli użytkownik; później rzekieruj projekt .NET 4.6 i dodawanie dodatkowych pakietów, użyje tych TFM net46. Niezgodność obiektu docelowego projektu i `targetFramework` atrybutami spowoduje wygenerowanie ostrzeżenia, w tym przypadku można ponownie zainstalować pakiety, których to dotyczy. | 
| allowedVersions | Nie | Zakres dozwolonych wersji tego pakietu, stosowane podczas aktualizacji pakietu (zobacz [wersji uaktualnienie Constraining](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Robi *nie* wpływają na jakie pakiet jest zainstalowany podczas instalacji lub operacji przywracania. Zobacz [przechowywanie wersji pakietów](../reference/package-versioning.md#version-ranges-and-wildcards) składni. Interfejs użytkownika PackageManager wyłącza również wszystkie wersje poza dozwolonym zakresem. | 
| DevelopmentDependency | Nie | W przypadku używania sam projekt tworzy pakiet NuGet, ustawienie tej opcji na `true` dla zależności zapobiega włączaniu po utworzeniu pakietu konsumencki tego pakietu. Wartość domyślna to `false`. | 

## <a name="examples"></a>Przykłady

Następujące `packages.config` odwołuje się do dwie zależności:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Następujące `packages.config` odwołuje się do dziewięć pakietów, ale `Microsoft.Net.Compilers` nie zostaną uwzględnione podczas tworzenia pakietu korzystanie z powodu `developmentDependency` atrybutu. Odwołanie do pakietu Newtonsoft.Json ogranicza również aktualizacje tylko 8.x i 9.x wersji.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
