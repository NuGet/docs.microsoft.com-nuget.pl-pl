---
title: project.jsodwołania do pliku dla pakietu NuGet
description: W przypadku niektórych typów projektów project.jsna zachowuje listę pakietów NuGet używanych w projekcie.
author: JonDouglas
ms.author: jodou
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 6665f4f3e688cb4a3989216c8c8f1a8655b61ed8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775197"
---
# <a name="projectjson-reference"></a>project.jsna temat odwołania

*Pakiet NuGet 3. x +*

`project.json`Plik zachowuje listę pakietów używanych w projekcie, nazywanych formatem zarządzania pakietami. Jest on zastępowany `packages.config` , ale jest zastępowany przez [PackageReference](../consume-packages/package-references-in-project-files.md) z pakietem NuGet 4.0 +.

[`project.lock.json`](#projectlockjson)Plik (opisany poniżej) jest również używany w projektach korzystających z programu `project.json` .

`project.json` ma następującą strukturę podstawową, w której każdy z czterech obiektów najwyższego poziomu może mieć dowolną liczbę obiektów podrzędnych:

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a>Zależności

Wyświetla listę zależności pakietu NuGet projektu w następującej postaci:

```json
"PackageID" : "version_constraint"
```

Na przykład:

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

`dependencies`Sekcja jest miejscem, w którym okno dialogowe Menedżera pakietów NuGet dodaje zależności pakietu do projektu.

Identyfikator pakietu odpowiada identyfikatorowi pakietu w nuget.org, tak samo jak identyfikator używany w konsoli Menedżera pakietów: `Install-Package Microsoft.NETCore` .

Gdy przywracane są pakiety, ograniczenie wersji `"5.0.0"` wskazuje `>= 5.0.0` . Oznacza to, że jeśli 5.0.0 nie jest dostępny na serwerze, ale 5.0.1 to, pakiet NuGet instaluje 5.0.1 i ostrzega o uaktualnieniu. W przeciwnym razie program NuGet wybiera najmniejszą możliwą wersję na serwerze pasującym do ograniczenia.

Zobacz [rozpoznawanie zależności](../concepts/dependency-resolution.md) , aby uzyskać więcej informacji o regułach rozpoznawania.

### <a name="managing-dependency-assets"></a>Zarządzanie zasobami zależności

Które zasoby z zależności są przepływem do projektu najwyższego poziomu, są kontrolowane przez określenie zestawu tagów rozdzielanych przecinkami we `include` `exclude` właściwościach i odwołania do zależności. Tagi są wymienione w poniższej tabeli:

| Include/Exclude — tag | Zmodyfikowane foldery elementu docelowego |
| --- | --- |
| contentFiles | Zawartość  |
| środowisko uruchomieniowe | Środowisko uruchomieniowe, zasoby i FrameworkAssemblies  |
| kompilowanie | lib |
| kompilacja | Kompilacja (właściwości i elementy docelowe programu MSBuild) |
| natywne | natywne |
| brak | Brak folderów |
| all | Wszystkie foldery |

Tagi określone za pomocą `exclude` mają pierwszeństwo przed tymi określonymi przy użyciu `include` . Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"` .

Na przykład, aby uwzględnić `build` foldery i `native` zależności, użyj następujących elementów:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

Aby wykluczyć `content` foldery i `build` zależności, użyj następujących elementów:

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a>Struktury

Wyświetla listę struktur, na których działa projekt, na przykład, `net45` `netcoreapp` , `netstandard` .

```json
"frameworks": {
    "netcore50": {}
    }
 ```

W sekcji dozwolony jest tylko pojedynczy wpis `frameworks` . (Wyjątek to `project.json` pliki dla projektów ASP.NET, które są kompilowane z nieprawidłowym łańcuchem narzędzi środowiska DNX, który pozwala na wiele elementów docelowych).

## <a name="runtimes"></a>Runtime

Wyświetla listę systemów operacyjnych i architektur, na których działa aplikacja, na przykład, `win10-arm` `win8-x64` `win8-x86` .

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

Pakiet zawierający PCL, który można uruchomić w dowolnym środowisku uruchomieniowym, nie musi określać środowiska uruchomieniowego. Musi on również mieć wartość true dla wszystkich zależności, w przeciwnym razie należy określić środowiska uruchomieniowe.


## <a name="supports"></a>Obsługuje

Definiuje zestaw kontroli zależności pakietów. Możesz określić, gdzie ma zostać uruchomione PCL lub aplikacja. Definicje nie są restrykcyjne, ponieważ kod może być uruchomiony w innym miejscu. Jednak określenie tych testów powoduje sprawdzenie, czy wszystkie zależności są spełnione na liście TxMs. Przykłady wartości dla tego elementu to: `net46.app` , `uwp.10.0.app` itp.

Ta sekcja powinna być wypełniana automatycznie po wybraniu wpisu w oknie dialogowym elementy docelowe biblioteki klas przenośnych.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Importowania

Importy zostały zaprojektowane tak, aby zezwalały na pakiety, które używają `dotnet` TxM, do działania z pakietami, które nie deklarują TxM dotnet. Jeśli projekt używa `dotnet` TxM, wszystkie pakiety, od których zależy, muszą mieć również `dotnet` TxM, o ile nie zostanie dodany następujący element do programu, `project.json` Aby zezwolić na `dotnet` niezgodność platform z `dotnet` :

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Jeśli używasz `dotnet` TxM, system projektu PCL dodaje odpowiednią `imports` instrukcję na podstawie obsługiwanych elementów docelowych.

## <a name="differences-from-portable-apps-and-web-projects"></a>Różnice między aplikacjami przenośnymi i projektami sieci Web

`project.json`Plik używany przez program NuGet jest podzbiorem znalezionym w projektach ASP.NET Core. W ASP.NET Core `project.json` jest używany dla metadanych projektu, informacji o kompilacji i zależności. W przypadku użycia w innych systemach projektów te trzy elementy są podzielone na osobne pliki i `project.json` zawierają mniej informacji. Istotne różnice obejmują:

- W sekcji może istnieć tylko jedna struktura `frameworks` .

- Plik nie może zawierać zależności, opcji kompilacji itp., które są widoczne w `project.json` plikach środowiska DNX. Uwzględniając, że może istnieć tylko jedna struktura, nie ma sensu, aby wprowadzać zależności specyficzne dla struktury.

- Kompilacja jest obsługiwana przez program MSBuild, więc opcje kompilacji, Definicje preprocesora itp. są wszystkie częścią pliku projektu programu MSBuild `project.json` .

W programie NuGet 3 + deweloperzy nie mogą ręcznie edytować programu `project.json` , ponieważ interfejs użytkownika Menedżera pakietów w programie Visual Studio manipuluje zawartością. Tym samym, można wyedytować plik, ale należy skompilować projekt, aby uruchomić pakiet przywracania lub wywołać przywracanie w inny sposób. Zobacz [przywracanie pakietu](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>project.lock.jsna

`project.lock.json`Plik jest generowany w procesie przywracania pakietów NuGet w projektach, które używają `project.json` . Zawiera migawkę wszystkich informacji, które są generowane jako pakiet NuGet, prowadzi do grafu pakietów i zawiera wersję, zawartość i zależności wszystkich pakietów w projekcie. System kompilacji używa tego do wybrania pakietów z globalnej lokalizacji, która jest istotna podczas kompilowania projektu, a nie w zależności od lokalnego folderu pakietów w samym projekcie. Powoduje to szybszą wydajność kompilacji, ponieważ jest konieczna tylko do odczytu, `project.lock.json` a nie wielu oddzielnych `.nuspec` plików.

`project.lock.json` jest generowany automatycznie podczas przywracania pakietu, więc można go pominąć z kontroli źródła przez dodanie go do `.gitignore` i `.tfignore` plików (zobacz [pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md). Jednakże jeśli zostanie uwzględniony w kontroli źródła, historia zmian pokazuje zmiany w zależnościach rozwiązanych w czasie.
