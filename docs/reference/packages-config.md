---
title: Dokumentacja pliku packages.config NuGet
description: W przypadku niektórych typów projektów packages.config obsługuje listę pakietów NuGet używanych w projekcie.
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: da682197d4a156f9dff8ce169aab449a5392ef41
ms.sourcegitcommit: c19d398cecee3cad2d79a8b22650fc1988d41a3f
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 02/02/2021
ms.locfileid: "99260306"
---
# <a name="packagesconfig-reference"></a>Informacje packages.config

Ten `packages.config` plik jest używany w niektórych typach projektów do obsługi listy pakietów, do których odwołuje się projekt. Dzięki temu NuGet może łatwo przywrócić zależności projektu, gdy projekt ma być transportowany do innego komputera, na przykład na serwerze kompilacji, bez wszystkich pakietów.

Jeśli jest używany, `packages.config` zazwyczaj znajduje się w katalogu głównym projektu. Jest ona tworzona automatycznie podczas uruchamiania pierwszej operacji NuGet, ale można ją również utworzyć ręcznie przed uruchomieniem jakichkolwiek poleceń, takich jak `nuget restore` .

Projekty używające [PackageReference](../consume-packages/Package-References-in-Project-Files.md) nie są używane `packages.config` .

## <a name="schema"></a>Schemat

Schemat jest prosty: poniżej standardowego nagłówka XML jest pojedynczy `<packages>` węzeł, który zawiera jeden lub więcej `<package>` elementów, po jednym dla każdego odwołania. Każdy `<package>` element może mieć następujące atrybuty:

| Atrybut | Wymagane | Opis |
| --- | --- | --- |
| identyfikator | Tak | Identyfikator pakietu, taki jak Newtonsoft.json lub Microsoft. AspNet. MVC. | 
| Wersja | Tak | Dokładna wersja pakietu do zainstalowania, taka jak 3.1.1 lub 4.2.5.11-beta. Ciąg wersji musi zawierać co najmniej trzy cyfry; czwarta jest opcjonalna, ponieważ jest sufiksem w wersji wstępnej. Zakresy są niedozwolone. | 
| targetFramework | Nie | [Moniker platformy docelowej (TFM)](target-frameworks.md) , który ma zostać zastosowany podczas instalowania pakietu. Jest to początkowo ustawione na obiekt docelowy projektu po zainstalowaniu pakietu. W efekcie różne `<package>` elementy mogą mieć różne TFMs. Na przykład jeśli tworzysz projekt przeznaczony dla platformy .NET 4.5.2, pakiety zainstalowane w tym punkcie będą korzystały z TFM net452. Jeśli użytkownik; później przekieruje projekt do programu .NET 4,6 i doda więcej pakietów, będzie używać TFM z net46. Niezgodność między obiektem docelowym projektu a `targetFramework` atrybutami spowoduje wygenerowanie ostrzeżeń, w takim przypadku można ponownie zainstalować odpowiednie pakiety. | 
| allowedVersions | Nie | Zakres dozwolonych wersji tego pakietu stosowany podczas aktualizacji pakietu (zobacz ograniczenia dotyczące [wersji uaktualnienia](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions). *Nie ma to wpływu na* pakiet instalowany podczas operacji instalowania lub przywracania. Aby poznać składnię, zobacz [wersja pakietu](../concepts/package-versioning.md#version-ranges) . Interfejs użytkownika pakietu Packagemanager wyłącza również wszystkie wersje poza dozwolonym zakresem. | 
| developmentDependency | Nie | Jeśli sam projekt tworzy pakiet NuGet, ustawienie tej opcji na `true` dla zależności uniemożliwia uwzględnienie tego pakietu podczas tworzenia pakietu. Wartość domyślna to `false`. | 

## <a name="examples"></a>Przykłady

Następujące `packages.config` odnoszą się do dwóch zależności:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Poniższe elementy `packages.config` odnoszą się do dziewięciu pakietów, ale `Microsoft.Net.Compilers` nie zostaną uwzględnione podczas kompilowania pakietu zużywanego z powodu `developmentDependency` atrybutu. Odwołanie do Newtonsoft.Json również ogranicza aktualizacje tylko do wersji 8. x i 9. x.

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
