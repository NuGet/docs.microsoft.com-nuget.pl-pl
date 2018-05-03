---
title: Odwołanie do pliku packages.config NuGet
description: W niektórych typów projektów packages.config przechowuje listę pakiety NuGet służące do projektu.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 73234f79cb9eb30327c4e206a5bc51c5bc1c6f1d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/26/2018
---
# <a name="packagesconfig-reference"></a>Odwołanie do pliku Packages.config

`packages.config` Plik jest używany w niektórych typów projektów w celu zachowania listy pakietów odwołuje się projekt. Dzięki temu NuGet łatwo przywrócić zależności projektu podczas projektu do innej maszynie, na przykład serwer kompilacji bez tych pakietów.

## <a name="schema"></a>Schemat

Schemat jest prosty: następujące standardowy nagłówek XML jest jeden `<packages>` węzła, który zawiera co najmniej jeden `<package>` elementy, dla każdego odwołania. Każdy `<package>` element może mieć następujące atrybuty:

| Atrybut | Wymagane | Opis |
| --- | --- | --- |
| identyfikator | Tak | Identyfikator pakietu, takich jak Newtonsoft.json lub Microsoft.AspNet.Mvc. | 
| version | Tak | Dokładną wersję pakietu do zainstalowania, takich jak 3.1.1 lub 4.2.5.11-beta. Ciąg wersji musi mieć co najmniej trzech cyfr; czwarty jest opcjonalne, jak jest sufiksem wersji wstępnej. Zakresy są niedozwolone. | 
| targetFramework | Nie | [Target framework moniker (TFM)](target-frameworks.md) do zastosowania podczas instalowania pakietu. To jest ustawiany do projektu docelowego podczas instalowania pakietu. Dzięki temu różnych `<package>` elementy mogą mieć różne TFMs. Na przykład jeśli tworzysz projekt przeznaczony dla platformy .NET w wersji 4.5.2 pakiety zainstalowane w tym momencie użyje TFM z net452. Jeśli użytkownik; później Przekieruj projektu 4.6 .NET i dodać więcej pakietów użyje tych TFM net46. Niezgodność między docelowym projektu i `targetFramework` atrybutami spowoduje wygenerowanie ostrzeżenia, w tym przypadku można ponownie zainstalować odpowiednich pakietów. | 
| allowedVersions | Nie | Dla zakresu dozwolonych wersji tego pakietu zastosowane podczas aktualizacji pakietu (zobacz [wersji uaktualnienie Constraining](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). Robi *nie* wpływają na jakie pakietu jest instalowana podczas instalacji lub operację przywracania. Zobacz [wersji pakietu](../reference/package-versioning.md#version-ranges-and-wildcards) składni. Interfejs użytkownika PackageManager dodatkowo wyłącza wszystkie wersje poza dozwolonym zakresem. | 
| DevelopmentDependency | Nie | Jeśli korzystanie z projektu sam tworzy pakietu NuGet, ustawienie to `true` dla zależności uniemożliwia dołączanie po utworzeniu pakietu odbierającą tego pakietu. Wartość domyślna to `false`. | 

## <a name="examples"></a>Przykłady

Następujące `packages.config` odwołuje się do dwóch zależności:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Następujące `packages.config` odwołuje się do pakietów dziewięć, ale `Microsoft.Net.Compilers` nie zostanie uwzględniony podczas tworzenia pakietu korzystanie z powodu `developmentDependency` atrybutu. Odwołanie do Newtonsoft.Json ogranicza również aktualizacji do wersji 8.x i 9.x tylko.

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
