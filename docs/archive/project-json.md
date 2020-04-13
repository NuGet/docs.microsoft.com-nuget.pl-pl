---
title: project.json— numer pliku dla usługi NuGet
description: W niektórych typach projektów project.json przechowuje listę pakietów NuGet używanych w projekcie.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 5ecbcd4855de8ea7b6301a5e307779216baf96fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488282"
---
# <a name="projectjson-reference"></a>odwołanie do pliku project.json

*NuGet 3.x+*

Plik `project.json` przechowuje listę pakietów używanych w projekcie, znany jako format zarządzania pakietami. Zastępuje, `packages.config` ale z kolei zastępuje [packagereference](../consume-packages/package-references-in-project-files.md) z NuGet 4.0 +.

Plik [`project.lock.json`](#projectlockjson) (opisany poniżej) jest również używany `project.json`w projektach zatrudniających .

`project.json`ma następującą podstawową strukturę, w której każdy z czterech obiektów najwyższego poziomu może mieć dowolną liczbę obiektów podrzędnych:

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

Wyświetla listę zależności pakietu NuGet projektu w następującej formie:

```json
"PackageID" : "version_constraint"
```

Przykład:

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

Sekcja `dependencies` jest, gdzie NuGet Package Manager okno dialogowe dodaje zależności pakietów do projektu.

Identyfikator pakietu odpowiada identyfikatorowi pakietu na nuget.org , tak samo jak identyfikator używany w konsoli menedżera `Install-Package Microsoft.NETCore`pakietów: .

Podczas przywracania pakietów ograniczenie `"5.0.0"` wersji `>= 5.0.0`implikuje . Oznacza to, że jeśli 5.0.0 nie jest dostępny na serwerze, ale 5.0.1 jest, NuGet instaluje 5.0.1 i ostrzega o uaktualnieniu. NuGet w przeciwnym razie wybiera najniższą możliwą wersję na serwerze pasujące do ograniczenia.

Zobacz [rozpoznawanie zależności, aby](../concepts/dependency-resolution.md) uzyskać więcej informacji na temat reguł rozwiązywania problemów.

### <a name="managing-dependency-assets"></a>Zarządzanie zasobami zależności

Które zasoby z zależności przepływu do projektu najwyższego poziomu jest kontrolowana przez określenie rozdzielanych przecinkami zestaw tagów w `include` i `exclude` właściwości odwołania zależności. Tagi są wymienione w poniższej tabeli:

| Tag Dołącz/Wyklucz | Foldery docelowe, których dotyczy problem, |
| --- | --- |
| contentFiles | Zawartość  |
| środowisko uruchomieniowe | Środowisko wykonawcze, zasoby i asemblies framework  |
| kompilowanie | Lib |
| kompilacja | build (REKWIZYTY i obiekty docelowe MSBuild) |
| natywne | natywne |
| brak | Brak folderów |
| all | Wszystkie foldery |

Znaczniki określone `exclude` z pierwszeństwem nad `include`tymi określonymi za pomocą . Na przykład `include="runtime, compile" exclude="compile"` jest taka `include="runtime"`sama jak .

Na przykład, aby `build` `native` uwzględnić i foldery zależności, należy użyć następujących czynności:

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

Aby wykluczyć `content` `build` i foldery zależności, należy użyć następujących czynności:

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

Wyświetla listę struktur, na których działa `net45` `netcoreapp`projekt, takich jak , , `netstandard`.

```json
"frameworks": {
    "netcore50": {}
    }
 ```

W `frameworks` sekcji dozwolony jest tylko jeden wpis. (Wyjątkiem są `project.json` pliki dla ASP.NET projektów, które są budowane z przestarzałym łańcuchem narzędzi DNX, co pozwala na wiele obiektów docelowych).

## <a name="runtimes"></a>Środowiska wykonawcze

Wyświetla listę systemów operacyjnych i architektur, na `win10-arm` `win8-x64`których `win8-x86`działa aplikacja, takich jak , .

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

Pakiet zawierający PCL, który można uruchomić w dowolnym czasie wykonywania nie trzeba określać środowiska wykonawczego. Musi to być również prawdziwe wszelkie zależności, w przeciwnym razie należy określić środowiska wykonawcze.


## <a name="supports"></a>Obsługuje

Definiuje zestaw kontroli zależności pakietu. Można zdefiniować, gdzie można oczekiwać PCL lub aplikacji do uruchomienia. Definicje nie są restrykcyjne, ponieważ kod może być w stanie uruchomić w innym miejscu. Jednak określenie tych kontroli sprawia, że NuGet sprawdza, czy wszystkie zależności są spełnione na wymienionych TxM. Przykłady wartości dla tego `net46.app`są: , `uwp.10.0.app`, itp.

Ta sekcja powinna być wypełniana automatycznie po wybraniu wpisu w oknie dialogowym Docelowe biblioteki klas przenośnych.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Przywozu

Importy są przeznaczone do zezwalania pakietom, które używają `dotnet` TxM do pracy z pakietami, które nie deklarują dotnet TxM. Jeśli projekt korzysta `dotnet` z TxM, wszystkie pakiety, od `dotnet` których jesteś zależny, muszą `project.json` mieć również `dotnet` TxM, `dotnet`chyba że dodasz do niego następujące elementy, aby umożliwić zgodność innych platform z:

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Jeśli używasz `dotnet` TxM następnie system projektu PCL `imports` dodaje odpowiednią instrukcję na podstawie obsługiwanych obiektów docelowych.

## <a name="differences-from-portable-apps-and-web-projects"></a>Różnice w stosunku do aplikacji przenośnych i projektów internetowych

Plik `project.json` używany przez NuGet jest podzbiorem, który znajduje się w ASP.NET podstawowych projektów. W ASP.NET Core `project.json` jest używany dla metadanych projektu, informacji kompilacji i zależności. Te trzy elementy są używane w innych systemach `project.json` projektu i zawierają mniej informacji. Znaczące różnice obejmują:

- W `frameworks` sekcji może istnieć tylko jedna struktura.

- Plik nie może zawierać zależności, opcji kompilacji itp., `project.json` które są widoczne w plikach DNX. Biorąc pod uwagę, że może istnieć tylko pojedyncza struktura nie ma sensu, aby wprowadzić zależności specyficzne dla struktury.

- Kompilacja jest obsługiwana przez MSBuild więc opcje kompilacji, definicje preprocesora itp. `project.json`

W NuGet 3+, deweloperzy nie oczekuje `project.json`się ręcznie edytować , jak interfejs użytkownika Menedżera pakietów w programie Visual Studio manipuluje zawartością. To powiedzia się, z pewnością można edytować plik, ale należy utworzyć projekt, aby rozpocząć przywracanie pakietu lub wywołać przywracanie w inny sposób. Zobacz [Przywracanie pakietu](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>projekt.lock.json

Plik `project.lock.json` jest generowany w procesie przywracania pakietów NuGet `project.json`w projektach, które używają . Posiada migawkę wszystkich informacji, które są generowane jako NuGet spacery wykres pakietów i zawiera wersję, zawartość i zależności wszystkich pakietów w projekcie. System kompilacji używa tego, aby wybrać pakiety z lokalizacji globalnej, które są istotne podczas tworzenia projektu, a nie w zależności od folderu pakietów lokalnych w samym projekcie. Powoduje to szybszą wydajność kompilacji, ponieważ `project.lock.json` jest to `.nuspec` konieczne do odczytu tylko zamiast wielu oddzielnych plików.

`project.lock.json`jest generowany automatycznie przy przywracanie pakietu, więc można go pominąć w kontroli źródła, dodając go do `.gitignore` i `.tfignore` plików (zobacz [Pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md). Jednak jeśli uwzględnisz go w kontroli źródła, historia zmian pokazuje zmiany zależności rozwiązane w czasie.
