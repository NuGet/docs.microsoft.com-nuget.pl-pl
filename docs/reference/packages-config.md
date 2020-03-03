---
title: Dokumentacja pliku Packages. config pakietów NuGet
description: W niektórych typach projektów Packages. config obsługuje listę pakietów NuGet używanych w projekcie.
author: karann-msft
ms.author: karann
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 3665989d35d7362b30a106cf6b4ed0210619efee
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230582"
---
# <a name="packagesconfig-reference"></a>Dokumentacja Packages. config

Plik `packages.config` jest używany w niektórych typach projektów do obsługi listy pakietów, do których odwołuje się projekt. Dzięki temu NuGet może łatwo przywrócić zależności projektu, gdy projekt ma być transportowany do innego komputera, na przykład na serwerze kompilacji, bez wszystkich pakietów.

Jeśli jest używany, `packages.config` zwykle znajduje się w katalogu głównym projektu. Jest ona tworzona automatycznie podczas uruchamiania pierwszej operacji NuGet, ale można ją również utworzyć ręcznie przed uruchomieniem jakichkolwiek poleceń, takich jak `nuget restore`.

Projekty używające [PackageReference](../consume-packages/Package-References-in-Project-Files.md) nie używają `packages.config`.

## <a name="schema"></a>Schemat

Schemat jest prosty: poniżej standardowego nagłówka XML jest pojedynczy węzeł `<packages>`, który zawiera co najmniej jeden element `<package>`, jeden dla każdego odwołania. Każdy element `<package>` może mieć następujące atrybuty:

| Atrybut | Wymagany | Opis |
| --- | --- | --- |
| id | Yes | Identyfikator pakietu, taki jak Newtonsoft. JSON lub Microsoft. AspNet. MVC. | 
| version | Yes | Dokładna wersja pakietu do zainstalowania, taka jak 3.1.1 lub 4.2.5.11-beta. Ciąg wersji musi zawierać co najmniej trzy cyfry; czwarta jest opcjonalna, ponieważ jest sufiksem w wersji wstępnej. Zakresy są niedozwolone. | 
| targetFramework | Nie | [Moniker platformy docelowej (TFM)](target-frameworks.md) , który ma zostać zastosowany podczas instalowania pakietu. Jest to początkowo ustawione na obiekt docelowy projektu po zainstalowaniu pakietu. W efekcie różne elementy `<package>` mogą mieć różne TFMs. Na przykład jeśli tworzysz projekt przeznaczony dla platformy .NET 4.5.2, pakiety zainstalowane w tym punkcie będą korzystały z TFM net452. Jeśli użytkownik; później przekieruje projekt do programu .NET 4,6 i doda więcej pakietów, będzie używać TFM z net46. Niezgodność między atrybutami docelowymi projektu a `targetFramework` będzie generować ostrzeżenia, w takim przypadku można ponownie zainstalować pakiety, których to dotyczy. | 
| allowedVersions | Nie | Zakres dozwolonych wersji tego pakietu stosowany podczas aktualizacji pakietu (zobacz ograniczenia dotyczące [wersji uaktualnienia](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). *Nie ma to wpływu na* pakiet instalowany podczas operacji instalowania lub przywracania. Aby poznać składnię, zobacz [wersja pakietu](../concepts/package-versioning.md#version-ranges) . Interfejs użytkownika pakietu Packagemanager wyłącza również wszystkie wersje poza dozwolonym zakresem. | 
| DevelopmentDependency | Nie | Jeśli sam projekt będzie tworzył pakiet NuGet, ustawienie tej opcji na `true` dla zależności uniemożliwia uwzględnienie tego pakietu podczas tworzenia pakietu. Wartość domyślna to `false`. | 

## <a name="examples"></a>Przykłady

Następujące `packages.config` odnoszą się do dwóch zależności:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Następujące `packages.config` odnoszą się do dziewięciu pakietów, ale `Microsoft.Net.Compilers` nie będzie uwzględniane podczas kompilowania pakietu zużywanego z powodu atrybutu `developmentDependency`. Odwołanie do Newtonsoft. JSON również ogranicza aktualizacje tylko do wersji 8. x i 9. x.

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
