---
title: Odwołanie do pliku Project.JSON programu NuGet | Dokumentacja firmy Microsoft
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/27/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: W niektórych typów projektów project.json przechowuje listę pakiety NuGet służące do projektu.
keywords: Odwołania do pakietu NuGet, zależności NuGet, plikiem project.lock.json w pliku project.json NuGet
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 21542a219faa3d1fa0c32a838645d4471c5aa935
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/28/2018
---
# <a name="projectjson-reference"></a>Odwołanie do pliku Project.JSON

*NuGet 3.x+*

`project.json` Pliku przechowuje listę pakietów używane w projekcie, znane jako formatu pakietu zarządzania. Zastępuje ona `packages.config` , ale z kolei został zastąpiony przez [PackageReference](../consume-packages/package-references-in-project-files.md) nuget 4.0 +.

[ `project.lock.json` ](#projectlockjson) Pliku (opisanych poniżej) służy także projektów wykorzystujących `project.json`.

`project.json` ma następującą strukturę podstawowe, gdzie każdy z czterech obiektów najwyższego poziomu może mieć dowolną liczbę obiektów podrzędnych:

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

Zawiera listę zależności pakietu NuGet projektu w następującej postaci:

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

`dependencies` Sekcja jest, gdy okno dialogowe Menedżer pakietów NuGet dodaje zależności pakietów do projektu.

Identyfikator pakietu identyfikatorowi pakietu na nuget.org, taki sam jak identyfikator używany w konsoli Menedżera pakietów: `Install-Package Microsoft.NETCore`.

Podczas przywracania pakietów, ograniczenie wersji `"5.0.0"` oznacza `>= 5.0.0`. Oznacza to, że jeśli 5.0.0 nie jest dostępny na serwerze, ale jest 5.0.1, NuGet instaluje 5.0.1 i ostrzega użytkownika o uaktualnienie. NuGet, w przeciwnym razie wybiera Najniższa wersja możliwe na serwerze ograniczenie dopasowania.

Zobacz [rozpoznawania zależności](../consume-packages/dependency-resolution.md) uzyskać więcej informacji na temat reguł rozwiązywania.

### <a name="managing-dependency-assets"></a>Zarządzanie zasobami zależności

Które zasoby z zależnościami przepływać do projektu najwyższego poziomu jest kontrolowany przez podanie rozdzielana przecinkami zestawu tagów w `include` i `exclude` właściwości zależności odwołania. Tagi są wymienione w poniższej tabeli:

| Dołączania/wykluczania tag | Odpowiednie foldery elementu docelowego |
| --- | --- |
| Pliki | Zawartość  |
| środowisko uruchomieniowe | Środowisko uruchomieniowe, zasobów i FrameworkAssemblies  |
| Kompilacji | lib |
| kompilacja | Kompilacja (właściwości programu MSBuild i elementy docelowe) |
| natywne | natywne |
| brak | Brak folderów |
| wszystkie | Wszystkie foldery |

Określony za pomocą tagów `exclude` pierwszeństwo określony za pomocą `include`. Na przykład `include="runtime, compile" exclude="compile"` jest taka sama jak `include="runtime"`.

Na przykład, aby uwzględnić `build` i `native` foldery zależności, należy użyć następującego:

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

Aby wykluczyć `content` i `build` foldery zależności, należy użyć następującego:

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

Wyświetla listę platform, których projekt używa, takich jak `net45`, `netcoreapp`, `netstandard`.

```json
"frameworks": {
    "netcore50": {}
    }
 ```

Tylko jeden wpis jest dozwolony w `frameworks` sekcji. (Wyjątkiem jest `project.json` pliki projektów ASP.NET, które są kompilowane z DNX przestarzałe narzędzie łańcucha, co umożliwia obsługę wielu elementów docelowych.)

## <a name="runtimes"></a>środowisk uruchomieniowych

Zawiera listę systemów operacyjnych i architektur, których aplikacja będzie działać, takich jak `win10-arm`, `win8-x64`, `win8-x86`.

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

Pakiet zawierający PCL, która może działać na dowolnym środowiska uruchomieniowego nie trzeba określić środowisko uruchomieniowe. Musi to być także spełnione wszystkie zależności, w przeciwnym razie należy określić środowisk uruchomieniowych.


## <a name="supports"></a>Obsługuje

Definiuje zestaw sprawdza, czy zależności pakietów. Można określić, którego można spodziewać się PCL lub uruchamiania aplikacji. Definicje nie są restrykcyjne kodu mogą być w stanie do uruchamiania innych miejscach. Ale określenie kontrole powoduje, że NuGet, sprawdź, czy wszystkie zależności na liście TxMs. Przykładowe wartości tej sytuacji należą: `net46.app`, `uwp.10.0.app`itp.

W tej sekcji powinny zostać wypełnione automatycznie po wybraniu pozycji w oknie dialogowym elementy docelowe przenośnej biblioteki klas.

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a>Importy

Importy pozwalają pakiety, które używają `dotnet` TxM do pracy z pakietami, które nie deklaruje dotnet TxM. Jeśli w twoim projekcie są używani `dotnet` TxM, a następnie wszystkie pakiety zależą od musi mieć również `dotnet` TxM, chyba że Dodaj następujący kod do Twojej `project.json` umożliwia z systemem innym niż `dotnet` platformy, aby był zgodny z `dotnet`:

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

Jeśli używasz `dotnet` TxM następnie system projektu PCL dodaje odpowiednie `imports` instrukcji na podstawie obsługiwanych celów.

## <a name="differences-from-portable-apps-and-web-projects"></a>Różnice z przenośnym aplikacji i projekty sieci web

`project.json` Plik używany przez narzędzie NuGet jest podzbiorem wykryte w projektach platformy ASP.NET Core. W przypadku platformy ASP.NET Core `project.json` służy do metadanych projektu, informacje o kompilacji i zależności. Gdy są używane w innych systemach projektu, te trzy elementy są podzielone na osobne pliki i `project.json` zawiera mniej informacji. Istotnych różnic obejmują:

- Może istnieć tylko jeden framework w `frameworks` sekcji.

- Plik nie może zawierać zależności, opcje kompilacji, itp., który pojawi się w DNX `project.json` plików. Biorąc pod uwagę, że może istnieć tylko jeden framework go nie ma sensu wprowadzenia zależności określonej struktury.

- Kompilacja jest obsługiwany przez MSBuild tak definiuje opcje kompilacji preprocesora, itp. to części pliku projektu MSBuild i nie `project.json`.

W NuGet 3 + deweloperzy najprawdopodobniej nie ręcznie edytować `project.json`, ponieważ zawartość manipuluje interfejsu użytkownika Menedżera pakietów w programie Visual Studio. Inaczej mówiąc, na pewno można edytować plik, ale musisz go skompilować projekt, aby uruchomić Przywracanie pakietu lub wywołanie przywracania w inny sposób. Zobacz [Przywracanie pakietu](../consume-packages/package-restore.md).


## <a name="projectlockjson"></a>project.lock.json

`project.lock.json` Plik został wygenerowany w trakcie przywracania pakietów NuGet w projektach, które używają `project.json`. Przechowuje migawkę wszystkie informacje, które są generowane zgodnie z NuGet przedstawia wykres pakietów i zawiera wersję, zawartość i zależności wszystkich pakietów w projekcie. System kompilacji używa go do wybierz pakiety z globalnej lokalizacji, które mają zastosowanie podczas kompilowania projektu zamiast w zależności od folderem lokalnym pakietów w samym projekcie. Powoduje to zwiększyć wydajność kompilacji, ponieważ jest tylko do odczytu `project.lock.json` zamiast wielu oddzielnych `.nuspec` plików.

`project.lock.json` jest generowana automatycznie na Przywracanie pakietu, dlatego można je pominąć z kontroli źródła, dodając go do `.gitignore` i `.tfignore` plików (zobacz [pakietów i kontroli źródła](../consume-packages/packages-and-source-control.md). Jednak jeśli uwzględniony w kontroli źródła, historii zmian przedstawia zmiany w zależnościach rozwiązał w czasie.
