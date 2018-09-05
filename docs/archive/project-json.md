---
title: Odwołanie do pliku Project.JSON do NuGet
description: W niektórych typach projektów project.json przechowuje listę pakietów NuGet, używany w projekcie.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: e4d8b5b9ab4605516827ead8939f278d110c7a48
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547787"
---
# <a name="projectjson-reference"></a>Odwołanie do pliku Project.JSON

*NuGet 3.x+*

`project.json` Pliku prowadzi listę pakietów używanych w projekcie, znane jako format pakietu zarządzania. Zastępuje ona `packages.config` , ale są kolejno zastępowane [PackageReference](../consume-packages/package-references-in-project-files.md) nuget 4.0 +.

[ `project.lock.json` ](#projectlockjson) Pliku (opisanych poniżej) jest również używane w projektach wykorzystujących `project.json`.

`project.json` ma podstawowe następującą strukturę, w którym każdy z czterech obiektów najwyższego poziomu może mieć dowolną liczbę obiektów podrzędnych:

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

Zawiera listę zależności pakietów NuGet projektu w następującej postaci:

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

`dependencies` Sekcja jest, gdy okno Menedżera pakietów NuGet dodaje zależności pakietów do projektu.

Identyfikator pakietu odnosi się do identyfikatora pakietu w witrynie nuget.org, taki sam jak identyfikator używany w konsoli Menedżera pakietów: `Install-Package Microsoft.NETCore`.

Podczas przywracania pakietów, ograniczenie wersji `"5.0.0"` oznacza `>= 5.0.0`. Oznacza to jeśli 5.0.0 nie jest dostępny na serwerze, ale jest 5.0.1, NuGet instaluje 5.0.1 i ostrzega o uaktualnieniu. NuGet, w przeciwnym razie wybiera najniższa możliwa wersja na serwerze, pasujących do ograniczenia.

Zobacz [rozpoznawania zależności](../consume-packages/dependency-resolution.md) więcej informacji na temat reguł rozwiązywania.

### <a name="managing-dependency-assets"></a>Zarządzanie zasobami zależności

Które zasoby z zależnościami przepływać do najwyższego poziomu projektu jest kontrolowany przez określenie zestawu rozdzielonych przecinkami tagów w `include` i `exclude` właściwości odwołania zależności. Tagi są wymienione w poniższej tabeli:

| Uwzględnianie/wykluczanie znaczników | Odpowiednie foldery elementu docelowego |
| --- | --- |
| Pliki | Zawartość  |
| środowisko uruchomieniowe | Środowisko uruchomieniowe, zasobów i FrameworkAssemblies  |
| Kompilacji | lib |
| kompilacja | Kompilacja (cele i właściwości programu MSBuild) |
| natywne | natywne |
| brak | Brak folderów |
| wszystkie | Wszystkie foldery |

Określony za pomocą tagów `exclude` pierwszeństwo określony za pomocą `include`. Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"`.

Na przykład w celu uwzględnienia `build` i `native` folderów zależność, należy użyć następującego:

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

Aby wykluczyć `content` i `build` folderów zależność, należy użyć następującego:

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

Wyświetla listę struktur, w których działa projektu, taki jak `net45`, `netcoreapp`, `netstandard`.

```json
"frameworks": {
    "netcore50": {}
    }
 ```

Tylko pojedynczy wpis jest dozwolona w `frameworks` sekcji. (Wyjątek stanowi `project.json` plików dla projektów programu ASP.NET, które są kompilowane przy użyciu środowiska DNX przestarzałe narzędzie łańcucha, który pozwala na wiele obiektów docelowych.)

## <a name="runtimes"></a>środowiska uruchomieniowe

Zawiera listę systemów operacyjnych i architektur, które aplikacja działa w systemie, takie jak `win10-arm`, `win8-x64`, `win8-x86`.

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

Pakiet zawierający wersję PCL, która może działać na dowolnym środowiska uruchomieniowego nie należy określić środowisko uruchomieniowe. Musi to być również wartość true, wszystkie zależności, w przeciwnym razie należy określić środowisk uruchomieniowych.


## <a name="supports"></a>Obsługuje

Definiuje zestaw sprawdza, czy zależności pakietów. Można zdefiniować, którego można spodziewać się PCL lub aplikacja była uruchomiona. Definicje są restrykcyjna, jak Twój kod może być mogą być uruchamiane w innym miejscu. Ale określenie tych sprawdzeń sprawia, że NuGet, sprawdź, czy wszystkie zależności na liście TxMs. Przykładowe wartości do tego są: `net46.app`, `uwp.10.0.app`itp.

W tej sekcji powinno zostać automatycznie wypełnione, po wybraniu wpisu w oknie dialogowym cele Portable Class Library.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Importy

Importy pozwalają pakiety, które używają `dotnet` TxM do pracy z pakietami, które nie deklarują dotnet TxM. Jeśli w twoim projekcie są używani `dotnet` TxM, a następnie wszystkich pakietów, na których polegasz musi również mieć `dotnet` TxM, chyba że dodasz następujące polecenie, aby Twoje `project.json` umożliwia bez `dotnet` platform, aby był zgodny z `dotnet`:

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Jeśli używasz `dotnet` TxM następnie system projektu PCL dodaje odpowiednie `imports` oświadczenie na podstawie obsługiwanych celów.

## <a name="differences-from-portable-apps-and-web-projects"></a>Różnice z przenośnym aplikacje oraz projekty sieci web

`project.json` Plik używany przez NuGet jest podzbiorem wykrytym w projektach ASP.NET Core. W programie ASP.NET Core `project.json` służy do metadanych projektu, informacje o kompilacji i zależności. Gdy jest używana w innych systemach projektu, te trzy elementy są podzielone na osobne pliki i `project.json` zawiera mniej informacji. Istotne różnice obejmują:

- Może istnieć tylko jeden struktura w systemie `frameworks` sekcji.

- Plik nie może zawierać zależności, opcji kompilacji, itp., widoczny w środowiska DNX `project.json` plików. Biorąc pod uwagę, że może istnieć tylko jedną strukturę nie ma sensu wprowadzenia zależności określonej platformy.

- Kompilacja jest obsługiwany przez program MSBuild, więc definiuje opcje kompilacji preprocesora, itp. są częścią pliku projektu MSBuild i nie `project.json`.

W pakiecie NuGet 3 +, deweloperzy najprawdopodobniej nie ręcznie edytować `project.json`, ponieważ interfejs użytkownika Menedżera pakietów w programie Visual Studio obsługuje zawartość. Inaczej mówiąc, plik pewno można edytować, ale należy utworzyć projekt, aby rozpocząć przywracanie pakietu lub wywołaj przywracania w inny sposób. Zobacz [Przywracanie pakietu](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>project.lock.json

`project.lock.json` Plik jest generowany w trakcie przywracania pakietów NuGet w projektach korzystających z `project.json`. Przechowuje migawki wszystkie informacje, które są generowane zgodnie z narzędzi przedstawia wykres pakietów NuGet i zawiera wersję, zawartość i zależności dla wszystkich pakietów w projekcie. System kompilacji używa tej wartości do wyboru pakietów globalnej lokalizacji, które mają zastosowanie podczas kompilowania projektu, a nie w zależności od folderem lokalnym pakietów w samym projekcie. Skutkuje to zwiększyć wydajność kompilacji ponieważ tylko do odczytu `project.lock.json` zamiast wiele oddzielnych `.nuspec` plików.

`project.lock.json` jest generowany automatycznie na Przywracanie pakietu, dzięki czemu może być pominięty z kontroli źródła, dodając ją do `.gitignore` i `.tfignore` plików (zobacz [pakiety i kontrola źródła](../consume-packages/packages-and-source-control.md). Jednak jeśli uwzględniony w kontroli źródła, historię zmian przedstawia zmiany w zależnościach rozwiązane wraz z upływem czasu.
